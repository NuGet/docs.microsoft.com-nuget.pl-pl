---
title: Polecenie wypychania interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń wypychania nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a9460944e2c232e2a72195434a491d26eee3559
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877960"
---
# <a name="push-command-nuget-cli"></a>polecenie wypychania (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu publikowania &bullet; **obsługiwane wersje:** wszystkie; 4.1.0+ wymagane dla repozytorium nuget.org

> [!Important]
> Aby wypychania pakietów na stronie nuget.org należy użyć nuget.exe verze 4.1.0 +, która implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md).

Wypychanie pakietu do źródła pakietu i publikuje go.

NuGet domyślnej konfiguracji można uzyskać przez ładowanie `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), następnie ładowania wszelkie `Nuget.Config` lub `.nuget\Nuget.Config` plików od głównego dysku i kończący się w bieżącym katalogu (zobacz [Konfigurowanie Zachowania programu NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Użycie

```cli
nuget push <packagePath> [options]
```

gdzie `<packagePath>` identyfikuje pakiet do wypychania do serwera.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ApiKey | Klucz interfejsu API w repozytorium docelowym. Jeśli nie występuje, określony w pliku konfiguracji jest używany. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| DisableBuffering | Wyłącza buforowanie podczas wypychania do serwera HTTP (s) w celu zmniejszenia użycia pamięci. Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie Windows może nie działać. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla Pomoc dla polecenia. |
| NonInteractive | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| NoSymbols | *(3.5 +)*  Jeżeli istnieje pakiet symboli, nie będą jej wypychane do serwera symboli. |
| Source | Określa adres URL serwera. NuGet identyfikuje UNC lub lokalny folder źródłowy i po prostu kopiuje plik zamiast wypychanie go przy użyciu protokołu HTTP.  Ponadto, począwszy od NuGet 3.4.2, jest to parametr obowiązkowy chyba że `NuGet.Config` plik Określa *DefaultPushSource* wartości (zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Określa adres URL serwera symboli; nuget.smbsrc.net jest używany podczas wypychania do repozytorium nuget.org |
| SymbolApiKey | *(3.5 +)*  Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`. |
| limit czasu | Określa limit czasu w sekundach, wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/
```
