---
title: Polecenie pomocy interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia pomocy
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779358"
---
# <a name="help-or--command-nuget-cli"></a>help lub ? polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Wyświetla ogólne informacje pomocy i informacje pomocy dotyczące określonych poleceń.

## <a name="usage"></a>Użycie

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

gdzie [polecenie] identyfikuje konkretne polecenie, dla którego ma zostać wyświetlona pomoc.

> [!Warning]
> W przypadku niektórych poleceń należy zastanowić się, jak w pierwszej kolejności określić *Pomoc* , `nuget help install` ponieważ istnieje pakiet o nazwie "Help" w witrynie NuGet.org. Jeśli połączysz polecenie `nuget install help` , nie otrzymasz pomocy dotyczącej polecenia install, ale zamiast tego zainstalujemy pakiet o nazwie help.

## <a name="options"></a>Opcje

- **`-All`**

  Drukuj szczegółową pomoc dotyczącą wszystkich dostępnych poleceń; ignorowany, jeśli podano określone polecenie.

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-Markdown`**

  Drukuj szczegółową pomoc w formacie promocji w przypadku korzystania z programu `-All` . Zignorowane w przeciwnym razie.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
