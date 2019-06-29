---
title: Zawartość archiwum pliku project.json NuGet
description: Różne bity zawartość pliku project.json usunięcie z innych obszarów dokumentacja programu NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: d43f002b740b669de13f5872844ac0df97fc8fdc
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467786"
---
# <a name="projectjson-archive"></a>archiwum pliku Project.JSON

`project.json` Format zarządzania wprowadzono nuget 3.x i używane w przypadku niektórych typów projektów. Została ona zakończona wraz z wprowadzeniem PackageReference format, w którym zależności są wymienione bezpośrednio w pliku projektu.

Zobacz też:

- [project.json schema](project-json.md)
- [wpływ pliku Project.JSON na autorom pakietów](project-json-impact.md)
- [Plik project.json i platforma UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Format zarządzania project.json

*Początkowo w [Przywracanie pakietu](../what-is-nuget.md).*

Na liście formatów zarządzania:

- [`project.json`](project-json.md): *(przestarzałe)* pliku JSON, który utrzymuje listę zależności projektu za pomocą ogólny wykres pakietu skojarzony plik `project.lock.json`. Ten format jest zastąpiona PackageReference.

## <a name="nuget-restore-on-mono"></a>Przywracanie nuget dla platformy Mono

*Początkowo w [narzędzia klienta programu NuGet zainstalować](../install-nuget-client-tools.md).*

W programach `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Ograniczający wersji pakietu, dzięki funkcji przywracania

*Początkowo w [Przywracanie pakietu](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*

- `project.json`: Określ zakres wersji bezpośrednio z numerem wersji zależności. Na przykład:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Polecenia interfejsu wiersza polecenia NuGet

- `nuget install` nie działa z `project.json`.
- `nuget restore`: z projektami za pomocą `project.json`, generuje `project.lock.json` pliku i `<project>.nuget.props` pliku, jeśli to konieczne. (Oba pliki można pominąć z kontroli źródła.) `<projectPath>` Argument może wskazywać `project.json` plików i ma takie samo zachowanie, co wskazuje `packages.config` lub pliku projektu. W kolejności priorytetu do folderów pakietów `%userprofile%\.nuget\packages` jest przeszukiwany w pierwszej kolejności przy użyciu `project.json`.
- `nuget update`: W rozwiązaniu Mono to polecenie nie działa z projektami za pomocą `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Rozpoznawanie zależności za pomocą funkcji PackageReference

*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Zachowanie funkcji PackageReference ma również zastosowanie do `project.json`. Przywracanie pakietów NuGet zapisuje wykres zależności w pliku o nazwie `project.lock.json` obok `project.json`.

## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Korzystając z `project.json` formatu, można kontrolować, które zasoby z przepływem zależności do najwyższego poziomu projektu. Aby uzyskać więcej informacji, zobacz [project.json](project-json.md).

## <a name="excluding-references"></a>Z wyjątkiem odwołania

*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: Dodaj `"exclude" : "all"` powstanie zależności dla PackageC:

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

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie błędów pakietu niezgodne

*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Dodano sposób Rozwiązywanie błędów:

- **Nie zaleca się**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projekty przeznaczone dla `netcore`, `netstandard`, i `netcoreapp` można oznaczają inne struktury jako zgodne, umożliwiając w ten sposób pakiety przeznaczone dla tych inne struktury do użycia. Zobacz [importuje plik project.json](project-json.md#imports) i [docelowej przywracania MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Może to powodować nieoczekiwane zachowania, więc ponownie jest najlepsze rozwiązanie niezgodności pakietu poprzez współdziałanie z autorem pakietu podczas aktualizacji.

## <a name="target-frameworks"></a>Platformy docelowe

*Początkowo w [ustalać platformy docelowe](../reference/target-frameworks.md).*

- [project.json](project-json.md): `frameworks` Węzła określa wersje framework skompilowany projekt.

## <a name="creating-a-package"></a>Tworzenie pakietu

*Początkowo w [Tworzenie pakietu](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Ustawianie typu pakietu

Za pomocą programu .NET Core 1.x, gdy DotnetCliTool pakiet jest zainstalowany, program Visual Studio umieszcza pakiet w `project.json` `tools` węzła zamiast `dependencies` węzła.

Typy pakietów są ustawiane w `project.json`.

- `project.json`: Wskazuje typ pakietu we `packOptions.packageType` właściwości json:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Dodawanie obiektów docelowych i właściwości dla programu MSBuild

*Początkowo w [utworzyć pakiety NuGet standardowy .NET przy użyciu programu Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Korzystając z `project.json`, elementy docelowe nie są dodawane do projektu, ale są udostępniane za pośrednictwem `project.lock.json`.

### <a name="package-versioning"></a>Przechowywanie wersji pakietów

*Początkowo w [przechowywanie wersji pakietów](../reference/package-versioning.md).*

Korzystając z `project.json` formatowania, NuGet również obsługuje używanie notacji symbolu wieloznacznego, \*, główne, pomocnicze, poprawki i sufiks wersji wstępnej części numeru.

### <a name="nugetconfig-reference"></a>Odwołanie do pliku NuGet.Config

*Początkowo w [odwołanie do pliku NuGet.Config](../reference/nuget-config-file.md).*

`globalPackagesFolder` ma zastosowanie tylko do `project.json`. (Dodanie uwagi: ma zastosowanie również do odwołania PackageReference.)

### <a name="nuspec-file-reference"></a>Odwołanie do pliku nuspec

*Początkowo w [odwołania nuspec](../reference/nuspec.md).*

`<contentFiles>` Element jest używany zamiast `<files>` z `project.json`.

### <a name="package-manager-options-control"></a>Kontrolka opcji Menedżera pakietów

*Początkowo w [informacje o interfejsie użytkownika Menedżera pakietów](../tools/package-manager-ui.md).*

Projekty, za pomocą `project.json` zarządzania format zobrazit pouze **Pokaż okno podglądu** opcji.

### <a name="visual-studio-templates"></a>Szablony Visual Studio

*Początkowo w [pakietów NuGet w programie Visual Studio szablonach](../visual-studio-extensibility/visual-studio-templates.md).*

Najlepsze rozwiązania: szablony nie obejmują `project.json` pliku i nie obejmują lub odwołania do dowolnej zawartości, która zostanie dodany po zainstalowaniu pakietów NuGet.