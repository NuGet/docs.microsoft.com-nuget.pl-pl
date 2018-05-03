---
title: Polecenie zmiennych lokalnych NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe polecenia zmiennych lokalnych
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a>Zmienne lokalne polecenia (NuGet CLI)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +

Czyści lub wyświetla ich listę zasobów lokalnych NuGet takich jak *pamięci podręcznej http*, *globalne pakiety* folder i folderu tymczasowego. `locals` Polecenia można również wyświetlić listę tych lokalizacjach. Aby uzyskać więcej informacji, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Użycie

```cli
nuget locals <folder> [options]
```

gdzie `<folder>` jest jednym z `all`, `http-cache`, `packages-cache` *(3.5 i wcześniejszymi)*, `global-packages`, i `temp` *(3.4 +)*.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Wyczyść | Usuwa określony folder. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Lista | Wyświetla lokalizację określony folder lub lokalizacje wszystkich folderów, gdy jest używany z *wszystkich*. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Aby uzyskać dodatkowe przykłady, zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).
