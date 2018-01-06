---
title: Co to jest NuGet i jakie zadania wykonuje? | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: Obszerne jakie NuGet jest i jest
keywords: "Menedżer pakietów NuGet, użycie, tworzenia pakietu pakiet hostingu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bc6a9e154df287fee6a7e00cc1349dfa2100643
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="an-introduction-to-nuget"></a>Wprowadzenie do NuGet

Podstawowe narzędzie dla dowolnej platformy nowoczesnych programowanie jest mechanizm, za pośrednictwem której deweloperzy można utworzyć, udostępniania oraz korzystać z kodu przydatne. Często taki kod jest połączone w "packages" zawierające skompilowanego kodu (w postaci bibliotek DLL) wraz z inną zawartość w projektach, które wykorzystać te pakiety.

Dla platformy .NET, jest mechanizm udostępnianie kodu **NuGet**, który definiuje sposób pakietów dla platformy .NET są tworzone, obsługiwane i używane i udostępnia narzędzia dla każdej z tych ról. 

Po prostu umieść NuGet pakiet jest pojedynczy plik ZIP z `.nupkg` rozszerzenie zawiera skompilowanego kodu (dll), inne pliki związane z tym kodem i opisową manifestu, który zawiera informacje, takie jak numer wersji pakietu. Deweloperzy biblioteki tworzenie plików pakietów i opublikuj je na hoście. Konsumenci pakietu odbierać pakiety, dodaj je do projektów, a następnie wywołać funkcji tej biblioteki w ich kod projektu. NuGet sama obsługuje wszystkie szczegóły pośrednich.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Przepływu pakietów między twórców, hostów i konsumentów

