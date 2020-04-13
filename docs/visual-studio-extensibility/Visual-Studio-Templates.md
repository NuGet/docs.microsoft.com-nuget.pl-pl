---
title: Pakiety NuGet w szablonach programu Visual Studio
description: Instrukcje dotyczące dołączania pakietów NuGet w ramach szablonów projektów i elementów programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498240"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="fd739-103">Pakiety w szablonach programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fd739-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="fd739-104">Szablony projektów i elementów programu Visual Studio często muszą upewnić się, że niektóre pakiety są instalowane podczas tworzenia projektu lub elementu.</span><span class="sxs-lookup"><span data-stu-id="fd739-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="fd739-105">Na przykład szablon ASP.NET MVC 3 instaluje jQuery, Modernizr i inne pakiety.</span><span class="sxs-lookup"><span data-stu-id="fd739-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="fd739-106">Aby to poprzeć, autorzy szablonów mogą poinstruować NuGet, aby zainstalował niezbędne pakiety, a nie poszczególne biblioteki.</span><span class="sxs-lookup"><span data-stu-id="fd739-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="fd739-107">Deweloperzy mogą następnie łatwo zaktualizować te pakiety w dowolnym późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="fd739-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="fd739-108">Aby dowiedzieć się więcej o samodzielnym tworzeniu szablonów, zobacz [Jak: Tworzenie szablonów projektów](/visualstudio/ide/how-to-create-project-templates) lub [Tworzenie szablonów projektów niestandardowych i elementów](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="fd739-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="fd739-109">W dalszej części tej sekcji opisano konkretne kroki, które należy wykonać podczas tworzenia szablonu, aby poprawnie dołączyć pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd739-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="fd739-110">Dodawanie pakietów do szablonu</span><span class="sxs-lookup"><span data-stu-id="fd739-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="fd739-111">Najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fd739-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="fd739-112">Na przykład zobacz [przykład NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="fd739-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="fd739-113">Dodawanie pakietów do szablonu</span><span class="sxs-lookup"><span data-stu-id="fd739-113">Adding packages to a template</span></span>

<span data-ttu-id="fd739-114">Po wystąpieniu szablonu jest wywoływany [kreator szablonów,](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) aby załadować listę pakietów do zainstalowania wraz z informacjami o tym, gdzie można znaleźć te pakiety.</span><span class="sxs-lookup"><span data-stu-id="fd739-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="fd739-115">Pakiety mogą być osadzone w vsix, osadzone w szablonie lub znajduje się na lokalnym dysku twardym, w którym to przypadku można użyć klucza rejestru, aby odwołać się do ścieżki pliku.</span><span class="sxs-lookup"><span data-stu-id="fd739-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="fd739-116">Szczegółowe informacje na temat tych lokalizacji podano w dalszej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="fd739-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="fd739-117">Preinstalowane pakiety działają przy użyciu [kreatorów szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="fd739-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="fd739-118">Specjalny kreator jest wywoływany, gdy szablon zostanie s wystąpieniowy.</span><span class="sxs-lookup"><span data-stu-id="fd739-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="fd739-119">Kreator ładuje listę pakietów, które muszą być zainstalowane i przekazuje te informacje do odpowiednich interfejsów API NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd739-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="fd739-120">Kroki dołączania pakietów do szablonu:</span><span class="sxs-lookup"><span data-stu-id="fd739-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="fd739-121">W `vstemplate` pliku dodaj odwołanie do kreatora szablonu [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) NuGet, dodając element:</span><span class="sxs-lookup"><span data-stu-id="fd739-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="fd739-122">`NuGet.VisualStudio.Interop.dll`jest zestawem, który `TemplateWizard` zawiera tylko klasę, która jest prostym otokiem, który wywołuje rzeczywistą implementację w . `NuGet.VisualStudio.dll`</span><span class="sxs-lookup"><span data-stu-id="fd739-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="fd739-123">Wersja zestawu nigdy nie zmieni się tak, że szablony projektu/elementu nadal pracować z nowymi wersjami NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd739-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="fd739-124">Dodaj listę pakietów do zainstalowania w projekcie:</span><span class="sxs-lookup"><span data-stu-id="fd739-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="fd739-125">Kreator obsługuje `<package>` wiele elementów do obsługi wielu źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="fd739-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="fd739-126">Wymagane `id` są `version` atrybuty i atrybuty, co oznacza, że zostanie zainstalowana określona wersja pakietu, nawet jeśli dostępna jest nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="fd739-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="fd739-127">Zapobiega to aktualizacji pakietu z łamanie szablonu, pozostawiając możliwość aktualizacji pakietu do dewelopera przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="fd739-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="fd739-128">Określ repozytorium, w którym NuGet można znaleźć pakiety zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="fd739-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="fd739-129">Repozytorium pakietów VSIX</span><span class="sxs-lookup"><span data-stu-id="fd739-129">VSIX package repository</span></span>

