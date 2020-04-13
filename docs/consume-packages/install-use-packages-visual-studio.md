---
title: Instalowanie pakietów NuGet i zarządzanie nimi w programie Visual Studio
description: Instrukcje dotyczące korzystania z interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet.
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
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428696"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="40b07-103">Instalowanie pakietów w programie Visual Studio i zarządzanie nimi przy użyciu Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="40b07-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="40b07-104">Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio w systemie Windows umożliwia łatwe instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="40b07-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="40b07-105">Aby uzyskać środowisko w programie Visual Studio dla komputerów Mac, zobacz [Dołączanie pakietu NuGet w projekcie.](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)</span><span class="sxs-lookup"><span data-stu-id="40b07-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="40b07-106">Interfejs użytkownika Menedżera pakietów nie jest dołączony do kodu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40b07-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="40b07-107">Jeśli brakuje Menedżera pakietów NuGet w programie Visual Studio 2015, sprawdź **narzędzia > rozszerzenia i aktualizacje...** i wyszukaj rozszerzenie Menedżera *pakietów NuGet.*</span><span class="sxs-lookup"><span data-stu-id="40b07-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="40b07-108">Jeśli nie możesz użyć instalatora rozszerzeń w programie Visual [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Studio, pobierz je bezpośrednio z programu .</span><span class="sxs-lookup"><span data-stu-id="40b07-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="40b07-109">Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są automatycznie instalowane z dowolnym . Obciążenia związane z siecią.</span><span class="sxs-lookup"><span data-stu-id="40b07-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="40b07-110">Zainstaluj go indywidualnie, wybierając poszczególne składniki > narzędzia Kodu > menedżera **pakietów NuGet** w instalatorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40b07-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="40b07-111">Znajdowanie i instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="40b07-111">Find and install a package</span></span>

1. <span data-ttu-id="40b07-112">W **Eksploratorze rozwiązań**kliknij prawym przyciskiem myszy **odwołania** lub projekt i wybierz pozycję **Zarządzaj pakietami NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="40b07-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Opcja menu Zarządzanie pakietami NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="40b07-114">Karta **Przeglądaj** wyświetla pakiety według popularności z aktualnie wybranego źródła (patrz [źródła pakietów).](#package-sources)</span><span class="sxs-lookup"><span data-stu-id="40b07-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="40b07-115">Wyszukaj określony pakiet za pomocą pola wyszukiwania w lewym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="40b07-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="40b07-116">Wybierz pakiet z listy, aby wyświetlić jego informacje, co również włącza przycisk **Zainstaluj** wraz z listą rozwijaną wyboru wersji.</span><span class="sxs-lookup"><span data-stu-id="40b07-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Karta Przeglądanie okna dialogowego Zarządzanie pakietami NuGet](media/Search.png)

1. <span data-ttu-id="40b07-118">Wybierz żądaną wersję z listy rozwijanej i wybierz **pozycję Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="40b07-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="40b07-119">Visual Studio instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="40b07-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="40b07-120">Użytkownik może zostać poproszony o zaakceptowanie postanowień licencyjnych.</span><span class="sxs-lookup"><span data-stu-id="40b07-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="40b07-121">Po zakończeniu instalacji dodane pakiety są wyświetlane na karcie **References** `using` **Zainstalowane.**</span><span class="sxs-lookup"><span data-stu-id="40b07-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Odwołania w Eksploratorze rozwiązań](media/References.png)

