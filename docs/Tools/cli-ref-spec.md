---
title: Polecenie specyfikacji interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Informacje dotyczące polecenia specyfikacji nuget.exe"
keywords: "Odwołanie specyfikacji nuget, specyfikacji polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>Specyfikacja polecenia (NuGet CLI)

**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** wszystkie

Generuje `.nuspec` plików dla nowego pakietu. Jeśli uruchomione w tym samym folderze co plik projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` tworzy tokenami `.nuspec` pliku. Aby uzyskać dodatkowe informacje, zobacz [utworzenie pakietu](../create-packages/creating-a-package.md).

## <a name="usage"></a>Użycie

```
nuget spec [<packageID>] [options]
```

gdzie `<packageID>` jest identyfikatorem opcjonalny pakiet do zapisania w `.nuspec` pliku.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Zestawu AssemblyPath | Określa ścieżkę do zestawu do użycia na potrzeby metadanych. |
| Wymuś | Zastępuje istniejące `.nuspec` pliku. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
