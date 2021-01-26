---
title: Jak spakować formanty interfejsu użytkownika za pomocą narzędzia NuGet
description: Jak utworzyć pakiety NuGet, które zawierają kontrolki platformy UWP lub WPF, w tym niezbędne metadane i pliki pomocnicze dla projektantów programów Visual Studio i Blend.
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 317937b4d9d773d74384b8ebfcd2146062236ac1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774326"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="4d120-103">Tworzenie kontrolek interfejsu użytkownika jako pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="4d120-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="4d120-104">Począwszy od programu Visual Studio 2017, możesz skorzystać z dodatkowych możliwości dla formantów platformy UWP i WPF dostarczanych w pakietach NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d120-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="4d120-105">Ten przewodnik przeprowadzi Cię przez te możliwości w kontekście formantów platformy UWP za pomocą [przykładu ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="4d120-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="4d120-106">To samo dotyczy formantów WPF, chyba że określono inaczej.</span><span class="sxs-lookup"><span data-stu-id="4d120-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d120-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4d120-107">Prerequisites</span></span>

1. <span data-ttu-id="4d120-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4d120-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="4d120-109">Informacje na temat [tworzenia pakietów platformy UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4d120-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="4d120-110">Generuj układ biblioteki</span><span class="sxs-lookup"><span data-stu-id="4d120-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="4d120-111">Ma to zastosowanie tylko do kontrolek platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="4d120-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="4d120-112">Ustawienie `GenerateLibraryLayout` Właściwości zapewnia, że dane wyjściowe kompilacji projektu są generowane w układzie gotowym do spakowania bez potrzeby pojedynczych wpisów plików w nuspec.</span><span class="sxs-lookup"><span data-stu-id="4d120-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="4d120-113">Na stronie właściwości projektu przejdź do karty kompilacja i zaznacz pole wyboru "Generuj układ biblioteki".</span><span class="sxs-lookup"><span data-stu-id="4d120-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="4d120-114">Spowoduje to zmodyfikowanie pliku projektu i ustawienie `GenerateLibraryLayout` flagi na true dla aktualnie wybranej konfiguracji kompilacji i platformy.</span><span class="sxs-lookup"><span data-stu-id="4d120-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="4d120-115">Alternatywnie Edytuj plik projektu, aby dodać `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do pierwszej niewarunkowej grupy właściwości.</span><span class="sxs-lookup"><span data-stu-id="4d120-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="4d120-116">Spowoduje to zastosowanie właściwości niezależnie od konfiguracji kompilacji i platformy.</span><span class="sxs-lookup"><span data-stu-id="4d120-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="4d120-117">Obsługa okienka Dodawanie zestawu narzędzi/zasobów dla kontrolek XAML</span><span class="sxs-lookup"><span data-stu-id="4d120-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="4d120-118">Aby formant XAML pojawił się w przyborniku projektanta XAML w programie Visual Studio i w okienku zasoby programu Blend, Utwórz `VisualStudioToolsManifest.xml` plik w `tools` folderze głównym folderu projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="4d120-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="4d120-119">Ten plik nie jest wymagany, Jeśli kontrolka nie jest potrzebna w okienku Przybornik lub składniki.</span><span class="sxs-lookup"><span data-stu-id="4d120-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

<span data-ttu-id="4d120-120">Struktura pliku jest następująca:</span><span class="sxs-lookup"><span data-stu-id="4d120-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="4d120-121">gdzie:</span><span class="sxs-lookup"><span data-stu-id="4d120-121">where:</span></span>

- <span data-ttu-id="4d120-122">*your_package_file*: nazwa pliku kontrolnego, na przykład `ManagedPackage.winmd` ("ManagedPackage", to arbitralna Nazwa użyta dla tego przykładu i nie ma innego znaczenia).</span><span class="sxs-lookup"><span data-stu-id="4d120-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="4d120-123">*vs_category*: etykieta grupy, w której formant powinien pojawić się w przyborniku projektanta programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d120-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="4d120-124">`VSCategory`Jest to konieczne, aby formant pojawił się w przyborniku.</span><span class="sxs-lookup"><span data-stu-id="4d120-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="4d120-125">*ui_framework*: Nazwa struktury, taka jak "WPF", należy pamiętać, że ten `UIFramework` atrybut jest wymagany w węzłach ToolboxItems w programie Visual Studio 16,7 Preview 3 lub nowszym, aby formant pojawił się w przyborniku.</span><span class="sxs-lookup"><span data-stu-id="4d120-125">*ui_framework*: The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="4d120-126">*blend_category*: etykieta grupy, w której formant powinien pojawić się w okienku zasobów projektanta mieszania.</span><span class="sxs-lookup"><span data-stu-id="4d120-126">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="4d120-127">`BlendCategory`Jest to konieczne, aby formant pojawił się w elementach zawartości.</span><span class="sxs-lookup"><span data-stu-id="4d120-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="4d120-128">*type_full_name_n*: w pełni kwalifikowana nazwa dla każdej kontrolki, łącznie z przestrzenią nazw, taką jak `ManagedPackage.MyCustomControl` .</span><span class="sxs-lookup"><span data-stu-id="4d120-128">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="4d120-129">Należy zauważyć, że format kropki jest używany zarówno dla typów zarządzanych, jak i natywnych.</span><span class="sxs-lookup"><span data-stu-id="4d120-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="4d120-130">W bardziej zaawansowanych scenariuszach można także uwzględnić wiele `<File>` elementów w obrębie, `<FileList>` gdy jeden pakiet zawiera wiele zestawów kontrolek.</span><span class="sxs-lookup"><span data-stu-id="4d120-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="4d120-131">Możesz również mieć wiele `<ToolboxItems>` węzłów w obrębie jednej, `<File>` Jeśli chcesz zorganizować kontrolki w osobnych kategoriach.</span><span class="sxs-lookup"><span data-stu-id="4d120-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="4d120-132">W poniższym przykładzie kontrolka zaimplementowana w programie `ManagedPackage.winmd` zostanie wyświetlona w programie Visual Studio i Blend w grupie o nazwie "pakiet zarządzany" i "MyCustomControl" pojawi się w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="4d120-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="4d120-133">Wszystkie te nazwy są dowolne.</span><span class="sxs-lookup"><span data-stu-id="4d120-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Przykładowa kontrolka wyświetlana w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Przykładowa kontrolka wyświetlana w programie Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="4d120-136">Należy jawnie określić każdą kontrolkę, która ma być widoczna w okienku Przybornik/składniki.</span><span class="sxs-lookup"><span data-stu-id="4d120-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="4d120-137">Upewnij się, że określisz je w formacie `Namespace.ControlName` .</span><span class="sxs-lookup"><span data-stu-id="4d120-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="4d120-138">Dodawanie niestandardowych ikon do kontrolek</span><span class="sxs-lookup"><span data-stu-id="4d120-138">Add custom icons to your controls</span></span>

<span data-ttu-id="4d120-139">Aby wyświetlić niestandardową ikonę w okienku Przybornik/składniki, Dodaj obraz do projektu lub odpowiedni `design.dll` projekt o nazwie "Namespace. ControlName. Extension" i ustaw akcję Build na "osadzony zasób".</span><span class="sxs-lookup"><span data-stu-id="4d120-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="4d120-140">Należy również upewnić się, że skojarzona wartość `AssemblyInfo.cs` określa atrybut ProvideMetadata- `[assembly: ProvideMetadata(typeof(RegisterMetadata))]` .</span><span class="sxs-lookup"><span data-stu-id="4d120-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="4d120-141">Zapoznaj się z tym [przykładem](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="4d120-141">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="4d120-142">Obsługiwane formaty to `.png` ,,, `.jpg` `.jpeg` `.gif` i `.bmp` .</span><span class="sxs-lookup"><span data-stu-id="4d120-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="4d120-143">Zalecany format to BMP24 16 pikseli przez 16 pikseli.</span><span class="sxs-lookup"><span data-stu-id="4d120-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Ikona pola narzędzia — przykład](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="4d120-145">Różowe tło jest zastępowane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4d120-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="4d120-146">Po zmianie motywu programu Visual Studio ikony są zmieniane, a jego kolor tła jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="4d120-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="4d120-147">Aby uzyskać więcej informacji, zapoznaj się z [obrazami i ikonami dla programu Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="4d120-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="4d120-148">W poniższym przykładzie projekt zawiera plik obrazu o nazwie "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="4d120-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Ustawianie niestandardowej ikony w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="4d120-150">W przypadku kontrolek natywnych należy umieścić ikonę jako zasób w `design.dll` projekcie.</span><span class="sxs-lookup"><span data-stu-id="4d120-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="4d120-151">Obsługa określonych wersji platformy systemu Windows</span><span class="sxs-lookup"><span data-stu-id="4d120-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="4d120-152">Pakiety platformy UWP mają TargetPlatformVersion (TPV) i element targetplatformminversion (TPMinV) definiujące górne i dolne granice wersji systemu operacyjnego, w których można zainstalować aplikację.</span><span class="sxs-lookup"><span data-stu-id="4d120-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="4d120-153">TPV dalsze określa wersję zestawu SDK, dla którego aplikacja została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="4d120-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="4d120-154">Pamiętaj o tych właściwościach podczas tworzenia pakietu platformy UWP: Używanie interfejsów API poza granicami wersji platformy zdefiniowanych w aplikacji spowoduje, że kompilacja zakończy się niepowodzeniem lub aplikacja zakończy się niepowodzeniem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4d120-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="4d120-155">Załóżmy na przykład, że ustawiono TPMinV dla pakietu formantów w systemie Windows 10 w wersji rocznicowej (10,0; Kompilacja 14393), aby upewnić się, że pakiet jest używany tylko przez projekty platformy UWP zgodne z tym dolną granicą.</span><span class="sxs-lookup"><span data-stu-id="4d120-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="4d120-156">Aby zezwolić na korzystanie z pakietu przez projekty platformy UWP, należy spakować kontrolki następującymi nazwami folderów:</span><span class="sxs-lookup"><span data-stu-id="4d120-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

<span data-ttu-id="4d120-157">Pakiet NuGet automatycznie sprawdzi TPMinV pakietu, a instalacja nie powiedzie się, jeśli jest starsza niż Windows 10 rocznic Edition (10,0; Kompilacja 14393)</span><span class="sxs-lookup"><span data-stu-id="4d120-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="4d120-158">W przypadku WPF Załóżmy, że chcesz, aby pakiet formantów WPF był używany przez projekty ukierunkowane na .NET Framework v w wersji 4.6.1 lub wyższej.</span><span class="sxs-lookup"><span data-stu-id="4d120-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="4d120-159">Aby wymusić to, należy spakować kontrolki o następujących nazwach folderów:</span><span class="sxs-lookup"><span data-stu-id="4d120-159">To enforce that, you must package your controls with the following folder names:</span></span>

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a><span data-ttu-id="4d120-160">Dodawanie obsługi czasu projektowania</span><span class="sxs-lookup"><span data-stu-id="4d120-160">Add design-time support</span></span>

<span data-ttu-id="4d120-161">Aby skonfigurować, gdzie są wyświetlane właściwości kontrolki w Inspektorze właściwości, Dodaj niestandardowe moduły definiowania układu itp., umieść `design.dll` plik wewnątrz `lib\uap10.0.14393\Design` folderu odpowiednio do platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="4d120-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="4d120-162">Ponadto, aby upewnić się, że **[Edytuj szablon > edytowanie funkcji kopiowania](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** , należy uwzględnić `Generic.xaml` i wszystkie słowniki zasobów, które Scala w `<your_assembly_name>\Themes` folderze (ponownie przy użyciu rzeczywistej nazwy zestawu).</span><span class="sxs-lookup"><span data-stu-id="4d120-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="4d120-163">(Ten plik nie ma wpływu na zachowanie w czasie wykonywania kontrolki). Struktura folderów będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4d120-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

<span data-ttu-id="4d120-164">W przypadku platformy WPF kontynuując przykład, w którym chcesz, aby pakiet formantów WPF był używany przez projekty przeznaczone dla .NET Framework v 4.6.1 lub wyższych:</span><span class="sxs-lookup"><span data-stu-id="4d120-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> <span data-ttu-id="4d120-165">Domyślnie właściwości kontrolki będą wyświetlane w kategorii Różne w Inspektorze właściwości.</span><span class="sxs-lookup"><span data-stu-id="4d120-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="4d120-166">Korzystanie z ciągów i zasobów</span><span class="sxs-lookup"><span data-stu-id="4d120-166">Use strings and resources</span></span>

<span data-ttu-id="4d120-167">W pakiecie można osadzić zasoby ciągów ( `.resw` ), które mogą być używane przez formant lub projekt zużywający platformy UWP, ustawić właściwość **Akcja kompilacji** `.resw` pliku na **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="4d120-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="4d120-168">Aby zapoznać się z przykładem, zobacz [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładzie ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="4d120-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="4d120-169">Ma to zastosowanie tylko do kontrolek platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="4d120-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="4d120-170">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4d120-170">See also</span></span>

- [<span data-ttu-id="4d120-171">Tworzenie pakietów platformy UWP</span><span class="sxs-lookup"><span data-stu-id="4d120-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="4d120-172">Przykład ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="4d120-172">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)