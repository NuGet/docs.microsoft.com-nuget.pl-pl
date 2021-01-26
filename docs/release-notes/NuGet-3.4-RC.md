---
title: Pakiet NuGet 3,4 — Informacje o wersji RC
description: Informacje o wersji programu NuGet 3,4 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780242"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="6f2a3-103">Pakiet NuGet 3,4 — Informacje o wersji RC</span><span class="sxs-lookup"><span data-stu-id="6f2a3-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="6f2a3-104">Informacje o wersji narzędzia [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Informacje o wersji narzędzia NuGet 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="6f2a3-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="6f2a3-105">Pakiet NuGet 3,4-RC został wydana 3 marca, 2016 obok programu Visual Studio 2015 Update 2 RC i został skompilowany za pomocą kilku założenia w zdanie:</span><span class="sxs-lookup"><span data-stu-id="6f2a3-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="6f2a3-106">Obsługa wielu platform</span><span class="sxs-lookup"><span data-stu-id="6f2a3-106">Cross-Platform support</span></span>
* <span data-ttu-id="6f2a3-107">Usprawnienia wydajności</span><span class="sxs-lookup"><span data-stu-id="6f2a3-107">Performance improvements</span></span>
* <span data-ttu-id="6f2a3-108">Ulepszenia pomocniczych interfejsów użytkownika</span><span class="sxs-lookup"><span data-stu-id="6f2a3-108">Minor UI improvements</span></span>

<span data-ttu-id="6f2a3-109">W tej wersji RC dostępne są następujące funkcje z zaplanowanymi wersjami ostateczną 3,4.</span><span class="sxs-lookup"><span data-stu-id="6f2a3-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="6f2a3-110">Nowe funkcje</span><span class="sxs-lookup"><span data-stu-id="6f2a3-110">New Features</span></span>

* <span data-ttu-id="6f2a3-111">Klienci NuGet obsługują teraz kodowanie zawartości gzip z repozytoriów</span><span class="sxs-lookup"><span data-stu-id="6f2a3-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="6f2a3-112">Obsługa plików PDB z pakietów w projektach xproj</span><span class="sxs-lookup"><span data-stu-id="6f2a3-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="6f2a3-113">Obsługa akcji kompilacji dla systemów iOS i Android w elemencie contentFiles</span><span class="sxs-lookup"><span data-stu-id="6f2a3-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="6f2a3-114">Obsługa krótkich monikerów struktury netstandardapp</span><span class="sxs-lookup"><span data-stu-id="6f2a3-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="6f2a3-115">Nowe funkcje interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="6f2a3-115">New User Interface Features</span></span>

* <span data-ttu-id="6f2a3-116">Znaczące ulepszenia wydajności dotyczące kart zainstalowanych, aktualizacji i konsolidowania</span><span class="sxs-lookup"><span data-stu-id="6f2a3-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="6f2a3-117">Karty zainstalowane i aktualizacje są teraz sortowane alfabetycznie</span><span class="sxs-lookup"><span data-stu-id="6f2a3-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="6f2a3-118">Dodano przycisk odświeżania, który umożliwia odświeżenie wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="6f2a3-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="6f2a3-119">Aktualizacje i ulepszenia</span><span class="sxs-lookup"><span data-stu-id="6f2a3-119">Updates and Improvements</span></span>

* <span data-ttu-id="6f2a3-120">Pakiety, do których się odwołują `project.json` , mają przepływającą wersję, nie będą aktualizowane dla każdej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="6f2a3-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="6f2a3-121">Zamiast tego zostaną one zaktualizowane tylko wtedy, gdy zostanie wymuszone przywrócenie, oczyszczenie, odbudowanie lub zmodyfikowanie `project.json` .</span><span class="sxs-lookup"><span data-stu-id="6f2a3-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="6f2a3-122">źródła repozytorium nuget.org nie są już wymuszane w konfiguracji projektu podczas korzystania z interfejsu użytkownika konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="6f2a3-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="6f2a3-123">Pakiet NuGet nie przywraca już pakietów w projektach udostępnionych ani nie zapisuje pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="6f2a3-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="6f2a3-124">Ulepszono awarię sieci i obsługę ponownych prób w przypadku nieosiągalnych lub wolnych serwerów.</span><span class="sxs-lookup"><span data-stu-id="6f2a3-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="6f2a3-125">W interfejsie użytkownika Menedżera pakietów programu Visual Studio Ulepszono zachowania klawiatury i myszy.</span><span class="sxs-lookup"><span data-stu-id="6f2a3-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="6f2a3-126">Teraz obsługujemy najnowszy `project.json` schemat w programie środowiska DNX.</span><span class="sxs-lookup"><span data-stu-id="6f2a3-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6f2a3-127">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="6f2a3-127">Known Issues</span></span>

<span data-ttu-id="6f2a3-128">Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="6f2a3-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>