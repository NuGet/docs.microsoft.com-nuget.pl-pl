---
title: Informacje o wersji 1.4 NuGet
description: Informacje o wersji programu NuGet 1.4 tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550634"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="3f4ea-103">Informacje o wersji 1.4 NuGet</span><span class="sxs-lookup"><span data-stu-id="3f4ea-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="3f4ea-104">[Informacje o wersji NuGet 1.3](../release-notes/nuget-1.3.md) | [informacjach o wersji NuGet w wersji 1.5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="3f4ea-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="3f4ea-105">NuGet 1.4 został wydany 17 czerwca 2011.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="3f4ea-106">Funkcje</span><span class="sxs-lookup"><span data-stu-id="3f4ea-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="3f4ea-107">Ulepszenia dotyczące pakietów aktualizacji</span><span class="sxs-lookup"><span data-stu-id="3f4ea-107">Update-Package improvements</span></span>
<span data-ttu-id="3f4ea-108">NuGet 1.4 wprowadzono wiele ulepszeń do polecenia pakiet aktualizacji, co ułatwia zapewnienie pakietów w tej samej wersji wielu projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="3f4ea-109">Na przykład podczas uaktualniania pakietu do najnowszej wersji, jest bardzo często mają wszystkie projekty z pakietu, aby zainstalować zaktualizowane do tej samej verision.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="3f4ea-110">`Update-Package` Polecenia umożliwia teraz łatwiejsze do:</span><span class="sxs-lookup"><span data-stu-id="3f4ea-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="3f4ea-111">Aktualizuj wszystkie pakiety w jednym projekcie</span><span class="sxs-lookup"><span data-stu-id="3f4ea-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="3f4ea-112">Aktualizuj pakiet we wszystkich projektach</span><span class="sxs-lookup"><span data-stu-id="3f4ea-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="3f4ea-113">Aktualizuj wszystkie pakiety we wszystkich projektach</span><span class="sxs-lookup"><span data-stu-id="3f4ea-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="3f4ea-114">Przeprowadzania "bezpieczne" Aktualizuj wszystkie pakiety</span><span class="sxs-lookup"><span data-stu-id="3f4ea-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="3f4ea-115">`-Safe` Flagi ogranicza uaktualnienia do wersji tylko za pomocą tego samego składnika wersji głównych i pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="3f4ea-116">Na przykład, jeśli jest zainstalowana wersja 1.0.0 pakietu i wersji 1.0.1, 1.0.2 i 1.1 są dostępne w źródle danych `-Safe` flagi aktualizuje pakiet 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="3f4ea-117">Uaktualnianie bez `-Safe` flagi czy uaktualnić pakiet do najnowszej wersji 1.1.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="3f4ea-118">Zarządzanie pakietami na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="3f4ea-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="3f4ea-119">Przed NuGet 1.4 instalowania pakietu w wielu projektach było uciążliwe, korzystając z okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="3f4ea-120">Wymaga ona, uruchamiając okno dialogowe raz na projekt.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="3f4ea-121">NuGet 1.4 dodaje obsługi instalowania/odinstalowywania/aktualizowania pakietów w wielu projektach, w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="3f4ea-122">Po prostu uruchomić, klikając prawym przyciskiem myszy rozwiązanie i wybierając **Zarządzaj pakietami NuGet** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Okno dialogowe poziom Zarządzaj pakietami NuGet rozwiązania](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="3f4ea-124">Zwróć uwagę, że na pasku tytułu okna dialogowego nazwę rozwiązania jest wyświetlany, a nie nazwa projektu.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="3f4ea-125">Operacje pakietu udostępniają teraz listy pól wyboru z listy projektów, których mają dotyczyć operacji.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Zarządzanie wybór projektu pakiety NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="3f4ea-127">Aby uzyskać więcej informacji, zobacz temat w [Zarządzanie pakietami dla rozwiązania](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="3f4ea-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="3f4ea-128">Ograniczając uaktualniania do wersji dozwolone</span><span class="sxs-lookup"><span data-stu-id="3f4ea-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="3f4ea-129">Domyślnie podczas uruchamiania `Update-Package` na pakiet (lub aktualizowanie pakietu za pomocą okna dialogowego), polecenia zostaną zaktualizowane do najnowszej wersji w źródle danych.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="3f4ea-130">Z nową obsługę aktualizacji wszystkich pakietów może być przypadki, w których chcesz zablokować pakietu do określonego zakresu wersji.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="3f4ea-131">Na przykład mogą wiedzieć z wyprzedzeniem, że aplikacja będzie działać tylko z 2.\* wersji pakietu, ale nie 3.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="3f4ea-132">Aby zapobiec przypadkowemu aktualizacja pakietu do 3, NuGet 1.4 dodaje obsługę ograniczając zakres wersji, które pakiety mogą być uaktualniane do, ręcznie edytując `packages.config` plików za pomocą nowego `allowedVersions` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="3f4ea-133">Na przykład, poniższy przykład pokazuje, jak zablokować `SomePackage` pakietu wersji zakresu w wersji 2.0 — 3.0 (wyłącznie).</span><span class="sxs-lookup"><span data-stu-id="3f4ea-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="3f4ea-134">`allowedVersions` Atrybut akceptuje wartości za pomocą [formatu zakres wersji](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="3f4ea-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="3f4ea-135">Należy pamiętać, że 1.4, blokowanie pakietu do określonego zakresu wersji musi być ręcznie edytowany.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="3f4ea-136">W wersji 1.5 NuGet planujemy dodanie obsługi wprowadzania do tego zakresu, za pośrednictwem `Install-Package` polecenia.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="3f4ea-137">Pakiet wizualizatora</span><span class="sxs-lookup"><span data-stu-id="3f4ea-137">Package Visualizer</span></span>
<span data-ttu-id="3f4ea-138">Wizualizator nowego pakietu, wyszukiwarce uruchamianej w **narzędzia** -> **Menedżer pakietów biblioteki** -> **pakiet wizualizatora** opcji menu pozwala na łatwo Wizualizuj wszystkich projektów i ich zależności pakietów w ramach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="3f4ea-139">_**Ważna Uwaga:** ta funkcja korzysta z pomocy technicznej DGML w programie Visual Studio. Tworzenie wizualizacji jest obsługiwana tylko w programie Visual Studio Ultimate. Wyświetlanie diagramu DGML jest obsługiwana tylko w Visual Studio Premium lub wyższego._</span><span class="sxs-lookup"><span data-stu-id="3f4ea-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Pakiet wizualizatora](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="3f4ea-141">Sprawdzanie aktualizacji automatycznych dla okna dialogowego NuGet</span><span class="sxs-lookup"><span data-stu-id="3f4ea-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="3f4ea-142">Niektóre wersje NuGet wprowadzać nowe funkcje, które wyrażone za pomocą `.nuspec` pliku, który jest niezrozumiały przez starsze wersje programu NuGet okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="3f4ea-143">Przykładem jest wprowadzenie 1.4 NuGet dla [określania zestawów framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="3f4ea-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="3f4ea-144">W związku z tym należy używać najnowszej wersji pakietu NuGet, aby upewnić się, że możesz użyć pakietów, korzystając z zalet najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="3f4ea-145">Aby wprowadzić aktualizacje NuGet bardziej widoczne, okno dialogowe NuGet zawiera logikę do Podświetl, gdy dostępna jest nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="3f4ea-146">_**Uwaga**: sprawdzanie jest wykonywane tylko wtedy, gdy **Online** kartę został wybrany w bieżącej sesji._</span><span class="sxs-lookup"><span data-stu-id="3f4ea-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Zarządzanie pakietami NuGet dialog z dostępna nowa wersja](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="3f4ea-148">Aby wyłączyć funkcję automatycznego sprawdzania aktualizacji, przejdź do okna dialogowego Ustawienia NuGet i usuń zaznaczenie pola wyboru **automatycznie sprawdzaj dostępność aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Ustawienia NuGet](./media/nuget-settings.png)

<span data-ttu-id="3f4ea-150">Ta funkcja rzeczywiście został dodany do programu NuGet 1.3, ale nie będzie widoczny, oczywiście, aż aktualizacja 1.3, takie jak NuGet 1.4, została udostępniona.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="3f4ea-151">Ulepszenia okna dialogowego Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="3f4ea-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="3f4ea-152">**Nazwy menu ulepszone**: Opcje Menu, aby uruchomić okno dialogowe zostały zmienione w celu uściślenia.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="3f4ea-153">Opcja menu jest teraz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="3f4ea-154">**Okienko szczegółów pokazuje Najpóźniejsza data aktualizacji**: NuGet, okno dialogowe wyświetla datę ostatniej aktualizacji w okienku szczegółów pakietu podczas **Online** lub **aktualizuje** wybrana jest karta.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="3f4ea-155">**Lista tagów wyświetlane**: tagi Wyświetla okno dialogowe Nuget.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="3f4ea-156">Ulepszenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f4ea-156">Powershell Improvements</span></span>
* <span data-ttu-id="3f4ea-157">**Podpisane skrypty programu PowerShell**: NuGet zawiera podpisanych skryptów programu Powershell umożliwiające użycie w środowiskach bardziej restrykcyjne.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="3f4ea-158">**Monitowanie pomocy technicznej**: konsoli Menedżera pakietów obsługuje teraz monitowania użytkownika za pośrednictwem `$host.ui.Prompt` i `$host.ui.PromptForChoice` poleceń.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="3f4ea-159">**Pakiet nazw źródeł**: podanie nazwy źródła pakietu jest obsługiwana w przypadku określania źródła pakietu przy użyciu `-Source` flagi.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="3f4ea-160">ulepszenia wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="3f4ea-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="3f4ea-161">**Niestandardowe polecenia NuGet**: nuget.exe jest rozszerzalny za pomocą polecenia niestandardowe za pomocą MEF.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="3f4ea-162">**Prostsze przepływu pracy do tworzenia pakietów symbol**: `-Symbols` flagi mogą być stosowane do normalnego oparte na Konwencji strukturę folderów, tworzenie pakietu symboli, umieszczając tylko źródła i `.pdb` pliki znajdujące się w folderze.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="3f4ea-163">**Określanie wielu źródeł**: `NuGet install` polecenie obsługuje Określanie wielu źródeł przy użyciu średników, jak ogranicznik lub określając `-Source` wiele razy.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="3f4ea-164">**Obsługuje uwierzytelnianie serwera proxy**: 1,4 NuGet dodaje obsługę monit o podanie poświadczeń użytkownika, gdy używasz serwera proxy, który wymaga uwierzytelniania za pomocą narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="3f4ea-165">**nuget.exe aktualizacji zmiana powodująca niezgodność**: `-Self` flaga jest teraz wymagany nuget.exe samodzielne zaktualizowanie się.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="3f4ea-166">`nuget.exe Update` teraz przyjmuje ścieżkę do `packages.config` plik i spróbuje pakietów aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="3f4ea-167">Należy pamiętać, że ta aktualizacja jest ograniczony w tym, że nie będzie: ** zaktualizować, Dodaj, usuń zawartość w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="3f4ea-168">** Uruchamiania skryptów programu Powershell w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="3f4ea-169">Obsługa serwera NuGet wypychania pakietów przy użyciu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="3f4ea-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="3f4ea-170">NuGet zawiera prosty sposób hosta [uproszczone sieci web na podstawie repozytorium NuGet](../hosting-packages/nuget-server.md) za pośrednictwem `NuGet.Server` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="3f4ea-171">NuGet 1.4 lekki serwer obsługuje wypychanie i usuwanie pakietów przy użyciu nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="3f4ea-172">Najnowszą wersję `NuGet.Server` dodaje nowy `appSetting`o nazwie `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="3f4ea-173">Gdy klucz zostanie pominięty lub pole pozostanie puste, wypychanie pakietów do kanału informacyjnego jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="3f4ea-174">Ustawienie apiKey wartości (najlepiej silne hasło) umożliwia wypychania pakietów przy użyciu nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="3f4ea-175">Obsługa wersji Mango narzędzi Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3f4ea-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="3f4ea-176">NuGet jest teraz obsługiwana w wersji release candidate narzędzi Windows Phone dla Mango.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="3f4ea-177">Obecnie narzędzia Windows Phone nie ma obsługi dla Menedżera rozszerzenia Visual Studio tak zainstalować narzędzia do dla Windows Phone NuGet, może być konieczne pobranie i uruchomienie VSIX ręcznie.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="3f4ea-178">Aby odinstalować NuGet dla Windows Phone narzędzia, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="3f4ea-179">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="3f4ea-179">Bug Fixes</span></span>
<span data-ttu-id="3f4ea-180">NuGet 1.4 ma w sumie 88 stałej elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="3f4ea-181">71 tych zostały oznaczone jako błędy.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="3f4ea-182">Aby uzyskać pełną listę prac elementy rozwiązane w NuGet 1.4, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="3f4ea-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="3f4ea-183">Poprawki błędów warte odnotowania:</span><span class="sxs-lookup"><span data-stu-id="3f4ea-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="3f4ea-184">[Problem 603](http://nuget.codeplex.com/workitem/603): zależności pakietów w różnych repozytoriach jest rozpoznawana jako poprawnie podczas określania źródła określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="3f4ea-185">[Problem 1036](http://nuget.codeplex.com/workitem/1036): dodawanie `NuGet Pack SomeProject.csproj` na zdarzenie po kompilacji nie jest już powoduje nieskończoną pętlę.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="3f4ea-186">[Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` flagi obsługuje ścieżki względne.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="3f4ea-187">Aktualizacja NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="3f4ea-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="3f4ea-188">Wkrótce po wydaniu NuGet 1.4 znaleźliśmy kilka problemów, które były ważne rozwiązać problem.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="3f4ea-189">Liczba określonych wersji tej aktualizacji 1.4 jest 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="3f4ea-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="3f4ea-190">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="3f4ea-190">Bug Fixes</span></span>
* <span data-ttu-id="3f4ea-191">[Problem 1220](http://nuget.codeplex.com/workitem/1220): pakiet aktualizacji nie jest wykonywany `install.ps1` / `uninstall.ps1` we wszystkich projektach w sytuacji, gdy istnieje więcej niż jeden projekt</span><span class="sxs-lookup"><span data-stu-id="3f4ea-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="3f4ea-192">[Problem 1156](http://nuget.codeplex.com/workitem/1156): konsoli Menedżera pakietów została zablokowana na W2K3/XP (Jeśli nie zainstalowano programu Powershell 2)</span><span class="sxs-lookup"><span data-stu-id="3f4ea-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
