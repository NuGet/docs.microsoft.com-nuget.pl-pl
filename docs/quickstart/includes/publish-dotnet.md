---
ms.openlocfilehash: 1df35c96124584bddbe58b8dd6587e3fff256ef9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825310"
---
1. Zmień folder zawierający `.nupkg` plik.

1. Uruchom następujące polecenie, określając nazwę pakietu (unikatowy identyfikator pakietu) i zastępując wartość klucza kluczem interfejsu API:

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. dotnet wyświetla wyniki procesu publikowania:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Zobacz [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).