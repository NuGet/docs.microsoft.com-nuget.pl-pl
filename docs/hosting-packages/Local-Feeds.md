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
# <a name="local-feeds"></a><span data-ttu-id="aac7b-103">Lokalne kanały informacyjne</span><span class="sxs-lookup"><span data-stu-id="aac7b-103">Local feeds</span></span>

<span data-ttu-id="aac7b-104">Lokalne źródła danych pakietu NuGet są po prostu hierarchicznymi strukturami folderów w sieci lokalnej (lub nawet tylko na własnym komputerze), w których umieszczasz pakiety.</span><span class="sxs-lookup"><span data-stu-id="aac7b-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="aac7b-105">Te źródła danych mogą być następnie używane jako źródła pakietów ze wszystkimi innymi operacjami NuGet przy użyciu interfejsu wiersza polecenia, interfejsu użytkownika Menedżera pakietów i konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="aac7b-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="aac7b-106">Aby włączyć źródło, dodaj jego nazwa `\\myserver\packages`ścieżki (na przykład) do listy źródeł przy [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) użyciu interfejsu użytkownika Menedżera [pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources) lub polecenia.</span><span class="sxs-lookup"><span data-stu-id="aac7b-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="aac7b-107">Hierarchiczne struktury folderów są obsługiwane w nuget 3.3+.</span><span class="sxs-lookup"><span data-stu-id="aac7b-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="aac7b-108">Starsze wersje NuGet używać tylko jeden folder zawierający pakiety, z których wydajność jest znacznie niższa niż hierarchicznej struktury.</span><span class="sxs-lookup"><span data-stu-id="aac7b-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="aac7b-109">Inicjowanie i obsługa folderów hierarchicznych</span><span class="sxs-lookup"><span data-stu-id="aac7b-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="aac7b-110">Hierarchiczne drzewo folderów wersjlowane ma następującą strukturę ogólną:</span><span class="sxs-lookup"><span data-stu-id="aac7b-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="aac7b-111">NuGet tworzy tę strukturę automatycznie, gdy używasz [`nuget add`](../reference/cli-reference/cli-ref-add.md) polecenia do kopiowania pakietu do źródła danych:</span><span class="sxs-lookup"><span data-stu-id="aac7b-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="aac7b-112">Polecenie `nuget add` działa z jednym pakietem naraz, co może być niewygodne podczas konfigurowania kanału informacyjnego z wieloma pakietami.</span><span class="sxs-lookup"><span data-stu-id="aac7b-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="aac7b-113">W takich przypadkach [`nuget init`](../reference/cli-reference/cli-ref-init.md) użyj polecenia, aby skopiować wszystkie pakiety `nuget add` w folderze do kanału informacyjnego, tak jakby uruchomiono na każdym z nich indywidualnie.</span><span class="sxs-lookup"><span data-stu-id="aac7b-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="aac7b-114">Na przykład następujące polecenie kopiuje `c:\packages` wszystkie pakiety `\\myserver\packages`z drzewa hierarchicznego na:</span><span class="sxs-lookup"><span data-stu-id="aac7b-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="aac7b-115">Podobnie jak `add` w `init` przypadku polecenia, tworzy folder dla każdego identyfikatora pakietu, z których każdy zawiera folder numeru wersji, w którym znajduje się odpowiedni pakiet.</span><span class="sxs-lookup"><span data-stu-id="aac7b-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
