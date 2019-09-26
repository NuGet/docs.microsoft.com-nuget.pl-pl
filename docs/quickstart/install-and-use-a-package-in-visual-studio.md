---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 92fc78a88733d0308dc26e10c5b0bafb86b78045
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307226"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="99383-103">Szybki start: Instalowanie i używanie pakietu w programie Visual Studio (tylko system Windows)</span><span class="sxs-lookup"><span data-stu-id="99383-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="99383-104">Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="99383-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="99383-105">Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="99383-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="99383-106">Pakiety są instalowane w projekcie programu Visual Studio za pomocą Menedżera pakietów NuGet lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="99383-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="99383-107">W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu Windows Presentation Foundation (WPF).</span><span class="sxs-lookup"><span data-stu-id="99383-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="99383-108">Ten sam proces ma zastosowanie do dowolnego innego projektu .NET lub .NET Core.</span><span class="sxs-lookup"><span data-stu-id="99383-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="99383-109">Po zainstalowaniu programu zapoznaj się z pakietem w `using <namespace>` kodzie \<,\> gdzie przestrzeń nazw jest specyficzna dla używanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="99383-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="99383-110">Po wprowadzeniu odwołania można wywołać pakiet za pomocą jego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="99383-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="99383-111">**Zacznij od NuGet.org**: *NuGet.org* przeglądania polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="99383-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="99383-112">Możesz przeszukiwać *NuGet.org* bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="99383-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="99383-113">Aby uzyskać ogólne informacje, zobacz [Znajdź i Oceń pakiety NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="99383-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99383-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="99383-114">Prerequisites</span></span>

