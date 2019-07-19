---
title: Konfigurowanie lokalnych źródeł danych NuGet
description: Tworzenie lokalnego źródła danych dla pakietów NuGet przy użyciu folderów w sieci lokalnej
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317591"
---
# <a name="local-feeds"></a>Lokalne kanały informacyjne

Lokalne źródła pakietów NuGet są po prostu hierarchicznymi strukturami folderów w sieci lokalnej (lub nawet na swoim komputerze), w których umieszczane są pakiety. Te kanały informacyjne mogą być następnie używane jako źródła pakietów ze wszystkimi innymi operacjami NuGet przy użyciu interfejsu wiersza polecenia, Menedżera pakietów i konsoli Menedżera pakietów.

Aby włączyć źródło, Dodaj jego nazwę ścieżki (na przykład `\\myserver\packages`) do listy źródeł przy użyciu [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) [interfejsu użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources) lub polecenia.

> [!Note]
> Hierarchiczne struktury folderów są obsługiwane w NuGet 3.3 +. Starsze wersje programu NuGet używają tylko jednego folderu zawierającego pakiety, z których wydajność jest znacznie mniejsza niż struktura hierarchiczna.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicjowanie i obsługa folderów hierarchicznych

Hierarchiczne drzewo folderów z wersjami ma następującą strukturę ogólną:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

Pakiet NuGet automatycznie tworzy tę strukturę przy użyciu [`nuget add`](../reference/cli-reference/cli-ref-add.md) polecenia do kopiowania pakietu do źródła danych:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Polecenie działa z jednym pakietem na raz, co może być niewygodne podczas konfigurowania kanału informacyjnego z wieloma pakietami.

W takich przypadkach należy użyć [`nuget init`](../reference/cli-reference/cli-ref-init.md) polecenia, aby skopiować wszystkie pakiety w folderze do źródła danych, tak jakby były uruchamiane `nuget add` osobno na każdym z nich. Na przykład następujące polecenie kopiuje wszystkie pakiety z `c:\packages` do `\\myserver\packages`drzewa hierarchicznego:

```cli
nuget init c:\packages \\myserver\packages
```

Podobnie jak w `add` przypadku polecenia `init` program tworzy folder dla każdego identyfikatora pakietu, z którego każdy zawiera folder numeru wersji, w którym jest odpowiednim pakietem.
