---
title: Polecenie init interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623087"
---
# <a name="init-command-nuget-cli"></a>init — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje:** 3.3 +

Kopiuje wszystkie pakiety z folderu płaskiego do folderu docelowego przy użyciu układu hierarchicznego zgodnie z opisem dla [polecenia Dodaj](cli-ref-add.md). Oznacza to, że użycie `init` jest równoważne użyciu `add` polecenia w każdym pakiecie w folderze.

Tak jak w przypadku `add` , miejsce docelowe musi być folderem lokalnym lub ścieżką UNC; Repozytoria pakietów HTTP, takie jak nuget.org lub serwery prywatne, nie są obsługiwane.

## <a name="usage"></a>Użycie

```cli
nuget init <source> <destination> [options]
```

gdzie `<source>` folder zawiera pakiety i `<destination>` jest folderem lokalnym lub ŚCIEŻKą UNC, do której są kopiowane pakiety.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-Expand`**

  Dodaje wszystkie pliki w każdym pakiecie, które są dodawane do źródła pakietu; Analogicznie jak `-Expand` `add` polecenie.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
