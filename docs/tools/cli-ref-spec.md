---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń specyfikacji nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794154"
---
# <a name="spec-command-nuget-cli"></a>Specyfikacja polecenia (interfejs wiersza polecenia NuGet)

**Dotyczy:** Tworzenie pakietu &bullet; **obsługiwane wersje:** wszystkie

Generuje `.nuspec` pliku dla nowego pakietu. Jeśli w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku. Aby uzyskać więcej informacji, zobacz [Tworzenie pakietu](../create-packages/creating-a-package.md).

## <a name="usage"></a>Użycie

```cli
nuget spec [<packageID>] [options]
```

gdzie `<packageID>` jest identyfikatorem pakietu opcjonalnego można zapisać w `.nuspec` pliku.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Ścieżkazestawu | Określa ścieżkę do zestawu do użycia dla metadanych. |
| Wymuś | Powoduje zastąpienie wszystkich istniejących `.nuspec` pliku. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
