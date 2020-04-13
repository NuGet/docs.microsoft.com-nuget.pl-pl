---
title: Migracja z package.config do formatów PackageReference
description: Szczegółowe informacje na temat migracji projektu z formatu zarządzania package.config do packageReference obsługiwanego przez nuget 4.0+ i VS2017 oraz .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428892"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Migrowanie z package.config do PackageReference

Visual Studio 2017 w wersji 15.7 i nowszych obsługuje migracji projektu z formatu zarządzania [packages.config](../reference/packages-config.md) do formatu [PackageReference.](../consume-packages/Package-References-in-Project-Files.md)

## <a name="benefits-of-using-packagereference"></a>Korzyści z używania PackageReference

* **Zarządzaj wszystkimi zależnościami projektu w jednym miejscu:** Podobnie jak odwołania do projektu i `PackageReference` odwołania do zestawu, odwołania do pakietu NuGet (przy użyciu węzła) są zarządzane bezpośrednio w plikach projektu, a nie przy użyciu oddzielnego pliku packages.config.
* **Przejrzysty widok zależności najwyższego poziomu:** W przeciwieństwie do packages.config, PackageReference wyświetla tylko te pakiety NuGet, które zostały bezpośrednio zainstalowane w projekcie. W rezultacie interfejs użytkownika Menedżera pakietów NuGet i plik projektu nie są zaśmiecone zależnościami na poziomie down.As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.
* **Ulepszenia wydajności:** Podczas korzystania z PackageReference pakiety są przechowywane w folderze *pakietów globalnych* (zgodnie `packages` z opisem w sprawie Zarządzanie [pakietami globalnymi i folderami pamięci podręcznej,](../consume-packages/managing-the-global-packages-and-cache-folders.md) a nie w folderze w rozwiązaniu. W rezultacie PackageReference wykonuje szybciej i zużywa mniej miejsca na dysku.
* **Fine kontroli nad zależnościami i przepływem zawartości:** Za pomocą istniejących funkcji MSBuild pozwala [warunkowo odwołać się do pakietu NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) i wybrać odwołania do pakietu na platformę docelową, konfigurację, platformę lub inne przestawne.
* **PackageReference jest w trakcie aktywnego rozwoju:** Zobacz [PackageReference problemy na GitHub](https://aka.ms/nuget-pr-improvements). packages.config nie jest już w fazie aktywnego rozwoju.

### <a name="limitations"></a>Ograniczenia

* NuGet PackageReference nie jest dostępny w programie Visual Studio 2015 i wcześniejszych. Zmigrowane projekty można otwierać tylko w programie Visual Studio 2017 i nowszych.
* Migracja nie jest obecnie dostępna dla projektów języka C++ i ASP.NET.
* Niektóre pakiety mogą nie być w pełni zgodne z PackageReference. Aby uzyskać więcej informacji, zobacz [problemy ze zgodnością pakietów](#package-compatibility-issues).

Ponadto istnieją pewne różnice w sposobie działania PackageReferences w porównaniu do packages.config. Na przykład - [ograniczanie wersji uaktualnienia](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) nie jest supprted przez PackageReference, ale dodać obsługę [wersji pływających](../consume-packages/package-references-in-project-files.md#floating-versions).

### <a name="known-issues"></a>Znane problemy

1. Opcja `Migrate packages.config to PackageReference...` ta nie jest dostępna w menu kontekstowym po kliknięciu prawym przyciskiem myszy 

#### <a name="issue"></a>Problem 
 
Po pierwszym otwarciu projektu NuGet może nie zainicjować, dopóki nie zostanie wykonana operacja NuGet. Powoduje to, że opcja migracji nie jest chlubna w menu kontekstowym po kliknięciu prawym przyciskiem myszy lub `packages.config` `References`. 

#### <a name="workaround"></a>Obejście 

Wykonaj dowolną z następujących akcji NuGet: 
* Otwórz interfejs użytkownika Menedżera pakietów `References` — kliknij prawym przyciskiem myszy i wybierz pozycję`Manage NuGet Packages...` 
* Otwórz konsolę Menedżera `Tools > NuGet Package Manager`pakietów — od , wybierz`Package Manager Console` 
* Uruchom przywracanie NuGet - Kliknij prawym przyciskiem myszy węzeł rozwiązania w Eksploratorze rozwiązań i wybierz pozycję`Restore NuGet Packages` 
* Tworzenie projektu, który również wyzwala przywracanie NuGet 

Teraz powinna być widoczna opcja migracji. Należy zauważyć, że ta opcja nie jest obsługiwana i nie będzie wyświetlana dla typów projektów ASP.NET i C++. 

## <a name="migration-steps"></a>Kroki migracji

> [!Note]
> Przed rozpoczęciem migracji program Visual Studio tworzy kopię zapasową projektu, aby umożliwić [wycofanie do packages.config,](#how-to-roll-back-to-packagesconfig) jeśli to konieczne.

1. Otwórz rozwiązanie zawierające projekt `packages.config`przy użyciu programu .

1. W **Eksploratorze rozwiązań**kliknij prawym `packages.config` przyciskiem myszy węzeł **Odwołania** lub plik i wybierz pozycję **Migruj package.config do PackageReference...**.

1. Migracji analizuje odwołania do pakietu NuGet projektu i próbuje kategoryzować je do **zależności najwyższego poziomu** (pakiety NuGet, które zostały zainstalowane bezpośrednio) i **przechodnie zależności** (pakiety, które zostały zainstalowane jako zależności pakietów najwyższego poziomu).

   > [!Note]
   > PackageReference obsługuje przywracanie pakietów przechodnich i dynamicznie rozwiązuje zależności, co oznacza, że zależności przechodnie nie muszą być instalowane jawnie.

1. (Opcjonalnie) Można traktować Pakiet NuGet sklasyfikowane jako zależności przechodnie jako zależności najwyższego poziomu, wybierając opcję **najwyższego poziomu** dla pakietu. Ta opcja jest automatycznie ustawiana dla pakietów zawierających zasoby, które `build`nie `buildCrossTargeting` `contentFiles`przepływają `analyzers` przechodnie (te w folderach`developmentDependency = "true"`, , lub folderów) i pakietów oznaczonych jako zależność rozwojowa ( ).

1. Przejrzyj wszelkie [problemy ze zgodnością pakietów](#package-compatibility-issues).

1. Wybierz **przycisk OK,** aby rozpocząć migrację.

1. Na końcu migracji visual studio udostępnia raport ze ścieżką do kopii zapasowej, listę zainstalowanych pakietów (zależności najwyższego poziomu), listę pakietów, do których odwołuje się przechodnie zależności i listę problemów ze zgodnością zidentyfikowanych na początku migracji. Raport zostanie zapisany w folderze kopii zapasowej.

1. Sprawdź, czy rozwiązanie tworzy i uruchamia. Jeśli wystąpią problemy, [zgłać problem na GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Jak przywrócić plik packages.config

1. Zamknij zmigrowany projekt.

1. Skopiuj `packages.config` plik projektu i `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`z kopii zapasowej (zazwyczaj) do folderu projektu. Usuń folder obj, jeśli istnieje w katalogu głównym projektu.

1. Otwórz projekt.

1. Otwórz konsolę Menedżera pakietów za pomocą polecenia **menu Menedżer pakietów > Narzędzia NuGet > konsoli Menedżera pakietów.**

1. Uruchom następujące polecenie w konsoli:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Tworzenie pakietu po migracji

Po zakończeniu migracji zaleca się dodanie odwołania do pakietu [nuget.build.tasks.pack,](https://www.nuget.org/packages/nuget.build.tasks.pack) a następnie użycie [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) do utworzenia pakietu. Chociaż w niektórych scenariuszach można użyć `dotnet.exe pack` zamiast `msbuild -t:pack`, nie jest zalecane.

## <a name="package-compatibility-issues"></a>Problemy ze zgodnością pakietów

Niektóre aspekty, które były obsługiwane w packages.config nie są obsługiwane w PackageReference. Migrownik analizuje i wykrywa takie problemy. Każdy pakiet, który ma jeden lub więcej z następujących problemów może nie zachowywać się zgodnie z oczekiwaniami po migracji.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Skrypty "install.ps1" są ignorowane po zainstalowaniu pakietu po migracji

| | |
| --- | --- |
| **Opis** | W przypadku programu PackageReference skrypty programu Install.ps1 i uninstall.ps1 programu PowerShell nie są wykonywane podczas instalowania lub odinstalowywania pakietu. |
| **Potencjalny wpływ** | Pakiety, które zależą od tych skryptów, aby skonfigurować pewne zachowanie w projekcie docelowym może nie działać zgodnie z oczekiwaniami. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Zasoby "zawartości" nie są dostępne po zainstalowaniu pakietu po migracji

| | |
| --- | --- |
| **Opis** | Zasoby w `content` folderze pakietu nie są obsługiwane za pomocą PackageReference i są ignorowane. PackageReference dodaje `contentFiles` obsługę, aby mieć lepszą obsługę przechodnie i zawartość udostępnioną.  |
| **Potencjalny wpływ** | Zasoby w `content` nie są kopiowane do kodu projektu i projektu, który zależy od obecności tych zasobów wymaga refaktoryzacji.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Transformacje XDT nie są stosowane, gdy pakiet jest zainstalowany po uaktualnieniu

| | |
| --- | --- |
| **Opis** | Transformacje XDT nie są obsługiwane przez `.xdt` PackageReference, a pliki są ignorowane podczas instalowania lub odinstalowywania pakietu.   |
| **Potencjalny wpływ** | Transformacje XDT nie są stosowane do żadnych plików XML `web.config.uninstall.xdt`projektu, najczęściej i` web.config` , co oznacza, `web.config.install.xdt` że plik projektu nie jest aktualizowany, gdy pakiet jest zainstalowany lub odinstalowany. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Zestawy w katalogu głównym lib są ignorowane, gdy pakiet jest zainstalowany po migracji

| | |
| --- | --- |
| **Opis** | Z PackageReference, zestawy obecne w `lib` katalogu głównym folderu bez struktury docelowej określonego podfolderu są ignorowane. NuGet szuka podfolder pasujący do monikera struktury docelowej (TFM) odpowiadającego platformie docelowej projektu i instaluje pasujące zestawy w projekcie. |
| **Potencjalny wpływ** | Pakiety, które nie mają podfolderu pasującego do docelowego monikera (TFM) odpowiadającego platformom docelowym projektu, mogą nie zachowywać się zgodnie z oczekiwaniami po przejściu lub nieudanej instalacji podczas migracji |

## <a name="found-an-issue-report-it"></a>Znalazłeś problem? Zgłoś to!

Jeśli napotkasz problem z migracją, [zgłoś problem w repozytorium NuGet GitHub](https://github.com/NuGet/Home/issues/).
