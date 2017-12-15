---
title: NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Pełną dokumentację poleceń programu PowerShell dostępne w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a><span data-ttu-id="2f4dc-104">W programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f4dc-104">PowerShell reference</span></span>

<span data-ttu-id="2f4dc-105">Konsola Menedżera pakietów zawiera interfejsu programu PowerShell w programie Visual Studio w systemie Windows do interakcji z NuGet za pomocą określonych poleceń wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-105">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="2f4dc-106">(Konsola nie jest obecnie dostępna w programie Visual Studio for Mac.) Przewodnik dotyczący za pomocą konsoli, zobacz [Konsola Menedżera pakietów](../tools/package-manager-console.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-106">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="2f4dc-107">Wszystkie polecenia programu PowerShell odnosić się tylko do użycia pakietu.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-107">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="2f4dc-108">Brak poleceń programu PowerShell odnoszą się do tworzenia i publikowania pakietów z wyjątkiem w zakresie, w jakim pakietu można też klient korzystający z innymi pakietami.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-108">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="2f4dc-109">Polecenia wymienione w tym miejscu są specyficzne dla konsoli Menedżera pakietów w programie Visual Studio i różnią się od [pakietu administracyjnego modułu polecenia](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) dostępnych w środowisku PowerShell ogólne.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="2f4dc-110">Każde środowisko ma poleceń, które nie są dostępne w innych i poleceń o tej samej nazwie również może różnić się w ich określonych argumentów.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="2f4dc-111">Korzystając z konsoli zarządzania pakietów w programie Visual Studio, zastosowanie polecenia i argumentów opisane w niniejszym dokumencie obecny.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="2f4dc-112">Typowe polecenia</span><span class="sxs-lookup"><span data-stu-id="2f4dc-112">Common Commands</span></span> | <span data-ttu-id="2f4dc-113">Opis</span><span class="sxs-lookup"><span data-stu-id="2f4dc-113">Description</span></span> | <span data-ttu-id="2f4dc-114">Wersja narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="2f4dc-114">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="2f4dc-115">Pakiet instalacyjny</span><span class="sxs-lookup"><span data-stu-id="2f4dc-115">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="2f4dc-116">Instaluje pakiet i jego zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-116">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="2f4dc-117">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="2f4dc-117">All</span></span> |
| [<span data-ttu-id="2f4dc-118">Pakiet aktualizacji</span><span class="sxs-lookup"><span data-stu-id="2f4dc-118">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="2f4dc-119">Aktualizuje pakiet i jego zależności lub wszystkie pakiety w projekcie.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-119">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="2f4dc-120">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="2f4dc-120">All</span></span> |
| [<span data-ttu-id="2f4dc-121">Znajdź pakiet</span><span class="sxs-lookup"><span data-stu-id="2f4dc-121">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="2f4dc-122">Wyszukuje źródło pakietu przy użyciu Identyfikatora pakietu lub słowa kluczowe.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-122">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="2f4dc-123">3.0+</span><span class="sxs-lookup"><span data-stu-id="2f4dc-123">3.0+</span></span> |
| [<span data-ttu-id="2f4dc-124">Get pakietu</span><span class="sxs-lookup"><span data-stu-id="2f4dc-124">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="2f4dc-125">Pobiera listę pakietów zainstalowanych w lokalnym repozytorium, lub wyświetla ich listę pakietów dostępnych ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-125">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="2f4dc-126">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="2f4dc-126">All</span></span> |

| <span data-ttu-id="2f4dc-127">Dodatkowej poleceń</span><span class="sxs-lookup"><span data-stu-id="2f4dc-127">Secondary Commands</span></span> | <span data-ttu-id="2f4dc-128">Opis</span><span class="sxs-lookup"><span data-stu-id="2f4dc-128">Description</span></span> | <span data-ttu-id="2f4dc-129">Wersja narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="2f4dc-129">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="2f4dc-130">Dodaj BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="2f4dc-130">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="2f4dc-131">Sprawdza wszystkie zestawy w ścieżce wyjściowej dla projektu i dodaje przekierowania powiązania do `app.config` lub `web.config` w miarę potrzeby.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-131">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="2f4dc-132">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="2f4dc-132">All</span></span> |
| [<span data-ttu-id="2f4dc-133">Get projektu</span><span class="sxs-lookup"><span data-stu-id="2f4dc-133">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="2f4dc-134">Wyświetla informacje o domyślnych lub określony projekt.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-134">Displays information about the default or specified project.</span></span> | <span data-ttu-id="2f4dc-135">3.0+</span><span class="sxs-lookup"><span data-stu-id="2f4dc-135">3.0+</span></span> |
| [<span data-ttu-id="2f4dc-136">Otwórz PackagePage</span><span class="sxs-lookup"><span data-stu-id="2f4dc-136">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="2f4dc-137">Uruchamia domyślnej przeglądarki z projektu, licencji lub adresu URL programu report nadużyć dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-137">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="2f4dc-138">Przestarzałe w 3.0 +</span><span class="sxs-lookup"><span data-stu-id="2f4dc-138">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="2f4dc-139">Rejestr TabExpansion</span><span class="sxs-lookup"><span data-stu-id="2f4dc-139">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="2f4dc-140">Rejestruje rozszerzenia kartę parametrów polecenia umożliwiające tworzenie dostosowanego rozszerzenia dla wartości parametrów najczęściej używanych.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-140">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="2f4dc-141">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="2f4dc-141">All</span></span> |
| [<span data-ttu-id="2f4dc-142">Synchronizacja pakietu</span><span class="sxs-lookup"><span data-stu-id="2f4dc-142">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="2f4dc-143">Pobierz wersję zainstalowanego pakietu z określony projekt i synchronizuje wersję z resztą projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-143">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="2f4dc-144">3.0+</span><span class="sxs-lookup"><span data-stu-id="2f4dc-144">3.0+</span></span> |
| [<span data-ttu-id="2f4dc-145">Odinstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="2f4dc-145">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="2f4dc-146">Usuwa pakiet z projektu, opcjonalnie usunięcie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-146">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="2f4dc-147">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="2f4dc-147">All</span></span> |

<span data-ttu-id="2f4dc-148">Pełne, szczegółowe pomocy w przypadku dowolnego z tych poleceń, w konsoli uruchom następujące polecenie z daną nazwą polecenia:</span><span class="sxs-lookup"><span data-stu-id="2f4dc-148">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="2f4dc-149">Wszystkie polecenia konsoli Menedżera pakietów obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="2f4dc-149">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="2f4dc-150">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="2f4dc-150">Debug</span></span>
- <span data-ttu-id="2f4dc-151">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="2f4dc-151">ErrorAction</span></span>
- <span data-ttu-id="2f4dc-152">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="2f4dc-152">ErrorVariable</span></span>
- <span data-ttu-id="2f4dc-153">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="2f4dc-153">OutBuffer</span></span>
- <span data-ttu-id="2f4dc-154">OutVariable</span><span class="sxs-lookup"><span data-stu-id="2f4dc-154">OutVariable</span></span>
- <span data-ttu-id="2f4dc-155">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="2f4dc-155">PipelineVariable</span></span>
- <span data-ttu-id="2f4dc-156">Pełny</span><span class="sxs-lookup"><span data-stu-id="2f4dc-156">Verbose</span></span>
- <span data-ttu-id="2f4dc-157">WarningAction</span><span class="sxs-lookup"><span data-stu-id="2f4dc-157">WarningAction</span></span>
- <span data-ttu-id="2f4dc-158">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="2f4dc-158">WarningVariable</span></span>

<span data-ttu-id="2f4dc-159">Aby uzyskać więcej informacji, zapoznaj się [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) w dokumentacji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f4dc-159">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
