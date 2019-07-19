---
title: Polecenie dublowania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia dublowania NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328304"
---
# <a name="mirror-command-nuget-cli"></a>mirror command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **wersje obsługiwane** przez &bullet; publikowanie pakietów: przestarzałe w 3.2 +

Odzwierciedla pakiet i jego zależności z określonych repozytoriów źródłowych do repozytorium docelowego.

> [!NOTE]
> Aby włączyć to polecenie dla wersji NuGet przed 3,2, przejdź do [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), wybierz najnowszą stabilną wersję, Pobierz `NuGet.ServerExtensions.dll` i `Nuget-Signed.exe` na dysk lokalny, a następnie `Nuget-Signed.exe` Zmień `nuget.exe` nazwę na.

## <a name="usage"></a>Użycie

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

gdzie `<packageID>` jest pakiet do dublowania lub `<configFilePath>` identyfikuje `packages.config` plik, który zawiera listę pakietów do dublowania.

Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe. `<listUrlTarget>`

Jeśli repozytorium docelowe znajduje się na `https://machine/repo` komputerze, na którym jest uruchomiony program [NuGet. Server](../../hosting-packages/nuget-server.md), lista i adresy `https://machine/repo/nuget` URL `https://machine/repo/api/v2/package`wypychania będą odpowiednio i.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ApiKey | Klucz interfejsu API repozytorium docelowego. Jeśli nie istnieje, jest używany określony w pliku konfiguracyjnym (`%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NoCache | Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej. |
| Aktualizujący nie działa | Rejestruje co robić, ale nie wykonuje akcji; przyjęto założenie sukcesu dla operacji wypychania. |
| Wersja wstępna | Obejmuje pakiety wersji wstępnej w operacji dublowania. |
| Source | Lista źródeł pakietów do dublowania. Jeśli nie określono żadnych źródeł, są one zdefiniowane w pliku konfiguracyjnym (zobacz ApiKey powyżej), jeśli nie określono żadnego z nich. |
| limit czasu | Określa limit czasu (w sekundach) wypychania do serwera. Wartość domyślna to 300 sekund (5 minut). |
| Wersja | Wersja pakietu do zainstalowania. Jeśli nie zostanie określony, Najnowsza wersja jest dublowana. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
