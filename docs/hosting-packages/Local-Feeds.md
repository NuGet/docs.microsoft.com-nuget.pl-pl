---
title: Konfigurowanie lokalnych źródeł danych NuGet
description: Jak utworzyć lokalnego źródła danych dla pakietów NuGet za pomocą folderów w sieci lokalnej
author: karann-msft
ms.author: karann
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 91c072c8895ab4267c64fd04deae010ae5af4d37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545455"
---
# <a name="local-feeds"></a>Lokalne źródła danych

Lokalne źródła danych pakietu NuGet są po prostu hierarchiczne folder struktury w sieci lokalnej (lub nawet tylko Twój własny komputer), w których umieszczane są pakiety. Te źródła danych mogą być następnie używane jako źródła pakietu z innymi operacjami NuGet za pomocą interfejsu wiersza polecenia, interfejs użytkownika Menedżera pakietów i konsoli Menedżera pakietów.

Aby włączyć źródłowego, Dodaj swoją nazwę ścieżki (takie jak `\\myserver\packages`) do listy źródeł przy użyciu [interfejs użytkownika Menedżera pakietów](../tools/package-manager-ui.md#package-sources) lub [ `nuget sources` ](../tools/cli-ref-sources.md) polecenia.

> [!Note]
> Folder hierarchicznej struktury są obsługiwane w pakiecie NuGet 3.3 +. Starsze wersje pakietu nuget, użyj tylko pojedynczy folder zawierający pakiety, których wydajność jest znacznie niższa niż hierarchicznej struktury.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicjowanie i utrzymywanie folderów hierarchicznych

Drzewo hierarchiczne folderów numerów wersji ma następującą strukturę ogólne:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet tworzy automatycznie tej struktury, korzystając z [ `nuget add` ](../tools/cli-ref-add.md) polecenie, aby skopiować pakiet do źródła danych:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Polecenia współpracuje z jednym pakiecie w czasie, który może być niewygodne, podczas konfigurowania źródła danych z wielu pakietów.

W takiej sytuacji należy użyć [ `nuget init` ](../tools/cli-ref-init.md) polecenie, aby skopiować wszystkie pakiety w folderze w strumieniowym źródle danych, jak w przypadku uruchomienia `nuget add` na każdym z nich osobno. Na przykład następujące polecenie kopiuje wszystkie pakiety z `c:\packages` do drzewa hierarchicznego na `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Podobnie jak w przypadku `add` polecenia `init` tworzy folder dla każdego pakietu identyfikator folderu numeru wersji, z których każdy zawiera poziomu będący odpowiedniego pakietu.
