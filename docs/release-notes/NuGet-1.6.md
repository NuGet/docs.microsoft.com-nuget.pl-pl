---
title: Informacje o wersji narzędzia NuGet 1,6
description: Informacje o wersji programu NuGet 1,6, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384140"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="0a97a-103">Informacje o wersji narzędzia NuGet 1,6</span><span class="sxs-lookup"><span data-stu-id="0a97a-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="0a97a-104">[Informacje o wersji pakietu nuget 1,5](../release-notes/nuget-1.5.md) | [Informacje o wersji narzędzia NuGet 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="0a97a-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="0a97a-105">Pakiet NuGet 1,6 został opublikowany 13 grudnia 2011.</span><span class="sxs-lookup"><span data-stu-id="0a97a-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="0a97a-106">Znany problem z instalacją</span><span class="sxs-lookup"><span data-stu-id="0a97a-106">Known Installation Issue</span></span>
<span data-ttu-id="0a97a-107">W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.</span><span class="sxs-lookup"><span data-stu-id="0a97a-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="0a97a-108">Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="0a97a-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="0a97a-109">Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="0a97a-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="0a97a-110">Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".</span><span class="sxs-lookup"><span data-stu-id="0a97a-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="0a97a-111">Funkcje</span><span class="sxs-lookup"><span data-stu-id="0a97a-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="0a97a-112">Obsługa wersji semantycznych i pakietów wstępnych</span><span class="sxs-lookup"><span data-stu-id="0a97a-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="0a97a-113">Pakiet NuGet 1,6 wprowadza obsługę wersji semantycznej (SemVer).</span><span class="sxs-lookup"><span data-stu-id="0a97a-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="0a97a-114">Aby uzyskać więcej informacji na temat korzystania z SemVer, Przeczytaj [dokumentację dotyczącą wersji](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0a97a-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="0a97a-115">Używanie narzędzia NuGet bez sprawdzania pakietów (Przywracanie pakietu)</span><span class="sxs-lookup"><span data-stu-id="0a97a-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="0a97a-116">Pakiet NuGet 1,6 ma teraz obsługę pierwszej klasy dla przepływu pracy, w którym pakiety NuGet nie są dodawane do kontroli źródła, ale w razie braku są przywracane w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0a97a-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="0a97a-117">Aby uzyskać więcej informacji, zapoznaj się z tematem [Używanie narzędzia NuGet bez zatwierdzania pakietów do kontroli źródła](../consume-packages/packages-and-source-control.md) .</span><span class="sxs-lookup"><span data-stu-id="0a97a-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="0a97a-118">Szablony elementów instalujących pakiety NuGet</span><span class="sxs-lookup"><span data-stu-id="0a97a-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="0a97a-119">Kompilowanie pracy w celu obsługi wstępnie zainstalowanego pakietu NuGet w szablonach projektów programu Visual Studio, NuGet 1,6 również dodaje obsługę szablonów elementów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0a97a-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="0a97a-120">Szablony elementów mogą mieć skojarzone pakiety NuGet, które są instalowane, gdy szablon jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="0a97a-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="0a97a-121">Aby uzyskać więcej informacji na temat zmiany szablonu projektu/elementu w celu zainstalowania pakietów NuGet, przeczytaj temat [pakiety w temacie szablony programu Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="0a97a-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="0a97a-122">Obsługa wyłączania źródeł pakietów</span><span class="sxs-lookup"><span data-stu-id="0a97a-122">Support for disabling package sources</span></span>
<span data-ttu-id="0a97a-123">W przypadku skonfigurowania wielu źródeł pakietów pakiet NuGet będzie wyglądał dla pakietów podczas instalacji pakietu i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="0a97a-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="0a97a-124">Źródło pakietu, które nie działa z jakiegoś powodu, może poważnie spowalniać działanie programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="0a97a-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="0a97a-125">Przed pakietem NuGet 1,6 można było usunąć źródło pakietu, ale należy pamiętać o tym, że trzeba będzie je dodać z powrotem do programu.</span><span class="sxs-lookup"><span data-stu-id="0a97a-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="0a97a-126">Pakiet NuGet 1,6 umożliwia odszukanie źródła pakietu, aby je wyłączyć, ale zachować jego zachowanie.</span><span class="sxs-lookup"><span data-stu-id="0a97a-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Wyłączanie pakietu](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="0a97a-128">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="0a97a-128">Bug Fixes</span></span>
<span data-ttu-id="0a97a-129">Pakiet NuGet 1,6 zawiera łącznie 106 elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="0a97a-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="0a97a-130">95 z tych elementów zostało sklasyfikowanych jako błędy i 10 z nich.</span><span class="sxs-lookup"><span data-stu-id="0a97a-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="0a97a-131">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,6, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="0a97a-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
