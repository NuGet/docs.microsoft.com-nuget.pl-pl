---
title: Tworzenie pakietu NuGet przy użyciu programu MSBuild
description: Szczegółowy przewodnik po procesie projektowania i tworzenia pakietu NuGet, w tym kluczowych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231321"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Tworzenie pakietu NuGet przy użyciu programu MSBuild

Podczas tworzenia pakietu NuGet z kodu, pakiet tej funkcji do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów. W tym artykule opisano sposób tworzenia pakietu przy użyciu msbuild. MSBuild jest preinstalowany z każdym obciążeniem programu Visual Studio, które zawiera NuGet. Dodatkowo można również użyć MSBuild za pośrednictwem dotnet CLI z [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).

W przypadku projektów .NET Core i .NET Standard, które używają [formatu w stylu zestawu SDK,](../resources/check-project-format.md)oraz innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do utworzenia pakietu.  W przypadku projektu w stylu nieskładu SDK, który używa, `<PackageReference>`NuGet używa również pliku projektu do utworzenia pakietu.

Projekty w stylu zestawu SDK mają domyślnie dostępną funkcję pakietu. W przypadku projektów packagereference w stylu nieskładek zestawu SDK należy dodać pakiet NuGet.Build.Tasks.Pack do zależności projektu. Aby uzyskać szczegółowe informacje na temat obiektów docelowych pakietu MSBuild, zobacz [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).

Polecenie, które tworzy `msbuild -t:pack`pakiet, jest funkcją równoważną `dotnet pack`.

> [!IMPORTANT]
> W tym temacie stosuje się do projektów [w stylu zestawu SDK,](../resources/check-project-format.md) zazwyczaj .NET Core i .NET Standard projektów i projektów w stylu innych niż SDK, które używają PackageReference.

## <a name="set-properties"></a>Ustawianie właściwości

Następujące właściwości są wymagane do utworzenia pakietu.

- `PackageId`, identyfikator pakietu, który musi być unikatowy w galerii, która obsługuje pakiet. Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.
- `Version`, określony numer wersji w postaci *Major.Minor.Patch[-Suffix],* gdzie *-Suffix* identyfikuje [wersje przedpremierowe](prerelease-packages.md). Jeśli nie zostanie określona, wartość domyślna to 1.0.0.
- Tytuł pakietu, który powinien pojawić się na hoście (np. nuget.org)
- `Authors`, informacje o autorze i właścicielu. Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.
- `Company`, nazwę firmy. Jeśli nie zostanie określona, wartością domyślną jest `AssemblyName`.

Ponadto w przypadku pakowania projektów w stylu innych niż SDK, które używają PackageReference, wymagane jest:

- `PackageOutputPath`, folder wyjściowy pakietu wygenerowanego podczas wywoływania pakietu.

W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksploratorze **rozwiązań,** wybierz polecenie Właściwości i wybierz kartę **Pakiet).** Można również ustawić te właściwości bezpośrednio w plikach projektu (*.csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Nadaj pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od źródła pakietu, którego używasz.

W poniższym przykładzie przedstawiono prosty, kompletny plik projektu z tymi właściwościami.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Można również ustawić właściwości opcjonalne, `Title` `PackageDescription`takie `PackageTags`jak , i , zgodnie z opisem w [msbuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym znaleźć pakiet i zrozumieć, co robi.

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [Odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md) i przechowywanie wersji [pakietu](../concepts/package-versioning.md). Jest również możliwe do powierzchni zasobów z zależności bezpośrednio w `<IncludeAssets>` `<ExcludeAssets>` pakiecie przy użyciu i atrybuty. Aby uzyskać więcej informacji, zobacz [Kontrolowanie zasobów zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Dodawanie opcjonalnego pola opisu

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Wybierz unikatowy identyfikator pakietu i ustaw numer wersji

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Dodaj pakiet NuGet.Build.Tasks.Pack

Jeśli używasz MSBuild z projektu w stylu nie w stylu SDK i PackageReference, dodaj pakiet NuGet.Build.Tasks.Pack do projektu.

1. Otwórz plik projektu i dodaj `<PropertyGroup>` następujące elementy po elemencie:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Otwórz wiersz polecenia Deweloper (w polu **Wyszukiwania** wpisz **wiersz polecenia Deweloper**).

   Zazwyczaj chcesz uruchomić wiersz polecenia dewelopera dla programu Visual Studio z menu **Start,** ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla usługi MSBuild.

3. Przełącz się do folderu zawierającego plik projektu i wpisz następujące polecenie, aby zainstalować pakiet NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Upewnij się, że dane wyjściowe MSBuild wskazuje, że kompilacja została pomyślnie ukończona.

## <a name="run-the-msbuild--tpack-command"></a>Uruchom polecenie msbuild -t:pack

Aby utworzyć pakiet NuGet `.nupkg` (plik) z projektu, uruchom `msbuild -t:pack` polecenie, które również automatycznie tworzy projekt:

W wierszu polecenia Deweloper dla programu Visual Studio wpisz następujące polecenie:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

Dane wyjściowe pokazuje `.nupkg` ścieżkę do pliku.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Automatyczne generowanie pakietu na kompilacji

Aby automatycznie `msbuild -t:pack` uruchamiać projekt podczas tworzenia lub przywracania projektu, `<PropertyGroup>`dodaj następujący wiersz do pliku projektu w obrębie:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Po uruchomieniu `msbuild -t:pack` rozwiązania, to pakuje wszystkie projekty w rozwiązaniu,[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) które są `true`spakowane (właściwość jest ustawiona na ).

> [!NOTE]
> Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji dla projektu.

### <a name="test-package-installation"></a>Instalacja pakietu testowego

Przed opublikowaniem pakietu zazwyczaj chcesz przetestować proces instalowania pakietu w projekcie. Testy upewnij się, że wszystkie pliki koniecznie kończy się w ich odpowiednich miejscach w projekcie.

Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia, wykonując [normalne kroki instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Pakiety są niezmienne. Jeśli rozwiążesz problem, zmień zawartość pakietu i zapakuj ponownie, podczas ponownego testowania nadal będziesz używać starej wersji pakietu, dopóki nie [wyczyścisz folderu pakietów globalnych.](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) Jest to szczególnie istotne podczas testowania pakietów, które nie używają unikatowej etykiety wstępnej wersji w każdej kompilacji.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w [polu Publikowanie pakietu.](../nuget-org/publish-a-package.md)

Można również rozszerzyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze, jak opisano w następujących tematach:

- [NuGet pack and restore as MSBuild targets NuGet pack and restore as MSBuild targets NuGet pack and restore as MSBuild targets NuGet](../reference/msbuild-targets.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przekształcenia plików źródłowych i konfiguracyjnych](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje w wersji wstępnej](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów z zestawami współdziałań COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Na koniec istnieją dodatkowe typy pakietów, o których należy pamiętać:

- [Pakiety natywne](../guides/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
