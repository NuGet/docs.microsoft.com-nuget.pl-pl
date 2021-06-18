---
title: Informacje o wersji nuGet 5.9
description: Informacje o wersji dla programu NuGet 5.9, w tym nowe funkcje, poprawki błędów i dcr.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 1152af99cf1421918a42d0d1faa33f1452f54a8f
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323885"
---
# <a name="nuget-59-release-notes"></a>Informacje o wersji nuGet 5.9

Pojazdy dystrybucji NuGet:

| Wersja nuGet | Dostępne w Visual Studio wersji | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Zainstalowano</sup> z programem Visual Studio 2019 z obciążeniem .NET Core
  
> [!NOTE]
> Visual Studio 16.9, MSBuild 16.9 i .NET 5.0.200+ NuGet.exe 5.9 lub nowsze.

## <a name="summary-whats-new-in-59"></a>Podsumowanie: Co nowego w 5.9

* Dodawania elementu menu kontekstowego "Aktualizuj" dla zależności pakietów, które uruchamiają interfejs użytkownika Menedżer pakietów z wstępnie wybranymi pakietami do zaktualizowania — [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Środowisko aktualizacji pakietu klikane prawym przyciskiem myszy](media/releasenotes-59-update.png)

* Pokaż żądaną wersję (w tym wersję zmienną lub żądanie zakresu wersji) w kolumnie "Wersja" na liście projektów na poziomie rozwiązania Menedżer pakietów interfejsu użytkownika — [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Żądana wersja w interfejsie użytkownika Menedżer pakietów rozwiązania](media/releasenotes-59-requested-version.png)

