---
title: Informacje o wersji narzędzia NuGet 5,4
description: Informacje o wersji programu NuGet 5,4, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384114"
---
# <a name="nuget-54-release-notes"></a>Informacje o wersji narzędzia NuGet 5,4

Pojazdy dystrybucji NuGet:

| Wersja programu NuGet | Dostępne w wersji programu Visual Studio| Dostępne w zestawach SDK platformy .NET|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 w wersji 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core

## <a name="summary-whats-new-in-54"></a>Podsumowanie: co nowego w 5,4

* Krótszy czas ładowania rozwiązania, który umożliwia wykonywanie kodu NuGet podczas pierwszego ładowania rozwiązania, został zredukowany za pomocą częściowej metody NGen w celu zmniejszenia kosztów JIT — [#6007](https://github.com/NuGet/Home/issues/6007)

* Nowa funkcja pomocnika — otrzymano listę identyfikatorów pakietów i wersji, należy uzyskać odpowiednie pakiety najwyższego poziomu. - [#8316](https://github.com/NuGet/Home/issues/8316)

* Nowe [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) akcje dotyczące instalowania i konfigurowania programu NuGet. exe w ramach [akcji usługi GitHub](https://github.com/features/actions). - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>Problemy rozwiązane w tej wersji

**Usterek**

* Wtyczka: dokładność czasu rejestrowania jest wyłączona w systemie Linux/Mac — [#8747](https://github.com/NuGet/Home/issues/8747)

* Odrzucanie wtyczki może czasami zgłosić i zakończyć całą operację. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Zatrzymaj wyświetlanie duplikatów wersji na liście dozwolonych i zablokowanych wersji w PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)

* Plik blokady nie został prawidłowo wygenerowany — porządkowanie struktury nie powinno mieć wpływu na przywracanie z zablokowanym- [#8645](https://github.com/NuGet/Home/issues/8645)

* Weryfikacja LockFile nie powiedzie się w przypadku projektów z zestawem <RuntimeIdentifiers> w zestawie SDK 3.0.100 — [#8639](https://github.com/NuGet/Home/issues/8639)

* Sprawdzanie poprawności podpisywania będzie teraz prawidłowo odrzucać sygnatury z sygnaturami czasowymi, które mają 2 wartości pod tym samym identyfikatorem OID- [#8629](https://github.com/NuGet/Home/issues/8629)

* Aktualizowanie listy licencji — [#8544](https://github.com/NuGet/Home/issues/8544)

**DCR**

* Dołączanie plików diagnostycznych do IFeedbackDiagnosticFileProvider — [#8535](https://github.com/NuGet/Home/issues/8535)

**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
