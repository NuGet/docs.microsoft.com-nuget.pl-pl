---
title: Informacje o wersji narzędzia NuGet 5,9
description: Informacje o wersji programu NuGet 5,9, w tym nowe funkcje, poprawki błędów i DCR.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859581"
---
# <a name="nuget-59-release-notes"></a>Informacje o wersji narzędzia NuGet 5,9

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,9](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> zainstalowano z programem Visual Studio 2019 przy użyciu obciążenia .NET Core
  
> [!NOTE]
> Programy Visual Studio 16,9, MSBuild 16,9 i .NET 5.0.3 + wymagają NuGet.exe 5,9 lub nowszego.

## <a name="summary-whats-new-in-59"></a>Podsumowanie: co nowego w 5,9

* Dodaj element menu kontekstowego "Update" dla zależności pakietu, które uruchamiają interfejs użytkownika Menedżera pakietów z wstępnie wybranymi pakietami do aktualizacji — [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Kliknij prawym przyciskiem myszy pakiet "Update".](media/releasenotes-59-update.png)

* Pokaż żądaną wersję (w tym przepływaną wersję lub żądanie zakresu wersji) w kolumnie "wersja" listy projektów w interfejsie użytkownika Menedżera pakietów na poziomie rozwiązania — [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Żądana wersja w interfejsie użytkownika Menedżera pakietów na poziomie rozwiązania](media/releasenotes-59-requested-version.png)

* Sugestie dotyczące pakietu rozszerzenia intellicode w karcie przeglądania interfejsu użytkownika Menedżera pakietów wydanej w ramach testu A/B- [#10053](https://github.com/NuGet/Home/issues/10053)

* Rozwiń `.nupkg.metadata` plik, aby uwzględnić Źródło instalacji — [#10354](https://github.com/NuGet/Home/issues/10354)

* Wprowadź nową właściwość MSBuild, aby wykluczyć dane wyjściowe kompilacji dla określonych TFMs podczas wykonywania zadania w pakiecie — [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**DCR (żądanie zmiany projektu):**

* Ikona w dół, gdy Najnowsza wersja pakietu jest zainstalowana nie jest intuicyjna. Stary zielony znacznik był idealnym [#9789](https://github.com/NuGet/Home/issues/9789)

* Poziom szczegółowości debugowania NuGet powinien powiedzieć, gdzie pakiet pochodzi z- [#3055](https://github.com/NuGet/Home/issues/3055)

* Pakiet NuGet powinien przechwycić błędne pominięcie kropki w numerze wersji — [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM] Wyłącz Przypinanie centralnych zależności przechodnich — [#10132](https://github.com/NuGet/Home/issues/10132)

* NET5 TFM: Wystąpił błąd podczas tworzenia brakującej TPV- [#9441](https://github.com/NuGet/Home/issues/9441)

* Contenthash pakietu dziennika podczas rejestrowania przywracania (podczas wyodrębniania) — [#10384](https://github.com/NuGet/Home/issues/10384)

* Zaimplementuj mechanizm przed rejestracją dla starszych projektów żądania ściągnięcia, które wywołują przywracanie w rozwiązaniu z otwartym [#9986](https://github.com/NuGet/Home/issues/9986)

* Zalecane jest, aby zalecenie dotyczące pakietu NuGet działało, gdy w Menedżerze pakietów wybrano więcej niż jedno źródło — [#10433](https://github.com/NuGet/Home/issues/10433)

* Podczas przywracania z normalną szczegółowością należy rejestrować źródło, z którego jest przywracany pakiet- [#10461](https://github.com/NuGet/Home/issues/10461)

**Błędy:**

* INuGetPackageFileService — Pobieraj obrazy i osadzone licencje dla Codespaces — połączone i autonomiczne — [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: IProjectMetadataContextInfo brak programu formatującego [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM-perf] Zmniejsz informacje zapisywane do centralTransitiveDependencyGroups — [#10002](https://github.com/NuGet/Home/issues/10002)

* Operacje przywracania, które są zgłaszane z powodu nieładowania projektu, są raportowane jako `NoOp` dane telemetryczne [#9985](https://github.com/NuGet/Home/issues/9985)

* Ikony z niektórymi paletami kolorów powodują awarię interfejsu użytkownika PM w programie VS- [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM-perf] Zmniejsz klon PackageSpec podczas dodawania informacji o CPVM — [#10003](https://github.com/NuGet/Home/issues/10003)

* Interfejs użytkownika PM — ładowanie ikony asyncify — [#10009](https://github.com/NuGet/Home/issues/10009)

* Opóźnienie interfejsu użytkownika podczas ładowania ikon adresów URL w interfejsie użytkownika PM — [#8505](https://github.com/NuGet/Home/issues/8505)

* Koligacja wątku w wątkach interfejsu użytkownika BitmapSource i WPF — [#9161](https://github.com/NuGet/Home/issues/9161)

* Ostrzeżenie dla NU5128 ostrzegawczego, gdy packastool z aliasem TargetFramework- [#10097](https://github.com/NuGet/Home/issues/10097)

* Logika OutputPath w elementach docelowych pakietu w niestandardowej kompilacji nie działa prawidłowo — [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: pamięć podręczna IServiceBroker wystąpienia na kliencie [#10141](https://github.com/NuGet/Home/issues/10141)

* Tworzenie NuGetProjectActions na potrzeby odinstalowywania z interfejsu użytkownika PM, operacja równoległa — [#9956](https://github.com/NuGet/Home/issues/9956)

* Wydajność: redukcja UIDelays w GetPackageSpecsAsync dla starszych projektów i projektów innych niż żądania PR — [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` nie wypychanie więcej niż jednego pliku [#4393](https://github.com/NuGet/Home/issues/4393)

* Dane wyjściowe są opakowane o 80 znaków w macOS po przekierowaniu [#10198](https://github.com/NuGet/Home/issues/10198)

* Przywracanie nie powiodło się z <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406) -Source

* netcoreapp 5.0 — system Windows nie wykonuje rundy i nie analizuje informacji o platformie — [#10177](https://github.com/NuGet/Home/issues/10177)

* Niestandardowe projekty CPS wymagają możliwości projektu AssemblyReferences w celu przywrócenia. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Funkcja sprawdzania istnienia pliku licencji i ikony powinna zawsze używać porównania z uwzględnieniem wielkości liter [#9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference powoduje, że trudno jest przyczynić się do niedziałania projektów No-op/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)

* Trudno zobaczyć pole linia kreskowana formatu pakietu podczas nawigowania po karcie w oknie dialogowym "Wybieranie formatu Menedżera pakietów NuGet" w motywie ciemnym — [#9729](https://github.com/NuGet/Home/issues/9729)

* Wyklucz odwołania do struktury przechodniej z `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Właściwości statyczne porównujące powinny być idempotentne- [#10339](https://github.com/NuGet/Home/issues/10339)

* Rozwiązywanie ładowania zestawu kontraktów wewnętrznych (Fix RPS pliku lub Get Exception) — [#9919](https://github.com/NuGet/Home/issues/9919)

* Zastąp GetService with GetServiceAsync w NuGet. Klienci, część 1 — [#10362](https://github.com/NuGet/Home/issues/10362)

* Instalacje interfejsu wiersza polecenia nie powinny instalować pakietów nieznajdujących się na liście — [#7466](https://github.com/NuGet/Home/issues/7466)

* Statyczne przywracanie grafu MSBuild-unnnecessary rejestrowanie informacji o MSBuildStartupDirectory- [#10335](https://github.com/NuGet/Home/issues/10335)

* Zależności projektu zawierających oznaczone jako PrivateAssets nie powinny być zawarte w zablokowaniu Zablokuj do dnia — [#8565](https://github.com/NuGet/Home/issues/8565)

* Projekty zestawu SDK z nieprawidłowymi danymi, które nie pokazują błędów przywracania w programie VS- [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 podczas przywracania rozwiązania, które ma mieszane starsze i netstandard2e projekty z wiersza polecenia cmd z zablokowanym trybem [#9623](https://github.com/NuGet/Home/issues/9623)

* Pakiet zawiera zawartość przeprowadzoną przez pakiety zależności do pakietu bieżącego projektu (tylko projekty oparte na zestawie SDK) — [#8867](https://github.com/NuGet/Home/issues/8867)

* Dodaj telemetrię dla błędów interfejsu API rozszerzalności programu NuGet VS — [#10062](https://github.com/NuGet/Home/issues/10062)

* Dodaj GenerateRestoreGraphFile do statycznego przywracania wykresu, aby zwiększyć możliwość debugowania.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Nie można otworzyć Menedżera pakietów NuGet — [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/Narrator nie odczytuje etykiety "License" dla linku "Apache-2,0" — [#10425](https://github.com/NuGet/Home/issues/10425)

* Komunikat paska stanu z aktualną datą nie jest dobry w programie VS- [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.json używa nieprawidłowej struktury docelowej — [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces: napraw dane telemetryczne z https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* Błąd NU1004 znika podczas kompilowania rozwiązania po włączeniu "RestoreLockedMode" — [#8973](https://github.com/NuGet/Home/issues/8973)

* Przechodzenie do następnego [#10234](https://github.com/NuGet/Home/issues/10234) kierunku przez PMUI

* Debugowanie PMUI w wystąpieniu eksperymentalnym czasami zgłasza InvalidCastException z SolutionView do ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)

* Wersja domyślna to null po kliknięciu przestarzałego pakietu na karcie Przeglądaj — [#10380](https://github.com/NuGet/Home/issues/10380)

* Menedżer NuGet w programie Visual Studio zostanie ponownie załadowany po odzyskanie fokusu — [#4176](https://github.com/NuGet/Home/issues/4176)

* Usuń IPackageSourceProvider2 i powiązane typy — [#10098](https://github.com/NuGet/Home/issues/10098)

* Pakiet "NameOfPackage" jest niezgodny ze strukturami "All" w projekcie — [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync wykonuje niepotrzebne porównania NuGetVersion- [#10436](https://github.com/NuGet/Home/issues/10436)

* Pakiet NuGet. Klient powinien zastąpić użycie elementu ManagedImageMonikers z KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)

* Przestarzała ikona pokrywa się z wersją przestarzałego pakietu na karcie Przeglądaj — [#10452](https://github.com/NuGet/Home/issues/10452)

* Obsługa błędów PackageReference NU1604 różni się w zależności od programu VS i wiersza polecenia (Przywracanie & interfejsie użytkownika Menedżera pakietów) — [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces: nie zarejestrowano wymaganych elementów formatujących — [#10467](https://github.com/NuGet/Home/issues/10467)

* Usuń net45 jako platformę docelową z NuGet. Frameworks- [#10470](https://github.com/NuGet/Home/issues/10470)

* Implementacja — Dodaj nowe telemetrii do śledzenia zdarzeń związanych z użyciem kryteriów PMC i programu PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* Tylko jeden pakiet jest wyświetlany w oknie Podgląd zmian, jeśli dostępnych jest wiele pakietów do zaktualizowania w interfejsie użytkownika Menedżera pakietów — [#10483](https://github.com/NuGet/Home/issues/10483)

* Puste grupy frameworkReferences powinny być generowane w przypadku projektów wieloobiektowych z opakowaniami — [#10218](https://github.com/NuGet/Home/issues/10218)

* Trudno zobaczyć, że pole wyboru pakietu na karcie "aktualizacje" jest skoncentrowane na polu linii kreskowej podczas nawigowania po karcie w kolorze niebieskim/niebieskim (dodatkowy kontrast) motywy/Light — [#8963](https://github.com/NuGet/Home/issues/8963)

* Pola wyboru karty aktualizacje nie działają poprawnie z czytnikami ekranu — [#10449](https://github.com/NuGet/Home/issues/10449)

* Aktualizacja w PMUI powoduje, że odwołanie do obiektu nie jest ustawione na wystąpienie obiektu [#9882](https://github.com/NuGet/Home/issues/9882)

* Implementacja — Dodaj nowe telemetrii do śledzenia zdarzeń związanych z zastosowaniem kryteriów PMC i programu PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Błąd kopiowania/wklejania w V2FeedPackageInfo — [#10480](https://github.com/NuGet/Home/issues/10480)

* NuGetPackageFileService Fix — Użyj polecenia using dla jednorazowej elementu MemoryStream- [#10503](https://github.com/NuGet/Home/issues/10503)


**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Lista zatwierdzeń w tej wersji — 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy, że wszyscy Współautorzy, którzy pomogą Ci w udostępnieniu tej wersji NuGet!

|Którzy|Żądań ściągnięcia|Problemy|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Błąd kopiowania/wklejania w V2FeedPackageInfo — [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Brak testów dla przypadków, w których pakiety są przywoływane z atrybutem PrivateAssets = "All"- [#10397](https://github.com/NuGet/Home/issues/10397)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Dodawanie obsługi wypychania wielu pakietów — [#4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Kompilacja bibliotek NuGet jest uszkodzona, gdy podpisywanie zestawu jest wyłączone — [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Wyczyść dokumenty z udziałami — [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Funkcja sprawdzania istnienia pliku licencji i ikony powinna zawsze używać porównania z uwzględnieniem wielkości liter [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Użyj BitmapCreateOptions. IgnoreColorProfile do obejścia problemu WPF podczas korzystania z DecodePixelWidth- [#10037](https://github.com/NuGet/Home/issues/10037)
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Łącze Windows SDK 10 zostało przerwane w narzędziu NuGet. Przewodnik po udziale klienta — [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Linki względne zostały przerwane w programie NuGet. Przewodnik po debugowaniu klienta — [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Ulepszanie osprzętu testów i powiązanego kodu — [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Dane wyjściowe są opakowane o 80 znaków w macOS po przekierowaniu [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Udostępnienie NuGet. PackageManagement jako pakietu .NET Standard — [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Wprowadź nową właściwość MSBuild, aby wykluczyć dane wyjściowe kompilacji dla określonych TFMS podczas wykonywania zadania w pakiecie — [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="feedback-welcome"></a>Opinie — Zapraszamy!

Twoja opinia jest dla nas ważna.  Jeśli występują problemy z tą wersją, zapoznaj się z naszymi problemami dotyczącymi usługi [GitHub](https://github.com/NuGet/Home/issues) i [społeczności deweloperów programu Visual Studio](https://developercommunity.visualstudio.com/) .  W przypadku nowych problemów w programie NuGet Zgłoś problem z usługą [GitHub](https://github.com/NuGet/Home/issues/new).
Aby zapoznać się z ogólnymi problemami dotyczącymi środowiska NuGet, poinformuj nas o opcji " [Zgłoś problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " znajdującej się w ulubionym środowisku IDE w obszarze **Pomoc > Zgłoś problem**.
