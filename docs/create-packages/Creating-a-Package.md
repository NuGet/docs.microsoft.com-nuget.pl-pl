---
title: Jak utworzyć pakiet NuGet
description: Szczegółowy przewodnik dotyczący proces projektowania i tworzenia pakietu NuGet, w tym punkty decyzyjne klucza, takich jak pliki i przechowywania wersji.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 435db2d0cddcfd6b9db530cb384cf7facb9170dd
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818467"
---
# <a name="creating-nuget-packages"></a>Tworzenie pakietów NuGet

Niezależnie od tego, czego pakiet lub jego kodu zawiera, użyj `nuget.exe` do tej funkcji do składnika, który można udostępniać i używane przez dowolną liczbę inni deweloperzy pakietu. Aby zainstalować `nuget.exe`, zobacz [instalowania NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli). Należy pamiętać, że program Visual Studio nie ma automatycznie `nuget.exe`.

Jak to działa, pakiet NuGet jest tylko plik ZIP, który jest zastępowana `.nupkg` rozszerzenia i których zawartość odpowiada niektórych Konwencji. W tym temacie opisano szczegółowe proces tworzenia pakietu, który spełnia te Konwencji. Wskazówki ukierunkowanych, można znaleźć w temacie [Szybki Start: tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).

OPAKOWYWANIE rozpoczyna się od skompilowanego kodu (zestawy), symbole i/lub innych plików, które mają zostać dostarczone jako pakiet (zobacz [Przegląd i przepływ pracy](overview-and-workflow.md)). Ten proces jest niezależna od kompilowania lub w przeciwnym razie generowania plików, które są przekazywane do pakietu, mimo że można narysować z informacji w pliku projektu w celu synchronizowania skompilowane zestawy i pakietów.

