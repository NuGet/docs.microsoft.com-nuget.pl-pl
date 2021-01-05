---
title: Polecenie listy interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia nuget.exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d8e5c8574b44375e651f3ff1a4868681b3ce6d66
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699849"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="d76be-103">list — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="d76be-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="d76be-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="d76be-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d76be-105">Wyświetla listę pakietów z danego źródła.</span><span class="sxs-lookup"><span data-stu-id="d76be-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="d76be-106">Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w globalnym pliku konfiguracji `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` ,.</span><span class="sxs-lookup"><span data-stu-id="d76be-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="d76be-107">Jeśli `NuGet.Config` nie określa żadnych źródeł, program `list` używa domyślnego kanału informacyjnego (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="d76be-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="d76be-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="d76be-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="d76be-109">gdzie opcjonalne terminy wyszukiwania będą filtrować listę wyświetlaną.</span><span class="sxs-lookup"><span data-stu-id="d76be-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="d76be-110">[Terminy wyszukiwania](../../consume-packages/finding-and-choosing-packages.md#search-syntax) są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d76be-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="d76be-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="d76be-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="d76be-112">Wyświetl listę wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="d76be-112">List all versions of a package.</span></span> <span data-ttu-id="d76be-113">Domyślnie zostanie wyświetlona tylko Najnowsza wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="d76be-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d76be-114">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="d76be-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d76be-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="d76be-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d76be-116">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="d76be-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d76be-117">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="d76be-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="d76be-118">*(3.2 +)* Wyświetlanie pakietów nieznajdujących się na liście.</span><span class="sxs-lookup"><span data-stu-id="d76be-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d76be-119">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d76be-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="d76be-120">Zawiera pakiety wersji wstępnej znajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="d76be-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="d76be-121">Źródło pakietu do przeszukania.</span><span class="sxs-lookup"><span data-stu-id="d76be-121">The package source to search.</span></span> <span data-ttu-id="d76be-122">Można określić wiele źródeł przy użyciu `-Source` opcji wiele razy.</span><span class="sxs-lookup"><span data-stu-id="d76be-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d76be-123">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d76be-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d76be-124">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d76be-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d76be-125">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d76be-125">Examples</span></span>

<span data-ttu-id="d76be-126">Wyświetl listę wszystkich pakietów ze skonfigurowanych źródeł:</span><span class="sxs-lookup"><span data-stu-id="d76be-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="d76be-127">Wyświetl listę pakietów związanych z platformą Azure z szczegółowym szczegółowośćem:</span><span class="sxs-lookup"><span data-stu-id="d76be-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="d76be-128">Wyświetl listę wszystkich wersji pakietów związanych z platformą Azure ze skonfigurowanych kanałów informacyjnych:</span><span class="sxs-lookup"><span data-stu-id="d76be-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="d76be-129">Wyświetl listę wszystkich wersji pakietów związanych z notacją JSON z określonego źródła/kanału informacyjnego:</span><span class="sxs-lookup"><span data-stu-id="d76be-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="d76be-130">Wyświetlanie listy pakietów związanych z notacją JSON z wielu źródeł/źródeł:</span><span class="sxs-lookup"><span data-stu-id="d76be-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
