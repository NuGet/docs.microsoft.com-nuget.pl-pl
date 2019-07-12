---
title: Dokumentacja programu PowerShell Get projekt NuGet
description: Dokumentacja poleceń programu GetProject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842283"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="35027-103">Get-Project (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="35027-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="35027-104">*Dostępne tylko w obrębie [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows.*</span><span class="sxs-lookup"><span data-stu-id="35027-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="35027-105">Wyświetla informacje o domyślnej lub określony projekt.</span><span class="sxs-lookup"><span data-stu-id="35027-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="35027-106">`Get-Project` w szczególności zwraca obiekt obsługujący obiektowi Visual Studio DTE (środowisko programistyczne narzędzia) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="35027-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="35027-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="35027-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="35027-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="35027-108">Parameters</span></span>

| <span data-ttu-id="35027-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="35027-109">Parameter</span></span> | <span data-ttu-id="35027-110">Opis</span><span class="sxs-lookup"><span data-stu-id="35027-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="35027-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="35027-111">Name</span></span> | <span data-ttu-id="35027-112">Określa projekt do wyświetlenia, domyślnie używany będzie domyślny projekt wybrany w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="35027-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="35027-113">— Nazwa przełącznika jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="35027-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="35027-114">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="35027-114">All</span></span> | <span data-ttu-id="35027-115">Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="35027-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="35027-116">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="35027-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="35027-117">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="35027-117">Common Parameters</span></span>

<span data-ttu-id="35027-118">`Get-Project` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="35027-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="35027-119">Przykłady</span><span class="sxs-lookup"><span data-stu-id="35027-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```