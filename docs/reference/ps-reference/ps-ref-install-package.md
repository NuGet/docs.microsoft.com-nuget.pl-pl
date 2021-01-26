---
title: Dokumentacja programu NuGet Install-Package PowerShell
description: Informacje dotyczące Install-Package polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 110b41e830636d60741b14292c17840aa5a63dfd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777446"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="91835-103">Install-Package (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="91835-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="91835-104">*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Ogólne polecenie programu PowerShell Install-Package można znaleźć w [dokumentacji programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="91835-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="91835-105">Instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="91835-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="91835-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="91835-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="91835-107">W programie NuGet 2.8 + `Install-Package` można obniżyć poziom istniejącego pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="91835-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="91835-108">Na przykład jeśli masz zainstalowany plik Microsoft. AspNet. MVC 5.1.0-RC1, następujące polecenie obniży go do 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="91835-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="91835-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="91835-109">Parameters</span></span>

| <span data-ttu-id="91835-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="91835-110">Parameter</span></span> | <span data-ttu-id="91835-111">Opis</span><span class="sxs-lookup"><span data-stu-id="91835-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91835-112">Id</span><span class="sxs-lookup"><span data-stu-id="91835-112">Id</span></span> | <span data-ttu-id="91835-113">Potrzeb Identyfikator pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="91835-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="91835-114">(*3.0 +*) Identyfikator może być ścieżką lub adresem URL `packages.config` pliku lub `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="91835-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="91835-115">Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="91835-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="91835-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="91835-116">IgnoreDependencies</span></span> | <span data-ttu-id="91835-117">Zainstaluj tylko ten pakiet, a nie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="91835-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="91835-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="91835-118">ProjectName</span></span> | <span data-ttu-id="91835-119">Projekt, w którym ma zostać zainstalowany pakiet, domyślny dla projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="91835-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="91835-120">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="91835-120">Source</span></span> | <span data-ttu-id="91835-121">Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania.</span><span class="sxs-lookup"><span data-stu-id="91835-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="91835-122">Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="91835-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="91835-123">W przypadku pominięcia program `Install-Package` przeszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="91835-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="91835-124">Wersja</span><span class="sxs-lookup"><span data-stu-id="91835-124">Version</span></span> | <span data-ttu-id="91835-125">Wersja pakietu do zainstalowania, domyślnie przyaktualna do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="91835-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="91835-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="91835-126">IncludePrerelease</span></span> | <span data-ttu-id="91835-127">Traktuje pakiety wersji wstępnej do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="91835-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="91835-128">W przypadku pominięcia są brane pod uwagę tylko pakiety stabilne.</span><span class="sxs-lookup"><span data-stu-id="91835-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="91835-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="91835-129">FileConflictAction</span></span> | <span data-ttu-id="91835-130">Akcja, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="91835-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="91835-131">Możliwe wartości to *overwrite, IGNORE, None, OverwriteAll* i *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="91835-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="91835-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="91835-132">DependencyVersion</span></span> | <span data-ttu-id="91835-133">Wersja pakietów zależności do użycia, która może być jedną z następujących:</span><span class="sxs-lookup"><span data-stu-id="91835-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="91835-134">*Najniższy* (domyślny): najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="91835-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="91835-135">*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="91835-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="91835-136">*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="91835-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="91835-137">*Najwyższe* (domyślnie dla Update-Package bez parametrów): najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="91835-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="91835-138">Możesz ustawić wartość domyślną przy użyciu [`dependencyVersion`](../nuget-config-file.md#config-section) Ustawienia w `Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="91835-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="91835-139">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="91835-139">WhatIf</span></span> | <span data-ttu-id="91835-140">Pokazuje, co się stanie po uruchomieniu polecenia bez faktycznego wykonania instalacji.</span><span class="sxs-lookup"><span data-stu-id="91835-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="91835-141">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="91835-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="91835-142">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="91835-142">Common Parameters</span></span>

<span data-ttu-id="91835-143">`Install-Package` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="91835-143">`Install-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="91835-144">Przykłady</span><span class="sxs-lookup"><span data-stu-id="91835-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```