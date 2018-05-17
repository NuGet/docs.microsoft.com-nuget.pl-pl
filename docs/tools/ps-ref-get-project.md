---
title: Get projekt NuGet w programie PowerShell
description: Odwołanie do polecenia programu GetProject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="7e9e8-103">Get-Project (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7e9e8-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7e9e8-104">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="7e9e8-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7e9e8-105">Wyświetla informacje o domyślnych lub określony projekt.</span><span class="sxs-lookup"><span data-stu-id="7e9e8-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="7e9e8-106">`Get-Project` w szczególności zwraca obiekt obsługujący w obiekt Visual Studio DTE (Development Tools Environment) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="7e9e8-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="7e9e8-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="7e9e8-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7e9e8-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="7e9e8-108">Parameters</span></span>

| <span data-ttu-id="7e9e8-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="7e9e8-109">Parameter</span></span> | <span data-ttu-id="7e9e8-110">Opis</span><span class="sxs-lookup"><span data-stu-id="7e9e8-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e9e8-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7e9e8-111">Name</span></span> | <span data-ttu-id="7e9e8-112">Określa projekt do wyświetlenia, domyślnie używany będzie domyślny projekt wybrany w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="7e9e8-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="7e9e8-113">-Name przełącznik jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7e9e8-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="7e9e8-114">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="7e9e8-114">All</span></span> | <span data-ttu-id="7e9e8-115">Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="7e9e8-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="7e9e8-116">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="7e9e8-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7e9e8-117">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="7e9e8-117">Common Parameters</span></span>

<span data-ttu-id="7e9e8-118">`Get-Project` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7e9e8-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7e9e8-119">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7e9e8-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```