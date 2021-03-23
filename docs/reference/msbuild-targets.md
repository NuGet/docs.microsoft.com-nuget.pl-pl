---
title: NuGet Pakowanie i przywracanie jako MSBuild elementy docelowe
description: NuGet Pakowanie i przywracanie może współdziałać bezpośrednio jako MSBuild elementy docelowe z NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858969"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet Pakowanie i przywracanie jako MSBuild elementy docelowe

*NuGet 4.0 +*

W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, a nie przy użyciu osobnego `.nuspec` pliku.

MSBuild15.1 +, NuGet jest również MSBuild obywatelem pierwszej klasy z `pack` i celami, zgodnie z `restore` poniższym opisem. Te elementy docelowe umożliwiają współdziałanie z NuGet innymi MSBuild zadaniami lub obiektami docelowymi. Aby uzyskać instrukcje tworzenia NuGet pakietu przy użyciu programu MSBuild , zobacz [Tworzenie NuGet pakietu MSBuild przy użyciu ](../create-packages/creating-a-package-msbuild.md). (W przypadku NuGet 3. x i starszych, zamiast tego należy użyć poleceń [pakowanie](../reference/cli-reference/cli-ref-pack.md) i [przywracanie](../reference/cli-reference/cli-ref-restore.md) za pomocą NuGet interfejsu wiersza polecenia.)

## <a name="target-build-order"></a>Kolejność kompilowania obiektów docelowych

Ponieważ `pack` i `restore` są  MSBuild obiektami docelowymi, można uzyskać do nich dostęp, aby usprawnić przepływ pracy. Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu. Można to zrobić, dodając następujący plik w pliku projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Podobnie można napisać MSBuild zadanie, napisać własne miejsce docelowe i użyć NuGet właściwości w MSBuild zadaniu.

> [!NOTE]
> `$(OutputPath)` jest względna i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.

## <a name="pack-target"></a>cel pakietu

W przypadku projektów platformy .NET korzystających z tego `PackageReference` formatu użycie `msbuild -t:pack` rysuje dane wejściowe z pliku projektu do użycia podczas tworzenia NuGet pakietu.

W poniższej tabeli opisano MSBuild właściwości, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle. Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym. Dla wygody tabela jest zorganizowana według równoważnej właściwości w [ `.nuspec` pliku](../reference/nuspec.md).

