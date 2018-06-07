---
title: Jak formantów interfejsu użytkownika pakietu NuGet
description: Tworzenie pakietów NuGet, które zawierają platformy uniwersalnej systemu Windows lub programu WPF steruje tym niezbędne metadane i pliki pomocnicze dla programu Visual Studio i Blend projektantów.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ab7499c415f63319fd314f33607f74d400b5f957
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818661"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="128fa-103">Tworzenie formantów interfejsu użytkownika jako pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="128fa-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="128fa-104">Z programu Visual Studio 2017 r można korzystać z możliwości dodane dla platformy uniwersalnej systemu Windows i WPF formantów dostarczających w pakietach NuGet.</span><span class="sxs-lookup"><span data-stu-id="128fa-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="128fa-105">Ten przewodnik przeprowadzi Cię przez te funkcje w kontekście formantów platformy uniwersalnej systemu Windows za pomocą [próbki ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="128fa-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="128fa-106">To samo dotyczy formantów WPF chyba, że wymienione w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="128fa-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="128fa-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="128fa-107">Prerequisites</span></span>

1. <span data-ttu-id="128fa-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="128fa-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="128fa-109">Opis sposobu [tworzenia pakietów platformy uniwersalnej systemu Windows](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="128fa-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="128fa-110">Generowanie układu biblioteki</span><span class="sxs-lookup"><span data-stu-id="128fa-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="128fa-111">Ma to zastosowanie tylko do formantów platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="128fa-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="128fa-112">Ustawienie `GenerateLibraryLayout` właściwości zapewnia wygenerowania danych wyjściowych kompilacji projektu w układzie, który jest gotowy do umieszczone bez konieczności poszczególne wpisy w plik nuspec.</span><span class="sxs-lookup"><span data-stu-id="128fa-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="128fa-113">We właściwościach projektu, przejdź do karty kompilacji, a następnie zaznacz pole wyboru "Generowanie układu biblioteki".</span><span class="sxs-lookup"><span data-stu-id="128fa-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="128fa-114">Spowoduje to modyfikowania pliku projektu i ustawić `GenerateLibraryLayout` flagi na wartość true dla aktualnie wybranej kompilacji konfiguracji i platformy.</span><span class="sxs-lookup"><span data-stu-id="128fa-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="128fa-115">Alternatywnie Edytuj plik projektu, aby dodać `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do pierwszej grupy właściwości bezwarunkowe.</span><span class="sxs-lookup"><span data-stu-id="128fa-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="128fa-116">Ma to zastosowanie właściwości niezależnie od konfigurację kompilacji i platformy.</span><span class="sxs-lookup"><span data-stu-id="128fa-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="128fa-117">Obsługę przybornika/zasoby okienka kontrolki XAML</span><span class="sxs-lookup"><span data-stu-id="128fa-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="128fa-118">Aby wymusić formantowi XAML w przyborniku projektanta XAML w Visual Studio i w okienku zasobów programu Blend, Utwórz `VisualStudioToolsManifest.xml` pliku w folderze głównym `tools` folderu projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="128fa-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="128fa-119">Ten plik nie jest wymagane, jeśli nie ma potrzeby wyglądać w przyborniku lub w okienku zasoby.</span><span class="sxs-lookup"><span data-stu-id="128fa-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="128fa-120">Struktura pliku jest następujący:</span><span class="sxs-lookup"><span data-stu-id="128fa-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="128fa-121">gdzie:</span><span class="sxs-lookup"><span data-stu-id="128fa-121">where:</span></span>

- <span data-ttu-id="128fa-122">*your_package_file*: Nazwa formantu plików, takich jak `ManagedPackage.winmd` ("ManagedPackage" jest używany w tym przykładzie dowolnego o nazwie i nie ma innych znaczenia).</span><span class="sxs-lookup"><span data-stu-id="128fa-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="128fa-123">*vs_category*: Etykieta grupy, w którym ma wyglądać formant przybornika projektanta programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="128fa-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="128fa-124">A `VSCategory` jest niezbędna dla formantu pojawią się w przyborniku.</span><span class="sxs-lookup"><span data-stu-id="128fa-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="128fa-125">*blend_category*: Etykieta grupy ma wyglądać formant, w okienku zasoby projektanta mieszania.</span><span class="sxs-lookup"><span data-stu-id="128fa-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="128fa-126">A `BlendCategory` jest niezbędna dla formantu pojawią się w zasobach.</span><span class="sxs-lookup"><span data-stu-id="128fa-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="128fa-127">*type_full_name_n*: pełni kwalifikowaną nazwą dla każdej kontrolki, w tym przestrzeń nazw, takich jak `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="128fa-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="128fa-128">Należy pamiętać, że format kropka jest używana przez typy zarządzane i natywne.</span><span class="sxs-lookup"><span data-stu-id="128fa-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="128fa-129">W bardziej zaawansowanych scenariuszy, mogą również obejmować wiele `<File>` elementów w obrębie `<FileList>` Jeśli pojedynczy pakiet zawiera wiele zestawów formantu.</span><span class="sxs-lookup"><span data-stu-id="128fa-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="128fa-130">Można również mieć wielu `<ToolboxItems>` węzłów w jednym `<File>` aby organizować formantów na osobne kategorie.</span><span class="sxs-lookup"><span data-stu-id="128fa-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="128fa-131">W poniższym przykładzie formantu realizowane w `ManagedPackage.winmd` będą wyświetlane w programie Visual Studio i Blend w grupie o nazwie "Zarządzanego pakietu" i "MyCustomControl" pojawi się w tej grupie.</span><span class="sxs-lookup"><span data-stu-id="128fa-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="128fa-132">Te nazwy są dowolne.</span><span class="sxs-lookup"><span data-stu-id="128fa-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="128fa-135">Należy jawnie określić każdego formantu, który chcesz wyświetlić w okienku przybornika/zasobów.</span><span class="sxs-lookup"><span data-stu-id="128fa-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="128fa-136">Upewnij się, określ w formacie `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="128fa-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="128fa-137">Dodawanie ikon niestandardowych do formantów</span><span class="sxs-lookup"><span data-stu-id="128fa-137">Add custom icons to your controls</span></span>

<span data-ttu-id="128fa-138">Aby wyświetlić ikon niestandardowych w okienku przybornika/zasoby, należy dodać obraz do projektu lub odpowiednie `design.dll` projektu o nazwie "Namespace.ControlName.extension" i ustawić akcji kompilacji "Osadzonego zasobu".</span><span class="sxs-lookup"><span data-stu-id="128fa-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="128fa-139">Obsługiwane formaty to `.png`, `.jpg`, `.jpeg`, `.gif`, i `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="128fa-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="128fa-140">Rozmiar obrazu zalecane jest x 64 pikseli 64.</span><span class="sxs-lookup"><span data-stu-id="128fa-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="128fa-141">W poniższym przykładzie projekt zawiera plik o nazwie "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="128fa-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Ustawienie ikon niestandardowych w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="128fa-143">Dla natywnych kontrolek, możesz umieścić ikony jako zasób w `design.dll` projektu.</span><span class="sxs-lookup"><span data-stu-id="128fa-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="128fa-144">Obsługuje określonych wersji platformy systemu Windows</span><span class="sxs-lookup"><span data-stu-id="128fa-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="128fa-145">Pakiety platformy uniwersalnej systemu Windows zawierają TargetPlatformVersion (TPV) i TargetPlatformMinVersion (TPMinV), które definiują górne i dolne granice wersji systemu operacyjnego zainstalowaną aplikację.</span><span class="sxs-lookup"><span data-stu-id="128fa-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="128fa-146">Dalsze TPV Określa wersję zestawu SDK, względem której aplikacja jest wbudowana.</span><span class="sxs-lookup"><span data-stu-id="128fa-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="128fa-147">Można w trosce o te właściwości, podczas tworzenia pakietu platformy uniwersalnej systemu Windows: poza granicami wersje platformy zdefiniowanych w aplikacji przy użyciu interfejsów API spowoduje niepowodzenie kompilacji lub aplikację, aby zakończyć się niepowodzeniem w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="128fa-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="128fa-148">Na przykład załóżmy, że ustawiono TPMinV pakietu formantów systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393), tak aby mieć pewność, że pakiet jest używany tylko przez platformy uniwersalnej systemu Windows projekcję pasujących obniżyć powiązane z.</span><span class="sxs-lookup"><span data-stu-id="128fa-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="128fa-149">Umożliwia pakietu zużywanych przez projekty platformy uniwersalnej systemu Windows, należy spakować formantów z następującymi nazwami folderu:</span><span class="sxs-lookup"><span data-stu-id="128fa-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="128fa-150">NuGet zostanie automatycznie Sprawdź TPMinV odbierającą projektu i niepowodzenie instalacji, jeśli jest mniejszy od systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393)</span><span class="sxs-lookup"><span data-stu-id="128fa-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="128fa-151">W przypadku WPF Załóżmy się, że chcesz pakietu formantów WPF wykorzystanych w projektach przeznaczonych dla platformy .NET Framework v4.6.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="128fa-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="128fa-152">Aby wymusić, który, należy spakować formantów z następującymi nazwami folderu:</span><span class="sxs-lookup"><span data-stu-id="128fa-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="128fa-153">Dodawanie obsługi w czasie projektowania</span><span class="sxs-lookup"><span data-stu-id="128fa-153">Add design-time support</span></span>

