---
title: Dokumentacja programu PowerShell NuGet
description: Kompletne odwołanie do poleceń programu PowerShell dostępnych w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328382"
---
# <a name="powershell-reference"></a><span data-ttu-id="e9936-103">Dokumentacja programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9936-103">PowerShell reference</span></span>

<span data-ttu-id="e9936-104">Konsola Menedżera pakietów udostępnia interfejs programu PowerShell w programie Visual Studio w systemie Windows, który umożliwia współpracę z pakietem NuGet za pomocą określonych poleceń wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="e9936-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="e9936-105">(Konsola nie jest obecnie dostępna w Visual Studio dla komputerów Mac). Przewodnik dotyczący korzystania z konsoli programu znajduje się w temacie [Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md) .</span><span class="sxs-lookup"><span data-stu-id="e9936-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="e9936-106">Wszystkie polecenia programu PowerShell odnoszą się tylko do zużycia pakietów.</span><span class="sxs-lookup"><span data-stu-id="e9936-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="e9936-107">Żadne polecenia programu PowerShell nie są związane z tworzeniem i publikowaniem pakietów, z wyjątkiem przypadków, w których pakiet może być również odbiorcą innych pakietów.</span><span class="sxs-lookup"><span data-stu-id="e9936-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="e9936-108">Polecenia wymienione tutaj są specyficzne dla konsoli Menedżera pakietów w programie Visual Studio i różnią się od [poleceń modułu Zarządzanie pakietami](/powershell/module/packagemanagement/?view=powershell-6) , które są dostępne w ogólnym środowisku programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9936-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="e9936-109">W każdym środowisku istnieją polecenia, które nie są dostępne w innym, a polecenia o tej samej nazwie mogą również różnić się do określonych argumentów.</span><span class="sxs-lookup"><span data-stu-id="e9936-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="e9936-110">W przypadku korzystania z konsoli Zarządzanie pakietami w programie Visual Studio stosowane są polecenia i argumenty opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="e9936-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="e9936-111">Typowe polecenia</span><span class="sxs-lookup"><span data-stu-id="e9936-111">Common Commands</span></span> | <span data-ttu-id="e9936-112">Opis</span><span class="sxs-lookup"><span data-stu-id="e9936-112">Description</span></span> | <span data-ttu-id="e9936-113">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="e9936-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="e9936-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="e9936-114">Install-Package</span></span>](ps-reference/ps-ref-install-package.md) | <span data-ttu-id="e9936-115">Instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e9936-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="e9936-116">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e9936-116">All</span></span> |
| [<span data-ttu-id="e9936-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="e9936-117">Update-Package</span></span>](ps-reference/ps-ref-update-package.md) | <span data-ttu-id="e9936-118">Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e9936-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="e9936-119">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e9936-119">All</span></span> |
| [<span data-ttu-id="e9936-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="e9936-120">Find-Package</span></span>](ps-reference/ps-ref-find-package.md) | <span data-ttu-id="e9936-121">Wyszukuje źródło pakietu przy użyciu identyfikatora lub słów kluczowych pakietu.</span><span class="sxs-lookup"><span data-stu-id="e9936-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="e9936-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="e9936-122">3.0+</span></span> |
| [<span data-ttu-id="e9936-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="e9936-123">Get-Package</span></span>](ps-reference/ps-ref-get-package.md) | <span data-ttu-id="e9936-124">Pobiera listę pakietów zainstalowanych w repozytorium lokalnym lub wyświetla listę pakietów dostępnych ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="e9936-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="e9936-125">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e9936-125">All</span></span> |

| <span data-ttu-id="e9936-126">Polecenia pomocnicze</span><span class="sxs-lookup"><span data-stu-id="e9936-126">Secondary Commands</span></span> | <span data-ttu-id="e9936-127">Opis</span><span class="sxs-lookup"><span data-stu-id="e9936-127">Description</span></span> | <span data-ttu-id="e9936-128">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="e9936-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="e9936-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="e9936-129">Add-BindingRedirect</span></span>](ps-reference/ps-ref-add-bindingredirect.md) | <span data-ttu-id="e9936-130">Bada wszystkie zestawy w ścieżce wyjściowej projektu i dodaje przekierowania powiązań do lub `app.config` `web.config` w miarę potrzeb.</span><span class="sxs-lookup"><span data-stu-id="e9936-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="e9936-131">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e9936-131">All</span></span> |
| [<span data-ttu-id="e9936-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="e9936-132">Get-Project</span></span>](ps-reference/ps-ref-get-project.md) | <span data-ttu-id="e9936-133">Wyświetla informacje dotyczące domyślnego lub określonego projektu.</span><span class="sxs-lookup"><span data-stu-id="e9936-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="e9936-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="e9936-134">3.0+</span></span> |
| [<span data-ttu-id="e9936-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="e9936-135">Open-PackagePage</span></span>](ps-reference/ps-ref-open-packagepage.md) | <span data-ttu-id="e9936-136">Uruchamia domyślną przeglądarkę z adresem URL nadużycia projektu, licencji lub raportu dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="e9936-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="e9936-137">Przestarzałe w wersji 3.0 +</span><span class="sxs-lookup"><span data-stu-id="e9936-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="e9936-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="e9936-138">Register-TabExpansion</span></span>](ps-reference/ps-ref-register-tabexpansion.md) | <span data-ttu-id="e9936-139">Rejestruje rozwinięcie tabulatora dla parametrów polecenia, co pozwala na tworzenie dostosowanych rozszerzeń dla najczęściej używanych wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="e9936-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="e9936-140">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e9936-140">All</span></span> |
| [<span data-ttu-id="e9936-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="e9936-141">Sync-Package</span></span>](ps-reference/ps-ref-sync-package.md) | <span data-ttu-id="e9936-142">Pobierz wersję zainstalowanego pakietu z określonego projektu i zsynchronizuj wersję z pozostałymi projektami w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="e9936-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="e9936-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="e9936-143">3.0+</span></span> |
| [<span data-ttu-id="e9936-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="e9936-144">Uninstall-Package</span></span>](ps-reference/ps-ref-uninstall-package.md) | <span data-ttu-id="e9936-145">Usuwa pakiet z projektu, opcjonalnie usuwając jego zależności.</span><span class="sxs-lookup"><span data-stu-id="e9936-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="e9936-146">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e9936-146">All</span></span> |

<span data-ttu-id="e9936-147">Aby uzyskać pełną, szczegółową pomoc dotyczącą dowolnego z tych poleceń w konsoli programu, po prostu uruchom następujące polecenie z nazwą polecenia:</span><span class="sxs-lookup"><span data-stu-id="e9936-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="e9936-148">Wszystkie polecenia konsoli Menedżera pakietów obsługują następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="e9936-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="e9936-149">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="e9936-149">Debug</span></span>
- <span data-ttu-id="e9936-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="e9936-150">ErrorAction</span></span>
- <span data-ttu-id="e9936-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="e9936-151">ErrorVariable</span></span>
- <span data-ttu-id="e9936-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="e9936-152">OutBuffer</span></span>
- <span data-ttu-id="e9936-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="e9936-153">OutVariable</span></span>
- <span data-ttu-id="e9936-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="e9936-154">PipelineVariable</span></span>
- <span data-ttu-id="e9936-155">Pełny</span><span class="sxs-lookup"><span data-stu-id="e9936-155">Verbose</span></span>
- <span data-ttu-id="e9936-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="e9936-156">WarningAction</span></span>
- <span data-ttu-id="e9936-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="e9936-157">WarningVariable</span></span>

<span data-ttu-id="e9936-158">Aby uzyskać szczegółowe informacje, zobacz [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) w dokumentacji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9936-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>