---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860577"
---
<span data-ttu-id="b88a0-101">Użyj polecenia [Restore](../../reference/cli-reference/cli-ref-restore.md) , które pobiera i instaluje wszystkie brakujące pakiety w folderze *Packages* .</span><span class="sxs-lookup"><span data-stu-id="b88a0-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="b88a0-102">W przypadku projektów migrowanych do PackageReference Użyj polecenia [MSBuild-t:Restore](../package-restore.md#restore-using-msbuild) , aby przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="b88a0-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="b88a0-103">`restore`dodaje pakiety tylko do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="b88a0-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="b88a0-104">Aby przywrócić zależności projektu, należy `packages.config`zmodyfikować, a następnie `restore` użyć polecenia.</span><span class="sxs-lookup"><span data-stu-id="b88a0-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="b88a0-105">Podobnie jak w przypadku `nuget.exe` innych poleceń interfejsu wiersza polecenia, najpierw Otwórz wiersz poleceń i przejdź do katalogu, który zawiera plik projektu.</span><span class="sxs-lookup"><span data-stu-id="b88a0-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="b88a0-106">Aby przywrócić pakiet przy użyciu `restore`:</span><span class="sxs-lookup"><span data-stu-id="b88a0-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```