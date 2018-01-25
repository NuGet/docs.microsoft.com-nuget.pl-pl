---
title: Get projekt NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do polecenia programu GetProject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Get-projektu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb98498d6cc6245c9e22b00eada097b816160aea
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="9edff-104">Get projekt (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9edff-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9edff-105">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="9edff-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9edff-106">Wyświetla informacje o domyślnych lub określony projekt.</span><span class="sxs-lookup"><span data-stu-id="9edff-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="9edff-107">`Get-Project`w szczególności zwraca obiekt obsługujący w obiekt Visual Studio DTE (Development Tools Environment) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="9edff-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="9edff-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="9edff-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9edff-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="9edff-109">Parameters</span></span>

| <span data-ttu-id="9edff-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="9edff-110">Parameter</span></span> | <span data-ttu-id="9edff-111">Opis</span><span class="sxs-lookup"><span data-stu-id="9edff-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9edff-112">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9edff-112">Name</span></span> | <span data-ttu-id="9edff-113">Określa projekt do wyświetlenia, domyślnie używany będzie domyślny projekt wybrany w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="9edff-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="9edff-114">-Name przełącznik jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="9edff-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="9edff-115">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="9edff-115">All</span></span> | <span data-ttu-id="9edff-116">Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="9edff-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="9edff-117">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="9edff-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9edff-118">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="9edff-118">Common Parameters</span></span>

<span data-ttu-id="9edff-119">`Get-Project`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9edff-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9edff-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9edff-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```