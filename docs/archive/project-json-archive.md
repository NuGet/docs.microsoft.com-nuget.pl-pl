---
title: Zawartość archiwum Project. JSON elementu NuGet
description: Różne bity zawartości pliku Project. JSON usunięte z innych obszarów dokumentacji programu NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 87116669c1e685ffd0dbe4142c2f7e357c413497
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488245"
---
# <a name="projectjson-archive"></a>Archiwum Project. JSON

Format `project.json` zarządzania został wprowadzony z pakietem NuGet 3. x i używany dla niektórych typów projektów. Była przestarzała z wprowadzeniem formatu PackageReference, w którym zależności są wyświetlane bezpośrednio w pliku projektu.

Zobacz również:

- [project.json schema](project-json.md)
- [wpływ pliku Project. JSON na autorów pakietów](project-json-impact.md)
- [Plik project.json i platforma UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Format zarządzania project.json

*Pierwotnie w ramach [przywracania pakietu](../what-is-nuget.md).*

Na liście formatów zarządzania:

- [`project.json`](project-json.md): *(przestarzałe)* plik JSON, który przechowuje listę zależności projektu z ogólnym grafem pakietu w skojarzonym pliku `project.lock.json`. Ten format jest przestarzały na korzyść PackageReference.

## <a name="nuget-restore-on-mono"></a>Przywracanie NuGet przy mono

*Pierwotnie [zainstalowane narzędzia klienta NuGet](../install-nuget-client-tools.md).*

Współpracuje z `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Ograniczanie wersji pakietów przy użyciu funkcji przywracania

*Pierwotnie w ramach [przywracania pakietu](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*

- `project.json`: Określ zakres wersji bezpośrednio z numerem wersji zależności. Przykład:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Poleceń interfejsu wiersza polecenia NuGet

- `nuget install`nie działa z `project.json`.
- `nuget restore`: w przypadku projektów `project.json`korzystających z `project.lock.json` programu Program generuje `<project>.nuget.props` plik i plik, w razie konieczności. (Oba pliki można pominąć z kontroli źródła). Argument może wskazywać plik i ma takie samo `packages.config` zachowanie jak wskazanie pliku projektu lub. `project.json` `<projectPath>` W kolejności według priorytetu dla folderów pakietów `%userprofile%\.nuget\packages` program jest wyszukiwany `project.json`jako pierwszy podczas korzystania z programu.
- `nuget update`: W przypadku mono to polecenie nie działa z projektami przy użyciu `project.json`programu.

## <a name="dependency-resolution-with-packagereference"></a>Rozpoznawanie zależności z PackageReference

*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference).*

Zachowanie PackageReference ma zastosowanie również do `project.json`. Funkcja przywracania NuGet zapisuje wykres zależności w pliku o nazwie `project.lock.json` obok `project.json`.

## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#managing-dependency-assets).*

W przypadku korzystania `project.json` z formatu można kontrolować, które zasoby z zależności są przepływem do projektu najwyższego poziomu. Aby uzyskać szczegółowe informacje, zobacz plik [Project. JSON](project-json.md).

## <a name="excluding-references"></a>Wykluczanie odwołań

*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#excluding-references).*

- `project.json`: Dodaj `"exclude" : "all"` w zależności od PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie niezgodnych błędów pakietów

*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).*

Dodano metodę rozwiązywania błędów:

- **Niezalecane**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projekty `netcore`mające znaczenie, `netstandard`i `netcoreapp` mogą wskazywać inne struktury jako zgodne, umożliwiając tym samym stosowanie pakietów docelowych platformy, które mają być używane. Zobacz plik [Project. JSON Imports](project-json.md#imports) i [element docelowy przywracania MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Może to spowodować nieoczekiwane zachowanie, dlatego najlepiej rozwiązać niezgodności pakietów, pracując z autorem pakietu w ramach aktualizacji.

## <a name="target-frameworks"></a>Platformy docelowe

*Początkowo w [strukturach docelowych](../reference/target-frameworks.md).*

- [project.json](project-json.md): `frameworks` Węzeł określa wersje architektury, względem których można skompilować projekt.

## <a name="creating-a-package"></a>Tworzenie pakietu

*Pierwotnie podczas [tworzenia pakietu](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Ustawianie typu pakietu

W przypadku programu .NET Core 1. x po zainstalowaniu pakietu DotnetCliTool program Visual Studio umieszcza pakiet w `project.json` `tools` węźle, a nie `dependencies` w węźle.

Typy pakietów są ustawione w `project.json`.

- `project.json`: Wskaż typ pakietu w pliku `packOptions.packageType` json właściwości:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Dodawanie elementów docelowych i właściwości dla programu MSBuild

*Pierwotnie [twórz .NET standard pakiety NuGet przy użyciu programu Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

W przypadku `project.json`korzystania z obiektów docelowych nie są dodawane do projektu, ale są udostępniane `project.lock.json`za pośrednictwem.

### <a name="package-versioning"></a>Przechowywanie wersji pakietów

*Początkowo w [wersji pakietu](../concepts/package-versioning.md).*

W przypadku korzystania `project.json` z formatu, pakiet NuGet obsługuje również używanie \*notacji wieloznacznej, w przypadku elementów głównych, pomocniczych, poprawek i prefiksu w wersji wstępnej.

### <a name="nugetconfig-reference"></a>Dokumentacja NuGet. config

*Pierwotnie w [dokumentacji NuGet. config](../reference/nuget-config-file.md).*

`globalPackagesFolder`ma zastosowanie tylko `project.json`do. (Dodana Uwaga: dotyczy także PackageReference).

### <a name="nuspec-file-reference"></a>odwołanie do pliku nuspec

*Pierwotnie w [nuspec Reference](../reference/nuspec.md).*

Element jest używany `<files>` zamiast `project.json`. `<contentFiles>`

### <a name="package-manager-options-control"></a>Kontrola opcji Menedżera pakietów

*Pierwotnie w [dokumentacji interfejsu użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md).*

Projekty używające `project.json` formatu zarządzania pokazują tylko opcję **Pokaż podgląd okna** .

### <a name="visual-studio-templates"></a>Szablony Visual Studio

*Początkowo w [pakietach NuGet w szablonach programu Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Najlepsze rozwiązania: szablony nie zawierają `project.json` plików i nie zawierają odwołań ani zawartości, które zostałyby dodane po zainstalowaniu pakietów NuGet.