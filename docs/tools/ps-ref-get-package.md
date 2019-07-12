---
title: Dokumentacja programu PowerShell Get pakiet NuGet
description: Odniesienie do polecenia PowerShell Get-pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842516"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="60294-103">Get-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="60294-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="60294-104">*W tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia PowerShell Get-Package, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="60294-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="60294-105">Pobranie listy pakietów zainstalowanych w lokalnym repozytorium, zawiera listę pakietów, które są dostępne ze źródła pakietu, gdy jest używana z opcją - ListAvailable lub wyświetla ich listę dostępnych aktualizacji, gdy jest używana z przełącznikiem - Update.</span><span class="sxs-lookup"><span data-stu-id="60294-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="60294-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="60294-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="60294-107">Bez parametrów `Get-Package` umożliwia wyświetlenie listy pakietów zainstalowanych w projekt domyślny.</span><span class="sxs-lookup"><span data-stu-id="60294-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="60294-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="60294-108">Parameters</span></span>

| <span data-ttu-id="60294-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="60294-109">Parameter</span></span> | <span data-ttu-id="60294-110">Opis</span><span class="sxs-lookup"><span data-stu-id="60294-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60294-111">Source</span><span class="sxs-lookup"><span data-stu-id="60294-111">Source</span></span> | <span data-ttu-id="60294-112">Ścieżka adresu URL lub folder pakietu.</span><span class="sxs-lookup"><span data-stu-id="60294-112">The URL or folder path for the package .</span></span> <span data-ttu-id="60294-113">Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="60294-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="60294-114">W przypadku pominięcia `Get-Package` przeszukuje źródło obecnie wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="60294-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="60294-115">Gdy jest używane z - ListAvailable, wartość domyślna to nuget.org.</span><span class="sxs-lookup"><span data-stu-id="60294-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="60294-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="60294-116">ListAvailable</span></span> | <span data-ttu-id="60294-117">Zawiera listę pakietów, które są dostępne ze źródła pakietu przyjęty adres nuget.org. Pokazuje domyślne pakietów 50, chyba że określono - PageSize i/lub - pierwszy.</span><span class="sxs-lookup"><span data-stu-id="60294-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="60294-118">Aktualizacje</span><span class="sxs-lookup"><span data-stu-id="60294-118">Updates</span></span> | <span data-ttu-id="60294-119">Zawiera listę pakietów, które mają dostępną aktualizację ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="60294-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="60294-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="60294-120">ProjectName</span></span> | <span data-ttu-id="60294-121">Projekt, z którego można pobrać zainstalowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="60294-121">The project from which to get installed packages.</span></span> <span data-ttu-id="60294-122">Jeśli argument jest pominięty, zwraca zainstalowane projektów dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="60294-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="60294-123">Filtr</span><span class="sxs-lookup"><span data-stu-id="60294-123">Filter</span></span> | <span data-ttu-id="60294-124">Ciąg filtru, w celu zawężenia listy pakietów, stosując identyfikator pakietu, opis i tagów.</span><span class="sxs-lookup"><span data-stu-id="60294-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="60294-125">pierwszy</span><span class="sxs-lookup"><span data-stu-id="60294-125">First</span></span> | <span data-ttu-id="60294-126">Liczba pakietów do zwrócenia z początku listy.</span><span class="sxs-lookup"><span data-stu-id="60294-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="60294-127">Jeśli nie zostanie określony, wartość domyślna to 50.</span><span class="sxs-lookup"><span data-stu-id="60294-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="60294-128">Skip</span><span class="sxs-lookup"><span data-stu-id="60294-128">Skip</span></span> | <span data-ttu-id="60294-129">Pomija pierwszy &lt;int&gt; pakiety z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="60294-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="60294-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="60294-130">AllVersions</span></span> | <span data-ttu-id="60294-131">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="60294-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="60294-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="60294-132">IncludePrerelease</span></span> | <span data-ttu-id="60294-133">Obejmuje pakiety w wersjach wstępnych, w wynikach.</span><span class="sxs-lookup"><span data-stu-id="60294-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="60294-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="60294-134">PageSize</span></span> | <span data-ttu-id="60294-135">*(3.0 +)*  Stosowania przy użyciu - ListAvailable (wymagane), liczba pakietów na liście przed przekazaniem wiersz, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="60294-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="60294-136">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="60294-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="60294-137">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="60294-137">Common Parameters</span></span>

<span data-ttu-id="60294-138">`Get-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="60294-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="60294-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="60294-139">Examples</span></span>

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
