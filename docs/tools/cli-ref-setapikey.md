---
title: Polecenie setapikey NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia setapikey nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817687"
---
# <a name="setapikey-command-nuget-cli"></a>polecenie setapikey (NuGet CLI)

**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie

Zapisuje klucz interfejsu API dla danego adresu URL podanego serwera do `NuGet.Config` tak, aby nie trzeba wprowadzać dla kolejnych poleceń.

## <a name="usage"></a>Użycie

```cli
nuget setapikey <key> -Source <url> [options]
```

gdzie `<source>` identyfikuje serwer i `<key>` to klucz lub hasło, aby zapisać. Jeśli `<source>` jest pominięty, zakłada nuget.org.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
