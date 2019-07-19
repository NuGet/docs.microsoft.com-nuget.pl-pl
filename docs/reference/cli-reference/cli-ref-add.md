---
title: Polecenie Add interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia Add dla NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328361"
---
# <a name="add-command-nuget-cli"></a>add command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy**: **obsługiwane wersje**publikowania &bullet; pakietów: 3.3+

Dodaje określony pakiet do źródła pakietów innego niż HTTP (folderu lub ścieżki UNC) w układzie hierarchicznym, w którym foldery są tworzone dla identyfikatora pakietu i numeru wersji. Przykład:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

W przypadku przywracania lub aktualizowania względem źródła pakietu układ hierarchiczny zapewnia znacznie lepszą wydajność.

Aby rozwinąć wszystkie pliki w pakiecie do źródła pakietu docelowego, użyj `-Expand` przełącznika. Zwykle powoduje to dodanie dodatkowych podfolderów w miejscu docelowym, takich `tools` jak `lib`i.

## <a name="usage"></a>Użycie

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

gdzie `<packagePath>` jest ścieżką do pakietu do dodania i `<sourcePath>` określa źródło pakietu, do którego zostanie dodany pakiet. Źródła HTTP nie są obsługiwane.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| Expand | Dodaje wszystkie pliki w pakiecie do źródła pakietu. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
