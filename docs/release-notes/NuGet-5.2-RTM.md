---
title: Informacje o wersji narzędzia NuGet 5,2 RTM
description: Informacje o wersji programu NuGet 5,2, w tym nowe funkcje, poprawki błędów i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776205"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="4ef60-103">Informacje o wersji narzędzia NuGet 5,2</span><span class="sxs-lookup"><span data-stu-id="4ef60-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="4ef60-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="4ef60-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="4ef60-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="4ef60-105">NuGet version</span></span> | <span data-ttu-id="4ef60-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ef60-106">Available in Visual Studio version</span></span>| <span data-ttu-id="4ef60-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="4ef60-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="4ef60-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="4ef60-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="4ef60-109">Visual Studio 2019 w wersji 16,2</span><span class="sxs-lookup"><span data-stu-id="4ef60-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="4ef60-110">[2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="4ef60-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="4ef60-111"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="4ef60-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="4ef60-112"><sup>2</sup> Dostępne jako opcjonalna instalacja z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="4ef60-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="4ef60-113">Podsumowanie: co nowego w 5,2</span><span class="sxs-lookup"><span data-stu-id="4ef60-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="4ef60-114">Rozwiązano błąd krytyczny, który spowodował sporadyczne niepowodzenia operacji NuGet ze względu na problemy z ścieżką w systemie Linux & Mac — [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="4ef60-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="4ef60-115">Ulepszona czas odpowiedzi interfejsu użytkownika podczas przeglądania pakietów przy użyciu interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio, szczególnie zauważalne w przypadku wolnych źródeł — [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="4ef60-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="4ef60-116">Tony poprawek niezawodności dla pliku blokady ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114)[#7840](https://github.com/NuGet/Home/issues/7840)) i wtyczki uwierzytelniania ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198), #7845)[](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="4ef60-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="4ef60-117">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="4ef60-117">Issues fixed in this release</span></span>

<span data-ttu-id="4ef60-118">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="4ef60-118">**Bugs**</span></span>

* <span data-ttu-id="4ef60-119">Wydajność: Konsola Menedżera pakietów: zaznaczono wartość pola kombi "Projekt domyślny" z opóźnieniem interfejsu użytkownika — [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="4ef60-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="4ef60-120">Wydajność: ulepszenia wydajności w interfejsie użytkownika PM — [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="4ef60-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="4ef60-121">Wydajność: opóźnienie interfejsu użytkownika podczas odczytywania domyślnego projektu w kryterium PMC- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="4ef60-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="4ef60-122">Wydajność: [vsfeedback] karta aktualizacji NuGet zawiesza się dla lokalnego źródła pakietów — [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="4ef60-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="4ef60-123">Wtyczki: pakiet NuGet czeka na pełny limit czasu, jeśli wtyczka nie zostanie uruchomiona lub zakończy się wcześnie [#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="4ef60-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="4ef60-124">Wtyczki: zwiększanie diagnozy niepowodzenia uruchamiania wtyczki — [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="4ef60-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="4ef60-125">Wtyczki: problem z nuget.exe odnajdywania wbudowanych wtyczek — [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="4ef60-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="4ef60-126">Wtyczki: plik pamięci podręcznej nigdy nie jest odczytywany [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="4ef60-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="4ef60-127">Wtyczki: "zadanie zostało anulowane."</span><span class="sxs-lookup"><span data-stu-id="4ef60-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="4ef60-128">błędy przy użyciu wtyczki uwierzytelniania podczas przywracania [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="4ef60-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="4ef60-129">Buforowanie wtyczek nie jest sporadycznie wykrywalne na platformach z systemem Linux — [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="4ef60-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="4ef60-130">LockFile: z ATF, ma wartość false NU1004 z powodu nieprawidłowej kontroli równości platformy docelowej, [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="4ef60-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="4ef60-131">LockFile: Flaga przywracania "--locked-Mode" nie jest przestrzegana, jeśli plik blokady jest pusty lub źle sformułowany — [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="4ef60-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="4ef60-132">LockFile: nie małe projekty z niestandardowymi nazwami zestawów w pliku blokady pakietu — [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="4ef60-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="4ef60-133">LockFile: Zmień wielkość liter w odwołaniu do projektu w pliku blokady — [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="4ef60-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="4ef60-134">Przywracanie: Instalowanie podpisanego pakietu z naruszonymi wynikami w wielu nieudanych próbach instalacji (z powtórzonym wyjściem) — [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="4ef60-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="4ef60-135">VS: nie można deserializować opcji użytkownika rozwiązania po aktualizacji NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="4ef60-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="4ef60-136">Pakiet dotnet-list-Package w projekcie testu jednostkowego zwraca błąd- [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="4ef60-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="4ef60-137">Utwórz grupę pakietów NuGet dla Instalatora programu VS — naprawianie niektórych problemów z instalacją VSIX — [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="4ef60-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="4ef60-138">GeneratePackageOnBuild nie powinna być ustawiona nobuild.</span><span class="sxs-lookup"><span data-stu-id="4ef60-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="4ef60-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="4ef60-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="4ef60-140">Nowa opcja "-SymbolPackageFormat snupkg" generuje błąd, gdy plik. nuspec zawiera jawny element odwołania do zestawu — [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="4ef60-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="4ef60-141">NuGet. targets (498, 5): błąd: nie można odnaleźć części ścieżki "/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="4ef60-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="4ef60-142">**DCR**</span><span class="sxs-lookup"><span data-stu-id="4ef60-142">**DCR:**</span></span>

* <span data-ttu-id="4ef60-143">Dodaj właściwość programu MSBuild, która wskazuje, że PackageDownload jest obsługiwana — [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="4ef60-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="4ef60-144">FrameworkReference Pomijaj przepływ zależności za pośrednictwem FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="4ef60-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="4ef60-145">Mechanizm dostarczania runtime.jsna zewnątrz pakietu [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="4ef60-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="4ef60-146">**[Lista wszystkich problemów rozwiązanych w tym wydaniu — 5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="4ef60-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


