---
title: Polecenie init interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551413"
---
# <a name="init-command-nuget-cli"></a>polecenie init (interfejs wiersza polecenia NuGet)

**Dotyczy:** Tworzenie pakietu &bullet; **obsługiwane wersje:** 3.3 +

Kopiuje wszystkie pakiety z prostego folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](cli-ref-add.md). Oznacza to, za pomocą `init` jest równoważne użyciu `add` polecenie każdego pakietu, w tym folderze.

Podobnie jak w przypadku `add`, miejsce docelowe musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietów protokołu HTTP, np. nuget.org lub serwery prywatne nie są obsługiwane.

## <a name="usage"></a>Użycie

```cli
nuget init <source> <destination> [options]
```

gdzie `<source>` jest folder zawierający pakiety i `<destination>` jest lokalny folder lub ścieżka UNC, do której są kopiowane pakietów.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Rozwiń węzeł | Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
