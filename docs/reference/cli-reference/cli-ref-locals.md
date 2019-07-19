---
title: Polecenie locale interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia Locals NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328346"
---
# <a name="locals-command-nuget-cli"></a>locals command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : 3.3+

Czyści lub wyświetla lokalne zasoby NuGet, takie jak folder *http pamięci*podręcznej, *pakiety globalne* i folder tymczasowy. Można również użyć polecenia, aby wyświetlić listę tych lokalizacji. `locals` Aby uzyskać więcej informacji, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.

## <a name="usage"></a>Użycie

```cli
nuget locals <folder> [options]
```

gdzie `<folder>` jest jedną z `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 i wcześniejszą)* ,, *(3.4 +)* i *(4.8 +)* .

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Clear | Czyści określony folder. |
| ConfigFile | Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Help | Wyświetla informacje pomocy dla polecenia. |
| Lista | Wyświetla lokalizację określonego folderu lub lokalizacje wszystkich folderów, jeśli są używane ze *wszystkimi*. |
| NonInteractive | Pomija monity o dane wejściowe lub potwierdzone przez użytkownika. |
| Verbosity | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Aby uzyskać więcej przykładów, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.