<span data-ttu-id="fd739-130">Zalecane podejście wdrażania dla szablonów projektu/elementu programu Visual Studio jest [rozszerzeniem VSIX,](/visualstudio/extensibility/shipping-visual-studio-extensions) ponieważ umożliwia spakowanie wielu szablonów projektu/elementu razem i umożliwia deweloperom łatwe odnajdywanie szablonów przy użyciu Menedżera rozszerzeń programu VS lub Galerii programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd739-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="fd739-131">Aktualizacje rozszerzenia są również łatwe do wdrożenia przy użyciu [mechanizmu automatycznej aktualizacji programu Visual Studio Extension Manager](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="fd739-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="fd739-132">Sam VSIX może służyć jako źródło pakietów wymaganych przez szablon:</span><span class="sxs-lookup"><span data-stu-id="fd739-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="fd739-133">Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fd739-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="fd739-134">Atrybut `repository` określa typ repozytorium, gdy `extension` `repositoryId` jest unikatowym identyfikatorem samego VSIX (Jest to `ID` wartość atrybutu w `vsixmanifest` pliku rozszerzenia, zobacz [Odwołanie do schematu rozszerzenia VSIX 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="fd739-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="fd739-135">Umieść `nupkg` pliki w folderze wywoływanym `Packages` w programie VSIX.</span><span class="sxs-lookup"><span data-stu-id="fd739-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="fd739-136">Dodaj niezbędne pliki `<Asset>` pakietów, jak w `vsixmanifest` pliku (zobacz odwołanie do [schematu rozszerzenia VSIX 2.0):](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)</span><span class="sxs-lookup"><span data-stu-id="fd739-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="fd739-137">Należy zauważyć, że można dostarczyć pakiety w tym samym VSIX jako szablony projektu lub można umieścić je w osobnym VSIX, jeśli ma to większy sens dla scenariusza.</span><span class="sxs-lookup"><span data-stu-id="fd739-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="fd739-138">Jednak nie odwoływać się do wszystkich VSIX, nad którym nie masz kontroli, ponieważ zmiany w tym rozszerzeniu może spowodować przerwanie szablonu.</span><span class="sxs-lookup"><span data-stu-id="fd739-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="fd739-139">Repozytorium pakietów szablonów</span><span class="sxs-lookup"><span data-stu-id="fd739-139">Template package repository</span></span>

<span data-ttu-id="fd739-140">Jeśli rozprowadzasz tylko jeden szablon projektu/elementu i nie musisz pakować wielu szablonów razem, możesz użyć prostszego, ale bardziej ograniczonego podejścia, które zawiera pakiety bezpośrednio w pliku ZIP szablonu projektu/elementu:</span><span class="sxs-lookup"><span data-stu-id="fd739-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="fd739-141">Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fd739-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="fd739-142">Atrybut `repository` ma wartość `template` i `repositoryId` atrybut nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="fd739-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="fd739-143">Umieść pakiety w folderze głównym pliku ZIP szablonu projektu/elementu.</span><span class="sxs-lookup"><span data-stu-id="fd739-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="fd739-144">Należy zauważyć, że za pomocą tej metody w VSIX, który zawiera wiele szablonów prowadzi do niepotrzebnego uwędzić, gdy jeden lub więcej pakietów są wspólne dla szablonów.</span><span class="sxs-lookup"><span data-stu-id="fd739-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="fd739-145">W takich przypadkach należy użyć [VSIX jako repozytorium,](#vsix-package-repository) jak opisano w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="fd739-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="fd739-146">Ścieżka folderu określona w rejestrze</span><span class="sxs-lookup"><span data-stu-id="fd739-146">Registry-specified folder path</span></span>

<span data-ttu-id="fd739-147">Zestawy SDK zainstalowane przy użyciu msi można zainstalować pakiety NuGet bezpośrednio na komputerze dewelopera.</span><span class="sxs-lookup"><span data-stu-id="fd739-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="fd739-148">Dzięki temu natychmiast dostępne, gdy używany jest szablon projektu lub elementu, zamiast wyodrębnić je w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="fd739-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="fd739-149">ASP.NET szablony używają tego podejścia.</span><span class="sxs-lookup"><span data-stu-id="fd739-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="fd739-150">Zamieść pakiety instalacyjne MSI na komputerze.</span><span class="sxs-lookup"><span data-stu-id="fd739-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="fd739-151">Można zainstalować tylko `.nupkg` pliki lub można je zainstalować wraz z rozwiniętą zawartością, co pozwala zaoszczędzić dodatkowy krok, gdy szablon jest używany.</span><span class="sxs-lookup"><span data-stu-id="fd739-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="fd739-152">W takim przypadku należy postępować zgodnie ze standardową strukturą folderów NuGet, w której `.nupkg` pliki znajdują się w folderze głównym, a następnie każdy pakiet ma podfolder z parą identyfikator/wersja jako nazwę podfolderu.</span><span class="sxs-lookup"><span data-stu-id="fd739-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="fd739-153">Napisz klucz rejestru, aby zidentyfikować lokalizację pakietu:</span><span class="sxs-lookup"><span data-stu-id="fd739-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="fd739-154">Kluczowa lokalizacja: szablony i `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` pakiety zainstalowane na całym komputerze lub na użytkownika, alternatywnie`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="fd739-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="fd739-155">Nazwa klucza: użyj nazwy, która jest dla Ciebie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="fd739-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="fd739-156">Na przykład ASP.NET szablonów MVC 4 dla vs 2012 używać `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="fd739-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="fd739-157">Wartości: pełna ścieżka do folderu pakietów.</span><span class="sxs-lookup"><span data-stu-id="fd739-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="fd739-158">W `<packages>` elemencie w `.vstemplate` pliku `repository="registry"` dodaj atrybut i określ `keyName` nazwę klucza rejestru w atrybucie.</span><span class="sxs-lookup"><span data-stu-id="fd739-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="fd739-159">Jeśli wstępnie rozpakowałeś pakiety, użyj `isPreunzipped="true"` tego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="fd739-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="fd739-160">*(NuGet 3.2+)* Jeśli chcesz wymusić kompilację czasu projektowania na końcu `forceDesignTimeBuild="true"` instalacji pakietu, dodaj atrybut.</span><span class="sxs-lookup"><span data-stu-id="fd739-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="fd739-161">Jako optymalizację `skipAssemblyReferences="true"` dodaj, ponieważ sam szablon zawiera już niezbędne odwołania.</span><span class="sxs-lookup"><span data-stu-id="fd739-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="fd739-162">Najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="fd739-162">Best Practices</span></span>

1. <span data-ttu-id="fd739-163">Zadeklaruj zależność od NuGet VSIX, dodając odwołanie do niej w manifeście VSIX:</span><span class="sxs-lookup"><span data-stu-id="fd739-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="fd739-164">Wymagaj, aby szablony projektu/elementu [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) były `.vstemplate` zapisywane podczas tworzenia, dołączając do niego plik.</span><span class="sxs-lookup"><span data-stu-id="fd739-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="fd739-165">Szablony nie zawierają `packages.config` pliku i nie zawierają żadnych odwołań ani zawartości, które zostaną dodane po zainstalowaniu pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd739-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
