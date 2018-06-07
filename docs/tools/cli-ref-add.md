---
title: Interfejs wiersza polecenia NuGet Dodaj — polecenie
description: Dodaj odwołanie do nuget.exe — polecenie
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817613"
---
# <a name="add-command-nuget-cli"></a>add command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy**: publikowanie pakietu &bullet; **obsługiwane wersje**: 3.3 +

Dodaje określony pakiet do źródła pakietu protokołu HTTP (folder lub ścieżka UNC) w układzie hierarchicznym, w którym są tworzone foldery numeru identyfikator i wersję pakietu. Na przykład:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Podczas przywracania lub aktualizowania źródle pakietu, hierarchiczna układ zapewnia znacznie wyższą wydajność.

Aby rozwinąć wszystkie pliki w pakiecie do docelowego źródła pakietu, należy użyć `-Expand` przełącznika. Zazwyczaj powoduje to dodatkowe podfolderów znajdujących się w lokalizacji docelowej, takie jak `tools` i `lib`.

## <a name="usage"></a>Użycie

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

gdzie `<packagePath>` jest ścieżka do pakietu, aby dodać, a `<sourcePath>` określa źródła pakietu na podstawie folderu, do którego zostanie dodany pakiet. Źródła HTTP nie są obsługiwane.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| Rozwiń węzeł | Dodaje wszystkie pliki w pakiecie do źródła pakietu. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
