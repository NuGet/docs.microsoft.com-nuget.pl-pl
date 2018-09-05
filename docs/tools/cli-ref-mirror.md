---
title: Polecenie dublowanie interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenia dublowanie nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550209"
---
# <a name="mirror-command-nuget-cli"></a>mirror command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu publikowania &bullet; **obsługiwane wersje:** uznane za przestarzałe w 3.2 +

Odzwierciedla pakietu oraz jego zależności z repozytoriów określone źródło do repozytorium docelowego.

> [!NOTE]
> Aby włączyć to polecenie dla wersji NuGet przed 3.2, przejdź do [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)wybierz najnowszej stabilnej wersji, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` do zmiany nazwy i dysku lokalnego, na których `Nuget-Signed.exe` do `nuget.exe`.

## <a name="usage"></a>Użycie

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

gdzie `<packageID>` to pakiet duplikatów, lub `<configFilePath>` identyfikuje `packages.config` pliku, który zawiera listę pakietów w celu utworzenia duplikatów.

`<listUrlTarget>` Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowego.

Jeśli Twoje repozytorium docelowym znajduje się na `https://machine/repo` uruchomionym [NuGet.Server](../hosting-packages/nuget-server.md), listy i wypychania adresy URL będą `https://machine/repo/nuget` i `https://machine/repo/api/v2/package`odpowiednio.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ApiKey | Klucz interfejsu API w repozytorium docelowym. Jeśli nie występuje, określony w pliku konfiguracji jest używana (`%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| NoCache | Uniemożliwia korzystania z pamięci podręcznej pakietów NuGet. Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Aktualizujący nie działa | Rejestruje, jakie będą wykonywane, ale nie wykonuje akcji; przyjęto założenie, Powodzenie operacji wypychania. |
| Wersja wstępna | Obejmuje pakiety w wersjach wstępnych w ramach operacji dublowania. |
| Źródło | Lista źródeł pakietów w celu utworzenia duplikatów. Jeśli nie określono żadnych źródeł, te zdefiniowane w pliku konfiguracji (patrz powyżej ApiKey) są używane, przyjęty adres nuget.org, jeśli żaden nie jest określony. |
| limit czasu | Określa limit czasu w sekundach, wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Wersja | Wersja pakietu do zainstalowania. Jeśli nie zostanie określony, znajduje odzwierciedlenie najnowszej wersji. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
