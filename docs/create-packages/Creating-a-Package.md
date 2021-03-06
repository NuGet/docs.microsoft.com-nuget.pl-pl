---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia nuget.exe
description: Szczegółowy przewodnik dotyczący projektowania i tworzenia pakietu NuGet, w tym plików i przechowywania wersji.
author: JonDouglas
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ebaa14325e477c7d864f5c5e88d99f467194e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774719"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>Tworzenie pakietu przy użyciu interfejsu wiersza polecenia nuget.exe

Niezależnie od tego, co Twój pakiet lub jaki kod zawiera, użyj jednego z narzędzi interfejsu wiersza polecenia `nuget.exe` lub `dotnet.exe` , aby spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów. Aby zainstalować narzędzia interfejsu wiersza polecenia NuGet, zobacz [Instalowanie narzędzi klienckich programu NuGet](../install-nuget-client-tools.md). Należy pamiętać, że program Visual Studio nie zawiera automatycznie narzędzia interfejsu wiersza polecenia.

- W przypadku projektów typu non-SDK, zwykle .NET Framework projektów, wykonaj kroki opisane w tym artykule, aby utworzyć pakiet. Aby uzyskać instrukcje krok po kroku dotyczące korzystania z programu Visual Studio i `nuget.exe` interfejsu wiersza polecenia, zobacz [Tworzenie i publikowanie pakietu .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).

- W przypadku projektów .NET Core i .NET Standard, które używają [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, zobacz [Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet](creating-a-package-dotnet-cli.md).

- W przypadku projektów migrowanych z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md)Użyj programu [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

Mówiąc technicznie, pakiet NuGet jest tylko plikiem ZIP, którego nazwa została zmieniona z `.nupkg` rozszerzeniem i którego zawartość pasuje do określonych konwencji. W tym temacie opisano szczegółowy proces tworzenia pakietu, który spełnia te konwencje.

Pakowanie rozpoczyna się od skompilowanego kodu (zestawów), symboli i/lub innych plików, które mają być dostarczane jako pakiet (zobacz [Omówienie i przepływ pracy](overview-and-workflow.md)). Ten proces jest niezależny od kompilacji lub w inny sposób wygenerowania plików, które przechodzą do pakietu, mimo że można rysować z informacji w pliku projektu, aby zachować synchronizację skompilowanych zestawów i pakietów.

> [!Important]
> Ten temat dotyczy projektów nie należących do zestawu SDK, zwykle projektów innych niż .NET Core i .NET Standard projektów przy użyciu programu Visual Studio 2017 i nowszych wersji oraz NuGet 4.0 +.

## <a name="decide-which-assemblies-to-package"></a>Wybór zestawów do spakowania

Większość pakietów ogólnego przeznaczenia zawiera jeden lub więcej zestawów, które mogą być używane przez innych deweloperów w swoich projektach.

- Ogólnie rzecz biorąc, najlepszym rozwiązaniem jest posiadanie jednego zestawu na pakiet NuGet, pod warunkiem, że każdy zestaw jest niezależnie przydatny. Na przykład jeśli masz, `Utilities.dll` który jest zależny od `Parser.dll` , i jest używany `Parser.dll` samodzielnie, Utwórz jeden pakiet dla każdej z nich. Dzięki temu deweloperzy mogą używać `Parser.dll` niezależnie od programu `Utilities.dll` .

- Jeśli biblioteka składa się z wielu zestawów, które nie są niezależnie przydatne, warto połączyć je w jeden pakiet. Korzystając z poprzedniego przykładu, jeśli `Parser.dll` zawiera kod, który jest używany tylko przez `Utilities.dll` , wówczas warto zachować `Parser.dll` w tym samym pakiecie.

- Podobnie, jeśli `Utilities.dll` jest to zależne od `Utilities.resources.dll` , gdzie ponownie nie jest on używany, należy umieścić oba te elementy w tym samym pakiecie.

Zasoby są w rzeczywistości szczególnym przypadkiem. Gdy pakiet jest instalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu do bibliotek DLL pakietu, *z wyjątkiem* tych, które są nazwane, `.resources.dll` ponieważ zakłada się, że są to zlokalizowane zespoły satelickie (zobacz [Tworzenie zlokalizowanych pakietów](creating-localized-packages.md)). Z tego powodu należy unikać używania `.resources.dll` dla plików, które w przeciwnym razie zawierają istotny kod pakietu.

Jeśli biblioteka zawiera zestawy międzyoperacyjności modelu COM, postępuj zgodnie z dodatkowymi wskazówkami w temacie [Tworzenie pakietów z zestawami międzyoperacyjnymi com](author-packages-with-com-interop-assemblies.md).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rola i struktura pliku. nuspec

Po poznaniu plików do spakowania następnym krokiem jest utworzenie manifestu pakietu w `.nuspec` pliku XML.

Manifest:

1. Opisuje zawartość pakietu i jest zawarta w pakiecie.
1. Dyski umożliwiają utworzenie pakietu i instruuje pakiet NuGet o sposobie instalacji pakietu w projekcie. Na przykład manifest identyfikuje inne zależności pakietu, aby pakiet NuGet mógł także zainstalować te zależności po zainstalowaniu pakietu głównego.
1. Zawiera właściwości wymagane i opcjonalne, zgodnie z poniższym opisem. Aby uzyskać dokładne informacje, w tym inne właściwości, które nie zostały wymienione w tym miejscu, zobacz [nuspec.](../reference/nuspec.md)

Wymagane właściwości:

- Identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet.
- Określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersje wstępne](prerelease-packages.md)
- Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)
- Informacje o autorze i właścicielu.
- Długi opis pakietu.

