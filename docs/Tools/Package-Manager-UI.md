---
title: "Informacje o interfejsie użytkownika Menedżera pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 62f6962b-7b84-4452-ae0d-a9e1ef1fc6f0
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: "Instrukcje dotyczące używania interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet."
keywords: "Interfejs użytkownika NuGet, Menedżer pakietów NuGet interfejsu użytkownika, NuGet w programie Visual Studio, Zarządzanie pakietami NuGet, NuGet interfejsu użytkownika Menedżera pakietów w programie Visual Studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39ce53184755887c419c8872148a6c13dc2c65ec
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="30def-104">Interfejs użytkownika Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="30def-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="30def-105">Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio w systemie Windows umożliwia łatwe instalowanie, odinstalowywanie oraz aktualizację pakietów NuGet w projekty i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="30def-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="30def-106">Środowisko w programie Visual Studio dla komputerów Mac, zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="30def-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="30def-107">Interfejs użytkownika Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="30def-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="30def-108">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="30def-108">In this topic:</span></span>

- [<span data-ttu-id="30def-109">Znajdowanie i instalowanie pakietu (Przeglądaj karta)</span><span class="sxs-lookup"><span data-stu-id="30def-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="30def-110">Odinstalowywanie pakietu (karta zainstalowana)</span><span class="sxs-lookup"><span data-stu-id="30def-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="30def-111">[Aktualizowanie pakietu (instalacji i aktualizacji karty)](#updating-a-package) (obejmuje ["Niejawnie odwołuje się zestaw SDK" lub "AutoReferenced" wiadomości](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="30def-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="30def-112">[Zarządzanie pakietami dla rozwiązania](#managing-packages-for-the-solution) (Praca z wieloma projektami w tym samym czasie).</span><span class="sxs-lookup"><span data-stu-id="30def-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="30def-113">Źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="30def-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="30def-114">Kontrolki opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="30def-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="30def-115">Sprawdź, czy jest Brak Menedżera pakietów NuGet w programie Visual Studio 2015, **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj *Menedżera pakietów NuGet* rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="30def-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="30def-116">Jeśli nie można użyć Instalatora rozszerzeń programu Visual Studio, pobierz rozszerzenie bezpośrednio z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="30def-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="30def-117">W programie Visual Studio 2017 r. NuGet i Menedżer pakietów NuGet są automatycznie instalowane ze wszystkimi. Obciążenia związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="30def-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="30def-118">Zainstalować oddzielnie, wybierając **pojedynczych składników > narzędzia Code > Menedżera pakietów NuGet** opcji w Instalatorze programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="30def-118">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="30def-119">Znajdowanie i instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="30def-119">Finding and installing a package</span></span>

1. <span data-ttu-id="30def-120">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy albo **odwołania** lub projektu i wybierz **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="30def-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Zarządzanie pakietami NuGet opcji menu](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="30def-122">**Przeglądaj** karcie są wyświetlane pakiety przez popularne z aktualnie wybranego źródła (zobacz [pakietu źródeł](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="30def-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="30def-123">Wyszukiwanie określonego pakietu przy użyciu pola wyszukiwania w lewym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="30def-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="30def-124">Wybierz pakiet z listy, aby wyświetlić jego informacje, które umożliwia również **zainstalować** przycisk wraz z menu rozwijane wyboru wersji.</span><span class="sxs-lookup"><span data-stu-id="30def-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Zarządzaj kartą Przeglądaj okna dialogowego pakietów NuGet](media/Search.png)

1. <span data-ttu-id="30def-126">Wybierz żądaną wersję z listy rozwijanej i wybierz **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="30def-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="30def-127">Visual Studio instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="30def-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="30def-128">Może być monit zaakceptować warunki umowy licencyjnej.</span><span class="sxs-lookup"><span data-stu-id="30def-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="30def-129">Po zakończeniu instalacji dodano pakiety są wyświetlane na **zainstalowana** kartę. Pakiety są również wyświetlane w **odwołania** węzła Eksploratorze rozwiązań i wskazujący, że można odwołać się do nich w projekcie z `using` instrukcje.</span><span class="sxs-lookup"><span data-stu-id="30def-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Odwołania w Eksploratorze rozwiązań](media/References.png)

> [!Tip]
    > <span data-ttu-id="30def-131">Aby w wyszukiwaniu uwzględnić wersje wstępne i udostępnić wersje wstępne w wersji listy rozwijanej, wybierz **Uwzględnij wersję wstępną** opcji.</span><span class="sxs-lookup"><span data-stu-id="30def-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="30def-132">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="30def-132">Uninstalling a package</span></span>

