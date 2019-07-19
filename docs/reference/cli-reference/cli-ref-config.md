---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328358"
---
# <a name="config-command-nuget-cli"></a>config — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje**: wszystkie

Pobiera lub ustawia wartości konfiguracji NuGet. Aby uzyskać dodatkowe użycie, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md). Szczegółowe informacje na temat dozwolonych nazw kluczy można znaleźć w [dokumentacji pliku konfiguracji NuGet](../nuget-config-file.md).

## <a name="usage"></a>Użycie

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

gdzie `<name>` i`<value>` określić parę klucz-wartość, która ma zostać ustawiona w konfiguracji. Można określić dowolną liczbę par. Aby usunąć wartość, określ nazwę i `=` znak, ale nie wartości.

Aby uzyskać dozwolone nazwy kluczy, zobacz [Dokumentacja pliku konfiguracji programu NuGet](../nuget-config-file.md).

W programie NuGet 3.4 + `<value>` można używać [zmiennych środowiskowych](cli-ref-environment-variables.md).

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AsPath | Zwraca wartość konfiguracji jako ścieżkę, która jest ignorowana `-Set` , gdy jest używana. |
| ConfigFile | Plik konfiguracji NuGet do zmodyfikowania. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

### <a name="examples"></a>Przykłady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
