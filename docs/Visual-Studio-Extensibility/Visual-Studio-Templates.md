---
title: Pakiety NuGet w szablony Visual Studio | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/03/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Instrukcje dotyczące tym pakiety NuGet jako część programu Visual Studio szablonów projektów i elementów.
keywords: NuGet w Visual Studio, szablony projektu Visual Studio, szablony elementów Visual Studio, pakiety w szablonach projektu, pakiety w szablonach elementów
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 8c1751ba9caf5e71ace7a81575e4e5448b1e4185
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="a4e14-104">Pakiety w szablony programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a4e14-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="a4e14-105">Szablony Visual Studio projektu i elementu często konieczne jest zainstalowanie niektórych pakietów podczas tworzenia projektów lub elementów.</span><span class="sxs-lookup"><span data-stu-id="a4e14-105">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="a4e14-106">Na przykład szablonu platformy ASP.NET MVC 3 instaluje jQuery, Modernizr i inne pakiety.</span><span class="sxs-lookup"><span data-stu-id="a4e14-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="a4e14-107">W tym autorom można nakazać NuGet w celu zainstalowania wymaganych pakietów, a nie poszczególnych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="a4e14-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="a4e14-108">Deweloperzy i uaktualnić tych pakietów w dowolnym momencie nowsze.</span><span class="sxs-lookup"><span data-stu-id="a4e14-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="a4e14-109">Aby dowiedzieć się więcej na temat tworzenia szablony, zapoznaj się [porady: Tworzenie szablonów projektów](/visualstudio/ide/how-to-create-project-templates) lub [Tworzenie niestandardowych Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="a4e14-109">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="a4e14-110">W pozostałej części tej sekcji opisano procedury określonych w sytuacji, gdy tworzony jest szablon uwzględnienie poprawnie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="a4e14-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="a4e14-111">Dodawanie pakietów do szablonu</span><span class="sxs-lookup"><span data-stu-id="a4e14-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="a4e14-112">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="a4e14-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="a4e14-113">Na przykład zobacz [próbki NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="a4e14-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="a4e14-114">Dodawanie pakietów do szablonu</span><span class="sxs-lookup"><span data-stu-id="a4e14-114">Adding packages to a template</span></span>

<span data-ttu-id="a4e14-115">Podczas tworzenia wystąpienia klasy szablonu [Kreatora szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) jest wywoływane w celu załadowania listy pakietów do zainstalowania wraz z informacjami o tym, gdzie można znaleźć tych pakietów.</span><span class="sxs-lookup"><span data-stu-id="a4e14-115">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="a4e14-116">Pakietów można być osadzone w pliku VSIX, osadzone w szablonie lub znajduje się na lokalnym dysku twardym w takim przypadku odwołać się do ścieżki pliku za pomocą klucza rejestru.</span><span class="sxs-lookup"><span data-stu-id="a4e14-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="a4e14-117">Szczegółowe informacje o tych lokalizacji podane są później w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4e14-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="a4e14-118">Preinstalowane pakiety pracę za pomocą [kreatorów szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="a4e14-118">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="a4e14-119">Specjalne Kreator pobiera wywoływane, gdy pobiera wystąpienia szablonu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="a4e14-120">Kreator ładuje listę pakietów, które muszą być zainstalowane i przekazuje informację do odpowiednich interfejsów API NuGet.</span><span class="sxs-lookup"><span data-stu-id="a4e14-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="a4e14-121">Kroki pakiety mają być dołączane w szablonie:</span><span class="sxs-lookup"><span data-stu-id="a4e14-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="a4e14-122">W Twojej `vstemplate` plików, Dodaj odwołanie do Kreatora szablonów NuGet przez dodanie [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elementu:</span><span class="sxs-lookup"><span data-stu-id="a4e14-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="a4e14-123">`NuGet.VisualStudio.Interop.dll` jest zestaw, który zawiera tylko `TemplateWizard` klasy, która jest proste otoki, który odwołuje się do rzeczywistego wykonania w `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="a4e14-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="a4e14-124">Wersja zestawu nigdy nie zmieni się tak, aby kontynuować pracę z nowymi wersjami programu NuGet szablonów projektu/elementu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="a4e14-125">Dodaj listę pakietów, aby zainstalować w projekcie:</span><span class="sxs-lookup"><span data-stu-id="a4e14-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="a4e14-126">Kreator obsługuje wielu `<package>` elementy do obsługi wielu źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="a4e14-126">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="a4e14-127">Zarówno `id` i `version` atrybuty są wymagane, co oznacza, że określonej wersji pakietu zostanie zainstalowany, nawet jeśli jest dostępna nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="a4e14-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="a4e14-128">Zapobiega to fundamentalne szablonu, pozostawiając wyboru do zaktualizowania pakietu do deweloperów za pomocą szablonu pakietu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="a4e14-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="a4e14-129">Określ repozytorium, gdzie NuGet można znaleźć pakiety, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="a4e14-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="a4e14-130">Repozytorium pakietu VSIX</span><span class="sxs-lookup"><span data-stu-id="a4e14-130">VSIX package repository</span></span>

<span data-ttu-id="a4e14-131">Podejście zalecane wdrożenie szablonów projektu/elementu programu Visual Studio jest [rozszerzenia VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) ponieważ umożliwia pakietu ze sobą kilka szablonów projektu/elementu i umożliwia deweloperom łatwe odnajdowanie szablonów za pomocą Menedżera rozszerzenia programu VS lub galerii programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4e14-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="a4e14-132">Aktualizacje z rozszerzeniem są także łatwo wdrażać przy użyciu [mechanizmu aktualizacji automatycznych Menedżera rozszerzeń programu Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="a4e14-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="a4e14-133">Samego pliku VSIX może służyć jako źródło dla pakietów wymagane przez szablon:</span><span class="sxs-lookup"><span data-stu-id="a4e14-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="a4e14-134">Modyfikowanie `<packages>` element `.vstemplate` plików w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a4e14-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="a4e14-135">`repository` Atrybut określa typ z repozytorium jako `extension` podczas `repositoryId` jest unikatowym identyfikatorem VSIX, sama (jest to wartość `ID` atrybut do rozszerzenia `vsixmanifest` plików, zobacz [ Odwołanie do schematu 2.0 rozszerzenia VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="a4e14-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="a4e14-136">Miejsce Twojego `nupkg` pliki w folderze o nazwie `Packages` w pliku VSIX.</span><span class="sxs-lookup"><span data-stu-id="a4e14-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="a4e14-137">Dodaj pliki potrzebny pakiet jako `<Asset>` w Twojej `vsixmanifest` pliku (zobacz [odwołania 2.0 schematu rozszerzenia VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="a4e14-137">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="a4e14-138">Zauważ, że może dostarczać pakietów w tym samym pliku VSIX jako szablonów projektu lub można umieścić je w osobnym pliku VSIX jeśli ma to sens więcej dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="a4e14-138">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="a4e14-139">Jednak nie odwołuj się do żadnych VSIX, w którym nie ma kontroli, ponieważ zmiany tego rozszerzenia może spowodować przerwanie szablonu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-139">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="a4e14-140">Repozytorium pakietów szablonu</span><span class="sxs-lookup"><span data-stu-id="a4e14-140">Template package repository</span></span>

<span data-ttu-id="a4e14-141">Jeśli jest dystrybuowany szablon pojedynczego projektu/elementu i nie trzeba pakietu wielu szablonów jednocześnie, można użyć prostszą, ale bardziej ograniczone podejście, które zawiera pakiety bezpośrednio w pliku ZIP szablonu projektu/elementu:</span><span class="sxs-lookup"><span data-stu-id="a4e14-141">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="a4e14-142">Modyfikowanie `<packages>` element `.vstemplate` plików w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a4e14-142">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="a4e14-143">`repository` Atrybut ma wartość `template` i `repositoryId` atrybut nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="a4e14-143">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="a4e14-144">Umieść pakiety w folderze głównym pliku ZIP szablonu projektu/elementu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-144">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="a4e14-145">Należy pamiętać, że przy użyciu tej metody w pliku VSIX, który zawiera wiele szablonów prowadzi do niepotrzebnych rozrostu, gdy jeden lub więcej pakietów są wspólne dla szablonów.</span><span class="sxs-lookup"><span data-stu-id="a4e14-145">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="a4e14-146">W takiej sytuacji należy użyć [VSIX jako repozytorium](#vsix-package-repository) zgodnie z opisem w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4e14-146">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="a4e14-147">Ścieżka folderu określona w rejestrze</span><span class="sxs-lookup"><span data-stu-id="a4e14-147">Registry-specified folder path</span></span>

<span data-ttu-id="a4e14-148">Zestawy SDK, które są instalowane za pomocą Instalatora MSI można zainstalować pakietów NuGet bezpośrednio na komputerze dewelopera.</span><span class="sxs-lookup"><span data-stu-id="a4e14-148">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="a4e14-149">To sprawia, że ich natychmiast dostępna, gdy szablon projektu lub elementu jest używany, zamiast wyodrębnić je w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="a4e14-149">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="a4e14-150">Szablony ASP.NET posłuż się tą metodą.</span><span class="sxs-lookup"><span data-stu-id="a4e14-150">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="a4e14-151">Ma MSI zainstalować pakiety do komputera.</span><span class="sxs-lookup"><span data-stu-id="a4e14-151">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="a4e14-152">Można zainstalować tylko `.nupkg` pliki, lub zainstalować te, wraz z rozwiniętym zawartość, który zapisuje dodatkowych czynności, kiedy szablon jest używany.</span><span class="sxs-lookup"><span data-stu-id="a4e14-152">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="a4e14-153">W takim przypadku którym wykonaj struktury folderów standardowe NuGet `.nupkg` plików w folderze głównym, a następnie każdy pakiet ma podfolder o pary identyfikator/version jako nazwa podfolderu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-153">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="a4e14-154">Zapisu klucza rejestru, aby określić lokalizację pakietu:</span><span class="sxs-lookup"><span data-stu-id="a4e14-154">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="a4e14-155">Lokalizacji klucza: albo dla komputera `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` lub jeśli jest zainstalowana na użytkownika szablonów i pakietów, można również użyć `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="a4e14-155">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="a4e14-156">Nazwa klucza: Użyj nazwy, która jest unikatowa dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a4e14-156">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="a4e14-157">Na przykład szablony ASP.NET MVC 4 VS 2012 używają `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="a4e14-157">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="a4e14-158">Wartości: Pełna ścieżka do folderu pakietów.</span><span class="sxs-lookup"><span data-stu-id="a4e14-158">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="a4e14-159">W `<packages>` element `.vstemplate` plików, Dodaj atrybut `repository="registry"` i określ nazwę klucza rejestru w `keyName` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-159">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="a4e14-160">Jeśli zostały wstępnie unzipped pakietów, użyj `isPreunzipped="true"` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-160">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="a4e14-161">*(NuGet 3.2 +)*  Jeśli chcesz wymusić kompilację czasu projektowania na końcu instalacji pakietu, Dodaj `forceDesignTimeBuild="true"` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a4e14-161">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="a4e14-162">Do optymalizacji dodać `skipAssemblyReferences="true"` ponieważ samego szablonu zawiera już niezbędne odwołania.</span><span class="sxs-lookup"><span data-stu-id="a4e14-162">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="a4e14-163">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="a4e14-163">Best Practices</span></span>

1. <span data-ttu-id="a4e14-164">Dodanie odwołania do niego w manifeście VSIX zadeklarować zależność NuGet VSIX:</span><span class="sxs-lookup"><span data-stu-id="a4e14-164">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="a4e14-165">Wymagaj szablonów projektu/elementu można zapisać przy tworzeniu, umieszczając w niej [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) w `.vstemplate` pliku.</span><span class="sxs-lookup"><span data-stu-id="a4e14-165">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="a4e14-166">Szablony nie zawierają `packages.config` pliku, a nie dołączaj lub żadnych odwołań do zawartości lub zostanie dodany podczas instalowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="a4e14-166">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
