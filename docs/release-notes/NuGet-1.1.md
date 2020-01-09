---
title: Informacje o wersji pakietu NuGet 1,0 i 1,1
description: Informacje o wersji programu NuGet 1,1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4f90888eae4d039c99d6f6879a06107ec5a31a82
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384700"
---
# <a name="nuget-10-and-11-release-notes"></a>Informacje o wersji pakietu NuGet 1,0 i 1,1

[Informacje o wersji narzędzia NuGet 1,2](../release-notes/nuget-1.2.md)

Pakiet NuGet 1,0 został wydaną 13 stycznia 2011.  Pakiet NuGet 1,1 został wydano 12 lutego 2011.

## <a name="overview"></a>Omówienie

Ten dokument zawiera informacje o wersji dla różnych wersji programu NuGet 1,0 pogrupowanych zgodnie z wersją główną wersji zapoznawczej.

Pakiet NuGet zawiera następujące składniki:

* *NuGet. Tools. vsix* * składający się z:
  * **Okno dialogowe Dodawanie pakietu biblioteki** * okno dialogowe w programie Visual Studio służące do przeglądania i instalowania pakietów.
  * **Konsola Menedżera pakietów** * konsola programu PowerShell w programie Visual Studio.
* *Narzędzie wiersza polecenia NuGet* * używane do tworzenia pakietów (i ostatecznie opublikowanych).

Rozszerzenie narzędzia NuGet Tools programu Visual Studio (*NuGet. Tools. vsix*) wymaga:

* Visual Studio 2010 lub Visual Web Developer 2010 Express.

Narzędzie wiersza polecenia NuGet wymaga:

* .NET Framework w wersji 4

## <a name="installation"></a>Instalacja programu

