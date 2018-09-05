---
title: Interfejs wiersza polecenia NuGet polecenia Pomoc
description: Dokumentacja dotycząca pomocy polecenia nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546566"
---
# <a name="help-or--command-nuget-cli"></a>help or ? command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkich &bullet; **obsługiwane wersje**: wszystkie

Wyświetla ogólne informacje i pomoc dotyczącą określonego polecenia.

## <a name="usage"></a>Użycie

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

gdzie [polecenie] identyfikuje określonego polecenia, dla którego chcesz wyświetlić Pomoc.

> [!Warning]
> W niektórych poleceniach zachować ostrożność, aby określić *pomocy* najpierw, przy użyciu `nuget help install`, ponieważ pakiet o nazwie "help" w witrynie nuget.org. Jeśli nadasz polecenie `nuget install help`, nie będzie uzyskać pomoc dotyczącą polecenia instalacji, ale zamiast tego zostanie zainstalowany pakiet o nazwie pomocy.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Wszystkie | Drukuj szczegółową pomoc dotyczącą wszystkich dostępnych poleceń; ignorowane, jeśli podano określonego polecenia. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla niej samo polecenie Pomoc. |
| Markdown | Drukuj szczegółową pomoc w formacie markdown, gdy jest używane z `-All`. Ignorowany w innych przypadkach. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
