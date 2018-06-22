---
title: Informacje o wersji NuGet 3.0 w wersji zapoznawczej
description: Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr 3.0 NuGet w wersji zapoznawczej.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 67c217e52d975ed8f6889cd69f9b7e0d52b3a119
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821317"
---
# <a name="nuget-30-preview-release-notes"></a>Informacje o wersji NuGet 3.0 w wersji zapoznawczej

[Informacje o wersji RC NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta informacje o wersji](../release-notes/nuget-3.0-beta.md)

12 listopada 2014 r. w ramach wersji programu Visual Studio 2015 Preview został wydany NuGet 3.0 w wersji zapoznawczej. Firma Microsoft opublikowała program NuGet 3.0 w wersji zapoznawczej. Jest to duży wersji firmie Microsoft (chociaż wersja zapoznawcza), i radością zacznij uzyskiwać opinie na temat naszych zmian.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Podgląd NuGet 3.0 znajduje się w programie Visual Studio 2015 Preview. Pracujemy, aby uzyskać podgląd porzucania dla programu Visual Studio 2012 i Visual Studio 2013 bardzo szybko. Wcześniej poinformowaliśmy naszych zamiarze [przerwanie aktualizacji dla programu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), i wykonujemy tej decyzji trudne.

## <a name="brand-new-ui"></a>Nowy interfejsu użytkownika

Uwagi dotyczące NuGet 3.0 w wersji zapoznawczej w pierwszej kolejności jest naszego nowego interfejsu użytkownika. Nie jest już modalnego okna dialogowego; teraz jest pełne okno dokumentu programu Visual Studio. Dzięki temu można otworzyć Interfejs użytkownika dla wielu projektów (i/lub rozwiązanie) jednocześnie, wydzielić okna na inny monitor, dock ona jednak czy tak samo, jak itp.

