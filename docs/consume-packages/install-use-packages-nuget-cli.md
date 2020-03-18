---
title: Zarządzanie pakietami NuGet przy użyciu interfejsu wiersza polecenia NuGet. exe
description: Instrukcje dotyczące używania interfejsu wiersza polecenia NuGet. exe do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428689"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="7a899-103">Zarządzanie pakietami za pomocą interfejsu wiersza polecenia NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="7a899-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="7a899-104">Narzędzie interfejsu wiersza polecenia umożliwia łatwe aktualizowanie i przywracanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="7a899-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="7a899-105">To narzędzie zapewnia wszystkie możliwości programu NuGet w systemie Windows, a także zapewnia większość funkcji na komputerach Mac i Linux, gdy działa w trybie mono.</span><span class="sxs-lookup"><span data-stu-id="7a899-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="7a899-106">Interfejs wiersza polecenia `nuget.exe` jest przeznaczony dla projektu .NET Framework i projektów spoza zestawu SDK (na przykład projekt typu innego niż zestaw SDK przeznaczony dla bibliotek .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="7a899-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="7a899-107">Jeśli używasz projektu typu innego niż zestaw SDK, który został zmigrowany do `PackageReference`, zamiast tego użyj interfejsu wiersza polecenia `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="7a899-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="7a899-108">Interfejs wiersza polecenia `nuget.exe` wymaga pliku [Packages. config](../reference/packages-config.md) na potrzeby odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="7a899-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="7a899-109">W większości scenariuszy zalecamy [Migrowanie projektów typu non-SDK](../consume-packages/migrate-packages-config-to-package-reference.md) , które używają `packages.config` do PackageReference, a następnie można użyć interfejsu wiersza polecenia `dotnet` zamiast interfejsu wiersza polecenia `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="7a899-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="7a899-110">Migracja nie jest obecnie dostępna dla C++ projektów i ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7a899-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="7a899-111">W tym artykule przedstawiono podstawowe użycie kilku typowych poleceń interfejsu wiersza polecenia `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="7a899-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="7a899-112">W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu.</span><span class="sxs-lookup"><span data-stu-id="7a899-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="7a899-113">Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz [Dokumentacja interfejsu wiersza polecenia NuGet. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="7a899-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a899-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7a899-114">Prerequisites</span></span>

- <span data-ttu-id="7a899-115">Zainstaluj interfejs wiersza polecenia `nuget.exe`, pobierając go z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując plik `.exe` do odpowiedniego folderu i dodając go do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="7a899-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="7a899-116">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="7a899-116">Install a package</span></span>

<span data-ttu-id="7a899-117">Polecenie [instalacji](../reference/cli-reference/cli-ref-install.md) pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="7a899-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="7a899-118">Zainstaluj nowe pakiety w folderze *Packages* w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="7a899-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a899-119">Polecenie `install`nie modyfikuje pliku projektu ani *pakietów. config*; w ten sposób przypomina `restore`, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="7a899-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="7a899-120">Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj *plik Packages. config* , a następnie uruchom polecenie `install` lub `restore`.</span><span class="sxs-lookup"><span data-stu-id="7a899-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="7a899-121">Otwórz wiersz polecenia i przejdź do katalogu, który zawiera plik projektu.</span><span class="sxs-lookup"><span data-stu-id="7a899-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="7a899-122">Użyj poniższego polecenia, aby zainstalować pakiet NuGet w folderze *Packages* .</span><span class="sxs-lookup"><span data-stu-id="7a899-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="7a899-123">Aby zainstalować pakiet `Newtonsoft.json` w folderze *Packages* , użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7a899-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="7a899-124">Alternatywnie możesz użyć poniższego polecenia, aby zainstalować pakiet NuGet przy użyciu istniejącego pliku `packages.config` w folderze *Packages* .</span><span class="sxs-lookup"><span data-stu-id="7a899-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="7a899-125">Nie powoduje to dodania pakietu do zależności projektu, ale instaluje go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="7a899-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="7a899-126">Zainstaluj określoną wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="7a899-126">Install a specific version of a package</span></span>

<span data-ttu-id="7a899-127">Jeśli wersja nie zostanie określona podczas korzystania z polecenia [Install](../reference/cli-reference/cli-ref-install.md) , pakiet NuGet instaluje najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="7a899-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="7a899-128">Można także zainstalować określoną wersję pakietu NuGet:</span><span class="sxs-lookup"><span data-stu-id="7a899-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="7a899-129">Na przykład, aby dodać wersję 12.0.1 pakietu `Newtonsoft.json`, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7a899-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="7a899-130">Aby uzyskać więcej informacji o ograniczeniach i zachowaniu `install`, zobacz [Instalowanie pakietu](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="7a899-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="7a899-131">Usuń pakiet</span><span class="sxs-lookup"><span data-stu-id="7a899-131">Remove a package</span></span>

<span data-ttu-id="7a899-132">Aby usunąć co najmniej jeden pakiet, Usuń pakiety, które chcesz usunąć z folderu *pakiety* .</span><span class="sxs-lookup"><span data-stu-id="7a899-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="7a899-133">Jeśli chcesz ponownie zainstalować pakiety, użyj polecenia `restore` lub `install`.</span><span class="sxs-lookup"><span data-stu-id="7a899-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="7a899-134">Wyświetl listę pakietów</span><span class="sxs-lookup"><span data-stu-id="7a899-134">List packages</span></span>

<span data-ttu-id="7a899-135">Możesz wyświetlić listę pakietów z danego źródła za pomocą polecenia [list](../reference/cli-reference/cli-ref-list.md) .</span><span class="sxs-lookup"><span data-stu-id="7a899-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="7a899-136">Użyj opcji `-Source`, aby ograniczyć wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="7a899-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="7a899-137">Na przykład Wyświetl listę pakietów w folderze *Packages* .</span><span class="sxs-lookup"><span data-stu-id="7a899-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="7a899-138">W przypadku korzystania z wyszukiwanego terminu wyszukiwanie obejmuje nazwy pakietów, tagów i opisów pakietów.</span><span class="sxs-lookup"><span data-stu-id="7a899-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="7a899-139">Aktualizowanie pojedynczego pakietu</span><span class="sxs-lookup"><span data-stu-id="7a899-139">Update an individual package</span></span>

<span data-ttu-id="7a899-140">Pakiet NuGet instaluje najnowszą wersję pakietu przy użyciu polecenia `install`, o ile nie zostanie określona wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="7a899-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="7a899-141">Aktualizuj wszystkie pakiety</span><span class="sxs-lookup"><span data-stu-id="7a899-141">Update all packages</span></span>

<span data-ttu-id="7a899-142">Użyj polecenia [Aktualizuj](../reference/cli-reference/cli-ref-update.md) , aby zaktualizować wszystkie pakiety.</span><span class="sxs-lookup"><span data-stu-id="7a899-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="7a899-143">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do ich najnowszych dostępnych wersji.</span><span class="sxs-lookup"><span data-stu-id="7a899-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="7a899-144">Przed uruchomieniem `update`zaleca się uruchomienie `restore`.</span><span class="sxs-lookup"><span data-stu-id="7a899-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="7a899-145">Przywróć pakiety</span><span class="sxs-lookup"><span data-stu-id="7a899-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="7a899-146">Pobierz wersję interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7a899-146">Get the CLI version</span></span>

<span data-ttu-id="7a899-147">Użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7a899-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="7a899-148">Pierwszy wiersz w danych wyjściowych pomocy pokazuje wersję.</span><span class="sxs-lookup"><span data-stu-id="7a899-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="7a899-149">Aby uniknąć przewijania, Użyj zamiast tego `nuget help | more`.</span><span class="sxs-lookup"><span data-stu-id="7a899-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>