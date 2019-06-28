---
title: Przewodnik wprowadzający do korzystania z pakietów NuGet z poziomu programu Visual Studio
description: Samouczek wskazówki dotyczące procesu o instalowaniu i używaniu pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 014b316ea03b45584406c313d46b96ad36340124
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426232"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="121e2-103">Szybki start: Instalowanie i używanie pakietu w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121e2-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="121e2-104">Pakiety NuGet zawierają kodu wielokrotnego użytku, które inni deweloperzy zapewnić dostępność do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="121e2-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="121e2-105">Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="121e2-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="121e2-106">Pakiety są instalowane w projekcie programu Visual Studio za pomocą interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="121e2-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="121e2-107">W tym artykule przedstawiono proces, korzystając z popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu i projektu uniwersalnej platformy Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="121e2-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="121e2-108">Ten sam proces ma zastosowanie do innych projektów .NET lub .NET Core.</span><span class="sxs-lookup"><span data-stu-id="121e2-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="121e2-109">Po zakończeniu instalacji można znaleźć pakietu w kodzie za pomocą `using <namespace>` gdzie \<przestrzeni nazw\> jest właściwa dla pakietu jest używany.</span><span class="sxs-lookup"><span data-stu-id="121e2-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="121e2-110">Gdy odniesienia, można wywołać pakiet za pośrednictwem jego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="121e2-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="121e2-111">**Rozpoczynać nuget.org**: Przeglądanie nuget.org znajduje się, jak .NET deweloperzy zazwyczaj znajdują składników ponownego wykorzystania w swoich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="121e2-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="121e2-112">Można wyszukać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="121e2-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="121e2-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="121e2-113">Prerequisites</span></span>

