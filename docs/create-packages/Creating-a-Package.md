---
title: Tworzenie pakietu NuGet przy użyciu pliku wiersza polecenia nuget.exe
description: Szczegółowy przewodnik po procesie projektowania i tworzenia pakietu NuGet, w tym kluczowych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b3e6f0efc9e2e12de186ffd4ce29d496d07d5fc4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428948"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>Tworzenie pakietu przy użyciu pliku wiersza polecenia nuget.exe

Bez względu na to, co pakiet robi lub jaki kod zawiera, należy użyć jednego z narzędzi interfejsu wiersza polecenia, albo `nuget.exe` lub `dotnet.exe`, aby spakować tę funkcjonalność do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów. Aby zainstalować narzędzia NuGet CLI, zobacz [Instalowanie narzędzi klienckich NuGet](../install-nuget-client-tools.md). Należy zauważyć, że program Visual Studio nie zawiera automatycznie narzędzia interfejsu wiersza polecenia.

- W przypadku projektów w stylu innych niż SDK, zazwyczaj .NET Framework projektów, wykonaj kroki opisane w tym artykule, aby utworzyć pakiet. Aby uzyskać instrukcje krok po kroku `nuget.exe` przy użyciu programu Visual Studio i interfejsu wiersza polecenia, zobacz [Tworzenie i publikowanie pakietu .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).

- W przypadku projektów .NET Core i .NET Standard, które używają [formatu w stylu zestawu SDK,](../resources/check-project-format.md)oraz innych projektów w stylu zestawu SDK, zobacz [Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet](creating-a-package-dotnet-cli.md).

