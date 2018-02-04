---
title: Informacje o wersji 3.4 RC NuGet | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.4 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.4 informacje o wersji RC, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 749068683d6e2a3fd9dd29c69d9ff50137acdd46
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="b99d8-104">Informacje o wersji 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="b99d8-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="b99d8-105">[Informacje o wersji NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 informacje o wersji](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="b99d8-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="b99d8-106">NuGet 3.4-RC został wydany 3 marca 2016 obok programu Visual Studio 2015 Update 2 RC i został skompilowany z kilka rozwiązań w umysły:</span><span class="sxs-lookup"><span data-stu-id="b99d8-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="b99d8-107">Obsługa Platform</span><span class="sxs-lookup"><span data-stu-id="b99d8-107">Cross-Platform support</span></span>
* <span data-ttu-id="b99d8-108">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="b99d8-108">Performance improvements</span></span>
* <span data-ttu-id="b99d8-109">Drobne ulepszenia interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="b99d8-109">Minor UI improvements</span></span>

<span data-ttu-id="b99d8-110">Następujące funkcje są dostępne w tej wersji RC z planowane 3.4 ostatecznej wersji.</span><span class="sxs-lookup"><span data-stu-id="b99d8-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="b99d8-111">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="b99d8-111">New Features</span></span>

* <span data-ttu-id="b99d8-112">Klienci NuGet obsługuje teraz, kodowania zawartości gzip z repozytoriami</span><span class="sxs-lookup"><span data-stu-id="b99d8-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="b99d8-113">Obsługa baz danych PDB z pakietów w projektach xproj</span><span class="sxs-lookup"><span data-stu-id="b99d8-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="b99d8-114">Akcje w elemencie contentFiles kompilacji pomocy technicznej dla systemów iOS i Android</span><span class="sxs-lookup"><span data-stu-id="b99d8-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="b99d8-115">Obsługa krótkich nazw netstandard i netstandardapp monikerów framework</span><span class="sxs-lookup"><span data-stu-id="b99d8-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="b99d8-116">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="b99d8-116">New User Interface Features</span></span>

* <span data-ttu-id="b99d8-117">Znaczący wzrost wydajności szczególnie na kartach zainstalowane aktualizacje i Konsoliduj</span><span class="sxs-lookup"><span data-stu-id="b99d8-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="b99d8-118">Zainstalowane i aktualizacje kartach teraz są posortowane alfabetycznie</span><span class="sxs-lookup"><span data-stu-id="b99d8-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="b99d8-119">Dodaje przycisk Odśwież, która umożliwia wyszukiwanie, którego chcesz odświeżyć</span><span class="sxs-lookup"><span data-stu-id="b99d8-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b99d8-120">Aktualizacje i usprawnienia</span><span class="sxs-lookup"><span data-stu-id="b99d8-120">Updates and Improvements</span></span>

* <span data-ttu-id="b99d8-121">Pakiety, do którego odwołuje się `project.json` , która ma zmiennoprzecinkową wersji nie będzie aktualizowany przy każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b99d8-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="b99d8-122">Zamiast tego zostanie zaktualizowana tylko wtedy, gdy wymusić przywracanie, czyszczenia, odbudować lub zmodyfikować `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b99d8-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="b99d8-123">źródłach repozytoriów nuget.org już zostało wymuszone w konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="b99d8-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="b99d8-124">NuGet już przywraca pakietów w udostępnionych projektów nie zapisuje plik blokady.</span><span class="sxs-lookup"><span data-stu-id="b99d8-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="b99d8-125">Firma Microsoft została ulepszona awarii sieci, a następnie spróbuj ponownie obsługi dla serwerów jest nieosiągalny lub powolne na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="b99d8-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="b99d8-126">Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b99d8-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="b99d8-127">Obsługujemy teraz najnowszej `project.json` schematu w DNX.</span><span class="sxs-lookup"><span data-stu-id="b99d8-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="b99d8-128">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="b99d8-128">Known Issues</span></span>

<span data-ttu-id="b99d8-129">W dalszym ciągu do śledzenia problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="b99d8-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>