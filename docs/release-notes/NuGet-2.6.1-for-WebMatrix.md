---
title: NuGet 2.6.1 dla programu WebMatrix informacje o wersji
description: Informacje o wersji programu NuGet 2.6.1 dla programu WebMatrix, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550320"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="6fa17-103">NuGet 2.6.1 dla programu WebMatrix informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="6fa17-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="6fa17-104">[Informacje o wersji NuGet 2.6](../release-notes/nuget-2.6.md) | [informacjach o wersji NuGet w wersji 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="6fa17-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="6fa17-105">Zespół NuGet wydany zaktualizowane rozszerzenie Menedżera pakietów NuGet dla programu WebMatrix 26 marca 2014.</span><span class="sxs-lookup"><span data-stu-id="6fa17-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="6fa17-106">Tę aktualizację można zainstalować z [galerii rozszerzeń programu WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6fa17-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="6fa17-107">Otwórz program WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="6fa17-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="6fa17-108">Kliknij ikonę rozszerzenia na karcie wstążki Narzędzia główne</span><span class="sxs-lookup"><span data-stu-id="6fa17-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="6fa17-109">Wybierz kartę Aktualizacje</span><span class="sxs-lookup"><span data-stu-id="6fa17-109">Select the Updates tab</span></span>
1. <span data-ttu-id="6fa17-110">Kliknij, aby zaktualizować Menedżera pakietów NuGet do 2.6.1</span><span class="sxs-lookup"><span data-stu-id="6fa17-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="6fa17-111">Zamknij i ponownie uruchom program WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="6fa17-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="6fa17-112">Znaczące zmiany</span><span class="sxs-lookup"><span data-stu-id="6fa17-112">Notable Changes</span></span>

<span data-ttu-id="6fa17-113">To rozszerzenie aktualizacji adresy dwóch największych problemów użytkowników mają zmierzyła się dużo pakietów NuGet w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="6fa17-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="6fa17-114">Pierwszy wystąpił błąd w wersji schematu NuGet i drugim była usterkę, co prowadzi do dll zero bajtów w `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="6fa17-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="6fa17-115">Błąd wersji schematu NuGet</span><span class="sxs-lookup"><span data-stu-id="6fa17-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="6fa17-116">Ponieważ program WebMatrix 3 został wydany, nowe funkcje zostały wprowadzone do pakietu NuGet, który wymaga nowej wersji schematu dla pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="6fa17-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="6fa17-117">Podczas próby zarządzaniem Twoimi pakietami NuGet w witrynie sieci web, te nowe pakiety może prowadzić do błędów, które są wyświetlane w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="6fa17-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Wystąpił błąd.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="6fa17-121">Najnowsza wersja zapewnia zgodność z najnowszych pakietów NuGet, uniemożliwiając wystąpienia tego błędu.</span><span class="sxs-lookup"><span data-stu-id="6fa17-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="6fa17-122">Teraz można zainstalować nowe wersje pakietów w tym Microsoft.AspNet.WebPages w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="6fa17-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="6fa17-123">Niektóre z tych pakietów zostały przy użyciu funkcji NuGet takich jak [przekształca XDT config](../release-notes/nuget-2.6.md#xdt), który nie był obsługiwany w programie WebMatrix do tej pory.</span><span class="sxs-lookup"><span data-stu-id="6fa17-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="6fa17-124">DLL zero bajtów w pojemniku folderu</span><span class="sxs-lookup"><span data-stu-id="6fa17-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="6fa17-125">Niektórzy użytkownicy wykazały, że po zainstalowaniu NuGet pakietów w programie WebMatrix, który zawiera biblioteki dll, skopiowania do pojemnika, który show biblioteki dll w `bin` folderze co pliki 0 bajtów.</span><span class="sxs-lookup"><span data-stu-id="6fa17-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="6fa17-126">Spowoduje to podzielenie aplikacji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6fa17-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="6fa17-127">[Ten problem](https://nuget.codeplex.com/workitem/4060) teraz został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="6fa17-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="6fa17-128">Inne ulepszenia ostatnie</span><span class="sxs-lookup"><span data-stu-id="6fa17-128">Other Recent Improvements</span></span>

<span data-ttu-id="6fa17-129">Gdy 2.8 Menedżera pakietów NuGet został wydany dla programu Visual Studio, opublikowano także Menedżera pakietów NuGet 2.5.0 dla programu WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="6fa17-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="6fa17-130">Gdy to zostało opisane w [informacjach o wersji programu NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), firma Microsoft nie wspomnieć o konkretnym nowe funkcje tej aktualizacji wprowadzono.</span><span class="sxs-lookup"><span data-stu-id="6fa17-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="6fa17-131">Aktualizuj wszystkie</span><span class="sxs-lookup"><span data-stu-id="6fa17-131">Update All</span></span>

<span data-ttu-id="6fa17-132">Można teraz zaktualizować wszystkich pakietów witryny sieci web w jednym kroku!</span><span class="sxs-lookup"><span data-stu-id="6fa17-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="6fa17-133">Po otwarciu rozszerzenie NuGet w programie WebMatrix, zobaczysz listę wszystkich pakietów w galerii, zainstalowanych i wiedzę dzięki dostępne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="6fa17-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="6fa17-134">Wcześniej każdy pakiet musi być aktualizowane pojedynczo, ale teraz ma przydatne przycisk "Aktualizuj wszystkie", który pojawia się na karcie aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="6fa17-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Kliknij przycisk Aktualizuj wszystkie, aby zaktualizować wszystkich pakietów wraz z dostępnymi aktualizacjami](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="6fa17-136">Nadpisz istniejące pliki</span><span class="sxs-lookup"><span data-stu-id="6fa17-136">Overwrite Existing Files</span></span>

<span data-ttu-id="6fa17-137">Podczas instalowania pakietów, które zawierają pliki, które już istnieją w witrynie sieci web, NuGet ma zawsze dyskretnie ignorowana tych plików (autonomicznie pozostawiając istniejące pliki).</span><span class="sxs-lookup"><span data-stu-id="6fa17-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="6fa17-138">Może to prowadzić do wrażenie, że pakiet został zainstalowany lub poprawnie aktualizowany, gdy w rzeczywistości nie był to.</span><span class="sxs-lookup"><span data-stu-id="6fa17-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="6fa17-139">NuGet teraz wyświetli monit o pliki zostaną zastąpione.</span><span class="sxs-lookup"><span data-stu-id="6fa17-139">NuGet will now prompt for files to be overwritten.</span></span>

![Rozwiązywanie konfliktów plików](./media/NuGet-2.8/webmatrix-overwrite-file.png)
