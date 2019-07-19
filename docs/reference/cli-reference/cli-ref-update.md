---
title: Polecenie aktualizacji interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328256"
---
# <a name="update-command-nuget-cli"></a>update command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : wszystkie

Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`programu) do ich najnowszych dostępnych wersji. Zaleca się uruchomienie funkcji ["Restore"](cli-ref-restore.md) przed uruchomieniem `update`narzędzia. (Aby zaktualizować pojedynczy pakiet, użyj [`nuget install`](cli-ref-install.md) bez określenia numeru wersji, w którym przypadku pakiet NuGet instaluje najnowszą wersję).

Uwaga: `update` program nie współpracuje z interfejsem wiersza polecenia w systemie mono (Mac OSX lub Linux) lub w przypadku korzystania z formatu PackageReference.

`update` Polecenie aktualizuje również odwołania do zestawu w pliku projektu, pod warunkiem, że te odwołania już istnieją. Jeśli zaktualizowany pakiet ma dodany zestaw, nowe odwołanie *nie* zostanie dodane. Nowe zależności pakietu nie mają również dodanych odwołań do zestawów. Aby uwzględnić te operacje w ramach aktualizacji, zaktualizuj pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.

Tego polecenia można także użyć do zaktualizowania pliku NuGet. exe przy użyciu flagi *-Auto* .

## <a name="usage"></a>Użycie

```cli
nuget update <configPath> [options]
```

gdzie `<configPath>` identyfikuje`packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| FileConflictAction | Określa akcję, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt. Wartości są *zastępowane, ignorowanie, brak*. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| Id | Określa listę identyfikatorów pakietów do zaktualizowania. |
| MSBuildPath | *(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo `-MSBuildVersion`przed. |
| MSBuildVersion | *(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Wersja wstępna | Umożliwia aktualizację wersji wstępnych. Ta flaga nie jest wymagana podczas aktualizacji pakietów wersji wstępnej, które są już zainstalowane. |
| RepositoryPath | Określa folder lokalny, w którym są zainstalowane pakiety. |
| Sejf | Określa, że zostaną zainstalowane tylko aktualizacje o najwyższej wersji dostępnej w ramach tej samej wersji głównej i pomocniczej co zainstalowany pakiet. |
| Automatycznej | Aktualizuje plik NuGet. exe do najnowszej wersji; wszystkie pozostałe argumenty są ignorowane. |
| Source | Określa listę źródeł pakietów (jako adresy URL), które mają być używane na potrzeby aktualizacji. W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |
| Wersja | W przypadku użycia z jednym IDENTYFIKATORem pakietu określa wersję pakietu do zaktualizowania. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
