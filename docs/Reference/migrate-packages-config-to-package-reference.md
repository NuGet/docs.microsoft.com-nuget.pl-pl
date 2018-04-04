---
title: Migrowanie z package.config do formatów PackageReference | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Więcej informacji na temat migracji projektu z formatu zarządzania package.config do PackageReference obsługiwana przez NuGet 4.0 + i VS2017 i .NET Core 2.0
keywords: NuGet migrator migracji, odwołania do pakietu, projektu packages.config pliki, PackageReference, VS2017, Visual Studio 2017 r, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migracja z pliku packages.config do PackageReference

Visual Studio 2017 wersji 15.7 Preview 3 i nowsze wersje obsługują migracji projektu z [packages.config](./packages-config.md) format zarządzania [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.

## <a name="benefits-of-using-packagereference"></a>Korzyści wynikające ze stosowania PackageReference

* **Zarządzanie wszystkie zależności projektu w jednym miejscu**: Podobnie jak odwołań projektów i odwołania do zestawów odwołuje się do pakietu NuGet (przy użyciu `PackageReference` węzła) są zarządzane bezpośrednio w ramach plików projektu, zamiast używać oddzielnego pliku Packages.config.
* **Widok ikonami najwyższego poziomu zależności**: w przeciwieństwie do pliku packages.config, PackageReference wyświetla tylko te pakiety NuGet, które są bezpośrednio zainstalowanych w projekcie. W związku z tym interfejsu użytkownika Menedżera pakietów NuGet i plik projektu nie ma elementów z zależnościami niższego poziomu.
* **Ulepszenia wydajności**: używając PackageReference pakiety są obsługiwane w *globalne pakietów* folder (zgodnie z opisem na [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md) zamiast w `packages` folderu w ramach rozwiązania. W związku z tym PackageReference wykonuje szybciej i zajmuje mniej miejsca na dysku.
* **Drobne kontrolę nad zależności i zawartości przepływu**: istniejące funkcje programu MSBuild umożliwia [warunkowo odwołują się do pakietu NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) i wybierz polecenie odwołania do pakietu dla platformy docelowej, konfiguracji, Platforma lub innych przestawień.
* **PackageReference jest w fazie projektowania active**: zobacz [PackageReference problemów w serwisie GitHub](https://aka.ms/nuget-pr-improvements). Packages.config nie jest już opracowywane aktywne.

### <a name="limitations"></a>Ograniczenia

* NuGet PackageReference nie jest dostępne w programie Visual Studio 2015 lub starszym. Zmigrowane projekty można otwierać tylko w programie Visual Studio 2017 r.
* Migracja nie jest obecnie dostępne dla projektów C++ i platformy ASP.NET.
* Niektóre pakiety nie może być całkowicie zgodne z PackageReference. Aby uzyskać więcej informacji, zobacz [pakietu problemy ze zgodnością](#package-compatibility-issues).

## <a name="migration-steps"></a>Kroki migracji

> [!Note]
> Przed rozpoczęciem migracji programu Visual Studio tworzona jest kopia zapasowa projektu, co pozwala na [: Przywracanie pliku packages.config](#how-to-roll-back-to-packagesconfig) w razie potrzeby.

1. Otwórz rozwiązanie zawierające projekt za pomocą `packages.config`.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **odwołania** węzła lub `packages.config` plik i wybierz **migracji pliku packages.config do PackageReference...** .

1. Migrator analizuje odwołania do pakietu NuGet projektu i próbuje przeprowadzić ich do skategoryzowania **najwyższego poziomu zależności** (ten katalog można zainstalować pakietów NuGet) i **przechodnie zależności**(pakiety, które zostały zainstalowane jako zależności pakietów najwyższego poziomu).

   > [!Note]
   > PackageReference obsługuje Przywracanie pakietu przechodnie i jest rozpoznawany jako zależności dynamicznie, co oznacza przechodnie zależności muszą nie zainstalowania jawnie.

1. (Opcjonalnie) Możesz traktować pakietu NuGet sklasyfikowane jako zależność przechodnie jako zależność najwyższego poziomu, wybierając **najwyższego poziomu** opcją dla pakietu. Ta opcja jest automatycznie ustawiana pakiety zawierające zasoby, które nie wpływają przechodnie (w `build`, `buildCrossTargeting`, `contentFiles`, lub `analyzers` folderów) i tymi oznaczony jako zależność Programowanie (`developmentDependency = "true"`).

1. Przejrzyj wszelkie [pakietu problemy ze zgodnością](#package-compatibility-issues).

1. Wybierz **OK** do rozpoczęcia migracji.

1. Po zakończeniu migracji programu Visual Studio udostępnia raport ze ścieżką do kopii zapasowej, listy pakietów zainstalowanych (najwyższego poziomu zależności), listę pakietów, określany jako zależności przechodnie i listę problemów ze zgodnością identyfikowane na początku Migracja. Raport jest zapisywany w folderze kopii zapasowej.

1. Sprawdź, czy rozwiązanie tworzenia i uruchamiania. Jeśli wystąpią problemy, [pliku problemu w serwisie GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Jak przywrócić pliku packages.config

1. Zamknij projekt zmigrowane.

1. Skopiuj plik projektu i `packages.config` z kopii zapasowej (zazwyczaj `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) do folderu projektu.

1. Otwórz projekt.

1. Otwórz konsolę Menedżera pakietów przy użyciu **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia menu.

1. W konsoli, uruchom następujące polecenie:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problemy ze zgodnością pakietu

Niektóre aspekty, które są obsługiwane w pliku packages.config nie są obsługiwane w PackageReference. Migrator analizuje i wykrywa takich problemów. Dowolnego pakietu, który ma co najmniej jeden z następujących problemów może nie działać zgodnie z oczekiwaniami po migracji.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>skrypty "install.ps1" są ignorowane, gdy pakiet jest zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Z PackageReference install.ps1 i uninstall.ps1 skryptów programu PowerShell nie są wykonywane podczas instalowania lub odinstalowywania pakietu. |
| **Potencjalny wpływ** | Pakiety, które są zależne od tych skryptów, aby skonfigurować niektóre zachowania w projekcie docelowym może nie działać zgodnie z oczekiwaniami. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>"zawartość" zasoby są niedostępne, gdy pakiet jest zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Zasoby w pakiecie `content` folderu nie są obsługiwane z PackageReference i zostaną zignorowane. PackageReference dodaje obsługę `contentFiles` mają lepszą obsługę przechodnie i zawartości udostępnionej.  |
| **Potencjalny wpływ** | Zasoby w `content` nie są kopiowane do projektu i projektu wymaga refaktoryzacji kodu, która zależy od obecności tych zasobów.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformacje XDT nie są stosowane, gdy pakiet jest zainstalowany po uaktualnieniu

| | |
| --- | --- |
| **Opis** | Transformacje XDT nie są obsługiwane przez PackageReference i `.xdt` pliki są ignorowane, podczas instalowania lub odinstalowywania pakietu.   |
| **Potencjalny wpływ** | Transformacje XDT nie są stosowane do projektu pliki XML, najczęściej `web.config.install.xdt` i `web.config.uninstall.xdt`, co oznacza, że projekt` web.config` pliku nie jest aktualizowany po zainstalowaniu lub odinstalowaniu pakietu. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Zestawy w katalogu lib są ignorowane, gdy pakiet jest zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Z PackageReference, zestawów występujących w katalogu głównym `lib` folderu bez docelowego framework określonych podfolderów są ignorowane. NuGet szuka podfolderu dopasowania moniker platformy docelowej (TFM) odpowiadający platformy docelowej projektu i instaluje zestawy pasującego do projektu. |
| **Potencjalny wpływ** | Pakiety, które nie mają podfolderu dopasowania moniker platformy docelowej (TFM) odpowiadający platformy docelowej projektu może nie działać zgodnie z oczekiwaniami po przejściu lub niepowodzenie instalacji podczas migracji |

## <a name="found-an-issue-report-it"></a>Wystąpił problem związany? Zgłoś to!

Jeśli napotkasz problem z obsługi migracji [pliku problemu w repozytorium NuGet GitHub](https://github.com/NuGet/Home/issues/).
