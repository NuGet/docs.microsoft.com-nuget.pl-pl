---
title: Instalowanie i używanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 47593cc65ad707b8880d854dc43824b9234fd44a
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833301"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="b6dcd-103">Szybki start: Instalowanie i używanie pakietu przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="b6dcd-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="b6dcd-104">Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="b6dcd-105">Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="b6dcd-106">Pakiety są instalowane w projekcie .NET Core za pomocą `dotnet add package` polecenia, zgodnie z opisem w tym artykule dla popularnego pakietu [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) .</span><span class="sxs-lookup"><span data-stu-id="b6dcd-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="b6dcd-107">Po zainstalowaniu programu zapoznaj się z pakietem w `using <namespace>` kodzie \<,\> gdzie przestrzeń nazw jest specyficzna dla używanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="b6dcd-108">Następnie można użyć interfejsu API pakietu.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="b6dcd-109">**Zacznij od NuGet.org**: Nuget.org przeglądania polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="b6dcd-110">Możesz przeszukiwać nuget.org bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6dcd-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b6dcd-111">Prerequisites</span></span>

- <span data-ttu-id="b6dcd-112">[Zestaw .NET Core SDK](https://www.microsoft.com/net/download/), która udostępnia `dotnet` narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="b6dcd-113">Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="b6dcd-114">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="b6dcd-114">Create a project</span></span>

<span data-ttu-id="b6dcd-115">Pakiety NuGet można instalować w projekcie .NET pewnego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="b6dcd-116">W tym instruktażu Utwórz prosty projekt konsoli programu .NET Core w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="b6dcd-117">Utwórz folder dla projektu.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="b6dcd-118">Otwórz wiersz polecenia i przejdź do nowego folderu.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="b6dcd-119">Utwórz projekt przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-119">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="b6dcd-120">Użyj `dotnet run` , aby sprawdzić, czy aplikacja została utworzona poprawnie.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="b6dcd-121">Dodawanie pakietu NuGet Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="b6dcd-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="b6dcd-122">Użyj następującego polecenia, aby zainstalować `Newtonsoft.json` pakiet:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="b6dcd-123">Po zakończeniu wykonywania polecenia Otwórz `.csproj` plik, aby wyświetlić dodane odwołanie:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="b6dcd-124">Korzystanie z interfejsu API Newtonsoft. JSON w aplikacji</span><span class="sxs-lookup"><span data-stu-id="b6dcd-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="b6dcd-125">`Program.cs` Otwórz plik i Dodaj następujący wiersz w górnej części pliku:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="b6dcd-126">Dodaj następujący kod przed `class Program` wierszem:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="b6dcd-127">Zastąp `Main` funkcję następującymi:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="b6dcd-128">Skompiluj i uruchom aplikację za pomocą `dotnet run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="b6dcd-129">Dane wyjściowe powinny być reprezentacją `Account` json obiektu w kodzie:</span><span class="sxs-lookup"><span data-stu-id="b6dcd-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="b6dcd-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6dcd-130">Next steps</span></span>

<span data-ttu-id="b6dcd-131">Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="b6dcd-131">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6dcd-132">Instalowanie i używanie pakietów przy użyciu interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="b6dcd-132">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="b6dcd-133">Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.</span><span class="sxs-lookup"><span data-stu-id="b6dcd-133">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="b6dcd-134">Omówienie użycia pakietu i przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="b6dcd-134">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="b6dcd-135">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="b6dcd-135">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="b6dcd-136">Odwołania do pakietu w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="b6dcd-136">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
