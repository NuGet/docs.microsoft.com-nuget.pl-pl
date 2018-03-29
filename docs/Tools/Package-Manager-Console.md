---
title: Przewodnik konsoli Menedżera pakietów NuGet | Dokumentacja firmy Microsoft
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
f1_keywords:
- vs.nuget.packagemanager.console
description: Instrukcje dotyczące używania konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
keywords: Konsoli Menedżera pakietów NuGet, programu NuGet powershell zarządzać pakietami NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: af22a524f6b4a41a4c24077fe396846da6fb1ff8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="97377-104">Konsola Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="97377-104">Package Manager Console</span></span>

<span data-ttu-id="97377-105">Konsola Menedżera pakietów NuGet jest wbudowany w program Visual Studio w systemie Windows w wersji 2012 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="97377-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="97377-106">(Nie jest dołączony do programu Visual Studio for Mac lub Visual Studio Code.)</span><span class="sxs-lookup"><span data-stu-id="97377-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="97377-107">Konsolę pozwala używać [poleceń programu NuGet PowerShell](../tools/powershell-reference.md) można znaleźć, instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="97377-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="97377-108">Za pomocą konsoli jest niezbędne w przypadku, gdy interfejsu użytkownika Menedżera pakietów nie umożliwiają wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="97377-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="97377-109">Aby użyć `nuget.exe` poleceń w konsoli, zobacz [przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="97377-109">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="97377-110">Na przykład Znajdowanie i instalowanie pakietu wykonuje się za pomocą trzy łatwe kroki:</span><span class="sxs-lookup"><span data-stu-id="97377-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="97377-111">Otwórz projekt/rozwiązanie w programie Visual Studio, a następnie otwórz za pomocą konsoli **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="97377-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="97377-112">Znajdź pakiet, który chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="97377-112">Find the package you want to install.</span></span> <span data-ttu-id="97377-113">Jeśli znasz już to, przejdź do kroku 3.</span><span class="sxs-lookup"><span data-stu-id="97377-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="97377-114">Uruchom polecenie instalacji:</span><span class="sxs-lookup"><span data-stu-id="97377-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="97377-115">Można również wykonać wszystkie operacje, które są dostępne w konsoli za pomocą [interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="97377-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="97377-116">Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisane projektu/rozwiązania i często osiągnąć więcej niż ich równoważnych poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="97377-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="97377-117">Na przykład instalowania pakietu w konsoli dodaje odwołanie do projektu, natomiast polecenia interfejsu wiersza polecenia nie.</span><span class="sxs-lookup"><span data-stu-id="97377-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="97377-118">Z tego powodu deweloperów pracujących w programie Visual Studio zwykle preferowane przy użyciu konsoli do interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="97377-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="97377-119">Wiele operacji konsoli zależą od tego, o rozwiązania otwarte w programie Visual Studio o nazwie znanej ścieżce.</span><span class="sxs-lookup"><span data-stu-id="97377-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="97377-120">Jeśli masz niezapisane rozwiązanie lub żadne rozwiązanie, zostanie wyświetlony błąd, "nie jest otwarty lub nie zapisano rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="97377-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="97377-121">Upewnij się, że masz otwarte i zapisane rozwiązanie."</span><span class="sxs-lookup"><span data-stu-id="97377-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="97377-122">Oznacza to, że konsola nie może określić folder rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="97377-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="97377-123">Zapisywanie niezapisane rozwiązanie lub tworzenie i zapisywanie rozwiązanie, jeśli nie masz open, należy rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="97377-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="97377-124">Otwieranie konsoli i formanty konsoli</span><span class="sxs-lookup"><span data-stu-id="97377-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="97377-125">Otwórz program Visual Studio przy użyciu **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="97377-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="97377-126">Konsoli jest oknem programu Visual Studio, które mogą być rozmieszczane i znajduje się jednak chcesz (zobacz [dostosowywanie układów okien w programie Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="97377-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="97377-127">Domyślnie polecenia konsoli działają z określonego pakietu źródłowego i projektu jako zestaw w formancie w górnej części okna:</span><span class="sxs-lookup"><span data-stu-id="97377-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Formanty Konsola Menedżera pakietów dla projektów i źródła pakietu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="97377-129">Wybieranie źródła różnych pakietów i/lub projektu zmiany tych wartości domyślnych dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="97377-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="97377-130">Aby overrride tych ustawień bez zmiany ustawień domyślnych, większość używanych poleceń obsługiwać `-Source` i `-ProjectName` opcje.</span><span class="sxs-lookup"><span data-stu-id="97377-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="97377-131">Aby zarządzać źródła pakietów, wybierz ikonę Koło zębate.</span><span class="sxs-lookup"><span data-stu-id="97377-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="97377-132">Jest to skrót do **Narzędzia > Opcje > Menedżera pakietów NuGet > źródła pakietów** okno dialogowe zgodnie z opisem na [interfejsu użytkownika Menedżera pakietów](package-manager-ui.md#package-sources) strony.</span><span class="sxs-lookup"><span data-stu-id="97377-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="97377-133">Ponadto kontrolka selektora projektu z prawej strony Czyści zawartość konsoli programu:</span><span class="sxs-lookup"><span data-stu-id="97377-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Ustawienia konsoli Menedżera pakietów i usuń zaznaczenie formantów](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="97377-135">Po prawej stronie przycisku przerwań polecenia długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="97377-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="97377-136">Na przykład uruchomiona `Get-Package -ListAvailable -PageSize 500` listy pierwszych 500 pakietów na domyślne źródło (na przykład nuget.org), co może zająć kilka minut do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="97377-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Formant stop Konsola Menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="97377-138">Instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="97377-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="97377-139">Zobacz [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="97377-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="97377-140">Instalowanie pakietu w konsoli wykonuje te same kroki, zgodnie z opisem na [co się stanie po zainstalowaniu pakietu](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), z następującymi dodatkami:</span><span class="sxs-lookup"><span data-stu-id="97377-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="97377-141">W konsoli są wyświetlani odpowiednich postanowieniach licencyjnych w jego oknie umowę domyślnych.</span><span class="sxs-lookup"><span data-stu-id="97377-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="97377-142">Jeśli nie akceptujesz postanowień, należy odinstalować pakiet natychmiast.</span><span class="sxs-lookup"><span data-stu-id="97377-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="97377-143">Również odwołanie do pakietu są dodawane do pliku projektu i pojawia się w **Eksploratora rozwiązań** w obszarze **odwołania** węzła, musisz zapisać projekt, aby wyświetlić zmiany w pliku projektu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="97377-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="97377-144">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="97377-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="97377-145">Zobacz [Odinstaluj pakiet](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="97377-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="97377-146">Użyj [Get-Package](../tools/ps-ref-get-package.md) aby zobaczyć wszystkie pakiety zainstalowane w projekcie domyślnym, aby znaleźć identyfikator.</span><span class="sxs-lookup"><span data-stu-id="97377-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="97377-147">Odinstalowywanie pakietu wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="97377-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="97377-148">Usuwa odwołania do pakietu z projektu (i jest używany format niezależnie od zarządzania).</span><span class="sxs-lookup"><span data-stu-id="97377-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="97377-149">Odwołania nie są widoczne w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="97377-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="97377-150">(Konieczne może być ponownie skompilować projekt, aby zobaczyć, usunąć je z **Bin** folderu.)</span><span class="sxs-lookup"><span data-stu-id="97377-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="97377-151">Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` Jeśli pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="97377-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="97377-152">Usuwa wcześniej zainstalowane zależności nie pozostałych pakietów użycie tych zależności.</span><span class="sxs-lookup"><span data-stu-id="97377-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="97377-153">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="97377-153">Updating a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="97377-154">Zobacz [Get-Package](../tools/ps-ref-get-package.md) i [pakietu aktualizacji](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="97377-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="97377-155">Znajdowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="97377-155">Finding a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="97377-156">Zobacz [Znajdź pakiet](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="97377-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="97377-157">W programie Visual Studio 2013 lub starszej użyj [Get-Package](../tools/ps-ref-get-package.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="97377-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="97377-158">Dostępność konsoli</span><span class="sxs-lookup"><span data-stu-id="97377-158">Availability of the console</span></span>

<span data-ttu-id="97377-159">W programie Visual Studio 2017 r. NuGet i Menedżer pakietów NuGet są instalowane automatycznie po wybraniu dowolnego. Obciążeń związanych z NET; można także zainstalować go indywidualnie sprawdzając **pojedynczych składników > Code Narzędzia > Menedżera pakietów NuGet** opcji w Instalatorze programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="97377-159">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="97377-160">Ponadto jeśli jest Brak Menedżera pakietów NuGet w programie Visual Studio 2015 i starszych wersji, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj rozszerzenie NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="97377-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="97377-161">Jeśli nie możesz użyć Instalatora rozszerzeń programu Visual Studio, możesz pobrać rozszerzenia bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="97377-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="97377-162">Konsola Menedżera pakietów nie jest obecnie dostępna w programie Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="97377-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="97377-163">Jednak równoważnych poleceń są dostępne za pośrednictwem [interfejsu wiersza polecenia NuGet](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="97377-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="97377-164">Visual Studio dla komputerów Mac mają interfejsu użytkownika do zarządzania pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="97377-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="97377-165">Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="97377-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="97377-166">Konsola Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="97377-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="97377-167">Rozszerzanie konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="97377-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="97377-168">Niektóre pakiety Zainstaluj nowe polecenia konsoli.</span><span class="sxs-lookup"><span data-stu-id="97377-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="97377-169">Na przykład `MvcScaffolding` tworzy poleceń, takich jak `Scaffold` pokazano poniżej, generująca, widoków i kontrolerów ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="97377-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Zainstalowanie i używanie MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="97377-171">Konfigurowanie profilu programu NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="97377-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="97377-172">Profil programu PowerShell pozwala udostępnić najczęściej używanych poleceń tam, gdzie należy użyć programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97377-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="97377-173">NuGet obsługuje profil specyficzne dla NuGet zwykle znajdują się w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="97377-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="97377-174">Aby znaleźć profil, wpisz `$profile` w konsoli:</span><span class="sxs-lookup"><span data-stu-id="97377-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="97377-175">Aby uzyskać więcej informacji, zapoznaj się [Windows PowerShell profile](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="97377-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="97377-176">Przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli programu</span><span class="sxs-lookup"><span data-stu-id="97377-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="97377-177">Aby [ `nuget.exe` CLI](nuget-exe-cli-reference.md) dostępne w konsoli Menedżera pakietów Zainstaluj [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pakietu w konsoli:</span><span class="sxs-lookup"><span data-stu-id="97377-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
