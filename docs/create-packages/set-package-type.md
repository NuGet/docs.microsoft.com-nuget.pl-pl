---
title: Ustaw typ pakietu NuGet
description: Opisuje typy pakietów, aby wskazać zamierzone użycie pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774360"
---
# <a name="set-a-nuget-package-type"></a>Ustaw typ pakietu NuGet

W przypadku programu NuGet 3.5 + pakiety można oznaczyć przy użyciu określonego *typu pakietu* , aby wskazać jego zamierzone użycie. Pakiety, które nie są oznaczone jako typu, w tym wszystkie pakiety utworzone przy użyciu wcześniejszych wersji programu NuGet, domyślnie są `Dependency` typu.

- `Dependency` pakiety typów dodają zasoby kompilacji lub czasu wykonywania do bibliotek i aplikacji, które można zainstalować w dowolnym typie projektu (przy założeniu, że są one zgodne).

- `DotnetTool` pakiety typów są rozszerzeniami [interfejsu wiersza polecenia dotnet](/dotnet/articles/core/tools/index) i są wywoływane z wiersza poleceń. Takie pakiety można instalować tylko w projektach .NET Core i nie mają wpływu na operacje przywracania. Więcej informacji na temat tych rozszerzeń dla poszczególnych projektów można znaleźć w dokumentacji  [rozszerzalności platformy .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) .

- `Template` pakiety typów udostępniają [niestandardowe szablony](/dotnet/core/tools/custom-templates) , których można użyć do tworzenia plików lub projektów, takich jak aplikacja, usługa, narzędzie lub Biblioteka klas.

- Pakiety typu niestandardowego używają dowolnego identyfikatora typu, który jest zgodny z tymi samymi regułami formatowania co identyfikatory pakietów. Każdy typ inny niż `Dependency` i `DotnetTool` , ale nie jest rozpoznawany przez Menedżera pakietów NuGet w programie Visual Studio.

Typy pakietów są ustawiane w `.nuspec` pliku. Najlepiej, aby zapewnić zgodność z poprzednimi wersjami, aby *nie* ustawiać jawnie `Dependency` typu i zamiast tego polegać na NuGet przy założeniu, że ten typ nie jest określony.

- `.nuspec`: Wskaż typ pakietu w `packageTypes\packageType` węźle pod `<metadata>` elementem:

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
