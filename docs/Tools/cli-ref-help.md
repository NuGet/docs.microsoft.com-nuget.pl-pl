---
title: Polecenie help NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Dokumentacja dotycząca nuget.exe polecenie Pomoc"
keywords: Dokumentacja pomocy nuget, polecenie Pomoc
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b4255c353e412cf1d1a59590ee816b7887c90653
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="help-or--command-nuget-cli"></a>Pomoc lub? polecenia (NuGet CLI)

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
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
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
