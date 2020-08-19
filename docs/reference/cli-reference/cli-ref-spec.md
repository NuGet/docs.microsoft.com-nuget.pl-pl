---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622567"
---
# <a name="spec-command-nuget-cli"></a>Spec — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje** tworzenia pakietów: wszystkie

Generuje `.nuspec` plik dla nowego pakietu. W przypadku uruchomienia w tym samym folderze, w którym znajduje się plik projektu ( `.csproj` , `.vbproj` ,, `.fsproj` ), program `spec` tworzy plik z tokenami `.nuspec` . Aby uzyskać dodatkowe informacje, zobacz [Tworzenie pakietu](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Użycie

```cli
nuget spec [<packageID>] [options]
```

gdzie `<packageID>` jest opcjonalnym identyfikatorem pakietu, który ma zostać zapisany w `.nuspec` pliku.

## <a name="options"></a>Opcje

- **`-AssemblyPath`**

  Określa ścieżkę do zestawu, który ma być używany dla metadanych.

- **`-Force`**

  Zastępuje istniejący `.nuspec` plik.


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
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
