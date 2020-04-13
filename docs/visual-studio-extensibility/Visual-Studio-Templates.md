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
# <a name="packages-in-visual-studio-templates"></a>Pakiety w szablonach programu Visual Studio

Szablony projektów i elementów programu Visual Studio często muszą upewnić się, że niektóre pakiety są instalowane podczas tworzenia projektu lub elementu. Na przykład szablon ASP.NET MVC 3 instaluje jQuery, Modernizr i inne pakiety.

Aby to poprzeć, autorzy szablonów mogą poinstruować NuGet, aby zainstalował niezbędne pakiety, a nie poszczególne biblioteki. Deweloperzy mogą następnie łatwo zaktualizować te pakiety w dowolnym późniejszym czasie.

Aby dowiedzieć się więcej o samodzielnym tworzeniu szablonów, zobacz [Jak: Tworzenie szablonów projektów](/visualstudio/ide/how-to-create-project-templates) lub [Tworzenie szablonów projektów niestandardowych i elementów](/visualstudio/extensibility/creating-custom-project-and-item-templates).

W dalszej części tej sekcji opisano konkretne kroki, które należy wykonać podczas tworzenia szablonu, aby poprawnie dołączyć pakiety NuGet.

- [Dodawanie pakietów do szablonu](#adding-packages-to-a-template)
- [Najlepsze rozwiązania](#best-practices)

Na przykład zobacz [przykład NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Dodawanie pakietów do szablonu

Po wystąpieniu szablonu jest wywoływany [kreator szablonów,](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) aby załadować listę pakietów do zainstalowania wraz z informacjami o tym, gdzie można znaleźć te pakiety. Pakiety mogą być osadzone w vsix, osadzone w szablonie lub znajduje się na lokalnym dysku twardym, w którym to przypadku można użyć klucza rejestru, aby odwołać się do ścieżki pliku. Szczegółowe informacje na temat tych lokalizacji podano w dalszej części tej sekcji.

Preinstalowane pakiety działają przy użyciu [kreatorów szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Specjalny kreator jest wywoływany, gdy szablon zostanie s wystąpieniowy. Kreator ładuje listę pakietów, które muszą być zainstalowane i przekazuje te informacje do odpowiednich interfejsów API NuGet.

Kroki dołączania pakietów do szablonu:

1. W `vstemplate` pliku dodaj odwołanie do kreatora szablonu [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) NuGet, dodając element:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll`jest zestawem, który `TemplateWizard` zawiera tylko klasę, która jest prostym otokiem, który wywołuje rzeczywistą implementację w . `NuGet.VisualStudio.dll` Wersja zestawu nigdy nie zmieni się tak, że szablony projektu/elementu nadal pracować z nowymi wersjami NuGet.

1. Dodaj listę pakietów do zainstalowania w projekcie:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Kreator obsługuje `<package>` wiele elementów do obsługi wielu źródeł pakietów. Wymagane `id` są `version` atrybuty i atrybuty, co oznacza, że zostanie zainstalowana określona wersja pakietu, nawet jeśli dostępna jest nowsza wersja. Zapobiega to aktualizacji pakietu z łamanie szablonu, pozostawiając możliwość aktualizacji pakietu do dewelopera przy użyciu szablonu.

1. Określ repozytorium, w którym NuGet można znaleźć pakiety zgodnie z opisem w poniższych sekcjach.

### <a name="vsix-package-repository"></a>Repozytorium pakietów VSIX

Zalecane podejście wdrażania dla szablonów projektu/elementu programu Visual Studio jest [rozszerzeniem VSIX,](/visualstudio/extensibility/shipping-visual-studio-extensions) ponieważ umożliwia spakowanie wielu szablonów projektu/elementu razem i umożliwia deweloperom łatwe odnajdywanie szablonów przy użyciu Menedżera rozszerzeń programu VS lub Galerii programu Visual Studio. Aktualizacje rozszerzenia są również łatwe do wdrożenia przy użyciu [mechanizmu automatycznej aktualizacji programu Visual Studio Extension Manager](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

Sam VSIX może służyć jako źródło pakietów wymaganych przez szablon:

1. Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    Atrybut `repository` określa typ repozytorium, gdy `extension` `repositoryId` jest unikatowym identyfikatorem samego VSIX (Jest to `ID` wartość atrybutu w `vsixmanifest` pliku rozszerzenia, zobacz [Odwołanie do schematu rozszerzenia VSIX 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Umieść `nupkg` pliki w folderze wywoływanym `Packages` w programie VSIX.

1. Dodaj niezbędne pliki `<Asset>` pakietów, jak w `vsixmanifest` pliku (zobacz odwołanie do [schematu rozszerzenia VSIX 2.0):](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Należy zauważyć, że można dostarczyć pakiety w tym samym VSIX jako szablony projektu lub można umieścić je w osobnym VSIX, jeśli ma to większy sens dla scenariusza. Jednak nie odwoływać się do wszystkich VSIX, nad którym nie masz kontroli, ponieważ zmiany w tym rozszerzeniu może spowodować przerwanie szablonu.

### <a name="template-package-repository"></a>Repozytorium pakietów szablonów

Jeśli rozprowadzasz tylko jeden szablon projektu/elementu i nie musisz pakować wielu szablonów razem, możesz użyć prostszego, ale bardziej ograniczonego podejścia, które zawiera pakiety bezpośrednio w pliku ZIP szablonu projektu/elementu:

1. Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    Atrybut `repository` ma wartość `template` i `repositoryId` atrybut nie jest wymagane.

1. Umieść pakiety w folderze głównym pliku ZIP szablonu projektu/elementu.

Należy zauważyć, że za pomocą tej metody w VSIX, który zawiera wiele szablonów prowadzi do niepotrzebnego uwędzić, gdy jeden lub więcej pakietów są wspólne dla szablonów. W takich przypadkach należy użyć [VSIX jako repozytorium,](#vsix-package-repository) jak opisano w poprzedniej sekcji.

### <a name="registry-specified-folder-path"></a>Ścieżka folderu określona w rejestrze

Zestawy SDK zainstalowane przy użyciu msi można zainstalować pakiety NuGet bezpośrednio na komputerze dewelopera. Dzięki temu natychmiast dostępne, gdy używany jest szablon projektu lub elementu, zamiast wyodrębnić je w tym czasie. ASP.NET szablony używają tego podejścia.

1. Zamieść pakiety instalacyjne MSI na komputerze. Można zainstalować tylko `.nupkg` pliki lub można je zainstalować wraz z rozwiniętą zawartością, co pozwala zaoszczędzić dodatkowy krok, gdy szablon jest używany. W takim przypadku należy postępować zgodnie ze standardową strukturą folderów NuGet, w której `.nupkg` pliki znajdują się w folderze głównym, a następnie każdy pakiet ma podfolder z parą identyfikator/wersja jako nazwę podfolderu.

1. Napisz klucz rejestru, aby zidentyfikować lokalizację pakietu:

    - Kluczowa lokalizacja: szablony i `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` pakiety zainstalowane na całym komputerze lub na użytkownika, alternatywnie`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Nazwa klucza: użyj nazwy, która jest dla Ciebie unikatowa. Na przykład ASP.NET szablonów MVC 4 dla vs 2012 używać `AspNetMvc4VS11`.
    - Wartości: pełna ścieżka do folderu pakietów.

1. W `<packages>` elemencie w `.vstemplate` pliku `repository="registry"` dodaj atrybut i określ `keyName` nazwę klucza rejestru w atrybucie.

    - Jeśli wstępnie rozpakowałeś pakiety, użyj `isPreunzipped="true"` tego atrybutu.
    - *(NuGet 3.2+)* Jeśli chcesz wymusić kompilację czasu projektowania na końcu `forceDesignTimeBuild="true"` instalacji pakietu, dodaj atrybut.
    - Jako optymalizację `skipAssemblyReferences="true"` dodaj, ponieważ sam szablon zawiera już niezbędne odwołania.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Najlepsze rozwiązania

1. Zadeklaruj zależność od NuGet VSIX, dodając odwołanie do niej w manifeście VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Wymagaj, aby szablony projektu/elementu [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) były `.vstemplate` zapisywane podczas tworzenia, dołączając do niego plik.

1. Szablony nie zawierają `packages.config` pliku i nie zawierają żadnych odwołań ani zawartości, które zostaną dodane po zainstalowaniu pakietów NuGet.
