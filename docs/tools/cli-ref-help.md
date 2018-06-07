---
title: Polecenie help NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe polecenie Pomoc
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818259"
---
# <a name="help-or--command-nuget-cli"></a>help or ? command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Przedstawia ogólne informacje i pomoc dotyczącą określonego polecenia.

## <a name="usage"></a>Użycie

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

gdzie [polecenie] identyfikuje danego polecenia, do których chcesz wyświetlić Pomoc.

> [!Warning]
> W niektórych poleceniach zachować ostrożność, aby określić *pomocy* pierwszy jako z `nuget help install`, ponieważ istnieje pakiet o nazwie "help" w nuget.org. Jeśli polecenie `nuget install help`, nie będzie uzyskać pomoc dotyczącą polecenia instalacji, ale zamiast tego zostanie zainstalowany pakiet o nazwie pomocy.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Wszystkie | Drukowanie szczegółową pomoc dla dostępnych poleceń; ignorowane, jeśli podano określonego polecenia. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla samo polecenie Pomoc. |
| Język znaczników markdown | Drukowanie szczegółową pomoc w formacie markdown, gdy jest używany z `-All`. W przeciwnym razie ignorowane. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
