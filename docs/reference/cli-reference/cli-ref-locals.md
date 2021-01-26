---
title: Polecenie locale interfejsu wiersza polecenia NuGet
description: Informacje dotyczące nuget.exe lokalnych polecenia
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779200"
---
# <a name="locals-command-nuget-cli"></a>locale — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje pakietów:** 3.3 +

Czyści lub wyświetla lokalne zasoby NuGet, takie jak folder *http pamięci podręcznej*, *pakiety globalne* i folder tymczasowy. `locals`Można również użyć polecenia, aby wyświetlić listę tych lokalizacji. Aby uzyskać więcej informacji, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Użycie

```cli
nuget locals <folder> [options]
```

gdzie `<folder>` jest jedną z `all` , `http-cache` , `packages-cache` *(3,5 i wcześniejszą)*, `global-packages` , `temp` *(3.4 +)* i `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Opcje

- **`-Clear`**

  Czyści określony folder.

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-List`**

  Wyświetla lokalizację określonego folderu lub lokalizacje wszystkich folderów, jeśli są używane ze *wszystkimi*.

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Aby uzyskać więcej przykładów, zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