1. <span data-ttu-id="30def-133">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy albo **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="30def-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="30def-134">Wybierz **zainstalowana** kartę.</span><span class="sxs-lookup"><span data-stu-id="30def-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="30def-135">Wybierz pakietu do odinstalowania (za pomocą wyszukiwania, aby filtrować listę, jeśli to konieczne), a następnie wybierz **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="30def-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. <span data-ttu-id="30def-137">Należy pamiętać, że **obejmują preprelease** i **źródła pakietu** formanty nie mają żadnego skutku odinstalowanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="30def-137">Note that the **Include preprelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="30def-138">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="30def-138">Updating a package</span></span>

1. <span data-ttu-id="30def-139">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy albo **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** . (W projektach witryny sieci web, kliknij prawym przyciskiem myszy **Bin** folderu.)</span><span class="sxs-lookup"><span data-stu-id="30def-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="30def-140">Wybierz **aktualizacje** kartę, aby wyświetlić pakiety, które są dostępne aktualizacje ze źródeł wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="30def-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="30def-141">Wybierz **Uwzględnij wersję wstępną** do dołączenia do listy aktualizacji pakiety wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="30def-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="30def-142">Wybierz pakiet aktualizacji, wybierz odpowiednią wersję z listy rozwijanej po prawej stronie, a następnie wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="30def-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="30def-144">W przypadku niektórych pakietów **aktualizacji** przycisku jest wyłączona i zostanie wyświetlony komunikat informujący o tym, że "niejawnie odwołuje się zestaw SDK" (lub "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="30def-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="30def-145">Komunikat wskazuje, że pakiet, takie jak Microsoft.NETCore.App lub Microsoft.NETStandard.Library, jest częścią większej struktury lub zestawu SDK i nie powinny być aktualizowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="30def-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="30def-146">(Takie packagee wewnętrznie są oznaczone ikoną z `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Do zaktualizowania pakietu, należy zaktualizować zestawu SDK, do którego on należy.</span><span class="sxs-lookup"><span data-stu-id="30def-146">(Such packagee are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![Przykład pakietu oznaczenie niejawnie odwołania lub AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="30def-148">Aby zaktualizować wielu pakietów do swoich najnowszej wersji, wybierz je na liście i wybierz **aktualizacji** przycisk powyżej listy.</span><span class="sxs-lookup"><span data-stu-id="30def-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="30def-149">Można także zaktualizować poszczególnych pakietu z **zainstalowana** kartę. W takim przypadku informacje dla pakietu zawierają selektora wersji (podlega **Uwzględnij wersję wstępną** opcji) i **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="30def-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="30def-150">Zarządzanie pakietami dla rozwiązania</span><span class="sxs-lookup"><span data-stu-id="30def-150">Managing packages for the solution</span></span>

<span data-ttu-id="30def-151">Zarządzanie pakietami dla rozwiązania to wygodny sposób pracować z wieloma projektami równocześnie.</span><span class="sxs-lookup"><span data-stu-id="30def-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="30def-152">Wybierz **Narzędzia > Menedżera pakietów NuGet > Zarządzaj pakietami NuGet dla rozwiązania...**  menu poleceń, lub kliknij rozwiązanie prawym przyciskiem myszy i wybierz polecenie **Zarządzaj pakietami NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="30def-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Zarządzaj pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="30def-154">Podczas zarządzania pakietami dla rozwiązania, interfejs użytkownika umożliwia Wybierz projekty, do których zastosowano operacje:</span><span class="sxs-lookup"><span data-stu-id="30def-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="30def-156">Konsolidacja kartę</span><span class="sxs-lookup"><span data-stu-id="30def-156">Consolidate tab</span></span>

<span data-ttu-id="30def-157">Deweloperzy zazwyczaj uważają, że zły praktyką jest używanie różnych wersji tego samego pakietu NuGet wielu różnych projektów, w tym samym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="30def-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="30def-158">W przypadku zarządzania pakietami dla rozwiązania interfejsu użytkownika Menedżera pakietów zawiera **Konsoliduj** kartę, na którym można łatwo widzisz gdzie pakiety z różnych wersji numery są używane przez różne projekty w rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="30def-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Karta skonsolidować interfejsu użytkownika Menedżera pakietów](media/ConsolidateTab.png)

