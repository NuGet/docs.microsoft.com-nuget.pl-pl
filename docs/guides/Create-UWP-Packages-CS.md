---
title: Tworzenie pakietów NuGet dla uniwersalnej platformy systemu Windows
description: End-to-end instruktaż tworzenia pakietów NuGet przy użyciu składnika środowiska wykonawczego systemu Windows dla platformy uniwersalnego systemu Windows w języku C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231806"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="012f5-103">Tworzenie pakietów platformy uniwersalnej systemuśpiłni (C#)</span><span class="sxs-lookup"><span data-stu-id="012f5-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="012f5-104">[Platforma uniwersalna systemu Windows (UWP)](/windows/uwp) zapewnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="012f5-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="012f5-105">W ramach tego modelu aplikacje platformy uniwersalnej systemu Windows mogą wywoływać zarówno interfejsy API platformy WinRT, które są wspólne dla wszystkich urządzeń, jak i interfejsy API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na których jest uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="012f5-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="012f5-106">W tym instruktażu można utworzyć pakiet NuGet ze składnikiem platformy uniwersalnej systemu IP języka C # (w tym kontrolki XAML), który może być używany zarówno w projektach zarządzanych i natywnych.</span><span class="sxs-lookup"><span data-stu-id="012f5-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="012f5-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="012f5-107">Prerequisites</span></span>

