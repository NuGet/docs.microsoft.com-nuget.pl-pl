---
title: Dokumentacja programu NuGet Get-Project PowerShell
description: Odwołanie do polecenia getproject PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777464"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="c60fb-103">Get-Project (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c60fb-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c60fb-104">*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="c60fb-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c60fb-105">Wyświetla informacje dotyczące domyślnego lub określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="c60fb-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="c60fb-106">`Get-Project` w odniesieniu do obiektu "Visual Studio DTE (środowisko narzędzi programistycznych)" zwraca referent.</span><span class="sxs-lookup"><span data-stu-id="c60fb-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="c60fb-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="c60fb-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c60fb-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="c60fb-108">Parameters</span></span>

| <span data-ttu-id="c60fb-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="c60fb-109">Parameter</span></span> | <span data-ttu-id="c60fb-110">Opis</span><span class="sxs-lookup"><span data-stu-id="c60fb-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c60fb-111">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c60fb-111">Name</span></span> | <span data-ttu-id="c60fb-112">Określa projekt do wyświetlenia, domyślny projekt domyślny wybrany w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="c60fb-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="c60fb-113">Przełącznik-Name jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="c60fb-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="c60fb-114">Wszystko</span><span class="sxs-lookup"><span data-stu-id="c60fb-114">All</span></span> | <span data-ttu-id="c60fb-115">Wyświetla informacje dla każdego projektu w rozwiązaniu; kolejność projektów nie jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="c60fb-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="c60fb-116">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="c60fb-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c60fb-117">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="c60fb-117">Common Parameters</span></span>

<span data-ttu-id="c60fb-118">`Get-Project` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c60fb-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c60fb-119">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c60fb-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```