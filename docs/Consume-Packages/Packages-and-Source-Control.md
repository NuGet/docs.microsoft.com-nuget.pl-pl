---
title: "Pakiety NuGet i kontroli źródła | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Zagadnienia dotyczące sposobu traktowania pakietów NuGet w ramach systemów kontroli źródła i kontroli wersji oraz sposób Pomiń pakiety z usługi git i TFVC."
keywords: "Repozytoria kontrolę NuGet do kontroli źródła, NuGet kontroli wersji, NuGet i git, NuGet i TFS, NuGet i TFVC, pomijając pakietów, repozytoria kontroli źródła, wersja"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6261625d5d7eaa748f9ad15510b7b2af3c814e44
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Pominięcie pakietów NuGet w systemów kontroli źródła

Deweloperzy zazwyczaj Pomiń pakietów NuGet z ich repozytoria kontroli źródła i zamiast tego zależne [Przywracanie pakietów](../consume-packages/package-restore.md) ponowna instalacja zależności projektu przed kompilacji.

Dostępne są następujące przyczyny polegania na Przywracanie pakietu:

1. Systemów kontroli wersji rozproszonej, np. Git, obejmują pełne kopie każdej wersji wszystkich plików w repozytorium. Pliki binarne, które są często aktualizowane, prowadzić do znaczących rozrostu i powoduje nieznaczne wydłużenie czasu, potrzebnego do klonowania repozytorium.
1. Gdy pakiety są zawarte w repozytorium, deweloperzy mogą dodać odwołań bezpośrednio do zawartości pakietu na dysku, a nie odwołujący się pakiety za pośrednictwem pakietu NuGet, co może prowadzić do nazwy ścieżek ustalony w projekcie.
1. Staje się on trudniejsze do czyszczenia rozwiązania do pakietu nieużywanych folderów, jak należy upewnić się, że nie usuwaj pakietu foldery nadal w użyciu.
1. Pomijając pakietów, możesz zachować między kodu i pakiety od innych, zależnych od czystą granice własności. Wiele pakietów NuGet są już obsługiwane w ich własnych repozytoria kontroli źródła.

Mimo że Przywracanie pakietu nuget zachowanie domyślne, niektóre czynności ręcznych jest niezbędne pominąć pakiety&mdash;mianowicie `packages` folder w projekcie&mdash;z kontroli źródła, zgodnie z opisem w poniższych sekcjach.

## <a name="omitting-packages-with-git"></a>Pominięcie pakietów za pomocą narzędzia Git

Użyj [pliku .gitignore](https://git-scm.com/docs/gitignore) Aby uniknąć, włączając `packages` folderem w kontroli źródła. Aby informacje, zobacz [próbki `.gitignore` dla projektów programu Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Ważne części `.gitignore` plików są:

```gitignore
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Pominięcie pakiety z Team Foundation Version Control

> [!Note]
> Jeśli to możliwe, wykonaj następujące instrukcje *przed* Dodawanie projektu do kontroli źródła. W przeciwnym razie Usuń ręcznie `packages` folder z repozytorium i wyboru w tej zmiany przed kontynuowaniem.

Aby wyłączyć integracji kontroli źródła z TFVC dla wybranych plików:

1. Utwórz folder o nazwie `.nuget` w folderze rozwiązania (gdzie `.sln` pliku).
    - Porada: w systemie Windows, aby utworzyć ten folder w Eksploratorze Windows, należy użyć nazwy `.nuget.` *z* końcową kropkę.

1. W tym folderze utwórz plik o nazwie `NuGet.Config` i otworzyć do edycji.

1. Dodaj poniższy tekst jako minimum, gdzie [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) ustawienie powoduje, że Visual Studio, aby pominąć wszystkie elementy `packages` folderu:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Jeśli używasz programu TFS 2010 lub starszy, zamaskować `packages` folderu w mapowania obszaru roboczego.

1. Na TFS 2012 lub nowszym, lub z programu Visual Studio Team Services, utworzyć `.tfignore` plików zgodnie z opisem na [AddFiles na serwerze](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore). W tym pliku, należy uwzględnić zawartość poniżej, aby jawnie Ignoruj modyfikacje `\packages` folderu na poziomie repozytorium i kilka innych plików pośrednich. (Należy utworzyć plik w Eksploratorze Windows, przy użyciu nazwy `.tfignore.` końcową kropkę, ale może należy wyłączyć "Ukryj znanego rozszerzenia" opcja najpierw.):

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Dodaj `NuGet.Config` i `.tfignore` do kontroli źródła i zaewidencjonować zmiany.
