---
title: Informacje o wersji 3.4 RC NuGet
description: Informacje o wersji programu NuGet 3.4 RC obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546757"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="804b2-103">Informacje o wersji 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="804b2-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="804b2-104">[Informacje o wersji NuGet 3.3](../release-notes/nuget-3.3.md) | [informacjach o wersji NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="804b2-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="804b2-105">NuGet 3.4-RC został wydany 3 marca 2016 wraz z Visual Studio 2015 Update 2 RC i został skompilowany przy użyciu kilku założenia w umysłów:</span><span class="sxs-lookup"><span data-stu-id="804b2-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="804b2-106">Obsługa wielu Platform</span><span class="sxs-lookup"><span data-stu-id="804b2-106">Cross-Platform support</span></span>
* <span data-ttu-id="804b2-107">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="804b2-107">Performance improvements</span></span>
* <span data-ttu-id="804b2-108">Drobne ulepszenia interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="804b2-108">Minor UI improvements</span></span>

<span data-ttu-id="804b2-109">Następujące funkcje są dostępne w tej wersji RC, kolejne zaplanowane 3.4 ostatecznej wersji.</span><span class="sxs-lookup"><span data-stu-id="804b2-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="804b2-110">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="804b2-110">New Features</span></span>

* <span data-ttu-id="804b2-111">Klienci programu NuGet teraz obsługuje gzip kodowania zawartości z repozytoriów</span><span class="sxs-lookup"><span data-stu-id="804b2-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="804b2-112">Obsługa plików PDB z pakietów w kompilowanych projektach xproj</span><span class="sxs-lookup"><span data-stu-id="804b2-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="804b2-113">Obsługa systemów iOS i Android akcji kompilowania w systemach elementu contentFiles</span><span class="sxs-lookup"><span data-stu-id="804b2-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="804b2-114">Obsługa netstandard i netstandardapp monikerów framework</span><span class="sxs-lookup"><span data-stu-id="804b2-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="804b2-115">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="804b2-115">New User Interface Features</span></span>

* <span data-ttu-id="804b2-116">Znaczne ulepszenia wydajności zwłaszcza na kartach zainstalowany, aktualizacji i Konsolidacja</span><span class="sxs-lookup"><span data-stu-id="804b2-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="804b2-117">Zainstalowany i karty aktualizacje teraz są sortowane alfabetycznie</span><span class="sxs-lookup"><span data-stu-id="804b2-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="804b2-118">Dodaje przycisk odświeżania, która umożliwia wyszukiwanie do odświeżenia</span><span class="sxs-lookup"><span data-stu-id="804b2-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="804b2-119">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="804b2-119">Updates and Improvements</span></span>

* <span data-ttu-id="804b2-120">Pakiety, do którego odwołuje się `project.json` , które mają zmiennoprzecinkowy wersji nie będzie aktualizowana przy każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="804b2-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="804b2-121">Zamiast tego zostanie zaktualizowana tylko wtedy, gdy zmuszeni do przywrócenia, czyszczenia, odbudować lub zmodyfikować `project.json`.</span><span class="sxs-lookup"><span data-stu-id="804b2-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="804b2-122">źródeł repozytorium nuget.org już jest zmuszony do konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="804b2-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="804b2-123">NuGet nie są już pakiety w udostępnionych projektach ani zapisuje plik blokady.</span><span class="sxs-lookup"><span data-stu-id="804b2-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="804b2-124">Firma Microsoft może udoskonalenia awarii sieci, a następnie ponów próbę obsługi dla serwerów niedostępne lub powolne odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="804b2-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="804b2-125">Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="804b2-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="804b2-126">Obsługujemy teraz najnowsze `project.json` schemat środowiska DNX.</span><span class="sxs-lookup"><span data-stu-id="804b2-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="804b2-127">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="804b2-127">Known Issues</span></span>

<span data-ttu-id="804b2-128">W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="804b2-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>