* Sugestie pakietu IntelliCode na karcie przeglądania interfejsu Menedżer pakietów użytkownika wydane jako test A/B [—](https://github.com/NuGet/Home/issues/10053) #10053

* Rozszerzanie `.nupkg.metadata` pliku o źródło instalacji — [#10354](https://github.com/NuGet/Home/issues/10354)

* Wprowadź nową właściwość msbuild, aby wykluczyć dane wyjściowe kompilacji dla określonych tfmów podczas zadania pakietu — [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Kontrolery domeny (żądanie zmiany projektu):**

* Ikona ikony w dół po zainstalowaniu najnowszej wersji pakietu nie jest intuicyjna. Stary zielony znacznik był idealny [— #9789](https://github.com/NuGet/Home/issues/9789)

* Szczegółowość debugowania nuget powinna powiedzieć, skąd pochodzi pakiet — [#3055](https://github.com/NuGet/Home/issues/3055)

* Pakiet NuGet powinien przechwycić niepoprawne pomijanie kropki w numerach wersji [— #9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Wyłączanie przypinania centralnych zależności przechodniej — [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: błąd podczas braku protokołu TPV [— #9441](https://github.com/NuGet/Home/issues/9441)

* Zawartość pakietu dziennikahash podczas rejestrowania przywracania (podczas wyodrębniania) [— #10384](https://github.com/NuGet/Home/issues/10384)

* Implementowanie mechanizmu wstępnej rejestracji dla starszych projektów pr pr, które wywołują przywracanie w otwartym [rozwiązaniu](https://github.com/NuGet/Home/issues/9986) — #9986

* Program polecania pakietów NuGet powinien działać po wybraniu więcej niż jednego źródła w menedżerze pakietów — [#10433](https://github.com/NuGet/Home/issues/10433)

* Podczas przywracania z normalnym poziomem szczegółowości należy rejestrować źródło, z którego jest przywracany [pakiet](https://github.com/NuGet/Home/issues/10461) — #10461

**Błędy:**

* INuGetPackageFileService — pobieranie obrazów i osadzonych licencji dla połączonych i autonomicznych usług Codespaces — [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: Brakujący program formatujący IProjectMetadataContextInfo — [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Zmniejsz informacje zapisywane w grupach centralTransitiveDependencyGroup — [#10002](https://github.com/NuGet/Home/issues/10002)

* Operacje przywracania, które są zgłaszane z powodu nie załadowanego projektu, są zgłaszane jako w `NoOp` telemetrii [— #9985](https://github.com/NuGet/Home/issues/9985)

* Ikony z pewnymi paletami kolorów powodują awarię interfejsu użytkownika PM VS — [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Zmniejsz liczbę klonów PackageSpec podczas dodawania informacji OPVM [— #10003](https://github.com/NuGet/Home/issues/10003)

* Interfejs użytkownika PM — asynchroniczne ładowanie ikon [— #10009](https://github.com/NuGet/Home/issues/10009)

* Opóźnienie interfejsu użytkownika podczas ładowania adresów URL ikon w interfejsie użytkownika pm — [#8505](https://github.com/NuGet/Home/issues/8505)

* Koligacja wątku w wątkach interfejsu użytkownika BitmapSource i WPF — [#9161](https://github.com/NuGet/Home/issues/9161)

* Ostrzeżenie dotyczące ostrzeżenia NU5128 w przypadku narzędzia packastool z aliasem targetframework — [#10097](https://github.com/NuGet/Home/issues/10097)

* Logika OutputPath w docelowych pakietach w dostosowanej kompilacji nie działa prawidłowo [—](https://github.com/NuGet/Home/issues/9234) #9234

* VS OE: buforowanie wystąpienia IServiceBroker na kliencie [— #10141](https://github.com/NuGet/Home/issues/10141)

* Tworzenie akcji NuGetProjectActions do odinstalowania z interfejsu użytkownika pm jako operacji równoległej — [#9956](https://github.com/NuGet/Home/issues/9956)

* Wydajność: zmniejsz liczbę elementów UIDelay w parametrze GetPackageSpecsAsync w przypadku starszych projektów i projektów innych [niż](https://github.com/NuGet/Home/issues/9953) projekty #9953

* ``dotnet nuget push *.nupkg`` nie wypycha więcej niż jednego pliku [— #4393](https://github.com/NuGet/Home/issues/4393)

* Dane wyjściowe są opakowane w 80 znaków w systemie macOS po przekierowaniu — [#10198](https://github.com/NuGet/Home/issues/10198)

* Przywracanie kończy się niepowodzeniem z #9406 <Relative Path>  -  [](https://github.com/NuGet/Home/issues/9406)

* Netcoreapp5.0-windows nie zaokrągla i nie analizuje informacji o platformie [—](https://github.com/NuGet/Home/issues/10177) #10177

* Niestandardowe projekty CPS wymagają możliwości projektu AssemblyReferences w celu przywrócenia. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Sprawdzanie istnienia pliku licencji i ikony powinno zawsze używać porównania z wielkością liter — [#9817](https://github.com/NuGet/Home/issues/9817)

* Przywracanie DotnetCLiToolReference utrudnia wnioskowanie o liczby projektów bezoperacji/uptodateprojectscount — [#10038](https://github.com/NuGet/Home/issues/10038)

* Trudne do zobaczenia pole wiersza łącznika w formacie pakietu podczas nawigowania po karcie za pomocą okna dialogowego "Wybieranie formatu Menedżer pakietów NuGet" w motywie ciemnym [—](https://github.com/NuGet/Home/issues/9729) #9729

* Wykluczanie odwołań do struktury przechodniej `CollectFrameworkReferences`  -  [z #10314](https://github.com/NuGet/Home/issues/10314)

* Właściwości statyczne porównujące powinny być idempotentne [— #10339](https://github.com/NuGet/Home/issues/10339)

* rozwiązywanie problemów z ładowaniem zestawu kontraktów wewnętrznych (naprawianie rps lub uzyskiwanie wyjątku) — [#9919](https://github.com/NuGet/Home/issues/9919)

* Zastąp element GetService elementem GetServiceAsync w nuGet.Clients, część 1 [— #10362](https://github.com/NuGet/Home/issues/10362)

* Instalacje interfejsu wiersza polecenia nie powinny instalować pakietów nieznajdych się na [liście — #7466](https://github.com/NuGet/Home/issues/7466)

* Przywracanie statycznego grafu msbuild — rejestrowanie unnnecessary dotyczące obiektu MSBuildStartupDirectory — [#10335](https://github.com/NuGet/Home/issues/10335)

* Zależności projektu ProjectReferences oznaczone jako PrivateAssets nie powinny być uwzględniane w aktualnym sprawdzaniu pliku blokady [—](https://github.com/NuGet/Home/issues/8565) #8565

* Projekty zestawu SDK ze złymi danymi, które nie pokazują błędów przywracania w programie VS [— #10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 podczas przywracania rozwiązania, które ma mieszane projekty Legacy i netstandard2 z wiersza polecenia z trybem LockedMode — [#9623](https://github.com/NuGet/Home/issues/9623)

* Pakiet zawiera zawartość wprowadzono za pośrednictwem pakietów zależności do pakietu bieżącego projektu (tylko projekty oparte na zestawie SDK) [—](https://github.com/NuGet/Home/issues/8867) #8867

* Dodawanie danych telemetrycznych dla błędów interfejsu API rozszerzalności programu VS nuGet [— #10062](https://github.com/NuGet/Home/issues/10062)

* Dodaj plik GenerateRestoreGraphFile w przywróceniu wykresu statycznego, aby zwiększyć możliwości debugowania.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Nie można otworzyć menedżera pakietów NuGet [— #10336](https://github.com/NuGet/Home/issues/10336)

* Urządzenie NVDA/Narrator nie odczytuje etykiety "License" dla linku "Apache-2.0" — [#10425](https://github.com/NuGet/Home/issues/10425)

* Aktualny komunikat na pasku stanu nie jest doskonały w programie VS [— #9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jsużywa nieprawidłowej struktury docelowej — [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: naprawianie danych telemetrycznych https://github.com/NuGet/NuGet.Client/pull/3786  -  [z #10439](https://github.com/NuGet/Home/issues/10439)

* Błąd NU1004 znika podczas tworzenia rozwiązania po włączeniu trybu "RestoreLockedMode" — [#8973](https://github.com/NuGet/Home/issues/8973)

* Tabulatory za pomocą PMUI w odwrotnym kierunku powinny być dublowane w kierunku do przodu [— #10234](https://github.com/NuGet/Home/issues/10234)

* Debugowanie wystąpienia PMUI w wystąpieniu eksperymentalnym czasami zgłasza wyjątek InvalidCastException z obiektu SolutionView do widoku ProjectView [— #10416](https://github.com/NuGet/Home/issues/10416)

* Wersja domyślna ma wartość null po kliknięciu przestarzałego pakietu na karcie Przeglądaj — [#10380](https://github.com/NuGet/Home/issues/10380)

* Menedżer NuGet w programie Visual Studio ponownie po odzyskaniu fokusu — [#4176](https://github.com/NuGet/Home/issues/4176)

* Usuń typy IPackageSourceProvider2 i powiązane — [#10098](https://github.com/NuGet/Home/issues/10098)

* Pakiet "NameOfPackage" jest niezgodny z platformami "all" w projekcie — [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync nie tworzy niepotrzebnych porównań NuGetVersion [— #10436](https://github.com/NuGet/Home/issues/10436)

* NuGet.Client powinien zastąpić użycie funkcji ManagedImageMonikers za pomocą funkcji KnownMonikers — [#9977](https://github.com/NuGet/Home/issues/9977)

* Przestarzała ikona nakłada się na wersję przestarzałego pakietu na karcie Przeglądaj [—](https://github.com/NuGet/Home/issues/10452) #10452

* Obsługa błędów PackageReference NU1604 różni się w programie VS i wierszu polecenia (interfejs & Menedżer pakietów interfejsu użytkownika) — [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: niezbędne nierejestrowane formatery [— #10467](https://github.com/NuGet/Home/issues/10467)

* Usuń platformę net45 jako platformę docelową z nuGet.Frameworks — [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementacja — dodawanie nowych telemetrii w celu śledzenia zdarzeń związanych z użyciem usługi PMC i programu PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Tylko jeden pakiet jest wyświetlony w oknie Podgląd zmian, gdy w interfejsie użytkownika usługi Menedżer pakietów dostępnych jest wiele pakietów — [#10483](https://github.com/NuGet/Home/issues/10483)

* Pusta frameworkReferences grupy powinny być generowane podczas pakowania projektów wielozadaniowych — [#10218](https://github.com/NuGet/Home/issues/10218)

* Trudno zobaczyć pole wyboru pakietu na karcie "Aktualizacje" koncentruje się na polem kreski podczas nawigowania po karcie [](https://github.com/NuGet/Home/issues/8963) w motywach niebieski/niebieski (dodatkowy kontrast)/jasnych — #8963

* Pola wyboru karty Aktualizacje nie działają dobrze w przypadku czytników zawartości ekranu [— #10449](https://github.com/NuGet/Home/issues/10449)

* Aktualizacja w pmui powoduje, że odwołanie do obiektu nie jest ustawione na wystąpienie obiektu — [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementacja — dodawanie nowych telemetrii w celu śledzenia zdarzeń związanych z monitorowaniem użycia pmc i programu Powershell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Błąd kopiowania i wklejania w V2FeedPackageInfo [— #10480](https://github.com/NuGet/Home/issues/10480)

* Poprawka nuGetPackageFileService — używanie w przypadku strumienia pamięci jednorazowej — [#10503](https://github.com/NuGet/Home/issues/10503)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Lista zatwierdzeń w tej wersji — 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy wszystkim współautorom, którzy pomogli w wytwórzeniu tej wersji NuGet!

|Który|Prs|Problemy|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Błąd kopiowania i wklejania w V2FeedPackageInfo [— #10480](https://github.com/NuGet/Home/issues/10480)
[dojdą do 2017 r.](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Brak testów w przypadku, gdy pakiety są przywołyowane za pomocą atrybutu PrivateAssets="All" — [#10397](https://github.com/NuGet/Home/issues/10397)
[dojdą do 2017 r.](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Dodawanie obsługi wypychania wielu pakietów — [#4393](https://github.com/NuGet/Home/issues/4393)
[dojdą do 2017 r.](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Kompilacja bibliotek NuGet jest uszkodzona, gdy podpisywanie zestawu jest wyłączone [—](https://github.com/NuGet/Home/issues/10173) #10173
[do 2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Czyszczenie dokumentów współtwojących — [#10399](https://github.com/NuGet/Home/issues/10399)
[David z cykadem](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Sprawdzanie obecności pliku licencji i ikony powinno zawsze używać porównania z wielkością liter — [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Użyj funkcji BitmapCreateOptions.IgnoreColorProfile, aby obejść problem z WPF w przypadku korzystania z metody DecodeCodeelWidth [— #10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK 10 w przewodniku NuGet.Client Contribution guide - [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Linki względne są uszkodzone w przewodniku debugowania NuGet.Client [— #10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Ulepszanie poprawek testów i powiązanego kodu [— #9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Dane wyjściowe są opakowane w 80 znaków w systemie macOS po przekierowaniu — [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Udostępnij pakiet NuGet.PackageManagement jako .NET Standard pakietu — [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Wprowadzenie nowej właściwości programu msbuild w celu wykluczenia danych wyjściowych kompilacji dla określonych tfms podczas zadania pakietu — [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Podsumowanie: co nowego w programie 5.9.1

* "dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)
* Wyłącz domyślną weryfikację w systemie Linux, ale włącz ją domyślnie w systemie Windows — [#10713](https://github.com/NuGet/Home/issues/10713)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Lista zatwierdzeń w tej wersji — 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="known-issues"></a>Znane problemy

### <a name="nuget-59-pack-raises-null-reference-exception---10685"></a>Pakiet nuget 5.9 zgłasza `Null Reference` wyjątek. - [#10685](https://github.com/NuGet/Home/issues/10685)

#### <a name="issue"></a>Problem
W przypadku używania pliku wersja zgłasza wyjątek, jeśli określono jawne odwołania do zestawu bez dodawania żadnych dla `pack` `.nuspec` projektów `NuGet 5.9` `null reference` [](../reference/nuspec.md#explicit-assembly-references) `reference groups` docelowych `multiple frameworks` .

#### <a name="workaround"></a>Obejście
Użyj `nuget.exe` [wersji 5.8.1](https://dist.nuget.org/win-x86-commandline/v5.8.1/nuget.exe)  lub najnowszej innej niż `5.9.1` .

## <a name="feedback-welcome"></a>Opinie powitane

Twoja opinia jest dla nas ważna.  Jeśli występują problemy z tą wydaniem, zapoznaj się z naszymi problemami w usłudze [GitHub](https://github.com/NuGet/Home/issues) [i Visual Studio Developer Community,](https://developercommunity.visualstudio.com/) aby uzyskać informacje o istniejących problemach.  W przypadku nowych problemów w ramach narzędzia NuGet zgłoś problem [w usłudze GitHub.](https://github.com/NuGet/Home/issues/new)
W przypadku ogólnych problemów z programem NuGet daj nam znać za pośrednictwem opcji Zgłoś [problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) w ulubionym idee w obszarze **Pomoc > Zgłoś problem.**
