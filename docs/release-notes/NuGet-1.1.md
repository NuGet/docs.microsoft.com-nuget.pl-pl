---
title: Informacje o wersji NuGet 1.0 i 1.1
description: Informacje o wersji programu NuGet 1.1, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547024"
---
# <a name="nuget-10-and-11-release-notes"></a>Informacje o wersji NuGet 1.0 i 1.1

[Informacje o wersji 1.2 NuGet](../release-notes/nuget-1.2.md)

NuGet w wersji 1.0 został wydany 13 stycznia 2011.  NuGet 1.1 został wydany 12 lutego 2011 r.

## <a name="overview"></a>Omówienie

Ten dokument zawiera informacje o wersji dla różnych wersji 1.0 NuGet, pogrupowane według wersji głównej (wersja zapoznawcza).

NuGet obejmuje następujące składniki:

* *NuGet.Tools.vsix* * który składa się z:
  * **Dodaj okno dialogowe pakietu biblioteki** * okna dialogowego w programie Visual Studio umożliwia przeglądanie i instalowanie pakietów.
  * **Konsola Menedżera pakietów** * konsoli w programie Visual Studio oparte na programie Powershell.
* *Narzędzie wiersza polecenia NuGet* * narzędzia służące do tworzenia (i po pewnym czasie publikowania) pakietów.

Rozszerzenie NuGet narzędzia Visual Studio (*NuGet.Tools.vsix*) wymaga:

* Visual Studio 2010 ani Visual Web Developer 2010 Express.

Narzędzie wiersza polecenia NuGet wymaga:

* Wersja programu .NET framework 4

## <a name="installation"></a>Instalacja

