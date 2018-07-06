---
title: Migrowanie z plików package.config do formatów PackageReference
description: Szczegółowe informacje na temat sposobu przeprowadzania migracji projektu z formatu plików package.config zarządzania do odwołania PackageReference obsługiwana przez NuGet 4.0 + i programu VS 2017 i platformy .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 1ca97e1c2dfba876aefe6b06eab10def67b8d848
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843397"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migracja z pliku packages.config do elementu PackageReference

Visual Studio 2017 w wersji 15.7 i jego nowsze wersje obsługują migrację projektów z [packages.config](./packages-config.md) format zarządzania [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formatu.

## <a name="benefits-of-using-packagereference"></a>Korzyści z używania funkcji PackageReference

* **Zarządzanie wszystkimi zależnościami projektu w jednym miejscu**: Podobnie jak odwołań między projektami i odwołania do zestawów odwołuje się do pakietu NuGet (przy użyciu `PackageReference` węzła) odbywa się bezpośrednio z poziomu plików projektów, zamiast używać oddzielnego Plik Packages.config.
* **Pozostał widoku najwyższego poziomu zależności**: w przeciwieństwie do pliku packages.config, PackageReference Wyświetla listę tylko tych pakietów NuGet bezpośrednio zainstalowane w projekcie. W rezultacie interfejs użytkownika Menedżera pakietów NuGet i pliku projektu nie są "zatłoczony" z zależnościami niskiego poziomu.
* **Ulepszenia wydajności**: korzystając z funkcji PackageReference, pakiety są obsługiwane w *globalnymi pakietami* folder (zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md) zamiast w `packages` folder, w ramach rozwiązania. W rezultacie PackageReference wykonuje szybciej i zużywa mniej miejsca na dysku.
* **Poprawnie kontrolę nad zależności i zawartości przepływu**: przy użyciu istniejących funkcji programu MSBuild umożliwia [warunkowo odwołują się do pakietu NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) i wybierz odwołania do pakietu dla platformy docelowej konfiguracji Platforma lub inne tabele przestawne.
* **PackageReference podlega aktywnie**: zobacz [PackageReference problemy w usłudze GitHub](https://aka.ms/nuget-pr-improvements). Packages.config nie podlega już aktywnie.

### <a name="limitations"></a>Ograniczenia

* Formatu NuGet PackageReference nie jest dostępne w programie Visual Studio 2015 i starsze. Zmigrowane projektów można otworzyć tylko w programie Visual Studio 2017.
* Migracja nie jest obecnie dostępna dla projektów C++ i programu ASP.NET.
* Niektóre pakiety może nie być w pełni zgodne z PackageReference. Aby uzyskać więcej informacji, zobacz [problemy ze zgodnością pakietu](#package-compatibility-issues).

### <a name="known-issues"></a>Znane problemy

1. `Migrate packages.config to PackageReference...` Opcja nie jest dostępna w menu kontekstowym kliknij prawym przyciskiem myszy 

#### <a name="issue"></a>Problem 
 
Przy pierwszym otwarciu projektu, NuGet może nie mieć zainicjowany, dopóki nie jest wykonywana operacja NuGet. Powoduje to możliwość migracji nie pojawiają się w menu kontekstowym kliknij prawym przyciskiem myszy na `packages.config` lub `References`. 

#### <a name="workaround"></a>Obejście 

Wykonać jedną z następujących czynności NuGet: 
* Otwórz interfejs użytkownika Menedżera pakietów — kliknij prawym przyciskiem myszy `References` i wybierz pozycję `Manage NuGet Packages...` 
* Otwórz konsolę Menedżera pakietów — z `Tools > NuGet Package Manager`, wybierz opcję `Package Manager Console` 
* Uruchom Przywracanie pakietów NuGet — kliknij prawym przyciskiem myszy na węzeł rozwiązania w Eksploratorze rozwiązań i wybierz pozycję `Restore NuGet Packages` 
* Skompiluj projekt, który wyzwala również Przywracanie pakietów NuGet 

Teraz można wyświetlić opcji migracji. Należy zauważyć, że ta opcja nie jest obsługiwane i nie będzie widoczna dla typów projektów platformy ASP.NET i C++. 

## <a name="migration-steps"></a>Kroki migracji

> [!Note]
> Przed rozpoczęciem migracji, program Visual Studio tworzy kopię zapasową projektu, aby możliwe było [: Przywracanie pliku packages.config](#how-to-roll-back-to-packagesconfig) w razie potrzeby.

1. Otwórz rozwiązanie zawierające projekt za pomocą `packages.config`.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **odwołania** węzła lub `packages.config` plik i wybierz **Migrovat packages.config na PackageReference...** .

1. Migrator analizuje odwołania do pakietu NuGet projektu i spróbuje je do kategoryzowania **najwyższego poziomu zależności** (tego katalogu można zainstalować pakietów NuGet) i **przechodnie zależności**(pakietów, które zostały zainstalowane jako zależności pakietów najwyższego poziomu).

   > [!Note]
   > PackageReference obsługuje przywracania pakietów przechodnich i jest rozpoznawana jako zależności dynamicznie, co oznacza przechodnie zależności muszą nie zainstalowania jawnie.

1. (Opcjonalnie) Można traktować pakietu NuGet sklasyfikowane jako zależność przechodnie jako zależność najwyższego poziomu, wybierając **najwyższego poziomu** opcji dla pakietu. Ta opcja jest automatycznie ustawiona dla pakietów zawierających zasoby, których nie została przechodnio przepływu (znajdującymi się na `build`, `buildCrossTargeting`, `contentFiles`, lub `analyzers` folderów) i tymi oznaczone jako zależność na potrzeby opracowywania (`developmentDependency = "true"`).

1. Przejrzeć wszelkie [problemy ze zgodnością pakietu](#package-compatibility-issues).

1. Wybierz **OK** do rozpoczęcia migracji.

1. Po zakończeniu migracji programu Visual Studio udostępnia raport przy użyciu ścieżki kopii zapasowej, listę zainstalowanych pakietów (zależności najwyższego poziomu), do listy pakietów, określany jako zależności przechodnie i listę problemów ze zgodnością zidentyfikowane na początku Migracja. Raport jest zapisywany w folderze kopii zapasowej.

1. Sprawdź, czy rozwiązanie zostanie skompilowane i działa. Jeśli napotkasz problemy, [pliku wystąpił problem w serwisie GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Jak przywrócić pliku packages.config

1. Zamknij projekt zmigrowane.

1. Skopiuj plik projektu i `packages.config` z kopii zapasowej (zazwyczaj `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) do folderu projektu. Usuń obj folder, jeśli istnieje w katalogu głównym projektu.

1. Otwórz projekt.

1. Otwórz konsolę Menedżera pakietów przy użyciu **Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów** polecenia menu.

1. W konsoli, uruchom następujące polecenie:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problemy ze zgodnością pakietu

Niektóre cechy, które były obsługiwane w pliku packages.config nie są obsługiwane w funkcji PackageReference. Migrator analizuje i wykrywa takich problemów. Dowolny pakiet, który ma co najmniej jeden z następujących problemów może nie zachowywać się zgodnie z oczekiwaniami po zakończeniu migracji.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>skrypty "install.ps1" są ignorowane, gdy pakiet jest zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Za pomocą funkcji PackageReference install.ps1 i uninstall.ps1 skryptów programu PowerShell nie są wykonywane podczas instalowania lub odinstalowywania pakietu. |
| **Potencjalny wpływ** | Pakiety, które są zależne od tych skryptów, aby skonfigurować niektóre zachowania w projekcie docelowy może nie działać zgodnie z oczekiwaniami. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>zasoby "treści" są niedostępne, gdy pakiet jest zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Zasoby w pakiecie `content` folderu nie są obsługiwane za pomocą funkcji PackageReference i są ignorowane. PackageReference dodaje obsługę `contentFiles` lepiej obsługę przechodni i udostępnionej zawartości.  |
| **Potencjalny wpływ** | Zasoby w `content` nie są kopiowane do projektu i projektu wymaga refaktoryzacji kodu, który zależy od obecności tych zasobów.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Przekształcenia XDT nie są stosowane, gdy pakiet jest zainstalowany po uaktualnieniu

| | |
| --- | --- |
| **Opis** | Przekształcenia XDT nie są obsługiwane za pomocą funkcji PackageReference i `.xdt` pliki są ignorowane, podczas instalowania lub odinstalowywania pakietu.   |
| **Potencjalny wpływ** | Przekształcenia XDT nie są stosowane do wszystkich plików XML projektu najczęściej `web.config.install.xdt` i `web.config.uninstall.xdt`, co oznacza, że projekt` web.config` plik nie zostanie zaktualizowany po zainstalowaniu lub odinstalowaniu pakietu. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Zestawy w katalogu głównym lib są ignorowane, gdy pakiet jest zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Za pomocą funkcji PackageReference, zestawy są obecne w katalogu głównym `lib` folderu bez target framework określonych podfolderów są ignorowane. NuGet szuka podfolderu dopasowania krótką nazwę platformy docelowej (TFM) odpowiadający platformy docelowej projektu i instaluje zestawy pasujące do projektu. |
| **Potencjalny wpływ** | Pakiety, które nie mają podfolderu dopasowania krótką nazwę platformy docelowej (TFM) odpowiadający platforma docelowa projektu nie będą działać zgodnie z oczekiwaniami po przejściu lub niepowodzenie instalacji podczas migracji |

## <a name="found-an-issue-report-it"></a>Wykryliśmy problem? Zgłoś to!

Jeśli napotkasz problem ze środowiskiem migracji [pliku problemu w repozytorium NuGet GitHub](https://github.com/NuGet/Home/issues/).
