---
title: Informacje o wersji 3.5 Beta NuGet
description: Informacje o wersji programu NuGet 3.5 tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-release-notes"></a>Informacje o wersji 3.5 NuGet

[Informacje o wersji 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [— informacje o wersji RC NuGet 4.0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Poprawki błędów

* Pakiet nie używa MSBuild 14.1 na mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Aktualizacja nie wybierz pozycję najnowszej dostępnej wersji aktualizacji zamiast tego zaznacz bieżące zainstalowanej wersji — [#3498](https://github.com/NuGet/Home/issues/3498)

* Usuń awarii po prywatnej v2, MyGet źródła danych uwierzytelniania i kliknięcie przycisku "Pokaż x więcej wyników"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Komunikaty dziennika wydają się być w kolejności odwrotnej do interfejsu użytkownika — [#3446](https://github.com/NuGet/Home/issues/3446)

* Przywracanie Nuget v3.4.4 - zgłasza "format podanej ścieżki nie jest obsługiwany" - [#3442](https://github.com/NuGet/Home/issues/3442)

* CmdLine 3,6 NuGet w wersji beta nie honoruje - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* Powolne IKVM Nuget zainstalować na dużych projekt — [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe Update - Self przechowuje na aktualizowanie sam — [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 instalacji/przywracania z udziału UNC ma wydajności regresji z 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Błąd podczas instalowania Moq z interfejs zarządzania pakietami dla projektu net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Karta instalacji na poziomie rozwiązania nie wyświetla wersję pakietu - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` aktualizacji z karty zainstalowana utraci stan — [#3303](https://github.com/NuGet/Home/issues/3303)

* Pakiet NuGet w `.csproj` ignoruje element pustych plików w `.nuspec` pliku - [#3257](https://github.com/NuGet/Home/issues/3257)

* Projektów witryny sieci Web hostowanych w usługach IIS nie powinno powodować niepowodzenie — po ukończeniu przywracania [#3235](https://github.com/NuGet/Home/issues/3235)

* Poświadczenia nie są pobierane z pliku Nuget.Config, gdy punkt końcowy v3 przekierowuje do v2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Pakiet NuGet nie może rozpoznać zestawu podczas pobierania metadanych zestawu przenośnych - [#3128](https://github.com/NuGet/Home/issues/3128)

* Nie można odnaleźć Nuget `msbuild.exe` na Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* Pakiet nuget.exe nie zezwala na tagu wersji wstępnej, który rozpoczyna się od cyfry - [#1743](https://github.com/NuGet/Home/issues/1743)

* Instalacja pakietu nuget nie powiodło się na VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions filtru nie pracy na poziomie rozwiązania - [#333](https://github.com/NuGet/Home/issues/333)

* Przywracanie losowo kończy się niepowodzeniem z element o takim samym kluczem został już dodany. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nie można zainstalować Nuget.Common w `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Wyszukaj źródło V2 za pomocą interfejsu użytkownika, FindPackagesById jest wywoływana dwukrotnie dla każdego Identyfikatora - [#2517](https://github.com/NuGet/Home/issues/2517)

* Pakiety nie może zależeć od projektów - [#2490](https://github.com/NuGet/Home/issues/2490)

* Pakiet nuget.exe — Wyklucz jest udokumentowany, ale nie jest obsługiwana — [#2284](https://github.com/NuGet/Home/issues/2284)

* Problemy z powodu błędu wiadomości, gdy sekcję "pliki" `.nuspec` jest nieprawidłowy — [#1686](https://github.com/NuGet/Home/issues/1686)

* Wypychania zawsze wysyła cały pakiet dwa razy z uwierzytelniony źródła pakietów - [#1501](https://github.com/NuGet/Home/issues/1501)

* Żadne informacje nie podano, gdy wywoływanie nuget.exe *.csproj aktualizacji podczas projektu nie ma `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` Przywracanie nie ponów 5xx kodów stanu ze źródeł V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Dwie kropki w pliku src w `.nuspec` nie działa — [#2947](https://github.com/NuGet/Home/issues/2947)

* Przywracanie środowisko CoreCLR musi Ignoruj źródła danych za pomocą szyfrowania - [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe push Obsługa 403 - niepoprawnie monit o podanie poświadczeń — [#2910](https://github.com/NuGet/Home/issues/2910)

* Aktualizacja NuGet za pomocą Menedżera pakietów usuwa właściwości z `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio spróbuj załadować "NuGet.TeamFoundationServer14", ale zmiana nazwy biblioteki DLL "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)

* Menedżer pakietów interfejsu użytkownika nie wyświetla nowo zaktualizowanej wersji - [#2828](https://github.com/NuGet/Home/issues/2828)

* pakiet aktualizacji próby użycia pakietu, wersji, zamiast package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* nuget Przywracanie csproj powinien błąd Jeśli projekt nie jest przy użyciu narzędzia nuget (`packages.config` lub `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Błąd TFS "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego" podczas uaktualniania lub odinstalowywania, gdy rozwiązanie lub projekt jest powiązany z kontrolą źródła TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* pakiet aktualizacji nie uzyskać zależności pakietów niebędące - [#2724](https://github.com/NuGet/Home/issues/2724)

* Nie istnieje sposób ustawić poziom szczegółowości dzienniki dla akcji interfejsu użytkownika Menedżera pakietów Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfiguracja nuget projektu jest nieprawidłowy — VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource w `NuGetDefaults.Config` (`ProgramData\NuGet`) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)

* Wersja nuget 3.4.3 - pobieranie wartości nie może być pusty podczas kompilacji pakietu — [#2648](https://github.com/NuGet/Home/issues/2648)

* Przywracanie nie używa przechowywanych poświadczeń z pliku Nuget.Config dla źródła danych programu VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet przywracania] — configfile jest względem katalogu projektu zamiast cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Nadmierne alokacji w kodzie porównania wersji — [#2632](https://github.com/NuGet/Home/issues/2632)

* Wiele wystąpień nuget.exe spróbujesz zainstalować takie same pakietu w równoległych przyczyny zapisu podwójny - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informacje o zależnościach nie są buforowane dla wielu projektów operacji - [#2619](https://github.com/NuGet/Home/issues/2619)

* Instalowanie i pobierania pakietów aktualizacji bez sprawdzania folderu pakietów najpierw - [#2618](https://github.com/NuGet/Home/issues/2618)

* Jeśli lista źródła pakietu jest pusta, nie można dodać źródła pakietu za pośrednictwem interfejsu użytkownika (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Błąd błąd podczas próby zainstalowania pakietu, który jest zależny od czasu projektowania fasad - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalowanie pakietu z konsoli PackageManager, ustawienie "All" próbuje tylko pierwsze źródło - [#2557](https://github.com/NuGet/Home/issues/2557)

* Najnowszej wersji beta nie rozpakować ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 awarii podczas uruchamiania komputera z własnym wbudowanych NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Polecenie aktualizacji może być bardziej pełne i poproś go jako operacji.. - [#2418](https://github.com/NuGet/Home/issues/2418)

* Utworzony lokalnie VSIX powinny mieć te same biblioteki dll i plików jako elementu konfiguracji kompilacji. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Usuń NuGet obniżenia poziomu ostrzeżenia w kompilacji - [#2396](https://github.com/NuGet/Home/issues/2396)

* Nieudanych uwierzytelnień źródła pakietu (3 razy) jest zablokowana w nieskończoność - [#2362](https://github.com/NuGet/Home/issues/2362)

* Zawartość pakietu jest nie została poprawnie przywrócona podczas instalowania pakietu z v3.3 nuget + źródła danych z argumentem - NoCache, jeśli pakiet zawiera `.nupkg` pliki - [#2354](https://github.com/NuGet/Home/issues/2354)

* Nuget Install wszystkie źródła pakietów, ale brakuje 1 źródła pakietu nie powiodło się — [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Zainstaluj bloków, jeśli pojedyncze źródło odmawia autoryzacji - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Wersja zakresu powinny zastępować wersja - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Pakiet aktualizacji super powolna — "Próba zebrania informacji zależności" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Zmiany na NuGet ukrywana starszą wersję pakietu, gdy partii aktualizowanie zależnościami - [#1903](https://github.com/NuGet/Home/issues/1903)

* Aktualizacja nuget.exe porzuca silna nazwa zestawu i atrybut Private. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Względna ścieżka do pliku dla "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Poprawa komunikaty o błędach rozpoznawania — [#1373](https://github.com/NuGet/Home/issues/1373)

* pakiet aktualizacji w wersji 3 nie powiedzie się z pakietami nie znajduje się w określonym źródle - [#1013](https://github.com/NuGet/Home/issues/1013)

* Używanie ścieżek względnych dla źródła pakietu jest pozwala używać - [#865](https://github.com/NuGet/Home/issues/865)

* Brak zależności w pliku NUPKG generowane z projektu, jeśli istnieje już pośrednią zależność związaną z niższe wymagania dotyczące wersji - [#759](https://github.com/NuGet/Home/issues/759)

* Usuwanie projektu zamyka odpowiedniego okna interfejsu użytkownika, ale zmiana nazwy projektu nie powoduje zmiany nazwy okna interfejsu użytkownika. Należy pamiętać, że PMC nasłuchuje do zmiany nazwy projektu i projektu zdarzenia remove - [#670](https://github.com/NuGet/Home/issues/670)

* [Willow obciążenia sieci Web] Tworzenie Razor v3 WSP zawiesza się - [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalacja/przywracania określonego pakietu nie powiodło się "Pakiet zawiera wiele plików nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Małe litery identyfikatory & `packages.config` scenariusze - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2] Przywracanie pakietu nie powiedzie się pod kątem przywracania pakietów "starszych" - [#3208](https://github.com/NuGet/Home/issues/3208)

* Pakiet nuget dodaje wymuszone .TT — pliki do folderu zawartości bez względu na okoliczności - [#3203](https://github.com/NuGet/Home/issues/3203)

* pakiet aktualizacji aplikacji sieci web ASP.NET generuje ostrzeżenie związane z pliku: źródło - [#3194](https://github.com/NuGet/Home/issues/3194)

* csproj pakiet nuget (z `project.json`) ulega awarii, jeśli istnieją nie packOptions i właściciel w pliku JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* Pakiet nuget `project.json` ignoruje tagi packOptions podsumowanie, autorzy, właściciele itp - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Pakiet NuGet ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizowania wielu pakietów z wycofywania pozostawia projektu w stan przerwane — [#3139](https://github.com/NuGet/Home/issues/3139)

* Nie dodano pliki we wszystkich projektów krótkich nazw netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Nie można spakować biblioteki przeznaczonych dla platformy .net Standard poprawnie - [#3108](https://github.com/NuGet/Home/issues/3108)

* Plik -> Nowy Projekt -> projektu biblioteki klas (przenośna) kończy się niepowodzeniem w programie VS2015 i Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Błąd NuGet — 1.0.0-* nie jest prawidłowym ciągiem wersji - [#3070](https://github.com/NuGet/Home/issues/3070)

* Znajdź pakietu nie powiedzie się do wyświetlania, ale działa Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Błąd podczas "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Domyślnie pakiet nuget xproj ścieżkę docelową nieprawidłowy - [#3060](https://github.com/NuGet/Home/issues/3060)

* Gdy zainstalowanej wersji programu VS 2015 Aktualizacja 3 w wersji programu VS używane NuGet występuje błąd wersji 3.5.0 — [#3053](https://github.com/NuGet/Home/issues/3053)

* "Zablokowany w pliku packages.config" `project.json` (platformy uniwersalnej systemu Windows, nazywane również kompilacji zintegrowany) projektu - [#3046](https://github.com/NuGet/Home/issues/3046)

* Zaktualizuj dotnet zainstalowane za pomocą skryptu kompilacji do preview2-003121, czyli kompilacji oficjalnego preview2 interfejsu wiersza polecenia. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Pakiet interfejsu użytkownika Menedżera: nie są wyświetlane po zaktualizowaniu pakietu nowej wersji — [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey w wierszu polecenia delete nie odczytu/wysyłane 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć na zależność wersji wstępnej. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Pamięć podręczna OptimizedZipPackage pozostawia puste foldery - [#3029](https://github.com/NuGet/Home/issues/3029)

* Tworzenie PCL (net46 i windows 10) projektu get NullRef wyjątku. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizacja Nuget należy podać komunikat informacyjny w przypadku nowszej wersji jest ograniczony przez ograniczenie allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Problemy dotyczące przywracania v3 Nuget — [#2891](https://github.com/NuGet/Home/issues/2891)

* Dodatek poświadczeń został zakończony z powodu błędu -1 / błąd podczas pobierania pakietu podczas używania dostawcy poświadczeń z wielu źródeł - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` Przywracanie nuget powoduje ponowną kompilację, gdy nie zmienić - [#2817](https://github.com/NuGet/Home/issues/2817)

* Symbole pakietów nie należy nigdy używać w instalacji lub aktualizacji - [#2807](https://github.com/NuGet/Home/issues/2807)

* VS nie obsługuje zmiennych środowiskowych w repositoryPath (nie nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Etykieta bez etykiety elementy interfejsu użytkownika w interfejsie użytkownika Menedżera pakietów ułatwień dostępu - [#2745](https://github.com/NuGet/Home/issues/2745)

* Przenośne platformy przy użyciu profilów podzielonym są odrzucane. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Menedżer pakietów NuGet powinien stał się wyczyścić tej listy opcji w pakietach szczegółów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe wypychania lub usuń używać klucza API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Usuń właściwość locked z pliku blokady - [#2379](https://github.com/NuGet/Home/issues/2379)

* Aktualizacja NuGet 3.3.0 "... dodatkowe ograniczenie zdefiniowane w pliku packages.config uniemożliwia wykonanie tej operacji." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalowanie pakietu z lokalnego źródła, które nie istnieje zgłasza sfałszowany komunikat - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "Dostępne uaktualnienie" pokazuje uaktualnień, które narusza ograniczenie wersji - [#1094](https://github.com/NuGet/Home/issues/1094)

* Nie można zaktualizować oryginalne pakiety - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funkcje

* Obsługuje ustawienie CopyLocal FALSE na odwołania dodane przez narzędzie NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* Obsługa nuget.exe MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Obsługa pakietu.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Wyłączania akcja ze strony użytkownika, gdy jest wykonywana akcji użytkownika- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet należy dodać obsługę `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Dodaj brakujące w NuGet możliwości framework 2.x (które są już 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Obsługi rezerwowego pakietu folderów - [#2899](https://github.com/NuGet/Home/issues/2899)

* Projektowania i implementacji pojęcie typu pakietu do obsługi pakietów narzędzie - [#2476](https://github.com/NuGet/Home/issues/2476)

* Dodawanie interfejsu API można pobrać ścieżki do folderu pakietów globalne - [#2403](https://github.com/NuGet/Home/issues/2403)

* Włączanie programu SemVer 2.0.0 w pakiecie - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Dcr

* nuget.exe push - parametr limitu czasu nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)

* Tekst opisu pakiet powinien być możliwy - [#1769](https://github.com/NuGet/Home/issues/1769)

* Włącz nuget.exe do produkcji `.props` i `.targets` pliki `.nuproj` projekty [#2711](https://github.com/NuGet/Home/issues/2711)

* Dodawanie rozszerzeń interfejsu API można porównać struktury z importów - [#2633](https://github.com/NuGet/Home/issues/2633)

* Ukryj opcje zależności, korzystając z `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Wydrukować nagłówka wersji nuget.exe w szczegółowych danych wyjściowych - [#1887](https://github.com/NuGet/Home/issues/1887)

* Należy powiadomić użytkowników, że uaktualnienie/instalowanie tfm dotnet, na podstawie PCL może to spowodować problemy — NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* Ostrzegaj zły instalacja/aktualizacja dla projektu z tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Rozwiązywanie problemów z wydajnością z ReShaper i NuGet aktualizacji — [#3044](https://github.com/NuGet/Home/issues/3044)

* Dodawanie obsługi netcoreapp11 i netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Wykorzystywanie assemblymetadata — atrybut `.nuspec` token zamiany - [#2851](https://github.com/NuGet/Home/issues/2851)
