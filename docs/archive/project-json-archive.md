---
title: Zawartość archiwum project.json NuGet
description: Różne bity usunięte z innych części dokumentacji NuGet zawartość pliku project.json.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: cd0f4bc44c1acaeed3b3ed0241c501ddd281628d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="projectjson-archive"></a>archiwum Project.JSON

`project.json` Format zarządzania wprowadzono w systemie NuGet 3.x i używana do pewnych typów projektów. Go została uznana za przestarzałą wraz z wprowadzeniem PackageReference format, w którym zależności są wymienione bezpośrednio w pliku projektu.

Zobacz też:

- [project.json schema](project-json.md)
- [Project.JSON wpływ na autora pakietu](project-json-impact.md)
- [Plik project.json i platforma UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>format zarządzania Project.JSON

*Pierwotnie w [Przywracanie pakietu](../what-is-nuget.md).*

Na liście formatów zarządzania:

- [`project.json`](project-json.md): *(przestarzałe)* pliku A JSON, który przechowuje listę zależności projektu z ogólną wykres pakietu w skojarzony plik `project.lock.json`. Ten format jest zastąpiona PackageReference.

## <a name="nuget-restore-on-mono"></a>Przywracanie nuget dla Mono

*Pierwotnie w [NuGet zainstalować narzędzia klienta](../install-nuget-client-tools.md).*

Współpracuje z `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Ograniczający wersje pakietu z przywracania

*Pierwotnie w [Przywracanie pakietu](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*

- `project.json`: Określ zakres wersji bezpośrednio z numerem wersji tych zależności. Na przykład:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Polecenia interfejsu wiersza polecenia NuGet

- `nuget install` nie działa z `project.json`.
- `nuget restore`: z projektami za pomocą `project.json`, generuje `project.lock.json` pliku i `<project>.nuget.props` plików, jeśli to konieczne. (Oba pliki można pominąć z kontroli źródła). `<projectPath>` Argument może wskazywać `project.json` plików i zachowanie jest takie samo jak wskazujący `packages.config` lub pliku projektu. W kolejności priorytetu do folderów pakietów `%userprofile%\.nuget\packages` przeszukiwane są najpierw przy użyciu `project.json`.
- `nuget update`: Na Mono, to polecenie nie działa z projektami za pomocą `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Rozpoznawanie zależności z PackageReference

*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Zachowanie PackageReference dotyczą również `project.json`. Przywracanie NuGet zapisuje wykresu zależności w pliku o nazwie `project.lock.json` obok `project.json`.

## <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Korzystając z `project.json` format, można kontrolować, które zasoby z przepływu zależności w projekcie najwyższego poziomu. Aby uzyskać więcej informacji, zobacz [project.json](project-json.md).

## <a name="excluding-references"></a>Z wyjątkiem odwołania

*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: Dodaj `"exclude" : "all"` w zależność PackageC:

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

## <a name="resolving-incompatible-package-errors"></a>Rozwiązywanie błędów niezgodne pakietu

*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Dodano sposób rozwiązywaniu problemów z błędami:

- **Nie zaleca się**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projektów przeznaczonych dla `netcore`, `netstandard`, i `netcoreapp` są oznaczane innych platform, jako niezgodna, umożliwiając pakietów przeznaczonych dla tych innych platform, które mają być używane. Zobacz [importuje project.json](project-json.md#imports) i [docelowy programu MSBuild przywracania PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Może to spowodować nieoczekiwane wyniki, więc ponownie najlepiej rozwiązać niezgodności pakietu przy pracy z autorem pakietu podczas aktualizacji.

## <a name="target-frameworks"></a>Docelowych platform

*Pierwotnie w [platform docelowych](../reference/target-frameworks.md).*

- [Project.JSON](project-json.md): `frameworks` wersji framework, które mogą być kompilowane projektu przed określa węzła.

## <a name="creating-a-package"></a>Tworzenie pakietu

*Pierwotnie w [tworzenia pakietu](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Ustawienie typu pakietu

Z platformą .NET Core 1.x, gdy DotnetCliTool pakiet jest zainstalowany, program Visual Studio umieszcza pakietu w `project.json` `tools` węzła zamiast `dependencies` węzła.

Typy pakietów są ustawiane w `project.json`.

- `project.json`: Określ typ pakietu w `packOptions.packageType` właściwości json:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Dodawanie elementów docelowych i właściwości dla programu MSBuild

*Pierwotnie w [tworzenia pakietów NuGet standardowe .NET z programem Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Korzystając z `project.json`, elementy docelowe nie zostaną dodane do projektu, ale są udostępniane za pośrednictwem `project.lock.json`.

### <a name="package-versioning"></a>Przechowywanie wersji pakietu

*Pierwotnie w [wersji pakietu](../reference/package-versioning.md).*

Korzystając z `project.json` formacie NuGet również obsługuje za pomocą notacji symboli wieloznacznych, \*, główna, pomocnicze, poprawki i sufiks wersji wstępnej części numeru.

### <a name="nugetconfig-reference"></a>Odwołanie do pliku NuGet.Config.

*Pierwotnie w [odwołanie do pliku NuGet.Config](../reference/nuget-config-file.md).*

`globalPackagesFolder` dotyczy tylko `project.json`. (Dodanie uwagi: odnosi się także do PackageReference.)

### <a name="nuspec-file-reference"></a>Odwołanie do pliku nuspec

*Pierwotnie w [odwołania nuspec](../reference/nuspec.md).*

`<contentFiles>` Element jest używany zamiast `<files>` z `project.json`.

### <a name="package-manager-options-control"></a>Kontrolki opcji Menedżera pakietów

*Pierwotnie w [informacje o interfejsie użytkownika Menedżera pakietów](../tools/package-manager-ui.md).*

Projektów przy użyciu `project.json` zarządzania format Pokaż tylko **Pokaż okno podglądu** opcji.

### <a name="visual-studio-templates"></a>Szablony Visual Studio

*Pierwotnie w [pakietów NuGet w szablony Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Najlepsze rozwiązania: szablony nie zawierają `project.json` pliku, a nie dołączaj lub żadnych odwołań do zawartości lub zostanie dodany podczas instalowania pakietów NuGet.