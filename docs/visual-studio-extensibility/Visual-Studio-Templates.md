---
title: Pakiety NuGet w szablonach programu Visual Studio
description: Instrukcje dotyczące dołączania pakietów NuGet jako części szablonów projektów i elementów programu Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 2dfbd793eee05169f051d9c8943bc065945b92da
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622645"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="24eda-103">Pakiety w szablonach programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24eda-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="24eda-104">Szablony projektów i elementów programu Visual Studio często muszą mieć pewność, że niektóre pakiety są instalowane podczas tworzenia projektu lub elementu.</span><span class="sxs-lookup"><span data-stu-id="24eda-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="24eda-105">Na przykład szablon ASP.NET MVC 3 instaluje jQuery, modernizację i inne pakiety.</span><span class="sxs-lookup"><span data-stu-id="24eda-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="24eda-106">Aby to umożliwić, autorzy szablonów mogą wydać pakietowi NuGet zainstalowanie wymaganych pakietów zamiast poszczególnych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="24eda-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="24eda-107">Deweloperzy mogą następnie łatwo aktualizować te pakiety w dowolnym późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="24eda-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="24eda-108">Aby dowiedzieć się więcej na temat tworzenia szablonów, zobacz [jak: Tworzenie szablonów projektu](/visualstudio/ide/how-to-create-project-templates) lub [Tworzenie niestandardowych szablonów projektów i elementów](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="24eda-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="24eda-109">W pozostałej części tej sekcji opisano czynności, które należy wykonać podczas tworzenia szablonu w celu poprawnego uwzględnienia pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="24eda-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="24eda-110">Dodawanie pakietów do szablonu</span><span class="sxs-lookup"><span data-stu-id="24eda-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="24eda-111">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="24eda-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="24eda-112">Aby zapoznać się z przykładem, zobacz [NuGetInVsTemplates Sample](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="24eda-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="24eda-113">Dodawanie pakietów do szablonu</span><span class="sxs-lookup"><span data-stu-id="24eda-113">Adding packages to a template</span></span>

<span data-ttu-id="24eda-114">Po utworzeniu wystąpienia szablonu [Kreator szablonu](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) jest wywoływany w celu załadowania listy pakietów do zainstalowania wraz z informacjami o miejscu, w którym można znaleźć te pakiety.</span><span class="sxs-lookup"><span data-stu-id="24eda-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="24eda-115">Pakiety mogą być osadzone w VSIX, osadzone w szablonie lub znajdować się na lokalnym dysku twardym, w którym należy użyć klucza rejestru do odwoływania się do ścieżki pliku.</span><span class="sxs-lookup"><span data-stu-id="24eda-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="24eda-116">Szczegółowe informacje o tych lokalizacjach znajdują się w dalszej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="24eda-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="24eda-117">Wstępnie zainstalowane pakiety działają przy użyciu [kreatorów szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="24eda-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="24eda-118">Po utworzeniu wystąpienia szablonu zostanie wywołany specjalny Kreator.</span><span class="sxs-lookup"><span data-stu-id="24eda-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="24eda-119">Kreator ładuje listę pakietów, które muszą być zainstalowane, i przekazuje te informacje do odpowiednich interfejsów API NuGet.</span><span class="sxs-lookup"><span data-stu-id="24eda-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="24eda-120">Procedura dołączania pakietów do szablonu:</span><span class="sxs-lookup"><span data-stu-id="24eda-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="24eda-121">W `vstemplate` pliku Dodaj odwołanie do Kreatora szablonu NuGet poprzez dodanie [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elementu:</span><span class="sxs-lookup"><span data-stu-id="24eda-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="24eda-122">`NuGet.VisualStudio.Interop.dll` jest zestawem zawierającym tylko `TemplateWizard` klasę, która jest prostym otoką, która wywołuje rzeczywistą implementację w `NuGet.VisualStudio.dll` .</span><span class="sxs-lookup"><span data-stu-id="24eda-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="24eda-123">Wersja zestawu nigdy nie ulegnie zmianie, tak aby szablony projektów i elementów nadal działały z nowymi wersjami programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="24eda-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="24eda-124">Dodaj listę pakietów do zainstalowania w projekcie:</span><span class="sxs-lookup"><span data-stu-id="24eda-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="24eda-125">Kreator obsługuje wiele `<package>` elementów do obsługi wielu źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="24eda-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="24eda-126">Oba `id` atrybuty i `version` są wymagane, co oznacza, że określona wersja pakietu zostanie zainstalowana, nawet jeśli jest dostępna nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="24eda-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="24eda-127">Zapobiega to przerywaniu szablonu przez aktualizacje pakietów, pozostawiając wybór w celu zaktualizowania pakietu do dewelopera przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="24eda-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="24eda-128">Określ repozytorium, w którym narzędzia NuGet mogą znaleźć pakiety zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="24eda-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="24eda-129">Repozytorium pakietu VSIX</span><span class="sxs-lookup"><span data-stu-id="24eda-129">VSIX package repository</span></span>

