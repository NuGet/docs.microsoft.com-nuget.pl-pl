---
title: Informacje o wersji narzędzia NuGet 5,6
description: Informacje o wersji programu NuGet 5,6, w tym nowe funkcje, poprawki błędów i DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727822"
---
# <a name="nuget-56-release-notes"></a>Informacje o wersji narzędzia NuGet 5,6

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-56"></a>Podsumowanie: co nowego w 5,6

* Obsługa pakietów wstępnych w wersjach zmiennoprzecinkowych. `Version="*-*"`, `Version="1.*-*"` i podobne zmiennoprzecinkowe do najnowszych wersji, w tym wersje wstępne, w określonym zakresie- [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Błędy:**

* `nuget push *.nupkg`kończy się niepowodzeniem, gdy snupkg nie istnieje — [#8148](https://github.com/NuGet/Home/issues/8148)

* Pakiet i kilka innych ścieżek kodu nie są zależne od ustawień regionalnych. Użyj RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Wydajność: Specyfikacja DG dla scenariuszy niezaładowanych projektów nie powinna być napisywana w wersji zapoznawczej — [#8793](https://github.com/NuGet/Home/issues/8793)

* Przywracanie: zwiększanie wydajności przez buforowanie specyfikacji grafu zależności rozwiązania — [#9201](https://github.com/NuGet/Home/issues/9201)

* Interfejs użytkownika PM nie działa dla projektów w stylu zestawu SDK po zainstalowaniu pakietu z konsolą PM- [#9203](https://github.com/NuGet/Home/issues/9203)

* Ikona osadzona nie może być wyświetlana w interfejsie użytkownika PM przy użyciu lokalnego źródła danych — w zależności od/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict () powinien zwrócić wartość false, jeśli nie można przeanalizować- [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`Pomoc dla `-source` , powinna zasugerować użycie nazwy źródłowej, a nie adresu URL źródła — [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`tworzy złą nazwę źródłową pakietu domyślnego — [#9277](https://github.com/NuGet/Home/issues/9277)

* Czytnik ekranu nie ogłasza "wyszukiwania..." komunikat podczas przełączania kart — [#9307](https://github.com/NuGet/Home/issues/9307)

* Dostępność: Kolor prostokąta fokusu nie jest dostępny PM karty interfejsu użytkownika w ciemnym motywie — [#9336](https://github.com/NuGet/Home/issues/9336)

* nie można przywrócić pliku NuGet. exe 5,5 przy użyciu programu MSBuild 14 lub starszego — [#9458](https://github.com/NuGet/Home/issues/9458)

* Nie rejestruj czasów milisekund w komunikatach przywracania — [#8977](https://github.com/NuGet/Home/issues/8977)

* IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)

* Funkcja wybierania wersji programu MSBuild działa słabo w niektórych kulturach innych niż angielskie — [#9322](https://github.com/NuGet/Home/issues/9322)

* Brak domyślnego formatu w `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Wydajność: RestoreOperationLogger ma niepotrzebną koligację wątku — [#9288](https://github.com/NuGet/Home/issues/9288)

* Automatyczne tworzenie dokumentów dla `dotnet nuget` poleceń — [#9146](https://github.com/NuGet/Home/issues/9146)

* Domyślny poziom szczegółowości nie powinien raportować aktualizujący nie działa przywracania każdego projektu — [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`Parametr obsługi dla `NuGet.exe update` , podobny do polecenia instalacji — [#7694](https://github.com/NuGet/Home/issues/7694)


**DCR**

* Dodawanie początkowej obsługi dla platformy docelowej NET 5.0 — [#9584](https://github.com/NuGet/Home/issues/9584)

* Posortuj pakiety według identyfikatora na karcie aktualizacje interfejsu użytkownika PM — [#9278](https://github.com/NuGet/Home/issues/9278)


**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
