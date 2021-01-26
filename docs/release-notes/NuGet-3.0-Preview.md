---
title: Informacje o wersji narzędzia NuGet 3,0 Preview
description: Informacje o wersji programu NuGet 3,0 w wersji zapoznawczej, takie jak znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780327"
---
# <a name="nuget-30-preview-release-notes"></a>Informacje o wersji narzędzia NuGet 3,0 Preview

Informacje o wersji narzędzia [NuGet 2,9 RC](../release-notes/nuget-2.9-rc.md)  |  [Informacje o wersji programu NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)

Pakiet NuGet 3,0 Preview został opublikowany 12 listopada 2014 w ramach wersji zapoznawczej programu Visual Studio 2015. Opublikowano pakiet NuGet 3,0 w wersji zapoznawczej. Jest to Wielka wersja dla nas (choć w wersji zapoznawczej) i przyjemnością zacząć otrzymywać informacje o zmianach.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Ten program NuGet 3,0 Preview znajduje się w wersji zapoznawczej programu Visual Studio 2015. Pracujemy nad rozpoczęciem korzystania z wersji zapoznawczej dla programu Visual Studio 2012 i Visual Studio 2013 bardzo szybko. Firma Microsoft udostępniła poprzednio zamiar w celu [zaniechania aktualizacji programu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)i wybraliśmy tę trudną decyzję.

## <a name="brand-new-ui"></a>Zupełnie nowy interfejs użytkownika

Najpierw należy zauważyć, że pakiet NuGet 3,0 w wersji zapoznawczej to nasz nowy interfejs użytkownika. To nie jest już modalne okno dialogowe; jest to teraz pełne okno dokumentu programu Visual Studio. Pozwala to na jednoczesne otwarcie interfejsu użytkownika dla wielu projektów (i/lub rozwiązania), a następnie przekazanie okna do innego monitora.

