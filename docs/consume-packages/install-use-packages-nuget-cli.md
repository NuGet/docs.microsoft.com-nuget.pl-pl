---
title: Zarządzaj pakietami NuGet za pomocą interfejsu wiersza polecenia nuget.exe
description: Instrukcje dotyczące używania nuget.exe interfejsu wiersza polecenia do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a7177b956930835693921163e634321548c22462
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842370"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="143b8-103">Zarządzanie pakietami za pomocą interfejsu wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="143b8-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="143b8-104">Narzędzie interfejsu wiersza polecenia pozwala łatwo zaktualizować i przywracanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="143b8-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="143b8-105">To narzędzie oferuje wszystkie możliwości NuGet w Windows, a także większości funkcji na komputerach Mac i Linux w przypadku uruchomienia w Mono.</span><span class="sxs-lookup"><span data-stu-id="143b8-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="143b8-106">Nuget.exe interfejsu wiersza polecenia jest projekt programu .NET Framework i projektów innych stylu zestawu SDK (na przykład-SDK stylu projektu, który jest przeznaczony dla biblioteki .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="143b8-106">The nuget.exe CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="143b8-107">Jeśli używasz projektu bez stylu zestawu SDK, który zostały przeniesione do `PackageReference`, zamiast tego użyj wiersz polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="143b8-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the dotnet CLI instead.</span></span> <span data-ttu-id="143b8-108">Interfejs wiersza polecenia NuGet wymaga [packages.config](../reference/packages-config.md) odwołania do pakietu w pliku.</span><span class="sxs-lookup"><span data-stu-id="143b8-108">The NuGet CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="143b8-109">W większości przypadków zaleca się [migrowania projektów bez SDK-style](../reference/migrate-packages-config-to-package-reference.md) używające `packages.config` do odwołania PackageReference, a następnie przy użyciu interfejsu wiersza polecenia platformy dotnet zamiast `nuget.exe` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="143b8-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the dotnet CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="143b8-110">Migracja nie jest obecnie dostępna dla projektów C++ i programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="143b8-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="143b8-111">W tym artykule przedstawiono podstawowe użycie niektóre z najczęściej używanych poleceń interfejsu wiersza polecenia nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="143b8-111">This article shows you basic usage for a few of the most common nuget.exe CLI commands.</span></span> <span data-ttu-id="143b8-112">Dla większości z tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, o ile nie określono pliku projektu w poleceniu.</span><span class="sxs-lookup"><span data-stu-id="143b8-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="143b8-113">Aby uzyskać pełną listę poleceń i argumentów, można użyć, zobacz [dokumentacja interfejsu wiersza polecenia nuget.exe](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="143b8-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="143b8-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="143b8-114">Prerequisites</span></span>

- <span data-ttu-id="143b8-115">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywania, który `.exe` pliku do odpowiedniego folderu i dodawanie folderu do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="143b8-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="143b8-116">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="143b8-116">Install a package</span></span>

<span data-ttu-id="143b8-117">[Zainstalować](../tools/cli-ref-install.md) polecenie pobiera i instaluje pakiet do projektu, domyślnie używany do bieżącego folderu, za pomocą źródeł określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="143b8-117">The [install](../tools/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="143b8-118">Instalowanie nowych pakietów do *pakietów* folder w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="143b8-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="143b8-119">`install`Polecenie nie modyfikuje plik projektu lub *packages.config*; dzięki temu jest on podobny do `restore` , ponieważ jej tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="143b8-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="143b8-120">Aby dodać zależność, Dodaj pakiet za pomocą interfejs użytkownika Menedżera pakietów lub konsoli w programie Visual Studio lub zmodyfikować *packages.config* , a następnie uruchom opcję `install` lub `restore`.</span><span class="sxs-lookup"><span data-stu-id="143b8-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="143b8-121">Otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="143b8-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="143b8-122">Użyj następującego polecenia, aby zainstalować pakiet NuGet, aby *pakietów* folderu.</span><span class="sxs-lookup"><span data-stu-id="143b8-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="143b8-123">Aby zainstalować `Newtonsoft.json` pakietu *pakietów* folderu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="143b8-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="143b8-124">Alternatywnie można użyć następującego polecenia można zainstalować pakietu NuGet, za pomocą istniejącego `packages.config` plik *pakietów* folderu.</span><span class="sxs-lookup"><span data-stu-id="143b8-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="143b8-125">Nie powoduje dodania pakietu do zależności projektu, ale instaluje ją lokalnie.</span><span class="sxs-lookup"><span data-stu-id="143b8-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="143b8-126">Instalowanie określonej wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="143b8-126">Install a specific version of a package</span></span>

<span data-ttu-id="143b8-127">Jeśli nie określono wersji, gdy używasz [zainstalować](../tools/cli-ref-install.md) polecenia NuGet instaluje najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="143b8-127">If the version is not specified when you use the [install](../tools/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="143b8-128">Można także zainstalować określoną wersję pakietu Nuget:</span><span class="sxs-lookup"><span data-stu-id="143b8-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="143b8-129">Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.json` pakietów, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="143b8-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="143b8-130">Aby uzyskać więcej informacji na temat ograniczeń i zachowanie `install`, zobacz [zainstalować pakiet](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="143b8-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="143b8-131">Usuń pakiet</span><span class="sxs-lookup"><span data-stu-id="143b8-131">Remove a package</span></span>

<span data-ttu-id="143b8-132">Aby usunąć co najmniej jeden pakiet, Usuń pakiety, aby usunąć z *pakietów* folderu.</span><span class="sxs-lookup"><span data-stu-id="143b8-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="143b8-133">Jeśli chcesz ponownie zainstalować pakiety, użyj `restore` lub `install` polecenia.</span><span class="sxs-lookup"><span data-stu-id="143b8-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="143b8-134">Lista pakietów</span><span class="sxs-lookup"><span data-stu-id="143b8-134">List packages</span></span>

<span data-ttu-id="143b8-135">Możesz wyświetlić listę pakietów z danego źródła przy użyciu [listy](../tools/cli-ref-list.md) polecenia.</span><span class="sxs-lookup"><span data-stu-id="143b8-135">You can display a list of packages from a given source using the [list](../tools/cli-ref-list.md) command.</span></span> <span data-ttu-id="143b8-136">Użyj `-Source` opcję, aby ograniczyć wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="143b8-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="143b8-137">Na przykład listy pakietów *pakietów* folderu.</span><span class="sxs-lookup"><span data-stu-id="143b8-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="143b8-138">Jeśli używasz wyszukiwany termin, wyszukiwanie obejmuje nazwy pakietów, tagi i opisy pakietu.</span><span class="sxs-lookup"><span data-stu-id="143b8-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="143b8-139">Aktualizowanie poszczególnych pakietów</span><span class="sxs-lookup"><span data-stu-id="143b8-139">Update an individual package</span></span>

<span data-ttu-id="143b8-140">NuGet instaluje najnowszą wersję pakietu, gdy używasz `install` polecenia, chyba że określisz wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="143b8-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="143b8-141">Aktualizuj wszystkie pakiety</span><span class="sxs-lookup"><span data-stu-id="143b8-141">Update all packages</span></span>

<span data-ttu-id="143b8-142">Użyj [aktualizacji](../tools/cli-ref-update.md) polecenie, aby zaktualizować wszystkich pakietów.</span><span class="sxs-lookup"><span data-stu-id="143b8-142">Use the [update](../tools/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="143b8-143">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do jego najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="143b8-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="143b8-144">Zaleca się uruchomienie `restore` przed uruchomieniem `update`.</span><span class="sxs-lookup"><span data-stu-id="143b8-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="143b8-145">Przywracanie pakietów</span><span class="sxs-lookup"><span data-stu-id="143b8-145">Restore packages</span></span>

<span data-ttu-id="143b8-146">Użyj [przywrócić](../tools/cli-ref-restore.md) polecenia, które pobiera i instaluje wszystkie pakiety brakuje *pakietów* folderu.</span><span class="sxs-lookup"><span data-stu-id="143b8-146">Use the [restore](../tools/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="143b8-147">`restore` tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="143b8-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="143b8-148">Aby przywrócić zależności projektu, należy zmodyfikować `packages.config`, następnie za pomocą `restore` polecenia.</span><span class="sxs-lookup"><span data-stu-id="143b8-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="143b8-149">Podobnie jak w przypadku innych `dotnet` poleceń interfejsu wiersza polecenia, najpierw otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="143b8-149">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="143b8-150">Aby przywrócić dane przy użyciu pakietu `restore`:</span><span class="sxs-lookup"><span data-stu-id="143b8-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```