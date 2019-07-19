---
title: Synchronizacja NuGet — Dokumentacja programu PowerShell pakietu
description: Informacje dotyczące polecenia programu PowerShell dla pakietu Sync w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328196"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5df31-103">Sync-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5df31-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5df31-104">*Wersja 3.0 +; dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="5df31-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5df31-105">Pobiera wersję zainstalowanego pakietu z określonego (lub domyślnego) projektu i synchronizuje wersję do pozostałych projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="5df31-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="5df31-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="5df31-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5df31-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="5df31-107">Parameters</span></span>

| <span data-ttu-id="5df31-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="5df31-108">Parameter</span></span> | <span data-ttu-id="5df31-109">Opis</span><span class="sxs-lookup"><span data-stu-id="5df31-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5df31-110">Id</span><span class="sxs-lookup"><span data-stu-id="5df31-110">Id</span></span> | <span data-ttu-id="5df31-111">Potrzeb Identyfikator pakietu do zsynchronizowania. Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="5df31-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5df31-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="5df31-112">IgnoreDependencies</span></span> | <span data-ttu-id="5df31-113">Zainstaluj tylko ten pakiet, a nie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="5df31-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="5df31-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="5df31-114">ProjectName</span></span> | <span data-ttu-id="5df31-115">Projekt, z którego ma zostać zsynchronizowany pakiet, domyślnie do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="5df31-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="5df31-116">Wersja</span><span class="sxs-lookup"><span data-stu-id="5df31-116">Version</span></span> | <span data-ttu-id="5df31-117">Wersja pakietu do zsynchronizowania, która domyślnie jest aktualnie zainstalowana wersja.</span><span class="sxs-lookup"><span data-stu-id="5df31-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="5df31-118">Source</span><span class="sxs-lookup"><span data-stu-id="5df31-118">Source</span></span> | <span data-ttu-id="5df31-119">Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania.</span><span class="sxs-lookup"><span data-stu-id="5df31-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5df31-120">Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="5df31-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5df31-121">W przypadku pominięcia program `Sync-Package` przeszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="5df31-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5df31-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5df31-122">IncludePrerelease</span></span> | <span data-ttu-id="5df31-123">Obejmuje pakiety wersji wstępnej w synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="5df31-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="5df31-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5df31-124">FileConflictAction</span></span> | <span data-ttu-id="5df31-125">Akcja, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="5df31-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5df31-126">Możliwe wartości to *overwrite, IGNORE, None, OverwriteAll*i *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="5df31-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="5df31-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="5df31-127">DependencyVersion</span></span> | <span data-ttu-id="5df31-128">Wersja pakietów zależności do użycia, która może być jedną z następujących:</span><span class="sxs-lookup"><span data-stu-id="5df31-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="5df31-129">*Najniższy* (domyślnie): najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="5df31-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="5df31-130">*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="5df31-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="5df31-131">*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="5df31-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="5df31-132">*Najwyższa* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="5df31-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="5df31-133">Możesz ustawić wartość domyślną przy użyciu [`dependencyVersion`](../nuget-config-file.md#config-section) ustawienia `Nuget.Config` w pliku.</span><span class="sxs-lookup"><span data-stu-id="5df31-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="5df31-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="5df31-134">WhatIf</span></span> | <span data-ttu-id="5df31-135">Pokazuje, co się stanie po uruchomieniu polecenia bez przeprowadzania synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="5df31-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="5df31-136">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="5df31-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5df31-137">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="5df31-137">Common Parameters</span></span>

<span data-ttu-id="5df31-138">`Sync-Package`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5df31-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5df31-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5df31-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
