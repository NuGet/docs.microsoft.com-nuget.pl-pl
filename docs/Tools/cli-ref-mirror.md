---
title: Polecenie dublowanie interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Informacje dotyczące polecenia dublowanie nuget.exe"
keywords: nuget duplikatu odniesienia, polecenie dublowanie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a>polecenie dublowanie (NuGet CLI)

**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** uznane za przestarzałe w wersji 3.2 +

Odzwierciedla pakiet i jego zależności z repozytoriami określonego źródła w repozytorium docelowej.

> [!NOTE]
> Aby włączyć to polecenie dla wersji NuGet przed 3.2, przejdź do [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)wybierz najnowsza stabilna wersja, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` na dysku lokalnym i Zmień nazwę `Nuget-Signed.exe` do `nuget.exe`.

## <a name="usage"></a>Użycie

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

gdzie `<packageID>` jest pakietem dotyczącą tworzenia duplikatów, lub `<configFilePath>` identyfikuje `packages.config` pliku, który zawiera listę pakietów dublowanego.

`<listUrlTarget>` Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe.

Jeśli repozytorium docelowy znajduje się na `https://machine/repo` systemem [NuGet.Server](../hosting-packages/NuGet-Server.md), listy i wypychania adresów URL będzie `https://machine/repo/nuget` i `https://machine/repo/api/v2/package`odpowiednio.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| apiKey | Klucz interfejsu API dla repozytorium docelowej. Jeśli nie występuje, określony w *%AppData%\NuGet\NuGet.Config* jest używany. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| NoCache | Zapobiega z pamięci podręcznej komputera lokalnego za pomocą pakietów NuGet. |
| Operacja | Rejestruje co będą wykonywane, ale nie wykonuje akcji; Założono powodzenie operacji wypychania. |
| Wydanie wstępne | Zawiera pakiety wersji wstępnej w operacji dublowania. |
| Źródło | Lista źródła pakietów w celu utworzenia duplikatów. Jeśli nie określono żadnych źródeł, te zdefiniowane w *%AppData%\NuGet\NuGet.Config* służą przyjęty nuget.org, jeśli żaden nie jest określony. |
| Limit czasu | Określa limit czasu w sekundach, do wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Wersja | Wersja pakietu do zainstalowania. Jeśli nie zostanie określony, jest dublowany najnowszej wersji. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
