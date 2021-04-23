---
title: Informacje o programie PowerShell Get-Package NuGet
description: Informacje dotyczące Get-Package programu PowerShell w konsoli Menedżer pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901736"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="fdbaa-103">Get-Package (konsola Menedżer pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fdbaa-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fdbaa-104">*W tym temacie opisano polecenie w konsoli [Menedżer pakietów w](../../consume-packages/install-use-packages-powershell.md) Visual Studio w systemie Windows. Aby uzyskać ogólne polecenie Get-Package Programu PowerShell, zobacz informacje dotyczące polecenia [PackageManagement programu PowerShell.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="fdbaa-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="fdbaa-105">Pobiera listę pakietów zainstalowanych w repozytorium lokalnym, wyświetla listę pakietów dostępnych ze źródła pakietu, gdy są używane z przełącznikiem -ListAvailable, lub wyświetla listę dostępnych aktualizacji w przypadku korzystania z przełącznika -Update.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="fdbaa-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="fdbaa-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="fdbaa-107">Bez parametrów program `Get-Package` wyświetla listę pakietów zainstalowanych w projekcie domyślnym.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="fdbaa-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="fdbaa-108">Parameters</span></span>

| <span data-ttu-id="fdbaa-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="fdbaa-109">Parameter</span></span> | <span data-ttu-id="fdbaa-110">Opis</span><span class="sxs-lookup"><span data-stu-id="fdbaa-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fdbaa-111">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="fdbaa-111">Source</span></span> | <span data-ttu-id="fdbaa-112">Adres URL lub ścieżka folderu dla pakietu .</span><span class="sxs-lookup"><span data-stu-id="fdbaa-112">The URL or folder path for the package .</span></span> <span data-ttu-id="fdbaa-113">Ścieżki folderów lokalnych mogą być bezwzględne lub względne względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="fdbaa-114">W przypadku pominięcia `Get-Package` program wyszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="fdbaa-115">W przypadku korzystania z -ListAvailable wartość domyślna to nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="fdbaa-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="fdbaa-116">ListAvailable</span></span> | <span data-ttu-id="fdbaa-117">Wyświetla listę pakietów dostępnych ze źródła pakietu, domyślnie nuget.org. Przedstawia domyślną wartość 50 pakietów, chyba że określono -PageSize i/lub -First.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="fdbaa-118">Aktualizacje</span><span class="sxs-lookup"><span data-stu-id="fdbaa-118">Updates</span></span> | <span data-ttu-id="fdbaa-119">Wyświetla listę pakietów, które mają aktualizację dostępną ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="fdbaa-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="fdbaa-120">ProjectName</span></span> | <span data-ttu-id="fdbaa-121">Projekt, z którego mają zostać zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-121">The project from which to get installed packages.</span></span> <span data-ttu-id="fdbaa-122">W przypadku pominięcia funkcja zwraca zainstalowane projekty dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="fdbaa-123">Filtr</span><span class="sxs-lookup"><span data-stu-id="fdbaa-123">Filter</span></span> | <span data-ttu-id="fdbaa-124">Ciąg filtru używany do zawężenia listy pakietów przez zastosowanie go do identyfikatora pakietu, opisu i tagów.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="fdbaa-125">Pierwsze</span><span class="sxs-lookup"><span data-stu-id="fdbaa-125">First</span></span> | <span data-ttu-id="fdbaa-126">Liczba pakietów, które mają być zwracane od początku listy.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="fdbaa-127">Jeśli nie zostanie określony, wartość domyślna to 50.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="fdbaa-128">Pomiń</span><span class="sxs-lookup"><span data-stu-id="fdbaa-128">Skip</span></span> | <span data-ttu-id="fdbaa-129">Pomija pierwsze pakiety &lt; int &gt; z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="fdbaa-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="fdbaa-130">AllVersions</span></span> | <span data-ttu-id="fdbaa-131">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="fdbaa-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="fdbaa-132">IncludePrerelease</span></span> | <span data-ttu-id="fdbaa-133">Zawiera pakiety wytłaczania wstępnego w wynikach.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="fdbaa-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="fdbaa-134">PageSize</span></span> | <span data-ttu-id="fdbaa-135">*(3.0+)* W przypadku korzystania z polecenia z ciągiem -ListAvailable (wymagane) — liczba pakietów, które należy wyświetlić przed monitem o kontynuowanie.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="fdbaa-136">Żaden z tych parametrów nie akceptuje znaków wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fdbaa-137">Typowe parametry</span><span class="sxs-lookup"><span data-stu-id="fdbaa-137">Common Parameters</span></span>

<span data-ttu-id="fdbaa-138">`Get-Package` obsługuje następujące typowe [parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fdbaa-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fdbaa-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fdbaa-139">Examples</span></span>

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