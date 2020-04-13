---
title: Instalowanie pakietów NuGet przy użyciu konsoli przy użyciu konsoli i zarządzanie nimi
description: Instrukcje dotyczące korzystania z konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428955"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="7bdd3-103">Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów w programie Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7bdd3-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="7bdd3-104">Konsola Menedżera pakietów NuGet umożliwia znajdowanie, instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet za pomocą [poleceń NuGet PowerShell.](../reference/powershell-reference.md)</span><span class="sxs-lookup"><span data-stu-id="7bdd3-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="7bdd3-105">Korzystanie z konsoli jest konieczne w przypadkach, gdy interfejs użytkownika Menedżera pakietów nie zapewnia sposobu wykonania operacji.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="7bdd3-106">Aby `nuget.exe` użyć poleceń interfejsu wiersza polecenia w konsoli, zobacz [Korzystanie z interfejsu wiersza polecenia nuget.exe w konsoli](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="7bdd3-107">Konsola jest wbudowana w program Visual Studio w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="7bdd3-108">Nie jest dołączony do programu Visual Studio dla komputerów Mac lub Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="7bdd3-109">Znajdowanie i instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="7bdd3-109">Find and install a package</span></span>

<span data-ttu-id="7bdd3-110">Na przykład znalezienie i zainstalowanie pakietu odbywa się za pomocą trzech prostych kroków:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="7bdd3-111">Otwórz projekt/rozwiązanie w programie Visual Studio i otwórz konsolę za pomocą polecenia **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów.**</span><span class="sxs-lookup"><span data-stu-id="7bdd3-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="7bdd3-112">Znajdź pakiet, który chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-112">Find the package you want to install.</span></span> <span data-ttu-id="7bdd3-113">Jeśli już to wiesz, przejdź do kroku 3.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="7bdd3-114">Uruchom polecenie instalacji:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="7bdd3-115">Wszystkie operacje, które są dostępne w konsoli można również wykonać za pomocą [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="7bdd3-116">Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisanego projektu/rozwiązania i często osiągają więcej niż ich równoważne polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="7bdd3-117">Na przykład zainstalowanie pakietu za pośrednictwem konsoli dodaje odwołanie do projektu, podczas gdy polecenie CLI nie.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="7bdd3-118">Z tego powodu deweloperzy pracujący w programie Visual Studio zazwyczaj wolą używać konsoli do interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="7bdd3-119">Wiele operacji konsoli zależy od konieczności rozwiązania otwartego w programie Visual Studio o znanej nazwie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="7bdd3-120">Jeśli masz niezapisane rozwiązanie lub nie ma rozwiązania, możesz zobaczyć błąd " Rozwiązanie nie jest otwarte lub nie zapisane.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="7bdd3-121">Upewnij się, że masz otwarte i zapisane rozwiązanie."</span><span class="sxs-lookup"><span data-stu-id="7bdd3-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="7bdd3-122">Oznacza to, że konsola nie może określić folderu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="7bdd3-123">Zapisanie niezapisanego rozwiązania lub utworzenie i zapisanie rozwiązania, jeśli nie masz otwartego rozwiązania, powinno poprawić błąd.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="7bdd3-124">Otwieranie elementów sterujących konsoli i konsoli</span><span class="sxs-lookup"><span data-stu-id="7bdd3-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="7bdd3-125">Otwórz konsolę w programie Visual Studio za pomocą polecenia **Narzędzia > Menedżer pakietów NuGet > konsoli Menedżera pakietów.**</span><span class="sxs-lookup"><span data-stu-id="7bdd3-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="7bdd3-126">Konsola jest oknem programu Visual Studio, które można rozmieszczać i pozycjonować w jak sposób (zobacz [Dostosowywanie układów okien w programie Visual Studio).](/visualstudio/ide/customizing-window-layouts-in-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="7bdd3-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="7bdd3-127">Domyślnie polecenia konsoli działają względem określonego źródła pakietu i projektu zgodnie z ustawieniem w formancie w górnej części okna:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Formanty konsoli Menedżera pakietów dla źródła i projektu pakietu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="7bdd3-129">Wybranie innego źródła pakietu i/lub projektu powoduje zmianę tych wartości domyślnych dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="7bdd3-130">Aby przecenić te ustawienia bez zmiany ustawień `-Source` `-ProjectName` domyślnych, większość poleceń obsługuje i opcje.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="7bdd3-131">Aby zarządzać źródłami pakietów, wybierz ikonę koła zębatego.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="7bdd3-132">Jest to skrót do **narzędzia > opcje > NuGet Package Manager > źródła pakietów,** jak opisano na stronie interfejsu użytkownika Menedżera [pakietów.](install-use-packages-visual-studio.md#package-sources)</span><span class="sxs-lookup"><span data-stu-id="7bdd3-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="7bdd3-133">Ponadto kontrolka po prawej stronie selektora projektu czyści zawartość konsoli:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Ustawienia konsoli Menedżera pakietów i wyczyść kontrolki](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="7bdd3-135">Przycisk po prawej stronie przerywa długotrwałe polecenie.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="7bdd3-136">Na przykład `Get-Package -ListAvailable -PageSize 500` uruchomione wyświetla listę 500 najlepszych pakietów w źródle domyślnym (na przykład nuget.org), co może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Kontrola zatrzymania konsoli menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="7bdd3-138">Instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="7bdd3-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="7bdd3-139">Zobacz [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="7bdd3-140">Instalowanie pakietu w konsoli wykonuje te same kroki, co opisano w [sprawie Co się dzieje, gdy pakiet jest zainstalowany,](../concepts/package-installation-process.md)z następującymi dodatkami:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="7bdd3-141">Konsola wyświetla odpowiednie postanowienia licencyjne w swoim oknie z dorozumianą umową.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="7bdd3-142">Jeśli nie zgadzasz się na warunki, powinieneś natychmiast odinstalować pakiet.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="7bdd3-143">Również odwołanie do pakietu jest dodawany do pliku projektu i pojawia się w **Eksploratorze rozwiązań** w **węźle Odwołania,** należy zapisać projekt, aby zobaczyć zmiany w pliku projektu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="7bdd3-144">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="7bdd3-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="7bdd3-145">Zobacz [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="7bdd3-146">Użyj [Get-Package,](../reference/ps-reference/ps-ref-get-package.md) aby wyświetlić wszystkie pakiety aktualnie zainstalowane w projekcie domyślnym, jeśli trzeba znaleźć identyfikator.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="7bdd3-147">Odinstalowanie pakietu wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="7bdd3-148">Usuwa odwołania do pakietu z projektu (i niezależnie od formatu zarządzania jest w użyciu).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="7bdd3-149">Odwołania nie są już wyświetlane w **Eksploratorze rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="7bdd3-150">(Może być konieczne odbudowycie projektu, aby został usunięty z folderu **Bin).**</span><span class="sxs-lookup"><span data-stu-id="7bdd3-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="7bdd3-151">Odwraca wszelkie zmiany `app.config` wprowadzone `web.config` do lub gdy pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="7bdd3-152">Usuwa wcześniej zainstalowane zależności, jeśli żadne pozostałe pakiety nie używają tych zależności.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="7bdd3-153">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="7bdd3-153">Update a package</span></span>

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

<span data-ttu-id="7bdd3-154">Zobacz [Get-Package](../reference/ps-reference/ps-ref-get-package.md) i [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="7bdd3-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="7bdd3-155">Znajdź pakiet</span><span class="sxs-lookup"><span data-stu-id="7bdd3-155">Find a package</span></span>

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

<span data-ttu-id="7bdd3-156">Zobacz [Znajdź pakiet](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="7bdd3-157">W programie Visual Studio 2013 i wcześniejszych należy użyć [get-package](../reference/ps-reference/ps-ref-get-package.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="7bdd3-158">Dostępność konsoli</span><span class="sxs-lookup"><span data-stu-id="7bdd3-158">Availability of the console</span></span>

<span data-ttu-id="7bdd3-159">Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są instalowane automatycznie po wybraniu dowolnego . Obciążenia związane z siecią net; można również zainstalować go indywidualnie, sprawdzając poszczególne składniki > Narzędzia kodu > menedżer **pakietów NuGet** w instalatorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="7bdd3-160">Ponadto jeśli brakuje Menedżera pakietów NuGet w programie Visual Studio 2015 i wcześniejszych, sprawdź **Narzędzia > rozszerzenia i aktualizacje...** i wyszukaj rozszerzenie Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="7bdd3-161">Jeśli nie możesz użyć instalatora rozszerzeń w programie Visual Studio, [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)możesz pobrać je bezpośrednio z programu .</span><span class="sxs-lookup"><span data-stu-id="7bdd3-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="7bdd3-162">Konsola Menedżera pakietów nie jest obecnie dostępna w programie Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="7bdd3-163">Równoważne polecenia są jednak dostępne za pośrednictwem [interfejsu wiersza polecenia NuGet.](../reference/nuget-exe-CLI-reference.md)</span><span class="sxs-lookup"><span data-stu-id="7bdd3-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="7bdd3-164">Visual Studio dla komputerów Mac ma interfejs użytkownika do zarządzania pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="7bdd3-165">Zobacz [Dołączanie pakietu NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="7bdd3-166">Konsola Menedżera pakietów nie jest dołączona do programu Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="7bdd3-167">Rozszerzanie konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="7bdd3-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="7bdd3-168">Niektóre pakiety instalują nowe polecenia dla konsoli.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="7bdd3-169">Na przykład `MvcScaffolding` tworzy polecenia, takie jak `Scaffold` pokazano poniżej, który generuje ASP.NET kontrolerów MVC i widoków:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalacja i używanie rusztowania MvcS](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="7bdd3-171">Konfigurowanie profilu programu NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bdd3-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="7bdd3-172">Profil programu PowerShell umożliwia udostępnianie często używanych poleceń wszędzie tam, gdzie jest używany program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7bdd3-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="7bdd3-173">NuGet obsługuje profil specyficzne dla NuGet zazwyczaj znajduje się w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="7bdd3-174">Aby znaleźć profil, `$profile` wpisz w konsoli:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="7bdd3-175">Aby uzyskać więcej informacji, zobacz [Profile programu Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="7bdd3-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="7bdd3-176">Użyj interfejsu wiersza polecenia nuget.exe w konsoli</span><span class="sxs-lookup"><span data-stu-id="7bdd3-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="7bdd3-177">Aby udostępnić [ `nuget.exe` wiersz polecenia](../reference/nuget-exe-cli-reference.md) w konsoli Menedżera pakietów, zainstaluj pakiet [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) z konsoli:</span><span class="sxs-lookup"><span data-stu-id="7bdd3-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
