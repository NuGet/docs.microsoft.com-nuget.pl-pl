---
title: Ustaw typ pakietu NuGet
description: W tym artykule opisano typy pakietów, aby wskazać przeznaczenie pakietu.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843534"
---
# <a name="set-a-nuget-package-type"></a>Ustaw typ pakietu NuGet

Nuget 3.5 + pakiety mogą być oznaczone określonym *typ pakietu* do wskazania jego przeznaczenia. Domyślnie nie jest oznaczona za pomocą typu, w tym wszystkie pakiety utworzone w starszych wersjach programu NuGet, pakietów `Dependency` typu.

- `Dependency` pakiety typu Dodaj zasoby kompilacji lub czasu wykonywania bibliotek i aplikacji, a można zainstalować w dowolnym typem projektu (przy założeniu, że są one zgodne).

- `DotnetCliTool` rozszerzenia są pakiety typu [wiersz polecenia dotnet](/dotnet/articles/core/tools/index) i są wywoływane z poziomu wiersza polecenia. Takie pakiety można zainstalować tylko w projektach .NET Core i nie mają wpływu na operacje przywracania. Więcej informacji na temat tych rozszerzeń-projekt są dostępne w [rozszerzalność platformy .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentacji.

- Pakiety typu niestandardowego Użyj identyfikatora dowolnego typu, który jest zgodny z tych samych zasad format jako pakiet identyfikatorów. Dowolny typ inny niż `Dependency` i `DotnetCliTool`, jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.

Typy pakietów są ustawiane w `.nuspec` pliku. Jest najlepszym rozwiązaniem dla zapewnienia zgodności, aby *nie* jawnie ustawionej `Dependency` wpisz i zamiast polegać na NuGet, zakładając, że tego typu, gdy typ nie jest określony.

- `.nuspec`: Wskazuje typ pakietu we `packageTypes\packageType` węźle `<metadata>` elementu:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
