---
title: NuGet BindingRedirect w programie PowerShell
description: Odwołanie do polecenia programu PowerShell Dodaj BindingRedirect w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817626"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="4b8ad-103">Add-BindingRedirect (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4b8ad-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4b8ad-104">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="4b8ad-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4b8ad-105">Sprawdza wszystkie zestawy w ścieżce wyjściowej dla projektu i dodaje przekierowania powiązania do pliku konfiguracji aplikacji lub sieci web, w miarę potrzeby.</span><span class="sxs-lookup"><span data-stu-id="4b8ad-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="4b8ad-106">To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="4b8ad-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="4b8ad-107">Aby uzyskać szczegółowe informacje na powiązanie przekierowania i dlaczego ich użycia, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.</span><span class="sxs-lookup"><span data-stu-id="4b8ad-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="4b8ad-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="4b8ad-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4b8ad-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="4b8ad-109">Parameters</span></span>

| <span data-ttu-id="4b8ad-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="4b8ad-110">Parameter</span></span> | <span data-ttu-id="4b8ad-111">Opis</span><span class="sxs-lookup"><span data-stu-id="4b8ad-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b8ad-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4b8ad-112">ProjectName</span></span> | <span data-ttu-id="4b8ad-113">(Wymagane) Projekt, do którego mają zostać dodane przekierowania wiązań.</span><span class="sxs-lookup"><span data-stu-id="4b8ad-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="4b8ad-114">Przełącznika - NazwaProjektu sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="4b8ad-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="4b8ad-115">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="4b8ad-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4b8ad-116">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="4b8ad-116">Common Parameters</span></span>

<span data-ttu-id="4b8ad-117">`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4b8ad-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4b8ad-118">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4b8ad-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```