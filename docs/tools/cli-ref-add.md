---
title: Interfejs wiersza polecenia NuGet, Dodaj polecenie
description: Dokumentacja dotycząca nuget.exe dodaj — polecenie
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545837"
---
# <a name="add-command-nuget-cli"></a>add command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy**: publikowanie pakietu &bullet; **obsługiwane wersje**: 3.3 +

Dodaje określony pakiet do źródła pakietu protokołu HTTP (folder lub ścieżka UNC) w układzie hierarchicznym, w którym są tworzone foldery dla pakietu ID i numeru wersji. Na przykład:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Podczas przywracania lub aktualizowanie względem źródła pakietu, w układzie hierarchicznym zapewnia znacznie lepszą wydajność.

Aby rozwinąć wszystkie pliki w pakiecie do docelowego źródła pakietu, należy użyć `-Expand` przełącznika. Zazwyczaj powoduje to dodatkowe podfolderów znajdujących się w miejscu docelowym, takich jak `tools` i `lib`.

## <a name="usage"></a>Użycie

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

gdzie `<packagePath>` jest nazwa ścieżki do pakietu, aby dodać, a `<sourcePath>` określa źródła pakietu na podstawie folderu, do którego zostanie dodany pakietu. Źródła HTTP nie są obsługiwane.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| Rozwiń węzeł | Dodaje wszystkie pliki w pakiecie do źródła pakietu. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
