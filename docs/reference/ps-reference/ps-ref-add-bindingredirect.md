---
title: Dokumentacja programu PowerShell Add-BindingRedirect
description: Dokumentacja polecenia Add-BindingRedirect środowiska PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328241"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="e6c53-103">Add-BindingRedirect (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e6c53-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e6c53-104">*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="e6c53-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e6c53-105">Bada wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do pliku konfiguracji aplikacji lub sieci Web, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e6c53-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="e6c53-106">To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="e6c53-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="e6c53-107">Aby uzyskać szczegółowe informacje o przekierowaniach powiązań i o tym, dlaczego są używane, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.</span><span class="sxs-lookup"><span data-stu-id="e6c53-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="e6c53-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="e6c53-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e6c53-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="e6c53-109">Parameters</span></span>

| <span data-ttu-id="e6c53-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="e6c53-110">Parameter</span></span> | <span data-ttu-id="e6c53-111">Opis</span><span class="sxs-lookup"><span data-stu-id="e6c53-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e6c53-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e6c53-112">ProjectName</span></span> | <span data-ttu-id="e6c53-113">Potrzeb Projekt, do którego mają zostać dodane przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="e6c53-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="e6c53-114">Przełącznik-ProjectName jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="e6c53-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="e6c53-115">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="e6c53-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e6c53-116">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="e6c53-116">Common Parameters</span></span>

<span data-ttu-id="e6c53-117">`Add-BindingRedirect`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e6c53-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e6c53-118">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e6c53-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```