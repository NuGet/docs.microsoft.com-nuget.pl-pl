---
title: Informacje o interfejsie użytkownika Menedżera pakietów NuGet
description: Instrukcje dotyczące używania interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 422faf99e58e058d86db774a8f3c1c576b3dc393
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637626"
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="ad87a-103">Interfejs użytkownika Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="ad87a-103">NuGet Package Manager UI</span></span>

<span data-ttu-id="ad87a-104">Interfejs użytkownika Menedżera pakietów NuGet w programie Visual Studio na Windows pozwala na łatwe instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="ad87a-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="ad87a-105">Aby w programie Visual Studio dla komputerów Mac, zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="ad87a-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="ad87a-106">Interfejs użytkownika Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ad87a-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="ad87a-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="ad87a-107">In this topic:</span></span>

- [<span data-ttu-id="ad87a-108">Znajdowanie i instalowanie pakietu (Karta Przeglądaj)</span><span class="sxs-lookup"><span data-stu-id="ad87a-108">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="ad87a-109">Odinstalowywanie pakietu (karta zainstalowane)</span><span class="sxs-lookup"><span data-stu-id="ad87a-109">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="ad87a-110">[Aktualizowanie pakietu (karty aktualizacji i zainstalowane)](#updating-a-package) (obejmuje ["Niejawnie odwołuje zestawu SDK" lub "AutoReferenced" wiadomości](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="ad87a-110">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="ad87a-111">[Zarządzanie pakietami dla rozwiązania](#managing-packages-for-the-solution) (Praca z wieloma projektami w tym samym czasie).</span><span class="sxs-lookup"><span data-stu-id="ad87a-111">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="ad87a-112">Źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="ad87a-112">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="ad87a-113">Kontrolowanie opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="ad87a-113">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="ad87a-114">Jeśli masz Brak Menedżera pakietów NuGet w programie Visual Studio 2015, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj *Menedżera pakietów NuGet* rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ad87a-114">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="ad87a-115">Jeśli nie możesz używać Instalator rozszerzenia programu Visual Studio, należy pobrać rozszerzenia bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ad87a-115">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="ad87a-116">W programie Visual Studio 2017 Menedżer pakietów NuGet i NuGet są instalowane automatycznie z żadną. Obciążenia związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="ad87a-116">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="ad87a-117">Zainstalować osobno, wybierając **poszczególne składniki > Kod Narzędzia > Menedżer pakietów NuGet** opcji w Instalatorze programu Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ad87a-117">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="ad87a-118">Znajdowanie i instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ad87a-118">Finding and installing a package</span></span>

1. <span data-ttu-id="ad87a-119">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy opcję **odwołania** lub projektu i wybierz **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="ad87a-119">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Zarządzanie pakietami NuGet w menu](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="ad87a-121">**Przeglądaj** karcie są wyświetlane według popularności z aktualnie wybranego źródła pakietów (zobacz [pakietu źródeł](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="ad87a-121">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="ad87a-122">Wyszukiwanie określonego pakietu, korzystając z pola wyszukiwania w lewym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="ad87a-122">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="ad87a-123">Wybierz pakiet z listy, aby wyświetlić jego informacje, które umożliwia także **zainstalować** przycisk wraz z menu rozwijane wybór wersji.</span><span class="sxs-lookup"><span data-stu-id="ad87a-123">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Zarządzanie karty Przeglądaj, okno dialogowe pakiety NuGet](media/Search.png)

1. <span data-ttu-id="ad87a-125">Wybierz żądaną wersję z listy rozwijanej i wybierz **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="ad87a-125">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="ad87a-126">Program Visual Studio instaluje pakiet i jego zależności do projektu.</span><span class="sxs-lookup"><span data-stu-id="ad87a-126">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="ad87a-127">Może zostać wyświetlona prośba o zaakceptowanie postanowień licencyjnych.</span><span class="sxs-lookup"><span data-stu-id="ad87a-127">You may be asked to accept license terms.</span></span> <span data-ttu-id="ad87a-128">Po zakończeniu instalacji dodano pakiety są widoczne na **zainstalowane** kartę. Pakiety są również wyszczególnione w **odwołania** węzła Eksploratora rozwiązań, wskazujący, że możesz zapoznać się z nimi w projekcie z `using` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ad87a-128">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Odwołania w Eksploratorze rozwiązań](media/References.png)

> [!Tip]
> <span data-ttu-id="ad87a-130">Obejmuje wersje wstępne w wyszukiwaniu i udostępnianie wersji wstępnych w wersji listy rozwijanej, wybierz **Uwzględnij wersję wstępną** opcji.</span><span class="sxs-lookup"><span data-stu-id="ad87a-130">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="ad87a-131">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ad87a-131">Uninstalling a package</span></span>

1. <span data-ttu-id="ad87a-132">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy opcję **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="ad87a-132">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="ad87a-133">Wybierz **zainstalowane** kartę.</span><span class="sxs-lookup"><span data-stu-id="ad87a-133">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="ad87a-134">Wybierz pakiet, aby odinstalować (przy użyciu wyszukiwania, aby filtrować listę, jeśli to konieczne), a następnie wybierz **Odinstaluj**.</span><span class="sxs-lookup"><span data-stu-id="ad87a-134">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Odinstalowywanie pakietu](media/UninstallPackage.png)

1. <span data-ttu-id="ad87a-136">Należy pamiętać, że **Uwzględnij wersję wstępną** i **źródła pakietu** formanty nie mają zastosowania podczas odinstalowywanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad87a-136">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="ad87a-137">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ad87a-137">Updating a package</span></span>

1. <span data-ttu-id="ad87a-138">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy opcję **odwołania** lub żądanego projektu i wybierz **Zarządzaj pakietami NuGet...** . (W projektach witryny sieci web, kliknij prawym przyciskiem myszy **Bin** folderu.)</span><span class="sxs-lookup"><span data-stu-id="ad87a-138">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="ad87a-139">Wybierz **aktualizacje** kartę, aby zobaczyć pakiety, które są dostępne aktualizacje ze źródeł wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ad87a-139">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="ad87a-140">Wybierz **Uwzględnij wersję wstępną** obejmujący pakietów wydań wstępnych, na liście aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ad87a-140">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="ad87a-141">Wybierz pakiet do aktualizacji, wybierz żądaną wersję z listy rozwijanej po prawej stronie, a następnie wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="ad87a-141">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualizowanie pakietu](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="ad87a-143">W przypadku niektórych pakietów **aktualizacji** przycisk jest niedostępny i zostanie wyświetlony komunikat informujący o tym, że odwołuje się do"niejawnie zestawu SDK" (lub "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="ad87a-143">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="ad87a-144">Ten komunikat oznacza, że pakiet jest częścią większej struktury lub zestawu SDK i nie powinny być aktualizowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="ad87a-144">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="ad87a-145">(Wewnętrznie są oznaczone takie pakiety `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Na przykład `Microsoft.NETCore.App` jest częścią zestawu .NET Core SDK i wersję pakietu nie jest taka sama jak wersja framework środowiska uruchomieniowego używane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="ad87a-145">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="ad87a-146">Musisz [aktualizacji instalacji platformy .NET Core](https://aka.ms/dotnet-download) można pobrać nowe wersje środowiska uruchomieniowego platformy ASP.NET Core i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ad87a-146">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="ad87a-147">[Zobacz ten dokument, aby uzyskać więcej informacji na metapakiety platformy .NET Core i przechowywanie wersji](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="ad87a-147">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="ad87a-148">Dotyczy to często używane następujące pakiety:</span><span class="sxs-lookup"><span data-stu-id="ad87a-148">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="ad87a-149">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="ad87a-149">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="ad87a-150">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="ad87a-150">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="ad87a-151">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="ad87a-151">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="ad87a-152">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="ad87a-152">NETStandard.Library</span></span>

    ![Przykład pakietu oznaczenie niejawnie odwołania lub AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="ad87a-154">Aby zaktualizować wielu pakietów do ich najnowszych wersji, zaznacz je na liście i wybierz **aktualizacji** przycisk nad listą.</span><span class="sxs-lookup"><span data-stu-id="ad87a-154">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="ad87a-155">Możesz także zaktualizować poszczególnych pakietów, od **zainstalowane** kartę. W tym przypadku szczegóły pakietu obejmują selektor wersji (podlegają **Uwzględnij wersję wstępną** opcja) i **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ad87a-155">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="ad87a-156">Zarządzanie pakietami dla rozwiązania</span><span class="sxs-lookup"><span data-stu-id="ad87a-156">Managing packages for the solution</span></span>

<span data-ttu-id="ad87a-157">Zarządzanie pakietami dla rozwiązania jest wygodny sposób pracy z wieloma projektami równocześnie.</span><span class="sxs-lookup"><span data-stu-id="ad87a-157">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="ad87a-158">Wybierz **Narzędzia > Menedżer pakietów NuGet > Zarządzaj pakietami NuGet dla rozwiązania...**  menu poleceń, lub kliknij prawym przyciskiem myszy rozwiązanie i wybierz pozycję **Zarządzaj pakietami NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="ad87a-158">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Zarządzaj pakietami NuGet dla rozwiązania](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="ad87a-160">Podczas zarządzania pakietami dla rozwiązania, interfejs użytkownika umożliwia Wybierz projekty, których dotyczy operacji:</span><span class="sxs-lookup"><span data-stu-id="ad87a-160">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selektor projektu podczas zarządzania pakietami dla rozwiązania](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="ad87a-162">Konsolidacja kartę</span><span class="sxs-lookup"><span data-stu-id="ad87a-162">Consolidate tab</span></span>

<span data-ttu-id="ad87a-163">Deweloperzy zazwyczaj należy wziąć pod uwagę jej złym zwyczajem korzystają z różnych wersji pakietu NuGet między różnymi projektami w tym samym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ad87a-163">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="ad87a-164">W przypadku zarządzania pakietami dla rozwiązania udostępnia interfejs użytkownika Menedżera pakietów **Konsolidacja** karty, na którym można łatwo zobaczyć gdzie pakiety z numerami wersji distinct są używane przez różne projekty w rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="ad87a-164">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Karta Konsolidacja interfejsu użytkownika Menedżera pakietów](media/ConsolidateTab.png)

<span data-ttu-id="ad87a-166">W tym przykładzie projekt ClassLibrary1 jest za pomocą platformy EntityFramework 6.2.0, natomiast ConsoleApp1 jest za pomocą platformy EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="ad87a-166">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="ad87a-167">Aby skonsolidować wersje pakietów, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ad87a-167">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="ad87a-168">Wybierz projekty, które można zaktualizować w liście projektu.</span><span class="sxs-lookup"><span data-stu-id="ad87a-168">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="ad87a-169">Wybierz wersję do użycia w tych projektach w **wersji** kontrolki, takiej jak 6.2.0 platformy EntityFramework.</span><span class="sxs-lookup"><span data-stu-id="ad87a-169">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="ad87a-170">Wybierz **zainstalować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ad87a-170">Select the **Install** button.</span></span>

<span data-ttu-id="ad87a-171">Menedżer pakietów powoduje zainstalowanie wersji wybranego pakietu do wszystkich wybranych projektów, po upływie których pakiet nie jest już wyświetlany na **Konsolidacja** kartę.</span><span class="sxs-lookup"><span data-stu-id="ad87a-171">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="ad87a-172">Źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="ad87a-172">Package sources</span></span>

<span data-ttu-id="ad87a-173">Aby zmienić źródło, z którego program Visual Studio pobiera pakiety, wybierz jeden z selektora źródła:</span><span class="sxs-lookup"><span data-stu-id="ad87a-173">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selektor źródła pakietów w interfejs użytkownika Menedżera pakietów](media/PackageSourceDropDown.png)

<span data-ttu-id="ad87a-175">Aby zarządzać źródeł pakietów:</span><span class="sxs-lookup"><span data-stu-id="ad87a-175">To manage package sources:</span></span>

1. <span data-ttu-id="ad87a-176">Wybierz **ustawienia** ikony w Interfejsie użytkownika Menedżera pakietów opisane poniżej, lub użyj **Narzędzia > Opcje** polecenia, a następnie przewiń listę do **Menedżera pakietów NuGet**:</span><span class="sxs-lookup"><span data-stu-id="ad87a-176">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ikona ustawienia interfejsu użytkownika Menedżera pakietów](media/PackageSourceSettings.png)

1. <span data-ttu-id="ad87a-178">Wybierz **źródeł pakietów** węzła:</span><span class="sxs-lookup"><span data-stu-id="ad87a-178">Select the **Package Sources** node:</span></span>

    ![Opcje źródła pakietów](media/options.png)

1. <span data-ttu-id="ad87a-180">Aby dodać źródła, wybierz **+**, umożliwia edytowanie nazwy, wprowadź adres URL lub ścieżkę w **źródła** sterowania, a następnie wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="ad87a-180">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="ad87a-181">Źródło jest teraz wyświetlany w selektorze listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ad87a-181">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="ad87a-182">Aby zmienić źródło pakietu, należy ją zaznaczyć, dokonaj edycji w **nazwa** i **źródła** pola, a następnie wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="ad87a-182">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="ad87a-183">Aby wyłączyć źródło pakietu, wyczyść pole po lewej stronie nazwy na liście.</span><span class="sxs-lookup"><span data-stu-id="ad87a-183">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="ad87a-184">Aby usunąć źródło pakietu, wybierz ją, a następnie wybierz pozycję **X** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ad87a-184">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="ad87a-185">Za pomocą w górę i Strzałka w dół przyciski nie zmienia kolejność priorytetów źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="ad87a-185">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="ad87a-186">Program Visual Studio ignoruje kolejność źródeł pakietów przy użyciu pakietów z dowolnego źródła najpierw do odpowiadania na żądania.</span><span class="sxs-lookup"><span data-stu-id="ad87a-186">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="ad87a-187">Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ad87a-187">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="ad87a-188">Jeśli źródło pakietu pojawi się ponownie po jej usunięciu, mogą być wymienione w poziomie komputera lub użytkownika na poziomie `NuGet.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="ad87a-188">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="ad87a-189">Zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md) dla lokalizacji tych plików, następnie usuń źródła przez edycję plików ręcznie lub za pomocą [nuget źródeł polecenia](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ad87a-189">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="ad87a-190">Kontrolowanie opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="ad87a-190">Package manager Options control</span></span>

<span data-ttu-id="ad87a-191">Po wybraniu pakietu interfejsu użytkownika Menedżera pakietów wyświetla mały rozwijania **opcje** kontroli poniżej selektor wersji (tutaj pokazane zarówno zwinięte i rozwinięte).</span><span class="sxs-lookup"><span data-stu-id="ad87a-191">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="ad87a-192">Należy zauważyć, że dla niektórych projektów tylko typy **Pokaż okno podglądu** znajduje się opcja.</span><span class="sxs-lookup"><span data-stu-id="ad87a-192">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opcje Menedżera pakietów](media/PackageManagerUIOptions.png)

<span data-ttu-id="ad87a-194">W poniższych sekcjach opisano te opcje.</span><span class="sxs-lookup"><span data-stu-id="ad87a-194">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="ad87a-195">Pokaż okno (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="ad87a-195">Show preview window</span></span>

<span data-ttu-id="ad87a-196">Po wybraniu modalny Wyświetla które zależności wybranego pakietu przed zainstalowaniem pakietu:</span><span class="sxs-lookup"><span data-stu-id="ad87a-196">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Przykładowe okno dialogowe z wersji zapoznawczej](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="ad87a-198">Instalowanie i aktualizowanie opcje</span><span class="sxs-lookup"><span data-stu-id="ad87a-198">Install and Update Options</span></span>

<span data-ttu-id="ad87a-199">(Niedostępne dla wszystkich typów projektów).</span><span class="sxs-lookup"><span data-stu-id="ad87a-199">(Not available for all project types.)</span></span>

<span data-ttu-id="ad87a-200">**Zachowanie zależności** konfiguruje się, jak NuGet decyduje, które wersje zależne pakiety do zainstalowania:</span><span class="sxs-lookup"><span data-stu-id="ad87a-200">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="ad87a-201">*Ignoruj zależności* pomija instalowanie jakieś zależności, która dzieli zazwyczaj jest zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="ad87a-201">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="ad87a-202">*Najniższy* [domyślnie] instaluje zależność o numerze minimalnej wersji, który spełnia wymagania wybranego pakiet główny.</span><span class="sxs-lookup"><span data-stu-id="ad87a-202">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="ad87a-203">*Poprawka najwyższy* powoduje zainstalowanie wersji z takie same numery wersji głównych i pomocniczych, ale najwyższy numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="ad87a-203">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="ad87a-204">Na przykład jeśli określono wersję 1.2.2 następnie najwyższa wersja, która rozpoczyna się od 1.2 zostanie zainstalowany</span><span class="sxs-lookup"><span data-stu-id="ad87a-204">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="ad87a-205">*Najwyższy drobnych* powoduje zainstalowanie wersji ten sam główny numer wersji, ale najwyższy numer podrzędny i numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="ad87a-205">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="ad87a-206">Jeśli wersja 1.2.2 jest określona, następnie najwyższa wersja, która rozpoczyna się od 1 zostanie zainstalowany</span><span class="sxs-lookup"><span data-stu-id="ad87a-206">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="ad87a-207">*Najwyższy* instaluje najwyższej dostępnej wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="ad87a-207">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="ad87a-208">**Plik akcji konflikt** określa sposób obsługi NuGet pakiety, które już istnieją w projekcie lub komputer lokalny:</span><span class="sxs-lookup"><span data-stu-id="ad87a-208">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="ad87a-209">*Monituj* powoduje, że rozszerzenie NuGet, aby zadać, czy zachować, czy zastąpić istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="ad87a-209">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="ad87a-210">*Ignoruj wszystkie* powoduje, że rozszerzenie NuGet, aby pominąć, zastępując istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="ad87a-210">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="ad87a-211">*Zastąpienie wszystkich* powoduje, że rozszerzenie NuGet, aby zastąpić istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="ad87a-211">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="ad87a-212">Odinstaluj opcje</span><span class="sxs-lookup"><span data-stu-id="ad87a-212">Uninstall Options</span></span>

<span data-ttu-id="ad87a-213">(Niedostępne dla wszystkich typów projektów).</span><span class="sxs-lookup"><span data-stu-id="ad87a-213">(Not available for all project types.)</span></span>

<span data-ttu-id="ad87a-214">**Usuń zależności**: po wybraniu usuwa wszelkie zależne pakiety, jeśli są one nie odwoływać się gdzie indziej w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad87a-214">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="ad87a-215">**Wymuszaj odinstalowanie nawet, jeśli istnieją zależności na nim**: po wybraniu odinstalowuje pakiet nawet wtedy, gdy nadal jest on przywoływany w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad87a-215">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="ad87a-216">To jest zwykle używany w połączeniu z **usuwanie zależności** do usunięcia pakietu i niezależnie od zależności ona zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="ad87a-216">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="ad87a-217">Użycie tej opcji może jednak prowadzić do przerwanymi odwołaniami w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ad87a-217">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="ad87a-218">W takich przypadkach może być konieczne [ponownie zainstalować te pakiety innych](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ad87a-218">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
