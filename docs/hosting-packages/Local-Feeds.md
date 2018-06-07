---
title: Konfigurowanie lokalnych źródeł danych NuGet
description: Jak utworzyć lokalnego źródła danych za pomocą folderów w sieci lokalnej pakietów NuGet
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 5d86657bdf26452d027593b953168e28694acf82
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818688"
---
# <a name="local-feeds"></a><span data-ttu-id="4a44d-103">Lokalne źródła danych</span><span class="sxs-lookup"><span data-stu-id="4a44d-103">Local feeds</span></span>

<span data-ttu-id="4a44d-104">Lokalne źródła danych pakietu NuGet są struktury po prostu hierarchiczna folderów w sieci lokalnej (lub nawet po prostu swojego komputera), w którym zostanie umieszczony pakietów.</span><span class="sxs-lookup"><span data-stu-id="4a44d-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="4a44d-105">Te źródła danych mogą następnie służyć jako źródła pakietów z innymi operacjami NuGet przy użyciu interfejsu wiersza polecenia, interfejs użytkownika Menedżera pakietów i konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="4a44d-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="4a44d-106">Aby włączyć źródła, dodaj jego pathname (takich jak `\\myserver\packages`) do listy źródeł za pomocą [interfejsu użytkownika Menedżera pakietów](../tools/package-manager-ui.md#package-sources) lub [ `nuget sources` ](../tools/cli-ref-sources.md) polecenia.</span><span class="sxs-lookup"><span data-stu-id="4a44d-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="4a44d-107">Struktury folderów hierarchicznych są obsługiwane w NuGet 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="4a44d-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="4a44d-108">Starsze wersje programu NuGet Użyj tylko pojedynczy folder zawierający pakiety, z którymi jest znacznie niższa niż strukturę hierarchiczną wydajności.</span><span class="sxs-lookup"><span data-stu-id="4a44d-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="4a44d-109">Inicjowanie i utrzymywanie folderów hierarchicznych</span><span class="sxs-lookup"><span data-stu-id="4a44d-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="4a44d-110">Hierarchiczna folder z kontrolą wersji drzewa ma następującą strukturę ogólne:</span><span class="sxs-lookup"><span data-stu-id="4a44d-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="4a44d-111">NuGet tworzy automatycznie tej struktury, korzystając z [ `nuget add` ](../tools/cli-ref-add.md) polecenie, aby skopiować pakiet do źródła danych:</span><span class="sxs-lookup"><span data-stu-id="4a44d-111">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="4a44d-112">`nuget add` Polecenia współpracuje z jednym pakiecie w czasie, który może być niewygodne, podczas konfigurowania źródła danych z wielu pakietów.</span><span class="sxs-lookup"><span data-stu-id="4a44d-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="4a44d-113">W takiej sytuacji należy użyć [ `nuget init` ](../tools/cli-ref-init.md) polecenie, aby skopiować wszystkie pakiety w folderze do źródła danych, jak w przypadku uruchomienia `nuget add` na każdej z nich osobno.</span><span class="sxs-lookup"><span data-stu-id="4a44d-113">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="4a44d-114">Na przykład następujące polecenie kopiuje wszystkie pakiety z `c:\packages` hierarchiczne drzewa na `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="4a44d-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="4a44d-115">Jak `add` polecenia `init` tworzy folder dla każdej identyfikator pakietu, folder numer wersji, z których każdy zawiera poziomu czyli odpowiedniego pakietu.</span><span class="sxs-lookup"><span data-stu-id="4a44d-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
