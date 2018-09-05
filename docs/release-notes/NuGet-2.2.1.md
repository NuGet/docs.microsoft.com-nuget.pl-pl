---
title: Informacje o wersji NuGet 2.2.1
description: Informacje o wersji programu NuGet 2.2.1 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550701"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="11d73-103">Informacje o wersji NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="11d73-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="11d73-104">[Informacje o wersji NuGet 2.2](../release-notes/nuget-2.2.md) | [informacjach o wersji NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="11d73-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="11d73-105">NuGet 2.2.1 15 lutego 2013 został wydany.</span><span class="sxs-lookup"><span data-stu-id="11d73-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="11d73-106">Numer wersji rozszerzenia programu VS jest 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="11d73-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="11d73-107">Lokalizacja odświeżania</span><span class="sxs-lookup"><span data-stu-id="11d73-107">Localization Refresh</span></span>
<span data-ttu-id="11d73-108">Gdy NuGet jest dostarczana jako część programu Visual Studio 2012, w pełni został zlokalizowany do języka angielskiego + 13 innych języków.</span><span class="sxs-lookup"><span data-stu-id="11d73-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="11d73-109">Od tamtej pory NuGet 2.1 i 2.2 zostały wprowadzone do użytku, ale nie miał zostały odświeżone lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="11d73-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="11d73-110">Wersji NuGet 2.2.1 odświeża naszych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="11d73-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="11d73-111">Konsoli programu PowerShell i interfejsu użytkownika NuGet są zlokalizowane w następujących językach:</span><span class="sxs-lookup"><span data-stu-id="11d73-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="11d73-112">Chiński uproszczony</span><span class="sxs-lookup"><span data-stu-id="11d73-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="11d73-113">Chiński (tradycyjny)</span><span class="sxs-lookup"><span data-stu-id="11d73-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="11d73-114">czeski</span><span class="sxs-lookup"><span data-stu-id="11d73-114">Czech</span></span>
1. <span data-ttu-id="11d73-115">Angielski</span><span class="sxs-lookup"><span data-stu-id="11d73-115">English</span></span>
1. <span data-ttu-id="11d73-116">francuski</span><span class="sxs-lookup"><span data-stu-id="11d73-116">French</span></span>
1. <span data-ttu-id="11d73-117">niemiecki</span><span class="sxs-lookup"><span data-stu-id="11d73-117">German</span></span>
1. <span data-ttu-id="11d73-118">Włoski</span><span class="sxs-lookup"><span data-stu-id="11d73-118">Italian</span></span>
1. <span data-ttu-id="11d73-119">japoński</span><span class="sxs-lookup"><span data-stu-id="11d73-119">Japanese</span></span>
1. <span data-ttu-id="11d73-120">koreański</span><span class="sxs-lookup"><span data-stu-id="11d73-120">Korean</span></span>
1. <span data-ttu-id="11d73-121">polski</span><span class="sxs-lookup"><span data-stu-id="11d73-121">Polish</span></span>
1. <span data-ttu-id="11d73-122">portugalski (Brazylia)</span><span class="sxs-lookup"><span data-stu-id="11d73-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="11d73-123">Rosyjski</span><span class="sxs-lookup"><span data-stu-id="11d73-123">Russian</span></span>
1. <span data-ttu-id="11d73-124">Hiszpański</span><span class="sxs-lookup"><span data-stu-id="11d73-124">Spanish</span></span>
1. <span data-ttu-id="11d73-125">turecki</span><span class="sxs-lookup"><span data-stu-id="11d73-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="11d73-126">Szablony programu Visual Studio obsługują wiele repozytoriów preinstalowanych pakietu</span><span class="sxs-lookup"><span data-stu-id="11d73-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="11d73-127">W przypadku utworzenia szablonów programu Visual Studio, można użyć NuGet, aby [przed instalacją pakietów](../visual-studio-extensibility/visual-studio-templates.md) jako część szablonu.</span><span class="sxs-lookup"><span data-stu-id="11d73-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="11d73-128">Do tej pory ta funkcja ma ograniczenie, wszystkie pakiety wymagane pochodziły z tego samego źródła.</span><span class="sxs-lookup"><span data-stu-id="11d73-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="11d73-129">Jednak z NuGet 2.2.1 może mieć zainstalowane pakiety z wielu repozytoriów (w szablonie VSIX lub folderu na dysku, zdefiniowana w rejestrze).</span><span class="sxs-lookup"><span data-stu-id="11d73-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="11d73-130">Scenariusz głównego dla tej funkcji jest niestandardowe szablony projektów programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="11d73-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="11d73-131">Wbudowane szablony platformy ASP.NET za pomocą pakietów wstępnie zainstalowane, ściąganie pakiety z dysku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="11d73-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="11d73-132">Można teraz utworzyć szablonu niestandardowego projektu ASP.NET, który wykorzystuje istniejące pakiety instalowane przez platformę ASP.NET, ale Dodaj dodatkowe pakiety NuGet do szablonu.</span><span class="sxs-lookup"><span data-stu-id="11d73-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="11d73-133">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="11d73-133">Bug Fixes</span></span>
<span data-ttu-id="11d73-134">NuGet 2.2.1 zawiera kilka poprawek błędów docelowych.</span><span class="sxs-lookup"><span data-stu-id="11d73-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="11d73-135">Lista prac elementów rozwiązane w NuGet 2.2.1, sprawdź widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="11d73-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="11d73-136">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="11d73-136">Known Issues</span></span>

<span data-ttu-id="11d73-137">Jeśli rozszerzania szablony projektów programu ASP.NET, wszystkie repozytoria pakiet wstępnie zainstalowane, należy użyć taką samą wartość `isPreunzipped` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="11d73-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
