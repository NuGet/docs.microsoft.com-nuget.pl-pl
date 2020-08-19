---
title: Polecenie aktualizacji interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe Update — polecenie
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 84f939188ac190f6d539f8ee2b422049a274f178
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622580"
---
# <a name="update-command-nuget-cli"></a>Update — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje** pakietów: wszystkie

Aktualizuje wszystkie pakiety w projekcie (przy użyciu programu `packages.config` ) do ich najnowszych dostępnych wersji. Zaleca się uruchomienie funkcji ["Restore"](cli-ref-restore.md) przed uruchomieniem narzędzia `update` . (Aby zaktualizować pojedynczy pakiet, użyj [`nuget install`](cli-ref-install.md) bez określenia numeru wersji, w którym przypadku pakiet NuGet instaluje najnowszą wersję).

Uwaga: `update` program nie współpracuje z interfejsem wiersza polecenia w systemie mono (Mac OSX lub Linux) lub w przypadku korzystania z formatu PackageReference.

`update`Polecenie aktualizuje również odwołania do zestawu w pliku projektu, pod warunkiem, że te odwołania już istnieją. Jeśli zaktualizowany pakiet ma dodany zestaw, nowe odwołanie *nie* zostanie dodane. Nowe zależności pakietu nie mają również dodanych odwołań do zestawów. Aby uwzględnić te operacje w ramach aktualizacji, zaktualizuj pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.

To polecenie służy również do aktualizowania nuget.exe samego siebie przy użyciu flagi *-Auto* .

## <a name="usage"></a>Użycie

```cli
nuget update <configPath> [options]
```

gdzie `<configPath>` identyfikuje `packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Określa domyślną akcję, gdy plik z pakietu już istnieje w projekcie docelowym. Ustaw, aby `Overwrite` zawsze zastępowały pliki. Ustaw, aby `Ignore` pominąć pliki.

  Akcja domyślnie wyświetli monit o podanie `PromptUser` każdego pliku powodującego konflikt, chyba że `OverwriteAll` lub `IgnoreAll` nie zostanie podany, który zostanie zastosowany do wszystkich pozostałych plików.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-Id`**

  Określa listę identyfikatorów pakietów do zaktualizowania.

- **`-MSBuildPath`**

  *(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo przed `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-PreRelease`**

  Umożliwia aktualizację wersji wstępnych. Ta flaga nie jest wymagana podczas aktualizacji pakietów wersji wstępnej, które są już zainstalowane.

- **`-RepositoryPath`**

  Określa folder lokalny, w którym są zainstalowane pakiety.

- **`-Safe`**

  Określa, że zostaną zainstalowane tylko aktualizacje o najwyższej wersji dostępnej w ramach tej samej wersji głównej i pomocniczej co zainstalowany pakiet.

- **`-Self`**

  Aktualizuje nuget.exe do najnowszej wersji; wszystkie pozostałe argumenty są ignorowane.

- **`-Source`**

  Określa listę źródeł pakietów (jako adresy URL), które mają być używane na potrzeby aktualizacji. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

- **`-Version`**

  W przypadku użycia z jednym IDENTYFIKATORem pakietu określa wersję pakietu do zaktualizowania.

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
