---
title: Jak kontrolek interfejsu użytkownika pakietu nuget
description: Jak utworzyć pakiety NuGet, które zawierają platformy uniwersalnej systemu Windows lub programu WPF steruje tym potrzebnych metadanych i plików pomocniczych dla projektantów programu Visual Studio i Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: dfbd6a3e6d59dfcea6394891703ea66bce5e8e92
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580277"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="38684-103">Tworzenie kontrolek interfejsu użytkownika jako pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="38684-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="38684-104">Za pomocą programu Visual Studio 2017 możesz korzystać z zalet dodano funkcje dla platformy uniwersalnej systemu Windows i kontrolek WPF, które dostarczają w pakietach NuGet.</span><span class="sxs-lookup"><span data-stu-id="38684-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="38684-105">Ten przewodnik przeprowadzi Cię przez te możliwości w kontekście kontrolek platformy UWP przy użyciu [przykładowe ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="38684-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="38684-106">To samo dotyczy kontrolek WPF, chyba, że wymienione w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="38684-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38684-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38684-107">Prerequisites</span></span>

1. <span data-ttu-id="38684-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="38684-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="38684-109">Opis sposobu [tworzenie pakietów platformy UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="38684-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="38684-110">Generuj układ biblioteki</span><span class="sxs-lookup"><span data-stu-id="38684-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="38684-111">Dotyczy tylko kontrolek platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="38684-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="38684-112">Ustawienie `GenerateLibraryLayout` właściwość gwarantuje, że dane wyjściowe kompilacji projektu jest generowany w układzie, który jest gotowy do umieszczenia w pakiecie bez konieczności dla poszczególnych plików zapisów nuspec.</span><span class="sxs-lookup"><span data-stu-id="38684-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="38684-113">Z właściwości projektu przejdź na kartę kompilacji, a następnie zaznacz pole wyboru "Generuj układ biblioteki".</span><span class="sxs-lookup"><span data-stu-id="38684-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="38684-114">Spowoduje to zmodyfikowania pliku projektu i ustawić `GenerateLibraryLayout` flagi na wartość true dla aktualnie wybrana konfiguracja kompilacji i platformy.</span><span class="sxs-lookup"><span data-stu-id="38684-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="38684-115">Możesz również edytować plik projektu, aby dodać `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do pierwszej grupy właściwości bezwarunkowy.</span><span class="sxs-lookup"><span data-stu-id="38684-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="38684-116">Ma to zastosowanie właściwości niezależnie od tego, czy konfigurację kompilacji i platformy.</span><span class="sxs-lookup"><span data-stu-id="38684-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="38684-117">Obsługę przybornika/zasoby okienka kontrolki XAML</span><span class="sxs-lookup"><span data-stu-id="38684-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="38684-118">Aby kontrolki XAML są wyświetlane w przyborniku projektanta XAML w programie Visual Studio i w okienku zasobów programu Blend, należy utworzyć `VisualStudioToolsManifest.xml` pliku w folderze głównym `tools` folderu projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="38684-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="38684-119">Ten plik nie jest wymagane, jeśli nie potrzebujesz, aby formant mógł być wyświetlany w przyborniku lub w okienku zasobów.</span><span class="sxs-lookup"><span data-stu-id="38684-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="38684-120">Struktura pliku jest następująca:</span><span class="sxs-lookup"><span data-stu-id="38684-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="38684-121">gdzie:</span><span class="sxs-lookup"><span data-stu-id="38684-121">where:</span></span>

- <span data-ttu-id="38684-122">*your_package_file*: pliku nazwę kontrolki, takie jak `ManagedPackage.winmd` ("ManagedPackage" jest używany na potrzeby tego przykładu i nie ma innych znaczenia dowolną o nazwie).</span><span class="sxs-lookup"><span data-stu-id="38684-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="38684-123">*vs_category*: Etykieta dla grupy, w którym formant powinna zostać wyświetlona w przyborniku projektanta programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38684-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="38684-124">Element `VSCategory` jest konieczny, aby formant mógł być wyświetlany w przyborniku.</span><span class="sxs-lookup"><span data-stu-id="38684-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="38684-125">*blend_category*: Etykieta dla grupy, w którym formant powinna zostać wyświetlona w okienku zasobów projektanta programu Blend.</span><span class="sxs-lookup"><span data-stu-id="38684-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="38684-126">Element `BlendCategory` jest konieczny, aby formant mógł być wyświetlany w zasoby.</span><span class="sxs-lookup"><span data-stu-id="38684-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="38684-127">*type_full_name_n*: w pełni kwalifikowaną nazwę dla każdej kontrolki, w tym przestrzeń nazw, takich jak `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="38684-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="38684-128">Należy pamiętać, że format kropka jest używane dla typów zarządzane i natywne.</span><span class="sxs-lookup"><span data-stu-id="38684-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="38684-129">W bardziej zaawansowanych scenariuszy może również obejmować wiele `<File>` elementów w obrębie `<FileList>` Jeśli pojedynczy pakiet zawiera wiele zestawów formantu.</span><span class="sxs-lookup"><span data-stu-id="38684-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="38684-130">Mogą też istnieć wiele `<ToolboxItems>` węzłów w ramach pojedynczej `<File>` aby organizować formantów na osobne kategorie.</span><span class="sxs-lookup"><span data-stu-id="38684-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="38684-131">W poniższym przykładzie kontrolki implementowany w `ManagedPackage.winmd` pojawi się w programie Visual Studio i Blend w grupie o nazwie "Pakiet Managed" i "MyCustomControl" pojawi się w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="38684-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="38684-132">Te nazwy są dowolne.</span><span class="sxs-lookup"><span data-stu-id="38684-132">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Kontrolka w postaci przykład postaci, w jakiej są wyświetlane w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Kontrolka w postaci przykład postaci, w jakiej są wyświetlane w programie Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="38684-135">Należy jawnie określić każdy formant, który chcesz zobaczyć w okienku przybornika/zasobów.</span><span class="sxs-lookup"><span data-stu-id="38684-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="38684-136">Upewnij się, podaj w formacie `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="38684-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="38684-137">Dodawanie niestandardowych ikon do formantów</span><span class="sxs-lookup"><span data-stu-id="38684-137">Add custom icons to your controls</span></span>

<span data-ttu-id="38684-138">Aby wyświetlić ikonę niestandardową, w okienku przybornika/zasoby, należy dodać obraz do projektu lub odpowiednich `design.dll` projektu o nazwie "Namespace.ControlName.extension" i Ustaw akcję kompilacji "Osadzonego zasobu".</span><span class="sxs-lookup"><span data-stu-id="38684-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="38684-139">Należy również zagwarantować, że skojarzone `AssemblyInfo.cs` Określa atrybut ProvideMetadata - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span><span class="sxs-lookup"><span data-stu-id="38684-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="38684-140">Zobacz ten [przykładowe](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="38684-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="38684-141">Obsługiwane formaty to `.png`, `.jpg`, `.jpeg`, `.gif`, i `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="38684-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="38684-142">Zalecanym formatem jest BMP24 16 x 16 pikseli.</span><span class="sxs-lookup"><span data-stu-id="38684-142">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Przykład ikona okno narzędzia](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="38684-144">Różowa tła jest zastąpione w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="38684-144">The pink background is replaced at runtime.</span></span> <span data-ttu-id="38684-145">Ikony są ponownie pokolorowane, po zmianie motywu programu Visual Studio i oczekuje się, że kolor tła.</span><span class="sxs-lookup"><span data-stu-id="38684-145">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="38684-146">Aby uzyskać więcej informacji, zobacz [obrazy i ikony dla programu Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="38684-146">For more information, please reference [Images and Icons for Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="38684-147">W poniższym przykładzie projekt zawiera plik o nazwie "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="38684-147">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Ustawienie ikony niestandardowej w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="38684-149">W przypadku natywnych kontrolek należy umieścić ikony jako zasób w `design.dll` projektu.</span><span class="sxs-lookup"><span data-stu-id="38684-149">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="38684-150">Obsługa określonych wersji platformy Windows</span><span class="sxs-lookup"><span data-stu-id="38684-150">Support specific Windows platform versions</span></span>

<span data-ttu-id="38684-151">Pakiety platformy uniwersalnej systemu Windows mają TargetPlatformVersion (TPV) i TargetPlatformMinVersion (TPMinV), które definiują górne i dolne granice wersji systemu operacyjnego zainstalowaną aplikację.</span><span class="sxs-lookup"><span data-stu-id="38684-151">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="38684-152">Dodatkowo TPV Określa wersję zestawu SDK, względem którego skompilowano aplikację.</span><span class="sxs-lookup"><span data-stu-id="38684-152">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="38684-153">Można je na uwadze tych właściwości, podczas tworzenia pakietu platformy uniwersalnej systemu Windows: za pomocą interfejsów API poza granicami wersje platformy, zdefiniowane w aplikacji spowoduje, że kompilacja nie powiedzie się lub aplikację, aby zakończyć się niepowodzeniem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="38684-153">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="38684-154">Na przykład załóżmy, że ustawiono TPMinV dla pakietu formanty do systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393), tak aby mieć pewność, że pakiet jest używane tylko przez platformy uniwersalnej systemu Windows projektów pasujący i obniżyć powiązane z.</span><span class="sxs-lookup"><span data-stu-id="38684-154">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="38684-155">Aby umożliwić pakietu do użycia w projektach platformy uniwersalnej systemu Windows, należy spakować formantów z następującymi nazwami folderu:</span><span class="sxs-lookup"><span data-stu-id="38684-155">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="38684-156">NuGet sprawdzi automatycznie TPMinV konsumencki projektu i zakończona niepowodzeniem instalacji, jeśli jest on niższy niż Windows 10 Anniversary Edition (10.0; Kompilacja 14393)</span><span class="sxs-lookup"><span data-stu-id="38684-156">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="38684-157">W przypadku WPF Załóżmy się, że chcesz, aby pakiet kontrolek WPF być wykorzystane przez projekty przeznaczone dla .NET Framework v4.6.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="38684-157">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="38684-158">Aby wymusić, który, należy spakować formantów z następującymi nazwami folderu:</span><span class="sxs-lookup"><span data-stu-id="38684-158">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="38684-159">Dodawanie obsługi w czasie projektowania</span><span class="sxs-lookup"><span data-stu-id="38684-159">Add design-time support</span></span>