> [!Note]
> W tym temacie dotyczą projektów typu innego niż projektów .NET Core za pomocą programu Visual Studio 2017 i NuGet 4.0 +. W tych projektach platformy .NET Core NuGet używa informacji w pliku projektu bezpośrednio. Aby uzyskać więcej informacji, zobacz [utworzyć .NET Standard pakiety z programu Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) i [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Przy wyborze zestawy, które do pakietu

Najbardziej ogólnego przeznaczenia pakietów zawiera jeden lub więcej zestawów, które innych deweloperzy mogą używać w ich własnych projektów.

- Ogólnie rzecz biorąc najlepiej jeden zestaw na pakietu NuGet, pod warunkiem, że każdy zestaw przydaje się niezależnie. Na przykład, jeśli masz `Utilities.dll` to zależy od `Parser.dll`, i `Parser.dll` przydaje się samodzielnie, a następnie utworzyć jeden pakiet dla każdego. Dzięki temu deweloperom używanie `Parser.dll` niezależnie od `Utilities.dll`.

- Jeśli biblioteki składa się z wielu zestawów, które nie są przydatne niezależnie, jest poprawnie połączyć je w jeden pakiet. W poprzednim przykładzie, jeśli `Parser.dll` zawiera kod, który jest używany tylko przez `Utilities.dll`, a następnie; można zachować `Parser.dll` w tym samym pakiecie.

- Podobnie jeśli `Utilities.dll` zależy od `Utilities.resources.dll`, gdzie ponownie nie jest on przydatny samodzielnie, następnie umieść zarówno w tym samym pakiecie.

Zasoby są w rzeczywistości w szczególnych przypadkach. Po zainstalowaniu pakietu w projekcie NuGet automatycznie dodaje odwołania do zestawów do biblioteki dll pakietu, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie (zobacz [ Tworzenie zlokalizowanych pakietów](creating-localized-packages.md)). Z tego powodu należy unikać `.resources.dll` plików, które w przeciwnym razie zawiera istotne pakiet kodu.

Jeśli biblioteka zawiera zestawy międzyoperacyjne COM, wykonaj dodatkowe wskazówki zawarte w [tworzenia pakietów z zestawy międzyoperacyjne COM](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rola i struktura pliku .nuspec

Po sprawdzeniu, jakie pliki do pakietu, następnym krokiem jest utworzenie manifestu pakietu w `.nuspec` pliku XML.

Plik manifestu:

1. Zawiera opis zawartości pakietu i jest uwzględniony w pakiecie.
1. Dyski tworzenia pakietu i program NuGet w sposób instalowania pakietu w projekcie. Na przykład manifest identyfikuje innych zależności pakietów tak, aby NuGet można także zainstalować te zależności, po zainstalowaniu pakietu głównego.
1. Zawiera właściwości zarówno wymaganych i opcjonalnych, zgodnie z poniższym opisem. Dokładne szczegółów, w tym inne właściwości nie są wymienione w tym miejscu można znaleźć [odwołania .nuspec](../reference/nuspec.md).

Wymagane właściwości:

- Identyfikator pakietu musi być unikatowa w galerii, który jest hostem pakietu.
- Numer wersji określonej w formie *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]* gdzie *-sufiks* identyfikuje [wersje wstępne](prerelease-packages.md)
- Tytuł pakietu jako powinien pojawia się na hoście (na przykład nuget.org)
- Informacje o autora i właściciela.
- Długi opis pakietu.

Wspólne właściwości opcjonalne:

- Uwagi do wersji
- Informacje o prawach autorskich
- Krótki opis [interfejsu użytkownika Menedżera pakietów w programie Visual Studio](../tools/package-manager-ui.md)
- Identyfikator ustawień regionalnych
- Strona główna i adres URL licencji
- Adres URL ikony
- Wyświetla zależności i odwołań
- Tagi, które pomagają w galerii wyszukiwania

Poniżej przedstawiono typowe (ale fikcyjne) `.nuspec` pliku z komentarzami opisujące właściwości:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
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

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

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

Szczegółowe informacje o deklarowanie zależności i określanie numerów wersji, zobacz [wersji pakietu](../reference/package-versioning.md). Możliwe jest również do powierzchni zasoby z zależnościami bezpośrednio w pakiecie przy użyciu `include` i `exclude` atrybutów na `dependency` elementu. Zobacz [.nuspec — odwołanie do zależności](../reference/nuspec.md#dependencies).

Ponieważ manifestu jest uwzględniony w pakiecie z niej utworzyć, dowolną liczbę dodatkowe przykłady można znaleźć, sprawdzając istniejące pakiety. Jest dobrym źródłem *globalne pakiety* folderu na komputerze, lokalizację, jest zwracany za pomocą następującego polecenia:

```cli
nuget locals -list global-packages
```

Przejdź do dowolnego *package\version* folder, kopia `.nupkg` pliku na `.zip` pliku, a następnie otwórz to `.zip` pliku i sprawdź, czy `.nuspec` znajdujące się w nim.

> [!Note]
> Podczas tworzenia `.nuspec` z projektu programu Visual Studio manifestu zawiera tokenów, które są zastępowane informacji z projektu, podczas tworzenia pakietu. Zobacz [tworzenie .nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>Tworzenie pliku .nuspec

Tworzenie manifestu pełną zwykle zaczyna się od podstawowego `.nuspec` plik wygenerowany za pomocą jednego z następujących metod:

- [Katalog roboczy opartych na konwencjach](#from-a-convention-based-working-directory)
- [Zestaw biblioteki DLL](#from-an-assembly-dll)
- [Projektu programu Visual Studio](#from-a-visual-studio-project)    
- [Nowy plik z wartościami domyślnymi](#new-file-with-default-values)

Możesz następnie przeprowadź edycję pliku ręcznie tak aby dokładnie zawartość, którą chcesz w ostatnim pakiecie.

> [!Important]
> Wygenerowany `.nuspec` pliki zawierają symbole zastępcze, które muszą zostać zmodyfikowane przed utworzeniem pakietu z `nuget pack` polecenia. Aby polecenie kończy się niepowodzeniem, jeśli `.nuspec` zawiera wszystkie elementy zastępcze.

### <a name="from-a-convention-based-working-directory"></a>Z katalogu roboczego opartych na konwencjach

Ponieważ pakiet NuGet jest tylko plik ZIP, który jest zastępowana `.nupkg` rozszerzenia jego często najłatwiej Utwórz strukturę folderów w lokalnym systemie plików, następnie utwórz `.nuspec` pliku bezpośrednio z tej struktury. `nuget pack` Polecenia następnie automatycznie dodaje wszystkie pliki w tej struktury folderów (z wyłączeniem wszelkich folderów zaczynające się `.`, co pozwala przechowywać pliki prywatne w tej samej struktury).

Zaletą tej metody jest, że nie należy określić w manifeście pliki, które mają zostać uwzględnione w pakiecie (zgodnie z objaśnieniem w dalszej części tego tematu). Program może po prostu utworzyć strukturę folderów dokładne, który jest przesyłany w pakiecie procesu kompilacji i łatwo może zawierać inne pliki, które mogą być częścią projektu w przeciwnym razie:

- Zawartość i kod źródłowy, który powinien zostać dodane do projektu docelowego.
- Skrypty programu PowerShell (pakietów używane w NuGet 2.x można uwzględnić również skrypty instalacji, który nie jest obsługiwany w NuGet 3.x lub nowszy).
- Przekształcenia do istniejących plików konfiguracji i źródła kodu w projekcie.

Konwencje folderu są następujące:

| Folder | Opis | Akcja po instalacji |
| --- | --- | --- |
| (root) | Lokalizacja readme.txt | Visual Studio Wyświetla plik readme.txt w folderze głównym pakietu, gdy pakiet jest zainstalowany. |
| lib/{tfm} | Zestaw (`.dll`), dokumentacji (`.xml`) oraz symbol (`.pdb`) plików dla danego docelowej Framework Moniker (TFM) | Zestawy są dodawane jako odwołania; `.xml` i `.pdb` kopiowane do folderów projektu. Zobacz [obsługujący wiele platform docelowych](supporting-multiple-target-frameworks.md) tworzenia framework podfoldery specyficznych dla obiektu docelowego. |
| środowisk uruchomieniowych | Zestaw architektury (`.dll`), symbol (`.pdb`), a zasób macierzysty (`.pri`) plików | Zestawy są dodawane jako odwołania; inne pliki są kopiowane do folderów projektu. Zobacz [obsługujący wiele platform docelowych](supporting-multiple-target-frameworks.md). |
| zawartość | Wybrane pliki | Zawartość jest kopiowana do katalogu głównego projektu. Pomyśl o **zawartości** folder jako katalog główny aplikacji docelowej, który ostatecznie wykorzystuje pakiet. Aby dodać obraz w aplikacji pakietu */obrazy* folderu, umieść go w pakiecie *zawartości/obrazów* folderu. |
| kompilacja | MSBuild `.targets` i `.props` plików | Automatycznie dodaje do pliku projektu lub `project.lock.json` (NuGet 3.x+). |
| narzędzia | Skrypty programu PowerShell i programy dostępne w konsoli Menedżera pakietów | `tools` Folderu zostanie dodany do `PATH` zmiennej środowiskowej tylko za pomocą konsoli Menedżera pakietów (w szczególności *nie* do `PATH` zgodnie z ustaleniami dla MSBuild podczas kompilowania projektu). |

Struktury folderu może zawierać dowolną liczbę zestawów dla dowolnej liczby docelowych platform, ta metoda jest niezbędne, podczas tworzenia pakietów, które obsługuje wiele platform 

W każdym przypadku, gdy struktura odpowiedni folder w miejscu, uruchom następujące polecenie w tym folderze, aby utworzyć `.nuspec` pliku:

```cli
nuget spec
```

Ponownie wygenerowanego `.nuspec` nie zawiera żadnych jawnych odwołań do plików w folderze struktury. Po utworzeniu pakietu NuGet automatycznie uwzględnia wszystkie pliki. Nadal trzeba jednak edytować symbole zastępcze w innych częściach manifestu.

### <a name="from-an-assembly-dll"></a>Z zestawu biblioteki DLL

W przypadku prostego tworzenia pakietu z zestawu, można wygenerować `.nuspec` pliku z metadanych w zestawie przy użyciu następującego polecenia:

```cli
nuget spec <assembly-name>.dll
```

Za pomocą tego formularza zastępuje kilka symbole zastępcze w manifeście z określonymi wartościami z zestawu. Na przykład `<id>` właściwość jest ustawiona na nazwę zestawu, a `<version>` ustawiono wersji zestawu. Inne właściwości w manifeście, jednak nie pasują do wartości w zestawie i w związku z tym nadal zawierają symbole zastępcze.

### <a name="from-a-visual-studio-project"></a>Z projektu programu Visual Studio

Tworzenie `.nuspec` z `.csproj` lub `.vbproj` plik jest wygodne, ponieważ inne pakiety, które zostały zainstalowane w projekcie tych odwołuje się automatycznie jako zależności. W tym samym folderze co plik projektu, po prostu użyj następującego polecenia:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Powstałe w ten sposób `<project-name>.nuspec` plik zawiera *tokenów* który są zamieniane w czasie tworzenia pakietów z wartościami z projektu, w tym odwołania do innych pakietów, które zostały już zainstalowane.

Token jest rozdzielone `$` symbole po obu stronach właściwości projektu. Na przykład `<id>` wartości w manifeście, generowane w ten sposób zwykle wygląda następująco:

```xml
<id>$id$</id>
```

Token ten zostaje zastąpiony `AssemblyName` wartości z pliku projektu w czasie pakowania. Mapowanie dokładne wartości projektu do `.nuspec` tokenów, zobacz [odwołują się zastąpienia tokenów](../reference/nuspec.md#replacement-tokens).

Tokeny zwalnia z konieczności aktualizacji ważnych wartości, takich jak numer wersji w `.nuspec` jak aktualizacji projektu. (Możesz zawsze zastąpić tokenów wartości literałów w razie potrzeby). 

Należy pamiętać, że dostępnych jest kilka dodatkowych pakietów opcji dostępne podczas pracy z projektu programu Visual Studio, zgodnie z opisem w [uruchomiony pakiet nuget do wygenerowania pliku .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) później.

#### <a name="solution-level-packages"></a>Rozwiązanie na poziomie pakietów

*NuGet tylko 2.x. Nie jest dostępna w NuGet 3.0 +.*

NuGet 2.x obsługiwane podstawowe pojęcie w zakresie rozwiązania na poziomie pakietu, który instaluje narzędzia lub dodatkowych poleceń dla konsoli Menedżera pakietów (zawartość `tools` folderu), ale nie dodać odwołania do zawartości, lub utworzyć dostosowań do żadnych projektów rozwiązanie. Takie pakiety zawierają żadne pliki w jego bezpośrednio `lib`, `content`, lub `build` folderów, a żaden z jego zależności są pliki w odpowiednich `lib`, `content`, lub `build` folderów.

Śledzi NuGet zainstalowane pakiety poziomu rozwiązania w `packages.config` w pliku `.nuget` , zamiast folderu projektu `packages.config` pliku.

### <a name="new-file-with-default-values"></a>Nowy plik z wartościami domyślnymi

Poniższe polecenie tworzy manifest domyślny z symbole zastępcze, co zapewnia spełnienie rozpoczynać struktura prawidłowego pliku:

```cli
nuget spec [<package-name>]
```

W przypadku pominięcia \<nazwy pakietu\>, wynikowy plik jest `Package.nuspec`. Jeśli podasz nazwę taką jak `Contoso.Utility.UsefulStuff`, plik jest `Contoso.Utility.UsefulStuff.nuspec`.

Powstałe w ten sposób `.nuspec` zawiera symbole zastępcze dla wartości, takich jak `projectUrl`. Pamiętaj edytować plik przed użyciem jej do utworzenia ostatecznego `.nupkg` pliku.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Wybieranie identyfikator unikatowy pakiet i ustawianie numeru wersji

Identyfikator pakietu (`<id>` element) oraz numer wersji (`<version>` element) są dwie najważniejsze wartości w manifeście, ponieważ jednoznacznie zidentyfikować dokładną kod, który jest zawarty w pakiecie.

**Najlepsze rozwiązania dotyczące identyfikator pakietu:**

- **Unikatowość**: identyfikator musi być unikatowa w nuget.org lub niezależnie od galerii znajduje się pakiet. Przed podjęciem decyzji na podstawie identyfikatora, wyszukiwanie odpowiednich galerii, aby sprawdzić, czy nazwa jest już używany. Aby uniknąć konfliktów, dobrym wzorzec jest używać nazwy firmy jako pierwsza część identyfikatora, takich jak `Contoso.`.
- **Nazw Namespace przypominającej**: postępuj zgodnie z wzorcem podobne do przestrzeni nazw w programie .NET, używając zapisu kropkowego zamiast łączniki. Na przykład użyć `Contoso.Utility.UsefulStuff` zamiast `Contoso-Utility-UsefulStuff` lub `Contoso_Utility_UsefulStuff`. Konsumenci znajduje się także przydatne, gdy identyfikator pakietu jest zgodna z obszarów nazw używanych w kodzie.
- **Przykładowe pakiety**: Jeśli utworzyć pakiet przykładowy kod, który demonstruje sposób używania inny pakiet, dołącz `.Sample` sufiks identyfikatora, jak w `Contoso.Utility.UsefulStuff.Sample`. (Przykładowy pakiet oczywiście mają zależności na inny pakiet.) Podczas tworzenia pakietu próbki, metoda opartych na konwencjach pracy katalogu opisany wcześniej. W `content` folderu, Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` jako w `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Najlepsze rozwiązania dla wersji pakietu:**

- Ogólnie rzecz biorąc Ustaw wersję pakietu do dopasowania biblioteki, chociaż nie jest ścisłym wymogiem. Jest to proste sprawa ograniczenie długości pakietu w jednym zestawie zgodnie z wcześniejszym opisem w [podejmowania decyzji o którym zestawów do pakietu](#deciding-which-assemblies-to-package). Ogólnie należy pamiętać, że NuGet sam dotyczy wersji pakietu, podczas rozpoznawania zależności, a nie wersji zestawu.
- Podczas korzystania z niestandardowej wersji schematu, należy wziąć pod uwagę NuGet reguły kontroli wersji, zgodnie z objaśnieniem w [wersji pakietu](../reference/package-versioning.md).

> Następujący szereg krótki blogach są także zrozumieć, przechowywanie wersji:
>
> - [Część 1: Przyjęcia piekłem bibliotek DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2: Algorytm core](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: Ujednolicenie za pomocą przekierowania powiązań](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Ustawienie typu pakietu

Nuget 3.5 +, można oznaczyć pakiety z określonym *typu* wskazująca jego przeznaczenia. Domyślnie pakiety nie oznaczona atrybutem typu, w tym wszystkich pakietów utworzonych w starszych wersjach programu NuGet, `Dependency` typu.

- `Dependency` pakiety typu Dodaj kompilacji lub wykonywania zasoby do biblioteki i aplikacji, a można zainstalować w dowolnym typie projektu (przy założeniu, że są one zgodne).

- `DotnetCliTool` rozszerzenia są pakiety typu [.NET CLI](/dotnet/articles/core/tools/index) i są wywoływane z poziomu wiersza polecenia. Takie pakiety można zainstalować tylko w projektach platformy .NET Core i nie mają wpływu na operacje przywracania. Więcej informacji na temat tych rozszerzeń dla projektu są dostępne w [rozszerzenia architektury .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentacji.

- Typ niestandardowy pakietów, użyj identyfikatora dowolnego typu, który odpowiada te same zasady stosowania formatu w pakiecie identyfikatorów. Dowolny typ innych niż `Dependency` i `DotnetCliTool`, jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.

Typy pakietów są ustawiane w `.nuspec` pliku. Najlepiej dla zapewnienia zgodności do *nie* jawnie ustawione `Dependency` wpisz i zamiast tego polegać na NuGet zakładając, że ten typ, jeśli żaden typ nie jest określona.

- `.nuspec`: Określ typ pakietu w `packageTypes\packageType` węźle `<metadata>` elementu:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>Dodawanie pliku readme i innych plików

Aby określić bezpośrednio plików do uwzględnienia w pakiecie, należy użyć `<files>` w węźle `.nuspec` pliku, który *następuje* `<metadata>` tagu:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
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
> Korzystając z podejścia opartych na konwencjach katalog roboczy, możesz umieścić readme.txt w katalogu głównym pakietu i innych zawartości w `content` folderu. Nie `<file>` elementy są niezbędne w manifeście.

Jeśli dołączysz plik o nazwie `readme.txt` w katalogu głównym pakietu Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst od razu po zainstalowaniu pakietu bezpośrednio. (Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności). Na przykład poniżej przedstawiono sposób wyświetlania plik readme dla pakietu HtmlAgilityPack:

![Wyświetlanie plik readme dla pakietu NuGet podczas instalacji](media/Create_01-ShowReadme.png)

> [!Note]
> Jeśli dołączysz pustą `<files>` w węźle `.nuspec` pliku NuGet nie zawiera innej zawartości w pakiecie inne niż w `lib` folderu.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>W tym właściwości programu MSBuild i obiektów docelowych w pakiecie

W niektórych przypadkach można dodać elementów docelowych niestandardowej kompilacji lub właściwości w projektach używające pakietu, takie jak uruchomienie niestandardowego narzędzia lub procesu podczas kompilacji. Możesz to zrobić przez umieszczenie plików w postaci `<package_id>.targets` lub `<package_id>.props` (takich jak `Contoso.Utility.UsefulStuff.targets`) w ramach `\build` folderu projektu.

Pliki w folderze głównym `\build` folderu są traktowane jako odpowiednie dla wszystkich docelowych platform. Aby zapewnić pliki określonej struktury, najpierw umieścić te w odpowiednie podfoldery, takie jak następujące:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Następnie w `.nuspec` pliku, pamiętaj odwołać się do tych plików w `<files>` węzła:

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

W tym właściwości programu MSBuild i obiektów docelowych w pakiecie został [wprowadzone w systemie NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), dlatego zalecane jest dodawanie `minClientVersion="2.5"` atrybutu `metadata` element, aby wskazać minimalnej wersji klienta NuGet wymaganej do Korzystanie z pakietu.

Gdy NuGet instaluje pakiet o `\build` pliki, dodaje MSBuild `<Import>` elementów w pliku projektu wskazujący `.targets` i `.props` plików. (`.props` dodaje się u góry pliku projektu; `.targets` zostanie dodany na dole.) Oddzielne MSBuild warunkowego `<Import>` element jest dodawany do każdej platformy docelowej.

MSBuild `.props` i `.targets` plików dla framework między celem można umieścić w `\buildCrossTargeting` folderu. Podczas instalacji pakietu NuGet dodaje odpowiadającego `<Import>` elementy do pliku projektu z warunkiem, że platforma docelowa nie jest ustawiona (właściwość MSBuild `$(TargetFramework)` może być pusta).

Nuget 3.x, elementy docelowe nie zostaną dodane do projektu, ale zamiast tego stają się dostępne za pośrednictwem `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>Tworzenie pakietów z zestawy międzyoperacyjne COM

Pakiety, które zawierają zestawy międzyoperacyjne COM musi zawierać odpowiednie [plik elementów docelowych](#including-msbuild-props-and-targets-in-a-package) , aby poprawny `EmbedInteropTypes` metadanych jest dodawana do projektów przy użyciu formatu PackageReference. Domyślnie `EmbedInteropTypes` metadanych zawsze ma wartość false dla wszystkich zestawów stosowania PackageReference tak jawnie dodaje plik elementów docelowych tych metadanych. Aby uniknąć konfliktów, nazwa docelowego powinna być unikatowa; najlepiej, jeśli jest użycie kombinacji nazwę pakietu i zestaw są osadzone, zastępując `{InteropAssemblyName}` w przykładzie poniżej tej wartości. (Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) np.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Należy pamiętać, że przy użyciu `packages.config` format zarządzania Dodawanie odwołania do zestawów z pakietów powoduje NuGet i Visual Studio sprawdzić zestawy międzyoperacyjne COM i ustaw `EmbedInteropTypes` na wartość true w pliku projektu. W takim przypadku elementy docelowe są zastąpione.

Ponadto domyślnie [zasoby kompilacji nie przepływu przechodnie](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakiety utworzone zgodnie z opisem w tym miejscu pracy inaczej, gdy są one pobierane jako zależność przechodnie z odwołaniem projektu do projektu. Konsument pakietu zezwolić im na przepływ, zmieniając wartość domyślną PrivateAssets, aby nie był uwzględniany kompilacji.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>Z dodatkiem Service pack nuget, aby wygenerować plik .nupkg

Korzystając z zestawu lub katalog roboczy opartych na konwencjach, Utwórz pakiet, uruchamiając `nuget pack` z Twojej `.nuspec` pliku, zastępując `<project-name>` z Twojej określonej nazwy pliku:

```cli
nuget pack <project-name>.nuspec
```

Korzystając z projektu programu Visual Studio, uruchom `nuget pack` z pliku projektu, który automatycznie ładuje projektu `.nuspec` pliku i zastępuje wszystkie tokeny w nim przy użyciu wartości w pliku projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Bezpośrednio przy użyciu pliku projektu jest niezbędna dla zastępujący tokenu, ponieważ projekt jest źródłem wartości tokenów. Token zastępczy nie następuje, jeśli używasz `nuget pack` z `.nuspec` pliku.

We wszystkich przypadkach `nuget pack` wyklucza foldery, które zaczynać się kropką, takich jak `.git` lub `.hg`.

NuGet wskazuje, czy wystąpiły żadne błędy w `.nuspec` pliku, który należy korygowanie, takich jak włączaniu zmienić symbole zastępcze w manifeście.

Raz `nuget pack` zakończy się powodzeniem, masz `.nupkg` pliku, który można opublikować odpowiedni galerii zgodnie z opisem w [publikowania pakietu](../create-packages/publish-a-package.md).

> [!Tip]
> Można zbadać pakietu po jego utworzeniu otworzyć go w [Explorer pakietu](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) narzędzia. Umożliwia widoku graficznego elementów zawartości pakietu i jego manifestu. Można również zmienić powstałe w ten sposób `.nupkg` pliku `.zip` plików i przejrzyj jego zawartość bezpośrednio.

### <a name="additional-options"></a>Dodatkowe opcje

Można użyć różnych przełączników wiersza polecenia z `nuget pack` Aby wykluczyć pliki, Zastąp numer wersji w manifeście i zmień folder wyjściowy, między innymi funkcjami. Pełną listę można znaleźć [pakietu poleceń](../tools/cli-ref-pack.md).

Czy masz kilka typowych z projektów Visual Studio są następujące opcje:

- **Odwołanie do projektów**: Jeśli projekt odwołuje się do innych projektów, możesz dodać przywoływane projekty jako część pakietu lub zależności, za pomocą `-IncludeReferencedProjects` opcji:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Ten proces dołączania jest rekursywny, więc jeśli `MyProject.csproj` odwołań projektów B i C i tych projektów odwołania D i E, F, a następnie pliki z B, C, D, E i F znajdują się w pakiecie.

    Jeśli przywoływanego projektu zawiera `.nuspec` pliku własną, następnie NuGet dodaje przywoływanego projektu jako zależności zamiast tego.  Należy spakować i oddzielnie publikowanie tego projektu.

- **Konfiguracja kompilacji**: domyślnie NuGet używa domyślnej konfiguracji kompilacji ustawione w pliku projektu, zwykle *debugowania*. Można spakować pliki z różnych kompilacji konfiguracji, takich jak *wersji*, użyj `-properties` opcji konfiguracji:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symbole**: Aby dołączać symbole, umożliwiających konsumentów do wykonania kroków opisanych w debugerze kodu pakietu, należy użyć `-Symbols` opcji:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Testowanie instalacji pakietu aktualizacji

Przed opublikowaniem pakietu, zwykle można przetestować proces instalowania pakietu w projekcie. Testy, upewnij się, że zawsze pliki wszystkie kończyć w ich w odpowiednim miejscu w projekcie.

Testowanie instalacji ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu normalnych [kroki instalacji pakietu](../consume-packages/ways-to-install-a-package.md).

Do testów automatycznych podstawowy proces przebiega w następujący sposób:

1. Kopiuj `.nupkg` plik do folderu lokalnego.
1. Dodaj folder do źródła pakietu przy użyciu `nuget sources add -name <name> -source <path>` polecenia (zobacz [źródeł nuget](../tools/cli-ref-sources.md)). Należy pamiętać, że tylko należy ustawić tego lokalnego źródła raz na dowolnym komputerze z danym.
1. Zainstaluj pakiet z tego źródła za pomocą `nuget install <packageID> -source <name>` gdzie `<name>` jest zgodna z nazwą źródła przydzieloną `nuget sources`. Określanie źródła zapewnia zainstalowanie pakietu z tego samego źródła.
1. Sprawdź, czy system plików, aby sprawdzić, czy pliki są zainstalowane poprawnie.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` plików, można opublikować w Galerii wybranym zgodnie z opisem na [publikowania pakietu](../create-packages/publish-a-package.md).

Można również rozszerzyć możliwości pakietu lub w przeciwnym razie sprostania innym sytuacjom zgodnie z opisem w następujących tematach:

- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przekształcenia źródła i plików konfiguracji](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje wstępne](../create-packages/prerelease-packages.md)

Ponadto istnieją typy dodatkowego pakietu pod uwagę:

- [Pakiety natywne](../create-packages/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
