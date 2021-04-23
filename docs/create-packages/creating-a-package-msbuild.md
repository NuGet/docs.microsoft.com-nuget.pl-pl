---
title: Tworzenie pakietu NuGet przy użyciu programu MSBuild
description: Szczegółowy przewodnik po procesie projektowania i tworzenia pakietu NuGet przy użyciu programu MSBuild, w tym kluczowe punkty decyzyjne, takie jak pliki i wersje.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 18e0da335f65fde99d035388b95f35160757ee84
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901463"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Tworzenie pakietu NuGet przy użyciu programu MSBuild

Tworząc pakiet NuGet z kodu, możesz spakować tę funkcję do składnika, który może być współużytkowane i używane przez dowolną liczbę innych deweloperów. W tym artykule opisano sposób tworzenia pakietu przy użyciu programu MSBuild. Usługa MSBuild jest wstępnie zainstalowana z każdym Visual Studio, które zawiera nuGet. Ponadto można również używać programu MSBuild za pośrednictwem interfejsu wiersza polecenia dotnet z [programem dotnet msbuild.](/dotnet/core/tools/dotnet-msbuild)

W przypadku projektów .NET Core i .NET Standard, które używają formatu w stylu zestawu SDK, i innych projektów w stylu zestawu [SDK,](../resources/check-project-format.md)pakiet NuGet używa informacji w pliku projektu bezpośrednio do utworzenia pakietu.  W przypadku projektu bez zestawu SDK, który używa narzędzia , program NuGet używa również pliku projektu do `<PackageReference>` utworzenia pakietu.

Projekty w stylu zestawu SDK mają domyślnie dostępną funkcjonalność pakietu. W przypadku projektów nie stylu zestawu SDK PackageReference należy dodać pakiet NuGet.Build.Tasks.Pack do zależności projektu. Aby uzyskać szczegółowe informacje na temat obiektów docelowych pakietu MSBuild, zobacz [Temat NuGet pack and restore as MSBuild targets (Pakiet NuGet](../reference/msbuild-targets.md)i przywracanie jako obiekty docelowe msBuild).

Polecenie , które tworzy pakiet `msbuild -t:pack` , jest funkcjonalnością równoważną funkcji `dotnet pack` .

> [!IMPORTANT]
> Ten temat dotyczy projektów w stylu [zestawu SDK,](../resources/check-project-format.md) zazwyczaj projektów .NET Core i .NET Standard, oraz projektów innych niż w stylu zestawu SDK, które używają funkcji PackageReference.

## <a name="set-properties"></a>Ustawianie właściwości

Następujące właściwości są wymagane do utworzenia pakietu.

- `PackageId`, identyfikator pakietu, który musi być unikatowy w galerii, która hostuje pakiet. Jeśli nie zostanie określona, wartość domyślna to `AssemblyName` .
- `Version`, określony numer wersji w postaci *Główna.Pomocnicza.Poprawka[-Sufiks],* gdzie *-Sufiks* identyfikuje [wersje wstępne](prerelease-packages.md). Jeśli nie zostanie określony, wartość domyślna to 1.0.0.
- Tytuł pakietu powinien być wyświetlany na hoście (na przykład nuget.org)
- `Authors`, informacje o autorze i właścicielu. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName` .
- `Company`, nazwa firmy. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName` .

Ponadto w przypadku pakowania projektów innych niż w stylu zestawu SDK, które korzystają z funkcji PackageReference, wymagane są następujące elementy:

- `PackageOutputPath`, folder wyjściowy pakietu wygenerowanego podczas wywoływania pakietu.

W Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w oknie Eksplorator rozwiązań, wybierz pozycję Właściwości **i** wybierz **kartę** Pakiet. Te właściwości można również ustawić bezpośrednio w plikach projektu *(csproj).*

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Nadaj pakietowi identyfikator unikatowy dla nuget.org dowolnego źródła pakietu, z których korzystasz.

W poniższym przykładzie pokazano prosty, kompletny plik projektu z tymi właściwościami.

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

