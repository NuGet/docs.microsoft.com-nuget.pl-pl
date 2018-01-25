---
title: NuGet BindingRedirect w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do polecenia programu PowerShell Dodaj BindingRedirect w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Dodaj BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b755970402f29a72b9a10f1a94e4a799e9cb71cf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="932ee-104">Dodaj BindingRedirect (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="932ee-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="932ee-105">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="932ee-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="932ee-106">Sprawdza wszystkie zestawy w ścieżce wyjściowej dla projektu i dodaje przekierowania powiązania do pliku konfiguracji aplikacji lub sieci web, w miarę potrzeby.</span><span class="sxs-lookup"><span data-stu-id="932ee-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="932ee-107">To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="932ee-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="932ee-108">Aby uzyskać szczegółowe informacje na powiązanie przekierowania i dlaczego ich użycia, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.</span><span class="sxs-lookup"><span data-stu-id="932ee-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="932ee-109">Składnia</span><span class="sxs-lookup"><span data-stu-id="932ee-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="932ee-110">Parametry</span><span class="sxs-lookup"><span data-stu-id="932ee-110">Parameters</span></span>

| <span data-ttu-id="932ee-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="932ee-111">Parameter</span></span> | <span data-ttu-id="932ee-112">Opis</span><span class="sxs-lookup"><span data-stu-id="932ee-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="932ee-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="932ee-113">ProjectName</span></span> | <span data-ttu-id="932ee-114">(Wymagane) Projekt, do którego mają zostać dodane przekierowania wiązań.</span><span class="sxs-lookup"><span data-stu-id="932ee-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="932ee-115">Przełącznika - NazwaProjektu sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="932ee-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="932ee-116">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="932ee-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="932ee-117">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="932ee-117">Common Parameters</span></span>

<span data-ttu-id="932ee-118">`Add-BindingRedirect`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="932ee-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="932ee-119">Przykłady</span><span class="sxs-lookup"><span data-stu-id="932ee-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```