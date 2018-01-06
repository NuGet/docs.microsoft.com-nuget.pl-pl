---
title: Get pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: "Dokumentacja dotycząca polecenia PowerShell Get-pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Pobierz pakiet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 632936fe4dd9736f7c3740a2f763173dc725424a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e78ba-104">Get-Package (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e78ba-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e78ba-105">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia PowerShell Get-Package, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e78ba-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e78ba-106">Pobiera listę pakietów zainstalowanych w lokalnym repozytorium, zawiera listę pakietów dostępnych ze źródła pakietu, gdy jest używany z flagą - ListAvailable przełącznika lub wymieniono dostępne aktualizacje, gdy jest używany z przełącznikiem - Update.</span><span class="sxs-lookup"><span data-stu-id="e78ba-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="e78ba-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="e78ba-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="e78ba-108">Bez parametrów `Get-Package` Wyświetla listę pakietów zainstalowanych w projekcie domyślnym.</span><span class="sxs-lookup"><span data-stu-id="e78ba-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="e78ba-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="e78ba-109">Parameters</span></span>

| <span data-ttu-id="e78ba-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="e78ba-110">Parameter</span></span> | <span data-ttu-id="e78ba-111">Opis</span><span class="sxs-lookup"><span data-stu-id="e78ba-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78ba-112">Źródło</span><span class="sxs-lookup"><span data-stu-id="e78ba-112">Source</span></span> | <span data-ttu-id="e78ba-113">Ścieżka adresu URL lub folderu pakietu.</span><span class="sxs-lookup"><span data-stu-id="e78ba-113">The URL or folder path for the package .</span></span> <span data-ttu-id="e78ba-114">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="e78ba-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e78ba-115">Pominięcie `Get-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="e78ba-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="e78ba-116">W przypadku korzystania z flagą-ListAvailable, wartość domyślna to nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e78ba-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="e78ba-117">Flagą ListAvailable</span><span class="sxs-lookup"><span data-stu-id="e78ba-117">ListAvailable</span></span> | <span data-ttu-id="e78ba-118">Wyświetla listę dostępnych pakietów ze źródła pakietu przyjęty nuget.org. Pokazuje domyślnie 50 pakietów, chyba że określono - PageSize i/lub - pierwszy.</span><span class="sxs-lookup"><span data-stu-id="e78ba-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="e78ba-119">Aktualizacje</span><span class="sxs-lookup"><span data-stu-id="e78ba-119">Updates</span></span> | <span data-ttu-id="e78ba-120">Wyświetla listę pakietów, które mają jest dostępna aktualizacja w źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="e78ba-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="e78ba-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e78ba-121">ProjectName</span></span> | <span data-ttu-id="e78ba-122">Projekt, z którego ma zostać pobrane zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="e78ba-122">The project from which to get installed packages.</span></span> <span data-ttu-id="e78ba-123">Pominięcie zwraca zainstalowane projekty dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e78ba-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="e78ba-124">Filtr</span><span class="sxs-lookup"><span data-stu-id="e78ba-124">Filter</span></span> | <span data-ttu-id="e78ba-125">Ciąg filtru używany do zawężania listy pakietów, uwzględniając identyfikator pakietu, opisie i tagach.</span><span class="sxs-lookup"><span data-stu-id="e78ba-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="e78ba-126">pierwszy</span><span class="sxs-lookup"><span data-stu-id="e78ba-126">First</span></span> | <span data-ttu-id="e78ba-127">Liczba pakietów do zwrócenia z początku listy.</span><span class="sxs-lookup"><span data-stu-id="e78ba-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="e78ba-128">Jeśli nie zostanie określony, domyślnie 50.</span><span class="sxs-lookup"><span data-stu-id="e78ba-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="e78ba-129">Skip</span><span class="sxs-lookup"><span data-stu-id="e78ba-129">Skip</span></span> | <span data-ttu-id="e78ba-130">Pominięto pierwszy &lt;int&gt; pakiety z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="e78ba-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="e78ba-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="e78ba-131">AllVersions</span></span> | <span data-ttu-id="e78ba-132">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="e78ba-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="e78ba-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e78ba-133">IncludePrerelease</span></span> | <span data-ttu-id="e78ba-134">Zawiera pakiety wersji wstępnej w wynikach.</span><span class="sxs-lookup"><span data-stu-id="e78ba-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="e78ba-135">Wartość PageSize</span><span class="sxs-lookup"><span data-stu-id="e78ba-135">PageSize</span></span> | <span data-ttu-id="e78ba-136">*(3.0 +)*  Podczas używane z flagą-ListAvailable (wymagane), liczba pakietów, aby wyświetlić listę przed przekazaniem wiersza, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="e78ba-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="e78ba-137">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="e78ba-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e78ba-138">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="e78ba-138">Common Parameters</span></span>

<span data-ttu-id="e78ba-139">`Get-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e78ba-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e78ba-140">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e78ba-140">Examples</span></span>

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

