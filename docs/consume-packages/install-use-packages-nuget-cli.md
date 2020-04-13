---
title: Zarządzanie pakietami NuGet przy użyciu interfejsu wiersza polecenia nuget.exe
description: Instrukcje dotyczące korzystania z nuget.exe CLI do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428689"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="f5465-103">Zarządzanie pakietami przy użyciu interfejsu wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f5465-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="f5465-104">Narzędzie CLI umożliwia łatwą aktualizację i przywracanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="f5465-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="f5465-105">To narzędzie zapewnia wszystkie funkcje NuGet w systemie Windows, a także zapewnia większość funkcji na komputerach Mac i Linux podczas uruchamiania w obszarze Mono.</span><span class="sxs-lookup"><span data-stu-id="f5465-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="f5465-106">Cli `nuget.exe` jest dla projektu .NET Framework i projektów w stylu innych niż SDK (na przykład projekt stylu innych niż SDK, który jest przeznaczony dla bibliotek .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="f5465-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="f5465-107">Jeśli używasz projektu w stylu nieskładu SDK, który został zmigrowany do `PackageReference`, użyj `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f5465-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="f5465-108">Cli `nuget.exe` wymaga pliku [packages.config](../reference/packages-config.md) dla odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="f5465-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="f5465-109">W większości scenariuszy zaleca się [migrację projektów w stylu innych niż SDK,](../consume-packages/migrate-packages-config-to-package-reference.md) które używają `packages.config` do PackageReference, a następnie można użyć `dotnet` interfejsu wiersza polecenia zamiast interfejsu wiersza `nuget.exe` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f5465-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="f5465-110">Migracja nie jest obecnie dostępna dla projektów języka C++ i ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f5465-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="f5465-111">W tym artykule przedstawiono podstawowe użycie `nuget.exe` kilku najczęściej spotykanych poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f5465-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="f5465-112">W przypadku większości z tych poleceń narzędzie interfejsu wiersza polecenia wyszukuje plik projektu w bieżącym katalogu, chyba że w poleceniu określono plik projektu.</span><span class="sxs-lookup"><span data-stu-id="f5465-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="f5465-113">Aby uzyskać pełną listę poleceń i argumenty, których można użyć, zobacz [odwołanie do interfejsu wiersza polecenia nuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f5465-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5465-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f5465-114">Prerequisites</span></span>

- <span data-ttu-id="f5465-115">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go `.exe` z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując ten plik do odpowiedniego folderu i dodając ten folder do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="f5465-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="f5465-116">Instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="f5465-116">Install a package</span></span>

<span data-ttu-id="f5465-117">Polecenie [install](../reference/cli-reference/cli-ref-install.md) pobiera i instaluje pakiet w projekcie, domyślnie w bieżącym folderze, przy użyciu określonych źródeł pakietu.</span><span class="sxs-lookup"><span data-stu-id="f5465-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="f5465-118">Zainstaluj nowe pakiety w folderze *pakietów* w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="f5465-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5465-119">Polecenie `install`nie modyfikuje pliku projektu ani *pliku packages.config*; w ten sposób jest `restore` podobny do tego, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="f5465-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="f5465-120">Aby dodać zależność, dodaj pakiet za pośrednictwem interfejsu użytkownika menedżera pakietów lub konsoli w programie Visual `install` `restore`Studio lub zmodyfikuj *plik packages.config,* a następnie uruchom albo .</span><span class="sxs-lookup"><span data-stu-id="f5465-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="f5465-121">Otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="f5465-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="f5465-122">Użyj następującego polecenia, aby zainstalować pakiet NuGet w folderze *pakietów.*</span><span class="sxs-lookup"><span data-stu-id="f5465-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="f5465-123">Aby zainstalować `Newtonsoft.json` pakiet w folderze *pakietów,* użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f5465-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="f5465-124">Alternatywnie można użyć następującego polecenia, aby zainstalować pakiet `packages.config` NuGet przy użyciu istniejącego pliku do folderu *pakietów.*</span><span class="sxs-lookup"><span data-stu-id="f5465-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="f5465-125">Nie powoduje to dodania pakietu do zależności projektu, ale instaluje go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f5465-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="f5465-126">Instalowanie określonej wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="f5465-126">Install a specific version of a package</span></span>

<span data-ttu-id="f5465-127">Jeśli wersja nie jest określona podczas korzystania z polecenia [install,](../reference/cli-reference/cli-ref-install.md) NuGet instaluje najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="f5465-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="f5465-128">Można również zainstalować określoną wersję pakietu Nuget:</span><span class="sxs-lookup"><span data-stu-id="f5465-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="f5465-129">Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.json` pakietu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f5465-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="f5465-130">Aby uzyskać więcej informacji na `install`temat ograniczeń i zachowania programu , zobacz [Instalowanie pakietu](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="f5465-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="f5465-131">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="f5465-131">Remove a package</span></span>

<span data-ttu-id="f5465-132">Aby usunąć jeden lub więcej pakietów, usuń pakiety, które chcesz usunąć z folderu *pakietów.*</span><span class="sxs-lookup"><span data-stu-id="f5465-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="f5465-133">Jeśli chcesz ponownie zainstalować pakiety, `restore` `install` użyj polecenia lub polecenia.</span><span class="sxs-lookup"><span data-stu-id="f5465-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="f5465-134">Lista pakietów</span><span class="sxs-lookup"><span data-stu-id="f5465-134">List packages</span></span>

<span data-ttu-id="f5465-135">Za pomocą polecenia [list](../reference/cli-reference/cli-ref-list.md) można wyświetlić listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="f5465-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="f5465-136">Użyj `-Source` tej opcji, aby ograniczyć wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="f5465-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="f5465-137">Na przykład lista pakietów w folderze *pakietów.*</span><span class="sxs-lookup"><span data-stu-id="f5465-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="f5465-138">Jeśli używasz wyszukiwanego terminu, wyszukiwanie zawiera nazwy pakietów, tagów i opisów pakietów.</span><span class="sxs-lookup"><span data-stu-id="f5465-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="f5465-139">Aktualizowanie pojedynczego pakietu</span><span class="sxs-lookup"><span data-stu-id="f5465-139">Update an individual package</span></span>

<span data-ttu-id="f5465-140">NuGet instaluje najnowszą wersję pakietu `install` podczas korzystania z polecenia, chyba że określisz wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="f5465-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="f5465-141">Aktualizuj wszystkie pakiety</span><span class="sxs-lookup"><span data-stu-id="f5465-141">Update all packages</span></span>

<span data-ttu-id="f5465-142">Użyj polecenia [update,](../reference/cli-reference/cli-ref-update.md) aby zaktualizować wszystkie pakiety.</span><span class="sxs-lookup"><span data-stu-id="f5465-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="f5465-143">Aktualizuje wszystkie pakiety `packages.config`w projekcie (za pomocą) do ich najnowszych dostępnych wersji.</span><span class="sxs-lookup"><span data-stu-id="f5465-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="f5465-144">Zaleca się uruchomienie `restore` przed `update`uruchomieniem .</span><span class="sxs-lookup"><span data-stu-id="f5465-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="f5465-145">Przywracanie pakietów</span><span class="sxs-lookup"><span data-stu-id="f5465-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="f5465-146">Pobierz wersję interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="f5465-146">Get the CLI version</span></span>

<span data-ttu-id="f5465-147">Użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f5465-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="f5465-148">Pierwszy wiersz w danych wyjściowych pomocy pokazuje wersję.</span><span class="sxs-lookup"><span data-stu-id="f5465-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="f5465-149">Aby uniknąć przewijania `nuget help | more` w górę, użyj zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f5465-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>