> [!Tip]
> <span data-ttu-id="40b07-123">Aby uwzględnić wersje wersji wstępnej w wyszukiwaniu i udostępnić wersje wstępnej w wersji rozwijanej, wybierz opcję **Dołącz wersję wstępną.**</span><span class="sxs-lookup"><span data-stu-id="40b07-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="40b07-124">NuGet ma dwa formaty, w których [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)projekt może używać pakietów: i .</span><span class="sxs-lookup"><span data-stu-id="40b07-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="40b07-125">[Wartość domyślną można ustawić w oknie opcji programu Visual Studio](Package-Restore.md#choose-default-package-management-format).</span><span class="sxs-lookup"><span data-stu-id="40b07-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="40b07-126">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="40b07-126">Uninstall a package</span></span>

1. <span data-ttu-id="40b07-127">W **Eksploratorze rozwiązań**kliknij prawym przyciskiem myszy **odwołania** lub żądany projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="40b07-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="40b07-128">Wybierz kartę **Zainstalowano**.</span><span class="sxs-lookup"><span data-stu-id="40b07-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="40b07-129">Wybierz pakiet do odinstalowania (w razie potrzeby za pomocą wyszukiwania odfiltrować listę) i wybierz pozycję **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="40b07-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. <span data-ttu-id="40b07-131">Należy zauważyć, że **uwzględnij prerelease** i **Package source** formantów nie mają wpływu podczas odinstalowywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="40b07-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="40b07-132">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="40b07-132">Update a package</span></span>

1. <span data-ttu-id="40b07-133">W **Eksploratorze rozwiązań**kliknij prawym przyciskiem myszy **odwołania** lub żądany projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet...**. (W projektach witryn sieci Web kliknij prawym przyciskiem myszy folder **Bin).**</span><span class="sxs-lookup"><span data-stu-id="40b07-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="40b07-134">Wybierz kartę **Aktualizacje,** aby wyświetlić pakiety, które mają dostępne aktualizacje z wybranych źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="40b07-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="40b07-135">Wybierz **dołącz wstępnąrelea,** aby uwzględnić pakiety wersji wstępnej na liście aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="40b07-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="40b07-136">Wybierz pakiet do aktualizacji, wybierz żądaną wersję z listy rozwijanej po prawej stronie i wybierz pozycję **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="40b07-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="40b07-138">W przypadku niektórych pakietów przycisk **Aktualizuj** jest wyłączony i pojawia się komunikat informujący, że jest "niejawnie odwołuje się SDK" (lub "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="40b07-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="40b07-139">Ten komunikat wskazuje, że pakiet jest częścią większej struktury lub zestawu SDK i nie powinien być aktualizowany niezależnie.</span><span class="sxs-lookup"><span data-stu-id="40b07-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="40b07-140">(Takie pakiety są `<IsImplicitlyDefined>True</IsImplicitlyDefined>`wewnętrznie oznaczone .) Na przykład `Microsoft.NETCore.App` jest częścią zestawu .NET Core SDK, a wersja pakietu nie jest taka sama jak wersja struktury środowiska wykonawczego używane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="40b07-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="40b07-141">Musisz [zaktualizować instalację .NET Core,](https://aka.ms/dotnet-download) aby uzyskać nowe wersje środowiska wykonawczego ASP.NET Core i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="40b07-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="40b07-142">[Więcej informacji na temat metapakietów rdzeni .NET i przechowywania wersji można znaleźć w tym dokumencie.](/dotnet/core/packages)</span><span class="sxs-lookup"><span data-stu-id="40b07-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="40b07-143">Dotyczy to następujących powszechnie używanych pakietów:</span><span class="sxs-lookup"><span data-stu-id="40b07-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="40b07-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="40b07-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="40b07-145">Aplikacja Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="40b07-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="40b07-146">Aplikacja Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="40b07-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="40b07-147">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="40b07-147">NETStandard.Library</span></span>

    ![Przykładowy pakiet oznaczony jako niejawnie odwołania lub AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="40b07-149">Aby zaktualizować wiele pakietów do ich najnowszych wersji, zaznacz je na liście i wybierz przycisk **Aktualizuj** nad listą.</span><span class="sxs-lookup"><span data-stu-id="40b07-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="40b07-150">Można również zaktualizować pojedynczy pakiet na karcie **Zainstalowane.** W takim przypadku szczegóły pakietu obejmują selektor wersji (z zastrzeżeniem opcji **Dołącz wersję wstępną)** i przycisk **Update.**</span><span class="sxs-lookup"><span data-stu-id="40b07-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="40b07-151">Zarządzanie pakietami dla rozwiązania</span><span class="sxs-lookup"><span data-stu-id="40b07-151">Manage packages for the solution</span></span>

<span data-ttu-id="40b07-152">Zarządzanie pakietami dla rozwiązania jest wygodnym sposobem pracy z wieloma projektami jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="40b07-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="40b07-153">Wybierz polecenie **menu Narzędzia > Menedżera pakietów NuGet > zarządzanie pakietami NuGet dla rozwiązania...** lub kliknij prawym przyciskiem myszy rozwiązanie i wybierz polecenie **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="40b07-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Zarządzanie pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="40b07-155">Podczas zarządzania pakietami dla rozwiązania interfejsu użytkownika pozwala wybrać projekty, których dotyczą operacje:</span><span class="sxs-lookup"><span data-stu-id="40b07-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="40b07-157">Karta Konsolidacja</span><span class="sxs-lookup"><span data-stu-id="40b07-157">Consolidate tab</span></span>

<span data-ttu-id="40b07-158">Deweloperzy zazwyczaj uważają, że złe praktyki do korzystania z różnych wersji tego samego pakietu NuGet w różnych projektach w tym samym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="40b07-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="40b07-159">Po wybraniu do zarządzania pakietami dla rozwiązania, Interfejs menedżera pakietów udostępnia **konsolidować** kartę, na której można łatwo zobaczyć, gdzie pakiety z różnymi numerami wersji są używane przez różne projekty w rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="40b07-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Karta Konsolidacja interfejsu użytkownika menedżera pakietów](media/ConsolidateTab.png)

<span data-ttu-id="40b07-161">W tym przykładzie classlibrary1 projektu używa EntityFramework 6.2.0, podczas gdy ConsoleApp1 używa EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="40b07-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="40b07-162">Aby skonsolidować wersje pakietów, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="40b07-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="40b07-163">Wybierz projekty, które mają być aktualizowane na liście projektów.</span><span class="sxs-lookup"><span data-stu-id="40b07-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="40b07-164">Wybierz wersję, która ma być używana we wszystkich tych projektach w **formancie Wersja,** takich jak EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="40b07-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="40b07-165">Wybierz przycisk **Zainstaluj.**</span><span class="sxs-lookup"><span data-stu-id="40b07-165">Select the **Install** button.</span></span>

<span data-ttu-id="40b07-166">Menedżer pakietów instaluje wybraną wersję pakietu we wszystkich wybranych projektach, po czym pakiet nie jest już wyświetlany na karcie **Konsolidacja.**</span><span class="sxs-lookup"><span data-stu-id="40b07-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="40b07-167">Źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="40b07-167">Package sources</span></span>

<span data-ttu-id="40b07-168">Aby zmienić źródło, z którego program Visual Studio uzyskuje pakiety, wybierz jeden z selektora źródłowego:</span><span class="sxs-lookup"><span data-stu-id="40b07-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selektor źródła pakietów w interfejsie użytkownika menedżera pakietów](media/PackageSourceDropDown.png)

<span data-ttu-id="40b07-170">Aby zarządzać źródłami pakietów:</span><span class="sxs-lookup"><span data-stu-id="40b07-170">To manage package sources:</span></span>

1. <span data-ttu-id="40b07-171">Wybierz ikonę **Ustawienia** w interfejsie użytkownika Menedżera pakietów opisanego poniżej lub użyj polecenia **Narzędzia > Opcje** i przewiń do Menedżera **pakietów NuGet:**</span><span class="sxs-lookup"><span data-stu-id="40b07-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ikona ustawień interfejsu użytkownika menedżera pakietów](media/PackageSourceSettings.png)

1. <span data-ttu-id="40b07-173">Wybierz węzeł **Źródła pakietów:**</span><span class="sxs-lookup"><span data-stu-id="40b07-173">Select the **Package Sources** node:</span></span>

    ![Opcje źródeł pakietów](media/options.png)

1. <span data-ttu-id="40b07-175">Aby dodać źródło, **+** wybierz , edytuj nazwę, wprowadź adres URL lub ścieżkę w formancie **Źródło** i wybierz pozycję **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="40b07-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="40b07-176">Źródło pojawi się teraz w z listy rozwijanej selektora.</span><span class="sxs-lookup"><span data-stu-id="40b07-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="40b07-177">Aby zmienić źródło pakietu, zaznacz je, wykonuj zmiany w polach **Nazwa** i **Źródło, a** następnie wybierz pozycję **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="40b07-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="40b07-178">Aby wyłączyć źródło pakietu, wyczyść pole po lewej stronie nazwy na liście.</span><span class="sxs-lookup"><span data-stu-id="40b07-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="40b07-179">Aby usunąć źródło pakietu, zaznacz go, a następnie wybierz przycisk **X.**</span><span class="sxs-lookup"><span data-stu-id="40b07-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="40b07-180">Za pomocą przycisków strzałki w górę i w dół nie zmienia kolejność priorytetów źródeł pakietu.</span><span class="sxs-lookup"><span data-stu-id="40b07-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="40b07-181">Visual Studio ignoruje kolejność źródeł pakietów, przy użyciu pakietu, z któregokolwiek źródła jest pierwszy odpowiedzieć na żądania.</span><span class="sxs-lookup"><span data-stu-id="40b07-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="40b07-182">Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="40b07-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="40b07-183">Jeśli źródło pakietu pojawi się ponownie po usunięciu go, może być wymieniony w `NuGet.Config` plikach na poziomie komputera lub na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40b07-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="40b07-184">Zobacz [typowe konfiguracje NuGet](../consume-packages/configuring-nuget-behavior.md) dla lokalizacji tych plików, a następnie usunąć źródło, edytując pliki ręcznie lub za pomocą [polecenia nuget sources](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="40b07-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="40b07-185">Kontrola opcji menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="40b07-185">Package manager Options control</span></span>

<span data-ttu-id="40b07-186">Po wybraniu pakietu interfejs użytkownika Menedżera pakietów wyświetla mały, rozwijany **formant Opcji** poniżej selektora wersji (pokazane tutaj zarówno zwinięte, jak i rozwinięte).</span><span class="sxs-lookup"><span data-stu-id="40b07-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="40b07-187">Należy zauważyć, że w przypadku niektórych typów projektów dostępna jest tylko opcja **Pokaż okno podglądu.**</span><span class="sxs-lookup"><span data-stu-id="40b07-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opcje menedżera pakietów](media/PackageManagerUIOptions.png)

<span data-ttu-id="40b07-189">W poniższych sekcjach wyjaśniono te opcje.</span><span class="sxs-lookup"><span data-stu-id="40b07-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="40b07-190">Pokaż okno podglądu</span><span class="sxs-lookup"><span data-stu-id="40b07-190">Show preview window</span></span>

<span data-ttu-id="40b07-191">Po wybraniu tej opcji w oknie modalnym zostaną wyświetlone zależności wybranego pakietu przed zainstalowaniem pakietu:</span><span class="sxs-lookup"><span data-stu-id="40b07-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Przykładowe okno dialogowe podglądu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="40b07-193">Opcje instalacji i aktualizacji</span><span class="sxs-lookup"><span data-stu-id="40b07-193">Install and Update Options</span></span>

<span data-ttu-id="40b07-194">(Niedostępne dla wszystkich typów projektów).</span><span class="sxs-lookup"><span data-stu-id="40b07-194">(Not available for all project types.)</span></span>

<span data-ttu-id="40b07-195">**Zachowanie zależności** konfiguruje sposób, w jaki NuGet decyduje, które wersje pakietów zależnych należy zainstalować:</span><span class="sxs-lookup"><span data-stu-id="40b07-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="40b07-196">*Ignoruj zależności* pomija instalowanie żadnych zależności, które zazwyczaj przerywa pakiet jest instalowany.</span><span class="sxs-lookup"><span data-stu-id="40b07-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="40b07-197">*Najniższa* [Domyślna] instaluje zależność z minimalnym numerem wersji, który spełnia wymagania wybranego pakietu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="40b07-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="40b07-198">*Najwyższa poprawka* instaluje wersję z tymi samymi głównymi i pomocniczymi numerami wersji, ale z najwyższą liczbą poprawek.</span><span class="sxs-lookup"><span data-stu-id="40b07-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="40b07-199">Na przykład, jeśli określono wersję 1.2.2, zostanie zainstalowana najwyższa wersja, która zaczyna się od wersji 1.2</span><span class="sxs-lookup"><span data-stu-id="40b07-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="40b07-200">*Najwyższy Minor* instaluje wersję z tym samym głównym numerem wersji, ale z najwyższą liczbą pomocniczą i numerem poprawki.</span><span class="sxs-lookup"><span data-stu-id="40b07-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="40b07-201">Jeśli zostanie określona wersja 1.2.2, zostanie zainstalowana najwyższa wersja, która zaczyna się od 1</span><span class="sxs-lookup"><span data-stu-id="40b07-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="40b07-202">*Najwyższa* instaluje najwyższą dostępną wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="40b07-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="40b07-203">**Akcja konfliktu plików** określa, jak NuGet powinien obsługiwać pakiety, które już istnieją w projekcie lub na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="40b07-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="40b07-204">*Prompt* nakazuje NuGet zapytać, czy zachować lub zastąpić istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="40b07-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="40b07-205">*Ignoruj wszystko* nakazuje NuGet pominąć zastępowanie istniejących pakietów.</span><span class="sxs-lookup"><span data-stu-id="40b07-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="40b07-206">*Zastąpienie wszystkie* nakazuje NuGet zastąpić wszystkie istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="40b07-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="40b07-207">Opcje odinstalowywania</span><span class="sxs-lookup"><span data-stu-id="40b07-207">Uninstall Options</span></span>

<span data-ttu-id="40b07-208">(Niedostępne dla wszystkich typów projektów).</span><span class="sxs-lookup"><span data-stu-id="40b07-208">(Not available for all project types.)</span></span>

<span data-ttu-id="40b07-209">**Usuń zależności:** gdy ta opcja jest zaznaczona, usuwa wszystkie pakiety zależne, jeśli nie są one dostępne w innym miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="40b07-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="40b07-210">**Wymuś odinstalowanie, nawet jeśli istnieją zależności od niego:** po wybraniu, odinstalowuje pakiet, nawet jeśli jest nadal odwołuje się w projekcie.</span><span class="sxs-lookup"><span data-stu-id="40b07-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="40b07-211">Jest to zwykle używane w połączeniu z **Usuń zależności,** aby usunąć pakiet i niezależnie od zależności, które zainstalowano.</span><span class="sxs-lookup"><span data-stu-id="40b07-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="40b07-212">Użycie tej opcji może jednak prowadzić do przerwanych odwołań w projekcie.</span><span class="sxs-lookup"><span data-stu-id="40b07-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="40b07-213">W takich przypadkach może być konieczne [ponowne zainstalowanie tych innych pakietów](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="40b07-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
