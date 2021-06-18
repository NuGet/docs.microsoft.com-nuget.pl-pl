---
title: Instalowanie pakietów NuGet i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet
description: Instrukcje dotyczące używania interfejsu wiersza polecenia dotnet do pracy z pakietami NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 62c05aad388c25120d5b9f5143017a2f4f3b276b
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323612"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="d28d4-103">Instalowanie pakietów i zarządzanie nimi przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="d28d4-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="d28d4-104">Narzędzie interfejsu wiersza polecenia umożliwia łatwe instalowanie, odinstalowywanie i aktualizowanie pakietów NuGet w projektach i rozwiązaniach.</span><span class="sxs-lookup"><span data-stu-id="d28d4-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="d28d4-105">Działa w systemach Windows, Mac OS X i Linux.</span><span class="sxs-lookup"><span data-stu-id="d28d4-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="d28d4-106">Interfejs wiersza polecenia dotnet jest przeznaczony do użycia w projekcie .NET Core i .NET Standard (typy projektów w stylu zestawu SDK) oraz w innych projektach w stylu zestawu SDK (na przykład w projekcie w stylu zestawu SDK przeznaczonym dla .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="d28d4-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="d28d4-107">Aby uzyskać więcej informacji, zobacz [Atrybut zestawu SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="d28d4-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="d28d4-108">W tym artykule przedstawiono podstawowe użycie kilku najpopularniejszych poleceń interfejsu wiersza polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="d28d4-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="d28d4-109">W przypadku większości tych poleceń narzędzie interfejsu wiersza polecenia szuka pliku projektu w bieżącym katalogu, chyba że w poleceniu określono plik projektu (plik projektu jest opcjonalnym przełącznikiem).</span><span class="sxs-lookup"><span data-stu-id="d28d4-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="d28d4-110">Aby uzyskać pełną listę poleceń i argumentów, których można użyć, zobacz narzędzia interfejsu wiersza polecenia [(CLI) programu .NET Core.](../reference/dotnet-commands.md)</span><span class="sxs-lookup"><span data-stu-id="d28d4-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d28d4-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d28d4-111">Prerequisites</span></span>

- <span data-ttu-id="d28d4-112">Narzędzie [zestaw .NET Core SDK](https://www.microsoft.com/net/download/), które udostępnia `dotnet` narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d28d4-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="d28d4-113">Począwszy od Visual Studio 2017 r., interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami powiązanymi z programem .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d28d4-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="d28d4-114">Instalowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="d28d4-114">Install a package</span></span>

<span data-ttu-id="d28d4-115">[Dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) dodaje odwołanie do pakietu do pliku projektu, a następnie uruchamia program `dotnet restore` w celu zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="d28d4-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="d28d4-116">Otwórz wiersz polecenia i przejdź do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="d28d4-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="d28d4-117">Użyj następującego polecenia, aby zainstalować pakiet NuGet:</span><span class="sxs-lookup"><span data-stu-id="d28d4-117">Use the following command to install a NuGet package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="d28d4-118">Aby na przykład zainstalować `Newtonsoft.Json` pakiet, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="d28d4-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="d28d4-119">Po zakończeniu polecenia sprawdź plik projektu, aby upewnić się, że pakiet został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="d28d4-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="d28d4-120">Możesz otworzyć `.csproj` plik, aby zobaczyć dodane odwołanie:</span><span class="sxs-lookup"><span data-stu-id="d28d4-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="d28d4-121">Instalowanie określonej wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="d28d4-121">Install a specific version of a package</span></span>

<span data-ttu-id="d28d4-122">Jeśli wersja nie zostanie określona, program NuGet zainstaluje najnowszą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="d28d4-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="d28d4-123">Możesz również użyć polecenia [dotnet add package,](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) aby zainstalować określoną wersję pakietu NuGet:</span><span class="sxs-lookup"><span data-stu-id="d28d4-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a NuGet package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="d28d4-124">Aby na przykład dodać wersję 12.0.1 `Newtonsoft.Json` pakietu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d28d4-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="d28d4-125">Lista odwołań do pakietów</span><span class="sxs-lookup"><span data-stu-id="d28d4-125">List package references</span></span>

<span data-ttu-id="d28d4-126">Odwołania do pakietu dla projektu można wyświetlić za pomocą polecenia [dotnet list package.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)</span><span class="sxs-lookup"><span data-stu-id="d28d4-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="d28d4-127">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="d28d4-127">Remove a package</span></span>

<span data-ttu-id="d28d4-128">Użyj polecenia [dotnet remove package,](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) aby usunąć odwołanie do pakietu z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="d28d4-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="d28d4-129">Aby na przykład usunąć `Newtonsoft.Json` pakiet, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="d28d4-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="d28d4-130">Aktualizowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="d28d4-130">Update a package</span></span>

<span data-ttu-id="d28d4-131">NuGet instaluje najnowszą wersję pakietu podczas korzystania z polecenia , chyba że określisz wersję `dotnet add package` pakietu `-v` (przełącznik).</span><span class="sxs-lookup"><span data-stu-id="d28d4-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="d28d4-132">Przywracanie pakietów</span><span class="sxs-lookup"><span data-stu-id="d28d4-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
