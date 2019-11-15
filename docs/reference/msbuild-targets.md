---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą współpracować bezpośrednio z obiektami docelowymi programu MSBuild z pakietem NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 1c2af0b42e88623fa7a1216c17aa269e9b0a58cf
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096907"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild

*Pakiet NuGet 4.0 +*

W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) program NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego pliku `.nuspec`.

W programie MSBuild 15.1 + pakiet NuGet jest również pierwszą klasą obywatela programu MSBuild z `pack` i `restore`, zgodnie z poniższym opisem. Te elementy docelowe umożliwiają współdziałanie z pakietem NuGet, podobnie jak w przypadku każdego innego zadania lub celu programu MSBuild. Aby uzyskać instrukcje tworzenia pakietu NuGet przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md). (W przypadku programu NuGet 3. x i starszych należy użyć poleceń [pakiet](../reference/cli-reference/cli-ref-pack.md) i [Przywróć](../reference/cli-reference/cli-ref-restore.md) zamiast tego w interfejsie wiersza polecenia NuGet).

## <a name="target-build-order"></a>Docelowy porządek kompilacji

Ponieważ `pack` i `restore` są obiektami docelowymi programu MSBuild, można uzyskać do nich dostęp, aby usprawnić przepływ pracy. Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu. Można to zrobić, dodając następujący plik w pliku projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Podobnie można napisać zadanie programu MSBuild, napisać własne miejsce docelowe i korzystać z właściwości NuGet w zadaniu MSBuild.

> [!NOTE]
> `$(OutputPath)` jest względna i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.

## <a name="pack-target"></a>cel pakietu

W przypadku projektów .NET Standard przy użyciu formatu PackageReference użycie `msbuild -t:pack` rysuje dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.

W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w pierwszym węźle `<PropertyGroup>`. Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym. Dla wygody tabela jest zorganizowana przez równoważną właściwość w [pliku `.nuspec`](../reference/nuspec.md).

Należy zauważyć, że właściwości `Owners` i `Summary` z `.nuspec` nie są obsługiwane w programie MSBuild.

