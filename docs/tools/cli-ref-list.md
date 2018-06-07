---
title: Lista interfejsu wiersza polecenia NuGet — polecenie
description: Informacje dotyczące polecenia listy nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818441"
---
# <a name="list-command-nuget-cli"></a>Lista polecenia (NuGet CLI)

**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie

Wyświetla listę pakietów z danego źródła. Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w pliku konfigurację globalną `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config`, są używane. Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).

## <a name="usage"></a>Użycie

```cli
nuget list [search terms] [options]
```

gdzie terminy wyszukiwania opcjonalne będzie odfiltrowania wyświetlonej listy. Terminy wyszukiwania są stosowane do nazwy pakietów, znaczników i opisy pakietu, tak jak za pomocą ich nuget.org.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AllVersions | Wyświetl listę wszystkich wersji pakietu. Domyślnie wyświetlane jest tylko najnowszą wersję pakietu. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| IncludeDelisted | *(3.2 +)*  Wyświetlanie nieznajdujące się na liście pakietów. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Wydanie wstępne | Zawiera pakiety wersji wstępnej na liście. |
| Źródło | Określa listę źródła pakietów do wyszukiwania. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
