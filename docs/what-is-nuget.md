---
title: Co to jest NuGet i co robi?
description: Kompleksowe wprowadzenie do tego, czym nuget jest i co robi
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: c326cf184ff20fb798a5770f0a4cf9bf42bed3f5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230697"
---
# <a name="an-introduction-to-nuget"></a>Wprowadzenie do NuGet

Podstawowym narzędziem dla każdej nowoczesnej platformy programistycznej jest mechanizm, za pomocą którego deweloperzy mogą tworzyć, udostępniać i używać użytecznego kodu. Często taki kod jest wiązany do "pakietów", które zawierają skompilowany kod (jako biblioteki DLL) wraz z inną zawartością potrzebną w projektach, które korzystają z tych pakietów.

W przypadku platformy .NET (w tym platformy .NET Core) obsługiwany przez firmę Microsoft mechanizm udostępniania kodu to **NuGet**, który definiuje sposób tworzenia, hostowania i korzystania z pakietów dla platformy .NET oraz [udostępnia narzędzia](install-nuget-client-tools.md) dla każdej z tych ról.

Mówiąc prościej, pakiet NuGet jest `.nupkg` pojedynczy plik ZIP z rozszerzeniem, który zawiera skompilowany kod (DLL), inne pliki związane z tym kodem i manifest opisowy, który zawiera informacje, takie jak numer wersji pakietu. Deweloperzy z kodem do udostępniania pakietów tworzenia i publikowania ich do hosta publicznego lub prywatnego. Konsumenci pakietów uzyskują te pakiety od odpowiednich hostów, dodają je do swoich projektów, a następnie wywołują funkcjonalność pakietu w kodzie projektu. NuGet się następnie obsługuje wszystkie szczegóły pośrednie.

Ponieważ NuGet obsługuje hosty prywatne obok hosta nuget.org publicznych, można użyć pakietów NuGet do udostępniania kodu, który jest wyłączny dla organizacji lub grupy roboczej. Można również użyć pakietów NuGet jako wygodny sposób, aby uwzględnić własny kod do użycia w nic, ale własne projekty. W skrócie pakiet NuGet jest jednostką kodu współużytkowanych, ale nie wymaga ani nie implikuje żadnych szczególnych środków udostępniania.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Przepływ pakietów między twórcami, hostami i konsumentami

