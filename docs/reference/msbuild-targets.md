---
title: Pakiet NuGet i przywracania jako docelowych elementów MSBuild
description: Pakiet NuGet i przywracania może współpracować bezpośrednio jako docelowych elementów MSBuild nuget 4.0 +.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 00d763bcfdd2f3db50378a1e7774eae7a2e1fcd1
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Pakiet NuGet i przywracania jako docelowych elementów MSBuild

*NuGet 4.0+*

W formacie PackageReference NuGet 4.0 + mogą przechowywać wszystkie manifestu metadanych bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.

Przy użyciu programu MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` celem zgodnie z poniższym opisem. Następujących elementów docelowych umożliwiają pracę z programem NuGet, tak jak inne zadanie programu MSBuild lub docelowego. (Programu NuGet 3.x i wcześniej, użyj [pakietu](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast tego polecenia za pomocą interfejsu wiersza polecenia NuGet.)

## <a name="target-build-order"></a>Kolejność kompilowania obiektów docelowych

Ponieważ `pack` i `restore` MSBuild elementów docelowych, można wywołać w celu zwiększenia przepływu pracy. Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu go. Możesz to zrobić przez dodanie poniższego w pliku projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Podobnie można zapisać zadania programu MSBuild, napisać własny docelowych i korzystać z właściwości NuGet w zadanie programu MSBuild.

## <a name="pack-target"></a>docelowy pakiet

Dla platformy .NET Standard projektów przy użyciu formatu PackageReference, używając `msbuild /t:pack` pobiera dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.

W poniższej tabeli opisano właściwości programu MSBuild, które mogą zostać dodane do pliku projektu w pierwszym `<PropertyGroup>` węzła. Wprowadź te zmiany łatwe w Visual Studio 2017 i później przez kliknięcie prawym przyciskiem myszy projekt i wybierając **edytować {nazwa_projektu}** w menu kontekstowym. Dla wygody tabeli jest zorganizowana według równoważne właściwości w [ `.nuspec` pliku](../reference/nuspec.md).

Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane przy użyciu programu MSBuild.

| Wartość atrybutu/NuSpec. | Właściwości programu MSBuild | Domyślny | Uwagi |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) z MSBuild |
| Wersja | PackageVersion | Wersja | Jest to zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" programu semver |
| VersionPrefix | PackageVersionPrefix | empty | Ustawienie PackageVersion zastępuje PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) z programu MSBuild. Ustawienie PackageVersion zastępuje PackageVersionSuffix |
| Autorzy | Autorzy | Nazwa bieżącego użytkownika | |
| Właściciele | Brak | Nie istnieje w pliku NuSpec | |
| Tytuł | Tytuł | PackageId| |
| Opis | Opis | "Opis pakietu" | |
| Prawa autorskie | Prawa autorskie | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| LicenseUrl | PackageLicenseUrl | empty | |
| ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Znaczniki | PackageTags | empty | Tagi są rozdzielone średnikami. |
| releaseNotes | PackageReleaseNotes | empty | |
| Adres Url i repozytorium | RepositoryUrl | empty | Adres URL repozytorium jest używany do klonowania lub pobrać kodu źródłowego. Przykład: *https://github.com/NuGet/NuGet.Client.git* |
| Repozytorium/typ | RepositoryType | empty | Typ repozytorium. Przykłady: *git*, *tfs*. |
| Repozytorium/gałęzi | RepositoryBranch | empty | Informacje o gałęzi repozytorium opcjonalne. *RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione. Przykład: *wzorca* (NuGet 4.7.0+) |
| Repozytorium/zatwierdzeniu | RepositoryCommit | empty | Opcjonalne repozytorium zatwierdzania lub zestaw zmian, aby wskazać, który źródła pakietu został skompilowany przy. *RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione. Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Podsumowanie | Nieobsługiwane | | |

### <a name="pack-target-inputs"></a>dane wejściowe docelowego pakietu

- IsPackable
- PackageVersion
- PackageId
- Autorzy
- Opis
- Prawa autorskie
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>scenariusze z dodatkiem Service Pack

### <a name="packageiconurl"></a>PackageIconUrl

Zmiana w ramach [352 problem NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` po pewnym czasie zostaną zmienione na `PackageIconUri` i może być względna ścieżka do pliku ikony, które zostaną uwzględnione w katalogu głównym wynikowy pakiet.

### <a name="output-assemblies"></a>Zestawy danych wyjściowych

`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`. Pliki wyjściowe, które są kopiowane są zależne od MSBuild zapewnia z `BuiltOutputProjectGroup` docelowej.

Istnieją dwie właściwości programu MSBuild, które są dostępne w pliku projektu lub wiersza polecenia w celu sterowania gdzie zestawy danych wyjściowych:

