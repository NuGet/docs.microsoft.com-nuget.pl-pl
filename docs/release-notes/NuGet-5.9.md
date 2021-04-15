---
title: Informacje o wersji nuGet 5.9
description: Informacje o wersji dla programu NuGet 5.9, w tym nowe funkcje, poprawki błędów i dcrs.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 50fd277a4f1f39b4a68a89cd07af4e21f0d3d831
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508816"
---
# <a name="nuget-59-release-notes"></a>Informacje o wersji nuGet 5.9

Pojazdy dystrybucji NuGet:

| Wersja nuGet | Dostępne w Visual Studio wersji | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.9.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.9.1**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.9](https://visualstudio.microsoft.com/downloads/) | [5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Zainstalowane</sup> z programem Visual Studio 2019 z obciążeniem .NET Core
  
> [!NOTE]
> Visual Studio 16.9, MSBuild 16.9 i .NET 5.0.200+ NuGet.exe 5.9 lub nowszej.

## <a name="summary-whats-new-in-59"></a>Podsumowanie: co nowego w programie 5.9

* Dodawania elementu menu kontekstowego "Aktualizuj" dla zależności pakietów, które uruchamiają interfejs użytkownika Menedżer pakietów z wstępnie wybranymi pakietami do zaktualizowania — [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Środowisko aktualizacji pakietu klikane prawym przyciskiem myszy](media/releasenotes-59-update.png)

* Pokaż żądaną wersję (w tym zmiennoprzecinkową wersję lub żądanie zakresu wersji) w kolumnie "Wersja" listy projektów na poziomie rozwiązania w interfejsie użytkownika Menedżer pakietów — [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Żądana wersja w interfejsie użytkownika Menedżer pakietów rozwiązania](media/releasenotes-59-requested-version.png)

* Sugestie pakietu IntelliCode na karcie przeglądania interfejsu Menedżer pakietów użytkownika wydane jako test A/B [—](https://github.com/NuGet/Home/issues/10053) #10053

* Rozszerz `.nupkg.metadata` plik, aby uwzględnić źródło instalacji [— #10354](https://github.com/NuGet/Home/issues/10354)

* Wprowadzenie nowej właściwości programu msbuild w celu wykluczenia danych wyjściowych kompilacji dla określonych tfmów podczas zadania pakietu — [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Kontrolery domeny (żądanie zmiany projektu):**

* Ikona ikony w dół po zainstalowaniu najnowszej wersji pakietu nie jest intuicyjna. Stary zielony znacznik był idealny [— #9789](https://github.com/NuGet/Home/issues/9789)

* Szczegółowość debugowania nuget powinna powiedzieć, skąd pochodzi pakiet — [#3055](https://github.com/NuGet/Home/issues/3055)

* Pakiet NuGet powinien przechwycić nieprawidłowe pominięcie kropki w numerach wersji [— #9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Wyłączanie przypinania centralnych zależności przechodniej — [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: błąd podczas braku protokołu TPV [— #9441](https://github.com/NuGet/Home/issues/9441)

* Zawartość pakietu dziennikahash podczas rejestrowania przywracania (podczas wyodrębniania) [— #10384](https://github.com/NuGet/Home/issues/10384)

* Implementowanie mechanizmu wstępnej rejestracji dla starszych projektów pr pr, które wywołują przywracanie w otwartym [rozwiązaniu](https://github.com/NuGet/Home/issues/9986) — #9986

* Program polecania pakietów NuGet powinien działać po wybraniu więcej niż jednego źródła w menedżerze pakietów [—](https://github.com/NuGet/Home/issues/10433) #10433

* Podczas przywracania z normalnym poziomem szczegółowości należy rejestrować źródło, z którego jest przywracany [pakiet](https://github.com/NuGet/Home/issues/10461) — #10461

**Błędy:**

* INuGetPackageFileService — pobieranie obrazów i osadzonych licencji dla usługi Codespaces połączonej i autonomicznej — [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: Brakujący program formatujący IProjectMetadataContextInfo — [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-Perf] Zmniejsz informacje zapisywane w grupach centralTransitiveDependencyGroup — [#10002](https://github.com/NuGet/Home/issues/10002)

* Operacje przywracania, które są zgłaszane z powodu nie załadowanego projektu, są zgłaszane jako operacje `NoOp` [telemetryczne — #9985](https://github.com/NuGet/Home/issues/9985)

* Ikony z pewnymi paletami kolorów powodują awarię interfejsu użytkownika pm w programie VS — [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-Perf] Zmniejsz liczbę klonów PackageSpec podczas dodawania informacji o protokole CPVM [— #10003](https://github.com/NuGet/Home/issues/10003)

* Interfejs użytkownika PM — asynchroniczne ładowanie ikon [— #10009](https://github.com/NuGet/Home/issues/10009)

* Opóźnienie interfejsu użytkownika podczas ładowania adresów URL ikon w interfejsie użytkownika PM [— #8505](https://github.com/NuGet/Home/issues/8505)

* Koligacja wątku w wątkach bitmapSource i interfejsu użytkownika WPF [— #9161](https://github.com/NuGet/Home/issues/9161)

* Ostrzeżenie dotyczące ostrzeżenia NU5128 w przypadku narzędzia packastool z aliasem targetframework — [#10097](https://github.com/NuGet/Home/issues/10097)

* Logika OutputPath w docelowych celach pakietu w niestandardowej kompilacji nie działa prawidłowo [—](https://github.com/NuGet/Home/issues/9234) #9234

* Vs OE: buforowanie wystąpienia IServiceBroker na kliencie [— #10141](https://github.com/NuGet/Home/issues/10141)

* Tworzenie akcji NuGetProjectActions do odinstalowywania z interfejsu użytkownika pm jako operacji równoległej — [#9956](https://github.com/NuGet/Home/issues/9956)

* Wydajność: zmniejszenie liczby elementów UIDelay w parametrze GetPackageSpecsAsync w przypadku starszych projektów i projektów innych niż projekty #9953 [](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` nie wypycha więcej niż jednego pliku [— #4393](https://github.com/NuGet/Home/issues/4393)

* Dane wyjściowe są opakowane w 80 znaków w systemie macOS po przekierowaniu — [#10198](https://github.com/NuGet/Home/issues/10198)

* Przywracanie kończy się niepowodzeniem z plikiem <Relative Path>  -  [-Source #9406](https://github.com/NuGet/Home/issues/9406)

* Netcoreapp5.0-windows nie zaokrągla i nie analizuje informacji o platformie [—](https://github.com/NuGet/Home/issues/10177) #10177

* Niestandardowe projekty CPS wymagają możliwości projektu AssemblyReferences w celu przywrócenia. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Sprawdzanie obecności pliku licencji i ikony powinno zawsze używać porównania z wielkością liter — [#9817](https://github.com/NuGet/Home/issues/9817)

* Przywracanie DotnetCLiToolReference utrudnia wnioskowanie o liczba/uptodateprojectscount projektów [](https://github.com/NuGet/Home/issues/10038) bez #10038

* Trudno zobaczyć pole wiersza łącznika formatu pakietu podczas nawigowania po karcie za pomocą okna dialogowego "Wybieranie formatu Menedżer pakietów NuGet" w obszarze Ciemny motyw [—](https://github.com/NuGet/Home/issues/9729) #9729

* Wykluczanie odwołań do struktury przechodniej `CollectFrameworkReferences`  -  [z #10314](https://github.com/NuGet/Home/issues/10314)

* Właściwości statyczne porównujące powinny być idempotentne [— #10339](https://github.com/NuGet/Home/issues/10339)

* rozwiązywanie problemów z ładowaniem zestawu kontraktów wewnętrznych (naprawianie rps lub uzyskiwanie wyjątku) [— #9919](https://github.com/NuGet/Home/issues/9919)

* Zastąp element GetService elementem GetServiceAsync w nuGet.Clients, część 1 [— #10362](https://github.com/NuGet/Home/issues/10362)

* Instalacje interfejsu wiersza polecenia nie powinny instalować pakietów nieznajdowych — [#7466](https://github.com/NuGet/Home/issues/7466)

* Przywracanie statycznego grafu msbuild — rejestrowanie bez aktualizacji dotyczące obiektu MSBuildStartupDirectory — [#10335](https://github.com/NuGet/Home/issues/10335)

* Zależności projektu ProjectReferences oznaczone jako PrivateAssets nie powinny być uwzględniane w aktualnym sprawdzaniu pliku blokady [—](https://github.com/NuGet/Home/issues/8565) #8565

* Projekty zestawu SDK ze złymi danymi, które nie pokazują błędów przywracania w programie VS — [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 podczas przywracania rozwiązania, które ma mieszane projekty Legacy i netstandard2 z wiersza polecenia z LockedMode — [#9623](https://github.com/NuGet/Home/issues/9623)

* Pakiet zawiera zawartość wprowadzono za pośrednictwem pakietów zależności do pakietu bieżącego projektu (tylko projekty oparte na zestawie SDK) [— #8867](https://github.com/NuGet/Home/issues/8867)

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

* Usuwanie IPackageSourceProvider2 i powiązanych typów [— #10098](https://github.com/NuGet/Home/issues/10098)

* Pakiet "NameOfPackage" jest niezgodny z platformami "all" w projekcie — [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync does unnecessary NuGetVersion Compares - [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet.Client powinien zastąpić użycie funkcji ManagedImageMonikers za pomocą funkcji KnownMonikers [— #9977](https://github.com/NuGet/Home/issues/9977)

* Przestarzała ikona nakłada się na wersję przestarzałego pakietu na karcie [Przeglądaj](https://github.com/NuGet/Home/issues/10452) — #10452

* Obsługa błędów PackageReference NU1604 różni się w programie VS i wierszu polecenia (interfejs & Menedżer pakietów) [—](https://github.com/NuGet/Home/issues/9289) #9289

* Codespaces: niezbędne nierejestrowane wymagane formatery [— #10467](https://github.com/NuGet/Home/issues/10467)

* Usuń platformę net45 jako platformę docelową z nuGet.Frameworks — [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementacja — dodawanie nowych telemetrii w celu śledzenia zdarzeń związanych z użyciem usługi PMC i programu PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Tylko jeden pakiet jest wyświetlony w oknie Podgląd zmian, jeśli w interfejsie użytkownika usługi Menedżer pakietów dostępnych jest [wiele](https://github.com/NuGet/Home/issues/10483) pakietów #10483

* Pusta frameworkReferences grupy powinny być generowane podczas pakowania projektów wielotargetowych — [#10218](https://github.com/NuGet/Home/issues/10218)

* Pole wyboru pakietu na karcie "Aktualizacje" jest trudne do sprawdzenia przy użyciu pola kreski podczas nawigowania po [](https://github.com/NuGet/Home/issues/8963) karcie w motywach niebieski/niebieski (dodatkowy kontrast)/jasnych — #8963

* Pola wyboru karty Aktualizacje nie działają dobrze w przypadku czytników zawartości ekranu [— #10449](https://github.com/NuGet/Home/issues/10449)

* Aktualizacja w PMUI powoduje, że odwołanie do obiektu nie jest ustawione na wystąpienie obiektu — [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementacja — dodawanie nowych telemetrii w celu śledzenia zdarzeń związanych z używaniem usługi PMC i programu PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Błąd kopiowania i wklejania w V2FeedPackageInfo [— #10480](https://github.com/NuGet/Home/issues/10480)

* Poprawka nuGetPackageFileService — używanie w przypadku strumienia pamięci jednorazowej — [#10503](https://github.com/NuGet/Home/issues/10503)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Lista zatwierdzeń w tej wersji — 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy wszystkim współautorom, którzy pomogli w dosyć świetnym wydaniu nuGet!

|Który|Prs|Problemy|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Błąd kopiowania i wklejania w V2FeedPackageInfo [— #10480](https://github.com/NuGet/Home/issues/10480)
[węzłochy-wsadowe](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Brak testów w przypadku, gdy pakiety są przywoływyne za pomocą atrybutu PrivateAssets="All" — [#10397](https://github.com/NuGet/Home/issues/10397)
[węzłochy-wsadowe](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Dodawanie obsługi wypychania wielu pakietów — [#4393](https://github.com/NuGet/Home/issues/4393)
[węzłochy-wsadowe](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Kompilacja bibliotek NuGet jest uszkodzona, gdy podpisywanie zestawu jest wyłączone [—](https://github.com/NuGet/Home/issues/10173) #10173
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Czyszczenie dokumentów współtwojących — [#10399](https://github.com/NuGet/Home/issues/10399)
[Zdavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Sprawdzanie obecności pliku licencji i ikony powinno zawsze używać porównania z wielkością liter — [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Użyj funkcji BitmapCreateOptions.IgnoreColorProfile, aby obejść problem Z WPF w przypadku korzystania z metody DecodePixelWidth [— #10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Windows SDK 10 w przewodniku NuGet.Client Contribution guide - [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Linki względne są uszkodzone w przewodniku debugowania NuGet.Client [— #10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Ulepszanie poprawek testów i powiązanego kodu [— #9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Dane wyjściowe są opakowane w 80 znaków w systemie macOS po przekierowaniu — [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Udostępnij pakiet NuGet.PackageManagement jako pakiet .NET Standard — [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Wprowadzenie nowej właściwości msbuild w celu wykluczenia danych wyjściowych kompilacji dla określonych tfms podczas zadania pakietu — [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="summary-whats-new-in-591"></a>Podsumowanie: Co nowego w 5.9.1

* "dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)
* Wyłącz domyślną walidację w systemie Linux, ale włącz ją domyślnie w systemie Windows — [#10713](https://github.com/NuGet/Home/issues/10713)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**

**[Lista zatwierdzeń w tej wersji — 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**

## <a name="feedback-welcome"></a>Opinie powitane

Twoja opinia jest dla nas ważna.  Jeśli w tej wersji występują jakiekolwiek problemy, zapoznaj się z naszymi problemami usługi [GitHub](https://github.com/NuGet/Home/issues) [i Visual Studio Developer Community,](https://developercommunity.visualstudio.com/) aby uzyskać informacje o istniejących problemach.  W przypadku nowych problemów w ramach narzędzia NuGet zgłoś problem [w usłudze GitHub.](https://github.com/NuGet/Home/issues/new)
W przypadku ogólnych problemów ze środowiskami NuGet daj nam znać za pomocą opcji Zgłoś [problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) w ulubionym idee w obszarze Pomoc > Zgłoś **problem.**