<span data-ttu-id="30def-160">W tym przykładzie projektu ClassLibrary1 jest za pomocą platformy EntityFramework 6.2.0, podczas gdy ConsoleApp1 jest za pomocą platformy EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="30def-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.2.0.</span></span> <span data-ttu-id="30def-161">Aby skonsolidować wersji pakietu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="30def-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="30def-162">Wybierz projekty, aby zaktualizować w liście projektu.</span><span class="sxs-lookup"><span data-stu-id="30def-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="30def-163">Wybierz wersję do użycia w tych projektach w **wersji** kontroli, takich jak EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="30def-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="30def-164">Wybierz **zainstalować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="30def-164">Select the **Install** button.</span></span>

<span data-ttu-id="30def-165">Menedżer pakietów instaluje wersję wybranego pakietu do wszystkich wybranych projektów, po których pakiet nie jest już widoczna na **Konsoliduj** kartę.</span><span class="sxs-lookup"><span data-stu-id="30def-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="30def-166">Źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="30def-166">Package sources</span></span>

<span data-ttu-id="30def-167">Aby zmienić źródło, z którego program Visual Studio pobiera pakiety, wybierz jedną z selektora źródła:</span><span class="sxs-lookup"><span data-stu-id="30def-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selektor źródła pakietu w interfejs użytkownika Menedżera pakietów](media/PackageSourceDropDown.png)

<span data-ttu-id="30def-169">Aby zarządzać źródła pakietów:</span><span class="sxs-lookup"><span data-stu-id="30def-169">To manage package sources:</span></span>

1. <span data-ttu-id="30def-170">Wybierz **ustawienia** ikonę w Interfejsie użytkownika Menedżera pakietów przedstawione poniżej lub użyj **Narzędzia > Opcje** polecenia, a następnie przewiń do **Menedżera pakietów NuGet**:</span><span class="sxs-lookup"><span data-stu-id="30def-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ikona ustawienia interfejsu użytkownika Menedżera pakietów](media/PackageSourceSettings.png)

1. <span data-ttu-id="30def-172">Wybierz **źródła pakietów** węzła:</span><span class="sxs-lookup"><span data-stu-id="30def-172">Select the **Package Sources** node:</span></span>

    ![Opcje źródła pakietów](media/options.png)

