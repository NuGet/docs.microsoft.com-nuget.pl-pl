---
title: Zainstaluj pakiet NuGet w programie PowerShell
description: Odwołanie do polecenia programu PowerShell Install-Package w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 6b2326d7b1ada8a337ae50ffd09f9deea80545af
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817957"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f6c3b-103">Install-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f6c3b-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f6c3b-104">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows. Polecenia programu PowerShell Install-Package ogólny, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f6c3b-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f6c3b-105">Instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="f6c3b-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="f6c3b-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f6c3b-107">W NuGet 2.8 + `Install-Package` mogłoby obniżyć poziom istniejącego pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="f6c3b-108">Na przykład jeśli masz zainstalowany 5.1.0-rc1 Microsoft.AspNet.MVC następujące polecenie spowoduje obniżyć go 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="f6c3b-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="f6c3b-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="f6c3b-109">Parameters</span></span>

| <span data-ttu-id="f6c3b-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="f6c3b-110">Parameter</span></span> | <span data-ttu-id="f6c3b-111">Opis</span><span class="sxs-lookup"><span data-stu-id="f6c3b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6c3b-112">Id</span><span class="sxs-lookup"><span data-stu-id="f6c3b-112">Id</span></span> | <span data-ttu-id="f6c3b-113">(Wymagane) Identyfikator pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="f6c3b-114">(*3.0 +*) identyfikator może być ścieżka lub adres URL `packages.config` pliku lub `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="f6c3b-115">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f6c3b-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f6c3b-116">IgnoreDependencies</span></span> | <span data-ttu-id="f6c3b-117">Zainstaluj tylko ten pakiet, bez jego zależności.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="f6c3b-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f6c3b-118">ProjectName</span></span> | <span data-ttu-id="f6c3b-119">Projekt, do którego można zainstalować pakietu, domyślnie używany do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="f6c3b-120">Źródło</span><span class="sxs-lookup"><span data-stu-id="f6c3b-120">Source</span></span> | <span data-ttu-id="f6c3b-121">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f6c3b-122">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f6c3b-123">Pominięcie `Install-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f6c3b-124">Wersja</span><span class="sxs-lookup"><span data-stu-id="f6c3b-124">Version</span></span> | <span data-ttu-id="f6c3b-125">Wersja pakietu do zainstalowania, domyślnie używany do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f6c3b-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f6c3b-126">IncludePrerelease</span></span> | <span data-ttu-id="f6c3b-127">Uwzględnia pakiety wersji wstępnej instalacji.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="f6c3b-128">W przypadku jego pominięcia są traktowane jako tylko pakiety w wersji stabilnej.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="f6c3b-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f6c3b-129">FileConflictAction</span></span> | <span data-ttu-id="f6c3b-130">Akcja wykonywana po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f6c3b-131">Możliwe wartości to *zastępowania, Ignoruj, brak OverwriteAll*, i *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="f6c3b-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f6c3b-132">DependencyVersion</span></span> | <span data-ttu-id="f6c3b-133">Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f6c3b-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f6c3b-134">*Najniższa* (domyślnie): Najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="f6c3b-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f6c3b-135">*HighestPatch*: wersja z najniższą głównych, najniższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="f6c3b-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f6c3b-136">*HighestMinor*: wersja z najniższą głównych, najwyższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="f6c3b-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f6c3b-137">*Najwyższy* (domyślnie pakiet aktualizacji bez parametrów): najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="f6c3b-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f6c3b-138">Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f6c3b-139">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="f6c3b-139">WhatIf</span></span> | <span data-ttu-id="f6c3b-140">Pokazuje, co się stanie po uruchomieniu polecenia bez rzeczywistego wykonania instalacji.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="f6c3b-141">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f6c3b-142">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="f6c3b-142">Common Parameters</span></span>

<span data-ttu-id="f6c3b-143">`Install-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f6c3b-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f6c3b-144">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f6c3b-144">Examples</span></span>

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