- <span data-ttu-id="121e2-114">Program Visual Studio 2017 z obciążeniem programowanie uniwersalnej platformy Windows, lub</span><span class="sxs-lookup"><span data-stu-id="121e2-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="121e2-115">Visual Studio 2015 Update 3 za pomocą narzędzia Tools for Universal Windows Apps.</span><span class="sxs-lookup"><span data-stu-id="121e2-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="121e2-116">Wersja Community 2017 można zainstalować bezpłatnie z [visualstudio.com](https://www.visualstudio.com/) lub użyj Professional lub Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="121e2-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="121e2-117">Jeśli używasz programu Visual Studio dla komputerów Mac, zobacz [obejmują pakiet NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="121e2-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="121e2-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="121e2-118">Create a project</span></span>

<span data-ttu-id="121e2-119">Do każdego projektu .NET można zainstalować pakietów NuGet, pod warunkiem, że pakiet obsługuje platformę docelową tego samego jako projekt.</span><span class="sxs-lookup"><span data-stu-id="121e2-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="121e2-120">W ramach tego przewodnika należy użyć prostej aplikacji Universal Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="121e2-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="121e2-121">Tworzenie projektu w programie Visual Studio przy użyciu **Plik > Nowy projekt...**  i wybierając polecenie **Windows Universal > Pusta aplikacja (Windows Universal)** .</span><span class="sxs-lookup"><span data-stu-id="121e2-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="121e2-122">Zaakceptuj wartości domyślne dla wersji docelowej i wersję minimalną po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="121e2-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="121e2-123">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="121e2-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="121e2-124">Aby zainstalować pakiet, można użyć interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="121e2-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="121e2-125">Podczas instalowania pakietu NuGet rejestruje zależność w jednym pliku projektu lub `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="121e2-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="121e2-126">Aby uzyskać więcej informacji, zobacz [pakietu zużycie omówienie i przepływ pracy](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="121e2-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="121e2-127">Interfejs użytkownika menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="121e2-127">Package Manager UI</span></span>

1. <span data-ttu-id="121e2-128">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="121e2-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Zarządzanie pakietami NuGet polecenia dla odwołania do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="121e2-130">Wybierz pozycję "nuget.org" jako **źródła pakietu**, wybierz opcję **Przeglądaj** kartę, wyszukaj **Newtonsoft.Json**, a następnie wybierz pakiet z listy i wybierz  **Zainstaluj**:</span><span class="sxs-lookup"><span data-stu-id="121e2-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="121e2-132">Zaakceptuj wszystkie monity licencji.</span><span class="sxs-lookup"><span data-stu-id="121e2-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="121e2-133">(Visual Studio 2017) Jeśli zostanie wyświetlony monit, aby wybrać format pakiet zarządzania, wybierz opcję **packagereference v souboru projektu**:</span><span class="sxs-lookup"><span data-stu-id="121e2-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Wybieranie formatu zarządzania pakietów](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="121e2-135">W przypadku wyświetlenia monitu o przegląd zmian dokonanych wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="121e2-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="121e2-136">Konsola menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="121e2-136">Package Manager Console</span></span>

1. <span data-ttu-id="121e2-137">Wybierz **Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="121e2-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="121e2-138">Po otwarciu konsoli, sprawdź, czy **projekt domyślny** listy rozwijanej pokazuje projektu, do którego chcesz zainstalować pakiet.</span><span class="sxs-lookup"><span data-stu-id="121e2-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="121e2-139">Jeśli masz jednego projektu w rozwiązaniu, jest już wybrany.</span><span class="sxs-lookup"><span data-stu-id="121e2-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="121e2-141">Wprowadź polecenie `Install-Package Newtonsoft.Json` (zobacz [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="121e2-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="121e2-142">W oknie konsoli wyświetlane dane wyjściowe polecenia.</span><span class="sxs-lookup"><span data-stu-id="121e2-142">The console window shows output for the command.</span></span> <span data-ttu-id="121e2-143">Błędy zazwyczaj wskazują, że pakiet nie jest zgodny z platforma docelowa projektu.</span><span class="sxs-lookup"><span data-stu-id="121e2-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="121e2-144">Użyj pakietu Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="121e2-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="121e2-145">Przy użyciu pakietu Newtonsoft.Json w projekcie, można wywołać jej `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg czytelny dla człowieka.</span><span class="sxs-lookup"><span data-stu-id="121e2-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="121e2-146">Otwórz `MainPage.xaml` , zastępując istniejącą `Grid` element następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="121e2-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="121e2-147">Otwórz `MainPage.xaml.cs` pliku (znajdujący się w oknie Eksploratora rozwiązań pod `MainPage.xaml` węzła) i Wstaw następujący kod wewnątrz `MainPage` Konstruktor:</span><span class="sxs-lookup"><span data-stu-id="121e2-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="121e2-148">Mimo że pakietu Newtonsoft.Json jest dodawany do projektu, czerwone faliste linie pojawia się w obszarze `JsonConvert` ponieważ będzie potrzebny `using` instrukcji na górze pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="121e2-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="121e2-149">Skompilować i uruchomić aplikację, naciskając klawisz F5 lub wybierając **Debuguj > Rozpocznij debugowanie**:</span><span class="sxs-lookup"><span data-stu-id="121e2-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Początkowe dane wyjściowe aplikacji platformy uniwersalnej systemu Windows](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="121e2-151">Wybierz przycisk, aby wyświetlić zawartość TextBlock zastąpiony tekst JSON:</span><span class="sxs-lookup"><span data-stu-id="121e2-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Dane wyjściowe aplikacji platformy uniwersalnej systemu Windows po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="121e2-153">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="121e2-153">Related articles</span></span>

- [<span data-ttu-id="121e2-154">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="121e2-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="121e2-155">Instalowanie i zarządzanie pakietami za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="121e2-155">Install and manage packages using Visual Studio</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="121e2-156">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="121e2-156">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="121e2-157">Typowe konfiguracje NuGet</span><span class="sxs-lookup"><span data-stu-id="121e2-157">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
