---
title: Migrowanie z packages.config do formatów PackageReference
description: Szczegółowe informacje na temat migrowania projektu z packages.configego formatu zarządzania do PackageReference jako obsługiwanego przez narzędzia NuGet 4.0 + i program VS2017 i .NET Core 2,0
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8161f4a39d4adfdb9efb25bcb840b20b85a58e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774786"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrowanie z packages.config do PackageReference

Program Visual Studio 2017 w wersji 15,7 lub nowszej obsługuje Migrowanie projektu z [packages.configego ](../reference/packages-config.md) formatu zarządzania do formatu [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Zalety korzystania z usługi PackageReference

* **Zarządzaj wszystkimi zależnościami projektu w jednym miejscu**: podobnie jak odwołania do projektu i odwołania do zestawów, odwołania do pakietów NuGet (przy użyciu `PackageReference` węzła) są zarządzane bezpośrednio w plikach projektu, a nie przy użyciu oddzielnego pliku packages.config.
* **Nieczytelny widok zależności najwyższego poziomu**: w przeciwieństwie do packages.config, PackageReference wyświetla tylko te pakiety NuGet, które zostały bezpośrednio zainstalowane w projekcie. W związku z tym interfejs użytkownika Menedżera pakietów NuGet i plik projektu nie są zachowywane w zależnościach niskiego poziomu.
* **Udoskonalenia wydajności**: w przypadku korzystania z PackageReference pakiety są przechowywane w folderze *Global-Packages* (zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md) , a nie w `packages` folderze w ramach rozwiązania. W efekcie PackageReference wykonuje szybszy i zużywa mniej miejsca na dysku.
* **Kontrola nad zależnościami i przepływem zawartości**: korzystając z istniejących funkcji programu MSBuild, można [warunkowo odwoływać się do pakietu NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) i wybierać odwołania do pakietów na platformę docelową, konfigurację, platformę lub inne przestawki.
* **PackageReference jest objęty aktywnym programowaniem**: zobacz [PackageReference problemy w witrynie GitHub](https://aka.ms/nuget-pr-improvements). packages.config nie jest już w trakcie aktywnego programowania.

### <a name="limitations"></a>Ograniczenia

* Pakiet NuGet PackageReference nie jest dostępny w programie Visual Studio 2015 i jego starszych wersjach. Zmigrowane projekty można otwierać tylko w programie Visual Studio 2017 i nowszych.
* Migracja nie jest obecnie dostępna dla projektów C++ i ASP.NET.
* Niektóre pakiety mogą nie być w pełni zgodne z PackageReference. Aby uzyskać więcej informacji, zobacz [problemy ze zgodnością pakietu](#package-compatibility-issues).

Ponadto istnieją pewne różnice w sposobie, w jaki składnika packagereferences pracują w porównaniu do packages.config. Na przykład [nieograniczone wersje uaktualnienia](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) nie są Supprted przez PackageReference, ale dodano obsługę [wersji zmiennoprzecinkowych](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Znane problemy

1. `Migrate packages.config to PackageReference...`Opcja nie jest dostępna w menu kontekstowym po kliknięciu prawym przyciskiem myszy 

#### <a name="issue"></a>Problem 
 
Po pierwszym otwarciu projektu, pakiet NuGet może nie zostać zainicjowany do momentu wykonania operacji NuGet. Powoduje to, że opcja migracji nie jest wyświetlana w menu kontekstowym prawym przyciskiem myszy w `packages.config` lub `References` . 

#### <a name="workaround"></a>Obejście 

Wykonaj jedną z następujących akcji NuGet: 
* Otwórz interfejs użytkownika Menedżera pakietów — kliknij prawym przyciskiem myszy `References` i wybierz pozycję `Manage NuGet Packages...` 
* Otwórz konsolę Menedżera pakietów — z `Tools > NuGet Package Manager` , wybierz pozycję `Package Manager Console` 
* Uruchom przywracanie NuGet — kliknij prawym przyciskiem myszy węzeł rozwiązania w Eksplorator rozwiązań a następnie wybierz pozycję `Restore NuGet Packages` 
* Kompiluj projekt, który również wyzwala przywracanie NuGet 

Teraz powinno być możliwe sprawdzenie opcji migracji. Należy zauważyć, że ta opcja nie jest obsługiwana i nie będzie wyświetlana dla typów projektów ASP.NET i C++. 

## <a name="migration-steps"></a>Kroki migracji

> [!Note]
> Przed rozpoczęciem migracji program Visual Studio tworzy kopię zapasową projektu, aby umożliwić [przywrócenie do packages.configw ](#how-to-roll-back-to-packagesconfig) razie potrzeby.

1. Otwórz rozwiązanie zawierające projekt przy użyciu `packages.config` .

1. W **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy węzeł **odwołania** lub `packages.config` plik, a następnie wybierz polecenie **Migruj packages.config do PackageReference...**.

1. Migrator analizuje odwołania do pakietu NuGet projektu i podejmuje próbę skategoryzowania ich do **zależności najwyższego poziomu** (pakiety NuGet zainstalowane bezpośrednio) i **zależności przechodnie** (pakiety, które zostały zainstalowane jako zależności pakietów najwyższego poziomu).

   > [!Note]
   > PackageReference obsługuje przechodnie przywracanie pakietów i dynamiczne Rozwiązywanie zależności, co oznacza, że zależności przechodnie nie muszą być instalowane jawnie.

1. Obowiązkowe Można traktować pakiet NuGet sklasyfikowany jako zależność przechodnią jako zależność najwyższego poziomu, wybierając opcję **najwyższego poziomu** dla pakietu. Ta opcja jest ustawiana automatycznie dla pakietów zawierających zasoby, które nie przepływy przechodnie (te `build` w `buildCrossTargeting` folderach,, `contentFiles` , lub `analyzers` ) i są oznaczone jako zależność programistyczna ( `developmentDependency = "true"` ).

1. Przejrzyj wszelkie [problemy ze zgodnością pakietu](#package-compatibility-issues).

1. Wybierz **przycisk OK** , aby rozpocząć migrację.

1. Po zakończeniu migracji program Visual Studio udostępnia raport ze ścieżką do kopii zapasowej, listę zainstalowanych pakietów (zależności najwyższego poziomu), listę pakietów przywoływanych jako zależności przechodnie oraz listę problemów ze zgodnością zidentyfikowaną na początku migracji. Raport jest zapisywany w folderze kopii zapasowej.

1. Sprawdź, czy rozwiązanie zostało skompilowane i uruchomione. Jeśli wystąpią problemy, należy [rozwiązać problem w serwisie GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Jak przywrócić packages.config

1. Zamknij zmigrowany projekt.

1. Skopiuj plik projektu i `packages.config` z kopii zapasowej (zazwyczaj `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\` ) do folderu projektu. Usuń folder obj, jeśli istnieje w katalogu głównym projektu.

1. Otwórz projekt.

1. Otwórz konsolę Menedżera pakietów przy użyciu **narzędzi > Menedżer pakietów NuGet > menu konsoli Menedżera** pakietów.

1. Uruchom następujące polecenie w konsoli programu:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Utwórz pakiet po migracji

Po zakończeniu migracji zalecamy dodanie odwołania do pakietu NuGet [NuGet. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) , a następnie użycie programu [MSBuild-t:Pack](../reference/msbuild-targets.md#pack-target) w celu utworzenia pakietu. Chociaż w niektórych scenariuszach można korzystać `dotnet.exe pack` z programu zamiast `msbuild -t:pack` , nie jest to zalecane.

## <a name="package-compatibility-issues"></a>Problemy ze zgodnością pakietu

Niektóre aspekty, które były obsługiwane w packages.config nie są obsługiwane w PackageReference. Migrator analizuje i wykrywa te problemy. Każdy pakiet, który ma co najmniej jeden z następujących problemów, może nie zachowywać się zgodnie z oczekiwaniami po migracji.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Skrypty "install.ps1" są ignorowane, gdy pakiet zostanie zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | W programie PackageReference skrypty programu PowerShell install.ps1 i uninstall.ps1 nie są wykonywane podczas instalowania lub odinstalowywania pakietu. |
| **Potencjalny wpływ** | Pakiety, które są zależne od tych skryptów, aby skonfigurować zachowanie w projekcie docelowym, mogą nie funkcjonować zgodnie z oczekiwaniami. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>zasoby "Content" nie są dostępne, gdy pakiet zostanie zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Elementy zawartości w folderze pakietu `content` nie są obsługiwane w programie PackageReference i są ignorowane. PackageReference dodaje obsługę programu `contentFiles` w celu uzyskania lepszej obsługi przechodniej i zawartości udostępnionej.  |
| **Potencjalny wpływ** | Elementy zawartości w programie `content` nie są kopiowane do projektu i kodu projektu, które są zależne od obecności tych zasobów, wymagają refaktoryzacji.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Przekształcenia XDT nie są stosowane, gdy pakiet zostanie zainstalowany po uaktualnieniu

| | |
| --- | --- |
| **Opis** | Przekształcenia XDT są nieobsługiwane w przypadku PackageReference i `.xdt` pliki są ignorowane podczas instalowania lub odinstalowywania pakietu.   |
| **Potencjalny wpływ** | Przekształcenia XDT nie są stosowane do żadnych plików XML projektu, najczęściej `web.config.install.xdt` i `web.config.uninstall.xdt` , co oznacza, że ` web.config` plik projektu nie jest aktualizowany po zainstalowaniu lub odinstalowaniu pakietu. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Zestawy w katalogu głównym lib są ignorowane, gdy pakiet zostanie zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | W przypadku PackageReference zestawy znajdujące się w katalogu głównym `lib` folderu bez podfolderu specyficznego dla platformy docelowej są ignorowane. Pakiet NuGet szuka podfolderu pasującego do krótkiej nazwy platformy docelowej (TFM) odpowiadającej platformie docelowej projektu i instaluje pasujące zestawy do projektu. |
| **Potencjalny wpływ** | Pakiety, które nie mają podfolderu pasującego do monikera platformy docelowej (TFM) odpowiadające platformie docelowej projektu, mogą nie zachowywać się zgodnie z oczekiwaniami po przejściu lub nieudanej instalacji podczas migracji |

## <a name="found-an-issue-report-it"></a>Znaleziono problem? Zgłoś!

Jeśli wystąpi problem ze środowiska migracji, należy [rozwiązać problem w repozytorium GitHub usługi NuGet](https://github.com/NuGet/Home/issues/).
