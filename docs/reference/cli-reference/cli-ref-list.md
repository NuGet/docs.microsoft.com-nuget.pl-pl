---
title: Polecenie listy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia list NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328325"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="fa014-103">list — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="fa014-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="fa014-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="fa014-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fa014-105">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="fa014-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="fa014-106">Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w globalnym pliku `%AppData%\NuGet\NuGet.Config` konfiguracji (system Windows `~/.nuget/NuGet/NuGet.Config`) lub,.</span><span class="sxs-lookup"><span data-stu-id="fa014-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="fa014-107">Jeśli `NuGet.Config` nie określa żadnych źródeł `list` , program używa domyślnego kanału informacyjnego (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="fa014-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="fa014-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="fa014-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="fa014-109">gdzie opcjonalne terminy wyszukiwania będą filtrować listę wyświetlaną.</span><span class="sxs-lookup"><span data-stu-id="fa014-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="fa014-110">Terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fa014-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="fa014-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="fa014-111">Options</span></span>

| <span data-ttu-id="fa014-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="fa014-112">Option</span></span> | <span data-ttu-id="fa014-113">Opis</span><span class="sxs-lookup"><span data-stu-id="fa014-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fa014-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="fa014-114">AllVersions</span></span> | <span data-ttu-id="fa014-115">Wyświetl listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa014-115">List all versions of a package.</span></span> <span data-ttu-id="fa014-116">Domyślnie zostanie wyświetlona tylko Najnowsza wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa014-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="fa014-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fa014-117">ConfigFile</span></span> | <span data-ttu-id="fa014-118">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="fa014-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fa014-119">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fa014-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fa014-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fa014-120">ForceEnglishOutput</span></span> | <span data-ttu-id="fa014-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="fa014-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fa014-122">Help</span><span class="sxs-lookup"><span data-stu-id="fa014-122">Help</span></span> | <span data-ttu-id="fa014-123">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="fa014-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="fa014-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="fa014-124">IncludeDelisted</span></span> | <span data-ttu-id="fa014-125">*(3.2 +)* Wyświetlanie pakietów nieznajdujących się na liście.</span><span class="sxs-lookup"><span data-stu-id="fa014-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="fa014-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fa014-126">NonInteractive</span></span> | <span data-ttu-id="fa014-127">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa014-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fa014-128">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="fa014-128">PreRelease</span></span> | <span data-ttu-id="fa014-129">Zawiera pakiety wersji wstępnej znajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="fa014-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="fa014-130">Source</span><span class="sxs-lookup"><span data-stu-id="fa014-130">Source</span></span> | <span data-ttu-id="fa014-131">Określa listę źródeł pakietów do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="fa014-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="fa014-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fa014-132">Verbosity</span></span> | <span data-ttu-id="fa014-133">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="fa014-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fa014-134">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fa014-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fa014-135">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fa014-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
