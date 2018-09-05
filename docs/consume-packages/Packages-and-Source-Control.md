---
title: Pakiety NuGet i kontrola źródła
description: Informacje dotyczące sposobu traktowania pakietów NuGet w ramach systemów kontroli wersji kontroli i źródła i pominąć pakiety za pomocą narzędzia git i TFVC.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 0338c3445b2a3d8169158171d97d1e874533a80a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551802"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Pominięcie pakietów NuGet w systemów kontroli źródła

Deweloperzy zazwyczaj pakietów NuGet z ich repozytoriów kontroli źródła i pominięte zamiast polegać na [pakietu przywracania](package-restore.md) ponowna instalacja zależności projektu przed kompilacją.

Opierając się na Przywracanie pakietu przyczyny są następujące:

1. Systemy kontroli wersji rozproszonej, takich jak Git, zawierać pełne kopie każdej wersji każdego pliku w repozytorium. Pliki binarne, które są często aktualizowane prowadzić do znaczących rozrostu i powoduje nieznaczne wydłużenie czasu potrzebnego do sklonowania repozytorium.
1. Gdy pakiety są zawarte w repozytorium, deweloperzy mają ponosić odpowiedzialności wobec Dodaj odwołania bezpośrednio do zawartości pakietu na dysku, a nie na pakiety odwołujący się za pośrednictwem pakietu NuGet, co może prowadzić do nazwy zakodowanych ścieżek w projekcie.
1. Ze zrozumieniem czystego rozwiązania wszystkie foldery nieużywanych pakietów na potrzeby upewnij się, że nie usuwaj żadnych folderów pakietu nadal w użyciu.
1. Pomijając pakietów, możesz zachować czyste granice prawa własności między kod aplikacji i pakietów od innych, zależnych od. Wiele pakietów NuGet są już obsługiwane w ich własnych repozytoriów kontroli źródła.

Mimo że Przywracanie pakietu jest to domyślne zachowanie nuget, niektóre ręczne praca jest konieczna pominąć pakietów&mdash;, `packages` folder w projekcie&mdash;z kontroli źródła, zgodnie z opisem w tym artykule.

## <a name="omitting-packages-with-git"></a>Pominięcie pakietów przy użyciu narzędzia Git

Użyj [pliku .gitignore](https://git-scm.com/docs/gitignore) ignorowanie pakiety NuGet (`.nupkg`) `packages` folderu i `project.assets.json`, między innymi. Aby informacje, zobacz [przykładowe `.gitignore` dla projektów programu Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Ważne elementy `.gitignore` pliku są:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Pominięcie pakiety z kontroli wersji serwera Team Foundation

> [!Note]
> Jeśli to możliwe, wykonaj następujące instrukcje *przed* Dodawanie projektu do kontroli źródła. W przeciwnym razie ręcznie usuń `packages` folder z repozytorium i zaewidencjonuj zmiany przed kontynuowaniem.

Aby wyłączyć integrację kontroli źródła z użyciem systemu TFVC dla wybranych plików:

1. Utwórz folder o nazwie `.nuget` w folderze rozwiązania (gdzie `.sln` pliku).
    - Porada: na Windows, aby utworzyć ten folder w Eksploratorze Windows, należy użyć nazwy `.nuget.` *z* końcową kropkę.

1. W tym folderze utwórz plik o nazwie `NuGet.Config` i otworzyć do edycji.

1. Dodaj następujący tekst jako minimum, gdzie [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) ustawienie powoduje, że Visual Studio, aby pominąć wszystkie elementy `packages` folderu:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Jeśli używasz programu TFS 2010 lub starszy, zamaskować `packages` folderu mapowania obszarów roboczych.

1. W programie TFS 2012 lub nowszym lub Visual Studio Team Services, utworzyć `.tfignore` plików zgodnie z opisem na [AddFiles serwerowi](/vsts/tfvc/add-files-server.md?view=vsts#tfignore). W tym pliku obejmują zawartość poniżej, aby jawnie Ignoruj modyfikacje `\packages` folder na poziomie repozytorium i kilka innych plików pośrednich. (Należy utworzyć plik w Eksploratorze Windows, przy użyciu nazwy `.tfignore.` końcową kropkę, ale może być konieczne można wyłączyć "Ukryj rozszerzenia znanych" opcji najpierw.):

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Dodaj `NuGet.Config` i `.tfignore` do kontroli źródła i zaewidencjonuj zmiany.
