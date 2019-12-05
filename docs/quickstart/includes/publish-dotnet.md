---
ms.openlocfilehash: 1df35c96124584bddbe58b8dd6587e3fff256ef9
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825310"
---
1. <span data-ttu-id="14f5f-101">Przejdź do folderu zawierającego plik `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="14f5f-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="14f5f-102">Uruchom następujące polecenie, określając nazwę pakietu (unikatowy identyfikator pakietu) i zastępując kluczową wartość kluczem interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="14f5f-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="14f5f-103">dotnet wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="14f5f-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="14f5f-104">Zobacz [wypychanie NuGet narzędzia dotnet](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="14f5f-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>