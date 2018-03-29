---
title: Odinstaluj — pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Odwołanie do polecenia programu PowerShell Odinstaluj pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
keywords: NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, odinstaluj pakiet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b53a36a6456522aa0d9d0d7cdf412de464ba9e08
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e452d-104">Odinstaluj pakiet (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e452d-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e452d-105">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia pakietu dezinstalacji programu PowerShell, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e452d-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e452d-106">Usuwa pakiet z projektu, opcjonalnie usunięcie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="e452d-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="e452d-107">Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.</span><span class="sxs-lookup"><span data-stu-id="e452d-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="e452d-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="e452d-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e452d-109">Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.</span><span class="sxs-lookup"><span data-stu-id="e452d-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="e452d-110">Parametry</span><span class="sxs-lookup"><span data-stu-id="e452d-110">Parameters</span></span>

| <span data-ttu-id="e452d-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="e452d-111">Parameter</span></span> | <span data-ttu-id="e452d-112">Opis</span><span class="sxs-lookup"><span data-stu-id="e452d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e452d-113">Id</span><span class="sxs-lookup"><span data-stu-id="e452d-113">Id</span></span> | <span data-ttu-id="e452d-114">(Wymagane) Identyfikator pakietu do odinstalowania.</span><span class="sxs-lookup"><span data-stu-id="e452d-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="e452d-115">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="e452d-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e452d-116">Wersja</span><span class="sxs-lookup"><span data-stu-id="e452d-116">Version</span></span> | <span data-ttu-id="e452d-117">Wersja pakietu do odinstalowania, przyjęty obecnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="e452d-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e452d-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="e452d-118">RemoveDependencies</span></span> | <span data-ttu-id="e452d-119">Odinstaluj pakiet i jego nieużywane zależności.</span><span class="sxs-lookup"><span data-stu-id="e452d-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="e452d-120">Oznacza to jeśli wszystkie zależności zależy od niego inny pakiet, zostaje pominięta.</span><span class="sxs-lookup"><span data-stu-id="e452d-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="e452d-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e452d-121">ProjectName</span></span> | <span data-ttu-id="e452d-122">Projekt, z którego ma zostać odinstalowany pakiet, domyślnie używany do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="e452d-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="e452d-123">Wymuś</span><span class="sxs-lookup"><span data-stu-id="e452d-123">Force</span></span> | <span data-ttu-id="e452d-124">Wymusza pakietu do odinstalowania, nawet jeśli inne pakiety są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="e452d-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="e452d-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e452d-125">WhatIf</span></span> | <span data-ttu-id="e452d-126">Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania dezinstalacji.</span><span class="sxs-lookup"><span data-stu-id="e452d-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="e452d-127">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="e452d-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e452d-128">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="e452d-128">Common Parameters</span></span>

<span data-ttu-id="e452d-129">`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e452d-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e452d-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e452d-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
