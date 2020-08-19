---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą współpracować bezpośrednio z obiektami docelowymi programu MSBuild z pakietem NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 16fd7b9103ef5ac335f0b2e5493dd2983b182f50
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623178"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild

*Pakiet NuGet 4.0 +*

W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) program NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.

Dzięki programowi MSBuild 15.1 + pakiet NuGet jest również pierwszym klasą obywatela programu MSBuild z `pack` `restore` obiektami docelowymi, zgodnie z poniższym opisem. Te elementy docelowe umożliwiają współdziałanie z pakietem NuGet, podobnie jak w przypadku każdego innego zadania lub celu programu MSBuild. Aby uzyskać instrukcje tworzenia pakietu NuGet przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md). (W przypadku programu NuGet 3. x i starszych należy użyć poleceń [pakiet](../reference/cli-reference/cli-ref-pack.md) i [Przywróć](../reference/cli-reference/cli-ref-restore.md) zamiast tego w interfejsie wiersza polecenia NuGet).

## <a name="target-build-order"></a>Kolejność kompilowania obiektów docelowych

Ponieważ `pack` i `restore` są obiektami docelowymi programu MSBuild, możesz uzyskać do nich dostęp, aby usprawnić przepływ pracy. Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu. Można to zrobić, dodając następujący plik w pliku projektu:

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

W przypadku projektów .NET Standard przy użyciu formatu PackageReference użycie narzędzi `msbuild -t:pack` Pobiera dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.

W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle. Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym. Dla wygody tabela jest zorganizowana przez równoważną właściwość w [ `.nuspec` pliku](../reference/nuspec.md).

Należy zauważyć, `Owners` że `Summary` właściwości i z `.nuspec` nie są obsługiwane w programie MSBuild.

| Wartość atrybutu/NuSpec | Właściwość programu MSBuild | Domyślny | Uwagi |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $ (AssemblyName) z MSBuild |
| Wersja | PackageVersion | Wersja | Jest to zgodne z semver, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | puste | Ustawienie PackageVersion zastępowanie PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | puste | $ (VersionSuffix) z programu MSBuild. Ustawienie PackageVersion zastępowanie PackageVersionSuffix |
| Autorzy | Autorzy | Nazwa_użytkownika bieżącego użytkownika | |
| Właściciele | Nie dotyczy | Nieobecny w NuSpec | |
| Tytuł | Tytuł | PackageId| |
| Opis | Opis | "Opis pakietu" | |
| Prawa autorskie | Prawa autorskie | puste | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | fałsz | |
| license (licencja) | PackageLicenseExpression | puste | Odnosi się do `<license type="expression">` |
| license (licencja) | PackageLicenseFile | puste | Odnosi się do `<license type="file">` . Należy jawnie spakować plik licencji, do której istnieje odwołanie. |
| LicenseUrl | PackageLicenseUrl | puste | `PackageLicenseUrl` jest przestarzałe, użyj właściwości PackageLicenseExpression lub PackageLicenseFile |
| ProjectUrl | PackageProjectUrl | puste | |
| Ikona | PackageIcon | puste | Należy jawnie spakować plik obrazu ikony, do którego istnieje odwołanie.|
| IconUrl | PackageIconUrl | puste | W przypadku najlepszego środowiska niskiego poziomu `PackageIconUrl` należy określić oprócz programu `PackageIcon` . Dłuższy termin, `PackageIconUrl` będzie przestarzały. |
| Tagi | PackageTags | puste | Tagi są rozdzielane średnikami. |
| ReleaseNotes | PackageReleaseNotes | puste | |
| Repozytorium/adres URL | RepositoryUrl | puste | Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego. Przyklad *https://github.com/NuGet/NuGet.Client.git* |
| Repozytorium/typ | Repozytorium | puste | Typ repozytorium. Przykłady: *git*i *TFS*. |
| Repozytorium/gałąź | RepositoryBranch | puste | Opcjonalne informacje o gałęzi repozytorium. Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* . Przykład: *Master* (NuGet 4.7.0 +) |
| Repozytorium/zatwierdzenie | RepositoryCommit | puste | Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet. Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* . Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Podsumowanie | Nieobsługiwane | | |