> [!NOTE]
> `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane w programie MSBuild .

| Atrybut/ nuspec wartość | MSBuild Wartość | Domyślne | Uwagi |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | `$(AssemblyName)` wniosek MSBuild |
| `Version` | `PackageVersion` | Wersja | Jest to zgodne z semver, na przykład, `1.0.0` `1.0.0-beta` lub `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | puste | Ustawianie `PackageVersion` zastępowanie `PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | puste | `$(VersionSuffix)` z programu MSBuild . Ustawianie `PackageVersion` zastępowanie `PackageVersionSuffix` |
| `Authors` | `Authors` | Nazwa_użytkownika bieżącego użytkownika | Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów w nuget.org. Są one wyświetlane w NuGet galerii w witrynie NuGet.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów. |
| `Owners` | Nie dotyczy | Nieobecne w nuspec | |
| `Title` | `Title` | Element `PackageId`. | Przyjazny dla człowieka tytuł pakietu, zazwyczaj używany w interfejsie użytkownika jako nuget.org i Menedżer pakietów w programie Visual Studio. |
| `Description` | `Description` | "Opis pakietu" | Długi opis zestawu. Jeśli `PackageDescription` nie jest określony, ta właściwość jest również używana jako Opis pakietu. |
| `Copyright` | `Copyright` | puste | Szczegóły dotyczące praw autorskich pakietu. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu. |
| `license` | `PackageLicenseExpression` | puste | Odnosi się do `<license type="expression">` . Zobacz [pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file). |
| `license` | `PackageLicenseFile` | puste | Ścieżka do pliku licencji w pakiecie w przypadku korzystania z licencji niestandardowej lub licencji, która nie ma przypisanego identyfikatora SPDX. Należy jawnie spakować plik licencji, do której istnieje odwołanie. Odnosi się do `<license type="file">` . Zobacz [pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file). |
| `LicenseUrl` | `PackageLicenseUrl` | puste | `PackageLicenseUrl` jest przestarzały. Użyj polecenia `PackageLicenseExpression` or `PackageLicenseFile` . |
| `ProjectUrl` | `PackageProjectUrl` | puste | |
| `Icon` | `PackageIcon` | puste | Ścieżka do obrazu w pakiecie do użycia jako ikona pakietu. Należy jawnie spakować plik obrazu ikony, do którego istnieje odwołanie. Aby uzyskać więcej informacji, zobacz [pakowanie pliku obrazu ikony](#packing-an-icon-image-file) i [ `icon` metadanych](/nuget/reference/nuspec#icon). |
| `IconUrl` | `PackageIconUrl` | puste | `PackageIconUrl` jest przestarzały `PackageIcon` . Jednak w przypadku najlepszego środowiska niskiego poziomu należy określić `PackageIconUrl` oprócz `PackageIcon` . |
| `Tags` | `PackageTags` | puste | Rozdzielana średnikami lista znaczników, które wyznaczają pakiet. |
| `ReleaseNotes` | `PackageReleaseNotes` | puste | Informacje o wersji pakietu. |
| `Repository/Url` | `RepositoryUrl` | puste | Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego. Przykład: *https://github.com/ NuGet / NuGet . Klient. git*. |
| `Repository/Type` | `RepositoryType` | puste | Typ repozytorium. Przykłady: `git` (domyślnie), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | puste | Opcjonalne informacje o gałęzi repozytorium. `RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona. Przykład: *Master* ( NuGet 4.7.0 +). |
| `Repository/Commit` | `RepositoryCommit` | puste | Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet. `RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona. Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | Nieobsługiwane | | |

### <a name="pack-target-inputs"></a>docelowe dane wejściowe pakietu

| Właściwość | Opis |
| - | - |
| `IsPackable` | Wartość logiczna określająca, czy projekt może być spakowany. Wartość domyślna to `true`. |
| `SuppressDependenciesWhenPacking` | Ustaw, aby `true` pominąć zależności pakietów z wygenerowanego NuGet pakietu. |
| `PackageVersion` | Określa wersję, która będzie miała pakiet otrzymany. Akceptuje wszystkie formy NuGet ciągu wersji. Wartość domyślna to `$(Version)` , czyli Właściwość `Version` w projekcie. |
| `PackageId` | Określa nazwę pakietu, który ma zostać utworzony. Jeśli nie zostanie określony, `pack` operacja będzie domyślnie używać `AssemblyName` nazwy katalogu jako nazwy pakietu. |
| `PackageDescription` | Długi opis pakietu do wyświetlania interfejsu użytkownika. |
| `Authors` | Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów w nuget.org. Są one wyświetlane w NuGet galerii w witrynie NuGet.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów. |
| `Description` | Długi opis zestawu. Jeśli `PackageDescription` nie jest określony, ta właściwość jest również używana jako Opis pakietu. |
| `Copyright` | Szczegóły dotyczące praw autorskich pakietu. |
| `PackageRequireLicenseAcceptance` | Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu. Wartość domyślna to `false`. |
| `DevelopmentDependency` | Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do programowania, który uniemożliwia dołączenie pakietu jako zależności w innych pakietach. W przypadku `PackageReference` ( NuGet 4.8 +) Ta flaga oznacza również, że zasoby czasu kompilacji są wyłączone z kompilacji. Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| `PackageLicenseExpression` | Identyfikator lub wyrażenie [licencji SPDX](https://spdx.org/licenses/) , na przykład `Apache-2.0` . Aby uzyskać więcej informacji, zobacz [pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file). |
| `PackageLicenseFile` | Ścieżka do pliku licencji w pakiecie w przypadku korzystania z licencji niestandardowej lub licencji, która nie ma przypisanego identyfikatora SPDX. |
| `PackageLicenseUrl` | `PackageLicenseUrl` jest przestarzały. Użyj polecenia `PackageLicenseExpression` or `PackageLicenseFile` . |
| `PackageProjectUrl` | |
| `PackageIcon` | Określa ścieżkę ikony pakietu względem katalogu głównego pakietu. Aby uzyskać więcej informacji, zobacz [pakowanie pliku obrazu ikony](#packing-an-icon-image-file). |
| `PackageReleaseNotes` | Informacje o wersji pakietu. |
| `PackageTags` | Rozdzielana średnikami lista znaczników, które wyznaczają pakiet. |
| `PackageOutputPath` | Określa ścieżkę wyjściową, w której zostanie usunięty spakowany pakiet. Wartość domyślna to `$(OutputPath)`. |
| `IncludeSymbols` | Ta wartość logiczna wskazuje, czy pakiet powinien utworzyć dodatkowy pakiet symboli podczas pakowania projektu. Format pakietu symboli jest kontrolowany przez `SymbolPackageFormat` Właściwość. Aby uzyskać więcej informacji, zobacz [IncludeSymbols](#includesymbols). |
| `IncludeSource` | Ta wartość logiczna wskazuje, czy proces pakietu powinien utworzyć pakiet źródłowy. Pakiet źródłowy zawiera kod źródłowy biblioteki, a także pliki PDB. Pliki źródłowe są umieszczane w `src/ProjectName` katalogu w pliku pakietu, który został utworzony. Aby uzyskać więcej informacji, zobacz [IncludeSource](#includesource). |
| `PackageType` | |
| `IsTool` | Określa, czy wszystkie pliki wyjściowe są kopiowane do folderu *Tools* zamiast folderu *lib* . Aby uzyskać więcej informacji, zobacz [istool](#istool). |
| `RepositoryUrl` | Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego. Przykład: *https://github.com/ NuGet / NuGet . Klient. git*. |
| `RepositoryType` | Typ repozytorium. Przykłady: `git` (domyślnie), `tfs` . |
| `RepositoryBranch` | Opcjonalne informacje o gałęzi repozytorium. `RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona. Przykład: *Master* ( NuGet 4.7.0 +). |
| `RepositoryCommit` | Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet. `RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona. Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `SymbolPackageFormat` | Określa format pakietu symboli. W przypadku wystąpienia "Symbols. nupkg" jest tworzony pakiet starszych symboli z rozszerzeniem *. Symbols. nupkg* zawierającym plików PDB, DLL i inne pliki wyjściowe. W przypadku "snupkg" tworzony jest pakiet symboli snupkg zawierający przenośne plików PDB. Wartość domyślna to "Symbols. nupkg". |
| `NoPackageAnalysis` | Określa, że `pack` nie należy uruchamiać analizy pakietu po skompilowaniu pakietu. |
| `MinClientVersion` | Określa minimalną wersję klienta, NuGet który może zainstalować ten pakiet, wymuszony przez nuget.exe i Menedżera pakietów programu Visual Studio. |
| `IncludeBuildOutput` | Ta wartość logiczna określa, czy zestawy danych wyjściowych kompilacji powinny być pakowane do pliku *. nupkg* , czy nie. |
| `IncludeContentInPack` | Ta wartość logiczna określa, czy wszystkie elementy, które mają typ `Content` są zawarte w pakiecie, są automatycznie uwzględniane. Wartość domyślna to `true`. |
| `BuildOutputTargetFolder` | Określa folder, w którym mają zostać umieszczone zestawy wyjściowe. Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury. Aby uzyskać więcej informacji, zobacz [zestawy danych wyjściowych](#output-assemblies). |
| `ContentTargetFolders` | Określa domyślną lokalizację, w której należy wykonać wszystkie pliki zawartości, jeśli `PackagePath` nie została określona dla nich. Wartość domyślna to "Content; contentFiles". Aby uzyskać więcej informacji, zobacz temat [uwzględnianie zawartości w pakiecie](#including-content-in-a-package). |
| `NuspecFile` | Względna lub bezwzględna ścieżka do *.nuspec* pliku używanego do pakowania. Jeśli ta wartość jest określona, jest używana **wyłącznie** na potrzeby informacji o pakowaniu, a wszelkie informacje w projektach nie są używane. Aby uzyskać więcej informacji, zobacz [pakowanie przy .nuspec użyciu a ](#packing-using-a-nuspec-file). |
| `NuspecBasePath` | Podstawowa ścieżka do *.nuspec* pliku. Aby uzyskać więcej informacji, zobacz [pakowanie przy .nuspec użyciu a ](#packing-using-a-nuspec-file). |
| `NuspecProperties` | Rozdzielana średnikami lista par klucz = wartość. Aby uzyskać więcej informacji, zobacz [pakowanie przy .nuspec użyciu a ](#packing-using-a-nuspec-file). |

## <a name="pack-scenarios"></a>scenariusze dotyczące pakietów

### <a name="suppressing-dependencies"></a>Pomijanie zależności

Aby pominąć zależności pakietów z wygenerowanego NuGet pakietu, ustaw opcję `SuppressDependenciesWhenPacking` na `true` , która zezwoli na pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.

### `PackageIconUrl`

`PackageIconUrl` jest przestarzałe na rzecz [`PackageIcon`](#packageicon) właściwości. Począwszy od NuGet 5,3 i programu Visual Studio 2019 w wersji 16,3, program `pack` wywołuje ostrzeżenie [NU5048](./errors-and-warnings/nu5048.md) , jeśli tylko metadane pakietu są określone `PackageIconUrl` .

### `PackageIcon`

> [!Tip]
> Aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które jeszcze nie obsługują `PackageIcon` , określ zarówno, `PackageIcon` jak i `PackageIconUrl` . Program Visual Studio obsługuje `PackageIcon` pakiety pochodzące ze źródła opartego na folderach.

#### <a name="packing-an-icon-image-file"></a>Pakowanie pliku obrazu ikony

Podczas pakowania pliku obrazu ikony Użyj właściwości, `PackageIcon` Aby określić ścieżkę pliku ikony względem katalogu głównego pakietu. Ponadto upewnij się, że plik jest dołączony do pakietu. Rozmiar pliku obrazu jest ograniczony do 1 MB. Obsługiwane formaty plików to JPEG i PNG. Zalecamy rozdzielczość obrazu 128 x 128.

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

[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/main/PackageIconExample).

Aby uzyskać nuspec odpowiedni odpowiednik, zapoznaj się z [ nuspec odwołaniem do ikony](nuspec.md#icon).

### <a name="output-assemblies"></a>Zestawy wyjściowe

`nuget pack` Kopiuje pliki wyjściowe z rozszerzeniami,,,, `.exe` `.dll` `.xml` `.winmd` `.json` i `.pri` . Kopiowane pliki wyjściowe zależą od tego, co jest MSBuild dostępne w `BuiltOutputProjectGroup` miejscu docelowym.

Istnieją dwie MSBuild  właściwości, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie są dostępne zestawy wyjściowe:

- `IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być zawarte w pakiecie.
- `BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy wyjściowe. Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.

### <a name="package-references"></a>Odwołania do pakietu

Zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Odwołania projektu do projektu

Odwołania do projektu są uwzględniane domyślnie jako NuGet odwołania do pakietu. Na przykład:

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

Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (a nie `content` `contentFiles` obu), możesz użyć MSBuild właściwości `ContentTargetFolders` , która domyślnie przyjmuje wartość "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu. Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` umieszcza plików w obszarze `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction` .

