---
title: Polecenie Usuń interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenie Usuń nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548513"
---
# <a name="delete-command-nuget-cli"></a>Usuń polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu publikowania &bullet; **obsługiwane wersje:** wszystkie

Usuwa lub unlists pakietu ze źródła pakietu. Dla nuget.org, polecenie Usuń [unlists pakietu](../policies/deleting-packages.md).

## <a name="usage"></a>Użycie

```cli
nuget delete <packageID> <packageVersion> [options]
```

gdzie `<packageID>` i `<packageVersion>` zidentyfikować dokładny pakiet do usunięcia lub wyrejestrowanie. Dokładne zachowanie zależy od źródła. Foldery lokalne na przykład pakiet jest usunięty; w przypadku nuget.org pakietu jest nieobecne na liście.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ApiKey | Klucz interfejsu API w repozytorium docelowym. Jeśli nie występuje, określony w pliku konfiguracji jest używany. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Źródło | Określa adres URL serwera. Adres URL repozytorium nuget.org jest `https://api.nuget.org/v3/index.json`. Dla prywatnych źródeł danych, zastąp nazwę hosta, na przykład *%hostname%/api/v3*. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
