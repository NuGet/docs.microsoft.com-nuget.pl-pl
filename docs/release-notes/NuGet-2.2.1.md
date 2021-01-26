---
title: Informacje o wersji pakietu NuGet 2.2.1
description: Informacje o wersji programu NuGet 2.2.1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776809"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="c8d6d-103">Informacje o wersji pakietu NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="c8d6d-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="c8d6d-104">Informacje o wersji narzędzia [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Informacje o wersji narzędzia NuGet 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="c8d6d-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="c8d6d-105">Program NuGet 2.2.1 został opublikowany 15 lutego 2013.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="c8d6d-106">Numer wersji rozszerzenia programu VS to 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="c8d6d-107">Odświeżanie lokalizacji</span><span class="sxs-lookup"><span data-stu-id="c8d6d-107">Localization Refresh</span></span>
<span data-ttu-id="c8d6d-108">Gdy pakiet NuGet dostarczany jako część programu Visual Studio 2012, został w pełni zlokalizowany w języku angielskim + 13 innych językach.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="c8d6d-109">Od tego czasu NuGet 2,1 i 2,2 zostały wysłane, ale lokalizacja nie została odświeżona.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="c8d6d-110">Wydanie NuGet 2.2.1 spowoduje odświeżenie naszej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="c8d6d-111">Interfejs użytkownika i konsola programu PowerShell narzędzia NuGet są zlokalizowane w następujących językach:</span><span class="sxs-lookup"><span data-stu-id="c8d6d-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="c8d6d-112">Chiński (uproszczony)</span><span class="sxs-lookup"><span data-stu-id="c8d6d-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="c8d6d-113">Chiński (tradycyjny)</span><span class="sxs-lookup"><span data-stu-id="c8d6d-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="c8d6d-114">Czeski</span><span class="sxs-lookup"><span data-stu-id="c8d6d-114">Czech</span></span>
1. <span data-ttu-id="c8d6d-115">Angielski</span><span class="sxs-lookup"><span data-stu-id="c8d6d-115">English</span></span>
1. <span data-ttu-id="c8d6d-116">Francuski</span><span class="sxs-lookup"><span data-stu-id="c8d6d-116">French</span></span>
1. <span data-ttu-id="c8d6d-117">niemiecki</span><span class="sxs-lookup"><span data-stu-id="c8d6d-117">German</span></span>
1. <span data-ttu-id="c8d6d-118">Włoski</span><span class="sxs-lookup"><span data-stu-id="c8d6d-118">Italian</span></span>
1. <span data-ttu-id="c8d6d-119">japoński</span><span class="sxs-lookup"><span data-stu-id="c8d6d-119">Japanese</span></span>
1. <span data-ttu-id="c8d6d-120">koreański</span><span class="sxs-lookup"><span data-stu-id="c8d6d-120">Korean</span></span>
1. <span data-ttu-id="c8d6d-121">polski</span><span class="sxs-lookup"><span data-stu-id="c8d6d-121">Polish</span></span>
1. <span data-ttu-id="c8d6d-122">portugalski (Brazylia)</span><span class="sxs-lookup"><span data-stu-id="c8d6d-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="c8d6d-123">Rosyjski</span><span class="sxs-lookup"><span data-stu-id="c8d6d-123">Russian</span></span>
1. <span data-ttu-id="c8d6d-124">Hiszpański</span><span class="sxs-lookup"><span data-stu-id="c8d6d-124">Spanish</span></span>
1. <span data-ttu-id="c8d6d-125">turecki</span><span class="sxs-lookup"><span data-stu-id="c8d6d-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="c8d6d-126">Szablony programu Visual Studio obsługują wiele preinstalowanych repozytoriów pakietów</span><span class="sxs-lookup"><span data-stu-id="c8d6d-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="c8d6d-127">W przypadku tworzenia szablonów programu Visual Studio można użyć narzędzia NuGet do [preinstalacji pakietów](../visual-studio-extensibility/visual-studio-templates.md) jako części szablonu.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="c8d6d-128">Do tej pory ta funkcja miała ograniczenie, że wszystkie pakiety muszą pochodzić z tego samego źródła.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="c8d6d-129">W przypadku programu NuGet 2.2.1 mimo że pakiety są instalowane z wielu repozytoriów (w ramach szablonu, VSIX lub folderu na dysku zdefiniowanym w rejestrze).</span><span class="sxs-lookup"><span data-stu-id="c8d6d-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="c8d6d-130">Głównym scenariuszem tej funkcji są niestandardowe szablony projektów ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="c8d6d-131">Wbudowane szablony ASP.NET używają wstępnie zainstalowanych pakietów, pobierając pakiety z dysku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="c8d6d-132">Teraz można utworzyć niestandardowy szablon projektu ASP.NET, który używa istniejących pakietów instalowanych przez ASP.NET, ale dodając do szablonu dodatkowe pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c8d6d-133">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="c8d6d-133">Bug Fixes</span></span>
<span data-ttu-id="c8d6d-134">Pakiet NuGet 2.2.1 zawiera kilka dokierowanych poprawek błędów.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="c8d6d-135">Aby zapoznać się z listą elementów roboczych ustalonych w NuGet 2.2.1, zobacz [monitor problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="c8d6d-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="c8d6d-136">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="c8d6d-136">Known Issues</span></span>

<span data-ttu-id="c8d6d-137">W przypadku rozszerzania szablonów projektów ASP.NET wszystkie wstępnie zainstalowane repozytoria pakietów muszą używać tej samej wartości `isPreunzipped` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="c8d6d-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
