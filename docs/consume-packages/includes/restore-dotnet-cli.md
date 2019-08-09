---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860608"
---
<span data-ttu-id="9789f-101">Użyj [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenie, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="9789f-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="9789f-102">W przypadku platformy .NET Core 2,0 i nowszych przywracanie jest wykonywane automatycznie `dotnet build` z `dotnet run`i.</span><span class="sxs-lookup"><span data-stu-id="9789f-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="9789f-103">W przypadku programu NuGet 4,0 ten sam kod jest uruchamiany co `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="9789f-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="9789f-104">Podobnie jak w przypadku `dotnet` innych poleceń interfejsu wiersza polecenia, najpierw Otwórz wiersz poleceń i przejdź do katalogu, który zawiera plik projektu.</span><span class="sxs-lookup"><span data-stu-id="9789f-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="9789f-105">Aby przywrócić pakiet przy użyciu `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="9789f-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```