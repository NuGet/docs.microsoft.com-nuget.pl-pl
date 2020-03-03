---
title: Instalowanie pakietów NuGet i zarządzanie nimi w programie Visual Studio
description: Instrukcje dotyczące używania interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231010"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="ad314-103">Instalowanie pakietów i zarządzanie nimi w programie Visual Studio przy użyciu Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="ad314-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="ad314-104">Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio w systemie Windows umożliwia łatwe instalowanie, Odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="ad314-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="ad314-105">Aby zapoznać się z doświadczeniem w Visual Studio dla komputerów Mac, zobacz [dołączanie pakietu NuGet do projektu](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span><span class="sxs-lookup"><span data-stu-id="ad314-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="ad314-106">Interfejs użytkownika Menedżera pakietów nie jest dołączony do Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ad314-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="ad314-107">Jeśli brakuje Menedżera pakietów NuGet w programie Visual Studio 2015, sprawdź **narzędzia > rozszerzenia i aktualizacje...** , a następnie wyszukaj rozszerzenie *Menedżera pakietów NuGet* .</span><span class="sxs-lookup"><span data-stu-id="ad314-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="ad314-108">Jeśli nie możesz użyć Instalatora rozszerzeń w programie Visual Studio, Pobierz rozszerzenie bezpośrednio z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ad314-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="ad314-109">Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są automatycznie instalowane z dowolnymi. Obciążenia związane z usługą SIECIową.</span><span class="sxs-lookup"><span data-stu-id="ad314-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="ad314-110">Zainstaluj ją oddzielnie, wybierając opcję **> narzędzia kodu > opcji Menedżera pakietów NuGet** w Instalatorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad314-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="ad314-111">Znajdowanie i instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ad314-111">Find and install a package</span></span>

1. <span data-ttu-id="ad314-112">W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy opcję **odwołania** lub projekt i wybierz polecenie **Zarządzaj pakietami NuGet.**...</span><span class="sxs-lookup"><span data-stu-id="ad314-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Opcja menu Zarządzaj pakietami NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="ad314-114">Na karcie **przeglądanie** są wyświetlane pakiety według popularności z aktualnie wybranego źródła (zobacz [źródła pakietu](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="ad314-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="ad314-115">Wyszukaj konkretny pakiet przy użyciu pola wyszukiwania w lewym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="ad314-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="ad314-116">Wybierz pakiet z listy, aby wyświetlić jego informacje, które również włącza przycisk **Instaluj** wraz z listą rozwijaną wyboru wersji.</span><span class="sxs-lookup"><span data-stu-id="ad314-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Karta przeglądania okna dialogowego Zarządzanie pakietami NuGet](media/Search.png)

1. <span data-ttu-id="ad314-118">Wybierz żądaną wersję z listy rozwijanej i wybierz pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="ad314-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="ad314-119">Program Visual Studio instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad314-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="ad314-120">Może zostać wyświetlony monit o zaakceptowanie postanowień licencyjnych.</span><span class="sxs-lookup"><span data-stu-id="ad314-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="ad314-121">Po zakończeniu instalacji dodane pakiety pojawiają się na **zainstalowanej** karcie. pakiety są również wymienione w węźle **odwołania** Eksplorator rozwiązań, co oznacza, że można odwołać się do nich w projekcie za pomocą instrukcji `using`.</span><span class="sxs-lookup"><span data-stu-id="ad314-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Odwołania w Eksplorator rozwiązań](media/References.png)

