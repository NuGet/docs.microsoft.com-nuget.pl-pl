---
title: Polecenie zmiennych lokalnych NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca nuget.exe polecenia zmiennych lokalnych
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818204"
---
# <a name="locals-command-nuget-cli"></a>locals command, polecenie (interfejs wiersza polecenia NuGet)

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
