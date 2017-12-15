---
title: "Konfigurowanie lokalnych źródeł danych NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "Jak utworzyć lokalnego źródła danych za pomocą folderów w sieci lokalnej pakietów NuGet"
keywords: "NuGet źródła danych, Galeria NuGet, pakiet lokalny źródła danych"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a>Lokalne źródła danych

Lokalne źródła danych pakietu NuGet są struktury po prostu hierarchiczna folderów w sieci lokalnej (lub nawet po prostu swojego komputera), w którym zostanie umieszczony pakietów. Te źródła danych mogą następnie służyć jako źródła pakietów z innymi operacjami NuGet przy użyciu interfejsu wiersza polecenia, interfejs użytkownika Menedżera pakietów i konsoli Menedżera pakietów.

Aby włączyć źródła, dodaj jego pathname (takich jak `\\myserver\packages`) do listy źródeł za pomocą [interfejsu użytkownika Menedżera pakietów](../tools/package-manager-ui.md#package-sources) lub [ `nuget sources` ](../tools/cli-ref-sources.md) polecenia.

> [!Note]
> Struktury folderów hierarchicznych są obsługiwane w NuGet 3.3 +. Starsze wersje programu NuGet Użyj tylko pojedynczy folder zawierający pakiety, z którymi jest znacznie niższa niż strukturę hierarchiczną wydajności.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicjowanie i utrzymywanie folderów hierarchicznych

Hierarchiczna folder z kontrolą wersji drzewa ma następującą strukturę ogólne:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet tworzy automatycznie tej struktury, korzystając z [ `nuget add` ](../tools/cli-ref-add.md) polecenie, aby skopiować pakiet do źródła danych:

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Polecenia współpracuje z jednym pakiecie w czasie, który może być niewygodne, podczas konfigurowania źródła danych z wielu pakietów.

W takiej sytuacji należy użyć [ `nuget init` ](../tools/cli-ref-init.md) polecenie, aby skopiować wszystkie pakiety w folderze do źródła danych, jak w przypadku uruchomienia `nuget add` na każdej z nich osobno. Na przykład następujące polecenie kopiuje wszystkie pakiety z `c:\packages` hierarchiczne drzewa na `\\myserver\packages`:

```
nuget init c:\packages \\myserver\packages
```

Jak `add` polecenia `init` tworzy folder dla każdej identyfikator pakietu, folder numer wersji, z których każdy zawiera poziomu czyli odpowiedniego pakietu.
