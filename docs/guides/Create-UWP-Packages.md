---
title: Tworzenie pakietów NuGet dla platformy Universal Windows
description: End-to-end Przewodnik tworzenia pakietów NuGet dla platformy uniwersalnej Windows za pomocą składnika środowiska wykonawczego Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 52f2057f7d1012b75bba9e8730eacffd99adacfa
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426859"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="58082-103">Tworzenie pakietów platformy UWP</span><span class="sxs-lookup"><span data-stu-id="58082-103">Create UWP packages</span></span>

<span data-ttu-id="58082-104">[Windows platformy Uniwersalnej](https://developer.microsoft.com/windows) udostępnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="58082-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="58082-105">W tym modelu aplikacji platformy UWP może wywoływać zarówno interfejsów API WinRT, które są wspólne dla wszystkich urządzeń, a także interfejsów API (w tym Win32 i platformy .NET), które są specyficzne dla rodziny urządzeń, na którym działa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="58082-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="58082-106">W tym przewodniku tworzenia pakietów NuGet za pomocą natywnego platformy uniwersalnej systemu Windows składnik (w tym kontrolki XAML) używanej w zarządzanych i natywnych projektów.</span><span class="sxs-lookup"><span data-stu-id="58082-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58082-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="58082-107">Prerequisites</span></span>

1. <span data-ttu-id="58082-108">Program Visual Studio 2017 lub Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="58082-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="58082-109">Zainstaluj 2017 Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/); można użyć również wersje Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="58082-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="58082-110">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="58082-110">NuGet CLI.</span></span> <span data-ttu-id="58082-111">Pobierz najnowszą wersję `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), zapisanie go do wybranej lokalizacji (pliki do pobrania jest `.exe` bezpośrednio).</span><span class="sxs-lookup"><span data-stu-id="58082-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="58082-112">Następnie dodaj tej lokalizacji do zmiennej środowiskowej PATH, jeśli jeszcze tego nie zrobiono.</span><span class="sxs-lookup"><span data-stu-id="58082-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="58082-113">Tworzenie składników środowiska wykonawczego Windows platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="58082-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="58082-114">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C++ > Windows > Universal** węzła, wybierz opcję **składnika środowiska wykonawczego Windows (Windows Universal)** szablonu, Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="58082-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="58082-115">Zaakceptuj wartości domyślne dla wersji docelowej i wersję minimalną po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="58082-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Tworzenie nowego projektu składnika wykonawczego Windows platformy uniwersalnej systemu Windows](media/UWP-NewProject.png)

1. <span data-ttu-id="58082-117">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, wybierz pozycję **Dodaj > Nowy element**, kliknij przycisk **Visual C++ > XAML** węzeł **formant z szablonem**, Zmień nazwę na AwesomeImageControl.cpp, a następnie kliknij przycisk **Dodaj**:</span><span class="sxs-lookup"><span data-stu-id="58082-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Dodawanie nowego elementu kontrolka z szablonem XAML do projektu](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="58082-119">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **właściwości.**</span><span class="sxs-lookup"><span data-stu-id="58082-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="58082-120">Na stronie właściwości rozwiń węzeł **właściwości konfiguracji > C/C++** i kliknij przycisk **pliki wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="58082-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="58082-121">W okienku po prawej stronie Zmień wartość **Generuj pliki dokumentacji XML** tak:</span><span class="sxs-lookup"><span data-stu-id="58082-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Ustawienia Generuj pliki dokumentacji XML tak](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="58082-123">Kliknij prawym przyciskiem myszy *rozwiązania* Wybierz teraz **tworzenie partii**, trzy pola debugowania w oknie dialogowym Sprawdź, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="58082-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="58082-124">Dzięki temu po wykonaniu kompilacji wygenerować pełny zestaw artefaktów dla każdego z docelowych systemach, które obsługuje Windows.</span><span class="sxs-lookup"><span data-stu-id="58082-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Kompilacji wsadowej](media/UWP-BatchBuild.png)

1. <span data-ttu-id="58082-126">W zadaniu wsadowym Tworzenie okna dialogowego, a następnie kliknij przycisk **kompilacji** w celu sprawdzenia projektu i utworzyć pliki wyjściowe, które są potrzebne dla pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="58082-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="58082-127">W tym przewodniku użyjesz artefaktów debugowania dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="58082-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="58082-128">Pakietu bez debugowania zamiast tego wybierz opcje wersji w oknie dialogowym Tworzenie usługi Batch i odwołać się do wynikowego folderów wydania w opisanych poniżej.</span><span class="sxs-lookup"><span data-stu-id="58082-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="58082-129">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="58082-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="58082-130">Aby utworzyć początkowy `.nuspec` plików, wykonaj następujące trzy kroki.</span><span class="sxs-lookup"><span data-stu-id="58082-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="58082-131">Sekcje, które należy wykonać, a następnie prowadzi przez innych wymaganych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="58082-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="58082-132">Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.vcxproj` (będzie podfolder poniżej, gdzie jest to plik rozwiązania).</span><span class="sxs-lookup"><span data-stu-id="58082-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="58082-133">Uruchom rozszerzenie NuGet `spec` polecenie, aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana z nazwy `.vcxproj` plików):</span><span class="sxs-lookup"><span data-stu-id="58082-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="58082-134">Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizuj go zgodnie z poniższym, zamieniając twoja_nazwa odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="58082-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="58082-135">`<id>` Wartość, w szczególności musi być unikatowa w witrynie nuget.org (konwencje nazewnictwa, opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="58082-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="58082-136">Należy również zauważyć, że należy również zaktualizować autor i opis znaczników lub wystąpi błąd podczas wykonywania kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="58082-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="58082-137">W przypadku pakietów utworzone do użytku publicznego należy zwrócić szczególną uwagę na `<tags>` elementu, jak te znaczniki pomóc innym odnaleźć pakietu i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="58082-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="58082-138">Dodanie metadanych Windows do pakietu</span><span class="sxs-lookup"><span data-stu-id="58082-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="58082-139">Składnik środowiska wykonawczego Windows wymaga metadane opisujące wszystkich typów publicznie dostępny, co umożliwia dla innych aplikacji i bibliotek korzystanie z komponentu.</span><span class="sxs-lookup"><span data-stu-id="58082-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="58082-140">Te metadane są zawarte w pliku winmd, która jest tworzona podczas kompilowania projektu i muszą być zawarte w pakiecie NuGet.</span><span class="sxs-lookup"><span data-stu-id="58082-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="58082-141">Plik XML z danymi IntelliSense jest również zbudowana w tym samym czasie i mają zostać uwzględnione również.</span><span class="sxs-lookup"><span data-stu-id="58082-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="58082-142">Dodaj następujący kod `<files>` węzeł `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="58082-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="58082-143">Dodawanie zawartości XAML</span><span class="sxs-lookup"><span data-stu-id="58082-143">Adding XAML content</span></span>

<span data-ttu-id="58082-144">Aby dołączyć kontrolki XAML przy użyciu składnika, należy dodać plik XAML, którego szablonu domyślnego dla formantu (wygenerowane przez szablon projektu).</span><span class="sxs-lookup"><span data-stu-id="58082-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="58082-145">Prowadzi to również `<files>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="58082-145">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="58082-146">Dodawanie bibliotek natywnych implementacji</span><span class="sxs-lookup"><span data-stu-id="58082-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="58082-147">W ramach składnika, podstawowe zasady logiczne typu ImageEnhancer jest w kodzie natywnym, która jest zawarta w różnych `ImageEnhancer.dll` zestawów, które są generowane dla każdego docelowe środowisko uruchomieniowe (x 86 i x64 ARM).</span><span class="sxs-lookup"><span data-stu-id="58082-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="58082-148">Aby uwzględnić je w pakiecie, odwoływać się do nich w `<files>` sekcji wraz z plikami zasobów .pri skojarzone:</span><span class="sxs-lookup"><span data-stu-id="58082-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="58082-149">Dodawanie .targets</span><span class="sxs-lookup"><span data-stu-id="58082-149">Adding .targets</span></span>

<span data-ttu-id="58082-150">Następnie projektów C++ i JavaScript, które może używać pakietu NuGet muszą pliku .targets w celu identyfikowania niezbędne pliki zestawu i winmd.</span><span class="sxs-lookup"><span data-stu-id="58082-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="58082-151">(Projektów C# i Visual Basic to zrobić automatycznie.) Utwórz ten plik, kopiując poniższy tekst do `ImageEnhancer.targets` i zapisz go w tym samym folderze co `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="58082-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="58082-152">_Uwaga_: To `.targets` pliku musi mieć taką samą nazwę jak identyfikator pakietu (np. `<Id>` element `.nupspec` plików):</span><span class="sxs-lookup"><span data-stu-id="58082-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="58082-153">Następnie zapoznaj się `ImageEnhancer.targets` w swojej `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="58082-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="58082-154">Końcowe .nuspec</span><span class="sxs-lookup"><span data-stu-id="58082-154">Final .nuspec</span></span>

<span data-ttu-id="58082-155">Ostateczna `.nuspec` plik powinien teraz wyglądać podobnie do poniższego, gdzie ponownie twoja_nazwa należy zamienić na odpowiednie wartości:</span><span class="sxs-lookup"><span data-stu-id="58082-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="58082-156">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="58082-156">Package the component</span></span>

<span data-ttu-id="58082-157">Za pomocą ukończoną `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="58082-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="58082-158">Spowoduje to wygenerowanie `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="58082-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="58082-159">Otwarcie tego pliku w narzędzia, takiego jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobacz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="58082-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Wyświetlanie pakietu ImageEnhancer Eksplorator pakietów NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="58082-161">A `.nupkg` plik jest po prostu plikiem ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="58082-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="58082-162">Można także sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale należy pamiętać przywrócić rozszerzenia przed przekazaniem pakietu na stronie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="58082-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="58082-163">Aby udostępnić pakietu innym deweloperom, postępuj zgodnie z instrukcjami [publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="58082-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="58082-164">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="58082-164">Related topics</span></span>

- [<span data-ttu-id="58082-165">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="58082-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="58082-166">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="58082-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="58082-167">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="58082-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="58082-168">Obsługiwanie wielu wersji programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="58082-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="58082-169">Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="58082-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="58082-170">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="58082-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