`PackagePath` może to być rozdzielany średnikami zestaw ścieżek docelowych. Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu. Na przykład następujące polecenie dodaje `libuv.txt` do `content\myfiles` , `content\samples` i katalog główny pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Istnieje również MSBuild Właściwość `$(IncludeContentInPack)` , której wartością domyślną jest `true` . Jeśli ta wartość jest ustawiona na `false` dla każdego projektu, zawartość z tego projektu nie jest dołączana do pakietu NuGet.

Inne metadane specyficzne dla pakietu, które można ustawić dla każdego z powyższych elementów, obejmują ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` które zestawy ```CopyToOutput``` i ```Flatten``` wartości ```contentFiles``` wpisu w danych wyjściowych nuspec .

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

W przypadku korzystania z wyrażenia licencji Użyj `PackageLicenseExpression` właściwości. Aby uzyskać przykład, zobacz [przykładowe wyrażenie licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Aby dowiedzieć się więcej na temat wyrażeń licencji i licencji akceptowanych przez NuGet program. org, zobacz [metadane licencji](nuspec.md#license).

Podczas pakowania pliku licencji Użyj właściwości, `PackageLicenseFile` Aby określić ścieżkę pakietu względem katalogu głównego pakietu. Ponadto upewnij się, że plik jest dołączony do pakietu. Na przykład:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Aby uzyskać przykład, zobacz [przykład pliku licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).

> [!NOTE]
> Tylko jeden z `PackageLicenseExpression` , `PackageLicenseFile` i `PackageLicenseUrl` można określić w danym momencie.

### <a name="packing-a-file-without-an-extension"></a>Pakowanie pliku bez rozszerzenia

W niektórych scenariuszach, takich jak podczas pakowania pliku licencji, może być konieczne dołączenie pliku bez rozszerzenia.
Z przyczyn historycznych NuGet  &  MSBuild Traktuj ścieżki bez rozszerzenia jako katalogów.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Plik bez rozszerzenia](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).

### <a name="istool"></a>Istool

W przypadku korzystania z programu `MSBuild -t:pack -p:IsTool=true` wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , są kopiowane do `tools` folderu, a nie do `lib` folderu. Należy zauważyć, że różni się to od elementu, `DotNetCliTool` który jest określony przez ustawienie `PackageType` w `.csproj` pliku.

### <a name="packing-using-a-nuspec-file"></a>Pakowanie przy użyciu `.nuspec` pliku

Mimo że zaleca się [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu, można użyć `.nuspec` pliku do spakowania projektu. W przypadku projektu typu innego niż zestaw SDK, który używa programu `PackageReference` , należy go zaimportować, `NuGet.Build.Tasks.Pack.targets` Aby można było wykonać zadanie pakietu. Nadal trzeba przywrócić projekt, aby można było spakować nuspec plik. (Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).

Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania a nuspec . Następujące trzy MSBuild właściwości są istotne dla pakowania przy użyciu `.nuspec` :

1. `NuspecFile`: względna lub bezwzględna ścieżka do `.nuspec` pliku używanego do pakowania.
1. `NuspecProperties`: rozdzielana średnikami lista par klucz = wartość. Ze względu na sposób MSBuild działania analizy wiersza polecenia należy określić wiele właściwości w następujący sposób: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: Ścieżka podstawowa dla `.nuspec` pliku.

Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Jeśli używasz MSBuild do pakowania projektu, użyj następującego polecenia:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Należy pamiętać, że pakowanie a nuspec using dotnet.exe lub MSBuild również prowadzi do domyślnego kompilowania projektu. Można to uniknąć przez przekazanie ```--no-build``` właściwości do dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.

Przykład pliku *. csproj* do spakowania nuspec pliku:

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

#### `TargetsForTfmSpecificBuildOutput`

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

#### `TargetsForTfmSpecificContentInPackage`

Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości. Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki w obiekcie Items `TfmSpecificPackageFile` i ustawić następujące opcjonalne metadane:

- `PackagePath`: Ścieżka, w której plik powinien być wyprowadzany w pakiecie. NuGet wyświetla ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.
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
1. Przekaż MSBuild dane do NuGet.Build.Tasks.dll
1. Uruchom przywracanie
1. Pobierz pakiety
1. Zapisz plik zasobów, cele i właściwości.

`restore`Obiekt docelowy działa dla projektów przy użyciu formatu PackageReference.
`MSBuild 16.5+` Ponadto zapewnia [obsługę](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) tego `packages.config` formatu.

> [!NOTE]
> `restore`Element docelowy [nie powinien być uruchamiany](#restoring-and-building-with-one-msbuild-command) w połączeniu z `build` elementem docelowym.

### <a name="restore-properties"></a>Właściwości przywracania

Dodatkowe ustawienia przywracania mogą pochodzić z MSBuild właściwości w pliku projektu. Wartości można również ustawić z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).

| Właściwość | Opis |
|--------|--------|
| `RestoreSources` | Rozdzielana średnikami lista źródeł pakietów. |
| `RestorePackagesPath` | Ścieżka folderu pakietów użytkownika. |
| `RestoreDisableParallel` | Ogranicz pobieranie do jednej naraz. |
| `RestoreConfigFile` | Ścieżka do `Nuget.Config` pliku, który ma zostać zastosowany. |
| `RestoreNoCache` | Jeśli ma wartość true, unika używania buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| `RestoreIgnoreFailedSources` | W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów. |
| `RestoreFallbackFolders` | Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika. |
| `RestoreAdditionalProjectSources` | Dodatkowe źródła do użycia podczas przywracania. |
| `RestoreAdditionalProjectFallbackFolders` | Dodatkowe foldery rezerwowe do użycia podczas przywracania. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | Ścieżka do `NuGet.Build.Tasks.dll` . |
| `RestoreGraphProjectInput` | Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne. |
| `RestoreUseSkipNonexistentTargets`  | Gdy projekty są zbierane za pośrednictwem, MSBuild określają, czy są zbierane przy użyciu `SkipNonexistentTargets` optymalizacji. Gdy wartość nie jest ustawiona, wartością domyślną jest `true` . Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu. |
| `MSBuildProjectExtensionsPath` | Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` i `obj` folder. |
| `RestoreForce` | W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie. Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku. Nie powoduje to obejścia pamięci podręcznej protokołu HTTP. |
| `RestorePackagesWithLockFile` | Umożliwia użycie pliku blokady. |
| `RestoreLockedMode` | Uruchom przywracanie w trybie zablokowanym. Oznacza to, że przywracanie nie będzie obliczać zależności. |
| `NuGetLockFilePath` | Niestandardowa lokalizacja pliku blokady. Domyślna lokalizacja jest obok projektu i ma nazwę `packages.lock.json` . |
| `RestoreForceEvaluate` | Wymusza ponowne obliczenie zależności przez Przywracanie i zaktualizowanie pliku blokady bez ostrzeżenia. |
| `RestorePackagesConfig` | Opcjonalny przełącznik, który przywraca projekty z packages.config. Obsługa `MSBuild -t:restore` wyłącznie. |
| `RestoreUseStaticGraphEvaluation` | Opcjonalny przełącznik służący do użycia oceny wykresu statycznego MSBuild zamiast standardowej oceny. Obliczanie wykresu statycznego to eksperymentalna funkcja, która jest znacznie szybsza w przypadku dużych repozytoriów i rozwiązań. |

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
| `{projectName}.projectFileExtension.nuget.g.props` | Odwołania do MSBuild Właściwości props zawartych w pakietach |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odwołania do MSBuild elementów docelowych zawartych w pakietach |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Przywracanie i kompilowanie za pomocą jednego MSBuild polecenia