- `IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.
- `BuildOutputTargetFolder`: Określa folder, w którym ma zostać umieszczony zestawy danych wyjściowych. Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich framework folderów.

### <a name="package-references"></a>Odwołania do pakietu

Zobacz [pakietu odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Projekt do odwołań projektu

Projekt do odwołań projektu są traktowane jako domyślnie jako odwołania do pakietu nuget, na przykład:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Można również dodać następujące metadane odwołania do projektu:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>W tym zawartości w pakiecie

Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu. Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że nadpiszesz zapisami jak następujące:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Domyślnie pobiera wszystkie elementy dodane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje struktury folder względny, o ile nie zostanie określona ścieżka pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` oba), można użyć właściwości programu MSBuild `ContentTargetFolders`, jakie nie "zawartość; pliki", ale może być ustawiony na inne nazwy folderu. Należy pamiętać, że po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.

`PackagePath` może być rozdzielone średnikami zbiór ścieżek docelowych. Określenie ścieżki pusty pakietu dodać plik w katalogu głównym pakietu. Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Istnieje również właściwość MSBuild `$(IncludeContentInPack)`, jakie nie `true`. Jeśli ta wartość jest równa `false` w żadnym projekcie następnie zawartość z tego projektu nie znajdują się w pakiecie nuget.

Zawiera inne metadane określonego pakietu, które można ustawić na żadnym z powyższych elementów ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który określa ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpisu w pliku nuspec danych wyjściowych.

> [!Note]
> Oprócz elementy zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić na pliki z akcją kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.
>
> Pakiet można dołączyć nazwę pliku do ścieżki pakietu przy użyciu globbing wzorców ścieżka do pakietu musi być zakończona z folderu znak separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełna ścieżka, łącznie z nazwą pliku.

### <a name="includesymbols"></a>IncludeSymbols

Korzystając z `MSBuild /t:pack /p:IncludeSymbols=true`, odpowiadającego `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.

### <a name="includesource"></a>IncludeSource

To jest taka sama jak `IncludeSymbols`, ale kopiuje pliki źródłowe wraz z programem `.pdb` również pliki. Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną w pakiecie wynikowy. W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` ustawioną `false`.

Jeśli plik typu skompilować, znajduje się poza folderu projektu, a następnie wystarczy dodać go do `src\<ProjectName>\`.

### <a name="istool"></a>IsTool

Korzystając z `MSBuild /t:pack /p:IsTool=true`, wszystkie dane wyjściowe pliki, jak określono w [zestawy danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folder zamiast `lib` folderu. Należy pamiętać, że jest inny niż `DotNetCliTool` który jest określany przez ustawienie `PackageType` w `.csproj` pliku.

### <a name="packing-using-a-nuspec"></a>Przy użyciu .nuspec pakowania

Można użyć `.nuspec` plik można spakować projektu, pod warunkiem, że masz SDK plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` , dzięki czemu mogą być wykonywane zadanie pakietów. Nadal potrzebujesz przywrócić projekt przed można pliku nuspec. Platforma docelowa pliku projektu nie ma znaczenia, a nie używany podczas pakowania nuspec. Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania przy użyciu `.nuspec`:

1. `NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` pliku używany na potrzeby pakowania.
1. `NuspecProperties`: Rozdzielana średnikami lista klucz = pary wartości. Ze względu na sposób działania analizy wiersza polecenia programu MSBuild, wiele właściwości musi być następujący: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Ścieżki podstawowa dla `.nuspec` pliku.

Jeśli przy użyciu `dotnet.exe` pakowania projektu, użyj polecenia podobnie do następującej:

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Jeśli pakiet projektu za pomocą programu MSBuild, należy użyć polecenia podobne do poniższych:

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Należy pamiętać, pakowanie nuspec przy użyciu dotnet.exe lub msbuild również prowadzi do tworzenia projektu domyślnie. Można tego uniknąć przez przekazanie ```--no-build``` dotnet.exe, który jest odpowiednikiem ustawienie dla właściwości ```<NoBuild>true</NoBuild> ``` w pliku projektu oraz ustawienie ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu

Przykładowy plik csproj, można spakować plik nuspec to:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Zaawansowane punktów rozszerzenia, aby utworzyć dostosowany pakiet

`pack` Docelowy zawiera dwa punkty rozszerzeń uruchamianych w wewnętrznej, określonej kompilacji framework docelowej. Punkty rozszerzenia pomocy technicznej oraz docelowego framework określone zestawy w pakiecie:

