---
title: Pakiety NuGet w szablonach programu Visual Studio
description: Instrukcje w tym pakietów NuGet jako część programu Visual Studio szablonów projektów i elementów.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550513"
---
# <a name="packages-in-visual-studio-templates"></a>Pakiety szablonów programu Visual Studio

Szablony Visual Studio projektów i elementów często zachodzi potrzeba upewnij się, że niektóre pakiety są instalowane po utworzeniu projektu lub elementu. Na przykład szablonu platformy ASP.NET MVC 3 instaluje, jQuery, Modernizr i innych pakietów.

Aby to umożliwić, autorzy szablonów można nakazać pakietu NuGet, aby zainstalować wymagane pakiety, a nie poszczególnych bibliotekach. Deweloperzy następnie można łatwo zaktualizować te pakiety w dowolnym momencie nowsze.

Aby dowiedzieć się więcej na temat tworzenia szablonów, zobacz [porady: Tworzenie szablonów projektów](/visualstudio/ide/how-to-create-project-templates) lub [Tworzenie niestandardowych szablonów projektów i elementów](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Dalszej części tej sekcji opisano konkretne czynności umożliwiające podczas tworzenia szablonu prawidłowo uwzględnić następujące pakiety NuGet.

- [Trwa dodawanie pakietów do szablonu](#adding-packages-to-a-template)
- [Najlepsze rozwiązania](#best-practices)

Aby uzyskać przykład, zobacz [przykładowe NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Trwa dodawanie pakietów do szablonu

Podczas tworzenia wystąpienia szablonu [Kreatora szablonu](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) wywoływana w celu załadowania listy pakiety do zainstalowania, wraz z informacjami o tym, gdzie można znaleźć te pakiety. Pakiety mogą być osadzone w pliku VSIX, osadzonego w szablonie lub znajdujący się na lokalnym dysku twardym w którym to przypadku odwoływać się do ścieżki pliku za pomocą klucza rejestru. Szczegółowe informacje na temat te lokalizacje są podane w dalszej części w tej sekcji.

Przy pracy z wstępnie zainstalowane pakiety [kreatorów szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Specjalne Kreator pobiera wywoływane, gdy pobiera wystąpienia szablonu. Kreator ładuje listę pakietów, które muszą być zainstalowane i przekazuje informację do odpowiedniego interfejsów API NuGet.

Kroki, aby uwzględnić następujące pakiety w szablonie:

1. W swojej `vstemplate` Dodaj odwołanie do Kreatora szablonu NuGet, dodając [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elementu:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` to zestaw, który zawiera tylko `TemplateWizard` klasy, która jest proste otoki, która wywołuje rzeczywistą implementację w `NuGet.VisualStudio.dll`. Wersja zestawu nigdy nie zmieni się tak, aby kontynuować pracę z nowej wersji pakietu nuget szablonów projektu/elementu.

1. Dodaj listę pakietów do zainstalowania w projekcie:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Kreator obsługuje wiele `<package>` elementy, które obsługują wielu źródeł pakietów. Zarówno `id` i `version` atrybuty są wymagane, co oznacza, że określonej wersji pakietu zostanie zainstalowany, nawet jeśli jest dostępna nowsza wersja. Zapobiega to przerwanie szablonu, pozostawiając wybraną do zaktualizowania pakietu do deweloperów za pomocą szablonu pakietu aktualizacji.

1. Określ repozytorium, gdzie NuGet można znaleźć pakiety, zgodnie z opisem w poniższych sekcjach.

### <a name="vsix-package-repository"></a>Repozytorium pakietów VSIX

Podejście zalecane wdrożenie dla szablonów projektu/elementu programu Visual Studio jest [rozszerzenia VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) ponieważ umożliwia pakietu ze sobą wiele szablonów projektu/elementu i umożliwia deweloperom łatwe odnajdowanie szablonów Korzystanie z Menedżera rozszerzeń programu VS lub galerii Visual Studio. Aktualizacje rozszerzenia również są łatwe do wdrożenia przy użyciu [mechanizmu aktualizacji automatycznych Menedżera rozszerzeń programu Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

Samego VSIX może służyć jako źródło dla pakietów wymaganych przez szablon:

1. Modyfikowanie `<packages>` element `.vstemplate` pliku w następujący sposób:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` Atrybut określa typ repozytorium jako `extension` podczas `repositoryId` to unikatowy identyfikator VSIX, sama (jest to wartość `ID` atrybutu do rozszerzenia `vsixmanifest` plików, zobacz [ Odwołanie do schematu 2.0 rozszerzenia VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Umieść swoje `nupkg` pliki w folderze o nazwie `Packages` w pliku VSIX.

1. Dodaj pliki potrzebny pakiet jako `<Asset>` w swojej `vsixmanifest` pliku (zobacz [VSIX rozszerzenia schematu 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Należy pamiętać, że możesz dostarczyć pakietów w samym VSIX jako szablony projektu lub można je umieścić w oddzielnych VSIX, jeśli ma to sens więcej dla danego scenariusza. Jednak nie odwołuj się do dowolnej VSIX nad tym, którzy nie mają kontrolę, ponieważ zmiany do tego rozszerzenia może spowodować przerwanie szablonu.

### <a name="template-package-repository"></a>Repozytorium pakietów szablonu

Jeśli jest dystrybuowany szablon pojedynczego projektu/elementu i nie powinny być pakietu ze sobą wiele szablonów, można skorzystać z podejścia prostsze, ale bardziej ograniczone, zawierający pakiety bezpośrednio w pliku ZIP szablonu projektu/elementu:

1. Modyfikowanie `<packages>` element `.vstemplate` pliku w następujący sposób:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` Atrybut ma wartość `template` i `repositoryId` atrybut nie jest wymagana.

1. Umieść pakiety w folderze głównym pliku ZIP szablonu projektu/elementu.

Należy pamiętać o tym, czy użycie tej metody w VSIX, który zawiera wiele szablonów prowadzi do rozrostu niepotrzebne, gdy jeden lub więcej pakietów są wspólne dla szablonów. W takiej sytuacji należy użyć [VSIX jako repozytorium](#vsix-package-repository) zgodnie z opisem w poprzedniej sekcji.

### <a name="registry-specified-folder-path"></a>Ścieżka do folderu określonego w rejestrze

Zestawy SDK, które są instalowane za pomocą Instalatora MSI można zainstalować pakietów NuGet bezpośrednio na komputerze dewelopera. To sprawia, że ich od razu dostępna, gdy szablon projektu lub elementu jest używana zamiast konieczności wyodrębnić je w tym samym czasie. Szablony ASP.NET używają tej metody.

1. Mieć MSI zainstalować pakiety do maszyny. Można zainstalować tylko `.nupkg` plików, lub zainstalować te, wraz z rozwiniętej zawartości, co pozwala na zaoszczędzenie dodatkowy krok, gdy szablon jest używany. W takim przypadku postępuj zgodnie z strukturę folderów standardowa NuGet polegającego `.nupkg` pliki znajdują się w folderze głównym, a następnie każdy pakiet ma podfolder o par identyfikator/version jako nazwy podfolderu.

1. Napisz klucz rejestru, aby określić lokalizację pakietu:

    - Lokalizacja klucza: albo całej maszyny `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` lub jeśli jest zainstalowana na użytkownika szablonów i pakietów, można również użyć `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Nazwa klucza: Użyj nazwy, która jest unikatowa dla Ciebie. Na przykład szablony platformy ASP.NET MVC 4 dla programu VS 2012 używają `AspNetMvc4VS11`.
    - Wartości: Pełna ścieżka do folderu pakietów.

1. W `<packages>` element `.vstemplate` plików, Dodaj atrybut `repository="registry"` i określ nazwę klucza rejestru w `keyName` atrybutu.

    - Jeśli masz wstępnie rozpakowano pakietów, użyj `isPreunzipped="true"` atrybutu.
    - *(NuGet 3.2 +)*  Jeśli chcesz wymusić kompilacji czasu projektowania na końcu instalacji pakietu aktualizacji, należy dodać `forceDesignTimeBuild="true"` atrybutu.
    - Optymalizacja dodanie `skipAssemblyReferences="true"` ponieważ samego szablonu zawiera już niezbędne odwołania.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Najlepsze praktyki

1. Należy zadeklarować zależność w NuGet VSIX, dodając odwołanie do niej w manifeście VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Wymagane szablony projektu/elementu mają być zapisane na tworzenie, umieszczając [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) w `.vstemplate` pliku.

1. Szablony nie obejmują `packages.config` pliku i nie obejmują lub odwołania do dowolnej zawartości, która zostanie dodany po zainstalowaniu pakietów NuGet.
