---
title: "Przewodnik wprowadzający do korzystania z pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "Samouczek wskazówki dotyczące procesu instalacji i przy użyciu pakietu NuGet w projekcie."
keywords: "instalowania NuGet użycia pakietu NuGet, instalowanie pakietów NuGet, odwołania do pakietu NuGet, za pomocą pakietów NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="f0842-104">Zainstaluj i użyj pakietu</span><span class="sxs-lookup"><span data-stu-id="f0842-104">Install and use a package</span></span>

<span data-ttu-id="f0842-105">Pakiety NuGet to jednostki do ponownego użycia kodu, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="f0842-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="f0842-106">Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="f0842-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="f0842-107">Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz.</span><span class="sxs-lookup"><span data-stu-id="f0842-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="f0842-108">Po odniesienia, można wywołać pakietu za pośrednictwem jej interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f0842-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="f0842-109">W pozostałej części tego tematu, który przeprowadzi Cię przez proces instalowania popularnego przy użyciu interfejsu użytkownika Menedżera pakietów [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakiet w projekcie systemu Windows platformy Uniwersalnej.</span><span class="sxs-lookup"><span data-stu-id="f0842-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="f0842-110">Następnie pokaże przykładem przy użyciu pakietu.</span><span class="sxs-lookup"><span data-stu-id="f0842-110">It then shows an example of using the package.</span></span> <span data-ttu-id="f0842-111">Używasz podobne tego samego przepływu pracy dla niemal każdego pakietu NuGet, które stosowanie w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f0842-111">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="f0842-112">Zainstaluj wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f0842-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="f0842-113">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="f0842-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="f0842-114">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="f0842-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="f0842-115">Użyj Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0842-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="f0842-116">**Rozpoczynać nuget.org**: Instalowanie pakietów z nuget.org to typowe przepływ pracy deweloperów platformy .NET Użyj, aby znaleźć można ponownie użyć składników we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="f0842-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="f0842-117">Może zawsze wyszukiwania nuget.org bezpośrednio lub znajdować i instalować pakiety w programie Visual Studio, jak pokazano w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="f0842-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="f0842-118">Zainstaluj wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f0842-118">Install pre-requisites</span></span>

<span data-ttu-id="f0842-119">Ten samouczek wymaga programu Visual Studio 2015 Update 3 z narzędzia dla uniwersalnych aplikacji systemu Windows lub programu Visual Studio 2017 z obciążeniem rozwoju platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f0842-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="f0842-120">Jeśli masz już zainstalowanego programu Visual Studio, można uruchomić Instalatora ponownie, aby dodać narzędzia platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f0842-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="f0842-121">Można zainstalować Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/) lub użyj Professional lub Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="f0842-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="f0842-122">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="f0842-122">Create a project</span></span>

<span data-ttu-id="f0842-123">Aby zainstalować pakiet NuGet, należy niektóre rodzaju. Na podstawie NET projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0842-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="f0842-124">W ramach tego przewodnika, można użyć prostej aplikacji Windows Presentation Foundation (WPF) lub platformy uniwersalnej systemu Windows (UWP):</span><span class="sxs-lookup"><span data-stu-id="f0842-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="f0842-125">WPF (Windows 7 +), wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C#**, wybierz pozycję **klasycznego pulpitu systemu Windows > WPF aplikacji (.NET Framework)**i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0842-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="f0842-126">Dla platformy uniwersalnej systemu Windows (Windows 10), użyj **uniwersalnych systemu Windows > Pusta aplikacja (uniwersalna systemu Windows)** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f0842-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="f0842-127">Zaakceptuj wartości domyślne dla wersji docelowej i minimalna wersja po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="f0842-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="f0842-128">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="f0842-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="f0842-129">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f0842-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Zarządzanie pakietami NuGet polecenia dla odwołania do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="f0842-131">Wybierz polecenie "nuget.org" jako **źródła pakietu**, wybierz pozycję **Przeglądaj** karcie, wyszukaj **Newtonsoft.Json**, wybierz z listy tego pakietu i wybierz  **Zainstaluj**:</span><span class="sxs-lookup"><span data-stu-id="f0842-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="f0842-133">Jeśli zostanie wyświetlony monit, aby wybrać format pakietu zarządzania, wybierz między PackageReference (zalecane) i `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="f0842-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Wybieranie formatu odwołanie do pakietu](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="f0842-135">Jeśli zostanie wyświetlony monit o przegląd zmian dokonanych, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0842-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="f0842-136">Kliknij prawym przyciskiem myszy rozwiązanie w Eksploratorze rozwiązań i wybierz **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="f0842-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="f0842-137">Spowoduje to przywrócenie żadnych pakietów NuGet wymienionych w obszarze **odwołania**.</span><span class="sxs-lookup"><span data-stu-id="f0842-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="f0842-138">Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="f0842-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="f0842-139">Użyj Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0842-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="f0842-140">Przy użyciu pakietu Newtonsoft.Json w projekcie, można wywołać jej `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg zrozumiałą dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0842-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="f0842-141">Otwórz `MainWindow.xaml` (WPF) lub `MainPage.xaml` (UWP) i Zastąp istniejące `Grid` element z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f0842-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="f0842-142">Rozwiń węzeł `MainWindow.xaml` (WPF) lub `MainPage.xaml` węzła (UWP) w Eksploratorze rozwiązań Otwórz `.cs` pliku i Wstaw następujący kod w `MainWindow` lub `MainPage` klasy po konstruktora:</span><span class="sxs-lookup"><span data-stu-id="f0842-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="f0842-143">Nawet jeśli pakiet Newtonsoft.Json dodane do projektu, red zygzaki jest wyświetlany w obszarze `JsonConvert` ponieważ potrzebne `using` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="f0842-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="f0842-144">Umieść kursor nad podkreślony `JsonConvert` i zobaczysz żarówka wraz z opcją **Pokaż potencjalne rozwiązania**:</span><span class="sxs-lookup"><span data-stu-id="f0842-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Żarówka z możliwości Pokaż poprawki polecenia](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="f0842-146">Polecenie **Pokaż potencjalne rozwiązania** (lub żarówka) i wybierz pierwszy sugerowanej poprawki, `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="f0842-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="f0842-147">Spowoduje to dodanie wiersza niezbędne do początku pliku.</span><span class="sxs-lookup"><span data-stu-id="f0842-147">This adds the necessary line to the top of the file.</span></span>

    ![Żarówka nadanie opcję, aby dodać using — instrukcja](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="f0842-149">Skompilować i uruchomić aplikację, naciskając klawisz F5 lub wybranie **Debuguj > Rozpocznij debugowanie** (UWP pokazane; WPF przypomina):</span><span class="sxs-lookup"><span data-stu-id="f0842-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Początkowe dane wyjściowe aplikacji platformy uniwersalnej systemu Windows](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="f0842-151">Wybierz przycisk, aby wyświetlić zawartość obiektu TextBlock zastąpione tekst JSON:</span><span class="sxs-lookup"><span data-stu-id="f0842-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Dane wyjściowe aplikacji platformy uniwersalnej systemu Windows po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="f0842-153">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="f0842-153">Related topics</span></span>

- [<span data-ttu-id="f0842-154">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="f0842-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="f0842-155">Wyszukiwanie i Wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="f0842-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="f0842-156">Konfigurowanie zachowania programu NuGet</span><span class="sxs-lookup"><span data-stu-id="f0842-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
