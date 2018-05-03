---
title: Polecenie aktualizacji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia update nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a>polecenie aktualizacji (NuGet CLI)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie

Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do ich najnowszej dostępnej wersji. Zalecane jest uruchomienie ["Przywracanie"](cli-ref-restore.md) przed uruchomieniem `update`. (Aby poszczególnych pakiet aktualizacji, należy użyć [ `nuget install` ](cli-ref-install.md) bez określania numeru wersji, w których wielkość NuGet instaluje najnowszą wersję.)

Uwaga: `update` nie działa z systemem w obszarze Mono (Mac OS x lub Linux) lub gdy w formacie PackageReference interfejsu wiersza polecenia.

`update` Polecenie aktualizuje również odwołania do zestawów w pliku projektu, pod warunkiem tych odwołuje się do już istnieje. Jeśli zaktualizowany pakiet został dodany zestaw, jest nowe odwołanie *nie* dodane. Nowe zależności pakietów również nie ma ich dodać odwołania do zestawów. Aby uwzględnić te operacje w ramach aktualizacji, należy zaktualizować pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.

To polecenie można także zaktualizować nuget.exe się przy użyciu *-self* flagi.

## <a name="usage"></a>Użycie

```cli
nuget update <configPath> [options]
```

gdzie `<configPath>` identyfikuje albo `packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| FileConflictAction | Określa akcję wykonywaną po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt. Wartości są *zastępowania, zignorować, Brak*. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Id | Określa listę identyfikatorów do zaktualizowania pakietu. |
| MSBuildPath | *(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia. Obsługiwane wartości to 4, 12, 14, 15. Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Wydanie wstępne | Umożliwia aktualizacji do wersji wstępnej. Ta flaga nie jest wymagana podczas aktualizowania pakiety wersji wstępnej, które są już zainstalowane. |
| RepositoryPath | Określa folder lokalny, w którym są zainstalowane pakiety. |
| Bezpieczne | Określa, że tylko aktualizacje o najwyższej dostępne w ramach tej samej wersji głównej i pomocniczej wersji zgodnie z zainstalowanym pakietem zostanie zainstalowana. |
| Samodzielnie | Nuget.exe aktualizacji do najnowszej wersji; wszystkie inne argumenty są ignorowane. |
| Źródło | Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby aktualizacji. W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md). |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |
| Wersja | W przypadku użycia z jeden identyfikator pakietu, określa wersję pakietu do zaktualizowania. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