- <span data-ttu-id="99383-115">Program Visual Studio 2019 z obciążeniem programistycznym dla programu .NET Desktop.</span><span class="sxs-lookup"><span data-stu-id="99383-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="99383-116">Wersję 2019 Community można zainstalować bezpłatnie z usługi [VisualStudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="99383-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="99383-117">Jeśli używasz Visual Studio dla komputerów Mac, zobacz [Instalowanie i używanie pakietu w programie Visual Studio dla komputerów Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="99383-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="99383-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="99383-118">Create a project</span></span>

<span data-ttu-id="99383-119">Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje tę samą platformę docelową co projekt.</span><span class="sxs-lookup"><span data-stu-id="99383-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="99383-120">W tym instruktażu należy użyć prostej aplikacji WPF.</span><span class="sxs-lookup"><span data-stu-id="99383-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="99383-121">Utwórz projekt w programie Visual Studio przy użyciu **pliku** > **Nowy projekt**, wpisz **.NET** w polu wyszukiwania, a następnie wybierz **aplikację WPF (.NET Framework)** .</span><span class="sxs-lookup"><span data-stu-id="99383-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="99383-122">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="99383-122">Click **Next**.</span></span> <span data-ttu-id="99383-123">Zaakceptuj wartości domyślne dla **struktury** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="99383-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="99383-124">Program Visual Studio tworzy projekt, który zostanie otwarty w Eksplorator rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="99383-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="99383-125">Dodawanie pakietu NuGet Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="99383-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="99383-126">Aby zainstalować pakiet, można użyć Menedżera pakietów NuGet lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="99383-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="99383-127">Podczas instalacji pakietu NuGet rejestruje zależność w pliku projektu lub `packages.config` pliku (w zależności od formatu projektu).</span><span class="sxs-lookup"><span data-stu-id="99383-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="99383-128">Aby uzyskać więcej informacji, zobacz [Omówienie użycia pakietu i przepływ pracy](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="99383-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="99383-129">Menedżer pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="99383-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="99383-130">W Eksplorator rozwiązań kliknij prawym przyciskiem myszy pozycję **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="99383-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Polecenie zarządzania pakietami NuGet dla odwołań do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="99383-132">Wybierz pozycję "nuget.org" jako **Źródło pakietu**, wybierz kartę **Przeglądaj** , wyszukaj ciąg **Newtonsoft. JSON**, wybierz ten pakiet z listy, a następnie wybierz pozycję **Zainstaluj**:</span><span class="sxs-lookup"><span data-stu-id="99383-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="99383-134">Aby uzyskać więcej informacji na temat Menedżera pakietów NuGet, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą programu Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="99383-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="99383-135">Zaakceptuj wszelkie zapytanie licencji.</span><span class="sxs-lookup"><span data-stu-id="99383-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="99383-136">(Tylko w programie Visual Studio 2017) Jeśli zostanie wyświetlony monit o wybranie formatu zarządzania pakietami, wybierz pozycję **PackageReference w pliku projektu**:</span><span class="sxs-lookup"><span data-stu-id="99383-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Wybieranie formatu zarządzania pakietami](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="99383-138">Jeśli zostanie wyświetlony monit o przejrzenie zmian, wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="99383-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="99383-139">Konsola menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="99383-139">Package Manager Console</span></span>

1. <span data-ttu-id="99383-140">Wybierz kolejno pozycje **Narzędzia** >  > **Menedżer pakietów NuGet**polecenie**konsola Menedżera pakietów** .</span><span class="sxs-lookup"><span data-stu-id="99383-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="99383-141">Po otwarciu konsoli Sprawdź, czy na liście rozwijanej **Projekt domyślny** znajduje się projekt, w którym ma zostać zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="99383-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="99383-142">Jeśli w rozwiązaniu istnieje pojedynczy projekt, jest on już zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="99383-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="99383-144">Wprowadź polecenie `Install-Package Newtonsoft.Json` (zobacz [install-package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="99383-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="99383-145">W oknie konsoli są wyświetlane dane wyjściowe polecenia.</span><span class="sxs-lookup"><span data-stu-id="99383-145">The console window shows output for the command.</span></span> <span data-ttu-id="99383-146">Błędy zwykle wskazują, że pakiet nie jest zgodny z platformą docelową projektu.</span><span class="sxs-lookup"><span data-stu-id="99383-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="99383-147">Aby uzyskać więcej informacji na temat konsoli Menedżera pakietów, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą konsoli Menedżera pakietów](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="99383-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="99383-148">Korzystanie z interfejsu API Newtonsoft. JSON w aplikacji</span><span class="sxs-lookup"><span data-stu-id="99383-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="99383-149">Za pomocą pakietu Newtonsoft. JSON w projekcie można wywołać `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.</span><span class="sxs-lookup"><span data-stu-id="99383-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="99383-150">Otwórz `MainWindow.xaml` i Zastąp istniejący `Grid` element następującym:</span><span class="sxs-lookup"><span data-stu-id="99383-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="99383-151">Otwórz plik (znajdujący się w Eksplorator rozwiązań `MainWindow.xaml` pod węzłem) i Wstaw następujący kod wewnątrz `MainWindow` klasy: `MainWindow.xaml.cs`</span><span class="sxs-lookup"><span data-stu-id="99383-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="99383-152">Mimo że dodano pakiet Newtonsoft. JSON do projektu, czerwone zygzaki pojawiają się w obszarze `JsonConvert` , ponieważ `using` potrzebujesz instrukcji w górnej części pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="99383-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="99383-153">Skompiluj i uruchom aplikację, naciskając klawisz F5 lub wybierając pozycję **Debuguj** > **Rozpocznij debugowanie**:</span><span class="sxs-lookup"><span data-stu-id="99383-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Początkowe dane wyjściowe aplikacji WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="99383-155">Wybierz przycisk na przycisku, aby zobaczyć zawartość elementu TextBlock zamienionego na jakiś tekst JSON:</span><span class="sxs-lookup"><span data-stu-id="99383-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Dane wyjściowe aplikacji WPF po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a><span data-ttu-id="99383-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99383-157">Next steps</span></span>

<span data-ttu-id="99383-158">Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="99383-158">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99383-159">Instalowanie pakietów i zarządzanie nimi za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99383-159">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="99383-160">Instalowanie pakietów i zarządzanie nimi przy użyciu konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="99383-160">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="99383-161">Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.</span><span class="sxs-lookup"><span data-stu-id="99383-161">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="99383-162">Omówienie użycia pakietu i przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="99383-162">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="99383-163">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="99383-163">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="99383-164">Odwołania do pakietu w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="99383-164">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
