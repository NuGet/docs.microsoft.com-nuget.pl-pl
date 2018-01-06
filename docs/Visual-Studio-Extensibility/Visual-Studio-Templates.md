---
title: Pakiety NuGet w szablony Visual Studio | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/3/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Instrukcje dotyczące tym pakiety NuGet jako część programu Visual Studio szablonów projektów i elementów."
keywords: "NuGet w Visual Studio, szablony projektu Visual Studio, szablony elementów Visual Studio, pakiety w szablonach projektu, pakiety w szablonach elementów"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 45a2ca2c08660be650f9cf38301f628923e1f8be
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="packages-in-visual-studio-templates"></a>Pakiety w szablony programu Visual Studio

Szablony Visual Studio projektu i elementu często konieczne jest zainstalowanie niektórych pakietów podczas tworzenia projektów lub elementów. Na przykład szablonu platformy ASP.NET MVC 3 instaluje jQuery, Modernizr i inne pakiety.

W tym autorom można nakazać NuGet w celu zainstalowania wymaganych pakietów, a nie poszczególnych bibliotek. Deweloperzy i uaktualnić tych pakietów w dowolnym momencie nowsze.

Aby dowiedzieć się więcej na temat tworzenia szablony, zapoznaj się [porady: Tworzenie szablonów projektów](/visualstudio/ide/how-to-create-project-templates) lub [Tworzenie niestandardowych Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).

W pozostałej części tej sekcji opisano procedury określonych w sytuacji, gdy tworzony jest szablon uwzględnienie poprawnie pakietów NuGet.

