---
title: Dokumentacja programu PowerShell synchronizacji — pakiet NuGet
description: Dokumentacja poleceń programu PowerShell synchronizacji pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842249"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b5b6b-103">Sync-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b5b6b-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b5b6b-104">*W wersji 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows.*</span><span class="sxs-lookup"><span data-stu-id="b5b6b-104">*Version 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b5b6b-105">Pobiera wersję zainstalowanego pakietu z określony (lub domyślny) projektu i synchronizuje wersji w pozostałej części projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="b5b6b-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="b5b6b-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b5b6b-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="b5b6b-107">Parameters</span></span>

| <span data-ttu-id="b5b6b-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="b5b6b-108">Parameter</span></span> | <span data-ttu-id="b5b6b-109">Opis</span><span class="sxs-lookup"><span data-stu-id="b5b6b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b5b6b-110">Id</span><span class="sxs-lookup"><span data-stu-id="b5b6b-110">Id</span></span> | <span data-ttu-id="b5b6b-111">(Wymagane) Identyfikator pakietu do synchronizacji. — Identyfikator samym przełączniku jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b5b6b-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="b5b6b-112">IgnoreDependencies</span></span> | <span data-ttu-id="b5b6b-113">Zainstaluj tylko ten pakiet, a nie z jego zależności.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="b5b6b-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b5b6b-114">ProjectName</span></span> | <span data-ttu-id="b5b6b-115">Projekt, aby zsynchronizować pakiet, domyślnie używany będzie domyślny projekt.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="b5b6b-116">Wersja</span><span class="sxs-lookup"><span data-stu-id="b5b6b-116">Version</span></span> | <span data-ttu-id="b5b6b-117">Wersja pakietu do synchronizacji, przyjęty obecnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="b5b6b-118">Source</span><span class="sxs-lookup"><span data-stu-id="b5b6b-118">Source</span></span> | <span data-ttu-id="b5b6b-119">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="b5b6b-120">Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="b5b6b-121">W przypadku pominięcia `Sync-Package` przeszukuje źródło obecnie wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="b5b6b-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="b5b6b-122">IncludePrerelease</span></span> | <span data-ttu-id="b5b6b-123">Obejmuje pakiety w wersjach wstępnych podczas synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="b5b6b-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="b5b6b-124">FileConflictAction</span></span> | <span data-ttu-id="b5b6b-125">Akcja do wykonania po wyświetleniu monitu o zastąpienie lub zignorować istniejące pliki przywoływanego przez projekt.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="b5b6b-126">Możliwe wartości to *zastąpienia, Zignoruj, None, OverwriteAll*, i *(3.0 i nowsze)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="b5b6b-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="b5b6b-127">DependencyVersion</span></span> | <span data-ttu-id="b5b6b-128">Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="b5b6b-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="b5b6b-129">*Najniższy* (ustawienie domyślne): Najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="b5b6b-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="b5b6b-130">*HighestPatch*: wersja przy najniższe główne, najniższą pomocnicza, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="b5b6b-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="b5b6b-131">*HighestMinor*: wersji z najniższą główne, najwyższy pomocnicza, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="b5b6b-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="b5b6b-132">*Najwyższy* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="b5b6b-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="b5b6b-133">Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ustawienie w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="b5b6b-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="b5b6b-134">WhatIf</span></span> | <span data-ttu-id="b5b6b-135">Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="b5b6b-136">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b5b6b-137">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="b5b6b-137">Common Parameters</span></span>

<span data-ttu-id="b5b6b-138">`Sync-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b5b6b-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b5b6b-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="b5b6b-139">Examples</span></span>

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