W swojej roli jako host NuGet sam przechowuje ponad 60 000 pakietów unikatowy, publicznie dostępne w centralnym repozytorium [nuget.org](https://www.nuget.org). Te pakiety są zatrudnieni przez miliony deweloperów platformy .NET każdego dnia. NuGet można również do hostowania pakietów przez użytkowników w chmurze, w sieci prywatnej, lub nawet po prostu lokalnego systemu plików. W ten sposób te pakiety są dostępne tylko deweloperów w określonej grupie organizacji lub klienta. Opcje zostały wyjaśnione w [Hosting źródła NuGet](Hosting-Packages/Overview.md).

Niezależnie od jego natury hosta służy jako punkt połączenia między pakietu *twórców* i pakietu *konsumentów*. Twórcy kompilacji przydatne pakietów NuGet i opublikuj je na hoście. Konsumenci następnie wyszukaj użyteczne i zgodne pakiety na hostach dostępnych, pobieranie i, w tym tych pakietów w swoich projektach. Po zainstalowaniu w projekcie, interfejsy API te pakiety są dostępne z resztą kodu projektu.

![Relacja między twórców pakietu, pakietu hostów i konsumentów pakietu](media/nuget-roles.png)

W takim przypadku pakietem "zgodny" oznacza, że zawiera zestawy skompilowany dla co najmniej jeden element docelowy .NET framework, która jest zgodna z platformy docelowej projektu odbierającą. Aby pakiet powszechnie zgodne, twórcy kompiluje oddzielne zestawy dla różnych platform docelowych i zawiera wszystkie z nich w tym samym pakiecie. Podczas instalowania tego pakietu klienta NuGet wyodrębnia tylko zestawy, które są wymagane przez projekt. Pozwala to zmniejszyć wpływ pakietu w końcowym aplikacji i/lub zestawy utworzone przez tego projektu.

## <a name="nuget-tools"></a>Narzędzia NuGet

Oprócz obsługi pomocy technicznej, NuGet zapewnia różne narzędzia używane zarówno twórcy, jak i użytkowników:

| Narzędzie | Platformy | Scenariusze zastosowania | Opis |
| --- | --- | --- | --- |
| [nuget.exe interfejsu wiersza polecenia](Tools/nuget-exe-CLI-Reference.md) | Wszystkie | Tworzenie, zużycia | Zawiera wszystkie funkcje NuGet, z niektórych poleceń stosowania specjalnie do pakietu twórcy, niektóre mające zastosowanie tylko do użytkowników, i inne osoby mające zastosowanie do obu. Na przykład pakiet Użyj twórców `nuget pack` polecenie, aby utworzyć pakiet z różnych zestawów i powiązane pliki, użyj konsumentów pakietu `nuget install` pakiety mają być projektem i wszyscy używa `nuget config` konfiguracji NuGet zmienne.  |
| [Interfejs użytkownika menedżera pakietów](Tools/Package-Manager-UI.md) | Visual Studio w systemie Windows | Zużycie | Zapewnia łatwy w użyciu interfejsu użytkownika dotyczące instalowania i zarządzania pakietami w projektach platformy .NET. | 
| [Zarządzanie NuGet interfejsu użytkownika](/visualstudio/mac/nuget-walkthrough) | Visual Studio for Mac | Zużycie | Podaj łatwy w użyciu interfejsu użytkownika dotyczące instalowania i zarządzania pakietami w projektach platformy .NET. |
| [Konsola menedżera pakietów](Tools/Package-Manager-Console.md) | Visual Studio w systemie Windows | Zużycie | Udostępnia [poleceń programu PowerShell](Tools/Powershell-Reference.md) instalowania i zarządzania pakietami w projektach platformy .NET. | 
| [DotNet interfejsu wiersza polecenia](Tools/dotnet-Commands.md) | Wszystkie | Tworzenie, zużycia | Zapewnia możliwości bezpośrednio w ramach łańcuch narzędzi platformy .NET Core niektórych interfejsu wiersza polecenia NuGet. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Tworzenie, zużycia | Zapewnia możliwość tworzenia pakietów i przywrócenia pakietów używane w projekcie bezpośrednio przez łańcuch narzędzi programu MSBuild. |

Jak widać, narzędzia, z którymi współpracujesz NuGet zależą od znacznie na pakiety czy w przypadku tworzenia (i publikowania) lub korzystanie z, a platforma pracy. Więcej szczegółów można znaleźć w [przepływ pracy tworzenia pakietu](Create-Packages/Overview-and-Workflow.md) i [przepływu pracy przez pakiet](Consume-Packages/Overview-and-Workflow.md) tematy, wraz z innych tematach w tych sekcjach. 

Twórcy pakietu zazwyczaj są to również użytkowników, zgodnie z ich bazując na funkcje, które istnieje w innych pakietach NuGet. I tych pakietów, mogą z kolei są zależne od nadal innych użytkowników.

## <a name="managing-dependencies"></a>Zarządzanie zależności

Umożliwia łatwe tworzenie w pracy innych jest jednym z rzeczy, które powoduje, że system zarządzania pakiet tak zaawansowanego. W związku z tym większość NuGet jest zarządzanie tym drzewie zależności lub "wykresu" w imieniu projektu. Prostu, użytkownik musi dotyczyć jedynie samodzielnie z tych pakietów, których używasz bezpośrednio w projekcie. Jeśli żadnego z tych samych pakietów korzystać z innych pakietów (które może używać pakietów) NuGet zapewnia obsługę tych zależności niższego poziomu.

Na poniższej ilustracji przedstawiono projekt, który jest zależny od pięciu pakietów, które z kolei są zależne od wielu innych.  

![Wykres zależności NuGet przykład dla projektu platformy .NET](media/dependency-graph.png)

Należy zauważyć, że niektóre pakiety występuje wiele razy na wykresie zależności. Na przykład istnieją trzy różne konsumentów pakietu B, a każdy odbiorca może również określić inną wersję tego pakietu (tego nie pokazano). Ponieważ jest to często dochodzi, NuGet na szczęście jest cała praca dokładnie wersji pakietu B spełnia swoich odbiorców. Następnie NuGet jest taka sama dla wszystkich innych pakietów, niezależnie od tego, jak głęboko staje się na wykresie zależności.

Więcej szczegółów w sposób NuGet wykonywania tej usługi, zobacz [rozpoznawania zależności](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Odwołań śledzenia i przywracanie pakietów

Ponieważ projekty mogą łatwo przenosić między komputerami deweloperów, repozytoria kontroli źródła, serwery kompilacji i itp., jest bardzo niemożliwe do zachowania binarne zestawy z pakietami NuGet bezpośrednio powiązany z projektem. Nie tylko spowoduje to, że każdy skopiuj niepotrzebnie przeglądarek projektu (i tym samym utratę miejsca w repozytoria kontroli źródła), jego również spowodowałoby, że bardzo trudne zaktualizować do nowszej wersji, ponieważ będzie to miało być przeprowadzane przez wszystkie kopie plików binarnych pakietu Projekt. 

Zamiast tego NuGet po prostu przechowuje odwołanie listę pakietów, od których zależy od (wraz z zależnościami najwyższego poziomu oraz niższych) projektu i udostępnia środki do przywrócenia wszystkich przywoływanych pakietów na żądanie, zgodnie z opisem na [pakietu Przywróć](Consume-Packages/Package-Restore.md). Oznacza to, że podczas instalowania pakietu z niektórych hosta do projektu, NuGet rejestruje identyfikator pakietu i numer wersji na tej liście odwołania. (Odinstalowanie pakietu, usuwa ją z listy.) 

![Lista odwołań NuGet jest tworzony w instalacji pakietu i może służyć do przywrócenia pakietów w innym miejscu](media/nuget-restore.png)

Z tylko listę odwołań NuGet ponownie zainstalować&mdash;oznacza to, Przywróć&mdash;wszystkie pakiety z hostów publiczne i prywatne w dowolnym momencie nowsze. (Z tego powodu nuget.org nie zezwala na trwałe usunięcie opublikowanej pakietów, chociaż można ich ukryć; zobacz [usunięcie pakietów](Policies/deleting-packages.md).) Podczas zatwierdzania projekt do kontroli źródła lub udostępnianie w inny sposób, muszą zawierać tylko na liście, a nie musi zawierać wszystkie pliki binarne pakietu (zobacz [pakietów i kontroli źródła](Consume-Packages/Packages-and-Source-Control.md).)

Komputer, który odbiera projektu, takich jak serwer kompilacji, uzyskując kopię projektu jako część systemu automatycznego wdrażania zapyta, po prostu NuGet, aby przywrócić zależności zawsze, gdy są potrzebne. Stworzyć systemy, takie jak Visual Studio Team Services zawierają opis etapów "Przywracanie NuGet", w tym celu dokładnego. Podobnie, gdy deweloperzy uzyskać kopię projektu (tak jak w przypadku klonowania repozytorium) następnie otwórz projekt w programie Visual Studio i uruchom kompilację, Visual Studio automatycznie przywraca wymaganych pakietów NuGet. Deweloperzy może także określić NuGet pod kątem przywracania pakietów w dowolnej chwili za pomocą `nuget restore` polecenia interfejsu wiersza polecenia lub `Install-Package` polecenia cmdlet w konsoli Menedżera pakietów.

Wyraźnie widać następnie podstawową rolą NuGet, których dotyczy to deweloperom jest utrzymanie tej listy odwołania w imieniu projektu i umożliwianie wydajnie przywrócić (i zaktualizować) tych pakietów do którego istnieje odwołanie.

Jak dokładnie dzieje się to powstał przez różne wersje programu NuGet, co w kilku *pakietu zarządzania formaty*, jak są nazywane:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 +)* pliku XML, który przechowuje to płaska lista wszystkie zależności w projekcie, wraz z zależnościami innych zainstalowanych pakietów. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0 +)* pliku A JSON, który przechowuje listę zależności projektu z ogólną wykres pakietu w skojarzony plik `project.lock.json`. Taka struktura zapewnia lepszą wydajność za pośrednictwem `packages.config` zgodnie z opisem na [rozpoznawania zależności](Consume-Packages/Dependency-Resolution.md), włączając przechodnie przywracania, ale sam została zazwyczaj zastąpiona PackageReference poniżej.
- [Pakiet odwołań w plikach projektu](Consume-Packages/Package-References-in-Project-Files.md) (znanej także jako "PackageReference") | *(NuGet 4.0 +)* przechowuje listę najwyższego poziomu zależności projektu bezpośrednio w pliku projektu, więc nie jest wymagane nie oddzielny plik. Skojarzony plik `project.assets.json`, generowane dynamicznie jak `project.lock.json` do zarządzania ogólną wykresu zależności.

