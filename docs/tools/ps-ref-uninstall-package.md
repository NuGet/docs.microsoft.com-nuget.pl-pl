---
title: Dokumentacja programu PowerShell odinstalować — pakiet NuGet
description: Dokumentacja polecenia PowerShell Odinstaluj pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842472"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="75f6d-103">Uninstall-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="75f6d-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="75f6d-104">*W tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia pakietu dezinstalacji programu PowerShell, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="75f6d-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="75f6d-105">Usuwa pakiet z projektem, opcjonalnie usunięcie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="75f6d-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="75f6d-106">Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że Force określono opcję.</span><span class="sxs-lookup"><span data-stu-id="75f6d-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="75f6d-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="75f6d-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="75f6d-108">Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że Force określono opcję.</span><span class="sxs-lookup"><span data-stu-id="75f6d-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="75f6d-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="75f6d-109">Parameters</span></span>

| <span data-ttu-id="75f6d-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="75f6d-110">Parameter</span></span> | <span data-ttu-id="75f6d-111">Opis</span><span class="sxs-lookup"><span data-stu-id="75f6d-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75f6d-112">Id</span><span class="sxs-lookup"><span data-stu-id="75f6d-112">Id</span></span> | <span data-ttu-id="75f6d-113">(Wymagane) Identyfikator pakietu do odinstalowania.</span><span class="sxs-lookup"><span data-stu-id="75f6d-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="75f6d-114">— Identyfikator samym przełączniku jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="75f6d-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="75f6d-115">Wersja</span><span class="sxs-lookup"><span data-stu-id="75f6d-115">Version</span></span> | <span data-ttu-id="75f6d-116">Wersja pakietu, aby odinstalować, przyjęty obecnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="75f6d-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="75f6d-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="75f6d-117">RemoveDependencies</span></span> | <span data-ttu-id="75f6d-118">Odinstaluj pakiet i jego zależności nieużywane.</span><span class="sxs-lookup"><span data-stu-id="75f6d-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="75f6d-119">Oznacza to jeśli wszystkie zależności ma inny pakiet, który zależy od niego, zostanie ona pominięta.</span><span class="sxs-lookup"><span data-stu-id="75f6d-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="75f6d-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="75f6d-120">ProjectName</span></span> | <span data-ttu-id="75f6d-121">Projekt, z którego można odinstalować pakietu, domyślnie używany będzie domyślny projekt.</span><span class="sxs-lookup"><span data-stu-id="75f6d-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="75f6d-122">Wymuś</span><span class="sxs-lookup"><span data-stu-id="75f6d-122">Force</span></span> | <span data-ttu-id="75f6d-123">Wymusza pakietu dezinstalację, nawet jeśli inne pakiety są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="75f6d-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="75f6d-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="75f6d-124">WhatIf</span></span> | <span data-ttu-id="75f6d-125">Pokazuje, co się stanie, podczas uruchamiania polecenia bez rzeczywistego wykonania dezinstalacji.</span><span class="sxs-lookup"><span data-stu-id="75f6d-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="75f6d-126">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="75f6d-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="75f6d-127">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="75f6d-127">Common Parameters</span></span>

<span data-ttu-id="75f6d-128">`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="75f6d-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="75f6d-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="75f6d-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
