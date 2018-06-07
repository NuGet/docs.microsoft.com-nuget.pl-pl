---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia specyfikacji nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817089"
---
# <a name="spec-command-nuget-cli"></a>Specyfikacja polecenia (NuGet CLI)

**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** wszystkie

Generuje `.nuspec` plików dla nowego pakietu. Jeśli uruchomione w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku. Aby uzyskać dodatkowe informacje, zobacz [utworzenie pakietu](../create-packages/creating-a-package.md).

## <a name="usage"></a>Użycie

```cli
nuget spec [<packageID>] [options]
```

gdzie `<packageID>` jest identyfikatorem opcjonalny pakiet do zapisania w `.nuspec` pliku.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Zestawu AssemblyPath | Określa ścieżkę do zestawu do użycia na potrzeby metadanych. |
| Wymuś | Zastępuje istniejące `.nuspec` pliku. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
