---
title: Utwórz pakiety NuGet dla platforma uniwersalna systemu Windows
description: Kompleksowy przewodnik tworzenia pakietów NuGet przy użyciu składnika środowisko wykonawcze systemu Windows dla platforma uniwersalna systemu Windows w programie C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231806"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="e6f6f-103">Utwórz pakiety platformy UWP (C#)</span><span class="sxs-lookup"><span data-stu-id="e6f6f-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="e6f6f-104">[Platforma uniwersalna systemu Windows (platformy UWP)](/windows/uwp) zapewnia wspólną platformę aplikacji dla każdego urządzenia z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="e6f6f-105">W ramach tego modelu aplikacje platformy UWP mogą wywoływać oba interfejsy API WinRT, które są wspólne dla wszystkich urządzeń, a także interfejsy API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na których działa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="e6f6f-106">W tym instruktażu utworzysz pakiet NuGet ze składnikiem C# platformy UWP (w tym formantem XAML), który może być używany w projektach zarządzanych i natywnych.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6f6f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6f6f-107">Prerequisites</span></span>

1. <span data-ttu-id="e6f6f-108">Program Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-108">Visual Studio 2019.</span></span> <span data-ttu-id="e6f6f-109">Zainstaluj bezpłatnie wersję 2019 Community z [VisualStudio.com](https://www.visualstudio.com/); można również używać wersji Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="e6f6f-110">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-110">NuGet CLI.</span></span> <span data-ttu-id="e6f6f-111">Pobierz najnowszą wersję `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji (pobieranie jest `.exe` bezpośrednio).</span><span class="sxs-lookup"><span data-stu-id="e6f6f-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="e6f6f-112">Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="e6f6f-113">[Więcej szczegółów](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="e6f6f-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="e6f6f-114">Utwórz składnik środowisko wykonawcze systemu Windows platformy UWP</span><span class="sxs-lookup"><span data-stu-id="e6f6f-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="e6f6f-115">W programie Visual Studio wybierz kolejno pozycje **plik > nowy > projekt**, wyszukaj ciąg "platformy UWP c#", wybierz szablon **składnik środowisko wykonawcze systemu Windows (uniwersalny system Windows)** , kliknij przycisk Dalej, Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk Utwórz.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="e6f6f-116">Po wyświetleniu monitu zaakceptuj wartości domyślne wersji docelowej i wersji minimalnej.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Tworzenie nowego projektu składnika środowisko wykonawcze systemu Windows platformy UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="e6f6f-118">Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań, wybierz pozycję **dodaj > nowy element**, wybierz opcję **formant z szablonem**, Zmień nazwę na AwesomeImageControl.cs, a następnie kliknij przycisk **Dodaj**:</span><span class="sxs-lookup"><span data-stu-id="e6f6f-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Dodawanie nowego elementu formantu XAML z szablonem do projektu](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="e6f6f-120">Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **właściwości.**</span><span class="sxs-lookup"><span data-stu-id="e6f6f-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="e6f6f-121">Na stronie właściwości wybierz kartę **kompilacja** i Włącz **plik dokumentacji XML**:</span><span class="sxs-lookup"><span data-stu-id="e6f6f-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Ustawienie Generuj pliki dokumentacji XML na tak](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="e6f6f-123">Kliknij teraz *rozwiązanie* prawym przyciskiem myszy, wybierz pozycję **kompilacja wsadowa**, a następnie sprawdź pięć pól kompilacji w oknie dialogowym, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="e6f6f-124">Daje to pewność, że po wykonaniu kompilacji zostanie wygenerowany pełen zestaw artefaktów dla każdego systemu docelowego obsługiwanego przez system Windows.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Kompilacja wsadowa](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="e6f6f-126">W oknie dialogowym kompilacja wsadowa, a następnie kliknij przycisk **Kompiluj** , aby zweryfikować projekt i utworzyć pliki wyjściowe potrzebne dla pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="e6f6f-127">W tym instruktażu użyjesz artefaktów debugowania dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="e6f6f-128">W przypadku pakietu bez debugowania Sprawdź opcje wydania w oknie dialogowym kompilacja wsadowa, a następnie zapoznaj się z folderem wydania w poniższej procedurze.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="e6f6f-129">Utwórz i zaktualizuj plik. nuspec</span><span class="sxs-lookup"><span data-stu-id="e6f6f-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="e6f6f-130">Aby utworzyć początkowy plik `.nuspec`, wykonaj trzy poniższe czynności.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="e6f6f-131">Poniższe sekcje przeprowadzą Cię przez inne niezbędne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="e6f6f-132">Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.csproj` (będzie to podfolder poniżej miejsca, w którym znajduje się plik rozwiązania).</span><span class="sxs-lookup"><span data-stu-id="e6f6f-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="e6f6f-133">Uruchom [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) polecenie, aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana z nazwy pliku `.csroj`):</span><span class="sxs-lookup"><span data-stu-id="e6f6f-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="e6f6f-134">Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizuj go tak, aby pasował do następujących, zastępując YOUR_NAME z odpowiednią wartością.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="e6f6f-135">Nie pozostawiaj żadnych wartości $propertyName $.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="e6f6f-136">Wartość `<id>`, szczególnie, musi być unikatowa w obrębie nuget.org (zobacz Konwencje nazewnictwa opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="e6f6f-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="e6f6f-137">Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="e6f6f-138">W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na element `<tags>`, ponieważ te Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="e6f6f-139">Dodawanie metadanych systemu Windows do pakietu</span><span class="sxs-lookup"><span data-stu-id="e6f6f-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="e6f6f-140">Składnik środowisko wykonawcze systemu Windows wymaga metadanych, które opisują wszystkie dostępne publicznie typy, które umożliwiają korzystanie z składnika przez inne aplikacje i biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="e6f6f-141">Te metadane są zawarte w pliku winmd, który jest tworzony podczas kompilowania projektu i musi być dołączony do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="e6f6f-142">Plik XML z danymi IntelliSense jest również zbudowany w tym samym czasie i powinien być również dołączony.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="e6f6f-143">Dodaj następujący węzeł `<files>` do pliku `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e6f6f-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="e6f6f-144">Dodawanie zawartości XAML</span><span class="sxs-lookup"><span data-stu-id="e6f6f-144">Adding XAML content</span></span>

<span data-ttu-id="e6f6f-145">Aby dołączyć kontrolkę XAML do składnika, należy dodać plik XAML, który ma szablon domyślny dla formantu (zgodnie z szablonem projektu).</span><span class="sxs-lookup"><span data-stu-id="e6f6f-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="e6f6f-146">Jest to również sekcja `<files>`:</span><span class="sxs-lookup"><span data-stu-id="e6f6f-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="e6f6f-147">Dodawanie natywnych bibliotek implementacji</span><span class="sxs-lookup"><span data-stu-id="e6f6f-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="e6f6f-148">W składniku podstawowa logika typu ImageEnhancer jest w kodzie natywnym, który jest zawarty w różnych zestawach `ImageEnhancer.winmd`, które są generowane dla każdego docelowego środowiska uruchomieniowego (ARM, ARM64, x86 i x64).</span><span class="sxs-lookup"><span data-stu-id="e6f6f-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="e6f6f-149">Aby uwzględnić je w pakiecie, odwołują się do nich w sekcji `<files>` wraz ze skojarzonymi z nimi plikami zasobów. pri:</span><span class="sxs-lookup"><span data-stu-id="e6f6f-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="e6f6f-150">Final. nuspec</span><span class="sxs-lookup"><span data-stu-id="e6f6f-150">Final .nuspec</span></span>

<span data-ttu-id="e6f6f-151">Końcowy plik `.nuspec` powinien teraz wyglądać podobnie do poniższego, gdzie ponownie YOUR_NAME należy zastąpić odpowiednią wartością:</span><span class="sxs-lookup"><span data-stu-id="e6f6f-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="e6f6f-152">Pakowanie składnika</span><span class="sxs-lookup"><span data-stu-id="e6f6f-152">Package the component</span></span>

<span data-ttu-id="e6f6f-153">Wraz z `.nuspec` zakończonymi odwołującymi się do wszystkich plików, które należy uwzględnić w pakiecie, możesz uruchomić polecenie [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) :</span><span class="sxs-lookup"><span data-stu-id="e6f6f-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="e6f6f-154">Spowoduje to wygenerowanie `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="e6f6f-155">Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobaczysz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="e6f6f-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Eksplorator pakietów NuGet przedstawiający pakiet ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e6f6f-157">Plik `.nupkg` jest po prostu plikiem ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e6f6f-158">Możesz również przeanalizować zawartość pakietu, zmieniając `.nupkg` na `.zip`, pamiętając o przywróceniu rozszerzenia przed przekazaniem pakietu do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e6f6f-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e6f6f-159">Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e6f6f-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="e6f6f-160">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="e6f6f-160">Related topics</span></span>

- [<span data-ttu-id="e6f6f-161">nuspec — odwołanie</span><span class="sxs-lookup"><span data-stu-id="e6f6f-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="e6f6f-162">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="e6f6f-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="e6f6f-163">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="e6f6f-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="e6f6f-164">Obsługa wielu wersji .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e6f6f-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e6f6f-165">Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="e6f6f-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="e6f6f-166">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="e6f6f-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
