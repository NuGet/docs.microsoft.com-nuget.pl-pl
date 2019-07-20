---
title: Instalowanie i używanie pakietu NuGet w programie Visual Studio
description: Samouczek instruktażowy dotyczący procesu instalowania i używania pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 1976d1dc7129da4edb44a1346c6ce74ad3e93b1b
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342490"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="01c13-103">Szybki start: Instalowanie i używanie pakietu w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01c13-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="01c13-104">Pakiety NuGet zawierają kod wielokrotnego użytku, który inni deweloperzy udostępnili do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="01c13-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="01c13-105">Zobacz, [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="01c13-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="01c13-106">Pakiety są instalowane w projekcie programu Visual Studio za pomocą interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="01c13-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="01c13-107">W tym artykule przedstawiono proces przy użyciu popularnego pakietu [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) i projektu platforma uniwersalna systemu Windows (platformy UWP).</span><span class="sxs-lookup"><span data-stu-id="01c13-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="01c13-108">Ten sam proces ma zastosowanie do dowolnego innego projektu .NET lub .NET Core.</span><span class="sxs-lookup"><span data-stu-id="01c13-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="01c13-109">Po zainstalowaniu programu zapoznaj się z pakietem w `using <namespace>` kodzie \<,\> gdzie przestrzeń nazw jest specyficzna dla używanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="01c13-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="01c13-110">Po wprowadzeniu odwołania można wywołać pakiet za pomocą jego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="01c13-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="01c13-111">**Zacznij od NuGet.org**: Nuget.org przeglądania polega na tym, że deweloperzy platformy .NET zwykle wyszukują składniki, których mogą ponownie używać w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="01c13-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="01c13-112">Możesz przeszukiwać nuget.org bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="01c13-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01c13-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="01c13-113">Prerequisites</span></span>

- <span data-ttu-id="01c13-114">Program Visual Studio 2017 z obciążeniem programowanie platforma uniwersalna systemu Windows lub</span><span class="sxs-lookup"><span data-stu-id="01c13-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="01c13-115">Program Visual Studio 2015 Update 3 z narzędziami dla aplikacji uniwersalnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="01c13-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="01c13-116">Wersję 2017 Community można zainstalować bezpłatnie z usługi [VisualStudio.com](https://www.visualstudio.com/) lub korzystać z wersji Professional lub Enterprise.</span><span class="sxs-lookup"><span data-stu-id="01c13-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="01c13-117">Jeśli używasz Visual Studio dla komputerów Mac, zobacz [Dołącz pakiet NuGet do projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="01c13-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="01c13-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="01c13-118">Create a project</span></span>

<span data-ttu-id="01c13-119">Pakiety NuGet można zainstalować w dowolnym projekcie .NET, pod warunkiem, że pakiet obsługuje tę samą platformę docelową co projekt.</span><span class="sxs-lookup"><span data-stu-id="01c13-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="01c13-120">W tym instruktażu należy użyć prostej aplikacji uniwersalnej systemu Windows (platformy UWP).</span><span class="sxs-lookup"><span data-stu-id="01c13-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="01c13-121">Utwórz projekt w programie Visual Studio przy użyciu **pliku > nowy projekt...** i wybierz pozycję **Windows Universal > Blank (aplikacja uniwersalna systemu Windows)** .</span><span class="sxs-lookup"><span data-stu-id="01c13-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="01c13-122">Po wyświetleniu monitu zaakceptuj wartości domyślne wersji docelowej i wersji minimalnej.</span><span class="sxs-lookup"><span data-stu-id="01c13-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="01c13-123">Dodawanie pakietu NuGet Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="01c13-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="01c13-124">Aby zainstalować pakiet, można użyć interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="01c13-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="01c13-125">Podczas instalacji pakietu NuGet rejestruje zależność w pliku projektu lub `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="01c13-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="01c13-126">Aby uzyskać więcej informacji, zobacz [Omówienie użycia pakietu i przepływ pracy](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="01c13-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="01c13-127">Interfejs użytkownika menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="01c13-127">Package Manager UI</span></span>

1. <span data-ttu-id="01c13-128">W Eksplorator rozwiązań kliknij prawym przyciskiem myszy pozycję **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="01c13-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Polecenie zarządzania pakietami NuGet dla odwołań do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="01c13-130">Wybierz pozycję "nuget.org" jako **Źródło pakietu**, wybierz kartę **Przeglądaj** , wyszukaj ciąg **Newtonsoft. JSON**, wybierz ten pakiet z listy, a następnie wybierz pozycję **Zainstaluj**:</span><span class="sxs-lookup"><span data-stu-id="01c13-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="01c13-132">Zaakceptuj wszelkie zapytanie licencji.</span><span class="sxs-lookup"><span data-stu-id="01c13-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="01c13-133">(Visual Studio 2017) Jeśli zostanie wyświetlony monit o wybranie formatu zarządzania pakietami, wybierz pozycję **PackageReference w pliku projektu**:</span><span class="sxs-lookup"><span data-stu-id="01c13-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Wybieranie formatu zarządzania pakietami](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="01c13-135">Jeśli zostanie wyświetlony monit o przejrzenie zmian, wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="01c13-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="01c13-136">Konsola menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="01c13-136">Package Manager Console</span></span>

1. <span data-ttu-id="01c13-137">Wybierz **narzędzia > Menedżer pakietów NuGet > menu konsoli Menedżera pakietów** .</span><span class="sxs-lookup"><span data-stu-id="01c13-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="01c13-138">Po otwarciu konsoli Sprawdź, czy na liście rozwijanej **Projekt domyślny** znajduje się projekt, w którym ma zostać zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="01c13-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="01c13-139">Jeśli w rozwiązaniu istnieje pojedynczy projekt, jest on już zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="01c13-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Lokalizowanie pakietu Newtonsoft. JSON](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="01c13-141">Wprowadź polecenie `Install-Package Newtonsoft.Json` (zobacz [install-package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="01c13-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="01c13-142">W oknie konsoli są wyświetlane dane wyjściowe polecenia.</span><span class="sxs-lookup"><span data-stu-id="01c13-142">The console window shows output for the command.</span></span> <span data-ttu-id="01c13-143">Błędy zwykle wskazują, że pakiet nie jest zgodny z platformą docelową projektu.</span><span class="sxs-lookup"><span data-stu-id="01c13-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="01c13-144">Korzystanie z interfejsu API Newtonsoft. JSON w aplikacji</span><span class="sxs-lookup"><span data-stu-id="01c13-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="01c13-145">Za pomocą pakietu Newtonsoft. JSON w projekcie można wywołać `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.</span><span class="sxs-lookup"><span data-stu-id="01c13-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="01c13-146">Otwórz `MainPage.xaml` i Zastąp istniejący `Grid` element następującym:</span><span class="sxs-lookup"><span data-stu-id="01c13-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="01c13-147">Otwórz plik (znajdujący się w Eksplorator rozwiązań `MainPage.xaml` pod węzłem) i Wstaw następujący kod wewnątrz `MainPage` konstruktora: `MainPage.xaml.cs`</span><span class="sxs-lookup"><span data-stu-id="01c13-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="01c13-148">Mimo że dodano pakiet Newtonsoft. JSON do projektu, czerwone zygzaki pojawiają się w obszarze `JsonConvert` , ponieważ `using` potrzebujesz instrukcji w górnej części pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="01c13-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="01c13-149">Skompiluj i uruchom aplikację, naciskając klawisz F5 lub wybierając pozycję **debuguj > Rozpocznij debugowanie**:</span><span class="sxs-lookup"><span data-stu-id="01c13-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Początkowe dane wyjściowe aplikacji platformy UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="01c13-151">Wybierz przycisk na przycisku, aby zobaczyć zawartość elementu TextBlock zamienionego na jakiś tekst JSON:</span><span class="sxs-lookup"><span data-stu-id="01c13-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Dane wyjściowe aplikacji platformy UWP po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a><span data-ttu-id="01c13-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01c13-153">Next steps</span></span>

<span data-ttu-id="01c13-154">Gratulacje z myślą o instalowaniu i używaniu pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="01c13-154">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01c13-155">Instalowanie pakietów i zarządzanie nimi za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01c13-155">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

<span data-ttu-id="01c13-156">Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.</span><span class="sxs-lookup"><span data-stu-id="01c13-156">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="01c13-157">Omówienie użycia pakietu i przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="01c13-157">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="01c13-158">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="01c13-158">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="01c13-159">Odwołania do pakietu w plikach projektu</span><span class="sxs-lookup"><span data-stu-id="01c13-159">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
