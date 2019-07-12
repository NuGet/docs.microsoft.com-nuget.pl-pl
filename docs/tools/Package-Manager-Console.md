---
title: Instalowanie i Zarządzaj pakietami NuGet za pomocą konsoli w programie Visual Studio
description: Instrukcje dotyczące korzystania z konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 91ab3859994e5ae738c6637219681ebbfc92d420
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842593"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="738f6-103">Instalowanie i zarządzanie pakietami za pomocą konsoli Menedżera pakietów w programie Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="738f6-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="738f6-104">Konsola Menedżera pakietów NuGet umożliwia korzystanie z [poleceń programu NuGet PowerShell](../tools/powershell-reference.md) można znaleźć, instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="738f6-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="738f6-105">Za pomocą konsoli jest konieczne w przypadku, gdy interfejs użytkownika Menedżera pakietów nie zapewnia sposób wykonania operacji.</span><span class="sxs-lookup"><span data-stu-id="738f6-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="738f6-106">Aby użyć `nuget.exe` poleceń interfejsu wiersza polecenia w konsoli, zobacz [przy użyciu nuget.exe interfejsu wiersza polecenia w konsoli](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="738f6-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="738f6-107">Konsoli jest wbudowana w programie Visual Studio na Windows.</span><span class="sxs-lookup"><span data-stu-id="738f6-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="738f6-108">Nie jest uwzględniona w programie Visual Studio for Mac lub Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="738f6-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="738f6-109">Znajdowanie i instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="738f6-109">Find and install a package</span></span>

<span data-ttu-id="738f6-110">Na przykład Znajdowanie i instalowanie pakietu jest przeprowadzane za pomocą trzech prostych krokach:</span><span class="sxs-lookup"><span data-stu-id="738f6-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="738f6-111">Otwórz projekt/rozwiązanie w programie Visual Studio i Otwórz za pomocą konsoli **Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="738f6-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="738f6-112">Znajdź pakiet, który chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="738f6-112">Find the package you want to install.</span></span> <span data-ttu-id="738f6-113">Jeśli znasz już to, przejdź do kroku 3.</span><span class="sxs-lookup"><span data-stu-id="738f6-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="738f6-114">Uruchom polecenia instalacji:</span><span class="sxs-lookup"><span data-stu-id="738f6-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="738f6-115">Można również wykonać wszystkie operacje, które są dostępne w konsoli za pomocą [interfejs wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="738f6-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="738f6-116">Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisany projekt/rozwiązanie i często osiągnąć bardziej niż ich równoważne poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="738f6-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="738f6-117">Na przykład instalowanie pakietu za pomocą konsoli dodaje odwołanie do projektu, natomiast nie obsługuje polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="738f6-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="738f6-118">Z tego powodu deweloperzy pracujący w programie Visual Studio zazwyczaj preferują przy użyciu konsoli dla interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="738f6-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="738f6-119">Wiele operacji konsoli zależą od tego, rozwiązanie otwarte w programie Visual Studio o nazwie znanej ścieżce.</span><span class="sxs-lookup"><span data-stu-id="738f6-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="738f6-120">Jeśli masz niezapisane rozwiązanie lub żadne rozwiązanie nie zostanie wyświetlony błąd, "rozwiązania nie otwarcie lub nie zostały zapisane.</span><span class="sxs-lookup"><span data-stu-id="738f6-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="738f6-121">Upewnij się, że masz rozwiązanie otwarty i zapisany."</span><span class="sxs-lookup"><span data-stu-id="738f6-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="738f6-122">Oznacza to, że konsoli nie można ustalić folderu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="738f6-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="738f6-123">Zapisywanie niezapisane rozwiązanie lub tworzenie i zapisywanie rozwiązania, jeśli nie masz otwarte, należy rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="738f6-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="738f6-124">Otwieranie konsoli i formanty konsoli</span><span class="sxs-lookup"><span data-stu-id="738f6-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="738f6-125">Otwórz konsolę programu Visual Studio przy użyciu **Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów** polecenia.</span><span class="sxs-lookup"><span data-stu-id="738f6-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="738f6-126">Konsola jest okno programu Visual Studio, które mogą być ułożone umieszczony w dowolny sposób (zobacz [dostosowywanie układów okien w programie Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="738f6-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="738f6-127">Domyślnie polecenia konsoli działają względem źródła określonego pakietu i projektu jako zestawu w formancie w górnej części okna:</span><span class="sxs-lookup"><span data-stu-id="738f6-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Formanty Konsola Menedżera pakietów dla projektów i źródła pakietu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="738f6-129">Wybór źródła pakietu inny projekt i/lub zmienia te ustawienia domyślne używane przy kolejnych poleceniach.</span><span class="sxs-lookup"><span data-stu-id="738f6-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="738f6-130">Aby overrride tych ustawień bez zmiany ustawień domyślnych, większość używanych poleceń obsługiwać `-Source` i `-ProjectName` opcje.</span><span class="sxs-lookup"><span data-stu-id="738f6-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="738f6-131">Aby zarządzać źródła pakietu, wybierz ikonę koła zębatego.</span><span class="sxs-lookup"><span data-stu-id="738f6-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="738f6-132">Jest to skrót do **Narzędzia > Opcje > Menedżer pakietów NuGet > źródeł pakietów** okno dialogowe, zgodnie z opisem na [interfejs użytkownika Menedżera pakietów](package-manager-ui.md#package-sources) strony.</span><span class="sxs-lookup"><span data-stu-id="738f6-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="738f6-133">Ponadto kontrolka selektora projektów po prawej stronie Czyści zawartość konsoli programu:</span><span class="sxs-lookup"><span data-stu-id="738f6-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Ustawienia konsoli Menedżera pakietów i wyczyść formantów](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="738f6-135">Po prawej stronie przycisku przerywa działanie polecenia długoterminowych.</span><span class="sxs-lookup"><span data-stu-id="738f6-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="738f6-136">Aby na przykład uruchomić `Get-Package -ListAvailable -PageSize 500` zawiera listę pakietów pierwszych 500 na domyślnego źródła (np. nuget.org), który może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="738f6-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Kontrolka stop Konsola Menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="738f6-138">Instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="738f6-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="738f6-139">Zobacz [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="738f6-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="738f6-140">Instalowanie pakietu w konsoli wykonuje te same czynności, zgodnie z opisem na [co się dzieje po zainstalowaniu pakietu](../concepts/package-installation-process.md), z następującymi dodatkami:</span><span class="sxs-lookup"><span data-stu-id="738f6-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="738f6-141">Konsoli są wyświetlane w odpowiednich postanowieniach licencyjnych w jego oknie dorozumianych umowy.</span><span class="sxs-lookup"><span data-stu-id="738f6-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="738f6-142">Jeśli nie akceptujesz postanowień, należy odinstalować pakiet natychmiast.</span><span class="sxs-lookup"><span data-stu-id="738f6-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="738f6-143">Również odwołanie do pakietu są dodawane do pliku projektu i pojawia się w **Eksploratora rozwiązań** w obszarze **odwołania** węzła, musisz zapisać projekt, aby zobaczyć zmiany w pliku projektu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="738f6-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="738f6-144">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="738f6-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="738f6-145">Zobacz [Odinstaluj pakiet](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="738f6-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="738f6-146">Użyj [Get-Package](../tools/ps-ref-get-package.md) aby zobaczyć wszystkie pakiety, które obecnie zainstalowana na projekt domyślny, jeśli chcesz znaleźć identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="738f6-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="738f6-147">Odinstalowywanie pakietu wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="738f6-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="738f6-148">Usuwa odwołania do pakietu z projektu (i jest używany format niezależnie od zarządzania).</span><span class="sxs-lookup"><span data-stu-id="738f6-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="738f6-149">Odwołania nie są wyświetlane w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="738f6-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="738f6-150">(Może być konieczne ponownie skompiluj projekt, aby zobaczyć, że usuwane z **Bin** folderu.)</span><span class="sxs-lookup"><span data-stu-id="738f6-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="738f6-151">Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` gdy pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="738f6-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="738f6-152">Zależności usuwa wcześniej zainstalowane nie pozostałe pakiety użycia tych zależności.</span><span class="sxs-lookup"><span data-stu-id="738f6-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="738f6-153">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="738f6-153">Updating a package</span></span>

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

<span data-ttu-id="738f6-154">Zobacz [Get-Package](../tools/ps-ref-get-package.md) i [pakiet aktualizacji](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="738f6-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="738f6-155">Znajdowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="738f6-155">Finding a package</span></span>

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

<span data-ttu-id="738f6-156">Zobacz [Znajdź pakiet](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="738f6-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="738f6-157">W programie Visual Studio 2013 i starszych, użyj [Get-Package](../tools/ps-ref-get-package.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="738f6-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="738f6-158">Dostępność w konsoli programu</span><span class="sxs-lookup"><span data-stu-id="738f6-158">Availability of the console</span></span>

<span data-ttu-id="738f6-159">Począwszy od programu Visual Studio 2017, Menedżer pakietów NuGet i NuGet są automatycznie instalowane po zaznaczeniu innego. Obciążenia związane z NET; można także zainstalować je oddzielnie, sprawdzając **poszczególne składniki > Kod Narzędzia > Menedżer pakietów NuGet** opcji w Instalatorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="738f6-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="738f6-160">Ponadto jeśli masz Brak Menedżera pakietów NuGet w programie Visual Studio 2015 i starszych, sprawdź **Narzędzia > rozszerzenia i aktualizacje...**  i wyszukaj rozszerzenia Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="738f6-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="738f6-161">Jeśli nie możesz używać Instalator rozszerzenia programu Visual Studio, możesz pobrać rozszerzenia bezpośrednio z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="738f6-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="738f6-162">Konsola Menedżera pakietów nie jest obecnie dostępne w programie Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="738f6-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="738f6-163">Równoważne polecenia są jednak dostępne za pośrednictwem [interfejs wiersza polecenia NuGet](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="738f6-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="738f6-164">Program Visual Studio for Mac ma interfejs użytkownika zarządzania pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="738f6-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="738f6-165">Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="738f6-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="738f6-166">Konsola Menedżera pakietów nie jest uwzględniona w programie Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="738f6-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="738f6-167">Rozszerzanie Konsola Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="738f6-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="738f6-168">Niektóre pakiety instalują nowe polecenia do konsoli.</span><span class="sxs-lookup"><span data-stu-id="738f6-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="738f6-169">Na przykład `MvcScaffolding` tworzy poleceń, takich jak `Scaffold` pokazano poniżej, które mają widoków i kontrolerów platformy ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="738f6-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Zainstalowanie i używanie MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="738f6-171">Konfigurowanie profilu NuGet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="738f6-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="738f6-172">Profil programu PowerShell umożliwia udostępnianie często używanych poleceń w dowolnym miejscu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="738f6-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="738f6-173">NuGet obsługuje profilu specyficzne dla NuGet, zwykle znajdują się w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="738f6-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="738f6-174">Aby znaleźć profilu, wpisz `$profile` w konsoli:</span><span class="sxs-lookup"><span data-stu-id="738f6-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="738f6-175">Aby uzyskać więcej informacji, zapoznaj się [programu Windows PowerShell profile](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="738f6-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="738f6-176">Za pomocą nuget.exe interfejsu wiersza polecenia w konsoli programu</span><span class="sxs-lookup"><span data-stu-id="738f6-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="738f6-177">Zapewnienie [ `nuget.exe` interfejsu wiersza polecenia](nuget-exe-cli-reference.md) dostępne w konsoli Menedżera pakietów Zainstaluj [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pakietu z poziomu konsoli:</span><span class="sxs-lookup"><span data-stu-id="738f6-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