![Nowy interfejs użytkownika NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Poza różnice użyteczność z powodu porzucanie modalnego okna dialogowego mamy także wiele nowych funkcji w nowych interfejsu użytkownika.

### <a name="version-selection"></a>Wybór wersji

Być może najpopularniejszych funkcji interfejsu użytkownika jest wybranie wersji pakietu instalacji i aktualizacji — to jest teraz dostępna.

![Wybór wersji pakietu](./media/NuGet-3.0-Preview/version-selection.png)

Czy instalowania lub aktualizowania pakietu lista rozwijana wersji pozwala wyświetlić wszystkie dostępne dla pakietu, wersji w pewnych wersjach zauważalne awansowane na początku listy wyboru łatwe. Nie trzeba pobieranie określonych wersji, które nie są najnowsze za pomocą konsoli programu PowerShell.

### <a name="combined-installedonlineupdates-workflows"></a>Połączone przepływy pracy zainstalowany / / aktualizacje w trybie Online

Naszego poprzedniej interfejsu użytkownika miał 3 tabulatory aktualizacji oprogramowania zainstalowany w trybie Online, i. Pakiety wymienione są specyficzne dla tych przepływów pracy i Akcje dostępne zostały określone dla przepływów pracy oraz. Gdy który sprawiał logiczne, możemy heard, że wiele osób może często uzyskać samoczynnie przy tym rozdzielenie.

Mamy teraz Scalonej doświadczenia, gdzie można zainstalować, zaktualizować lub odinstalować pakiet niezależnie od tego, jak otrzymano pakietu wybranego. Aby ułatwić konkretnych przepływów pracy, mamy teraz listy rozwijanej filtru, umożliwiający filtrowanie pakietów widoczne, ale następnie Akcje dostępne dla pakietu są zgodne.

![Odinstaluj pakiet](./media/NuGet-3.0-Preview/uninstall-package.png)

Przy użyciu filtru "Installed", możesz łatwo sprawdzić zainstalowanych pakietów, które są dostępne aktualizacje, a następnie możesz odinstalować lub zaktualizować pakiet, zmieniając wybór wersji, aby zobaczyć zmiany dostępnych akcji.

![Aktualizacja pakietu](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Wersja konsolidacji

Jest to często mają tego samego pakietu zainstalowane w wielu projektów w rozwiązaniu. Czasami wersje zainstalowane w każdym projekcie można rozchodzenia się i konieczne jest konsolidacja używane wersje. NuGet 3.0 w wersji zapoznawczej wprowadzono nową funkcję właśnie w tym scenariuszu.

Okno Zarządzanie rozwiązanie na poziomie pakietu są dostępne przez kliknięcie prawym przyciskiem myszy rozwiązanie i wybierając pozycję Zarządzaj pakietami NuGet dla rozwiązania. Z tego miejsca w przypadku wybrania pakietu, który jest zainstalowany w wielu projektach, ale z różnymi wersjami w użyciu, nowa akcja "Konsoliduj" staje się dostępna. Na ekranie zrzut poniżej `Newtonsoft.Json` został zainstalowany w `SamplesClassLibrary` z wersją `6.0.4` i zainstalowane w `SamplesConsoleApp` z wersją `5.0.4`.

![Konsolidacja wersjach](./media/NuGet-3.0-Preview/consolidate.png)

Oto przepływu pracy do konsolidacji na jednej wersji.

1. Wybierz `Newtonsoft.Json` pakietu na liście
1. Wybierz `Consolidate` z `Action` listy rozwijanej
1. Użyj `Version` listy rozwijanej, aby wybrać wersję, aby być konsolidowane
1. Sprawdź pola dla projektów, które powinny być konsolidowane w tej wersji (należy pamiętać, że projekty już w wybranej wersji będzie wyszarzona)
1. Kliknij przycisk `Consolidate` przycisku konsolidacji

### <a name="operation-previews"></a>Operacja podglądy

Niezależnie od tego, która operacja wykonujesz — instalacji/aktualizacji/dezinstalacji — nowy interfejs użytkownika oferuje teraz sposób, aby wyświetlić podgląd zmiany wprowadzone do projektu. Ta wersja zapoznawcza zostaną wyświetlone wszystkie nowe pakiety, które zostaną zainstalowane, pakiety zostaną zaktualizowane, które pakiety, które zostaną odinstalowane wraz z pakietami, które mają być zmienione podczas operacji.

W poniższym przykładzie widać, że instalowanie Microsoft.AspNet.SignalR spowoduje kilka zmian do projektu.

![Instalowanie SignalR w wersji zapoznawczej](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opcje instalacji

Za pomocą konsoli programu PowerShell, użytkownik miał kontrolę nad kilka opcji zauważalne instalacji. W Interfejsie użytkownika również jest teraz dostępna teraz te funkcje. Teraz można kontrolować zachowanie rozpoznawania zależności jak wybrano wersji zależności.

![Zachowanie zależności](./media/NuGet-3.0-Preview/dependency-behavior.png)

Można również określić akcję wykonywaną, gdy pliki zawartości z pakietów w konflikcie z plikami już w projekcie.

![Akcja konflikt pliku](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Nieskończone przewijania

Firma Microsoft używany do pobierania sobą opinii naszych interfejsu użytkownika o konieczności zarówno przewijania i stronicowania wzorcami podczas wyświetlania pakietów. Było bardzo często mają do przewiń w dół krótką listę, kliknij przycisk Dalej numer strony, a następnie przewiń ponownie. Przy użyciu nowego interfejsu użytkownika wdrożyliśmy nieskończone przewijanie w listy pakietów, aby tylko wymagane przewinięcie ekranu — już stronicowania.

![Nieskończone przewijania](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Była pracy, spowodować szybkie, stał się Pretty

Możemy radością uzyskać ten nowy interfejs użytkownika można wypróbować usługę. W tej wersji zapoznawczej punktu kontrolnego, firma Microsoft już zostały następujące dobrej starego adage z "przekształcenia go w pracy, stał się szybkie, stał się bardzo." W tej wersji zapoznawczej firma Microsoft osiągnąć większość tego celu pierwszy — działa. Wiemy, nie jest jeszcze bardzo szybko i wiemy, że nie jest dość pretty jeszcze. Zaufania, że firma Microsoft będzie działać na te cele od chwili wersji RC. W międzyczasie, chcielibyśmy usłyszeć Twoja opinia o *użyteczność* nowy interfejs użytkownika — przepływ pracy, operacje i w jaki sposób go *tak* do użycia nowego interfejsu użytkownika.

Istnieje kilka funkcji, które usunięto w porównaniu do starego interfejsu użytkownika. Jeden z nich było zamierzone, a drugi właśnie nie udało się wykonać w czasie.

#### <a name="searching-all-package-sources"></a>Wyszukiwanie "Wszystkie" źródła pakietów

Starego interfejsu użytkownika można wykonać wyszukiwanie pakietu przed wszystkie źródła pakietów. Usunęliśmy tej funkcji w interfejsie użytkownika i firma Microsoft nie będzie można jej przejściem w tryb ponownie. Ta funkcja umożliwia wykonywanie operacji wyszukiwania przed wszystkie źródła pakietów, fale wyniki ze sobą i spróbuj kolejność dla wybranego sortowania wyników.

Znaleziono czy istotność wyszukiwania są naprawdę fale razem. Można wyobrazić wyszukiwania przed Google i Bing i tkaniem wyniki ze sobą? Ponadto ta funkcja była powolne, łatwo *przypadkowo* użycia i firma Microsoft uważają, rzadko została faktycznie przydatne. Z powodu problemów funkcji wprowadzone, odebrano numer na nim raportów usterki, które może nigdy nie został rozwiązany.

#### <a name="update-all"></a>Aktualizuj wszystkie

My używamy w celu zapewnienia przycisk "Aktualizuj wszystkie" starego interfejsu użytkownika, który nie ma w nowym Interfejsie jeszcze. Firma Microsoft będzie przywracania aktywności tej funkcji w naszym wersji RC.

## <a name="new-clientserver-api"></a>Nowy klient/serwer interfejsu API

Oprócz wszystkich nowych funkcji w naszym nowy interfejs zarządzania pakietami będziemy również używane na niektóre szczegóły implementacji protokołu NuGet klient/serwer. Czynności, które firma Microsoft wykonane jest utworzenie "V3 interfejsu API" programu NuGet, który jest zaprojektowana dla wysokiej dostępności dla scenariuszy o kluczowym znaczeniu, takie jak Przywracanie pakietu i instalowania pakietów. Nowy interfejs API jest oparta na REST i wybranych hipermedialnych i my [JSON-LD](http://json-ld.org) jako naszych format zasobów.

W bitach NuGet 3.0 w wersji zapoznawczej zobacz temat nowe źródło pakietów o nazwie "preview.nuget.org" w menu rozwijanym źródła pakietu. W przypadku wybrania tego źródła pakietu, użyjemy naszego nowy interfejs API zamiast do nawiązania połączenia nuget.org. Wprowadziliśmy źródła podglądu dostępne w interfejsie użytkownika podczas możemy kontynuować testowanie, popraw i zwiększyć nowy interfejs API. W wersji NuGet 3.0 RC to nowe źródło pakietów na podstawie v3 interfejsu API spowoduje zastąpienie źródła pakietu na podstawie v2 "nuget.org".

Pomimo inwestycji, które firma Microsoft jest wprowadzenie do interfejsu API w wersji 3 wprowadziliśmy wszystkie te nowe funkcje również współpracować z naszych istniejącego interfejsu API w wersji 2 protokołu, co oznacza, że będą one działać z istniejącymi źródłami pakietu niż nuget.org również.

## <a name="new-features-coming"></a>Nowe funkcje dostępne

Od chwili 3.0 RTM również pracujemy nad niektórych podstawowych nowych NuGet funkcji, poza informacje wyświetlane w interfejsie użytkownika. Poniżej przedstawiono krótką listę obszarów inwestycji istotne:

1. Firma Microsoft jest partnerstwo z programem Visual Studio i zespoły MSBuild, aby uzyskać [NuGet zapoznanie się z platformy](http://blog.nuget.org/20141014/in-the-platform.html).
1. Pracujemy nad abandon konwencje czas instalacji pakietu i zamiast tego stosuje się te konwencje w czasie tworzenia pakietów przez wprowadzenie nowego "autorytatywne" [manifestu pakietu](http://blog.nuget.org/20141023/package-manifests.html).
1. Pracujemy nad zrefaktoryzuj NuGet codebase dokonanie składniki klienta i serwera może być ponownie używane w różnych domenach poza pakietu zarządzania w programie Visual Studio.
1. Analizowania pojęcie "zależności prywatnej" gdzie pakietu może wskazać, że ma zależności od innych pakietów dla tylko szczegóły implementacji i tych zależności nie powinny być udostępniane jako zależności najwyższego poziomu.

## <a name="stay-tuned"></a>Wkrótce

Można śledzić na [naszym blogu](http://blog.nuget.org) więcej i powiadomień dla NuGet 3.0!