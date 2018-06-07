---
title: Polecenie init NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia init nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817821"
---
# <a name="init-command-nuget-cli"></a>init polecenia (NuGet CLI)

**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 3.3 +

Kopiuje wszystkie pakiety z płaskim folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](cli-ref-add.md). Oznacza to, za pomocą `init` odpowiada za pomocą `add` na każdy pakiet w folderze.

Jak `add`, docelowy musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietu HTTP, takie jak nuget.org lub prywatnej serwery nie są obsługiwane.

## <a name="usage"></a>Użycie

```cli
nuget init <source> <destination> [options]
```

gdzie `<source>` jest folder zawierający pakietów i `<destination>` jest lokalny folder lub ścieżka UNC, do której są kopiowane pakiety.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Rozwiń węzeł | Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
