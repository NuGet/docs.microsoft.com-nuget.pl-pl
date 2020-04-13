---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet
description: Instrukcje dotyczące korzystania z dotnet CLI do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825162"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="1e021-103">Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="1e021-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="1e021-104">Narzędzie CLI umożliwia łatwe instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="1e021-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="1e021-105">Działa w systemach Windows, Mac OS X i Linux.</span><span class="sxs-lookup"><span data-stu-id="1e021-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="1e021-106">Dotnet CLI jest do użytku w projekcie .NET Core i .NET Standard (typy projektów w stylu SDK) oraz dla wszystkich innych projektów w stylu SDK (na przykład projektu w stylu SDK, który jest przeznaczony dla platformy .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="1e021-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="1e021-107">Aby uzyskać więcej informacji, zobacz [atrybut SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="1e021-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="1e021-108">W tym artykule przedstawiono podstawowe użycie kilku najczęściej spotykanych poleceń dotnet CLI.</span><span class="sxs-lookup"><span data-stu-id="1e021-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="1e021-109">W przypadku większości z tych poleceń narzędzie interfejsu wiersza polecenia wyszukuje plik projektu w bieżącym katalogu, chyba że plik projektu jest określony w poleceniu (plik projektu jest przełącznikiem opcjonalnym).</span><span class="sxs-lookup"><span data-stu-id="1e021-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="1e021-110">Aby uzyskać pełną listę poleceń i argumenty, których można użyć, zobacz [narzędzia interfejsu wiersza polecenia .NET Core .](../reference/dotnet-commands.md)</span><span class="sxs-lookup"><span data-stu-id="1e021-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e021-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1e021-111">Prerequisites</span></span>

- <span data-ttu-id="1e021-112">Zestaw [SDK .NET Core](https://www.microsoft.com/net/download/) `dotnet` , który udostępnia narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1e021-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="1e021-113">Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnego .NET Core obciążeń związanych.</span><span class="sxs-lookup"><span data-stu-id="1e021-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="1e021-114">Instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="1e021-114">Install a package</span></span>

<span data-ttu-id="1e021-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołanie do pakietu `dotnet restore` do pliku projektu, a następnie uruchamia się, aby zainstalować pakiet.</span><span class="sxs-lookup"><span data-stu-id="1e021-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="1e021-116">Otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="1e021-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="1e021-117">Aby zainstalować pakiet Nuget, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1e021-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="1e021-118">Na przykład, aby `Newtonsoft.Json` zainstalować pakiet, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="1e021-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="1e021-119">Po zakończeniu polecenia, spójrz na plik projektu, aby upewnić się, że pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="1e021-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="1e021-120">Możesz otworzyć `.csproj` plik, aby wyświetlić dodane odwołanie:</span><span class="sxs-lookup"><span data-stu-id="1e021-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="1e021-121">Instalowanie określonej wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="1e021-121">Install a specific version of a package</span></span>

<span data-ttu-id="1e021-122">Jeśli wersja nie jest określona, NuGet instaluje najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e021-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="1e021-123">Można również użyć polecenia [dotnet add package,](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) aby zainstalować określoną wersję pakietu Nuget:</span><span class="sxs-lookup"><span data-stu-id="1e021-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="1e021-124">Na przykład, aby dodać wersję 12.0.1 `Newtonsoft.Json` pakietu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1e021-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="1e021-125">Numery pakietów list</span><span class="sxs-lookup"><span data-stu-id="1e021-125">List package references</span></span>

<span data-ttu-id="1e021-126">Odwołania do pakietu dla projektu można wyświetlić za pomocą polecenia [pakietu listy dotnet.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)</span><span class="sxs-lookup"><span data-stu-id="1e021-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="1e021-127">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="1e021-127">Remove a package</span></span>

<span data-ttu-id="1e021-128">Użyj polecenia [dotnet remove package,](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) aby usunąć odwołanie do pakietu z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="1e021-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="1e021-129">Na przykład, aby `Newtonsoft.Json` usunąć pakiet, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="1e021-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="1e021-130">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="1e021-130">Update a package</span></span>

<span data-ttu-id="1e021-131">NuGet instaluje najnowszą wersję pakietu `dotnet add package` podczas korzystania z polecenia,`-v` chyba że określisz wersję pakietu ( przełącznik).</span><span class="sxs-lookup"><span data-stu-id="1e021-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="1e021-132">Przywracanie pakietów</span><span class="sxs-lookup"><span data-stu-id="1e021-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
