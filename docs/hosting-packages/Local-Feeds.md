---
title: Konfigurowanie lokalnych źródeł danych NuGet
description: Tworzenie lokalnego źródła danych dla pakietów NuGet przy użyciu folderów w sieci lokalnej
author: JonDouglas
ms.author: jodou
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 1eb194c9ddaee05281749c7a0420cbaf77044fe3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774044"
---
# <a name="local-feeds"></a>Lokalne kanały informacyjne

Lokalne źródła pakietów NuGet są po prostu hierarchicznymi strukturami folderów w sieci lokalnej (lub nawet na swoim komputerze), w których umieszczane są pakiety. Te kanały informacyjne mogą być następnie używane jako źródła pakietów ze wszystkimi innymi operacjami NuGet przy użyciu interfejsu wiersza polecenia, Menedżera pakietów i konsoli Menedżera pakietów.

Aby włączyć źródło, Dodaj jego nazwę ścieżki (na przykład `\\myserver\packages` ) do listy źródeł przy użyciu [interfejsu użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources) lub [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) polecenia.

> [!Note]
> Hierarchiczne struktury folderów są obsługiwane w NuGet 3.3 +. Starsze wersje programu NuGet używają tylko jednego folderu zawierającego pakiety, z których wydajność jest znacznie mniejsza niż struktura hierarchiczna.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicjowanie i obsługa folderów hierarchicznych

Hierarchiczne drzewo folderów z wersjami ma następującą strukturę ogólną:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      └─<other files>
```

Pakiet NuGet automatycznie tworzy tę strukturę przy użyciu [`nuget add`](../reference/cli-reference/cli-ref-add.md) polecenia do kopiowania pakietu do źródła danych:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add`Polecenie działa z jednym pakietem na raz, co może być niewygodne podczas konfigurowania kanału informacyjnego z wieloma pakietami.

W takich przypadkach należy użyć [`nuget init`](../reference/cli-reference/cli-ref-init.md) polecenia, aby skopiować wszystkie pakiety w folderze do źródła danych, tak jakby były uruchamiane `nuget add` osobno na każdym z nich. Na przykład następujące polecenie kopiuje wszystkie pakiety z `c:\packages` do drzewa hierarchicznego `\\myserver\packages` :

```cli
nuget init c:\packages \\myserver\packages
```

Podobnie jak w przypadku `add` polecenia program `init` tworzy folder dla każdego identyfikatora pakietu, z którego każdy zawiera folder numeru wersji, w którym jest odpowiednim pakietem.