Można również ustawić opcjonalne właściwości, takie jak , i , zgodnie z opisem w tece Obiekty docelowe pakietu MSBuild, Kontrolowanie zasobów zależności i właściwości `Title` `PackageDescription` `PackageTags` [metadanych NuGet.](/dotnet/core/tools/csproj#nuget-metadata-properties) [](../reference/msbuild-targets.md#pack-target) [](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)

> [!NOTE]
> W przypadku pakietów sypkich do publicznego użycia zwróć szczególną uwagę na właściwość **PackageTags,** ponieważ tagi pomagają innym osobom znaleźć Twój pakiet i zrozumieć, co on robi.

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz Odwołania do pakietu w [plikach projektu](../consume-packages/package-references-in-project-files.md) i [Zarządzanie wersjami pakietów](../concepts/package-versioning.md). Istnieje również możliwość powierzchni zasobów z zależności bezpośrednio w pakiecie przy użyciu `<IncludeAssets>` atrybutów `<ExcludeAssets>` i . Aby uzyskać więcej informacji, zobacz [Kontrolowanie zasobów zależności.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)

## <a name="add-an-optional-description-field"></a>Dodawanie opcjonalnego pola opisu

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Wybierz unikatowy identyfikator pakietu i ustaw numer wersji

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Dodawanie pakietu NuGet.Build.Tasks.Pack

Jeśli używasz programu MSBuild z projektem innym niż zestaw SDK i packageReference, dodaj pakiet NuGet.Build.Tasks.Pack do projektu.

1. Otwórz plik projektu i dodaj następujący kod po `<PropertyGroup>` elemencie :

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Otwórz wiersz polecenia dewelopera (w **polu Wyszukaj** wpisz wiersz **polecenia dewelopera**).

   Zazwyczaj chcesz uruchomić aplikację dla programu wiersz polecenia dla deweloperów Visual Studio menu **Start,** ponieważ zostanie ona skonfigurowana ze wszystkimi niezbędnymi ścieżkami dla programu MSBuild.

3. Przejdź do folderu zawierającego plik projektu i wpisz następujące polecenie, aby zainstalować pakiet NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Upewnij się, że dane wyjściowe programu MSBuild wskazują, że kompilacja została ukończona pomyślnie.

## <a name="run-the-msbuild--tpack-command"></a>Uruchom polecenie msbuild -t:pack

Aby skompilować pakiet NuGet (plik) z projektu, uruchom polecenie , które również automatycznie `.nupkg` `msbuild -t:pack` skompilowało projekt:

W wierszu polecenia dewelopera Visual Studio wpisz następujące polecenie:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

Dane wyjściowe pokazują ścieżkę do `.nupkg` pliku.

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

### <a name="automatically-generate-package-on-build"></a>Automatyczne generowanie pakietu podczas kompilacji

Aby automatycznie uruchomić `msbuild -t:pack` projekt podczas kompilowania lub przywracania, dodaj następujący wiersz do pliku projektu w pliku `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Po uruchomieniu w rozwiązaniu zostaną spakowane wszystkie projekty w rozwiązaniu, które można `msbuild -t:pack` spakować [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) (właściwość jest ustawiona na `true` ).

> [!NOTE]
> W przypadku automatycznego generowania pakietu czas jego pakowania wydłuża czas kompilacji projektu.

### <a name="test-package-installation"></a>Testowanie instalacji pakietu

Przed opublikowaniem pakietu zwykle chcesz przetestować proces instalowania pakietu w projekcie. Testy upewniają się, że wszystkie pliki muszą być w odpowiednich miejscach w projekcie.

Instalacje można przetestować ręcznie w programie Visual Studio wierszu polecenia przy użyciu normalnych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Pakiety są niezmienne. Jeśli rozwiązasz problem, zmień zawartość pakietu i ponownie go spakuj. Podczas ponownego testu nadal będziesz używać starej wersji pakietu do momentu wyczyszczenia globalnego folderu [pakietów.](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) Jest to szczególnie istotne w przypadku testowania pakietów, które nie używają unikatowej etykiety w wstępnej kompilacji.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest plikiem, możesz opublikować go w wybranej galerii, zgodnie z opisem w tece `.nupkg` [Publikowanie pakietu](../nuget-org/publish-a-package.md).

Możesz również rozszerzyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze, zgodnie z opisem w następujących tematach:

- [Pakiet NuGet i przywracanie jako obiekty docelowe msBuild](../reference/msbuild-targets.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przekształcenia plików źródłowych i konfiguracji](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje wstępne](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów za pomocą zestawów międzyopunkowych COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Ponadto istnieją dodatkowe typy pakietów, o których należy pamiętać:

- [Pakiety natywne](../guides/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)