---
title: Dokumentacja pliku. nuspec dla narzędzia NuGet
description: Plik. nuspec zawiera metadane pakietu używane podczas kompilowania pakietu i dostarczania informacji użytkownikom pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4028657862cfd56d0653b370e8344cab8392d69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859502"
---
# <a name="nuspec-reference"></a>nuspec — odwołanie

`.nuspec`Plik jest manifestem XML zawierającym metadane pakietu. Ten manifest jest używany zarówno do kompilowania pakietu, jak i dostarczania informacji klientom. Manifest jest zawsze zawarty w pakiecie.

W tym temacie:

- [Ogólny formularz i schemat](#general-form-and-schema)
- [Tokeny zastępcze](#replacement-tokens) (gdy są używane z projektem programu Visual Studio)
- [Zależności](#dependencies)
- [Jawne odwołania do zestawów](#explicit-assembly-references)
- [Odwołania do zestawów struktury](#framework-assembly-references)
- [Dołączanie plików zestawów](#including-assembly-files)
- [Dołączanie plików zawartości](#including-content-files)
- [Przykładowe pliki nuspec](#example-nuspec-files)

## <a name="project-type-compatibility"></a>Zgodność typu projektu

- Używany `.nuspec` z programem `nuget.exe pack` dla projektów typu non-SDK, które używają `packages.config` .

- `.nuspec`Plik nie jest wymagany do tworzenia pakietów dla [projektów w stylu zestawu SDK](../resources/check-project-format.md) (zazwyczaj platformy .net core i .NET Standard projektów, które używają [atrybutu SDK](/dotnet/core/tools/csproj#additions)). (Należy pamiętać, że `.nuspec` jest generowany podczas tworzenia pakietu).

   Jeśli tworzysz pakiet przy użyciu programu `dotnet.exe pack` lub `msbuild pack target` , zalecamy [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu. Można jednak wybrać opcję [użycia `.nuspec` pliku do spakowania przy użyciu `dotnet.exe` lub `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).

- W przypadku projektów migrowanych z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md) `.nuspec` plik nie jest wymagany do utworzenia pakietu. Zamiast tego należy użyć [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

## <a name="general-form-and-schema"></a>Ogólny formularz i schemat

Bieżący `nuspec.xsd` plik schematu znajduje się w [repozytorium GitHub usługi NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

W tym schemacie `.nuspec` plik ma następującą formę ogólną:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Aby wyczyścić wizualną reprezentację schematu, Otwórz plik schematu w programie Visual Studio w trybie projektowania i kliknij link **Eksplorator schematu XML** . Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze, a następnie wybierz polecenie **Pokaż Eksplorator schematu XML**. W dowolnym momencie możesz wyświetlić widok podobny do przedstawionego poniżej (w większości rozwiniętych):

![Eksplorator schematu programu Visual Studio z otwartym nuspec. xsd](media/SchemaExplorer.png)

Wszystkie nazwy elementów XML w pliku nuspec są rozróżniane wielkości liter, podobnie jak w przypadku XML. Na przykład użycie elementu Metadata `<description>` jest poprawne i `<Description>` nie jest poprawne. Poniższa Nazwa każdego elementu jest opisana poniżej.

### <a name="required-metadata-elements"></a>Wymagane elementy metadanych

Mimo że następujące elementy są minimalnymi wymaganiami dotyczącymi pakietu, należy rozważyć dodanie [opcjonalnych elementów metadanych](#optional-metadata-elements) w celu poprawienia ogólnych doświadczeń deweloperów korzystających z Twojego pakietu. 

Te elementy muszą znajdować się w obrębie `<metadata>` elementu.

#### <a name="id"></a>identyfikator 
Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowy w obrębie nuget.org lub dowolnej galerii, w której znajduje się pakiet. Identyfikatory nie mogą zawierać spacji ani znaków, które są nieprawidłowe dla adresu URL, i ogólnie przestrzegają reguł przestrzeni nazw platformy .NET. Aby uzyskać wskazówki [, zobacz Wybieranie unikatowego identyfikatora pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .

Podczas przekazywania pakietu do nuget.org, `id` pole jest ograniczone do 128 znaków.

#### <a name="version"></a>Wersja
Wersja pakietu, po wzorcu *główna. pomocnicza. poprawka* . Numery wersji mogą zawierać sufiks wstępnej wersji, zgodnie z opisem w temacie [wersja pakietu](../concepts/package-versioning.md#pre-release-versions). 

Podczas przekazywania pakietu do nuget.org, `version` pole jest ograniczone do 64 znaków.

#### <a name="description"></a>description (opis)
Opis pakietu na potrzeby wyświetlania interfejsu użytkownika.

Podczas przekazywania pakietu do nuget.org, `description` pole jest ograniczone do 4000 znaków.

#### <a name="authors"></a>autorów
Rozdzielana przecinkami lista autorów pakietów, które pasują do nazw profilów w nuget.org. Są one wyświetlane w galerii NuGet w witrynie nuget.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów. 

Podczas przekazywania pakietu do nuget.org, `authors` pole jest ograniczone do 4000 znaków.

### <a name="optional-metadata-elements"></a>Opcjonalne elementy metadanych

#### <a name="owners"></a>rzecz
> [!Important]
> Właściciele są przestarzałi. Zamiast tego użyj autorów.

Rozdzielana przecinkami lista twórców pakietów korzystających z nazw profilów w nuget.org. Jest to często taka sama lista jak w programie `authors` i jest ignorowana podczas przekazywania pakietu do NuGet.org. Zobacz [Zarządzanie właścicielami pakietów w witrynie NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). 

#### <a name="projecturl"></a>projectUrl
Adres URL strony głównej pakietu, często wyświetlany w interfejsie użytkownika, a także nuget.org. 

Podczas przekazywania pakietu do nuget.org, `projectUrl` pole jest ograniczone do 4000 znaków.

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl jest przestarzała. Zamiast tego użyj licencji.

Adres URL licencji pakietu, często przedstawiony w interfejsów użytkownika, na przykład nuget.org.

Podczas przekazywania pakietu do nuget.org, `licenseUrl` pole jest ograniczone do 4000 znaków.

#### <a name="license"></a>license (licencja)

*Obsługiwane przez **4.9.0 NuGet** i nowsze*

Wyrażenie licencji SPDX lub ścieżka do pliku licencji w pakiecie, często pokazywane w interfejsów użytkownika, jak nuget.org. Jeśli pakiet jest licencjonowany w ramach wspólnej licencji, takiej jak MIT lub BSD-2-klauzule, należy użyć skojarzonego [identyfikatora licencji SPDX](https://spdx.org/licenses/). Na przykład:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org akceptuje tylko wyrażenia licencyjne zatwierdzone przez inicjatywę Open Source lub bezpłatną program Software Foundation.

Jeśli pakiet jest licencjonowany w ramach wielu popularnych licencji, możesz określić licencję złożoną przy użyciu [składni wyrażenia SPDX w wersji 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60). Na przykład:

`<license type="expression">BSD-2-Clause OR MIT</license>`

Jeśli używasz niestandardowej licencji, która nie jest obsługiwana przez wyrażenia licencji, możesz spakować `.txt` `.md` plik lub z tekstem licencji. Na przykład:

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

Aby uzyskać odpowiedniki programu MSBuild, zapoznaj się z tematem [pakowanie wyrażenia licencji lub pliku licencji](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

Dokładna składnia wyrażeń licencji narzędzia NuGet została opisana poniżej w [ABNF](https://tools.ietf.org/html/rfc5234).

```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl

> [!Important]
> iconUrl jest przestarzała. Zamiast tego użyj ikony.

Adres URL obrazu 128 x 128 z przezroczystym tłem, który będzie używany jako ikona pakietu w wyświetlanym interfejsie użytkownika. Upewnij się, że ten element zawiera *adres URL obrazu bezpośredniego* , a nie adres URL strony sieci Web zawierającej obraz. Na przykład, aby użyć obrazu z usługi GitHub, użyj adresu URL nieprzetworzonego pliku, takiego jak <em> https://github.com/ \<username\> / \<repository\> /RAW/ \<branch\> / \<logo.png\> </em>. 

Podczas przekazywania pakietu do nuget.org, `iconUrl` pole jest ograniczone do 4000 znaków.

#### <a name="icon"></a>ikona

*Obsługiwane przez **5.3.0 NuGet** i nowsze*

Jest to ścieżka do pliku obrazu w pakiecie, często pokazana w interfejsów użytkownika, jak nuget.org jako ikona pakietu. Rozmiar pliku obrazu jest ograniczony do 1 MB. Obsługiwane formaty plików to JPEG i PNG. Zalecamy rozdzielczość obrazu 128 x 128.

Można na przykład dodać następujący element do nuspec podczas tworzenia pakietu przy użyciu nuget.exe:

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[Przykład nuspec ikony pakietu.](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

W przypadku odpowiedników programu MSBuild zapoznaj się z [opakowaniem pliku obrazu ikony](msbuild-targets.md#packing-an-icon-image-file).

> [!Tip]
> Można określić zarówno `icon` , jak i `iconUrl` zachować zgodność z poprzednimi wersjami ze źródłami, które nie są obsługiwane `icon` . Program Visual Studio będzie obsługiwał `icon` pakiety pochodzące ze źródła opartego na folderach w przyszłej wersji.

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.

#### <a name="developmentdependency"></a>developmentDependency
*(2.8 +)* Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do programowania, który uniemożliwia dołączenie pakietu jako zależności w innych pakietach. W przypadku PackageReference (NuGet 4.8 +) Ta flaga oznacza również, że wykluczają się zasoby czasu kompilacji z kompilacji. Zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)

#### <a name="summary"></a>Podsumowanie
> [!Important]
> `summary` jest przestarzały. Zamiast tego użyj polecenia cmdlet `description`.

Krótki opis pakietu do wyświetlania interfejsu użytkownika. W przypadku pominięcia `description` zostanie użyta obcięta wersja.

Podczas przekazywania pakietu do nuget.org, `summary` pole jest ograniczone do 4000 znaków.

#### <a name="releasenotes"></a>releaseNotes
*(1,5 +)* Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak karta **aktualizacje** w Menedżerze pakietów programu Visual Studio zamiast opisu pakietu.

Podczas przekazywania pakietu do nuget.org, `releaseNotes` pole jest ograniczone do 35 000 znaków.

#### <a name="copyright"></a>informacji o prawach autorskich,
*(1,5 +)* Szczegóły dotyczące praw autorskich pakietu.

Podczas przekazywania pakietu do nuget.org, `copyright` pole jest ograniczone do 4000 znaków.

#### <a name="language"></a>language
Identyfikator ustawień regionalnych dla pakietu. Zobacz [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md).

#### <a name="tags"></a>tags
Rozdzielana spacjami Lista tagów i słów kluczowych, które opisują pakiet i ułatwiają odnajdywanie pakietów przez wyszukiwanie i filtrowanie. 

Podczas przekazywania pakietu do nuget.org, `tags` pole jest ograniczone do 4000 znaków.

#### <a name="serviceable"></a>Obsługa 
*(3.3 +)* Tylko do użytku wewnętrznego narzędzia NuGet.

#### <a name="repository"></a>repozytorium
Metadane repozytorium zawierające cztery opcjonalne atrybuty: `type` i `url` *(4.0 +)* i `branch` i `commit` *(4.6 +)*. Te atrybuty umożliwiają mapowanie `.nupkg` do repozytorium, które zostało przez niego skompilowane, z możliwością uzyskania tak szczegółowej nazwy gałęzi i/lub zatwierdzenia skrótu SHA-1, który skompilowano pakiet. Powinien to być publicznie dostępny adres URL, który może być wywoływany bezpośrednio przez oprogramowanie kontroli wersji. Nie powinna być stroną HTML, ponieważ jest ona przeznaczona dla komputera. W przypadku łączenia ze stroną projektu `projectUrl` zamiast tego użyj pola.

Na przykład:
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

Podczas przekazywania pakietu do nuget.org, `type` atrybut jest ograniczony do 100 znaków, a `url` atrybut jest ograniczony do 4000 znaków.

#### <a name="title"></a>tytuł
Przyjazny dla człowieka tytuł pakietu, który może być używany w niektórych interfejsach użytkownika. (nuget.org i Menedżer pakietów w programie Visual Studio nie wyświetla tytułu)

Podczas przekazywania pakietu do nuget.org, `title` pole jest ograniczone do 256 znaków, ale nie jest używane do żadnych celów wyświetlania.

#### <a name="collection-elements"></a>Elementy kolekcji

#### <a name="packagetypes"></a>packageTypes
*(3.5 +)* Kolekcja elementów o zerowym lub większej liczbie `<packageType>` określająca typ pakietu, jeśli jest inny niż tradycyjny pakiet zależności. Każdy pakiet PackageType ma atrybuty *nazwy* i *wersji*. Zobacz [Ustawianie typu pakietu](../create-packages/set-package-type.md).

#### <a name="dependencies"></a>zależności
Kolekcja elementów co najmniej zero `<dependency>` określających zależności pakietu. Każda zależność ma atrybuty *identyfikatora*, *wersji*, *include* (3. x +) i *exclude* (3. x +). Zobacz [zależności](#dependencies-element) poniżej.

#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2 +)* Kolekcja zawierająca zero lub więcej `<frameworkAssembly>` elementów .NET Framework identyfikujących odwołania do zestawów, które są wymagane przez ten pakiet, co zapewnia, że odwołania są dodawane do projektów zużywających pakiet. Każdy frameworkAssembly ma atrybuty *AssemblyName* i *TargetFramework* . Zobacz [Określanie zestawu Framework odwołuje się do poniższej pamięci podręcznej](#specifying-framework-assembly-references-gac) .

#### <a name="references"></a>odwołania
*(1,5 +)* Kolekcja `<reference>` elementów w `lib` folderze pakietu, które są dodawane jako odwołania do projektu. Każde odwołanie ma atrybut *pliku* . `<references>` może również zawierać `<group>` element z atrybutem *TargetFramework* , który zawiera `<reference>` elementy. W przypadku pominięcia `lib` zostaną uwzględnione wszystkie odwołania. Zobacz [Określanie jawnych odwołań do zestawów](#specifying-explicit-assembly-references) poniżej.

#### <a name="contentfiles"></a>contentFiles
*(3.3 +)* Kolekcja `<files>` elementów, które identyfikują pliki zawartości do uwzględnienia w projekcie zużywanym. Te pliki są określone za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu. Zobacz sekcję [określanie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej.

#### <a name="files"></a>files 
`<package>`Węzeł może zawierać `<files>` węzeł jako element równorzędny i element `<metadata>` `<contentFiles>` podrzędny w programie `<metadata>` , aby określić, które pliki zestawu i zawartości mają być zawarte w pakiecie. Szczegółowe informacje znajdują się w temacie [zawierającym pliki zestawu](#including-assembly-files) i [pliki zawartości](#including-content-files) w dalszej części tego tematu.

### <a name="metadata-attributes"></a>atrybuty metadanych

#### <a name="minclientversion"></a>minClientVersion
Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszony przez nuget.exe i Menedżera pakietów programu Visual Studio. Jest on używany zawsze, gdy pakiet jest zależny od określonych funkcji `.nuspec` pliku, które zostały dodane w określonej wersji klienta NuGet. Na przykład pakiet używający `developmentDependency` atrybutu powinien określać wartość "2,8" dla `minClientVersion` . Podobnie pakiet używający `contentFiles` elementu (patrz następna sekcja) powinien mieć ustawioną wartość `minClientVersion` "3,3". Należy zauważyć, że ponieważ klienci NuGet przed 2,5 nie rozpoznają tej flagi, *zawsze* odmówią instalacji pakietu bez względu na to, co `minClientVersion` zawiera.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a>Tokeny zastępcze

Podczas tworzenia pakietu [ `nuget pack` polecenie](../reference/cli-reference/cli-ref-pack.md) zastępuje tokeny $-Limited w `.nuspec` `<metadata>` węźle pliku wartościami, które pochodzą z pliku projektu lub `pack` `-properties` przełącznika polecenia.

W wierszu polecenia należy określić wartości tokenu przy użyciu `nuget pack -properties <name>=<value>;<name>=<value>` . Na przykład można użyć tokenu, takiego jak `$owners$` i `$desc$` w `.nuspec` i podać wartości w czasie pakowania w następujący sposób:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Aby użyć wartości z projektu, należy określić tokeny opisane w poniższej tabeli (AssemblyInfo odnosi się do pliku, na przykład `Properties` `AssemblyInfo.cs` lub `AssemblyInfo.vb` ).

Aby użyć tych tokenów, uruchom polecenie `nuget pack` z plikiem projektu, a nie tylko `.nuspec` . Na przykład podczas korzystania z następującego polecenia `$id$` `$version$` tokeny i w `.nuspec` pliku są zastępowane `AssemblyName` i `AssemblyVersion` wartościami projektu:

```ps
nuget pack MyProject.csproj
```

Zazwyczaj w przypadku projektu można utworzyć `.nuspec` początkowo przy użyciu, `nuget spec MyProject.csproj` który automatycznie zawiera niektóre z tych standardowych tokenów. Jeśli jednak projekt nie zawiera wartości wymaganych `.nuspec` elementów, `nuget pack` kończy się niepowodzeniem. Ponadto jeśli zmienisz wartości projektu, pamiętaj, aby ponownie skompilować przed utworzeniem pakietu; można to zrobić przy użyciu przełącznika polecenia pakietu `build` .

Z wyjątkiem `$configuration$` wartości w projekcie są używane w preferencjach do wszystkich przypisanych do tego samego tokenu w wierszu polecenia.

| Token | Źródło wartości | Wartość
| --- | --- | ---
| **$id $** | Plik projektu | AssemblyName (title) z pliku projektu |
| **$version $** | AssemblyInfo | AssemblyInformationalVersion, jeśli jest obecny, w przeciwnym razie AssemblyVersion |
| **$author $** | AssemblyInfo | AssemblyCompany |
| **$title $** | AssemblyInfo | AssemblyTitle |
| **$description $** | AssemblyInfo | AssemblyDescription |
| **$copyright $** | AssemblyInfo | AssemblyCopyright |
| **$configuration $** | Biblioteka DLL zestawu | Konfiguracja użyta do skompilowania zestawu, czyli domyślnego debugowania. Należy pamiętać, że aby utworzyć pakiet przy użyciu konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` w wierszu polecenia. |

Tokeny mogą być również używane do rozpoznawania ścieżek podczas dołączania [plików zestawu](#including-assembly-files) i [plików zawartości](#including-content-files). Tokeny mają takie same nazwy jak właściwości programu MSBuild, dzięki czemu można wybrać pliki do uwzględnienia w zależności od bieżącej konfiguracji kompilacji. Jeśli na przykład w pliku są używane następujące tokeny `.nuspec` :

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

Po utworzeniu zestawu `AssemblyName` , którego konfiguracja jest `LoggingLibrary` `Release` w programie MSBuild, wyniki wierszy w `.nuspec` pliku w pakiecie są następujące:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Element zależności

`<dependencies>`Element w obrębie `<metadata>` zawiera dowolną liczbę `<dependency>` elementów, które identyfikują inne pakiety, od których zależy pakiet najwyższego poziomu. Atrybuty dla każdej z nich `<dependency>` są następujące:

| Atrybut | Opis |
| --- | --- |
| `id` | Potrzeb Identyfikator pakietu zależności, taki jak "EntityFramework" i "NUnit", czyli nazwa pakietu nuget.org wyświetlana na stronie pakietu. |
| `version` | Potrzeb Zakres wersji akceptowalnych jako zależność. Aby uzyskać dokładną składnię, zobacz [wersja pakietu](../concepts/package-versioning.md#version-ranges) . Wersje zmiennoprzecinkowe nie są obsługiwane. |
| include | Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazujących zależność do uwzględnienia w pakiecie końcowym. Wartość domyślna to `all`. |
| wykluczanie | Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazujących zależność do wykluczenia w końcowym pakiecie. Wartość domyślna to `build,analyzers` , że można ją wypisać. Ale `content/ ContentFiles` są również niejawnie wykluczone w pakiecie końcowym, który nie może być nadpisany. Tagi określone za pomocą `exclude` mają pierwszeństwo przed tymi określonymi przy użyciu `include` . Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"` . |

Podczas przekazywania pakietu do nuget.org, każdy `id` atrybut zależności jest ograniczony do 128 znaków, a `version` atrybut jest ograniczony do 256 znaków.

| Include/Exclude — tag | Zmodyfikowane foldery elementu docelowego |
| --- | --- |
| contentFiles | Zawartość |
| środowisko uruchomieniowe | Środowisko uruchomieniowe, zasoby i FrameworkAssemblies |
| kompilowanie | lib |
| kompilacja | Kompilacja (właściwości i elementy docelowe programu MSBuild) |
| natywne | natywne |
| brak | Brak folderów |
| all | Wszystkie foldery |

Na przykład następujące wiersze wskazują zależności w `PackageA` wersji 1.1.0 lub nowszej, a `PackageB` wersja 1. x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Poniższe wiersze wskazują zależności dotyczące tych samych pakietów, ale określają, że mają być dostępne foldery i i `contentFiles` `build` wszystkie z nich, `PackageA` ale `native` `compile` Foldery `PackageB` "

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> Podczas tworzenia `.nuspec` z projektu przy użyciu `nuget spec` , zależności, które istnieją w tym projekcie, nie są automatycznie dołączane do `.nuspec` pliku. Zamiast tego należy użyć `nuget pack myproject.csproj` i pobrać plik *. nuspec* z wygenerowanego pliku *NUPKG* . This *. nuspec* zawiera zależności.

### <a name="dependency-groups"></a>Grupy zależności

*Wersja 2.0 +*

Jako alternatywę dla pojedynczej płaskiej listy, zależności można określić zgodnie z profilem struktury projektu docelowego za pomocą `<group>` elementów w `<dependencies>` .

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów. Te zależności są instalowane razem, gdy struktura docelowa jest zgodna z profilem struktury projektu.

`<group>`Element bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista zależności. Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.

> [!Important]
> Format grupy nie może być mieszany z płaską listą.

> [!Note]
> Format [monikera platformy docelowej (TFM)](../reference/target-frameworks.md) używany w `lib/ref` folderze jest inny w porównaniu z TFM używanym w `dependency groups` . Jeśli Platformy docelowe zadeklarowane w `dependencies group` `lib/ref` folderze i `.nuspec` pliku nie mają dokładnych odpowiedników, `pack` polecenie spowoduje [wygenerowanie ostrzeżenia NuGet NU5128](../reference/errors-and-warnings/nu5128.md).

W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Jawne odwołania do zestawów

`<references>`Element jest używany przez projekty `packages.config` , aby jawnie określić zestawy, do których projekt docelowy powinien odwoływać się przy użyciu pakietu. Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania. Aby uzyskać więcej informacji, zobacz stronę [wybierania zestawów, do których odwołują się projekty](../create-packages/select-assemblies-referenced-by-projects.md) , aby uzyskać więcej informacji.

Na przykład poniższy `<references>` element instruuje pakiet NuGet, aby dodać odwołania do tylko `xunit.dll` , a `xunit.extensions.dll` nawet wtedy, gdy w pakiecie istnieją dodatkowe zestawy:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>Grupy odwołań

Jako alternatywę dla pojedynczej płaskiej listy, odwołania można określić zgodnie z profilem struktury projektu docelowego za pomocą `<group>` elementów w `<references>` .

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów. Te odwołania są dodawane do projektu, gdy struktura docelowa jest zgodna z profilem struktury projektu.

`<group>`Element bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista odwołań. Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.

> [!Important]
> Format grupy nie może być mieszany z płaską listą.

W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Odwołania do zestawów struktury

Zestawy struktur są tymi, które są częścią programu .NET Framework i powinny już znajdować się w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej maszyny. Identyfikując te zestawy w obrębie `<frameworkAssemblies>` elementu, pakiet może zapewnić, że wymagane odwołania są dodawane do projektu w przypadku, gdy projekt nie ma już odwołań. Takie zespoły nie są bezpośrednio zawarte w pakiecie.

`<frameworkAssemblies>`Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **assemblyName** | Potrzeb W pełni kwalifikowana nazwa zestawu. |
| **targetFramework** | Obowiązkowe Określa platformę docelową, do której stosuje się to odwołanie. W przypadku pominięcia wskazuje, że odwołanie dotyczy wszystkich platform. Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy. |

W poniższym przykładzie przedstawiono odwołanie do `System.Net` dla wszystkich platform docelowych i odwołania do `System.ServiceModel` tylko dla .NET Framework 4,0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Dołączanie plików zestawów

Jeśli przestrzegasz Konwencji opisanych w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md), nie musisz jawnie określać listy plików w `.nuspec` pliku. `nuget pack`Polecenie automatycznie pobiera niezbędne pliki.

> [!Important]
> Gdy pakiet jest instalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu do bibliotek DLL pakietu, *z wyjątkiem* tych, które są nazwane, `.resources.dll` ponieważ zakłada się, że są to zlokalizowane zespoły satelickie. Z tego powodu należy unikać używania `.resources.dll` dla plików, które w przeciwnym razie zawierają istotny kod pakietu.

Aby ominąć to automatyczne zachowanie i jawnie kontrolować, które pliki są zawarte w pakiecie, umieść `<files>` element jako obiekt podrzędny `<package>` (i element równorzędny `<metadata>` ), identyfikując każdy plik z oddzielnym `<file>` elementem. Na przykład:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

W przypadku pakietów NuGet 2. x i starszych oraz projektów korzystających z programu `packages.config` `<files>` element jest również używany do uwzględniania niezmiennych plików zawartości podczas instalowania pakietu. W przypadku pakietów NuGet 3.3 + i projektów PackageReference, `<contentFiles>` element jest używany. Aby uzyskać szczegółowe informacje, zobacz temat [uwzględnianie plików zawartości](#including-content-files) poniżej.

### <a name="file-element-attributes"></a>Atrybuty elementu pliku

Każdy `<file>` element określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **src** | Lokalizacja pliku lub plików do dołączenia, z uwzględnieniem wyjątków określonych przez `exclude` atrybut. Ścieżka jest względna do `.nuspec` pliku, chyba że zostanie określona ścieżka bezwzględna. Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów. |
| **obiektów** | Ścieżka względna do folderu w pakiecie, w którym znajdują się pliki źródłowe, które muszą zaczynać się od `lib` , `content` , `build` , lub `tools` . Zobacz [Tworzenie nuspec z katalogu roboczego opartego na Konwencji](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **wykluczanie** | Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji. Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów. |

### <a name="examples"></a>Przykłady

**Pojedynczy zestaw**

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

**Pojedynczy zestaw specyficzny dla platformy docelowej**

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

**Zestaw bibliotek DLL przy użyciu symbolu wieloznacznego**

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

**Biblioteki DLL dla różnych platform**

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

**Wykluczanie plików**

```
Source files:
    \tools\fileA.bak
    \tools\fileB.bak
    \tools\fileA.log
    \tools\build\fileB.log

.nuspec entries:
    <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
    <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

Package result:
    (no files)
```

## <a name="including-content-files"></a>Dołączanie plików zawartości

Pliki zawartości to niezmienne pliki, których pakiet musi zawierać w projekcie. Są niezmienne, nie są przeznaczone do modyfikacji przez projekt zużywający. Przykładowe pliki zawartości obejmują:

- Obrazy osadzone jako zasoby
- Pliki źródłowe, które zostały już skompilowane
- Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu
- Pliki konfiguracji pakietu, które muszą być zawarte w projekcie, ale nie muszą mieć żadnych zmian specyficznych dla projektu

Pliki zawartości są zawarte w pakiecie przy użyciu `<files>` elementu, określając `content` folder w `target` atrybucie. Jednak takie pliki są ignorowane, gdy pakiet zostanie zainstalowany w projekcie przy użyciu PackageReference, który zamiast tego używa `<contentFiles>` elementu.

Aby zapewnić maksymalną zgodność z zużywanymi projektami, pakiet najlepiej określa pliki zawartości w obu elementach.

### <a name="using-the-files-element-for-content-files"></a>Używanie elementu Files dla plików zawartości

W przypadku plików zawartości wystarczy użyć tego samego formatu co w przypadku plików zestawu, ale określić `content` jako folder podstawowy w `target` atrybucie, jak pokazano w poniższych przykładach.

**Podstawowe pliki zawartości**

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

**Pliki zawartości z strukturą katalogów**

```
Source files:
    css\mobile\style.css
    css\mobile\wp7\style.css
    css\browser\style.css

.nuspec entry:
    <file src="css\**\*.css" target="content\css" />

Packaged result:
    content\css\mobile\style.css
    content\css\mobile\wp7\style.css
    content\css\browser\style.css
```

**Plik zawartości specyficzny dla platformy docelowej**

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

**Plik zawartości skopiowany do folderu z kropką w nazwie**

W takim przypadku pakiet NuGet uważa, że rozszerzenie w programie nie jest `target` zgodne z rozszerzeniem w `src` i w ten sposób traktuje tę część nazwy w `target` postaci folderu:

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

**Pliki zawartości bez rozszerzeń**

Aby dołączyć pliki bez rozszerzenia, użyj `*` `**` symboli wieloznacznych lub:

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

**Pliki zawartości ze szczegółową ścieżką i głębokiego celu**

W tym przypadku, ponieważ rozszerzenia plików dla dopasowania źródłowego i docelowego, pakiet NuGet zakłada, że obiektem docelowym jest nazwa pliku, a nie folder:

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

**Zmiana nazwy pliku zawartości w pakiecie**

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

**Wykluczanie plików**

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Używanie elementu contentFiles dla plików zawartości

*Pakiet NuGet 4.0 + z PackageReference*

Domyślnie pakiet umieszcza zawartość w `contentFiles` folderze (patrz poniżej) i `nuget pack` uwzględnia wszystkie pliki w tym folderze przy użyciu atrybutów domyślnych. W takim przypadku nie trzeba umieszczać `contentFiles` węzła w ogóle `.nuspec` .

Aby kontrolować, które pliki są uwzględniane, `<contentFiles>` element Określa kolekcję `<files>` elementów, które identyfikują dokładne pliki include.

Te pliki są określone za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu:

| Atrybut | Opis |
| --- | --- |
| **być** | Potrzeb Lokalizacja pliku lub plików do dołączenia, z uwzględnieniem wyjątków określonych przez `exclude` atrybut. Ścieżka jest `contentFiles` określana względem folderu, chyba że określona jest ścieżka bezwzględna. Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów. |
| **wykluczanie** | Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji. Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów. |
| **buildAction** | Akcja kompilacji, która ma zostać przypisana do elementu zawartości dla programu MSBuild, takich jak,,, `Content` `None` `Embedded Resource` `Compile` itd. Wartość domyślna to `Compile` . |
| **copyToOutput** | Wartość logiczna wskazująca, czy elementy zawartości mają być kopiowane do folderu wyjściowego kompilacja (lub publikacja). Wartością domyślną jest false. |
| **Flatten** | Wartość logiczna wskazująca, czy kopiować elementy zawartości do pojedynczego folderu w danych wyjściowych kompilacji (true), czy też zachować strukturę folderów w pakiecie (false). Ta flaga działa tylko wtedy, gdy flaga copyToOutput jest ustawiona na wartość true. Wartością domyślną jest false. |

Podczas instalacji pakietu NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu. Jeśli wiele wpisów pasuje do tego samego pliku, zostaną zastosowane wszystkie wpisy. Wpis najwyższego poziomu zastępuje niższe wpisy w przypadku konfliktu dla tego samego atrybutu.

#### <a name="package-folder-structure"></a>Struktura folderu pakietu

Projekt pakietu powinien mieć strukturę zawartości przy użyciu następującego wzorca:

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- `codeLanguages` może być `cs` ,,, `vb` `fs` `any` lub małymi literami odpowiadającymi danej `$(ProjectLanguage)`
- `TxM` to dowolna docelowa moniker platformy docelowej, który obsługuje pakiet NuGet (patrz [Platformy docelowe](../reference/target-frameworks.md)).
- Wszystkie struktury folderów mogą być dołączane na końcu tej składni.

Na przykład:

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

Za pomocą pustych folderów można `.` zrezygnować z udostępniania zawartości dla niektórych kombinacji języka i TxM, na przykład:

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a>Przykładowa sekcja contentFiles

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a>Grupy odwołań platformy

*Tylko wersja 5.1 + wih PackageReference*

Odwołania do platformy są koncepcjami platformy .NET Core reprezentującymi współdzielone platformy, takie jak WPF lub Windows Forms.
Określając strukturę udostępnioną, pakiet gwarantuje, że wszystkie jej zależności struktury są zawarte w projekcie odwołującym.

Każdy `<group>` element wymaga `targetFramework` atrybutu i zero lub więcej `<frameworkReference>` elementów.

W poniższym przykładzie przedstawiono nuspec wygenerowane dla projektu WPF platformy .NET Core.
Należy zauważyć, że nie zaleca się tworzenia ręcznie nuspecs, które zawierają odwołania do struktury. Rozważ użycie pakietu [Target](msbuild-targets.md) Pack, co spowoduje automatyczne wywnioskowanie ich z projektu.

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a>Przykładowe pliki nuspec

**Prosta `.nuspec` , która nie określa zależności ani plików**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**A `.nuspec` z zależnościami**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**A `.nuspec` z plikami**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**`.nuspec`Z zestawami Framework**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

W tym przykładzie są zainstalowane następujące elementy docelowe dla konkretnych projektów:

- . NET4 > `System.Web` , `System.Net`
- . Profil klienta NET4 — > `System.Net`
- Silverlight 3 — > `System.Json`
- WindowsPhone — > `Microsoft.Devices.Sensors`