<span data-ttu-id="24eda-130">Zalecanym podejściem do wdrażania szablonów projektów/elementów programu Visual Studio jest [rozszerzenie VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) , ponieważ umożliwia ono spakowanie wielu szablonów projektów/elementów i umożliwia deweloperom łatwe odnajdywanie szablonów przy użyciu Menedżera rozszerzenia programu vs lub Galerii programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24eda-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="24eda-131">Aktualizacje rozszerzenia można również łatwo wdrożyć przy użyciu [mechanizmu aktualizacji automatycznych programu Visual Studio Extension Manager](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="24eda-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="24eda-132">Sam VSIX może stanowić źródło pakietów wymaganych przez szablon:</span><span class="sxs-lookup"><span data-stu-id="24eda-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="24eda-133">Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="24eda-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="24eda-134">Ten `repository` atrybut określa typ repozytorium, tak jak `extension` while `repositoryId` jest unikatowym identyfikatorem VSIX (jest to wartość `ID` atrybutu w `vsixmanifest` pliku rozszerzenia, zobacz [Dokumentacja schematu rozszerzenia VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="24eda-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="24eda-135">Umieść `nupkg` pliki w folderze o nazwie w `Packages` VSIX.</span><span class="sxs-lookup"><span data-stu-id="24eda-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="24eda-136">Dodaj niezbędne pliki pakietu jako `<Asset>` `vsixmanifest` plik (zobacz [odwołanie do schematu rozszerzenia VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="24eda-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="24eda-137">Należy pamiętać, że możesz dostarczać pakiety w tym samym VSIX co szablony projektu lub umieścić je w oddzielnym VSIX, jeśli ma to sens dla scenariusza.</span><span class="sxs-lookup"><span data-stu-id="24eda-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="24eda-138">Jednakże nie należy odwoływać się do żadnego VSIX, nad którym nie masz kontroli, ponieważ zmiany w tym rozszerzeniu mogłyby spowodować uszkodzenie szablonu.</span><span class="sxs-lookup"><span data-stu-id="24eda-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="24eda-139">Repozytorium pakietu szablonów</span><span class="sxs-lookup"><span data-stu-id="24eda-139">Template package repository</span></span>

<span data-ttu-id="24eda-140">Jeśli dystrybuowany jest tylko jeden szablon projektu/elementu i nie ma potrzeby jednoczesnego pakowania wielu szablonów, można użyć prostszego, ale bardziej ograniczonego podejścia zawierającego pakiety bezpośrednio w pliku ZIP szablonu/elementu.</span><span class="sxs-lookup"><span data-stu-id="24eda-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="24eda-141">Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="24eda-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="24eda-142">`repository`Atrybut ma wartość `template` i `repositoryId` atrybut nie jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="24eda-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="24eda-143">Umieść pakiety w folderze głównym pliku ZIP szablonu/elementu.</span><span class="sxs-lookup"><span data-stu-id="24eda-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="24eda-144">Należy zauważyć, że użycie tej metody w VSIX, która zawiera wiele szablonów, prowadzi do niepotrzebnych przeładowanie, gdy jeden lub więcej pakietów jest wspólnych dla szablonów.</span><span class="sxs-lookup"><span data-stu-id="24eda-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="24eda-145">W takich przypadkach należy użyć [VSIX jako repozytorium](#vsix-package-repository) , zgodnie z opisem w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="24eda-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="24eda-146">Ścieżka folderu określona w rejestrze</span><span class="sxs-lookup"><span data-stu-id="24eda-146">Registry-specified folder path</span></span>

<span data-ttu-id="24eda-147">Zestawy SDK, które są instalowane przy użyciu pliku MSI, mogą instalować pakiety NuGet bezpośrednio na komputerze dewelopera.</span><span class="sxs-lookup"><span data-stu-id="24eda-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="24eda-148">Dzięki temu są one natychmiast dostępne, gdy zostanie użyty szablon projektu lub elementu, a nie trzeba go wyodrębnić w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="24eda-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="24eda-149">Użycie tego podejścia przez szablony ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="24eda-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="24eda-150">Zainstaluj pakiety MSI na komputerze.</span><span class="sxs-lookup"><span data-stu-id="24eda-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="24eda-151">Można zainstalować tylko `.nupkg` pliki lub zainstalować je wraz z rozwiniętą zawartością, co spowoduje zaoszczędzenie dodatkowego kroku, gdy szablon jest używany.</span><span class="sxs-lookup"><span data-stu-id="24eda-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="24eda-152">W takim przypadku należy przestrzegać standardowej struktury folderów programu NuGet `.nupkg` , w której pliki znajdują się w folderze głównym, a następnie każdy pakiet ma podfolder z parą ID/Version jako nazwę podfolderu.</span><span class="sxs-lookup"><span data-stu-id="24eda-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="24eda-153">Napisz klucz rejestru, aby zidentyfikować lokalizację pakietu:</span><span class="sxs-lookup"><span data-stu-id="24eda-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="24eda-154">Lokalizacja klucza: dla całej maszyny lub w `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` przypadku szablonów i pakietów zainstalowanych dla poszczególnych użytkowników, Alternatywnie użyj `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="24eda-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="24eda-155">Nazwa klucza: Użyj nazwy, która jest unikatowa dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24eda-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="24eda-156">Przykładowo Użyj szablonów ASP.NET MVC 4 dla programu VS 2012 `AspNetMvc4VS11` .</span><span class="sxs-lookup"><span data-stu-id="24eda-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="24eda-157">Wartości: pełna ścieżka do folderu Packages.</span><span class="sxs-lookup"><span data-stu-id="24eda-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="24eda-158">W `<packages>` elemencie w `.vstemplate` pliku, Dodaj atrybut `repository="registry"` i określ nazwę klucza rejestru w `keyName` atrybucie.</span><span class="sxs-lookup"><span data-stu-id="24eda-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="24eda-159">Jeśli pakiety są wstępnie rozpakowane, użyj `isPreunzipped="true"` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="24eda-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="24eda-160">*(NuGet 3.2 +)* Jeśli chcesz wymusić kompilację w czasie projektowania na końcu instalacji pakietu, Dodaj `forceDesignTimeBuild="true"` atrybut.</span><span class="sxs-lookup"><span data-stu-id="24eda-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="24eda-161">Jako Optymalizacja należy dodać, `skipAssemblyReferences="true"` ponieważ sam szablon zawiera już niezbędne odwołania.</span><span class="sxs-lookup"><span data-stu-id="24eda-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="24eda-162">Najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="24eda-162">Best Practices</span></span>

1. <span data-ttu-id="24eda-163">Zadeklaruj zależność w VSIX NuGet, dodając odwołanie do niego w manifeście VSIX:</span><span class="sxs-lookup"><span data-stu-id="24eda-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="24eda-164">Wymagaj zapisania szablonów projektu/elementu przy tworzeniu przez uwzględnienie [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) w `.vstemplate` pliku.</span><span class="sxs-lookup"><span data-stu-id="24eda-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="24eda-165">Szablony nie zawierają `packages.config` pliku ani nie obejmują ani nie dodawaj żadnych odwołań ani zawartości, które zostałyby dodane po zainstalowaniu pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="24eda-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
