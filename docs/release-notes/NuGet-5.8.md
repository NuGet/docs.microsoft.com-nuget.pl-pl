---
title: Informacje o wersji narzędzia NuGet 5,8
description: Informacje o wersji programu NuGet 5,8, w tym nowe funkcje, poprawki błędów i DCR.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 86e173b9d760578454df8f5f817533f64e193996
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550759"
---
# <a name="nuget-58-release-notes"></a>Informacje o wersji narzędzia NuGet 5,8

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> zainstalowano z programem Visual Studio 2019 przy użyciu obciążenia .NET Core
  
> [!NOTE]
> Programy Visual Studio 16,8, MSBuild 16,8 i .NET 5,0 wymagają NuGet.exe 5,8 lub nowszego.


## <a name="summary-whats-new-in-58"></a>Podsumowanie: co nowego w 5,8
🎉 **jest to pierwsza wersja, która oferuje pełną obsługę tworzenia i przywracania pakietów NuGet przeznaczonych dla platformy .net 5,0** 🎉

* Wyświetl szczegóły luk w zabezpieczeniach pakietu w okienku szczegółów pakietu interfejsu użytkownika Menedżera pakietów — [#9850](https://github.com/NuGet/Home/issues/9850)

* Sprawdź, czy podpisane pakiety NuGet z nowym [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) poleceniem [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) obsługuje `--prerelease` opcję dodania najnowszej wersji pakietu, w tym wersji wstępnej — [#4699](https://github.com/NuGet/Home/issues/4699)

* Wyszukaj pakiety w interfejsie wiersza [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) polecenia z poleceniem [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) Opcja obsługuje `--verbosity` [#9600](https://github.com/NuGet/Home/issues/9600)

* Włącz optymalizację funkcji Fast No-Op Restore dla projektów opartych na PackageReference w programie Visual Studio — [#9565](https://github.com/NuGet/Home/issues/9565)

* Operacje interfejsu użytkownika Menedżera pakietów na poziomie rozwiązania, takie jak instalacje i aktualizacje pakietów, są szybsze i 10X [#6010](https://github.com/NuGet/Home/issues/6010)

* Kilka innych ulepszeń wydajności NuGet w programie Visual Studio — [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**DCR**

* .NET 5,0 TFM: reguły pierwszeństwa platformy — [#9436](https://github.com/NuGet/Home/issues/9436)

* Pakiet NuGet nie powinien wywnioskować wersji platformy kropek podczas analizowania TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842)

* Użyj TargetFrameworkMoniker & TargetPlatformMoniker do wywnioskowania struktur zamiast używania poszczególnych TFI, TFV, TPI, TPV właściwości — [#9895](https://github.com/NuGet/Home/issues/9895)

* Aktualizacja `GetReferenceNearestTargetFrameworkTask()` umożliwiająca obsługę platform docelowych z platformami (takimi jak NET 5.0-Windows) — [#9894](https://github.com/NuGet/Home/issues/9894)

* Interfejsy API programu .NET 5,0 Visual Studio — [#9650](https://github.com/NuGet/Home/issues/9650)

* Interfejs użytkownika Menedżera pakietów: operacje konsolidacji lub aktualizacji pakietów nie powinny być blokowane z powodu błędów (obniżenie pakietów itp.) — [#9224](https://github.com/NuGet/Home/issues/9224)

* Funkcje NuGet powinny być jasne dla projektów, które mają możliwość; "Składnika packagereferences" — [#9957](https://github.com/NuGet/Home/issues/9957)

* Pomijanie No-Op przywracania komunikatów w programie Visual Studio — [#6384](https://github.com/NuGet/Home/issues/6384)

**Błędy:**

* Nie należy wywoływać konstruktora OutputWindowTextWriter w wątku w tle — [#9764](https://github.com/NuGet/Home/issues/9764)

* Przywróć podpisane pakiety na procesorach big endian — [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger nie powinna wywoływać metod koligacji w konstruktorach MEF- [#9591](https://github.com/NuGet/Home/issues/9591)

* Usterka w narzędziu NuGet. commandline. Console `PrintJustified()` — [#9737](https://github.com/NuGet/Home/issues/9737)

* Przeciek pamięci interfejsu użytkownika Menedżera pakietów, gdy metadane pakietu są zbierane jako elementy bezużyteczne ze względu na nieprawidłowe powiązanie — [#9757](https://github.com/NuGet/Home/issues/9757)

* Pisywać W Lista błędów podczas instalowania podpisanego pakietu przy użyciu formatu packages.config w interfejsie użytkownika Menedżera pakietów nie jest wyświetlane ostrzeżenie — [#9798](https://github.com/NuGet/Home/issues/9798)

* Pakiet NuGet. commandline. XPlat nie powinien mieć publicznych interfejsów API — [#9821](https://github.com/NuGet/Home/issues/9821)

* Zmniejszenie rywalizacji o zasoby w czasie ładowania rozwiązania spowodowanym zablokowaniem wątku wątków w puli za pomocą `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* W przypadku przywracania z użyciem wiersza polecenia z projektami z obsługą wiele obiektów NuGet powinien odczytać informacje dotyczące platformy docelowej powiązane z wewnętrzną kompilacją [#9869](https://github.com/NuGet/Home/issues/9869)

* Odczytaj Graf identyfikatora środowiska uruchomieniowego za poorednictwem elementu TargetFrameworkInformation — [#9874](https://github.com/NuGet/Home/issues/9874)

* Statyczne przywracanie wykresu jest niespójne w odniesieniu do właściwości CrossTargeting w porównaniu do programu Visual Studio i zwykłego przywrócenia oceny MSBuild — [#9881](https://github.com/NuGet/Home/issues/9881)

* W przypadku statycznego przywracania wykresu z projektami wielowymiarowymi pakiet NuGet powinien odczytać informacje dotyczące platformy docelowej powiązane z wewnętrzną kompilacją. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Zezwalaj na `net5.0-platform` ładowanie i przywracanie projektów w programie Visual Studio — [#9863](https://github.com/NuGet/Home/issues/9863)

* Wyświetl rozpoznaną wersję w interfejsie użytkownika Menedżera pakietów — [#9826](https://github.com/NuGet/Home/issues/9826)

* Interfejs użytkownika Menedżera pakietów: Eksplorator rozwiązań nie pokazuje wszystkich zależności pakietów NuGet — [#9898](https://github.com/NuGet/Home/issues/9898)

* Aktualizowanie listy licencji SPDX — [#9946](https://github.com/NuGet/Home/issues/9946)

* Awarie programu VS 2019 po otwarciu narzędzia do zarządzania pakietami NuGet: ikona powoduje nieobsłużony wyjątek w obrazie conversio — [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. pakowanie. wyodrębnianie wymaga ilmerge do wykluczenia Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* Pakowanie z ContinuePackingAfterGeneratingNuspec = false nie powinno kończyć się niepowodzeniem w przypadku braku błędów — [#9786](https://github.com/NuGet/Home/issues/9786)

* Interfejs użytkownika Menedżera pakietów: ikony nie są prawidłowo odwracające kolory — [#10017](https://github.com/NuGet/Home/issues/10017)

* Niepoprawna liczba projektów dla aktualnych i No-Opych projektów podczas przywracania [#10026](https://github.com/NuGet/Home/issues/10026)

* Użycie `/p:RestoreUseStaticGraphEvaluation=true` wyników w wartości nie może mieć wartości null- [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` błędne użycie aliasu dla projektów biblioteki WPF — [#10020](https://github.com/NuGet/Home/issues/10020)

* Interfejs użytkownika Menedżera pakietów: NullReferenceException, gdy Walidacja podpisu kończy się niepowodzeniem — [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces: nie używaj `object` typu dla wartości metadanych projektu — [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces: zapisywanie źródeł pakietów w opcjach narzędzi spowoduje zastąpienie poświadczeń — [#9711](https://github.com/NuGet/Home/issues/9711)


**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Lista problemów/zatwierdzeń rozwiązanych w tej wersji — 5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy, że wszyscy Współautorzy, którzy pomogą Ci w udostępnieniu tej wersji NuGet!

|Którzy|Żądań ściągnięcia|Problemy|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Literówka w komunikacie o błędzie. "Administrator" zamiast "Administrator" — [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Pakiet NuGet z nieprawidłowymi raportami AssemblyInformationalVersion "jest wymagany opis"- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` nie uwzględnia rozgałęzień i właściwości zatwierdzania — [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | Klikanie kodu ni w oknie programu Visual Studio Lista błędów powinien przejść do https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Użyj elementu "https://" podczas dodawania nowego źródła pakietu za pomocą opcji programu Visual Studio — [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` problem z wydajnością w programie mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Dodaj obiekt TypeConverter dla klasy SemanticVersion — [#9125](https://github.com/NuGet/Home/issues/9125)


## <a name="feedback-welcome"></a>Opinie — Zapraszamy!

Twoja opinia jest dla nas ważna.  Jeśli występują problemy z tą wersją, zapoznaj się z naszymi problemami dotyczącymi usługi [GitHub](https://github.com/NuGet/Home/issues) i [społeczności deweloperów programu Visual Studio](https://developercommunity.visualstudio.com/) .  W przypadku nowych problemów w programie NuGet Zgłoś problem z usługą [GitHub](hhttps://github.com/NuGet/Home/issues/new).
Aby zapoznać się z ogólnymi problemami dotyczącymi środowiska NuGet, poinformuj nas o opcji " [Zgłoś problem](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " znajdującej się w ulubionym środowisku IDE w obszarze **Pomoc > Zgłoś problem**.