| Wartość atrybutu/NuSpec | Właściwość programu MSBuild | Domyślny | Uwagi |
|--------|--------|--------|--------|
| #C1 | PackageId | AssemblyName | $ (AssemblyName) z MSBuild |
| Wersja | PackageVersion | Wersja | Jest to zgodne z semver, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | Ustawienie PackageVersion zastępowanie PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $ (VersionSuffix) z programu MSBuild. Ustawienie PackageVersion zastępowanie PackageVersionSuffix |
| Autorów | Autorów | Nazwa_użytkownika bieżącego użytkownika | |
| rzecz | Brak | Nieobecny w NuSpec | |
| Tytuł | Tytuł | PackageId| |
| Opis | Opis | "Opis pakietu" | |
| Prawo | Prawo | empty | |
| requireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| licencjonowan | PackageLicenseExpression | empty | Odnosi się do `<license type="expression">` |
| licencjonowan | PackageLicenseFile | empty | Odnosi się do `<license type="file">`. Należy jawnie spakować plik licencji, do której istnieje odwołanie. |
| licenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` jest przestarzałe, użyj właściwości PackageLicenseExpression lub PackageLicenseFile |
| projectUrl | PackageProjectUrl | empty | |
| Ikona | PackageIcon | empty | Należy jawnie spakować plik obrazu ikony, do którego istnieje odwołanie.|
| iconUrl | PackageIconUrl | empty | Aby zapewnić najlepsze środowisko niskiego poziomu, `PackageIconUrl` należy określić oprócz `PackageIcon`. Dłuższy termin, `PackageIconUrl` będzie przestarzały. |
| Znaczniki | PackageTags | empty | Tagi są rozdzielane średnikami. |
| releaseNotes | PackageReleaseNotes | empty | |
| Repozytorium/adres URL | RepositoryUrl | empty | Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego. Przykład: *https://github.com/NuGet/NuGet.Client.git* |
| Repozytorium/typ | Repozytorium | empty | Typ repozytorium. Przykłady: *git*i *TFS*. |
| Repozytorium/gałąź | RepositoryBranch | empty | Opcjonalne informacje o gałęzi repozytorium. Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* . Przykład: *Master* (NuGet 4.7.0 +) |
| Repozytorium/zatwierdzenie | RepositoryCommit | empty | Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet. Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* . Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Podsumowanie | Nieobsługiwane | | |

### <a name="pack-target-inputs"></a>docelowe dane wejściowe pakietu

- Ispacking
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- Autorów
- Opis
- Prawo
- PackageRequireLicenseAcceptance
- developmentDependency
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
- packageTypes
- Istool
- RepositoryUrl
- Repozytorium
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

## <a name="pack-scenarios"></a>scenariusze dotyczące pakietów

### <a name="suppress-dependencies"></a>Pomiń zależności

Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet, ustaw wartość `SuppressDependenciesWhenPacking` na `true`, co umożliwi pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` będą przestarzałe na korzyść nowej właściwości [`PackageIcon`](#packageicon) .

Począwszy od programu NuGet 5,3 & Visual Studio 2019 w wersji 16,3, `pack` zwróci ostrzeżenie [NU5048](errors-and-warnings/nu5048) , jeśli metadane pakietu określają tylko `PackageIconUrl`.

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Należy określić zarówno `PackageIcon`, jak i `PackageIconUrl`, aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które jeszcze nie obsługują `PackageIcon`. Program Visual Studio będzie obsługiwał `PackageIcon` pakietów pochodzących ze źródła opartego na folderach w przyszłej wersji.

#### <a name="packing-an-icon-image-file"></a>Pakowanie pliku obrazu ikony

Podczas pakowania pliku obrazu ikony należy użyć właściwości `PackageIcon`, aby określić ścieżkę pakietu względem katalogu głównego pakietu. Ponadto należy się upewnić, że plik jest dołączony do pakietu. Rozmiar pliku obrazu jest ograniczony do 1 MB. Obsługiwane formaty plików to JPEG i PNG. Zalecamy rozdzielczość obrazu 64x64.

Na przykład:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/master/PackageIconExample).

