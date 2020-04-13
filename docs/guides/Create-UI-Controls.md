---
title: Jak spakować kontrolki interfejsu użytkownika za pomocą nuget
description: Jak utworzyć pakiety NuGet, które zawierają formanty platformy uniwersalnej systemu Wizjudy lub WPF, w tym niezbędne metadane i pliki pomocnicze dla projektantów programu Visual Studio i Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: da8c5a05311c790bf6b873bc0f1a077d3ef1db87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610618"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="26a0f-103">Tworzenie kontrolek interfejsu użytkownika jako pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="26a0f-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="26a0f-104">Począwszy od programu Visual Studio 2017, można skorzystać z dodatkowych funkcji dla formantów platformy uniwersalnej systemu i WPF, które dostarczasz w pakietach NuGet.</span><span class="sxs-lookup"><span data-stu-id="26a0f-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="26a0f-105">W tym przewodniku przeprowadzi Cię przez te możliwości w kontekście formantów platformy uniwersalnej systemuśpiłnie przy użyciu [extensionSDKasNuGetPackage próbki](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="26a0f-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="26a0f-106">To samo dotyczy formantów WPF, chyba że określono inaczej.</span><span class="sxs-lookup"><span data-stu-id="26a0f-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26a0f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="26a0f-107">Prerequisites</span></span>

