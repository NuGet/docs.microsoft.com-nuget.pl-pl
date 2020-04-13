---
title: Ustawianie typu pakietu NuGet
description: W tym artykule opisano typy pakietów, aby wskazać zamierzone użycie pakietu.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230827"
---
# <a name="set-a-nuget-package-type"></a>Ustawianie typu pakietu NuGet

Z NuGet 3.5+, pakiety mogą być oznaczone określonego *typu pakietu,* aby wskazać jego przeznaczenie. Pakiety nie są oznaczone typem, w tym wszystkie pakiety `Dependency` utworzone z wcześniejszymi wersjami NuGet, domyślnie typu.

- `Dependency`pakiety typu dodać zasoby kompilacji lub wykonywania do bibliotek i aplikacji i mogą być instalowane w dowolnym typie projektu (przy założeniu, że są one zgodne).

- `DotnetTool`pakiety typów są rozszerzeniami do [dotnet CLI](/dotnet/articles/core/tools/index) i są wywoływane z wiersza polecenia. Takie pakiety mogą być instalowane tylko w projektach .NET Core i nie mają wpływu na operacje przywracania. Więcej szczegółów na temat tych rozszerzeń dla projektu są dostępne w dokumentacji [rozszerzalności .NET Core.](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)

- `Template`pakiety typów zapewniają [niestandardowe szablony,](/dotnet/core/tools/custom-templates) które mogą być używane do tworzenia plików lub projektów, takich jak aplikacja, usługa, narzędzie lub biblioteka klas.

- Niestandardowe pakiety typów używają dowolnego identyfikatora typu, który jest zgodny z regułami tego samego formatu co identyfikatory pakietów. Każdy typ `Dependency` inny `DotnetTool`niż i , jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.

Typy pakietów `.nuspec` są ustawiane w pliku. Najlepiej jest dla zgodności z powrotem, aby *nie* jawnie ustawić `Dependency` typ i zamiast polegać na NuGet przy założeniu, że ten typ, gdy nie określono typu.

- `.nuspec`: Wskazać typ pakietu `packageTypes\packageType` w `<metadata>` węźle pod elementem:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
