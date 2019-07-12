---
title: Dokumentacja programu PowerShell Install pakiet NuGet
description: Dokumentacja poleceń programu PowerShell Install-Package, w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842496"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="06323-103">Install-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="06323-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="06323-104">*W tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia programu PowerShell Install-Package, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="06323-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="06323-105">Instaluje pakiet i jego zależności do projektu.</span><span class="sxs-lookup"><span data-stu-id="06323-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="06323-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="06323-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="06323-107">W pakiecie NuGet 2.8 + `Install-Package` mogą obniżyć wersję istniejącego pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="06323-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="06323-108">Na przykład w przypadku 5.1.0-rc1 Microsoft.AspNet.MVC zainstalowane następujące polecenie będzie obniżyć do 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="06323-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="06323-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="06323-109">Parameters</span></span>

| <span data-ttu-id="06323-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="06323-110">Parameter</span></span> | <span data-ttu-id="06323-111">Opis</span><span class="sxs-lookup"><span data-stu-id="06323-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06323-112">Id</span><span class="sxs-lookup"><span data-stu-id="06323-112">Id</span></span> | <span data-ttu-id="06323-113">(Wymagane) Identyfikator pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="06323-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="06323-114">(*3.0 +* ) identyfikator może być ścieżka lub adres URL `packages.config` pliku lub `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="06323-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="06323-115">— Identyfikator samym przełączniku jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="06323-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="06323-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="06323-116">IgnoreDependencies</span></span> | <span data-ttu-id="06323-117">Zainstaluj tylko ten pakiet, a nie z jego zależności.</span><span class="sxs-lookup"><span data-stu-id="06323-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="06323-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="06323-118">ProjectName</span></span> | <span data-ttu-id="06323-119">Projekt, do którego można zainstalować pakietu, domyślnie używany będzie domyślny projekt.</span><span class="sxs-lookup"><span data-stu-id="06323-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="06323-120">Source</span><span class="sxs-lookup"><span data-stu-id="06323-120">Source</span></span> | <span data-ttu-id="06323-121">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="06323-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="06323-122">Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="06323-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="06323-123">W przypadku pominięcia `Install-Package` przeszukuje źródło obecnie wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="06323-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="06323-124">Wersja</span><span class="sxs-lookup"><span data-stu-id="06323-124">Version</span></span> | <span data-ttu-id="06323-125">Wersja pakietu do zainstalowania, ustawiając domyślnie do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="06323-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="06323-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="06323-126">IncludePrerelease</span></span> | <span data-ttu-id="06323-127">Uwzględnia pakiety w wersjach wstępnych instalacji.</span><span class="sxs-lookup"><span data-stu-id="06323-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="06323-128">Jeśli argument jest pominięty, są traktowane jako tylko stabilne pakiety.</span><span class="sxs-lookup"><span data-stu-id="06323-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="06323-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="06323-129">FileConflictAction</span></span> | <span data-ttu-id="06323-130">Akcja do wykonania po wyświetleniu monitu o zastąpienie lub zignorować istniejące pliki przywoływanego przez projekt.</span><span class="sxs-lookup"><span data-stu-id="06323-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="06323-131">Możliwe wartości to *zastąpienia, Zignoruj, None, OverwriteAll*, i *(3.0 i nowsze)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="06323-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="06323-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="06323-132">DependencyVersion</span></span> | <span data-ttu-id="06323-133">Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="06323-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="06323-134">*Najniższy* (ustawienie domyślne): Najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="06323-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="06323-135">*HighestPatch*: wersja przy najniższe główne, najniższą pomocnicza, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="06323-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="06323-136">*HighestMinor*: wersji z najniższą główne, najwyższy pomocnicza, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="06323-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="06323-137">*Najwyższy* (domyślnie dla pakietu aktualizacji bez parametrów): najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="06323-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="06323-138">Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ustawienie w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="06323-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="06323-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="06323-139">WhatIf</span></span> | <span data-ttu-id="06323-140">Pokazuje, co się stanie po uruchomieniu polecenia bez rzeczywistego wykonania instalacji.</span><span class="sxs-lookup"><span data-stu-id="06323-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="06323-141">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="06323-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="06323-142">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="06323-142">Common Parameters</span></span>

<span data-ttu-id="06323-143">`Install-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="06323-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="06323-144">Przykłady</span><span class="sxs-lookup"><span data-stu-id="06323-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
