---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu konsoli programu Visual Studio
description: Instrukcje dotyczące korzystania z konsoli Menedżera pakietów NuGet w programie Visual Studio do pracy z pakietami.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 1fb12c6cb9f7702c05990f79a6d43b9dd739e8cc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328424"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="c26be-103">Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów w programie Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c26be-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="c26be-104">Konsola Menedżera pakietów NuGet umożliwia używanie [poleceń programu PowerShell NuGet](../reference/powershell-reference.md) do znajdowania, instalowania, odinstalowywania i aktualizowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="c26be-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="c26be-105">Korzystanie z konsoli programu jest niezbędne w przypadkach, gdy interfejs użytkownika Menedżera pakietów nie zapewnia sposobu wykonywania operacji.</span><span class="sxs-lookup"><span data-stu-id="c26be-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="c26be-106">Aby użyć `nuget.exe` poleceń interfejsu wiersza polecenia w konsoli programu, zobacz [using the NuGet. exe CLI w konsoli programu](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="c26be-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="c26be-107">Konsola programu jest wbudowana w program Visual Studio w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="c26be-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="c26be-108">Nie jest on dołączony do Visual Studio dla komputerów Mac ani Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c26be-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="c26be-109">Znajdowanie i instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c26be-109">Find and install a package</span></span>

