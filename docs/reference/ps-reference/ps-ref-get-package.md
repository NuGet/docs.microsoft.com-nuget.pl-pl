---
title: Dokumentacja poleceń Get-Package programu NuGet
description: Dokumentacja polecenia Get-Package programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328208"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="94fef-103">Get-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="94fef-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="94fef-104">*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem Get-Package programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="94fef-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="94fef-105">Pobiera listę pakietów zainstalowanych w repozytorium lokalnym, wyświetla listę pakietów dostępnych ze źródła pakietów, gdy jest używany z przełącznikiem-ListAvailable lub wyświetla listę dostępnych aktualizacji, gdy jest używany z przełącznikiem-Update.</span><span class="sxs-lookup"><span data-stu-id="94fef-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="94fef-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="94fef-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="94fef-107">Bez parametrów, `Get-Package` wyświetla listę pakietów zainstalowanych w domyślnym projekcie.</span><span class="sxs-lookup"><span data-stu-id="94fef-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="94fef-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="94fef-108">Parameters</span></span>

| <span data-ttu-id="94fef-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="94fef-109">Parameter</span></span> | <span data-ttu-id="94fef-110">Opis</span><span class="sxs-lookup"><span data-stu-id="94fef-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="94fef-111">Source</span><span class="sxs-lookup"><span data-stu-id="94fef-111">Source</span></span> | <span data-ttu-id="94fef-112">Ścieżka adresu URL lub folderu dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="94fef-112">The URL or folder path for the package .</span></span> <span data-ttu-id="94fef-113">Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="94fef-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="94fef-114">W przypadku pominięcia program `Get-Package` przeszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="94fef-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="94fef-115">W przypadku użycia z opcją-ListAvailable wartość domyślna to nuget.org.</span><span class="sxs-lookup"><span data-stu-id="94fef-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="94fef-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="94fef-116">ListAvailable</span></span> | <span data-ttu-id="94fef-117">Wyświetla listę pakietów dostępnych ze źródła pakietów, domyślnie nuget.org. Wyświetla domyślnie 50 pakietów, chyba że są określone wartości-PageSize i/lub-First.</span><span class="sxs-lookup"><span data-stu-id="94fef-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="94fef-118">Aktualizacje</span><span class="sxs-lookup"><span data-stu-id="94fef-118">Updates</span></span> | <span data-ttu-id="94fef-119">Wyświetla listę pakietów z aktualizacją dostępną w źródle pakietu.</span><span class="sxs-lookup"><span data-stu-id="94fef-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="94fef-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="94fef-120">ProjectName</span></span> | <span data-ttu-id="94fef-121">Projekt, z którego mają zostać pobrane zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="94fef-121">The project from which to get installed packages.</span></span> <span data-ttu-id="94fef-122">W przypadku pominięcia zwraca zainstalowane projekty dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="94fef-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="94fef-123">Filtr</span><span class="sxs-lookup"><span data-stu-id="94fef-123">Filter</span></span> | <span data-ttu-id="94fef-124">Ciąg filtru służący do zawężenia listy pakietów przez zastosowanie jej do identyfikatora pakietu, opisu i tagów.</span><span class="sxs-lookup"><span data-stu-id="94fef-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="94fef-125">pierwszego</span><span class="sxs-lookup"><span data-stu-id="94fef-125">First</span></span> | <span data-ttu-id="94fef-126">Liczba pakietów do zwrócenia od początku listy.</span><span class="sxs-lookup"><span data-stu-id="94fef-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="94fef-127">Jeśli nie zostanie określony, wartość domyślna to 50.</span><span class="sxs-lookup"><span data-stu-id="94fef-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="94fef-128">Skip</span><span class="sxs-lookup"><span data-stu-id="94fef-128">Skip</span></span> | <span data-ttu-id="94fef-129">Pomija pierwsze &lt;pakiety int&gt; z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="94fef-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="94fef-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="94fef-130">AllVersions</span></span> | <span data-ttu-id="94fef-131">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="94fef-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="94fef-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="94fef-132">IncludePrerelease</span></span> | <span data-ttu-id="94fef-133">Zawiera pakiety wersji wstępnej w wynikach.</span><span class="sxs-lookup"><span data-stu-id="94fef-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="94fef-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="94fef-134">PageSize</span></span> | <span data-ttu-id="94fef-135">*(3.0 +)* Jeśli jest używany z-ListAvailable (required), liczba pakietów do wyświetlenia przed podawaniem monitu o kontynuowanie.</span><span class="sxs-lookup"><span data-stu-id="94fef-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="94fef-136">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="94fef-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="94fef-137">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="94fef-137">Common Parameters</span></span>

<span data-ttu-id="94fef-138">`Get-Package`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="94fef-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="94fef-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="94fef-139">Examples</span></span>

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
