---
title: Polecenie Add interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe Dodaj polecenie
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776087"
---
# <a name="add-command-nuget-cli"></a>Add — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy**: &bullet; **obsługiwane wersje** publikowania pakietów: 3.3 +

Dodaje określony pakiet do źródła pakietów innego niż HTTP (folderu lub ścieżki UNC) w układzie hierarchicznym, w którym foldery są tworzone dla identyfikatora pakietu i numeru wersji. Na przykład:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

W przypadku przywracania lub aktualizowania względem źródła pakietu układ hierarchiczny zapewnia znacznie lepszą wydajność.

Aby rozwinąć wszystkie pliki w pakiecie do źródła pakietu docelowego, użyj `-Expand` przełącznika. Zwykle powoduje to dodanie dodatkowych podfolderów w miejscu docelowym, takich jak `tools` i `lib` .

## <a name="usage"></a>Użycie

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

gdzie `<packagePath>` jest ścieżką do pakietu do dodania i `<sourcePath>` określa źródło pakietu, do którego zostanie dodany pakiet. Źródła HTTP nie są obsługiwane.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-Expand`**

  Dodaje wszystkie pliki w pakiecie do źródła pakietu.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.
Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-src|-Source`**

   Określa źródło pakietu, które jest folderem lub udziałem UNC, do którego zostanie dodany NUPKG. Źródła http nie są obsługiwane.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
