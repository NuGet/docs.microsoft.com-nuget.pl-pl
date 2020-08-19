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
# <a name="packages-in-visual-studio-templates"></a>Pakiety w szablonach programu Visual Studio

Szablony projektów i elementów programu Visual Studio często muszą mieć pewność, że niektóre pakiety są instalowane podczas tworzenia projektu lub elementu. Na przykład szablon ASP.NET MVC 3 instaluje jQuery, modernizację i inne pakiety.

Aby to umożliwić, autorzy szablonów mogą wydać pakietowi NuGet zainstalowanie wymaganych pakietów zamiast poszczególnych bibliotek. Deweloperzy mogą następnie łatwo aktualizować te pakiety w dowolnym późniejszym czasie.

Aby dowiedzieć się więcej na temat tworzenia szablonów, zobacz [jak: Tworzenie szablonów projektu](/visualstudio/ide/how-to-create-project-templates) lub [Tworzenie niestandardowych szablonów projektów i elementów](/visualstudio/extensibility/creating-custom-project-and-item-templates).

W pozostałej części tej sekcji opisano czynności, które należy wykonać podczas tworzenia szablonu w celu poprawnego uwzględnienia pakietów NuGet.

- [Dodawanie pakietów do szablonu](#adding-packages-to-a-template)
- [Najlepsze praktyki](#best-practices)

Aby zapoznać się z przykładem, zobacz [NuGetInVsTemplates Sample](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Dodawanie pakietów do szablonu

Po utworzeniu wystąpienia szablonu [Kreator szablonu](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) jest wywoływany w celu załadowania listy pakietów do zainstalowania wraz z informacjami o miejscu, w którym można znaleźć te pakiety. Pakiety mogą być osadzone w VSIX, osadzone w szablonie lub znajdować się na lokalnym dysku twardym, w którym należy użyć klucza rejestru do odwoływania się do ścieżki pliku. Szczegółowe informacje o tych lokalizacjach znajdują się w dalszej części tej sekcji.

Wstępnie zainstalowane pakiety działają przy użyciu [kreatorów szablonów](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Po utworzeniu wystąpienia szablonu zostanie wywołany specjalny Kreator. Kreator ładuje listę pakietów, które muszą być zainstalowane, i przekazuje te informacje do odpowiednich interfejsów API NuGet.

Procedura dołączania pakietów do szablonu:

1. W `vstemplate` pliku Dodaj odwołanie do Kreatora szablonu NuGet poprzez dodanie [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elementu:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` jest zestawem zawierającym tylko `TemplateWizard` klasę, która jest prostym otoką, która wywołuje rzeczywistą implementację w `NuGet.VisualStudio.dll` . Wersja zestawu nigdy nie ulegnie zmianie, tak aby szablony projektów i elementów nadal działały z nowymi wersjami programu NuGet.

1. Dodaj listę pakietów do zainstalowania w projekcie:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Kreator obsługuje wiele `<package>` elementów do obsługi wielu źródeł pakietów. Oba `id` atrybuty i `version` są wymagane, co oznacza, że określona wersja pakietu zostanie zainstalowana, nawet jeśli jest dostępna nowsza wersja. Zapobiega to przerywaniu szablonu przez aktualizacje pakietów, pozostawiając wybór w celu zaktualizowania pakietu do dewelopera przy użyciu szablonu.

1. Określ repozytorium, w którym narzędzia NuGet mogą znaleźć pakiety zgodnie z opisem w poniższych sekcjach.

### <a name="vsix-package-repository"></a>Repozytorium pakietu VSIX

Zalecanym podejściem do wdrażania szablonów projektów/elementów programu Visual Studio jest [rozszerzenie VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) , ponieważ umożliwia ono spakowanie wielu szablonów projektów/elementów i umożliwia deweloperom łatwe odnajdywanie szablonów przy użyciu Menedżera rozszerzenia programu vs lub Galerii programu Visual Studio. Aktualizacje rozszerzenia można również łatwo wdrożyć przy użyciu [mechanizmu aktualizacji automatycznych programu Visual Studio Extension Manager](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

Sam VSIX może stanowić źródło pakietów wymaganych przez szablon:

1. Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    Ten `repository` atrybut określa typ repozytorium, tak jak `extension` while `repositoryId` jest unikatowym identyfikatorem VSIX (jest to wartość `ID` atrybutu w `vsixmanifest` pliku rozszerzenia, zobacz [Dokumentacja schematu rozszerzenia VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Umieść `nupkg` pliki w folderze o nazwie w `Packages` VSIX.

1. Dodaj niezbędne pliki pakietu jako `<Asset>` `vsixmanifest` plik (zobacz [odwołanie do schematu rozszerzenia VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Należy pamiętać, że możesz dostarczać pakiety w tym samym VSIX co szablony projektu lub umieścić je w oddzielnym VSIX, jeśli ma to sens dla scenariusza. Jednakże nie należy odwoływać się do żadnego VSIX, nad którym nie masz kontroli, ponieważ zmiany w tym rozszerzeniu mogłyby spowodować uszkodzenie szablonu.

### <a name="template-package-repository"></a>Repozytorium pakietu szablonów

Jeśli dystrybuowany jest tylko jeden szablon projektu/elementu i nie ma potrzeby jednoczesnego pakowania wielu szablonów, można użyć prostszego, ale bardziej ograniczonego podejścia zawierającego pakiety bezpośrednio w pliku ZIP szablonu/elementu.

1. Zmodyfikuj `<packages>` element w pliku w `.vstemplate` następujący sposób:

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    `repository`Atrybut ma wartość `template` i `repositoryId` atrybut nie jest wymagany.

1. Umieść pakiety w folderze głównym pliku ZIP szablonu/elementu.

Należy zauważyć, że użycie tej metody w VSIX, która zawiera wiele szablonów, prowadzi do niepotrzebnych przeładowanie, gdy jeden lub więcej pakietów jest wspólnych dla szablonów. W takich przypadkach należy użyć [VSIX jako repozytorium](#vsix-package-repository) , zgodnie z opisem w poprzedniej sekcji.

### <a name="registry-specified-folder-path"></a>Ścieżka folderu określona w rejestrze

Zestawy SDK, które są instalowane przy użyciu pliku MSI, mogą instalować pakiety NuGet bezpośrednio na komputerze dewelopera. Dzięki temu są one natychmiast dostępne, gdy zostanie użyty szablon projektu lub elementu, a nie trzeba go wyodrębnić w tym czasie. Użycie tego podejścia przez szablony ASP.NET.

1. Zainstaluj pakiety MSI na komputerze. Można zainstalować tylko `.nupkg` pliki lub zainstalować je wraz z rozwiniętą zawartością, co spowoduje zaoszczędzenie dodatkowego kroku, gdy szablon jest używany. W takim przypadku należy przestrzegać standardowej struktury folderów programu NuGet `.nupkg` , w której pliki znajdują się w folderze głównym, a następnie każdy pakiet ma podfolder z parą ID/Version jako nazwę podfolderu.

1. Napisz klucz rejestru, aby zidentyfikować lokalizację pakietu:

    - Lokalizacja klucza: dla całej maszyny lub w `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` przypadku szablonów i pakietów zainstalowanych dla poszczególnych użytkowników, Alternatywnie użyj `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Nazwa klucza: Użyj nazwy, która jest unikatowa dla użytkownika. Przykładowo Użyj szablonów ASP.NET MVC 4 dla programu VS 2012 `AspNetMvc4VS11` .
    - Wartości: pełna ścieżka do folderu Packages.

1. W `<packages>` elemencie w `.vstemplate` pliku, Dodaj atrybut `repository="registry"` i określ nazwę klucza rejestru w `keyName` atrybucie.

    - Jeśli pakiety są wstępnie rozpakowane, użyj `isPreunzipped="true"` atrybutu.
    - *(NuGet 3.2 +)* Jeśli chcesz wymusić kompilację w czasie projektowania na końcu instalacji pakietu, Dodaj `forceDesignTimeBuild="true"` atrybut.
    - Jako Optymalizacja należy dodać, `skipAssemblyReferences="true"` ponieważ sam szablon zawiera już niezbędne odwołania.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Najlepsze rozwiązania

1. Zadeklaruj zależność w VSIX NuGet, dodając odwołanie do niego w manifeście VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Wymagaj zapisania szablonów projektu/elementu przy tworzeniu przez uwzględnienie [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) w `.vstemplate` pliku.

1. Szablony nie zawierają `packages.config` pliku ani nie obejmują ani nie dodawaj żadnych odwołań ani zawartości, które zostałyby dodane po zainstalowaniu pakietów NuGet.
