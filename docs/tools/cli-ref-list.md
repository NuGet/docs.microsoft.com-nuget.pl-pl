---
title: Interfejs wiersza polecenia NuGet lista — polecenie
description: Dokumentacja dotycząca polecenia nuget.exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549804"
---
# <a name="list-command-nuget-cli"></a>Lista, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** zużycie pakietów, publikowania &bullet; **obsługiwane wersje:** wszystkie

Wyświetla listę pakietów z danego źródła. Jeśli nie określono żadnych źródeł, wszystkich źródeł są zdefiniowane w pliku konfiguracji globalnej `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config`, są używane. Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).

## <a name="usage"></a>Użycie

```cli
nuget list [search terms] [options]
```

gdzie opcjonalne wyszukiwane terminy będą odfiltrowania wyświetlonej listy. Wyszukiwane terminy są stosowane do nazw pakietów, tagi i opisy pakietu, tak jak podczas korzystania z nich w witrynie nuget.org.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AllVersions | Wyświetla listę wszystkich wersji pakietu. Domyślnie jest wyświetlana tylko najnowszą wersję pakietu. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| IncludeDelisted | *(3.2 +)*  Wyświetlić nieznajdujące się na liście pakietów. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Wersja wstępna | Obejmuje pakiety w wersjach wstępnych, na liście. |
| Źródło | Określa listę źródeł pakietów do wyszukania. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
