---
title: Przewodnik wprowadzający, aby za pomocą NuGet pakiety za pośrednictwem interfejsu wiersza polecenia platformy dotnet
description: Samouczek wskazówki dotyczące procesu o instalowaniu i używaniu pakietu NuGet w projekcie platformy .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1060d98278fed89ac63ee17c1896ae8bdce72a9e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426165"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="9e280-103">Szybki start: Instalowanie i używanie pakietu przy użyciu interfejsu wiersza polecenia platformy dotnet</span><span class="sxs-lookup"><span data-stu-id="9e280-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="9e280-104">Pakiety NuGet zawierają kodu wielokrotnego użytku, które inni deweloperzy zapewnić dostępność do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="9e280-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="9e280-105">Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="9e280-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="9e280-106">Pakiety zostaną zainstalowane do projektu .NET Core przy użyciu `dotnet add package` polecenia zgodnie z opisem w tym artykule, aby popularnej [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e280-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="9e280-107">Po zakończeniu instalacji można znaleźć pakietu w kodzie za pomocą `using <namespace>` gdzie \<przestrzeni nazw\> jest właściwa dla pakietu jest używany.</span><span class="sxs-lookup"><span data-stu-id="9e280-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="9e280-108">Następnie można użyć interfejsu API pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e280-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="9e280-109">**Rozpoczynać nuget.org**: Przeglądanie nuget.org znajduje się, jak .NET deweloperzy zazwyczaj znajdują składników ponownego wykorzystania w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="9e280-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="9e280-110">Można wyszukać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9e280-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e280-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e280-111">Prerequisites</span></span>

- <span data-ttu-id="9e280-112">[Zestawu .NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="9e280-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="9e280-113">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="9e280-113">Create a project</span></span>

<span data-ttu-id="9e280-114">Można zainstalować pakietów NuGet do projektu .NET pewnego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="9e280-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="9e280-115">W tym przewodniku Utwórz prosty projekt konsoli .NET Core w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9e280-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="9e280-116">Utwórz folder dla projektu.</span><span class="sxs-lookup"><span data-stu-id="9e280-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="9e280-117">Utwórz projekt za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9e280-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="9e280-118">Użyj `dotnet run` do przetestowania, czy aplikacja została utworzona prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="9e280-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="9e280-119">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="9e280-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="9e280-120">Użyj następującego polecenia, aby zainstalować `Newtonsoft.json` pakietu:</span><span class="sxs-lookup"><span data-stu-id="9e280-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="9e280-121">Po zakończeniu działania polecenia Otwórz `.csproj` plik, aby zobaczyć odwołania dodane:</span><span class="sxs-lookup"><span data-stu-id="9e280-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="9e280-122">Użyj pakietu Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="9e280-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="9e280-123">Otwórz `Program.cs` pliku i Dodaj następujący wiersz w górnej części pliku:</span><span class="sxs-lookup"><span data-stu-id="9e280-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="9e280-124">Dodaj następujący kod przed `class Program` wiersza:</span><span class="sxs-lookup"><span data-stu-id="9e280-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="9e280-125">Zastąp `Main` funkcji następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="9e280-125">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="9e280-126">Kompilowanie i uruchamianie aplikacji za pomocą `dotnet run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="9e280-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="9e280-127">Dane wyjściowe powinny być reprezentacji JSON `Account` obiektu w kodzie:</span><span class="sxs-lookup"><span data-stu-id="9e280-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="9e280-128">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="9e280-128">Related articles</span></span>

- [<span data-ttu-id="9e280-129">Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia platformy dotnet</span><span class="sxs-lookup"><span data-stu-id="9e280-129">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="9e280-130">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="9e280-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="9e280-131">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="9e280-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="9e280-132">Typowe konfiguracje NuGet</span><span class="sxs-lookup"><span data-stu-id="9e280-132">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
