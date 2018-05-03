---
title: Get pakiet NuGet w programie PowerShell
description: Dokumentacja dotycząca polecenia PowerShell Get-pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: c70e60b7391f19026e2dcd502d667fbe1da7e6e2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ea8b9-103">Get-Package (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ea8b9-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ea8b9-104">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia PowerShell Get-Package, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="ea8b9-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ea8b9-105">Pobiera listę pakietów zainstalowanych w lokalnym repozytorium, zawiera listę pakietów dostępnych ze źródła pakietu, gdy jest używany z flagą - ListAvailable przełącznika lub wymieniono dostępne aktualizacje, gdy jest używany z przełącznikiem - Update.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="ea8b9-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="ea8b9-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="ea8b9-107">Bez parametrów `Get-Package` Wyświetla listę pakietów zainstalowanych w projekcie domyślnym.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="ea8b9-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="ea8b9-108">Parameters</span></span>

| <span data-ttu-id="ea8b9-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="ea8b9-109">Parameter</span></span> | <span data-ttu-id="ea8b9-110">Opis</span><span class="sxs-lookup"><span data-stu-id="ea8b9-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea8b9-111">Źródło</span><span class="sxs-lookup"><span data-stu-id="ea8b9-111">Source</span></span> | <span data-ttu-id="ea8b9-112">Ścieżka adresu URL lub folderu pakietu.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-112">The URL or folder path for the package .</span></span> <span data-ttu-id="ea8b9-113">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ea8b9-114">Pominięcie `Get-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="ea8b9-115">W przypadku korzystania z flagą-ListAvailable, wartość domyślna to nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="ea8b9-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="ea8b9-116">ListAvailable</span></span> | <span data-ttu-id="ea8b9-117">Wyświetla listę dostępnych pakietów ze źródła pakietu przyjęty nuget.org. Pokazuje domyślnie 50 pakietów, chyba że określono - PageSize i/lub - pierwszy.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="ea8b9-118">Aktualizacje</span><span class="sxs-lookup"><span data-stu-id="ea8b9-118">Updates</span></span> | <span data-ttu-id="ea8b9-119">Wyświetla listę pakietów, które mają jest dostępna aktualizacja w źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="ea8b9-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ea8b9-120">ProjectName</span></span> | <span data-ttu-id="ea8b9-121">Projekt, z którego ma zostać pobrane zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-121">The project from which to get installed packages.</span></span> <span data-ttu-id="ea8b9-122">Pominięcie zwraca zainstalowane projekty dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="ea8b9-123">Filtr</span><span class="sxs-lookup"><span data-stu-id="ea8b9-123">Filter</span></span> | <span data-ttu-id="ea8b9-124">Ciąg filtru używany do zawężania listy pakietów, uwzględniając identyfikator pakietu, opisie i tagach.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="ea8b9-125">pierwszy</span><span class="sxs-lookup"><span data-stu-id="ea8b9-125">First</span></span> | <span data-ttu-id="ea8b9-126">Liczba pakietów do zwrócenia z początku listy.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="ea8b9-127">Jeśli nie zostanie określony, domyślnie 50.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="ea8b9-128">Skip</span><span class="sxs-lookup"><span data-stu-id="ea8b9-128">Skip</span></span> | <span data-ttu-id="ea8b9-129">Pominięto pierwszy &lt;int&gt; pakiety z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="ea8b9-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ea8b9-130">AllVersions</span></span> | <span data-ttu-id="ea8b9-131">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="ea8b9-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ea8b9-132">IncludePrerelease</span></span> | <span data-ttu-id="ea8b9-133">Zawiera pakiety wersji wstępnej w wynikach.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="ea8b9-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="ea8b9-134">PageSize</span></span> | <span data-ttu-id="ea8b9-135">*(3.0 +)*  Podczas używane z flagą-ListAvailable (wymagane), liczba pakietów, aby wyświetlić listę przed przekazaniem wiersza, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="ea8b9-136">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ea8b9-137">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="ea8b9-137">Common Parameters</span></span>

<span data-ttu-id="ea8b9-138">`Get-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ea8b9-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ea8b9-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ea8b9-139">Examples</span></span>

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
