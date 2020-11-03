---
title: Dokumentacja programu NuGet Uninstall-Package PowerShell
description: Informacje dotyczące Uninstall-Package polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237130"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="6d0fe-103">Uninstall-Package (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6d0fe-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6d0fe-104">*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Ogólne polecenie programu PowerShell Uninstall-Package można znaleźć w [dokumentacji programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="6d0fe-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="6d0fe-105">Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="6d0fe-106">Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że określono opcję – Force.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="6d0fe-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="6d0fe-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="6d0fe-108">Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że określono opcję – Force.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="6d0fe-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="6d0fe-109">Parameters</span></span>

| <span data-ttu-id="6d0fe-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="6d0fe-110">Parameter</span></span> | <span data-ttu-id="6d0fe-111">Opis</span><span class="sxs-lookup"><span data-stu-id="6d0fe-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d0fe-112">Id</span><span class="sxs-lookup"><span data-stu-id="6d0fe-112">Id</span></span> | <span data-ttu-id="6d0fe-113">Potrzeb Identyfikator pakietu do odinstalowania.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="6d0fe-114">Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="6d0fe-115">Wersja</span><span class="sxs-lookup"><span data-stu-id="6d0fe-115">Version</span></span> | <span data-ttu-id="6d0fe-116">Wersja pakietu do odinstalowania, domyślnie przydana do aktualnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="6d0fe-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="6d0fe-117">RemoveDependencies</span></span> | <span data-ttu-id="6d0fe-118">Odinstaluj pakiet i jego nieużywane zależności.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="6d0fe-119">Oznacza to, że jeśli jakakolwiek zależność ma inny pakiet, który od niego zależy, zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="6d0fe-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="6d0fe-120">ProjectName</span></span> | <span data-ttu-id="6d0fe-121">Projekt, z którego ma zostać odinstalowany pakiet, domyślny projekt domyślny.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="6d0fe-122">Force</span><span class="sxs-lookup"><span data-stu-id="6d0fe-122">Force</span></span> | <span data-ttu-id="6d0fe-123">Wymusza odinstalowanie pakietu, nawet jeśli inne pakiety są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="6d0fe-124">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="6d0fe-124">WhatIf</span></span> | <span data-ttu-id="6d0fe-125">Pokazuje, co się stanie po uruchomieniu polecenia bez faktycznego wykonania operacji odinstalowywania.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="6d0fe-126">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6d0fe-127">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="6d0fe-127">Common Parameters</span></span>

<span data-ttu-id="6d0fe-128">`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6d0fe-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6d0fe-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="6d0fe-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```