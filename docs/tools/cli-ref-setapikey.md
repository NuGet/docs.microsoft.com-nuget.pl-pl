---
title: Polecenie setapikey interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń setapikey nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549223"
---
# <a name="setapikey-command-nuget-cli"></a>polecenie setapikey (interfejs wiersza polecenia NuGet)

**Dotyczy:** zużycie pakietów, publikowania &bullet; **obsługiwane wersje:** wszystkie

Zapisuje klucz interfejsu API dla danego serwera adresu URL do `NuGet.Config` tak, aby nie trzeba wprowadzić używane przy kolejnych poleceniach.

## <a name="usage"></a>Użycie

```cli
nuget setapikey <key> -Source <url> [options]
```

gdzie `<source>` identyfikuje serwer i `<key>` jest klucz lub hasło, aby zapisać. Jeśli `<source>` jest pominięty, zakłada nuget.org.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
