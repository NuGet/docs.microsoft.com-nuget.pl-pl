---
title: Polecenie Usuń NuGet interfejsu wiersza polecenia
description: Dokumentacja dla polecenia delete nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a>Usuwanie polecenia (NuGet CLI)

**Dotyczy:** publikowania pakietu &bullet; **obsługiwane wersje:** wszystkie

Usuwa lub unlists pakietu ze źródła pakietu. Dla nuget.org, polecenia delete [unlists pakietu](../policies/deleting-packages.md).

## <a name="usage"></a>Użycie

```cli
nuget delete <packageID> <packageVersion> [options]
```

gdzie `<packageID>` i `<packageVersion>` identyfikować dokładną pakiet do usunięcia lub unlist. Dokładne zachowanie zależy od źródła. Foldery lokalne na przykład pakiet został usunięty; w przypadku nuget.org pakietu jest nieznajdujące się na liście.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| apiKey | Klucz interfejsu API dla repozytorium docelowej. Jeśli nie istnieje określony w pliku konfiguracji jest używany. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Źródło | Określa adres URL serwera. Adres URL nuget.org jest `https://api.nuget.org/v3/index.json`. Dla prywatnych źródeł danych, zastąp nazwę hosta, na przykład *%hostname%/api/v3*. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
