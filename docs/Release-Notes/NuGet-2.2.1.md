---
title: Informacje o wersji NuGet 2.2.1 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 39ceaeb3-2d33-4b1c-b195-eba36c6cbf9a
description: "Informacje o wersji programu NuGet 2.2.1 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.2.1 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c31150572b4b6e066643ebcf0d92be16b25c6e19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="52313-104">Informacje o wersji NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="52313-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="52313-105">[Informacje o wersji NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 informacje o wersji](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="52313-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="52313-106">NuGet 2.2.1 został wydany 15 lutego 2013.</span><span class="sxs-lookup"><span data-stu-id="52313-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="52313-107">Numer wersji rozszerzenia VS jest 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="52313-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="52313-108">Lokalizacja odświeżania</span><span class="sxs-lookup"><span data-stu-id="52313-108">Localization Refresh</span></span>
<span data-ttu-id="52313-109">Gdy NuGet jest dostarczane jako część programu Visual Studio 2012, został pełni zlokalizowanych na angielski + 13 innych języków.</span><span class="sxs-lookup"><span data-stu-id="52313-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="52313-110">Od tego czasu NuGet 2.1 i 2.2 został wysłany, ale lokalizacji gdyby nie zostały odświeżone.</span><span class="sxs-lookup"><span data-stu-id="52313-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="52313-111">W wersji NuGet 2.2.1 odświeża naszych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="52313-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="52313-112">Interfejs użytkownika i konsoli programu PowerShell w narzędziu NuGet są zlokalizowane w następujących językach:</span><span class="sxs-lookup"><span data-stu-id="52313-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="52313-113">Chiński uproszczony</span><span class="sxs-lookup"><span data-stu-id="52313-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="52313-114">Chiński (tradycyjny)</span><span class="sxs-lookup"><span data-stu-id="52313-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="52313-115">czeski</span><span class="sxs-lookup"><span data-stu-id="52313-115">Czech</span></span>
1. <span data-ttu-id="52313-116">angielski</span><span class="sxs-lookup"><span data-stu-id="52313-116">English</span></span>
1. <span data-ttu-id="52313-117">francuski</span><span class="sxs-lookup"><span data-stu-id="52313-117">French</span></span>
1. <span data-ttu-id="52313-118">niemiecki</span><span class="sxs-lookup"><span data-stu-id="52313-118">German</span></span>
1. <span data-ttu-id="52313-119">Włoski</span><span class="sxs-lookup"><span data-stu-id="52313-119">Italian</span></span>
1. <span data-ttu-id="52313-120">japoński</span><span class="sxs-lookup"><span data-stu-id="52313-120">Japanese</span></span>
1. <span data-ttu-id="52313-121">koreański</span><span class="sxs-lookup"><span data-stu-id="52313-121">Korean</span></span>
1. <span data-ttu-id="52313-122">polski</span><span class="sxs-lookup"><span data-stu-id="52313-122">Polish</span></span>
1. <span data-ttu-id="52313-123">portugalski (Brazylia)</span><span class="sxs-lookup"><span data-stu-id="52313-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="52313-124">Rosyjski</span><span class="sxs-lookup"><span data-stu-id="52313-124">Russian</span></span>
1. <span data-ttu-id="52313-125">Hiszpański</span><span class="sxs-lookup"><span data-stu-id="52313-125">Spanish</span></span>
1. <span data-ttu-id="52313-126">turecki</span><span class="sxs-lookup"><span data-stu-id="52313-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="52313-127">Szablony Visual Studio obsługują wielu repozytoriów pakietu preinstalowane</span><span class="sxs-lookup"><span data-stu-id="52313-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="52313-128">Jeśli musisz utworzyć szablony programu Visual Studio, można użyć NuGet do [preinstalowane pakiety](../visual-studio-extensibility/visual-studio-templates.md) w ramach szablonu.</span><span class="sxs-lookup"><span data-stu-id="52313-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="52313-129">Do tej pory, ta funkcja ma ograniczenie wszystkich pakietów konieczne pochodzą z tego samego źródła.</span><span class="sxs-lookup"><span data-stu-id="52313-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="52313-130">Jednak dzięki NuGet 2.2.1 mogą mieć pakiety zainstalowane z wielu repozytoriów (w szablonie, VSIX lub folderu na dysku zdefiniowana w rejestrze).</span><span class="sxs-lookup"><span data-stu-id="52313-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="52313-131">Scenariusz głównego dla tej funkcji jest niestandardowe szablony projektów programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="52313-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="52313-132">Wbudowane szablony ASP.NET użyć wstępnie zainstalowane pakiety ściąganie pakiety z dysku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="52313-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="52313-133">Można teraz utworzyć szablon niestandardowy projektu ASP.NET, który wykorzystuje istniejące pakiety zainstalowane przez platformę ASP.NET, ale Dodaj dodatkowe pakiety NuGet do szablonu.</span><span class="sxs-lookup"><span data-stu-id="52313-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="52313-134">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="52313-134">Bug Fixes</span></span>
<span data-ttu-id="52313-135">NuGet 2.2.1 obejmuje kilka poprawek błędów docelowych.</span><span class="sxs-lookup"><span data-stu-id="52313-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="52313-136">Lista prac elementów ustalone w NuGet 2.2.1, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="52313-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="52313-137">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="52313-137">Known Issues</span></span>

<span data-ttu-id="52313-138">Jeśli rozszerzania szablony projektów programu ASP.NET, wszystkie repozytoria preinstalowane pakietu należy używać tej samej wartości dla `isPreunzipped` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="52313-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
