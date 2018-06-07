---
title: Odwołanie do pliku .nuspec programu NuGet
description: Plik .nuspec zawiera metadane pakietów używane podczas tworzenia pakietu i podaj informacje dla konsumentów pakietu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 2ff83538f9f1cf3bd4ed616ec8f5f1aef3ffd9d6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818545"
---
# <a name="nuspec-reference"></a>odwołanie .nuspec

A `.nuspec` plik jest manifestu XML zawierający metadane pakietów. Tego manifestu jest używany zarówno do tworzenia pakietu i źródło informacji dla konsumentów. Manifest zawsze znajduje się w pakiecie.

W tym temacie:

- [Ogólny kształt i schematu](#general-form-and-schema)
- [Zastąpienie tokenów](#replacement-tokens) (w przypadku użycia z projektu programu Visual Studio)
- [Zależności](#dependencies)
- [Odwołania do zestawów jawne](#explicit-assembly-references)
- [Odwołania do zestawów struktury](#framework-assembly-references)
- [W tym pliki zestawu](#including-assembly-files)
- [W tym pliki zawartości](#including-content-files)
- [Przykłady](#examples)

## <a name="general-form-and-schema"></a>Ogólny kształt i schematu

Bieżący `nuspec.xsd` można znaleźć w pliku schematu [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

W tym schemacie `.nuspec` plik ma następujący format Ogólne:

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

Dla wyczyść wizualną reprezentację schematu, otwórz plik schematu w programie Visual Studio w trybie projektowania, a następnie wybierz polecenie **Eksploratora schematu XML** łącza. Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz **Pokaż Eksploratora schematu XML**. W obu przypadkach (jeśli jest to przede wszystkim rozwinięty) wyświetlony widok, tak jak poniżej:

![Visual Studio Explorer schematu z nuspec.xsd Otwórz](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>Atrybuty metadanych

`<metadata>` Elementu obsługuje atrybuty opisane w poniższej tabeli.

| Atrybut | Wymagane | Opis |
| --- | --- | --- | 
| **minClientVersion** | Nie | Określa minimalną wersję klienta NuGet, który można zainstalować ten pakiet, wymuszane przez nuget.exe i Menedżer pakietów programu Visual Studio. To jest używana zawsze, gdy pakiet jest zależny od konkretnych cech `.nuspec` plików, które zostały dodane w przypadku konkretnej wersji klienta NuGet. Na przykład pakietu za pomocą `developmentDependency` atrybut powinien określać "2.8" dla `minClientVersion`. Podobnie, pakietu za pomocą `contentFiles` (zobacz następną sekcję) należy ustawić element `minClientVersion` do "3.3". Należy zauważyć, że ponieważ klientów NuGet przed 2.5 nie rozpoznają tej flagi one *zawsze* odmówić można zainstalować pakietu, niezależnie od tego, co `minClientVersion` zawiera. |

### <a name="required-metadata-elements"></a>Elementy wymagane metadane

Następujące elementy są minimalne wymagania dotyczące pakietu, należy rozważyć dodanie [elementy opcjonalne metadane](#optional-metadata-elements) celu usprawnienie obsługi ogólnej mogą korzystać z pakietem.

Te elementy muszą występować w `<metadata>` elementu.

| Element | Opis |
| --- | --- |
| **id** | Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowa w nuget.org lub niezależnie od pakietu, który znajduje się w galerii. Identyfikatory nie może zawierać spacji ani znaków, które nie są prawidłowe dla danego adresu URL i ogólnie zgodne reguły obszaru nazw .NET. Zobacz [Wybieranie identyfikator unikatowy pakiet](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) orientacji. |
| **Wersja** | Wersja pakietu, następujące *Wersja_główna.WERSJA_POMOCNICZA.poprawka* wzorca. Numery wersji może zawierać sufiks wersji wstępnej, zgodnie z opisem w [wersji pakietu](../reference/package-versioning.md#pre-release-versions). |
| **Opis elementu** | Długi opis pakietu do wyświetlenia interfejsu użytkownika. |
| **Autorzy** | Rozdzielana przecinkami lista autorzy pakietów, zgodne z nazwami profilu na nuget.org. Te są wyświetlane w galerii NuGet w nuget.org i są odwoływania się do pakietów przez tego samego autorów. |

### <a name="optional-metadata-elements"></a>Elementy opcjonalne metadane

Te elementy mogą być widoczne w `<metadata>` elementu.

#### <a name="single-elements"></a>Pojedyncze elementy

| Element | Opis |
| --- | --- |
| **Tytuł** | Tytuł przyjaznych dla człowieka pakietu, zwykle używanych w wyświetla interfejsu użytkownika na nuget.org i Menedżera pakietów w programie Visual Studio. Jeśli nie zostanie określony, identyfikator pakietu jest używany. |
| **Właściciele** | Rozdzielana przecinkami lista twórców pakietu przy użyciu nazwy profilu na nuget.org. Jest to często jak w tej samej listy `authors`i jest ignorowane w przypadku przekazywania pakietu do nuget.org. Zobacz [Zarządzanie właścicieli pakietu na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). |
| **projectUrl** | Wyświetla adres URL strony głównej pakietu, często są wyświetlane w interfejsie użytkownika oraz nuget.org. |
| **licenseUrl** | Adres URL wyświetlany w wyświetla interfejsu użytkownika, a także nuget.org licencji pakietu. |
| **iconUrl** | Adres URL obrazu 64 x 64, przezroczystość tła ma być używana jako ikonę pakietu w wyświetlania interfejsu użytkownika. Pamiętaj, że ten element zawiera *bezpośredni adres URL obrazu* , a nie adres URL strony sieci web zawierającej obraz. Na przykład, aby użyć obrazu z witryny GitHub, użyj plik raw, takie jak adres URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>. |
| **requireLicenseAcceptance** | Wartość logiczna, określając, czy klient musi monitować o konsumenta, aby zaakceptować licencji pakietu przed zainstalowaniem pakietu. |
| **DevelopmentDependency** | *(2.8 +)*  Wartość logiczna A, określając, czy pakiet jest oznaczone jako programowanie — tylko zależność, która zapobiega włączaniu jako zależności w innych pakietach pakietu. |
| **Podsumowanie** | Krótki opis pakietu do wyświetlenia interfejsu użytkownika. Pominięcie skrócona wersja `description` jest używany. |
| **releaseNotes** | *(w wersji 1.5 +)*  Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak **aktualizacje** kartę programu Visual Studio Menedżer pakietów zamiast Opis pakietu. |
| **copyright** | *(w wersji 1.5 +)*  Copyright szczegóły pakietu. |
| **Język** | Identyfikator ustawień regionalnych dla pakietu. Zobacz [tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md). |
| **Tagi**  | Rozdzieloną spacjami listę tagów i słów kluczowych, które opisują odnajdywania pakietu i pomocy pakietów za pomocą wyszukiwania i filtrowania. |
| **serviceable** | *(3.3 +)*  Programu NuGet wewnętrznego użytku. |

#### <a name="collection-elements"></a>Elementy kolekcji

| Element | Opis |
| --- | --- |
**packageTypes** | *(3.5 +)*  Kolekcji zero lub więcej `<packageType>` elementy określenie typu pakietu, jeśli inne niż tradycyjne zależności pakietu. Każdy packageType ma atrybuty *nazwa* i *wersji*. Zobacz [ustawienie typu pakietu](../create-packages/creating-a-package.md#setting-a-package-type). |
| **Zależności** | Kolekcja zero lub więcej `<dependency>` elementy określania zależności dla pakietu. Poszczególne zależności ma atrybuty *identyfikator*, *wersji*, *obejmują* (3.x+) i *wykluczyć* (3.x+). Zobacz [zależności](#dependencies) poniżej. |
| **frameworkAssemblies** | *(1.2 +)*  Kolekcji zero lub więcej `<frameworkAssembly>` elementy identyfikowanie odwołań zestawu .NET Framework, które wymaga tego pakietu, który zapewnia dodania odwołań do projektów korzystających z pakietu. Każdy frameworkAssembly ma *assemblyName* i *targetFramework* atrybutów. Zobacz [określenie zestawu struktury odwołuje się do pamięci podręcznej GAC](#specifying-framework-assembly-references-gac) poniżej. |
| **Odwołania** | *(w wersji 1.5 +)*  Kolekcji zero lub więcej `<reference>` elementy nazw zestawów, w tym pakiecie `lib` folderów, które są dodawane jako odwołania do projektu. Odwołanie do każdego ma *pliku* atrybutu. `<references>` może również zawierać `<group>` element z *targetFramework* atrybut, który następnie zawiera `<reference>` elementów. Pominięcie wszystkie odwołania w `lib` są uwzględniane. Zobacz [odwołania do zestawów jawne określenie](#specifying-explicit-assembly-references) poniżej. |
| **contentFiles** | *(3.3 +)*  Kolekcja `<files>` elementy identyfikujące pliki zawartości do uwzględnienia w projekcie odbierającą. Te pliki są określane za pomocą zestawu atrybutów, które opisują jak powinny być używane w ramach systemu projektu. Zobacz [określenie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej. |

### <a name="files-element"></a>Element Pliki

`<package>` Węzeł może zawierać `<files>` węzeł jako element równorzędny do `<metadata>`, a lub `<contentFiles>` dziecka poniżej `<metadata>`, aby określić, które pliki zestawu i zawartości do uwzględnienia w pakiecie. Zobacz [w tym pliki zestawu](#including-assembly-files) i [plików zawartości w tym](#including-content-files) dalszej części tego tematu, aby uzyskać szczegółowe informacje.

## <a name="replacement-tokens"></a>Zastąpienie tokenów

Podczas tworzenia pakietu, [ `nuget pack` polecenia](../tools/cli-ref-pack.md) zastępuje rozdzielany $ tokenów w `.nuspec` pliku `<metadata>` węzeł z wartości pochodzących z jednego pliku projektu lub `pack` polecenia `-properties`przełącznika.

W wierszu polecenia, określić wartości tokenów z `nuget pack -properties <name>=<value>;<name>=<value>`. Na przykład, takich jak można użyć tokenu `$owners$` i `$desc$` w `.nuspec` i podaj wartości w pakowania czasu w następujący sposób:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Aby użyć wartości z projektu, określ tokeny opisane w poniższej tabeli (AssemblyInfo odwołuje się do pliku w `Properties` takich jak `AssemblyInfo.cs` lub `AssemblyInfo.vb`).

Aby użyć tych tokenów, uruchom `nuget pack` z pliku projektu, a nie tylko `.nuspec`. Na przykład przy użyciu następującego polecenia `$id$` i `$version$` tokenów w `.nuspec` plików są zastępowane projektu `AssemblyName` i `AssemblyVersion` wartości:

```ps
nuget pack MyProject.csproj
```

Zwykle, gdy projekt, tworzenia `.nuspec` początkowo przy użyciu `nuget spec MyProject.csproj` automatycznie zawierające niektóre z tych standardowe tokenów. Jednak jeśli projekt nie ma wartości dla wymaganych `.nuspec` elementy, a następnie `nuget pack` zakończy się niepowodzeniem. Ponadto w przypadku zmiany wartości projektu, upewnij się odbudować przed utworzeniem pakietu; Można to zrobić wygodnie przy użyciu polecenia pakiet `build` przełącznika.

Z wyjątkiem produktów `$configuration$`, wartości w projekcie są używane zamiast wszelkie przypisane do tego samego tokenu w wierszu polecenia.

| Token | Wartość źródła | Wartość
| --- | --- | ---
| **$id$** | plik projektu | AssemblyName (tytuł) z pliku projektu |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion, jeśli jest obecna, w przeciwnym razie AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Zestaw biblioteki DLL | Konfiguracja używany do tworzenia zestawu, domyślnie używany do debugowania. Pamiętaj, że do utworzenia pakietu przy użyciu konfiguracji wydanie, zawsze używać `-properties Configuration=Release` w wierszu polecenia. |

Tokeny mogą służyć do rozpoznawania ścieżek po dołączeniu [pliki zestawu](#including-assembly-files) i [zawartości plików](#including-content-files). Tokeny mają takie same nazwy jako właściwości programu MSBuild, dzięki czemu można wybrać pliki, które zostaną uwzględnione w zależności od bieżącej konfiguracji kompilacji. Na przykład, jeśli można używać następujących tokenów w `.nuspec` pliku:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

I kompilacji zestawu których `AssemblyName` jest `LoggingLibrary` z `Release` konfiguracji w programie MSBuild, wynikowy wiersze `.nuspec` pliku w pakiecie jest następujący:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>Zależności

`<dependencies>` w elemencie `<metadata>` zawiera dowolną liczbę `<dependency>` elementy, które identyfikują inne pakiety, od których zależy Pakiet najwyższego poziomu. Atrybuty dla każdego `<dependency>` są następujące:

| Atrybut | Opis |
| --- | --- |
| `id` | (Wymagane) Identyfikator pakietu zależności, takich jak "EntityFramework" i "NUnit", czyli nazwa nuget.org pakietu zawiera stronę pakietu. |
| `version` | (Wymagane) Zakres wersji akceptowane jako zależność. Zobacz [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards) dla określonej składni. |
| include | Rozdzielana przecinkami lista dołączania/wykluczania znaczniki (patrz poniżej) wskazujący zależności, aby uwzględnić w ostatnim pakiecie. Wartość domyślna to `none`. |
| wykluczanie | Rozdzielana przecinkami lista dołączania/wykluczania znaczniki (patrz poniżej) wskazujący zależności do wykluczenia w ostatnim pakiecie. Wartość domyślna to `all`. Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`. Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`. |

| Dołączania/wykluczania tag | Odpowiednie foldery elementu docelowego |
| --- | --- |
| Pliki | Zawartość |
| środowisko uruchomieniowe | Środowisko uruchomieniowe, zasobów i FrameworkAssemblies |
| Kompilacji | lib |
| kompilacja | Kompilacja (właściwości programu MSBuild i elementy docelowe) |
| natywne | natywne |
| brak | Brak folderów |
| wszystkie | Wszystkie foldery |

Na przykład wskazać zależności następujące wiersze na `PackageA` wersji 1.1.0 lub nowszej, i `PackageB` wersja 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Następujące wiersze oznaczają zależności na te same pakiety, ale określa uwzględnienie `contentFiles` i `build` folderów do `PackageA` i wszystko, ale `native` i `compile` foldery `PackageB`"

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Uwaga: Podczas tworzenia `.nuspec` projektu używającego `nuget spec`, zależności, które istnieją w tym projekcie są automatycznie umieszczane w wynikowym `.nuspec` pliku.

### <a name="dependency-groups"></a>Grupy zależności

*W wersji 2.0 +*

Alternatywą dla pojedynczego płaską listę zależności można określić zgodnie z profil platformy docelowej projektu przy użyciu `<group>` elementów w obrębie `<dependencies>`.

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów. Te zależności są zainstalowane jednocześnie, gdy platforma docelowa jest zgodny z profilem framework projektu.

`<group>` Bez `targetFramework` atrybut jest używany jako domyślny lub powrotu listę zależności. Zobacz [platform docelowych](../reference/target-frameworks.md) identyfikatorów dokładne framework.

> [!Important]
> Format grupy nie może się zmieszać z płaska lista.

W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Odwołania do zestawów jawne

`<references>` Element jawnie określa zestawy, które docelowy projekt powinien odwoływać się przy użyciu pakietu. Gdy ten element jest obecny, NuGet Dodaj odwołania do tylko zestawy wymienionych; nie powoduje dodania odwołania do innych zestawów, w tym pakiecie `lib` folderu.

Na przykład następująca `<references>` NuGet, aby dodać odwołania do tylko powoduje, że element `xunit.dll` i `xunit.extensions.dll` nawet jeśli istnieją dodatkowe zestawy w pakiecie:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania. Korzystając z [kontraktów kodu](/dotnet/framework/debug-trace-profile/code-contracts), na przykład zestawów kontraktu musi być obok zestawy środowiska wykonawczego, do których one rozszerzyć, aby można je odnaleźć programu Visual Studio, ale zestawów kontraktu nie musi być odwołuje się projekt lub kopiowane w projekcie `bin` folderu.

Podobnie jawne odwołania mogą być używane dla platform testów jednostkowych, takich jak XUnit, którą należy jej narzędzi zestawy znajdujące się obok zestawy środowiska wykonawczego, ale nie wymaga ich uwzględniane jako odwołania do projektu.

### <a name="reference-groups"></a>Grupy odwołania

Alternatywą dla pojedynczego płaska lista odwołań można określić zgodnie z profil platformy docelowej projektu przy użyciu `<group>` elementów w obrębie `<references>`.

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów. Te odwołania są dodawane do projektu, gdy platforma docelowa jest zgodny z profilem framework projektu.

`<group>` Bez `targetFramework` atrybut jest używany jako domyślny lub powrotu lista odwołań. Zobacz [platform docelowych](../reference/target-frameworks.md) identyfikatorów dokładne framework.

> [!Important]
> Format grupy nie może się zmieszać z płaska lista.

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

Zestawy struktury są tymi, które są częścią programu .NET framework i powinna już być w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej podanej maszyny. Dzięki identyfikacji te zestawy w `<frameworkAssemblies>` elementu pakietu można upewnij się, że odwołania wymagane są dodawane do projektu, w przypadku gdy projekt nie ma takich odwołania już. Takie zestawy oczywiście nie znajdują się w pakiecie bezpośrednio.

`<frameworkAssemblies>` Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **assemblyName** | (Wymagane) Nazwa FQDN zestawu. |
| **targetFramework** | (Opcjonalnie) Określa platformę docelową, do którego odnosi się to odwołanie. Pominięcie wskazuje, że odwołanie jest stosowana do wszystkich platform. Zobacz [platform docelowych](../reference/target-frameworks.md) identyfikatorów dokładne framework. |

W poniższym przykładzie przedstawiono odwołanie do `System.Net` dla wszystkich docelowych platform oraz odwołanie do `System.ServiceModel` dla programu .NET Framework 4.0 tylko:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>W tym pliki zestawu

Jeśli wykonujesz konwencje opisanego w [utworzenie pakietu](../create-packages/creating-a-package.md), nie trzeba jawnie określić listę plików w `.nuspec` pliku. `nuget pack` Polecenie automatycznie przejmuje wymaganych plików.

> [!Important]
> Po zainstalowaniu pakietu w projekcie NuGet automatycznie dodaje odwołania do zestawów do biblioteki dll pakietu, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie. Z tego powodu należy unikać `.resources.dll` plików, które w przeciwnym razie zawiera istotne pakiet kodu.

Aby pominąć to działanie automatyczne i jawnie kontrolować pliki, które są umieszczone w pakiecie, umieść `<files>` element jako element podrzędny `<package>` (i element równorzędny `<metadata>`), identyfikowanie poszczególnych plików za pomocą oddzielnego `<file>` elementu. Na przykład:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Nuget 2.x i wcześniej i projektów przy użyciu `packages.config`, `<files>` elementu służy również do obejmuje niezmienne plików zawartości, gdy jest zainstalowany pakiet. Z projektów PackageReference i NuGet 3.3 + `<contentFiles>` zamiast tego użyć elementu. Zobacz [plików zawartości w tym](#including-content-files) poniżej szczegółowe informacje.

### <a name="file-element-attributes"></a>Atrybuty elementu

Każdy `<file>` element określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **src** | Lokalizacja pliku lub plików do uwzględnienia, mogą ulec wykluczenia określony przez `exclude` atrybutu. Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną. Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania. |
| **docelowy** | Względna ścieżka do folderu w pakiecie, gdzie znajdują się pliki źródłowe, musi rozpoczynać się od `lib`, `content`, `build`, lub `tools`. Zobacz [tworzenie .nuspec z katalogu roboczego opartych na konwencjach](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji. Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania. |

### <a name="examples"></a>Przykłady

**Jednym zestawie**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Specyficzne dla platformy docelowej jednym zestawie**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Zestaw biblioteki DLL przy użyciu symboli wieloznacznych**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Biblioteki DLL dla różnych platform**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Wykluczanie plików**

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

## <a name="including-content-files"></a>W tym pliki zawartości

Pliki zawartości są niezmienne pliki pakietu musi zawierać się w projekcie. Są niezmienne, nie mają zostać zmodyfikowane przez odbierającą projektu. Pliki zawartości przykład obejmują:

- Obrazy osadzone jako zasoby
- Pliki źródłowe, które już są kompilowane
- Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu
- Pliki konfiguracji pakietu, które należy uwzględnić w projekcie, ale nie ma potrzeby zmiany specyficznego dla projektu

Zawartości plików znajdują się w pakietu przy użyciu `<files>` elementu, określając `content` folderu w `target` atrybutu. Jednak takie pliki są ignorowane, gdy pakiet jest zainstalowany w projekcie przy użyciu PackageReference, którego użyje `<contentFiles>` elementu.

Maksymalną zgodność z używania projektów pakietu w idealnym przypadku określa pliki zawartości w obu elementów.

### <a name="using-the-files-element-for-content-files"></a>Za pomocą elementu plików dla plików zawartości

Dla plików zawartości, po prostu używany ten sam format plików zestawu jednak określić `content` jako podstawowy folder w `target` atrybutu, jak pokazano w poniższych przykładach.

**Podstawowe pliki zawartości**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Pliki zawartości ze struktury katalogów**

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

**Plik zawartości, które są specyficzne dla platformy docelowej**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Kopiowane do folderu z kropką w nazwie pliku zawartości**

W takim przypadku NuGet widzi, że rozszerzenie w `target` nie pasuje do rozszerzenia w `src` i w związku z tym traktuje część nazwy w `target` jako folder:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Pliki zawartości bez rozszerzenia**

Aby uwzględnić pliki bez rozszerzenia, należy użyć `*` lub `**` symboli wieloznacznych:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Pliki zawartości ze ścieżki głębokie i celem bezpośrednich**

W takim przypadku ponieważ pasuje do rozszerzenia plików źródłowych i docelowych, NuGet zakłada, że element docelowy nazwę pliku, a nie folder:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Zmiana nazwy pliku zawartości w pakiecie**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Wykluczanie plików**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Za pomocą elementu pliki plików zawartości

*NuGet 4.0 + z PackageReference*

Domyślnie pakiet umieszcza zawartość `contentFiles` folder (patrz poniżej) i `nuget pack` uwzględnione wszystkie pliki w tym folderze przy użyciu atrybutów domyślnych. W takim przypadku nie jest konieczne jest stosowanie `contentFiles` w węźle `.nuspec` wcale.

Do kontroli, które pliki są uwzględnione `<contentFiles>` element określa jest kolekcją `<files>` obejmują elementy, które identyfikują konkretne pliki.

Te pliki są określane za pomocą zestawu atrybutów, które opisują jak powinny być używane w ramach systemu projektu:

| Atrybut | Opis |
| --- | --- |
| **include** | (Wymagane) Lokalizacja pliku lub plików do uwzględnienia, mogą ulec wykluczenia określony przez `exclude` atrybutu. Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną. Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania. |
| **exclude** | Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji. Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania. |
| **buildAction** | Akcja kompilacji można przypisać do elementu zawartości dla programu MSBuild, takich jak `Content`, `None`, `Embedded Resource`, `Compile`itp. Wartość domyślna to `Compile`. |
| **copyToOutput** | Wartość logiczna wskazująca, czy skopiować elementy zawartości do kompilacji (lub opublikować) folder wyjściowy. Wartością domyślną jest false. |
| **spłaszczanie** | Wartość logiczna wskazująca, czy można skopiować elementy zawartości do pojedynczego folderu w danych wyjściowych kompilacji (true) czy zachowanie struktury folderów w pakiecie (false). Ta flaga działa tylko wtedy, gdy copyToOutput flaga jest ustawiona na true. Wartością domyślną jest false. |

Podczas instalowania pakietu, NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu. Jeśli wiele wpisów pasuje do tego samego pliku wszystkie wpisy są stosowane. Wpis najwyższy przesłania wpisy niższe konflikt dla tego samego atrybutu.

#### <a name="package-folder-structure"></a>Struktura folderów pakietu

Projekt pakietu wymagana struktura zawartości przy użyciu następującego wzorca:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` może być `cs`, `vb`, `fs`, `any`, lub małe odpowiednikiem danego `$(ProjectLanguage)`
- `TxM` jest żadnych moniker platformy docelowej prawnych, która obsługuje NuGet (zobacz [platform docelowych](../reference/target-frameworks.md)).
- Dowolnej struktury folderów może dołączany na końcu tej składni.

Na przykład:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Można użyć puste foldery `.` rezygnacji z zawarto dla niektórych kombinacji języka i TxM, na przykład:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Przykładowe pliki sekcji

```xml
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
```

## <a name="example-nuspec-files"></a>Przykład .nuspec plików

**Prosty `.nuspec` które nie określają zależności lub plików**

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
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
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

**A `.nuspec` z zestawów struktury**

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

W tym przykładzie poniżej są zainstalowane dla określonego projektu celów:

- .NET4 -> `System.Web`, `System.Net`
- . NET4 -> Client Profile `System.Net`
- -> Silverlight 3 `System.Json`
- -> Programu Silverlight 4 `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