- `TargetsForTfmSpecificBuildOutput` docelowy: pliki znajdujące się na użytek `lib` folder lub folder, określić przy użyciu `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` docelowy: Użyj dla plików znajdujących się poza `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Zapisz niestandardowe docelowych i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości. Pliki, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), element docelowy należy zapisać te pliki do ItemGroup `BuildOutputInPackage` i ustaw następujące dwie wartości metadanych:

- `FinalOutputPath`: Ścieżka bezwzględna plików; Jeśli nie podano tożsamości jest używane do analizowania ścieżki źródłowej.
- `TargetPath`: (Opcjonalnie) ustawić, gdy trzeba przejdź do podfolderu w pliku `lib\<TargetFramework>` , takie jak towarzyszącej zestawy tego Przejdź w folderach ich odpowiednich kultury. Wartość domyślna to nazwa pliku.

Przykład:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Zapisz niestandardowe docelowych i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości. W przypadku plików do uwzględnienia w pakiecie docelowy należy zapisać te pliki do ItemGroup `TfmSpecificPackageFile` i ustaw następujące opcjonalne metadane:

- `PackagePath`: Ścieżka, gdy ten plik powinien być dane wyjściowe w pakiecie. NuGet wygeneruje ostrzeżenie, jeśli więcej niż jeden plik został dodany do tej samej ścieżki pakietu.
- `BuildAction`: Akcja kompilacji do przypisania do plików, jest wymagany tylko wtedy, jeśli ścieżka pakietu znajduje się w `contentFiles` folderu. Wartość domyślna to "None".

Przykład:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
  <ItemGroup>
    <TfmSpecificPackageFile Include=""abc.txt"">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Lokalizacja docelowa przywracania

`MSBuild /t:restore` (który `nuget restore` i `dotnet restore` za pomocą platformy .NET Core projektów), przywraca pakietów, do których odwołuje się w pliku projektu w następujący sposób:

1. Przeczytaj wszystkich odwołań do projektu do projektu
1. Właściwości projektu, aby znaleźć pośredniego struktury folderów i obiekt docelowy do odczytu
1. Przekazywanie danych msbuild do NuGet.Build.Tasks.dll
1. Uruchamianie przywracania
1. Pobieranie pakietów
1. Zapis plików zasobów, cele i właściwości

`restore` Docelowy działa **tylko** dla projektów w formacie PackageReference. Robi **nie** pracy dla projektów przy użyciu `packages.config` sformatować; użyj [Przywracanie nuget](../tools/cli-ref-restore.md) zamiast tego.

### <a name="restore-properties"></a>Przywróć właściwości

Przywróć dodatkowe ustawienia mogą pochodzić z właściwości programu MSBuild w pliku projektu. Można również ustawić wartości z wiersza polecenia przy użyciu `/p:` przełącznika (Zobacz przykłady poniżej).

| Właściwość | Opis |
|--------|--------|
| RestoreSources | Rozdzielana średnikami lista źródeł pakietów. |
| RestorePackagesPath | Ścieżka folderu pakietów użytkownika. |
| RestoreDisableParallel | Limit pobiera pojedynczo. |
| RestoreConfigFile | Ścieżka do `Nuget.Config` pliku w celu zastosowania. |
| RestoreNoCache | Jeśli PRAWDA, pozwala uniknąć za pomocą pakietów pamięci podręcznej. Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Jeśli PRAWDA, ignoruje wystąpił błąd lub Brak źródeł pakietów. |
| RestoreTaskAssemblyFile | Ścieżka do `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych. |
| RestoreOutputPath | Folder wyjściowy, przyjęty `obj` folderu. |

#### <a name="examples"></a>Przykłady

Wiersz polecenia:

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

Plik projektu:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Przywróć dane wyjściowe

Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:

| Plik | Opis |
|--------|--------|
| `project.assets.json` | Zawiera wykres zależności wszystkie odwołania do pakietu. |
| `{projectName}.projectFileExtension.nuget.g.props` | Odwołania do właściwości programu MSBuild zawartych w pakietach |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odwołania do zawartych w pakietach docelowych elementów MSBuild |

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` Element służy do określenia zestawu zgodne cele, które mają być użyte podczas przywracania pakietów. Został zaprojektowany tak, aby umożliwić pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklaruje dotnet TxM. Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkie pakiety zależy on od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do projektu, aby umożliwić platformy dotnet z systemem innym niż był zgodny z dotnet.

Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależny pakiet zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projekt zakończy się niepowodzeniem do kompilacji. Jeśli chcesz przenieść jest ostatnim biblioteki DLL, a następnie można dodać `PackageTargetFallback` w następujący sposób, aby oznacza, że `portable-net45+win81` zgodnego biblioteki DLL:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Aby zadeklarować używane dla wszystkich elementów docelowych w projekcie, pozostaw `Condition` atrybutu. Można również rozszerzyć zasięg wszelkie istniejące `PackageTargetFallback` przez dołączenie `$(PackageTargetFallback)` w sposób pokazany poniżej:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Zastępowanie jedną bibliotekę z wykresu przywracania

Jeśli przywracania jest Przywracanie nieprawidłowy zestaw, jest możliwe do wykluczenia z pakietów domyślny wybór i zamień ją na dowolny inny. Pierwszy z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Następnie dodaj własne odwołanie do odpowiedniego lokalną kopię pliku DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
