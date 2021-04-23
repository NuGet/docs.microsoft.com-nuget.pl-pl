---
title: Pakiety NuGet i kontrola źródła
description: Zagadnienia dotyczące traktowania pakietów NuGet w systemach kontroli wersji i kontroli źródła oraz pomijania pakietów za pomocą usług git i TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: fa3ec6992002224c9fb56a53aee9096e6d2c6fbb
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901671"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Pomijanie pakietów NuGet w systemach kontroli źródła

Deweloperzy zwykle pomijają pakiety NuGet ze swoich [](package-restore.md) repozytoriów kontroli źródła i polegają zamiast tego na przywracaniu pakietów, aby ponownie zainstalować zależności projektu przed kompilacją.

Powody, dla których można polegać na przywracaniu pakietów, są następujące:

1. Rozproszone systemy kontroli wersji, takie jak Git, obejmują pełne kopie każdej wersji każdego pliku w repozytorium. Pliki binarne, które są często aktualizowane, prowadzą do znacznej ilości danych i wydłużają czas klonowania repozytorium.
1. Gdy pakiety są zawarte w repozytorium, deweloperzy są odpowiedzialne za dodawanie odwołań bezpośrednio do zawartości pakietu na dysku zamiast odwoływać się do pakietów za pośrednictwem narzędzia NuGet, co może prowadzić do zakodowanych nazw ścieżek w projekcie.
1. Czyszczenie rozwiązania z nieużywanych folderów pakietów staje się trudniejsze, ponieważ należy upewnić się, że żadne foldery pakietów nie są nadal używane.
1. Pominięcie pakietów pozwala zachować czyste granice własności między kodem a pakietami innych, od których zależysz. Wiele pakietów NuGet jest już utrzymywanych we własnych repozytoriach kontroli źródła.

Chociaż przywracanie pakietów jest zachowaniem domyślnym w przypadku pakietu NuGet, niektóre działania ręczne są niezbędne do pominięcia pakietów, czyli folderu w projekcie, z kontroli źródła, zgodnie z opisem w &mdash; `packages` tym &mdash; artykule.

## <a name="omitting-packages-with-git"></a>Pomijanie pakietów za pomocą usługi Git

Użyj pliku [.gitignore,](https://git-scm.com/docs/gitignore) aby zignorować między innymi pakiety NuGet ( `.nupkg` ), folder i `packages` `project.assets.json` . Aby uzyskać informacje, zobacz [przykład `.gitignore` dla Visual Studio projektów:](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)

Ważne elementy pliku `.gitignore` to:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Pomijanie pakietów za pomocą Kontrola wersji serwera Team Foundation

> [!Note]
> Jeśli to możliwe, postępuj zgodnie z tymi *instrukcjami* przed dodaniem projektu do kontroli źródła. W przeciwnym razie ręcznie usuń `packages` folder z repozytorium i zaewidencjuj tę zmianę przed kontynuowaniem.

Aby wyłączyć integrację kontroli źródła z programem TFVC dla wybranych plików:

1. Utwórz folder o `.nuget` nazwie w folderze rozwiązania (gdzie `.sln` znajduje się plik).
    - Porada: w systemie Windows, aby utworzyć ten folder w Eksplorator Windows, użyj nazwy z `.nuget.`  kropką na końcu.

1. W tym folderze utwórz plik o nazwie `NuGet.Config` i otwórz go do edycji.

1. Dodaj co najmniej następujący tekst, w którym ustawienie [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) Visual Studio pominięcie wszystkiego w `packages` folderze:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Jeśli używasz programu TFS 2010 lub starszego, skłoń `packages` folder w mapowania obszaru roboczego.

1. Na serwerze TFS 2012 lub nowszym lub w Visual Studio Team Services utwórz plik zgodnie z opisem na stronie `.tfignore` Dodawanie plików do [serwera](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true). W tym pliku dołącz zawartość poniżej, aby jawnie zignorować modyfikacje folderu na poziomie repozytorium i `\packages` kilku innych plików pośrednich. (Plik można utworzyć w Eksplorator Windows przy użyciu nazwy a z kropką na końcowej kropce, ale może być konieczne najpierw wyłączenie opcji "Ukryj znane rozszerzenia `.tfignore.` plików"):

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

1. Dodaj `NuGet.Config` i do kontroli źródła i `.tfignore` zaewidencjlij zmiany.