### <a name="pack-target-inputs"></a>docelowe dane wejściowe pakietu

- Ispacking
- SuppressDependenciesWhenPacking
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

Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet, ustaw opcję `SuppressDependenciesWhenPacking` na `true` , która będzie zezwalać na pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` zostanie zaniechane na korzyść nowej [`PackageIcon`](#packageicon) właściwości.

Począwszy od programu NuGet 5,3 & programu Visual Studio 2019 w wersji 16,3, `pack` program zwróci ostrzeżenie [NU5048](./errors-and-warnings/nu5048.md) , jeśli określi on tylko metadane pakietu `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Należy określić zarówno `PackageIcon` i, `PackageIconUrl` Aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które nie są jeszcze obsługiwane `PackageIcon` . Program Visual Studio będzie obsługiwał `PackageIcon` pakiety pochodzące ze źródła opartego na folderach w przyszłej wersji.

#### <a name="packing-an-icon-image-file"></a>Pakowanie pliku obrazu ikony

Podczas pakowania pliku obrazu ikony należy użyć `PackageIcon` właściwości, aby określić ścieżkę pakietu względem katalogu głównego pakietu. Ponadto należy się upewnić, że plik jest dołączony do pakietu. Rozmiar pliku obrazu jest ograniczony do 1 MB. Obsługiwane formaty plików to JPEG i PNG. Zalecamy rozdzielczość obrazu 128 x 128.

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

`nuget pack` Kopiuje pliki wyjściowe z rozszerzeniami,,,, `.exe` `.dll` `.xml` `.winmd` `.json` i `.pri` . Pliki wyjściowe, które są kopiowane, zależą od tego, co program MSBuild dostarcza z `BuiltOutputProjectGroup` elementu docelowego.

Istnieją dwie właściwości programu MSBuild, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie znajdują się zestawy wyjściowe:

- `IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być zawarte w pakiecie.
- `BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy wyjściowe. Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.

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

Aby dołączyć zawartość, Dodaj dodatkowe metadane do istniejącego `<Content>` elementu. Domyślnie wszystkie elementy typu "Content" są uwzględniane w pakiecie, chyba że przestąpisz do wpisów, takich jak następujące:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Domyślnie wszystko jest dodawane do katalogu głównego `content` `contentFiles\any\<target_framework>` folderu i w pakiecie i zachowuje względną strukturę folderów, chyba że zostanie określona ścieżka pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (a nie `content` `contentFiles` obu), możesz użyć właściwości programu MSBuild `ContentTargetFolders` , która jest wartością domyślną "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu. Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` umieszcza plików w obszarze `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction` .

`PackagePath` może to być rozdzielany średnikami zestaw ścieżek docelowych. Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu. Na przykład następujące polecenie dodaje `libuv.txt` do `content\myfiles` , `content\samples` i katalog główny pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Istnieje również właściwość programu MSBuild `$(IncludeContentInPack)` , której wartością domyślną jest `true` . Jeśli ta wartość jest ustawiona na `false` dla każdego projektu, zawartość z tego projektu nie jest dołączana do pakietu NuGet.

