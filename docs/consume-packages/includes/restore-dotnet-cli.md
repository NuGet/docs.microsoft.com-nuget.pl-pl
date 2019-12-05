---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825172"
---
<span data-ttu-id="57d49-101">Użyj [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenie, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="57d49-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="57d49-102">W przypadku platformy .NET Core 2,0 i nowszych przywracanie jest wykonywane automatycznie przy użyciu `dotnet build` i `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="57d49-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="57d49-103">W przypadku programu NuGet 4,0 ten sam kod jest uruchamiany co `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="57d49-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="57d49-104">Podobnie jak w przypadku innych poleceń interfejsu wiersza polecenia `dotnet`, najpierw Otwórz wiersz i przejdź do katalogu, który zawiera plik projektu.</span><span class="sxs-lookup"><span data-stu-id="57d49-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="57d49-105">Aby przywrócić pakiet przy użyciu `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="57d49-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```