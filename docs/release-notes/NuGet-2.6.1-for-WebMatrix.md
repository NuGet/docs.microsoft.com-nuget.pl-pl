---
title: Informacje o wersji programu NuGet DataMatrix
description: Informacje o wersji programu NuGetobject dla programu WebMatrix, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780416"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="a6eaf-103">Informacje o wersji programu NuGet DataMatrix</span><span class="sxs-lookup"><span data-stu-id="a6eaf-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="a6eaf-104">Informacje o wersji narzędzia [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Informacje o wersji narzędzia NuGet 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="a6eaf-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="a6eaf-105">Zespół NuGet udostępnił zaktualizowane rozszerzenie Menedżera pakietów NuGet dla programu WebMatrix w dniu 26 marca 2014.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="a6eaf-106">Tę aktualizację można zainstalować z [galerii rozszerzeń WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) , wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a6eaf-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="a6eaf-107">Otwórz WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="a6eaf-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="a6eaf-108">Kliknij ikonę rozszerzenia na Wstążce Narzędzia główne.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="a6eaf-109">Wybierz kartę aktualizacje</span><span class="sxs-lookup"><span data-stu-id="a6eaf-109">Select the Updates tab</span></span>
1. <span data-ttu-id="a6eaf-110">Kliknij, aby zaktualizować Menedżera pakietów NuGet do</span><span class="sxs-lookup"><span data-stu-id="a6eaf-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="a6eaf-111">Zamknij i uruchom ponownie aplikację WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="a6eaf-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="a6eaf-112">Istotne zmiany</span><span class="sxs-lookup"><span data-stu-id="a6eaf-112">Notable Changes</span></span>

<span data-ttu-id="a6eaf-113">Ta aktualizacja rozszerzenia dotyczy dwóch największych problemów, w których użytkownicy mają zużywać pakiety NuGet w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="a6eaf-114">Pierwszy był błędem wersji schematu NuGet, a drugi był usterką wiodącą w przypadku bibliotek DLL o zerowej bajcie w `bin` folderze.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="a6eaf-115">Błąd wersji schematu NuGet</span><span class="sxs-lookup"><span data-stu-id="a6eaf-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="a6eaf-116">Ponieważ program WebMatrix 3 został wystawiony, w pakiecie NuGet wprowadzono nowe funkcje, które wymagają nowej wersji schematu dla pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="a6eaf-117">Podczas próby zarządzania pakietami NuGet w witrynie sieci Web te nowe pakiety mogą prowadzić do błędów, które są widoczne w programie WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Wystąpił błąd.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="a6eaf-121">Ta Najnowsza wersja zapewnia zgodność z najnowszymi pakietami NuGet, zapobiegając wystąpieniu tego błędu.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="a6eaf-122">W programie WebMatrix można teraz zainstalować nowe wersje pakietów, w tym Microsoft. AspNet. Webpages.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="a6eaf-123">Niektóre z tych pakietów korzystają z funkcji NuGet, takich jak [XDT config](../release-notes/nuget-2.6.md#xdt), które nie były obsługiwane w programie WebMatrix do chwili obecnej.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="a6eaf-124">Zero-Byte bibliotek DLL w folderze bin</span><span class="sxs-lookup"><span data-stu-id="a6eaf-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="a6eaf-125">Niektórzy użytkownicy zgłosili, że po zainstalowaniu pakietów NuGet w programie WebMatrix, które zawierają biblioteki DLL, które są kopiowane do pliku bin, są wyświetlane w `bin` folderze jako pliki 0-bajtowe.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="a6eaf-126">Spowoduje to przerwanie działania aplikacji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="a6eaf-127">[Ten problem](https://nuget.codeplex.com/workitem/4060) został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="a6eaf-128">Inne Ostatnie ulepszenia</span><span class="sxs-lookup"><span data-stu-id="a6eaf-128">Other Recent Improvements</span></span>

<span data-ttu-id="a6eaf-129">Gdy Menedżer pakietów NuGet 2,8 został opublikowany dla programu Visual Studio, wydano również 2.5.0 Menedżera pakietów NuGet dla WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="a6eaf-130">Chociaż został on wymieniony w [informacjach o wersji NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), nie wspominamy o określonych nowych funkcjach wprowadzonych przez aktualizację.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="a6eaf-131">Aktualizuj wszystkie</span><span class="sxs-lookup"><span data-stu-id="a6eaf-131">Update All</span></span>

<span data-ttu-id="a6eaf-132">Teraz możesz zaktualizować wszystkie pakiety witryny sieci Web w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="a6eaf-133">Po otwarciu rozszerzenia NuGet w programie WebMatrix zostanie wyświetlona lista wszystkich pakietów z galerii, zainstalowanych i dostępnych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="a6eaf-134">Wcześniej każdy pakiet musiał zostać zaktualizowany pojedynczo, ale teraz istnieje przydatny przycisk "Aktualizuj wszystko", który jest wyświetlany na karcie Aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Kliknij przycisk Aktualizuj wszystko, aby zaktualizować wszystkie pakiety z dostępnymi aktualizacjami](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="a6eaf-136">Zastąp istniejące pliki</span><span class="sxs-lookup"><span data-stu-id="a6eaf-136">Overwrite Existing Files</span></span>

<span data-ttu-id="a6eaf-137">W przypadku instalowania pakietów zawierających pliki, które już istnieją w witrynie sieci Web, pakiet NuGet zawsze po prostu zignorował te pliki (pozostawiając istniejące pliki).</span><span class="sxs-lookup"><span data-stu-id="a6eaf-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="a6eaf-138">Może to prowadzić do tego, że pakiet został zainstalowany lub zaktualizowany prawidłowo, gdy w rzeczywistości nie był.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="a6eaf-139">Pakiet NuGet będzie teraz monitował o pliki do zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="a6eaf-139">NuGet will now prompt for files to be overwritten.</span></span>

![Rozwiązywanie konfliktów plików](./media/NuGet-2.8/webmatrix-overwrite-file.png)
