---
title: Informacje o wersji narzędzia NuGet 5,4
description: Informacje o wersji programu NuGet 5,4, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828409"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="abf90-103">Informacje o wersji narzędzia NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="abf90-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="abf90-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="abf90-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="abf90-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="abf90-105">NuGet version</span></span> | <span data-ttu-id="abf90-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="abf90-106">Available in Visual Studio version</span></span>| <span data-ttu-id="abf90-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="abf90-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="abf90-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="abf90-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="abf90-109">Visual Studio 2019 w wersji 16,4</span><span class="sxs-lookup"><span data-stu-id="abf90-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="abf90-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="abf90-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="abf90-111"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="abf90-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="abf90-112">Podsumowanie: co nowego w 5,4</span><span class="sxs-lookup"><span data-stu-id="abf90-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="abf90-113">Krótszy czas ładowania rozwiązania, który umożliwia wykonywanie kodu NuGet podczas pierwszego ładowania rozwiązania, został zredukowany za pomocą częściowej metody NGen w celu zmniejszenia kosztów JIT — [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="abf90-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="abf90-114">Nowa funkcja pomocnika — otrzymano listę identyfikatorów pakietów i wersji, należy uzyskać odpowiednie pakiety najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="abf90-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="abf90-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="abf90-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="abf90-116">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="abf90-116">Issues fixed in this release</span></span>

<span data-ttu-id="abf90-117">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="abf90-117">**Bugs**</span></span>

* <span data-ttu-id="abf90-118">Wtyczka: dokładność czasu rejestrowania jest wyłączona w systemie Linux/Mac — [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="abf90-118">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="abf90-119">Odrzucanie wtyczki może czasami zgłosić i zakończyć całą operację.</span><span class="sxs-lookup"><span data-stu-id="abf90-119">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="abf90-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="abf90-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="abf90-121">Zatrzymaj wyświetlanie duplikatów wersji na liście dozwolonych i zablokowanych wersji w PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="abf90-121">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="abf90-122">Plik blokady nie został prawidłowo wygenerowany — porządkowanie struktury nie powinno mieć wpływu na przywracanie z zablokowanym- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="abf90-122">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="abf90-123">Weryfikacja LockFile nie powiedzie się w przypadku projektów z zestawem <RuntimeIdentifiers> w zestawie SDK 3.0.100 — [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="abf90-123">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="abf90-124">Sprawdzanie poprawności podpisywania będzie teraz prawidłowo odrzucać sygnatury z sygnaturami czasowymi, które mają 2 wartości pod tym samym identyfikatorem OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="abf90-124">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="abf90-125">Aktualizowanie listy licencji — [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="abf90-125">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="abf90-126">**DCR**</span><span class="sxs-lookup"><span data-stu-id="abf90-126">**DCRs**</span></span>

* <span data-ttu-id="abf90-127">Dołączanie plików diagnostycznych do IFeedbackDiagnosticFileProvider — [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="abf90-127">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="abf90-128">**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="abf90-128">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
