---
title: Konfigurowanie lokalnych kanałów informacyjnych NuGet
description: Jak utworzyć lokalny kanał informacyjny dla pakietów NuGet przy użyciu folderów w sieci lokalnej
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 42a5c30c058a9efb35338c1b484235b6ad111bd0
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "68317591"
---
# <a name="local-feeds"></a>Lokalne kanały informacyjne

Lokalne źródła danych pakietu NuGet są po prostu hierarchicznymi strukturami folderów w sieci lokalnej (lub nawet tylko na własnym komputerze), w których umieszczasz pakiety. Te źródła danych mogą być następnie używane jako źródła pakietów ze wszystkimi innymi operacjami NuGet przy użyciu interfejsu wiersza polecenia, interfejsu użytkownika Menedżera pakietów i konsoli Menedżera pakietów.

Aby włączyć źródło, dodaj jego nazwa `\\myserver\packages`ścieżki (na przykład) do listy źródeł przy [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) użyciu interfejsu użytkownika Menedżera [pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources) lub polecenia.

> [!Note]
> Hierarchiczne struktury folderów są obsługiwane w nuget 3.3+. Starsze wersje NuGet używać tylko jeden folder zawierający pakiety, z których wydajność jest znacznie niższa niż hierarchicznej struktury.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicjowanie i obsługa folderów hierarchicznych

Hierarchiczne drzewo folderów wersjlowane ma następującą strukturę ogólną:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet tworzy tę strukturę automatycznie, gdy używasz [`nuget add`](../reference/cli-reference/cli-ref-add.md) polecenia do kopiowania pakietu do źródła danych:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

Polecenie `nuget add` działa z jednym pakietem naraz, co może być niewygodne podczas konfigurowania kanału informacyjnego z wieloma pakietami.

W takich przypadkach [`nuget init`](../reference/cli-reference/cli-ref-init.md) użyj polecenia, aby skopiować wszystkie pakiety `nuget add` w folderze do kanału informacyjnego, tak jakby uruchomiono na każdym z nich indywidualnie. Na przykład następujące polecenie kopiuje `c:\packages` wszystkie pakiety `\\myserver\packages`z drzewa hierarchicznego na:

```cli
nuget init c:\packages \\myserver\packages
```

Podobnie jak `add` w `init` przypadku polecenia, tworzy folder dla każdego identyfikatora pakietu, z których każdy zawiera folder numeru wersji, w którym znajduje się odpowiedni pakiet.
