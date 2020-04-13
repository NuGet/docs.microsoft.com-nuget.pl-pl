---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860577"
---
Użyj polecenia [przywracania,](../../reference/cli-reference/cli-ref-restore.md) które pobiera i instaluje wszystkie pakiety brakujące w folderze *pakietów.*

W przypadku projektów migrowanych do PackageReference należy użyć [msbuild -t:restore,](../package-restore.md#restore-using-msbuild) aby zamiast tego przywrócić pakiety.

`restore`dodaje tylko pakiety do dysku, ale nie zmienia zależności projektu. Aby przywrócić zależności projektu, zmodyfikuj `packages.config` `restore` , a następnie użyj polecenia.

Podobnie jak `nuget.exe` w przypadku innych poleceń interfejsu wiersza polecenia, najpierw otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.

Aby przywrócić pakiet `restore`przy użyciu:

```cli
nuget restore MySolution.sln
```