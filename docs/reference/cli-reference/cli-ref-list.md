---
title: Polecenie listy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia list NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813341"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="939d1-103">list — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="939d1-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="939d1-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="939d1-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="939d1-105">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="939d1-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="939d1-106">Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w pliku konfiguracji globalnej, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="939d1-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="939d1-107">Jeśli `NuGet.Config` nie określa żadnych źródeł, `list` używa domyślnego kanału informacyjnego (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="939d1-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="939d1-108">Pomiar</span><span class="sxs-lookup"><span data-stu-id="939d1-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="939d1-109">gdzie opcjonalne terminy wyszukiwania będą filtrować listę wyświetlaną.</span><span class="sxs-lookup"><span data-stu-id="939d1-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="939d1-110">Terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="939d1-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="939d1-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="939d1-111">Options</span></span>

| <span data-ttu-id="939d1-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="939d1-112">Option</span></span> | <span data-ttu-id="939d1-113">Opis</span><span class="sxs-lookup"><span data-stu-id="939d1-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="939d1-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="939d1-114">AllVersions</span></span> | <span data-ttu-id="939d1-115">Wyświetl listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="939d1-115">List all versions of a package.</span></span> <span data-ttu-id="939d1-116">Domyślnie zostanie wyświetlona tylko Najnowsza wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="939d1-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="939d1-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="939d1-117">ConfigFile</span></span> | <span data-ttu-id="939d1-118">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="939d1-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="939d1-119">Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="939d1-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="939d1-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="939d1-120">ForceEnglishOutput</span></span> | <span data-ttu-id="939d1-121">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="939d1-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="939d1-122">Pomoc</span><span class="sxs-lookup"><span data-stu-id="939d1-122">Help</span></span> | <span data-ttu-id="939d1-123">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="939d1-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="939d1-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="939d1-124">IncludeDelisted</span></span> | <span data-ttu-id="939d1-125">*(3.2 +)* Wyświetlanie pakietów nieznajdujących się na liście.</span><span class="sxs-lookup"><span data-stu-id="939d1-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="939d1-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="939d1-126">NonInteractive</span></span> | <span data-ttu-id="939d1-127">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="939d1-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="939d1-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="939d1-128">PreRelease</span></span> | <span data-ttu-id="939d1-129">Zawiera pakiety wersji wstępnej znajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="939d1-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="939d1-130">Obiekt źródłowy</span><span class="sxs-lookup"><span data-stu-id="939d1-130">Source</span></span> | <span data-ttu-id="939d1-131">Określa listę źródeł pakietów do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="939d1-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="939d1-132">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="939d1-132">Verbosity</span></span> | <span data-ttu-id="939d1-133">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="939d1-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="939d1-134">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="939d1-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="939d1-135">Przykłady</span><span class="sxs-lookup"><span data-stu-id="939d1-135">Examples</span></span>

<span data-ttu-id="939d1-136">Wyświetl listę wszystkich pakietów ze skonfigurowanych źródeł:</span><span class="sxs-lookup"><span data-stu-id="939d1-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="939d1-137">Wyświetl listę pakietów związanych z platformą Azure z szczegółowym szczegółowośćem:</span><span class="sxs-lookup"><span data-stu-id="939d1-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="939d1-138">Wyświetl listę wszystkich wersji pakietów związanych z platformą Azure ze skonfigurowanych kanałów informacyjnych:</span><span class="sxs-lookup"><span data-stu-id="939d1-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="939d1-139">Wyświetl listę wszystkich wersji pakietów związanych z notacją JSON z określonego źródła/kanału informacyjnego:</span><span class="sxs-lookup"><span data-stu-id="939d1-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="939d1-140">Wyświetlanie listy pakietów związanych z notacją JSON z wielu źródeł/źródeł:</span><span class="sxs-lookup"><span data-stu-id="939d1-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

