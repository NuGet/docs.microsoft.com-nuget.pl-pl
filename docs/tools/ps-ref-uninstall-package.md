---
title: Odinstaluj — pakiet NuGet w programie PowerShell
description: Odwołanie do polecenia programu PowerShell Odinstaluj pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="de4ce-103">Uninstall-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="de4ce-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="de4ce-104">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia pakietu dezinstalacji programu PowerShell, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="de4ce-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="de4ce-105">Usuwa pakiet z projektu, opcjonalnie usunięcie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="de4ce-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="de4ce-106">Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.</span><span class="sxs-lookup"><span data-stu-id="de4ce-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="de4ce-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="de4ce-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="de4ce-108">Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.</span><span class="sxs-lookup"><span data-stu-id="de4ce-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="de4ce-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="de4ce-109">Parameters</span></span>

| <span data-ttu-id="de4ce-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="de4ce-110">Parameter</span></span> | <span data-ttu-id="de4ce-111">Opis</span><span class="sxs-lookup"><span data-stu-id="de4ce-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de4ce-112">Id</span><span class="sxs-lookup"><span data-stu-id="de4ce-112">Id</span></span> | <span data-ttu-id="de4ce-113">(Wymagane) Identyfikator pakietu do odinstalowania.</span><span class="sxs-lookup"><span data-stu-id="de4ce-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="de4ce-114">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="de4ce-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="de4ce-115">Wersja</span><span class="sxs-lookup"><span data-stu-id="de4ce-115">Version</span></span> | <span data-ttu-id="de4ce-116">Wersja pakietu do odinstalowania, przyjęty obecnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="de4ce-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="de4ce-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="de4ce-117">RemoveDependencies</span></span> | <span data-ttu-id="de4ce-118">Odinstaluj pakiet i jego nieużywane zależności.</span><span class="sxs-lookup"><span data-stu-id="de4ce-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="de4ce-119">Oznacza to jeśli wszystkie zależności zależy od niego inny pakiet, zostaje pominięta.</span><span class="sxs-lookup"><span data-stu-id="de4ce-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="de4ce-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="de4ce-120">ProjectName</span></span> | <span data-ttu-id="de4ce-121">Projekt, z którego ma zostać odinstalowany pakiet, domyślnie używany do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="de4ce-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="de4ce-122">Wymuś</span><span class="sxs-lookup"><span data-stu-id="de4ce-122">Force</span></span> | <span data-ttu-id="de4ce-123">Wymusza pakietu do odinstalowania, nawet jeśli inne pakiety są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="de4ce-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="de4ce-124">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="de4ce-124">WhatIf</span></span> | <span data-ttu-id="de4ce-125">Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania dezinstalacji.</span><span class="sxs-lookup"><span data-stu-id="de4ce-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="de4ce-126">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="de4ce-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="de4ce-127">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="de4ce-127">Common Parameters</span></span>

<span data-ttu-id="de4ce-128">`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="de4ce-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="de4ce-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="de4ce-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