1. <span data-ttu-id="012f5-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="012f5-108">Visual Studio 2019.</span></span> <span data-ttu-id="012f5-109">Zainstaluj edycję społeczności 2019 bezpłatnie od [visualstudio.com;](https://www.visualstudio.com/) można również korzystać z wersji Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="012f5-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="012f5-110">Funkcja Interfejsu wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="012f5-110">NuGet CLI.</span></span> <span data-ttu-id="012f5-111">Pobierz najnowszą `nuget.exe` wersję z [nuget.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji `.exe` (pobieranie jest bezpośrednio).</span><span class="sxs-lookup"><span data-stu-id="012f5-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="012f5-112">Następnie dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli jeszcze jej nie ma.</span><span class="sxs-lookup"><span data-stu-id="012f5-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="012f5-113">[Więcej szczegółów](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="012f5-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="012f5-114">Tworzenie składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="012f5-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="012f5-115">W programie Visual Studio wybierz polecenie **Plik > Nowy projekt >**, wyszukaj hasło "uwp c#", wybierz szablon **Składnika Wykonawczego systemu Windows (Universal Windows),** kliknij przycisk dalej, zmień nazwę na ImageEnhancer i kliknij przycisk Utwórz.</span><span class="sxs-lookup"><span data-stu-id="012f5-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="012f5-116">Po wyświetleniu monitu zaakceptuj wartości domyślne dla wersji docelowej i wersji minimalnej.</span><span class="sxs-lookup"><span data-stu-id="012f5-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Tworzenie nowego projektu składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="012f5-118">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, wybierz pozycję **Dodaj > nowy element**, wybierz pozycję **Formant szablonu,** zmień nazwę na AwesomeImageControl.cs, a następnie kliknij przycisk **Dodaj:**</span><span class="sxs-lookup"><span data-stu-id="012f5-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Dodawanie nowego elementu formantu szablonu XAML do projektu](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="012f5-120">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **polecenie Właściwości.**</span><span class="sxs-lookup"><span data-stu-id="012f5-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="012f5-121">Na stronie Właściwości wybierz kartę **Kompilacja** i włącz **plik dokumentacji XML:**</span><span class="sxs-lookup"><span data-stu-id="012f5-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Ustawienie Generowanie plików dokumentacji XML na Tak](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="012f5-123">Kliknij prawym przyciskiem myszy *rozwiązanie* teraz, wybierz **polecenie Kompilacja wsadowa**, zaznacz pięć pól kompilacji w oknie dialogowym, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="012f5-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="012f5-124">Dzięki temu podczas wykonywania kompilacji, można wygenerować pełny zestaw artefaktów dla każdego z systemów docelowych, które obsługuje system Windows.</span><span class="sxs-lookup"><span data-stu-id="012f5-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Kompilacja wsadowego](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="012f5-126">W oknie dialogowym Kompilacja wsadowa i kliknij przycisk **Buduj,** aby zweryfikować projekt i utworzyć pliki wyjściowe potrzebne dla pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="012f5-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="012f5-127">W tym instruktażu należy użyć artefaktów debugowania dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="012f5-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="012f5-128">W przypadku pakietu nie debugowania sprawdź opcje wydania w oknie dialogowym kompilacji wsadowej i zapoznaj się z wynikowymi folderami release w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="012f5-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="012f5-129">Tworzenie i aktualizowanie pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="012f5-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="012f5-130">Aby utworzyć `.nuspec` plik początkowy, wykonaj trzy kroki poniżej.</span><span class="sxs-lookup"><span data-stu-id="012f5-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="012f5-131">Sekcje, które następują, następnie poprowadzi Cię przez inne niezbędne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="012f5-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="012f5-132">Otwórz wiersz polecenia i przejdź do `ImageEnhancer.csproj` folderu zawierającego (będzie to podfolder poniżej, gdzie znajduje się plik rozwiązania).</span><span class="sxs-lookup"><span data-stu-id="012f5-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="012f5-133">Uruchom [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) polecenie do `ImageEnhancer.nuspec` wygenerowania (nazwa pliku pochodzi od `.csroj` nazwy pliku):</span><span class="sxs-lookup"><span data-stu-id="012f5-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="012f5-134">Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizuj go, aby dopasować go do następujących, zastępując YOUR_NAME odpowiednią wartością.</span><span class="sxs-lookup"><span data-stu-id="012f5-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="012f5-135">Nie należy pozostawiać żadnych wartości $propertyName$.</span><span class="sxs-lookup"><span data-stu-id="012f5-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="012f5-136">Wartość, `<id>` w szczególności, musi być unikatowa w nuget.org (zobacz konwencje nazewnictwa opisane w [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="012f5-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="012f5-137">Należy również pamiętać, że należy również zaktualizować tagi autora i opisu lub pojawi się błąd podczas kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="012f5-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="012f5-138">W przypadku pakietów przeznaczonych do `<tags>` użytku publicznego należy zwrócić szczególną uwagę na element, ponieważ te tagi pomagają innym znaleźć pakiet i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="012f5-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="012f5-139">Dodawanie metadanych systemu Windows do pakietu</span><span class="sxs-lookup"><span data-stu-id="012f5-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="012f5-140">Składnik środowiska wykonawczego systemu Windows wymaga metadanych, które opisują wszystkie jego publicznie dostępne typy, co umożliwia innym aplikacjom i bibliotekom korzystanie ze składnika.</span><span class="sxs-lookup"><span data-stu-id="012f5-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="012f5-141">Te metadane są zawarte w pliku .winmd, który jest tworzony podczas kompilowania projektu i musi być uwzględniony w pakiecie NuGet.</span><span class="sxs-lookup"><span data-stu-id="012f5-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="012f5-142">Plik XML z danymi IntelliSense jest również zbudowany w tym samym czasie i powinien być również dołączony.</span><span class="sxs-lookup"><span data-stu-id="012f5-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="012f5-143">Dodaj do `<files>` `.nuspec` pliku następujący węzeł:</span><span class="sxs-lookup"><span data-stu-id="012f5-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="012f5-144">Dodawanie zawartości XAML</span><span class="sxs-lookup"><span data-stu-id="012f5-144">Adding XAML content</span></span>

<span data-ttu-id="012f5-145">Aby dołączyć formant XAML do składnika, należy dodać plik XAML, który ma domyślny szablon formantu (wygenerowany przez szablon projektu).</span><span class="sxs-lookup"><span data-stu-id="012f5-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="012f5-146">Dotyczy to również `<files>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="012f5-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="012f5-147">Dodawanie natywnych bibliotek implementacji</span><span class="sxs-lookup"><span data-stu-id="012f5-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="012f5-148">W ramach składnika podstawowa logika typu ImageEnhancer jest w kodzie `ImageEnhancer.winmd` macierzystym, który jest zawarty w różnych zestawach, które są generowane dla każdego docelowego środowiska uruchomieniowego (ARM, ARM64, x86 i x64).</span><span class="sxs-lookup"><span data-stu-id="012f5-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="012f5-149">Aby uwzględnić je w pakiecie, `<files>` odwołaj się do nich w sekcji wraz z skojarzonymi z nimi plikami zasobów .pri:</span><span class="sxs-lookup"><span data-stu-id="012f5-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="012f5-150">Końcowy .nuspec</span><span class="sxs-lookup"><span data-stu-id="012f5-150">Final .nuspec</span></span>

<span data-ttu-id="012f5-151">Plik `.nuspec` końcowy powinien teraz wyglądać następująco, gdzie ponownie YOUR_NAME należy zastąpić odpowiednią wartością:</span><span class="sxs-lookup"><span data-stu-id="012f5-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="012f5-152">Zapakuj składnik</span><span class="sxs-lookup"><span data-stu-id="012f5-152">Package the component</span></span>

<span data-ttu-id="012f5-153">Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) w pakiecie, możesz uruchomić polecenie:</span><span class="sxs-lookup"><span data-stu-id="012f5-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="012f5-154">To generuje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="012f5-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="012f5-155">Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozwijając wszystkie węzły, zostanie wyświetleni następująca zawartość:</span><span class="sxs-lookup"><span data-stu-id="012f5-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer przedstawiający pakiet ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="012f5-157">Plik `.nupkg` to tylko plik ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="012f5-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="012f5-158">Możesz również sprawdzić zawartość pakietu, `.nupkg` a `.zip`następnie, zmieniając na , ale pamiętaj, aby przywrócić rozszerzenie przed przesłaniem pakietu do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="012f5-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="012f5-159">Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="012f5-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="012f5-160">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="012f5-160">Related topics</span></span>

- [<span data-ttu-id="012f5-161">.nuspec Odwołanie</span><span class="sxs-lookup"><span data-stu-id="012f5-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="012f5-162">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="012f5-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="012f5-163">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="012f5-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="012f5-164">Obsługa wielu wersji programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="012f5-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="012f5-165">Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie</span><span class="sxs-lookup"><span data-stu-id="012f5-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="012f5-166">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="012f5-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
