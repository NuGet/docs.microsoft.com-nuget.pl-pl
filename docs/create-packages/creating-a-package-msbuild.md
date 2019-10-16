---
title: Tworzenie pakietu NuGet przy użyciu programu MSBuild
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym najważniejszych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9512899a4086d17d2584f16833aba33efb321eae
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380693"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Tworzenie pakietu NuGet przy użyciu programu MSBuild

Podczas tworzenia pakietu NuGet przy użyciu kodu należy spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów. W tym artykule opisano sposób tworzenia pakietu przy użyciu programu MSBuild. Program MSBuild jest preinstalowany z każdym obciążeniem programu Visual Studio, który zawiera pakiet NuGet. Ponadto można również użyć MSBuild za pomocą interfejsu wiersza polecenia dotnet z użyciem programu [dotnet MSBuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)

W przypadku projektów .NET Core i .NET Standard, które korzystają z [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, NuGet używa informacji w pliku projektu bezpośrednio do tworzenia pakietu.  Dla projektu typu innego niż zestaw SDK, który używa `<PackageReference>`, NuGet używa również pliku projektu do utworzenia pakietu.

Projekty w stylu zestawu SDK mają funkcje pakietu dostępne domyślnie. W przypadku projektów PackageReference bez zestawu SDK należy dodać pakiet NuGet. Build. Tasks. Pack do zależności projektu. Aby uzyskać szczegółowe informacje o obiektach docelowych programu MSBuild, zobacz [pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md).

Polecenie, które tworzy pakiet, `msbuild -t:pack`, jest funkcją odpowiadającą `dotnet pack`.

> [!IMPORTANT]
> Ten temat ma zastosowanie do projektów w [stylu zestawu SDK](../resources/check-project-format.md) , zwykle .NET Core i .NET Standard projektów oraz do projektów typu non-SDK, które używają PackageReference.

## <a name="set-properties"></a>Ustaw właściwości

Do utworzenia pakietu wymagane są następujące właściwości.

- `PackageId`, identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.
- `Version` — określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersję wstępną](prerelease-packages.md). Jeśli nie zostanie określony, wartość domyślna to 1.0.0.
- Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)
- `Authors`, informacje o autorze i właścicielu. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.
- `Company`, nazwa firmy. Jeśli nie zostanie określony, wartość domyślna to `AssemblyName`.

W programie Visual Studio można ustawić te wartości we właściwościach projektu (kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz **Właściwości**, a następnie wybierz kartę **pakiet** ). Możesz również ustawić te właściwości bezpośrednio w plikach projektu ( *. csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Nadaj pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego źródła pakietów, którego używasz.

Poniższy przykład pokazuje prosty, kompletny plik projektu z tymi właściwościami.

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

Można również ustawić właściwości opcjonalne, takie jak `Title`, `PackageDescription` i `PackageTags`, zgodnie z opisem w obszarze [targets pakietu MSBuild](../reference/msbuild-targets.md#pack-target), [kontrolowanie elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)i [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na Właściwość **PackageTags** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md) i [przechowywanie wersji pakietu](../concepts/package-versioning.md). Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu atrybutów `<IncludeAssets>` i `<ExcludeAssets>`. Aby uzyskać więcej informacji, seee [kontrolowania elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Wybierz unikatowy identyfikator pakietu i ustaw numer wersji

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Dodaj pakiet NuGet. Build. Tasks. Pack

Jeśli używasz programu MSBuild z projektem w stylu innym niż zestaw SDK i PackageReference, Dodaj pakiet NuGet. Build. Tasks. Pack do projektu.

1. Otwórz plik projektu i Dodaj następujący element po elemencie `<PropertyGroup>`:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Otwórz wiersz polecenia dewelopera (w polu **wyszukiwania** wpisz **wiersz polecenia programisty**).

   Zazwyczaj chcesz uruchomić wiersz polecenia dla deweloperów dla programu Visual Studio z menu **Start** , ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla programu MSBuild.

3. Przejdź do folderu zawierającego plik projektu i wpisz następujące polecenie, aby zainstalować pakiet NuGet. Build. Tasks. Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Upewnij się, że dane wyjściowe programu MSBuild wskazują, że kompilacja została ukończona pomyślnie.

## <a name="run-the-msbuild--tpack-command"></a>Uruchamianie polecenia MSBuild-t:Pack

Aby skompilować pakiet NuGet (plik `.nupkg`) z projektu, uruchom polecenie `msbuild -t:pack`, które również automatycznie kompiluje projekt:

W wierszu polecenia dla deweloperów dla programu Visual Studio wpisz następujące polecenie:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

Dane wyjściowe przedstawiają ścieżkę do pliku `.nupkg`.

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

### <a name="automatically-generate-package-on-build"></a>Automatycznie Generuj pakiet podczas kompilacji

Aby automatycznie uruchomić `msbuild -t:pack` podczas kompilowania lub przywracania projektu, Dodaj następujący wiersz do pliku projektu w ramach `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Po uruchomieniu `msbuild -t:pack` w rozwiązaniu to pakiety wszystkie projekty w rozwiązaniu, które są możliwe do spakowania (Właściwość[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) jest ustawiona na `true`).

> [!NOTE]
> Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji projektu.

### <a name="test-package-installation"></a>Instalacja pakietu testowego

Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie. Testy upewniają się, że wszystkie pliki, które się na bieżąco, kończą się w ich prawidłowym miejscu w projekcie.

Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Pakiety są niezmienne. W przypadku usunięcia problemu należy ponownie zmienić zawartość pakietu i pakietu, po ponownym przetestowaniu nadal będzie używana stara wersja pakietu do momentu [wyczyszczenia folderu pakiety globalne](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) . Jest to szczególnie istotne w przypadku testowania pakietów, które nie używają unikatowej etykiety wersji wstępnej dla każdej kompilacji.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest plikiem `.nupkg`, można opublikować go w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).

Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:

- [Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md)
- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/multiple-target-frameworks-project-file.md)
- [Przekształcenia plików źródłowych i konfiguracji](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje wstępne](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Na koniec należy pamiętać o dodatkowych typach pakietów:

- [Pakiety natywne](../guides/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
