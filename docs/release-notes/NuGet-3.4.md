---
title: Informacje o wersji 3.4 NuGet
description: Informacje o wersji programu NuGet 3.4, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551194"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="a3c4e-103">Informacje o wersji 3.4 NuGet</span><span class="sxs-lookup"><span data-stu-id="a3c4e-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="a3c4e-104">[Informacje o wersji 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [informacjach o wersji NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="a3c4e-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="a3c4e-105">NuGet 3.4 jako część programu Visual Studio 2015 Update 2 i programu Visual Studio 15 (wersja zapoznawcza) wersji wydanej 30 marca 2016 r. i został skompilowany przy użyciu kilku założenia w umysłów:</span><span class="sxs-lookup"><span data-stu-id="a3c4e-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="a3c4e-106">Obsługa wielu Platform</span><span class="sxs-lookup"><span data-stu-id="a3c4e-106">Cross-Platform support</span></span>
* <span data-ttu-id="a3c4e-107">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="a3c4e-107">Performance improvements</span></span>
* <span data-ttu-id="a3c4e-108">Drobne ulepszenia interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="a3c4e-108">Minor UI improvements</span></span>

<span data-ttu-id="a3c4e-109">Następujące funkcje zostały wcześniej dodane w wersji RC i zostały zaktualizowane lub ukończone w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="a3c4e-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="a3c4e-110">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="a3c4e-110">New Features</span></span>

* <span data-ttu-id="a3c4e-111">Klienci programu NuGet teraz obsługuje gzip kodowania zawartości z repozytoriów</span><span class="sxs-lookup"><span data-stu-id="a3c4e-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="a3c4e-112">Obsługa plików PDB z pakietów w kompilowanych projektach xproj</span><span class="sxs-lookup"><span data-stu-id="a3c4e-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="a3c4e-113">Obsługa systemów iOS i Android akcji kompilowania w systemach elementu contentFiles</span><span class="sxs-lookup"><span data-stu-id="a3c4e-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="a3c4e-114">Obsługa netstandard i netstandardapp monikerów framework</span><span class="sxs-lookup"><span data-stu-id="a3c4e-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="a3c4e-115">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="a3c4e-115">New User Interface Features</span></span>

* <span data-ttu-id="a3c4e-116">Znaczne ulepszenia wydajności zwłaszcza na kartach zainstalowany, aktualizacji i Konsolidacja</span><span class="sxs-lookup"><span data-stu-id="a3c4e-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="a3c4e-117">Łączny źródło wszystkich źródeł pakietów jest dostępne ze scalaniem wynik właściwego wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="a3c4e-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="a3c4e-118">Zainstalowany i karty aktualizacje teraz są sortowane alfabetycznie</span><span class="sxs-lookup"><span data-stu-id="a3c4e-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="a3c4e-119">Dodaje przycisk odświeżania, która umożliwia wyszukiwanie do odświeżenia</span><span class="sxs-lookup"><span data-stu-id="a3c4e-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="a3c4e-120">Najnowsze opcje kompilacji w górnej części listy wersji</span><span class="sxs-lookup"><span data-stu-id="a3c4e-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="a3c4e-121">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="a3c4e-121">Updates and Improvements</span></span>

* <span data-ttu-id="a3c4e-122">Pakiety, do którego odwołuje się `project.json` , które mają zmiennoprzecinkowy wersji nie będzie aktualizowana przy każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="a3c4e-123">Zamiast tego zostanie zaktualizowana tylko wtedy, gdy zmuszeni do przywrócenia, czyszczenia, odbudować lub zmodyfikować `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="a3c4e-124">źródeł repozytorium nuget.org już jest zmuszony do konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="a3c4e-125">NuGet nie są już pakiety w udostępnionych projektach ani zapisuje plik blokady.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="a3c4e-126">Firma Microsoft może udoskonalenia awarii sieci, a następnie ponów próbę obsługi dla serwerów niedostępne lub powolne odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="a3c4e-127">Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="a3c4e-128">Obsługujemy teraz najnowsze `project.json` schemat środowiska DNX.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="a3c4e-129">Fundamentalne zmiany</span><span class="sxs-lookup"><span data-stu-id="a3c4e-129">Breaking Changes</span></span>

* <span data-ttu-id="a3c4e-130">Numery wersji pakietu teraz są znormalizowane zgodnie z formatem *głównych*. *drobne*. *poprawka*-*wstępnej* wszystkich głównych i niewielkie i patch są traktowane jako liczby całkowite i usunąć wszelkie zer wiodących.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="a3c4e-131">Wstępne informacje są traktowane jako ciąg i są do niego zastosowane żadne zmiany.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="a3c4e-132">Numery te są używane w zapytaniach przez klientów NuGet i wyszukiwania w usłudze nuget.org dostępne.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="a3c4e-133">Więcej szczegółów można znaleźć w dokumentacji systemu NuGet w obszarze [wersji wstępnych](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a3c4e-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="a3c4e-134">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a3c4e-134">Known Issues</span></span>

* <span data-ttu-id="a3c4e-135">**Problem:** użytkownicy v1511 systemu Windows 10, mogą wystąpić problemy lub nawet awarii programu Visual Studio przy użyciu programu Powershell w programie Visual Studio w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="a3c4e-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="a3c4e-136">Instalowanie / Odinstalowywanie pakietów, które mają install.ps1 / uninstall.ps1 skryptów</span><span class="sxs-lookup"><span data-stu-id="a3c4e-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="a3c4e-137">Ładowanie projektów, które mają skrypt init.ps1 (na przykład EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="a3c4e-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="a3c4e-138">Publikowanie zawartości sieci web</span><span class="sxs-lookup"><span data-stu-id="a3c4e-138">Publishing web content</span></span>

* <span data-ttu-id="a3c4e-139">**Obejście:** upewnić się, że Twoja instalacja systemu Windows 10 najnowszych poprawek, które są stosowane, expecially styczeń 2016 r. (KB 3124263) lub nowsza aktualizacja.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="a3c4e-140">Więcej informacji jest dostępnych na [problem w usłudze GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="a3c4e-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="a3c4e-141">**Problem:** Przekierowania protokołu NuGet w wersji 2 są przerwane.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="a3c4e-142">Niestandardowe repozytoria NuGet, które przekierowują żądania do alternatywnego hosta, nie uznają żądania przekierowania.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="a3c4e-143">**Obejście:** Aby obejść ten problem, skonfiguruj identyfikator URI repozytorium pakietów w ustawieniach, aby wskazać lokalizację serwera po przekierowaniu.</span><span class="sxs-lookup"><span data-stu-id="a3c4e-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="a3c4e-144">Aby uzyskać więcej informacji, zobacz [żądania ściągnięcia serwisu GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="a3c4e-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="a3c4e-145">W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a3c4e-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>