---
title: Polecenie dublowanie NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia dublowanie nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4cec854f05fcd207bb15a50ea4ebdc201fdb3ac6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818155"
---
# <a name="mirror-command-nuget-cli"></a>mirror command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** uznane za przestarzałe w wersji 3.2 +

Odzwierciedla pakiet i jego zależności z repozytoriami określonego źródła w repozytorium docelowej.

> [!NOTE]
> Aby włączyć to polecenie dla wersji NuGet przed 3.2, przejdź do [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)wybierz najnowsza stabilna wersja, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` na dysku lokalnym i Zmień nazwę `Nuget-Signed.exe` do `nuget.exe`.

## <a name="usage"></a>Użycie

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

gdzie `<packageID>` jest pakietem dotyczącą tworzenia duplikatów, lub `<configFilePath>` identyfikuje `packages.config` pliku, który zawiera listę pakietów dublowanego.

`<listUrlTarget>` Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe.

Jeśli repozytorium docelowy znajduje się na `https://machine/repo` systemem [NuGet.Server](../hosting-packages/nuget-server.md), listy i wypychania adresów URL będzie `https://machine/repo/nuget` i `https://machine/repo/api/v2/package`odpowiednio.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| apiKey | Klucz interfejsu API dla repozytorium docelowej. Jeśli nie występuje, określony w pliku konfiguracyjnym jest używana (`%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux)). |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| NoCache | Zapobiega przy użyciu pamięci podręcznej pakietów NuGet. Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Operacja | Rejestruje co będą wykonywane, ale nie wykonuje akcji; Założono powodzenie operacji wypychania. |
| Wydanie wstępne | Zawiera pakiety wersji wstępnej w operacji dublowania. |
| Źródło | Lista źródła pakietów w celu utworzenia duplikatów. Jeśli nie określono żadnych źródeł, te zdefiniowane w pliku konfiguracyjnym (zobacz powyżej ApiKey) są używane, przyjęty nuget.org, jeśli żaden nie jest określony. |
| Limit czasu | Określa limit czasu w sekundach, do wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Wersja | Wersja pakietu do zainstalowania. Jeśli nie zostanie określony, jest dublowany najnowszej wersji. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
