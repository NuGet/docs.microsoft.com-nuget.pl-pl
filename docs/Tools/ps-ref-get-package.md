---
title: Get pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Dokumentacja dotycząca polecenia PowerShell Get-pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Pobierz pakiet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c38e0da2e98d2e5bf5b4fc165462e9abcfdd73c0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3c1d7-104">Get-Package (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3c1d7-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3c1d7-105">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia PowerShell Get-Package, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3c1d7-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3c1d7-106">Pobiera listę pakietów zainstalowanych w lokalnym repozytorium, zawiera listę pakietów dostępnych ze źródła pakietu, gdy jest używany z flagą - ListAvailable przełącznika lub wymieniono dostępne aktualizacje, gdy jest używany z przełącznikiem - Update.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="3c1d7-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="3c1d7-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="3c1d7-108">Bez parametrów `Get-Package` Wyświetla listę pakietów zainstalowanych w projekcie domyślnym.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="3c1d7-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="3c1d7-109">Parameters</span></span>

| <span data-ttu-id="3c1d7-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="3c1d7-110">Parameter</span></span> | <span data-ttu-id="3c1d7-111">Opis</span><span class="sxs-lookup"><span data-stu-id="3c1d7-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c1d7-112">Źródło</span><span class="sxs-lookup"><span data-stu-id="3c1d7-112">Source</span></span> | <span data-ttu-id="3c1d7-113">Ścieżka adresu URL lub folderu pakietu.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-113">The URL or folder path for the package .</span></span> <span data-ttu-id="3c1d7-114">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3c1d7-115">Pominięcie `Get-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="3c1d7-116">W przypadku korzystania z flagą-ListAvailable, wartość domyślna to nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="3c1d7-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="3c1d7-117">ListAvailable</span></span> | <span data-ttu-id="3c1d7-118">Wyświetla listę dostępnych pakietów ze źródła pakietu przyjęty nuget.org. Pokazuje domyślnie 50 pakietów, chyba że określono - PageSize i/lub - pierwszy.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="3c1d7-119">Aktualizacje</span><span class="sxs-lookup"><span data-stu-id="3c1d7-119">Updates</span></span> | <span data-ttu-id="3c1d7-120">Wyświetla listę pakietów, które mają jest dostępna aktualizacja w źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="3c1d7-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="3c1d7-121">ProjectName</span></span> | <span data-ttu-id="3c1d7-122">Projekt, z którego ma zostać pobrane zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-122">The project from which to get installed packages.</span></span> <span data-ttu-id="3c1d7-123">Pominięcie zwraca zainstalowane projekty dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="3c1d7-124">Filtr</span><span class="sxs-lookup"><span data-stu-id="3c1d7-124">Filter</span></span> | <span data-ttu-id="3c1d7-125">Ciąg filtru używany do zawężania listy pakietów, uwzględniając identyfikator pakietu, opisie i tagach.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="3c1d7-126">pierwszy</span><span class="sxs-lookup"><span data-stu-id="3c1d7-126">First</span></span> | <span data-ttu-id="3c1d7-127">Liczba pakietów do zwrócenia z początku listy.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="3c1d7-128">Jeśli nie zostanie określony, domyślnie 50.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="3c1d7-129">Skip</span><span class="sxs-lookup"><span data-stu-id="3c1d7-129">Skip</span></span> | <span data-ttu-id="3c1d7-130">Pominięto pierwszy &lt;int&gt; pakiety z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="3c1d7-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3c1d7-131">AllVersions</span></span> | <span data-ttu-id="3c1d7-132">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="3c1d7-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3c1d7-133">IncludePrerelease</span></span> | <span data-ttu-id="3c1d7-134">Zawiera pakiety wersji wstępnej w wynikach.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="3c1d7-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="3c1d7-135">PageSize</span></span> | <span data-ttu-id="3c1d7-136">*(3.0 +)*  Podczas używane z flagą-ListAvailable (wymagane), liczba pakietów, aby wyświetlić listę przed przekazaniem wiersza, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="3c1d7-137">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3c1d7-138">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="3c1d7-138">Common Parameters</span></span>

<span data-ttu-id="3c1d7-139">`Get-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3c1d7-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3c1d7-140">Przykłady</span><span class="sxs-lookup"><span data-stu-id="3c1d7-140">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