> [!Tip]
> <span data-ttu-id="ad314-123">Aby uwzględnić wersje wstępne w wyszukiwaniu i udostępnić wersje wstępne dostępne na liście rozwijanej wersja, wybierz opcję **Uwzględnij wersję wstępną** .</span><span class="sxs-lookup"><span data-stu-id="ad314-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="ad314-124">Pakiet NuGet ma dwa formaty, w których projekt może używać pakietów: [`PackageReference`](package-references-in-project-files.md) i [`packages.config`](../reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="ad314-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="ad314-125">Wartość [domyślną można ustawić w oknie Opcje programu Visual Studio](Package-Restore.md#choose-default-package-management-format).</span><span class="sxs-lookup"><span data-stu-id="ad314-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="ad314-126">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ad314-126">Uninstall a package</span></span>

1. <span data-ttu-id="ad314-127">W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **odwołania** lub żądany projekt, a następnie wybierz polecenie **Zarządzaj pakietami NuGet.**...</span><span class="sxs-lookup"><span data-stu-id="ad314-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="ad314-128">Wybierz kartę **Zainstalowano**.</span><span class="sxs-lookup"><span data-stu-id="ad314-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="ad314-129">Wybierz pakiet, który ma zostać odinstalowany (za pomocą wyszukiwania, w razie potrzeby odfiltruj listę), a następnie wybierz pozycję **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="ad314-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. <span data-ttu-id="ad314-131">Należy zauważyć, że kontrolki **Uwzględnij wersję wstępną** i **Źródło pakietu** nie mają wpływu na Odinstalowywanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad314-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="ad314-132">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ad314-132">Update a package</span></span>

1. <span data-ttu-id="ad314-133">W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy pozycję **odwołania** lub żądany projekt, a następnie wybierz polecenie **Zarządzaj pakietami NuGet.**... (W obszarze projekty witryny sieci Web kliknij prawym przyciskiem myszy folder **bin** ).</span><span class="sxs-lookup"><span data-stu-id="ad314-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="ad314-134">Wybierz kartę **aktualizacje** , aby zobaczyć pakiety z dostępnymi aktualizacjami z wybranych źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad314-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="ad314-135">Wybierz pozycję **Uwzględnij wersję wstępną** , aby uwzględnić pakiety wersji wstępnej na liście aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ad314-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="ad314-136">Wybierz pakiet do zaktualizowania, wybierz żądaną wersję z listy rozwijanej po prawej stronie, a następnie wybierz pozycję **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="ad314-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="ad314-138">W przypadku niektórych pakietów przycisk **Aktualizuj** jest wyłączony i pojawia się komunikat informujący o tym, że jest to "niejawnie przywoływane przez zestaw SDK" (lub "autoreferencja").</span><span class="sxs-lookup"><span data-stu-id="ad314-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="ad314-139">Ten komunikat oznacza, że pakiet jest częścią większej struktury lub zestawu SDK i nie należy go aktualizować niezależnie.</span><span class="sxs-lookup"><span data-stu-id="ad314-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="ad314-140">(Takie pakiety są wewnętrznie oznaczone `<IsImplicitlyDefined>True</IsImplicitlyDefined>`m). Na przykład `Microsoft.NETCore.App` jest częścią zestaw .NET Core SDK, a wersja pakietu nie jest taka sama jak wersja środowiska uruchomieniowego używanego przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="ad314-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="ad314-141">Musisz [zaktualizować instalację programu .NET Core](https://aka.ms/dotnet-download) , aby uzyskać nowe wersje ASP.NET Core i środowiska uruchomieniowego platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ad314-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="ad314-142">[Zapoznaj się z tym dokumentem, aby uzyskać szczegółowe informacje o pakietach i wersjach platformy .NET Core](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="ad314-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="ad314-143">Dotyczy to następujących najczęściej używanych pakietów:</span><span class="sxs-lookup"><span data-stu-id="ad314-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="ad314-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="ad314-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="ad314-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="ad314-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="ad314-146">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="ad314-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="ad314-147">Biblioteka standardowa. Library</span><span class="sxs-lookup"><span data-stu-id="ad314-147">NETStandard.Library</span></span>

    ![Przykładowy pakiet oznaczony jako niejawnie przywoływany lub autoreferencja](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="ad314-149">Aby zaktualizować wiele pakietów do ich najnowszych wersji, zaznacz je na liście i wybierz przycisk **Aktualizuj** nad listą.</span><span class="sxs-lookup"><span data-stu-id="ad314-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="ad314-150">Możesz również zaktualizować pojedynczy pakiet z karty **zainstalowane** . W takim przypadku szczegóły pakietu obejmują selektor wersji (z opcją **Uwzględnij wersję wstępną** ) i przycisk **Aktualizuj** .</span><span class="sxs-lookup"><span data-stu-id="ad314-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="ad314-151">Zarządzaj pakietami dla rozwiązania</span><span class="sxs-lookup"><span data-stu-id="ad314-151">Manage packages for the solution</span></span>

<span data-ttu-id="ad314-152">Zarządzanie pakietami dla rozwiązania jest wygodnym sposobem pracy z wieloma projektami jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="ad314-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="ad314-153">Wybierz **narzędzia > Menedżer pakietów nuget > zarządzanie pakietami NuGet dla rozwiązania...** menu, lub kliknij rozwiązanie prawym przyciskiem myszy i wybierz pozycję **Zarządzaj pakietami NuGet...**:</span><span class="sxs-lookup"><span data-stu-id="ad314-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Zarządzaj pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="ad314-155">Podczas zarządzania pakietami dla rozwiązania interfejs użytkownika umożliwia wybranie projektów, na które mają wpływ operacje:</span><span class="sxs-lookup"><span data-stu-id="ad314-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="ad314-157">Karta konsolidowanie</span><span class="sxs-lookup"><span data-stu-id="ad314-157">Consolidate tab</span></span>

<span data-ttu-id="ad314-158">Deweloperzy zazwyczaj uważają, że niewłaściwe rozwiązanie do korzystania z różnych wersji tego samego pakietu NuGet w różnych projektach w tym samym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ad314-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="ad314-159">W przypadku wybrania opcji zarządzania pakietami dla rozwiązania interfejs użytkownika Menedżera pakietów zawiera kartę **Konsolidacja** , w której można łatwo zobaczyć, gdzie pakiety o różnych numerach wersji są używane przez różne projekty w rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="ad314-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Karta konsolidacja interfejsu użytkownika Menedżera pakietów](media/ConsolidateTab.png)

<span data-ttu-id="ad314-161">W tym przykładzie projekt ClassLibrary1 korzysta z EntityFramework 6.2.0, a ConsoleApp1 używa EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="ad314-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="ad314-162">Aby skonsolidować wersje pakietów, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ad314-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="ad314-163">Wybierz projekty do zaktualizowania na liście projektów.</span><span class="sxs-lookup"><span data-stu-id="ad314-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="ad314-164">Wybierz wersję, która ma być używana we wszystkich projektach w kontroli **wersji** , np. EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="ad314-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="ad314-165">Wybierz przycisk **Instaluj** .</span><span class="sxs-lookup"><span data-stu-id="ad314-165">Select the **Install** button.</span></span>

<span data-ttu-id="ad314-166">Menedżer pakietów instaluje wybraną wersję pakietu we wszystkich wybranych projektach, po upływie których pakiet nie jest już wyświetlany na karcie **konsolidowanie** .</span><span class="sxs-lookup"><span data-stu-id="ad314-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="ad314-167">Źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="ad314-167">Package sources</span></span>

<span data-ttu-id="ad314-168">Aby zmienić źródło, z którego program Visual Studio uzyskuje pakiety, wybierz jeden z selektora źródła:</span><span class="sxs-lookup"><span data-stu-id="ad314-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selektor źródła pakietu w interfejsie użytkownika Menedżera pakietów](media/PackageSourceDropDown.png)

<span data-ttu-id="ad314-170">Aby zarządzać źródłami pakietów:</span><span class="sxs-lookup"><span data-stu-id="ad314-170">To manage package sources:</span></span>

1. <span data-ttu-id="ad314-171">Wybierz ikonę **ustawień** w interfejsie użytkownika Menedżera pakietów przedstawionym poniżej lub użyj **narzędzi > Opcje** i przewiń do **Menedżera pakietów NuGet**:</span><span class="sxs-lookup"><span data-stu-id="ad314-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ikona ustawień interfejsu użytkownika Menedżera pakietów](media/PackageSourceSettings.png)

1. <span data-ttu-id="ad314-173">Wybierz węzeł **źródła pakietów** :</span><span class="sxs-lookup"><span data-stu-id="ad314-173">Select the **Package Sources** node:</span></span>

    ![Opcje źródeł pakietów](media/options.png)

1. <span data-ttu-id="ad314-175">Aby dodać źródło, wybierz **+**, Edytuj nazwę, wprowadź adres URL lub ścieżkę w kontroli **źródła** , a następnie wybierz pozycję **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="ad314-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="ad314-176">Źródło zostanie wyświetlone na liście rozwijanej selektora.</span><span class="sxs-lookup"><span data-stu-id="ad314-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="ad314-177">Aby zmienić źródło pakietu, zaznacz je, wprowadź zmiany w polach **Nazwa** i **Źródło** , a następnie wybierz pozycję **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="ad314-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="ad314-178">Aby wyłączyć źródło pakietu, wyczyść pole z lewej strony nazwy na liście.</span><span class="sxs-lookup"><span data-stu-id="ad314-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="ad314-179">Aby usunąć źródło pakietu, zaznacz je, a następnie wybierz przycisk **X** .</span><span class="sxs-lookup"><span data-stu-id="ad314-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="ad314-180">Używanie przycisków strzałek w górę i w dół nie zmienia kolejności priorytetów źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad314-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="ad314-181">Program Visual Studio ignoruje kolejność źródeł pakietów przy użyciu pakietu z dowolnego źródła jest najpierw odpowiedzi na żądania.</span><span class="sxs-lookup"><span data-stu-id="ad314-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="ad314-182">Aby uzyskać więcej informacji, zobacz [przywracanie pakietu](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ad314-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="ad314-183">Jeśli źródło pakietu zostanie ponownie wyświetlone po jego usunięciu, może ono znajdować się na liście plików `NuGet.Config` na poziomie komputera lub użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad314-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="ad314-184">Zapoznaj się z [typowymi konfiguracjami NuGet](../consume-packages/configuring-nuget-behavior.md) dla lokalizacji tych plików, a następnie Usuń źródło, edytując pliki ręcznie lub używając [polecenia źródła NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ad314-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="ad314-185">Kontrola opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="ad314-185">Package manager Options control</span></span>

<span data-ttu-id="ad314-186">Po wybraniu pakietu interfejs użytkownika Menedżera pakietów wyświetla małą, rozwijalną kontrolkę **opcji** poniżej selektora wersji (pokazanej w tym miejscu: zwinięte i rozwinięte).</span><span class="sxs-lookup"><span data-stu-id="ad314-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="ad314-187">Należy pamiętać, że w przypadku niektórych typów projektów dostępna jest tylko opcja **Pokaż podgląd okna** .</span><span class="sxs-lookup"><span data-stu-id="ad314-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opcje Menedżera pakietów](media/PackageManagerUIOptions.png)

<span data-ttu-id="ad314-189">W poniższych sekcjach opisano te opcje.</span><span class="sxs-lookup"><span data-stu-id="ad314-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="ad314-190">Pokaż okno podglądu</span><span class="sxs-lookup"><span data-stu-id="ad314-190">Show preview window</span></span>

<span data-ttu-id="ad314-191">Po wybraniu okno modalne wyświetla zależności wybranego pakietu przed zainstalowaniem pakietu:</span><span class="sxs-lookup"><span data-stu-id="ad314-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Przykładowe okno dialogowe podglądu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="ad314-193">Opcje instalacji i aktualizacji</span><span class="sxs-lookup"><span data-stu-id="ad314-193">Install and Update Options</span></span>

<span data-ttu-id="ad314-194">(Niedostępne dla wszystkich typów projektów).</span><span class="sxs-lookup"><span data-stu-id="ad314-194">(Not available for all project types.)</span></span>

<span data-ttu-id="ad314-195">**Zachowanie zależności** konfiguruje sposób, w jaki pakiet NuGet decyduje, które wersje pakietów zależnych zainstalować:</span><span class="sxs-lookup"><span data-stu-id="ad314-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="ad314-196">*Ignorowanie zależności* powoduje pominięcie instalacji wszelkich zależności, które zwykle przerywa instalację pakietu.</span><span class="sxs-lookup"><span data-stu-id="ad314-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="ad314-197">*Najniższy* [domyślnie] instaluje zależność z minimalnym numerem wersji, który spełnia wymagania głównego wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ad314-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="ad314-198">*Najwyższa poprawka* instaluje wersję z tymi samymi głównymi i pomocniczymi numerami wersji, ale najwyższa numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="ad314-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="ad314-199">Na przykład jeśli zostanie określona wersja 1.2.2, zostanie zainstalowana najwyższa wersja, która rozpoczyna się od 1,2</span><span class="sxs-lookup"><span data-stu-id="ad314-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="ad314-200">*Największa drobna* instaluje wersję z tym samym głównym numerem wersji, ale z najwyższym numerem i numerem poprawki.</span><span class="sxs-lookup"><span data-stu-id="ad314-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="ad314-201">Jeśli zostanie określona wersja 1.2.2, zostanie zainstalowana najwyższa wersja, która rozpoczyna się od 1</span><span class="sxs-lookup"><span data-stu-id="ad314-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="ad314-202">*Najwyższa* instalacja jest najwyższa dostępna wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="ad314-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="ad314-203">**Akcja konfliktu plików** określa, jak NuGet powinien obsługiwać pakiety, które już istnieją w projekcie lub na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="ad314-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="ad314-204">*Monit* instruuje pakiet NuGet, aby poprosił o zachowanie lub zastąpienie istniejących pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad314-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="ad314-205">*Zignoruj wszystkie* instruuje pakiet NuGet, aby pominąć zastępowanie wszystkich istniejących pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad314-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="ad314-206">Polecenie *overwrite All* instruuje pakiet NuGet, aby zastąpić wszystkie istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="ad314-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="ad314-207">Opcje dezinstalacji</span><span class="sxs-lookup"><span data-stu-id="ad314-207">Uninstall Options</span></span>

<span data-ttu-id="ad314-208">(Niedostępne dla wszystkich typów projektów).</span><span class="sxs-lookup"><span data-stu-id="ad314-208">(Not available for all project types.)</span></span>

<span data-ttu-id="ad314-209">**Usuń zależności**: po zaznaczeniu usuwa wszystkie zależne pakiety, jeśli nie są one przywoływane w innym miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad314-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="ad314-210">**Wymuś dezinstalację, nawet jeśli istnieją zależności**: w przypadku wybrania tej funkcji program Odinstalowuje pakiet nawet wtedy, gdy jest on nadal przywoływany w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad314-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="ad314-211">Jest to zwykle używane w połączeniu z **usuwaniem zależności** w celu usunięcia pakietu i wszelkich zależnych od niego zależności.</span><span class="sxs-lookup"><span data-stu-id="ad314-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="ad314-212">Użycie tej opcji może jednak prowadzić do przerwania odwołań w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad314-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="ad314-213">W takich przypadkach może być konieczne [ponowne zainstalowanie tych innych pakietów](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ad314-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
