---
title: Synchronizacja — pakiet NuGet w programie PowerShell
description: Odwołanie do polecenia programu PowerShell synchronizacji pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="532ae-103">Sync-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="532ae-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="532ae-104">*W wersji 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="532ae-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="532ae-105">Pobiera wersję zainstalowanego pakietu z określony (lub domyślna) projektu i synchronizuje wersję z resztą projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="532ae-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="532ae-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="532ae-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="532ae-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="532ae-107">Parameters</span></span>

| <span data-ttu-id="532ae-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="532ae-108">Parameter</span></span> | <span data-ttu-id="532ae-109">Opis</span><span class="sxs-lookup"><span data-stu-id="532ae-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="532ae-110">Id</span><span class="sxs-lookup"><span data-stu-id="532ae-110">Id</span></span> | <span data-ttu-id="532ae-111">(Wymagane) Identyfikator pakietu do synchronizacji. Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="532ae-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="532ae-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="532ae-112">IgnoreDependencies</span></span> | <span data-ttu-id="532ae-113">Zainstaluj tylko ten pakiet, bez jego zależności.</span><span class="sxs-lookup"><span data-stu-id="532ae-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="532ae-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="532ae-114">ProjectName</span></span> | <span data-ttu-id="532ae-115">Projekt do zsynchronizowania pakietu, domyślnie używany do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="532ae-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="532ae-116">Wersja</span><span class="sxs-lookup"><span data-stu-id="532ae-116">Version</span></span> | <span data-ttu-id="532ae-117">Wersja pakietu do synchronizacji, w obecnie zainstalowanej wersji przyjęto wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="532ae-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="532ae-118">Źródło</span><span class="sxs-lookup"><span data-stu-id="532ae-118">Source</span></span> | <span data-ttu-id="532ae-119">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="532ae-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="532ae-120">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="532ae-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="532ae-121">Pominięcie `Sync-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="532ae-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="532ae-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="532ae-122">IncludePrerelease</span></span> | <span data-ttu-id="532ae-123">Zawiera pakiety wersji wstępnej synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="532ae-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="532ae-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="532ae-124">FileConflictAction</span></span> | <span data-ttu-id="532ae-125">Akcja wykonywana po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="532ae-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="532ae-126">Możliwe wartości to *zastępowania, Ignoruj, brak OverwriteAll*, i *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="532ae-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="532ae-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="532ae-127">DependencyVersion</span></span> | <span data-ttu-id="532ae-128">Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="532ae-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="532ae-129">*Najniższa* (domyślnie): Najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="532ae-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="532ae-130">*HighestPatch*: wersja z najniższą głównych, najniższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="532ae-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="532ae-131">*HighestMinor*: wersja z najniższą głównych, najwyższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="532ae-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="532ae-132">*Najwyższy* (domyślnie pakiet aktualizacji bez parametrów): najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="532ae-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="532ae-133">Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="532ae-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="532ae-134">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="532ae-134">WhatIf</span></span> | <span data-ttu-id="532ae-135">Pokazuje, co się stanie po uruchomieniu polecenia bez rzeczywistego wykonania synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="532ae-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="532ae-136">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="532ae-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="532ae-137">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="532ae-137">Common Parameters</span></span>

<span data-ttu-id="532ae-138">`Sync-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="532ae-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="532ae-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="532ae-139">Examples</span></span>

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