Wspólne właściwości opcjonalne:

- Informacje o wersji
- Informacje o prawach autorskich
- Krótki opis [interfejsu użytkownika Menedżera pakietów w programie Visual Studio](../consume-packages/install-use-packages-visual-studio.md)
- Identyfikator ustawień regionalnych
- Adres URL projektu
- Licencja jako wyrażenie lub plik ( `licenseUrl` jest przestarzały, Użyj zamiast niego [ `license` elementu metadanych nuspec](../reference/nuspec.md#license) )
- Plik ikony ( `iconUrl` jest przestarzały zamiast tego użyj [ `icon` elementu metadanych nuspec](../reference/nuspec.md#icon) )
- Listy zależności i odwołań
- Tagi pomocne w przeszukiwaniu galerii

Poniżej znajduje się typowy (ale fikcyjny) `.nuspec` plik z komentarzami opisującymi właściwości:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

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
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

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
        <file src="icon.png" target="" />
    </files>
</package>
```

Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [packages.config](../reference/packages-config.md) i [wersja pakietu](../concepts/package-versioning.md). Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu `include` `exclude` atrybutów i dla `dependency` elementu. Zobacz [. nuspec — zależności](../reference/nuspec.md#dependencies).

Ponieważ manifest jest zawarty w utworzonym przez niego pakiecie, można znaleźć dowolną liczbę dodatkowych przykładów, sprawdzając istniejące pakiety. Dobrym źródłem jest folder *Global-Packages* na komputerze, który jest zwracany przez następujące polecenie:

```cli
nuget locals -list global-packages
```

Przejdź do dowolnego folderu *package\version* , skopiuj `.nupkg` plik do `.zip` pliku, a następnie otwórz ten `.zip` plik i przejrzyj `.nuspec` go.

> [!Note]
> Podczas tworzenia `.nuspec` z projektu programu Visual Studio manifest zawiera tokeny, które są zastępowane informacjami z projektu podczas kompilowania pakietu. Zobacz [Tworzenie nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).

## <a name="create-the-nuspec-file"></a>Utwórz plik. nuspec

Tworzenie kompletnego manifestu zwykle zaczyna się od `.nuspec` pliku podstawowego wygenerowanego za pomocą jednej z następujących metod:

- [Katalog roboczy oparty na Konwencji](#from-a-convention-based-working-directory)
- [Biblioteka DLL zestawu](#from-an-assembly-dll)
- [Projekt programu Visual Studio](#from-a-visual-studio-project)    
- [Nowy plik z wartościami domyślnymi](#new-file-with-default-values)

Następnie możesz edytować plik ręcznie, tak aby opisuje dokładną zawartość, którą chcesz w pakiecie końcowym.

> [!Important]
> Wygenerowane `.nuspec` pliki zawierają symbole zastępcze, które należy zmodyfikować przed utworzeniem pakietu przy użyciu `nuget pack` polecenia. To polecenie kończy się niepowodzeniem, jeśli `.nuspec` zawiera symbole zastępcze.

### <a name="from-a-convention-based-working-directory"></a>Z katalogu roboczego opartego na Konwencji

Ponieważ pakiet NuGet jest tylko plikiem ZIP, którego nazwa została zmieniona przy użyciu `.nupkg` rozszerzenia, często najłatwiej jest utworzyć strukturę folderu w lokalnym systemie plików, a następnie utworzyć `.nuspec` plik bezpośrednio z tej struktury. `nuget pack`Polecenie automatycznie dodaje wszystkie pliki w tej strukturze folderów (z wyjątkiem folderów, które zaczynają się od `.` , co pozwala na przechowywanie prywatnych plików w tej samej strukturze).

Zaletą tego podejścia jest to, że nie trzeba określać w manifeście plików, które mają zostać uwzględnione w pakiecie (jak wyjaśniono w dalszej części tego tematu). Możesz po prostu utworzyć proces kompilacji o dokładnej strukturze folderów, która znajduje się w pakiecie, i można łatwo dołączać inne pliki, które mogą nie być częścią projektu:

- Zawartość i kod źródłowy, które powinny zostać dodane do projektu docelowego.
- Skrypty środowiska PowerShell
- Przekształca do istniejącej konfiguracji i plików kodu źródłowego w projekcie.

Konwencje folderów są następujące:

| Folder | Opis | Akcja po zainstalowaniu pakietu |
| --- | --- | --- |
| pierwiastek | Lokalizacja dla readme.txt | Program Visual Studio Wyświetla readme.txt plik w katalogu głównym pakietu po zainstalowaniu pakietu. |
| lib/{TFM} | Zestaw ( `.dll` ), dokumentacja ( `.xml` ) i pliki symboli ( `.pdb` ) dla danej monikera platformy docelowej (TFM) | Zestawy są dodawane jako odwołania do kompilowania, a także środowiska uruchomieniowego. `.xml` i `.pdb` skopiowane do folderów projektu. Zobacz [Obsługa wielu struktur docelowych](supporting-multiple-target-frameworks.md) na potrzeby tworzenia podfolderów specyficznych dla platformy docelowej. |
| ref/{TFM} | Zestaw () `.dll` i pliki symboli ( `.pdb` ) dla danej monikera platformy docelowej (TFM) | Zestawy są dodawane jako odwołania tylko dla czasu kompilacji; Nic nie zostanie skopiowane do folderu bin projektu. |
| Runtime | Zestaw specyficzny dla architektury ( `.dll` ), symbol ( `.pdb` ) i pliki zasobów natywnych ( `.pri` ) | Zestawy są dodawane jako odwołania tylko dla środowiska uruchomieniowego; inne pliki są kopiowane do folderów projektu. Zawsze powinien istnieć odpowiedni zestaw (TFM) `AnyCPU` określony w obszarze `/ref/{tfm}` folder, aby zapewnić odpowiedni zestaw czasu kompilacji. Zobacz [Obsługa wielu platform docelowych](supporting-multiple-target-frameworks.md). |
| zawartość | Dowolne pliki | Zawartość jest kopiowana do katalogu głównego projektu. Folder **zawartości** należy traktować jako katalog główny aplikacji docelowej, która ostatecznie zużywa pakiet. Aby pakiet mógł dodać obraz w folderze */images* aplikacji, umieść go w folderze *content/images* pakietu. |
| kompilacja | *(3. x +)* MSBuild `.targets` i `.props` pliki | Automatycznie wstawione do projektu. |
| buildMultiTargeting | *(4.0 +)* Program MSBuild `.targets` i `.props` pliki dla celów międzyplatformowych | Automatycznie wstawione do projektu. |
| buildTransitive | *(5.0 +)* Program MSBuild `.targets` i `.props` pliki, które są przesyłane przechodniie do dowolnego, zużywanego projektu. Zobacz stronę [funkcji](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) . | Automatycznie wstawione do projektu. |
| tools | Skrypty i programy PowerShell dostępne z konsoli Menedżera pakietów | `tools`Folder jest dodawany do `PATH` zmiennej środowiskowej tylko dla konsoli Menedżera pakietów (w *odróżnieniu* od `PATH` Ustawienia ustawionego dla programu MSBuild podczas kompilowania projektu). |

Ponieważ struktura folderów może zawierać dowolną liczbę zestawów dla dowolnej liczby platform docelowych, ta metoda jest konieczna podczas tworzenia pakietów, które obsługują wiele platform.

W każdym przypadku, gdy masz pożądaną strukturę folderów, uruchom następujące polecenie w tym folderze, aby utworzyć `.nuspec` plik:

```cli
nuget spec
```

Ponownie wygenerowany `.nuspec` nie zawiera żadnych jawnych odwołań do plików w strukturze folderów. Pakiet NuGet automatycznie uwzględnia wszystkie pliki podczas tworzenia pakietu. Mimo to należy edytować wartości zastępcze w innych częściach manifestu.

### <a name="from-an-assembly-dll"></a>Z biblioteki DLL zestawu

W prostym przypadku tworzenia pakietu z zestawu można wygenerować `.nuspec` plik z metadanych w zestawie przy użyciu następującego polecenia:

```cli
nuget spec <assembly-name>.dll
```

Użycie tego formularza zastępuje kilka symboli zastępczych w manifeście przy użyciu określonych wartości z zestawu. Na przykład `<id>` Właściwość jest ustawiana na nazwę zestawu i `<version>` jest ustawiona na wersję zestawu. Inne właściwości w manifeście nie mają jednak pasujących wartości w zestawie i w ten sposób nadal zawierają symbole zastępcze.

### <a name="from-a-visual-studio-project"></a>Z projektu programu Visual Studio

Tworzenie `.nuspec` `.csproj` pliku z lub `.vbproj` jest wygodne, ponieważ inne pakiety, które zostały zainstalowane w projekcie, są automatycznie przywoływane jako zależności. Po prostu Użyj następującego polecenia w tym samym folderze, w którym znajduje się plik projektu:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Utworzony `<project-name>.nuspec` plik zawiera *tokeny* , które są zastępowane w czasie pakowania z wartościami z projektu, w tym odwołaniami do innych pakietów, które zostały już zainstalowane.

Jeśli masz zależności pakietu do uwzględnienia w *nuspec*, zamiast tego użyj `nuget pack` i Pobierz plik *. nuspec* z wygenerowanego pliku *. nupkg* . Na przykład użyj poniższego polecenia.

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

Token jest rozdzielany `$` symbolami po obu stronach właściwości projektu. Na przykład `<id>` wartość w manifeście wygenerowaną w ten sposób zwykle pojawia się w następujący sposób:

```xml
<id>$id$</id>
```

Ten token jest zastępowany `AssemblyName` wartością z pliku projektu w czasie pakowania. Aby uzyskać dokładne mapowanie wartości projektu na `.nuspec` tokeny, zobacz [odwołanie do tokenów zastępczych](../reference/nuspec.md#replacement-tokens).

Tokeny zwalniają z konieczności aktualizowania najważniejszych wartości, takich jak numer wersji w `.nuspec` trakcie aktualizacji projektu. (Można zawsze zastąpić tokeny wartościami literału, jeśli jest to wymagane). 

Należy pamiętać, że podczas pracy z projektem programu Visual Studio jest dostępnych kilka dodatkowych opcji pakowania, zgodnie z opisem w artykule [uruchamianie pakietu NuGet w celu wygenerowania pliku. nupkg](#run-nuget-pack-to-generate-the-nupkg-file) w późniejszym czasie.

#### <a name="solution-level-packages"></a>Pakiety na poziomie rozwiązania

*Tylko pakiet NuGet 2. x. Niedostępne w programie NuGet 3.0 lub nowszym.*

Pakiet NuGet 2. x obsługuje pojęcie pakietu na poziomie rozwiązania, który instaluje narzędzia lub dodatkowe polecenia dla konsoli Menedżera pakietów (zawartość `tools` folderu), ale nie dodaje odwołań, zawartości ani dostosowań kompilacji do żadnych projektów w rozwiązaniu. Takie pakiety nie zawierają plików w jego bezpośredniej `lib` , `content` , ani `build` folderach i żadna z jej zależności nie ma plików w odpowiednich `lib` `content` folderach,, ani `build` .

Pakiet NuGet śledzi zainstalowane pakiety na poziomie rozwiązania w `packages.config` pliku w `.nuget` folderze, a nie w `packages.config` pliku projektu.

### <a name="new-file-with-default-values"></a>Nowy plik z wartościami domyślnymi

Następujące polecenie tworzy manifest domyślny z symbolami zastępczymi, co zapewnia rozpoczęcie od właściwej struktury plików:

```cli
nuget spec [<package-name>]
```

W przypadku pominięcia \<package-name\> plik zostanie utworzony `Package.nuspec` . Jeśli podano nazwę, taką jak `Contoso.Utility.UsefulStuff` , plik jest `Contoso.Utility.UsefulStuff.nuspec` .

Wyniki `.nuspec` zawierają symbole zastępcze dla wartości, takich jak `projectUrl` . Pamiętaj, aby edytować plik przed jego użyciem, aby utworzyć końcowy `.nupkg` plik.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Wybierz unikatowy identyfikator pakietu i ustaw numer wersji

Identyfikator pakietu ( `<id>` element) i numer wersji ( `<version>` element) to dwie najważniejsze wartości w manifeście, ponieważ jednoznacznie identyfikują dokładny kod zawarty w pakiecie.

**Najlepsze rozwiązania dotyczące identyfikatora pakietu:**

- **Unikatowość**: Identyfikator musi być unikatowy w obrębie NuGet.org lub dowolnej galerii, w której znajduje się pakiet. Przed podjęciem decyzji o identyfikatorze Przeszukaj stosowną galerię, aby sprawdzić, czy nazwa jest już używana. Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej części identyfikatora, na przykład `Contoso.` .
- **Nazwy podobne do nazw**: Postępuj zgodnie ze wzorcem podobnym do przestrzeni nazw w programie .NET przy użyciu notacji kropkowej zamiast łączników. Na przykład użyj `Contoso.Utility.UsefulStuff` zamiast `Contoso-Utility-UsefulStuff` lub `Contoso_Utility_UsefulStuff` . Konsumenci są również pomocne, gdy identyfikator pakietu jest zgodny z przestrzeniami nazw używanymi w kodzie.
- **Przykładowe pakiety**: w przypadku tworzenia pakietu przykładowego kodu, który pokazuje, jak używać innego pakietu, Dołącz `.Sample` jako sufiks do identyfikatora, jak w `Contoso.Utility.UsefulStuff.Sample` . (Przykładowy pakiet jest oczywiście zależny od innego pakietu). Podczas tworzenia przykładowego pakietu Użyj metody katalogu roboczego opartej na Konwencji opisanej wcześniej. W `content` folderze Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` w `\Samples\Contoso.Utility.UsefulStuff.Sample` .

**Najlepsze rozwiązania dotyczące wersji pakietu:**

- Ogólnie rzecz biorąc Ustaw wersję pakietu na zgodną z biblioteką, chociaż nie jest to wymagane absolutnie. Jest to prosta kwestia w przypadku ograniczenia pakietu do jednego zestawu, zgodnie z wcześniejszym opisem w [wyborze zestawów do spakowania](#decide-which-assemblies-to-package). Ogólnie, pamiętaj, że sam pakiet NuGet zajmuje się wersjami pakietu podczas rozpoznawania zależności, a nie wersji zestawu.
- W przypadku korzystania ze schematu wersji niestandardowej należy wziąć pod uwagę reguły obsługi wersji NuGet zgodnie z opisem w temacie [wersja pakietu](../concepts/package-versioning.md).

> Poniższa seria krótkich wpisów w blogu pomaga również zrozumieć przechowywanie wersji:
>
> - [Część 1: pobieranie biblioteki DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2: podstawowy algorytm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: ujednolicenie za pośrednictwem przekierowań powiązań](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>Dodaj plik Readme i inne pliki

Aby bezpośrednio określić pliki do dołączenia do pakietu, użyj `<files>` węzła w `.nuspec` pliku, który *następuje* po `<metadata>` tagu:

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
> W przypadku stosowania podejścia do katalogu roboczego opartego na konwencji można umieścić readme.txt w katalogu głównym pakietu i w innej zawartości w `content` folderze. `<file>`W manifeście nie są wymagane żadne elementy.

Po dołączeniu pliku o nazwie `readme.txt` w katalogu głównym pakietu program Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst bezpośrednio po zainstalowaniu pakietu bezpośrednio. (Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności). Na przykład poniżej przedstawiono sposób wyświetlania pliku Readme dla pakietu HtmlAgilityPack:

![Wyświetlanie pliku Readme dla pakietu NuGet podczas instalacji](media/Create_01-ShowReadme.png)

> [!Note]
> W przypadku dołączenia pustego `<files>` węzła do `.nuspec` pliku, pakiet NuGet nie zawiera żadnej innej zawartości pakietu niż zawartość `lib` folderu.

## <a name="include-msbuild-props-and-targets-in-a-package"></a>Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild

W niektórych przypadkach może zajść potrzeba dodania niestandardowych elementów docelowych kompilacji lub właściwości w projektach korzystających z pakietu, takich jak uruchamianie niestandardowego narzędzia lub procesu podczas kompilacji. W tym celu należy umieścić pliki w postaci `<package_id>.targets` lub `<package_id>.props` (takie jak `Contoso.Utility.UsefulStuff.targets` ) w `\build` folderze projektu.

Pliki w folderze głównym `\build` są uważane za odpowiednie dla wszystkich platform docelowych. Aby zapewnić pliki specyficzne dla struktury, należy najpierw umieścić je w odpowiednich podfolderach, takich jak następujące:

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

Następnie w `.nuspec` pliku Pamiętaj o odwoływaniu się do tych plików w `<files>` węźle:

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

W tym, że w pakiecie [NuGet 2,5 wprowadzono](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)atrybuty i elementy docelowe programu MSBuild, dlatego zaleca się dodanie `minClientVersion="2.5"` atrybutu do `metadata` elementu w celu wskazania minimalnej wersji klienta NuGet wymaganej do korzystania z pakietu.

Gdy NuGet instaluje pakiet z `\build` plikami, dodaje elementy programu MSBuild `<Import>` w pliku projektu wskazujące `.targets` `.props` pliki i. ( `.props` zostanie dodany u góry pliku projektu; `.targets` zostanie dodany u dołu). `<Import>` Dla każdej platformy docelowej dodawany jest oddzielny warunkowy element programu MSBuild.

Program MSBuild `.props` i `.targets` pliki dla celów docelowych dla wielu platform można umieścić w `\buildMultiTargeting` folderze. Podczas instalacji pakietu NuGet dodaje odpowiednie `<Import>` elementy do pliku projektu z warunkiem, że platforma docelowa nie jest ustawiona (Właściwość programu MSBuild `$(TargetFramework)` musi być pusta).

W przypadku programu NuGet 3. x elementy docelowe nie są dodawane do projektu, ale zamiast tego są udostępniane za pomocą `{projectName}.nuget.g.targets` i `{projectName}.nuget.g.props` .

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>Uruchom pakiet NuGet, aby wygenerować plik. nupkg

W przypadku korzystania z zestawu lub katalogu roboczego opartego na Konwencji Utwórz pakiet, uruchamiając `nuget pack` `.nuspec` plik, zastępując `<project-name>` go określoną nazwą pliku:

```cli
nuget pack <project-name>.nuspec
```

W przypadku korzystania z projektu programu Visual Studio Uruchom polecenie `nuget pack` z plikiem projektu, który automatycznie ładuje plik projektu `.nuspec` i zastępuje wszystkie tokeny w nim przy użyciu wartości w pliku projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Użycie pliku projektu bezpośrednio jest niezbędne do zastąpienia tokenu, ponieważ jest to źródło wartości tokenu. Zastępowanie tokenu nie odbywa `nuget pack` się w przypadku użycia z `.nuspec` plikiem.

We wszystkich przypadkach `nuget pack` wyklucza foldery, które zaczynają się od kropki, takie jak `.git` lub `.hg` .

Pakiet NuGet wskazuje, czy w pliku występują błędy `.nuspec` , które wymagają skorygowania, na przykład zapominanie o zmianie wartości symboli zastępczych w manifeście.

Po `nuget pack` pomyślnym wykonaniu tej procedury istnieje `.nupkg` plik, który można opublikować w odpowiedniej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).

> [!Tip]
> Przydatnym sposobem na badanie pakietu po jego utworzeniu jest otwarcie go w narzędziu [Eksplorator pakietów](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) . Dzięki temu można wyświetlić graficzny widok zawartości pakietu i jego manifestu. Możesz również zmienić nazwę wyniku `.nupkg` pliku w `.zip` pliku i zbadać jego zawartość bezpośrednio.

### <a name="additional-options"></a>Opcje dodatkowe

W celu wykluczania plików można użyć różnych przełączników wiersza polecenia `nuget pack` , zastąpić numer wersji w manifeście i zmienić folder wyjściowy między innymi. Pełną listę można znaleźć w [dokumentacji polecenia pakietu](../reference/cli-reference/cli-ref-pack.md).

Poniżej wymieniono kilka opcji, które są wspólne dla projektów programu Visual Studio:

- **Przywoływane projekty**: Jeśli projekt odwołuje się do innych projektów, można dodać przywoływane projekty jako część pakietu lub jako zależności, korzystając z `-IncludeReferencedProjects` opcji:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Ten proces dołączania jest cykliczny, więc jeśli `MyProject.csproj` odwołuje się do projektów b i c, a te projekty odwołują się do D, E i f, wówczas pliki z B, C, D, E i f są zawarte w pakiecie.

    Jeśli przywoływany projekt zawiera `.nuspec` własny plik, wówczas pakiet NuGet dodaje do projektu przywoływanego jako zależność.  Należy osobno spakować i opublikować ten projekt.

- **Konfiguracja kompilacji**: domyślnie NuGet używa domyślnego zestawu konfiguracji kompilacji w pliku projektu, zazwyczaj *Debuguj*. Aby spakować pliki z innej konfiguracji kompilacji, takiej jak *wersja*, użyj `-properties` opcji z konfiguracją:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symbole**: Aby dołączyć symbole umożliwiające użytkownikom przechodzenie przez kod pakietu w debugerze, użyj `-Symbols` opcji:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Instalacja pakietu testowego

Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie. Testy upewniają się, że wszystkie pliki, które się na bieżąco, kończą się w ich prawidłowym miejscu w projekcie.

Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

W przypadku zautomatyzowanych testów proces podstawowy jest następujący:

1. Skopiuj `.nupkg` plik do folderu lokalnego.
1. Dodaj folder do źródeł pakietów przy użyciu `nuget sources add -name <name> -source <path>` polecenia (zobacz [źródła NuGet](../reference/cli-reference/cli-ref-sources.md)). Należy pamiętać, że to źródło lokalne należy ustawić tylko raz na danym komputerze.
1. Zainstaluj pakiet z tego źródła, używając `nuget install <packageID> -source <name>` gdzie `<name>` jest zgodny z nazwą źródła określoną dla `nuget sources` . Określenie źródła gwarantuje, że pakiet jest instalowany wyłącznie z tego źródła.
1. Sprawdź system plików, aby sprawdzić, czy pliki są poprawnie zainstalowane.

## <a name="next-steps"></a>Następne kroki

Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).

Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:

- [Przechowywanie wersji pakietów](../concepts/package-versioning.md)
- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md)
- [Przekształcenia plików źródłowych i konfiguracji](../create-packages/source-and-config-file-transformations.md)
- [Lokalizacja](../create-packages/creating-localized-packages.md)
- [Wersje wstępne](../create-packages/prerelease-packages.md)
- [Ustawianie typu pakietu](../create-packages/set-package-type.md)
- [Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Na koniec należy pamiętać o dodatkowych typach pakietów:

- [Pakiety natywne](../guides/native-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md)
