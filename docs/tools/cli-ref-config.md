---
title: Polecenie konfiguracji interfejsu wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń konfiguracji nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546481"
---
# <a name="config-command-nuget-cli"></a>polecenie config (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkich &bullet; **obsługiwane wersje**: wszystkie

Pobiera lub ustawia wartości konfiguracji NuGet. Aby uzyskać dodatkowe użycie, zobacz [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md). Szczegółowe informacje dotyczące dopuszczalny rozmiar nazwy kluczy, można znaleźć [odwołanie do pliku config NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Użycie

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

gdzie `<name>` i `<value>` określ parę klucz wartość należy ustawić w konfiguracji. Można określić dowolną liczbę par zgodnie z potrzebami. Aby usunąć wartość, określ nazwę i `=` logowania, ale bez wartości.

Dopuszczalny rozmiar klucza nazwy opisano w artykule [odwołanie do pliku config NuGet](../reference/nuget-config-file.md).

W pakiecie NuGet 3.4 + `<value>` służy [zmienne środowiskowe](cli-ref-environment-variables.md).

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| AsPath | Zwraca wartość konfiguracji w postaci ścieżki, ignorowane, gdy `-Set` jest używany. |
| ConfigFile | Plik konfiguracyjny NuGet do zmodyfikowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla Pomoc dla polecenia. |
| NonInteractive | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

### <a name="examples"></a>Przykłady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
