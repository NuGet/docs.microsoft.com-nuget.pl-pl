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
# <a name="local-feeds"></a><span data-ttu-id="fba4a-103">Lokalne kanały informacyjne</span><span class="sxs-lookup"><span data-stu-id="fba4a-103">Local feeds</span></span>

<span data-ttu-id="fba4a-104">Lokalne źródła pakietów NuGet są po prostu hierarchicznymi strukturami folderów w sieci lokalnej (lub nawet na swoim komputerze), w których umieszczane są pakiety.</span><span class="sxs-lookup"><span data-stu-id="fba4a-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="fba4a-105">Te kanały informacyjne mogą być następnie używane jako źródła pakietów ze wszystkimi innymi operacjami NuGet przy użyciu interfejsu wiersza polecenia, Menedżera pakietów i konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="fba4a-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="fba4a-106">Aby włączyć źródło, Dodaj jego nazwę ścieżki (na przykład `\\myserver\packages`) do listy źródeł przy użyciu [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) [interfejsu użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md#package-sources) lub polecenia.</span><span class="sxs-lookup"><span data-stu-id="fba4a-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md#package-sources) or the [`nuget sources`](../reference/cli-reference/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="fba4a-107">Hierarchiczne struktury folderów są obsługiwane w NuGet 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="fba4a-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="fba4a-108">Starsze wersje programu NuGet używają tylko jednego folderu zawierającego pakiety, z których wydajność jest znacznie mniejsza niż struktura hierarchiczna.</span><span class="sxs-lookup"><span data-stu-id="fba4a-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="fba4a-109">Inicjowanie i obsługa folderów hierarchicznych</span><span class="sxs-lookup"><span data-stu-id="fba4a-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="fba4a-110">Hierarchiczne drzewo folderów z wersjami ma następującą strukturę ogólną:</span><span class="sxs-lookup"><span data-stu-id="fba4a-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="fba4a-111">Pakiet NuGet automatycznie tworzy tę strukturę przy użyciu [`nuget add`](../reference/cli-reference/cli-ref-add.md) polecenia do kopiowania pakietu do źródła danych:</span><span class="sxs-lookup"><span data-stu-id="fba4a-111">NuGet creates this structure automatically when you use the [`nuget add`](../reference/cli-reference/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="fba4a-112">`nuget add` Polecenie działa z jednym pakietem na raz, co może być niewygodne podczas konfigurowania kanału informacyjnego z wieloma pakietami.</span><span class="sxs-lookup"><span data-stu-id="fba4a-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="fba4a-113">W takich przypadkach należy użyć [`nuget init`](../reference/cli-reference/cli-ref-init.md) polecenia, aby skopiować wszystkie pakiety w folderze do źródła danych, tak jakby były uruchamiane `nuget add` osobno na każdym z nich.</span><span class="sxs-lookup"><span data-stu-id="fba4a-113">In such cases, use the [`nuget init`](../reference/cli-reference/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="fba4a-114">Na przykład następujące polecenie kopiuje wszystkie pakiety z `c:\packages` do `\\myserver\packages`drzewa hierarchicznego:</span><span class="sxs-lookup"><span data-stu-id="fba4a-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="fba4a-115">Podobnie jak w `add` przypadku polecenia `init` program tworzy folder dla każdego identyfikatora pakietu, z którego każdy zawiera folder numeru wersji, w którym jest odpowiednim pakietem.</span><span class="sxs-lookup"><span data-stu-id="fba4a-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