Aby uzyskać odpowiedniki nuspec, zapoznaj się z tematem [nuspec Reference dla ikony](nuspec.md#icon).

### <a name="output-assemblies"></a>Zestawy wyjściowe

`nuget pack` kopiuje pliki wyjściowe z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json` i `.pri`. Pliki wyjściowe, które są kopiowane, zależą od tego, co dziedziczy program MSBuild z elementu docelowego `BuiltOutputProjectGroup`.

Istnieją dwie właściwości programu MSBuild, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie znajdują się zestawy wyjściowe:

- `IncludeBuildOutput`: wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być dołączone do pakietu.
- `BuildOutputTargetFolder`: określa folder, w którym należy umieścić zestawy wyjściowe. Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.

### <a name="package-references"></a>Odwołania do pakietu

Zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Odwołania projektu do projektu

Odwołania projektu do projektu są traktowane domyślnie jako odwołania do pakietów NuGet, na przykład:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Możesz również dodać następujące metadane do odwołania do projektu:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Dołączanie zawartości do pakietu

Aby dołączyć zawartość, Dodaj dodatkowe metadane do istniejącego elementu `<Content>`. Domyślnie wszystkie elementy typu "Content" są uwzględniane w pakiecie, chyba że przestąpisz do wpisów, takich jak następujące:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Domyślnie wszystko jest dodawane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje względną strukturę folderów, chyba że zostanie określona ścieżka pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (zamiast `content` i `contentFiles`), możesz użyć właściwości programu MSBuild `ContentTargetFolders`, która domyślnie przyjmuje wartość "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu. Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` umieszcza pliki w `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.

`PackagePath` może być zestawem z rozdzielonymi średnikami ścieżkami docelowymi. Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu. Na przykład następujące dodaje `libuv.txt` do `content\myfiles`, `content\samples` i katalogu głównego pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Istnieje również właściwość programu MSBuild `$(IncludeContentInPack)`, która ma wartość domyślną `true`. Jeśli jest ustawiona na `false` w każdym projekcie, zawartość z tego projektu nie jest dołączana do pakietu NuGet.

Inne metadane specyficzne dla pakietu, które można ustawić dla dowolnego z powyższych elementów, obejmują ```<PackageCopyToOutput>``` i ```<PackageFlatten>```, które ustawiają wartości ```CopyToOutput``` i ```Flatten``` w pozycji ```contentFiles``` w danych wyjściowych nuspec.

> [!Note]
> Oprócz elementów zawartości można również ustawić metadane `<Pack>` i `<PackagePath>` dla plików z akcją kompilacji kompilowania, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.
>
> Aby pakiet mógł dołączyć nazwę pliku do ścieżki pakietu przy użyciu wzorców obsługi symboli wieloznacznych, ścieżka pakietu musi kończyć się znakiem separatora folderów. w przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka, w tym nazwa pliku.

### <a name="includesymbols"></a>IncludeSymbols

W przypadku używania `MSBuild -t:pack -p:IncludeSymbols=true` odpowiednie pliki `.pdb` są kopiowane wraz z innymi plikami wyjściowymi (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy zwykły pakiet *i* pakiet symboli.

### <a name="includesource"></a>IncludeSource

Jest to taka sama jak `IncludeSymbols`, z tą różnicą, że kopiuje pliki źródłowe wraz z również plikami `.pdb`. Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowując strukturę folderu ścieżki względnej w pakietie będącym wynikiem. Dzieje się tak samo w przypadku plików źródłowych dowolnego `ProjectReference` z ustawieniem `TreatAsPackageReference` ustawionym na `false`.

Jeśli plik typu Kompiluj znajduje się poza folderem projektu, to właśnie został dodany do `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Pakowanie wyrażenia licencji lub pliku licencji

W przypadku korzystania z wyrażenia licencji Właściwość PackageLicenseExpression powinna zostać użyta. 
[Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[Dowiedz się więcej na temat wyrażeń licencji i licencji akceptowanych przez NuGet.org](nuspec.md#license).

Podczas pakowania pliku licencji należy użyć właściwości PackageLicenseFile, aby określić ścieżkę pakietu względem katalogu głównego pakietu. Ponadto należy się upewnić, że plik jest dołączony do pakietu. Na przykład:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

[Przykład pliku licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>Istool

W przypadku używania `MSBuild -t:pack -p:IsTool=true` wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , są kopiowane do folderu `tools` zamiast folderu `lib`. Należy zauważyć, że różni się od `DotNetCliTool`, który jest określony przez ustawienie `PackageType` w pliku `.csproj`.

### <a name="packing-using-a-nuspec"></a>Pakowanie przy użyciu elementu. nuspec

Mimo że zaleca się [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w pliku z `.nuspec` w pliku projektu, można użyć pliku `.nuspec` do spakowania projektu. W przypadku projektu typu innego niż zestaw SDK, który używa `PackageReference`, należy zaimportować `NuGet.Build.Tasks.Pack.targets`, aby można było wykonać zadanie pakietu. Nadal trzeba przywrócić projekt, aby można było spakować plik NUSPEC. (Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).

Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania nuspec. Następujące trzy właściwości programu MSBuild dotyczą pakowania przy użyciu `.nuspec`:

1. `NuspecFile`: ścieżka względna lub bezwzględna do pliku `.nuspec` używanego do pakowania.
1. `NuspecProperties`: rozdzielana średnikami lista par klucz = wartość. Ze względu na sposób działania analizy wiersza polecenia MSBuild należy określić wiele właściwości: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Ścieżka bazowa dla pliku `.nuspec`.

Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Jeśli używasz programu MSBuild do pakowania projektu, użyj następującego polecenia:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Należy pamiętać, że pakowanie nuspec przy użyciu programu dotnet. exe lub MSBuild również prowadzi do domyślnego kompilowania projektu. Można to uniknąć przez przekazanie właściwości ```--no-build``` do programu dotnet. exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.

Przykład pliku *. csproj* do spakowania pliku nuspec jest:

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

### <a name="advanced-extension-points-to-create-customized-package"></a>Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu

Element docelowy `pack` zawiera dwa punkty rozszerzenia, które są uruchamiane w wewnętrznej kompilacji specyficznej dla platformy docelowej. Obsługa punktów rozszerzenia umożliwia uwzględnienie zawartości i zestawów określonych dla platformy docelowej w pakiecie:

- element docelowy `TargetsForTfmSpecificBuildOutput`: Użyj dla plików znajdujących się w folderze `lib` lub folderze określonym przy użyciu `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` target: Użyj dla plików poza `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Napisz niestandardowy element docelowy i określ go jako wartość właściwości `$(TargetsForTfmSpecificBuildOutput)`. Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), obiekt docelowy powinien zapisać te pliki w obiekcie Items `BuildOutputInPackage` i ustawić następujące dwie wartości metadanych:

- `FinalOutputPath`: ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość służy do oszacowania ścieżki źródłowej.
- `TargetPath`: (opcjonalnie) ustawia się, gdy plik musi przejść do podfolderu w `lib\<TargetFramework>`, podobnie jak zestawy satelickie, które przechodzą w odpowiednie foldery kultury. Wartością domyślną jest nazwa pliku.

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

Napisz niestandardowy element docelowy i określ go jako wartość właściwości `$(TargetsForTfmSpecificContentInPackage)`. Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki do `TfmSpecificPackageFile` i ustawić następujące opcjonalne metadane:

- `PackagePath`: ścieżka, w której plik powinien być wyprowadzany w pakiecie. Pakiet NuGet wystawia ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.
- `BuildAction`: Akcja kompilacji, która ma zostać przypisana do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w folderze `contentFiles`. Wartość domyślna to "none".

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

## <a name="restore-target"></a>Przywróć miejsce docelowe

`MSBuild -t:restore` (które `nuget restore` i `dotnet restore` są używane z projektami .NET Core), przywraca pakiety, do których odwołuje się plik projektu, w następujący sposób:

1. Odczytuj wszystkie odwołania projektu do projektu
1. Odczytywanie właściwości projektu w celu znalezienia pośredniego folderu i platform docelowych
1. Przekaż dane programu MSBuild do pliku NuGet. Build. Tasks. dll
1. Uruchom przywracanie
1. Pobierz pakiety
1. Zapisz plik zasobów, cele i właściwości.

Element docelowy `restore` działa **tylko** w przypadku projektów korzystających z formatu PackageReference. **Nie działa w** przypadku projektów przy użyciu formatu `packages.config`; Zamiast tego użyj [przywracania NuGet](../reference/cli-reference/cli-ref-restore.md) .

### <a name="restore-properties"></a>Właściwości przywracania

Dodatkowe ustawienia przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu. Wartości można również ustawić z poziomu wiersza polecenia przy użyciu przełącznika `-p:` (Zobacz poniższe przykłady).

| Właściwość | Opis |
|--------|--------|
| RestoreSources | Rozdzielana średnikami lista źródeł pakietów. |
| RestorePackagesPath | Ścieżka folderu pakietów użytkownika. |
| RestoreDisableParallel | Ogranicz pobieranie do jednej naraz. |
| RestoreConfigFile | Ścieżka do pliku `Nuget.Config`, który ma zostać zastosowany. |
| RestoreNoCache | Jeśli ma wartość true, unika używania buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów. |
| RestoreFallbackFolders | Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika. |
| RestoreAdditionalProjectSources | Dodatkowe źródła do użycia podczas przywracania. |
| RestoreAdditionalProjectFallbackFolders | Dodatkowe foldery rezerwowe do użycia podczas przywracania. |
| RestoreAdditionalProjectFallbackFoldersExcludes | Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Ścieżka do `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne. |
| RestoreUseSkipNonexistentTargets  | Gdy projekty są zbierane za pośrednictwem programu MSBuild, określa, czy są zbierane przy użyciu optymalizacji `SkipNonexistentTargets`. Gdy nie jest ustawiona, wartość domyślna to `true`. Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu. |
| MSBuildProjectExtensionsPath | Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` i folder `obj`. |
| RestoreForce | W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie. Określenie tej flagi jest podobne do usuwania pliku `project.assets.json`. Nie powoduje to obejścia pamięci podręcznej protokołu HTTP. |
| RestorePackagesWithLockFile | Umożliwia użycie pliku blokady. |
| RestoreLockedMode | Uruchom przywracanie w trybie zablokowanym. Oznacza to, że przywracanie nie będzie obliczać zależności. |
| NuGetLockFilePath | Niestandardowa lokalizacja pliku blokady. Domyślna lokalizacja jest obok projektu i nosi nazwę `packages.lock.json`. |
| RestoreForceEvaluate | Wymusza ponowne obliczenie zależności przez Przywracanie i zaktualizowanie pliku blokady bez ostrzeżenia. | 

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

### <a name="restore-outputs"></a>Przywróć dane wyjściowe

Instrukcja RESTORE tworzy następujące pliki w folderze Build `obj`:

| Plik | Opis |
|--------|--------|
| `project.assets.json` | Zawiera wykres zależności wszystkich odwołań do pakietu. |
| `{projectName}.projectFileExtension.nuget.g.props` | Odwołania do właściwości programu MSBuild zawartych w pakietach |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odwołania do elementów docelowych programu MSBuild zawartych w pakietach |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Przywracanie i kompilowanie za pomocą jednego polecenia MSBuild

Ze względu na fakt, że pakiet NuGet może przywrócić pakiety, które wyłączają elementy docelowe i właściwości programu MSBuild, a oceny przywracania i kompilacji są uruchamiane z różnymi właściwośćmi globalnymi.
Oznacza to, że następujące elementy będą miały nieprzewidywalne i często nieprawidłowe zachowanie.

```cli
msbuild -t:restore,build
```

 Zamiast tego zalecane podejście to:

```cli
msbuild -t:build -restore
```

Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build`.

### <a name="packagetargetfallback"></a>PackageTargetFallback

Element `PackageTargetFallback` umożliwia określenie zestawu zgodnych elementów docelowych, które mają być używane podczas przywracania pakietów. Została zaprojektowana tak, aby zezwalać na pakiety, które używają [TxM](../reference/target-frameworks.md) dotnet, do pracy z zgodnymi pakietami, które nie deklarują TxM dotnet. Oznacza to, że jeśli projekt używa TxM dotnet, wszystkie pakiety, od których zależy, muszą także mieć TxM dotnet, chyba że dodasz `<PackageTargetFallback>` do projektu w celu umożliwienia zgodności z platformą dotnet.

Na przykład jeśli projekt używa `netstandard1.6` TxM, a pakiet zależny zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, to projekt nie zostanie skompilowany. Jeśli to, co chcesz zrobić, jest tą samą biblioteką DLL, można dodać `PackageTargetFallback` w następujący sposób, aby wyznaczyć, że biblioteka `portable-net45+win81` jest zgodna:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Aby zadeklarować rezerwę dla wszystkich obiektów docelowych w projekcie, pozostaw atrybut `Condition`. Możesz również rozłożyć wszystkie istniejące `PackageTargetFallback` przez uwzględnienie `$(PackageTargetFallback)`, jak pokazano poniżej:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Zastępowanie jednej biblioteki na podstawie grafu przywracania

Jeśli przywracanie powoduje przełączenie niewłaściwego zestawu, możliwe jest wykluczenie domyślnego wyboru pakietów i zamienienie go na własny wybór. Po pierwsze `PackageReference` Wyklucz wszystkie elementy zawartości:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Następnie Dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
