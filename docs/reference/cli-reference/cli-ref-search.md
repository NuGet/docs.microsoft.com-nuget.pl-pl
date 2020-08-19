---
title: Polecenie wyszukiwania interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia Search
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623270"
---
# <a name="search-command-nuget-cli"></a>Search — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje pakietów:** 5.8 +

Wyszukuje dane źródło przy użyciu podanego ciągu zapytania. Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w% AppData% \NuGet\NuGet.config.

## <a name="usage"></a>Użycie

```cli
nuget search [search terms] [options]
```

gdzie terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie nuget.org.

## <a name="options"></a>Opcje

| Nazwa | Opis | Użycie |
| ---  |     ---     |  :-:  |
| Wersja wstępna | Pakiety wersji wstępnej nie są uwzględniane domyślnie, ale mogą być dołączane za pomocą tego argumentu | -Wersja wstępna |
| Element źródłowy | Określone źródła pakietów do przeszukania zamiast wysyłania zapytań do domyślnych źródeł w __nuget.config__ | -Źródło `<Source URL>`|
| Take | Liczba wyników do zwrócenia. Wartość domyślna to 20. | -Zrób `<positive integer>` |
| Szczegółowość | Poziom szczegółowości, który ma być wyświetlany w danych wyjściowych. Wartość domyślna to _normalny_. (Zobacz uwagi poniżej)  | -Poziom szczegółowości `<quiet\|normal\|detailed>` |
| Pomoc | Wyświetla informacje pomocy dla polecenia | -Pomoc |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

__UWAGA__

Poziomy szczegółowości:

* _cichy_ — identyfikator pakietu, wersja
* _normalny_ — identyfikator pakietu, wersja, pobieranie, wersja zapoznawcza opisu
* _szczegółowy_ — identyfikator pakietu, wersja, pobieranie, pełny opis, inne informacje, takie jak adres URL zapytania

## <a name="examples"></a>Przykłady

Wyszukaj pakiety powiązane z *rejestrowaniem*ze źródeł domyślnych:
```
nuget search logging
```
Wyszukaj pakiety związane z *rejestrowaniem*ze szczegółowym szczegółowośćem:
```
nuget search logging -Verbosity detailed
```
Wyszukaj pakiety związane z *rejestrowaniem*i Pokaż tylko 5 najważniejszych wyników:
```
nuget search logging -Take 5
```
Wyszukaj pakiety powiązane ze standardem *JSON*, w tym wersje wstępne, z określonych źródeł/źródła danych:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Wyszukaj pakiety powiązane ze standardem *JSON*z wielu źródeł/źródeł:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
