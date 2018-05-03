---
title: Co to jest NuGet i jakie zadania wykonuje?
description: Obszerne jakie NuGet jest i jest
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/10/2018
ms.topic: overview
ms.openlocfilehash: 7237db8f3be3d9a1d46b9e6be41bff5c06593a20
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="an-introduction-to-nuget"></a>Wprowadzenie do NuGet

Podstawowe narzędzie dla dowolnej platformy nowoczesnych programowanie jest mechanizm, za pośrednictwem której deweloperzy można utworzyć, udostępniania oraz korzystać z kodu przydatne. Często taki kod jest połączone w "packages" zawierające skompilowanego kodu (w postaci bibliotek DLL) wraz z inną zawartość w projektach, które wykorzystać te pakiety.

Dla platformy .NET (w tym oprogramowanie .NET Core), jest obsługiwane przez firmę Microsoft mechanizm udostępnianie kodu **NuGet**, który definiuje sposób pakietów dla platformy .NET są tworzone, obsługiwane i używane i udostępnia narzędzia dla każdej z tych ról.

Po prostu umieść NuGet pakiet jest pojedynczy plik ZIP z `.nupkg` rozszerzenie zawiera skompilowanego kodu (dll), inne pliki związane z tym kodem i opisową manifestu, który zawiera informacje, takie jak numer wersji pakietu. Deweloperom kodu, aby udostępnić tworzenia pakietów i opublikuj je na hoście publicznych lub prywatnych. Konsumenci pakietu uzyskać te pakiety z odpowiednich hostów, dodaj je do projektów, a następnie wywołać funkcji pakietu w ich kod projektu. NuGet sama obsługuje wszystkie szczegóły pośrednich.

Ponieważ NuGet obsługuje hostów prywatnych obok hosta nuget.org publiczne, można użyć pakietów NuGet udostępnianie kodu, który jest na wyłączność dla organizacji lub grupie roboczej. Umożliwia także pakietów NuGet to wygodny sposób składników kodu do użycia w żadnej zawartości ale własnych projektów. Krótko mówiąc, pakiet NuGet kodu, możliwe do udostępnienia jednostki, ale nie jest wymagają ani oznaczać środków określonego udostępniania.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Przepływu pakietów między twórców, hostów i konsumentów

