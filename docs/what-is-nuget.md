---
title: Co to jest NuGet i czego?
description: Obszerne jakie NuGet jest i wykonuje
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: 087bb043ba4b388b9de6d94cd838915a2e7247f4
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426132"
---
# <a name="an-introduction-to-nuget"></a>Wprowadzenie do narzędzia NuGet

Niezbędne narzędzia dla dowolnej platformy nowoczesne tworzenie oprogramowania to mechanizm, za pomocą których deweloperzy mogą utworzyć, współdzielenie i używanie przydatne kodu. Często takiego kodu jest zawarte w pakiecie do "packages", które zawierają skompilowany kod (jako biblioteki dll) wraz z inną zawartością potrzebne w projektach, korzystających z tych pakietów.

Dla platformy .NET (w tym .NET Core), jest mechanizm obsługiwane przez firmę Microsoft do udostępniania kodu **NuGet**, który definiuje sposób tworzenia pakietów dla platformy .NET, hostowanych i wykorzystane, i [zapewnia narzędzia](install-nuget-client-tools.md) dla każdego z te role.

Najprościej mówiąc, NuGet pakiet jest pojedynczym pliku ZIP z `.nupkg` rozszerzenia, która zawiera skompilowanego kodu (dll), inne pliki związane z tym kodem i opisowe manifestu, który zawiera informacje, takie jak numer wersji pakietu. Deweloperom kodu do udostępniania tworzenie pakietów i opublikuj je na hoście publicznych lub prywatnych. Konsumentów pakietu uzyskać te pakiety z odpowiednie hosty, dodaj je do swoich projektów i wywoływać funkcje pakietu w ich kodzie projektu. NuGet, sama obsługuje wszystkie szczegóły pośrednich.

Ponieważ NuGet obsługuje hostów prywatnych wraz z hosta publicznego repozytorium nuget.org, można użyć pakiety NuGet umożliwiające udostępnianie kodu, która jest dostępna wyłącznie dla organizacji lub grupie roboczej. Można również użyć pakietów NuGet to wygodny sposób, aby uwzględnić kod do użycia w nothing, ale własnych projektów. W skrócie pakietu NuGet jest możliwa do udostępniania kodu, jednostki, ale nie wymagają ani nie oznaczają wykrywają określonego udostępniania.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Przepływu pakietów między dla twórców, hosty i klientów

