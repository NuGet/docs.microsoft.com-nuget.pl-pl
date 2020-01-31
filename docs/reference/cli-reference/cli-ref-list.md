---
title: Polecenie listy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia list NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813341"
---
# <a name="list-command-nuget-cli"></a>list — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Wyświetla listę pakietów z danego źródła. Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w pliku konfiguracji globalnej, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config`. Jeśli `NuGet.Config` nie określa żadnych źródeł, `list` używa domyślnego kanału informacyjnego (nuget.org).

## <a name="usage"></a>Pomiar

```cli
nuget list [search terms] [options]
```

gdzie opcjonalne terminy wyszukiwania będą filtrować listę wyświetlaną. Terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie nuget.org.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AllVersions | Wyświetl listę wszystkich wersji pakietu. Domyślnie zostanie wyświetlona tylko Najnowsza wersja pakietu. |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla informacje pomocy dla polecenia. |
| IncludeDelisted | *(3.2 +)* Wyświetlanie pakietów nieznajdujących się na liście. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| PreRelease | Zawiera pakiety wersji wstępnej znajdujące się na liście. |
| Obiekt źródłowy | Określa listę źródeł pakietów do wyszukania. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

Wyświetl listę wszystkich pakietów ze skonfigurowanych źródeł:
```
nuget list
```
Wyświetl listę pakietów związanych z platformą Azure z szczegółowym szczegółowośćem:
```
nuget list Azure -Verbosity detailed
```
Wyświetl listę wszystkich wersji pakietów związanych z platformą Azure ze skonfigurowanych kanałów informacyjnych:
```
nuget list Azure -AllVersions
```
Wyświetl listę wszystkich wersji pakietów związanych z notacją JSON z określonego źródła/kanału informacyjnego:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Wyświetlanie listy pakietów związanych z notacją JSON z wielu źródeł/źródeł:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