<span data-ttu-id="38684-160">Aby skonfigurować, gdzie właściwości kontrolki wyświetlane w panelu Inspektor właściwości, Dodaj niestandardowe moduły definiowania układu itp., umieść usługi `design.dll` pliku wewnątrz `lib\uap10.0.14393\Design` folderów właściwe dla platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="38684-160">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="38684-161">Ponadto aby upewnić się, że **[Edytuj szablon > Edytuj kopię](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** działania funkcji musi zawierać `Generic.xaml` i słowników zasobów, które łączy się on w `<your_assembly_name>\Themes` folder (ponownie przy użyciu Twoja nazwa zestawu rzeczywistego).</span><span class="sxs-lookup"><span data-stu-id="38684-161">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="38684-162">(Ten plik nie ma wpływu na zachowanie środowiska uruchomieniowego kontrolki.) Struktura folderów związku z tym będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="38684-162">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="38684-163">Dla WPF kontynuując w przykładzie gdzie chcesz użytkownika WPF kontrolki pakiet, który ma zostać użyte przez projekty przeznaczone dla .NET Framework v4.6.1 lub nowszej:</span><span class="sxs-lookup"><span data-stu-id="38684-163">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="38684-164">Domyślnie właściwości kontrolki będą wyświetlane w różnych kategorii w panelu Inspektor właściwości.</span><span class="sxs-lookup"><span data-stu-id="38684-164">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="38684-165">Użyj ciągów i zasobów</span><span class="sxs-lookup"><span data-stu-id="38684-165">Use strings and resources</span></span>

<span data-ttu-id="38684-166">Możesz osadzić zasoby w postaci ciągów (`.resw`) do pakietu, które mogą być używane przez formant lub konsumencki projektu platformy uniwersalnej systemu Windows, należy ustawić **Build Action** właściwość `.resw` plik **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="38684-166">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="38684-167">Na przykład dotyczyć [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładzie ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="38684-167">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="38684-168">Dotyczy tylko kontrolek platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="38684-168">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="38684-169">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="38684-169">See also</span></span>

- [<span data-ttu-id="38684-170">Tworzenie pakietów platformy UWP</span><span class="sxs-lookup"><span data-stu-id="38684-170">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="38684-171">Przykładowe ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="38684-171">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