- [Dodawanie pakietów do szablonu](#adding-packages-to-a-template)
- [Najlepsze praktyki](#best-practices)

Na przykład zobacz [próbki NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Dodawanie pakietów do szablonu

Podczas tworzenia wystąpienia klasy szablonu [Kreatora szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) jest wywoływane w celu załadowania listy pakietów do zainstalowania wraz z informacjami o tym, gdzie można znaleźć tych pakietów. Pakietów można być osadzone w pliku VSIX, osadzone w szablonie lub znajduje się na lokalnym dysku twardym w takim przypadku odwołać się do ścieżki pliku za pomocą klucza rejestru. Szczegółowe informacje o tych lokalizacji podane są później w tej sekcji.

Preinstalowane pakiety pracę za pomocą [kreatorów szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Specjalne Kreator pobiera wywoływane, gdy pobiera wystąpienia szablonu. Kreator ładuje listę pakietów, które muszą być zainstalowane i przekazuje informację do odpowiednich interfejsów API NuGet.

Kroki pakiety mają być dołączane w szablonie:

1. W Twojej `vstemplate` plików, Dodaj odwołanie do Kreatora szablonów NuGet przez dodanie [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elementu:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll`jest zestaw, który zawiera tylko `TemplateWizard` klasy, która jest proste otoki, który odwołuje się do rzeczywistego wykonania w `NuGet.VisualStudio.dll`. Wersja zestawu nigdy nie zmieni się tak, aby kontynuować pracę z nowymi wersjami programu NuGet szablonów projektu/elementu.

1. Dodaj listę pakietów, aby zainstalować w projekcie:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    *(NuGet 2.2.1+)*  Kreator obsługuje wielu `<package>` elementy do obsługi wielu źródeł pakietów. Zarówno `id` i `version` atrybuty są wymagane, co oznacza, że określonej wersji pakietu zostanie zainstalowany, nawet jeśli jest dostępna nowsza wersja. Zapobiega to fundamentalne szablonu, pozostawiając wyboru do zaktualizowania pakietu do deweloperów za pomocą szablonu pakietu aktualizacji.

1. Określ repozytorium, gdzie NuGet można znaleźć pakiety, zgodnie z opisem w poniższych sekcjach.

### <a name="vsix-package-repository"></a>Repozytorium pakietu VSIX

Podejście zalecane wdrożenie szablonów projektu/elementu programu Visual Studio jest [rozszerzenia VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) ponieważ umożliwia pakietu ze sobą kilka szablonów projektu/elementu i umożliwia deweloperom łatwe odnajdowanie szablonów za pomocą Menedżera rozszerzenia programu VS lub galerii programu Visual Studio. Aktualizacje z rozszerzeniem są także łatwo wdrażać przy użyciu [mechanizmu aktualizacji automatycznych Menedżera rozszerzeń programu Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

Samego pliku VSIX może służyć jako źródło dla pakietów wymagane przez szablon:

1. Modyfikowanie `<packages>` element `.vstemplate` plików w następujący sposób:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` Atrybut określa typ z repozytorium jako `extension` podczas `repositoryId` jest unikatowym identyfikatorem VSIX, sama (jest to wartość `ID` atrybut do rozszerzenia `vsixmanifest` plików, zobacz [ Odwołanie do schematu 2.0 rozszerzenia VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Miejsce Twojego `nupkg` pliki w folderze o nazwie `Packages` w pliku VSIX.

1. Dodaj pliki potrzebny pakiet jako `<Asset>` w Twojej `vsixmanifest` pliku (zobacz [odwołania 2.0 schematu rozszerzenia VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Zauważ, że może dostarczać pakietów w tym samym pliku VSIX jako szablonów projektu lub można umieścić je w osobnym pliku VSIX jeśli ma to sens więcej dla danego scenariusza. Jednak nie odwołuj się do żadnych VSIX, w którym nie ma kontroli, ponieważ zmiany tego rozszerzenia może spowodować przerwanie szablonu.

### <a name="template-package-repository"></a>Repozytorium pakietów szablonu

Jeśli jest dystrybuowany szablon pojedynczego projektu/elementu i nie trzeba pakietu wielu szablonów jednocześnie, można użyć prostszą, ale bardziej ograniczone podejście, które zawiera pakiety bezpośrednio w pliku ZIP szablonu projektu/elementu:

1. Modyfikowanie `<packages>` element `.vstemplate` plików w następujący sposób:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` Atrybut ma wartość `template` i `repositoryId` atrybut nie jest wymagana.

1. Umieść pakiety w folderze głównym pliku ZIP szablonu projektu/elementu.

Należy pamiętać, że przy użyciu tej metody w pliku VSIX, który zawiera wiele szablonów prowadzi do niepotrzebnych rozrostu, gdy jeden lub więcej pakietów są wspólne dla szablonów. W takiej sytuacji należy użyć [VSIX jako repozytorium](#vsix-package-repository) zgodnie z opisem w poprzedniej sekcji.

### <a name="registry-specified-folder-path"></a>Ścieżka folderu określona w rejestrze

Zestawy SDK, które są instalowane za pomocą Instalatora MSI można zainstalować pakietów NuGet bezpośrednio na komputerze dewelopera. To sprawia, że ich natychmiast dostępna, gdy szablon projektu lub elementu jest używany, zamiast wyodrębnić je w tym samym czasie. Szablony ASP.NET posłuż się tą metodą.

1. Ma MSI zainstalować pakiety do komputera. Można zainstalować tylko `.nupkg` pliki, lub zainstalować te, wraz z rozwiniętym zawartość, który zapisuje dodatkowych czynności, kiedy szablon jest używany. W takim przypadku którym wykonaj struktury folderów standardowe NuGet `.nupkg` plików w folderze głównym, a następnie każdy pakiet ma podfolder o pary identyfikator/version jako nazwa podfolderu.

1. Zapisu klucza rejestru, aby określić lokalizację pakietu:

    - Lokalizacji klucza: albo dla komputera `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` lub jeśli jest zainstalowana na użytkownika szablonów i pakietów, można również użyć`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Nazwa klucza: Użyj nazwy, która jest unikatowa dla Ciebie. Na przykład szablony ASP.NET MVC 4 VS 2012 używają `AspNetMvc4VS11`.
    - Wartości: Pełna ścieżka do folderu pakietów.

1. W `<packages>` element `.vstemplate` plików, Dodaj atrybut `repository="registry"` i określ nazwę klucza rejestru w `keyName` atrybutu.

    - Jeśli zostały wstępnie unzipped pakietów, użyj `isPreunzipped="true"` atrybutu.
    - *(NuGet 3.2 +)*  Jeśli chcesz wymusić kompilację czasu projektowania na końcu instalacji pakietu, Dodaj `forceDesignTimeBuild="true"` atrybutu.
    - Do optymalizacji dodać `skipAssemblyReferences="true"` ponieważ samego szablonu zawiera już niezbędne odwołania.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Najlepsze praktyki

1. Dodanie odwołania do niego w manifeście VSIX zadeklarować zależność NuGet VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Wymagaj szablonów projektu/elementu można zapisać przy tworzeniu, umieszczając w niej [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) w `.vstemplate` pliku.

1. Szablony nie zawierają `packages.config` lub `project.json` pliku, a nie dołączaj lub żadnych odwołań do zawartości lub zostanie dodany podczas instalowania pakietów NuGet.
