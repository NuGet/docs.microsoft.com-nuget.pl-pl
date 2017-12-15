---
title: Polecenie init interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Informacje dotyczące polecenia init nuget.exe"
keywords: "Odwołanie init nuget, init, polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a>init polecenia (NuGet CLI)

**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 3.3 +

Kopiuje wszystkie pakiety z płaskim folderu do folderu docelowego przy użyciu układzie hierarchicznym, zgodnie z opisem dla [Dodaj polecenie](#add) powyżej. Oznacza to, za pomocą `init` odpowiada za pomocą `add` na każdy pakiet w folderze.

Jak `add`, docelowy musi być folderem lokalnym lub ścieżką UNC; Repozytoriów pakietu HTTP, takie jak nuget.org lub prywatnej serwery nie są obsługiwane.

## <a name="usage"></a>Użycie

```
nuget init <source> <destination> [options]
```

gdzie `<source>` jest folder zawierający pakietów i `<destination>` jest folder lokalny lub nazwa ścieżki UNC, do którego zostaną skopiowane pakiety.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Rozwiń węzeł | Dodaje wszystkie pliki w każdym pakiecie, który zostanie dodany do źródła pakietu; taki sam jak `-Expand` z `add` polecenia. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
