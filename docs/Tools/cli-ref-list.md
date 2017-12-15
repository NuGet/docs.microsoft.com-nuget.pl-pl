---
title: Polecenie listy interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Informacje dotyczące polecenia listy nuget.exe"
keywords: "Odwołanie do listy nuget, lista pakietów — polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>Lista polecenia (NuGet CLI)

**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie

Wyświetla listę pakietów z danego źródła. Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w pliku konfigurację globalną `%AppData%\NuGet\NuGet.Config`, są używane. Jeśli `NuGet.Config` określa żadnych źródeł, następnie `list` korzysta z domyślnego źródła danych (nuget.org).

## <a name="usage"></a>Użycie

```
nuget list [search terms] [options]
```

gdzie terminy wyszukiwania opcjonalne będzie odfiltrowania wyświetlonej listy. Terminy wyszukiwania są stosowane do nazwy pakietów, znaczników i opisy pakietu.

## <a name="options"></a>Opcje
| Opcja | Opis |
| --- | --- |
| AllVersions | Wyświetl listę wszystkich wersji pakietu. Domyślnie wyświetlane jest tylko najnowszą wersję pakietu. |
| ConfigFile | *(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| IncludeDelisted | *(3.2 +)*  Wyświetlanie nieznajdujące się na liście pakietów. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Wydanie wstępne | Zawiera pakiety wersji wstępnej na liście. |
| Źródło | Określa listę źródła pakietów do wyszukiwania. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
