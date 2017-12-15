---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Informacje dotyczące polecenia konfiguracyjnego nuget.exe"
keywords: "Odwołanie do konfiguracji nuget, config, polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 12a8b51dd11b9bc3a496e02e869cdeb95e67b9e3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="config-command-nuget-cli"></a>polecenie konfiguracji (NuGet CLI)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Pobiera lub ustawia wartości konfiguracji NuGet. Aby uzyskać dodatkowe obciążenie, zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md). Szczegółowe informacje dotyczące nazwami kluczy, zapoznaj się [odwołania do pliku config NuGet](../Schema/nuget-config-file.md).

## <a name="usage"></a>Użycie

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

gdzie `<name>` i `<value>` określ parę klucz wartość można ustawić w konfiguracji. Można określić dowolną liczbę par zgodnie z potrzebami. Aby usunąć wartość, określ nazwę i `=` logowania, ale żadnej wartości.

W NuGet 3.4 + `<value>` można użyć [zmiennych środowiskowych](cli-ref-environment-variables.md).

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AsPath | Zwraca wartość konfiguracji jako ścieżka, zignorowane, kiedy `-Set` jest używany. |
| ConfigFile | *(2.5 +)*  NuGet pliku konfiguracji do zmodyfikowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

### <a name="examples"></a>Przykłady

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
