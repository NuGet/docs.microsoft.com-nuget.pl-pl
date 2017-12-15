---
title: Polecenie help NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Dokumentacja dotycząca nuget.exe polecenie Pomoc"
keywords: Dokumentacja pomocy nuget, polecenie Pomoc
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>Pomoc lub? polecenia (NuGet CLI)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Przedstawia ogólne informacje i pomoc dotyczącą określonego polecenia.

## <a name="usage"></a>Użycie

```
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
| ConfigFile | *(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla samo polecenie Pomoc. |
| Język znaczników markdown | Drukowanie szczegółową pomoc w formacie markdown, gdy jest używany z `-All`. W przeciwnym razie ignorowane. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
