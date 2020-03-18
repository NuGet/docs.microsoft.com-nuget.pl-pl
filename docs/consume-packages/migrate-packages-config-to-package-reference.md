---
title: Migrowanie z pliku Package. config do formatów PackageReference
description: Szczegółowe informacje na temat migrowania projektu z formatu Package. config Management do PackageReference jako obsługiwanego przez narzędzia NuGet 4.0 + i program VS2017 i .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428892"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migruj z pliku Packages. config do PackageReference

Program Visual Studio 2017 w wersji 15,7 lub nowszej obsługuje Migrowanie projektu z formatu [Package. config](../reference/packages-config.md) Management do formatu [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Zalety korzystania z usługi PackageReference

* **Zarządzaj wszystkimi zależnościami projektu w jednym miejscu**: podobnie jak odwołania do projektu i odwołania do zestawów, odwołania do pakietów NuGet (przy użyciu węzła `PackageReference`) są zarządzane bezpośrednio w plikach projektu, a nie przy użyciu oddzielnego pliku Packages. config.
* **Nieczytelny widok zależności najwyższego poziomu**: w przeciwieństwie do Packages. config program PackageReference wyświetla listę tylko tych pakietów NuGet, które są bezpośrednio zainstalowane w projekcie. W związku z tym interfejs użytkownika Menedżera pakietów NuGet i plik projektu nie są zachowywane w zależnościach niskiego poziomu.
* **Udoskonalenia wydajności**: w przypadku korzystania z PackageReference pakiety są przechowywane w folderze *Global-Packages* (zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md) , a nie w folderze `packages` w ramach rozwiązania. W efekcie PackageReference wykonuje szybszy i zużywa mniej miejsca na dysku.
* **Kontrola nad zależnościami i przepływem zawartości**: korzystając z istniejących funkcji programu MSBuild, można [warunkowo odwoływać się do pakietu NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) i wybierać odwołania do pakietów na platformę docelową, konfigurację, platformę lub inne przestawki.
* **PackageReference jest objęty aktywnym programowaniem**: zobacz [PackageReference problemy w witrynie GitHub](https://aka.ms/nuget-pr-improvements). Pakiet Packages. config nie jest już objęty aktywnym programowaniem.

### <a name="limitations"></a>Ograniczenia

* Pakiet NuGet PackageReference nie jest dostępny w programie Visual Studio 2015 i jego starszych wersjach. Zmigrowane projekty można otwierać tylko w programie Visual Studio 2017 i nowszych.
* Migracja nie jest obecnie dostępna dla C++ projektów i ASP.NET.
* Niektóre pakiety mogą nie być w pełni zgodne z PackageReference. Aby uzyskać więcej informacji, zobacz [problemy ze zgodnością pakietu](#package-compatibility-issues).

Ponadto istnieją pewne różnice w sposobie działania składnika packagereferences w porównaniu z pakietem Packages. config. Na przykład [nieograniczone wersje uaktualnienia](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) nie są Supprted przez PackageReference, ale dodano obsługę [wersji zmiennoprzecinkowych](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Znane problemy

1. Opcja `Migrate packages.config to PackageReference...` nie jest dostępna w menu kontekstowym po kliknięciu prawym przyciskiem myszy 

#### <a name="issue"></a>Problem 
 
Po pierwszym otwarciu projektu, pakiet NuGet może nie zostać zainicjowany do momentu wykonania operacji NuGet. Powoduje to, że opcja migracji nie jest wyświetlana w menu kontekstowym prawym przyciskiem myszy w `packages.config` lub `References`. 

#### <a name="workaround"></a>Obejście 

Wykonaj jedną z następujących akcji NuGet: 
* Otwórz interfejs użytkownika Menedżera pakietów — kliknij prawym przyciskiem myszy `References` a następnie wybierz `Manage NuGet Packages...` 
* Otwórz konsolę Menedżera pakietów — w obszarze `Tools > NuGet Package Manager`wybierz pozycję `Package Manager Console` 
* Uruchom przywracanie NuGet — kliknij prawym przyciskiem myszy węzeł rozwiązania w Eksplorator rozwiązań a następnie wybierz pozycję `Restore NuGet Packages` 
* Kompiluj projekt, który również wyzwala przywracanie NuGet 

Teraz powinno być możliwe sprawdzenie opcji migracji. Należy zauważyć, że ta opcja nie jest obsługiwana i nie będzie wyświetlana dla ASP.NET C++ i typów projektów. 

## <a name="migration-steps"></a>Kroki migracji

> [!Note]
> Przed rozpoczęciem migracji program Visual Studio tworzy kopię zapasową projektu, aby umożliwić [wycofanie pliku Packages. config](#how-to-roll-back-to-packagesconfig) w razie potrzeby.

1. Otwórz rozwiązanie zawierające projekt przy użyciu `packages.config`.

1. W **Eksplorator rozwiązań**kliknij prawym przyciskiem myszy węzeł **odwołania** lub plik `packages.config` i wybierz polecenie **Migruj pakiety. config do PackageReference...** .

1. Migrator analizuje odwołania do pakietu NuGet projektu i podejmuje próbę skategoryzowania ich do **zależności najwyższego poziomu** (pakiety NuGet zainstalowane bezpośrednio) i **zależności przechodnie** (pakiety, które zostały zainstalowane jako zależności pakietów najwyższego poziomu).

   > [!Note]
   > PackageReference obsługuje przechodnie przywracanie pakietów i dynamiczne Rozwiązywanie zależności, co oznacza, że zależności przechodnie nie muszą być instalowane jawnie.

1. Obowiązkowe Można traktować pakiet NuGet sklasyfikowany jako zależność przechodnią jako zależność najwyższego poziomu, wybierając opcję **najwyższego poziomu** dla pakietu. Ta opcja jest ustawiana automatycznie dla pakietów zawierających zasoby, które nie przepływy przechodnie (te w folderach `build`, `buildCrossTargeting`, `contentFiles`lub `analyzers`) i są oznaczone jako zależność deweloperskia (`developmentDependency = "true"`).

1. Przejrzyj wszelkie [problemy ze zgodnością pakietu](#package-compatibility-issues).

1. Wybierz **przycisk OK** , aby rozpocząć migrację.

1. Po zakończeniu migracji program Visual Studio udostępnia raport ze ścieżką do kopii zapasowej, listę zainstalowanych pakietów (zależności najwyższego poziomu), listę pakietów przywoływanych jako zależności przechodnie oraz listę problemów ze zgodnością zidentyfikowaną na początku migracji. Raport jest zapisywany w folderze kopii zapasowej.

1. Sprawdź, czy rozwiązanie zostało skompilowane i uruchomione. Jeśli wystąpią problemy, należy [rozwiązać problem w serwisie GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Jak przywrócić pakiet Packages. config

1. Zamknij zmigrowany projekt.

1. Skopiuj plik projektu i `packages.config` z kopii zapasowej (zazwyczaj `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) do folderu projektu. Usuń folder obj, jeśli istnieje w katalogu głównym projektu.

1. Otwórz projekt.

1. Otwórz konsolę Menedżera pakietów przy użyciu **narzędzi > Menedżer pakietów NuGet > menu konsoli Menedżera** pakietów.

1. Uruchom następujące polecenie w konsoli programu:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Utwórz pakiet po migracji

Po zakończeniu migracji zalecamy dodanie odwołania do pakietu NuGet [NuGet. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) , a następnie użycie programu [MSBuild-t:Pack](../reference/msbuild-targets.md#pack-target) w celu utworzenia pakietu. Chociaż w niektórych scenariuszach można używać `dotnet.exe pack` zamiast `msbuild -t:pack`, nie jest to zalecane.

## <a name="package-compatibility-issues"></a>Problemy ze zgodnością pakietu

Niektóre aspekty obsługiwane w pakietach Package. config nie są obsługiwane w programie PackageReference. Migrator analizuje i wykrywa te problemy. Każdy pakiet, który ma co najmniej jeden z następujących problemów, może nie zachowywać się zgodnie z oczekiwaniami po migracji.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>skrypty "Install. ps1" są ignorowane, gdy pakiet zostanie zainstalowany po zakończeniu migracji

| | |
| --- | --- |
| **Opis** | Przy użyciu PackageReference Zainstaluj. ps1 i Odinstaluj. ps1 skrypty PowerShell nie są wykonywane podczas instalowania lub odinstalowywania pakietu. |
| **Potencjalny wpływ** | Pakiety, które są zależne od tych skryptów, aby skonfigurować zachowanie w projekcie docelowym, mogą nie funkcjonować zgodnie z oczekiwaniami. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>zasoby "Content" nie są dostępne, gdy pakiet zostanie zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Elementy zawartości w folderze `content` pakietu nie są obsługiwane w programie PackageReference i są ignorowane. PackageReference dodaje obsługę `contentFiles` w celu uzyskania lepszej obsługi przechodniej i zawartości udostępnionej.  |
| **Potencjalny wpływ** | Zasoby w `content` nie są kopiowane do projektu i kodu projektu, które są zależne od obecności tych zasobów, wymagają refaktoryzacji.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Przekształcenia XDT nie są stosowane, gdy pakiet zostanie zainstalowany po uaktualnieniu

| | |
| --- | --- |
| **Opis** | Przekształcenia XDT są nieobsługiwane w przypadku PackageReference i pliki `.xdt` są ignorowane podczas instalowania lub odinstalowywania pakietu.   |
| **Potencjalny wpływ** | Przekształcenia XDT nie są stosowane do żadnych plików XML projektu, najczęściej `web.config.install.xdt` i `web.config.uninstall.xdt`, co oznacza, że plik` web.config` projektu nie zostanie zaktualizowany po zainstalowaniu lub odinstalowaniu pakietu. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Zestawy w katalogu głównym lib są ignorowane, gdy pakiet zostanie zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | W przypadku PackageReference zestawy znajdujące się w katalogu głównym folderu `lib` bez podfolderu specyficznego dla platformy docelowej są ignorowane. Pakiet NuGet szuka podfolderu pasującego do krótkiej nazwy platformy docelowej (TFM) odpowiadającej platformie docelowej projektu i instaluje pasujące zestawy do projektu. |
| **Potencjalny wpływ** | Pakiety, które nie mają podfolderu pasującego do monikera platformy docelowej (TFM) odpowiadające platformie docelowej projektu, mogą nie zachowywać się zgodnie z oczekiwaniami po przejściu lub nieudanej instalacji podczas migracji |

## <a name="found-an-issue-report-it"></a>Znaleziono problem? Zgłoś!

Jeśli wystąpi problem ze środowiska migracji, należy [rozwiązać problem w repozytorium GitHub usługi NuGet](https://github.com/NuGet/Home/issues/).