1. <span data-ttu-id="30def-174">Aby dodać źródła, wybierz  **+** , umożliwia edytowanie nazwy, wprowadź adres URL lub ścieżkę w **źródła** kontroli i wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="30def-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="30def-175">Źródło jest teraz wyświetlany w selektorze listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="30def-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="30def-176">Aby zmienić źródło pakietu, wybierz ją, wprowadź zmiany w **nazwa** i **źródła** pola, a następnie wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="30def-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="30def-177">Aby wyłączyć źródła pakietu, usuń zaznaczenie pola nazwy na liście z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="30def-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="30def-178">Aby usunąć źródło pakietu, wybierz go, a następnie wybierz **X** przycisku.</span><span class="sxs-lookup"><span data-stu-id="30def-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="30def-179">W górę i w dół przycisków strzałek, aby zmienić kolejność priorytetów źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="30def-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="30def-180">Visual Studio wyszukuje tych źródeł w kolejności priorytetu, gdy trwa przywracanie pakietów dla projektu.</span><span class="sxs-lookup"><span data-stu-id="30def-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="30def-181">Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu](../Consume-Packages/Package-Restore.md).</span><span class="sxs-lookup"><span data-stu-id="30def-181">For more information, see [Package restore](../Consume-Packages/Package-Restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="30def-182">Jeśli źródła pakietu zostanie wyświetlony ponownie po jej usunięciu, mogą być wymienione w poziomie komputera lub użytkownika na poziomie `NuGet.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="30def-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="30def-183">Zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md) na lokalizację tych plików, następnie usunąć źródło przez edycję plików ręcznie lub za pomocą [nuget źródeł polecenia](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="30def-183">See [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="30def-184">Kontrolki opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="30def-184">Package manager Options control</span></span>

<span data-ttu-id="30def-185">Po wybraniu pakietu interfejsu użytkownika Menedżera pakietów wyświetla mały rozwijania **opcje** kontroli poniżej selektora wersji (przedstawione zarówno zwinięte i rozwinięte).</span><span class="sxs-lookup"><span data-stu-id="30def-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="30def-186">Należy pamiętać, że dla niektórych typów, takich jak oprogramowanie .NET Core i korzystających z projektu `project.json` format odwołania tylko **Pokaż okno podglądu** podano opcję.</span><span class="sxs-lookup"><span data-stu-id="30def-186">Note that for some project types, such as .NET Core and those using the `project.json` reference format, only the **Show preview window** option is provided.</span></span>

![Opcje Menedżera pakietów](media/PackageManagerUIOptions.png)

<span data-ttu-id="30def-188">W poniższych sekcjach opisano te opcje.</span><span class="sxs-lookup"><span data-stu-id="30def-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="30def-189">Pokaż okno podglądu</span><span class="sxs-lookup"><span data-stu-id="30def-189">Show preview window</span></span>

<span data-ttu-id="30def-190">Po wybraniu modalny Wyświetla którego zależności wybranego pakietu przed zainstalowaniem pakietu:</span><span class="sxs-lookup"><span data-stu-id="30def-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Przykład okna dialogowego podglądu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="30def-192">Opcje instalacji i aktualizacji</span><span class="sxs-lookup"><span data-stu-id="30def-192">Install and Update Options</span></span>

<span data-ttu-id="30def-193">(Niedostępne dla wszystkie typy projektów).</span><span class="sxs-lookup"><span data-stu-id="30def-193">(Not available for all project types.)</span></span>

<span data-ttu-id="30def-194">**Zachowanie zależności** konfiguruje sposób NuGet decyduje o tym, które wersje pakietów zależnych, aby zainstalować:</span><span class="sxs-lookup"><span data-stu-id="30def-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="30def-195">*Ignoruj zależności* pomija instalowanie zależności, co zwykle przerwie instalowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="30def-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="30def-196">*Najniższa* [domyślnie] instaluje zależności z numerem wersji minimalnego, który spełnia wymagania wybranego pakietu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="30def-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="30def-197">*Poprawka najwyższy* powoduje zainstalowanie wersji o tej samej liczby wersji głównej i pomocniczej, ale najwyższy numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="30def-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="30def-198">Na przykład jeśli określono wersję 1.2.2 następnie najwyższej wersji, która rozpoczyna się od 1.2 zostanie zainstalowana</span><span class="sxs-lookup"><span data-stu-id="30def-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="30def-199">*Pomocnicze najwyższy* powoduje zainstalowanie wersji tego samego numeru wersji głównej, ale najwyższym numerem i numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="30def-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="30def-200">Jeśli określono wersję 1.2.2, następnie najwyższej wersji, która rozpoczyna się od 1 zostanie zainstalowana</span><span class="sxs-lookup"><span data-stu-id="30def-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="30def-201">*Najwyższy* instaluje najwyższy dostępna wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="30def-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="30def-202">**Plik akcję konfliktów** określa sposób obsługi NuGet pakiety, które już istnieją w projekcie lub komputer lokalny:</span><span class="sxs-lookup"><span data-stu-id="30def-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="30def-203">*Monituj* nakazuje NuGet zapytać, czy zachować, czy zastąpić istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="30def-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="30def-204">*Ignoruj wszystkie* program NuGet, aby pominąć zastępowanie wszelkie istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="30def-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="30def-205">*Zastąpienie wszystkich* program NuGet, aby zastąpić wszystkie istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="30def-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="30def-206">Opcji odinstalowywania</span><span class="sxs-lookup"><span data-stu-id="30def-206">Uninstall Options</span></span>

<span data-ttu-id="30def-207">(Niedostępne dla wszystkie typy projektów).</span><span class="sxs-lookup"><span data-stu-id="30def-207">(Not available for all project types.)</span></span>

<span data-ttu-id="30def-208">**Usuwanie zależności**: po wybraniu usuwa wszystkie zależne pakiety, jeśli ich nie jest wywoływany w innym miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="30def-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="30def-209">**Życie odinstalować, nawet jeśli istnieją zależności na nim**: po wybraniu odinstalowuje pakiet nawet wtedy, gdy nadal jest ono przywoływane w projekcie.</span><span class="sxs-lookup"><span data-stu-id="30def-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="30def-210">To jest zwykle używana w połączeniu z **usuwanie zależności** do usunięcia pakietu i niezależnie od zależności ona zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="30def-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="30def-211">Przy użyciu tej opcji, może prowadzić do uszkodzenie odwołań w projekcie.</span><span class="sxs-lookup"><span data-stu-id="30def-211">Using this option may, however, lead to a broken references in the project.</span></span> <span data-ttu-id="30def-212">W takich przypadkach może być konieczne [ponownie zainstalować inne pakiety](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="30def-212">In such cases you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
