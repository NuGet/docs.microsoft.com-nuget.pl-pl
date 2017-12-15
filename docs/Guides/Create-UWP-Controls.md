---
title: Formanty porady pakietu platformy uniwersalnej systemu Windows z programem NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "Tworzenie pakietów NuGet, które zawierają platformy uniwersalnej systemu Windows steruje tym niezbędne metadane i pliki pomocnicze dla programu Visual Studio i Blend projektantów."
keywords: Formanty NuGet platformy uniwersalnej systemu Windows, programu Visual Studio XAML designer, projektanta programu Blend, formanty niestandardowe
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="8ee64-104">Tworzenie formantów platformy uniwersalnej systemu Windows w postaci pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="8ee64-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="8ee64-105">Z programu Visual Studio 2017 r można korzystać z możliwości dodane dla formantów platformy uniwersalnej systemu Windows, które dostarczają w pakietach NuGet.</span><span class="sxs-lookup"><span data-stu-id="8ee64-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="8ee64-106">Ten przewodnik przeprowadzi Cię przez te funkcje przy użyciu [próbki ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="8ee64-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="8ee64-107">Wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="8ee64-107">Pre-requisites:</span></span>

1.  <span data-ttu-id="8ee64-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8ee64-108">Visual Studio 2017</span></span>
1.  <span data-ttu-id="8ee64-109">Opis sposobu [tworzenia pakietów platformy uniwersalnej systemu Windows](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8ee64-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="8ee64-110">Obsługę przybornika/zasoby okienka kontrolki XAML</span><span class="sxs-lookup"><span data-stu-id="8ee64-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="8ee64-111">Aby wymusić formantowi XAML w przyborniku projektanta XAML w Visual Studio i w okienku zasobów programu Blend, Utwórz `VisualStudioToolsManifest.xml` pliku w folderze głównym `tools` folderu projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="8ee64-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="8ee64-112">Ten plik nie jest wymagane, jeśli nie ma potrzeby wyglądać w przyborniku lub w okienku zasoby.</span><span class="sxs-lookup"><span data-stu-id="8ee64-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

<span data-ttu-id="8ee64-113">Struktura pliku jest następujący:</span><span class="sxs-lookup"><span data-stu-id="8ee64-113">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="8ee64-114">gdzie:</span><span class="sxs-lookup"><span data-stu-id="8ee64-114">where:</span></span>

- <span data-ttu-id="8ee64-115">*your_package_file*: Nazwa formantu plików, takich jak `ManagedPackage.winmd` ("ManagedPackage" jest używany w tym przykładzie dowolnego o nazwie i nie ma innych znaczenia).</span><span class="sxs-lookup"><span data-stu-id="8ee64-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="8ee64-116">*vs_category*: Etykieta grupy, w którym ma wyglądać formant przybornika projektanta programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ee64-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="8ee64-117">A `VSCategory` jest niezbędna dla formantu pojawią się w przyborniku.</span><span class="sxs-lookup"><span data-stu-id="8ee64-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="8ee64-118">*blend_category*: Etykieta grupy ma wyglądać formant, w okienku zasoby projektanta mieszania.</span><span class="sxs-lookup"><span data-stu-id="8ee64-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="8ee64-119">A `BlendCategory` jest niezbędna dla formantu pojawią się w zasobach.</span><span class="sxs-lookup"><span data-stu-id="8ee64-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="8ee64-120">*type_full_name_n*: pełni kwalifikowaną nazwą dla każdej kontrolki, w tym przestrzeń nazw, takich jak `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="8ee64-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="8ee64-121">Należy pamiętać, że format kropka jest używana przez typy zarządzane i natywne.</span><span class="sxs-lookup"><span data-stu-id="8ee64-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="8ee64-122">W bardziej zaawansowanych scenariuszy, mogą również obejmować wiele `<File>` elementów w obrębie `<FileList>` Jeśli pojedynczy pakiet zawiera wiele zestawów formantu.</span><span class="sxs-lookup"><span data-stu-id="8ee64-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="8ee64-123">Można również mieć wielu `<ToolboxItems>` węzłów w jednym `<File>` aby organizować formantów na osobne kategorie.</span><span class="sxs-lookup"><span data-stu-id="8ee64-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="8ee64-124">W poniższym przykładzie formantu realizowane w `ManagedPackage.winmd` będą wyświetlane w programie Visual Studio i Blend w grupie o nazwie "Zarządzanego pakietu" i "MyCustomControl" pojawi się w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="8ee64-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="8ee64-125">Te nazwy są dowolne.</span><span class="sxs-lookup"><span data-stu-id="8ee64-125">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Formant przykład postaci, w jakiej są wyświetlane w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Formant przykład postaci, w jakiej są wyświetlane w programie Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="8ee64-128">Należy jawnie określić każdego formantu, który chcesz wyświetlić w okienku przybornika/zasobów.</span><span class="sxs-lookup"><span data-stu-id="8ee64-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="8ee64-129">Upewnij się, określ w formacie `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="8ee64-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="8ee64-130">Dodawanie ikon niestandardowych do formantów</span><span class="sxs-lookup"><span data-stu-id="8ee64-130">Add custom icons to your controls</span></span>

<span data-ttu-id="8ee64-131">Aby wyświetlić ikon niestandardowych w okienku przybornika/zasoby, należy dodać obraz do projektu lub odpowiednie `design.dll` projektu o nazwie "Namespace.ControlName.extension" i ustawić akcji kompilacji "Osadzonego zasobu".</span><span class="sxs-lookup"><span data-stu-id="8ee64-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="8ee64-132">Obsługiwane formaty to `.png`, `.jpg`, `.jpeg`, `.gif`, i `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="8ee64-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="8ee64-133">Rozmiar obrazu zalecane jest x 64 pikseli 64.</span><span class="sxs-lookup"><span data-stu-id="8ee64-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="8ee64-134">W poniższym przykładzie projekt zawiera plik o nazwie "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="8ee64-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Ustawienie ikon niestandardowych w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="8ee64-136">Dla natywnych kontrolek, możesz umieścić ikony jako zasób w `design.dll` projektu.</span><span class="sxs-lookup"><span data-stu-id="8ee64-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="8ee64-137">Obsługuje określonych wersji platformy systemu Windows</span><span class="sxs-lookup"><span data-stu-id="8ee64-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="8ee64-138">Pakiety platformy uniwersalnej systemu Windows zawierają TargetPlatformVersion (TPV) i TargetPlatformMinVersion (TPMinV), które definiują górne i dolne granice wersji systemu operacyjnego zainstalowaną aplikację.</span><span class="sxs-lookup"><span data-stu-id="8ee64-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="8ee64-139">Dalsze TPV Określa wersję zestawu SDK, względem której aplikacja jest wbudowana.</span><span class="sxs-lookup"><span data-stu-id="8ee64-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="8ee64-140">Można w trosce o te właściwości, podczas tworzenia pakietu platformy uniwersalnej systemu Windows: poza granicami wersje platformy zdefiniowanych w aplikacji przy użyciu interfejsów API spowoduje niepowodzenie kompilacji lub aplikację, aby zakończyć się niepowodzeniem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="8ee64-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="8ee64-141">Na przykład załóżmy, że ustawiono TPMinV pakietu formantów systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393), tak aby mieć pewność, że pakiet jest używany tylko przez platformy uniwersalnej systemu Windows projekcję pasujących obniżyć powiązane z.</span><span class="sxs-lookup"><span data-stu-id="8ee64-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="8ee64-142">Aby umożliwić pakietu jest używane przez `project.json` na podstawie projektów uniwersalnych systemu Windows, należy spakować formantów z następującymi nazwami folderu:</span><span class="sxs-lookup"><span data-stu-id="8ee64-142">To allow your package to be consumed by `project.json` based UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0\*
\ref\uap10.0\*
```

<span data-ttu-id="8ee64-143">Aby wymusić odpowiednie wyboru TPMinV, Utwórz [plik elementów docelowych MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) i pakietu go w folderze kompilacji (zastępując "your_assembly_name" o nazwie z określonego zestawu):</span><span class="sxs-lookup"><span data-stu-id="8ee64-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

<span data-ttu-id="8ee64-144">Oto przykład jak powinien wyglądać plik elementów docelowych:</span><span class="sxs-lookup"><span data-stu-id="8ee64-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="8ee64-145">Dodawanie obsługi w czasie projektowania</span><span class="sxs-lookup"><span data-stu-id="8ee64-145">Add design-time support</span></span>

<span data-ttu-id="8ee64-146">Aby skonfigurować, których właściwości wyświetlane w Inspektora właściwości, Dodaj niestandardowego modułu definiowania układu kodu itp., umieść Twojej `design.dll` pliku wewnątrz `lib\<platform>\Design` folderu odpowiednio do platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="8ee64-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="8ee64-147">Ponadto aby upewnić się, że  **[Edytuj szablon > edytowania kopii](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**  działa funkcja musi zawierać `Generic.xaml` i słowników zasobów, które w scaleń `<AssemblyName>\Themes` folderu.</span><span class="sxs-lookup"><span data-stu-id="8ee64-147">Also, to ensure that the **[Edit Template > Edit a Copy](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="8ee64-148">(Ten plik nie ma wpływu na zachowanie środowiska uruchomieniowego formantu.)</span><span class="sxs-lookup"><span data-stu-id="8ee64-148">(This file has no impact on the runtime behavior of a control.)</span></span>


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> <span data-ttu-id="8ee64-149">Domyślnie właściwości formantu będą widoczne w różnych kategorii w Inspektora właściwości.</span><span class="sxs-lookup"><span data-stu-id="8ee64-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>


## <a name="use-strings-and-resources"></a><span data-ttu-id="8ee64-150">Użyj ciągów i zasobów</span><span class="sxs-lookup"><span data-stu-id="8ee64-150">Use strings and resources</span></span>

<span data-ttu-id="8ee64-151">Osadzić zasobów ciągu (`.resw`) do pakietu, które mogą być używane przez formant lub odbierającą projektu platformy uniwersalnej systemu Windows, należy ustawić **Akcja kompilacji** właściwość `.resw` pliku **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="8ee64-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="8ee64-152">Na przykład dotyczą [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładowym ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="8ee64-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="8ee64-153">Pakiet zawartości, takich jak obrazy</span><span class="sxs-lookup"><span data-stu-id="8ee64-153">Package content such as images</span></span>

<span data-ttu-id="8ee64-154">Do pakietu zawartości, takich jak obrazy, które mogą być używane przez formant lub odbierającą projektu platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8ee64-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="8ee64-155">Dodaj te pliki `lib\uap10.0.14393.0` folderu w następujący sposób ("your_assembly_name" ponownie powinien odpowiadać określonego formantu):</span><span class="sxs-lookup"><span data-stu-id="8ee64-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

<span data-ttu-id="8ee64-156">Mogą również tworzyć[plik elementów docelowych MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) zapewnienie element zawartości jest kopiowany do folderu wyjściowego odbierającą projektu:</span><span class="sxs-lookup"><span data-stu-id="8ee64-156">You may also author an[MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="8ee64-157">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8ee64-157">See also</span></span>

- [<span data-ttu-id="8ee64-158">Tworzenie pakietów platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="8ee64-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="8ee64-159">Przykładowe ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="8ee64-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
