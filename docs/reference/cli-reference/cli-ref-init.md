---
title: Polecenie init interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia init programu NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328337"
---
# <a name="init-command-nuget-cli"></a>init — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** tworzenia &bullet; pakietów: 3.3+

Kopiuje wszystkie pakiety z folderu płaskiego do folderu docelowego przy użyciu układu hierarchicznego zgodnie z opisem dla [polecenia Dodaj](cli-ref-add.md). Oznacza to, że `init` użycie jest równoważne `add` użyciu polecenia w każdym pakiecie w folderze.

Tak jak `add`w przypadku, miejsce docelowe musi być folderem lokalnym lub ścieżką UNC; Repozytoria pakietów HTTP, takie jak nuget.org lub serwery prywatne, nie są obsługiwane.

## <a name="usage"></a>Użycie

```cli
nuget init <source> <destination> [options]
```

gdzie `<source>` folder zawiera pakiety i `<destination>` jest folderem lokalnym lub ścieżką UNC, do której są kopiowane pakiety.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Expand | Dodaje wszystkie pliki w każdym pakiecie, które są dodawane do źródła pakietu; Analogicznie `-Expand` jak `add` polecenie. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
