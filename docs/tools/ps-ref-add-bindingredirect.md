---
title: Dokumentacja programu PowerShell NuGet BindingRedirect
description: Dokumentacja poleceń programu PowerShell Dodaj BindingRedirect w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842539"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="09875-103">Add-BindingRedirect (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="09875-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="09875-104">*Dostępne tylko w obrębie [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows.*</span><span class="sxs-lookup"><span data-stu-id="09875-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="09875-105">Sprawdza, czy wszystkie zestawy w ramach ścieżki wyjściowej dla projektu, a następnie dodaje przekierowania powiązań do pliku konfiguracji sieci web lub aplikacji, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="09875-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="09875-106">To polecenie jest wykonywane automatycznie podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="09875-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="09875-107">Aby uzyskać szczegółowe informacje dotyczące powiązania przekierowania i dlaczego są one używane, zobacz [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="09875-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="09875-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="09875-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="09875-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="09875-109">Parameters</span></span>

| <span data-ttu-id="09875-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="09875-110">Parameter</span></span> | <span data-ttu-id="09875-111">Opis</span><span class="sxs-lookup"><span data-stu-id="09875-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09875-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="09875-112">ProjectName</span></span> | <span data-ttu-id="09875-113">(Wymagane) Projekt, do którego chcesz dodać przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="09875-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="09875-114">Sam przełącznik - ProjectName jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="09875-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="09875-115">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="09875-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="09875-116">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="09875-116">Common Parameters</span></span>

<span data-ttu-id="09875-117">`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="09875-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="09875-118">Przykłady</span><span class="sxs-lookup"><span data-stu-id="09875-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```