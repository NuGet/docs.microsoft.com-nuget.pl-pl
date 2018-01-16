---
title: Polecenie zmiennych lokalnych interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Dokumentacja dotycząca nuget.exe polecenia zmiennych lokalnych"
keywords: "Odwołanie do zmiennych lokalnych nuget, polecenie zmiennych lokalnych"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a>Zmienne lokalne polecenia (NuGet CLI)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +

Czyści lub wyświetla ich listę zasobów lokalnych NuGet pamięci podręcznej żądania http, pakiety w pamięci podręcznej i folderu pakietów globalne dla komputera. `locals` Polecenia można również wyświetlić listę tych lokalizacjach. Aby uzyskać więcej informacji, zobacz [Zarządzanie pamięci podręcznej NuGet](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Użycie

```
nuget locals <cache> [options]
```

gdzie `<cache>` jest jednym z `all`, `http-cache`, `packages-cache`, `global-packages`, i `temp` *(3.4 +)*.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Wyczyść | Usuwa określony pamięci podręcznej. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Lista | Wyświetla lokalizację pamięci podręcznej określony lub lokalizacje wszystkich usług pamięć podręczna w przypadku użycia z *wszystkich*. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```
nuget locals all -list
nuget locals http-cache -clear
```
