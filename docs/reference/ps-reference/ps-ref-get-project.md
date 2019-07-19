---
title: Dokumentacja pakietu NuGet Get-Project PowerShell
description: Odwołanie do polecenia getproject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328211"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="5886a-103">Get-Project (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5886a-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5886a-104">*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="5886a-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5886a-105">Wyświetla informacje dotyczące domyślnego lub określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="5886a-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="5886a-106">`Get-Project`w odniesieniu do obiektu "Visual Studio DTE (środowisko narzędzi programistycznych)" zwraca referent.</span><span class="sxs-lookup"><span data-stu-id="5886a-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="5886a-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="5886a-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5886a-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="5886a-108">Parameters</span></span>

| <span data-ttu-id="5886a-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="5886a-109">Parameter</span></span> | <span data-ttu-id="5886a-110">Opis</span><span class="sxs-lookup"><span data-stu-id="5886a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5886a-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5886a-111">Name</span></span> | <span data-ttu-id="5886a-112">Określa projekt do wyświetlenia, domyślny projekt domyślny wybrany w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5886a-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="5886a-113">Przełącznik-Name jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="5886a-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="5886a-114">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="5886a-114">All</span></span> | <span data-ttu-id="5886a-115">Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="5886a-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="5886a-116">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="5886a-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5886a-117">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="5886a-117">Common Parameters</span></span>

<span data-ttu-id="5886a-118">`Get-Project`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5886a-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5886a-119">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5886a-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```