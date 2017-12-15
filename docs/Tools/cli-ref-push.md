---
title: Polecenie wypychania interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Informacje dotyczące polecenia wypychania nuget.exe"
keywords: "Odwołanie do wypychania nuget, polecenie wypychania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>polecenie wypychania (NuGet CLI)

**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie; 4.1.0+ wymagane dla nuget.org

> [!Important]
> Aby wysyłać pakietów do nuget.org należy użyć nuget.exe v4.1.0 +, która implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).

Wypychanie pakietu do źródła pakietu i publikuje ją.

NuGet domyślnej konfiguracji są uzyskiwane przez ładowanie `%AppData%\NuGet\NuGet.Config`, a następnie ładowania `Nuget.Config` lub `.nuget\Nuget.Config` pliki, począwszy od katalogu głównego dysku i kończący się w bieżącym katalogu (zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Użycie

```
nuget push <packagePath> [options]
```

gdzie `<packagePath>` identyfikuje pakiet do serwera.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| apiKey | Klucz interfejsu API dla repozytorium docelowej. Jeśli nie występuje, określony w *%AppData%\NuGet\NuGet.Config* jest używany. |
| ConfigFile | *(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| DisableBuffering | Wyłącza buforowanie przypadku wypychania do serwera HTTP (s), aby zmniejszyć użycia pamięci. Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie działać. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| NoSymbols | *(3.5 +)*  Jeśli istnieje pakietu symboli, nie zostanie on przekazany do serwera symboli. |
| Źródło | Określa adres URL serwera. Nuget 2.5 + NuGet zidentyfikować UNC lub lokalny folder źródłowy i wystarczy skopiować plik zamiast wypychanie go przy użyciu protokołu HTTP.  Ponadto, począwszy od NuGet 3.4.2, jest to parametr obowiązkowy chyba że `NuGet.Config` plik Określa *DefaultPushSource* wartość (zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md)). |
| SymbolSource | *(3.5 +)*  Określa adres URL serwera symboli; nuget.smbsrc.net jest używana w przypadku wypychania w nuget.org |
| SymbolApiKey | *(3.5 +)*  Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`. |
| Limit czasu | Określa limit czasu w sekundach, do wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
