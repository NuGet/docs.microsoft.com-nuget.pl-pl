---
title: NuGet 3.4 informacje o wersji
description: Informacje o wersji programu NuGet 3.4, w tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820475"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="bf185-103">NuGet 3.4 informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="bf185-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="bf185-104">[Informacje o wersji 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 informacje o wersji](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="bf185-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="bf185-105">NuGet 3.4 jako część programu Visual Studio 2015 Update 2 i Visual Studio 15 Preview wersji wydanej 30 marca 2016 i został skompilowany z kilka rozwiązań w umysły:</span><span class="sxs-lookup"><span data-stu-id="bf185-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="bf185-106">Obsługa Platform</span><span class="sxs-lookup"><span data-stu-id="bf185-106">Cross-Platform support</span></span>
* <span data-ttu-id="bf185-107">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="bf185-107">Performance improvements</span></span>
* <span data-ttu-id="bf185-108">Drobne ulepszenia interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="bf185-108">Minor UI improvements</span></span>

<span data-ttu-id="bf185-109">Następujące funkcje zostały wcześniej dodane w wersji RC i zostały zaktualizowane lub zakończona w wersji 3.4:</span><span class="sxs-lookup"><span data-stu-id="bf185-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="bf185-110">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="bf185-110">New Features</span></span>

* <span data-ttu-id="bf185-111">Klienci NuGet obsługuje teraz, kodowania zawartości gzip z repozytoriami</span><span class="sxs-lookup"><span data-stu-id="bf185-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="bf185-112">Obsługa baz danych PDB z pakietów w projektach xproj</span><span class="sxs-lookup"><span data-stu-id="bf185-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="bf185-113">Akcje w elemencie contentFiles kompilacji pomocy technicznej dla systemów iOS i Android</span><span class="sxs-lookup"><span data-stu-id="bf185-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="bf185-114">Obsługa krótkich nazw netstandard i netstandardapp monikerów framework</span><span class="sxs-lookup"><span data-stu-id="bf185-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="bf185-115">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="bf185-115">New User Interface Features</span></span>

* <span data-ttu-id="bf185-116">Znaczący wzrost wydajności szczególnie na kartach zainstalowane aktualizacje i Konsoliduj</span><span class="sxs-lookup"><span data-stu-id="bf185-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="bf185-117">Źródła agregowania wszystkie źródła pakietów jest dostępna w programie scalanie wynik wyszukiwania właściwego</span><span class="sxs-lookup"><span data-stu-id="bf185-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="bf185-118">Zainstalowane i aktualizacje kartach teraz są posortowane alfabetycznie</span><span class="sxs-lookup"><span data-stu-id="bf185-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="bf185-119">Dodaje przycisk Odśwież, która umożliwia wyszukiwanie, którego chcesz odświeżyć</span><span class="sxs-lookup"><span data-stu-id="bf185-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="bf185-120">Najnowsze opcje kompilacji w górnej części listy wersji</span><span class="sxs-lookup"><span data-stu-id="bf185-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="bf185-121">Aktualizacje i usprawnienia</span><span class="sxs-lookup"><span data-stu-id="bf185-121">Updates and Improvements</span></span>

* <span data-ttu-id="bf185-122">Pakiety, do którego odwołuje się `project.json` , która ma zmiennoprzecinkową wersji nie będzie aktualizowany przy każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bf185-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="bf185-123">Zamiast tego zostanie zaktualizowana tylko wtedy, gdy wymusić przywracanie, czyszczenia, odbudować lub zmodyfikować `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bf185-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="bf185-124">źródłach repozytoriów nuget.org już zostało wymuszone w konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="bf185-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="bf185-125">NuGet już przywraca pakietów w udostępnionych projektów nie zapisuje plik blokady.</span><span class="sxs-lookup"><span data-stu-id="bf185-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="bf185-126">Firma Microsoft została ulepszona awarii sieci, a następnie spróbuj ponownie obsługi dla serwerów jest nieosiągalny lub powolne na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="bf185-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="bf185-127">Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf185-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="bf185-128">Obsługujemy teraz najnowszej `project.json` schematu w DNX.</span><span class="sxs-lookup"><span data-stu-id="bf185-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="bf185-129">Fundamentalne zmiany</span><span class="sxs-lookup"><span data-stu-id="bf185-129">Breaking Changes</span></span>

* <span data-ttu-id="bf185-130">Numery wersji pakietu są teraz znormalizowane do formatu *głównych*. *drobne*. *poprawka*-*wstępnej* poszczególnych głównych i pomocnicze i poprawki są traktowane jako liczby całkowite i upuść żadnych zera wiodące.</span><span class="sxs-lookup"><span data-stu-id="bf185-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="bf185-131">Wstępna informacje są traktowane jako ciąg, a żadne zmiany nie są stosowane do niego.</span><span class="sxs-lookup"><span data-stu-id="bf185-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="bf185-132">Numery te są używane w zapytaniach klientów NuGet i udostępniony przez usługę nuget.org wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="bf185-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="bf185-133">Więcej informacji znajduje się w Docs NuGet w obszarze [wersji wstępnej](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="bf185-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="bf185-134">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="bf185-134">Known Issues</span></span>

* <span data-ttu-id="bf185-135">**Problem:** użytkownicy v1511 systemu Windows 10 mogą wystąpić problemy lub nawet awarii programu Visual Studio przy użyciu programu Powershell w programie Visual Studio w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="bf185-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="bf185-136">Instalowanie / Odinstalowywanie pakiety, które mają install.ps1 / uninstall.ps1 skryptów</span><span class="sxs-lookup"><span data-stu-id="bf185-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="bf185-137">Ładowanie projektów, które mają skrypt init.ps1 (na przykład EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="bf185-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="bf185-138">Publikowanie zawartości sieci web</span><span class="sxs-lookup"><span data-stu-id="bf185-138">Publishing web content</span></span>

* <span data-ttu-id="bf185-139">**Obejście problemu:** upewnij się, że instalacji systemu Windows 10 ma najnowsze poprawki zastosowane, expecially styczeń 2016 r. (KB 3124263) lub późniejszą aktualizację.</span><span class="sxs-lookup"><span data-stu-id="bf185-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="bf185-140">Szczegółowe informacje są dostępne na [problem GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="bf185-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="bf185-141">**Problem:** Przekierowania protokołu NuGet w wersji 2 są przerwane.</span><span class="sxs-lookup"><span data-stu-id="bf185-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="bf185-142">Niestandardowe repozytoria NuGet, które przekierowują żądania do alternatywnego hosta, nie uznają żądania przekierowania.</span><span class="sxs-lookup"><span data-stu-id="bf185-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="bf185-143">**Obejście problemu:** Aby obejść ten problem, należy skonfigurować identyfikator URI repozytorium pakietów w ustawieniach, aby wskazać lokalizację serwera po przekierowaniu.</span><span class="sxs-lookup"><span data-stu-id="bf185-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="bf185-144">Aby uzyskać więcej informacji, zobacz [żądania ściągnięcia GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="bf185-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="bf185-145">W dalszym ciągu śledzenie problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="bf185-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>