---
title: Informacje o wersji narzędzia NuGet 3,4
description: Informacje o wersji programu NuGet 3,4, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776414"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="0afa1-103">Informacje o wersji narzędzia NuGet 3,4</span><span class="sxs-lookup"><span data-stu-id="0afa1-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="0afa1-104">Pakiet [NuGet 3,4 — informacje](../release-notes/nuget-3.4-RC.md)  |  o wersji RC [Informacje o wersji pakietu NuGet](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="0afa1-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="0afa1-105">Pakiet NuGet 3,4 został zwolniony 30 marca 2016 w ramach programu Visual Studio 2015 Update 2 i programu Visual Studio 15 Preview i został skompilowany za pomocą kilku założenia w zdanie:</span><span class="sxs-lookup"><span data-stu-id="0afa1-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="0afa1-106">Obsługa wielu platform</span><span class="sxs-lookup"><span data-stu-id="0afa1-106">Cross-Platform support</span></span>
* <span data-ttu-id="0afa1-107">Usprawnienia wydajności</span><span class="sxs-lookup"><span data-stu-id="0afa1-107">Performance improvements</span></span>
* <span data-ttu-id="0afa1-108">Ulepszenia pomocniczych interfejsów użytkownika</span><span class="sxs-lookup"><span data-stu-id="0afa1-108">Minor UI improvements</span></span>

<span data-ttu-id="0afa1-109">Następujące funkcje zostały wcześniej dodane do wersji RC i zostały zaktualizowane lub ukończone dla wydania 3,4:</span><span class="sxs-lookup"><span data-stu-id="0afa1-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="0afa1-110">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="0afa1-110">New Features</span></span>

* <span data-ttu-id="0afa1-111">Klienci NuGet obsługują teraz kodowanie zawartości gzip z repozytoriów</span><span class="sxs-lookup"><span data-stu-id="0afa1-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="0afa1-112">Obsługa plików PDB z pakietów w projektach xproj</span><span class="sxs-lookup"><span data-stu-id="0afa1-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="0afa1-113">Obsługa akcji kompilacji dla systemów iOS i Android w elemencie contentFiles</span><span class="sxs-lookup"><span data-stu-id="0afa1-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="0afa1-114">Obsługa krótkich monikerów struktury netstandardapp</span><span class="sxs-lookup"><span data-stu-id="0afa1-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="0afa1-115">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="0afa1-115">New User Interface Features</span></span>

* <span data-ttu-id="0afa1-116">Znaczące ulepszenia wydajności dotyczące kart zainstalowanych, aktualizacji i konsolidowania</span><span class="sxs-lookup"><span data-stu-id="0afa1-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="0afa1-117">Zagregowane Źródło "wszystkie źródła pakietów" jest dostępne z prawidłowym scalaniem wyników wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="0afa1-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="0afa1-118">Karty zainstalowane i aktualizacje są teraz sortowane alfabetycznie</span><span class="sxs-lookup"><span data-stu-id="0afa1-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="0afa1-119">Dodano przycisk odświeżania, który umożliwia odświeżenie wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="0afa1-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="0afa1-120">Najnowsze opcje kompilacji w górnej części listy wersji</span><span class="sxs-lookup"><span data-stu-id="0afa1-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="0afa1-121">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="0afa1-121">Updates and Improvements</span></span>

* <span data-ttu-id="0afa1-122">Pakiety, do których się odwołują `project.json` , mają przepływającą wersję, nie będą aktualizowane dla każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0afa1-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="0afa1-123">Zamiast tego zostaną one zaktualizowane tylko wtedy, gdy zostanie wymuszone przywrócenie, oczyszczenie, odbudowanie lub zmodyfikowanie `project.json` .</span><span class="sxs-lookup"><span data-stu-id="0afa1-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="0afa1-124">źródła repozytorium nuget.org nie są już wymuszane w konfiguracji projektu podczas korzystania z interfejsu użytkownika konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="0afa1-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="0afa1-125">Pakiet NuGet nie przywraca już pakietów w projektach udostępnionych ani nie zapisuje pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="0afa1-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="0afa1-126">Ulepszono awarię sieci i obsługę ponownych prób w przypadku nieosiągalnych lub wolnych serwerów.</span><span class="sxs-lookup"><span data-stu-id="0afa1-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="0afa1-127">W interfejsie użytkownika Menedżera pakietów programu Visual Studio Ulepszono zachowania klawiatury i myszy.</span><span class="sxs-lookup"><span data-stu-id="0afa1-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="0afa1-128">Teraz obsługujemy najnowszy `project.json` schemat w programie środowiska DNX.</span><span class="sxs-lookup"><span data-stu-id="0afa1-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="0afa1-129">Zmiany powodujące niezgodność</span><span class="sxs-lookup"><span data-stu-id="0afa1-129">Breaking Changes</span></span>

* <span data-ttu-id="0afa1-130">Numery wersji pakietu są teraz znormalizowane w formacie *głównym*. *pomocnicze*. *poprawka* - *wersja wstępna*   Każda z głównych, pomocniczych i poprawek jest traktowana jako liczba całkowita i upuszczania wiodących zer.</span><span class="sxs-lookup"><span data-stu-id="0afa1-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="0afa1-131">Informacje o wersji wstępnej są traktowane jako ciąg i nie są do niego stosowane żadne zmiany.</span><span class="sxs-lookup"><span data-stu-id="0afa1-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="0afa1-132">Te liczby są używane w zapytaniach przez klientów NuGet i wyszukiwaniech dostarczonych przez usługę nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0afa1-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="0afa1-133">Więcej informacji można znaleźć w dokumentacji pakietu NuGet w obszarze [wersje wstępne](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0afa1-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0afa1-134">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="0afa1-134">Known Issues</span></span>

* <span data-ttu-id="0afa1-135">**Problem:** Użytkownicy systemu Windows 10 v1511 mogą napotkać problemy, a nawet program Visual Studio w programie PowerShell w programie Visual Studio w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="0afa1-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="0afa1-136">Instalowanie/Odinstalowywanie pakietów, które mają skrypty install.ps1/uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="0afa1-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="0afa1-137">Ładowanie projektów, które mają skrypt init.ps1 (na przykład EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="0afa1-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="0afa1-138">Publikowanie zawartości sieci Web</span><span class="sxs-lookup"><span data-stu-id="0afa1-138">Publishing web content</span></span>

* <span data-ttu-id="0afa1-139">**Obejście problemu:** Upewnij się, że w instalacji systemu Windows 10 zostały zastosowane najnowsze poprawki, expecially 2016 stycznia (KB 3124263) lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="0afa1-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="0afa1-140">Więcej szczegółów można znaleźć w witrynie [GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="0afa1-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="0afa1-141">**Problem:** Przekierowania protokołu NuGet w wersji 2 są przerwane.</span><span class="sxs-lookup"><span data-stu-id="0afa1-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="0afa1-142">Niestandardowe repozytoria NuGet, które przekierowują żądania do alternatywnego hosta, nie uznają żądania przekierowania.</span><span class="sxs-lookup"><span data-stu-id="0afa1-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="0afa1-143">**Obejście problemu:**  Aby obejść ten problem, należy skonfigurować identyfikator URI repozytorium pakietów w ustawieniach, aby wskazywał lokalizację serwera przekierowanego.</span><span class="sxs-lookup"><span data-stu-id="0afa1-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="0afa1-144">Aby uzyskać więcej informacji, zobacz [#387 żądania ściągnięcia usługi GitHub](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="0afa1-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="0afa1-145">Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="0afa1-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>