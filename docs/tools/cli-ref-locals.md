---
title: Polecenie lokalne interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca polecenia nuget.exe zmiennych lokalnych
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545031"
---
# <a name="locals-command-nuget-cli"></a>locals command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 3.3 +

Usuwa lub wyświetla ich listę zasobów lokalnych NuGet takich jak *pamięci podręcznej http*, *globalnymi pakietami* folder i folderu tymczasowego. `locals` Polecenia można również wyświetlić listę tych lokalizacjach. Aby uzyskać więcej informacji, zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Użycie

```cli
nuget locals <folder> [options]
```

gdzie `<folder>` jest jednym z `all`, `http-cache`, `packages-cache` *(3.5 i starszych)*, `global-packages`, `temp` *(3.4 i nowsze)*, i `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| Usuń zaznaczenie | Usuwa określony folder. |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.|
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| Lista | Wyświetla listę lokalizacji wskazanym folderze lub lokalizacje wszystkich folderów, gdy jest używane z *wszystkich*. |
| Nieinterakcyjnym | Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Aby uzyskać więcej przykładów, zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).
