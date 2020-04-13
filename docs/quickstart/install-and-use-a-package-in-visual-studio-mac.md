---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio dla komputerów Mac
description: Samouczek instruktażowy na temat procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio dla komputerów Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238526"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="590b5-103">Szybki start: instalowanie i używanie pakietu w programie Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="590b5-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="590b5-104">Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępniają do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="590b5-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="590b5-105">Zobacz [Co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="590b5-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="590b5-106">Pakiety są instalowane w projekcie programu Visual Studio dla komputerów Mac przy użyciu Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="590b5-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="590b5-107">W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu konsoli .NET Core.</span><span class="sxs-lookup"><span data-stu-id="590b5-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="590b5-108">Ten sam proces dotyczy każdego innego projektu platformy Xamarin lub .NET Core.</span><span class="sxs-lookup"><span data-stu-id="590b5-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="590b5-109">Po zainstalowaniu należy zapoznać `using <namespace>` się \<z\> pakietem w kodzie, w którym obszar nazw jest specyficzny dla używanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="590b5-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="590b5-110">Po nawiązaniu odwołania można wywołać pakiet za pośrednictwem jego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="590b5-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="590b5-111">**Zacznij od nuget.org:** Przeglądanie *nuget.org* to sposób, w jaki deweloperzy platformy .NET zazwyczaj znajdują składniki, których mogą ponownie wykorzystać we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="590b5-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="590b5-112">Można wyszukiwać *nuget.org* bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="590b5-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="590b5-113">Aby uzyskać ogólne informacje, zobacz [Znajdowanie i ocenianie pakietów NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="590b5-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="590b5-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="590b5-114">Prerequisites</span></span>

- <span data-ttu-id="590b5-115">Visual Studio 2019 dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="590b5-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="590b5-116">Wersję społeczności 2019 można zainstalować bezpłatnie w [visualstudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="590b5-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="590b5-117">Jeśli używasz programu Visual Studio w systemie Windows, zobacz [Instalowanie i używanie pakietu w programie Visual Studio (tylko dla systemu Windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="590b5-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="590b5-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="590b5-118">Create a project</span></span>

<span data-ttu-id="590b5-119">Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje taką samą platformę docelową jak projekt.</span><span class="sxs-lookup"><span data-stu-id="590b5-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="590b5-120">W tym instruktażu należy użyć prostej aplikacji konsoli .NET Core Console.</span><span class="sxs-lookup"><span data-stu-id="590b5-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="590b5-121">Utwórz projekt w programie Visual Studio dla komputerów Mac przy użyciu **> nowego rozwiązania plików...**, wybierz szablon **aplikacji konsoli .NET Core > App > Console.**</span><span class="sxs-lookup"><span data-stu-id="590b5-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="590b5-122">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="590b5-122">Click **Next**.</span></span> <span data-ttu-id="590b5-123">Zaakceptuj wartości domyślne dla **platformy docelowej** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="590b5-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="590b5-124">Visual Studio tworzy projekt, który otwiera się w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="590b5-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="590b5-125">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="590b5-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="590b5-126">Aby zainstalować pakiet, należy użyć Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="590b5-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="590b5-127">Po zainstalowaniu pakietu NuGet rejestruje zależność w pliku projektu `packages.config` lub pliku (w zależności od formatu projektu).</span><span class="sxs-lookup"><span data-stu-id="590b5-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="590b5-128">Aby uzyskać więcej informacji, zobacz [Omówienie zużycia pakietów i przepływ pracy](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="590b5-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="590b5-129">Menedżer pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="590b5-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="590b5-130">W Eksploratorze **rozwiązań** kliknij prawym przyciskiem myszy pozycję Zależności i wybierz polecenie **Dodaj pakiety...**.</span><span class="sxs-lookup"><span data-stu-id="590b5-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Zarządzanie poleceniem NuGet Packages dla odwołań do projektu](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="590b5-132">Wybierz "nuget.org" jako **źródło pakietu** w lewym górnym rogu okna dialogowego i wyszukaj **plik Newtonsoft.Json**, wybierz ten pakiet na liście i wybierz pozycję **Dodaj pakiety...**:</span><span class="sxs-lookup"><span data-stu-id="590b5-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Lokalizowanie pakietu Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="590b5-134">Aby uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio dla komputerów Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="590b5-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="590b5-135">Korzystanie z interfejsu API Newtonsoft.Json w aplikacji</span><span class="sxs-lookup"><span data-stu-id="590b5-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="590b5-136">Za pomocą pakietu Newtonsoft.Json w projekcie `JsonConvert.SerializeObject` można wywołać jego metodę konwersji obiektu na ciąg czytelny dla człowieka.</span><span class="sxs-lookup"><span data-stu-id="590b5-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="590b5-137">Otwórz `Program.cs` plik (znajdujący się w panelu rozwiązania) i zastąp zawartość pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="590b5-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="590b5-138">Tworzenie i uruchamianie aplikacji przez wybranie **opcji Uruchom > Rozpocznij debugowanie:**</span><span class="sxs-lookup"><span data-stu-id="590b5-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="590b5-139">Po uruchomieniu aplikacji w konsoli pojawi się serializowane dane wyjściowe JSON:</span><span class="sxs-lookup"><span data-stu-id="590b5-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Dane wyjściowe aplikacji Console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="590b5-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="590b5-141">Next steps</span></span>
<span data-ttu-id="590b5-142">Gratulujemy instalacji i korzystania z pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="590b5-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="590b5-143">Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="590b5-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="590b5-144">Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.</span><span class="sxs-lookup"><span data-stu-id="590b5-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="590b5-145">Omówienie i przepływ pracy zużycia pakietów</span><span class="sxs-lookup"><span data-stu-id="590b5-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="590b5-146">Odwołania do pakietu w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="590b5-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
