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
# <a name="nuget-54-release-notes"></a><span data-ttu-id="46a93-103">Informacje o wersji narzędzia NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="46a93-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="46a93-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="46a93-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="46a93-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="46a93-105">NuGet version</span></span> | <span data-ttu-id="46a93-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46a93-106">Available in Visual Studio version</span></span>| <span data-ttu-id="46a93-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="46a93-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="46a93-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="46a93-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="46a93-109">Visual Studio 2019 w wersji 16,4</span><span class="sxs-lookup"><span data-stu-id="46a93-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="46a93-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="46a93-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="46a93-111"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="46a93-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="46a93-112">Podsumowanie: co nowego w 5,4</span><span class="sxs-lookup"><span data-stu-id="46a93-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="46a93-113">Krótszy czas ładowania rozwiązania, który umożliwia wykonywanie kodu NuGet podczas pierwszego ładowania rozwiązania, został zredukowany za pomocą częściowej metody NGen w celu zmniejszenia kosztów JIT — [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="46a93-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="46a93-114">Nowa funkcja pomocnika — otrzymano listę identyfikatorów pakietów i wersji, należy uzyskać odpowiednie pakiety najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="46a93-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="46a93-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="46a93-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="46a93-116">Nowe [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) akcje dotyczące instalowania i konfigurowania programu NuGet. exe w ramach [akcji usługi GitHub](https://github.com/features/actions).</span><span class="sxs-lookup"><span data-stu-id="46a93-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="46a93-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="46a93-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="46a93-118">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="46a93-118">Issues fixed in this release</span></span>

<span data-ttu-id="46a93-119">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="46a93-119">**Bugs**</span></span>

* <span data-ttu-id="46a93-120">Wtyczka: dokładność czasu rejestrowania jest wyłączona w systemie Linux/Mac — [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="46a93-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="46a93-121">Odrzucanie wtyczki może czasami zgłosić i zakończyć całą operację.</span><span class="sxs-lookup"><span data-stu-id="46a93-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="46a93-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="46a93-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="46a93-123">Zatrzymaj wyświetlanie duplikatów wersji na liście dozwolonych i zablokowanych wersji w PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="46a93-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="46a93-124">Plik blokady nie został prawidłowo wygenerowany — porządkowanie struktury nie powinno mieć wpływu na przywracanie z zablokowanym- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="46a93-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="46a93-125">Weryfikacja LockFile nie powiedzie się w przypadku projektów z zestawem <RuntimeIdentifiers> w zestawie SDK 3.0.100 — [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="46a93-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="46a93-126">Sprawdzanie poprawności podpisywania będzie teraz prawidłowo odrzucać sygnatury z sygnaturami czasowymi, które mają 2 wartości pod tym samym identyfikatorem OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="46a93-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="46a93-127">Aktualizowanie listy licencji — [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="46a93-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="46a93-128">**DCR**</span><span class="sxs-lookup"><span data-stu-id="46a93-128">**DCRs**</span></span>

* <span data-ttu-id="46a93-129">Dołączanie plików diagnostycznych do IFeedbackDiagnosticFileProvider — [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="46a93-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="46a93-130">**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="46a93-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