Format pakietu administracyjnego jest stosowanych w żadnym konkretnym projektem zależy od tego, typ projektu i dostępna wersja NuGet i Visual Studio. Aby sprawdzić, jakie format jest używany, po prostu wyszukaj `packages.config` lub `project.json` w katalogu głównym projektu po zainstalowaniu pakietu pierwszy. Jeśli nie widzisz albo plikiem, poszukaj w pliku projektu bezpośrednio dla &lt;PackageReference&gt;elementu.

W programie Visual Studio 2017 r, na przykład większość typów projektu użyj `packages.config` z wyjątkiem projektów platformy UWP C# i .NET Core, które używają PackageReference. 

## <a name="what-else-does-nuget-do"></a>Co działa NuGet?

Podsumowując, co możemy zostały objęte wykonanej do tej pory, NuGet zawiera (w swojej roli hostingu) repozytorium nuget.org centralnej i obsługuje hosting prywatnych. NuGet oferuje deweloperom narzędzia potrzebne do tworzenia, publikowanie i korzystanie z pakietów. I najważniejsze, NuGet obsługuje listę odwołania pakietów używany w projekcie i możliwości przywracania oraz tych pakietów z listy aktualizacji.

Aby te procesy wydajną pracę, NuGet ma pewne optymalizacje wewnętrznych. Głównie NuGet zarządza zarówno komputera i buforuje specyficznego dla projektu pakietu instalacji skrótów i ponownej instalacji. Gdzie dotyczy pamięci podręcznej komputera dowolnego pakietu, który można pobrać i zainstalować w projekcie są przechowywane w pamięci podręcznej, tak, aby instalowania tego samego pakietu w innym projekcie nie ma pobrać ją ponownie. Jest to wyraźnie bardzo przydatne podczas często w przypadku przywracania większej liczby pakietów, jak na serwerze kompilacji. Więcej szczegółów na mechanizmie oraz sposób pracy z nim, zobacz [Zarządzanie pamięci podręcznej NuGet](Consume-Packages/Managing-the-Nuget-Cache.md).

