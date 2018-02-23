---
title: "2.6.1 NuGet, aby uzyskać informacje o wersji programu WebMatrix | Dokumentacja firmy Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Informacje o wersji programu NuGet 2.6.1 dla programu WebMatrix, w tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: "NuGet 2.6.1 informacje o wersji programu WebMatrix, poprawki, znanych problemów, nowe funkcje, dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 633b71011dd1bc897ad95fd706337cef3aeef34c
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="7d04b-104">2.6.1 NuGet, aby uzyskać informacje o wersji programu WebMatrix</span><span class="sxs-lookup"><span data-stu-id="7d04b-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="7d04b-105">[Informacje o wersji NuGet 2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7 informacje o wersji](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="7d04b-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="7d04b-106">Zespół NuGet wydany zaktualizowane rozszerzenie NuGet Package Manager dla programu WebMatrix 26 marca 2014 r.</span><span class="sxs-lookup"><span data-stu-id="7d04b-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="7d04b-107">Tę aktualizację można zainstalować z [galerii rozszerzeń programu WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7d04b-107">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="7d04b-108">Otwórz program WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7d04b-108">Open WebMatrix 3</span></span>
1. <span data-ttu-id="7d04b-109">Kliknij ikonę rozszerzeń na Wstążce głównej</span><span class="sxs-lookup"><span data-stu-id="7d04b-109">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="7d04b-110">Wybierz kartę aktualizacji</span><span class="sxs-lookup"><span data-stu-id="7d04b-110">Select the Updates tab</span></span>
1. <span data-ttu-id="7d04b-111">Kliknij, aby zaktualizować Menedżera pakietów NuGet do 2.6.1</span><span class="sxs-lookup"><span data-stu-id="7d04b-111">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="7d04b-112">Zamknij i uruchom ponownie program WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7d04b-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="7d04b-113">Ważne zmiany</span><span class="sxs-lookup"><span data-stu-id="7d04b-113">Notable Changes</span></span>

<span data-ttu-id="7d04b-114">To rozszerzenie aktualizacji adresy dwa największych problemów użytkowników ma muszą ponosić odbierającą pakietów NuGet w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7d04b-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="7d04b-115">Pierwszy błąd NuGet w wersji schematu, a drugi czasami jest usterka, co może prowadzić do biblioteki DLL zero bajtów w `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="7d04b-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="7d04b-116">Błąd wersji schematu NuGet</span><span class="sxs-lookup"><span data-stu-id="7d04b-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="7d04b-117">Od czasu wydania programu WebMatrix 3, NuGet, która wymaga nowej wersji schematu do pakietów NuGet wprowadzono nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="7d04b-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="7d04b-118">Podczas próby Zarządzanie pakietów NuGet w witrynie sieci web, te nowe pakiety może prowadzić do błędów, które są wyświetlane w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7d04b-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Wystąpił błąd.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="7d04b-122">Tej najnowszej wersji zapewnia zgodność z najnowszych pakietów NuGet, uniemożliwia wystąpienia tego błędu.</span><span class="sxs-lookup"><span data-stu-id="7d04b-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="7d04b-123">Teraz można zainstalować nowe wersje pakietów w tym Microsoft.AspNet.WebPages w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7d04b-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="7d04b-124">Niektóre z tych pakietów NuGet funkcji były używane takie jak [przekształca XDT config](../release-notes/nuget-2.6.md#xdt), który nie był obsługiwany w programie WebMatrix do tej pory.</span><span class="sxs-lookup"><span data-stu-id="7d04b-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="7d04b-125">Biblioteki DLL zero bajtów w pojemniku folderu</span><span class="sxs-lookup"><span data-stu-id="7d04b-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="7d04b-126">W przypadku niektórych użytkowników wykazały, że po instalowania NuGet pakietów w programie WebMatrix, obejmujących bibliotek DLL, które uzyskać skopiowane do bin, który Pokaż biblioteki dll w `bin` folderze co pliki 0 bajtów.</span><span class="sxs-lookup"><span data-stu-id="7d04b-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="7d04b-127">To spowoduje przerwanie aplikacji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7d04b-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="7d04b-128">[Ten problem](https://nuget.codeplex.com/workitem/4060) teraz został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="7d04b-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="7d04b-129">Inne ulepszenia ostatnie</span><span class="sxs-lookup"><span data-stu-id="7d04b-129">Other Recent Improvements</span></span>

<span data-ttu-id="7d04b-130">Po wydaniu został 2.8 Menedżera pakietów NuGet dla programu Visual Studio również opublikowano Menedżera pakietów NuGet 2.5.0 dla programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7d04b-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="7d04b-131">Gdy zostało to wymienione w [NuGet 2.8 wersji](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), firma Microsoft nie wspomina o konkretnym nowych funkcji tej aktualizacji wprowadzono.</span><span class="sxs-lookup"><span data-stu-id="7d04b-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="7d04b-132">Aktualizuj wszystkie</span><span class="sxs-lookup"><span data-stu-id="7d04b-132">Update All</span></span>

<span data-ttu-id="7d04b-133">Można teraz zaktualizować wszystkich pakietów witryny sieci web w jednym kroku!</span><span class="sxs-lookup"><span data-stu-id="7d04b-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="7d04b-134">Po otwarciu rozszerzenie NuGet w programie WebMatrix zapoznać się z listą wszystkich pakietów w galerii, zainstalowani i sieci z dostępnych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7d04b-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="7d04b-135">Wcześniej każdy pakiet musi zostać zaktualizowany pojedynczo, ale teraz znajduje się przydatne przycisk "Aktualizuj wszystkie", które są wyświetlane na karcie aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="7d04b-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Kliknij przycisk Aktualizuj wszystkie, można zaktualizować wszystkich pakietów o dostępności aktualizacji](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="7d04b-137">Zastąpienie istniejących plików</span><span class="sxs-lookup"><span data-stu-id="7d04b-137">Overwrite Existing Files</span></span>

<span data-ttu-id="7d04b-138">Podczas instalowania pakietów zawierających pliki, które już istnieją w witrynie sieci web, NuGet zawsze w trybie dyskretnym zignorował tych plików (istniejące pliki pozostawiając bez zmian).</span><span class="sxs-lookup"><span data-stu-id="7d04b-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="7d04b-139">Może to prowadzić do wrażenie, że pakiet został zainstalowany ani poprawnie aktualizowany, gdy, w rzeczywistości nie był.</span><span class="sxs-lookup"><span data-stu-id="7d04b-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="7d04b-140">NuGet teraz wyświetli monit o podanie pliki zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="7d04b-140">NuGet will now prompt for files to be overwritten.</span></span>

![Rozwiązywanie konfliktów plików](./media/NuGet-2.8/webmatrix-overwrite-file.png)
