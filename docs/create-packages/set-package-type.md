---
title: Ustaw typ pakietu NuGet
description: Opisuje typy pakietów, aby wskazać zamierzone użycie pakietu.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230827"
---
# <a name="set-a-nuget-package-type"></a>Ustaw typ pakietu NuGet

W przypadku programu NuGet 3.5 + pakiety można oznaczyć przy użyciu określonego *typu pakietu* , aby wskazać jego zamierzone użycie. Pakiety, które nie są oznaczone jako typu, w tym wszystkie pakiety utworzone przy użyciu wcześniejszych wersji programu NuGet, domyślnie są typu `Dependency`.

- pakiety typu `Dependency` umożliwiają dodawanie zasobów kompilacji lub czasu wykonywania do bibliotek i aplikacji, które można zainstalować w dowolnym typie projektu (przy założeniu, że są one zgodne).

- pakiety typu `DotnetTool` są rozszerzeniami [interfejsu wiersza polecenia dotnet](/dotnet/articles/core/tools/index) i są wywoływane z wiersza poleceń. Takie pakiety można instalować tylko w projektach .NET Core i nie mają wpływu na operacje przywracania. Więcej informacji na temat tych rozszerzeń dla poszczególnych projektów można znaleźć w dokumentacji [rozszerzalności platformy .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) .

- pakiety typu `Template` udostępniają [niestandardowe szablony](/dotnet/core/tools/custom-templates) , których można użyć do tworzenia plików lub projektów, takich jak aplikacja, usługa, narzędzie lub Biblioteka klas.

- Pakiety typu niestandardowego używają dowolnego identyfikatora typu, który jest zgodny z tymi samymi regułami formatowania co identyfikatory pakietów. Jednak żaden typ inny niż `Dependency` i `DotnetTool`nie jest rozpoznawany przez Menedżera pakietów NuGet w programie Visual Studio.

Typy pakietów są ustawiane w pliku `.nuspec`. Najlepiej, aby zapewnić zgodność z poprzednimi wersjami, aby *nie* ustawiać jawnie typu `Dependency` i zamiast tego polegać na NuGet przy założeniu, że typ nie jest określony.

- `.nuspec`: wskaż typ pakietu w węźle `packageTypes\packageType` pod elementem `<metadata>`:

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
