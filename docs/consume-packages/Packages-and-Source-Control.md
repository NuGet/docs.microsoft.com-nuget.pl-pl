---
title: Pakiety NuGet i kontrola źródła
description: Zagadnienia dotyczące sposobu traktowania pakietów NuGet w systemach kontroli wersji i kontroli źródła oraz jak pominąć pakiety za pomocą usługi git i TFVC.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9bae65573ca49c68d07250228c1923890e0f14ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775012"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Pomijanie pakietów NuGet w systemach kontroli źródła

Deweloperzy zwykle pomijają pakiety NuGet z ich repozytoriów kontroli źródła i polegają na [przywróceniu pakietu](package-restore.md) , aby ponownie zainstalować zależności projektu przed kompilacją.

Przyczyny związane z przywracaniem pakietu są następujące:

1. Rozproszone systemy kontroli wersji, takie jak Git, obejmują pełne kopie każdej wersji każdego pliku w repozytorium. Pliki binarne, które są często aktualizowane, powodują znaczące przeładowanie i wydłużą czas klonowania repozytorium.
1. Gdy pakiety są zawarte w repozytorium, deweloperzy mogą dodawać odwołania bezpośrednio do zawartości pakietu na dysku, a nie odwołania do pakietów za pomocą NuGet, co może prowadzić do zakodowanych nazw ścieżek w projekcie.
1. Nieużywane foldery pakietów staną się trudniejsze do oczyszczenia, co jest konieczne, aby nie usuwać żadnych folderów pakietów, które są nadal używane.
1. Pominięcie pakietów spowoduje zachowanie czystych granic własności między kodem a pakietami od innych użytkowników. Wiele pakietów NuGet jest już przechowywanych w ich własnych repozytoriach kontroli źródła.

Chociaż przywracanie pakietów jest domyślnym zachowaniem w pakiecie NuGet, niektóre czynności ręczne są niezbędne do pominięcia pakietów &mdash; , czyli `packages` folderu w projekcie &mdash; z kontroli źródła, zgodnie z opisem w tym artykule.

## <a name="omitting-packages-with-git"></a>Pomijanie pakietów w usłudze git

Użyj [pliku. gitignore](https://git-scm.com/docs/gitignore) do ignorowania pakietów NuGet ( `.nupkg` ) `packages` folderu i `project.assets.json` , między innymi. Aby uzyskać informacje, zobacz [przykład `.gitignore` dla projektów programu Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Ważne części `.gitignore` pliku są następujące:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Pomijanie pakietów z Kontrola wersji serwera Team Foundation

> [!Note]
> Jeśli to możliwe, wykonaj te instrukcje *przed* dodaniem projektu do kontroli źródła. W przeciwnym razie ręcznie usuń `packages` folder z repozytorium i Zaewidencjonuj tę zmianę przed kontynuowaniem.

Aby wyłączyć integrację kontroli źródła z TFVC dla wybranych plików:

1. Utwórz folder o nazwie `.nuget` w folderze rozwiązania (w którym `.sln` znajduje się plik).
    - Porada: w systemie Windows Aby utworzyć ten folder w Eksploratorze Windows, użyj nazwy `.nuget.` *z* kropką końcową.

1. W tym folderze Utwórz plik o nazwie `NuGet.Config` i otwórz go do edycji.

1. Dodaj następujący tekst jako minimum, gdzie ustawienie [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) instruuje program Visual Studio, aby pominąć wszystkie elementy w `packages` folderze:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Jeśli używasz programu TFS 2010 lub starszego, zamaskowanie `packages` folderu w mapowaniu obszaru roboczego.

1. Na serwerze TFS 2012 lub nowszym lub z Visual Studio Team Services Utwórz `.tfignore` plik zgodnie z opisem w temacie [Dodawanie plików do serwera](/vsts/tfvc/add-files-server?view=vsts#tfignore). W tym pliku Uwzględnij poniżej zawartość, aby jawnie zignorować modyfikacje w `\packages` folderze na poziomie repozytorium i kilku innych plikach pośrednich. (Można utworzyć plik w Eksploratorze Windows przy użyciu nazwy a `.tfignore.` z kropką końcową, ale może być konieczne wyłączenie najpierw opcji "Ukryj znane rozszerzenia plików"):

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

1. Dodaj `NuGet.Config` i `.tfignore` do kontroli źródła i Zaewidencjonuj zmiany.
