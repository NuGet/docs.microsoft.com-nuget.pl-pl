---
title: Polecenie usunięcia interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia Delete programu NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328355"
---
# <a name="delete-command-nuget-cli"></a>DELETE — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** publikowania &bullet; pakietów: wszystkie

Usuwa pakiet ze źródła pakietu. W przypadku nuget.org polecenie Delete wystawia [pakiet](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Użycie

```cli
nuget delete <packageID> <packageVersion> [options]
```

gdzie `<packageID>` i`<packageVersion>` Zidentyfikuj dokładny pakiet do usunięcia lub Wycofaj listy. Dokładne zachowanie zależy od źródła. Na przykład dla folderów lokalnych pakiet jest usuwany; dla nuget.org pakiet nie znajduje się na liście.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ApiKey | Klucz interfejsu API repozytorium docelowego. Jeśli nie istnieje, jest używany określony w pliku konfiguracji. |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Source | Określa adres URL serwera. Adres URL nuget.org ma `https://api.nuget.org/v3/index.json`wartość. W przypadku prywatnych kanałów informacyjnych należy zastąpić nazwę hosta, na przykład *% hostname%/API/v3*. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