W roli hosta publicznego, NuGet sam utrzymuje centralne repozytorium ponad 100.000 unikalnych pakietów w [nuget.org](https://www.nuget.org). Pakiety te są codziennie wykorzystywane przez miliony programistów .NET/.NET Core. NuGet umożliwia również hostowania pakietów prywatnie w chmurze (na przykład w usłudze Azure DevOps), w sieci prywatnej, a nawet tylko w lokalnym systemie plików. W ten sposób te pakiety są dostępne tylko dla tych deweloperów, którzy mają dostęp do hosta, co daje możliwość udostępnienia pakietów określonej grupie konsumentów. Opcje są wyjaśnione na [hosting własnych kanałów NuGet](hosting-packages/overview.md). Za pomocą opcji konfiguracji można również kontrolować dokładnie, które hosty mogą być dostępne dla danego komputera, zapewniając w ten sposób, że pakiety są uzyskiwane z określonych źródeł, a nie z publicznego repozytorium, takiego jak nuget.org.

Niezależnie od jego charakteru, gospodarz służy jako punkt połączenia między *twórcami pakietów* a *konsumentami pakietów.* Twórcy tworzyć przydatne pakiety NuGet i publikować je do hosta. Następnie konsumenci wyszukują przydatne i kompatybilne pakiety na dostępnych hostach, pobierając i włączając te pakiety do swoich projektów. Po zainstalowaniu w projekcie interfejsy API pakietów są dostępne dla pozostałej części kodu projektu.

![Relacje między twórcami pakietów, hostami pakietów i odbiorcami pakietów](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Zgodność z kierowaniami pakietami

Pakiet "kompatybilny" oznacza, że zawiera zestawy utworzone dla co najmniej jednego docelowego programu .NET framework, który jest zgodny z platformą docelową projektu zużywającego. Deweloperzy mogą tworzyć pakiety, które są specyficzne dla jednej struktury, podobnie jak w przypadku formantów platformy uniwersalnej systemu i platformy uniwersalnej lub mogą obsługiwać szerszy zakres obiektów docelowych. Aby zmaksymalizować zgodność pakietu, deweloperzy target [.NET Standard](/dotnet/standard/net-standard), które wszystkie .NET i .NET Core projektów może korzystać. Jest to najbardziej efektywny środek zarówno dla twórców, jak i konsumentów, ponieważ pojedynczy pakiet (zwykle zawierający jeden zestaw) działa dla wszystkich projektów zużywających.

Deweloperzy pakietów, którzy wymagają interfejsów API poza .NET Standard, z drugiej strony, utworzyć oddzielne zestawy dla różnych struktur docelowych, które chcą obsługiwać i uwzględnić wszystkie te zestawy w tym samym pakiecie (który jest nazywany "multi-targeting"). Gdy konsument instaluje taki pakiet, NuGet wyodrębnia tylko te zestawy, które są potrzebne przez projekt. Minimalizuje to rozmiar pakietu w ostatecznej aplikacji i/lub zestawów produkowanych przez ten projekt. Pakiet z wieloma celami jest oczywiście trudniejszy do utrzymania dla jego twórcy.

> [!Note]
> Targetowanie .NET Standard zastępuje poprzednie podejście przy użyciu różnych docelowych biblioteki klas przenośnych (PCL). W związku z tym ta dokumentacja koncentruje się na tworzeniu pakietów dla platformy .NET Standard.

## <a name="nuget-tools"></a>Narzędzia NuGet

Oprócz obsługi hostingu NuGet udostępnia również wiele narzędzi używanych zarówno przez twórców, jak i konsumentów. Zobacz [Instalowanie narzędzi klienta NuGet,](install-nuget-client-tools.md) aby dowiedzieć się, jak uzyskać określone narzędzia.

| Narzędzie | Platformy | Odpowiednie scenariusze | Opis |
| --- | --- | --- | --- |
| [Interfejs wiersza polecenia dotnet](consume-packages/install-use-packages-dotnet-cli.md) | Wszystkie | Tworzenie, konsumpcja | Narzędzie INTERFEJSU WIERSZA dla bibliotek .NET Core i .NET Standard oraz dla projektów w stylu zestawu SDK przeznaczonych dla programu .NET Framework (zobacz [atrybut SDK](/dotnet/core/tools/csproj#additions)). Zapewnia pewne funkcje interfejsu wiersza polecenia NuGet bezpośrednio w łańcuchu narzędzi .NET Core. Podobnie jak `nuget.exe` w wierszu polecenia, dotnet interfejsu wiersza polecenia nie wchodzi w interakcje z projektami programu Visual Studio. |
| [Interfejs wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md) | Wszystkie | Tworzenie, konsumpcja | Narzędzie INTERFEJSU WIERSZA dla bibliotek programu .NET Framework i projektów w stylu innych niż SDK przeznaczonych dla bibliotek .NET Standard. Zapewnia wszystkie możliwości NuGet, z niektórych poleceń stosowania specjalnie do twórców pakietu, niektóre zastosowanie tylko do konsumentów, a inne zastosowanie do obu. Na przykład twórcy `nuget pack` pakietu używają polecenia do tworzenia pakietu z różnych zestawów i powiązanych plików, konsumentów pakietów używać `nuget install` do dołączania pakietów w folderze projektu i każdy używa `nuget config` do ustawiania zmiennych konfiguracyjnych NuGet. Jako narzędzie niezależne od platformy narzędzie NuGet CLI nie wchodzi w interakcję z projektami programu Visual Studio. |
| [Konsola menedżera pakietów](consume-packages/install-use-packages-powershell.md) | Visual Studio w systemie Windows | Zużycie | Udostępnia [polecenia programu PowerShell](reference/Powershell-Reference.md) do instalowania pakietów i zarządzania nimi w projektach programu Visual Studio. |
| [Interfejs użytkownika menedżera pakietów](consume-packages/install-use-packages-visual-studio.md) | Visual Studio w systemie Windows | Zużycie | Zapewnia łatwy w użyciu interfejs użytkownika do instalowania pakietów i zarządzania nimi w projektach programu Visual Studio. |
| [Zarządzanie interfejsem użytkownika NuGet](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Zużycie | Udostępnij łatwy w użyciu interfejs użytkownika do instalowania pakietów i zarządzania nimi w projektach programu Visual Studio dla komputerów Mac. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Tworzenie, konsumpcja | Zapewnia możliwość tworzenia pakietów i przywracania pakietów używanych w projekcie bezpośrednio za pośrednictwem łańcucha narzędzi MSBuild. |

Jak widać, narzędzia NuGet, z którymi pracujesz, zależą w dużej mierze od tego, czy tworzysz, konsumujesz lub publikujesz pakiety, a także od platformy, na której pracujesz. Twórcy pakietów są zazwyczaj również konsumentów, ponieważ opierają się one na podstawie funkcji, które istnieją w innych pakietów NuGet. A te pakiety, oczywiście, mogą z kolei zależeć od jeszcze innych.

Aby uzyskać więcej informacji, należy rozpocząć od [przepływu pracy tworzenia pakietów](create-packages/Overview-and-Workflow.md) i artykułów [przepływu pracy zużycie pakietu.](consume-packages/Overview-and-Workflow.md)

## <a name="managing-dependencies"></a>Zarządzanie zależnościami

Możliwość łatwego budowania na pracy innych jest jedną z najpotężniejszych funkcji systemu zarządzania pakietami. W związku z tym wiele z tego, co NuGet nie jest zarządzanie tego drzewa zależności lub "wykres" w imieniu projektu. Po prostu powiedział, trzeba tylko dotyczyć się z tych pakietów, które są bezpośrednio używane w projekcie. Jeśli którykolwiek z tych pakietów się zużywają inne pakiety (które z kolei mogą zużywać jeszcze inne), NuGet zajmuje się wszystkie te zależności na poziomie.

Na poniższej ilustracji przedstawiono projekt, który zależy od pięciu pakietów, które z kolei zależą od wielu innych.

![Przykładowy wykres zależności NuGet dla projektu .NET](media/dependency-graph.png)

Należy zauważyć, że niektóre pakiety pojawiają się wiele razy na wykresie zależności. Na przykład istnieją trzy różnych konsumentów pakietu B, a każdy konsument może również określić inną wersję dla tego pakietu (nie pokazano). Jest to powszechne zjawisko, szczególnie w przypadku powszechnie używanych pakietów. NuGet na szczęście wykonuje całą ciężką pracę, aby dokładnie określić, która wersja pakietu B spełnia wszystkich konsumentów. NuGet następnie robi to samo dla wszystkich innych pakietów, bez względu na to, jak głęboki wykres zależności.

Aby uzyskać więcej informacji na temat sposobu wykonywania tej usługi przez nuget, zobacz [Rozpoznawanie zależności.](concepts/dependency-resolution.md)

## <a name="tracking-references-and-restoring-packages"></a>Śledzenie odwołań i przywracanie pakietów

Ponieważ projekty można łatwo przenosić między komputerami deweloperów, repozytoria kontroli źródła, budować serwery i tak dalej, jest wysoce niepraktyczne, aby zachować zestawy binarne pakietów NuGet bezpośrednio powiązane z projektem. W ten sposób każda kopia projektu niepotrzebnie nadęty (a tym samym miejsca na odpady w repozytoriach kontroli źródła). Byłoby to również bardzo trudne do aktualizacji plików binarnych pakietu do nowszych wersji, jak aktualizacje musiałyby być stosowane we wszystkich kopiach projektu.

NuGet zamiast tego utrzymuje prostą listę odwołań pakietów, od których zależy projekt, w tym zależności najwyższego i down-level. Oznacza to, że za każdym razem, gdy instalujesz pakiet z jakiegoś hosta w projekcie, NuGet rejestruje identyfikator pakietu i numer wersji na liście odwołań. (Odinstalowanie pakietu oczywiście usuwa go z listy). NuGet następnie zapewnia środki do przywrócenia wszystkich pakietów, do których istnieje odwołanie na żądanie, zgodnie z opisem w [przywracaniu pakietu.](consume-packages/package-restore.md)

![Lista odwołań NuGet jest tworzona podczas instalacji pakietu i może służyć do przywracania pakietów w innym miejscu](media/nuget-restore.png)

Z tylko listy odwołań NuGet można&mdash;następnie ponownie zainstalować, czyli *przywrócić*&mdash;wszystkie te pakiety z publicznych i/lub prywatnych hostów w dowolnym późniejszym czasie. Podczas zatwierdzania projektu do kontroli źródła lub udostępniania go w inny sposób, należy dołączyć tylko listę odwołań i wykluczyć wszelkie pliki binarne pakietu (zobacz [Pakiety i kontroli źródła](consume-packages/packages-and-source-control.md).)

Komputer, który odbiera projekt, takich jak serwer kompilacji uzyskania kopii projektu w ramach automatycznego systemu wdrażania, po prostu prosi NuGet przywrócić zależności, gdy są one potrzebne. Tworzenie systemów, takich jak Azure DevOps zapewniają kroki "Przywracanie NuGet" w tym dokładnie celu. Podobnie, gdy deweloperzy uzyskać kopię projektu (jak podczas klonowania repozytorium), `nuget restore` mogą wywołać `dotnet restore` polecenia, takie jak `Install-Package` (NuGet CLI), (dotnet CLI) lub (Package Manager Console) w celu uzyskania wszystkich niezbędnych pakietów. Visual Studio, ze swojej strony, automatycznie przywraca pakiety podczas tworzenia projektu (pod warunkiem, że automatyczne przywracanie jest włączone, zgodnie z opisem w [przywracaniu pakietu](consume-packages/package-restore.md)).

Oczywiście, a następnie główną rolę NuGet, gdzie deweloperzy są zainteresowane jest utrzymanie tej listy odwołań w imieniu projektu i zapewnienie środków do skutecznego przywracania (i aktualizacji) tych pakietów, do których istnieje odwołanie. Ta lista jest obsługiwana w jednym z dwóch *formatów zarządzania pakietami,* tak jak są one nazywane:

- [PackageReference](consume-packages/package-references-in-project-files.md) (lub "odwołania do pakietów w plikach projektu") | *(NuGet 4.0+)* Przechowuje listę zależności najwyższego poziomu projektu bezpośrednio w pliku projektu, więc nie jest potrzebny osobny plik. Skojarzony plik `obj/project.assets.json`, jest generowany dynamicznie w celu zarządzania ogólnym wykresem zależności pakietów używanych przez projekt wraz ze wszystkimi zależnościami na poziomie w dół. PackageReference jest zawsze używany przez projekty .NET Core.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0+)* Plik XML, który utrzymuje płaską listę wszystkich zależności w projekcie, w tym zależności innych zainstalowanych pakietów. Zainstalowane lub przywrócone pakiety `packages` są przechowywane w folderze.

Format zarządzania pakietami jest stosowany w danym projekcie zależy od typu projektu i dostępnej wersji NuGet (i/lub visual studio). Aby sprawdzić, jaki format jest `packages.config` używany, po prostu poszukaj w katalogu głównym projektu po zainstalowaniu pierwszego pakietu. Jeśli nie masz tego pliku, poszukaj w \<pliku projektu\> bezpośrednio dla PackageReference elementu.

Gdy masz wybór, zaleca się korzystanie PackageReference. `packages.config`jest utrzymywana do celów starszych i nie jest już w fazie aktywnego rozwoju.

> [!Tip]
> Różne `nuget.exe` polecenia INTERFEJSU `nuget install`WIERSZA, takie jak , nie automatycznie dodają pakiet do listy odwołań. Lista jest aktualizowana podczas instalowania pakietu z Menedżerem pakietów `dotnet.exe` programu Visual Studio (UI lub Konsola) i z interfejsem wiersza polecenia.

## <a name="what-else-does-nuget-do"></a>Do czego jeszcze działa NuGet?

Do tej pory nauczyłeś się następujących cech NuGet:

- NuGet zapewnia centralne repozytorium nuget.org z obsługą hostingu prywatnego.
- NuGet zapewnia narzędzia potrzebne deweloperom do tworzenia, publikowania i korzystania z pakietów.
- Co najważniejsze, NuGet przechowuje listę odwołań pakietów używanych w projekcie i możliwość przywracania i aktualizowania tych pakietów z tej listy.

Aby te procesy działały wydajnie, NuGet wykonuje pewne zakulisowe optymalizacje. W szczególności NuGet zarządza pamięcią podręczną pakietów i globalnym folderem pakietów w celu zainstalowania i ponownej instalacji skrótów. Pamięć podręczna pozwala uniknąć pobierania pakietu, który został już zainstalowany na komputerze. Folder pakietów globalnych umożliwia wiele projektów do udziału w tym samym zainstalowanym pakiecie, zmniejszając w ten sposób ogólny ślad NuGet na komputerze. Pamięć podręczna i folder pakietów globalnych są również bardzo pomocne, gdy często przywracasz większą liczbę pakietów, jak na serwerze kompilacji. Aby uzyskać więcej informacji na temat tych mechanizmów, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](consume-packages/managing-the-global-packages-and-cache-folders.md).

W ramach pojedynczego projektu NuGet zarządza ogólny wykres zależności, który ponownie zawiera rozwiązywanie wielu odwołań do różnych wersji tego samego pakietu. Jest dość powszechne, że projekt ma zależność od jednego lub więcej pakietów, które same mają takie same zależności. Niektóre z najbardziej przydatnych pakietów narzędziowych na nuget.org są wykorzystywane przez wiele innych pakietów. Na wykresie całej zależności, a następnie można łatwo mieć dziesięć różnych odwołań do różnych wersji tego samego pakietu. Aby uniknąć wprowadzania wielu wersji tego pakietu do samej aplikacji, NuGet sortuje, która wersja pojedyncza może być używana przez wszystkich konsumentów. (Aby uzyskać więcej informacji, zobacz [Rozpoznawanie zależności](concepts/dependency-resolution.md).)

Poza tym NuGet zachowuje wszystkie specyfikacje związane z strukturą pakietów (w tym symbolami [lokalizacji](create-packages/creating-localized-packages.md) i [debugowania)](create-packages/symbol-packages-snupkg.md)i sposobu [odwoływania się do ich (w](consume-packages/package-references-in-project-files.md) tym [zakresów wersji](concepts/package-versioning.md#version-ranges) i [wersji wstępnych](create-packages/prerelease-packages.md)).) NuGet udostępnia również różne interfejsy API do pracy z jego usług programowo i zapewnia obsługę dla deweloperów, którzy piszą rozszerzenia programu Visual Studio i szablony projektów.

Poświęć chwilę, aby przejrzeć spis treści dla tej dokumentacji i zobaczysz wszystkie te możliwości reprezentowane tam, wraz z informacji o wersji sięga początków NuGet.Take a moment to browse the table of contents for this documentation, and you see all of these capabilities represented there, along with release notes dating back to NuGet's beginnings.

## <a name="related-video"></a>Podobne wideo

> [!Video https://channel9.msdn.com/Series/NuGet-101/What-is-NuGet-1-of-5/player]

Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="comments-contributions-and-issues"></a>Uwagi, opinie i problemy

Na koniec bardzo mile widziane komentarze i&mdash;wkłady do tej dokumentacji po prostu wybierz **polecenia Opinie** i **Edytuj** u góry dowolnej strony lub odwiedź listę [repozytorium dokumentów](https://github.com/NuGet/docs.microsoft.com-nuget/) i [dokumentów](https://github.com/NuGet/docs.microsoft.com-nuget/issues) w GitHub.

Zapraszamy również do udziału w NuGet się za pośrednictwem [różnych repozytoriów GitHub;](https://github.com/NuGet/Home) Problemy NuGet można [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)znaleźć na .

Ciesz się swoim doświadczeniem NuGet!