- W przypadku projektów `packages.config` migrowanych z programu [PackageReference](../consume-packages/package-references-in-project-files.md)należy użyć [pliku msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

Technicznie rzecz biorąc pakiet NuGet to tylko plik ZIP, który `.nupkg` został przemianowany z rozszerzeniem i którego zawartość odpowiada niektórym konwencjom. W tym temacie opisano szczegółowy proces tworzenia pakietu, który spełnia te konwencje.

Pakowanie rozpoczyna się od skompilowanego kodu (zestawów), symboli i/lub innych plików, które chcesz dostarczyć jako pakiet (zobacz [Omówienie i przepływ pracy](overview-and-workflow.md)). Ten proces jest niezależny od kompilowania lub w inny sposób generowania plików, które idą do pakietu, chociaż można rysować z informacji w pliku projektu, aby zachować skompilowane zestawy i pakiety w synchronizacji.

> [!Important]
> W tym temacie stosuje się do projektów w stylu innych niż SDK, zazwyczaj projektów innych niż .NET Core i .NET Standard projektów przy użyciu programu Visual Studio 2017 i wyższych wersji i NuGet 4.0+.

## <a name="decide-which-assemblies-to-package"></a>Określanie, które zestawy mają być pakowane

Większość pakietów ogólnego przeznaczenia zawiera jeden lub więcej zestawów, które inni deweloperzy mogą używać w swoich własnych projektach.

- Ogólnie rzecz biorąc najlepiej jest mieć jeden zestaw na pakiet NuGet, pod warunkiem, że każdy zestaw jest niezależnie przydatne. Na przykład, jeśli `Utilities.dll` masz, `Parser.dll`który `Parser.dll` zależy od , i jest przydatny samodzielnie, a następnie utworzyć jeden pakiet dla każdego. Pozwala to programistom `Parser.dll` na `Utilities.dll`korzystanie niezależnie od .

- Jeśli biblioteka składa się z wielu zestawów, które nie są niezależnie przydatne, to dobrze jest połączyć je w jeden pakiet. Przy użyciu poprzedniego `Parser.dll` przykładu, jeśli zawiera `Utilities.dll`kod, który jest używany `Parser.dll` tylko przez , to jest w porządku, aby zachować w tym samym pakiecie.

- Podobnie, jeśli `Utilities.dll` zależy `Utilities.resources.dll`od , gdzie znowu ten ostatni nie jest przydatny sam, a następnie umieścić zarówno w tym samym opakowaniu.

Zasoby są w istocie szczególnym przypadkiem. Gdy pakiet jest zainstalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu dll pakietu, `.resources.dll` z *wyłączeniem* tych, które są nazwane, ponieważ są one uważane za zlokalizowane zestawy sateliczne (zobacz [Tworzenie zlokalizowanych pakietów](creating-localized-packages.md)). Z tego powodu `.resources.dll` należy unikać używania dla plików, które w przeciwnym razie zawierają kod pakietu istotne.

Jeśli biblioteka zawiera zestawy współdziałacze COM, postępuj zgodnie z dodatkowymi wskazówkami w [aplikacji Tworzenie pakietów z zestawami współdziałań COM.](author-packages-with-com-interop-assemblies.md)

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rola i struktura pliku nuspec

Gdy wiesz, jakie pliki chcesz spakować, następnym krokiem jest `.nuspec` utworzenie manifestu pakietu w pliku XML.

Manifest:

1. Opisuje zawartość pakietu i sam znajduje się w pakiecie.
1. Dyski zarówno tworzenie pakietu i instruuje NuGet na jak zainstalować pakiet w projekcie. Na przykład manifest identyfikuje inne zależności pakietu, takie jak NuGet można również zainstalować te zależności, gdy pakiet główny jest zainstalowany.
1. Zawiera właściwości wymagane i opcjonalne, jak opisano poniżej. Aby uzyskać dokładne informacje, w tym inne właściwości, o których nie wspomniano tutaj, zobacz [.nuspec reference](../reference/nuspec.md).

Wymagane właściwości:

- Identyfikator pakietu, który musi być unikatowy w galerii, która obsługuje pakiet.
- Określony numer wersji w postaci *Major.Minor.Patch[-Sufiks]* gdzie *-Suffix* identyfikuje [wersje przedpremierowe](prerelease-packages.md)
- Tytuł pakietu, który powinien pojawić się na hoście (np. nuget.org)
- Informacje o autorze i właścicielu.
- Długi opis paczki.

Typowe właściwości opcjonalne:

- Informacje o wersji
- Informacje o prawach autorskich
- Krótki opis interfejsu [użytkownika Menedżera pakietów w programie Visual Studio](../consume-packages/install-use-packages-visual-studio.md)
- Identyfikator ustawień regionalnych
- Adres URL projektu
- Licencja jako wyrażenie`licenseUrl` lub plik ( jest przestarzałe, użyj [ `license` elementu metadanych nuspec)](../reference/nuspec.md#license)
- Ikona URL
- Listy zależności i odwołań
- Tagi ułatwiających wyszukiwanie w galerii

Poniżej znajduje się typowy (ale `.nuspec` fikcyjny) plik z komentarzami opisującymi właściwości:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [packages.config](../reference/packages-config.md) i [Package versioning](../concepts/package-versioning.md). Jest również możliwe do powierzchni zasobów z zależności bezpośrednio w `include` `exclude` pakiecie przy `dependency` użyciu i atrybuty na element. Zobacz [.nuspec Reference - Zależności](../reference/nuspec.md#dependencies).

Ponieważ manifest znajduje się w pakiecie utworzonym z niego, można znaleźć dowolną liczbę dodatkowych przykładów, badając istniejące pakiety. Dobrym źródłem jest folder *pakietów globalnych* na komputerze, którego lokalizacja jest zwracana przez następujące polecenie:

```cli
nuget locals -list global-packages
```

Przejdź do dowolnego *folderu package\version,* `.nupkg` skopiuj `.zip` plik do pliku, a następnie otwórz ten `.zip` plik i sprawdź w `.nuspec` nim.

> [!Note]
> Podczas tworzenia `.nuspec` z projektu Visual Studio manifest zawiera tokeny, które są zastępowane informacjami z projektu, gdy pakiet jest zbudowany. Zobacz [Tworzenie nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).

## <a name="create-the-nuspec-file"></a>Tworzenie pliku nuspec

Tworzenie pełnego manifestu zazwyczaj rozpoczyna `.nuspec` się od pliku podstawowego wygenerowanego za pomocą jednej z następujących metod:

- [Katalog roboczy oparty na konwencji](#from-a-convention-based-working-directory)
- [Biblioteka DLL zespołu](#from-an-assembly-dll)
- [Projekt programu Visual Studio](#from-a-visual-studio-project)    
- [Nowy plik z wartościami domyślnymi](#new-file-with-default-values)

Następnie edytuj plik ręcznie, tak aby opisywłaścił dokładną zawartość, którą chcesz w pakiecie końcowym.

> [!Important]
> Wygenerowane `.nuspec` pliki zawierają symbole zastępcze, które muszą `nuget pack` zostać zmodyfikowane przed utworzeniem pakietu za pomocą polecenia. To polecenie kończy `.nuspec` się niepowodzeniem, jeśli zawiera żadnych symboli zastępczych.

### <a name="from-a-convention-based-working-directory"></a>Z katalogu roboczego opartego na konwencji

Ponieważ pakiet NuGet to tylko plik ZIP, który `.nupkg` został zmieniony z rozszerzeniem, często najłatwiej jest utworzyć odpowiednią strukturę folderów w lokalnym systemie plików, a następnie utworzyć `.nuspec` plik bezpośrednio z tej struktury. Następnie `nuget pack` polecenie automatycznie dodaje wszystkie pliki w tej strukturze folderów `.`(z wyłączeniem folderów, które zaczynają się od , co pozwala zachować prywatne pliki w tej samej strukturze).

Zaletą tego podejścia jest to, że nie trzeba określić w manifeście, które pliki mają zostać uwzględnione w pakiecie (jak wyjaśniono w dalszej części tego tematu). Możesz po prostu mieć proces kompilacji produkcji dokładnej struktury folderu, który przechodzi do pakietu i można łatwo dołączyć inne pliki, które nie mogą być częścią projektu w przeciwnym razie:

- Zawartość i kod źródłowy, które powinny być wstrzykiwane do projektu docelowego.
- Skrypty środowiska PowerShell
- Przekształcenia do istniejących plików konfiguracji i kodu źródłowego w projekcie.

Konwencje folderów są następujące:

| Folder | Opis | Działanie po zainstalowaniu pakietu |
| --- | --- | --- |
| (korzeń) | Lokalizacja dla readme.txt | Program Visual Studio wyświetla plik readme.txt w katalogu głównym pakietu po zainstalowaniu pakietu. |
| lib/{tfm} | Pliki`.dll`zestawu (`.xml`), dokumentacji`.pdb`( ) i symbolu ( ) dla danego monikera ram docelowych (TFM) | Zestawy są dodawane jako odwołania do kompilacji, a także środowiska wykonawczego; `.xml` i `.pdb` skopiowane do folderów projektu. Zobacz [Obsługa wielu struktur docelowych](supporting-multiple-target-frameworks.md) do tworzenia podfolderów specyficznych dla platformy docelowej. |
| ref/{tfm} | Pliki`.dll`zestawu (`.pdb`) i symbol ( ) dla danego monikera ram docelowych (TFM) | Zestawy są dodawane jako odwołania tylko dla czasu kompilacji; Więc nic nie zostanie skopiowane do folderu bin projektu. |
| środowiska wykonawcze | Pliki zestawu specyficznego dla architektury (`.dll`), symbolu (`.pdb`) i zasobów natywnych (`.pri`) | Zestawy są dodawane jako odwołania tylko dla środowiska wykonawczego; inne pliki są kopiowane do folderów projektu. Zawsze powinien istnieć odpowiedni `AnyCPU` (TFM) `/ref/{tfm}` określonego zestawu w folderze, aby zapewnić odpowiedni zestaw czasu kompilacji. Zobacz [Obsługa wielu struktur docelowych](supporting-multiple-target-frameworks.md). |
| content | Dowolne pliki | Zawartość jest kopiowana do katalogu głównego projektu. Potraktowanie folderu **zawartości** jako katalogu głównego aplikacji docelowej, która ostatecznie zużywa pakiet. Aby pakiet dodać obraz w folderze */images* aplikacji, umieść go w folderze *zawartości/obrazów* pakietu. |
| kompilacja | *(3,x+)* MSBuild `.targets` `.props` i pliki | Automatycznie wstawiany do projektu. |
| buildMultiTargeting | *(4,0+)* MSBuild `.targets` `.props` i pliki do kierowania krzyżowego | Automatycznie wstawiany do projektu. |
| buildTransitive | *(5,0+)* MSBuild `.targets` `.props` i pliki, które przepływają przechodnie do dowolnego projektu zużywającego. Zobacz stronę [funkcji.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) | Automatycznie wstawiany do projektu. |
| narzędzia | Skrypty i programy programu Powershell dostępne z konsoli Menedżera pakietów | Folder `tools` jest dodawany `PATH` do zmiennej środowiskowej tylko dla konsoli `PATH` Menedżera pakietów (w szczególności *nie* do zestawu ustawionego dla MSBuild podczas tworzenia projektu). |

Ponieważ struktura folderów może zawierać dowolną liczbę zestawów dla dowolnej liczby struktur docelowych, ta metoda jest konieczna podczas tworzenia pakietów, które obsługują wiele struktur.

W każdym razie po utworzeniu żądanej struktury folderów uruchom następujące polecenie `.nuspec` w tym folderze, aby utworzyć plik:

```cli
nuget spec
```

Ponownie wygenerowane `.nuspec` nie zawiera żadnych jawnych odwołań do plików w strukturze folderów. NuGet automatycznie zawiera wszystkie pliki podczas tworzenia pakietu. Nadal jednak trzeba edytować wartości zastępcze w innych częściach manifestu.

### <a name="from-an-assembly-dll"></a>Z biblioteki DLL zestawu

W prostym przypadku tworzenia pakietu z zestawu, można `.nuspec` wygenerować plik z metadanych w zestawie za pomocą następującego polecenia:

```cli
nuget spec <assembly-name>.dll
```

Za pomocą tego formularza zastępuje kilka symboli zastępczych w manifeście z określonych wartości z zestawu. Na przykład `<id>` właściwość jest ustawiona na `<version>` nazwę zestawu i jest ustawiona na wersję zestawu. Inne właściwości w manifeście, jednak nie mają pasujące wartości w zestawie i w związku z tym nadal zawierają symbole zastępcze.

### <a name="from-a-visual-studio-project"></a>Z projektu programu Visual Studio

Tworzenie `.nuspec` z `.csproj` pliku `.vbproj` lub jest wygodne, ponieważ inne pakiety, które zostały zainstalowane w tym projekcie są automatycznie odwoływane jako zależności. Wystarczy użyć następującego polecenia w tym samym folderze co plik projektu:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Wynikowy `<project-name>.nuspec` plik zawiera *tokeny,* które są zastępowane w czasie pakowania wartościami z projektu, w tym odwołaniami do innych pakietów, które zostały już zainstalowane.

Jeśli masz zależności pakietu do uwzględnienia w *.nuspec*, zamiast użyć `nuget pack`, i uzyskać plik *nuspec* z poziomu wygenerowanego pliku *nupkg.* Na przykład użyj następującego polecenia.

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

Token jest rozdzielany `$` symbolami po obu stronach właściwości projektu. Na przykład `<id>` wartość w manifeście wygenerowanym w ten sposób zazwyczaj pojawia się w następujący sposób:

```xml
<id>$id$</id>
```

Ten token jest `AssemblyName` zastępowany wartością z pliku projektu w czasie pakowania. Aby uzyskać dokładne mapowanie `.nuspec` wartości projektu do tokenów, zobacz [odwołanie tokeny zastępcze](../reference/nuspec.md#replacement-tokens).

Tokeny zwalniają cię z konieczności aktualizacji kluczowych `.nuspec` wartości, takich jak numer wersji w podczas aktualizowania projektu. (Zawsze można zastąpić tokeny wartościami literału, w razie potrzeby). 

Należy zauważyć, że istnieje kilka dodatkowych opcji pakowania dostępnych podczas pracy z projektu programu Visual Studio, zgodnie z opisem w [Running nuget pack do wygenerowania pliku nupkg](#run-nuget-pack-to-generate-the-nupkg-file) później.

#### <a name="solution-level-packages"></a>Pakiety na poziomie rozwiązania

*Tylko nuGet 2.x. Niedostępne w nuget 3.0+.*

NuGet 2.x obsługiwane pojęcie pakietu na poziomie rozwiązania, który instaluje narzędzia lub dodatkowe polecenia `tools` dla Konsoli Menedżera pakietów (zawartość folderu), ale nie dodaje odwołania, zawartość lub budować dostosowania do żadnych projektów w rozwiązaniu. Takie pakiety nie zawierają `lib` `content`żadnych `build` plików w jego bezpośrednim , lub foldery, `content`a `build` żadna z jego zależności nie ma plików w ich odpowiednich `lib`, lub folderów.

NuGet śledzi zainstalowane pakiety `packages.config` na poziomie `.nuget` rozwiązania w pliku w `packages.config` folderze, a nie w pliku projektu.

### <a name="new-file-with-default-values"></a>Nowy plik z wartościami domyślnymi

Następujące polecenie tworzy domyślny manifest z symbolami zastępczymi, który zapewnia rozpoczęcie od prawidłowej struktury pliku:

```cli
nuget spec [<package-name>]
```

Jeśli pominiesz \<\>nazwę pakietu, wynikowy plik to `Package.nuspec`. Jeśli podasz nazwę, `Contoso.Utility.UsefulStuff`taką jak `Contoso.Utility.UsefulStuff.nuspec`, plik jest .

Wynikowy `.nuspec` zawiera symbole zastępcze `projectUrl`dla wartości, takich jak . Przed użyciem go do utworzenia pliku `.nupkg` końcowego należy edytować plik.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Wybieranie unikatowego identyfikatora pakietu i ustawianie numeru wersji

Identyfikator pakietu (`<id>` element) i numer`<version>` wersji ( element) są dwie najważniejsze wartości w manifeście, ponieważ jednoznacznie identyfikują dokładny kod, który jest zawarty w pakiecie.

**Najważniejsze wskazówki dotyczące identyfikatora pakietu:**

- **Unikatowość:** identyfikator musi być unikatowy w nuget.org lub dowolnej galerii hostuje pakiet. Przed podjęciem decyzji o identyfikatorze przeszukaj odpowiednią galerię, aby sprawdzić, czy nazwa jest już używana. Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej `Contoso.`części identyfikatora, takiej jak .
- Nazwy podobne do **przestrzeni nazw:** Postępuj zgodnie ze wzorcem podobnym do obszarów nazw w domenie .NET, używając notacji kropkowej zamiast łączników. Na przykład `Contoso.Utility.UsefulStuff` użyj, `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`a nie lub . Konsumenci również znaleźć przydatne, gdy identyfikator pakietu pasuje do obszarów nazw używanych w kodzie.
- **Przykładowe pakiety:** Jeśli tworzysz pakiet przykładowego kodu, który `.Sample` pokazuje, jak używać innego pakietu, `Contoso.Utility.UsefulStuff.Sample`dołącz jako sufiks do identyfikatora, jak w . (Przykładowy pakiet będzie oczywiście zależny od innego pakietu.) Podczas tworzenia przykładowego pakietu należy użyć opisanej wcześniej metody katalogu roboczego opartego na konwencji. W `content` folderze rozmieść przykładowy `\Samples\<identifier>` kod `\Samples\Contoso.Utility.UsefulStuff.Sample`w folderze o nazwie w pliku .

**Najważniejsze wskazówki dotyczące wersji pakietu:**

- Ogólnie rzecz biorąc ustaw wersję pakietu, aby dopasować bibliotekę, chociaż nie jest to ściśle wymagane. Jest to prosta sprawa, gdy ograniczysz pakiet do pojedynczego zestawu, jak opisano wcześniej w [podejmowaniu decyzji, które zestawy do spakowania](#decide-which-assemblies-to-package). Ogólnie rzecz biorąc, należy pamiętać, że NuGet sam zajmuje się wersjami pakietów podczas rozpoznawania zależności, a nie wersji zestawu.
- Korzystając z niestandardowego schematu wersji, należy wziąć pod uwagę reguły wersji NuGet, jak wyjaśniono w [wersji pakietu.](../concepts/package-versioning.md)

> Poniższa seria krótkich wpisów na blogu są również pomocne w zrozumieniu przechowywania wersji:
>
> - [Część 1: Biorąc na DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2: Podstawowy algorytm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: Ujednolicenie za pomocą przekierowań wiążących](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>Dodawanie pliku readme i innych plików

Aby bezpośrednio określić pliki do uwzględnienia `<files>` w pakiecie, `.nuspec` użyj węzła w pliku, który *następuje po* tagu: `<metadata>`

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Korzystając z podejścia opartego na konwencji katalogu roboczego, można umieścić readme.txt `content` w katalogu głównym pakietu i innej zawartości w folderze. W `<file>` manifeście nie są potrzebne żadne elementy.

Po dołączeniu pliku `readme.txt` o nazwie w katalogu głównym pakietu program Visual Studio wyświetla zawartość tego pliku jako zwykły tekst bezpośrednio po zainstalowaniu pakietu bezpośrednio. (Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności). Na przykład, oto jak readme dla pakietu HtmlAgilityPack pojawia się:

![Wyświetlanie pliku readme dla pakietu NuGet po instalacji](media/Create_01-ShowReadme.png)

> [!Note]
> Jeśli dodasz `<files>` pusty węzeł `.nuspec` w pliku, NuGet nie zawiera żadnych innych treści w `lib` pakiecie innych niż to, co znajduje się w folderze.

## <a name="include-msbuild-props-and-targets-in-a-package"></a>Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie

W niektórych przypadkach można dodać niestandardowe obiekty docelowe kompilacji lub właściwości w projektach, które korzystają z pakietu, takich jak uruchamianie niestandardowego narzędzia lub procesu podczas kompilacji. Można to zrobić, umieszczając `<package_id>.targets` pliki `<package_id>.props` w `Contoso.Utility.UsefulStuff.targets`formularzu `\build` lub (na przykład) w folderze projektu.

Pliki w `\build` folderze głównym są uważane za odpowiednie dla wszystkich struktur docelowych. Aby udostępnić pliki specyficzne dla struktury, należy je najpierw umieścić w odpowiednich podfolderach, takich jak:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Następnie w `.nuspec` pliku, należy odwołać się `<files>` do tych plików w węźle:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

W tym MSBuild rekwizyty i obiekty docelowe w pakiecie został [wprowadzony z NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), dlatego zaleca się dodać `minClientVersion="2.5"` atrybut do `metadata` elementu, aby wskazać minimalną wersję klienta NuGet wymagane do korzystania z pakietu.

Gdy NuGet instaluje `\build` pakiet z plikami, `<Import>` dodaje MSBuild elementów `.props` w pliku projektu wskazując i `.targets` plików. (`.props` jest dodawany w górnej części pliku projektu; `.targets` dodaje się na dole).) Oddzielny warunkowy element MSBuild `<Import>` jest dodawany dla każdej struktury docelowej.

MSBuild `.props` `.targets` i pliki dla kierowania cross-framework `\buildMultiTargeting` mogą być umieszczane w folderze. Podczas instalacji pakietu NuGet `<Import>` dodaje odpowiednie elementy do pliku projektu z warunkiem, że struktura docelowa nie jest ustawiona (właściwość `$(TargetFramework)` MSBuild musi być pusta).

W nuget 3.x cele nie są dodawane do projektu, ale zamiast tego są udostępniane za pośrednictwem `{projectName}.nuget.g.targets` i `{projectName}.nuget.g.props`.

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>Uruchom pakiet nuget, aby wygenerować plik nupkg

W przypadku używania zestawu lub katalogu roboczego opartego `nuget pack` na `.nuspec` konwencji `<project-name>` utwórz pakiet, uruchamiając plik, zastępując określoną nazwę pliku:

```cli
nuget pack <project-name>.nuspec
```

Podczas korzystania z projektu `nuget pack` programu Visual Studio, uruchom z pliku projektu, który automatycznie ładuje `.nuspec` plik projektu i zastępuje wszystkie tokeny w nim przy użyciu wartości w pliku projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Korzystanie z pliku projektu bezpośrednio jest niezbędne do zastąpienia tokenu, ponieważ projekt jest źródłem wartości tokenu. Zastępowanie tokenu nie `nuget pack` ma `.nuspec` miejsca, jeśli używasz z plikiem.

We wszystkich `nuget pack` przypadkach nie obejmuje folderów rozpoczynających `.git` się `.hg`od kropki, takich jak lub .

NuGet wskazuje, jeśli istnieją błędy `.nuspec` w pliku, które wymagają poprawiania, takie jak zapominanie o zmianie wartości zastępczych w manifeście.

Po `nuget pack` pomyślnym, `.nupkg` masz plik, który można opublikować w odpowiedniej galerii, zgodnie z opisem w [Publikowanie pakietu](../nuget-org/publish-a-package.md).

> [!Tip]
> Pomocnym sposobem zbadania pakietu po jego utworzeniu jest otwarcie go w narzędziu [Eksplorator pakietów.](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) Daje to graficzny widok zawartości pakietu i jego manifestu. Można również zmienić nazwę `.nupkg` pliku `.zip` wynikowego na plik i eksplorować jego zawartość bezpośrednio.

### <a name="additional-options"></a>Opcje dodatkowe

Można użyć różnych przełączników wiersza polecenia, `nuget pack` aby wykluczyć pliki, zastąpić numer wersji w manifeście i zmienić folder wyjściowy, między innymi funkcje. Pełna lista znajduje się w [1999 roku.](../reference/cli-reference/cli-ref-pack.md)

Następujące opcje są kilka, które są wspólne z projektami programu Visual Studio:

- **Projekty, do których istnieją odwołania:** Jeśli projekt odwołuje się do innych projektów, można dodać projekty, `-IncludeReferencedProjects` do których istnieje odwołanie, jako część pakietu lub jako zależności, za pomocą opcji:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Ten proces dołączania jest cykliczny, więc jeśli `MyProject.csproj` odwołania do projektów B i C, a te projekty odnoszą się do D, E i F, a następnie pliki z B, C, D, E i F są zawarte w pakiecie.

    Jeśli projekt, do `.nuspec` którego istnieje odwołanie, zawiera własny plik, następnie NuGet dodaje, że odwołuje się do projektu jako zależność zamiast.  Należy spakować i opublikować ten projekt oddzielnie.

- **Konfiguracja kompilacji:** Domyślnie NuGet używa domyślnej konfiguracji kompilacji ustawionej w pliku projektu, zazwyczaj *debugowania*. Aby spakować pliki z innej konfiguracji kompilacji, takiej jak *Release*, użyj `-properties` opcji z konfiguracją:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symbole**: aby uwzględnić symbole, które umożliwiają konsumentom przechodzenie przez `-Symbols` kod pakietu w debugerze, użyj tej opcji:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Instalacja pakietu testowego

Przed opublikowaniem pakietu zazwyczaj chcesz przetestować proces instalowania pakietu w projekcie. Testy upewnij się, że wszystkie pliki koniecznie kończy się w ich odpowiednich miejscach w projekcie.

Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia, wykonując [normalne kroki instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

W przypadku automatycznych testów podstawowy proces jest następujący:

1. Skopiuj `.nupkg` plik do folderu lokalnego.
1. Dodaj folder do źródeł pakietu `nuget sources add -name <name> -source <path>` za pomocą polecenia (patrz [źródła nuget](../reference/cli-reference/cli-ref-sources.md)). Należy pamiętać, że to źródło lokalne należy ustawić tylko raz na danym komputerze.
1. Zainstaluj pakiet z tego `nuget install <packageID> -source <name>` `<name>` źródła, używając miejsca, w `nuget sources`którym jest to zgodne z nazwą źródła, jak podano . Określenie źródła zapewnia, że pakiet jest zainstalowany tylko z tego źródła.
1. Sprawdź system plików, aby sprawdzić, czy pliki są poprawnie zainstalowane.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w [polu Publikowanie pakietu.](../nuget-org/publish-a-package.md)

Można również rozszerzyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze, jak opisano w następujących tematach:

- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przekształcenia plików źródłowych i konfiguracyjnych](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje w wersji wstępnej](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów z zestawami współdziałań COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Na koniec istnieją dodatkowe typy pakietów, o których należy pamiętać:

- [Pakiety natywne](../guides/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