W roli jako publiczny hosta NuGet sam przechowuje ponad 100 000 pakietów unikatowy w centralnym repozytorium [nuget.org](https://www.nuget.org). Te pakiety są zatrudnieni przez miliony deweloperów.NET/.NET Core każdego dnia. NuGet można również do hostowania pakietów przez użytkowników w chmurze (takich jak w programie Visual Studio Team Services), w sieci prywatnej, lub nawet po prostu lokalnego systemu plików. W ten sposób te pakiety są dostępne tylko deweloperów, które mają dostęp do hosta, dzięki czemu mogą udostępnić pakietów do określonej grupy konsumentów. Opcje zostały wyjaśnione w [Hosting źródła NuGet](hosting-packages/overview.md). Za pomocą opcji konfiguracji można też kontrolować dokładnie hosty, które są dostępne dla dowolnego danego komputera, zapewniając, że pakiety są uzyskiwane z określonego źródła zamiast publicznego repozytorium, takich jak nuget.org.

Niezależnie od jego natury hosta służy jako punkt połączenia między pakietu *twórców* i pakietu *konsumentów*. Twórcy kompilacji przydatne pakietów NuGet i opublikuj je na hoście. Konsumenci następnie wyszukaj użyteczne i zgodne pakiety na hostach dostępnych, pobieranie i, w tym tych pakietów w swoich projektach. Po zainstalowaniu w projekcie, interfejsy API te pakiety są dostępne z resztą kodu projektu.

![Relacja między twórców pakietu, pakietu hostów i konsumentów pakietu](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Pakiet przeznaczony dla zgodności

Pakiet "zgodny" oznacza, że zawiera zestawy skompilowany dla co najmniej jeden element docelowy .NET framework, która jest zgodna z platformy docelowej projektu odbierającą. Deweloperzy mogą tworzyć pakiety, które są specyficzne dla jednej platformy, podobnie jak w przypadku kontrolek platformy uniwersalnej systemu Windows lub ich obsługi większej liczby obiektów docelowych. Aby zmaksymalizować pakietu w celu zapewnienia zgodności docelowej deweloperzy [.NET Standard](/dotnet/standard/net-standard), której można korzystać z usług .NET i .NET Core wszystkich projektów. Jest to najbardziej efektywny sposób zarówno twórcy, jak i konsumentów, pojedynczy pakiet (zazwyczaj zawierającej w jednym zestawie) działa w przypadku wszystkich projektów odbierającą.

Pakiet deweloperów, którzy wymagają interfejsów API poza .NET Standard z drugiej strony, Utwórz oddzielne zestawy dla platform inny element docelowy, potrzebnego do obsługi i obejmują wszystkie te zestawy w tym samym pakiecie (co jest nazywane "multi-targeting"). Podczas instalowania klienta taki pakiet NuGet wyodrębnia tylko zestawy, które są wymagane przez projekt. Pozwala to zmniejszyć wpływ pakietu w końcowym aplikacji i/lub zestawy utworzone przez tego projektu. Pakiet wielowersyjności kodu jest oczywiście trudniejsze dla twórcy do obsługi.

> [!Note]
> Przeznaczonych dla platformy .NET Standard zastępuje poprzednie podejście przy użyciu różnych celów (PCL) biblioteki klas przenośnych. W tej dokumentacji w związku z tym skupia się na tworzeniu pakietów dla platformy .NET Standard.

## <a name="nuget-tools"></a>Narzędzia NuGet

Oprócz obsługi pomocy technicznej, NuGet zawiera szereg narzędzi używanych przez zarówno twórcy, jak i konsumentów. Zobacz [narzędzia klienta instalowania NuGet](install-nuget-client-tools.md) dotyczące sposobu uzyskania określonych narzędzi.

| Narzędzie | Platformy | Scenariusze zastosowania | Opis |
| --- | --- | --- | --- |
| [nuget.exe interfejsu wiersza polecenia](tools/nuget-exe-cli-reference.md) | Wszystkie | Tworzenie, zużycia | Zawiera wszystkie funkcje NuGet, z niektórych poleceń stosowania specjalnie do pakietu twórcy, niektóre mające zastosowanie tylko do użytkowników, i inne osoby mające zastosowanie do obu. Na przykład pakiet Użyj twórców `nuget pack` polecenie, aby utworzyć pakiet z różnych zestawów i powiązane pliki, użyj konsumentów pakietu `nuget install` pakiety mają być dołączane w folderze projektu i wszyscy używa `nuget config` konfiguracji NuGet zmienne. Jako narzędzie niezależny od platformy NuGet CLI nie współdziała z projektów Visual Studio. |
| [DotNet interfejsu wiersza polecenia](tools/dotnet-Commands.md) | Wszystkie | Tworzenie, zużycia | Zapewnia możliwości bezpośrednio w ramach łańcucha narzędzi dla platformy .NET Core niektórych interfejsu wiersza polecenia NuGet. Podobnie jak w przypadku interfejsu wiersza polecenia NuGet dotnet CLI nie współdziała z projektów Visual Studio. |
| [Konsola menedżera pakietów](tools/package-manager-console.md) | Visual Studio w systemie Windows | Zużycie | Udostępnia [poleceń programu PowerShell](tools/Powershell-Reference.md) instalowania i zarządzania pakietami w projektach Visual Studio. |
| [Interfejs użytkownika menedżera pakietów](tools/package-manager-ui.md) | Visual Studio w systemie Windows | Zużycie | Zapewnia łatwy w użyciu interfejsu użytkownika dotyczące instalowania i zarządzania pakietami w projektach Visual Studio. |
| [Zarządzanie NuGet interfejsu użytkownika](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Zużycie | Podaj łatwy w użyciu interfejsu użytkownika dotyczące instalowania i zarządzania pakietami w programie Visual Studio dla komputerów Mac projektów. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Tworzenie, zużycia | Zapewnia możliwość tworzenia pakietów i przywrócenia pakietów używane w projekcie bezpośrednio przez łańcuch narzędzi programu MSBuild. |

Jak widać, korzystać z narzędzia NuGet zależą od znacznie Określa, czy podczas tworzenia, wykorzystywanie lub publikowania pakietów i platformy, na którym pracujesz. Twórcy pakietu zazwyczaj są to również użytkowników, zgodnie z ich bazując na funkcje, które istnieje w innych pakietach NuGet. I tych pakietów, mogą z kolei są zależne od nadal innych użytkowników.

Aby uzyskać więcej informacji, rozpoczynać [przepływ pracy tworzenia pakietu](create-packages/Overview-and-Workflow.md) i [przepływu pracy przez pakiet](consume-packages/Overview-and-Workflow.md) artykułów.

## <a name="managing-dependencies"></a>Zarządzanie zależności

Umożliwia łatwe tworzenie w pracy innych jest jednym z najbardziej zaawansowanych funkcji systemu zarządzania pakietu. W związku z tym większość NuGet jest zarządza tym drzewie zależności lub "wykresu" w imieniu projektu. Prostu, użytkownik musi dotyczyć jedynie samodzielnie z tych pakietów, których używasz bezpośrednio w projekcie. Jeśli żadnego z tych samych pakietów korzystać z innych pakietów (które mogą z kolei zużywają nadal innym) NuGet zapewnia obsługę tych zależności niższego poziomu.

Na poniższej ilustracji przedstawiono projekt, który jest zależny od pięciu pakietów, które z kolei są zależne od wielu innych.

![Wykres zależności NuGet przykład dla projektu platformy .NET](media/dependency-graph.png)

Należy zauważyć, że niektóre pakiety występuje wiele razy na wykresie zależności. Na przykład istnieją trzy różne konsumentów pakietu B, a każdy odbiorca może również określić inną wersję tego pakietu (tego nie pokazano). Jest to często dochodzi, szczególnie w przypadku pakietów powszechnie używane. NuGet na szczęście wykonuje całą pracę twarde dokładnie wersji pakietu B spełnia wszystkich użytkowników. NuGet następnie jest taka sama dla wszystkich innych pakietów, niezależnie od tego, jak głęboko na wykresie zależności.

Więcej szczegółów w sposób NuGet wykonywania tej usługi, zobacz [rozpoznawania zależności](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Odwołań śledzenia i przywracanie pakietów

Ponieważ projekty mogą łatwo przenosić między komputerami deweloperów, repozytoria kontroli źródła, serwery kompilacji i itp., jest bardzo niemożliwe do zachowania binarne zestawy pakietów NuGet bezpośrednio powiązany z projektem. W ten sposób czy każdej kopii niepotrzebnie przeglądarek projektu (i tym samym utratę miejsca w repozytoria kontroli źródła). To spowoduje również, że jego bardzo trudne do plików binarnych pakietu aktualizacji do nowszej wersji, ponieważ miałoby aktualizacje mają być stosowane na wszystkich kartach projektu.

NuGet zamiast niego przechowuje listę proste odwołanie pakietów, od których jest zależna projektu, w tym zależności najwyższego poziomu oraz niższych. Oznacza to, że podczas instalowania pakietu z niektórych hosta do projektu, NuGet rejestruje identyfikator pakietu i numer wersji na liście odwołania. (Odinstalowanie pakietu, usuwa ją z listy.) NuGet następnie udostępnia środki do przywrócenia wszystkich przywoływanych pakietów na żądanie, zgodnie z opisem na [Przywracanie pakietu](consume-packages/package-restore.md).

![Lista odwołań NuGet jest tworzony w instalacji pakietu i może służyć do przywrócenia pakietów w innym miejscu](media/nuget-restore.png)

Z tylko listę odwołań NuGet ponownie zainstalować&mdash;oznacza to, *przywrócić*&mdash;wszystkie pakiety z hostów publiczne i prywatne w dowolnym momencie nowsze. Podczas zatwierdzania projekt do kontroli źródła lub udostępnianie w inny sposób, zawierają tylko listę odwołań i Wyklucz wszystkie pliki binarne pakietu (zobacz [pakietów i kontroli źródła](consume-packages/packages-and-source-control.md).)

Komputer, który odbiera projektu, takich jak serwer kompilacji, uzyskując kopię projektu jako część systemu automatycznego wdrażania zapyta, po prostu NuGet, aby przywrócić zależności zawsze, gdy są potrzebne. Stworzyć systemy, takie jak Visual Studio Team Services zawierają opis etapów "Przywracanie NuGet", w tym celu dokładnego. Podobnie, gdy deweloperzy uzyskać kopię projektu (tak jak w przypadku klonowania repozytorium), ich wywołania polecenia, takich jak `nuget restore` (NuGet interfejsu wiersza polecenia), `dotnet restore` (dotnet interfejsu wiersza polecenia) lub `Install-Package` (Konsola Menedżera pakietów) można uzyskać wymaganych pakietów. Podczas kompilowania projektu programu Visual Studio, ze swojej strony automatycznie przywraca pakietów (pod warunkiem, że włączone automatyczne przywracanie zgodnie z opisem na [Przywracanie pakietu](consume-packages/package-restore.md)).

Wyraźnie widać następnie podstawową rolą NuGet, których dotyczy to deweloperom jest utrzymanie tej listy odwołania w imieniu projektu i umożliwianie wydajnie przywrócić (i zaktualizować) tych pakietów do którego istnieje odwołanie. Ta lista jest przechowywana w jednym z dwóch *pakietu zarządzania formaty*, jak są nazywane:

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)* pliku XML, który przechowuje to płaska lista wszystkie zależności w projekcie, wraz z zależnościami innych zainstalowanych pakietów. Pakiety został zainstalowany lub jest przywracane są przechowywane w `packages` folderu.

- [PackageReference](consume-packages/package-references-in-project-files.md) (lub "odwołań w projekcie plików pakietu") | *(NuGet 4.0 +)* przechowuje listę najwyższego poziomu zależności projektu bezpośrednio w pliku projektu, więc nie jest wymagane nie oddzielny plik. Skojarzony plik `obj/project.assets.json`, generowane dynamicznie do zarządzania ogólną wykresu zależności pakietów, które korzysta z projektem oraz wszystkie zależności niższego poziomu. PackageReference jest zawsze używana w projektach platformy .NET Core.

Zatrudnienia format pakietu administracyjnego w żadnym konkretnym projektem zależy od typu projektu i dostępna wersja NuGet (i/lub Visual Studio). Aby sprawdzić, jakie format jest używany, po prostu wyszukaj `packages.config` w katalogu głównym projektu po zainstalowaniu pakietu pierwszy. Jeśli nie masz tego pliku, poszukaj w pliku projektu bezpośrednio dla \<PackageReference\> elementu.

Jeżeli można wybrać, firma Microsoft zaleca używanie PackageReference. `packages.config` jest obsługiwana dla celów starszej wersji i nie jest już aktywne opracowywane.

> [!Tip]
> Różne `nuget.exe` polecenia interfejsu wiersza polecenia, takie jak `nuget install`, nie automatycznie dodawaj pakietu do listy odwołania. Lista jest aktualizowana podczas instalowania pakietu z programu Visual Studio Menedżera pakietów (interfejsu użytkownika lub konsolę) i z `dotnet.exe` interfejsu wiersza polecenia.

## <a name="what-else-does-nuget-do"></a>Co działa NuGet?

Do tej pory znasz następujące właściwości NuGet:

- NuGet udostępnia repozytorium nuget.org centralnej i pomocy technicznej dla prywatnych hostingu.
- NuGet oferuje deweloperom narzędzia potrzebne do tworzenia, publikowanie i korzystanie z pakietów.
- Przede wszystkim NuGet przechowuje listę odwołania pakietów używany w projekcie i możliwości przywracania oraz tych pakietów z listy aktualizacji.

Aby te procesy wydajną pracę, NuGet ma pewne optymalizacje wewnętrznych. Głównie NuGet zarządza pamięć podręczną pakietów i folder globalne pakietów do instalacji skrótów i ponownej instalacji. Pamięć podręczna pozwala uniknąć pobierania pakietu, który jest już zainstalowany na tym komputerze. Folder globalne pakietów umożliwia wielu projektów udostępnianie tego samego zainstalowanego pakietu, co zmniejsza ogólną miejsca w narzędziu NuGet na komputerze. Pamięci podręcznej i folderu packages globalne są także bardzo przydatne jest często Przywracanie większej liczby pakietów, jak na serwerze kompilacji. Aby uzyskać więcej informacji o tych mechanizmów, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](consume-packages/managing-the-global-packages-and-cache-folders.md).

W ramach pojedynczego projektu NuGet zarządza wykresu zależności ogólną ponownie zawiera wiele odwołań do różnych wersji tego samego pakietu rozwiązania. Jest bardzo często, że projekt ma zależność na co najmniej jeden pakiet, że mają się tym samym zależności. Niektóre z najbardziej przydatne pakiety narzędzia na nuget.org są zatrudnieni przez inne pakiety. Na wykresie zależności całego następnie, można łatwo masz dziesięć różne odwołania do różnych wersji tego samego pakietu. Aby uniknąć pobierania wiele wersji tego pakietu do samej aplikacji, NuGet sortuje się jednej wersji można używany przez wszystkich użytkowników. (Aby uzyskać więcej informacji, zobacz [rozpoznawania zależności](consume-packages/dependency-resolution.md).)

Ponadto NuGet obsługuje wszystkie wymagania dotyczące struktury pakietów (łącznie z [lokalizacja](create-packages/creating-localized-packages.md) i [symbole debugowania](create-packages/symbol-packages.md)) i jak są przywoływane (w tym [ zakresy wersji](reference/package-versioning.md#version-ranges-and-wildcards) i [wersje wstępne](create-packages/prerelease-packages.md).) NuGet także udostępnia różne interfejsy API do pracy z jego usług programowo i zapewnia obsługę dla deweloperów, którzy szablony projektów i rozszerzenia programu Visual Studio.

Poświęć chwilę, aby przeglądać spis treści niniejszej dokumentacji i wyświetlić wszystkie te funkcje reprezentowane istnieje, oraz informacje o wersji sprzed początku NuGet.

## <a name="comments-contributions-and-issues"></a>Komentarze, udziały i problemów

Na koniec znacznie prosimy komentarze i udziału w niniejszej dokumentacji&mdash;po prostu wybierz **opinii** i **Edytuj** poleceń w górnej części dowolnej strony lub odwiedź [dokumentów repozytorium](https://github.com/NuGet/docs.microsoft.com-nuget/) i [Lista problemów docs](https://github.com/NuGet/docs.microsoft.com-nuget/issues) w witrynie GitHub.

Prosimy udział NuGet się za pośrednictwem jego [różnych repozytoriów GitHub](https://github.com/NuGet/Home); Problemy z NuGet można znaleźć w [ https://github.com/NuGet/home/issues ](https://github.com/NuGet/home/issues).

Owocnej środowiska NuGet
