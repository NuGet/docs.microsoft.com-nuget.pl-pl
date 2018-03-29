---
title: Zainstaluj pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Odwołanie do polecenia programu PowerShell Install-Package w konsoli Menedżera pakietów NuGet w programie Visual Studio.
keywords: NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Install-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99c965c2f8c12c7a59ee48e270172b719c1482ea
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="692ec-104">Install-Package (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="692ec-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="692ec-105">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows. Polecenia programu PowerShell Install-Package ogólny, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="692ec-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="692ec-106">Instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="692ec-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="692ec-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="692ec-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="692ec-108">W NuGet 2.8 + `Install-Package` mogłoby obniżyć poziom istniejącego pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="692ec-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="692ec-109">Na przykład jeśli masz zainstalowany 5.1.0-rc1 Microsoft.AspNet.MVC następujące polecenie spowoduje obniżyć go 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="692ec-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="692ec-110">Parametry</span><span class="sxs-lookup"><span data-stu-id="692ec-110">Parameters</span></span>

| <span data-ttu-id="692ec-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="692ec-111">Parameter</span></span> | <span data-ttu-id="692ec-112">Opis</span><span class="sxs-lookup"><span data-stu-id="692ec-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="692ec-113">Id</span><span class="sxs-lookup"><span data-stu-id="692ec-113">Id</span></span> | <span data-ttu-id="692ec-114">(Wymagane) Identyfikator pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="692ec-114">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="692ec-115">(*3.0 +*) identyfikator może być ścieżka lub adres URL `packages.config` pliku lub `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="692ec-115">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="692ec-116">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="692ec-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="692ec-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="692ec-117">IgnoreDependencies</span></span> | <span data-ttu-id="692ec-118">Zainstaluj tylko ten pakiet, bez jego zależności.</span><span class="sxs-lookup"><span data-stu-id="692ec-118">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="692ec-119">ProjectName</span><span class="sxs-lookup"><span data-stu-id="692ec-119">ProjectName</span></span> | <span data-ttu-id="692ec-120">Projekt, do którego można zainstalować pakietu, domyślnie używany do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="692ec-120">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="692ec-121">Źródło</span><span class="sxs-lookup"><span data-stu-id="692ec-121">Source</span></span> | <span data-ttu-id="692ec-122">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="692ec-122">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="692ec-123">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="692ec-123">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="692ec-124">Pominięcie `Install-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="692ec-124">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="692ec-125">Wersja</span><span class="sxs-lookup"><span data-stu-id="692ec-125">Version</span></span> | <span data-ttu-id="692ec-126">Wersja pakietu do zainstalowania, domyślnie używany do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="692ec-126">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="692ec-127">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="692ec-127">IncludePrerelease</span></span> | <span data-ttu-id="692ec-128">Uwzględnia pakiety wersji wstępnej instalacji.</span><span class="sxs-lookup"><span data-stu-id="692ec-128">Considers prerelease packages for the install.</span></span> <span data-ttu-id="692ec-129">W przypadku jego pominięcia są traktowane jako tylko pakiety w wersji stabilnej.</span><span class="sxs-lookup"><span data-stu-id="692ec-129">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="692ec-130">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="692ec-130">FileConflictAction</span></span> | <span data-ttu-id="692ec-131">Akcja wykonywana po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="692ec-131">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="692ec-132">Możliwe wartości to *zastępowania, Ignoruj, brak OverwriteAll*, i *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="692ec-132">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="692ec-133">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="692ec-133">DependencyVersion</span></span> | <span data-ttu-id="692ec-134">Wersja pakietów zależności do użycia, które może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="692ec-134">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="692ec-135">*Najniższa* (domyślnie): Najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="692ec-135">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="692ec-136">*HighestPatch*: wersja z najniższą głównych, najniższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="692ec-136">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="692ec-137">*HighestMinor*: wersja z najniższą głównych, najwyższy niewielkie, najwyższy poziom poprawki</span><span class="sxs-lookup"><span data-stu-id="692ec-137">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="692ec-138">*Najwyższy* (domyślnie pakiet aktualizacji bez parametrów): najnowsza wersja</span><span class="sxs-lookup"><span data-stu-id="692ec-138">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="692ec-139">Można ustawić przy użyciu wartości domyślnej [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="692ec-139">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="692ec-140">WhatIf</span><span class="sxs-lookup"><span data-stu-id="692ec-140">WhatIf</span></span> | <span data-ttu-id="692ec-141">Pokazuje, co się stanie po uruchomieniu polecenia bez rzeczywistego wykonania instalacji.</span><span class="sxs-lookup"><span data-stu-id="692ec-141">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="692ec-142">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="692ec-142">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="692ec-143">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="692ec-143">Common Parameters</span></span>

<span data-ttu-id="692ec-144">`Install-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="692ec-144">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="692ec-145">Przykłady</span><span class="sxs-lookup"><span data-stu-id="692ec-145">Examples</span></span>

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
