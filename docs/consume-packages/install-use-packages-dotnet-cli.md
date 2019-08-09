---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet
description: Instrukcje dotyczące używania interfejsu wiersza polecenia dotnet do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: d9e9f0026e4c907351b4b0cd0adced28a4670575
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860590"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="dc164-103">Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="dc164-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="dc164-104">Narzędzie interfejsu wiersza polecenia umożliwia łatwe instalowanie, Odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="dc164-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="dc164-105">Działa w systemach Windows, Mac OS X i Linux.</span><span class="sxs-lookup"><span data-stu-id="dc164-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="dc164-106">Interfejs wiersza polecenia dotnet jest używany w projekcie .NET Core i .NET Standard projektu (typy projektów w stylu zestawu SDK) oraz dla innych projektów w stylu zestawu SDK (na przykład projekt w stylu zestawu SDK, który jest przeznaczony dla .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="dc164-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="dc164-107">Aby uzyskać więcej informacji, zobacz [atrybut zestawu SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="dc164-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="dc164-108">W tym artykule przedstawiono podstawowe użycie kilku typowych poleceń interfejsu wiersza polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="dc164-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="dc164-109">W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu (plik projektu jest przełącznikiem opcjonalnym).</span><span class="sxs-lookup"><span data-stu-id="dc164-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="dc164-110">Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz [Narzędzia interfejsu wiersza polecenia (CLI) platformy .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="dc164-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc164-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dc164-111">Prerequisites</span></span>

- <span data-ttu-id="dc164-112">[Zestaw .NET Core SDK](https://www.microsoft.com/net/download/), która udostępnia `dotnet` narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="dc164-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="dc164-113">Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.</span><span class="sxs-lookup"><span data-stu-id="dc164-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="dc164-114">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="dc164-114">Install a package</span></span>

<span data-ttu-id="dc164-115">polecenie [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołanie do pakietu do pliku projektu, a następnie `dotnet restore` uruchamia polecenie, aby zainstalować pakiet.</span><span class="sxs-lookup"><span data-stu-id="dc164-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="dc164-116">Otwórz wiersz polecenia i przejdź do katalogu, który zawiera plik projektu.</span><span class="sxs-lookup"><span data-stu-id="dc164-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="dc164-117">Użyj następującego polecenia, aby zainstalować pakiet NuGet:</span><span class="sxs-lookup"><span data-stu-id="dc164-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="dc164-118">Na przykład aby zainstalować `Newtonsoft.Json` pakiet, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="dc164-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="dc164-119">Po zakończeniu wykonywania polecenia Sprawdź plik projektu, aby upewnić się, że pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="dc164-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="dc164-120">Możesz otworzyć `.csproj` plik, aby zobaczyć dodane odwołanie:</span><span class="sxs-lookup"><span data-stu-id="dc164-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="dc164-121">Zainstaluj określoną wersję pakietu</span><span class="sxs-lookup"><span data-stu-id="dc164-121">Install a specific version of a package</span></span>

<span data-ttu-id="dc164-122">Jeśli wersja nie zostanie określona, NuGet zainstaluje najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="dc164-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="dc164-123">Aby zainstalować określoną wersję pakietu NuGet, można również użyć polecenia [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) :</span><span class="sxs-lookup"><span data-stu-id="dc164-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="dc164-124">Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.Json` pakietu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="dc164-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="dc164-125">Wyświetl listę odwołań do pakietów</span><span class="sxs-lookup"><span data-stu-id="dc164-125">List package references</span></span>

<span data-ttu-id="dc164-126">Możesz wyświetlić listę odwołań do pakietów dla projektu przy użyciu polecenia [pakietu dotnet list](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) .</span><span class="sxs-lookup"><span data-stu-id="dc164-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="dc164-127">Usuń pakiet</span><span class="sxs-lookup"><span data-stu-id="dc164-127">Remove a package</span></span>

<span data-ttu-id="dc164-128">Aby usunąć odwołanie do pakietu z pliku projektu, użyj polecenia [dotnet Remove Package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) .</span><span class="sxs-lookup"><span data-stu-id="dc164-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="dc164-129">Na przykład aby usunąć `Newtonsoft.Json` pakiet, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="dc164-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="dc164-130">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="dc164-130">Update a package</span></span>

<span data-ttu-id="dc164-131">Pakiet NuGet instaluje najnowszą wersję pakietu przy użyciu `dotnet add package` polecenia, o ile nie zostanie określona wersja pakietu (`-v` przełącznik).</span><span class="sxs-lookup"><span data-stu-id="dc164-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="dc164-132">Przywróć pakiety</span><span class="sxs-lookup"><span data-stu-id="dc164-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
