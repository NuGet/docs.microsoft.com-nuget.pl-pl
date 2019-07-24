---
title: Polecenie pomocy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia pomocy NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328343"
---
# <a name="help-or--command-nuget-cli"></a>help or ? command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Wyświetla ogólne informacje pomocy i informacje pomocy dotyczące określonych poleceń.

## <a name="usage"></a>Użycie

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

gdzie [polecenie] identyfikuje konkretne polecenie, dla którego ma zostać wyświetlona pomoc.

> [!Warning]
> W przypadku niektórych poleceń należy zastanowić  się, jak w `nuget help install`pierwszej kolejności określić pomoc, ponieważ istnieje pakiet o nazwie "Help" w witrynie NuGet.org. Jeśli połączysz polecenie `nuget install help`, nie otrzymasz pomocy dotyczącej polecenia install, ale zamiast tego zainstalujemy pakiet o nazwie help.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Wszystkie | Drukuj szczegółową pomoc dotyczącą wszystkich dostępnych poleceń; ignorowany, jeśli podano określone polecenie. |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dotyczące samego polecenia pomocy. |
| Markdown | Drukuj szczegółową pomoc w formacie promocji w przypadku `-All`korzystania z programu. Zignorowane w przeciwnym razie. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
