---
title: Pakiet aktualizacji NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do polecenia programu PowerShell pakietu aktualizacji w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, pakiet aktualizacji"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 768fdb4d7c785b4f3ed9e70958390676ea965794
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="51d88-104">Pakiet aktualizacji (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="51d88-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="51d88-105">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="51d88-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="51d88-106">Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie do nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="51d88-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="51d88-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="51d88-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="51d88-108">W NuGet 2.8 + `Update-Package` można obniżyć istniejący pakiet w projekcie.</span><span class="sxs-lookup"><span data-stu-id="51d88-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="51d88-109">Na przykład jeśli masz zainstalowany 5.1.0-rc1 Microsoft.AspNet.MVC następujące polecenie spowoduje obniżyć go 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="51d88-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="51d88-110">NuGet 2.7 i starszych zwraca błąd informujący o tym, że jest już zainstalowana nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="51d88-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>

## <a name="parameters"></a><span data-ttu-id="51d88-111">Parametry</span><span class="sxs-lookup"><span data-stu-id="51d88-111">Parameters</span></span>

|  <span data-ttu-id="51d88-112">Parametr</span><span class="sxs-lookup"><span data-stu-id="51d88-112">Parameter</span></span> | <span data-ttu-id="51d88-113">Opis</span><span class="sxs-lookup"><span data-stu-id="51d88-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51d88-114">Id</span><span class="sxs-lookup"><span data-stu-id="51d88-114">Id</span></span> | <span data-ttu-id="51d88-115">Identyfikator pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="51d88-115">The identifier of the package to update.</span></span> <span data-ttu-id="51d88-116">Pominięcie aktualizuje wszystkie pakiety.</span><span class="sxs-lookup"><span data-stu-id="51d88-116">If omitted, updates all packages.</span></span> <span data-ttu-id="51d88-117">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="51d88-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="51d88-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="51d88-118">IgnoreDependencies</span></span> | <span data-ttu-id="51d88-119">Pomija zależności pakietu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="51d88-119">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="51d88-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="51d88-120">ProjectName</span></span> | <span data-ttu-id="51d88-121">Nazwa projektu zawierającego pakietów aktualizacji, domyślnie używany do wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="51d88-121">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="51d88-122">Wersja</span><span class="sxs-lookup"><span data-stu-id="51d88-122">Version</span></span> | <span data-ttu-id="51d88-123">Wersja do użycia podczas uaktualniania, domyślnie używany do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="51d88-123">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="51d88-124">W NuGet 3.0 + wartość wersji musi być jedną z *najniższy, najwyższa, HighestMinor*, lub *HighestPatch* (równoważne - bezpieczny).</span><span class="sxs-lookup"><span data-stu-id="51d88-124">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="51d88-125">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="51d88-125">Safe</span></span> | <span data-ttu-id="51d88-126">Ogranicza uaktualnienia do wersji tylko z tej samej wersji głównej i pomocniczej jako aktualnie zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="51d88-126">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="51d88-127">Źródło</span><span class="sxs-lookup"><span data-stu-id="51d88-127">Source</span></span> | <span data-ttu-id="51d88-128">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="51d88-128">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="51d88-129">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="51d88-129">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="51d88-130">Pominięcie `Uninstall-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="51d88-130">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="51d88-131">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="51d88-131">IncludePrerelease</span></span> | <span data-ttu-id="51d88-132">Zawiera pakiety wersji wstępnej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="51d88-132">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="51d88-133">Zainstaluj ponownie</span><span class="sxs-lookup"><span data-stu-id="51d88-133">Reinstall</span></span> | <span data-ttu-id="51d88-134">Pakiety Resintalls przy użyciu ich obecnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="51d88-134">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="51d88-135">Zobacz [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="51d88-135">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="51d88-136">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="51d88-136">FileConflictAction</span></span> | <span data-ttu-id="51d88-137">Akcja wykonywana po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="51d88-137">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="51d88-138">Możliwe wartości to *zastępowania, Ignoruj, brak OverwriteAll*, i *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="51d88-138">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="51d88-139">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="51d88-139">DependencyVersion</span></span> | <span data-ttu-id="51d88-140">Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="51d88-140">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="51d88-141">*Najniższa* (domyślnie): Najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="51d88-141">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="51d88-142">*HighestPatch*: wersja z najniższą głównych, najniższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="51d88-142">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="51d88-143">*HighestMinor*: wersja z najniższą głównych, najwyższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="51d88-143">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="51d88-144">*Najwyższy* (domyślnie pakiet aktualizacji bez parametrów): najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="51d88-144">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="51d88-145">Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="51d88-145">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="51d88-146">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="51d88-146">ToHighestPatch</span></span> | <span data-ttu-id="51d88-147">Ogranicza uaktualnienia do tylko wersji z tej samej wersji pomocniczej jako aktualnie zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="51d88-147">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="51d88-148">Tohighestminor powoduje aktualizację</span><span class="sxs-lookup"><span data-stu-id="51d88-148">ToHighestMinor</span></span> | <span data-ttu-id="51d88-149">Ogranicza uaktualnienia do tylko wersji z taką samą wersję główną jako aktualnie zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="51d88-149">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="51d88-150">WhatIf</span><span class="sxs-lookup"><span data-stu-id="51d88-150">WhatIf</span></span> | <span data-ttu-id="51d88-151">Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="51d88-151">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="51d88-152">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="51d88-152">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="51d88-153">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="51d88-153">Common Parameters</span></span>

<span data-ttu-id="51d88-154">`Update-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="51d88-154">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="51d88-155">Przykłady</span><span class="sxs-lookup"><span data-stu-id="51d88-155">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```