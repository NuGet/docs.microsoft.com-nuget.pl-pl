---
title: NuGet wersji 5.10
description: Informacje o wersji dla NuGet 5.10, w tym nowe funkcje, poprawki błędów i dcrs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726954"
---
# <a name="nuget-510-release-notes"></a>NuGet wersji 5.10

NuGet pojazdów dystrybucji:

| NuGet wersji | Dostępne w Visual Studio wersji | Dostępne w zestawach SDK platformy .NET |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1 Zainstalowane</sup> z programem Visual Studio 2019 z obciążeniem .NET Core
  
> [!NOTE]
> Visual Studio 16.10, MSBuild 16.10, a .NET 5.0.300+ wymaga NuGet.exe 5.10 lub nowszej.

## <a name="summary-whats-new-in-510"></a>Podsumowanie: co nowego w programie 5.10

* Podpisywanie: implementowanie polecenia dotnet trusted-signers — [#8053](https://github.com/NuGet/Home/issues/8053)

* Wyłącz domyślną walidację w systemie Linux, ale włącz ją domyślnie na Windows — [#10713](https://github.com/NuGet/Home/issues/10713)

* Dodawanie zmiennej ENV do weryfikacji podpisywania pakietów na platformie .NET 5+ Linux/MAC [— #10742](https://github.com/NuGet/Home/issues/10742)

* Poprawianie wydajności instalacji nowych pakietów dla dużych rozwiązań [— #10166](https://github.com/NuGet/Home/issues/10166)

* Dodaj typ projektu `nfproj` do listy supportedProjectExtensions dla interfejsu wiersza polecenia nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

* Pomijanie `<requireLicenseAcceptance>` elementu podczas pakowania projektu — [#5133](https://github.com/NuGet/Home/issues/5133)

* Ostrzeżenie o wersji zapoznawczej [CPVM] powinno być wyświetlane w interfejsie wiersza polecenia dotnet [— #10226](https://github.com/NuGet/Home/issues/10226)

* Zaktualizuj tokeny koloru tła i pierwszego planu dla pmui na CommonDocumentColors — [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash] Błąd "operacja anulowana przez użytkownika" jest wyświetlany w oknie Lista błędów podczas szybkiego przełączania między kartami w interfejsie użytkownika PM — [#10671](https://github.com/NuGet/Home/issues/10671)

* Interfejs użytkownika PM: Poprawianie wydajności instalacji pakietu na poziomie rozwiązania — [#10210](https://github.com/NuGet/Home/issues/10210)

* Zastąp getservice getservice getserviceasync wszędzie w NuGet. Klienci — [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe wydajności pakietu z `..` ścieżką względną [— #5016](https://github.com/NuGet/Home/issues/5016)

* Wydajność "pakietu nuget" spada wraz ze wzrostem poziomów w ścieżkach źródłowych — [#5706](https://github.com/NuGet/Home/issues/5706)

* NuGet nie występuje błąd podczas pakowania nuspec ze zduplikowanymi plikami. - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet "Określona wartość DateTimeOffset nie może zostać przekonwertowana na znacznik czasu pliku zip" [— #7001](https://github.com/NuGet/Home/issues/7001)

* Znaczniki czasu pliku spakowanego pakietu są przesunięte o strefę czasową [— #7395](https://github.com/NuGet/Home/issues/7395)

* Nu1004 powinien zawierać więcej informacji z akcjami [— #7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash] [Test Failure] Pusty/źle sformułowany plik blokady nie powinien być aktualizowany podczas uruchamiania dotnet restore --use-lock-file --locked-mode" [— #8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange umożliwia analizowanie logicznie nieprawidłowych zakresów — [#9145](https://github.com/NuGet/Home/issues/9145)

* Interfejs użytkownika PM nie może wyświetlać wyróżniających się kolorów tła między wybranymi i najechanym kursorem źródeł pakietów [—](https://github.com/NuGet/Home/issues/9538) #9538

* Pole wyboru wyboru wyboru wyboru projektów do zainstalowania nie jest odczytywane przez czytnik zawartości ekranu — [#9578](https://github.com/NuGet/Home/issues/9578)

* Opcja domyślna listy rozwijanej Wersje okienka szczegółów powinna być zainstalowana/najnowszaStable na kartach Zainstalowane/Aktualizacje — [#9887](https://github.com/NuGet/Home/issues/9887)

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

* Przywracanie nuget powoduje niepowodzenie sprawdzania integralności pakietu w big endian — [#10567](https://github.com/NuGet/Home/issues/10567)

* Zamiast wyjątek PackagingException jest zgłaszany wyjątek FormatException [— #10595](https://github.com/NuGet/Home/issues/10595)

* CPVM — problemy ze współbieżnością w algorytmie chybienia grafu — [#10598](https://github.com/NuGet/Home/issues/10598)

* Dodawanie telemetrii wersji programu PowerShell — [#10609](https://github.com/NuGet/Home/issues/10609)

* Poprawianie wydajności sortowania w wersji NuGetVersion [— #10611](https://github.com/NuGet/Home/issues/10611)

* Dodanie zaufanych podpisujących ma niespójne argumenty [— #10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 16.9.0: przełączanie kart w NuGet Menedżer pakietów z "Aktualizacje" na "Zainstalowane" nie aktualizuje ramki. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Usuń "v" z numeru wersji w pmui — [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync zgłasza wyjątek przed otrzymaniem nominacji systemu projektu CPS — [#10681](https://github.com/NuGet/Home/issues/10681)

* Osadzone ikony powodują odmowę dostępu ze źródła "pakiety Microsoft Visual Studio offline" na karcie Przeglądaj — [#10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService.GetInstalledPackagesAsync zgłasza wyjątek, gdy ścieżka MSBuildProjectExtensionsPath nie jest ustawiona [— #10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget blokuje wątek puli wątków w metodzie asynchronicznej, wywołując synchroniczne wywołanie wątku interfejsu użytkownika — [#10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` jest niechybny kod i wydajność jest zaniona [— #10790](https://github.com/NuGet/Home/issues/10790)

* Używanie osadzonej ikony w NuGet SDK — [#10795](https://github.com/NuGet/Home/issues/10795)

* Aktualizowanie listy licencji SPDX [— #10806](https://github.com/NuGet/Home/issues/10806)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Lista zatwierdzeń w tej wersji — 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Materiały przekazywane przez społeczność

Dziękujemy wszystkim współautorom, którzy pomogli w NuGet tej wersji!

|KtoTo|Prs|Problemy|
|----|----|----|
[luizja-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange nie może analizowania zakresów jednocyfrowych [— #10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. Klient build.sh uszkodzony — [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. Klient build.sh uszkodzony — [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Wydajność "pakietu nuget" spada wraz ze wzrostem poziomów w ścieżkach źródłowych — [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe z wydajnością pakietu. ścieżka względna [— #5016](https://github.com/NuGet/Home/issues/5016)
[z o.o.](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM — problemy ze współbieżnością w algorytmie chybienia grafu — [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Dodaj typ projektu nfproj do listy supportedProjectExtensions dla interfejsu wiersza polecenia nuget. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Opinie powitane

Twoja opinia jest dla nas ważna.  Jeśli występują problemy z tą wydaniem, zapoznaj się z naszymi GitHub i Visual Studio [Developer Community](https://developercommunity.visualstudio.com/) istniejących problemów. [](https://github.com/NuGet/Home/issues)  W przypadku nowych problemów NuGet zgłoś problem [z GitHub .](https://github.com/NuGet/Home/issues/new)
W przypadku ogólnych NuGet problemów, daj nam znać za pośrednictwem opcji Zgłoś [problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) w ulubionym idee w obszarze Pomoc **> Zgłoś problem.**
