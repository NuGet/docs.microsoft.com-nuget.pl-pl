---
title: "Odinstaluj — pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Odwołanie do polecenia programu PowerShell Odinstaluj pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, odinstaluj pakiet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 679e89e9cfb16dbe484f133b0b6431313b9d87ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ec8ec-104">Odinstaluj pakiet (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ec8ec-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ec8ec-105">*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia pakietu dezinstalacji programu PowerShell, zobacz [odwołania programu PowerShell PackageManagement](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="ec8ec-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ec8ec-106">Usuwa pakiet z projektu, opcjonalnie usunięcie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="ec8ec-107">Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="ec8ec-108">Składnia</span><span class="sxs-lookup"><span data-stu-id="ec8ec-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="ec8ec-109">Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="ec8ec-110">Parametry</span><span class="sxs-lookup"><span data-stu-id="ec8ec-110">Parameters</span></span>

| <span data-ttu-id="ec8ec-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="ec8ec-111">Parameter</span></span> | <span data-ttu-id="ec8ec-112">Opis</span><span class="sxs-lookup"><span data-stu-id="ec8ec-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec8ec-113">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="ec8ec-113">Id</span></span> | <span data-ttu-id="ec8ec-114">(Wymagane) Identyfikator pakietu do odinstalowania.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="ec8ec-115">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ec8ec-116">Wersja</span><span class="sxs-lookup"><span data-stu-id="ec8ec-116">Version</span></span> | <span data-ttu-id="ec8ec-117">Wersja pakietu do odinstalowania, przyjęty obecnie zainstalowanej wersji.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="ec8ec-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="ec8ec-118">RemoveDependencies</span></span> | <span data-ttu-id="ec8ec-119">Odinstaluj pakiet i jego nieużywane zależności.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="ec8ec-120">Oznacza to jeśli wszystkie zależności zależy od niego inny pakiet, zostaje pominięta.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-120">That is, if any dependency has another package that depends on it, it is skipped.</span></span> |
| <span data-ttu-id="ec8ec-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ec8ec-121">ProjectName</span></span> | <span data-ttu-id="ec8ec-122">Projekt, z którego ma zostać odinstalowany pakiet, domyślnie używany do projektu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="ec8ec-123">Wymuś</span><span class="sxs-lookup"><span data-stu-id="ec8ec-123">Force</span></span> | <span data-ttu-id="ec8ec-124">Wymusza pakietu do odinstalowania, nawet jeśli inne pakiety są od niego zależne.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="ec8ec-125">Instrukcja WhatIf</span><span class="sxs-lookup"><span data-stu-id="ec8ec-125">WhatIf</span></span> | <span data-ttu-id="ec8ec-126">Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania dezinstalacji.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="ec8ec-127">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ec8ec-128">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="ec8ec-128">Common Parameters</span></span>

<span data-ttu-id="ec8ec-129">`Uninstall-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ec8ec-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ec8ec-130">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ec8ec-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
