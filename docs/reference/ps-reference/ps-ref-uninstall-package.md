---
title: Informacje o programie PowerShell Uninstall-Package NuGet
description: Informacje dotyczące Uninstall-Package programu PowerShell w konsoli Menedżer pakietów NuGet w Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901788"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="291d6-103">Uninstall-Package (Menedżer pakietów Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="291d6-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="291d6-104">*W tym temacie opisano polecenie w konsoli [Menedżer pakietów w](../../consume-packages/install-use-packages-powershell.md) Visual Studio w systemie Windows. Aby uzyskać ogólne polecenie polecenia Uninstall-Package PowerShell, zobacz informacje dotyczące polecenia [PackageManagement programu PowerShell](/powershell/module/packagemanagement).*</span><span class="sxs-lookup"><span data-stu-id="291d6-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="291d6-105">Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności.</span><span class="sxs-lookup"><span data-stu-id="291d6-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="291d6-106">Jeśli inne pakiety zależą od tego pakietu, polecenie nie powiedzie się, chyba że określono opcję –Force.</span><span class="sxs-lookup"><span data-stu-id="291d6-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="291d6-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="291d6-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="291d6-108">Jeśli inne pakiety zależą od tego pakietu, polecenie nie powiedzie się, chyba że określono opcję –Force.</span><span class="sxs-lookup"><span data-stu-id="291d6-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="291d6-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="291d6-109">Parameters</span></span>

| <span data-ttu-id="291d6-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="291d6-110">Parameter</span></span> | <span data-ttu-id="291d6-111">Opis</span><span class="sxs-lookup"><span data-stu-id="291d6-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="291d6-112">Id</span><span class="sxs-lookup"><span data-stu-id="291d6-112">Id</span></span> | <span data-ttu-id="291d6-113">(Wymagane) Identyfikator pakietu do odinstalowania.</span><span class="sxs-lookup"><span data-stu-id="291d6-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="291d6-114">Sam przełącznik -Id jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="291d6-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="291d6-115">Wersja</span><span class="sxs-lookup"><span data-stu-id="291d6-115">Version</span></span> | <span data-ttu-id="291d6-116">Wersja pakietu do odinstalowania, domyślnie zainstalowana wersja.</span><span class="sxs-lookup"><span data-stu-id="291d6-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="291d6-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="291d6-117">RemoveDependencies</span></span> | <span data-ttu-id="291d6-118">Odinstaluj pakiet i jego nieużywane zależności.</span><span class="sxs-lookup"><span data-stu-id="291d6-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="291d6-119">Oznacza to, że jeśli jakakolwiek zależność ma inny pakiet, który od niego zależy, zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="291d6-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="291d6-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="291d6-120">ProjectName</span></span> | <span data-ttu-id="291d6-121">Projekt, z którego ma zostać odinstalowany pakiet ( domyślnie jest to projekt domyślny).</span><span class="sxs-lookup"><span data-stu-id="291d6-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="291d6-122">Force</span><span class="sxs-lookup"><span data-stu-id="291d6-122">Force</span></span> | <span data-ttu-id="291d6-123">Wymusza odinstalowanie pakietu, nawet jeśli od niego zależą inne pakiety.</span><span class="sxs-lookup"><span data-stu-id="291d6-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="291d6-124">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="291d6-124">WhatIf</span></span> | <span data-ttu-id="291d6-125">Pokazuje, co się stanie w przypadku uruchomienia polecenia bez przeprowadzania dezinstalacji.</span><span class="sxs-lookup"><span data-stu-id="291d6-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="291d6-126">Żaden z tych parametrów nie akceptuje znaków wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="291d6-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="291d6-127">Typowe parametry</span><span class="sxs-lookup"><span data-stu-id="291d6-127">Common Parameters</span></span>

<span data-ttu-id="291d6-128">`Uninstall-Package` obsługuje następujące typowe [parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="291d6-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="291d6-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="291d6-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```