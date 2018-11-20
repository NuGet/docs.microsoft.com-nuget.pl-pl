---
title: Jak utworzyć pakiet NuGet
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym punkty kluczowe decyzje, np. plików i przechowywania wersji.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: db02089bec3d2b8c001518fa0542375dc5418eb8
ms.sourcegitcommit: c825eb7e222d4a551431643f5b5617ae868ebe0a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/19/2018
ms.locfileid: "51944070"
---
# <a name="creating-nuget-packages"></a>Tworzenie pakietów NuGet

Niezależnie od tego, co robi pakietu lub co do kodu zawiera, możesz użyć `nuget.exe` spakować tej funkcji do składnika udostępnione i używane przez innych programistów. Aby zainstalować `nuget.exe`, zobacz [zainstalować interfejs wiersza polecenia NuGet](../install-nuget-client-tools.md#nugetexe-cli). Należy zauważyć, że program Visual Studio nie ma automatycznie `nuget.exe`.

Technicznie rzecz biorąc, pakiet NuGet jest po prostu plik ZIP, który jest zastępowana `.nupkg` rozszerzenie i których zawartość dopasowania do określonych konwencji. W tym temacie opisano szczegółowe proces tworzenia pakietu, który spełnia te Konwencji. Ukierunkowane instruktażu, można znaleźć [Szybki Start: tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).

Pakowanie zaczyna się od skompilowanego kodu (zestawów), symbole i/lub innych plików, które mają zostać dostarczone jako pakiet (zobacz [omówienie i przepływ pracy](overview-and-workflow.md)). Ten proces jest niezależna od kompilacji, albo w przeciwnym razie generowania plików, które są przekazywane do pakietu, mimo że można narysować z informacji w pliku projektu, aby zachować synchronizację skompilowanych zestawów i pakietów.

> [!Note]
> W tym temacie dotyczą projektów typów innych niż projektów .NET Core przy użyciu programu Visual Studio 2017 i NuGet 4.0 +. W tych projektach platformy .NET Core NuGet korzysta z informacji w pliku projektu bezpośrednio. Aby uzyskać więcej informacji, zobacz [Utwórz standardowy pakiety .NET przy użyciu programu Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) i [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Przy wyborze rozwiązania, które zestawy do pakietu

Najbardziej ogólnego przeznaczenia pakiety zawierają jeden lub więcej zestawów, umożliwiające innym deweloperom w ich własnych projektów.

- Ogólnie rzecz biorąc najlepiej jest mieć jeden zestaw dla pakietu NuGet, pod warunkiem, że każdy zestaw przydaje się niezależnie. Na przykład, jeśli masz `Utilities.dll` zależy `Parser.dll`, i `Parser.dll` przydaje się samodzielnie, a następnie utworzyć jeden pakiet, dla każdego. Dzięki temu deweloperzy mogą używać `Parser.dll` niezależnie od `Utilities.dll`.

- Jeśli Twoja biblioteka składa się z wielu zestawów, które nie są przydatne niezależnie, jest dobrym rozwiązaniem połączyć je w jednym pakiecie. W poprzednim przykładzie, jeśli `Parser.dll` zawiera kod, który jest używany wyłącznie przez `Utilities.dll`, a następnie jest dobrym rozwiązaniem zachować `Parser.dll` w tym samym pakiecie.

- Podobnie jeśli `Utilities.dll` zależy od `Utilities.resources.dll`, w którym ponownie nie jest on przydatny samodzielnie, następnie składane w tym samym pakiecie.

Zasoby są w rzeczywistości szczególny przypadek. Po zainstalowaniu do projektu pakiet NuGet automatycznie dodaje odwołania do zestawów do pakietu biblioteki dll, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie (patrz [ Tworzenie zlokalizowanych pakietów](creating-localized-packages.md)). Z tego powodu należy unikać `.resources.dll` dla plików, w przeciwnym razie zawierające kod essential pakietu.

Jeśli Twoja biblioteka zawiera zestawy międzyoperacyjne COM, wykonaj dodatkowe wskazówki zawarte w [tworzenia pakietów z zestawy międzyoperacyjne COM](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rola i struktura pliku .nuspec

Gdy wiesz, jakie pliki, które chcesz pakietu, następnym krokiem jest utworzenie manifestu pakietu w `.nuspec` pliku XML.

Manifest:

1. W tym artykule opisano zawartość pakietu i jest uwzględniony w pakiecie.
1. Tworzenia pakietu i powoduje, że NuGet na temat instalowania pakietu do projektu. Na przykład manifest identyfikuje inne zależności pakietu, taki sposób, że NuGet można także zainstalować te zależności, po zainstalowaniu pakietu głównego.
1. Zawiera właściwości wymagane i opcjonalne, zgodnie z poniższym opisem. Szczegółowymi informacjami na temat, w tym inne właściwości, które nie są wymienione w tym miejscu można znaleźć [odwołania .nuspec](../reference/nuspec.md).

Wymagane właściwości:

- Identyfikator pakietu musi być unikatowa w galerii, który jest hostem pakietu.
- Numer wersji określonej w formie *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]* gdzie *-sufiks* identyfikuje [wersje wstępne](prerelease-packages.md)
- Tytuł pakietu, ponieważ powinien pojawić się na hoście (np. nuget.org)
- Informacje dotyczące autora i właściciela.
- Długi opis pakietu.

Wspólne właściwości opcjonalne:

- Uwagi do wersji
- Informacje o prawach autorskich
- Krótki opis [interfejs użytkownika Menedżera pakietów w programie Visual Studio](../tools/package-manager-ui.md)
- Identyfikator ustawień regionalnych
- Adres URL projektu
- Licencja jako wyrażenie lub plik (`licenseUrl` jest wycofywany, użyj [ `license` elementu metadanych nuspec](../reference/nuspec.md#license))
- Adres URL ikony
- Listy zależności i odwołań
- Tagi, które pomagają w galerii wyszukiwania

Poniżej przedstawiono typowe (ale fikcyjne) `.nuspec` pliku z komentarzami opisujący właściwości:

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

Aby uzyskać szczegółowe informacje dotyczące zadeklarowania zależnościami i określania numerów wersji, zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md). Możliwe jest również do powierzchni zasoby z zależnościami bezpośrednio w pakiecie przy użyciu `include` i `exclude` atrybuty na `dependency` elementu. Zobacz [odwołanie .nuspec — zależności](../reference/nuspec.md#dependencies).

Ponieważ manifestu jest uwzględniony w pakiecie utworzonych na jej podstawie, dowolną liczbę dodatkowe przykłady można znaleźć, sprawdzając istniejących pakietów. Jest dobrym źródłem *globalnymi pakietami* folderu na komputerze, lokalizacji, który jest zwracany przez polecenie:

```cli
nuget locals -list global-packages
```

Przejdź do dowolnego *package\version* folderu, kopiowanie `.nupkg` plik `.zip` pliku, a następnie otwórz to `.zip` plików i zbadaj `.nuspec` znajdujący się w nim.

> [!Note]
> Podczas tworzenia `.nuspec` z projektu programu Visual Studio manifest zawiera tokenów, które są zastępowane informacjami z projektu podczas kompilowania pakietu. Zobacz [tworzenie .nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>Tworzenie pliku .nuspec

Tworzenie pełny manifeście zwykle zaczyna się od podstawowego `.nuspec` plik wygenerowany za pomocą jednego z następujących metod:

- [Przejdź do katalogu roboczego oparty na Konwencji](#from-a-convention-based-working-directory)
- [Zestaw bibliotek DLL](#from-an-assembly-dll)
- [Projekt programu Visual Studio](#from-a-visual-studio-project)    
- [Nowy plik z wartościami domyślnymi](#new-file-with-default-values)

Możesz następnie przeprowadź edycję pliku ręcznie, aby go w tym artykule opisano dokładnie zawartość, którą chcesz w pakiecie końcowym.

> [!Important]
> Wygenerowany `.nuspec` pliki zawierają symbole zastępcze, które muszą zostać zmodyfikowane, przed utworzeniem pakietu o `nuget pack` polecenia. Czy polecenie zakończy się niepowodzeniem, jeśli `.nuspec` zawiera wszystkie symbole zastępcze.

### <a name="from-a-convention-based-working-directory"></a>Z katalogu roboczego oparty na Konwencji

Ponieważ pakiet NuGet jest po prostu plik ZIP, który jest zastępowana `.nupkg` rozszerzenia, często łatwiej jest utworzyć strukturę folderów w lokalnym systemie plików, a następnie utwórz `.nuspec` pliku bezpośrednio z tej struktury. `nuget pack` Polecenie następnie automatycznie dodaje wszystkie pliki w tej strukturze folderu (z wyłączeniem wszystkie foldery, które zaczynają się od `.`, dzięki czemu możesz przechowywać pliki prywatne w tej samej struktury).

Zaletą tego podejścia jest to, nie należy określić w manifeście pliki, które mają zostać uwzględnione w pakiecie (opisany w dalszej części tego tematu). Po prostu może mieć proces kompilacji, tworzyć strukturę folderów dokładnie, która przechodzi do pakietu i innych plików, które mogą być częścią projektu w przeciwnym razie można łatwo dołączyć:

- Zawartość i kod źródłowy, który powinien dodane do projektu docelowego.
- Skrypty programu PowerShell (pakietów używane w pakiecie NuGet 2.x może obejmować także skrypty instalacji, co nie jest obsługiwane w pakiecie NuGet 3.x lub nowszy).
- Przekształcenia do istniejącej konfiguracji i plikami źródła kodu w projekcie.

Konwencje folderze są następujące:

| Folder | Opis | Akcja po instalacji pakietu |
| --- | --- | --- |
| (root) | Lokalizacja readme.txt | Visual Studio Wyświetla plik readme.txt w katalogu głównym pakietu, gdy pakiet jest zainstalowany. |
| lib/{tfm} | Zestaw (`.dll`), dokumentacji (`.xml`) i symbol (`.pdb`) plików dla danego Moniker Framework docelowych (TFM) | Zestawy są dodawane jako odwołania do kompilacji, jak również środowisko uruchomieniowe `.xml` i `.pdb` skopiowane do folderów projektu. Zobacz [Obsługa wielu platform docelowych](supporting-multiple-target-frameworks.md) tworzenia framework podfoldery specyficznych dla obiektu docelowego. |
| REF / {tfm} | Zestaw (`.dll`) i symbol (`.pdb`) plików dla danego Moniker Framework docelowych (TFM) | Zestawy są dodawane jako odwołania tylko w przypadku kompilowania; Nic nie zostanie więc skopiowane do folderu bin projektu. |
| środowiska uruchomieniowe | Architektury zestawu (`.dll`), symbol (`.pdb`), a zasób macierzysty (`.pri`) plików | Zestawy są dodawane jako odwołania tylko dla środowiska uruchomieniowego; inne pliki są kopiowane do folderów projektu. Zawsze powinien istnieć odpowiedni (TFM) `AnyCPU` określony zestaw, w obszarze `/ref/{tfm}` folder w celu zapewnienia odpowiedniego zestawu czasu kompilacji. Zobacz [Obsługa wielu platform docelowych](supporting-multiple-target-frameworks.md). |
| zawartość | Wybrane pliki | Zawartość jest kopiowana do katalogu głównego projektu. Traktować **zawartości** folder jako katalog główny aplikacji docelowej, który ostatecznie używa pakietu. Do pakietu, Dodaj obraz w aplikacji */obrazy* folder, umieść go w tym pakiecie *zawartości/obrazów* folderu. |
| kompilacja | Program MSBuild `.targets` i `.props` plików | Automatycznie wstawiany do pliku projektu lub `project.lock.json` (NuGet 3.x+). |
| narzędzia | Skrypty programu PowerShell i programów dostępne z konsoli Menedżera pakietów | `tools` Folder zostanie dodany do `PATH` zmiennej środowiskowej tylko za pomocą konsoli Menedżera pakietów (w szczególności *nie* do `PATH` według stawki ustalonej dla platformy MSBuild podczas kompilowania projektu). |

Twoja struktura folderów może zawierać dowolną liczbę zestawów dla dowolnej liczby platform docelowych, ta metoda jest niezbędna, podczas tworzenia pakietów, które obsługują wiele platform.

W każdym przypadku, gdy struktura żądany folder w miejscu, uruchom następujące polecenie w tym folderze, aby utworzyć `.nuspec` pliku:

```cli
nuget spec
```

Ponownie wygenerowany `.nuspec` nie zawiera żadnych jawnych odwołań do plików w strukturze folderu. Po utworzeniu pakietu NuGet automatycznie uwzględnia wszystkie pliki. Nadal należy jednak edytować wartości symboli zastępczych w innych częściach manifestu.

### <a name="from-an-assembly-dll"></a>Z zestawu biblioteki DLL

W prostym przypadku tworzenie pakietu z zestawu, można wygenerować `.nuspec` pliku z metadanych w zestawie, używając następującego polecenia:

```cli
nuget spec <assembly-name>.dll
```

Za pomocą tego formularza zastępuje kilka symboli zastępczych w manifeście z określonymi wartościami z zestawu. Na przykład `<id>` właściwość jest ustawiona na nazwę zestawu i `<version>` ustawiono wersję zestawu. Inne właściwości w manifeście, jednak nie ma pasującej wartości w zestawie i związku z tym nadal zawierają symbole zastępcze.

### <a name="from-a-visual-studio-project"></a>Z projektu programu Visual Studio

Tworzenie `.nuspec` z `.csproj` lub `.vbproj` pliku jest wygodne, ponieważ inne pakiety, które zostały zainstalowane do tych projektu są automatycznie określane jako zależności. W tym samym folderze co plik projektu, po prostu użyj następującego polecenia:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Wartość wynikowa `<project-name>.nuspec` plik zawiera *tokenów* , zostaną zastąpione podczas pakowania wartości z projektu, w tym odwołania do innych pakietów, które zostały już zainstalowane.

Token jest rozdzielone `$` symbole po obu stronach właściwości projektu. Na przykład `<id>` wartość manifestu wygenerowane w ten sposób zwykle pojawia się w następujący sposób:

```xml
<id>$id$</id>
```

Token ten zostanie zastąpiony `AssemblyName` wartości z pliku projektu w czasie pakowania. Dokładne mapowania projektu wartości `.nuspec` tokenów, zobacz [odwoływać się do zastąpienia tokenów](../reference/nuspec.md#replacement-tokens).

Tokeny zwalnia z konieczności aktualizowania niezwykle istotne wartości, takich jak numer wersji w `.nuspec` podczas aktualizowania projektu. (Możesz zawsze zastąpić tokeny przy użyciu wartości literału w razie potrzeby). 

Należy pamiętać, że kilka opcji tworzenia dodatkowych pakietów dostępne podczas pracy z projektu programu Visual Studio, zgodnie z opisem w [uruchomiony pakiet nuget, aby wygenerować plik .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) później.

#### <a name="solution-level-packages"></a>Pakiety na poziomie rozwiązania

*NuGet 2.x tylko. Nie jest dostępna w pakiecie NuGet 3.0 +.*

NuGet 2.x obsługuje pojęcie pakiet poziomie rozwiązania, który instaluje narzędzia lub dodatkowych poleceń konsoli Menedżera pakietów (zawartość `tools` folderu), ale dodaj odwołania do zawartości, ani nie lacji do żadnych projektów rozwiązanie. Takie pakiety zawierają żadnych plików w jego bezpośredniej `lib`, `content`, lub `build` foldery i żaden z jej zależnościami mieć plików w odpowiednich `lib`, `content`, lub `build` folderów.

Śledzi NuGet zainstalowanych pakietów poziomie rozwiązania w `packages.config` w pliku `.nuget` projektu, a nie folder `packages.config` pliku.

### <a name="new-file-with-default-values"></a>Nowy plik z wartościami domyślnymi

Następujące polecenie tworzy domyślny manifest z symbolami zastępczymi, który gwarantuje, że rozpoczynać struktury odpowiednich plików:

```cli
nuget spec [<package-name>]
```

Jeżeli pominięto \<nazwy pakietu\>, wynikowy plik jest `Package.nuspec`. Jeśli takie jak Podaj nazwę `Contoso.Utility.UsefulStuff`, plik jest `Contoso.Utility.UsefulStuff.nuspec`.

Wartość wynikowa `.nuspec` zawiera symbole zastępcze dla wartości, takich jak `projectUrl`. Pamiętaj edytować plik przed użyciem jej do utworzenia końcowe `.nupkg` pliku.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Wybieranie identyfikator unikatowy pakiet i ustawiania numeru wersji

Identyfikator pakietu (`<id>` elementu) i numeru wersji (`<version>` elementu) są dwoma najważniejszymi wartościami w manifeście, ponieważ jednoznacznie zidentyfikować dokładny kod, który jest zawarty w pakiecie.

**Najlepsze rozwiązania dotyczące identyfikator pakietu:**

- **Unikatowość**: identyfikator musi być unikatowa w repozytorium nuget.org, lub niezależnie od galerii obsługuje pakiet. Przed podjęciem decyzji o odpowiadającym, wyszukiwanie dotyczy galerii, sprawdź, czy nazwa jest już używana. Aby uniknąć konfliktów, dobrym deseń ma używać nazwy firmy jako pierwsza część identyfikatora, takich jak `Contoso.`.
- **Jak Namespace nazw**: podobne do przestrzeni nazw na platformie .NET, używając zapisu kropkowego zamiast łączniki wzorca. Na przykład użyć `Contoso.Utility.UsefulStuff` zamiast `Contoso-Utility-UsefulStuff` lub `Contoso_Utility_UsefulStuff`. Odbiorcy również okazać się pomocne podczas identyfikator pakietu jest zgodny przestrzenie nazw używane w kodzie.
- **Przykładowe pakiety**: w przypadku utworzenia pakiet przykładowy kod, który pokazuje, jak korzystać z innym pakietem, dołącz `.Sample` jako sufiks do identyfikatora, jak `Contoso.Utility.UsefulStuff.Sample`. (Przykładowego pakietu oczywiście musi zależność od innego pakietu.) Podczas tworzenia pakiet przykładowy, użyj opisanego wcześniej metody opartej na Konwencji katalogu roboczego. W `content` folderze Rozmieść przykładowego kodu w folderze o nazwie `\Samples\<identifier>` jak `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Najlepsze rozwiązania dla używanej wersji pakietu:**

- Ogólnie rzecz biorąc należy ustawić wersję pakietu pasuje do biblioteki, chociaż nie jest to bezwzględnie konieczne. To będzie polegać na ograniczenie pakietu w jednym zestawie, jak opisano wcześniej w [podejmowania decyzji, które zestawy do pakietu](#deciding-which-assemblies-to-package). Ogólnie należy pamiętać, że NuGet, sama zajmuje się wersje pakietów, podczas rozpoznawania zależności, a nie wersji zestawu.
- Przy użyciu schematu niestandardowej wersji, należy wziąć pod uwagę reguły kontroli wersji NuGet, jak wyjaśniono w [przechowywanie wersji pakietów](../reference/package-versioning.md).

> Następujące serię wpisów w blogu krótki są pomocne w zrozumieniu przechowywanie wersji:
>
> - [Część 1: Podjęcie na piekłem bibliotek DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2: Algorytmu](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: Ujednolicenie za pomocą przekierowania powiązań](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Ustawianie typu pakietu

Nuget 3.5 + pakiety mogą być oznaczone określonym *typ pakietu* do wskazania jego przeznaczenia. Domyślnie nie jest oznaczona za pomocą typu, w tym wszystkie pakiety utworzone w starszych wersjach programu NuGet, pakietów `Dependency` typu.

- `Dependency` pakiety typu Dodaj zasoby kompilacji lub czasu wykonywania bibliotek i aplikacji, a można zainstalować w dowolnym typem projektu (przy założeniu, że są one zgodne).

- `DotnetCliTool` rozszerzenia są pakiety typu [.NET CLI](/dotnet/articles/core/tools/index) i są wywoływane z poziomu wiersza polecenia. Takie pakiety można zainstalować tylko w projektach .NET Core i nie mają wpływu na operacje przywracania. Więcej informacji na temat tych rozszerzeń-projekt są dostępne w [rozszerzalność platformy .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentacji.

- Pakiety typu niestandardowego Użyj identyfikatora dowolnego typu, który jest zgodny z tych samych zasad format jako pakiet identyfikatorów. Dowolny typ inny niż `Dependency` i `DotnetCliTool`, jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.

Typy pakietów są ustawiane w `.nuspec` pliku. Jest najlepszym rozwiązaniem dla zapewnienia zgodności, aby *nie* jawnie ustawionej `Dependency` wpisz i zamiast polegać na NuGet, zakładając, że tego typu, gdy typ nie jest określony.

- `.nuspec`: Wskazuje typ pakietu we `packageTypes\packageType` węźle `<metadata>` elementu:

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

## <a name="adding-a-readme-and-other-files"></a>Dodawanie pliku readme i inne pliki

Aby bezpośrednio określić pliki do dołączenia do pakietu, należy użyć `<files>` w węźle `.nuspec` pliku, który *następuje* `<metadata>` tag:

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
> Korzystając z podejścia opartego na Konwencji katalog roboczy, możesz umieścić readme.txt w głównym pakietu i innych zawartości `content` folderu. Nie `<file>` elementy są niezbędne w manifeście.

Gdy uwzględnisz plik o nazwie `readme.txt` w katalogu głównym pakietu Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst od razu po zainstalowaniu pakietu bezpośrednio. (Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności). Na przykład poniżej przedstawiono sposób wyświetlania pliku readme pakietu HtmlAgilityPack:

![Wyświetlanie pliku readme podczas instalacji pakietu NuGet](media/Create_01-ShowReadme.png)

> [!Note]
> Jeśli dołączysz pustą `<files>` w węźle `.nuspec` pliku NuGet nie zawiera także do innej zawartości w pakiecie innych niż `lib` folderu.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>W tym cele i właściwości programu MSBuild w pakiecie

W niektórych przypadkach warto dodać obiekty docelowe kompilacji niestandardowej lub właściwości w projektach korzystających z pakietu, takie jak uruchomienie niestandardowego narzędzia lub procesu podczas kompilacji. Można to zrobić, umieszczanie plików w postaci `<package_id>.targets` lub `<package_id>.props` (takie jak `Contoso.Utility.UsefulStuff.targets`) w ramach `\build` folderu projektu.

Pliki w folderze głównym `\build` folderu są traktowane jako odpowiednie dla wszystkich ustalać platformy docelowe. Do udostępnienia plików określonej platformy, najpierw umieścić je w odpowiednich podfolderach, takie jak następujące:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Następnie w `.nuspec` pliku, pamiętaj odwoływać się do tych plików w `<files>` węzła:

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

W tym cele i właściwości programu MSBuild w pakiecie został [wprowadzone w programie NuGet w wersji 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), dlatego zalecane jest dodawanie `minClientVersion="2.5"` atrybutu `metadata` element, aby wskazać, minimalna wersja klienta NuGet, wymagane do Używanie pakietu.

Gdy NuGet instaluje pakiet o `\build` pliki, dodaje MSBuild `<Import>` elementy w pliku projektu, wskazując `.targets` i `.props` plików. (`.props` zostanie dodany w górnej części pliku projektu; `.targets` zostanie dodany w dolnej części.) Oddzielne MSBuild warunkowego `<Import>` element jest dodawany dla każdej platformy docelowej.

Program MSBuild `.props` i `.targets` pliki for cross-adresowanie można umieścić w `\buildCrossTargeting` folderu. Podczas instalacji pakietu NuGet dodaje odpowiednich `<Import>` elementy do pliku projektu z warunkiem, że platforma docelowa nie jest ustawiona (właściwości programu MSBuild `$(TargetFramework)` może być pusta).

Nuget 3.x, elementy docelowe nie są dodawane do projektu, ale zamiast tego udostępnionych za pośrednictwem `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>Tworzenie pakietów przy użyciu zestawów międzyoperacyjnych COM

Pakiety, które zawierają zestawy międzyoperacyjne COM musi zawierać odpowiednią [plik docelowy](#including-msbuild-props-and-targets-in-a-package) tak, aby poprawny `EmbedInteropTypes` metadane dodawane do projektów przy użyciu formatu PackageReference. Domyślnie `EmbedInteropTypes` metadanych ma zawsze wartość false dla wszystkich zestawów stosowania PackageReference więc plik elementów docelowych dodaje te metadane jawnie. Aby uniknąć konfliktów, nazwa docelowego powinna być unikatowa. w idealnym przypadku należy użyć zestawienia nazwę pakietu i zestaw jest osadzony, zastępując `{InteropAssemblyName}` w poniższym przykładzie przy użyciu tej wartości. (Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) np.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Należy pamiętać, że podczas korzystania `packages.config` zarządzania formatu, dodawanie odwołań do zestawów z pakietów powoduje, że NuGet i programu Visual Studio sprawdzić, czy są zestawy międzyoperacyjne COM i ustawić `EmbedInteropTypes` na wartość true w pliku projektu. W tym przypadku cele są zastąpione.

Ponadto domyślnie [zasoby kompilacji nie została przechodnio przepływu](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakiety utworzone zgodnie z opisem w tym miejscu pracy inaczej, gdy są one pobierane jako zależność przechodnich z odwołaniem projektu do projektu. Konsument pakietu można zezwolić na przepływ, modyfikując wartość domyślną PrivateAssets wykluczającą kompilacji.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>Z dodatkiem Service pack nuget, aby wygenerować plik .nupkg

Korzystając z zestawu lub katalog roboczy oparty na Konwencji, Utwórz pakiet, uruchamiając `nuget pack` za pomocą usługi `.nuspec` pliku, zastępując `<project-name>` za pomocą usługi określonej nazwy pliku:

```cli
nuget pack <project-name>.nuspec
```

Korzystając z projektu programu Visual Studio, uruchom `nuget pack` przy użyciu pliku projektu, który automatycznie ładuje projektu `.nuspec` plików i zastępuje wszystkie tokeny znajdujący się w nim przy użyciu wartości w pliku projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Bezpośrednio przy użyciu pliku projektu jest niezbędna do zastępowania tokenu, ponieważ projekt jest źródłem wartości tokenu. Zastępowania tokenu nie następuje, jeśli używasz `nuget pack` z `.nuspec` pliku.

We wszystkich przypadkach `nuget pack` wyklucza folderów rozpoczynających się od kropki, takich jak `.git` lub `.hg`.

NuGet wskazuje, czy istnieją błędy w `.nuspec` plików, które wymagają korygowanie, takie jak Zapominanie o zmieniać wartości symboli zastępczych w manifeście.

Gdy `nuget pack` zakończy się powodzeniem, masz `.nupkg` pliku, który można opublikować odpowiedni galerii, zgodnie z opisem w [publikowania pakietu](../create-packages/publish-a-package.md).

> [!Tip]
> Można zbadać pakietu po jej utworzeniu go otworzyć w [narzędziu Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) narzędzia. Umożliwia graficzne przedstawienie zawartości pakietu i jego manifestu. Można również zmienić nazwę wynikowy `.nupkg` plik `.zip` pliku i przejrzyj jego zawartość bezpośrednio.

### <a name="additional-options"></a>Dodatkowe opcje

Można użyć różnych przełączników wiersza polecenia przy użyciu `nuget pack` Aby wykluczyć pliki, zastąpić numer wersji w manifeście i zmienić folderu wyjściowego, m.in. Aby uzyskać pełną listę, zobacz [pakietu odniesienie do polecenia](../tools/cli-ref-pack.md).

Dostępne są następujące opcje: kilka są powszechne projektów programu Visual Studio:

- **Odwołanie do projektów**: Jeśli projekt odwołuje się do innych projektów, możesz dodać projektów występujących w odwołaniu jako część pakietu, lub zależności, za pomocą `-IncludeReferencedProjects` opcji:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Ten proces dołączania plików jest cykliczna, więc jeśli `MyProject.csproj` odwołań projektów B i C i projekty, odwołania D i E, F, a następnie pliki z B, C, D, E i f. znajdują się w pakiecie.

    Jeśli przywoływany projekt zawiera `.nuspec` plik własną, następnie NuGet dodaje przywoływanego projektu jako zależność zamiast tego.  Należy w pakietach i publikowanie projektu oddzielnie.

- **Konfiguracja kompilacji**: Domyślnie program NuGet używa domyślnej konfiguracji kompilacji, zwykle ustawić w pliku projektu *debugowania*. Umieszczenie plików z konfiguracji różnych kompilacji, takie jak *wersji*, użyj `-properties` opcji konfiguracji:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symbole**: aby uwzględnić symboli, które pozwala użytkownikom przejść przez kod pakietu w debugerze, należy użyć `-Symbols` opcji:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Testowanie instalacji pakietu aktualizacji

Przed opublikowaniem pakietu, zazwyczaj chcesz przetestować proces instalowania pakietu do projektu. Testy, upewnij się, że zawsze pliki wszystkie znajdą się w ich w odpowiednim miejscu w projekcie.

Testowanie instalacji ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu normalnych [kroki instalacji pakietu](../consume-packages/ways-to-install-a-package.md).

Potrzeby zautomatyzowanego testowania podstawowy proces jest następująca:

1. Kopiuj `.nupkg` plik do folderu lokalnego.
1. Dodaj folder ze źródłami pakietów przy użyciu `nuget sources add -name <name> -source <path>` polecenia (zobacz [źródła nuget](../tools/cli-ref-sources.md)). Należy pamiętać, że będą potrzebne tylko ustawić to źródło lokalne raz na dowolnym danym komputerze.
1. Zainstaluj pakiet z tego źródła za pomocą `nuget install <packageID> -source <name>` gdzie `<name>` jest zgodna z nazwą swojego źródła jako przydzielony do `nuget sources`. Określanie źródła gwarantuje, że pakiet jest zainstalowany z tego samego źródła.
1. Sprawdź system plików, aby sprawdzić, czy pliki są poprawnie zainstalowane.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` pliku, można opublikować ją w Galerii wybranym zgodnie z opisem na [publikowania pakietu](../create-packages/publish-a-package.md).

Możesz również chcieć rozszerzają możliwości pakietu lub w przeciwnym razie obsługuje inne scenariusze, zgodnie z opisem w następujących tematach:

- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przekształceń źródła i plików konfiguracji](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje wstępne](../create-packages/prerelease-packages.md)

Ponadto istnieją typów dodatkowych pakietów, których trzeba pamiętać:

- [Pakiety natywne](../create-packages/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
