---
title: Dokumentacja programu PowerShell Add-BindingRedirect
description: Dokumentacja polecenia Add-BindingRedirect środowiska PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623126"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="4f6a6-103">Add-BindingRedirect (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4f6a6-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4f6a6-104">*Dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="4f6a6-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4f6a6-105">Bada wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do pliku konfiguracji aplikacji lub sieci Web, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="4f6a6-106">To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="4f6a6-107">Dotyczy to tylko scenariuszy korzystających z pliku packages.config.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="4f6a6-108">Aby uzyskać więcej informacji, zobacz [Dokumentacja pliku packages.config NuGet](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="4f6a6-109">Aby uzyskać szczegółowe informacje o przekierowaniach powiązań i o tym, dlaczego są używane, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="4f6a6-110">Składnia</span><span class="sxs-lookup"><span data-stu-id="4f6a6-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4f6a6-111">Parametry</span><span class="sxs-lookup"><span data-stu-id="4f6a6-111">Parameters</span></span>

| <span data-ttu-id="4f6a6-112">Parametr</span><span class="sxs-lookup"><span data-stu-id="4f6a6-112">Parameter</span></span> | <span data-ttu-id="4f6a6-113">Opis</span><span class="sxs-lookup"><span data-stu-id="4f6a6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f6a6-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4f6a6-114">ProjectName</span></span> | <span data-ttu-id="4f6a6-115">Potrzeb Projekt, do którego mają zostać dodane przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="4f6a6-116">Przełącznik-ProjectName jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="4f6a6-117">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4f6a6-118">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="4f6a6-118">Common Parameters</span></span>

<span data-ttu-id="4f6a6-119">`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4f6a6-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4f6a6-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
