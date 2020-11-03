---
title: Dokumentacja programu NuGet Add-BindingRedirect PowerShell
description: Informacje dotyczące Add-BindingRedirect polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237260"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="4d5f4-103">Add-BindingRedirect (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4d5f4-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4d5f4-104">*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="4d5f4-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4d5f4-105">Bada wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do pliku konfiguracji aplikacji lub sieci Web, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="4d5f4-106">To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="4d5f4-107">Dotyczy to tylko scenariuszy korzystających z pliku packages.config.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="4d5f4-108">Aby uzyskać więcej informacji, zobacz [Dokumentacja pliku packages.config NuGet](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="4d5f4-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="4d5f4-109">Aby uzyskać szczegółowe informacje o przekierowaniach powiązań i o tym, dlaczego są używane, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d5f4-110">Składnia</span><span class="sxs-lookup"><span data-stu-id="4d5f4-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4d5f4-111">Parametry</span><span class="sxs-lookup"><span data-stu-id="4d5f4-111">Parameters</span></span>

| <span data-ttu-id="4d5f4-112">Parametr</span><span class="sxs-lookup"><span data-stu-id="4d5f4-112">Parameter</span></span> | <span data-ttu-id="4d5f4-113">Opis</span><span class="sxs-lookup"><span data-stu-id="4d5f4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d5f4-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4d5f4-114">ProjectName</span></span> | <span data-ttu-id="4d5f4-115">Potrzeb Projekt, do którego mają zostać dodane przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="4d5f4-116">Przełącznik-ProjectName jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="4d5f4-117">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4d5f4-118">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="4d5f4-118">Common Parameters</span></span>

<span data-ttu-id="4d5f4-119">`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4d5f4-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4d5f4-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4d5f4-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```