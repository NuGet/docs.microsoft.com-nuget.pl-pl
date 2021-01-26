---
title: Polecenie dublowania interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia dublowania
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779173"
---
# <a name="mirror-command-nuget-cli"></a>Mirror — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **wersje obsługiwane** przez publikowanie pakietów: przestarzałe w 3.2 +

Odzwierciedla pakiet i jego zależności z określonych repozytoriów źródłowych do repozytorium docelowego.

> [!NOTE]
> NuGet.ServerExtensions.dll i NuGet-Signed.exe, które wcześniej obsługiwały to polecenie w programie NuGet 2. x (poprzez zmianę nazwy NuGet-Signed.exe na nuget.exe) nie są już dostępne do pobrania. Aby użyć polecenia podobnego do tego, wypróbuj [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Użycie

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

gdzie `<packageID>` jest pakiet do dublowania lub `<configFilePath>` identyfikuje plik, `packages.config` który zawiera listę pakietów do dublowania.

`<listUrlTarget>`Określa repozytorium źródłowe i `<publishUrlTarget>` określa repozytorium docelowe.

Jeśli repozytorium docelowe znajduje się na komputerze, na którym jest `https://machine/repo` uruchomiony program [NuGet. Server](../../hosting-packages/nuget-server.md), lista i adresy URL wypychania będą `https://machine/repo/nuget` `https://machine/repo/api/v2/package` odpowiednio i.

## <a name="options"></a>Opcje

- **`-ApiKey`**

  Klucz interfejsu API repozytorium docelowego. Jeśli nie istnieje, jest używany określony w pliku konfiguracyjnym ( `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NoCache`**

  Uniemożliwia narzędziu NuGet używanie buforowanych pakietów. Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Rejestruje co robić, ale nie wykonuje akcji; przyjęto założenie sukcesu dla operacji wypychania.

- **`-PreRelease`**

  Obejmuje pakiety wersji wstępnej w operacji dublowania.

- **`-Source`**

  Lista źródeł pakietów do dublowania. Jeśli nie określono żadnych źródeł, są one zdefiniowane w pliku konfiguracyjnym (zobacz ApiKey powyżej), jeśli nie określono żadnego z nich.

- **`-Timeout`**

  Określa limit czasu (w sekundach) wypychania do serwera. Wartość domyślna to 300 sekund (5 minut).

- **`-Version`**

  Wersja pakietu do zainstalowania. Jeśli nie zostanie określony, Najnowsza wersja jest dublowana.

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
