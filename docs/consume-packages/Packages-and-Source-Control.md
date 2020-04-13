---
title: Pakiety NuGet i kontrola źródła
description: Zagadnienia dotyczące sposobu leczenia pakietów NuGet w ramach kontroli wersji i systemów kontroli źródła oraz sposobu pominięcia pakietów z git i TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019978"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Pomijanie pakietów NuGet w systemach kontroli źródła

Deweloperzy zazwyczaj pominąć pakiety NuGet z ich repozytoriów kontroli źródła i zamiast tego polegać na [przywracanie pakietu,](package-restore.md) aby ponownie zainstalować zależności projektu przed kompilacją.

Powody, dla których warto polegać na przywracaniu pakietu, są następujące:

1. Rozproszone systemy kontroli wersji, takie jak Git, zawierają pełne kopie każdej wersji każdego pliku w repozytorium. Pliki binarne, które są często aktualizowane prowadzić do znacznego uwędzić i wydłuża czas potrzebny do sklonowania repozytorium.
1. Gdy pakiety są zawarte w repozytorium, deweloperzy są umienia dodać odwołania bezpośrednio do zawartości pakietu na dysku, a nie odwoływanie się do pakietów za pośrednictwem NuGet, co może prowadzić do zakodowanych nazw ścieżek w projekcie.
1. Staje się trudniejsze do czyszczenia rozwiązania nieużywanych folderów pakietu, jak trzeba upewnić się, że nie usuwać żadnych folderów pakietu nadal w użyciu.
1. Pomijając pakiety, należy zachować czyste granice własności między kodem a pakietami od innych, od których zależy. Wiele pakietów NuGet są już obsługiwane we własnych repozytoriach kontroli źródła.

Chociaż przywracanie pakietu jest domyślnym zachowaniem z NuGet,&mdash;niektóre ręczne prace są niezbędne do pominięcia pakietów, a mianowicie `packages` folder w projekcie&mdash;z kontroli źródła, zgodnie z opisem w tym artykule.

## <a name="omitting-packages-with-git"></a>Pomijanie pakietów z Git

Użyj [pliku gitignore,](https://git-scm.com/docs/gitignore) aby zignorować`.nupkg`pakiety NuGet ( ) `packages` folder i `project.assets.json`, między innymi. Aby uzyskać odwołanie, zobacz [przykład dla `.gitignore` projektów programu Visual Studio:](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)

Ważnymi częściami `.gitignore` pliku są:

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Pomijanie pakietów z kontrolą wersji Team Foundation

> [!Note]
> Postępuj zgodnie z tymi instrukcjami, jeśli to możliwe *przed* dodaniem projektu do kontroli źródła. W przeciwnym razie `packages` ręcznie usuń folder z repozytorium i zaewidencjonuj tę zmianę przed kontynuowaniem.

Aby wyłączyć integrację kontroli źródła z TFVC dla wybranych plików:

1. Utwórz folder `.nuget` wywoływany w folderze rozwiązania (w którym znajduje się `.sln` plik).
    - Wskazówka: w systemie Windows, aby utworzyć ten `.nuget.` folder w Eksploratorze Windows, użyj nazwy *z* końcową kropką.

1. W tym folderze utwórz plik o nazwie `NuGet.Config` i otwórz go do edycji.

1. Dodaj następujący tekst jako minimum, gdzie [ustawienie disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) nakazuje programowi Visual Studio pominąć wszystko w folderze: `packages`

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Jeśli używasz TFS 2010 lub wcześniej, zamaskuj `packages` folder w mapowaniach obszaru roboczego.

1. W programie TFS 2012 lub nowszym lub `.tfignore` w programie Visual Studio Team Services należy utworzyć plik zgodnie z opisem w programie [Dodaj pliki do serwera](/vsts/tfvc/add-files-server?view=vsts#tfignore). W tym pliku dołącz poniższą zawartość, aby `\packages` jawnie zignorować modyfikacje folderu na poziomie repozytorium i kilku innych plików pośrednich. (Plik można utworzyć w Eksploratorze `.tfignore.` Windows przy użyciu nazwy a z końcową kropką, ale może być konieczne wyłączenie opcji "Ukryj znane rozszerzenia plików".

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Dodaj `NuGet.Config` `.tfignore` i do kontroli źródła i zaewidencjonuj zmiany.
