---
title: Polecenie Usuń interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenie Usuń nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426106"
---
# <a name="delete-command-nuget-cli"></a>Usuń polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu publikowania &bullet; **obsługiwane wersje:** wszystkie

Usuwa lub unlists pakietu ze źródła pakietu. Dla nuget.org, polecenie Usuń [unlists pakietu](../nuget-org/policies/deleting-packages.md).

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
| Help | Wyświetla Pomoc dla polecenia. |
| NonInteractive | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Source | Określa adres URL serwera. Adres URL repozytorium nuget.org jest `https://api.nuget.org/v3/index.json`. Dla prywatnych źródeł danych, zastąp nazwę hosta, na przykład *%hostname%/api/v3*. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