Ze względu na fakt, że NuGet można przywrócić pakiety, które wyłączają MSBuild elementy docelowe i wartościowe, oceny przywracania i kompilacji są uruchamiane z różnymi właściwościami globalnymi.
Oznacza to, że następujące elementy będą miały nieprzewidywalne i często nieprawidłowe zachowanie.

```cli
msbuild -t:restore,build
```

 Zamiast tego zalecane podejście to:

```cli
msbuild -t:build -restore
```

Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build` .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>Przywracanie projektów PackageReference i packages.config za pomocą MSBuild

W przypadku programu MSBuild 16.5 + packages.config są również obsługiwane w programie `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` Przywracanie jest dostępne `MSBuild 16.5+` tylko z `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Przywracanie za pomocą MSBuild obliczenia wykresu statycznego

> [!NOTE]
> Program MSBuild 16.6 +, NuGet dodał funkcję eksperymentalną do użycia obliczeń wykresu statycznego z wiersza polecenia, który znacznie skraca czas przywracania dla dużych repozytoriów.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Alternatywnie możesz ją włączyć, ustawiając właściwość w katalogu. Build. props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Począwszy od programu Visual Studio 2019. x i NuGet 5. x, ta funkcja jest uznawana za eksperymentalną i niezależną. Aby uzyskać szczegółowe informacje o tym, kiedy ta funkcja zostanie włączona domyślnie, obserwuj [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) .

Statyczne przywracanie wykresu zmienia część programu MSBuild przywracania, odczytywanie i ocenianie projektu, ale nie algorytmem przywracania. Algorytm przywracania jest taki sam dla wszystkich NuGet narzędzi ( NuGet exe, MSBuild exe, dotnet.exe i Visual Studio).

W bardzo kilku scenariuszach statyczne przywracanie wykresu może zachowywać się inaczej niż bieżące przywracanie, a niektóre zadeklarowane składnika packagereferences lub zawierających mogą być niedostępne.

Aby ułatwić sobie zdanie, podczas migracji do przywracania wykresu statycznego należy wziąć pod uwagę następujące działania:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet*nie* należy zgłaszać żadnych zmian. Jeśli widzisz Niezgodność, zrób problem pod adresem [ NuGet /Home](https://github.com/nuget/home/issues/new).

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
