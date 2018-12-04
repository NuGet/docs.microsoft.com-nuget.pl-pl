---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą działać bezpośrednio jako elementów docelowych MSBuild nuget 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: a9427d87f69a2e942a9802fbdae5193eead1c724
ms.sourcegitcommit: af58d59669674c3bc0a230d5764e37020a9a3f1e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52831023"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild

*NuGet 4.0+*

Przy użyciu formatu PackageReference NuGet 4.0 + mogą przechowywać metadanych wszystkie manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.

Za pomocą narzędzia MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` jest przeznaczony dla zgodnie z poniższym opisem. Te obiekty docelowe umożliwiają pracę z NuGet, tak jak przy użyciu innych zadań programu MSBuild lub docelowego. (Dla NuGet 3.x i starszym użyj [pakiet](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast polecenia za pomocą interfejsu wiersza polecenia NuGet.)

## <a name="target-build-order"></a>Kolejność kompilowania obiektów docelowych

Ponieważ `pack` i `restore` są elementy docelowe programu MSBuild, można wywołać, aby zwiększyć przepływu pracy. Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu jej. Możesz to zrobić przez dodanie poniższego w pliku projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Podobnie można zapisać zadania programu MSBuild, napisać własne docelowe i korzystać z właściwości NuGet w zadaniu programu MSBuild.

## <a name="pack-target"></a>Pakiet docelowy

W przypadku projektów .NET Standard przy użyciu formatu PackageReference, przy użyciu `msbuild -t:pack` pobiera dane wejściowe z pliku projektu w celu utworzenia pakietu NuGet.

W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w obrębie pierwszych `<PropertyGroup>` węzła. Zmiany możesz wprowadzić te łatwe w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając polecenie **Edytuj {project_name}** w menu kontekstowym. Dla wygody tabeli jest zorganizowana według równoważne właściwość [ `.nuspec` pliku](../reference/nuspec.md).

Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane za pomocą narzędzia MSBuild.

| Wartość atrybutu/NuSpec | Właściwości programu MSBuild | Domyślny | Uwagi |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) z programu MSBuild |
| Wersja | PackageVersion | Wersja | Jest to semver zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | Ustawienie PackageVersion zastępuje PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) z programu MSBuild. Ustawienie PackageVersion zastępuje PackageVersionSuffix |
| Autorzy | Autorzy | Nazwa bieżącego użytkownika | |
| Właściciele | Brak | Nie są obecne w NuSpec | |
| Tytuł | Tytuł | Jako PackageId| |
| Opis | Opis | "Pakiet opis" | |
| Prawa autorskie | Prawa autorskie | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| Licencja | PackageLicenseExpression | empty | Odnosi się do `<license type="expression">` |
| Licencja | PackageLicenseFile | empty | Odnosi się do `<license type="file">`. Konieczne może być jawnie pakietu pliku odwołania licencji. |
| LicenseUrl | PackageLicenseUrl | empty | `licenseUrl` jest on przestarzały, użyj właściwości PackageLicenseExpression lub PackageLicenseFile |
| ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Znaczniki | PackageTags | empty | Tagi są rozdzielone średnikami. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| Adres Url i repozytorium | RepositoryUrl | empty | Adres URL repozytorium jest używany do klonowania lub pobierania kodu źródłowego. Przykład: *https://github.com/NuGet/NuGet.Client.git* |
| Repozytorium/typu | RepositoryType | empty | Typ repozytorium. Przykłady: *git*, *tfs*. |
| Repozytorium/gałąź | RepositoryBranch | empty | Informacje o gałęzi repozytorium opcjonalne. *RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia. Przykład: *wzorca* (NuGet 4.7.0+) |
| Repozytorium na zatwierdzenie | RepositoryCommit | empty | Opcjonalne repozytorium zatwierdzenia lub zestaw zmian, aby wskazać, które źródła pakietu została skompilowana. *RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia. Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
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
- PackageLicenseExpression
- PackageLicenseFile
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
- Atrybut MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>scenariusze z dodatkiem Service Pack

### <a name="packageiconurl"></a>PackageIconUrl

Zmiana w ramach [352 problem NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` ostatecznie zostanie zmieniony na `PackageIconUri` i może być ścieżką względną do pliku ikony, który zostanie uwzględniony w katalogu głównym pakietu wynikowego.

### <a name="output-assemblies"></a>Zestawy danych wyjściowych

`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`. Pliki wyjściowe, które są kopiowane zależą od tego, co MSBuild zapewnia klientom — od `BuiltOutputProjectGroup` docelowej.

Istnieją dwie właściwości programu MSBuild, które można w pliku projektu lub wiersza polecenia do kontrolki gdzie zestawy danych wyjściowych:

- `IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.
- `BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy danych wyjściowych. Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich ramach folderów.

### <a name="package-references"></a>Odwołania do pakietu

