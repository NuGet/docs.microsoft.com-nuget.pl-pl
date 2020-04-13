---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio
description: Samouczek instruktażowy na temat procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147490"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="fe4c7-103">Szybki start: instalowanie i używanie pakietu w programie Visual Studio (tylko w systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="fe4c7-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="fe4c7-104">Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępniają do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="fe4c7-105">Zobacz [Co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="fe4c7-106">Pakiety są instalowane w projekcie programu Visual Studio przy użyciu Menedżera pakietów NuGet, [konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell)lub [interfejsu wiersza polecenia dotnet.](install-and-use-a-package-using-the-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="fe4c7-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="fe4c7-107">W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="fe4c7-108">Ten sam proces dotyczy każdego innego projektu .NET lub .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="fe4c7-109">Po zainstalowaniu należy zapoznać `using <namespace>` się \<z\> pakietem w kodzie, w którym obszar nazw jest specyficzny dla używanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="fe4c7-110">Po nawiązaniu odwołania można wywołać pakiet za pośrednictwem jego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="fe4c7-111">**Zacznij od nuget.org:** Przeglądanie *nuget.org* to sposób, w jaki deweloperzy platformy .NET zazwyczaj znajdują składniki, których mogą ponownie wykorzystać we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="fe4c7-112">Można wyszukiwać *nuget.org* bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="fe4c7-113">Aby uzyskać ogólne informacje, zobacz [Znajdowanie i ocenianie pakietów NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe4c7-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fe4c7-114">Prerequisites</span></span>

- <span data-ttu-id="fe4c7-115">Visual Studio 2019 z obciążeniem .NET desktop development.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="fe4c7-116">Wersję społeczności 2019 można zainstalować bezpłatnie w [visualstudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="fe4c7-117">Jeśli używasz programu Visual Studio dla komputerów Mac, zobacz [Instalowanie i używanie pakietu w programie Visual Studio dla komputerów Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="fe4c7-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="fe4c7-118">Create a project</span></span>

<span data-ttu-id="fe4c7-119">Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje taką samą platformę docelową jak projekt.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="fe4c7-120">W tym instruktażu należy użyć prostej aplikacji WPF.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="fe4c7-121">Utwórz projekt w programie Visual Studio przy użyciu **programu File** > **New Project**, wpisując pozycję **.NET** w polu wyszukiwania, a następnie wybierając **aplikację WPF (.NET Framework).**</span><span class="sxs-lookup"><span data-stu-id="fe4c7-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="fe4c7-122">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-122">Click **Next**.</span></span> <span data-ttu-id="fe4c7-123">Zaakceptuj wartości domyślne dla **programu Framework** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="fe4c7-124">Visual Studio tworzy projekt, który otwiera się w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="fe4c7-125">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="fe4c7-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="fe4c7-126">Aby zainstalować pakiet, można użyć Menedżera pakietów NuGet lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="fe4c7-127">Po zainstalowaniu pakietu NuGet rejestruje zależność w pliku projektu `packages.config` lub pliku (w zależności od formatu projektu).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="fe4c7-128">Aby uzyskać więcej informacji, zobacz [Omówienie zużycia pakietów i przepływ pracy](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="fe4c7-129">Menedżer pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="fe4c7-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="fe4c7-130">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **pozycję Odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Zarządzanie poleceniem NuGet Packages dla odwołań do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="fe4c7-132">Wybierz "nuget.org" jako **źródło pakietu**, wybierz kartę **Przeglądaj,** wyszukaj **newtonsoft.Json**, wybierz ten pakiet na liście i wybierz pozycję **Zainstaluj:**</span><span class="sxs-lookup"><span data-stu-id="fe4c7-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Lokalizowanie pakietu Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="fe4c7-134">Jeśli chcesz uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="fe4c7-135">Zaakceptuj wszelkie monity licencyjne.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="fe4c7-136">(Tylko program Visual Studio 2017) Jeśli zostanie wyświetlony monit o wybranie formatu zarządzania pakietami, wybierz pozycję **PackageReference w pliku projektu:**</span><span class="sxs-lookup"><span data-stu-id="fe4c7-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Wybieranie formatu zarządzania pakietami](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="fe4c7-138">Jeśli zostanie wyświetlony monit o przejrzenie zmian, wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="fe4c7-139">Konsola menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="fe4c7-139">Package Manager Console</span></span>

1. <span data-ttu-id="fe4c7-140">Wybierz polecenie menu Konsola**Konsoli Menedżera pakietów** Menedżera **pakietów** >  > Narzędzia**NuGet.**</span><span class="sxs-lookup"><span data-stu-id="fe4c7-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="fe4c7-141">Po otwarciu konsoli sprawdź, czy lista rozwijana **Domyślny projekt** zawiera projekt, w którym chcesz zainstalować pakiet.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="fe4c7-142">Jeśli masz jeden projekt w rozwiązaniu, jest już zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Lokalizowanie pakietu Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="fe4c7-144">Wprowadź polecenie `Install-Package Newtonsoft.Json` (patrz [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="fe4c7-145">W oknie konsoli jest wyświetlane dane wyjściowe dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-145">The console window shows output for the command.</span></span> <span data-ttu-id="fe4c7-146">Błędy zazwyczaj wskazują, że pakiet nie jest zgodny z platformą docelową projektu.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="fe4c7-147">Aby uzyskać więcej informacji na temat Konsoli Menedżera pakietów, zobacz [Instalowanie pakietów i zarządzanie nimi przy użyciu konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="fe4c7-148">Korzystanie z interfejsu API Newtonsoft.Json w aplikacji</span><span class="sxs-lookup"><span data-stu-id="fe4c7-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="fe4c7-149">Za pomocą pakietu Newtonsoft.Json w projekcie `JsonConvert.SerializeObject` można wywołać jego metodę konwersji obiektu na ciąg czytelny dla człowieka.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="fe4c7-150">Otwórz `MainWindow.xaml` i zastąp istniejący `Grid` element następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="fe4c7-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="fe4c7-151">Otwórz `MainWindow.xaml.cs` plik (znajdujący się `MainWindow.xaml` w Eksploratorze rozwiązań `MainWindow` pod węzłem) i wstaw następujący kod wewnątrz klasy:</span><span class="sxs-lookup"><span data-stu-id="fe4c7-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="fe4c7-152">Mimo że dodano pakiet Newtonsoft.Json do projektu, czerwony squiggles pojawia się pod, `JsonConvert` ponieważ potrzebujesz `using` instrukcji w górnej części pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="fe4c7-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="fe4c7-153">Tworzenie i uruchamianie aplikacji przez naciśnięcie klawisza F5 lub wybranie **debugowania debugowania** > **startowego:**</span><span class="sxs-lookup"><span data-stu-id="fe4c7-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Wstępne dane wyjściowe aplikacji WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="fe4c7-155">Wybierz na przycisku, aby zobaczyć zawartość TextBlock zastąpione niektóre JSON tekst:</span><span class="sxs-lookup"><span data-stu-id="fe4c7-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Dane wyjściowe aplikacji WPF po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="fe4c7-157">Podobne wideo</span><span class="sxs-lookup"><span data-stu-id="fe4c7-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="fe4c7-158">Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="fe4c7-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe4c7-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe4c7-159">Next steps</span></span>

<span data-ttu-id="fe4c7-160">Gratulujemy instalacji i korzystania z pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="fe4c7-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe4c7-161">Instalowanie pakietów i zarządzanie nimi przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fe4c7-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe4c7-162">Instalowanie pakietów i zarządzanie nimi przy użyciu Konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="fe4c7-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="fe4c7-163">Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.</span><span class="sxs-lookup"><span data-stu-id="fe4c7-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="fe4c7-164">Omówienie i przepływ pracy zużycia pakietów</span><span class="sxs-lookup"><span data-stu-id="fe4c7-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="fe4c7-165">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="fe4c7-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="fe4c7-166">Odwołania do pakietu w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="fe4c7-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
