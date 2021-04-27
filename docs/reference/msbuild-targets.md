---
title: NuGet spakuj i przywróć jako MSBuild obiekty docelowe
description: NuGet Pakiet i przywracanie mogą działać bezpośrednio jako MSBuild obiekty docelowe w ponad NuGet 4.0.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067313"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet spakuj i przywróć jako MSBuild obiekty docelowe

*NuGet 4.0+*

W [formacie PackageReference](../consume-packages/package-references-in-project-files.md) program 4.0+ może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, NuGet zamiast używać oddzielnego `.nuspec` pliku.

W przypadku programu 15.1+ jest również pierwszoklasowym obywatelem z celami i , MSBuild NuGet jak MSBuild `pack` `restore` opisano poniżej. Te obiekty docelowe umożliwiają pracę z usługą tak NuGet jak z innymi zadaniami lub MSBuild obiektami docelowymi. Aby uzyskać instrukcje NuGet dotyczące tworzenia pakietu przy użyciu polecenia , zobacz Tworzenie pakietu przy użyciu MSBuild [ NuGet polecenia MSBuild ](../create-packages/creating-a-package-msbuild.md). (W przypadku NuGet W wersji 3.x lub starszej zamiast tego należy użyć poleceń [pakowania](../reference/cli-reference/cli-ref-pack.md) [i](../reference/cli-reference/cli-ref-restore.md) przywracania za pośrednictwem interfejsu NuGet wiersza polecenia).

## <a name="target-build-order"></a>Kolejność kompilowania obiektów docelowych

Ponieważ `pack` i `restore` są  MSBuild celami, możesz uzyskać do nich dostęp, aby ulepszyć przepływ pracy. Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu. Możesz to zrobić, dodając następujące elementy w pliku projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Podobnie można napisać MSBuild zadanie, napisać własny element docelowy i korzystać z właściwości w NuGet MSBuild zadaniu.

> [!NOTE]
> `$(OutputPath)` jest względny i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.

## <a name="pack-target"></a>element docelowy pakietu

W przypadku projektów .NET, które używają formatu , przy użyciu rysuje dane wejściowe z pliku projektu do `PackageReference` `msbuild -t:pack` użycia podczas tworzenia NuGet pakietu.

W poniższej tabeli MSBuild opisano właściwości, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle. Te zmiany można łatwo wprowadzić w programie Visual Studio 2017 lub nowszym, klikając prawym przyciskiem myszy projekt i wybierając pozycję Edytuj **{project_name}** w menu kontekstowym. Dla wygody tabela jest zorganizowana według równoważnej właściwości w [ `.nuspec` pliku](../reference/nuspec.md).

> [!NOTE]
> `Owners` Właściwości `Summary` i z nie są obsługiwane w `.nuspec` programie MSBuild .