<span data-ttu-id="128fa-154">Aby skonfigurować, których właściwości wyświetlane w Inspektora właściwości, Dodaj niestandardowego modułu definiowania układu kodu itp., umieść Twojej `design.dll` pliku wewnątrz `lib\uap10.0.14393\Design` folderu odpowiednio do platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="128fa-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="128fa-155">Ponadto aby upewnić się, że **[Edytuj szablon > edytowania kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** działa funkcja musi zawierać `Generic.xaml` i słowników zasobów, które w scaleń `<your_assembly_name>\Themes` folder (ponownie, używając Nazwa zestawu rzeczywiste).</span><span class="sxs-lookup"><span data-stu-id="128fa-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="128fa-156">(Ten plik nie ma wpływu na zachowanie środowiska uruchomieniowego formantu.) Struktura folderów w związku z tym będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="128fa-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="128fa-157">Dla WPF kontynuowanie w przykładzie miejsce chcesz programu WPF kontrolki pakiecie będą wykorzystane w projektach przeznaczonych dla platformy .NET Framework v4.6.1 lub nowszy:</span><span class="sxs-lookup"><span data-stu-id="128fa-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="128fa-158">Domyślnie właściwości formantu będą widoczne w różnych kategorii w Inspektora właściwości.</span><span class="sxs-lookup"><span data-stu-id="128fa-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="128fa-159">Użyj ciągów i zasobów</span><span class="sxs-lookup"><span data-stu-id="128fa-159">Use strings and resources</span></span>

<span data-ttu-id="128fa-160">Osadzić zasobów ciągu (`.resw`) do pakietu, które mogą być używane przez formant lub odbierającą projektu platformy uniwersalnej systemu Windows, należy ustawić **Akcja kompilacji** właściwość `.resw` pliku **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="128fa-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="128fa-161">Na przykład dotyczą [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładowym ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="128fa-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="128fa-162">Ma to zastosowanie tylko do formantów platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="128fa-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="128fa-163">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="128fa-163">See also</span></span>

- [<span data-ttu-id="128fa-164">Tworzenie pakietów platformy UWP</span><span class="sxs-lookup"><span data-stu-id="128fa-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="128fa-165">Przykładowe ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="128fa-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
