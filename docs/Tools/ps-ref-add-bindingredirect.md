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
ms.openlocfilehash: 41f27d7a1b6b363a562f26590b220d9e11e944f1
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="fc61c-104">Dodaj BindingRedirect (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fc61c-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fc61c-105">*Dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="fc61c-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fc61c-106">Sprawdza wszystkie zestawy w ścieżce wyjściowej dla projektu i dodaje przekierowania powiązania do pliku konfiguracji aplikacji lub sieci web, w miarę potrzeby.</span><span class="sxs-lookup"><span data-stu-id="fc61c-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="fc61c-107">To polecenie jest uruchamiane automatycznie podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="fc61c-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="fc61c-108">Aby uzyskać szczegółowe informacje na powiązanie przekierowania i dlaczego ich użycia, zobacz [przekierowywanie wersji zestawu](/dotnet/framework/configure-apps/redirect-assembly-versions) w dokumentacji programu .NET.</span><span class="sxs-lookup"><span data-stu-id="fc61c-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="fc61c-109">Składnia</span><span class="sxs-lookup"><span data-stu-id="fc61c-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="fc61c-110">Parametry</span><span class="sxs-lookup"><span data-stu-id="fc61c-110">Parameters</span></span>

| <span data-ttu-id="fc61c-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="fc61c-111">Parameter</span></span> | <span data-ttu-id="fc61c-112">Opis</span><span class="sxs-lookup"><span data-stu-id="fc61c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fc61c-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="fc61c-113">ProjectName</span></span> | <span data-ttu-id="fc61c-114">(Wymagane) Projekt, do którego mają zostać dodane przekierowania wiązań.</span><span class="sxs-lookup"><span data-stu-id="fc61c-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="fc61c-115">Przełącznika - NazwaProjektu sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="fc61c-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="fc61c-116">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="fc61c-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fc61c-117">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="fc61c-117">Common Parameters</span></span>

<span data-ttu-id="fc61c-118">`Add-BindingRedirect` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fc61c-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fc61c-119">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fc61c-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```