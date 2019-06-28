---
title: Instalowanie i Zarządzaj pakietami NuGet za pomocą interfejsu wiersza polecenia platformy dotnet
description: Instrukcje dotyczące używania interfejsu wiersza polecenia platformy dotnet do pracy z pakietów NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a8fd525f2446f9468664f1d80ef8808127a24be7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427642"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="44a8e-103">Instalowanie i zarządzanie pakietami za pomocą interfejsu wiersza polecenia platformy dotnet</span><span class="sxs-lookup"><span data-stu-id="44a8e-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="44a8e-104">Narzędzie interfejsu wiersza polecenia umożliwia łatwe instalowanie, odinstalowywanie oraz aktualizowanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="44a8e-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="44a8e-105">Działa w Windows, Mac OS X i Linux.</span><span class="sxs-lookup"><span data-stu-id="44a8e-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="44a8e-106">Wiersz polecenia dotnet jest do użytku w projekcie platformy .NET Core i .NET Standard (typy projektów zestawu SDK stylu) oraz wszelkich innych zestawu SDK stylu projektów (na przykład, zestawu SDK stylu projektu, który jest przeznaczony dla .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="44a8e-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="44a8e-107">Aby uzyskać więcej informacji, zobacz [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="44a8e-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="44a8e-108">W tym artykule przedstawiono podstawowe użycia kilka najbardziej typowe polecenia interfejsu wiersza polecenia platformy dotnet.</span><span class="sxs-lookup"><span data-stu-id="44a8e-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="44a8e-109">Dla większości z tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, o ile nie określono pliku projektu w poleceniu (plik projektu jest opcjonalnym przełącznikiem).</span><span class="sxs-lookup"><span data-stu-id="44a8e-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="44a8e-110">Aby uzyskać pełną listę poleceń i argumentów, można użyć, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="44a8e-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../tools/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44a8e-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44a8e-111">Prerequisites</span></span>

- <span data-ttu-id="44a8e-112">[Zestawu .NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="44a8e-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="44a8e-113">Począwszy od programu Visual Studio 2017, dotnet, których interfejs wiersza polecenia jest automatycznie instalowany z dowolnej platformy .NET Core powiązanych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="44a8e-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="44a8e-114">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="44a8e-114">Install a package</span></span>

<span data-ttu-id="44a8e-115">[polecenia DotNet Dodaj pakiet](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołania do pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="44a8e-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="44a8e-116">Otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="44a8e-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="44a8e-117">Aby zainstalować pakiet Nuget, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="44a8e-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="44a8e-118">Na przykład, aby zainstalować `Newtonsoft.Json` pakietów, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="44a8e-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="44a8e-119">Po wykonaniu polecenia, sprawdź plik projektu, aby upewnić się, że pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="44a8e-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="44a8e-120">Możesz otworzyć `.csproj` plik, aby zobaczyć odwołania dodane:</span><span class="sxs-lookup"><span data-stu-id="44a8e-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="44a8e-121">Instalowanie określonej wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="44a8e-121">Install a specific version of a package</span></span>

<span data-ttu-id="44a8e-122">Jeśli nie określono wersji, NuGet instaluje najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="44a8e-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="44a8e-123">Można również użyć [dotnet Dodaj pakiet](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) polecenie, aby zainstalować określoną wersję pakietu Nuget:</span><span class="sxs-lookup"><span data-stu-id="44a8e-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="44a8e-124">Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.Json` pakietów, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="44a8e-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="44a8e-125">Odwołania do pakietu z listy</span><span class="sxs-lookup"><span data-stu-id="44a8e-125">List package references</span></span>

<span data-ttu-id="44a8e-126">Możesz wyświetlić listę odwołań do pakietów dla projektów przy użyciu [dotnet wyświetlenia listy pakietów](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) polecenia.</span><span class="sxs-lookup"><span data-stu-id="44a8e-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="44a8e-127">Usuń pakiet</span><span class="sxs-lookup"><span data-stu-id="44a8e-127">Remove a package</span></span>

<span data-ttu-id="44a8e-128">Użyj [dotnet Usuń pakiet](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) polecenie, aby usunąć odwołanie do pakietu z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="44a8e-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="44a8e-129">Na przykład, aby usunąć `Newtonsoft.Json` pakietów, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="44a8e-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="44a8e-130">Aktualizacja pakietu</span><span class="sxs-lookup"><span data-stu-id="44a8e-130">Update a package</span></span>

<span data-ttu-id="44a8e-131">NuGet instaluje najnowszą wersję pakietu, gdy używasz `dotnet add package` polecenia, chyba że określisz wersja pakietu (`-v` przełącznika).</span><span class="sxs-lookup"><span data-stu-id="44a8e-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="44a8e-132">Przywracanie pakietów</span><span class="sxs-lookup"><span data-stu-id="44a8e-132">Restore packages</span></span>

<span data-ttu-id="44a8e-133">Użyj [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenia, które pakiety wymienione w pliku projektu (zobacz [PackageReference](../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="44a8e-133">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="44a8e-134">Za pomocą platformy .NET Core 2.0 i nowszych przywracania odbywa się automatycznie przy użyciu `dotnet build` i `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="44a8e-134">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="44a8e-135">Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="44a8e-135">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="44a8e-136">Aby przywrócić dane przy użyciu pakietu `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="44a8e-136">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```
