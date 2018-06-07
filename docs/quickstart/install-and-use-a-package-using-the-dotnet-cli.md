---
title: Przewodnik wprowadzający się za pomocą NuGet pakiety za pośrednictwem dotnet interfejsu wiersza polecenia
description: Samouczek wskazówki na proces instalowania i używania pakietu NuGet w projekcie platformy .NET Core.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 2fac013de5457f26bbbaeff37209316daedcdbb0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816946"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="05a26-103">Szybki Start: Instalacji i używania pakietu platformy dotnet interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="05a26-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="05a26-104">Pakiety NuGet zawiera kod wielokrotnego użytku, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="05a26-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="05a26-105">Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="05a26-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="05a26-106">Pakiety są zainstalowane w projekcie platformy .NET Core za pomocą `dotnet add package` polecenia zgodnie z opisem w tym artykule popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu.</span><span class="sxs-lookup"><span data-stu-id="05a26-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="05a26-107">Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz.</span><span class="sxs-lookup"><span data-stu-id="05a26-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="05a26-108">Następnie można użyć interfejsu API pakietu.</span><span class="sxs-lookup"><span data-stu-id="05a26-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="05a26-109">**Rozpoczynać nuget.org**: nuget.org przeglądania jest jak .NET deweloperzy zazwyczaj znaleźć składników może zostać ponownie użyty we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="05a26-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="05a26-110">Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="05a26-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05a26-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="05a26-111">Prerequisites</span></span>

- <span data-ttu-id="05a26-112">[.NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="05a26-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="05a26-113">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="05a26-113">Create a project</span></span>

<span data-ttu-id="05a26-114">Można zainstalować pakietów NuGet w projekcie .NET określonego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="05a26-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="05a26-115">W ramach tego przewodnika Utwórz prosty projekt konsoli .NET Core w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="05a26-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="05a26-116">Utwórz folder dla projektu.</span><span class="sxs-lookup"><span data-stu-id="05a26-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="05a26-117">Utwórz projekt za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="05a26-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="05a26-118">Użyj `dotnet run` do przetestowania, czy aplikacja została utworzona poprawnie.</span><span class="sxs-lookup"><span data-stu-id="05a26-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="05a26-119">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="05a26-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="05a26-120">Użyj następującego polecenia, aby zainstalować `Newtonsoft.json` pakietu:</span><span class="sxs-lookup"><span data-stu-id="05a26-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="05a26-121">Po zakończeniu działania polecenia Otwórz `.csproj` plik, aby wyświetlić odwołania dodane:</span><span class="sxs-lookup"><span data-stu-id="05a26-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="05a26-122">Użyj Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="05a26-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="05a26-123">Otwórz `Program.cs` pliku i Dodaj następujący wiersz na początku pliku:</span><span class="sxs-lookup"><span data-stu-id="05a26-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="05a26-124">Dodaj następujący kod przed `class Program` wiersza:</span><span class="sxs-lookup"><span data-stu-id="05a26-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="05a26-125">Zastąp `Main` funkcji z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="05a26-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="05a26-126">Tworzenie i uruchamianie aplikacji przy użyciu `dotnet run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="05a26-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="05a26-127">Dane wyjściowe powinny mieć reprezentacja JSON `Account` obiektu w kodzie:</span><span class="sxs-lookup"><span data-stu-id="05a26-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="05a26-128">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="05a26-128">Related articles</span></span>

- [<span data-ttu-id="05a26-129">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="05a26-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="05a26-130">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="05a26-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="05a26-131">Sposoby instalacji pakietu</span><span class="sxs-lookup"><span data-stu-id="05a26-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="05a26-132">Konfigurowanie zachowania programu NuGet</span><span class="sxs-lookup"><span data-stu-id="05a26-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
