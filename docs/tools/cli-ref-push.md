---
title: Polecenie wypychania NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia wypychania nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817194"
---
# <a name="push-command-nuget-cli"></a>polecenie wypychania (NuGet CLI)

**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie; 4.1.0+ wymagane dla nuget.org

> [!Important]
> Aby wysyłać pakietów do nuget.org należy użyć nuget.exe v4.1.0 +, która implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).

Wypychanie pakietu do źródła pakietu i publikuje ją.

Konfiguracja domyślna NuGet są uzyskiwane przez załadowanie `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux), następnie ładowania żadnych `Nuget.Config` lub `.nuget\Nuget.Config` pliki, począwszy od katalogu głównego dysku i kończący się w bieżącym katalogu (zobacz [Konfigurowanie Zachowanie NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Użycie

```cli
nuget push <packagePath> [options]
```

gdzie `<packagePath>` identyfikuje pakiet do serwera.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| apiKey | Klucz interfejsu API dla repozytorium docelowej. Jeśli nie istnieje określony w pliku konfiguracji jest używany. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| DisableBuffering | Wyłącza buforowanie przypadku wypychania do serwera HTTP (s), aby zmniejszyć użycia pamięci. Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie działać. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| NoSymbols | *(3.5 +)*  Jeśli istnieje pakietu symboli, nie zostanie on przekazany do serwera symboli. |
| Źródło | Określa adres URL serwera. NuGet identyfikuje UNC lub lokalny folder źródłowy i po prostu kopiuje plik zamiast wypychanie go przy użyciu protokołu HTTP.  Ponadto, począwszy od NuGet 3.4.2, jest to parametr obowiązkowy chyba że `NuGet.Config` plik Określa *DefaultPushSource* wartość (zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Określa adres URL serwera symboli; nuget.smbsrc.net jest używana w przypadku wypychania w nuget.org |
| SymbolApiKey | *(3.5 +)*  Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`. |
| Limit czasu | Określa limit czasu w sekundach, do wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
