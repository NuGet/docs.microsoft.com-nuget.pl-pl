---
title: Utwórz pakiety NuGet dla platforma uniwersalna systemu Windows
description: Kompleksowy przewodnik tworzenia pakietów NuGet przy użyciu składnika środowisko wykonawcze systemu Windows dla platforma uniwersalna systemu Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380764"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="6bc60-103">Tworzenie pakietów platformy UWP</span><span class="sxs-lookup"><span data-stu-id="6bc60-103">Create UWP packages</span></span>

<span data-ttu-id="6bc60-104">[Platforma uniwersalna systemu Windows (platformy UWP)](https://developer.microsoft.com/windows) zapewnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="6bc60-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="6bc60-105">W ramach tego modelu aplikacje platformy UWP mogą wywoływać oba interfejsy API WinRT, które są wspólne dla wszystkich urządzeń, a także interfejsy API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na których działa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="6bc60-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="6bc60-106">W tym instruktażu utworzysz pakiet NuGet z natywnym składnikiem platformy UWP (łącznie z kontrolką XAML), który może być używany w projektach zarządzanych i natywnych.</span><span class="sxs-lookup"><span data-stu-id="6bc60-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bc60-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6bc60-107">Prerequisites</span></span>

1. <span data-ttu-id="6bc60-108">Visual Studio 2017 lub Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6bc60-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="6bc60-109">Zainstaluj bezpłatnie wersję 2017 Community z [VisualStudio.com](https://www.visualstudio.com/); można również używać wersji Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6bc60-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="6bc60-110">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="6bc60-110">NuGet CLI.</span></span> <span data-ttu-id="6bc60-111">Pobierz najnowszą wersję `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji (pobieranie jest `.exe` bezpośrednio).</span><span class="sxs-lookup"><span data-stu-id="6bc60-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="6bc60-112">Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze.</span><span class="sxs-lookup"><span data-stu-id="6bc60-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="6bc60-113">Utwórz składnik środowisko wykonawcze systemu Windows platformy UWP</span><span class="sxs-lookup"><span data-stu-id="6bc60-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="6bc60-114">W programie Visual Studio wybierz kolejno opcje **plik > nowy > projekt**, rozwiń węzeł **Visual C++ > Windows > uniwersalny** , wybierz szablon **składnik środowisko wykonawcze systemu Windows (uniwersalny system Windows)** , Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="6bc60-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="6bc60-115">Po wyświetleniu monitu zaakceptuj wartości domyślne wersji docelowej i wersji minimalnej.</span><span class="sxs-lookup"><span data-stu-id="6bc60-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Tworzenie nowego projektu składnika środowisko wykonawcze systemu Windows platformy UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="6bc60-117">Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz pozycję **dodaj > nowy element**, kliknij węzeł **Visual C++ > XAML** , wybierz opcję **formant z szablonem**, Zmień nazwę na AwesomeImageControl. cpp, a następnie kliknij przycisk **Dodaj**:</span><span class="sxs-lookup"><span data-stu-id="6bc60-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Dodawanie nowego elementu formantu XAML z szablonem do projektu](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="6bc60-119">Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **właściwości.**</span><span class="sxs-lookup"><span data-stu-id="6bc60-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="6bc60-120">Na stronie właściwości rozwiń węzeł **Właściwości konfiguracji > CC++ /** i kliknij pozycję **pliki wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="6bc60-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="6bc60-121">W okienku po prawej stronie Zmień wartość opcji **Generuj pliki dokumentacji XML** na tak:</span><span class="sxs-lookup"><span data-stu-id="6bc60-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Ustawienie Generuj pliki dokumentacji XML na tak](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="6bc60-123">Kliknij teraz *rozwiązanie* prawym przyciskiem myszy, wybierz pozycję **kompilacja wsadowa**, a następnie sprawdź trzy pola debugowania w oknie dialogowym, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="6bc60-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="6bc60-124">Daje to pewność, że po wykonaniu kompilacji zostanie wygenerowany pełen zestaw artefaktów dla każdego systemu docelowego obsługiwanego przez system Windows.</span><span class="sxs-lookup"><span data-stu-id="6bc60-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Kompilacja wsadowa](media/UWP-BatchBuild.png)

1. <span data-ttu-id="6bc60-126">W oknie dialogowym kompilacja wsadowa, a następnie kliknij przycisk **Kompiluj** , aby zweryfikować projekt i utworzyć pliki wyjściowe potrzebne dla pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="6bc60-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="6bc60-127">W tym instruktażu użyjesz artefaktów debugowania dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="6bc60-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="6bc60-128">W przypadku pakietu bez debugowania Sprawdź opcje wydania w oknie dialogowym kompilacja wsadowa, a następnie zapoznaj się z folderem wydania w poniższej procedurze.</span><span class="sxs-lookup"><span data-stu-id="6bc60-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="6bc60-129">Utwórz i zaktualizuj plik. nuspec</span><span class="sxs-lookup"><span data-stu-id="6bc60-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="6bc60-130">Aby utworzyć początkowy plik `.nuspec`, wykonaj trzy poniższe czynności.</span><span class="sxs-lookup"><span data-stu-id="6bc60-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="6bc60-131">Poniższe sekcje przeprowadzą Cię przez inne niezbędne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="6bc60-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="6bc60-132">Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.vcxproj` (będzie to podfolder poniżej miejsca, w którym znajduje się plik rozwiązania).</span><span class="sxs-lookup"><span data-stu-id="6bc60-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="6bc60-133">Uruchom polecenie NuGet `spec`, aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana z nazwy pliku `.vcxproj`):</span><span class="sxs-lookup"><span data-stu-id="6bc60-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="6bc60-134">Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizuj go tak, aby pasował do poniższego, zastępując YOUR_NAME z odpowiednią wartością.</span><span class="sxs-lookup"><span data-stu-id="6bc60-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="6bc60-135">Wartość `<id>` musi być unikatowa w obrębie nuget.org (zobacz Konwencje nazewnictwa opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="6bc60-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="6bc60-136">Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="6bc60-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="6bc60-137">W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na element `<tags>`, ponieważ te Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.</span><span class="sxs-lookup"><span data-stu-id="6bc60-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="6bc60-138">Dodawanie metadanych systemu Windows do pakietu</span><span class="sxs-lookup"><span data-stu-id="6bc60-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="6bc60-139">Składnik środowisko wykonawcze systemu Windows wymaga metadanych, które opisują wszystkie dostępne publicznie typy, które umożliwiają korzystanie z składnika przez inne aplikacje i biblioteki.</span><span class="sxs-lookup"><span data-stu-id="6bc60-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="6bc60-140">Te metadane są zawarte w pliku winmd, który jest tworzony podczas kompilowania projektu i musi być dołączony do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="6bc60-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="6bc60-141">Plik XML z danymi IntelliSense jest również zbudowany w tym samym czasie i powinien być również dołączony.</span><span class="sxs-lookup"><span data-stu-id="6bc60-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="6bc60-142">Dodaj następujący węzeł `<files>` do pliku `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6bc60-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="6bc60-143">Dodawanie zawartości XAML</span><span class="sxs-lookup"><span data-stu-id="6bc60-143">Adding XAML content</span></span>

<span data-ttu-id="6bc60-144">Aby dołączyć kontrolkę XAML do składnika, należy dodać plik XAML, który ma szablon domyślny dla formantu (zgodnie z szablonem projektu).</span><span class="sxs-lookup"><span data-stu-id="6bc60-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="6bc60-145">Ta wartość znajduje się również w sekcji `<files>`:</span><span class="sxs-lookup"><span data-stu-id="6bc60-145">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="6bc60-146">Dodawanie natywnych bibliotek implementacji</span><span class="sxs-lookup"><span data-stu-id="6bc60-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="6bc60-147">W składniku podstawowa logika typu ImageEnhancer jest w kodzie natywnym, który jest zawarty w różnych zestawach `ImageEnhancer.dll` generowanych dla każdego docelowego środowiska uruchomieniowego (ARM, x86 i x64).</span><span class="sxs-lookup"><span data-stu-id="6bc60-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="6bc60-148">Aby uwzględnić je w pakiecie, odwołują się do nich w sekcji `<files>` wraz ze skojarzonymi z nimi plikami zasobów. pri:</span><span class="sxs-lookup"><span data-stu-id="6bc60-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="adding-targets"></a><span data-ttu-id="6bc60-149">Dodawanie elementów docelowych</span><span class="sxs-lookup"><span data-stu-id="6bc60-149">Adding .targets</span></span>

<span data-ttu-id="6bc60-150">Następnie projekty C++ języka JavaScript, które mogą zużywać pakiet NuGet, potrzebują pliku. targets do identyfikowania niezbędnych zestawów i plików WinMD.</span><span class="sxs-lookup"><span data-stu-id="6bc60-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="6bc60-151">(C# projekty Visual Basic są automatycznie.) Utwórz ten plik, kopiując poniższy tekst do `ImageEnhancer.targets` i Zapisz go w tym samym folderze, co plik `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6bc60-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="6bc60-152">_Uwaga_: ten plik `.targets` musi mieć taką samą nazwę jak identyfikator pakietu (np. element `<Id>` w pliku `.nupspec`):</span><span class="sxs-lookup"><span data-stu-id="6bc60-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

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

<span data-ttu-id="6bc60-153">Następnie zapoznaj się z `ImageEnhancer.targets` w pliku `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6bc60-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="6bc60-154">Final. nuspec</span><span class="sxs-lookup"><span data-stu-id="6bc60-154">Final .nuspec</span></span>

<span data-ttu-id="6bc60-155">Końcowy plik `.nuspec` powinien teraz wyglądać podobnie do poniższego, gdzie YOUR_NAME należy zastąpić odpowiednią wartością:</span><span class="sxs-lookup"><span data-stu-id="6bc60-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="6bc60-156">Pakowanie składnika</span><span class="sxs-lookup"><span data-stu-id="6bc60-156">Package the component</span></span>

<span data-ttu-id="6bc60-157">Po zakończeniu `.nuspec` odwołujące się do wszystkich plików, które należy uwzględnić w pakiecie, możesz uruchomić polecenie `pack`:</span><span class="sxs-lookup"><span data-stu-id="6bc60-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="6bc60-158">Spowoduje to wygenerowanie `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="6bc60-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="6bc60-159">Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobaczysz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="6bc60-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Eksplorator pakietów NuGet przedstawiający pakiet ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="6bc60-161">Plik `.nupkg` jest tylko plikiem ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="6bc60-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="6bc60-162">Możesz również przeanalizować zawartość pakietu, zmieniając `.nupkg` na `.zip`, ale pamiętaj o przywróceniu rozszerzenia przed przekazaniem pakietu do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6bc60-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="6bc60-163">Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="6bc60-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="6bc60-164">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="6bc60-164">Related topics</span></span>

- [<span data-ttu-id="6bc60-165">nuspec — odwołanie</span><span class="sxs-lookup"><span data-stu-id="6bc60-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="6bc60-166">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="6bc60-166">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="6bc60-167">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="6bc60-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="6bc60-168">Obsługa wielu wersji .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6bc60-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="6bc60-169">Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="6bc60-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="6bc60-170">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="6bc60-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