![Nowy interfejs użytkownika narzędzia NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Poza różnicami użyteczności z powodu porzucenia modalnych okien dialogowych w nowym interfejsie użytkownika dostępne są również wiele nowych funkcji.

### <a name="version-selection"></a>Wybór wersji

Prawdopodobnie najbardziej żądaną funkcją interfejsu użytkownika jest umożliwienie wyboru wersji na potrzeby instalacji i aktualizacji pakietu. jest ona teraz dostępna.

![Wybór wersji pakietu](./media/NuGet-3.0-Preview/version-selection.png)

Niezależnie od tego, czy instalujesz, czy aktualizujesz pakiet, lista rozwijana wersji umożliwia wyświetlenie wszystkich wersji dostępnych dla pakietu, z niektórymi istotnymi wersjami wyróżnionymi na początku listy. Nie trzeba już używać konsoli programu PowerShell do uzyskiwania określonych wersji, które nie są najnowsze.

### <a name="combined-installedonlineupdates-workflows"></a>Połączone przepływy pracy z zainstalowanymi/w trybie online/aktualizacjami

Poprzedni interfejs użytkownika ma 3 karty na potrzeby instalacji, online i aktualizacji. Wymienione pakiety są specyficzne dla tych przepływów pracy, a dostępne akcje dotyczyły również przepływów pracy. Chociaż te wartości były logiczne, wiemy, że wiele z nich jest często odbieranych przez tę separację.

Mamy już połączone środowisko, w którym można zainstalować, zaktualizować lub odinstalować pakiet niezależnie od tego, jak został wybrany pakiet. Aby uzyskać pomoc dotyczącą określonych przepływów pracy, mamy teraz listę rozwijaną filtru, która umożliwia filtrowanie widocznych pakietów, ale następnie akcje dostępne dla pakietu są spójne.

![Odinstalowywanie pakietu](./media/NuGet-3.0-Preview/uninstall-package.png)

Za pomocą filtru "zainstalowane" można łatwo zobaczyć zainstalowane pakiety, do których są dostępne aktualizacje, a następnie można odinstalować lub zaktualizować pakiet, zmieniając wybór wersji, aby zobaczyć zmianę dostępnej akcji.

![Aktualizowanie pakietu](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Konsolidacja wersji

Często istnieje możliwość zainstalowania tego samego pakietu w wielu projektach w ramach rozwiązania. Czasami wersje zainstalowane w każdym projekcie mogą oddzielić się od siebie i konieczna jest konsolidacja używanych wersji. W wersji zapoznawczej programu NuGet 3,0 wprowadzono nową funkcję tylko w tym scenariuszu.

Dostęp do okna zarządzania pakietami na poziomie rozwiązania można uzyskać, klikając prawym przyciskiem myszy rozwiązanie i wybierając pozycję Zarządzaj pakietami NuGet dla rozwiązania. W tym miejscu, jeśli wybierzesz pakiet, który jest instalowany w wielu projektach, ale z różnymi wersjami w użyciu, zostanie udostępniona nowa akcja "Konsoliduj". Na poniższym zrzucie ekranu program `Newtonsoft.Json` został zainstalowany w `SamplesClassLibrary` wersji z wersją `6.0.4` i zainstalowany w `SamplesConsoleApp` programie z wersją `5.0.4` .

![Konsolidowanie wersji](./media/NuGet-3.0-Preview/consolidate.png)

Oto przepływ pracy na potrzeby konsolidowania do pojedynczej wersji.

1. Wybierz `Newtonsoft.Json` pakiet z listy
1. Wybierz `Consolidate` z `Action` listy rozwijanej
1. Użyj `Version` listy rozwijanej, aby wybrać wersję do skonsolidowania
1. Zaznacz pola dla projektów, które powinny być skonsolidowane w tej wersji (należy zauważyć, że projekty znajdujące się już w wybranej wersji zostaną wyszarzone)
1. Kliknij `Consolidate` przycisk, aby przeprowadzić konsolidację

### <a name="operation-previews"></a>Podglądy operacji

Niezależnie od tego, która operacja jest wykonywana — Instalowanie/aktualizowanie/Odinstalowywanie — nowy interfejs użytkownika oferuje teraz możliwość wyświetlenia podglądu zmian wprowadzonych w projekcie. W tej wersji zapoznawczej zostaną wyświetlone wszystkie nowe pakiety, które zostaną zainstalowane, pakiety, które zostaną zaktualizowane, oraz pakiety, które zostaną odinstalowane wraz z pakietami, które nie zostaną zmienione podczas operacji.

W poniższym przykładzie możemy zobaczyć, że instalacja elementu Microsoft. AspNet. Signal spowoduje powstanie kilku zmian w projekcie.

![Podgląd instalacji sygnalizującej](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Opcje instalacji

Za pomocą konsoli programu PowerShell masz kontrolę nad kilkoma istotnymi opcjami instalacji. Teraz te funkcje zostały również wprowadzone do interfejsu użytkownika. Teraz można kontrolować zachowanie rozpoznawania zależności w przypadku wybrania wersji zależności.

![Zachowanie zależności](./media/NuGet-3.0-Preview/dependency-behavior.png)

Możesz również określić akcję do wykonania, gdy pliki zawartości z pakietów kolidują z plikami znajdującymi się już w projekcie.

![Akcja konfliktu plików](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Nieskończone przewijanie

Używamy w celu wypróbowania w naszym interfejsie użytkownika informacji o modelu przewijania i stronicowania podczas wyświetlania listy pakietów. Było to bardzo powszechne, aby było możliwe przewinięcie do dołu krótkiej listy, kliknij numer następnej strony, a następnie ponownie przewinięcie. Przy użyciu nowego interfejsu użytkownika wprowadziliśmy nieskończone przewijanie na liście pakietów, aby było wymagane tylko przewinięcie — nie ma więcej stronicowania.

![Nieskończone przewijanie](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Utwórz ją szybko, tak jak całkiem

Przyjemnościąmy, aby uzyskać ten nowy interfejs użytkownika do wypróbowania. W ramach tego punktu kontrolnego wersji zapoznawczej nastąpiło powiedzeniem z dobrymi poprzednimi wersjami ". W tej wersji zapoznawczej przepełnimy większość tego celu — działa. Wiemy, że nie jest jeszcze dość szybko i wiemy, że nie jest jeszcze całkiem całkiem. Ufasz, że będziemy pracować nad tymi celami między teraz a wersją RC. Tymczasem chcielibyśmy poznać Twoją opinię na temat *użyteczności* nowego interfejsu użytkownika — przepływów pracy, operacji i sposobu, w jaki *uważamy* , aby użyć nowego interfejsu użytkownika.

W porównaniu z starym interfejsem użytkownika istnieje kilka funkcji, które zostały usunięte. Jeden z nich był zamierzony, a druga nie została ukończona w czasie.

#### <a name="searching-all-package-sources"></a>Wyszukiwanie źródeł pakietów "All"

Stary interfejs użytkownika umożliwia przeprowadzenie wyszukiwania pakietu dla wszystkich źródeł pakietów. Ta funkcja została usunięta w interfejsie użytkownika i nie zostanie przywrócona. Ta funkcja używana do wykonywania operacji wyszukiwania dla wszystkich źródeł pakietów, splotu wyników i próby uporządkowania wyników w oparciu o wybór sortowania.

Znaleźliśmy, że znaczenie wyszukiwania jest naprawdę trudne do dwukierunkowego łączenia się ze sobą. Czy można wyobrazić wyszukiwanie w usłudze Google i Bing i potkane wyniki razem? Ponadto ta funkcja była niska, łatwa do *przypadkowego* użycia i uważamy, że była rzadko przydatna. Ze względu na to, jakie problemy wprowadzono w ramach tej funkcji, na tej stronie otrzymamy wiele raportów o błędach, które nigdy nie zostały naprawione.

#### <a name="update-all"></a>Aktualizuj wszystkie

W starym interfejsie użytkownika użyto przycisku "Aktualizuj wszystko", który jeszcze nie znajduje się w nowym interfejsie użytkownika. Ta funkcja zostanie przywracania aktywności w wersji RC.

## <a name="new-clientserver-api"></a>Nowy interfejs API klienta/serwera

Oprócz wszystkich nowych funkcji w naszym nowym interfejsie użytkownika zarządzania pakietami wprowadzono również pewne szczegóły implementacji protokołu klient/serwer narzędzia NuGet. Wykonana przez nas czynność polega na utworzeniu interfejsu API v3 dla programu NuGet, który jest przeznaczony dla wysokiej dostępności dla scenariuszy krytycznych, takich jak przywracanie pakietów i instalowanie pakietów. Nowy interfejs API jest oparty na REST i w pozostałej części, a jako nasz format został wybrany [kod JSON-LD](http://json-ld.org) .

W usłudze NuGet 3,0 w wersji zapoznawczej w menu rozwijanym źródła pakietu zostanie wyświetlone nowe źródło pakietu o nazwie "preview.nuget.org". W przypadku wybrania tego źródła pakietów zostanie użyty nasz nowy interfejs API, a nie zostanie nawiązane połączenie z usługą nuget.org. Źródło w wersji zapoznawczej zostało udostępnione w interfejsie użytkownika, podczas gdy będziemy kontynuować testowanie, poprawianie i ulepszanie nowego interfejsu API. W programie NuGet 3,0 RC to nowe źródło pakietów oparte na interfejsie API v3 spowoduje zastąpienie źródła pakietu "nuget.org" opartego na protokole v2.

Pomimo inwestycji dokonywanych w interfejsie API V3 wszystkie te nowe funkcje są również współdziałane z istniejącym protokołem API v2, co oznacza, że będą współpracować z istniejącymi źródłami pakietów innym niż nuget.org.

## <a name="new-features-coming"></a>Nowe funkcje

Od teraz do 3,0 RTM pracujemy również nad niektórymi podstawowymi nowymi funkcjami NuGet, poza tym, co widzisz w interfejsie użytkownika. Poniżej przedstawiono krótką listę obszarów inwestycji najważniejsze:

1. Współpracujemy z zespołami Visual Studio i MSBuild, aby uzyskać lepszy dostęp do [platformy NuGet](http://blog.nuget.org/20141014/in-the-platform.html).
1. Pracujemy nad porzuceniem Konwencji pakietu czasu instalacji. zamiast tego Zastosuj te konwencje w czasie pakowania, wprowadzając nowy "autorytatywny" [manifest pakietu](http://blog.nuget.org/20141023/package-manifests.html).
1. Pracujemy nad refaktoryzacją bazy kodu NuGet, aby składniki klienta i serwera były ponownie używane w różnych domenach poza zarządzaniem pakietami w programie Visual Studio.
1. Badamy koncepcję "zależności prywatnych", gdzie pakiet może wskazywać, że ma zależności od innych pakietów tylko do celów szczegółów implementacji, a te zależności nie powinny być rozłączane jako zależności najwyższego poziomu.

## <a name="stay-tuned"></a>Bądź na bieżąco

Obserwuj [nasz blog](http://blog.nuget.org) , aby uzyskać więcej informacji na temat postępu i anonsów dla programu NuGet 3,0!