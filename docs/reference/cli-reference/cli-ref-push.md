---
title: Polecenie push interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia push. exe wypychania
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328292"
---
# <a name="push-command-nuget-cli"></a>Push — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** publikacji &bullet; pakietu: ALL; 4.1.0 + Required for NuGet.org

> [!Important]
> Aby wypchnąć pakiety do nuget.org należy użyć NuGet. exe v 4.1.0 +, który implementuje wymagane [Protokoły NuGet](../../api/nuget-protocols.md).

Wypchnij pakiet do źródła pakietu i opublikuje go.

Domyślna konfiguracja narzędzia NuGet jest uzyskiwana przez `%AppData%\NuGet\NuGet.Config` załadowanie (system `~/.nuget/NuGet/NuGet.Config` Windows) lub (Mac/Linux `Nuget.Config` ) `.nuget\Nuget.Config` , a następnie załadowanie plików z katalogu głównego dysku i zakończenie w bieżącym katalogu (zobacz [Common NuGet konfiguracje](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Użycie

```cli
nuget push <packagePath> [options]
```

gdzie `<packagePath>` identyfikuje pakiet do wypychania do serwera.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ApiKey | Klucz interfejsu API repozytorium docelowego. Jeśli nie istnieje, jest używany określony w pliku konfiguracji. |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| DisableBuffering | Wyłącza buforowanie podczas wypychania do serwera HTTP (s) w celu zmniejszenia użycia pamięci. Uwaga: Jeśli ta opcja jest używana, zintegrowane uwierzytelnianie systemu Windows może nie być możliwe. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| NoSymbols | *(3.5 +)* Jeśli pakiet symboli istnieje, nie zostanie wypychany do serwera symboli. |
| Source | Określa adres URL serwera. Pakiet NuGet identyfikuje źródło folderu UNC lub lokalnego i po prostu kopiuje plik, zamiast wypchnięcia go przy użyciu protokołu HTTP.  Ponadto, rozpoczynając od 3.4.2 NuGet, jest to obowiązkowy parametr, chyba że `NuGet.Config` plik określa wartość *DefaultPushSource* (zobacz [Konfigurowanie zachowania NuGet](../../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | *(5.1 +)* Jeśli pakiet i wersja już istnieją, Pomiń ją i przejdź do następnego pakietu w wypychaniu (jeśli istnieje). |
| SymbolSource | *(3.5 +)* Określa adres URL serwera symboli; nuget.smbsrc.net jest używany podczas wypychania do nuget.org |
| SymbolApiKey | *(3.5 +)* Określa klucz interfejsu API dla adresu URL określonego w `-SymbolSource`. |
| limit czasu | Określa limit czasu (w sekundach) wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

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

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