| nuspecAtrybut/wartość | MSBuild Właściwość | Domyślne | Uwagi |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | `$(AssemblyName)` Z MSBuild |
| `Version` | `PackageVersion` | Wersja | Jest to zgodne z semver, na przykład `1.0.0` `1.0.0-beta` , lub `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | puste | Zastępowanie `PackageVersion` ustawień `PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | puste | `$(VersionSuffix)` z MSBuild . Zastępowanie `PackageVersion` ustawień `PackageVersionSuffix` |
| `Authors` | `Authors` | Nazwa użytkownika bieżącego użytkownika | Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów na nuget.org. Są one wyświetlane w galerii na nuget.org i są używane do odsyłania pakietów NuGet przez tych samych autorów. |
| `Owners` | Nie dotyczy | Nie ma w nuspec | |
| `Title` | `Title` | Element `PackageId`. | Przyjazny dla człowieka tytuł pakietu, zwykle używany w interfejsie użytkownika, jest wyświetlany jako nuget.org i Menedżer pakietów w Visual Studio. |
| `Description` | `Description` | "Opis pakietu" | Długi opis zestawu. Jeśli nie zostanie określony, ta właściwość jest również używana `PackageDescription` jako opis pakietu. |
| `Copyright` | `Copyright` | puste | Szczegóły praw autorskich dla pakietu. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu. |
| `license` | `PackageLicenseExpression` | puste | Odpowiada `<license type="expression">` . Zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file). |
| `license` | `PackageLicenseFile` | puste | Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji niestandardowej lub licencji, do których nie przypisano identyfikatora SPDX. Musisz jawnie spakować plik licencji, do których się odwołujesz. Odpowiada `<license type="file">` . Zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file). |
| `LicenseUrl` | `PackageLicenseUrl` | puste | `PackageLicenseUrl` jest przestarzała. Zamiast `PackageLicenseExpression` tego użyj lub `PackageLicenseFile` . |
| `ProjectUrl` | `PackageProjectUrl` | puste | |
| `Icon` | `PackageIcon` | puste | Ścieżka do obrazu w pakiecie do użycia jako ikona pakietu. Musisz jawnie spakować plik obrazu ikony, do których się odwołujesz. Aby uzyskać więcej informacji, zobacz [Pakowanie pliku obrazu ikony i](#packing-an-icon-image-file) [ `icon` metadanych](./nuspec.md#icon). |
| `IconUrl` | `PackageIconUrl` | puste | `PackageIconUrl` jest przestarzała na rzecz `PackageIcon` . Jednak aby uzyskać najlepsze środowisko na 1. łydce, oprócz wartości należy `PackageIconUrl` określić wartość `PackageIcon` . |
| `Readme` | `PackageReadmeFile` | puste | Należy jawnie spakować przywołyowany plik readme.|
| `Tags` | `PackageTags` | puste | Rozdzielana średnikami lista tagów, która wyznacza pakiet. |
| `ReleaseNotes` | `PackageReleaseNotes` | puste | Informacje o wersji pakietu. |
| `Repository/Url` | `RepositoryUrl` | puste | Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego. Przykład: *https://github.com/ NuGet / NuGet . Client.git*. |
| `Repository/Type` | `RepositoryType` | puste | Typ repozytorium. Przykłady: `git` (ustawienie domyślne), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | puste | Opcjonalne informacje o gałęzi repozytorium. `RepositoryUrl` Należy również określić dla tej właściwości, która ma zostać uwzględniona. Przykład: *master* NuGet (4.7.0+). |
| `Repository/Commit` | `RepositoryCommit` | puste | Opcjonalne zatwierdzenie repozytorium lub zestaw zmian w celu wskazania źródła, z którego został s zbudowany pakiet. `RepositoryUrl` Należy również określić dla tej właściwości do dołączona. Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | Wskazuje przeznaczenie pakietu. Typy pakietów używają tego samego formatu co identyfikatory pakietów i są rozdzielane znakiem `;` . Typy pakietów mogą być wersjonarowane przez dołączenie `,` ciągu [`Version`](/dotnet/api/system.version) i . Zobacz [Ustawianie NuGet typu pakietu](../create-packages/set-package-type.md) ( NuGet 3.5.0+). |
| `Summary` | Nieobsługiwane | | |

### <a name="pack-target-inputs"></a>docelowe dane wejściowe pakietu

| Właściwość | Opis |
| - | - |
| `IsPackable` | Wartość logiczna określająca, czy można spakować projekt. Wartość domyślna to `true`. |
| `SuppressDependenciesWhenPacking` | Ustaw na `true` , aby pominąć zależności pakietu z wygenerowanego NuGet pakietu. |
| `PackageVersion` | Określa wersję pakietu wynikowego. Akceptuje wszystkie formy ciągu NuGet wersji. Wartość domyślna to wartość , czyli właściwości `$(Version)` `Version` w projekcie. |
| `PackageId` | Określa nazwę pakietu wynikowego. Jeśli nie zostanie określony, `pack` operacja domyślnie będzie używać nazwy katalogu lub jako nazwy `AssemblyName` pakietu. |
| `PackageDescription` | Długi opis pakietu dla wyświetlania interfejsu użytkownika. |
| `Authors` | Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów na nuget.org. Są one wyświetlane w galerii na nuget.org i są używane do odsyłania pakietów NuGet przez tych samych autorów. |
| `Description` | Długi opis zestawu. Jeśli nie zostanie określony, ta właściwość jest również używana `PackageDescription` jako opis pakietu. |
| `Copyright` | Szczegóły praw autorskich dla pakietu. |
| `PackageRequireLicenseAcceptance` | Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu. Wartość domyślna to `false`. |
| `DevelopmentDependency` | Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w innych pakietach. W `PackageReference` przypadku programu (4.8+) ta flaga oznacza również, że zasoby w czasie kompilacji NuGet są wykluczone z kompilacji. Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference (Obsługa](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)zależności development dla packageReference). |
| `PackageLicenseExpression` | Identyfikator [licencji SPDX](https://spdx.org/licenses/) lub wyrażenie, na przykład `Apache-2.0` . Aby uzyskać więcej informacji, zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file). |
| `PackageLicenseFile` | Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji niestandardowej lub licencji, która nie ma przypisanego identyfikatora SPDX. |
| `PackageLicenseUrl` | `PackageLicenseUrl` jest przestarzała. Zamiast `PackageLicenseExpression` tego użyj lub `PackageLicenseFile` . |
| `PackageProjectUrl` | |
| `PackageIcon` | Określa ścieżkę ikony pakietu względem katalogu głównego pakietu. Aby uzyskać więcej informacji, zobacz [Pakowanie pliku obrazu ikony](#packing-an-icon-image-file). |
| `PackageReleaseNotes` | Informacje o wersji pakietu. |
| `PackageReadmeFile` | Readme dla pakietu. |
| `PackageTags` | Rozdzielana średnikami lista tagów, która wyznacza pakiet. |
| `PackageOutputPath` | Określa ścieżkę wyjściową, w której spakowany pakiet zostanie porzucony. Wartość domyślna to `$(OutputPath)`. |
| `IncludeSymbols` | Ta wartość logiczna wskazuje, czy pakiet powinien utworzyć dodatkowy pakiet symboli podczas pakowania projektu. Format pakietu symboli jest kontrolowany przez `SymbolPackageFormat` właściwość . Aby uzyskać więcej informacji, zobacz [IncludeSymbols](#includesymbols). |
| `IncludeSource` | Ta wartość logiczna wskazuje, czy proces pakietu powinien utworzyć pakiet źródłowy. Pakiet źródłowy zawiera kod źródłowy biblioteki, a także pliki PDB. Pliki źródłowe są umieszczane `src/ProjectName` w katalogu w wynikowym pliku pakietu. Aby uzyskać więcej informacji, zobacz [IncludeSource](#includesource). |
| `PackageType` | |
| `IsTool` | Określa, czy wszystkie pliki wyjściowe są kopiowane do folderu *tools,* a nie do *folderu lib.* Aby uzyskać więcej informacji, zobacz [IsTool](#istool). |
| `RepositoryUrl` | Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego. Przykład: *https://github.com/ NuGet / NuGet . Client.git*. |
| `RepositoryType` | Typ repozytorium. Przykłady: `git` (ustawienie domyślne), `tfs` . |
| `RepositoryBranch` | Opcjonalne informacje o gałęzi repozytorium. `RepositoryUrl` Należy również określić dla tej właściwości do dołączona. Przykład: *master* NuGet (4.7.0+). |
| `RepositoryCommit` | Opcjonalne zatwierdzenie repozytorium lub zestaw zmian w celu wskazania źródła, z którego został s zbudowany pakiet. `RepositoryUrl` Należy również określić dla tej właściwości do dołączona. Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `SymbolPackageFormat` | Określa format pakietu symboli. W przypadku pliku "symbols.nupkg" starszy pakiet symboli jest tworzony z rozszerzeniem *.symbols.nupkg* zawierającym pliki PDB, DLL i inne pliki wyjściowe. W przypadku polecenia "snupkg" tworzony jest pakiet symboli snupkg zawierający przenośne pliki PDB. Wartość domyślna to "symbols.nupkg". |
| `NoPackageAnalysis` | Określa, `pack` że nie należy uruchamiać analizy pakietu po sbudowania pakietu. |
| `MinClientVersion` | Określa minimalną wersję klienta, który może zainstalować ten pakiet, wymuszaną przez nuget.exe NuGet i Visual Studio Menedżer pakietów. |
| `IncludeBuildOutput` | Ta wartość logiczna określa, czy zestawy wyjściowe kompilacji powinny być spakowane w pliku *nupkg,* czy nie. |
| `IncludeContentInPack` | Ta wartość logiczna określa, czy jakiekolwiek elementy, które mają typ , są automatycznie uwzględniane `Content` w wynikowym pakiecie. Wartość domyślna to `true`. |
| `BuildOutputTargetFolder` | Określa folder, w którym mają być umieszczane zestawy wyjściowe. Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury. Aby uzyskać więcej informacji, zobacz [Output assemblies (Zestawy wyjściowe).](#output-assemblies) |
| `ContentTargetFolders` | Określa domyślną lokalizację, w której powinny przejść wszystkie pliki zawartości, jeśli `PackagePath` nie zostanie określona dla nich. Wartość domyślna to "content;contentFiles". Aby uzyskać więcej informacji, zobacz [Including content in a package](#including-content-in-a-package). |
| `NuspecFile` | Względna lub bezwzględna ścieżka *.nuspec* do pliku używanego do pakowania. Jeśli to określono, są używane **wyłącznie do pakowania** informacji, a żadne informacje w projektach nie są używane. Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file) |
| `NuspecBasePath` | Ścieżka podstawowa *.nuspec* pliku. Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file) |
| `NuspecProperties` | Rozdzielana średnikami lista par klucz=wartość. Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file) |

## <a name="pack-scenarios"></a>scenariusze pakietu

### <a name="suppressing-dependencies"></a>Pomijanie zależności

Aby pominąć zależności pakietu z wygenerowanego pakietu, ustaw wartość , aby umożliwić pominięcie wszystkich zależności z wygenerowanego NuGet `SuppressDependenciesWhenPacking` pliku `true` nupkg.

### `PackageIconUrl`

`PackageIconUrl` jest przestarzała na rzecz [`PackageIcon`](#packageicon) właściwości . Począwszy od NuGet wersji 5.3 i Visual Studio 2019 w wersji 16.3, program zgłasza ostrzeżenie `pack` [NU5048,](./errors-and-warnings/nu5048.md) jeśli metadane pakietu określają tylko wartość `PackageIconUrl` .

### `PackageIcon`

> [!Tip]
> Aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które nie obsługują jeszcze `PackageIcon` usługi , określ wartości i `PackageIcon` `PackageIconUrl` . Visual Studio obsługuje `PackageIcon` pakiety pochodzące ze źródła opartego na folderach.

#### <a name="packing-an-icon-image-file"></a>Pakowanie pliku obrazu ikony

Podczas pakowania pliku obrazu ikony użyj właściwości , aby określić ścieżkę pliku ikony względem katalogu `PackageIcon` głównego pakietu. Ponadto upewnij się, że plik znajduje się w pakiecie . Rozmiar pliku obrazu jest ograniczony do 1 MB. Obsługiwane formaty plików to JPEG i PNG. Zalecamy rozdzielczość obrazu 128 x 128.

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

Aby uzyskać odpowiednik, zobacz odwołanie do nuspec [ nuspec ikony](nuspec.md#icon).

### <a name="packagereadmefile"></a>PackageReadmeFile

*Obsługiwane w **NuGet wersji 5.10.0 (wersja zapoznawcza 2)**  /  **zestawu .NET SDK 5.0.300** i jego wersjach*

Podczas pakowania pliku readme należy użyć właściwości , aby określić ścieżkę pakietu względem katalogu `PackageReadmeFile` głównego pakietu. Oprócz tego należy się upewnić, że plik znajduje się w pakiecie . Obsługiwane formaty plików obejmują tylko markdown *(md).*

Na przykład:

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

Aby uzyskać nuspec odpowiednik, zapoznaj się z odwołaniem [ nuspec do readme](nuspec.md#readme).

### <a name="output-assemblies"></a>Zestawy wyjściowe

`nuget pack` Kopiuje pliki wyjściowe z `.exe` rozszerzeniami `.dll` , , , , i `.xml` `.winmd` `.json` `.pri` . Kopiowane pliki wyjściowe zależą od tego, MSBuild co zapewnia obiekt `BuiltOutputProjectGroup` docelowy.

Istnieją dwie właściwości, których można użyć w pliku projektu lub wierszu polecenia, aby kontrolować, MSBuild  gdzie trafiają zestawy wyjściowe:

- `IncludeBuildOutput`: wartość logiczna, która określa, czy zestawy wyjściowe kompilacji powinny być zawarte w pakiecie.
- `BuildOutputTargetFolder`: określa folder, w którym powinny zostać umieszczone zestawy wyjściowe. Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.

### <a name="package-references"></a>Odwołania do pakietu

Zobacz [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Odwołania projektu do projektu

Odwołania projektu do projektu są domyślnie traktowane jako odwołania NuGet do pakietu. Na przykład:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Możesz również dodać następujące metadane do odwołania do projektu:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Łącznie z zawartością w pakiecie

Aby dołączyć zawartość, dodaj dodatkowe metadane do istniejącego `<Content>` elementu. Domyślnie wszystko typu "Zawartość" jest uwzględniane w pakiecie, chyba że zastąpisz wpisami podobnymi do następujących:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Domyślnie wszystko jest dodawane do katalogu głównego folderu i w pakiecie i zachowuje względną strukturę folderów, chyba że określisz `content` `contentFiles\any\<target_framework>` ścieżkę pakietu:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (zamiast i obu), możesz użyć właściwości , która domyślnie ma wartość `content` `contentFiles` MSBuild "content;contentFiles", ale może być ustawiona na inne `ContentTargetFolders` nazwy folderów. Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` pliku umieszcza pliki w obszarze lub na podstawie `contentFiles\any\<target_framework>` `contentFiles\<language>\<target_framework>` `buildAction` .

`PackagePath` może być rozdzielany średnikami zestaw ścieżek docelowych. Określenie pustej ścieżki pakietu doda plik do katalogu głównego pakietu. Na przykład następujący kod dodaje `libuv.txt` do , i główny `content\myfiles` `content\samples` pakiet:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Istnieje również właściwość MSBuild , która domyślnie ma wartość `$(IncludeContentInPack)` `true` . Jeśli jest ona ustawiona na wartość w dowolnym projekcie, zawartość z tego projektu nie zostanie `false` uwzględniona w pakiecie nuget.

Inne metadane specyficzne dla pakietu, które można ustawić dla dowolnego z powyższych elementów, obejmują zestawy i wartości we wpisie ```<PackageCopyToOutput>``` ```<PackageFlatten>``` w danych ```CopyToOutput``` ```Flatten``` ```contentFiles``` wyjściowych nuspec .

> [!Note]
> Oprócz elementów zawartości metadane i można również ustawić dla plików z akcją kompilacji `<Pack>` `<PackagePath>` Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.
>
> Aby pakiet dołączał nazwę pliku do ścieżki pakietu w przypadku używania wzorców wieloznaków, ścieżka pakietu musi kończyć się znakiem separatora folderu. W przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka wraz z nazwą pliku.

### <a name="includesymbols"></a>IncludeSymbols

W przypadku `MSBuild -t:pack -p:IncludeSymbols=true` korzystania z programu odpowiednie pliki są `.pdb` kopiowane wraz z innymi plikami wyjściowych ( `.dll` , , , , , `.exe` `.winmd` `.xml` `.json` `.pri` ). Należy pamiętać, `IncludeSymbols=true` że ustawienie tworzy zwykły pakiet *i* pakiet symboli.

### <a name="includesource"></a>IncludeSource

Jest to taka sama jak , z tą różnicą, że kopiuje również pliki źródłowe `IncludeSymbols` `.pdb` wraz z plikami. Wszystkie pliki typu są kopiowane do zachowywania struktury folderów ścieżki `Compile` `src\<ProjectName>\` względnej w wynikowym pakiecie. To samo dzieje się również w przypadku plików źródłowych dowolnego `ProjectReference` z nich, dla `TreatAsPackageReference` którego ustawiono wartość `false` .

Jeśli plik typu Compile znajduje się poza folderem projektu, jest po prostu dodawany do `src\<ProjectName>\` pliku .

### <a name="packing-a-license-expression-or-a-license-file"></a>Pakowanie wyrażenia licencji lub pliku licencji

W przypadku korzystania z wyrażenia licencji użyj `PackageLicenseExpression` właściwości . Aby uzyskać przykład, zobacz [Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Aby dowiedzieć się więcej o wyrażeniach licencji i licencjach akceptowanych przez NuGet .org, zobacz [metadane licencji](nuspec.md#license).

Podczas pakowania pliku licencji użyj właściwości , aby określić ścieżkę pakietu względem katalogu `PackageLicenseFile` głównego pakietu. Ponadto upewnij się, że plik znajduje się w pakiecie . Na przykład:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Aby uzyskać przykład, zobacz [Przykładowy plik licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).

> [!NOTE]
> Jednocześnie można określić tylko jeden z , i `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` .

### <a name="packing-a-file-without-an-extension"></a>Pakowanie pliku bez rozszerzenia

W niektórych scenariuszach, takich jak pakowanie pliku licencji, warto dołączyć plik bez rozszerzenia.
Ze względów NuGet  &  MSBuild historycznych ścieżki bez rozszerzenia należy traktować jako katalogi.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Plik bez przykładowego rozszerzenia](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).

### <a name="istool"></a>IsTool

W przypadku korzystania z programu wszystkie pliki wyjściowe określone w scenariuszu Zestawów wyjściowych są kopiowane do folderu , `MSBuild -t:pack -p:IsTool=true` a nie do folderu [](#output-assemblies) `tools` `lib` . Należy zauważyć, że różni się to od `DotNetCliTool` obiektu , który jest określony przez ustawienie w pliku `PackageType` `.csproj` .

### <a name="packing-using-a-nuspec-file"></a>Pakowanie przy użyciu `.nuspec` pliku

Mimo że zaleca się, [aby](../reference/msbuild-targets.md#pack-target) zamiast tego uwzględnić wszystkie właściwości, które zwykle znajdują się w pliku projektu, można użyć pliku do `.nuspec` `.nuspec` pakowania projektu. W przypadku projektu bez zestawu SDK, który używa narzędzia , należy zaimportować plik , aby `PackageReference` można było wykonać zadanie `NuGet.Build.Tasks.Pack.targets` pakietu. Aby można było spakować plik, należy przywrócić nuspec projekt. (Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).

Docelowa framework pliku projektu nie ma znaczenia i nie jest używana podczas pakowania obiektu nuspec . Następujące trzy właściwości MSBuild są istotne w przypadku pakowania przy użyciu obiektu `.nuspec` :

1. `NuspecFile`: względna lub bezwzględna ścieżka `.nuspec` do pliku używanego do pakowania.
1. `NuspecProperties`: rozdzielana średnikami lista par klucz=wartość. Ze względu na sposób działania analizowania wiersza polecenia należy określić wiele właściwości MSBuild w następujący sposób: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: ścieżka podstawowa `.nuspec` pliku.

Jeśli używasz `dotnet.exe` polecenia do pakowania projektu, użyj polecenia podobnego do następującego:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Jeśli używasz MSBuild polecenia do pakowania projektu, użyj polecenia podobnego do następującego:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Należy pamiętać, że pakowanie przy użyciu dotnet.exe lub msbuild domyślnie prowadzi również nuspec do budowania projektu. Można tego uniknąć, przekazując właściwość do dotnet.exe, co jest odpowiednikiem ustawienia w pliku projektu wraz z ustawieniem ```--no-build``` ```<NoBuild>true</NoBuild> ``` w pliku ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` projektu.

Przykładem pliku *csproj do* pakowania nuspec pliku jest:

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

Obiekt `pack` docelowy udostępnia dwa punkty rozszerzenia, które są uruchamiane w kompilacji specyficznej dla wewnętrznej, docelowej struktury. Punkty rozszerzenia obsługują m.in. zawartość i zestawy specyficzne dla struktury docelowej w pakiecie:

- `TargetsForTfmSpecificBuildOutput`target: użyj dla plików w `lib` folderze lub folderze określonym za pomocą . `BuildOutputTargetFolder`
- `TargetsForTfmSpecificContentInPackage` target: użyj dla plików spoza `BuildOutputTargetFolder` .

#### `TargetsForTfmSpecificBuildOutput`

Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości . Dla wszystkich plików, które muszą przejść do pliku (domyślnie lib), obiekt docelowy powinien zapisać te pliki w grupie ItemGroup i ustawić `BuildOutputTargetFolder` `BuildOutputInPackage` następujące dwie wartości metadanych:

- `FinalOutputPath`: ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość jest używana do oceny ścieżki źródłowej.
- `TargetPath`: (Opcjonalnie) Ustaw, gdy plik musi przejść do podfolderu w programie , na przykład zestawów satelicie, które są dostępne w `lib\<TargetFramework>` odpowiednich folderach kulturowych. Wartość domyślna to nazwa pliku.

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

Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości . W przypadku plików do uwzględnienia w pakiecie element docelowy powinien zapisać te pliki w grupie ItemGroup i ustawić `TfmSpecificPackageFile` następujące opcjonalne metadane:

- `PackagePath`: ścieżka, w której plik powinien być wyjściowy w pakiecie. NuGet program wydaje ostrzeżenie, jeśli do tej samej ścieżki pakietu zostanie dodany więcej niż jeden plik.
- `BuildAction`: akcja kompilacji do przypisania do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w `contentFiles` folderze . Wartość domyślna to "Brak".

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

## <a name="restore-target"></a>przywracanie obiektu docelowego

`MSBuild -t:restore` (którego `nuget restore` i których można używać z projektami .NET Core), przywraca pakiety przywołyne `dotnet restore` w pliku projektu w następujący sposób:

1. Odczytywanie wszystkich odwołań do projektu
1. Odczytywanie właściwości projektu w celu znalezienia folderów pośrednich i platform docelowych
1. Przekaż MSBuild dane do NuGet.Build.Tasks.dll
1. Uruchamianie przywracania
1. Pobieranie pakietów
1. Zapis pliku zasobów, obiektów docelowych i propeduł

Element `restore` docelowy działa w przypadku projektów w formacie PackageReference.
`MSBuild 16.5+` Program [obsługuje również](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) format `packages.config` .

> [!NOTE]
> Obiektu `restore` [docelowego nie należy uruchamiać](#restoring-and-building-with-one-msbuild-command) w połączeniu z obiektem `build` docelowym.

### <a name="restore-properties"></a>Przywróć właściwości

Dodatkowe ustawienia przywracania mogą pochodzić MSBuild z właściwości w pliku projektu. Wartości można również ustawiać z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (zobacz przykłady poniżej).

| Właściwość | Opis |
|--------|--------|
| `RestoreSources` | Rozdzielana średnikami lista źródeł pakietów. |
| `RestorePackagesPath` | Ścieżka folderu pakietów użytkowników. |
| `RestoreDisableParallel` | Ogranicz pobieranie do jednego na raz. |
| `RestoreConfigFile` | Ścieżka do `Nuget.Config` pliku do zastosowania. |
| `RestoreNoCache` | W przypadku wartości true unika używania buforowanych pakietów. Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej.](../consume-packages/managing-the-global-packages-and-cache-folders.md) |
| `RestoreIgnoreFailedSources` | W przypadku wartości true ignoruje brakujące źródła pakietów lub je ignoruje. |
| `RestoreFallbackFolders` | Foldery rezerwowe używane w taki sam sposób jak folder pakietów użytkowników. |
| `RestoreAdditionalProjectSources` | Dodatkowe źródła do użycia podczas przywracania. |
| `RestoreAdditionalProjectFallbackFolders` | Dodatkowe foldery rezerwowe do użycia podczas przywracania. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | Ścieżka do `NuGet.Build.Tasks.dll` . |
| `RestoreGraphProjectInput` | Rozdzielana średnikami lista projektów do przywrócenia, która powinna zawierać ścieżki bezwzględne. |
| `RestoreUseSkipNonexistentTargets`  | Gdy projekty są zbierane za pośrednictwem programu , określa, czy są one MSBuild zbierane przy użyciu `SkipNonexistentTargets` optymalizacji. Jeśli nie zostanie ustawiona, wartość domyślna to `true` . Konsekwencją jest szybkie działanie w przypadku, gdy nie można zaimportować obiektów docelowych projektu. |
| `MSBuildProjectExtensionsPath` | Folder wyjściowy z wartością domyślną `BaseIntermediateOutputPath` i `obj` folderem . |
| `RestoreForce` | W projektach opartych na packageReference program wymusza rozwiązanie wszystkich zależności, nawet jeśli ostatnie przywracanie powiodło się. Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku. Nie pomija to pamięci podręcznej http. |
| `RestorePackagesWithLockFile` | Decyduje się na użycie pliku blokady. |
| `RestoreLockedMode` | Uruchom przywracanie w trybie zablokowanym. Oznacza to, że przywracanie nie spowoduje ponownej wyceny zależności. |
| `NuGetLockFilePath` | Niestandardowa lokalizacja pliku blokady. Domyślna lokalizacja znajduje się obok projektu i nosi nazwę `packages.lock.json` . |
| `RestoreForceEvaluate` | Wymusza przywracanie, aby ponownie skompilować zależności i zaktualizować plik blokady bez żadnego ostrzeżenia. |
| `RestorePackagesConfig` | Przełącznik zgody, który przywraca projekty za pomocą packages.config. Obsługa tylko `MSBuild -t:restore` za pomocą. |
| `RestoreUseStaticGraphEvaluation` | Przełączenie do korzystania z oceny statycznego MSBuild grafu zamiast standardowej oceny. Statyczna ocena grafu to funkcja eksperymentalna, która jest znacznie szybsza w przypadku dużych repos i rozwiązań. |

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

Przywracanie tworzy następujące pliki w `obj` folderze kompilacji:

| Plik | Opis |
|--------|--------|
| `project.assets.json` | Zawiera wykres zależności wszystkich odwołań do pakietu. |
| `{projectName}.projectFileExtension.nuget.g.props` | Odwołania do MSBuild propeduł zawartych w pakietach |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odwołania do MSBuild obiektów docelowych zawartych w pakietach |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Przywracanie i budowania za pomocą jednego MSBuild polecenia

Ze względu na fakt, że można przywrócić pakiety, które wprowadzają obiekty docelowe i propeduły, oceny przywracania i kompilacji są NuGet MSBuild uruchamiane z różnymi właściwościami globalnymi.
Oznacza to, że poniższe elementy będą mieć nieprzewidywalne i często nieprawidłowe zachowanie.

```cli
msbuild -t:restore,build
```

 Zamiast tego zalecane jest:

```cli
msbuild -t:build -restore
```

Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build` .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>Przywracanie packageReference i packages.config projektów za pomocą MSBuild

W MSBuild przypadku programu 16.5 packages.config są również obsługiwane dla programu `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` Przywracanie jest dostępne tylko z `MSBuild 16.5+` , a nie z `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Przywracanie za pomocą MSBuild statycznej oceny grafu

> [!NOTE]
> W MSBuild programie 16.6+ dodano eksperymentalną funkcję do korzystania z oceny statycznego grafu z wiersza polecenia, która znacznie poprawia czas przywracania w NuGet dużych repozytoriach.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Alternatywnie można ją włączyć, ustawiając właściwość w Directory.Build.Props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Od Visual Studio 2019.x i 5.x ta funkcja jest uznawana za eksperymentalną i NuGet zrezygnuje z jej otrzymywania. Postępuj [ NuGet zgodnie z tematem /Home#9803,](https://github.com/NuGet/Home/issues/9803) aby uzyskać szczegółowe informacje o tym, kiedy ta funkcja będzie domyślnie włączona.

Statyczne przywracanie grafu zmienia część msbuild przywracania, odczytywanie i ocenianie projektu, ale nie algorytm przywracania! Algorytm przywracania jest taki sam we wszystkich narzędziach NuGet NuGet (exe, MSBuild exe, dotnet.exe i Visual Studio).

W bardzo nielicznych scenariuszach przywracanie statycznego grafu może zachowywać się inaczej niż bieżące przywracanie, a niektóre zadeklarowane elementy PackageReferences lub ProjectReferences mogą być brakujące.

Aby ułatwić sobie rozum, podczas migracji do statycznego przywracania grafu rozważ uruchomienie:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet Nie *należy zgłaszać* żadnych zmian. Jeśli widzisz niezgodność, napisz na stronie [ NuGet /Home](https://github.com/nuget/home/issues/new)problem .

### <a name="replacing-one-library-from-a-restore-graph"></a>Zastępowanie jednej biblioteki z wykresu przywracania

Jeśli przywracanie przywraca niewłaściwy zestaw, można wykluczyć ten domyślny wybór pakietów i zastąpić go własnym wyborem. Najpierw przy użyciu najwyższego poziomu `PackageReference` wyklucz wszystkie zasoby:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Następnie dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