Inne metadane specyficzne dla pakietu, które można ustawić dla każdego z powyższych elementów, obejmują ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` które zestawy ```CopyToOutput``` i ```Flatten``` wartości ```contentFiles``` wpisu w danych wyjściowych nuspec.

> [!Note]
> Oprócz elementów zawartości `<Pack>` `<PackagePath>` można również ustawić metadane i dla plików z akcją kompilacji kompilowania, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.
>
> Aby pakiet mógł dołączyć nazwę pliku do ścieżki pakietu przy użyciu wzorców obsługi symboli wieloznacznych, ścieżka pakietu musi kończyć się znakiem separatora folderów. w przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka, w tym nazwa pliku.

### <a name="includesymbols"></a>IncludeSymbols

W przypadku korzystania z programu `MSBuild -t:pack -p:IncludeSymbols=true` odpowiednie `.pdb` pliki są kopiowane wraz z innymi plikami wyjściowymi ( `.dll` ,,,, `.exe` `.winmd` `.xml` `.json` , `.pri` ). Należy pamiętać, że ustawienie `IncludeSymbols=true` powoduje utworzenie regularnego pakietu *i* pakietu symboli.

### <a name="includesource"></a>IncludeSource

Jest to takie samo `IncludeSymbols` , jak, z tą różnicą, że kopiuje również pliki źródłowe wraz z `.pdb` plikami. Wszystkie pliki typu `Compile` są kopiowane za pośrednictwem `src\<ProjectName>\` , aby zachować strukturę folderu ścieżki względnej w pakietie będącym wynikiem. To samo występuje również dla plików źródłowych, `ProjectReference` które mają `TreatAsPackageReference` ustawioną wartość `false` .

Jeśli plik typu Kompiluj znajduje się poza folderem projektu, to właśnie został dodany do `src\<ProjectName>\` .

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

W przypadku korzystania z programu `MSBuild -t:pack -p:IsTool=true` wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , są kopiowane do `tools` folderu, a nie do `lib` folderu. Należy zauważyć, że różni się to od elementu, `DotNetCliTool` który jest określony przez ustawienie `PackageType` w `.csproj` pliku.

### <a name="packing-using-a-nuspec"></a>Pakowanie przy użyciu elementu. nuspec

Mimo że zaleca się [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu, można użyć `.nuspec` pliku do spakowania projektu. W przypadku projektu typu innego niż zestaw SDK, który używa programu `PackageReference` , należy go zaimportować, `NuGet.Build.Tasks.Pack.targets` Aby można było wykonać zadanie pakietu. Nadal trzeba przywrócić projekt, aby można było spakować plik NUSPEC. (Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).

Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania nuspec. Następujące trzy właściwości programu MSBuild dotyczą pakowania przy użyciu `.nuspec` :

1. `NuspecFile`: względna lub bezwzględna ścieżka do `.nuspec` pliku używanego do pakowania.
1. `NuspecProperties`: rozdzielana średnikami lista par klucz = wartość. Ze względu na sposób działania analizy wiersza polecenia programu MSBuild należy określić wiele właściwości w następujący sposób: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: Ścieżka podstawowa dla `.nuspec` pliku.

Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Jeśli używasz programu MSBuild do pakowania projektu, użyj następującego polecenia:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Należy pamiętać, że pakowanie nuspec przy użyciu dotnet.exe lub MSBuild również prowadzi do domyślnego kompilowania projektu. Można to uniknąć przez przekazanie ```--no-build``` właściwości do dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.

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

`pack`Element docelowy zawiera dwa punkty rozszerzenia, które są uruchamiane w wewnętrznej, docelowej kompilacji specyficznej dla platformy. Obsługa punktów rozszerzenia umożliwia uwzględnienie zawartości i zestawów określonych dla platformy docelowej w pakiecie:

- `TargetsForTfmSpecificBuildOutput` target: Użyj dla plików znajdujących się w `lib` folderze lub folderu określonego przy użyciu `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` target: Użyj dla plików poza `BuildOutputTargetFolder` .

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości. Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), obiekt docelowy powinien zapisać te pliki do obiektu Items `BuildOutputInPackage` i ustawić następujące dwie wartości metadanych:

- `FinalOutputPath`: Ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość służy do oszacowania ścieżki źródłowej.
- `TargetPath`: (Opcjonalnie) ustawia się, gdy plik musi przejść do podfolderu w `lib\<TargetFramework>` , podobnie jak zestawy satelickie, które przechodzą w odpowiednie foldery kultury. Wartością domyślną jest nazwa pliku.

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

Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości. Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki w obiekcie Items `TfmSpecificPackageFile` i ustawić następujące opcjonalne metadane:

- `PackagePath`: Ścieżka, w której plik powinien być wyprowadzany w pakiecie. Pakiet NuGet wystawia ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.
- `BuildAction`: Akcja kompilacji, która ma zostać przypisana do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w `contentFiles` folderze. Wartość domyślna to "none".

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

`MSBuild -t:restore` (które `nuget restore` `dotnet restore` są używane z projektami .NET Core), przywraca pakiety, do których odwołuje się plik projektu, w następujący sposób:

1. Odczytuj wszystkie odwołania projektu do projektu
1. Odczytywanie właściwości projektu w celu znalezienia pośredniego folderu i platform docelowych
1. Przekaż dane programu MSBuild do NuGet.Build.Tasks.dll
1. Uruchom przywracanie
1. Pobierz pakiety
1. Zapisz plik zasobów, cele i właściwości.

`restore`Obiekt docelowy działa **tylko** w przypadku projektów korzystających z formatu PackageReference. **Nie działa w** przypadku projektów przy użyciu `packages.config` formatu; zamiast tego należy użyć [przywracania NuGet](../reference/cli-reference/cli-ref-restore.md) .

### <a name="restore-properties"></a>Właściwości przywracania

Dodatkowe ustawienia przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu. Wartości można również ustawić z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).

| Właściwość | Opis |
|--------|--------|
| RestoreSources | Rozdzielana średnikami lista źródeł pakietów. |
| RestorePackagesPath | Ścieżka folderu pakietów użytkownika. |
| RestoreDisableParallel | Ogranicz pobieranie do jednej naraz. |
| RestoreConfigFile | Ścieżka do `Nuget.Config` pliku, który ma zostać zastosowany. |
| RestoreNoCache | Jeśli ma wartość true, unika używania buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów. |
| RestoreFallbackFolders | Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika. |
| RestoreAdditionalProjectSources | Dodatkowe źródła do użycia podczas przywracania. |
| RestoreAdditionalProjectFallbackFolders | Dodatkowe foldery rezerwowe do użycia podczas przywracania. |
| RestoreAdditionalProjectFallbackFoldersExcludes | Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Ścieżka do `NuGet.Build.Tasks.dll` . |
| RestoreGraphProjectInput | Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne. |
| RestoreUseSkipNonexistentTargets  | Gdy projekty są zbierane za pośrednictwem programu MSBuild, określa, czy są zbierane przy użyciu `SkipNonexistentTargets` optymalizacji. Gdy wartość nie jest ustawiona, wartością domyślną jest `true` . Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu. |
| MSBuildProjectExtensionsPath | Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` i `obj` folder. |
| RestoreForce | W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie. Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku. Nie powoduje to obejścia pamięci podręcznej protokołu HTTP. |
| RestorePackagesWithLockFile | Umożliwia użycie pliku blokady. |
| RestoreLockedMode | Uruchom przywracanie w trybie zablokowanym. Oznacza to, że przywracanie nie będzie obliczać zależności. |
| NuGetLockFilePath | Niestandardowa lokalizacja pliku blokady. Domyślna lokalizacja jest obok projektu i ma nazwę `packages.lock.json` . |
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

