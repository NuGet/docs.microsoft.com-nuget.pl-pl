---
title: Przewodnik wprowadzający się za pomocą NuGet pakiety za pośrednictwem dotnet interfejsu wiersza polecenia
description: Samouczek wskazówki na proces instalowania i używania pakietu NuGet w projekcie platformy .NET Core.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 41a249394a8a0504cc8841d3bdb67ad29ec2dc26
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="6dd34-103">Szybki Start: Instalacji i używania pakietu platformy dotnet interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="6dd34-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="6dd34-104">Pakiety NuGet zawiera kod wielokrotnego użytku, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="6dd34-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="6dd34-105">Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="6dd34-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="6dd34-106">Pakiety są zainstalowane w projekcie platformy .NET Core za pomocą `dotnet add package` polecenia zgodnie z opisem w tym artykule popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu.</span><span class="sxs-lookup"><span data-stu-id="6dd34-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="6dd34-107">Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz.</span><span class="sxs-lookup"><span data-stu-id="6dd34-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="6dd34-108">Następnie można użyć interfejsu API pakietu.</span><span class="sxs-lookup"><span data-stu-id="6dd34-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="6dd34-109">**Rozpoczynać nuget.org**: nuget.org przeglądania jest jak .NET deweloperzy zazwyczaj znaleźć składników może zostać ponownie użyty we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="6dd34-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="6dd34-110">Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="6dd34-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dd34-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6dd34-111">Prerequisites</span></span>

- <span data-ttu-id="6dd34-112">[.NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="6dd34-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="6dd34-113">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="6dd34-113">Create a project</span></span>

<span data-ttu-id="6dd34-114">Można zainstalować pakietów NuGet w projekcie .NET określonego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="6dd34-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="6dd34-115">W ramach tego przewodnika Utwórz prosty projekt konsoli .NET Core w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6dd34-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="6dd34-116">Utwórz folder dla projektu.</span><span class="sxs-lookup"><span data-stu-id="6dd34-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="6dd34-117">Utwórz projekt za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6dd34-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="6dd34-118">Użyj `dotnet run` do przetestowania, czy aplikacja została utworzona poprawnie.</span><span class="sxs-lookup"><span data-stu-id="6dd34-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="6dd34-119">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="6dd34-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="6dd34-120">Użyj następującego polecenia, aby zainstalować `Newtonsoft.json` pakietu:</span><span class="sxs-lookup"><span data-stu-id="6dd34-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="6dd34-121">Po zakończeniu działania polecenia Otwórz `.csproj` plik, aby wyświetlić odwołania dodane:</span><span class="sxs-lookup"><span data-stu-id="6dd34-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="6dd34-122">Użyj Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="6dd34-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="6dd34-123">Otwórz `Program.cs` pliku i Dodaj następujący wiersz na początku pliku:</span><span class="sxs-lookup"><span data-stu-id="6dd34-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="6dd34-124">Dodaj następujący kod przed `class Program` wiersza:</span><span class="sxs-lookup"><span data-stu-id="6dd34-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="6dd34-125">Zastąp `Main` funkcji z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6dd34-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="6dd34-126">Tworzenie i uruchamianie aplikacji przy użyciu `dotnet run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="6dd34-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="6dd34-127">Dane wyjściowe powinny mieć reprezentacja JSON `Account` obiektu w kodzie:</span><span class="sxs-lookup"><span data-stu-id="6dd34-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="6dd34-128">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="6dd34-128">Related articles</span></span>

- [<span data-ttu-id="6dd34-129">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="6dd34-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="6dd34-130">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="6dd34-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="6dd34-131">Sposoby instalacji pakietu</span><span class="sxs-lookup"><span data-stu-id="6dd34-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="6dd34-132">Konfigurowanie zachowania programu NuGet</span><span class="sxs-lookup"><span data-stu-id="6dd34-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
