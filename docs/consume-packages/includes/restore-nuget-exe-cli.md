---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860577"
---
Użyj polecenia [Restore](../../reference/cli-reference/cli-ref-restore.md) , które pobiera i instaluje wszystkie brakujące pakiety w folderze *Packages* .

W przypadku projektów migrowanych do PackageReference Użyj polecenia [MSBuild-t:Restore](../package-restore.md#restore-using-msbuild) , aby przywrócić pakiety.

`restore`dodaje pakiety tylko do dysku, ale nie zmienia zależności projektu. Aby przywrócić zależności projektu, należy `packages.config`zmodyfikować, a następnie `restore` użyć polecenia.

Podobnie jak w przypadku `nuget.exe` innych poleceń interfejsu wiersza polecenia, najpierw Otwórz wiersz poleceń i przejdź do katalogu, który zawiera plik projektu.

Aby przywrócić pakiet przy użyciu `restore`:

```cli
nuget restore MySolution.sln
```