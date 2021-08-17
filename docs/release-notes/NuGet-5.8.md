---
title: NuGet wersji 5.8
description: Informacje o wersji dla NuGet 5.8, w tym nowe funkcje, poprawki błędów i dcr.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209933"
---
# <a name="nuget-58-release-notes"></a>NuGet wersji 5.8

NuGet pojazdów dystrybucji:

| NuGet wersji | Dostępne w Visual Studio wersji | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1 Zainstalowano</sup> z programem Visual Studio 2019 z obciążeniem .NET Core
  
> [!NOTE]
> Visual Studio 16.8, MSBuild 16.8 i .NET 5.0 wymagają NuGet.exe 5.8 lub nowszej.


## <a name="summary-whats-new-in-58"></a>Podsumowanie: Co nowego w 5.8
🎉 to pierwsza wersja, która oferuje pełną obsługę tworzenia i przywracania pakietów NuGet przeznaczonych dla platform **.NET 5.0** 🎉

* Przyspieszanie wyodrębniania nupkg przy użyciu narzędzia mmap/CreateFileMapping [— #9807](https://github.com/NuGet/Home/issues/9807)

* Wyświetlanie szczegółów luki w zabezpieczeniach pakietu w okienku szczegółów Menedżer pakietów interfejsu użytkownika — [#9850](https://github.com/NuGet/Home/issues/9850)

* Sprawdź podpisane NuGet pakietów za pomocą nowego [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) polecenia — [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) Obsługuje `--prerelease` opcję dodawania najnowszej wersji pakietu, w tym wersji wstępnych — [#4699](https://github.com/NuGet/Home/issues/4699)

* Wyszukiwanie pakietów w interfejsie wiersza polecenia za [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) pomocą polecenia [— #9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) Polecenie obsługuje `--verbosity` opcję — [#9600](https://github.com/NuGet/Home/issues/9600)

* Włącz optymalizację szybkiego No-Op przywracania dla projektów opartych na stylu csproj i packageReference w Visual Studio — [#9565](https://github.com/NuGet/Home/issues/9565)

* Operacje interfejsu Menedżer pakietów na poziomie rozwiązania, takie jak instalowanie pakietów i aktualizacje, są nawet 10 razy [szybsze](https://github.com/NuGet/Home/issues/6010) — #6010

* Kilka innych NuGet wydajności Visual Studio — [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Kontrolery domeny:**

* TFM .NET 5.0: reguły pierwszeństwa struktury — [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet nie należy wywnioskować wersji platformy z kropkami podczas analizowania obiektu TargetFramework [— #9842](https://github.com/NuGet/Home/issues/9842)

* Użyj targetFrameworkMoniker & TargetPlatformMoniker, aby wywnioskować struktury zamiast poszczególnych właściwości TFI, TFV, TPI i TPV — #9895 [](https://github.com/NuGet/Home/issues/9895)

* Aktualizacja `GetReferenceNearestTargetFrameworkTask()` w celu obsługi platform docelowych z platformami (takimi jak net5.0-windows) — [#9894](https://github.com/NuGet/Home/issues/9894)

* Interfejsy API interfejsów API Visual Studio .NET 5.0 [— #9650](https://github.com/NuGet/Home/issues/9650)

* Menedżer pakietów Interfejs użytkownika: Operacje konsolidowania lub aktualizowania pakietów nie powinny być blokowane z powodu błędów (obniżenie poziomu pakietu itp.) [—](https://github.com/NuGet/Home/issues/9224) #9224

* NuGet funkcje powinny być dostępne dla projektów, które mają tę możliwość; "PackageReferences" [— #9957](https://github.com/NuGet/Home/issues/9957)

* Pomijanie No-Op komunikatów przywracania w Visual Studio — [#6384](https://github.com/NuGet/Home/issues/6384)

**Błędy:**

* Konstruktor OutputWindowTextWriter nie powinien być wywoływany w wątku w tle [—](https://github.com/NuGet/Home/issues/9764) #9764

* Przywracanie podpisanych pakietów na procesorach Big Endian — [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger nie powinien wywołać metod ffinitized w konstruktorach MEF — [#9591](https://github.com/NuGet/Home/issues/9591)

* Usterka w NuGet. CommandLine.Console, `PrintJustified()` metoda [— #9737](https://github.com/NuGet/Home/issues/9737)

* Menedżer pakietów Przeciek pamięci interfejsu użytkownika podczas odśmiecania pamięci metadanych pakietu z powodu złego powiązania — [#9757](https://github.com/NuGet/Home/issues/9757)

* [Podpisywanie] Żadne ostrzeżenie nie jest wyświetlane na liście błędów podczas instalowania podpisanego pakietu w formacie packages.config w interfejsie użytkownika Menedżer pakietów — [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine.XPlat nie powinien mieć publicznych interfejsów API — [#9821](https://github.com/NuGet/Home/issues/9821)

* Zmniejsz poziom kontrowania zasobów w czasie ładowania rozwiązania spowodowany przez zablokowanie wątku w puli wątkowo z `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* W przypadku przywracania wiersza polecenia w przypadku wielu projektów docelowych NuGet powinny odczytywać informacje dotyczące struktury docelowej z kompilacji wewnętrznej [—](https://github.com/NuGet/Home/issues/9869) #9869

* Odczytywanie grafu identyfikatora środowiska uruchomieniowego za pomocą elementu TargetFrameworkInformation [— #9874](https://github.com/NuGet/Home/issues/9874)

* Statyczne przywracanie grafu jest niespójne w odniesieniu do właściwości CrossTargeting w porównaniu Visual Studio i regularnego przywracania MSBuild oceny — [#9881](https://github.com/NuGet/Home/issues/9881)

* W przypadku statycznego przywracania grafów w przypadku wielu projektów docelowych NuGet odczytać informacje dotyczące struktury docelowej z kompilacji wewnętrznej. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Zezwalaj `net5.0-platform` na załadowanie i przywrócenie projektów w Visual Studio — [#9863](https://github.com/NuGet/Home/issues/9863)

* Wyświetlanie rozwiązanej wersji w interfejsie Menedżer pakietów użytkownika — [#9826](https://github.com/NuGet/Home/issues/9826)

* Menedżer pakietów Interfejs użytkownika: Eksplorator rozwiązań nie pokazuje wszystkich NuGet zależności pakietu — [#9898](https://github.com/NuGet/Home/issues/9898)

* Aktualizowanie listy licencji SPDX [— #9946](https://github.com/NuGet/Home/issues/9946)

* Program VS 2019 ulega awarii po otwarciu przycisku Zarządzaj pakietami NuGet: ikona powoduje nieobsługiwany wyjątek w konwersio obrazu [— #9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging.Extraction wymaga ilmerge, aby wykluczyć Newtonsoft.Jsna - [#9966](https://github.com/NuGet/Home/issues/9966)

* Pakowanie za pomocą parametru ContinuePackingAfterGeneratingNuspec=false nie powinno się nie powieść, jeśli nie ma żadnych błędów [—](https://github.com/NuGet/Home/issues/9786) #9786

* Menedżer pakietów Interfejs użytkownika: Ikony nie odwracają kolorów poprawnie — [#10017](https://github.com/NuGet/Home/issues/10017)

* Niepoprawne liczby projektów dla aktualnych i No-Op w przywróceniu — [#10026](https://github.com/NuGet/Home/issues/10026)

* Używanie `/p:RestoreUseStaticGraphEvaluation=true` wyników w wartości nie może mieć wartości null — [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` przez pomyłkę używa aliasu dla projektów biblioteki WPF [— #10020](https://github.com/NuGet/Home/issues/10020)

* Menedżer pakietów Interfejs użytkownika: NullReferenceException, gdy walidacja podpisu kończy się niepowodzeniem [— #10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: nie używaj `object` typu dla wartości metadanych projektu — [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: zapisywanie źródeł pakietów w opcjach narzędzi spowoduje zastąpienie poświadczeń — [#9711](https://github.com/NuGet/Home/issues/9711)


**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Lista problemów w tej wersji — 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy wszystkim współautorom, którzy pomogli w NuGet tej wersji!

|KtoTo|Prs|Problemy|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Literówka w komunikacie o błędzie. "administator" zamiast "administrator" [— #9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet Pakiet z nieprawidłowym assemblyInformationalVersion raporty "opis jest wymagany" — [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` nie uwzględnia właściwości Branch i Commit — [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Kliknięcie kodu NU w Visual Studio listy błędów powinno przejść do [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/)  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Użyj "https://" podczas dodawania nowego źródła pakietu za pomocą Visual Studio opcji — [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problem z wydajnością na mono [— #9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Dodawanie obiektu TypeConverter dla klasy SemanticVersion — [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Podsumowanie: Co nowego w programie 5.8.1

* packages.config package.lock.jsużywa nieprawidłowej struktury docelowej w programie 5.8 — [#10257](https://github.com/NuGet/Home/issues/10257)

* 5.8 + 16.8 Nie można rozwiązać zależności przechodniego projektu podczas łączenia właściwości PackageReference i packages.config — [#10326](https://github.com/NuGet/Home/issues/10326)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Lista zatwierdzeń w tej wersji — 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Opinie powitane

Twoja opinia jest dla nas ważna.  Jeśli w tej wersji występują jakiekolwiek [](https://github.com/NuGet/Home/issues) problemy, sprawdź nasze GitHub i skontaktuj się z Visual Studio [Developer Community,](https://developercommunity.visualstudio.com/) aby uzyskać informacje o istniejących problemach.  W przypadku nowych problemów w NuGet zgłoś problem [z GitHub .](https://github.com/NuGet/Home/issues/new)
W przypadku ogólnych NuGet problemów, daj nam znać za pośrednictwem opcji Zgłoś [problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) w ulubionym idee w obszarze Pomoc > Zgłoś **problem.**