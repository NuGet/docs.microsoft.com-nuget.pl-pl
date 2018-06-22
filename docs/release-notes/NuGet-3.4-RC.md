---
title: Informacje o wersji 3.4 RC NuGet
description: Informacje o wersji programu NuGet 3.4 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820823"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="b7d96-103">Informacje o wersji 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="b7d96-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="b7d96-104">[Informacje o wersji NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 informacje o wersji](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="b7d96-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="b7d96-105">NuGet 3.4-RC został wydany 3 marca 2016 obok programu Visual Studio 2015 Update 2 RC i został skompilowany z kilka rozwiązań w umysły:</span><span class="sxs-lookup"><span data-stu-id="b7d96-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="b7d96-106">Obsługa Platform</span><span class="sxs-lookup"><span data-stu-id="b7d96-106">Cross-Platform support</span></span>
* <span data-ttu-id="b7d96-107">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="b7d96-107">Performance improvements</span></span>
* <span data-ttu-id="b7d96-108">Drobne ulepszenia interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="b7d96-108">Minor UI improvements</span></span>

<span data-ttu-id="b7d96-109">Następujące funkcje są dostępne w tej wersji RC z planowane 3.4 ostatecznej wersji.</span><span class="sxs-lookup"><span data-stu-id="b7d96-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="b7d96-110">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="b7d96-110">New Features</span></span>

* <span data-ttu-id="b7d96-111">Klienci NuGet obsługuje teraz, kodowania zawartości gzip z repozytoriami</span><span class="sxs-lookup"><span data-stu-id="b7d96-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="b7d96-112">Obsługa baz danych PDB z pakietów w projektach xproj</span><span class="sxs-lookup"><span data-stu-id="b7d96-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="b7d96-113">Akcje w elemencie contentFiles kompilacji pomocy technicznej dla systemów iOS i Android</span><span class="sxs-lookup"><span data-stu-id="b7d96-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="b7d96-114">Obsługa krótkich nazw netstandard i netstandardapp monikerów framework</span><span class="sxs-lookup"><span data-stu-id="b7d96-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="b7d96-115">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="b7d96-115">New User Interface Features</span></span>

* <span data-ttu-id="b7d96-116">Znaczący wzrost wydajności szczególnie na kartach zainstalowane aktualizacje i Konsoliduj</span><span class="sxs-lookup"><span data-stu-id="b7d96-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="b7d96-117">Zainstalowane i aktualizacje kartach teraz są posortowane alfabetycznie</span><span class="sxs-lookup"><span data-stu-id="b7d96-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="b7d96-118">Dodaje przycisk Odśwież, która umożliwia wyszukiwanie, którego chcesz odświeżyć</span><span class="sxs-lookup"><span data-stu-id="b7d96-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b7d96-119">Aktualizacje i usprawnienia</span><span class="sxs-lookup"><span data-stu-id="b7d96-119">Updates and Improvements</span></span>

* <span data-ttu-id="b7d96-120">Pakiety, do którego odwołuje się `project.json` , która ma zmiennoprzecinkową wersji nie będzie aktualizowany przy każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b7d96-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="b7d96-121">Zamiast tego zostanie zaktualizowana tylko wtedy, gdy wymusić przywracanie, czyszczenia, odbudować lub zmodyfikować `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b7d96-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="b7d96-122">źródłach repozytoriów nuget.org już zostało wymuszone w konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="b7d96-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="b7d96-123">NuGet już przywraca pakietów w udostępnionych projektów nie zapisuje plik blokady.</span><span class="sxs-lookup"><span data-stu-id="b7d96-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="b7d96-124">Firma Microsoft została ulepszona awarii sieci, a następnie spróbuj ponownie obsługi dla serwerów jest nieosiągalny lub powolne na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="b7d96-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="b7d96-125">Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7d96-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="b7d96-126">Obsługujemy teraz najnowszej `project.json` schematu w DNX.</span><span class="sxs-lookup"><span data-stu-id="b7d96-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="b7d96-127">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="b7d96-127">Known Issues</span></span>

<span data-ttu-id="b7d96-128">W dalszym ciągu śledzenie problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="b7d96-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>