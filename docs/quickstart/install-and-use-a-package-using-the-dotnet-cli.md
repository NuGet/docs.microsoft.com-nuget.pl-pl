---
title: Instalowanie i używanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy na temat procesu instalowania i używania pakietu NuGet w projekcie .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231281"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="d9093-103">Szybki start: instalowanie i używanie pakietu przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="d9093-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="d9093-104">Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępniają do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="d9093-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="d9093-105">Zobacz [Co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="d9093-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="d9093-106">Pakiety są instalowane w `dotnet add package` projekcie .NET Core przy użyciu polecenia opisanego w tym artykule dla popularnego pakietu [Newtonsoft.Json.](https://www.nuget.org/packages/Newtonsoft.Json/)</span><span class="sxs-lookup"><span data-stu-id="d9093-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="d9093-107">Po zainstalowaniu należy zapoznać `using <namespace>` się \<z\> pakietem w kodzie, w którym obszar nazw jest specyficzny dla używanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9093-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="d9093-108">Następnie można użyć interfejsu API pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9093-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="d9093-109">**Zacznij od nuget.org:** Przeglądanie nuget.org to sposób, w jaki deweloperzy platformy .NET zazwyczaj znajdują składniki, których mogą ponownie wykorzystać we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="d9093-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="d9093-110">Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="d9093-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9093-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d9093-111">Prerequisites</span></span>

- <span data-ttu-id="d9093-112">Zestaw [SDK .NET Core](https://www.microsoft.com/net/download/) `dotnet` , który udostępnia narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d9093-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="d9093-113">Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnego .NET Core obciążeń związanych.</span><span class="sxs-lookup"><span data-stu-id="d9093-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="d9093-114">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="d9093-114">Create a project</span></span>

<span data-ttu-id="d9093-115">Pakiety NuGet mogą być instalowane w projekcie .NET pewnego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="d9093-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="d9093-116">W tym instruktażu utwórz prosty projekt konsoli .NET Core w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d9093-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="d9093-117">Utwórz folder dla projektu.</span><span class="sxs-lookup"><span data-stu-id="d9093-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="d9093-118">Otwórz wiersz polecenia i przełącz się do nowego folderu.</span><span class="sxs-lookup"><span data-stu-id="d9093-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="d9093-119">Utwórz projekt za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d9093-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="d9093-120">Służy `dotnet run` do testowania, czy aplikacja została utworzona poprawnie.</span><span class="sxs-lookup"><span data-stu-id="d9093-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="d9093-121">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="d9093-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="d9093-122">Aby zainstalować pakiet, `Newtonsoft.json` użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d9093-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="d9093-123">Po zakończeniu polecenia otwórz `.csproj` plik, aby wyświetlić dodane odwołanie:</span><span class="sxs-lookup"><span data-stu-id="d9093-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="d9093-124">Korzystanie z interfejsu API Newtonsoft.Json w aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9093-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="d9093-125">Otwórz `Program.cs` plik i dodaj następujący wiersz u góry pliku:</span><span class="sxs-lookup"><span data-stu-id="d9093-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="d9093-126">Dodaj następujący kod `class Program` przed wierszem:</span><span class="sxs-lookup"><span data-stu-id="d9093-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="d9093-127">Zastąp `Main` funkcję na następujące:</span><span class="sxs-lookup"><span data-stu-id="d9093-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="d9093-128">Tworzenie i uruchamianie aplikacji `dotnet run` za pomocą polecenia.</span><span class="sxs-lookup"><span data-stu-id="d9093-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="d9093-129">Dane wyjściowe powinny być reprezentacją JSON `Account` obiektu w kodzie:</span><span class="sxs-lookup"><span data-stu-id="d9093-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="d9093-130">Podobne wideo</span><span class="sxs-lookup"><span data-stu-id="d9093-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="d9093-131">Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="d9093-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9093-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9093-132">Next steps</span></span>

<span data-ttu-id="d9093-133">Gratulujemy instalacji i korzystania z pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="d9093-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d9093-134">Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="d9093-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="d9093-135">Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.</span><span class="sxs-lookup"><span data-stu-id="d9093-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="d9093-136">Omówienie i przepływ pracy zużycia pakietów</span><span class="sxs-lookup"><span data-stu-id="d9093-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="d9093-137">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="d9093-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="d9093-138">Odwołania do pakietu w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="d9093-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
