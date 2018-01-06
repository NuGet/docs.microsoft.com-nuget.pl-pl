---
title: NuGet 1.0 i 1.1 informacje o wersji | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0e7688f7-09d2-4477-9fdf-0e27f572a4de
description: "Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr 1.1 NuGet."
keywords: NuGet 1.1 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 593848b3e5e063816fbbec8b4d11e6fc789d05cd
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-10-and-11-release-notes"></a>Informacje o wersji NuGet 1.0 i 1.1

[Informacje o wersji 1.2 NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 został wydany 13 stycznia 2011.  NuGet 1.1 wydanej w dniu 12 lutego 2011.

## <a name="overview"></a>Omówienie

Ten dokument zawiera informacje o wersji dla różnych wersji 1.0 NuGet pogrupowane według wersji zapoznawczej głównych.

NuGet obejmuje następujące składniki:

* *NuGet.Tools.vsix* * który składa się z:
  * **Biblioteka pakietu w oknie dialogowym Dodawanie** * okna dialogowego w programie Visual Studio umożliwia przeglądanie i instalowanie pakietów.
  * **Konsola Menedżera pakietów** * konsoli w programie Visual Studio oparte na programie Powershell.
* *Narzędzie wiersza polecenia NuGet* * narzędzie używane do tworzenia (i po pewnym czasie publikowania) pakietów.

Rozszerzenie NuGet narzędzi Visual Studio (*NuGet.Tools.vsix*) wymaga:

* Visual Studio 2010 ani Visual Web Developer 2010 Express.

Narzędzia wiersza polecenia NuGet wymaga:

* .NET framework w wersji 4

## <a name="installation"></a>Instalacja

Aby użyć tego [najnowszej wersji](http://nuget.codeplex.com/releases/view/52018):

* Najpierw należy odinstalować starsze kompilacji. Musisz uruchomić VS jako administrator, aby to zrobić.
* Usuń wszystkie istniejące źródła danych, które masz.
* Dodaj nowe źródło danych wskazujące [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Lista problemów rozwiązanych w tej wersji [można znaleźć tutaj](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Jeden problem został rozwiązany dla wersji RTM od wersji RC.

* [Problem 474: Usuwanie pakietów dotyczy wszystkich projektów w rozwiązaniu](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>W wersji Release Candidate

Poniżej przedstawiono zmiany wprowadzone w tej wersji Release Candidate od CTP 2. Odwiedź stronę śledzenia problemu, aby zapoznać się z pełną listą błędów.

* [Aktualizowanie pakietu z konsoli nie aktualizuje zależności.](http://nuget.codeplex.com/workitem/443)
* [Dodawanie pakietu przejmuje bin pakietu nie odwołania (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualizowanie pakietu pozostawia przerwanymi odwołaniami](http://nuget.codeplex.com/workitem/440)
* [Get-Package-aktualizacji nie powiedzie się, w oknie dialogowym lub po wybraniu źródła "Wszystkie" agregowania w konsoli programu](http://nuget.codeplex.com/workitem/439)
* [Występują błędy weryfikacji pakietu](http://nuget.codeplex.com/workitem/426)
* [Ostrzega użytkowników, gdy nie można zainstalować pakietu, w oknie dialogowym Dodawanie pakietu](http://nuget.codeplex.com/workitem/425)
* [Get-Package-aktualizuje zgłasza podczas aktualizowania wielu pakietów](http://nuget.codeplex.com/workitem/424)
* [Poprawy obsługi błędu, gdy plików nuspec są autoryzowane](http://nuget.codeplex.com/workitem/423)
* [Pakiet Nuget ignoruje określone pliki](http://nuget.codeplex.com/workitem/422)
* [Usunięcie źródła pakietu na sekundę do ostatniego, a następnie klikając pozycję "Przenieś w dół" awarii VS](http://nuget.codeplex.com/workitem/418)
* [Usuń odwołanie do zestawu podczas instalowania pakietów](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException podczas otwierania okna dialogowego Ustawienia](http://nuget.codeplex.com/workitem/411)
* [Klucz dostępu do źródła pakietu w konsoli Menedżera pakietów nie działa](http://nuget.codeplex.com/workitem/410)
* [Klawisze dostępu okna dialogowego Ustawienia NuGet VS fokus niewłaściwych pól](http://nuget.codeplex.com/workitem/409)
* [Intellisense identyfikator pakietu nie należy zbadać za dużo elementów](http://nuget.codeplex.com/workitem/404)
* [Błąd podczas dodawania pakietów do projektu z znak kropki w nazwie projektu](http://nuget.codeplex.com/workitem/403)
* [Problem z określonych plików w nuspec](http://nuget.codeplex.com/workitem/400)
* [Poprawne oficjalnego źródła danych należy zarejestrować używając nowszej kompilacji](http://nuget.codeplex.com/workitem/399)
* [Tagi należy używać spacji zamiast #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata brakuje niektórych przydatnych informacji](http://nuget.codeplex.com/workitem/388)
* [Dodaj łącze do raportu nadużycia do okna dialogowego](http://nuget.codeplex.com/workitem/386)
* [Rozpakuj podziały pakietów w programie Visual Studio za pomocą App_Data](http://nuget.codeplex.com/workitem/380)
* [Implementuje tagów](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder umożliwia pusty pakietu bez zależności do utworzenia](http://nuget.codeplex.com/workitem/373)
* [Dodaj pole właścicieli pakietu](http://nuget.codeplex.com/workitem/365)
* [Zaktualizuj manifest VSIX musi wypowiedzieć Menedżera pakietów NuGet, a nie narzędzia VSIX](http://nuget.codeplex.com/workitem/364)
* [Polecenie Get-Package zgłasza błąd, po wybraniu wszystkich źródła](http://nuget.codeplex.com/workitem/359)
* [Kolejność źródeł pakietów w oknie dialogowym Opcje](http://nuget.codeplex.com/workitem/356)
* [Pakiet aktualizacji nie powoduje usunięcia starszych wersji](http://nuget.codeplex.com/workitem/352)
* [Określenie zakresu wersji wdrożenie zależności](http://nuget.codeplex.com/workitem/347)
* [Visual Studio ulega awarii po kliknięciu przycisku "Dodaj nowy pakiet"](http://nuget.codeplex.com/workitem/346)
* [Wyświetl pliki do pobrania i klasyfikacje w oknie dialogowym Dodaj pakietu](http://nuget.codeplex.com/workitem/345)
* [Zmiana między źródła pakietów w oknie dialogowym nie powoduje aktualizacji active źródła](http://nuget.codeplex.com/workitem/344)
* [Usuń powiązania klucza dla okna konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/339)
* [Pakiet instalacyjny nie został rozpoznany jako nazwa polecenia cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Instalowanie pakietu z lokalnego źródła danych zależności na regularne źródła danych nie są rozpoznawane.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies ma pomijać zależności, które są używane](http://nuget.codeplex.com/workitem/331)
* [Jeśli anulowanie nawigacji strony, użytkownik nie może przejść do innej strony podczas zwraca oryginalne żądanie strony](http://nuget.codeplex.com/workitem/325)
* [Sprawdź wydajność NuPack.Server dla obsługę źródeł danych z dużej liczby pakietów.](http://nuget.codeplex.com/workitem/324)
* [Drugim razem, gdy filtrować pakietu go używa źródła pakietu "Nowy", zamiast wcześniej wybranego źródła.](http://nuget.codeplex.com/workitem/321)
* [Po wybraniu karty "Online" w oknie dialogowym należy wybrać domyślne źródła pakietu.](http://nuget.codeplex.com/workitem/320)
* [Pakiet listy zainstalowanych pakietów powinny być widoczne domyślnie](http://nuget.codeplex.com/workitem/309)
* [HintPaths odwołanie do zestawu](http://nuget.codeplex.com/workitem/294)
* [Wyjątek podczas otwierania konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/268)
* [Intellisense konsoli pobiera całego źródła danych](http://nuget.codeplex.com/workitem/259)
* [Źródło pakietów "Default" powinien można zmienić nazwy na "Aktywny"](http://nuget.codeplex.com/workitem/258)
* [Pakiet źródła interfejsu użytkownika: naciśnięcie przycisku OK należy dodać nowego źródła, w przypadku pola Nazwa/źródłowe niepustym](http://nuget.codeplex.com/workitem/257)
* [Okno dialogowe staje się bardzo wolno, gdy jest duża liczba zainstalowanych pakietów](http://nuget.codeplex.com/workitem/243)
* [Obsługuje przekierowania powiązania dla silne nazwanych zestawów](http://nuget.codeplex.com/workitem/238)
* [Dodaj odwołanie do pakietu... Interfejs użytkownika, aby objąć listy rozwijanej źródła pakietu](http://nuget.codeplex.com/workitem/226)
* [NuPack musi obsługiwać przekształcenie konfiguracji agnostically o tej nazwie pliku konfiguracji](http://nuget.codeplex.com/workitem/224)
* [Umożliwia nieistniejący zostać zastąpiona w NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Działanie rezerwowe źródła pakietu](http://nuget.codeplex.com/workitem/204)
* [Awarii na graficznego interfejsu użytkownika](http://nuget.codeplex.com/workitem/201)
* [Dodaj sortowanie opcji, aby dodać okna dialogowego pakietu](http://nuget.codeplex.com/workitem/179)
* [klawisz skrótu, aby wyczyścić konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/174)
* [Konsoli PowerConsole powoduje, że Konsola NuPack się niepowodzeniem](http://nuget.codeplex.com/workitem/166)
* [Konsoli i dodać okna dialogowego pakietu w należy określić agenta użytkownika żądania](http://nuget.codeplex.com/workitem/141)
* [Ustaw numer wersji VSIX i NuPack.exe w kompilacji.](http://nuget.codeplex.com/workitem/134)
* [Ukryj typowe parametry programu PowerShell z-?](http://nuget.codeplex.com/workitem/118)
* [Dodaj - szczegółową pomoc dla poleceń konsoli](http://nuget.codeplex.com/workitem/110)
* [Dodaj pakiet okna dialogowego powinna zezwalać na wybór bieżącego źródła pakietów](http://nuget.codeplex.com/workitem/88)
* [Przenieś klasy NuPack.Core w różnych przestrzeniach nazw](http://nuget.codeplex.com/workitem/50)
* [Dodawanie pomocy do poleceń cmdlet](http://nuget.codeplex.com/workitem/23)
* [Sprawdź skrót ze strumieniowego źródła po pobraniu pakietu](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Najbardziej znaczących zmian wprowadzonych w wersji CTP 2 są następujące:

* Przełączono pakietu źródła danych z ATOM punkt końcowy usługi OData: po uaktualnieniu do wersji CTP2 programu NuGet, należy dodać następujący adres URL jako źródło pakietów: [http://go.microsoft.com/fwlink/?LinkID=204820](http://go.microsoft.com/fwlink/?LinkID=204820).
* Zmieniona polecenie Add-Package *Install-Package*.
* Zaktualizowano `.nuspec` Format. `.nuspec` Zawiera teraz format *iconUrl* pole służący do określania 32 x 32 ikona png, które będzie widoczne w oknie dialogowym Dodaj pakiet. Dlatego należy ustawić go do odróżnienia pakietu. `.nuspec` Format zawiera również nowe *adresem projectUrl* pola, które służy do punktu do strony sieci web, która zapewnia więcej informacji na temat pakietu.

Ta kompilacja nie będzie działać ze starą `.nupkg` plików. Jeśli otrzymasz wyjątki odwołanie o wartości null, używasz starego `.nupkg` pliku, a następnie trzeba ponownie go za pomocą zaktualizowanego [narzędzia wiersza polecenia NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Poniżej znajduje się lista funkcji i usterki, które zostały usunięte NuGet CTP 2 (nie ma błędów dla kodu pomocnicza czyszczenia itp.).

* [Błąd Rozpakowywanie zestawy pakietu podczas określenie TargetFramework dla zestawu.](http://nuget.codeplex.com/workitem/10)
* [Tworzenie okna konsoli NuPack mogą szybciej odnajdywać](http://nuget.codeplex.com/workitem/14)
* [ILMerge wersji nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Lepsze błąd/wyjątków](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager bezpiecznie powinna obsługiwać błędy związane z źródła danych](http://nuget.codeplex.com/workitem/28)
* [Potrzebne nową ikonę w konsoli programu](http://nuget.codeplex.com/workitem/29)
* [Localize — ciągi w oknie dialogowym](http://nuget.codeplex.com/workitem/38)
* [Pamięci podręczne NuPack pobranych plików .nupack w pamięci](http://nuget.codeplex.com/workitem/40)
* [Konsola NuPack: Zmienić domyślne skrót do wyświetlania konsoli](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem powinien obsługuje przekazywania wartości domyślnych dla wspólnych właściwości](http://nuget.codeplex.com/workitem/49)
* [Uruchamianie nupack.exe w folderze z tylko jednego pliku nuspec należy używać tego nuspec](http://nuget.codeplex.com/workitem/52)
* [Menu projektu zostaną wyświetlone nawet po załadowaniu projektu/rozwiązania](http://nuget.codeplex.com/workitem/54)
* [Build.cmd zakończy się niepowodzeniem na czystą klonu bazy kodu](http://nuget.codeplex.com/workitem/56)
* [Funkcja dostępne aktualizacje](http://nuget.codeplex.com/workitem/57)
* [Okno dialogowe: Dodawanie pakietu za pomocą okna dialogowego usuwa monitu w konsoli programu](http://nuget.codeplex.com/workitem/73)
* [Dodawanie pakietu przez kliknięcie przycisku "Zainstaluj" często jest powolne, bez visual opinii](http://nuget.codeplex.com/workitem/80)
* [Nie istnieje sposób odnajdywania, który Moje zainstalowane pakiety są aktualizacje.](http://nuget.codeplex.com/workitem/82)
* [Brak nie można zaktualizować zainstalowanego pakietu w oknie dialogowym.](http://nuget.codeplex.com/workitem/83)
* [Nie istnieje sposób odinstalowania zainstalowanego pakietu w oknie dialogowym](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Dodaj odwołanie do pakietu&hellip; &rdquo; jest wyświetlana w menu kontekstowym zainstalowanych odwołań](http://nuget.codeplex.com/workitem/85)
* [Po zaktualizowaniu pakietu w konsoli, zawiera zarówno starą wersję, jak i nowa wersja zainstalowany](http://nuget.codeplex.com/workitem/86)
* [Działania w konsoli, korzystając z okna dialogowego zniknie po użyciu](http://nuget.codeplex.com/workitem/87)
* [Wiersz polecenia czyszczenia analizowania nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Opcjonalną z przyjazną nazwą źródła pakietu](http://nuget.codeplex.com/workitem/98)
* [Aktualizacja .nuspec do obsługi tym ikony pakietu](http://nuget.codeplex.com/workitem/103)
* [Źródła interfejsu użytkownika nie zezwala na kopiowanie adresu URL](http://nuget.codeplex.com/workitem/105)
* [Lepszą obsługę błędów remove-package.](http://nuget.codeplex.com/workitem/107)
* [Wpisz w oknie konsoli zależy od fokus kursora](http://nuget.codeplex.com/workitem/112)
* [Komunikaty o błędach Szukaj awful](http://nuget.codeplex.com/workitem/116)
* [Wydajność Usuń pakietu dla pakietu, który nie jest zainstalowany jest nieodpowiedni](http://nuget.codeplex.com/workitem/117)
* [Usunięcie pakietu nie powiedzie się, gdy brak źródeł pakietu](http://nuget.codeplex.com/workitem/119)
* [Usuwanie pakietu nie powiedzie się, gdy źródła pakietu jest niedostępny](http://nuget.codeplex.com/workitem/120)
* [Dodaj tytuł metadane pakietów i źródła danych.](http://nuget.codeplex.com/workitem/125)
* [Dodaj parametr - źródła, Dodaj pakiet do](http://nuget.codeplex.com/workitem/127)
* [Pakiet listy powinien mieć parametr - źródła](http://nuget.codeplex.com/workitem/128)
* [NuPack.Server aktualizacji, aby wymagać NuPack użytkownika do pobrania pakiet agenta](http://nuget.codeplex.com/workitem/142)
* [Okno dialogowe akceptacji licencji musi zawierać licencji dla wszystkich zależności, które wymagają akceptacji](http://nuget.codeplex.com/workitem/145)
* [Błąd logowania, gdy pakiet zgłasza wyjątek w źródle danych](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe nie należy zezwalać pustą &lt;licenseurl&gt; — element](http://nuget.codeplex.com/workitem/152)
* [Zmień nazwę listy pakietu na Get pakiet, Dodaj do pakietu instalacji i usuwania pakietu można odinstalować pakietu](http://nuget.codeplex.com/workitem/155)
* [Przy użyciu elementu menu Dodaj odwołanie do pakietu z Nawigatora rozwiązania awarii programu Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Etykieta "pakiet dostępne źródła" Brak dwukropka](http://nuget.codeplex.com/workitem/160)
* [Wprowadź .nuspec xml elementu wielkości liter spójnie mieszanej wielkości liter](http://nuget.codeplex.com/workitem/161)
* [Manifest NuPack VSIX należy włączyć bit "admin"](http://nuget.codeplex.com/workitem/162)
* [Po uruchomieniu pakietu listy z nie źródeł danych, otrzymasz błąd ref wartości null](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: Określ ścieżkę docelową](http://nuget.codeplex.com/workitem/171)
* [Błędy środowiska PowerShell otwarcie konsoli zarządzania pakietów na Windows XP](http://nuget.codeplex.com/workitem/175)
* [VS awarii podczas próby załadowania listy pakietów](http://nuget.codeplex.com/workitem/176)
* [Zezwalaj na meta pakietów (nie plików, tylko zależności)](http://nuget.codeplex.com/workitem/180)
* [Konwertuj skrypt programu Powershell do modułu środowiska Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver należy odrzucić ścieżki części poprzedzających symboli wieloznacznych, gdy określono docelowego](http://nuget.codeplex.com/workitem/183)
* [Brak zależności](http://nuget.codeplex.com/workitem/186)
* [Błąd podczas instalowania Elmah](http://nuget.codeplex.com/workitem/192)
* [Transformacje konfiguracji nie działa prawidłowo z &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Zmienna "$globalne: projectCache" nie można pobrać, ponieważ nie została ustawiona](http://nuget.codeplex.com/workitem/203)
* [Dodaj zadanie programu MSBuild do tworzenia pakietów NuPack](http://nuget.codeplex.com/workitem/205)
* [Pakiet listy musi obsługiwać wyszukiwanie filtrowania](http://nuget.codeplex.com/workitem/206)
* [Zawsze wyświetlaj łącze do licencji, jeśli autora pakietu zawiera adresu URL licencji](http://nuget.codeplex.com/workitem/208)
* [Okazjonalne wyjątek "Odmowa dostępu" Remove-pakietu](http://nuget.codeplex.com/workitem/213)
* [Testy jednostkowe kończy się niepowodzeniem: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Umożliwić powrotu lub domyślnego zestawu plików, jeśli nie można odnaleźć przeznaczonych dla określonej wersji struktury](http://nuget.codeplex.com/workitem/223)
* [Dodaj odwołanie do pakietu... Interfejs użytkownika nie można usunąć pakietu](http://nuget.codeplex.com/workitem/225)
* [Dodaj odwołanie do pakietu awarii studio, gdy dla jednego lub więcej projektów jest zwolniony](http://nuget.codeplex.com/workitem/228)
* [Nie ma przekształcenie konfiguracji do pracy w pliku web.debug.config](http://nuget.codeplex.com/workitem/229)
* [init.ps1 nie uruchomiono na pakiecie niestandardowym](http://nuget.codeplex.com/workitem/237)
* [Podczas dodawania ścieżki do feedlist, przycisk domyślny jest ustawiona na OK, więc jeśli I naciśnij klawisz ENTER automatycznie zamyka](http://nuget.codeplex.com/workitem/240)
* [Aby odinstalować zależność ulegnie awarii programu VS, jeśli próba 2 razy pod rząd](http://nuget.codeplex.com/workitem/241)
* [Wyświetlany adres URL projektu w oknie dialogowym Dodawanie pakietu](http://nuget.codeplex.com/workitem/253)
* [Domyślnie okno dialogowe Dodaj pakiet, aby zainstalować pakiety](http://nuget.codeplex.com/workitem/254)
* [Zmień element menu Dodaj okna dialogowego pakietu.](http://nuget.codeplex.com/workitem/261)
* [Zmień nazwę przestrzeni nazw i zestawów](http://nuget.codeplex.com/workitem/274)
* [Zmień nazwę projektu NuPack na NuGet](http://nuget.codeplex.com/workitem/282)
* [Dodaj poniższy tekst na liście zależności](http://nuget.codeplex.com/workitem/288)
* [Zmień tekst akceptacji licencji w oknie dialogowym akceptacji licencji](http://nuget.codeplex.com/workitem/291)
* [Zmiany tekstu w oknie dialogowym akceptacji licencji powyżej listy pakietów](http://nuget.codeplex.com/workitem/292)
* [OData nie działa z adresu URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Interfejs użytkownika Menedżera pakietów: za pośrednictwem aktywnego buforowania liczby pakietów służący do stronicowania](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; błąd Konsola Menedżera pakietów](http://nuget.codeplex.com/workitem/335)
* [Dodaj pakiet okna dialogowego pokazuje licencji akceptacji dla już zainstalowane spakowane](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Poniżej znajduje się lista funkcji i usterki, które zostały usunięte NuGet CTP 1.

* [Rozszerzenie pakietu powinna być zmieniona na .nupack](http://nuget.codeplex.com/workitem/1)
* [Przenieś plik pakietu do folderu](http://nuget.codeplex.com/workitem/2)
* [Scal instalacji &amp; polecenia Dodaj PS](http://nuget.codeplex.com/workitem/3)
* [Tworzenie aliasów czasownik-rzeczownik poleceń cmdlet](http://nuget.codeplex.com/workitem/4)
* [NuPack pobiera pomylić podczas przełączania rozwiązań w programie VS](http://nuget.codeplex.com/workitem/6)
* [Domyślnie powinna ukryty folder "packages" rozwiązania](http://nuget.codeplex.com/workitem/11)
* [Dodaj obsługę zastępujący tokenu w elementach zawartości.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI należy użyć interfejsu API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager oznacza pakietów jako zainstalowany przed zainstalowaniem ich](http://nuget.codeplex.com/workitem/27)
* [Trwa usuwanie projektu domyślnego z rozwiązania wciąż pokazuje usuniętego projektu jako domyślny](http://nuget.codeplex.com/workitem/30)
* [Nowy pakiet nie powiodło się "Nie można dodać części dla określonego identyfikatora URI, ponieważ jest już w pakiecie."](http://nuget.codeplex.com/workitem/32)
* [Usuń parametry "NuPack" z programu Visual Studio graficznego interfejsu użytkownika](http://nuget.codeplex.com/workitem/35)
* [Dodaj plik Apache nagłówka do COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Usuń polecenie Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Nie można użyć podczas ładowania profilu Menedżera pakietów zgłasza wyjątek](http://nuget.codeplex.com/workitem/39)
* [init.ps1 i install.ps1, uninstall.ps1 konieczność odbierania dodatkowe stanu](http://nuget.codeplex.com/workitem/41)
* [Łączenie konsoli i pakietów graficznego interfejsu użytkownika w jednym zestawie](http://nuget.codeplex.com/workitem/42)
* [Logika transformacji XML nie działa, jeśli zastosowano do pliku XML, który nie jest w katalogu głównym](http://nuget.codeplex.com/workitem/43)
* [Źródeł ustawienia okno dialogowe Zarządzanie pakietem nie aktualizowania konsoli NuPack](http://nuget.codeplex.com/workitem/44)
* [Konsola NuPack interfejsu użytkownika: Zmień nazwę listy rozwijanej źródła pakietów do "Źródło pakietów"](http://nuget.codeplex.com/workitem/45)
* [Opcje konsoli NuPack: Zmień nazwę "Repozytorium UI", aby były spójne z konsoli NuPack](http://nuget.codeplex.com/workitem/46)
* [Dodawanie pakietu nie powiedzie się dla witryny sieci Web, która została otwarta z usług IIS lub adres URL](http://nuget.codeplex.com/workitem/53)
* [Źródło Menedżera pakietów nie działa z FwLink](http://nuget.codeplex.com/workitem/55)
* [Ustawienie domyślne źródła pakietu](http://nuget.codeplex.com/workitem/59)
* [Podczas dodawania źródła pakietów w przypadku opcji, gdy jest dostarczany tylko jedno źródło, przyjęto założenie, że jest to wartość domyślna.](http://nuget.codeplex.com/workitem/60)
* [Okno dialogowe interfejsu użytkownika zawiera fałszywych pakiety "najnowsze"](http://nuget.codeplex.com/workitem/62)
* [Opcje: Kliknięcie przycisku Anuluj nie Anuluj zmiany](http://nuget.codeplex.com/workitem/63)
* [Dodaj pakiet odwołanie okno wyszukiwania powinna być bez uwzględniania wielkości liter](http://nuget.codeplex.com/workitem/65)
* [Usuń firmy metadanych w plikach AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numer wersji pliku VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Za pomocą parametru-? Wyświetla Pomoc dwa razy](http://nuget.codeplex.com/workitem/72)
* [Wykonanie instalacji/dezinstalacji pakietów dla projektu poziomu pakietów](http://nuget.codeplex.com/workitem/74)
* [Nie można utworzyć źródła danych, gdy jeden nupack nie powiodło się sprawdzanie poprawności serwera](http://nuget.codeplex.com/workitem/90)
* [Trzeba wymienić NuPack ikony](http://nuget.codeplex.com/workitem/94)
* [Serwer proxy http NTLM nie uwierzytelnia do źródła pakietu.](http://nuget.codeplex.com/workitem/96)
* [Okno dialogowe nie uruchamiać wyśrodkowany w oknie programu VS](http://nuget.codeplex.com/workitem/100)
* [Wiele pól w szczegółach pakiety nie zostały są wypełnione w oknie dialogowym](http://nuget.codeplex.com/workitem/102)
* [Okno dialogowe interfejsu użytkownika nie wyświetla nazwy autorów](http://nuget.codeplex.com/workitem/108)
* [Dlaczego — wersja pakietu Usuń](http://nuget.codeplex.com/workitem/113)
* [Usuń ostatnie karty w oknie dialogowym interfejsu użytkownika](http://nuget.codeplex.com/workitem/115)
* [VS awarii po prawej kliknij folder rozwiązania po otwarciu okna dialogowego interfejsu użytkownika, co najmniej jeden.](http://nuget.codeplex.com/workitem/126)
* [Zmień parametr - Local pakietu listy - zainstalowanego](http://nuget.codeplex.com/workitem/129)
* [Zmień nazwę packages.xml na NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Konsoli wymusza kursora do końca wiersza](http://nuget.codeplex.com/workitem/135)
* [Usuń pakiet intellisense został przerwany](http://nuget.codeplex.com/workitem/136)
* [Dodaj flagę RequireLicenseAcceptance .nuspec i źródła danych](http://nuget.codeplex.com/workitem/137)
* [Dodaj źródła danych LicenseUrl .nuspec i pakietu](http://nuget.codeplex.com/workitem/138)
* [Klikając przycisk Zainstaluj pakietu, który wymaga zatwierdzenia powinny być widoczne akceptacji okna dialogowego](http://nuget.codeplex.com/workitem/139)
* [Dodaj do okna dialogowego pakietu Dodaj tekst klauzuli wyłączenia odpowiedzialności](http://nuget.codeplex.com/workitem/140)
* [Dodaj zastrzeżenie podczas pakietu konsola jest wykonywane po raz pierwszy](http://nuget.codeplex.com/workitem/143)
* [Wyświetl zastrzeżenie po zainstalowaniu pakietu w konsoli programu](http://nuget.codeplex.com/workitem/144)
* [Zmień nazwę rozszerzenia .nupack na .nupkg](http://nuget.codeplex.com/workitem/146)