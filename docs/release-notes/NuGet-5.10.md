---
title: Informacje o wersji nuGet 5.10
description: Informacje o wersji dla programu NuGet 5.10, w tym nowe funkcje, poprawki błędów i dcrs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356540"
---
# <a name="nuget-510-release-notes"></a>Informacje o wersji nuGet 5.10

Pojazdy dystrybucji NuGet:

| Wersja nuGet | Dostępne w Visual Studio wersji | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Zainstalowane</sup> z programem Visual Studio 2019 z obciążeniem .NET Core
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10 i .NET 5.0.300+ wymagają programu NuGet.exe 5.10 lub nowszego.

## <a name="summary-whats-new-in-510"></a>Podsumowanie: Co nowego w programie 5.10

* Podpisywanie: implementowanie polecenia dotnet trusted-signers — [#8053](https://github.com/NuGet/Home/issues/8053)

* Wyłącz domyślną weryfikację w systemie Linux, ale włącz ją domyślnie w systemie Windows — [#10713](https://github.com/NuGet/Home/issues/10713)

* Dodawanie zmiennej ENV do weryfikacji podpisywania pakietów na platformie .NET 5+ Linux/MAC [— #10742](https://github.com/NuGet/Home/issues/10742)

* Poprawianie wydajności instalacji nowych pakietów dla dużych rozwiązań [— #10166](https://github.com/NuGet/Home/issues/10166)

* Dodaj typ projektu `nfproj` do listy supportedProjectExtensions dla interfejsu wiersza polecenia nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Pomijanie <requireLicenseAcceptance> elementu podczas pakowania projektu — [#5133](https://github.com/NuGet/Home/issues/5133)

* Ostrzeżenie o wersji zapoznawczej [CPVM] powinno być wyświetlane w interfejsie wiersza polecenia dotnet [— #10226](https://github.com/NuGet/Home/issues/10226)

* Zaktualizuj tokeny koloru tła i pierwszego planu dla uwierzytelniania PMUI na CommonDocumentColors — [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash] Błąd "Operacja anulowana przez użytkownika" jest pokazywana w oknie Lista błędów podczas szybkiego przełączania między kartami w interfejsie użytkownika PM — [#10671](https://github.com/NuGet/Home/issues/10671)

* Interfejs użytkownika PM: Poprawianie wydajności instalacji pakietu na poziomie rozwiązania — [#10210](https://github.com/NuGet/Home/issues/10210)

* Zastąp getservice z GetServiceAsync wszędzie w NuGet.Clients — [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe wydajności pakietu z `..` ścieżką względną [— #5016](https://github.com/NuGet/Home/issues/5016)

* Wydajność "pakietu nuget" spada wraz ze wzrostem poziomów w ścieżkach źródłowych — [#5706](https://github.com/NuGet/Home/issues/5706)

* NuGet doesn't error when packaging nuspec with duplicate files (NuGet nie zwraca błędu podczas pakowania nuspec ze zduplikowanymi plikami). - [#6941](https://github.com/NuGet/Home/issues/6941)

* Pakiet NuGet "Określonego zestawu DateTimeOffset nie można przekonwertować na znacznik czasu pliku zip" — [#7001](https://github.com/NuGet/Home/issues/7001)

* Znaczniki czasu pliku spakowanego pakietu są przesunięte o strefę czasową [— #7395](https://github.com/NuGet/Home/issues/7395)

* Nu1004 powinien zawierać więcej informacji z akcjami [— #7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash] [Test Failure] Pusty/źle sformułowany plik blokady nie powinien być aktualizowany w przypadku uruchamiania pliku "dotnet restore --use-lock-file --locked-mode" — [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange umożliwia analizowanie logicznie nieprawidłowych zakresów — [#9145](https://github.com/NuGet/Home/issues/9145)

* Interfejs użytkownika PM nie może wyświetlać wyróżniających się kolorów tła między wybranymi i najechanym kursorem źródeł pakietów [—](https://github.com/NuGet/Home/issues/9538) #9538

* Pole wyboru wyboru wyboru wyboru projektów do zainstalowania nie jest odczytywane przez czytnik zawartości ekranu — [#9578](https://github.com/NuGet/Home/issues/9578)

* Domyślną domyślną wartością listy rozwijanej Wersje okienka szczegółów powinna być Zainstalowana/NajnowszaStable na kartach Zainstalowane/Aktualizacje — [#9887](https://github.com/NuGet/Home/issues/9887)

* Usuń konto obejścia dla niektórych zestawów SDK .NET 5, które zgłaszają element TargetPlatformMoniker ` ,Version= ` #9913  -  [](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify is too quiet - #10316 (Sprawdzanie dotnet nuget jest [zbyt #10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange nie może analizowania zakresów jednocyfrowych [— #10342](https://github.com/NuGet/Home/issues/10342)

* Menedżer rozwiązań programu VS zgłasza wyjątek o wartości null podczas debugowania [— #10352](https://github.com/NuGet/Home/issues/10352)

* Przenoszenie komunikatów o wyjątkach interfejsu wiersza polecenia do plików zasobów ciągu [— #10392](https://github.com/NuGet/Home/issues/10392)

* Usuwanie niechybnego kodu (TabItemButtonAutomationPeer) — [#10435](https://github.com/NuGet/Home/issues/10435)

* Menu kontekstowe aktualizacji powinno zostać przewinąć do pierwszego wybranego [elementu — #10498](https://github.com/NuGet/Home/issues/10498)

* Szczegóły PMUI rozwiązania mają nakładający się pasek poziomy [— #10533](https://github.com/NuGet/Home/issues/10533)

* Podpisywanie: szczegóły podpisu podstawowego nie są wyświetlane, gdy certyfikat wygasł i sygnatura czasowa jest niezaufana — [#10535](https://github.com/NuGet/Home/issues/10535)

* Brak włączonych źródeł uniemożliwia wyświetlanie interfejsu użytkownika PM — [#10541](https://github.com/NuGet/Home/issues/10541)

* Metadane pakietu (szczegóły, wycofana) czasami nie są ściągane z nuget.org CodeSpaces [—](https://github.com/NuGet/Home/issues/10549) #10549

* Inicjowanie PMUI kończy się niepowodzeniem z wyjątkiem podczas sesji debugowania [— #10559](https://github.com/NuGet/Home/issues/10559)

* Przywracanie nuget powoduje niepowodzenie sprawdzania integralności pakietu w big endian systemu — [#10567](https://github.com/NuGet/Home/issues/10567)

* Zamiast wyjątek PackagingException jest zgłaszany wyjątek FormatException [— #10595](https://github.com/NuGet/Home/issues/10595)

* CPVM — problemy ze współbieżnością w algorytmie chybienia grafu — [#10598](https://github.com/NuGet/Home/issues/10598)

* Dodawanie telemetrii wersji programu PowerShell dla pmc [— #10609](https://github.com/NuGet/Home/issues/10609)

* Poprawianie wydajności sortowania w wersji NuGetVersion [— #10611](https://github.com/NuGet/Home/issues/10611)

* Dodanie zaufanych podpisujących ma niespójne argumenty [— #10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 w wersji 16.9.0: przełączanie kart w programie NuGet Menedżer pakietów z "Aktualizacje" na "Zainstalowane" nie aktualizuje ramki. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Usuń "v" z numeru wersji w pmui — [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync zgłasza wyjątek przed otrzymaniem nominacji systemu projektu CPS — [#10681](https://github.com/NuGet/Home/issues/10681)

* Osadzone ikony powodują odmowę dostępu ze źródła "pakiety Microsoft Visual Studio offline" na karcie Przeglądaj [—](https://github.com/NuGet/Home/issues/10687) #10687

* INuGetProjectService.GetInstalledPackagesAsync zgłasza wyjątek, gdy ścieżka MSBuildProjectExtensionsPath nie jest ustawiona [— #10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget blokuje wątek threadpool w metodzie asynchronicznej, wywołując synchroniczne wywołanie wątku interfejsu użytkownika — [#10775](https://github.com/NuGet/Home/issues/10775)

* Narzędzia -> Opcje -> NuGet Menedżer pakietów ciąg jest obcięty — [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` jest niechybny kod i wydajność jest [zaniona — #10790](https://github.com/NuGet/Home/issues/10790)

* Używanie osadzonej ikony w pakietach zestawu NuGet SDK [— #10795](https://github.com/NuGet/Home/issues/10795)

* Aktualizowanie listy licencji SPDX [— #10806](https://github.com/NuGet/Home/issues/10806)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Lista zatwierdzeń w tej wersji — 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy wszystkim współautorom, którzy pomogli w wytwórzeniu tej wersji NuGet!

|Który|Prs|Problemy|
|----|----|----|
[luizja z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange nie może analizowania zakresów jednocyfrowych [— #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | Niedziała build.sh NuGet.Client — [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | Niedziała build.sh NuGet.Client — [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Wydajność "pakietu nuget" spada wraz ze wzrostem poziomów w ścieżkach źródłowych — [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe z wydajnością pakietu. ścieżka względna [— #5016](https://github.com/NuGet/Home/issues/5016)
[dojdą do 2017 r.](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM — problemy ze współbieżnością w algorytmie chybienia grafu — [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Dodaj typ projektu nfproj do listy supportedProjectExtensions dla interfejsu wiersza polecenia nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Opinie powitane

Twoja opinia jest dla nas ważna.  Jeśli w tej wersji występują jakiekolwiek problemy, zapoznaj się z naszymi problemami usługi [GitHub](https://github.com/NuGet/Home/issues) [i Visual Studio Developer Community](https://developercommunity.visualstudio.com/) istniejących problemów.  W przypadku nowych problemów w ramach narzędzia NuGet zgłoś problem [w usłudze GitHub.](https://github.com/NuGet/Home/issues/new)
W przypadku ogólnych problemów ze środowiskami NuGet daj nam znać za pośrednictwem opcji Zgłoś [problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) w ulubionym idee w obszarze Pomoc **> Zgłoś problem.**
