---
title: Polecenie listy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia nuget.exe list
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780060"
---
# <a name="list-command-nuget-cli"></a>list — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie

Wyświetla listę pakietów z danego źródła. Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w globalnym pliku konfiguracji `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` ,. Jeśli `NuGet.Config` nie określa żadnych źródeł, program `list` używa domyślnego kanału informacyjnego (NuGet.org).

## <a name="usage"></a>Użycie

```cli
nuget list [search terms] [options]
```

gdzie opcjonalne terminy wyszukiwania będą filtrować listę wyświetlaną. [Terminy wyszukiwania](../../consume-packages/finding-and-choosing-packages.md#search-syntax) są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie NuGet.org. 

## <a name="options"></a>Opcje

- **`-AllVersions`**

  Wyświetl listę wszystkich wersji pakietu. Domyślnie zostanie wyświetlona tylko Najnowsza wersja pakietu.

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-IncludeDelisted`**

  *(3.2 +)* Wyświetlanie pakietów nieznajdujących się na liście.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-PreRelease`**

  Zawiera pakiety wersji wstępnej znajdujące się na liście.

- **`-Source`**

  Źródło pakietu do przeszukania. Można określić wiele źródeł przy użyciu `-Source` opcji wiele razy.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

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