1. <span data-ttu-id="26a0f-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="26a0f-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="26a0f-109">Dowiesz się, jak [tworzyć pakiety platformy uniwersalnej systemuśpiłnie](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="26a0f-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="26a0f-110">Generowanie układu biblioteki</span><span class="sxs-lookup"><span data-stu-id="26a0f-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="26a0f-111">Dotyczy to tylko formantów platformy uniwersalnej systemuśpiłka.</span><span class="sxs-lookup"><span data-stu-id="26a0f-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="26a0f-112">Ustawienie `GenerateLibraryLayout` właściwości zapewnia, że dane wyjściowe kompilacji projektu jest generowany w układzie, który jest gotowy do pakowania bez konieczności poszczególnych wpisów plików w nuspec.</span><span class="sxs-lookup"><span data-stu-id="26a0f-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="26a0f-113">We właściwościach projektu przejdź do karty kompilacji i zaznacz pole wyboru "Generowanie układu biblioteki".</span><span class="sxs-lookup"><span data-stu-id="26a0f-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="26a0f-114">Spowoduje to zmodyfikowanie pliku `GenerateLibraryLayout` projektu i ustawienie flagi na true dla aktualnie wybranej konfiguracji kompilacji i platformy.</span><span class="sxs-lookup"><span data-stu-id="26a0f-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="26a0f-115">Alternatywnie edytuj plik projektu, `<GenerateLibraryLayout>true</GenerateLibraryLayout>` aby dodać go do pierwszej bezwarunkowej grupy właściwości.</span><span class="sxs-lookup"><span data-stu-id="26a0f-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="26a0f-116">To będzie zastosowanie właściwości niezależnie od konfiguracji kompilacji i platformy.</span><span class="sxs-lookup"><span data-stu-id="26a0f-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="26a0f-117">Dodawanie obsługi okienek przybornika/zasobów dla formantów XAML</span><span class="sxs-lookup"><span data-stu-id="26a0f-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="26a0f-118">Aby kontrolka XAML była wyświetlana w przyborniku projektanta XAML w programie `VisualStudioToolsManifest.xml` Visual Studio i `tools` okienku Zasoby programu Blend, utwórz plik w katalogu głównym folderu projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="26a0f-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="26a0f-119">Ten plik nie jest wymagany, jeśli nie potrzebujesz formantu, aby pojawić się w przyborniku lub okienku Zasoby.</span><span class="sxs-lookup"><span data-stu-id="26a0f-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="26a0f-120">Struktura pliku jest następująca:</span><span class="sxs-lookup"><span data-stu-id="26a0f-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="26a0f-121">gdzie:</span><span class="sxs-lookup"><span data-stu-id="26a0f-121">where:</span></span>

- <span data-ttu-id="26a0f-122">*your_package_file*: nazwa pliku kontrolnego, na `ManagedPackage.winmd` przykład ("ManagedPackage" jest dowolną nazwą używaną w tym przykładzie i nie ma innego znaczenia).</span><span class="sxs-lookup"><span data-stu-id="26a0f-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="26a0f-123">*vs_category:* Etykieta dla grupy, w której formant powinien pojawić się w przyborniku projektanta programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26a0f-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="26a0f-124">A `VSCategory` jest niezbędne, aby formant pojawiał się w przyborniku.</span><span class="sxs-lookup"><span data-stu-id="26a0f-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="26a0f-125">*blend_category*: Etykieta dla grupy, w której formant powinien być wyświetlany w okienku Zasoby projektanta mieszania.</span><span class="sxs-lookup"><span data-stu-id="26a0f-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="26a0f-126">A `BlendCategory` jest niezbędne do formantu do stawienia się w zasoby.</span><span class="sxs-lookup"><span data-stu-id="26a0f-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="26a0f-127">*type_full_name_n*: W pełni kwalifikowana nazwa dla każdego formantu, łącznie z obszarem nazw, na przykład `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="26a0f-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="26a0f-128">Należy zauważyć, że format kropki jest używany zarówno dla typów zarządzanych, jak i natywnych.</span><span class="sxs-lookup"><span data-stu-id="26a0f-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="26a0f-129">W bardziej zaawansowanych scenariuszach można `<File>` również `<FileList>` dołączyć wiele elementów w ramach, gdy pojedynczy pakiet zawiera wiele zestawów kontroli.</span><span class="sxs-lookup"><span data-stu-id="26a0f-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="26a0f-130">Można również mieć `<ToolboxItems>` wiele węzłów `<File>` w ramach jednego, jeśli chcesz zorganizować formanty w oddzielnych kategoriach.</span><span class="sxs-lookup"><span data-stu-id="26a0f-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="26a0f-131">W poniższym przykładzie formant `ManagedPackage.winmd` zaimplementowany w pojawi się w programie Visual Studio i Blend w grupie o nazwie "Pakiet zarządzany", a w tej grupie pojawi się "MyCustomControl".</span><span class="sxs-lookup"><span data-stu-id="26a0f-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="26a0f-132">Wszystkie te nazwy są dowolne.</span><span class="sxs-lookup"><span data-stu-id="26a0f-132">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Przykładowy formant wyświetlany w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Przykładowy formant wyświetlany w trybie Mieszania](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="26a0f-135">Należy jawnie określić każdy formant, który chcesz zobaczyć w polu narzędziowym/zasobach okienka.</span><span class="sxs-lookup"><span data-stu-id="26a0f-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="26a0f-136">Upewnij się, że `Namespace.ControlName`określisz je w formacie .</span><span class="sxs-lookup"><span data-stu-id="26a0f-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="26a0f-137">Dodawanie niestandardowych ikon do kontrolek</span><span class="sxs-lookup"><span data-stu-id="26a0f-137">Add custom icons to your controls</span></span>

<span data-ttu-id="26a0f-138">Aby wyświetlić niestandardową ikonę w okienku przybornika/zasobu, `design.dll` dodaj obraz do projektu lub odpowiedniego projektu o nazwie "Namespace.ControlName.extension" i ustaw akcję kompilacji na "Osadzony zasób".</span><span class="sxs-lookup"><span data-stu-id="26a0f-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="26a0f-139">Należy również upewnić się, że skojarzony `AssemblyInfo.cs` określa `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`atrybut ProvideMetadata - .</span><span class="sxs-lookup"><span data-stu-id="26a0f-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="26a0f-140">Zobacz ten [przykład](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="26a0f-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="26a0f-141">Obsługiwane formaty `.png`to `.jpg` `.jpeg`, `.gif`, `.bmp`, i .</span><span class="sxs-lookup"><span data-stu-id="26a0f-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="26a0f-142">Zalecanym formatem jest BMP24 w 16 pikselach na 16 pikseli.</span><span class="sxs-lookup"><span data-stu-id="26a0f-142">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Przykład ikony pola narzędzi](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="26a0f-144">Różowe tło zostanie zastąpione w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="26a0f-144">The pink background is replaced at runtime.</span></span> <span data-ttu-id="26a0f-145">Ikony są ponownie kolorowane po zmianie motywu programu Visual Studio i oczekuje się, że kolor tła.</span><span class="sxs-lookup"><span data-stu-id="26a0f-145">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="26a0f-146">Aby uzyskać więcej informacji, zapoznaj się [z obrazami i ikonami programu Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="26a0f-146">For more information, please reference [Images and Icons for Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="26a0f-147">W poniższym przykładzie projekt zawiera plik obrazu o nazwie "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="26a0f-147">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Ustawianie niestandardowej ikony w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="26a0f-149">W przypadku formantów natywnych należy `design.dll` umieścić ikonę jako zasób w projekcie.</span><span class="sxs-lookup"><span data-stu-id="26a0f-149">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="26a0f-150">Obsługa określonych wersji platformy systemu Windows</span><span class="sxs-lookup"><span data-stu-id="26a0f-150">Support specific Windows platform versions</span></span>

<span data-ttu-id="26a0f-151">Pakiety platformy uniwersalnej systemu Windows mają targetplatformversion (TPV) i TargetPlatformMinVersion (TPMinV), które definiują górne i dolne granice wersji systemu operacyjnego, w której można zainstalować aplikację.</span><span class="sxs-lookup"><span data-stu-id="26a0f-151">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="26a0f-152">TPV dalej określa wersję SDK, dla którego aplikacja jest zbudowana.</span><span class="sxs-lookup"><span data-stu-id="26a0f-152">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="26a0f-153">Należy pamiętać o tych właściwości podczas tworzenia pakietu platformy uniwersalnej systemu Windows: przy użyciu interfejsów API poza granicami wersji platformy zdefiniowane w aplikacji spowoduje, że kompilacja zakończy się niepowodzeniem lub aplikacji zakończy się niepowodzeniem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="26a0f-153">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="26a0f-154">Załóżmy na przykład, że ustawiłeś pakiet TPMinV dla pakietu formanty na Windows 10 Anniversary Edition (10.0; Kompilacja 14393), więc chcesz upewnić się, że pakiet jest zużywany tylko przez projekty platformy uniwersalnej systemu i platformy uniwersalnej systemu i platformy uniwersalnej systemu, które pasują do tej dolnej granicy.</span><span class="sxs-lookup"><span data-stu-id="26a0f-154">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="26a0f-155">Aby zezwolić na korzystanie z pakietu przez projekty platformy uniwersalnej systemu Windows, należy spakować formanty z następującymi nazwami folderów:</span><span class="sxs-lookup"><span data-stu-id="26a0f-155">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="26a0f-156">NuGet automatycznie sprawdzi TPMinV projektu zużywającego i zakończy się niepowodzeniem instalacji, jeśli jest niższa niż Windows 10 Anniversary Edition (10.0; Kompilacja 14393)</span><span class="sxs-lookup"><span data-stu-id="26a0f-156">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="26a0f-157">W przypadku WPF, załóżmy, że chcesz, aby pakiet formanty WPF do korzystania przez projekty przeznaczone dla platformy .NET Framework v4.6.1 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="26a0f-157">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="26a0f-158">Aby to wymusić, należy spakować formanty z następującymi nazwami folderów:</span><span class="sxs-lookup"><span data-stu-id="26a0f-158">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="26a0f-159">Dodaj obsługę czasu projektowania</span><span class="sxs-lookup"><span data-stu-id="26a0f-159">Add design-time support</span></span>

<span data-ttu-id="26a0f-160">Aby skonfigurować, gdzie właściwości formantu są wyświetlane w inspektorze właściwości, dodaj `design.dll` niestandardowe `lib\uap10.0.14393\Design` adorners itp., umieść plik wewnątrz folderu odpowiednio do platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="26a0f-160">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="26a0f-161">Ponadto, aby upewnić się, że edytuj szablon > Edytuj funkcję `Generic.xaml` **[kopiowania](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** działa, należy dołączyć `<your_assembly_name>\Themes` i wszystkie słowniki zasobów, które scala się w folderze (ponownie, przy użyciu rzeczywistej nazwy zestawu).</span><span class="sxs-lookup"><span data-stu-id="26a0f-161">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="26a0f-162">(Ten plik nie ma wpływu na zachowanie środowiska wykonawczego formantu.) Struktura folderów wydaje się zatem następująca:</span><span class="sxs-lookup"><span data-stu-id="26a0f-162">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="26a0f-163">W przypadku WPF, kontynuując przykład, w którym chcesz, aby pakiet formanty WPF był zużywany przez projekty przeznaczone dla platformy .NET Framework w wersji 4.6.1 lub wyższej:</span><span class="sxs-lookup"><span data-stu-id="26a0f-163">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="26a0f-164">Domyślnie właściwości formantu będą wyświetlane w kategorii Różne w Inspektorze właściwości.</span><span class="sxs-lookup"><span data-stu-id="26a0f-164">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="26a0f-165">Używanie ciągów i zasobów</span><span class="sxs-lookup"><span data-stu-id="26a0f-165">Use strings and resources</span></span>

<span data-ttu-id="26a0f-166">Można osadzić zasoby`.resw`ciągów ( ) w pakiecie, który może być używany przez formant lub `.resw` zużywający projekt platformy uniwersalnej systemu wytwórczego, ustaw właściwość **Kompilacja pliku** na **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="26a0f-166">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="26a0f-167">Na przykład należy zapoznać się [z MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w ExtensionSDKasNuGetPackage próbki.</span><span class="sxs-lookup"><span data-stu-id="26a0f-167">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="26a0f-168">Dotyczy to tylko formantów platformy uniwersalnej systemuśpiłka.</span><span class="sxs-lookup"><span data-stu-id="26a0f-168">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="26a0f-169">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="26a0f-169">See also</span></span>

- [<span data-ttu-id="26a0f-170">Tworzenie pakietów platformy uniwersalnej systemu i platformy uniwersalnej systemu</span><span class="sxs-lookup"><span data-stu-id="26a0f-170">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="26a0f-171">ExtensionSDKasNuGetPackage przykład</span><span class="sxs-lookup"><span data-stu-id="26a0f-171">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
