---
title: "Synchronizacja — pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do polecenia programu PowerShell synchronizacji pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, pakiet synchronizacji"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="6784f-104">Synchronizacja — pakiet (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6784f-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6784f-105">*W wersji 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="6784f-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6784f-106">Pobiera wersję zainstalowanego pakietu z określony (lub domyślna) projektu i synchronizuje wersję z resztą projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="6784f-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="6784f-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="6784f-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6784f-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="6784f-108">Parameters</span></span>

| <span data-ttu-id="6784f-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="6784f-109">Parameter</span></span> | <span data-ttu-id="6784f-110">Opis</span><span class="sxs-lookup"><span data-stu-id="6784f-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6784f-111">Id</span><span class="sxs-lookup"><span data-stu-id="6784f-111">Id</span></span> | <span data-ttu-id="6784f-112">(Wymagane) Identyfikator pakietu do synchronizacji. Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="6784f-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="6784f-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="6784f-113">IgnoreDependencies</span></span> | <span data-ttu-id="6784f-114">Zainstaluj tylko ten pakiet, bez jego zależności.</span><span class="sxs-lookup"><span data-stu-id="6784f-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="6784f-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="6784f-115">ProjectName</span></span> | <span data-ttu-id="6784f-116">Projekt do zsynchronizowania pakietu, domyślnie używany do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="6784f-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="6784f-117">Wersja</span><span class="sxs-lookup"><span data-stu-id="6784f-117">Version</span></span> | <span data-ttu-id="6784f-118">Wersja pakietu do synchronizacji, w obecnie zainstalowanej wersji przyjęto wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="6784f-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="6784f-119">Źródło</span><span class="sxs-lookup"><span data-stu-id="6784f-119">Source</span></span> | <span data-ttu-id="6784f-120">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="6784f-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="6784f-121">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="6784f-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="6784f-122">Pominięcie `Sync-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="6784f-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="6784f-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="6784f-123">IncludePrerelease</span></span> | <span data-ttu-id="6784f-124">Zawiera pakiety wersji wstępnej synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="6784f-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="6784f-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="6784f-125">FileConflictAction</span></span> | <span data-ttu-id="6784f-126">Akcja wykonywana po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="6784f-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="6784f-127">Możliwe wartości to *zastępowania, Ignoruj, brak OverwriteAll*, i *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="6784f-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="6784f-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="6784f-128">DependencyVersion</span></span> | <span data-ttu-id="6784f-129">Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6784f-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="6784f-130">*Najniższa* (domyślnie): Najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="6784f-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="6784f-131">*HighestPatch*: wersja z najniższą głównych, najniższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="6784f-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="6784f-132">*HighestMinor*: wersja z najniższą głównych, najwyższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="6784f-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="6784f-133">*Najwyższy* (domyślnie pakiet aktualizacji bez parametrów): najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="6784f-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="6784f-134">Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="6784f-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="6784f-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="6784f-135">WhatIf</span></span> | <span data-ttu-id="6784f-136">Pokazuje, co się stanie po uruchomieniu polecenia bez rzeczywistego wykonania synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="6784f-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="6784f-137">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="6784f-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6784f-138">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="6784f-138">Common Parameters</span></span>

<span data-ttu-id="6784f-139">`Sync-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6784f-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6784f-140">Przykłady</span><span class="sxs-lookup"><span data-stu-id="6784f-140">Examples</span></span>

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