Instrukcja RESTORE tworzy następujące pliki w folderze Build `obj` :

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

Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build` .

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback`Element umożliwia określenie zestawu zgodnych elementów docelowych, które mają być używane podczas przywracania pakietów. Została zaprojektowana tak, aby zezwalać na pakiety, które używają [TxM](../reference/target-frameworks.md) dotnet, do pracy z zgodnymi pakietami, które nie deklarują TxM dotnet. Oznacza to, że jeśli w projekcie jest używany TxM dotnet, wszystkie pakiety, od których zależy, muszą także mieć TxM dotnet, chyba że zostanie dodany `<PackageTargetFallback>` do projektu w celu umożliwienia zgodności z platformą dotnet.

Na przykład jeśli projekt używa `netstandard1.6` TxM, a pakiet zależny zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll` , to projekt nie zostanie skompilowany. Jeśli co chcesz zrobić, jest to Ostatnia Biblioteka DLL, a następnie możesz dodać polecenie w `PackageTargetFallback` następujący sposób, aby powiedzieć, że `portable-net45+win81` Biblioteka DLL jest zgodna:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Aby zadeklarować rezerwę dla wszystkich obiektów docelowych w projekcie, pozostaw ten `Condition` atrybut. Możesz również rozłożyć wszystkie istniejące `PackageTargetFallback` , w tym `$(PackageTargetFallback)` tutaj, jak pokazano poniżej:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Zastępowanie jednej biblioteki na podstawie grafu przywracania

Jeśli przywracanie powoduje przełączenie niewłaściwego zestawu, możliwe jest wykluczenie domyślnego wyboru pakietów i zamienienie go na własny wybór. Najpierw `PackageReference` należy wykluczyć wszystkie elementy zawartości z najwyższego poziomu:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Następnie Dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