W ramach pojedynczego projektu NuGet jest dużo pracy do zarządzania na wykresie zależności ogólnej. (Przy użyciu `project.json` lub &lt;PackageReference&gt;, NuGet śledzi, że informacje w dodatkowej pliku o nazwie `project.lock.json` i `project.assets.json`odpowiednio.) Ponownie w tym rozwiązaniu wiele odwołań do różnych wersji tego samego pakietu.

Oznacza to, że jest dość często, że projekt ma zależność na co najmniej jeden pakiet, że mają się tym samym zależności. Na przykład niektóre najbardziej przydatne pakiety narzędzia na nuget.org zatrudnionych przez inne pakiety. W na wykresie zależności całego, 10, możesz łatwo może mieć dziesięć różne odwołania do różnych wersji tego samego pakietu. Jednak nie będzie można wyświetlić wiele wersji tego pakietu do aplikacji, więc NuGet sortuje używaną wersję pojedynczego, którego mogą używać Wszyscy. (Zobacz [rozpoznawania zależności](Consume-Packages/Dependency-Resolution.md) Aby uzyskać więcej informacji na ten temat.)

Ponadto NuGet obsługuje wszystkie wymagania dotyczące struktury pakietów (łącznie z [lokalizacja](Create-Packages/Creating-Localized-Packages.md) i [symbole debugowania](Create-Packages/Symbol-Packages.md)) i jak są przywoływane (w tym [ zakresy wersji](reference/package-versioning.md#version-ranges-and-wildcards) i [wersje wstępne](create-packages/Prerelease-Packages.md).) NuGet udostępnia interfejsy API dla dostawcy poświadczeń (w przypadku uzyskiwania dostępu do hostów prywatnej) i dla deweloperów, którzy zapisu rozszerzeń programu Visual Studio i szablony projektu.

Poświęć chwilę, aby przeglądać spis treści niniejszej dokumentacji i zostaną wyświetlone wszystkie te możliwości reprezentowane istnieje, oraz informacje o wersji sprzed początku NuGet.

## <a name="comments-contributions-and-issues"></a>Komentarze, udziały i problemów

Na koniec znacznie prosimy komentarze i udziału w niniejszej dokumentacji&mdash;po prostu wybierz **komentarze** i **Edytuj** poleceń w dowolnej strony lub odwiedź [repozytorium dokumentów ](https://github.com/NuGet/docs.microsoft.com-nuget/) i [Lista problemów docs](https://github.com/NuGet/docs.microsoft.com-nuget/issues) w witrynie GitHub.

Prosimy udział NuGet się za pośrednictwem jego [różnych repozytoriów GitHub](https://github.com/NuGet/Home); Problemy z NuGet można znaleźć w [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

Owocnej środowiska NuGet
