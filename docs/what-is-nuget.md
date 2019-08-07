---
title: Co to jest NuGet i co robi?
description: Kompleksowe wprowadzenie do pakietu NuGet i jego działania
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: f16cc6f66bc12727a4ec8eb5da4ff44a9eeb1764
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833331"
---
# <a name="an-introduction-to-nuget"></a>Wprowadzenie do narzędzia NuGet

Ważnym narzędziem dla każdej nowoczesnej platformy deweloperskiej jest mechanizm, za pomocą którego deweloperzy mogą tworzyć, udostępniać i korzystać z użytecznych kodów. Często taki kod jest powiązany z "pakietami" zawierającymi skompilowany kod (jako biblioteki dll) wraz z inną zawartością wymaganą w projektach, które zużywają te pakiety.

W przypadku platformy .NET (w tym platformy .NET Core) obsługiwany przez firmę Microsoft mechanizm udostępniania kodu to **NuGet**, który definiuje sposób tworzenia, obsługiwania i używania pakietów dla platformy .NET, a [także udostępnia narzędzia](install-nuget-client-tools.md) dla każdej z tych ról.

Po prostu pakiet NuGet jest pojedynczym plikiem ZIP z `.nupkg` rozszerzeniem zawierającym skompilowany kod (dll), innymi plikami związanymi z tym kodem i manifestem opisowym zawierającym informacje takie jak numer wersji pakietu. Deweloperzy z kodem do udostępniania tworzenia pakietów i publikowania ich na hoście publicznym lub prywatnym. Odbiorcy pakietu uzyskują te pakiety z odpowiednich hostów, dodają je do swoich projektów, a następnie wywołują funkcje pakietu w kodzie projektu. Samo narzędzie NuGet obsługuje wszystkie szczegóły pośrednie.

Ponieważ NuGet obsługuje hosty prywatne obok publicznego hosta nuget.org, można użyć pakietów NuGet do udostępniania kodu, który jest wyłącznie dla organizacji lub grupy roboczej. Pakiety NuGet można także wykorzystać jako wygodny sposób na wykorzystanie kodu do użycia w przypadku braku własnych projektów. W skrócie pakiet NuGet jest jednostką z możliwością udostępniania kodu, ale nie wymaga ani nie implikuje żadnego konkretnego sposobu udostępniania.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Przepływ pakietów między twórców, hostami i konsumentami

