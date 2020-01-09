---
title: Odinstalowywanie NuGet — Dokumentacja programu PowerShell pakietu
description: Informacje dotyczące polecenia programu PowerShell dotyczącego odinstalowywania pakietu w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384418"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="777fb-103">Uninstall-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="777fb-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="777fb-104">*W tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem odinstalowywania programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="777fb-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="777fb-105">Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności.</span><span class="sxs-lookup"><span data-stu-id="777fb-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="777fb-106">Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że określono opcję – Force.</span><span class="sxs-lookup"><span data-stu-id="777fb-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="777fb-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="777fb-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="777fb-108">Jeśli inne pakiety zależą od tego pakietu, polecenie zakończy się niepowodzeniem, chyba że określono opcję – Force.</span><span class="sxs-lookup"><span data-stu-id="777fb-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="777fb-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="777fb-109">Parameters</span></span>

| <span data-ttu-id="777fb-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="777fb-110">Parameter</span></span> | <span data-ttu-id="777fb-111">Opis</span><span class="sxs-lookup"><span data-stu-id="777fb-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="777fb-112">Id</span><span class="sxs-lookup"><span data-stu-id="777fb-112">Id</span></span> | <span data-ttu-id="777fb-113">Potrzeb Identyfikator pakietu do odinstalowania.</span><span class="sxs-lookup"><span data-stu-id="777fb-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="777fb-114">Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="777fb-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="777fb-115">Wersja</span><span class="sxs-lookup"><span data-stu-id="777fb-115">Version</span></span> | <span data-ttu-id="777fb-116">Wersja pakietu do odinstalowania, domyślnie przydana do aktualnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="777fb-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="777fb-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="777fb-117">RemoveDependencies</span></span> | <span data-ttu-id="777fb-118">Odinstaluj pakiet i jego nieużywane zależności.</span><span class="sxs-lookup"><span data-stu-id="777fb-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="777fb-119">Oznacza to, że jeśli jakakolwiek zależność ma inny pakiet, który od niego zależy, zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="777fb-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="777fb-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="777fb-120">ProjectName</span></span> | <span data-ttu-id="777fb-121">Projekt, z którego ma zostać odinstalowany pakiet, domyślny projekt domyślny.</span><span class="sxs-lookup"><span data-stu-id="777fb-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="777fb-122">Force</span><span class="sxs-lookup"><span data-stu-id="777fb-122">Force</span></span> | <span data-ttu-id="777fb-123">Wymusza odinstalowanie pakietu, nawet jeśli inne pakiety są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="777fb-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="777fb-124">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="777fb-124">WhatIf</span></span> | <span data-ttu-id="777fb-125">Pokazuje, co się stanie po uruchomieniu polecenia bez faktycznego wykonania operacji odinstalowywania.</span><span class="sxs-lookup"><span data-stu-id="777fb-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="777fb-126">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="777fb-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="777fb-127">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="777fb-127">Common Parameters</span></span>

<span data-ttu-id="777fb-128">`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="777fb-128">`Uninstall-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="777fb-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="777fb-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