Zobacz [pakietu odwołania w plikach projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Projekt do odwołania do projektu

Projekt do odwołania do projektu są uznawane za domyślnie odwołania do pakietu nuget, na przykład:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Można również dodać następujące metadane, do której można się odwołać projektu:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>W tym zawartości w pakiecie

Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu. Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że przesłonisz z wpisy jak następujące:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Domyślnie dodawane pobiera wszystkie elementy w folderze głównym `content` i `contentFiles\any\<target_framework>` folder, w ramach pakietu i zachowuje strukturę folderu względnego, chyba że określisz Ścieżka pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` zarówno), można użyć właściwości programu MSBuild `ContentTargetFolders`, którego wartość domyślna to "zawartość; pliki", ale może być ustawiona na inne nazwy folderu. Należy pamiętać, który po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.

`PackagePath` może być rozdzielone średnikami zestaw ścieżek docelowych. Określenie ścieżki pusty pakiet dodać plik w katalogu głównym pakietu. Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Istnieje również właściwość narzędzia MSBuild `$(IncludeContentInPack)`, które domyślnie używa `true`. Jeśli jest ono ustawione na `false` w żadnym projekcie następnie zawartość z tego projektu nie są uwzględnione w pakiet nuget.

Obejmuje inne określonych metadanych pakietu, który dla każdego z powyższych elementów można ustawić ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który konfiguruje ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpis nuspec danych wyjściowych.

> [!Note]
> Oprócz elementów zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić w plikach za pomocą akcji kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource lub Brak.
>
> Pakiet można dołączyć nazwę pliku do ścieżki pakietu, korzystając z wzorców obsługi symboli wieloznacznych ścieżka do pakietu musi kończyć folderu znaku separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełną ścieżkę, łącznie z nazwą pliku.

### <a name="includesymbols"></a>IncludeSymbols

Korzystając z `MSBuild -t:pack -p:IncludeSymbols=true`, odpowiedni `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.

### <a name="includesource"></a>IncludeSource

To jest taka sama jak `IncludeSymbols`, chyba że kopiuje pliki źródłowe, wraz z `.pdb` również pliki. Pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną do pakietu wynikowego. W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` równa `false`.

Plik typu kompilacji, czy poza folderem projektu, a następnie po prostu dodać go do `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Pakowanie wyrażenie licencji lub też pliku licencji

Korzystając z wyrażenia licencji, właściwość PackageLicenseExpression powinna być używana. 
[Przykładowe wyrażenie licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

Podczas pakowania pliku licencji, należy użyć właściwości PackageLicenseFile do określenia ścieżki pakietu, względem katalogu głównego pakietu. Ponadto należy się upewnić, że plik znajduje się w pakiecie. Na przykład:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
[Przykładowy plik licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>IsTool

Korzystając z `MSBuild -t:pack -p:IsTool=true`, wszystkie dane wyjściowe pliki, jak to określono w [zestawów danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folderu zamiast `lib` folderu. Należy pamiętać, że to różni się od `DotNetCliTool` określić, ustawiając `PackageType` w `.csproj` pliku.

### <a name="packing-using-a-nuspec"></a>Pakowanie przy użyciu .nuspec

Możesz użyć `.nuspec` pliku do pakietu projektu, pod warunkiem, że masz zestaw SDK plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` tak, aby zadanie pakietów, które mogą być wykonywane. Nadal trzeba przywrócić projektu, zanim można spakować soubor nuspec. Platforma docelowa pliku projektu nie ma znaczenia, a nie używany podczas pakowania nuspec. Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania, za pomocą `.nuspec`:

1. `NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` plików używanych na potrzeby pakowania.
1. `NuspecProperties`: rozdzieloną średnikami listę klucz = wartość pary. Ze względu na sposób MSBuild wiersza polecenia analizy działa wiele właściwości należy określić w następujący sposób: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Podstawową ścieżkę dla `.nuspec` pliku.

Jeśli przy użyciu `dotnet.exe` umieszczenie projektu, użyj polecenia podobnego do poniższego:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Jeśli korzystanie z MSBuild do pakietu projektu, należy użyć polecenie podobne do następującego:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Należy pamiętać, pakowanie nuspec przy użyciu dotnet.exe lub msbuild również prowadzi do kompilowania projektu domyślnie. Można tego uniknąć, przekazując ```--no-build``` właściwości dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu oraz ustawienie ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu

Przykładowy plik csproj, umieszczenie soubor nuspec jest:

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

`pack` Docelowy zawiera dwa punkty rozszerzenia, które działają w wewnętrznej, target framework kompilacji. Punkty rozszerzenia obsługi w tym target framework określoną zawartość i zestawy w pakiecie:

- `TargetsForTfmSpecificBuildOutput` docelowy: pliki znajdujące się na użytek `lib` folder lub folder określony za pomocą `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` docelowy: używany do plików znajdujących się poza `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości. Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), element docelowy powinien zapisać te pliki do element ItemGroup `BuildOutputInPackage` i ustaw poniższe dwie wartości metadanych:

- `FinalOutputPath`: Ścieżka bezwzględna pliku. Jeśli nie zostanie podana, tożsamość jest używane do analizowania ścieżki źródłowej.
- `TargetPath`: (Opcjonalnie) ustawiana, jeśli plik musi przejść do podfolderu w `lib\<TargetFramework>` , takich jak zestawy satelickie tego go w ramach ich odpowiednich kultury folderów. Wartość domyślna to nazwa pliku.

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

Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości. Dla wszystkich plików do uwzględnienia w pakiecie docelowym powinien zapisać te pliki do element ItemGroup `TfmSpecificPackageFile` i ustaw następujące opcjonalne metadane:

- `PackagePath`: Ścieżka, gdzie plik powinien znajdować się w danych wyjściowych w pakiecie. NuGet generuje ostrzeżenie, jeśli więcej niż jeden plik jest dodawany do tej samej ścieżki pakietu.
- `BuildAction`: Akcja kompilacji do przypisania do plików, jest wymagany tylko, jeśli ścieżka pakietu jest w `contentFiles` folderu. Wartość domyślna to "None".

Przykład:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Lokalizacja docelowa przywracania

`MSBuild -t:restore` (który `nuget restore` i `dotnet restore` za pomocą projektów .NET Core), pakiety, do którego odwołuje się plik projektu w następujący sposób:

1. Odczyt wszystkich odwołań między projektami
1. Odczyt właściwości projektu, aby znaleźć pośrednich struktur dla folderu docelowego
1. Przekazywanie danych programu msbuild do NuGet.Build.Tasks.dll
1. Uruchom Przywracanie
1. Pobierz pakiety
1. Zapisu pliku zasobów, obiektów docelowych i właściwości

`restore` Docelowy działa **tylko** dla projektów przy użyciu formatu PackageReference. Robi **nie** nadają się do projektów przy użyciu `packages.config` formatowania; użyj [Przywracanie pakietów nuget](../tools/cli-ref-restore.md) zamiast tego.

### <a name="restore-properties"></a>Przywracanie właściwości

Ustawienia dodatkowe przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu. Ponadto można ustawić wartości z wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).

| Właściwość | Opis |
|--------|--------|
| RestoreSources | Rozdzielana średnikami lista źródeł pakietów. |
| RestorePackagesPath | Ścieżka folderu pakietów użytkownika. |
| RestoreDisableParallel | Limit pobiera pojedynczo. |
| RestoreConfigFile | Ścieżka do `Nuget.Config` pliku, aby zastosować. |
| RestoreNoCache | W przypadku wartości true umożliwia uniknięcie korzystania z pamięci podręcznej pakietów. Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | W przypadku opcji true ignoruje awarie lub Brak źródeł pakietów. |
| RestoreTaskAssemblyFile | Ścieżka do `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych. |
| RestoreOutputPath | Folder wyjściowy, przyjęty `obj` folderu. |

#### <a name="examples"></a>Przykłady

Wiersz polecenia:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

Plik projektu:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Przywracanie danych wyjściowych

Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:

| Plik | Opis |
|--------|--------|
| `project.assets.json` | Zawiera wykres zależności dla wszystkich odwołań do pakietów. |
| `{projectName}.projectFileExtension.nuget.g.props` | Odwołania do właściwości programu MSBuild zawartych w pakietach |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odwołania do elementów docelowych MSBuild zawartych w pakietach |

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` Element umożliwia określenie zestawu zgodnych elementów docelowych do użycia podczas przywracania pakietów. Został zaprojektowany tak, aby zezwolić na pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklarują dotnet TxM. Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkich pakietów to zależy od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do swojego projektu, aby umożliwić-dotnet platform zapewnić ich zgodność za pomocą polecenia dotnet.

Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależnego pakietu zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projektu zakończy się niepowodzeniem do kompilacji. Jeśli chcesz w ostatnim biblioteki DLL, wówczas można dodać `PackageTargetFallback` następujący powiedzieć, `portable-net45+win81` Biblioteka DLL jest niezgodny:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Aby zadeklarować rezerwowe dla wszystkich obiektów docelowych w projekcie, należy pozostawić wyłączone `Condition` atrybutu. Można także rozszerzyć istniejące `PackageTargetFallback` umieszczając `$(PackageTargetFallback)` jak pokazano poniżej:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Zastępowanie jedną bibliotekę z wykresu przywracania

Jeśli chodzi o przeniesienie zły zestaw przywracania, istnieje możliwość wykluczenia pakietów wybór domyślny i zamień ją na własną nazwę. Najpierw z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Następnie dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
