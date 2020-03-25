---
title: Informacje o wersji narzędzia NuGet 5,5
description: Informacje o wersji programu NuGet 5,5, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148298"
---
# <a name="nuget-55-release-notes"></a>Informacje o wersji narzędzia NuGet 5,5

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-55"></a>Podsumowanie: co nowego w 5,5

* Ulepszona obsługa ułatwień dostępu i czytnika ekranu dla interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio
    * Problemy z ułatwieniami dostępu w środowiskach odczytywania zawartości ekranu, brak altText i dostępnej nazwy dla zainstalowanego pola tekstowego itd.,- [#9059](https://github.com/NuGet/Home/issues/9059)
    * Problemy z ułatwieniami dostępu w programie odczytywanie zawartości ekranu na liście pakietów — [#9077](https://github.com/NuGet/Home/issues/9077)
    * Problemy z ułatwieniami dostępu w programie czytnika ekranu związane z kartami "Przeglądaj", "Zainstaluj" i "Aktualizuj" — [#9078](https://github.com/NuGet/Home/issues/9078)
    * Narrator nie ogłasza "puste", "No Dependencies", "NuGet. org", "MIT" etykiety łącza [#9157](https://github.com/NuGet/Home/issues/9157)

* Obsługa wbudowanych ikon samodzielnego umieszczania w interfejsie użytkownika Menedżera pakietów programu Visual Studio dla pakietów hostowanych w lokalnych źródłach danych — [#8189](https://github.com/NuGet/Home/issues/8189)

* Znacznie ulepszona wydajność przywracania No-op przy użyciu `RestoreUseStaticGraphEvaluation`, która przyspiesza Obliczanie przez wywoływanie interfejsów API programu MSBuild static Graph- [8791](https://github.com/NuGet/Home/issues/8791)

* Ulepszona niezawodność programu dotnet. exe z wtyczkami uwierzytelniania dla wielu platform
    * dotnet restore niepowodzenie z TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Wtyczka: "zadanie zostało anulowane" — problem z uwierzytelnianiem ADO z powodu tego elementu. - [#8528](https://github.com/NuGet/Home/issues/8528)

* Dodaj `dotnet nuget <add|remove|update|disable|enable|list> source` polecenie [#4126](https://github.com/NuGet/Home/issues/4126)

* Obsługę dla `--skip-duplicate` przy użyciu wypychania NuGet programu dotnet- [#8778](https://github.com/NuGet/Home/issues/8778)

* Obsługa `packages.config` przy użyciu programu MSBuild/Restore — [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Usterek**

* Współaktualizator z interfejsami API v3 — [#4197](https://github.com/NuGet/Home/issues/4197)

* Nieprawidłowa wersja zależności pakietu, jeśli w wersji zależności pakietu ustawiono wartość "*"- [#6697](https://github.com/NuGet/Home/issues/6697)

* ErrorUnsafePackageEntry komunikat o błędzie nie wskazuje źródła problemu — [#7505](https://github.com/NuGet/Home/issues/7505)

* Plik blokady nie jest uznawany za scenariusze "*" — [#8073](https://github.com/NuGet/Home/issues/8073)

* Program NuGet. exe nie jest rozpoznawany jako Najnowsza wersja pakietu, gdy jest używany program * w PackageReference (MSBuild/dotnet/przywracanie VS) — [#8432](https://github.com/NuGet/Home/issues/8432)

* pakiet listy dotnet z projektem WPF o wiele elementów docelowych — [#8463](https://github.com/NuGet/Home/issues/8463)

* Ulepsz ConcurrencyUtilities (Zmniejsz użycie procesora) — [#8653](https://github.com/NuGet/Home/issues/8653)

* Specyfikacja DG dla scenariuszy niezaładowanych projektów nie powinna być zapisywana w wersji zapoznawczej — [#8793](https://github.com/NuGet/Home/issues/8793)

* Pakiety NuGet programu Visual Studio (RestoreManagerPackage) muszą zostać automatyczne załadowane w zdarzeniach kompilacji rozwiązania — [#8796](https://github.com/NuGet/Home/issues/8796)

* Zakleszczenie w VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)

* Przybornik VisualStudio nie jest wypełniany w pakiecie NuGet, jeśli projekt jest umieszczony w folderze rozwiązania — [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: Przywracanie rozwiązania bezproblemowo nie powiodło się z powodu warunku wyścigu — [#8881](https://github.com/NuGet/Home/issues/8881)

* Stała "ładowanie.." na zainstalowanej karcie i "wyszukiwanie <term>.. "na karcie Aktualizacje — [#8890](https://github.com/NuGet/Home/issues/8890)

* Brak ikon osadzonych w interfejsie użytkownika programu VS PM po wygaśnięciu pamięci podręcznej — [#9069](https://github.com/NuGet/Home/issues/9069)

* Uruchamianie interfejsu użytkownika FireAndForget PM — [#9112](https://github.com/NuGet/Home/issues/9112)

* Instrukcja RESTORE: IncludeExcludeFiles. Equals (...) jest niepoprawna — [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore: PackageSpec. Clone () tworzy nierówny klon- [#9211](https://github.com/NuGet/Home/issues/9211)

* Pokazana Lista błędów mimo błędu "Zawsze pokazuj Lista błędów, jeśli kompilacja zakończy się z błędami" nie jest zaznaczona — [#8190](https://github.com/NuGet/Home/issues/8190)

* Statyczne przywracanie wykresu nie powinno przekazywać pustej SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)

* Przywróć: zamknięcie obliczone dla każdego projektu 4 razy — [#9042](https://github.com/NuGet/Home/issues/9042)

* Instrukcja RESTORE: DependencyGraphSpec. Load (...) nie wymaga JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Przywracanie: duże ciągi utworzone na stercie dużego obiektu (LOH) — [#9031](https://github.com/NuGet/Home/issues/9031)

* Niestandardowa NuGet. exe w nowszej wersji mono może ulec przerwaniu z powodu programu rozpoznawania SDK MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)

* Przywracanie kończy się niepowodzeniem, gdy plik NuGet. dgspec. JSON jest używany przez inny proces — [8692](https://github.com/NuGet/Home/issues/8692)

**DCR**

* Logika w _GetRestoreProjectStyle powinna znajdować się w [#8804](https://github.com/NuGet/Home/issues/8804) zadania

* Domyślnie Dodaj informacje o zaniechaniu na zainstalowanej karcie — [#8541](https://github.com/NuGet/Home/issues/8541)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
