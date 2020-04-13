---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825172"
---
<span data-ttu-id="0d4fe-101">Użyj polecenia [przywracania dotnet,](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) które przywraca pakiety wymienione w pliku projektu (patrz [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="0d4fe-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="0d4fe-102">Z .NET Core 2.0 i nowsze, przywracanie odbywa się automatycznie z `dotnet build` i `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="0d4fe-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="0d4fe-103">Od nuget 4.0, to działa `nuget restore`ten sam kod jako .</span><span class="sxs-lookup"><span data-stu-id="0d4fe-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="0d4fe-104">Podobnie jak `dotnet` w przypadku innych poleceń interfejsu wiersza polecenia, najpierw otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="0d4fe-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="0d4fe-105">Aby przywrócić pakiet `dotnet restore`przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="0d4fe-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```