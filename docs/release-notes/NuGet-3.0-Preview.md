---
title: Informacje o wersji programu NuGet 3.0 (wersja zapoznawcza)
description: Informacje o wersji programu NuGet 3.0 (wersja zapoznawcza) obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546468"
---
# <a name="nuget-30-preview-release-notes"></a>Informacje o wersji programu NuGet 3.0 (wersja zapoznawcza)

[Informacje o wersji RC NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [informacjach o wersji programu NuGet 3.0 w wersji Beta](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 w wersji zapoznawczej został wydany 12 listopada 2014 r. w ramach tej wersji programu Visual Studio 2015 w wersji zapoznawczej. Firma Microsoft opublikowała program NuGet 3.0 w wersji zapoznawczej. Jest to duża zmiana dla nas (chociaż wersja zapoznawcza), i Cieszymy się rozpocząć uzyskiwanie opinii na temat naszych zmian.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

W programie Visual Studio 2015 Preview znajduje się ta NuGet 3.0 w wersji zapoznawczej. Pracujemy nad bój spadnie (wersja zapoznawcza) dla programu Visual Studio 2012 i Visual Studio 2013 bardzo szybko. Wcześniej zaprezentowaliśmy naszym zamiarem [przerwanie aktualizacji dla programu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), i firma Microsoft została wprowadzona trudne decyzji.

## <a name="brand-new-ui"></a>Całkiem nowy interfejs użytkownika

Pierwszą rzeczą, jaką można zauważyć, że temat NuGet 3.0 w wersji zapoznawczej jest naszym zupełnie nowy interfejs użytkownika. Nie jest już modalne okno dialogowe; teraz jest pełna okno dokumentu programu Visual Studio. Dzięki temu można otworzyć w interfejsie użytkownika dla wielu projektów (i/lub rozwiązania) jednocześnie, wydzielić okna na inny monitor, go zadokować, jednak w przypadku, takie jak itp.

![Nowy interfejs użytkownika NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Po przekroczeniu różnic użyteczność ze względu na porzucenie modalne okno dialogowe mamy też wiele nowych funkcji w nowy interfejs użytkownika.

### <a name="version-selection"></a>Wybór wersji

Prawdopodobnie najpopularniejszych funkcji interfejsu użytkownika jest umożliwienie wybór wersji programu instalacji pakietu aktualizacji i update — ta opcja jest teraz dostępna.

![Wybór wersji pakietu](./media/NuGet-3.0-Preview/version-selection.png)

Czy instalowanie lub aktualizowanie pakietu, lista rozwijana wersji pozwala wyświetlić wszystkie wersje dostępne do pakietu, w niektórych wersjach istotne przeniesiony na górę listy wyboru łatwe. Nie potrzebujesz już pobieranie określonych wersji, które nie są najnowsze informacje przy użyciu konsoli programu PowerShell.

### <a name="combined-installedonlineupdates-workflows"></a>Połączone zainstalowane na stałe/Online/aktualizacje przepływów pracy

Nasze poprzednie interfejsu użytkownika miał 3 karty z zainstalowanym w trybie Online, i aktualizacjach. Pakiety wymienione są specyficzne dla tych przepływów pracy i dostępne akcje zostały określone dla przepływów pracy oraz. Gdy który sprawiał logiczne, a informowało NAS, że wiele osób będzie często uzyskać samoczynnie przy tym rozdzielenie.

W efekcie powstał połączone środowisko, w którym można zainstalować, zaktualizować lub odinstalować pakiet niezależnie od tego, jak masz pakietu wybranego. Aby ułatwić określonych przepływów pracy, mamy listę rozwijaną filtru, która pozwala filtrować te pakiety, które są widoczne, ale następnie Akcje dostępne dla pakietu są spójne.

![Odinstaluj pakiet](./media/NuGet-3.0-Preview/uninstall-package.png)

Za pomocą filtru "Zainstalowano", możesz łatwo sprawdzić, zainstalowane pakiety, które są dostępne aktualizacje, a następnie można odinstalować lub zaktualizować pakiet przez zmianę wersji, aby zobaczyć zmiany dostępnych akcji.

![Aktualizacja pakietu](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Wersja konsolidacji

Jest to często mają ten sam pakiet zainstalowane w wielu projektów w rozwiązaniu. Czasami wersje zainstalowane w każdym projekcie można odstępstw od siebie i jest skonsolidować używanych wersji. NuGet 3.0 w wersji zapoznawczej wprowadzono nową funkcję właśnie w tym scenariuszu.

Okno Zarządzanie poziomie rozwiązania pakietu jest możliwy przez kliknięcie prawym przyciskiem myszy rozwiązanie i wybierając pozycję Zarządzaj pakietami NuGet dla rozwiązania. W tym miejscu po wybraniu pakietu, który jest zainstalowany w wielu projektach, lecz z różnymi wersjami w użyciu, nowa akcja "Konsolidacja" staje się dostępna. W poniższym, zrzucie ekranu `Newtonsoft.Json` został zainstalowany w `SamplesClassLibrary` wersją `6.0.4` i zainstalowane w `SamplesConsoleApp` wersją `5.0.4`.

![Konsolidacja wersji](./media/NuGet-3.0-Preview/consolidate.png)

Poniżej przedstawiono przepływ pracy do konsolidacji na tylko jedną jego wersję.

1. Wybierz `Newtonsoft.Json` pakietu na liście
1. Wybierz `Consolidate` z `Action` listy rozwijanej
1. Użyj `Version` listy rozwijanej wybierz wersję, aby być konsolidowane
1. Zaznacz pola wyboru dla projektów, które powinny być konsolidowane w tej wersji (należy pamiętać, że projekty znajdujące się na wybranej wersji będą wyszarzone)
1. Kliknij przycisk `Consolidate` przycisk, aby przeprowadzić konsolidację

### <a name="operation-previews"></a>Wersje zapoznawcze operacji

Niezależnie od operacji, które wykonujesz — instalowanie/aktualizacji/odinstalowywanie — nowy interfejs użytkownika oferuje sposób nad wersją zapoznawczą zmiany wprowadzone do projektu. Ta wersja zapoznawcza zostaną wyświetlone wszystkie nowe pakiety, które zostaną zainstalowane, pakiety, które zostanie zaktualizowana i pakiety, które zostaną odinstalowane wraz z pakietów, które nie zmieni się podczas operacji.

W poniższym przykładzie widać, że instalowanie Microsoft.AspNet.SignalR spowoduje sporo zmiany do projektu.

![Instalowanie SignalR w wersji zapoznawczej](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opcje instalacji

Za pomocą konsoli programu PowerShell przeznaczono kontrolę nad kilka opcji instalacji istotne. Teraz teraz dostępna w interfejsie użytkownika również te funkcje. Teraz można kontrolować, jak są wybrane wersje zależności zachowanie rozpoznawania zależności.

![Zachowanie zależności](./media/NuGet-3.0-Preview/dependency-behavior.png)

Można również określić akcję do wykonania, gdy pliki zawartości z pakietów w konflikcie z plikami już w projekcie.

![Akcja konflikt pliku](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Nieskończona przewijania

Użyliśmy dość nieco uzyskiwanie opinii na temat naszego interfejsu użytkownika o obu przewijania i stronicowanie paradygmatów podczas wyświetlania listy pakietów. Było dość często mają do przewiń w dół krótką listę, kliknij przycisk Dalej numer strony, a następnie przewiń ponownie. Dzięki nowemu interfejsowi użytkownika wprowadziliśmy nieskończonej przewijanie na liście pakietów, tak że tylko konieczne przewinięcie widoku — nie ma więcej stronicowania.

![Nieskończona przewijania](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Ułatwiają pracę, ułatwiają szybkie, dzięki którym Pretty

Cieszymy się, można uzyskać ten nowy interfejs użytkownika umożliwiający wypróbowanie. Podczas tego punktu kontrolnego w wersji zapoznawczej, jesteśmy następujące dobre powiedzeniem starego elementu "stał się praca, ułatwiają szybkie, ułatwiają całkiem." W tej wersji zapoznawczej, możemy osiągnąć większość pierwszy celu — działa. Wiemy, nie jest dość szybko jeszcze i wiemy, że nie jest dość dość jeszcze. Ufać, że mamy nad tym pracować te cele między już teraz i w wersji RC. W międzyczasie, dlatego chcielibyśmy poznać Twoją opinię o *użyteczność* nowy interfejs użytkownika — przepływy pracy, operacje i w jaki sposób jej *czuje* korzystać z nowego interfejsu użytkownika.

Istnieje kilka funkcji, które usunięto w porównaniu do starego interfejsu użytkownika. Jeden z nich było to zamierzone, a druga po prostu nie udało się wykonać w czasie.

#### <a name="searching-all-package-sources"></a>Trwa wyszukiwanie źródła pakietów "All"

Stary interfejs użytkownika mogą możesz przeprowadzić wyszukiwanie pakietów przed wszystkie źródła pakietu. Usunęliśmy tę funkcję w interfejsie użytkownika, a firma Microsoft nie będą przynosili go ponownie. Ta funkcja używana do wykonywania operacji wyszukiwania względem wszystkich swoich źródeł pakietów mediów ze sobą wyniki i spróbuj kolejność wyników na podstawie wybranych sortowania.

Znaleziono, że trafności wyszukiwania jest bardzo trudne do mediów ze sobą. Można Wyobraź sobie przeprowadzania wyszukiwania względem serwis Google czy Bing i tkania wyniki ze sobą? Ponadto ta funkcja była powoli, można łatwo *przypadkowo* użycia, a firma Microsoft uważa, rzadko było to naprawdę przydatne. Ze względu na problemy wprowadzonej, Odebrano wiele raportów usterek na nim, które nigdy nie może zostać naprawione.

#### <a name="update-all"></a>Aktualizuj wszystkie

Użyliśmy mają przycisk "Aktualizuj wszystkie" w stary interfejs użytkownika, który nie jest dostępne w nowy interfejs użytkownika jeszcze. Firma Microsoft będzie operacji przywracania aktywności tej funkcji dla wersji RC.

## <a name="new-clientserver-api"></a>Nowy klient/serwer interfejsu API

Oprócz wszystkich nowych funkcji w naszej nowej zarządzania pakietami interfejsu użytkownika możemy również pracowano niektórych szczegółów implementacji protokołu klient/serwer NuGet. Dotychczasowej pracy jest utworzenie "Wersji 3 interfejsu API" dla pakietów NuGet zaprojektowany pod kątem wysokiej dostępności dla scenariuszy o kluczowym znaczeniu, takich jak Przywracanie pakietu i instalowania pakietów. Nowy interfejs API jest oparta na REST i wybranych hipermedialnych, a my [JSON-LD](http://json-ld.org) naszych wartość w formacie zasobów.

W bitach NuGet 3.0 w wersji zapoznawczej zobaczysz nowe źródło pakietu o nazwie "preview.nuget.org" w menu rozwijanym źródła pakietu. Wybranie tego źródła pakietów, użyjemy naszego nowego interfejsu API zamiast połączyć się z repozytorium nuget.org. Wprowadziliśmy źródła (wersja zapoznawcza) dostępnych w interfejsie użytkownika podczas gdy my będziemy do testowania, poprawiania i poprawić nowego interfejsu API. W programie NuGet 3.0 RC to nowe źródło pakiet w wersji 3 interfejsu API spowoduje zastąpienie źródła pakietu na podstawie v2 "nuget.org".

Pomimo inwestycji, w których firma Microsoft jest umieszczenie w wersji 3 interfejsu API które wprowadziliśmy wszystkich tych nowych funkcjach również działać z naszych istniejącego interfejsu API w wersji 2 protokołu, co oznacza, że będą one działać z istniejących źródeł pakietów innych niż również adres nuget.org.

## <a name="new-features-coming"></a>Nowe funkcje dostępne

Od chwili 3.0 RTM również pracujemy nad podstawowych nowe NuGet funkcje poza to, co widać w interfejsie użytkownika. Poniżej przedstawiono krótką listę inwestycji najważniejsze obszary:

1. Nawiązaliśmy partnerstwo firmą za pomocą programu Visual Studio i MSBuild zespoły, aby uzyskać [NuGet większe zagłębienie w platformie](http://blog.nuget.org/20141014/in-the-platform.html).
1. Pracujemy nad abandon konwencje czas instalacji pakietu i zamiast tego zastosować te konwencje w czasie tworzenia pakietów, wprowadzając nową "autorytatywne" [manifest pakietu](http://blog.nuget.org/20141023/package-manifests.html).
1. Pracujemy nad zrefaktoryzuj NuGet codebase się składniki klienta i serwera wielokrotnego użytku w różnych domenach poza zarządzania pakietami w programie Visual Studio.
1. Badamy pojęcie "zależności prywatnej" gdzie pakietu można wskazać, że ma zależności od innych pakietów dla tylko szczegóły dotyczące implementacji i te zależności nie powinny być udostępniane jako zależności najwyższego poziomu.

## <a name="stay-tuned"></a>Obserwuj na bieżąco

Można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonsów dla pakietów NuGet 3.0!