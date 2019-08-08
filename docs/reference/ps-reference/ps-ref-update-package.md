---
title: Aktualizacja NuGet — Dokumentacja programu PowerShell pakietu
description: Dokumentacja polecenia Update-Package programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328184"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="109f6-103">Update-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="109f6-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="109f6-104">*Dostępne tylko w [konsoli Menedżera pakietów NuGet](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="109f6-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="109f6-105">Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie do nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="109f6-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="109f6-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="109f6-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="109f6-107">W programie NuGet 2.8 + `Update-Package` można użyć do obniżenia poziomu istniejącego pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="109f6-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="109f6-108">Na przykład jeśli masz zainstalowany plik Microsoft. AspNet. MVC 5.1.0-RC1, następujące polecenie obniży go do 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="109f6-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="109f6-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="109f6-109">Parameters</span></span>

|  <span data-ttu-id="109f6-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="109f6-110">Parameter</span></span> | <span data-ttu-id="109f6-111">Opis</span><span class="sxs-lookup"><span data-stu-id="109f6-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="109f6-112">Id</span><span class="sxs-lookup"><span data-stu-id="109f6-112">Id</span></span> | <span data-ttu-id="109f6-113">Identyfikator pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="109f6-113">The identifier of the package to update.</span></span> <span data-ttu-id="109f6-114">W przypadku pominięcia program aktualizuje wszystkie pakiety.</span><span class="sxs-lookup"><span data-stu-id="109f6-114">If omitted, updates all packages.</span></span> <span data-ttu-id="109f6-115">Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="109f6-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="109f6-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="109f6-116">IgnoreDependencies</span></span> | <span data-ttu-id="109f6-117">Pomija aktualizowanie zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="109f6-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="109f6-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="109f6-118">ProjectName</span></span> | <span data-ttu-id="109f6-119">Nazwa projektu zawierającego pakiety do zaktualizowania, domyślnie dla wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="109f6-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="109f6-120">Wersja</span><span class="sxs-lookup"><span data-stu-id="109f6-120">Version</span></span> | <span data-ttu-id="109f6-121">Wersja, która ma zostać użyta do uaktualnienia, domyślna dla najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="109f6-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="109f6-122">W programie NuGet 3.0 + wartość wersji musi mieć jedną z najniższych, najwyższego, *HighestMinor*lub *HighestPatch* (równoważne z bezpiecznym).</span><span class="sxs-lookup"><span data-stu-id="109f6-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="109f6-123">Sejf</span><span class="sxs-lookup"><span data-stu-id="109f6-123">Safe</span></span> | <span data-ttu-id="109f6-124">Ogranicza uaktualnienia do wersji tylko z tą samą wersją główną i pomocniczą jak aktualnie zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="109f6-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="109f6-125">Source</span><span class="sxs-lookup"><span data-stu-id="109f6-125">Source</span></span> | <span data-ttu-id="109f6-126">Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania.</span><span class="sxs-lookup"><span data-stu-id="109f6-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="109f6-127">Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="109f6-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="109f6-128">W przypadku pominięcia program `Update-Package` przeszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="109f6-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="109f6-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="109f6-129">IncludePrerelease</span></span> | <span data-ttu-id="109f6-130">Obejmuje pakiety wersji wstępnej dla aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="109f6-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="109f6-131">Następnie</span><span class="sxs-lookup"><span data-stu-id="109f6-131">Reinstall</span></span> | <span data-ttu-id="109f6-132">Resintalls pakiety przy użyciu ich aktualnie zainstalowanych wersji.</span><span class="sxs-lookup"><span data-stu-id="109f6-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="109f6-133">Zobacz [ponowne instalowanie i aktualizowanie pakietów](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="109f6-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="109f6-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="109f6-134">FileConflictAction</span></span> | <span data-ttu-id="109f6-135">Akcja, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="109f6-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="109f6-136">Możliwe wartości to *overwrite, IGNORE, None, OverwriteAll*i *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="109f6-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="109f6-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="109f6-137">DependencyVersion</span></span> | <span data-ttu-id="109f6-138">Wersja pakietów zależności do użycia, która może być jedną z następujących:</span><span class="sxs-lookup"><span data-stu-id="109f6-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="109f6-139">*Najniższy* (domyślnie): najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="109f6-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="109f6-140">*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="109f6-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="109f6-141">*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="109f6-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="109f6-142">*Najwyższa* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="109f6-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="109f6-143">Możesz ustawić wartość domyślną przy użyciu [`dependencyVersion`](../nuget-config-file.md#config-section) ustawienia `Nuget.Config` w pliku.</span><span class="sxs-lookup"><span data-stu-id="109f6-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="109f6-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="109f6-144">ToHighestPatch</span></span> | <span data-ttu-id="109f6-145">równoważne z bezpiecznym.</span><span class="sxs-lookup"><span data-stu-id="109f6-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="109f6-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="109f6-146">ToHighestMinor</span></span> | <span data-ttu-id="109f6-147">Ogranicza uaktualnienia do wersji tylko z tą samą wersją główną jak aktualnie zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="109f6-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="109f6-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="109f6-148">WhatIf</span></span> | <span data-ttu-id="109f6-149">Pokazuje, co się stanie po uruchomieniu polecenia bez jego faktycznego wykonania.</span><span class="sxs-lookup"><span data-stu-id="109f6-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="109f6-150">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="109f6-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="109f6-151">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="109f6-151">Common Parameters</span></span>

<span data-ttu-id="109f6-152">`Update-Package`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="109f6-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="109f6-153">Przykłady</span><span class="sxs-lookup"><span data-stu-id="109f6-153">Examples</span></span>

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