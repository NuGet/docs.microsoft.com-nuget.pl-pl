---
title: Get projekt NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Odwołanie do polecenia programu GetProject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
keywords: NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Get-projektu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="01fd0-104">Get projekt (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="01fd0-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="01fd0-105">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="01fd0-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="01fd0-106">Wyświetla informacje o domyślnych lub określony projekt.</span><span class="sxs-lookup"><span data-stu-id="01fd0-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="01fd0-107">`Get-Project` w szczególności zwraca obiekt obsługujący w obiekt Visual Studio DTE (Development Tools Environment) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="01fd0-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="01fd0-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="01fd0-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="01fd0-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="01fd0-109">Parameters</span></span>

| <span data-ttu-id="01fd0-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="01fd0-110">Parameter</span></span> | <span data-ttu-id="01fd0-111">Opis</span><span class="sxs-lookup"><span data-stu-id="01fd0-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="01fd0-112">Nazwa</span><span class="sxs-lookup"><span data-stu-id="01fd0-112">Name</span></span> | <span data-ttu-id="01fd0-113">Określa projekt do wyświetlenia, domyślnie używany będzie domyślny projekt wybrany w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="01fd0-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="01fd0-114">-Name przełącznik jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="01fd0-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="01fd0-115">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="01fd0-115">All</span></span> | <span data-ttu-id="01fd0-116">Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="01fd0-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="01fd0-117">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="01fd0-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="01fd0-118">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="01fd0-118">Common Parameters</span></span>

<span data-ttu-id="01fd0-119">`Get-Project` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="01fd0-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="01fd0-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="01fd0-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```