W swojej roli jako publiczny hosta, NuGet, sam przechowuje centralne repozytorium ponad 100 000 pakietów unikatowy w [nuget.org](https://www.nuget.org). Te pakiety są zatrudnieni przez miliony deweloperów.NET/.NET Core każdego dnia. NuGet można również do hostowania pakietów przez użytkowników w chmurze (takie jak na DevOps platformy Azure), w sieci prywatnej lub nawet po prostu lokalnego systemu plików. Dzięki temu te pakiety są dostępne dla tych deweloperów, które mają dostęp do hosta, co daje możliwość udostępnienia pakietów do określonej grupy odbiorców. Opcje zostały wyjaśnione na [hostingu źródła NuGet](hosting-packages/overview.md). Za pomocą opcji konfiguracji można także kontrolować, dokładnie hosta, którego może zostać oceniony przez dowolnego danego komputera, zapewniając, że pakiety są uzyskiwane z konkretnych źródeł, a nie z publicznego repozytorium, np. nuget.org.

Niezależnie od ich charakter hosta służy jako punkt połączenia między pakietu *twórców* i pakietu *konsumentów*. Twórcy tworzenie przydatne pakietów NuGet i opublikuj je na hoście. Konsumenci Wyszukaj pakiety przydatne i są zgodne na hostach dostępny, pobieranie oraz w swoich projektach, takich jak te pakiety. Po zainstalowaniu w projekcie, interfejsy API te pakiety są dostępne w pozostałej części kodu projektu.

![Relacja między pakietu dla twórców, hosty pakietu oraz klientów pakietu](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Pakiet przeznaczony dla zgodności

Pakiet "zgodne" oznacza, że zawiera zestawy stworzona z myślą o co najmniej jeden element docelowy .NET framework, która jest zgodna z platforma docelowa projektu odbierająca komunikaty. Deweloperzy mogą tworzyć pakiety, które są specyficzne dla jednej struktury, podobnie jak w przypadku kontrolek platformy UWP lub obsługują szerszego zakresu elementów docelowych. Aby zapewnić maksymalną zgodność pakietu, deweloperzy docelowej [.NET Standard](/dotnet/standard/net-standard), które mogą wykorzystywać projektów wszystkich .NET i .NET Core. Jest to najbardziej efektywny sposób oznacza, że zarówno twórcy, jak i konsumentów, pojedynczy pakiet (zazwyczaj zawierający pojedynczy zestaw) działa we wszystkich projektach odbierająca komunikaty.

Deweloperów pakietu, którzy wymagają interfejsów API poza .NET Standard z drugiej strony, Utwórz oddzielne zestawy dla platform docelowych różnych, jaki mu pasuje, do obsługi i obejmuje wszystkie te zestawy w tym samym pakiecie (co jest nazywane "multi-targeting"). Podczas instalowania pakietu sieci konsumenta NuGet wyodrębnia tylko zestawy, które są wymagane przez projekt. Pozwoli to zmniejszyć zużycie pakietu w gotowych aplikacji i/lub zestawów generowane przez ten projekt. Pakiet z wielowersyjnością kodu – jest także trudniejsze dla twórcy zachować.

> [!Note]
> Przeznaczonych dla platformy .NET Standard zastępuje poprzedniego podejście przy użyciu różnych celów (PCL) biblioteka klas przenośnych. Ta dokumentacja w związku z tym koncentruje się na tworzenie pakietów dla platformy .NET Standard.

## <a name="nuget-tools"></a>Narzędzia NuGet

Oprócz hostowania pomocy technicznej, NuGet zawiera szereg narzędzi używane zarówno przez twórców i użytkowników. Zobacz [NuGet Instalowanie narzędzi klienckich](install-nuget-client-tools.md) dotyczące sposobu uzyskania określonych narzędzi.

| Narzędzie | Platformy | Zastosowanie scenariuszy | Opis |
| --- | --- | --- | --- |
| [Wiersz polecenia DotNet](consume-packages/install-use-packages-dotnet-cli.md) | Wszystkie | Tworzenie i użycia | Narzędzie interfejsu wiersza polecenia dla biblioteki .NET Core i .NET Standard, a dla zestawu SDK stylu projektów środowiska .NET Framework (zobacz [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions)). Udostępnia pewne interfejs wiersza polecenia NuGet możliwości bezpośrednio w ramach łańcucha narzędzi .NET Core. Podobnie jak w przypadku interfejsu wiersza polecenia NuGet, wiersz polecenia dotnet nie wchodzi w interakcję z projektów programu Visual Studio. |
| [Interfejs wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md) | Wszystkie | Tworzenie i użycia | Narzędzie interfejsu wiersza polecenia do bibliotek .NET Framework i projektów innych stylu zestawu SDK, przeznaczonych dla biblioteki .NET Standard. Zawiera wszystkie funkcje NuGet, z niektórymi poleceniami zastosowanie konkretnie do pakietu dla twórców, niektóre mające zastosowanie tylko do konsumentów, i inne osoby mające zastosowanie do obu. Na przykład pakiet użycia dla twórców `nuget pack` polecenie, aby utworzyć pakiet z różnych zestawów i powiązane pliki, użyj konsumentów pakietu `nuget install` do uwzględnienia pakiety w folderze projektu i wszyscy używa `nuget config` konfiguracji NuGet zmienne. Jako narzędzie niezależne od platformy interfejs wiersza polecenia NuGet nie wchodzi w interakcję z projektów programu Visual Studio. |
| [Konsola menedżera pakietów](tools/package-manager-console.md) | Visual Studio Windows | Zużycie | Udostępnia [poleceń programu PowerShell](tools/Powershell-Reference.md) dotyczące instalowania i zarządzania pakietami w projektach programu Visual Studio. |
| [Interfejs użytkownika menedżera pakietów](tools/package-manager-ui.md) | Visual Studio Windows | Zużycie | Zapewnia łatwy w użyciu interfejsu użytkownika dotyczące instalowania i zarządzania pakietami w projektach programu Visual Studio. |
| [Zarządzanie NuGet interfejsu użytkownika](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Zużycie | Zapewniają łatwy w użyciu interfejsu użytkownika dotyczące instalowania i zarządzania pakietami w programie Visual Studio dla komputerów Mac projektów. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Tworzenie i użycia | Umożliwia tworzenie pakietów i przywrócenia pakietów, używany w projekcie bezpośrednio za pomocą łańcucha narzędzi programu MSBuild. |

Jak widać, narzędzia NuGet, z którymi pracujesz znacznie zależeć od tego, czy tworzysz, wykorzystywanie czy Publikowanie pakietów i platformy, na którym pracujesz. Pakiet dla twórców zazwyczaj są to również konsumentów, ponieważ są one oparte na funkcji, znajdującą się w innych pakietach NuGet. I pakiety, oczywiście, mogą z kolei zależeć od nadal.

Aby uzyskać więcej informacji, rozpoczynać się [przepływ pracy tworzenia pakietu](create-packages/Overview-and-Workflow.md) i [przepływ pracy zużyciu pakietu](consume-packages/Overview-and-Workflow.md) artykułów.

## <a name="managing-dependencies"></a>Zarządzanie zależnościami

Umożliwia łatwe tworzenie we współpracy z innymi jest jednym z najbardziej zaawansowanych funkcji systemu zarządzania pakietami. W związku z tym większość co to jest NuGet zarządza tym drzewo zależności lub "wykresu" w imieniu projektu. Był wyświetlany, możesz muszą dotyczyć jedynie samodzielnie za pomocą tych pakietów, których używasz bezpośrednio w projekcie. Jeśli wykorzystasz żadnych pakietów, tych samych innych pakietów, (które mogą z kolei korzystać nadal inne osoby), NuGet zajmuje się tych zależności niskiego poziomu.

Na poniższej ilustracji przedstawiono projekt, który jest zależny od pięciu pakietów, które z kolei zależeć od wielu innych.

![Przykładowy Graf zależności NuGet dla projektu platformy .NET](media/dependency-graph.png)

Należy zauważyć, że niektóre pakiety pojawić się wiele razy w wykresie zależności. Na przykład istnieją trzy różne osoby korzystające z pakietu B, a każdy odbiorca może również określić inną wersję tego pakietu (niewyświetlany). To jest wystąpieniem typowe, szczególnie w przypadku powszechnie używane pakiety. NuGet szczęście wykonuje trudną pracę w dokładnie którą wersję pakietu B spełnia wszyscy odbiorcy. NuGet następnie działa tak samo dla wszystkich innych pakietów, niezależnie od tego, jak głęboką wykres zależności.

Aby uzyskać szczegółowe informacje na temat jak NuGet wykonuje tę usługę, zobacz [rozpoznawania zależności](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Śledzenie odwołań i przywracanie pakietów

Ponieważ projekty można łatwo przenosić między komputerami deweloperów, poziomie repozytoriów kontroli źródła, serwery kompilacji i itp., wysoce niepraktycznie jest zapewnienie binarne zestawy pakietów NuGet bezpośrednio powiązany z projektem. Ten sposób będzie każdej kopii projektu niepotrzebnie przeglądarek (i tym samym utratę miejsca w poziomie repozytoriów kontroli źródła). On również zwiększyłoby bardzo trudne zaktualizować pliki binarne pakietu do nowszych wersji, ponieważ miałoby aktualizacje mają być stosowane we wszystkich kopii projektu.

NuGet przechowuje zamiast tego prostego listą odwołań do pakietów, od których zależy od projektu, łącznie z zależności najwyższego poziomu i niskiego poziomu. Oznacza to, że zawsze, gdy zainstalujesz pakiet z niektórych hosta do projektu NuGet rejestruje identyfikator pakietu i numeru wersji na liście odwołania. (Odinstalowywanie pakietu, oczywiście, usuwa ją z listy.) NuGet następnie udostępnia środki do przywrócenia wszystkich przywoływanych pakietów na żądanie, zgodnie z opisem na [Przywracanie pakietu](consume-packages/package-restore.md).

![Lista odwołań NuGet jest tworzona w instalacji pakietu aktualizacji i może służyć do przywrócenia pakietów w innym miejscu](media/nuget-restore.png)

Za pomocą tylko listę odwołań NuGet ponownie zainstalować&mdash;oznacza to, *przywrócić*&mdash;wszystkie te pakiety z publiczne i prywatne hostów dowolnym później. Jeśli zobowiążą się projekt do kontroli źródła lub udostępnianie w inny sposób, obejmują tylko listę odwołań i Wyklucz wszystkie pliki binarne pakietu (zobacz [pakiety i kontrola źródła](consume-packages/packages-and-source-control.md).)

Komputer, który otrzyma projektu, takich jak serwer kompilacji, uzyskując kopię projektu jako część systemu automatycznego wdrażania, po prostu pyta, czy rozszerzenie NuGet, aby przywrócić zależności zawsze wtedy, gdy zajdzie taka potrzeba. Tworzenie systemów, takich jak DevOps platformy Azure zawierają opis etapów "Przywracanie pakietów NuGet", w tym celu dokładne. Podobnie, gdy deweloperzy uzyskać kopię projektu (tak jak podczas klonowania repozytorium), wywołują polecenia podobnego `nuget restore` (interfejs wiersza polecenia NuGet), `dotnet restore` (wiersz polecenia dotnet), lub `Install-Package` (Konsola Menedżera pakietów), aby uzyskać niezbędne pakiety. Podczas kompilowania projektu ze swojej strony w programie Visual Studio automatycznie przywraca pakietów (pod warunkiem, że automatycznego przywracania jest włączona, zgodnie z opisem na [Przywracanie pakietu](consume-packages/package-restore.md)).

Wyraźnie widać następnie podstawową rolą NuGet, których dotyczy to deweloperom utrzymuje tę listę odwołań w imieniu projektu i umożliwianie efektywnie przywracania (i zaktualizować) te pakiety do którego istnieje odwołanie. Ta lista jest przechowywana w jednej z dwóch *pakietu zarządzania formaty*, zgodnie z ich wywołania:

- [PackageReference](consume-packages/package-references-in-project-files.md) (lub "odwołania do w plikach projektu pakietu") | *(NuGet 4.0 +)* utrzymuje listę zależności najwyższego poziomu projektu, bezpośrednio w pliku projektu, więc ten sam plik jest potrzebny. Skojarzony plik `obj/project.assets.json`, jest generowana dynamicznie zarządzać ogólną wykres zależności pakietów, do których projekt używa wraz ze wszystkimi zależnościami niskiego poziomu. PackageReference jest zawsze używana w projektach .NET Core.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)*  Pliku XML, który zawiera płaską listę wszystkich zależności w projekcie, w tym zależności innych zainstalowanych pakietów. Zainstalowane lub przywróconej pakiety są przechowywane w `packages` folderu.

Format pakietu zarządzania są stosowane w żadnym konkretnym projektem zależy od tego, typ projektu i dostępnej wersji NuGet (i/lub programu Visual Studio). Aby sprawdzić, jakiego formatu jest używany, po prostu wyszukaj `packages.config` w katalogu głównym projektu po zainstalowaniu pierwszego pakietu. Jeśli nie masz tego pliku, poszukaj w pliku projektu bezpośrednio do \<PackageReference\> elementu.

Jeśli masz do wyboru, zaleca się przy użyciu funkcji PackageReference. `packages.config` jest utrzymywana ze względu na starsze celów i nie podlega już aktywnie.

> [!Tip]
> Różne `nuget.exe` polecenia interfejsu wiersza polecenia, takie jak `nuget install`, nie należy automatycznie dodawać pakietu do listy odwołania. Lista jest aktualizowana podczas instalowania pakietu przy użyciu Menedżera pakietów Visual Studio (interfejsu użytkownika lub konsolę) i za pomocą `dotnet.exe` interfejsu wiersza polecenia.

## <a name="what-else-does-nuget-do"></a>Do czego służy else NuGet?

Do tej pory wyjaśniono następujące właściwości pakietu nuget:

- NuGet zapewnia repozytorium nuget.org centralnej, korzystając z pomocy technicznej do hostowania prywatnych.
- NuGet oferuje deweloperom narzędzia potrzebne do tworzenia, publikowania i używania pakietów.
- Co najważniejsze NuGet przechowuje listą odwołań do pakietów używanych w projekcie i zdolność do przywracania i aktualizacji tych pakietów z tej listy.

Aby wprowadzić te procesy pracować wydajnie, NuGet wykonuje niektóre optymalizacje w tle. W szczególności NuGet zarządza pamięcią podręczną pakietu oraz folder globalnymi pakietami instalacji skrótów i jego ponowna instalacja. Pamięć podręczna unika się pobieranie pakietu, która jest już zainstalowana na komputerze. Folder globalnymi pakietami umożliwia wielu projektów udostępnić ten sam zainstalowanego pakietu NuGet całkowitego rozmiaru na komputerze, zmniejszając w ten sposób. Pamięć podręczną i folder globalnymi pakietami są także bardzo pomocne jest często Przywracanie większej liczby pakietów, jak na serwerze kompilacji. Aby uzyskać szczegółowe informacje na temat tych mechanizmów, zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](consume-packages/managing-the-global-packages-and-cache-folders.md).

W ramach pojedynczego projektu NuGet zarządza wykres zależności ogólną ponownie obejmuje rozpoznawanie wiele odwołań do różnych wersji tego samego pakietu. Jest to dość często, że projekt ma zależność na co najmniej jeden pakiet, że same mają ten sam zależności. Niektóre z najbardziej przydatnych pakiety narzędzia w witrynie nuget.org zatrudnionych przez wiele innych pakietów. Na wykresie całego zależności, można łatwo musisz dziesięć różne odwołania do innej wersji tego samego pakietu. Aby uniknąć wprowadzenia wielu wersji tego pakietu w samej aplikacji, NuGet sortuje limit jednej wersji mogą być używane przez wszystkich użytkowników. (Aby uzyskać więcej informacji, zobacz [rozpoznawania zależności](consume-packages/dependency-resolution.md).)

Poza tym, NuGet zachowuje wszystkie specyfikacje, które są związane z strukturze pakietów (łącznie z [lokalizacji](create-packages/creating-localized-packages.md) i [symbole debugowania](create-packages/symbol-packages.md)) i jak są przywoływane (w tym [ zakresów wersji](reference/package-versioning.md#version-ranges-and-wildcards) i [wersje wstępne](create-packages/prerelease-packages.md).) NuGet także udostępnia różne interfejsy API pracować programowo z jego usług i zapewnia obsługę dla deweloperów, którzy szablony projektów i rozszerzenia programu Visual Studio.

Poświęć chwilę, aby przejrzeć spis treści dla tej dokumentacji, a zobaczysz wszystkie te funkcje reprezentowane, oraz informacje o wersji sięga do początku NuGet.

## <a name="comments-contributions-and-issues"></a>Komentarze, wkładu i zagadnienia

Na koniec znacznie zachęcamy komentarze i wkładu do niniejszej dokumentacji&mdash;po prostu wybierz opcję **opinii** i **Edytuj** poleceń u góry dowolnej strony lub odwiedź [docs repozytorium](https://github.com/NuGet/docs.microsoft.com-nuget/) i [Lista problemów docs](https://github.com/NuGet/docs.microsoft.com-nuget/issues) w witrynie GitHub.

Zachęcamy także wkład w NuGet, sama za pośrednictwem jego [różnych repozytoriów GitHub](https://github.com/NuGet/Home); Problemy z NuGet można znaleźć na [ https://github.com/NuGet/home/issues ](https://github.com/NuGet/home/issues).

Sprawi NuGet!
