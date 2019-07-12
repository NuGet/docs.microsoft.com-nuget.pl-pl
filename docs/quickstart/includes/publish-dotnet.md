---
ms.openlocfilehash: bb39e1056ea97ecf1ac70d7fd8e79e65dc04655c
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842139"
---
1. <span data-ttu-id="b2c05-101">Zmień folder zawierający `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="b2c05-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="b2c05-102">Uruchom następujące polecenie, określając nazwę pakietu (identyfikator unikatowy pakiet) i zastępując wartość klucza swój klucz interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="b2c05-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="b2c05-103">polecenia DotNet wyświetla wyniki proces publikowania:</span><span class="sxs-lookup"><span data-stu-id="b2c05-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="b2c05-104">Zobacz [wypychania nuget dotnet](/dotnet/core/tools/dotnet-nuget-push).</span><span class="sxs-lookup"><span data-stu-id="b2c05-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>