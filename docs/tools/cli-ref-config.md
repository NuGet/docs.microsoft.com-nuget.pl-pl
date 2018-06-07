---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia konfiguracyjnego nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818168"
---
# <a name="config-command-nuget-cli"></a>polecenie konfiguracji (NuGet CLI)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Pobiera lub ustawia wartości konfiguracji NuGet. Aby uzyskać dodatkowe obciążenie, zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md). Szczegółowe informacje dotyczące nazwami kluczy, zapoznaj się [odwołania do pliku config NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Użycie

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

gdzie `<name>` i `<value>` określ parę klucz wartość można ustawić w konfiguracji. Można określić dowolną liczbę par zgodnie z potrzebami. Aby usunąć wartość, określ nazwę i `=` logowania, ale żadnej wartości.

Dopuszczalne nazw kluczy, zobacz [odwołania do pliku config NuGet](../reference/nuget-config-file.md).

W NuGet 3.4 + `<value>` można użyć [zmiennych środowiskowych](cli-ref-environment-variables.md).

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AsPath | Zwraca wartość konfiguracji jako ścieżka, zignorowane, kiedy `-Set` jest używany. |
| ConfigFile | Plik konfiguracji NuGet do zmodyfikowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

### <a name="examples"></a>Przykłady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
