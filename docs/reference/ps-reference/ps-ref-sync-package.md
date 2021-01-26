---
title: Dokumentacja programu NuGet Sync-Package PowerShell
description: Informacje dotyczące Sync-Package polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 4261b0a20a4fd4183f7b08096c3477e6f9d0a02d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777403"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="0d824-103">Sync-Package (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0d824-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0d824-104">*Wersja 3.0 +; dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="0d824-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0d824-105">Pobiera wersję zainstalowanego pakietu z określonego (lub domyślnego) projektu i synchronizuje wersję do pozostałych projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="0d824-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="0d824-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="0d824-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0d824-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="0d824-107">Parameters</span></span>

| <span data-ttu-id="0d824-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="0d824-108">Parameter</span></span> | <span data-ttu-id="0d824-109">Opis</span><span class="sxs-lookup"><span data-stu-id="0d824-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0d824-110">Id</span><span class="sxs-lookup"><span data-stu-id="0d824-110">Id</span></span> | <span data-ttu-id="0d824-111">Potrzeb Identyfikator pakietu do zsynchronizowania. Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0d824-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="0d824-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="0d824-112">IgnoreDependencies</span></span> | <span data-ttu-id="0d824-113">Zainstaluj tylko ten pakiet, a nie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="0d824-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="0d824-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="0d824-114">ProjectName</span></span> | <span data-ttu-id="0d824-115">Projekt, z którego ma zostać zsynchronizowany pakiet, domyślnie do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="0d824-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="0d824-116">Wersja</span><span class="sxs-lookup"><span data-stu-id="0d824-116">Version</span></span> | <span data-ttu-id="0d824-117">Wersja pakietu do zsynchronizowania, która domyślnie jest aktualnie zainstalowana wersja.</span><span class="sxs-lookup"><span data-stu-id="0d824-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="0d824-118">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="0d824-118">Source</span></span> | <span data-ttu-id="0d824-119">Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania.</span><span class="sxs-lookup"><span data-stu-id="0d824-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="0d824-120">Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="0d824-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="0d824-121">W przypadku pominięcia program `Sync-Package` przeszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="0d824-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="0d824-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="0d824-122">IncludePrerelease</span></span> | <span data-ttu-id="0d824-123">Obejmuje pakiety wersji wstępnej w synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="0d824-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="0d824-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="0d824-124">FileConflictAction</span></span> | <span data-ttu-id="0d824-125">Akcja, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="0d824-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="0d824-126">Możliwe wartości to *overwrite, IGNORE, None, OverwriteAll* i *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="0d824-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="0d824-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="0d824-127">DependencyVersion</span></span> | <span data-ttu-id="0d824-128">Wersja pakietów zależności do użycia, która może być jedną z następujących:</span><span class="sxs-lookup"><span data-stu-id="0d824-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="0d824-129">*Najniższy* (domyślny): najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="0d824-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="0d824-130">*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="0d824-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="0d824-131">*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="0d824-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="0d824-132">*Najwyższe* (domyślnie dla Update-Package bez parametrów): najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="0d824-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="0d824-133">Możesz ustawić wartość domyślną przy użyciu [`dependencyVersion`](../nuget-config-file.md#config-section) Ustawienia w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="0d824-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="0d824-134">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="0d824-134">WhatIf</span></span> | <span data-ttu-id="0d824-135">Pokazuje, co się stanie po uruchomieniu polecenia bez przeprowadzania synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="0d824-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="0d824-136">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="0d824-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0d824-137">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="0d824-137">Common Parameters</span></span>

<span data-ttu-id="0d824-138">`Sync-Package` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0d824-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0d824-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0d824-139">Examples</span></span>

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