<span data-ttu-id="c26be-110">Na przykład wyszukiwanie i instalowanie pakietu odbywa się z trzema prostymi krokami:</span><span class="sxs-lookup"><span data-stu-id="c26be-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="c26be-111">Otwórz projekt/rozwiązanie w programie Visual Studio i Otwórz konsolę przy użyciu **narzędzi > Menedżer pakietów NuGet > polecenie konsoli Menedżera pakietów** .</span><span class="sxs-lookup"><span data-stu-id="c26be-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="c26be-112">Znajdź pakiet, który chcesz zainstalować.</span><span class="sxs-lookup"><span data-stu-id="c26be-112">Find the package you want to install.</span></span> <span data-ttu-id="c26be-113">Jeśli już wiesz, przejdź do kroku 3.</span><span class="sxs-lookup"><span data-stu-id="c26be-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="c26be-114">Uruchom polecenie instalacji:</span><span class="sxs-lookup"><span data-stu-id="c26be-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="c26be-115">Wszystkie operacje, które są dostępne w konsoli programu, można również wykonać przy użyciu [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c26be-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="c26be-116">Jednak polecenia konsoli działają w kontekście programu Visual Studio i zapisanego projektu/rozwiązania i często wykonują więcej niż odpowiadające im polecenia interfejsu CLI.</span><span class="sxs-lookup"><span data-stu-id="c26be-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="c26be-117">Na przykład zainstalowanie pakietu za pomocą konsoli programu dodaje odwołanie do projektu, podczas gdy polecenie interfejsu wiersza polecenia nie jest.</span><span class="sxs-lookup"><span data-stu-id="c26be-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="c26be-118">Z tego powodu deweloperzy pracujący w programie Visual Studio zwykle preferują korzystanie z konsoli programu z interfejsem wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c26be-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="c26be-119">Wiele operacji konsoli jest zależne od tego, czy rozwiązanie zostało otwarte w programie Visual Studio o znanej nazwie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c26be-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="c26be-120">Jeśli masz niezapisane rozwiązanie lub nie masz rozwiązania, zobaczysz błąd, "rozwiązanie nie jest otwarte lub nie zostało zapisane.</span><span class="sxs-lookup"><span data-stu-id="c26be-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="c26be-121">Upewnij się, że masz otwarte i zapisane rozwiązanie ".</span><span class="sxs-lookup"><span data-stu-id="c26be-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="c26be-122">Oznacza to, że konsola nie może określić folderu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c26be-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="c26be-123">Podczas zapisywania niezapisanego rozwiązania lub tworzenia i zapisywania rozwiązania, jeśli nie masz otwartego, należy usunąć ten błąd.</span><span class="sxs-lookup"><span data-stu-id="c26be-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="c26be-124">Otwieranie konsoli programu i kontrolek konsoli</span><span class="sxs-lookup"><span data-stu-id="c26be-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="c26be-125">Otwórz konsolę programu Visual Studio przy użyciu **narzędzi > Menedżer pakietów NuGet > polecenie konsoli Menedżera pakietów** .</span><span class="sxs-lookup"><span data-stu-id="c26be-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="c26be-126">Konsola programu jest oknem programu Visual Studio, które można odpowiednio rozmieścić i umieścić (zobacz [Dostosowywanie układów okien w programie Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="c26be-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="c26be-127">Domyślnie polecenia konsoli działają względem określonego źródła pakietu i projektu ustawionego w kontrolce w górnej części okna:</span><span class="sxs-lookup"><span data-stu-id="c26be-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Formanty konsoli Menedżera pakietów dla źródła i projektu pakietu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="c26be-129">Wybranie innego źródła pakietu i/lub projektu powoduje zmianę ustawień domyślnych dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="c26be-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="c26be-130">Aby overrride te ustawienia bez zmiany wartości domyślnych, większość poleceń obsługuje `-Source` i `-ProjectName` opcje.</span><span class="sxs-lookup"><span data-stu-id="c26be-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="c26be-131">Aby zarządzać źródłami pakietów, wybierz ikonę koła zębatego.</span><span class="sxs-lookup"><span data-stu-id="c26be-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="c26be-132">Jest to skrót do **narzędzi > opcje > Menedżer pakietów NuGet > źródłami pakietów** , zgodnie z opisem na stronie [interfejsu użytkownika Menedżera pakietów](install-use-packages-visual-studio.md#package-sources) .</span><span class="sxs-lookup"><span data-stu-id="c26be-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="c26be-133">Ponadto kontrolka z prawej strony selektora projektu czyści zawartość konsoli:</span><span class="sxs-lookup"><span data-stu-id="c26be-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Ustawienia konsoli Menedżera pakietów i wyczyść kontrolki](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="c26be-135">Prawy przycisk przerywa wykonywanie długotrwałych poleceń.</span><span class="sxs-lookup"><span data-stu-id="c26be-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="c26be-136">Na przykład uruchomienie `Get-Package -ListAvailable -PageSize 500` programu wyświetla listę najważniejszych pakietów 500 dla domyślnego źródła (na przykład NuGet.org), co może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c26be-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Sterowanie zatrzymaniem konsoli Menedżera pakietów](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="c26be-138">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="c26be-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="c26be-139">Zobacz [install-package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="c26be-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="c26be-140">Zainstalowanie pakietu w konsoli programu wykonuje te same czynności, co opisane w temacie [co się stanie w przypadku zainstalowania pakietu](../concepts/package-installation-process.md), z następującymi dodatkami:</span><span class="sxs-lookup"><span data-stu-id="c26be-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="c26be-141">W oknie konsoli zostaną wyświetlone odpowiednie postanowienia licencyjne.</span><span class="sxs-lookup"><span data-stu-id="c26be-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="c26be-142">Jeśli nie akceptujesz warunków, należy odinstalować pakiet natychmiast.</span><span class="sxs-lookup"><span data-stu-id="c26be-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="c26be-143">Odwołanie do pakietu jest również dodawane do pliku projektu i pojawia się w **Eksplorator rozwiązań** w węźle **odwołania** , należy zapisać projekt, aby wyświetlić zmiany w pliku projektu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c26be-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="c26be-144">Odinstalowywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c26be-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="c26be-145">Zobacz [odinstalowywanie pakietu](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="c26be-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="c26be-146">Użyj [Get-Package](../reference/ps-reference/ps-ref-get-package.md) , aby zobaczyć wszystkie pakiety aktualnie zainstalowane w domyślnym projekcie, jeśli trzeba znaleźć identyfikator.</span><span class="sxs-lookup"><span data-stu-id="c26be-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="c26be-147">Odinstalowywanie pakietu wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c26be-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="c26be-148">Usuwa odwołania do pakietu z projektu (wraz z dowolnym formatem zarządzania jest używany).</span><span class="sxs-lookup"><span data-stu-id="c26be-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="c26be-149">Odwołania nie są już wyświetlane w **Eksplorator rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="c26be-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="c26be-150">(Może być konieczne ponowne skompilowanie projektu, aby zobaczyć, że został usunięty z folderu **bin** ).</span><span class="sxs-lookup"><span data-stu-id="c26be-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="c26be-151">Odwraca wszelkie zmiany wprowadzone do `app.config` lub `web.config` podczas instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="c26be-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="c26be-152">Usuwa wcześniej zainstalowane zależności, jeśli żadne pozostałe pakiety nie używają tych zależności.</span><span class="sxs-lookup"><span data-stu-id="c26be-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="c26be-153">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c26be-153">Update a package</span></span>

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

<span data-ttu-id="c26be-154">Zobacz [Get-Package](../reference/ps-reference/ps-ref-get-package.md) i [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="c26be-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="c26be-155">Znajdź pakiet</span><span class="sxs-lookup"><span data-stu-id="c26be-155">Find a package</span></span>

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

<span data-ttu-id="c26be-156">Zobacz sekcję [Znajdź pakiet](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="c26be-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="c26be-157">W Visual Studio 2013 i starszych, zamiast tego użyj polecenia [Get-Package](../reference/ps-reference/ps-ref-get-package.md) .</span><span class="sxs-lookup"><span data-stu-id="c26be-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="c26be-158">Dostępność konsoli programu</span><span class="sxs-lookup"><span data-stu-id="c26be-158">Availability of the console</span></span>

<span data-ttu-id="c26be-159">Począwszy od programu Visual Studio 2017, NuGet i Menedżer pakietów NuGet są instalowane automatycznie po wybraniu dowolnego z nich. Obciążenia związane z usługą SIECIową; można ją także zainstalować oddzielnie, sprawdzając **poszczególne składniki > narzędzia kodu > opcji Menedżera pakietów NuGet** w Instalatorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c26be-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="c26be-160">Ponadto w przypadku braku Menedżera pakietów NuGet w programie Visual Studio 2015 i jego wcześniejszych wersjach zapoznaj się z **narzędziami > rozszerzenia i aktualizacje...** , a następnie wyszukaj rozszerzenie Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="c26be-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="c26be-161">Jeśli nie możesz użyć Instalatora rozszerzeń w programie Visual Studio, możesz pobrać rozszerzenie bezpośrednio z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)programu.</span><span class="sxs-lookup"><span data-stu-id="c26be-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="c26be-162">Konsola Menedżera pakietów nie jest obecnie dostępna z Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="c26be-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="c26be-163">Równoważne polecenia są jednak dostępne za pomocą [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c26be-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="c26be-164">Visual Studio dla komputerów Mac ma interfejs użytkownika do zarządzania pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="c26be-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="c26be-165">Zobacz [dołączanie pakietu NuGet do projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="c26be-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="c26be-166">Konsola Menedżera pakietów nie jest dołączona do Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c26be-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="c26be-167">Rozwiń konsolę Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="c26be-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="c26be-168">Niektóre pakiety instalują nowe polecenia dla konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="c26be-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="c26be-169">Na przykład `MvcScaffolding` tworzy polecenia, jak `Scaffold` pokazano poniżej, generujące kontrolery i widoki ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="c26be-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalowanie i używanie MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="c26be-171">Konfigurowanie profilu programu PowerShell NuGet</span><span class="sxs-lookup"><span data-stu-id="c26be-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="c26be-172">Profil programu PowerShell umożliwia wykonywanie typowych poleceń dostępnych wszędzie tam, gdzie używasz programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c26be-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="c26be-173">Pakiet NuGet obsługuje profil specyficzny dla programu NuGet, który zwykle znajduje się w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c26be-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="c26be-174">Aby znaleźć profil, wpisz `$profile` w konsoli programu:</span><span class="sxs-lookup"><span data-stu-id="c26be-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="c26be-175">Aby uzyskać więcej informacji, zobacz [Profile programu Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="c26be-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="c26be-176">Korzystanie z interfejsu wiersza polecenia NuGet. exe w konsoli programu</span><span class="sxs-lookup"><span data-stu-id="c26be-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="c26be-177">Aby udostępnić [ `nuget.exe` interfejs wiersza polecenia](../reference/nuget-exe-cli-reference.md) w konsoli Menedżera pakietów, zainstaluj pakiet [NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) z konsoli programu:</span><span class="sxs-lookup"><span data-stu-id="c26be-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