Aby użyć tej funkcji [najnowszej wersji](http://nuget.codeplex.com/releases/view/52018):

* Najpierw należy odinstalować starsze kompilacji. Musisz uruchomić program VS jako administrator, aby to zrobić.
* Usuń wszystkie istniejące źródła danych, do których masz.
* Dodaj nowe źródło danych, wskazując [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Lista problemów rozwiązanych w tej wersji [można znaleźć tutaj](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Jeden problem został rozwiązany dla wersji RTM od czasu wersji RC.

* [Problem 474: Usuwanie pakietów ma wpływ na wszystkich projektów w rozwiązaniu](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>W wersji Release Candidate

Dostępne są następujące zmiany wprowadzone w tej wersji Release Candidate od CTP 2. Odwiedź witrynę śledzenia problemu, aby wyświetlić pełną listę błędów.

* [Aktualizowanie pakietu z konsoli nie aktualizuje zależności.](http://nuget.codeplex.com/workitem/443)
* [Dodawanie pakietu przejmuje bin nie pakietu odwołania (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Aktualizowanie pakietu pozostawia przerwanymi odwołaniami](http://nuget.codeplex.com/workitem/440)
* [Get-Package-aktualizacji nie powiedzie się, w oknie dialogowym lub po wybraniu źródła "Wszystkie" agregacji w konsoli programu](http://nuget.codeplex.com/workitem/439)
* [Występują błędy weryfikacji pakietu](http://nuget.codeplex.com/workitem/426)
* [Ostrzegać użytkowników, gdy nie można zainstalować pakietu z poziomu okna dialogowego Dodawanie pakietu](http://nuget.codeplex.com/workitem/425)
* [Get-Package-aktualizuje zgłasza wyjątek, gdy trwa aktualizowanie dużej liczby pakietów](http://nuget.codeplex.com/workitem/424)
* [Poprawa obsługi błędu, gdy nuspec plików są autoryzowane](http://nuget.codeplex.com/workitem/423)
* [Pakiet Nuget ignoruje określone pliki](http://nuget.codeplex.com/workitem/422)
* [Usunięcie źródła pakietu na sekundę do ostatniego, a następnie klikając przycisk "Przenieś w dół" ulega awarii programu VS](http://nuget.codeplex.com/workitem/418)
* [Usuń odwołanie do zestawu podczas instalowania pakietów](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException podczas otwierania okna dialogowego Ustawienia](http://nuget.codeplex.com/workitem/411)
* [Klucz dostępu do źródła pakietu w konsoli Menedżera pakietów nie działa](http://nuget.codeplex.com/workitem/410)
* [Klucze dostępu w oknie dialogowym Ustawienia NuGet programu VS fokus niewłaściwych pól](http://nuget.codeplex.com/workitem/409)
* [Funkcja intellisense pakietu ID nie powinien zbadać zbyt wiele elementów](http://nuget.codeplex.com/workitem/404)
* [Błąd podczas dodawania pakietu do projektu przy użyciu znaku kropki w nazwie projektu](http://nuget.codeplex.com/workitem/403)
* [Problem z określonych plików w nuspec](http://nuget.codeplex.com/workitem/400)
* [Podczas korzystania z nowszej kompilacji należy zarejestrować poprawne oficjalne źródło danych](http://nuget.codeplex.com/workitem/399)
* [Tagi użyj spacji zamiast #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata brakuje nieco przydatnych informacji](http://nuget.codeplex.com/workitem/388)
* [Dodawanie łącza zgłaszania nadużycia do okna dialogowego](http://nuget.codeplex.com/workitem/386)
* [Aby rozpakować podziały pakietów w programie Visual Studio przy użyciu App_Data](http://nuget.codeplex.com/workitem/380)
* [Implementowanie tagów](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder umożliwia pusty pakiet bez zależności do utworzenia](http://nuget.codeplex.com/workitem/373)
* [Dodaj pole właścicieli pakietu](http://nuget.codeplex.com/workitem/365)
* [Aktualizowanie manifestu VSIX powiedzieć, Menedżer pakietów NuGet, a nie narzędzia VSIX](http://nuget.codeplex.com/workitem/364)
* [Polecenie Get-Package zgłasza błąd, gdy wybrano wszystkie źródła](http://nuget.codeplex.com/workitem/359)
* [Kolejność źródeł pakietów w oknie dialogowym Opcje](http://nuget.codeplex.com/workitem/356)
* [Pakiet aktualizacji nie powoduje usunięcia starszych wersji](http://nuget.codeplex.com/workitem/352)
* [Zakres wersji implementacji specyfikacji dla zależności](http://nuget.codeplex.com/workitem/347)
* [Visual Studio ulega awarii po kliknięciu przycisku "Dodaj nowy pakiet"](http://nuget.codeplex.com/workitem/346)
* [Wyświetl pliki do pobrania i oceny w oknie dialogowym Dodaj pakiet](http://nuget.codeplex.com/workitem/345)
* [Zmiana między źródłami pakietów w oknie dialogowym nie powoduje aktualizacji aktywne źródłowe](http://nuget.codeplex.com/workitem/344)
* [Usuń powiązanie klawiszy dla okna konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/339)
* [Pakiet instalacyjny nie został rozpoznany jako nazwa polecenia cmdlet...](http://nuget.codeplex.com/workitem/338)
* [Instalowanie pakietu z lokalnego źródła danych zależności na regularne źródła danych nie są rozpoznawane.](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies należy pominąć zależności, które są nadal w użyciu](http://nuget.codeplex.com/workitem/331)
* [W przypadku anulowania nawigowania po stronach, użytkownik nie można przejść do innej strony, gdy zwraca oryginalne żądanie strony](http://nuget.codeplex.com/workitem/325)
* [Zbadaj wydajność NuPack.Server potrzeby źródeł danych za pomocą dużej liczby pakietów.](http://nuget.codeplex.com/workitem/324)
* [Po raz drugi filtrować pakietu używa źródła pakietu "Nowy", zamiast wcześniej wybranego źródła.](http://nuget.codeplex.com/workitem/321)
* [Należy wybrać domyślne źródło pakietu, wybierając kartę "Online" w oknie dialogowym.](http://nuget.codeplex.com/workitem/320)
* [Lista pakietów powinien być wyświetlony zainstalowane pakiety domyślnie](http://nuget.codeplex.com/workitem/309)
* [HintPaths odwołania zestawu](http://nuget.codeplex.com/workitem/294)
* [Wyjątek podczas otwierania konsoli Menedżera pakietów](http://nuget.codeplex.com/workitem/268)
* [Funkcja intellisense konsoli pliki do pobrania całego źródła danych](http://nuget.codeplex.com/workitem/259)
* [Powinny zostać zmienione "Default" źródła pakietu na "Aktywny"](http://nuget.codeplex.com/workitem/258)
* [Pakiet źródeł interfejsu użytkownika: naciśnięcie przycisku OK należy dodać nowe źródło, jeśli źródło/nazwy pól są niepuste](http://nuget.codeplex.com/workitem/257)
* [Okno dialogowe staje się bardzo wolno, jeśli liczba zainstalowanych pakietów jest duża](http://nuget.codeplex.com/workitem/243)
* [Obsługa przekierowań powiązań silne nazwanych zestawów](http://nuget.codeplex.com/workitem/238)
* [Dodaj odwołanie do pakietu... Interfejs użytkownika, aby uwzględnić listy rozwijanej dla źródła pakietu](http://nuget.codeplex.com/workitem/226)
* [NuPack musi obsługiwać przekształcenie konfiguracji agnostically o nazwie pliku konfiguracji](http://nuget.codeplex.com/workitem/224)
* [Umożliwia BasePath, który ma zostać zastąpiony w NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Działanie procedury rezerwowej źródła pakietu](http://nuget.codeplex.com/workitem/204)
* [Awarii po graficznego interfejsu użytkownika](http://nuget.codeplex.com/workitem/201)
* [Dodaj sortowanie opcji, aby dodać okno dialogowe pakietu](http://nuget.codeplex.com/workitem/179)
* [klawisz skrótu, aby wyczyścić Konsola Menedżera pakietów](http://nuget.codeplex.com/workitem/174)
* [PowerConsole powoduje, że Konsola NuPack nie powiedzie się](http://nuget.codeplex.com/workitem/166)
* [Konsola i Dodaj okno dialogowe pakietu, należy ustawić agenta użytkownika w żądań](http://nuget.codeplex.com/workitem/141)
* [Ustaw numer wersji VSIX i NuPack.exe w kompilacji.](http://nuget.codeplex.com/workitem/134)
* [Ukryj typowe parametry programu PowerShell z-?](http://nuget.codeplex.com/workitem/118)
* [Dodaj - szczegółową pomoc dotyczącą poleceń konsoli](http://nuget.codeplex.com/workitem/110)
* [Dodaj okno dialogowe pakietu powinien zezwalać na wybranie bieżącej źródła pakietu](http://nuget.codeplex.com/workitem/88)
* [Przenieś NuPack.Core klasy do różnych obszarów nazw](http://nuget.codeplex.com/workitem/50)
* [Dodawanie pomocy do poleceń cmdlet](http://nuget.codeplex.com/workitem/23)
* [Sprawdź skrót z kanału informacyjnego, po pobraniu pakietu](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Poniżej przedstawiono najbardziej znaczących zmian wprowadzonych w wersji CTP 2:

* Przełączono pakietu Kanał informacyjny z ATOM punkt końcowy usługi OData: po uaktualnieniu do wersji CTP2 pakietu NuGet, należy dodać następujący adres URL jako źródło pakietów: `https://feed.nuget.org/ctp2/odata/v1/`.
* Zmieniono nazwę polecenia Add-Package *Install-Package*.
* Zaktualizowano `.nuspec` formatu. `.nuspec` Formatu zawiera teraz *iconUrl* pola do określania ikonę png 32 x 32, która będzie wyświetlana w oknie dialogowym Dodawanie pakietu. Dlatego należy ustawić, aby odróżnić pakietu. `.nuspec` Formatu zawiera również nowe *projectUrl* pola, które można użyć, aby wskazywał strony sieci web, który zawiera więcej informacji na temat pakietu.

Ta kompilacja nie będzie działać ze starą `.nupkg` plików. Jeśli występują wyjątki odwołanie o wartości null, używasz starego `.nupkg` pliku i trzeba odbudować dane za pomocą zaktualizowanego [narzędzia wiersza polecenia NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Oto lista narzędzi i błędy, które zostały usunięte NuGet CTP 2 (nie ma błędów dla niewielkiej zmiany w kodzie przesłali itp.).

* [Rozpakowywanie zestawy pakietów błędu podczas określenie TargetFramework dla zestawu.](http://nuget.codeplex.com/workitem/10)
* [Tworzenie okna konsoli NuPack mogą szybciej odnajdywać](http://nuget.codeplex.com/workitem/14)
* [ILMerge wersji nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Lepsza obsługa wyjątków/błąd](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager bezpiecznie powinna obsługiwać błędy związane z kanału informacyjnego](http://nuget.codeplex.com/workitem/28)
* [Potrzebujesz nową ikonę dla konsoli](http://nuget.codeplex.com/workitem/29)
* [Localize — ciągi w oknie dialogowym](http://nuget.codeplex.com/workitem/38)
* [Pamięci podręczne NuPack pobranych plików .nupack w pamięci](http://nuget.codeplex.com/workitem/40)
* [Konsola NuPack: Zmień domyślny skrót do wyświetlania konsoli](http://nuget.codeplex.com/workitem/48)
* [Współdzielone powinien obsługiwać wartości domyślne dla często używanych właściwości](http://nuget.codeplex.com/workitem/49)
* [Uruchamianie nupack.exe w folderze przy użyciu tylko jednego pliku nuspec należy używać tego nuspec](http://nuget.codeplex.com/workitem/52)
* [Menu projektu pojawia się nawet wtedy, gdy projekt/rozwiązanie jest ładowany](http://nuget.codeplex.com/workitem/54)
* [Build.cmd zakończy się niepowodzeniem w czyste klonu kodu](http://nuget.codeplex.com/workitem/56)
* [Funkcja dostępnych aktualizacji](http://nuget.codeplex.com/workitem/57)
* [Okno dialogowe: Dodanie pakietu za pomocą okna dialogowego usuwa wiersz w konsoli programu](http://nuget.codeplex.com/workitem/73)
* [Dodawanie pakietu, klikając przycisk "Zainstaluj" odbywa się powoli, bez nie wizualną opinię](http://nuget.codeplex.com/workitem/80)
* [Nie ma możliwości odnajdywania, które Moje zainstalowane pakiety mają aktualizacje.](http://nuget.codeplex.com/workitem/82)
* [Nie ma możliwości można zaktualizować zainstalowanego pakietu w oknie dialogowym.](http://nuget.codeplex.com/workitem/83)
* [Nie ma możliwości odinstalowania zainstalowanego pakietu w oknie dialogowym](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Dodawanie odwołania do pakietu&hellip; &rdquo; pojawia się w menu kontekstowym zainstalowanych odwołań](http://nuget.codeplex.com/workitem/85)
* [Po zaktualizowaniu pakietu w konsoli, pokazuje zarówno starej wersji, jak i nowa wersja jako zainstalowane](http://nuget.codeplex.com/workitem/86)
* [Działanie w konsoli, korzystając z okna dialogowego, zniknie po użyciu](http://nuget.codeplex.com/workitem/87)
* [Analizowanie w nupack.exe wiersza polecenia oczyszczania](http://nuget.codeplex.com/workitem/89)
* [Dodaj przyjazną nazwę do źródła pakietu](http://nuget.codeplex.com/workitem/98)
* [Aktualizuj .nuspec do obsługi tym ikony pakietu](http://nuget.codeplex.com/workitem/103)
* [Źródła danych interfejsu użytkownika nie zezwala, kopiując adres URL](http://nuget.codeplex.com/workitem/105)
* [Lepsza obsługa błędów remove-package.](http://nuget.codeplex.com/workitem/107)
* [Wpisz w oknie konsoli jest zależna od fokus kursora](http://nuget.codeplex.com/workitem/112)
* [Często są bardzo Sprawdź komunikaty o błędach](http://nuget.codeplex.com/workitem/116)
* [Wydajność Remove-Package dla pakietu, który nie jest zainstalowany jest nieodpowiedni](http://nuget.codeplex.com/workitem/117)
* [Usunięcie pakietu nie powiedzie się, gdy brak źródeł pakietów](http://nuget.codeplex.com/workitem/119)
* [Remove-Package zakończy się niepowodzeniem, gdy źródło pakietu jest niedostępny](http://nuget.codeplex.com/workitem/120)
* [Dodaj tytuł metadane pakietów i źródła danych.](http://nuget.codeplex.com/workitem/125)
* [Dodaj parametr - źródła, przywracając Add-Package](http://nuget.codeplex.com/workitem/127)
* [Listy pakietu powinien mieć parametr - źródła](http://nuget.codeplex.com/workitem/128)
* [Aktualizuj NuPack.Server będą musieli NuPack użytkownika do pobrania pakiet agenta](http://nuget.codeplex.com/workitem/142)
* [Okno dialogowe akceptacja licencji musi katalogować licencji dla wszystkich zależności, które wymagają akceptacji](http://nuget.codeplex.com/workitem/145)
* [Zapisz błąd do dziennika, gdy pakiet zgłasza w źródle danych](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe nie powinien zezwalać na pustą &lt;licenseurl&gt; — element](http://nuget.codeplex.com/workitem/152)
* [Zmień nazwę listy pakietu Get-Package, Add-Package Install-Package i Remove-Package można odinstalować pakietu](http://nuget.codeplex.com/workitem/155)
* [Przy użyciu elementu menu Dodaj odwołanie do pakietu z Navigator rozwiązania awarie programu Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Brak dwukropka etykietę "pakiet źródła"](http://nuget.codeplex.com/workitem/160)
* [Wprowadź .nuspec xml element wielkość liter w wyrazie spójnie pisane z uwzględnieniem wielkości liter](http://nuget.codeplex.com/workitem/161)
* [Manifest NuPack VSIX musi włączyć bit "admin"](http://nuget.codeplex.com/workitem/162)
* [Jeśli uruchamiasz wyświetlenia listy pakietów z nie źródeł danych, otrzymasz błąd odwołania o wartości null](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: Określ ścieżkę docelową](http://nuget.codeplex.com/workitem/171)
* [Błędy programu PowerShell otwierania konsoli zarządzania pakietami na Windows XP](http://nuget.codeplex.com/workitem/175)
* [VS awarii podczas próby załadowania listy pakietów](http://nuget.codeplex.com/workitem/176)
* [Zezwalaj na metadane pakietów (nie plików, tylko zależności)](http://nuget.codeplex.com/workitem/180)
* [Konwertuj skrypt programu Powershell do modułu programu Powershell w wersji 2.0](http://nuget.codeplex.com/workitem/181)
* [PathResolver powinien usunąć znaki symboli wieloznacznych poprzedzającej część ścieżki, jeśli nie określono docelowej](http://nuget.codeplex.com/workitem/183)
* [Brak zależności](http://nuget.codeplex.com/workitem/186)
* [Błąd podczas instalowania biblioteki Elmah](http://nuget.codeplex.com/workitem/192)
* [Transformacje konfiguracji nie będą działać poprawnie z &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Zmienna "$globalny: projectCache" nie można pobrać, ponieważ nie zostało ustawione](http://nuget.codeplex.com/workitem/203)
* [Dodaj zadanie programu MSBuild do tworzenia pakietów NuPack](http://nuget.codeplex.com/workitem/205)
* [Lista pakietów obsługi musi obsługiwać wyszukiwanie/filtrowania](http://nuget.codeplex.com/workitem/206)
* [Zawsze wyświetlaj łącze do licencji, jeśli autor pakietu zawiera adres URL licencji](http://nuget.codeplex.com/workitem/208)
* [Sporadyczne wyjątek "Odmowa dostępu" Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Niepowodzenie testów jednostkowych: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Umożliwić rezerwowe, domyślny zbiór plików, jeśli nie można odnaleźć wersji framework przeznaczonych dla określonej](http://nuget.codeplex.com/workitem/223)
* [Dodaj odwołanie do pakietu... Interfejs użytkownika nie można usunąć pakietu](http://nuget.codeplex.com/workitem/225)
* [Dodaj odwołanie do pakietu awarii studio, gdy dla jednego lub więcej projektów jest zwolniony](http://nuget.codeplex.com/workitem/228)
* [Aby pracować na pliku web.debug.config nie ma przekształcenie konfiguracji](http://nuget.codeplex.com/workitem/229)
* [init.ps1 nie uruchomiono na pakiecie niestandardowym](http://nuget.codeplex.com/workitem/237)
* [Podczas dodawania ścieżek do feedlist, przycisk domyślny jest równa OK, więc jeśli I naciśnij klawisz ENTER automatyczne zamknięcie](http://nuget.codeplex.com/workitem/240)
* [Podejmować próby odinstalowania zależność ulegnie awarii programu VS, jeśli próba 2 razy z rzędu](http://nuget.codeplex.com/workitem/241)
* [Wyświetl adres URL projektu w oknie dialogowym Dodawanie pakietu](http://nuget.codeplex.com/workitem/253)
* [Domyślnie okno dialogowe Add-Package, aby zainstalować pakiety](http://nuget.codeplex.com/workitem/254)
* [Zmień element menu Dodaj okno dialogowe pakietu.](http://nuget.codeplex.com/workitem/261)
* [Zmień nazwę przestrzeni nazw i zestawów](http://nuget.codeplex.com/workitem/274)
* [Zmień nazwę projektu NuPack do narzędzia NuGet](http://nuget.codeplex.com/workitem/282)
* [Dodaj następujący tekst, na liście zależności](http://nuget.codeplex.com/workitem/288)
* [Zmień tekst akceptacja licencji w okno dialogowe akceptacja licencji](http://nuget.codeplex.com/workitem/291)
* [Zmień tekst w okno dialogowe akceptacja licencji powyżej listy pakietów](http://nuget.codeplex.com/workitem/292)
* [OData nie działa w przypadku adresu URL fwlink](http://nuget.codeplex.com/workitem/304)
* [Interfejs użytkownika Menedżera pakietów: za pośrednictwem agresywne buforowania liczba pakietów używane dla stronicowania](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet —&gt; błąd Konsola Menedżera pakietów](http://nuget.codeplex.com/workitem/335)
* [Dodaj pakiet okna dialogowego pokazuje licencji akceptacji dla już zainstalowane w pakiecie](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Oto lista narzędzi i błędy, które zostały usunięte NuGet wersja CTP 1.

* [Rozszerzenie pakietu powinna zostać zmieniona na .nupack](http://nuget.codeplex.com/workitem/1)
* [Przenieś plik pakietu do folderu](http://nuget.codeplex.com/workitem/2)
* [Scal instalacji &amp; polecenia Dodaj PS](http://nuget.codeplex.com/workitem/3)
* [Tworzenie aliasów dla poleceń cmdlet czasownik-rzeczownik](http://nuget.codeplex.com/workitem/4)
* [NuPack pobiera mylić podczas przełączania rozwiązanie w programie VS](http://nuget.codeplex.com/workitem/6)
* [Należy domyślnie jest ukryty folder "packages" rozwiązania](http://nuget.codeplex.com/workitem/11)
* [Dodanie obsługi zastępowania tokenu w elementach zawartości.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI należy używać interfejsu API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager oznacza pakietów, jak zainstalować przed zainstalowaniem ich](http://nuget.codeplex.com/workitem/27)
* [Usuwanie domyślny projekt z rozwiązania nadal pokazuje usuniętego projektu jako domyślny](http://nuget.codeplex.com/workitem/30)
* [Nowy pakiet nie powiodło się z "Nie można dodać części do określonego identyfikatora URI jest już w pakiecie."](http://nuget.codeplex.com/workitem/32)
* [Usuń parametry "NuPack" z programu Visual Studio GUI](http://nuget.codeplex.com/workitem/35)
* [Dodaj plik Apache nagłówka do COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Remove Update-PackageSource Command](http://nuget.codeplex.com/workitem/37)
* [Zgłasza wyjątek, Menedżer pakietów nienadające się do użytku podczas ładowania profilu](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 i uninstall.ps1 muszą otrzymać dodatkowy stan](http://nuget.codeplex.com/workitem/41)
* [Łączenie konsoli i pakietów graficznego interfejsu użytkownika w jednym pakiecie](http://nuget.codeplex.com/workitem/42)
* [Logika Przekształcanie XML nie działa, jeśli zastosowane do pliku XML, który nie jest w folderze głównym](http://nuget.codeplex.com/workitem/43)
* [Zarządzanie dialogowym ustawień źródła pakietu nie aktualizowania konsoli NuPack](http://nuget.codeplex.com/workitem/44)
* [Konsola NuPack interfejsu użytkownika: Zmiana nazwy listy rozwijanej kanał pakietów do "Źródło pakietu"](http://nuget.codeplex.com/workitem/45)
* [Opcje konsoli NuPack: Zmień nazwę "Repozytorium UI", aby były zgodne z konsoli NuPack](http://nuget.codeplex.com/workitem/46)
* [Dodawanie pakietu nie powiedzie się dla witryny sieci Web, która została otwarta z usług IIS lub adres URL](http://nuget.codeplex.com/workitem/53)
* [Źródło Menedżera pakietów nie współpracuje z FwLink](http://nuget.codeplex.com/workitem/55)
* [Ustaw domyślne źródło pakietu](http://nuget.codeplex.com/workitem/59)
* [Podczas dodawania źródeł pakietów w opcji, gdy są dostarczane tylko jedno źródło, zakłada się, że jest domyślna.](http://nuget.codeplex.com/workitem/60)
* [Okno dialogowe interfejsu użytkownika pokazano fałszywych pakietów "najnowsze"](http://nuget.codeplex.com/workitem/62)
* [Opcje: Kliknięcie przycisku Anuluj nie powoduje anulowania zmian](http://nuget.codeplex.com/workitem/63)
* [Dodawanie wyszukiwania okna dialogowego odwołanie do pakietu, powinien być bez uwzględniania wielkości liter](http://nuget.codeplex.com/workitem/65)
* [Napraw firmy metadanych w plikach AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Numer wersji pliku VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Za pomocą parametru-? Wyświetla Pomoc w dwa razy](http://nuget.codeplex.com/workitem/72)
* [Wykonywanie Instalowanie/Odinstalowywanie pakietów dla pakietów na poziomie projektu](http://nuget.codeplex.com/workitem/74)
* [Nie można utworzyć źródła danych, gdy jeden nupack nie powiodło się sprawdzanie poprawności serwera](http://nuget.codeplex.com/workitem/90)
* [Trzeba wymienić NuPack ikon](http://nuget.codeplex.com/workitem/94)
* [Serwer proxy http NTLM nie są uwierzytelniane kanał pakietów.](http://nuget.codeplex.com/workitem/96)
* [Okno dialogowe nie uruchamiać wyśrodkowany w oknie programu VS](http://nuget.codeplex.com/workitem/100)
* [Wiele pól w szczegółach pakietów nie trwa wypełnianie listy w oknie dialogowym](http://nuget.codeplex.com/workitem/102)
* [Okno dialogowe interfejsu użytkownika nie wyświetla nazwy autorów](http://nuget.codeplex.com/workitem/108)
* [Dlaczego — wersja pakietu Remove](http://nuget.codeplex.com/workitem/113)
* [Usuń kartę najnowsze na okno dialogowe interfejsu użytkownika](http://nuget.codeplex.com/workitem/115)
* [Awarii programu VS, gdy jest to odpowiednie kliknąć folder rozwiązania, po otwarciu okna dialogowego interfejsu użytkownika, co najmniej jeden.](http://nuget.codeplex.com/workitem/126)
* [Zmień parametr - Local listy pakietu: zainstalowana](http://nuget.codeplex.com/workitem/129)
* [Zmień nazwę packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Konsola wymusza kursor do końca wiersza](http://nuget.codeplex.com/workitem/135)
* [Funkcja intellisense pakietu Usuń został przerwany](http://nuget.codeplex.com/workitem/136)
* [Dodaj flagę RequireLicenseAcceptance .nuspec i źródła danych](http://nuget.codeplex.com/workitem/137)
* [Dodawanie źródła danych LicenseUrl .nuspec formatu i pakietu](http://nuget.codeplex.com/workitem/138)
* [Kliknięcie przycisku Zainstaluj pakiet, który wymaga akceptacji powinien wyświetlać okno dialogowe Akceptacja](http://nuget.codeplex.com/workitem/139)
* [Dodaj tekst klauzuli wyłączenia odpowiedzialności na okno dialogowe Dodawanie pakietu](http://nuget.codeplex.com/workitem/140)
* [Dodaj wykluczenie gdy konsola pakietów jest uruchamiany po raz pierwszy](http://nuget.codeplex.com/workitem/143)
* [Wyświetlanie zastrzeżenie po zainstalowaniu pakietu w konsoli programu](http://nuget.codeplex.com/workitem/144)
* [Zmień rozszerzenie .nupack .nupkg](http://nuget.codeplex.com/workitem/146)