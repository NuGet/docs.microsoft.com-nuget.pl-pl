---
title: Odwołanie do pliku nuspec dla nuGet
description: Plik nuspec zawiera metadane pakietu używane podczas budowania pakietu i w celu zapewnienia informacji klientom pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ed865aad6f72752adcf3e3921287a20b961c4a8a
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901814"
---
# <a name="nuspec-reference"></a>Odwołanie do nuspec

Plik `.nuspec` jest manifestem XML, który zawiera metadane pakietu. Ten manifest jest używany zarówno do kompilowania pakietu, jak i do zapewnienia informacji klientom. Manifest jest zawsze zawarty w pakiecie.

W tym temacie:

- [Ogólny formularz i schemat](#general-form-and-schema)
- [Tokeny zastępcze](#replacement-tokens) (w przypadku korzystania z Visual Studio projektu)
- [Zależności](#dependencies)
- [Jawne odwołania do zestawu](#explicit-assembly-references)
- [Odwołania do zestawu struktury](#framework-assembly-references)
- [Łącznie z plikami zestawu](#including-assembly-files)
- [Łącznie z plikami zawartości](#including-content-files)
- [Przykładowe pliki nuspec](#example-nuspec-files)

## <a name="project-type-compatibility"></a>Zgodność typu projektu

- Użyj `.nuspec` z dla projektów innych niż zestaw `nuget.exe pack` SDK, które używają `packages.config` .

- Plik nie jest wymagany do tworzenia pakietów dla projektów w stylu zestawu SDK (zazwyczaj platformy .NET Core i projektów .NET Standard, które `.nuspec` używają [atrybutu SDK](/dotnet/core/tools/csproj#additions)). [](../resources/check-project-format.md) (Zwróć uwagę, że podczas tworzenia pakietu `.nuspec` jest generowany obiekt .

   Jeśli tworzysz pakiet przy użyciu polecenia lub , zalecamy dołącz zamiast tego wszystkie właściwości, które zwykle znajdują się `dotnet.exe pack` `msbuild pack target` w pliku [](../reference/msbuild-targets.md#pack-target) `.nuspec` projektu. Zamiast tego można jednak użyć pliku do pakowania przy użyciu [ `.nuspec` programu `dotnet.exe` lub `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).

- W przypadku projektów migrowanych z do `packages.config` [packageReference](../consume-packages/package-references-in-project-files.md) `.nuspec` plik nie jest wymagany do utworzenia pakietu. Zamiast tego użyj [msbuild -t:pack.](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)

## <a name="general-form-and-schema"></a>Ogólny formularz i schemat

Bieżący plik `nuspec.xsd` schematu można znaleźć w [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

W ramach tego schematu `.nuspec` plik ma następującą ogólną postać:

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

Aby uzyskać czytelną wizualną reprezentację schematu, otwórz plik schematu w Visual Studio w trybie projektowania i kliknij link **Eksplorator schematu XML.** Alternatywnie otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz polecenie **Pokaż Eksplorator schematu XML.** W obu sposób możesz uzyskać widok podobny do poniższego (w przypadku większości rozwiniętego):

![Visual Studio Schema Explorer z otwartym programem nuspec.xsd](media/SchemaExplorer.png)

W nazwach wszystkich elementów XML w pliku nuspec jest wielkość liter, podobnie jak w przypadku XML. Na przykład użycie elementu metadanych `<description>` jest poprawne i nie jest `<Description>` poprawne. Prawidłowa nazwa każdego elementu zawiera prawidłową wielkością wielkości.

### <a name="required-metadata-elements"></a>Wymagane elementy metadanych

Chociaż poniższe elementy są minimalnymi wymaganiami pakietu, należy [](#optional-metadata-elements) rozważyć dodanie opcjonalnych elementów metadanych w celu poprawienia ogólnego środowiska pracy deweloperów z pakietem. 

Te elementy muszą znajdować się w `<metadata>` elemencie.

#### <a name="id"></a>identyfikator 
Identyfikator pakietu bez uwzględniania liter, który musi być unikatowy w nuget.org galerii, w której znajduje się pakiet. Identyfikatory mogą nie zawierać spacji lub znaków, które nie są prawidłowe dla adresu URL, i zazwyczaj są zgodne z regułami przestrzeni nazw .NET. Aby [uzyskać wskazówki, zobacz Choosing a unique package identifier (Wybieranie unikatowego identyfikatora](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) pakietu).

Podczas przekazywania pakietu do nuget.org pole `id` jest ograniczone do 128 znaków.

#### <a name="version"></a>Wersja
Wersja pakietu, zgodnie ze wzorcem *główna.pomocnicza.poprawka.* Numery wersji mogą zawierać sufiks wersji wstępnej zgodnie z opisem [w tece Wersje pakietu](../concepts/package-versioning.md#pre-release-versions). 

Podczas przekazywania pakietu do nuget.org pole `version` jest ograniczone do 64 znaków.

#### <a name="description"></a>description (opis)
Opis pakietu do wyświetlania interfejsu użytkownika.

Podczas przekazywania pakietu do nuget.org pole `description` jest ograniczone do 4000 znaków.

#### <a name="authors"></a>Autorów
Rozdzielana przecinkami lista autorów pakietów, pasująca do nazw profilów nuget.org. Są one wyświetlane w galerii NuGet na nuget.org i są używane do odsyłania pakietów przez tych samych autorów. 

Podczas przekazywania pakietu do nuget.org pole `authors` jest ograniczone do 4000 znaków.

### <a name="optional-metadata-elements"></a>Opcjonalne elementy metadanych

#### <a name="owners"></a>Właścicieli
> [!Important]
> Właściciele są przestarzali. Zamiast tego należy używać autorów.

Rozdzielana przecinkami lista twórców pakietów używających nazw profilów w nuget.org. Jest to często ta sama lista co w pliku i jest ignorowana podczas przekazywania pakietu do `authors` nuget.org. Zobacz Managing package owners on nuget.org (Zarządzanie [właścicielami pakietów na nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)). 

#### <a name="projecturl"></a>projectUrl
Adres URL strony głównej pakietu, często wyświetlany w interfejsie użytkownika, a także adres nuget.org. 

Podczas przekazywania pakietu do nuget.org pole `projectUrl` jest ograniczone do 4000 znaków.

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> LicenseUrl jest przestarzała. Zamiast tego użyj licencji.

Adres URL licencji pakietu, często wyświetlany w interfejsach użytkownika, takich jak nuget.org.

Podczas przekazywania pakietu do nuget.org pole `licenseUrl` jest ograniczone do 4000 znaków.

#### <a name="license"></a>license (licencja)

*Obsługiwane w **programie NuGet 4.9.0** i jego produktach*

Wyrażenie licencji SPDX lub ścieżka do pliku licencji w pakiecie, często wyświetlane w interfejsach użytkownika, takich jak nuget.org. Jeśli licencjonowanie pakietu jest na podstawie wspólnej licencji, na przykład MIT lub BSD-2-Clause, użyj skojarzonego identyfikatora licencji [SPDX](https://spdx.org/licenses/). Na przykład:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org akceptuje tylko wyrażenia licencji zatwierdzone przez inicjatywę Open Source Initiative lub Free Software Foundation.

Jeśli pakiet jest licencjonowany w ramach wielu typowych licencji, możesz określić licencję złożoną przy użyciu składni wyrażeń [SPDX w wersji 2.0.](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60) Na przykład:

`<license type="expression">BSD-2-Clause OR MIT</license>`

Jeśli używasz licencji niestandardowej, która nie jest obsługiwana przez wyrażenia licencji, możesz spakć plik lub `.txt` `.md` z tekstem licencji. Na przykład:

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

Aby uzyskać odpowiednik msBuild, zobacz [Pakowanie wyrażenia licencji lub plik licencji](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

Dokładna składnia wyrażeń licencji nuGet jest opisana poniżej w [abnf](https://tools.ietf.org/html/rfc5234).

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
> IconUrl jest przestarzała. Zamiast tego użyj ikony .

Adres URL obrazu o rozdzielczości 128 x 128 z przezroczystym tłem do użycia jako ikona pakietu na ekranie interfejsu użytkownika. Upewnij się, że ten element zawiera *bezpośredni adres URL obrazu,* a nie adres URL strony internetowej zawierającej obraz. Aby na przykład użyć obrazu z usługi GitHub, użyj adresu URL pliku nieprzetworzowego, takiego <em> https://github.com/ \<username\> / \<repository\> jak \<branch\> / \<logo.png\> /raw/</em>. 

Podczas przekazywania pakietu do nuget.org pole `iconUrl` jest ograniczone do 4000 znaków.

#### <a name="icon"></a>Ikonę

*Obsługiwane z **programem NuGet 5.3.0** i jego produktami*

Jest to ścieżka do pliku obrazu w pakiecie, często wyświetlana w interfejsach nuget.org jako ikona pakietu. Rozmiar pliku obrazu jest ograniczony do 1 MB. Obsługiwane formaty plików to JPEG i PNG. Zalecamy rozdzielczość obrazu 128 x 128.

Na przykład podczas tworzenia pakietu przy użyciu narzędzia do tworzenia pakietu należy dodać następujące nuget.exe:

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

[Ikona pakietu przykład nuspec.](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

Aby uzyskać odpowiednik msBuild, zobacz Pakowanie [pliku obrazu ikony](msbuild-targets.md#packing-an-icon-image-file).

> [!Tip]
> Można określić zarówno , `icon` jak i , aby zachować zgodność z `iconUrl` poprzednimi wersjami ze źródłami, które nie obsługują systemu `icon` . Visual Studio będzie obsługiwać pakiety pochodzące ze źródła opartego `icon` na folderach w przyszłej wersji.

#### <a name="readme"></a>Plik readme

*Obsługiwane w **przypadku programu NuGet 5.10.0 (wersja zapoznawcza 2 lub 2)***

Podczas pakowania pliku readme należy użyć elementu , aby określić ścieżkę pakietu względem `readme` katalogu głównego pakietu. Oprócz tego należy się upewnić, że plik znajduje się w pakiecie. Obsługiwane formaty plików obejmują tylko markdown *(md).*

Na przykład należy dodać następujący kod do swojego nuspec, aby spakować plik readme do projektu:

```xml
<package>
  <metadata>
    ...
    <readme>docs\readme.md</readme>
    ...
  </metadata>
  <files>
    ...
    <file src="..\readme.md" target="docs\" />
    ...
  </files>
</package>
```

Aby uzyskać odpowiednik msBuild, zapoznaj się z tematem [Pakowanie pliku readme.](msbuild-targets.md#packagereadmefile) 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.

#### <a name="developmentdependency"></a>developmentDependency
*(2.8+)* Wartość logiczna określająca, czy pakiet ma być oznaczony jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w innych pakietach. W przypadku pakietu PackageReference (NuGet 4.8+) ta flaga oznacza również, że wyklucza zasoby czasu kompilacji z kompilacji. Zobacz [DevelopmentDependency support for PackageReference (Obsługa zależności dla packageReference)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)

#### <a name="summary"></a>Podsumowanie
> [!Important]
> `summary` jest przestarzała. Zamiast tego użyj polecenia cmdlet `description`.

Krótki opis pakietu do wyświetlania interfejsu użytkownika. W przypadku pominięcia używana jest obcinana `description` wersja systemu .

Podczas przekazywania pakietu do nuget.org pole `summary` jest ograniczone do 4000 znaków.

#### <a name="releasenotes"></a>releaseNotes
*(1.5+)* Opis zmian wprowadzonych w tej wersji pakietu, często używany  w interfejsie użytkownika, taki jak karta Aktualizacje Visual Studio Menedżer pakietów w miejsce opisu pakietu.

Podczas przekazywania pakietu do nuget.org pole `releaseNotes` jest ograniczone do 35 000 znaków.

#### <a name="copyright"></a>informacji o prawach autorskich,
*(1.5+)* Szczegóły praw autorskich dla pakietu.

Podczas przekazywania pakietu do nuget.org pole `copyright` jest ograniczone do 4000 znaków.

#### <a name="language"></a>language
Identyfikator regionalny pakietu. Zobacz [Creating localized packages (Tworzenie zlokalizowanych pakietów).](../create-packages/creating-localized-packages.md)

#### <a name="tags"></a>tags
Rozdzielana spacjami lista tagów i słów kluczowych, które opisują pakiet i wspomagają odnajdywanie pakietów za pomocą wyszukiwania i filtrowania. 

Podczas przekazywania pakietu do nuget.org pole `tags` jest ograniczone do 4000 znaków.

#### <a name="serviceable"></a>Sprawne 
*(3.3+)* Wewnętrznego nuGet należy używać tylko.

#### <a name="repository"></a>repozytorium
Metadane repozytorium składające się z czterech atrybutów opcjonalnych: `type` i `url` *(4.0+)*, `branch` i `commit` *(4.6+)*. Te atrybuty umożliwiają mapowanie pliku do repozytorium, które go sbudowały, z możliwością uzyskania tak szczegółowych informacji jak nazwa poszczególnych gałęzi i/lub zatwierdzenie skrótu SHA-1, który sbudowali `.nupkg` pakiet. Powinien to być publicznie dostępny adres URL, który może być wywoływany bezpośrednio przez oprogramowanie do kontroli wersji. Nie powinna to być strona HTML, ponieważ jest przeznaczona dla komputera. W przypadku łączenia ze stroną projektu zamiast `projectUrl` tego użyj pola .

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

Podczas przekazywania pakietu do nuget.org atrybut jest ograniczony do 100 znaków, a atrybut jest ograniczony do `type` `url` 4000 znaków.

#### <a name="title"></a>tytuł
Zostanie wyświetlony przyjazny dla człowieka tytuł pakietu, który może być używany w niektórych interfejsach użytkownika. (nuget.org i Menedżer pakietów w Visual Studio nie są wyświetlane tytuły)

Podczas przekazywania pakietu do nuget.org pole jest ograniczone do 256 znaków, ale nie jest używane `title` do żadnych celów wyświetlania.

#### <a name="collection-elements"></a>Elementy kolekcji

#### <a name="packagetypes"></a>packageTypes
*(3,5+)* Kolekcja zerową lub większą liczbę elementów określającą typ pakietu, jeśli jest inny niż `<packageType>` tradycyjny pakiet zależności. Każdy typ packageType ma atrybuty *nazwy i* *wersji*. Zobacz [Setting a package type (Ustawianie typu pakietu).](../create-packages/set-package-type.md)

#### <a name="dependencies"></a>zależności
Kolekcja zerowych lub większej `<dependency>` liczby elementów określających zależności dla pakietu. Każda zależność ma atrybuty *identyfikatora*, *wersji*, *dołączania* (3.x+) i *wykluczania* (3.x+). Zobacz [zależności](#dependencies-element) poniżej.

#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2+)* Kolekcja zerową lub większą liczby elementów identyfikującą odwołania do .NET Framework, których wymaga ten pakiet, co gwarantuje, że odwołania są dodawane do projektów `<frameworkAssembly>` zydujące pakiet. Każdy element frameworkAssembly ma *atrybuty assemblyName* i *targetFramework.* Zobacz [Temat Specifying framework assembly references (Określanie odwołań do zestawu struktury) poniżej.](#specifying-framework-assembly-references-gac)

#### <a name="references"></a>odwołania
*(1,5+)* Kolekcja zerową lub większą liczby elementów nazewnictwa zestawów w `<reference>` `lib` folderze pakietu, które są dodawane jako odwołania do projektu. Każde odwołanie ma *atrybut* pliku. `<references>` Może również zawierać `<group>` element z *atrybutem targetFramework,* który następnie zawiera `<reference>` elementy. W przypadku pominięcia wszystkie odwołania w `lib` są uwzględniane. Zobacz [Temat Specifying explicit assembly references (Określanie jawnych odwołań do zestawu)](#specifying-explicit-assembly-references) poniżej.

#### <a name="contentfiles"></a>contentFiles
*(3.3+)* Kolekcja `<files>` elementów, które identyfikują pliki zawartości, które mają być dołączane do projektu zużywającego zasoby. Te pliki są określane za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu. Zobacz Specifying files to include in the package below (Określanie [plików do dołączyć do poniższego](#specifying-files-to-include-in-the-package) pakietu).

#### <a name="files"></a>files 
Węzeł może zawierać węzeł jako element równorzędny dla elementu i element podrzędny w programie , aby określić, które pliki zestawu i zawartości mają zostać `<package>` `<files>` zawarte w `<metadata>` `<contentFiles>` `<metadata>` pakiecie. Aby uzyskać [szczegółowe informacje, zobacz](#including-assembly-files) Tematy Including assembly files [(W tym pliki zestawu)](#including-content-files) i Including content files (W tym pliki zawartości) w dalszej części tego tematu.

### <a name="metadata-attributes"></a>atrybuty metadanych

#### <a name="minclientversion"></a>minClientVersion
Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszaną przez nuget.exe i Visual Studio Menedżer pakietów. Jest to używane za każdym razem, gdy pakiet zależy od określonych funkcji pliku, które zostały dodane w określonej wersji `.nuspec` klienta NuGet. Na przykład pakiet używający `developmentDependency` atrybutu powinien określać wartość "2.8" dla . `minClientVersion` Podobnie pakiet używający `contentFiles` elementu (zobacz następną sekcję) powinien mieć `minClientVersion` wartość "3.3". Należy również zauważyć, że ponieważ klienci NuGet wcześniejszych niż 2.5 nie rozpoznają tej flagi, zawsze odrzucają zainstalowanie pakietu niezależnie od tego, co  `minClientVersion` zawiera.

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

Podczas tworzenia pakietu [ `nuget pack` ](../reference/cli-reference/cli-ref-pack.md) polecenie zastępuje tokeny rozdzielane $w węźle pliku wartościami, które pochodzą z pliku projektu lub `.nuspec` `<metadata>` `pack` przełącznika `-properties` polecenia.

W wierszu polecenia należy określić wartości tokenu za pomocą `nuget pack -properties <name>=<value>;<name>=<value>` polecenia . Na przykład można użyć tokenu, takiego jak i , i podać wartości `$owners$` `$desc$` w czasie `.nuspec` pakowania w następujący sposób:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Aby użyć wartości z projektu, określ tokeny opisane w poniższej tabeli (AssemblyInfo odnosi się do pliku w `Properties` pliku, takim `AssemblyInfo.cs` jak lub `AssemblyInfo.vb` ).

Aby użyć tych tokenów, uruchom plik `nuget pack` projektu, a nie tylko plik `.nuspec` . Na przykład w przypadku użycia następującego polecenia tokeny i w pliku są zastępowane `$id$` `$version$` `.nuspec` wartościami `AssemblyName` i `AssemblyVersion` projektu:

```ps
nuget pack MyProject.csproj
```

Zwykle, gdy masz projekt, tworzysz początkowo przy użyciu , `.nuspec` który automatycznie zawiera niektóre z tych `nuget spec MyProject.csproj` standardowych tokenów. Jeśli jednak projekt nie ma wartości dla wymaganych elementów, to `.nuspec` nie `nuget pack` powiedzie się. Ponadto w przypadku zmiany wartości projektu należy ponownie skompilować pakiet przed utworzeniem pakietu; Można to zrobić wygodnie za pomocą przełącznika polecenia `build` pakietu.

Z wyjątkiem , wartości w projekcie są używane w preferencji do wszystkich przypisanych do tego `$configuration$` samego tokenu w wierszu polecenia.

| Token | Źródło wartości | Wartość
| --- | --- | ---
| **$id$** | Plik projektu | Nazwa_zestawu (tytuł) z pliku projektu |
| **$version$** | Assemblyinfo | AssemblyInformationalVersion, jeśli jest obecny, w przeciwnym razie AssemblyVersion |
| **$author$** | Assemblyinfo | AssemblyCompany |
| **$title$** | Assemblyinfo | AssemblyTitle |
| **$description$** | Assemblyinfo | AssemblyDescription (Deskryptor zestawu) |
| **$copyright$** | Assemblyinfo | AssemblyCopyright |
| **$configuration$** | Biblioteka DLL zestawu | Konfiguracja używana do kompilowania zestawu, domyślnie debugowania. Pamiętaj, że aby utworzyć pakiet przy użyciu konfiguracji wydania, zawsze używasz `-properties Configuration=Release` polecenia w wierszu polecenia. |

Tokeny mogą być również używane do rozpoznawania ścieżek w przypadku dołączania [plików zestawu i](#including-assembly-files) [plików zawartości](#including-content-files). Tokeny mają takie same nazwy jak właściwości programu MSBuild, dzięki czemu można wybierać pliki do dołączona w zależności od bieżącej konfiguracji kompilacji. Jeśli na przykład użyjemy w pliku następujących `.nuspec` tokenów:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

Podczas kompilowania zestawu, którego konfiguracja jest zgodna z konfiguracją w `AssemblyName` `LoggingLibrary` `Release` programie MSBuild, wynikowe wiersze w pliku w pakiecie `.nuspec` są następujące:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Element zależności

Element `<dependencies>` w `<metadata>` elemencie zawiera dowolną liczbę elementów, które identyfikują inne pakiety, od których zależy pakiet `<dependency>` najwyższego poziomu. Atrybuty dla każdego z `<dependency>` nich są następujące:

| Atrybut | Opis |
| --- | --- |
| `id` | (Wymagane) Identyfikator pakietu zależności, taki jak "EntityFramework" i "NUnit", który jest nazwą pakietu nuget.org na stronie pakietu. |
| `version` | (Wymagane) Zakres wersji akceptowalnych jako zależność. Aby [uzyskać dokładną składnię,](../concepts/package-versioning.md#version-ranges) zobacz Package versioning (Wersjonarowanie pakietów). Wersje zmiennoprzecinowe nie są obsługiwane. |
| include | Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazująca zależność do dołączyć do końcowego pakietu. Wartość domyślna to `all`. |
| wykluczanie | Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazująca zależność do wykluczenia w końcowym pakiecie. Wartość domyślna to `build,analyzers` , która może być zbyt zapisywana. Są `content/ ContentFiles` jednak również niejawnie wykluczane w końcowym pakiecie, którego nie można zbytniego napisano. Tagi określone za `exclude` pomocą mają pierwszeństwo przed tagami określonymi za pomocą . `include` Na przykład jest `include="runtime, compile" exclude="compile"` taka sama jak `include="runtime"` . |

Podczas przekazywania pakietu do nuget.org atrybut każdej zależności jest ograniczony do 128 znaków, a atrybut jest ograniczony do `id` `version` 256 znaków.

| Dołącz/Wyklucz tag | Foldery docelowe, których dotyczy problem |
| --- | --- |
| contentFiles | Zawartość |
| środowisko uruchomieniowe | Środowisko uruchomieniowe, zasoby i frameworkAssemblies |
| kompilowanie | Lib |
| kompilacja | build (obiekty prop i obiekty docelowe PROGRAMU MSBuild) |
| natywne | natywne |
| brak | Brak folderów |
| all | Wszystkie foldery |

Na przykład następujące wiersze wskazują zależności od wersji `PackageA` 1.1.0 lub wyższej oraz `PackageB` wersji 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Poniższe wiersze wskazują zależności od tych samych pakietów, ale określają, aby uwzględnić foldery i i wszystkie elementy oprócz folderów i `contentFiles` `build` `PackageA` `native` `compile` `PackageB` "

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> Podczas tworzenia pliku z projektu przy użyciu funkcji zależności, które istnieją w tym projekcie, nie są automatycznie uwzględniane `.nuspec` `nuget spec` w wynikowym `.nuspec` pliku. Zamiast tego należy `nuget pack myproject.csproj` użyć funkcji i pobrać plik *nuspec* z wygenerowanego pliku *nupkg.* Ten *plik nuspec* zawiera zależności.

### <a name="dependency-groups"></a>Grupy zależności

*Wersja 2.0 lub nowsza*

Alternatywą dla pojedynczej listy płaskiej jest możliwość określonej zależności zgodnie z profilem struktury projektu docelowego przy użyciu `<group>` elementów w ramach . `<dependencies>`

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów. Te zależności są instalowane razem, gdy docelowa framework jest zgodna z profilem struktury projektu.

Element `<group>` bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista zależności. Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).

> [!Important]
> Format grupy nie może być połączony z listą płaską.

> [!Note]
> Format monikera struktury docelowej [(TFM)](../reference/target-frameworks.md) używanej w folderze różni się w porównaniu z `lib/ref` programem TFM używanym w programie `dependency groups` . Jeśli struktury docelowe zadeklarowane w folderze i pliku nie mają dokładnych dopasowania, polecenie zwniesie ostrzeżenie `dependencies group` `lib/ref` `.nuspec` `pack` [NuGet NU5128.](../reference/errors-and-warnings/nu5128.md)

W poniższym przykładzie pokazano różne odmiany `<group>` elementu:

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

## <a name="explicit-assembly-references"></a>Jawne odwołania do zestawu

Element jest używany przez projekty przy użyciu , aby jawnie określić zestawy, do których powinien odwoływać się projekt docelowy `<references>` `packages.config` podczas korzystania z pakietu. Odwołania jawne są zwykle używane dla zestawów tylko w czasie projektowania. Aby uzyskać więcej informacji, zobacz stronę [wybierania zestawów,](../create-packages/select-assemblies-referenced-by-projects.md) do których odwołują się projekty.

Na przykład następujący element instruuje program NuGet, aby dodał odwołania tylko do elementu i nawet jeśli w pakiecie znajdują się `<references>` `xunit.dll` dodatkowe `xunit.extensions.dll` zestawy:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>Grupy odwoływek

Alternatywą dla pojedynczej listy płaskiej można określić odwołania zgodnie z profilem struktury projektu docelowego przy użyciu `<group>` elementów w ramach `<references>` .

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów. Te odwołania są dodawane do projektu, gdy docelowa framework jest zgodna z profilem struktury projektu.

Element `<group>` bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista odwołań. Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).

> [!Important]
> Format grupy nie może być połączony z listą płaską.

W poniższym przykładzie pokazano różne odmiany `<group>` elementu :

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

## <a name="framework-assembly-references"></a>Odwołania do zestawu struktury

Zestawy struktury to te, które są częścią programu .NET Framework i powinny już być w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej maszyny. Identyfikując te zestawy w elemencie, pakiet może zapewnić, że wymagane odwołania zostaną dodane do projektu w przypadku, gdy projekt nie ma jeszcze `<frameworkAssemblies>` takich odwołań. Oczywiście takie zestawy nie są bezpośrednio zawarte w pakiecie.

Element `<frameworkAssemblies>` zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **Assemblyname** | (Wymagane) W pełni kwalifikowana nazwa zestawu. |
| **targetFramework** | (Opcjonalnie) Określa platformę docelową, do której ma zastosowanie to odwołanie. W przypadku pominięcia wskazuje, że odwołanie ma zastosowanie do wszystkich platform. Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe). |

W poniższym przykładzie pokazano odwołanie do dla wszystkich platform docelowych i odwołanie do dla .NET Framework `System.Net` `System.ServiceModel` 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Łącznie z plikami zestawu

W przypadku śledzenia zgodnie z konwencjami opisanymi w tece [Tworzenie](../create-packages/creating-a-package.md)pakietu nie trzeba jawnie określać listy plików w `.nuspec` pliku. Polecenie `nuget pack` automatycznie pobiera niezbędne pliki.

> [!Important]
> Po zainstalowaniu pakietu w projekcie pakiet NuGet automatycznie dodaje odwołania do zestawów do bibliotek DLL *pakietu,* z wyłączeniem tych, które są nazwane, ponieważ zakłada się, że są zlokalizowanymi zestawami `.resources.dll` satelickimi. Z tego powodu należy unikać używania `.resources.dll` dla plików, które w przeciwnym razie zawierają podstawowy kod pakietu.

Aby pominąć to automatyczne zachowanie i jawnie kontrolować, które pliki znajdują się w pakiecie, umieść element jako element podrzędny (i element równorzędny ), identyfikując każdy plik z `<files>` `<package>` `<metadata>` oddzielnym `<file>` elementem. Na przykład:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

W programie NuGet 2.x i starszych wersjach oraz projektach korzystających z programu element jest również używany do dołączania niezmiennych plików zawartości podczas `packages.config` `<files>` instalowania pakietu. W przypadku pakietów NuGet 3.3+ i projektów PackageReference zamiast tego `<contentFiles>` jest używany element . Aby uzyskać [szczegółowe informacje, zobacz Temat Including content files](#including-content-files) below (W tym pliki zawartości poniżej).

### <a name="file-element-attributes"></a>Atrybuty elementu pliku

Każdy `<file>` element określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **src** | Lokalizacja pliku lub plików dołączyć, z zastrzeżeniem wykluczeń określonych przez `exclude` atrybut. Ścieżka jest względna do `.nuspec` pliku, chyba że określono ścieżkę bezwzględną. Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów. |
| **Docelowego** | Ścieżka względna do folderu w pakiecie, w którym znajdują się pliki źródłowe, która musi zaczynać się `lib` od , , , lub `content` `build` `tools` . Zobacz [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)(Tworzenie nuspec z katalogu roboczego opartego na konwencji). |
| **wykluczanie** | Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji. Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów. |

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

**Pojedynczy zestaw specyficzny dla struktury docelowej**

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

**Zestaw bibliotek DLL korzystających z symbolu wieloznacznego**

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

## <a name="including-content-files"></a>Łącznie z plikami zawartości

Pliki zawartości to pliki niezmienne, które pakiet musi uwzględnić w projekcie. Będąc niezmienne, nie są one przeznaczone do modyfikacji przez projekt konsumowania. Przykładowe pliki zawartości:

- Obrazy osadzone jako zasoby
- Pliki źródłowe, które zostały już skompilowane
- Skrypty, które muszą zostać dołączone do danych wyjściowych kompilacji projektu
- Pliki konfiguracji pakietu, które muszą zostać uwzględnione w projekcie, ale nie wymagają żadnych zmian specyficznych dla projektu

Pliki zawartości są zawarte w pakiecie przy użyciu `<files>` elementu , określając folder w `content` `target` atrybutze . Jednak takie pliki są ignorowane, gdy pakiet jest instalowany w projekcie przy użyciu funkcji PackageReference, która zamiast tego używa `<contentFiles>` elementu .

Aby uzyskać maksymalną zgodność z konsumowanie projektów, pakiet w idealnym przypadku określa pliki zawartości w obu elementach.

### <a name="using-the-files-element-for-content-files"></a>Używanie elementu files dla plików zawartości

W przypadku plików zawartości należy po prostu użyć tego samego formatu co dla plików zestawu, ale określić jako folder podstawowy w atrybutze , jak pokazano w `content` `target` poniższych przykładach.

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

**Pliki zawartości ze strukturą katalogów**

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

**Plik zawartości specyficzny dla struktury docelowej**

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

**Plik zawartości skopiowany do folderu z kropką w nazwie**

W takim przypadku program NuGet widzi, że rozszerzenie w pliku nie jest zgodne z rozszerzeniem w pliku i w związku z tym traktuje tę część nazwy `target` `src` w pliku jako `target` folder:

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

**Pliki zawartości bez rozszerzeń**

Aby dołączyć pliki bez rozszerzenia, użyj `*` symboli `**` wieloznacznych lub :

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

**Pliki zawartości ze ścieżką głęboką i głębokim elementem docelowym**

W tym przypadku, ponieważ rozszerzenia pliku źródłowego i docelowego są zgodne, nuGet zakłada, że element docelowy jest nazwą pliku, a nie folderem:

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

*NuGet 4.0+ z packageReference*

Domyślnie pakiet umieszcza zawartość w folderze (patrz poniżej) i uwzględnia wszystkie pliki w `contentFiles` `nuget pack` tym folderze przy użyciu atrybutów domyślnych. W takim przypadku nie trzeba w ogóle uwzględniać `contentFiles` węzła `.nuspec` w węźle .

Aby kontrolować, które pliki są dołączone, `<contentFiles>` element określa kolekcję `<files>` elementów, które identyfikują dokładne pliki obejmują.

Te pliki są określane za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu:

| Atrybut | Opis |
| --- | --- |
| **Obejmują** | (Wymagane) Lokalizacja pliku lub plików dołączyć, z zastrzeżeniem wykluczeń określonych przez `exclude` atrybut. Ścieżka jest względna do `contentFiles` folderu, chyba że określono ścieżkę bezwzględną. Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów. |
| **wykluczanie** | Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji. Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów. |
| **buildAction** | Akcja kompilacji do przypisania do elementu zawartości dla programu MSBuild, na przykład `Content` , `None` , , `Embedded Resource` `Compile` itp. Wartość domyślna to `Compile` . |
| **copyToOutput** | Wartość logiczna wskazująca, czy kopiować elementy zawartości do folderu wyjściowego kompilacji (lub publikowania). Wartością domyślną jest false. |
| **Spłaszczyć** | Wartość logiczna wskazująca, czy kopiować elementy zawartości do jednego folderu w danych wyjściowych kompilacji (true), czy zachować strukturę folderów w pakiecie (false). Ta flaga działa tylko wtedy, gdy flaga copyToOutput jest ustawiona na wartość true. Wartością domyślną jest false. |

Podczas instalowania pakietu pakiet NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu. Jeśli wiele wpisów pasuje do tego samego pliku, zostaną zastosowane wszystkie wpisy. Wpis o najwyższej wartości zastępuje niższe wpisy, jeśli występuje konflikt dla tego samego atrybutu.

#### <a name="package-folder-structure"></a>Struktura folderów pakietów

Projekt pakietu powinien mieć strukturę zawartości przy użyciu następującego wzorca:

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- `codeLanguages` może być `cs` , , , , lub `vb` `fs` `any` małymi literami równoważnymi danej `$(ProjectLanguage)`
- `TxM`to dowolna prawna docelowa podsieć struktury, która jest wspierana przez program NuGet [(zobacz Platforme docelowe).](../reference/target-frameworks.md)
- Na końcu tej składni można dołączyć dowolną strukturę folderów.

Na przykład:

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

Puste foldery mogą być używany do rezygnacji z dostarczania zawartości dla niektórych kombinacji języka i `.` TxM, na przykład:

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

## <a name="framework-reference-groups"></a>Grupy odwoływać się do struktury

*Tylko packageReference w wersji 5.1+*

Odwołania do platformy to pojęcie platformy .NET Core reprezentujące platformy udostępnione, takie jak WPF lub Windows Forms.
Określając platformę udostępnioną, pakiet zapewnia, że wszystkie jego zależności struktury zostaną uwzględnione w projekcie odwołującym się.

Każdy `<group>` element wymaga `targetFramework` atrybutu i zero lub więcej `<frameworkReference>` elementów.

W poniższym przykładzie pokazano nuspec wygenerowany dla projektu WPF platformy .NET Core.
Należy pamiętać, że ręczne tworzenie nuspecs, które zawierają odwołania do struktury, nie jest zalecane. Zamiast tego rozważ [użycie pakietu targets,](msbuild-targets.md) który automatycznie wywnioskuje je z projektu.

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

**Prosta, `.nuspec` która nie określa zależności ani plików**

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

**A `.nuspec` z zestawami struktury**

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

W tym przykładzie dla określonych celów projektu są instalowane następujące elementy:

- . NET4 — > `System.Web` , `System.Net`
- . Profil klienta NET4 — > `System.Net`
- Silverlight 3 —> `System.Json`
- WindowsPhone — > `Microsoft.Devices.Sensors`
