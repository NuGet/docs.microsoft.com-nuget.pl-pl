---
title: Polecenie listy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia list NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328325"
---
# <a name="list-command-nuget-cli"></a>list — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Wyświetla listę pakietów z danego źródła. Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w globalnym pliku `%AppData%\NuGet\NuGet.Config` konfiguracji (system Windows `~/.nuget/NuGet/NuGet.Config`) lub,. Jeśli `NuGet.Config` nie określa żadnych źródeł `list` , program używa domyślnego kanału informacyjnego (NuGet.org).

## <a name="usage"></a>Użycie

```cli
nuget list [search terms] [options]
```

gdzie opcjonalne terminy wyszukiwania będą filtrować listę wyświetlaną. Terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie nuget.org.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AllVersions | Wyświetl listę wszystkich wersji pakietu. Domyślnie zostanie wyświetlona tylko Najnowsza wersja pakietu. |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| IncludeDelisted | *(3.2 +)* Wyświetlanie pakietów nieznajdujących się na liście. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| PreRelease | Zawiera pakiety wersji wstępnej znajdujące się na liście. |
| Source | Określa listę źródeł pakietów do wyszukania. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
