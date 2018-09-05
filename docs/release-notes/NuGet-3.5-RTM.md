---
title: Informacje o wersji programu NuGet 3.5 Beta
description: Informacje o wersji programu NuGet 3.5, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550687"
---
# <a name="nuget-35-release-notes"></a>Informacje o wersji 3.5 NuGet

[Informacje o wersji 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [informacje o wersji programu NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Poprawki błędów

* Pakiet nie używa MSBuild 14.1 na mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Karta aktualizacji nie wybierze najnowszej dostępnej wersji, aby zaktualizować zamiast tego wybierz bieżącej zainstalowanej wersji - [#3498](https://github.com/NuGet/Home/issues/3498)

* Usunięcie awarii po uwierzytelniania prywatnej MyGet źródła danych w wersji 2, a następnie klikając pozycję "Pokaż x więcej wyników"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Komunikaty dziennika są prezentowani jako działający w odwrotnej kolejności dla interfejsu użytkownika — [#3446](https://github.com/NuGet/Home/issues/3446)

* Przywracanie pakietów Nuget v3.4.4 - zgłasza "format podanej ścieżce nie jest obsługiwany" - [#3442](https://github.com/NuGet/Home/issues/3442)

* CmdLine 3.6 NuGet w wersji beta nie uznaje — Konfiguracja Prop = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* IKVM Nuget jest powolne, zainstaluj na dużego projektu - [#3428](https://github.com/NuGet/Home/issues/3428)

* Update - Self przechowuje na aktualizowanie sam — nuget.exe [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 instalacji/przywracania z udziału UNC ma wydajność regresji z 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Błąd podczas instalowania Moq z pakietu zarządzania przy użyciu interfejsu użytkownika dla projektu net451 — [#3349](https://github.com/NuGet/Home/issues/3349)

* Instalowanie karty na poziomie rozwiązania nie wyświetla wersję pakietu - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` aktualizacji na karcie zainstalowane traci stan — [#3303](https://github.com/NuGet/Home/issues/3303)

* Pakiet NuGet na `.csproj` ignoruje element pustych plików w `.nuspec` pliku — [#3257](https://github.com/NuGet/Home/issues/3257)

* Projektów witryny sieci Web hostowanych w usługach IIS nie powinno powodować niepowodzenie - przywracania [#3235](https://github.com/NuGet/Home/issues/3235)

* Poświadczenia nie są pobierane z pliku Nuget.Config, gdy punkt końcowy v3 przekierowuje do wersji 2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Pakiet NuGet kończy się niepowodzeniem, można rozpoznać zestawu podczas pobierania metadanych zestawu przenośnego - [#3128](https://github.com/NuGet/Home/issues/3128)

* Nie można odnaleźć Nuget `msbuild.exe` na Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* Pakiet nuget.exe nie zezwala na tag wersji wstępnej, które zaczyna się od cyfry - [#1743](https://github.com/NuGet/Home/issues/1743)

* Instalacja pakietu nuget kończy się niepowodzeniem na VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions filtru nie pracować na poziomie rozwiązania - [#333](https://github.com/NuGet/Home/issues/333)

* Przywracanie przypadkowo nie powiedzie się za pomocą elementu o takiej samej klucz został już dodany. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nie można zainstalować Nuget.Common w `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Korzystając z interfejsu użytkownika do wyszukania źródła V2, FindPackagesById jest wywoływana dwa razy dla każdego Identyfikatora - [#2517](https://github.com/NuGet/Home/issues/2517)

* Pakiety nie może zależeć od projekty — [#2490](https://github.com/NuGet/Home/issues/2490)

* Pakiet nuget.exe — Wyklucz jest udokumentowany, ale nie jest obsługiwana — [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemy z powodu błędu komunikaty, kiedy sekcję "pliki" `.nuspec` jest nieprawidłowy — [#1686](https://github.com/NuGet/Home/issues/1686)

* Zawsze wysyła wypychane cały pakiet dwa razy z uwierzytelnione źródła pakietów - [#1501](https://github.com/NuGet/Home/issues/1501)

* Brak informacji podano podczas wywoływania nuget.exe *.csproj aktualizacji, podczas projektu nie ma `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` Przywracanie nie ponawia próby na kodach stanu 5xx ze źródeł w wersji 2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Dwie kropki w pliku src w `.nuspec` nie działa — [#2947](https://github.com/NuGet/Home/issues/2947)

* Przywracanie CoreCLR musi Ignoruj źródła danych za pomocą szyfrowania — [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe wypychania obsługi 403 - niepoprawnie monit o podanie poświadczeń - [#2910](https://github.com/NuGet/Home/issues/2910)

* Aktualizacja NuGet za pomocą Menedżera pakietów usuwa właściwości z `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* Próbuje załadować "NuGet.TeamFoundationServer14", ale że nazwa biblioteki DLL zmienił się na "NuGet.TeamFoundationServer" - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)

* Menedżer pakietów interfejsu użytkownika nie wyświetla nowo zaktualizowanej wersji - [#2828](https://github.com/NuGet/Home/issues/2828)

* Próba użycia packageid, pakiet aktualizacji wersji zamiast package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* csproj przywracania nuget powinny błąd, jeśli projekt nie jest za pomocą narzędzia nuget (`packages.config` lub `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Błąd w programie TFS "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego" podczas uaktualniania lub odinstalowywania, gdy rozwiązania/projektu jest powiązana z kontroli źródła w programie TFS — [#2739](https://github.com/NuGet/Home/issues/2739)

* pakiet aktualizacji nie uzyskać zależności pakietów-target - [#2724](https://github.com/NuGet/Home/issues/2724)

* Nie ma możliwości można ustawić poziom szczegółowości dzienników dla działania interfejsu użytkownika Menedżera pakietów Nuget — [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfiguracja nuget jest nieprawidłowy — VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource w `NuGetDefaults.Config` (`ProgramData\NuGet`) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)

* wydanie narzędzia nuget 3.4.3 — wprowadzenie wartości nie może być pusty podczas kompilacji pakietu - [#2648](https://github.com/NuGet/Home/issues/2648)

* Przywracanie nie używa przechowywanych poświadczeń w pliku Nuget.Config dla kanałów informacyjnych usług VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--configfile jest określana względem katalogu projektu zamiast cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Nadmierne alokacji w kodzie porównania wersji - [#2632](https://github.com/NuGet/Home/issues/2632)

* Wiele wystąpień programu nuget.exe próby zainstalowania takie same pakietu w równoległych powoduje, że podwójne write - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informacje o zależnościach nie jest buforowana dla operacji obejmujących wiele projektów — [#2619](https://github.com/NuGet/Home/issues/2619)

* Instalowanie i aktualizowanie pakietów do pobrania bez sprawdzania, czy packages folder najpierw - [#2618](https://github.com/NuGet/Home/issues/2618)

* Jeśli lista źródła pakietu jest pusta, nie można dodać źródła pakietu za pośrednictwem interfejsu użytkownika (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Błąd w błąd podczas próby zainstalowania pakietu, który zależy od czasu projektowania fasad - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalowanie pakietu z poziomu konsoli PackageManager z ustawieniem "All" próbuje tylko pierwsze źródło - [#2557](https://github.com/NuGet/Home/issues/2557)

* Najnowszej wersji beta nie rozpakowywania ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 awarii podczas uruchamiania komputera z NuGet samodzielnie 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Polecenie aktualizacji może być nieco bardziej szczegółowy, jeśli i poproś, aby była so... - [#2418](https://github.com/NuGet/Home/issues/2418)

* Skompilowany lokalnie VSIX powinny mieć tej samej biblioteki dll i plików jako kompilację o ciągłej integracji. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Rozwiąż ostrzeżenia dotyczące pakietu NuGet starszą wersję w kompilacji - [#2396](https://github.com/NuGet/Home/issues/2396)

* Nieudanych uwierzytelnień źródła pakietu (3 razy) jest zablokowany w nieskończoność - [#2362](https://github.com/NuGet/Home/issues/2362)

* Zawartość pakietu jest nie została poprawnie przywrócona podczas instalowania pakietu z v3.3 nuget + źródła danych z argumentem - Właściwość NoCache Jeśli pakiet zawiera `.nupkg` plików — [#2354](https://github.com/NuGet/Home/issues/2354)

* Nuget Install ze wszystkich źródeł pakietów, ale w pakiecie brakuje ze źródła 1 nie powiodło się — [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Zainstaluj bloków, jeśli pojedyncze źródło odmawia autoryzacji - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` zakres powinien przesłonić - IncludeReferencedProjects wersja — wersja [#1983](https://github.com/NuGet/Home/issues/1983)

* Pakiet aktualizacji bardzo wolno — "próby zebrania informacji zależności" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Zmiany na NuGet niewidzialności starszą wersję pakietu, gdy usługi batch jego zależności — aktualizowanie [#1903](https://github.com/NuGet/Home/issues/1903)

* Aktualizacja nuget.exe spada, silna nazwa zestawu i atrybut Private. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Względna ścieżka do pliku dla "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Poprawić komunikaty o błędach rozpoznawania - [#1373](https://github.com/NuGet/Home/issues/1373)

* pakiet aktualizacji w wersji 3 nie powiedzie się z pakietami w nie określone źródło - [#1013](https://github.com/NuGet/Home/issues/1013)

* Używanie ścieżek względnych dla źródeł pakietów jest problematyczne do użycia — [#865](https://github.com/NuGet/Home/issues/865)

* Brak zależności w pliku NUPKG, wygenerowany z projektu, jeśli istnieje już pośrednią zależność związaną z niższym wymaganie dotyczące wersji - [#759](https://github.com/NuGet/Home/issues/759)

* Usunięcie projektu zamyka odpowiednie okno interfejsu użytkownika, ale zmiana nazwy projektu nie powoduje zmiany nazwy w oknie interfejsu użytkownika. Należy pamiętać, że PMC nasłuchuje do zmiany nazwy projektu i projektu zdarzeń remove - [#670](https://github.com/NuGet/Home/issues/670)

* [Willow obciążenia sieci Web] Tworzenie Razor v3 WSP zawiesza się - [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalowanie/przywracania danego pakietu nie powiedzie się z "Pakiet zawiera wiele plików nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Małe litery, identyfikatory & `packages.config` scenariuszy — [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2] Przywracanie pakietu nie można przywrócić pakietów "starszych" - [#3208](https://github.com/NuGet/Home/issues/3208)

* Pakiet nuget dodaje wymuszone .TT — pliki do folderu zawartości, niezależnie od tego, co - [#3203](https://github.com/NuGet/Home/issues/3203)

* pakiet aktualizacji aplikacji sieci web platformy ASP.NET generuje ostrzeżenie związane z pliku: źródło - [#3194](https://github.com/NuGet/Home/issues/3194)

* Pakiet nuget w pliku csproj (przy użyciu `project.json`) ulega awarii, jeśli istnieją nie packOptions i właściciela w pliku JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* Pakiet nuget dla `project.json` ignoruje packOptions tagów, takich jak podsumowanie, autorów, właściciele itd - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Pakiet NuGet ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Trwa aktualizowanie wielu pakietów przy użyciu wycofywania pozostawia projektu w stanie uszkodzenia - [#3139](https://github.com/NuGet/Home/issues/3139)

* Pliki w żadnej nie są dodawane dla projektów netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Nie można utworzyć pakietu biblioteki przeznaczonych dla platformy .net Standard nieprawidłowo — [#3108](https://github.com/NuGet/Home/issues/3108)

* Plik -> Nowy Projekt -> Projekt Biblioteka klas (przenośna) kończy się niepowodzeniem w programie VS2015 i Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Błąd nuGet — 1.0.0-* nie jest prawidłowym ciągiem wersji - [#3070](https://github.com/NuGet/Home/issues/3070)

* Znajdź pakietu nie powiedzie się do wyświetlania, ale działa Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Błąd podczas "Jquery.validation Install-Package" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Nieprawidłowa docelowa ścieżka — domyślnie pakiet nuget xproj [#3060](https://github.com/NuGet/Home/issues/3060)

* Gdy zainstalowanego programu VS 2015 z aktualizacją 3 przy użyciu, których używa NuGet, występuje błąd wersji 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* "Zablokowany przez packages.config" `project.json` (systemu Windows UWP, przez kompilację zintegrowane) projekt — [#3046](https://github.com/NuGet/Home/issues/3046)

* Aktualizowanie interfejsu wiersza polecenia dotnet instalowane przez skryptu kompilacji w celu preview2-003121, czyli kompilacji oficjalnych preview2. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Interfejs użytkownika Menedżera pakietów: nie jest wyświetlany po zaktualizowaniu pakietu nowej wersji — [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey w wierszu polecenia delete nie odczytu/wysyłane 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Niepoprawny ciąg: stabilną wersję pakietu nie powinien mieć na zależność wersji wstępnej. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Pamięć podręczna OptimizedZipPackage pozostawia puste foldery - [#3029](https://github.com/NuGet/Home/issues/3029)

* Tworzenie projektu PCL (net46 i systemu windows 10) — get NullRef wyjątku. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizacja Nuget należy podać komunikat informacyjny w przypadku nowsza wersja jest ograniczony przez ograniczenie allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemy dotyczące przywracania v3 Nuget — [#2891](https://github.com/NuGet/Home/issues/2891)

* Wtyczka poświadczeń został zakończony z powodu błędu -1 / wystąpił błąd podczas pobierania pakietu podczas używania dostawcy poświadczeń z wielu źródeł - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` Przywracanie pakietów nuget powoduje ponowną kompilację, gdy nie trwa zmianie - [#2817](https://github.com/NuGet/Home/issues/2817)

* Pakiety symboli nie powinna być nigdy używane w instalacji lub aktualizacji — [#2807](https://github.com/NuGet/Home/issues/2807)

* Program VS nie obsługuje zmiennych środowiskowych w repositoryPath (nie nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Etykieta tagować elementy interfejsu użytkownika w interfejsie użytkownika Menedżera pakietów dla ułatwień dostępu — [#2745](https://github.com/NuGet/Home/issues/2745)

* Przenośne platformy przy użyciu profilów podzielonym są odrzucane. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Menedżer pakietów NuGet powinny było jasne, że listy opcji w pakietach szczegółów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe wypychane/delete nie używać klucza interfejsu API — [#2627](https://github.com/NuGet/Home/issues/2627)

* Usunąć zablokowanej właściwości z pliku blokady - [#2379](https://github.com/NuGet/Home/issues/2379)

* Aktualizacji NuGet 3.3.0 kończy się niepowodzeniem z "… dodatkowe ograniczenia zdefiniowane w pliku packages.config zapobiega tej operacji." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalowanie pakietu ze źródła lokalnego, która nie istnieje zgłasza sfałszowany komunikat o — [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "Dostępne dla uaktualnienie" przedstawia uaktualnień, które narusza ograniczenie wersji - [#1094](https://github.com/NuGet/Home/issues/1094)

* Nie można zaktualizować pakiety natywne - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funkcje

* Obsługuje ustawienie CopyLocal FALSE na odwołania dodane przez NuGet — [#329](https://github.com/NuGet/Home/issues/329)

* nuget.exe obsługę programu MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Obsługa pakietu.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Wyłączanie akcji przez użytkownika w przypadku akcji użytkownika wykonywane- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet należy dodać obsługę `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Dodaj możliwości framework Brak nuget 2.x, (które są już 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Obsługa folderów rezerwowego pakietu — [#2899](https://github.com/NuGet/Home/issues/2899)

* Projektowanie i implementowanie pojęcie typ pakietu do obsługi pakiety narzędzia - [#2476](https://github.com/NuGet/Home/issues/2476)

* Dodawanie interfejsu API, aby pobrać ścieżkę do folderu globalnymi pakietami - [#2403](https://github.com/NuGet/Home/issues/2403)

* Włącz SemVer 2.0.0 w pakiecie - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>DCRs

* wypychane nuget.exe — parametr limitu czasu nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)

* Tekst opisu pakietu powinien być możliwy - [#1769](https://github.com/NuGet/Home/issues/1769)

* Włącz nuget.exe pozwalające utworzyć `.props` i `.targets` pliki `.nuproj` projektów [#2711](https://github.com/NuGet/Home/issues/2711)

* Dodawanie rozszerzeń interfejsu API, aby porównać platform z import - [#2633](https://github.com/NuGet/Home/issues/2633)

* Ukryj opcje zależność, korzystając z `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Wydrukować nuget.exe nagłówka wersji w szczegółowe dane wyjściowe — [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet musi powiadomić użytkowników, że uaktualnienie/instalowanie tfm dotnet, na podstawie PCL może to spowodować problemy — [#3138](https://github.com/NuGet/Home/issues/3138)

* Ostrzegaj zły instalacja/Aktualizacja projektu z elementu tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Rozwiązywanie problemów z wydajnością z NuGet i ReShaper aktualizacji — [#3044](https://github.com/NuGet/Home/issues/3044)

* Dodanie obsługi netcoreapp11 i netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Assemblymetadata — Wykorzystaj atrybut `.nuspec` token zamiany - [#2851](https://github.com/NuGet/Home/issues/2851)
