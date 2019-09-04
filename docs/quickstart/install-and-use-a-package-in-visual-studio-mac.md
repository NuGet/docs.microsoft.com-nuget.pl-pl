---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio dla komputerów Mac
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie Visual Studio dla komputerów Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238526"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="f3381-103">Szybki start: Instalowanie i używanie pakietu w Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="f3381-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="f3381-104">Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="f3381-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="f3381-105">Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="f3381-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="f3381-106">Pakiety są instalowane w projekcie Visual Studio dla komputerów Mac przy użyciu Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3381-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="f3381-107">W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu konsoli .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f3381-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="f3381-108">Ten sam proces ma zastosowanie do dowolnego innego projektu Xamarin lub .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f3381-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="f3381-109">Po zainstalowaniu programu zapoznaj się z pakietem w `using <namespace>` kodzie \<,\> gdzie przestrzeń nazw jest specyficzna dla używanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="f3381-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="f3381-110">Po wprowadzeniu odwołania można wywołać pakiet za pomocą jego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f3381-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="f3381-111">**Zacznij od NuGet.org**: *NuGet.org* przeglądania polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="f3381-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="f3381-112">Możesz przeszukiwać *NuGet.org* bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="f3381-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="f3381-113">Aby uzyskać ogólne informacje, zobacz [Znajdź i Oceń pakiety NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f3381-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3381-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f3381-114">Prerequisites</span></span>

- <span data-ttu-id="f3381-115">Program Visual Studio 2019 dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="f3381-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="f3381-116">Wersję 2019 Community można zainstalować bezpłatnie z usługi [VisualStudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f3381-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="f3381-117">Jeśli używasz programu Visual Studio w systemie Windows, zobacz [Instalowanie i używanie pakietu w programie Visual Studio (tylko system Windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f3381-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="f3381-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="f3381-118">Create a project</span></span>

<span data-ttu-id="f3381-119">Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje tę samą platformę docelową co projekt.</span><span class="sxs-lookup"><span data-stu-id="f3381-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="f3381-120">W tym instruktażu należy użyć prostej aplikacji konsolowej platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f3381-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="f3381-121">Utwórz projekt w Visual Studio dla komputerów Mac przy użyciu **pliku > nowe rozwiązanie...** , wybierz **aplikację .NET Core > Application > szablon aplikacji konsolowej** .</span><span class="sxs-lookup"><span data-stu-id="f3381-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="f3381-122">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="f3381-122">Click **Next**.</span></span> <span data-ttu-id="f3381-123">Po wyświetleniu monitu zaakceptuj wartości domyślne dla **platformy docelowej** .</span><span class="sxs-lookup"><span data-stu-id="f3381-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="f3381-124">Program Visual Studio tworzy projekt, który zostanie otwarty w Eksplorator rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="f3381-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="f3381-125">Dodawanie pakietu NuGet Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="f3381-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="f3381-126">Aby zainstalować pakiet, należy użyć Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3381-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="f3381-127">Podczas instalacji pakietu NuGet rejestruje zależność w pliku projektu lub `packages.config` pliku (w zależności od formatu projektu).</span><span class="sxs-lookup"><span data-stu-id="f3381-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="f3381-128">Aby uzyskać więcej informacji, zobacz [Omówienie użycia pakietu i przepływ pracy](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="f3381-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="f3381-129">Menedżer pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="f3381-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="f3381-130">W Eksplorator rozwiązań kliknij prawym przyciskiem myszy pozycję **zależności** i wybierz polecenie **Dodaj pakiety..** ..</span><span class="sxs-lookup"><span data-stu-id="f3381-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Polecenie zarządzania pakietami NuGet dla odwołań do projektu](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="f3381-132">Wybierz pozycję "nuget.org" jako **Źródło pakietu** w lewym górnym rogu okna dialogowego, a następnie wyszukaj ciąg **Newtonsoft. JSON**, wybierz ten pakiet z listy, a następnie wybierz pozycję **Dodaj pakiety...** :</span><span class="sxs-lookup"><span data-stu-id="f3381-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="f3381-134">Aby uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą Visual Studio dla komputerów Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f3381-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="f3381-135">Korzystanie z interfejsu API Newtonsoft. JSON w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f3381-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="f3381-136">Za pomocą pakietu Newtonsoft. JSON w projekcie można wywołać `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.</span><span class="sxs-lookup"><span data-stu-id="f3381-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="f3381-137">`Program.cs` Otwórz plik (znajdujący się w okienko rozwiązania) i Zastąp zawartość pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="f3381-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

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

1. <span data-ttu-id="f3381-138">Skompiluj i uruchom aplikację, wybierając pozycję **Uruchom, > rozpocząć debugowanie**:</span><span class="sxs-lookup"><span data-stu-id="f3381-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="f3381-139">Po uruchomieniu aplikacji zobaczysz serializowane dane wyjściowe JSON wyświetlane w konsoli programu:</span><span class="sxs-lookup"><span data-stu-id="f3381-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Dane wyjściowe aplikacji konsolowej](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="f3381-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3381-141">Next steps</span></span>
<span data-ttu-id="f3381-142">Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="f3381-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3381-143">Instalowanie pakietów i zarządzanie nimi przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="f3381-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="f3381-144">Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.</span><span class="sxs-lookup"><span data-stu-id="f3381-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="f3381-145">Omówienie użycia pakietu i przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="f3381-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="f3381-146">Odwołania do pakietu w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="f3381-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
