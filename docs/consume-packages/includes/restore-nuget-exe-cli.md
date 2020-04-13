---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860577"
---
<span data-ttu-id="68c28-101">Użyj polecenia [przywracania,](../../reference/cli-reference/cli-ref-restore.md) które pobiera i instaluje wszystkie pakiety brakujące w folderze *pakietów.*</span><span class="sxs-lookup"><span data-stu-id="68c28-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="68c28-102">W przypadku projektów migrowanych do PackageReference należy użyć [msbuild -t:restore,](../package-restore.md#restore-using-msbuild) aby zamiast tego przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="68c28-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="68c28-103">`restore`dodaje tylko pakiety do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="68c28-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="68c28-104">Aby przywrócić zależności projektu, zmodyfikuj `packages.config` `restore` , a następnie użyj polecenia.</span><span class="sxs-lookup"><span data-stu-id="68c28-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="68c28-105">Podobnie jak `nuget.exe` w przypadku innych poleceń interfejsu wiersza polecenia, najpierw otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.</span><span class="sxs-lookup"><span data-stu-id="68c28-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="68c28-106">Aby przywrócić pakiet `restore`przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="68c28-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```