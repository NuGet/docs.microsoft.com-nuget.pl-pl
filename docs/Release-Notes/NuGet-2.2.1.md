---
title: Informacje o wersji NuGet 2.2.1
description: Informacje o wersji programu NuGet 2.2.1 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="0ea09-103">Informacje o wersji NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="0ea09-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="0ea09-104">[Informacje o wersji NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 informacje o wersji](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="0ea09-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="0ea09-105">NuGet 2.2.1 został wydany 15 lutego 2013.</span><span class="sxs-lookup"><span data-stu-id="0ea09-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="0ea09-106">Numer wersji rozszerzenia VS jest 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="0ea09-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="0ea09-107">Lokalizacja odświeżania</span><span class="sxs-lookup"><span data-stu-id="0ea09-107">Localization Refresh</span></span>
<span data-ttu-id="0ea09-108">Gdy NuGet jest dostarczane jako część programu Visual Studio 2012, został pełni zlokalizowanych na angielski + 13 innych języków.</span><span class="sxs-lookup"><span data-stu-id="0ea09-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="0ea09-109">Od tego czasu NuGet 2.1 i 2.2 został wysłany, ale lokalizacji gdyby nie zostały odświeżone.</span><span class="sxs-lookup"><span data-stu-id="0ea09-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="0ea09-110">W wersji NuGet 2.2.1 odświeża naszych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0ea09-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="0ea09-111">Interfejs użytkownika i konsoli programu PowerShell w narzędziu NuGet są zlokalizowane w następujących językach:</span><span class="sxs-lookup"><span data-stu-id="0ea09-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="0ea09-112">Chiński uproszczony</span><span class="sxs-lookup"><span data-stu-id="0ea09-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="0ea09-113">Chiński (tradycyjny)</span><span class="sxs-lookup"><span data-stu-id="0ea09-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="0ea09-114">czeski</span><span class="sxs-lookup"><span data-stu-id="0ea09-114">Czech</span></span>
1. <span data-ttu-id="0ea09-115">Angielski</span><span class="sxs-lookup"><span data-stu-id="0ea09-115">English</span></span>
1. <span data-ttu-id="0ea09-116">francuski</span><span class="sxs-lookup"><span data-stu-id="0ea09-116">French</span></span>
1. <span data-ttu-id="0ea09-117">niemiecki</span><span class="sxs-lookup"><span data-stu-id="0ea09-117">German</span></span>
1. <span data-ttu-id="0ea09-118">Włoski</span><span class="sxs-lookup"><span data-stu-id="0ea09-118">Italian</span></span>
1. <span data-ttu-id="0ea09-119">japoński</span><span class="sxs-lookup"><span data-stu-id="0ea09-119">Japanese</span></span>
1. <span data-ttu-id="0ea09-120">koreański</span><span class="sxs-lookup"><span data-stu-id="0ea09-120">Korean</span></span>
1. <span data-ttu-id="0ea09-121">polski</span><span class="sxs-lookup"><span data-stu-id="0ea09-121">Polish</span></span>
1. <span data-ttu-id="0ea09-122">portugalski (Brazylia)</span><span class="sxs-lookup"><span data-stu-id="0ea09-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="0ea09-123">Rosyjski</span><span class="sxs-lookup"><span data-stu-id="0ea09-123">Russian</span></span>
1. <span data-ttu-id="0ea09-124">Hiszpański</span><span class="sxs-lookup"><span data-stu-id="0ea09-124">Spanish</span></span>
1. <span data-ttu-id="0ea09-125">turecki</span><span class="sxs-lookup"><span data-stu-id="0ea09-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="0ea09-126">Szablony Visual Studio obsługują wielu repozytoriów pakietu preinstalowane</span><span class="sxs-lookup"><span data-stu-id="0ea09-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="0ea09-127">Jeśli musisz utworzyć szablony programu Visual Studio, można użyć NuGet do [preinstalowane pakiety](../visual-studio-extensibility/visual-studio-templates.md) w ramach szablonu.</span><span class="sxs-lookup"><span data-stu-id="0ea09-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="0ea09-128">Do tej pory, ta funkcja ma ograniczenie wszystkich pakietów konieczne pochodzą z tego samego źródła.</span><span class="sxs-lookup"><span data-stu-id="0ea09-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="0ea09-129">Jednak dzięki NuGet 2.2.1 mogą mieć pakiety zainstalowane z wielu repozytoriów (w szablonie, VSIX lub folderu na dysku zdefiniowana w rejestrze).</span><span class="sxs-lookup"><span data-stu-id="0ea09-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="0ea09-130">Scenariusz głównego dla tej funkcji jest niestandardowe szablony projektów programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0ea09-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="0ea09-131">Wbudowane szablony ASP.NET użyć wstępnie zainstalowane pakiety ściąganie pakiety z dysku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0ea09-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="0ea09-132">Można teraz utworzyć szablon niestandardowy projektu ASP.NET, który wykorzystuje istniejące pakiety zainstalowane przez platformę ASP.NET, ale Dodaj dodatkowe pakiety NuGet do szablonu.</span><span class="sxs-lookup"><span data-stu-id="0ea09-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="0ea09-133">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="0ea09-133">Bug Fixes</span></span>
<span data-ttu-id="0ea09-134">NuGet 2.2.1 obejmuje kilka poprawek błędów docelowych.</span><span class="sxs-lookup"><span data-stu-id="0ea09-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="0ea09-135">Lista prac elementów ustalone w NuGet 2.2.1, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="0ea09-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="0ea09-136">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="0ea09-136">Known Issues</span></span>

<span data-ttu-id="0ea09-137">Jeśli rozszerzania szablony projektów programu ASP.NET, wszystkie repozytoria preinstalowane pakietu należy używać tej samej wartości dla `isPreunzipped` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0ea09-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
