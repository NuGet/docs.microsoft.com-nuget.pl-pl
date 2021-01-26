---
title: Informacje o wersji narzędzia NuGet 1,4
description: Informacje o wersji programu NuGet 1,4, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777146"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="fc3e8-103">Informacje o wersji narzędzia NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="fc3e8-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="fc3e8-104">Informacje o wersji narzędzia [NuGet 1,3](../release-notes/nuget-1.3.md)  |  [Informacje o wersji narzędzia NuGet 1,5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="fc3e8-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="fc3e8-105">Pakiet NuGet 1,4 został wydanych 17 czerwca 2011.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="fc3e8-106">Funkcje</span><span class="sxs-lookup"><span data-stu-id="fc3e8-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="fc3e8-107">Udoskonalenia Update-Package</span><span class="sxs-lookup"><span data-stu-id="fc3e8-107">Update-Package improvements</span></span>
<span data-ttu-id="fc3e8-108">W pakiecie NuGet 1,4 wprowadzono wiele ulepszeń polecenia Update-Package ułatwiających utrzymywanie pakietów w tej samej wersji w wielu projektach w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="fc3e8-109">Na przykład w przypadku uaktualniania pakietu do najnowszej wersji bardzo często zachodzi potrzeba aktualizacji wszystkich projektów z zainstalowanym pakietem do tego samego verision.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="fc3e8-110">To `Update-Package` polecenie ułatwia teraz:</span><span class="sxs-lookup"><span data-stu-id="fc3e8-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="fc3e8-111">Aktualizuj wszystkie pakiety w pojedynczym projekcie</span><span class="sxs-lookup"><span data-stu-id="fc3e8-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="fc3e8-112">Aktualizowanie pakietu we wszystkich projektach</span><span class="sxs-lookup"><span data-stu-id="fc3e8-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="fc3e8-113">Aktualizuj wszystkie pakiety we wszystkich projektach</span><span class="sxs-lookup"><span data-stu-id="fc3e8-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="fc3e8-114">Wykonaj "bezpieczną" aktualizację na wszystkich pakietach</span><span class="sxs-lookup"><span data-stu-id="fc3e8-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="fc3e8-115">`-Safe`Flaga ogranicza uaktualnienia do wersji tylko z tym samym składnikiem wersji głównej i pomocniczej.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="fc3e8-116">Na przykład jeśli zainstalowano wersję 1.0.0 pakietu, a w kanale informacyjnym są dostępne wersje 1.0.1, 1.0.2 i 1,1, `-Safe` Flaga aktualizuje pakiet do 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="fc3e8-117">Uaktualnienie bez `-Safe` flagi spowoduje uaktualnienie pakietu do najnowszej wersji, 1,1.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="fc3e8-118">Zarządzanie pakietami na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fc3e8-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="fc3e8-119">Przed pakietem NuGet 1,4 zainstalowanie pakietu w wielu projektach było bardzo uciążliwe przy użyciu okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="fc3e8-120">Wymagane jest uruchomienie okna dialogowego raz dla każdego projektu.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="fc3e8-121">Pakiet NuGet 1,4 dodaje obsługę instalowania/odinstalowywania/aktualizowania pakietów w wielu projektach w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="fc3e8-122">Wystarczy uruchomić aplikację, klikając rozwiązanie prawym przyciskiem myszy, a następnie wybierając opcję **Zarządzaj pakietami NuGet** .</span><span class="sxs-lookup"><span data-stu-id="fc3e8-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Okno dialogowe Zarządzanie pakietami NuGet na poziomie rozwiązania](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="fc3e8-124">Zauważ, że na pasku tytułu okna dialogowego wyświetlana jest nazwa rozwiązania, a nie nazwa projektu.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="fc3e8-125">Operacje na pakietach udostępniają teraz listę pól wyboru z listą projektów, do których operacja powinna zostać zastosowana.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Zarządzaj wyborem projektu pakietów NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="fc3e8-127">Aby uzyskać więcej informacji, zobacz temat dotyczący [zarządzania pakietami dla rozwiązania](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="fc3e8-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="fc3e8-128">Ograniczanie uaktualnień do dozwolonych wersji</span><span class="sxs-lookup"><span data-stu-id="fc3e8-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="fc3e8-129">Domyślnie po uruchomieniu `Update-Package` polecenia w pakiecie (lub zaktualizowaniu pakietu przy użyciu okna dialogowego) zostanie ono zaktualizowane do najnowszej wersji w źródle danych.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="fc3e8-130">Dzięki nowej obsłudze aktualizacji wszystkich pakietów mogą wystąpić sytuacje, w których chcesz zablokować pakiet do określonego zakresu wersji.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="fc3e8-131">Na przykład może być wiadomo, że aplikacja będzie działała tylko w wersji 2. \* pakietu, ale nie 3,0 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="fc3e8-132">Aby zapobiec przypadkowemu aktualizowaniu pakietu do wersji 3, program NuGet 1,4 dodaje obsługę ograniczania zakresu wersji, do których można uaktualnić pakiety, poprzez ręczne edytowanie `packages.config` pliku przy użyciu nowego `allowedVersions` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="fc3e8-133">Na przykład poniższy przykład pokazuje, jak zablokować `SomePackage` pakiet do wersji 2,0 – 3,0 (wyłączne).</span><span class="sxs-lookup"><span data-stu-id="fc3e8-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="fc3e8-134">`allowedVersions`Atrybut akceptuje wartości przy użyciu [formatu zakresu wersji](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="fc3e8-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="fc3e8-135">Należy pamiętać, że w 1,4, blokowanie pakietu do określonego zakresu wersji musi być edytowane ręcznie.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="fc3e8-136">W programie NuGet 1,5 planujemy dodanie obsługi umieszczania tego zakresu za pośrednictwem `Install-Package` polecenia.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="fc3e8-137">Wizualizator pakietu</span><span class="sxs-lookup"><span data-stu-id="fc3e8-137">Package Visualizer</span></span>
<span data-ttu-id="fc3e8-138">Nowy wizualizator pakietu, uruchamiany za pomocą   ->  opcji menu wizualizator pakietu **Menedżera pakietów biblioteki** narzędzi  ->   , umożliwia łatwe wizualizację wszystkich projektów i ich zależności pakietów w ramach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="fc3e8-139">_**Ważna Uwaga:** Ta funkcja wykorzystuje obsługę DGML w programie Visual Studio. Tworzenie wizualizacji jest obsługiwane tylko w Visual Studio Ultimate. Wyświetlanie diagramu DGML jest obsługiwane tylko w Visual Studio Premium lub wyższym._</span><span class="sxs-lookup"><span data-stu-id="fc3e8-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Wizualizator pakietu](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="fc3e8-141">Automatyczne sprawdzanie aktualizacji dla okna dialogowego Narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="fc3e8-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="fc3e8-142">Niektóre wersje programu NuGet wprowadzają nowe funkcje wyrażone za pośrednictwem `.nuspec` pliku, które nie są rozpoznawane przez starsze wersje okna dialogowego Narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="fc3e8-143">Przykładem jest wprowadzenie w programie NuGet 1,4 do [określania zestawów struktury](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="fc3e8-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="fc3e8-144">Z tego względu należy użyć najnowszej wersji programu NuGet, aby upewnić się, że można używać pakietów korzystających z najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="fc3e8-145">Aby aktualizacje NuGet były bardziej widoczne, okno dialogowe NuGet zawiera logikę do wyróżnienia, gdy dostępna jest nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="fc3e8-146">_**Uwaga**: sprawdzanie jest wykonywane tylko wtedy, gdy w bieżącej sesji została wybrana karta **online** ._</span><span class="sxs-lookup"><span data-stu-id="fc3e8-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Okno dialogowe zarządzania pakietami NuGet z dostępną nową wersją](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="fc3e8-148">Aby wyłączyć automatyczne sprawdzanie aktualizacji, przejdź do okna dialogowego Ustawienia NuGet i usuń zaznaczenie pola **wyboru Automatycznie sprawdzaj dostępność aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Ustawienia narzędzia NuGet](./media/nuget-settings.png)

<span data-ttu-id="fc3e8-150">Ta funkcja została faktycznie dodana w programie NuGet 1,3, ale nie będzie widoczna, oczywiście dopóki nie zostanie udostępniona aktualizacja 1,3, taka jak NuGet 1,4.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="fc3e8-151">Ulepszenia okna dialogowego Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="fc3e8-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="fc3e8-152">**Ulepszone nazwy menu**: opcje menu umożliwiające uruchomienie okna dialogowego zostały zmienione pod kątem przejrzystości.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="fc3e8-153">Opcja menu umożliwia teraz **Zarządzanie pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="fc3e8-154">W **okienku szczegółów jest wyświetlana Najnowsza Data aktualizacji**: w oknie dialogowym narzędzia NuGet jest wyświetlana data najnowszej aktualizacji w okienku szczegółów pakietu po wybraniu karty **online** lub **aktualizacje** .</span><span class="sxs-lookup"><span data-stu-id="fc3e8-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="fc3e8-155">**Lista wyświetlanych tagów**: w oknie dialogowym NuGet są wyświetlane tagi.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="fc3e8-156">Ulepszenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc3e8-156">Powershell Improvements</span></span>
* <span data-ttu-id="fc3e8-157">**Podpisane skrypty programu PowerShell**: pakiet NuGet obejmuje podpisane skrypty programu PowerShell umożliwiające użycie w bardziej restrykcyjnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="fc3e8-158">**Monitowanie o pomoc techniczną**: Konsola Menedżera pakietów obsługuje teraz monitowanie za pomocą `$host.ui.Prompt` `$host.ui.PromptForChoice` poleceń i.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="fc3e8-159">**Nazwy źródeł pakietów**: podanie nazwy źródła pakietu jest obsługiwane podczas określania źródła pakietu przy użyciu `-Source` flagi.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="fc3e8-160">Udoskonalenia wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="fc3e8-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="fc3e8-161">**Polecenia niestandardowe NuGet**: nuget.exe jest rozszerzalny za pośrednictwem poleceń niestandardowych przy użyciu MEF.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="fc3e8-162">**Prostsze przepływ pracy do tworzenia pakietów symboli**: `-Symbols` flagę można zastosować do normalnej Konwencji na podstawie struktury folderów tworzącej pakiet symboli, dołączając tylko źródło i `.pdb` pliki znajdujące się w folderze.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="fc3e8-163">**Określanie wielu źródeł**: `NuGet install` polecenie obsługuje określanie wielu źródeł przy użyciu średnika jako ogranicznika lub przez `-Source` wiele razy.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="fc3e8-164">**Obsługa uwierzytelniania serwera proxy**: pakiet NuGet 1,4 dodaje obsługę monitowania o poświadczenia użytkownika w przypadku korzystania z programu NuGet za serwerem proxy wymagającym uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="fc3e8-165">**Zmiana wnuget.exe aktualizacji**: `-Self` flaga jest teraz wymagana do nuget.exe do aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="fc3e8-166">`nuget.exe Update` teraz Pobiera ścieżkę do `packages.config` pliku i próbuje zaktualizować pakiety.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="fc3e8-167">Należy pamiętać, że ta aktualizacja jest ograniczona, ponieważ nie będzie: \* \* aktualizowanie, Dodawanie, usuwanie zawartości w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="fc3e8-168">\* \* Uruchamianie skryptów programu PowerShell w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="fc3e8-169">Obsługa serwera NuGet na potrzeby wypychania pakietów przy użyciu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="fc3e8-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="fc3e8-170">Pakiet NuGet zawiera prosty sposób hostowania [uproszczonego, opartego na sieci Web repozytorium NuGet](../hosting-packages/nuget-server.md) za pośrednictwem `NuGet.Server` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="fc3e8-171">W programie NuGet 1,4 serwer uproszczony obsługuje wypychanie i usuwanie pakietów przy użyciu nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="fc3e8-172">Najnowsza wersja programu `NuGet.Server` dodaje nową `appSetting` nazwę `apiKey` .</span><span class="sxs-lookup"><span data-stu-id="fc3e8-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="fc3e8-173">Gdy klucz zostanie pominięty lub pozostawiono pusty, wypychanie pakietów do źródła danych jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="fc3e8-174">Ustawienie apiKey na wartość (idealnym silnym hasłem) umożliwia wypychanie pakietów przy użyciu nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="fc3e8-175">Obsługa narzędzi Windows Phone Tools mango Edition</span><span class="sxs-lookup"><span data-stu-id="fc3e8-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="fc3e8-176">Pakiet NuGet jest teraz obsługiwany w wersji Release Candidate narzędzi Windows Phone Tools for mango.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="fc3e8-177">Obecnie narzędzia Windows Phone nie obsługują Menedżera rozszerzeń programu Visual Studio, więc aby można było zainstalować pakiet NuGet dla Windows Phone narzędzi, może być konieczne ręczne pobranie i uruchomienie VSIX.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="fc3e8-178">Aby odinstalować pakiet NuGet dla narzędzi Windows Phone, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="fc3e8-179">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="fc3e8-179">Bug Fixes</span></span>
<span data-ttu-id="fc3e8-180">Pakiet NuGet 1,4 zawiera łącznie 88 elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="fc3e8-181">71 z tych elementów zostało oznaczonych jako błędy.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="fc3e8-182">Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,4, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="fc3e8-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="fc3e8-183">Poprawki błędów warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="fc3e8-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="fc3e8-184">[Problem 603](http://nuget.codeplex.com/workitem/603): zależności pakietów między różnymi repozytoriami są rozpoznawane poprawnie podczas określania określonego źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="fc3e8-185">[Problem 1036](http://nuget.codeplex.com/workitem/1036): Dodawanie `NuGet Pack SomeProject.csproj` do zdarzenia po kompilacji nie powoduje już pętli nieskończonej.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="fc3e8-186">[Problem 961](http://nuget.codeplex.com/workitem/961): `-Source` Flaga obsługuje ścieżki względne.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="fc3e8-187">Aktualizacja NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="fc3e8-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="fc3e8-188">Wkrótce po wydaniu programu NuGet 1,4 znaleźliśmy kilka problemów, które były ważne do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="fc3e8-189">Określony numer wersji tej aktualizacji do 1,4 to 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="fc3e8-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="fc3e8-190">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="fc3e8-190">Bug Fixes</span></span>
* <span data-ttu-id="fc3e8-191">[Problem 1220](http://nuget.codeplex.com/workitem/1220): Update-Package nie `install.ps1` / `uninstall.ps1` jest wykonywane we wszystkich projektach, gdy istnieje więcej niż jeden projekt</span><span class="sxs-lookup"><span data-stu-id="fc3e8-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="fc3e8-192">[Problem 1156](http://nuget.codeplex.com/workitem/1156): Konsolidacja Menedżera pakietów została zablokowana na W2K3/XP (gdy program PowerShell 2 nie jest zainstalowany)</span><span class="sxs-lookup"><span data-stu-id="fc3e8-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