Aby użyć tej [najnowszej wersji](http://nuget.codeplex.com/releases/view/52018):

* Najpierw odinstaluj starszą kompilację. Aby to zrobić, należy uruchomić programu VS jako administrator.
* Usuń wszystkie istniejące kanały informacyjne.
* Dodaj nowe źródło danych wskazujące na <https://go.microsoft.com/fwlink/?LinkId=206669>.

## <a name="nuget-11"></a>NuGet 1.1

Listę problemów rozwiązanych w tej wersji [można znaleźć tutaj](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>Pakiet NuGet 1,0 RTM

Jeden problem został rozwiązany w wersji RTM od wersji RC.

* [Problem 474: usuwanie pakietów ma wpływ na wszystkie projekty w rozwiązaniu](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Wersja Release Candidate

Poniżej przedstawiono zmiany wprowadzone w tej wersji kandydata od CTP 2. Odwiedź moduł śledzący problemy, aby wyświetlić pełną listę błędów.

* [Aktualizacja pakietu z konsoli nie aktualizuje zależności.](http://nuget.codeplex.com/workitem/443)
* [Dodawanie pakietu pobrania w górę pojemnika nie odwołanie do pakietu (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualizacja pakietu pozostawia przerwane odwołania](http://nuget.codeplex.com/workitem/440)
* [Polecenie Get-Package-Updates nie powiedzie się w oknie dialogowym lub gdy w konsoli jest wybrane źródło zagregowane "wszystkie"](http://nuget.codeplex.com/workitem/439)
* [Pobieranie błędów weryfikacji pakietu](http://nuget.codeplex.com/workitem/426)
* [Ostrzegaj użytkowników, gdy nie można zainstalować pakietu z okna dialogowego Dodawanie pakietu](http://nuget.codeplex.com/workitem/425)
* [Get-Package-Updates zgłaszanych podczas aktualizacji dużej liczby pakietów](http://nuget.codeplex.com/workitem/424)
* [Popraw obsługę błędów, gdy pliki nuspec zostały nieprawidłowo utworzone](http://nuget.codeplex.com/workitem/423)
* [Pakiet NuGet ignoruje określone pliki](http://nuget.codeplex.com/workitem/422)
* [Usuwanie drugiego źródła pakietu, a następnie kliknięcie pozycji "Przenieś w dół" w programie VS](http://nuget.codeplex.com/workitem/418)
* [Usuń odwołanie do zestawu podczas instalowania pakietów](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException podczas otwierania okna dialogowego ustawień](http://nuget.codeplex.com/workitem/411)
* [Klucz dostępu dla źródła pakietu w konsoli Menedżera pakietów nie działa](http://nuget.codeplex.com/workitem/410)
* [Klucze dostępu do okna dialogowego NuGet VS Settings nadają fokus do nieprawidłowych pól](http://nuget.codeplex.com/workitem/409)
* [Funkcja IntelliSense identyfikatora pakietu nie powinna wysyłać zapytań o zbyt wiele elementów](http://nuget.codeplex.com/workitem/404)
* [Nie można dodać pakietu do projektu z kropką w nazwie projektu](http://nuget.codeplex.com/workitem/403)
* [Problem z określonymi plikami w nuspec](http://nuget.codeplex.com/workitem/400)
* [Poprawne oficjalne źródło powinno zostać zarejestrowane przy użyciu nowszej kompilacji](http://nuget.codeplex.com/workitem/399)
* [Tagi powinny używać spacji zamiast #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata Brak pewnych użytecznych informacji](http://nuget.codeplex.com/workitem/388)
* [Dodaj łącze Zgłoś nadużycie do okna dialogowego](http://nuget.codeplex.com/workitem/386)
* [Używanie App_Data do rozpakowania pakietów w programie Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Zaimplementuj Tagi](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder umożliwia pusty pakiet bez zależności, które mają zostać utworzone](http://nuget.codeplex.com/workitem/373)
* [Dodaj pole właścicieli dla pakietu](http://nuget.codeplex.com/workitem/365)
* [Zaktualizuj manifest VSIX, aby powiedzieć Menedżer pakietów NuGet zamiast narzędzi VSIX](http://nuget.codeplex.com/workitem/364)
* [Polecenie Get-Package zgłasza błąd, jeśli wybrano wszystkie źródła](http://nuget.codeplex.com/workitem/359)
* [Zezwalaj na porządkowanie źródeł pakietów w oknie dialogowym opcji](http://nuget.codeplex.com/workitem/356)
* [Update-Package nie usuwa starszej wersji](http://nuget.codeplex.com/workitem/352)
* [Implementowanie specyfikacji zakresu wersji dla zależności](http://nuget.codeplex.com/workitem/347)
* [Program Visual Studio ulega awarii podczas klikania pozycji "Dodaj nowy pakiet"](http://nuget.codeplex.com/workitem/346)
* [Wyświetl pliki do pobrania i klasyfikacje w oknie dialogowym Dodaj pakiet](http://nuget.codeplex.com/workitem/345)
* [Zmiana źródła pakietów w oknie dialogowym nie powoduje aktualizacji aktywnego źródła](http://nuget.codeplex.com/workitem/344)
* [Usuń powiązanie klucza dla okna konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/339)
* [Pakiet instalacyjny nie został rozpoznany jako nazwa polecenia cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Instalowanie pakietu z lokalnego źródła danych nie są rozwiązywane zależności od zwykłych kanałów informacyjnych](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies powinny pomijać zależności, które są nadal używane](http://nuget.codeplex.com/workitem/331)
* [Jeśli anulujesz nawigację strony, użytkownik nie może przejść do innej strony, gdy żądanie oryginalnego strony zwróci wartość](http://nuget.codeplex.com/workitem/325)
* [Zbadaj wydajność NuPack. Server, aby obsługiwać źródła danych z dużą liczbą pakietów.](http://nuget.codeplex.com/workitem/324)
* [Podczas drugiego filtrowania pakietu używa "nowego" źródła pakietu zamiast poprzednio wybranego źródła.](http://nuget.codeplex.com/workitem/321)
* [Domyślne źródło pakietu powinno zostać wybrane podczas wybierania karty "online" w oknie dialogowym.](http://nuget.codeplex.com/workitem/320)
* [Pakiet list powinien domyślnie wyświetlać zainstalowane pakiety](http://nuget.codeplex.com/workitem/309)
* [HintPaths odwołania do zestawu](http://nuget.codeplex.com/workitem/294)
* [Wyjątek podczas otwierania konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/268)
* [Technologia IntelliSense pobiera całe źródło danych](http://nuget.codeplex.com/workitem/259)
* [Nazwa źródła pakietu "default" powinna mieć nazwę "Active"](http://nuget.codeplex.com/workitem/258)
* [Interfejs użytkownika źródeł pakietów: naciśnięcie przycisku OK powinno spowodować dodanie nowego źródła, jeśli nazwa/pola źródłowe nie są puste](http://nuget.codeplex.com/workitem/257)
* [Okno dialogowe działa bardzo wolno, gdy liczba zainstalowanych pakietów jest duża](http://nuget.codeplex.com/workitem/243)
* [Obsługa przekierowań powiązań dla silnych nazwanych zestawów](http://nuget.codeplex.com/workitem/238)
* [Dodaj odwołanie do pakietu... Interfejs użytkownika obejmujący listę rozwijaną dla źródła pakietu](http://nuget.codeplex.com/workitem/226)
* [NuPack musi obsługiwać agnostically w konfiguracji pliku konfiguracji](http://nuget.codeplex.com/workitem/224)
* [Zezwala BasePath na przesłonięta w NuPack. exe](http://nuget.codeplex.com/workitem/222)
* [Zachowanie rezerwowe źródła pakietów](http://nuget.codeplex.com/workitem/204)
* [Awaria w graficznym interfejsie użytkownika](http://nuget.codeplex.com/workitem/201)
* [Dodawanie opcji sortowania do okna dialogowego Dodawanie pakietu](http://nuget.codeplex.com/workitem/179)
* [klawisz skrótu do czyszczenia konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/174)
* [PowerConsole powoduje niepowodzenie konsoli NuPack](http://nuget.codeplex.com/workitem/166)
* [Okno dialogowe konsoli i dodawania pakietu powinno ustawić agenta użytkownika w żądaniach](http://nuget.codeplex.com/workitem/141)
* [Ustaw numer wersji VSIX i NuPack. exe w kompilacji.](http://nuget.codeplex.com/workitem/134)
* [Czy ukryć typowe parametry programu PowerShell z-?](http://nuget.codeplex.com/workitem/118)
* [Dodawanie szczegółowej pomocy dotyczącej poleceń konsoli](http://nuget.codeplex.com/workitem/110)
* [Okno dialogowe Dodawanie pakietu powinno zezwalać na wybór bieżącego źródła pakietu](http://nuget.codeplex.com/workitem/88)
* [Przenieś klasy NuPack. Core do różnych przestrzeni nazw](http://nuget.codeplex.com/workitem/50)
* [Dodaj pomoc do poleceń cmdlet](http://nuget.codeplex.com/workitem/23)
* [Weryfikuj mieszanie z kanału informacyjnego po pobraniu pakietu](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Poniżej przedstawiono najbardziej znaczące zmiany wprowadzone w CTP 2:

* Przełączono kanał informacyjny pakietu z ATOM do punktu końcowego usługi OData: w przypadku uaktualnienia do wersji CTP2 programu NuGet należy dodać następujący adres URL jako źródło pakietu: `https://feed.nuget.org/ctp2/odata/v1/`.
* Zmieniono nazwę polecenia Add-Package na *install-package*.
* Zaktualizowano format `.nuspec`. `.nuspec` format zawiera teraz pole *iconUrl* służące do określania ikony png 32x32, która będzie widoczna w oknie dialogowym Dodaj pakiet. Upewnij się, że ustawisz, aby odróżnić pakiet. `.nuspec` format zawiera również nowe pole *projectUrl* , za pomocą którego można wskazać stronę sieci Web, która zawiera więcej informacji na temat pakietu.

Ta kompilacja nie będzie działała ze starymi plikami `.nupkg`. W przypadku wystąpienia wyjątków odwołania o wartości null używany jest stary plik `.nupkg` i trzeba go ponownie skompilować przy użyciu zaktualizowanego [narzędzia wiersza polecenia NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Poniżej znajduje się lista funkcji i usterek, które zostały naprawione dla programu NuGet CTP 2 (nie obejmują błędów dla niewielkich programów do czyszczenia kodu itp.).

* [Wystąpił błąd podczas rozpakowywania zestawów pakietów, gdy specifiying TargetFramework dla zestawu.](http://nuget.codeplex.com/workitem/10)
* [Zwiększ możliwości odnajdywania okna konsoli NuPack](http://nuget.codeplex.com/workitem/14)
* [ILMerge wersję nupack. exe](http://nuget.codeplex.com/workitem/19)
* [Lepsza obsługa błędów/wyjątków](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core]: Packagemanager powinien bezpiecznie obsłużyć błędy związane z kanałem informacyjnym](http://nuget.codeplex.com/workitem/28)
* [Potrzebna jest nowa ikona dla konsoli](http://nuget.codeplex.com/workitem/29)
* [Lokalizowanie ciągów w oknie dialogowym](http://nuget.codeplex.com/workitem/38)
* [Pamięć podręczna NuPack pobrano pliki. NuPack w pamięci](http://nuget.codeplex.com/workitem/40)
* [Konsola NuPack: zmiana domyślnego skrótu do wyświetlania konsoli](http://nuget.codeplex.com/workitem/48)
* [Współdzielone powinny obsługiwać wartości domyślne dla wspólnych właściwości](http://nuget.codeplex.com/workitem/49)
* [Uruchomienie programu nupack. exe w folderze z tylko jednym plikiem nuspec powinno być używane przez ten nuspec](http://nuget.codeplex.com/workitem/52)
* [Menu Projekt jest wyświetlane nawet wtedy, gdy nie załadowano żadnego projektu/rozwiązania](http://nuget.codeplex.com/workitem/54)
* [Kompilacja. cmd kończy się niepowodzeniem na czystym klonie bazy kodu](http://nuget.codeplex.com/workitem/56)
* [Dostępna funkcja aktualizacji](http://nuget.codeplex.com/workitem/57)
* [Okno dialogowe: Dodawanie pakietu za pomocą okna dialogowego powoduje usunięcie monitu w konsoli programu](http://nuget.codeplex.com/workitem/73)
* [Dodawanie pakietu przez kliknięcie przycisku "Zainstaluj" jest często wolne, bez opinii o wizualizacji](http://nuget.codeplex.com/workitem/80)
* [Nie ma możliwości odnajdowania, które z zainstalowanych pakietów mają aktualizacje.](http://nuget.codeplex.com/workitem/82)
* [Nie ma możliwości aktualizacji zainstalowanego pakietu w oknie dialogowym.](http://nuget.codeplex.com/workitem/83)
* [Nie ma możliwości odinstalowania zainstalowanego pakietu w oknie dialogowym](http://nuget.codeplex.com/workitem/84)
* [&ldquo;dodawania odwołania do pakietu&hellip;&rdquo; pojawia się w menu kontekstowym zainstalowanych odwołań](http://nuget.codeplex.com/workitem/85)
* [Po zaktualizowaniu pakietu z poziomu konsoli programu wyświetlana jest zarówno stara wersja, jak i Nowa wersja zgodnie z zainstalowaną](http://nuget.codeplex.com/workitem/86)
* [Działanie w konsoli programu przy użyciu okna dialogowego znika po użyciu](http://nuget.codeplex.com/workitem/87)
* [Analiza wiersza polecenia oczyszczania w nupack. exe](http://nuget.codeplex.com/workitem/89)
* [Dodawanie przyjaznej nazwy do źródeł pakietów](http://nuget.codeplex.com/workitem/98)
* [Update. nuspec do obsługi, w tym ikon pakietów](http://nuget.codeplex.com/workitem/103)
* [Interfejs użytkownika kanału informacyjnego nie zezwala na kopiowanie adresu URL](http://nuget.codeplex.com/workitem/105)
* [Lepsza obsługa błędów usuwania pakietu.](http://nuget.codeplex.com/workitem/107)
* [Wpisywanie w oknie konsoli zależy od fokusu kursora](http://nuget.codeplex.com/workitem/112)
* [Komunikaty o błędach wyglądają Awful](http://nuget.codeplex.com/workitem/116)
* [Wydajność usuwania pakietu dla pakietu, który nie jest zainstalowany, jest zła](http://nuget.codeplex.com/workitem/117)
* [Usuwanie pakietu kończy się niepowodzeniem, gdy nie ma żadnych źródeł pakietów](http://nuget.codeplex.com/workitem/119)
* [Usuwanie pakietu nie powiodło się, gdy źródło pakietu jest niedostępne](http://nuget.codeplex.com/workitem/120)
* [Dodaj tytuł do metadanych pakietu i źródła danych.](http://nuget.codeplex.com/workitem/125)
* [Dodaj parametr-source z powrotem do dodatku Add-Package](http://nuget.codeplex.com/workitem/127)
* [Pakiet list powinien mieć parametr-source.](http://nuget.codeplex.com/workitem/128)
* [Zaktualizuj NuPack. Server, aby wymagał do pobrania pakietu przez agenta użytkownika NuPack](http://nuget.codeplex.com/workitem/142)
* [Okno dialogowe akceptacji licencji musi wyświetlić listę licencji dla wszystkich zależności, które wymagają akceptacji](http://nuget.codeplex.com/workitem/145)
* [Rejestruj błąd, gdy pakiet zgłosi w strumieniu danych](http://nuget.codeplex.com/workitem/150)
* [NuPack. exe nie powinien zezwalać na puste &lt;licenseurl elementu&gt;](http://nuget.codeplex.com/workitem/152)
* [Zmień nazwę listy-pakiet na Pobierz pakiet, Dodaj pakiet do instalacji pakietu i Usuń pakiet, aby odinstalować pakiet](http://nuget.codeplex.com/workitem/155)
* [Korzystanie z elementu menu Dodaj odwołanie do pakietu z okna Nawigator rozwiązań ulega awarii Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Brak dwukropka w etykiecie "available sources"](http://nuget.codeplex.com/workitem/160)
* [Utwórz nuspecą wielkość liter w elemencie XML spójnie notacji CamelCase](http://nuget.codeplex.com/workitem/161)
* [Manifest NuPack VSIX musi włączać bit "admin"](http://nuget.codeplex.com/workitem/162)
* [Jeśli zostanie uruchomiony pakiet list bez kanałów informacyjnych, otrzymasz błąd odwołania o wartości null](http://nuget.codeplex.com/workitem/164)
* [NuGet. exe: Określanie ścieżki docelowej](http://nuget.codeplex.com/workitem/171)
* [Błędy programu PowerShell otwierające konsolę Zarządzanie pakietami w systemie WinXP](http://nuget.codeplex.com/workitem/175)
* [VS Crash podczas próby załadowania listy pakietów](http://nuget.codeplex.com/workitem/176)
* [Zezwalaj na meta Packages (bez plików, tylko zależności)](http://nuget.codeplex.com/workitem/180)
* [Konwertuj skrypt programu PowerShell do modułu programu PowerShell 2,0](http://nuget.codeplex.com/workitem/181)
* [PathResolver powinna odrzucać część ścieżki poprzedzającą symbole wieloznaczne, gdy określono element docelowy](http://nuget.codeplex.com/workitem/183)
* [Brak zależności](http://nuget.codeplex.com/workitem/186)
* [Błąd instalowania pakietu ELMAH](http://nuget.codeplex.com/workitem/192)
* [Przekształcenia konfiguracji nie działają poprawnie z &lt;configSections&gt;](http://nuget.codeplex.com/workitem/194)
* [Nie można pobrać zmiennej "$global:p rojectCache", ponieważ nie została ona ustawiona](http://nuget.codeplex.com/workitem/203)
* [Dodaj zadanie programu MSBuild do tworzenia pakietów NuPack](http://nuget.codeplex.com/workitem/205)
* [Lista-pakiet musi obsługiwać wyszukiwanie/filtrowanie](http://nuget.codeplex.com/workitem/206)
* [Zawsze wyświetlaj link do licencji, jeśli autor pakietu udostępnia adres URL licencji](http://nuget.codeplex.com/workitem/208)
* [Wyjątek "odmowa dostępu" z usunięciem pakietu](http://nuget.codeplex.com/workitem/213)
* [Testy jednostkowe zakończone niepowodzeniem: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Zezwalaj na rezerwowy/domyślny zestaw plików, jeśli nie można znaleźć wersji platformy specfic Framework](http://nuget.codeplex.com/workitem/223)
* [Dodaj odwołanie do pakietu... Interfejs użytkownika nie może usunąć pakietu](http://nuget.codeplex.com/workitem/225)
* [Dodaj odwołanie do pakietu Crash Studio, gdy co najmniej jeden projekt zostanie zwolniony](http://nuget.codeplex.com/workitem/228)
* [Transformacja konfiguracji nie działa w pliku Web. Debug. config](http://nuget.codeplex.com/workitem/229)
* [init. ps1 nie jest wyzwalana w pakiecie niestandardowym](http://nuget.codeplex.com/workitem/237)
* [Po dodaniu ścieżek do feedlist, przycisk domyślny jest ustawiony na OK, więc po naciśnięciu klawisza ENTER jest automatycznie zamykana](http://nuget.codeplex.com/workitem/240)
* [Próba odinstalowania zależności spowoduje awarię, a jeśli w wierszu podjęto próbę 2 razy](http://nuget.codeplex.com/workitem/241)
* [Wyświetl adres URL projektu w oknie dialogowym Dodaj pakiet](http://nuget.codeplex.com/workitem/253)
* [Domyślne okno dialogowe Dodaj pakiet do zainstalowanych pakietów](http://nuget.codeplex.com/workitem/254)
* [Zmień element menu okna dialogowego Dodaj pakiet.](http://nuget.codeplex.com/workitem/261)
* [Zmień nazwę przestrzeni nazw i zestawów](http://nuget.codeplex.com/workitem/274)
* [Zmień nazwę projektu NuPack na NuGet](http://nuget.codeplex.com/workitem/282)
* [Dodaj następujący tekst poniżej listy zależności](http://nuget.codeplex.com/workitem/288)
* [Zmień tekst akceptacji licencji w oknie dialogowym akceptacji licencji](http://nuget.codeplex.com/workitem/291)
* [Zmień tekst w oknie dialogowym akceptacji licencji powyżej listy pakietów](http://nuget.codeplex.com/workitem/292)
* [Usługa OData nie działa z adresem URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Interfejs użytkownika Menedżera pakietów: zbyt agresywne buforowanie liczby pakietów używanej na potrzeby stronicowania](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet — błąd konsoli Menedżera pakietów&gt;](http://nuget.codeplex.com/workitem/335)
* [W oknie dialogowym Dodawanie pakietu jest wyświetlana akceptacja licencji dla już zainstalowanej spakowanej](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Poniżej znajduje się lista funkcji i usterek, które zostały naprawione dla programu NuGet CTP 1.

* [Nazwa rozszerzenia pakietu powinna mieć nazwę. nupack](http://nuget.codeplex.com/workitem/1)
* [Przenieś plik pakietu do folderu](http://nuget.codeplex.com/workitem/2)
* [Scalanie instalacji &amp; Dodawanie poleceń PS](http://nuget.codeplex.com/workitem/3)
* [Tworzenie aliasów dla poleceń cmdlet czasownik-rzeczownik](http://nuget.codeplex.com/workitem/4)
* [NuPack odmylić podczas przełączania rozwiązania w programie VS](http://nuget.codeplex.com/workitem/6)
* [Domyślnie Ukryj folder rozwiązania "Packages"](http://nuget.codeplex.com/workitem/11)
* [Dodano obsługę zamiany tokenów w elementach zawartości.](http://nuget.codeplex.com/workitem/12)
* [NuPack. interfejs użytkownika powinien używać interfejsu API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core]: Packagemanager oznacza pakiety jako zainstalowane przed ich zainstalowaniem](http://nuget.codeplex.com/workitem/27)
* [Usunięcie projektu domyślnego z rozwiązania nadal pokazuje usunięty projekt jako domyślny](http://nuget.codeplex.com/workitem/30)
* [Nowy pakiet — nie można dodać części dla określonego identyfikatora URI, ponieważ jest już w pakiecie.](http://nuget.codeplex.com/workitem/32)
* [Usuń ciągi "NuPack" z graficznego interfejsu użytkownika programu Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Dodaj nagłówek Apache do pliku COPYRIGHT. txt](http://nuget.codeplex.com/workitem/36)
* [Remove Update-PackageSource Command](http://nuget.codeplex.com/workitem/37)
* [Menedżer pakietów nie nadaje się do użytku podczas ładowania profilu zgłasza wyjątek](http://nuget.codeplex.com/workitem/39)
* [init. ps1, install. ps1 i Uninstall. ps1 muszą otrzymać dodatkowy stan](http://nuget.codeplex.com/workitem/41)
* [Łączenie konsoli i pakietów graficznego interfejsu użytkownika w jeden pakiet](http://nuget.codeplex.com/workitem/42)
* [Logika transformacji XML nie działa w przypadku zastosowania do kodu XML, który nie znajduje się w katalogu głównym](http://nuget.codeplex.com/workitem/43)
* [Okno dialogowe Zarządzanie ustawieniami źródeł pakietów nie aktualizuje konsoli NuPack](http://nuget.codeplex.com/workitem/44)
* [Interfejs użytkownika konsoli NuPack: Zmień nazwę listy rozwijanej "pakiet" na "Źródło pakietu"](http://nuget.codeplex.com/workitem/45)
* [Opcje konsoli NuPack: Zmień nazwę interfejsu użytkownika repozytorium na zgodną z konsolą NuPack](http://nuget.codeplex.com/workitem/46)
* [Dodawanie pakietu kończy się niepowodzeniem w witrynie sieci Web, która została otwarta z usług IIS lub z adresem URL](http://nuget.codeplex.com/workitem/53)
* [Źródło Menedżera pakietów nie współpracuje z FwLink](http://nuget.codeplex.com/workitem/55)
* [Ustaw domyślne źródło pakietu](http://nuget.codeplex.com/workitem/59)
* [Podczas dodawania źródeł pakietów w opcji, gdy jest dostarczane tylko jedno źródło, należy założyć, że jest to wartość domyślna.](http://nuget.codeplex.com/workitem/60)
* [Interfejs użytkownika okna dialogowego pokazuje fałszywe "ostatnie" pakiety](http://nuget.codeplex.com/workitem/62)
* [Opcje: kliknięcie przycisku Anuluj nie powoduje anulowania zmian](http://nuget.codeplex.com/workitem/63)
* [W oknie dialogowym Dodawanie odwołania do pakietu nie powinno się uwzględniać wielkości liter](http://nuget.codeplex.com/workitem/65)
* [Napraw metadane firmy w plikach AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numer wersji VSIX](http://nuget.codeplex.com/workitem/71)
* [Usuń pakiet: używanie-? Wyświetla pomoc dwa razy](http://nuget.codeplex.com/workitem/72)
* [Wykonaj pakiety instalacyjne/odinstalowywane dla pakietów na poziomie projektu](http://nuget.codeplex.com/workitem/74)
* [Serwer nie może utworzyć źródła danych w przypadku niepowodzenia weryfikacji jednej nupack](http://nuget.codeplex.com/workitem/90)
* [Należy zastąpić ikony NuPack](http://nuget.codeplex.com/workitem/94)
* [Serwer proxy HTTP NTLM nie jest uwierzytelniany w kanale informacyjnym pakietu.](http://nuget.codeplex.com/workitem/96)
* [Okno dialogowe nie jest zawsze uruchamiane w środkowym oknie programu VS](http://nuget.codeplex.com/workitem/100)
* [Wiele pól w szczegółach pakietów nie jest wypełnianych w oknie dialogowym](http://nuget.codeplex.com/workitem/102)
* [Interfejs użytkownika okna dialogowego nie wyświetla nazw autorów](http://nuget.codeplex.com/workitem/108)
* [Dlaczego — wersja do usunięcia pakietu](http://nuget.codeplex.com/workitem/113)
* [Usuń kartę ostatnie w interfejsie użytkownika okna dialogowego](http://nuget.codeplex.com/workitem/115)
* [VS Crash po kliknięciu prawym przyciskiem myszy folderu rozwiązania po otwarciu okna dialogowego interfejsu użytkownika co najmniej jeden.](http://nuget.codeplex.com/workitem/126)
* [Zmień parametr-Local elementu list-Package na-installed](http://nuget.codeplex.com/workitem/129)
* [Zmień nazwę Packages. XML na NuPack. config](http://nuget.codeplex.com/workitem/132)
* [Konsola wymusza przejście kursora do końca wiersza](http://nuget.codeplex.com/workitem/135)
* [Funkcja IntelliSense usuwania pakietów została przerwana](http://nuget.codeplex.com/workitem/136)
* [Dodaj flagę RequireLicenseAcceptance do. nuspec i źródła danych](http://nuget.codeplex.com/workitem/137)
* [Dodawanie LicenseUrl do formatu. nuspec i źródła danych pakietu](http://nuget.codeplex.com/workitem/138)
* [Kliknięcie przycisku Zainstaluj dla pakietu wymagającego akceptacji powinno spowodować wyświetlenie okna dialogowego akceptacji](http://nuget.codeplex.com/workitem/139)
* [Dodawanie tekstu odpowiedzialności do okna dialogowego Dodawanie pakietu](http://nuget.codeplex.com/workitem/140)
* [Dodaj zastrzeżenie, gdy konsola pakietu jest uruchamiana po raz pierwszy](http://nuget.codeplex.com/workitem/143)
* [Wyświetl oświadczenie po zainstalowaniu pakietu w konsoli](http://nuget.codeplex.com/workitem/144)
* [Zmień nazwę rozszerzenia nupack na. nupkg](http://nuget.codeplex.com/workitem/146)