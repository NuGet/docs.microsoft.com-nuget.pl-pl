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
# <a name="nuget-56-release-notes"></a><span data-ttu-id="acbe1-103">Informacje o wersji narzędzia NuGet 5,6</span><span class="sxs-lookup"><span data-stu-id="acbe1-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="acbe1-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="acbe1-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="acbe1-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="acbe1-105">NuGet version</span></span> | <span data-ttu-id="acbe1-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="acbe1-106">Available in Visual Studio version</span></span>| <span data-ttu-id="acbe1-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="acbe1-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="acbe1-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="acbe1-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="acbe1-109">Visual Studio 2019 w wersji 16,6</span><span class="sxs-lookup"><span data-stu-id="acbe1-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="acbe1-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="acbe1-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="acbe1-111"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="acbe1-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="acbe1-112">Podsumowanie: co nowego w 5,6</span><span class="sxs-lookup"><span data-stu-id="acbe1-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="acbe1-113">Obsługa pakietów wstępnych w wersjach zmiennoprzecinkowych.</span><span class="sxs-lookup"><span data-stu-id="acbe1-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="acbe1-114">`Version="*-*"`, `Version="1.*-*"` i podobne zmiennoprzecinkowe do najnowszych wersji, w tym wersje wstępne, w określonym zakresie- [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="acbe1-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="acbe1-115">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="acbe1-115">Issues fixed in this release</span></span>

<span data-ttu-id="acbe1-116">**Błędy:**</span><span class="sxs-lookup"><span data-stu-id="acbe1-116">**Bugs:**</span></span>

* <span data-ttu-id="acbe1-117">`nuget push *.nupkg`kończy się niepowodzeniem, gdy snupkg nie istnieje — [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="acbe1-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="acbe1-118">Pakiet i kilka innych ścieżek kodu nie są zależne od ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="acbe1-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="acbe1-119">Użyj RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="acbe1-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="acbe1-120">Wydajność: Specyfikacja DG dla scenariuszy niezaładowanych projektów nie powinna być napisywana w wersji zapoznawczej — [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="acbe1-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="acbe1-121">Przywracanie: zwiększanie wydajności przez buforowanie specyfikacji grafu zależności rozwiązania — [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="acbe1-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="acbe1-122">Interfejs użytkownika PM nie działa dla projektów w stylu zestawu SDK po zainstalowaniu pakietu z konsolą PM- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="acbe1-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="acbe1-123">Ikona osadzona nie może być wyświetlana w interfejsie użytkownika PM przy użyciu lokalnego źródła danych — w zależności od/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="acbe1-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="acbe1-124">NuGetVersion. TryParseStrict () powinien zwrócić wartość false, jeśli nie można przeanalizować- [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="acbe1-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="acbe1-125">`nuget.exe push`Pomoc dla `-source` , powinna zasugerować użycie nazwy źródłowej, a nie adresu URL źródła — [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="acbe1-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="acbe1-126">`dotnet nuget add package SourceUri`tworzy złą nazwę źródłową pakietu domyślnego — [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="acbe1-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="acbe1-127">Czytnik ekranu nie ogłasza "wyszukiwania..." komunikat podczas przełączania kart — [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="acbe1-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="acbe1-128">Dostępność: Kolor prostokąta fokusu nie jest dostępny PM karty interfejsu użytkownika w ciemnym motywie — [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="acbe1-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="acbe1-129">nie można przywrócić pliku NuGet. exe 5,5 przy użyciu programu MSBuild 14 lub starszego — [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="acbe1-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="acbe1-130">Nie rejestruj czasów milisekund w komunikatach przywracania — [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="acbe1-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="acbe1-131">IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="acbe1-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="acbe1-132">Funkcja wybierania wersji programu MSBuild działa słabo w niektórych kulturach innych niż angielskie — [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="acbe1-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="acbe1-133">Brak domyślnego formatu w `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="acbe1-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="acbe1-134">Wydajność: RestoreOperationLogger ma niepotrzebną koligację wątku — [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="acbe1-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="acbe1-135">Automatyczne tworzenie dokumentów dla `dotnet nuget` poleceń — [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="acbe1-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="acbe1-136">Domyślny poziom szczegółowości nie powinien raportować aktualizujący nie działa przywracania każdego projektu — [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="acbe1-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="acbe1-137">`-DependencyVersion`Parametr obsługi dla `NuGet.exe update` , podobny do polecenia instalacji — [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="acbe1-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="acbe1-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="acbe1-138">**DCRs:**</span></span>

* <span data-ttu-id="acbe1-139">Dodawanie początkowej obsługi dla platformy docelowej NET 5.0 — [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="acbe1-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="acbe1-140">Posortuj pakiety według identyfikatora na karcie aktualizacje interfejsu użytkownika PM — [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="acbe1-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="acbe1-141">**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="acbe1-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
