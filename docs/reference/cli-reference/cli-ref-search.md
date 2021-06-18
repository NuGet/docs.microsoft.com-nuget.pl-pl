---
title: Polecenie wyszukiwania interfejsu wiersza polecenia nuGet
description: Odwołanie do polecenia nuget.exe wyszukiwania
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323664"
---
# <a name="search-command-nuget-cli"></a>search , polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy: zużycie** pakietu &bullet; **Obsługiwane wersje:** 5.8+

Wyszukuje dane źródło przy użyciu podanego ciągu zapytania. Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w %AppData%\NuGet\NuGet.Config są używane.

## <a name="usage"></a>Użycie

```cli
nuget search [search terms] [options]
```

gdzie terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów tak samo, jak w przypadku używania ich w nuget.org.

## <a name="options"></a>Opcje

| Nazwa | Opis | Użycie |
| ---  |     ---     |  :-:  |
| Wstępną | Pakiety wersji wstępnej nie są domyślnie uwzględniane, ale mogą zostać dołączone przy użyciu tego argumentu | -PreRelease |
| Element źródłowy | Określone źródła pakietów do wyszukiwania zamiast wykonywania zapytań o domyślne źródła w __nuget.config__ | -Źródło `<Source URL>`|
| Take | Liczba wyników do zwrócenia. Wartość domyślna to 20. | -Take `<positive integer>` |
| Szczegółowość | Poziom szczegółowości do wyświetlenia w danych wyjściowych. Wartość domyślna to _normalna_. (Patrz uwaga poniżej)  | -Poziom szczegółowości `<quiet|normal|detailed>` |
| Help | Wyświetla informacje pomocy dotyczące polecenia | - Pomoc |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

> [!NOTE] 
> Poziomy szczegółowości:
> * _quiet_ — identyfikator pakietu, wersja
> * _normal_ — identyfikator pakietu, wersja, pliki do pobrania, wersja zapoznawcza opisu
> * _szczegółowe_ — identyfikator pakietu, wersja, pliki do pobrania, pełny opis, inne informacje, takie jak adres URL zapytania

## <a name="examples"></a>Przykłady

Wyszukaj pakiety *związane z rejestrowaniem* z domyślnych źródeł:
```
nuget search logging
```
Wyszukaj pakiety *związane z* rejestrowaniem ze szczegółowymi informacjami:
```
nuget search logging -Verbosity detailed
```
Wyszukaj pakiety *związane z* rejestrowaniem i wyświetl tylko 5 najlepszych wyników:
```
nuget search logging -Take 5
```
Wyszukaj pakiety *związane z kodem JSON,* w tym wersje wstępne, z określonego źródła/źródła danych:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Wyszukaj pakiety *związane z JSON* z wielu źródeł/źródeł danych:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
