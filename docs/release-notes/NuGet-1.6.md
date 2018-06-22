---
title: Informacje o wersji 1.6 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr NuGet w wersji 1.6.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0345e180893a56302385d27792c4e15ba5d96989
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820602"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="d8969-103">Informacje o wersji 1.6 NuGet</span><span class="sxs-lookup"><span data-stu-id="d8969-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="d8969-104">[Informacje o wersji NuGet w wersji 1.5](../release-notes/nuget-1.5.md) | [NuGet 1.7 informacje o wersji](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="d8969-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="d8969-105">NuGet w wersji 1.6 został wydany 13 grudnia 2011.</span><span class="sxs-lookup"><span data-stu-id="d8969-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="d8969-106">Znane problem</span><span class="sxs-lookup"><span data-stu-id="d8969-106">Known Installation Issue</span></span>
<span data-ttu-id="d8969-107">Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d8969-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="d8969-108">Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="d8969-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="d8969-109">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d8969-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="d8969-110">Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".</span><span class="sxs-lookup"><span data-stu-id="d8969-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="d8969-111">Funkcje</span><span class="sxs-lookup"><span data-stu-id="d8969-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="d8969-112">Obsługa Wersjonowania semantycznego i pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="d8969-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="d8969-113">NuGet 1.6 wprowadzono obsługę Wersjonowania semantycznego (programu SemVer).</span><span class="sxs-lookup"><span data-stu-id="d8969-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="d8969-114">Aby uzyskać więcej informacji o używaniu go programu SemVer, przeczytaj [dokumentacji Versioning](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d8969-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="d8969-115">Bez sprawdzania w pakietach (Przywracanie pakietu) przy użyciu narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="d8969-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="d8969-116">NuGet w wersji 1.6 ma teraz obsługę aparatów przepływu pracy, w których NuGet nie zostaną dodane do kontroli źródła pakietów, ale zamiast tego są przywracane podczas kompilacji Brak.</span><span class="sxs-lookup"><span data-stu-id="d8969-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="d8969-117">Aby uzyskać więcej informacji, przeczytaj [za pomocą NuGet bez zatwierdzania pakietów do kontroli źródła](../consume-packages/packages-and-source-control.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="d8969-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="d8969-118">Szablony elementów, które zainstalować pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="d8969-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="d8969-119">Korzystając z pracy do obsługi wstępnie zainstalowane pakiet NuGet do szablony projektu Visual Studio, NuGet w wersji 1.6 również dodaje obsługę szablony elementów Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8969-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="d8969-120">Szablony elementów może mieć skojarzone pakiety NuGet, które są instalowane przy szablonu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="d8969-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="d8969-121">Aby uzyskać więcej informacji na temat zmiany szablonu projektu/elementu można zainstalować pakietów NuGet, przeczytaj [pakietów w szablony Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="d8969-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="d8969-122">Obsługa wyłączenie źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="d8969-122">Support for disabling package sources</span></span>
<span data-ttu-id="d8969-123">Jeśli skonfigurowano wiele źródeł pakietów, NuGet będzie wyglądać w każdej z nich pakietów podczas instalowania pakietu i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="d8969-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="d8969-124">Źródło pakietu, który nie działa dla jakiegoś powodu może poważnie wolno dół NuGet.</span><span class="sxs-lookup"><span data-stu-id="d8969-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="d8969-125">Przed NuGet w wersji 1.6 można usunąć źródła pakietów, ale następnie należy pamiętać, że szczegółowe informacje, gdy chcesz dodać ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="d8969-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="d8969-126">NuGet w wersji 1.6 umożliwia zaznaczenie pola wyboru źródła pakietów, aby ją wyłączyć, ale zachować ją wokół.</span><span class="sxs-lookup"><span data-stu-id="d8969-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Wyłączanie pakietu](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="d8969-128">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="d8969-128">Bug Fixes</span></span>
<span data-ttu-id="d8969-129">NuGet w wersji 1.6 było łącznie 106 stałej elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="d8969-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="d8969-130">95 tych zostały sklasyfikowane jako usterki i 10 tych były funkcji.</span><span class="sxs-lookup"><span data-stu-id="d8969-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="d8969-131">Pełną listę prac elementów usunięto w wersji NuGet w wersji 1.6, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d8969-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