W roli jako hosta publicznego pakiet NuGet utrzymuje centralne repozytorium ponad 100 000 unikatowych pakietów w [NuGet.org](https://www.nuget.org). Te pakiety są wykorzystywane przez miliony deweloperów .NET/.NET Core codziennie. Pakiet NuGet umożliwia również hostowanie pakietów prywatnych w chmurze (na przykład na platformie Azure DevOps), w sieci prywatnej lub nawet w lokalnym systemie plików. Dzięki temu pakiety te są dostępne tylko dla tych deweloperów, którzy mają dostęp do hosta, co daje możliwość udostępnienia pakietów dla określonej grupy odbiorców. Te opcje są wyjaśnione w przypadku [hostowania własnych źródeł danych NuGet](hosting-packages/overview.md). Za pomocą opcji konfiguracji można również kontrolować, które hosty mogą być dostępne dla każdego komputera, zapewniając tym samym pewność, że pakiety są uzyskiwane z określonych źródeł, a nie do repozytorium publicznego, takiego jak nuget.org.

Niezależnie od ich charakteru Host służy jako punkt połączenia między *twórców* pakietu i użytkownikami pakietu. Twórcy tworzą przydatne pakiety NuGet i publikują je na hoście. Konsumenci szukają przydatnych i zgodnych pakietów na dostępnych hostach, pobierając i uwzględniając te pakiety w swoich projektach. Po zainstalowaniu w projekcie interfejsy API pakietów są dostępne dla pozostałej części kodu projektu.

![Relacja między twórcymi pakietów, hostami pakietów i użytkownikami pakietów](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Zgodność pakietu

Pakiet "zgodny" oznacza, że zawiera zestawy skompilowane dla co najmniej jednego docelowego programu .NET Framework, który jest zgodny z platformą docelową zużywanego projektu. Deweloperzy mogą tworzyć pakiety, które są specyficzne dla jednej struktury, podobnie jak w przypadku kontrolek platformy UWP, lub mogą obsługiwać szersze zakresy elementów docelowych. Aby zmaksymalizować zgodność pakietu, deweloperzy docelowi [.NET Standard](/dotnet/standard/net-standard), których mogą używać wszystkie projekty .NET i .NET Core. Jest to najbardziej wydajny sposób zarówno dla twórców, jak i konsumentów, jako pojedynczy pakiet (zazwyczaj zawierający pojedynczy zestaw) działa dla wszystkich zużywanych projektów.

Deweloperzy pakietów, którzy wymagają interfejsów API poza .NET Standard, z drugiej strony, tworzą oddzielne zestawy dla różnych platform docelowych, które chcą obsługiwać, i obejmują wszystkie te zestawy w tym samym pakiecie (nazywanym "wiele elementów docelowych"). Gdy konsument instaluje taki pakiet, NuGet wyodrębnia tylko te zestawy, które są niezbędne w projekcie. Pozwala to zminimalizować zasięg pakietu w końcowej aplikacji i/lub zestawach utworzonych przez ten projekt. Pakiet z wieloma względami jest oczywiście trudniejszy do utrzymania przez jego twórcę.

> [!Note]
> Ukierunkowanie .NET Standard zastępuje poprzednie podejście do korzystania z różnych elementów docelowych biblioteki klas przenośnych (PCL). Ta dokumentacja koncentruje się na tworzeniu pakietów dla .NET Standard.

## <a name="nuget-tools"></a>Narzędzia NuGet

Oprócz obsługi hostingu pakiet NuGet udostępnia również różne narzędzia używane przez twórców i użytkowników. Zobacz [Instalowanie narzędzi klienta NuGet](install-nuget-client-tools.md) na potrzeby uzyskiwania określonych narzędzi.

| Narzędzie | Platformy | Odpowiednie scenariusze | Opis |
| --- | --- | --- | --- |
| [Interfejs wiersza polecenia dotnet](consume-packages/install-use-packages-dotnet-cli.md) | Wszystkie | Tworzenie, użycie | Narzędzie interfejsu wiersza polecenia dla bibliotek .NET Core i .NET Standard oraz dla projektów w stylu zestawu SDK, które są przeznaczone dla .NET Framework (zobacz [atrybut zestawu SDK](/dotnet/core/tools/csproj#additions)). Zapewnia pewne możliwości interfejsu wiersza polecenia NuGet bezpośrednio w łańcuchu narzędzi programu .NET Core. Podobnie jak w `nuget.exe` przypadku interfejsu wiersza polecenia, interfejs wiersza polecenia dotnet nie współdziała z projektami programu Visual Studio. |
| [Interfejs wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md) | Wszystkie | Tworzenie, użycie | Narzędzie interfejsu wiersza polecenia dla bibliotek .NET Framework i projektów spoza zestawu SDK, które są przeznaczone dla .NET Standard bibliotek. Zapewnia wszystkie możliwości programu NuGet, z zastosowaniem określonych poleceń w odniesieniu do twórców pakietów, niektórych mających zastosowanie tylko do konsumentów i innych. Na przykład twórcy pakietów używają `nuget pack` polecenia, aby utworzyć pakiet z różnych zestawów i powiązanych plików, odbiorcy pakietów używają `nuget install` do dołączania pakietów do folderu projektu, a wszyscy używają `nuget config` do ustawiania konfiguracji NuGet modyfikacj. Jako narzędzie niezależny od platformy, interfejs wiersza polecenia NuGet nie współdziała z projektami programu Visual Studio. |
| [Konsola menedżera pakietów](consume-packages/install-use-packages-powershell.md) | Program Visual Studio w systemie Windows | Zużycie | Zawiera [polecenia programu PowerShell](reference/Powershell-Reference.md) służące do instalowania i zarządzania pakietami w projektach programu Visual Studio. |
| [Interfejs użytkownika menedżera pakietów](consume-packages/install-use-packages-visual-studio.md) | Program Visual Studio w systemie Windows | Zużycie | Oferuje łatwy w użyciu interfejs użytkownika do instalowania pakietów i zarządzania nimi w projektach programu Visual Studio. |
| [Zarządzaj interfejsem użytkownika NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Zużycie | Zapewnianie łatwego w użyciu interfejsu użytkownika do instalowania pakietów i zarządzania nimi w projektach Visual Studio dla komputerów Mac. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Tworzenie, użycie | Zapewnia możliwość tworzenia pakietów i przywracania pakietów używanych w projekcie bezpośrednio za pomocą łańcucha narzędzi programu MSBuild. |

Jak widać, narzędzia NuGet, z którymi pracujesz, zależą od tego, czy tworzysz, zużywają lub publikujesz pakiety oraz na platformie, na której pracujesz. Twórcy pakietu są zazwyczaj również odbiorcami, którzy tworzą na podstawie funkcjonalności, która istnieje w innych pakietach NuGet. Te pakiety oczywiście mogą być zależne od innych.

Aby uzyskać więcej informacji, Zacznij od [przepływu pracy tworzenia pakietu](create-packages/Overview-and-Workflow.md) i artykułów [przepływu pracy dotyczącego zużycia pakietów](consume-packages/Overview-and-Workflow.md) .

## <a name="managing-dependencies"></a>Zarządzanie zależnościami

Możliwość łatwej kompilacji w pracy z innymi to jedna z najbardziej zaawansowanych funkcji system zarządzania pakietami. W związku z tym większość narzędzi NuGet zarządza tym drzewem zależności lub "grafem" w imieniu projektu. Po prostu należy zainteresować siebie tylko z tymi pakietami, które są bezpośrednio używane w projekcie. Jeśli którykolwiek z tych pakietów korzysta z innych pakietów (które mogą z kolei nadal korzystać z innych), program NuGet bierze pod uwagę wszystkie te zależności niższego poziomu.

Na poniższej ilustracji przedstawiono projekt, który zależy od pięciu pakietów, co z kolei zależy od wielu innych.

![Przykładowy wykres zależności NuGet dla projektu .NET](media/dependency-graph.png)

Zauważ, że niektóre pakiety pojawiają się wiele razy na wykresie zależności. Na przykład istnieją trzy różne konsumenci pakietu B, a każdy odbiorca może także określić inną wersję dla tego pakietu (nie pokazano). Jest to typowe wystąpienie, szczególnie w przypadku powszechnie używanych pakietów. Pakiet NuGet na szczęście wykonuje wszystkie czynności twarde, aby dokładnie określić, która wersja pakietu B spełnia wszystkich klientów. Następnie program NuGet wykonuje te same działania dla wszystkich innych pakietów, niezależnie od tego, jak głębokiego wykresu zależności.

Aby uzyskać więcej informacji o tym, jak program NuGet wykonuje tę usługę, zobacz [rozpoznawanie zależności](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Śledzenie odwołań i przywracanie pakietów

Ponieważ projekty mogą łatwo przechodzić między komputery deweloperskie, repozytoria kontroli źródła, serwery kompilacji i tak dalej, wysoce niepraktyczne jest utrzymywanie binarnych zestawów pakietów NuGet bezpośrednio powiązanych z projektem. Dzięki temu każda kopia projektu niekoniecznie bloated (a tym samym miejsce w repozytoriach kontroli źródła). Może być również trudne do aktualizowania plików binarnych pakietu do nowszych wersji, ponieważ należy zastosować aktualizacje we wszystkich kopiach projektu.

Zamiast tego program NuGet utrzymuje prostą listę referencyjną pakietów, od których zależy projekt, w tym zarówno zależności najwyższego poziomu, jak i niskiego poziomu. Oznacza to, że za każdym razem, gdy instalujesz pakiet z jakiegoś hosta w projekcie, NuGet rejestruje identyfikator pakietu i numer wersji na liście referencyjnej. (Odinstalowanie pakietu oczywiście powoduje usunięcie go z listy). Następnie pakiet NuGet umożliwia przywrócenie wszystkich pakietów, do których istnieją odwołania, zgodnie z opisem w temacie [przywracanie pakietu](consume-packages/package-restore.md).

![Lista odwołań NuGet jest tworzona podczas instalacji pakietu i może być używana do przywracania pakietów w innym miejscu](media/nuget-restore.png)

Po wybraniu tylko listy odwołania program NuGet może ponownie&mdash;zainstalować program, a następnie *przywrócić*&mdash;wszystkie te pakiety z hostów publicznych i/lub prywatnych w późniejszym czasie. Podczas zatwierdzania projektu do kontroli źródła lub udostępniania go w inny sposób należy uwzględnić tylko listę odwołania i wykluczyć wszystkie pliki binarne pakietów (zobacz [pakiety i kontrola źródła](consume-packages/packages-and-source-control.md)).

Komputer, który odbiera projekt, taki jak serwer kompilacji, który uzyskuje kopię projektu w ramach zautomatyzowanego systemu wdrażania, po prostu prosi NuGet o przywrócenie zależności, gdy są potrzebne. Systemy kompilacji, takie jak Azure DevOps, udostępniają kroki "Przywróć NuGet" w tym konkretnym celu. Podobnie, gdy deweloperzy uzyskują kopię projektu (jak w przypadku klonowania repozytorium), mogą wywołać polecenie takie jak `nuget restore` (interfejs wiersza polecenia NuGet), `dotnet restore` (interfejs wiersza polecenia dotnet `Install-Package` ) lub (konsola Menedżera pakietów), aby uzyskać wszystkie wymagane pakiety. Program Visual Studio, z jego części, automatycznie przywraca pakiety podczas kompilowania projektu (pod warunkiem, że automatyczne przywracanie jest włączone, zgodnie z opisem w [przywracania pakietu](consume-packages/package-restore.md)).

Jasno rzecz mówiąc, podstawowa rola narzędzia NuGet, w której deweloperzy są przechowywał tę listę referencyjną w imieniu projektu i dostarczającą środki do wydajnego przywracania (i aktualizowania) tych pakietów, do których się odwołuje. Ta lista jest utrzymywana w jednym z dwóch *formatów zarządzania pakietami*, ponieważ są one wywoływane:

- [PackageReference](consume-packages/package-references-in-project-files.md) (lub "odwołania do pakietów w plikach projektu") | *(NuGet 4.0 +)* Zachowuje listę zależności najwyższego poziomu projektu bezpośrednio w pliku projektu, więc nie jest wymagany żaden oddzielny plik. Skojarzony plik `obj/project.assets.json`,,, jest generowany dynamicznie w celu zarządzania ogólnym wykresem zależności pakietów używanych przez projekt wraz ze wszystkimi zależnościami niskiego poziomu. PackageReference jest zawsze używana przez projekty .NET Core.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)* Plik XML, który przechowuje płaską listę wszystkich zależności w projekcie, w tym zależności innych zainstalowanych pakietów. Zainstalowane lub przywrócone pakiety są przechowywane w `packages` folderze.

Który format zarządzania pakietami jest używany w dowolnym projekcie, zależy od typu projektu i dostępnej wersji programu NuGet (i/lub programu Visual Studio). Aby sprawdzić, jaki format jest używany, po zainstalowaniu pierwszego `packages.config` pakietu wystarczy poszukać w katalogu głównym projektu. Jeśli nie masz tego pliku, poszukaj w pliku projektu bezpośrednio dla \<elementu PackageReference.\>

W przypadku wybrania opcji zalecamy użycie PackageReference. `packages.config`jest zachowywana w przypadku starszych celów i nie jest już aktywnie opracowywany.

> [!Tip]
> Różnych `nuget.exe` poleceń interfejsu wiersza polecenia `nuget install`, takich jak, nie należy automatycznie dodawać pakietu do listy odwołania. Lista jest aktualizowana podczas instalowania pakietu przy użyciu Menedżera pakietów programu Visual Studio (interfejsu użytkownika lub konsoli) i `dotnet.exe` interfejsu wiersza polecenia.

## <a name="what-else-does-nuget-do"></a>Co jeszcze robi pakiet NuGet?

Dotychczas znasz następujące cechy programu NuGet:

- Pakiet NuGet udostępnia centralne repozytorium nuget.org z obsługą hostingu prywatnego.
- Pakiet NuGet oferuje deweloperom narzędzia potrzebne do tworzenia, publikowania i zużywania pakietów.
- Co najważniejsze, NuGet zachowuje listę referencyjną pakietów używanych w projekcie oraz możliwość przywracania i aktualizowania tych pakietów z tej listy.

Aby procesy te działały wydajnie, pakiet NuGet wykonuje pewne optymalizacje w tle. W szczególności program NuGet zarządza pamięcią podręczną pakietu i folderem pakietów globalnych na potrzeby instalacji i ponownej instalacji skrótów. Pamięć podręczna pozwala uniknąć pobierania pakietu, który został już zainstalowany na komputerze. Folder pakiety globalne umożliwia wielu projektom współużytkowanie tego samego zainstalowanego pakietu, co zmniejsza ogólną wpływ narzędzia NuGet na komputerze. Folder pamięci podręcznej i pakiety globalne są również bardzo przydatne, gdy często przywracasz większą liczbę pakietów, jak na serwerze kompilacji. Aby uzyskać więcej informacji na temat tych mechanizmów, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.

W ramach pojedynczego projektu, pakiet NuGet zarządza ogólnym wykresem zależności, który ponownie obejmuje rozwiązywanie wielu odwołań do różnych wersji tego samego pakietu. Dość często zdarza się, że projekt bierze zależność od jednego lub większej liczby pakietów, które same mają te same zależności. Niektóre z najbardziej przydatnych pakietów narzędzi na nuget.org są wykorzystywane przez wiele innych pakietów. W całym grafie zależności można łatwo uzyskać dziesięć różnych odwołań do różnych wersji tego samego pakietu. Aby uniknąć przełączenia wielu wersji tego pakietu do samej aplikacji, program NuGet sortuje, która wersja może być używana przez wszystkich klientów. (Aby uzyskać więcej informacji, zobacz [rozpoznawanie zależności](consume-packages/dependency-resolution.md)).

Poza tym, pakiet NuGet zachowuje wszystkie specyfikacje związane ze strukturą pakietów (w tym [lokalizacjami](create-packages/creating-localized-packages.md) i [symbolami debugowania](create-packages/symbol-packages.md)) oraz ich [odwołania](consume-packages/package-references-in-project-files.md) (w tym [zakresami wersji](reference/package-versioning.md#version-ranges-and-wildcards) i [wersjami wstępnymi ](create-packages/prerelease-packages.md).) Pakiet NuGet udostępnia również różne interfejsy API służące do programistycznej pracy z usługami i zapewnia wsparcie dla deweloperów, którzy piszą rozszerzenia programu Visual Studio i szablony projektów.

Poświęć chwilę na przejrzenie spisu treści tej dokumentacji i zobaczysz wszystkie te funkcje w tym miejscu oraz informacje o wersji Datowanie z powrotem do początku narzędzia NuGet.

## <a name="comments-contributions-and-issues"></a>Komentarze, wkłady i problemy

Na koniec bardzo wiele komentarzy powitalnych i wkładów do tej&mdash;dokumentacji po prostu wybierasz **Opinie** i **Edycja** poleceń w górnej części dowolnej strony lub odwiedź [listę problemów](https://github.com/NuGet/docs.microsoft.com-nuget/issues) z repozytorium i dokumentacją usługi [docs](https://github.com/NuGet/docs.microsoft.com-nuget/) w witrynie GitHub.

Powitamy również udziały w programie NuGet w [różnych repozytoriach usługi GitHub](https://github.com/NuGet/Home). Problemy dotyczące narzędzia NuGet można znaleźć [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)w witrynie.

Korzystaj z Twojego środowiska NuGet!
