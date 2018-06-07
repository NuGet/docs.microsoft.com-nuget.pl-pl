---
title: Przewodnik konsoli Menedżera pakietów NuGet
description: Instrukcje dotyczące używania konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 06c525cab2dac61c92c4596533173f1d93493d9a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817661"
---
# <a name="package-manager-console"></a><span data-ttu-id="5f6b1-103">Konsola Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="5f6b1-103">Package Manager Console</span></span>

<span data-ttu-id="5f6b1-104">Konsola Menedżera pakietów NuGet jest wbudowany w program Visual Studio w systemie Windows w wersji 2012 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="5f6b1-105">(Nie jest dołączony do programu Visual Studio for Mac lub Visual Studio Code.)</span><span class="sxs-lookup"><span data-stu-id="5f6b1-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="5f6b1-106">Konsolę pozwala używać [poleceń programu NuGet PowerShell](../tools/powershell-reference.md) można znaleźć, instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="5f6b1-107">Za pomocą konsoli jest niezbędne w przypadku, gdy interfejsu użytkownika Menedżera pakietów nie umożliwiają wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="5f6b1-108">Aby użyć `nuget.exe` poleceń w konsoli, zobacz [przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="5f6b1-109">Na przykład Znajdowanie i instalowanie pakietu wykonuje się za pomocą trzy łatwe kroki:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="5f6b1-110">Otwórz projekt/rozwiązanie w programie Visual Studio, a następnie otwórz za pomocą konsoli **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="5f6b1-111">Znajdź pakiet, który chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-111">Find the package you want to install.</span></span> <span data-ttu-id="5f6b1-112">Jeśli znasz już to, przejdź do kroku 3.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="5f6b1-113">Uruchom polecenie instalacji:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="5f6b1-114">Można również wykonać wszystkie operacje, które są dostępne w konsoli za pomocą [interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="5f6b1-115">Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisane projektu/rozwiązania i często osiągnąć więcej niż ich równoważnych poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="5f6b1-116">Na przykład instalowania pakietu w konsoli dodaje odwołanie do projektu, natomiast polecenia interfejsu wiersza polecenia nie.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="5f6b1-117">Z tego powodu deweloperów pracujących w programie Visual Studio zwykle preferowane przy użyciu konsoli do interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="5f6b1-118">Wiele operacji konsoli zależą od tego, o rozwiązania otwarte w programie Visual Studio o nazwie znanej ścieżce.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="5f6b1-119">Jeśli masz niezapisane rozwiązanie lub żadne rozwiązanie, zostanie wyświetlony błąd, "nie jest otwarty lub nie zapisano rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="5f6b1-120">Upewnij się, że masz otwarte i zapisane rozwiązanie."</span><span class="sxs-lookup"><span data-stu-id="5f6b1-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="5f6b1-121">Oznacza to, że konsola nie może określić folder rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="5f6b1-122">Zapisywanie niezapisane rozwiązanie lub tworzenie i zapisywanie rozwiązanie, jeśli nie masz open, należy rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="5f6b1-123">Otwieranie konsoli i formanty konsoli</span><span class="sxs-lookup"><span data-stu-id="5f6b1-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="5f6b1-124">Otwórz program Visual Studio przy użyciu **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="5f6b1-125">Konsoli jest oknem programu Visual Studio, które mogą być rozmieszczane i znajduje się jednak chcesz (zobacz [dostosowywanie układów okien w programie Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="5f6b1-126">Domyślnie polecenia konsoli działają z określonego pakietu źródłowego i projektu jako zestaw w formancie w górnej części okna:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Formanty Konsola Menedżera pakietów dla projektów i źródła pakietu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="5f6b1-128">Wybieranie źródła różnych pakietów i/lub projektu zmiany tych wartości domyślnych dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="5f6b1-129">Aby overrride tych ustawień bez zmiany ustawień domyślnych, większość używanych poleceń obsługiwać `-Source` i `-ProjectName` opcje.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="5f6b1-130">Aby zarządzać źródła pakietów, wybierz ikonę Koło zębate.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="5f6b1-131">Jest to skrót do **Narzędzia > Opcje > Menedżera pakietów NuGet > źródła pakietów** okno dialogowe zgodnie z opisem na [interfejsu użytkownika Menedżera pakietów](package-manager-ui.md#package-sources) strony.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="5f6b1-132">Ponadto kontrolka selektora projektu z prawej strony Czyści zawartość konsoli programu:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Ustawienia konsoli Menedżera pakietów i usuń zaznaczenie formantów](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="5f6b1-134">Po prawej stronie przycisku przerwań polecenia długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="5f6b1-135">Na przykład uruchomiona `Get-Package -ListAvailable -PageSize 500` listy pierwszych 500 pakietów na domyślne źródło (na przykład nuget.org), co może zająć kilka minut do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Formant stop Konsola Menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="5f6b1-137">Instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="5f6b1-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="5f6b1-138">Zobacz [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="5f6b1-139">Instalowanie pakietu w konsoli wykonuje te same kroki, zgodnie z opisem na [co się stanie po zainstalowaniu pakietu](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), z następującymi dodatkami:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="5f6b1-140">W konsoli są wyświetlani odpowiednich postanowieniach licencyjnych w jego oknie umowę domyślnych.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="5f6b1-141">Jeśli nie akceptujesz postanowień, należy odinstalować pakiet natychmiast.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="5f6b1-142">Również odwołanie do pakietu są dodawane do pliku projektu i pojawia się w **Eksploratora rozwiązań** w obszarze **odwołania** węzła, musisz zapisać projekt, aby wyświetlić zmiany w pliku projektu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="5f6b1-143">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="5f6b1-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="5f6b1-144">Zobacz [Odinstaluj pakiet](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="5f6b1-145">Użyj [Get-Package](../tools/ps-ref-get-package.md) aby zobaczyć wszystkie pakiety zainstalowane w projekcie domyślnym, aby znaleźć identyfikator.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="5f6b1-146">Odinstalowywanie pakietu wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="5f6b1-147">Usuwa odwołania do pakietu z projektu (i jest używany format niezależnie od zarządzania).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="5f6b1-148">Odwołania nie są widoczne w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="5f6b1-149">(Konieczne może być ponownie skompilować projekt, aby zobaczyć, usunąć je z **Bin** folderu.)</span><span class="sxs-lookup"><span data-stu-id="5f6b1-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="5f6b1-150">Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` Jeśli pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="5f6b1-151">Usuwa wcześniej zainstalowane zależności nie pozostałych pakietów użycie tych zależności.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="5f6b1-152">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="5f6b1-152">Updating a package</span></span>

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

<span data-ttu-id="5f6b1-153">Zobacz [Get-Package](../tools/ps-ref-get-package.md) i [pakietu aktualizacji](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="5f6b1-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="5f6b1-154">Znajdowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="5f6b1-154">Finding a package</span></span>

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

<span data-ttu-id="5f6b1-155">Zobacz [Znajdź pakiet](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="5f6b1-156">W programie Visual Studio 2013 lub starszej użyj [Get-Package](../tools/ps-ref-get-package.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="5f6b1-157">Dostępność konsoli</span><span class="sxs-lookup"><span data-stu-id="5f6b1-157">Availability of the console</span></span>

<span data-ttu-id="5f6b1-158">W programie Visual Studio 2017 r. NuGet i Menedżer pakietów NuGet są instalowane automatycznie po wybraniu dowolnego. Obciążeń związanych z NET; można także zainstalować go indywidualnie sprawdzając **pojedynczych składników > Code Narzędzia > Menedżera pakietów NuGet** opcji w Instalatorze programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="5f6b1-159">Ponadto jeśli jest Brak Menedżera pakietów NuGet w programie Visual Studio 2015 i starszych wersji, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj rozszerzenie NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="5f6b1-160">Jeśli nie możesz użyć Instalatora rozszerzeń programu Visual Studio, możesz pobrać rozszerzenia bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="5f6b1-161">Konsola Menedżera pakietów nie jest obecnie dostępna w programie Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="5f6b1-162">Jednak równoważnych poleceń są dostępne za pośrednictwem [interfejsu wiersza polecenia NuGet](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="5f6b1-163">Visual Studio dla komputerów Mac mają interfejsu użytkownika do zarządzania pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="5f6b1-164">Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="5f6b1-165">Konsola Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="5f6b1-166">Rozszerzanie konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="5f6b1-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="5f6b1-167">Niektóre pakiety Zainstaluj nowe polecenia konsoli.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="5f6b1-168">Na przykład `MvcScaffolding` tworzy poleceń, takich jak `Scaffold` pokazano poniżej, generująca, widoków i kontrolerów ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Zainstalowanie i używanie MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="5f6b1-170">Konfigurowanie profilu programu NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f6b1-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="5f6b1-171">Profil programu PowerShell pozwala udostępnić najczęściej używanych poleceń tam, gdzie należy użyć programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f6b1-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="5f6b1-172">NuGet obsługuje profil specyficzne dla NuGet zwykle znajdują się w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="5f6b1-173">Aby znaleźć profil, wpisz `$profile` w konsoli:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="5f6b1-174">Aby uzyskać więcej informacji, zapoznaj się [Windows PowerShell profile](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f6b1-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="5f6b1-175">Przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli programu</span><span class="sxs-lookup"><span data-stu-id="5f6b1-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="5f6b1-176">Aby [ `nuget.exe` CLI](nuget-exe-cli-reference.md) dostępne w konsoli Menedżera pakietów Zainstaluj [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pakietu w konsoli:</span><span class="sxs-lookup"><span data-stu-id="5f6b1-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
