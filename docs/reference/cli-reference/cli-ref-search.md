---
title: Polecenie wyszukiwania interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia Search
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623270"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="6e588-103">Search — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="6e588-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="6e588-104">**Dotyczy:** &bullet; **obsługiwane wersje pakietów:** 5.8 +</span><span class="sxs-lookup"><span data-stu-id="6e588-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="6e588-105">Wyszukuje dane źródło przy użyciu podanego ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="6e588-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="6e588-106">Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w% AppData% \NuGet\NuGet.config.</span><span class="sxs-lookup"><span data-stu-id="6e588-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="6e588-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="6e588-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="6e588-108">gdzie terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6e588-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="6e588-109">Opcje</span><span class="sxs-lookup"><span data-stu-id="6e588-109">Options</span></span>

| <span data-ttu-id="6e588-110">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6e588-110">Name</span></span> | <span data-ttu-id="6e588-111">Opis</span><span class="sxs-lookup"><span data-stu-id="6e588-111">Description</span></span> | <span data-ttu-id="6e588-112">Użycie</span><span class="sxs-lookup"><span data-stu-id="6e588-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="6e588-113">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="6e588-113">PreRelease</span></span> | <span data-ttu-id="6e588-114">Pakiety wersji wstępnej nie są uwzględniane domyślnie, ale mogą być dołączane za pomocą tego argumentu</span><span class="sxs-lookup"><span data-stu-id="6e588-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="6e588-115">-Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="6e588-115">-PreRelease</span></span> |
| <span data-ttu-id="6e588-116">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="6e588-116">Source</span></span> | <span data-ttu-id="6e588-117">Określone źródła pakietów do przeszukania zamiast wysyłania zapytań do domyślnych źródeł w __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="6e588-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="6e588-118">-Źródło `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="6e588-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="6e588-119">Take</span><span class="sxs-lookup"><span data-stu-id="6e588-119">Take</span></span> | <span data-ttu-id="6e588-120">Liczba wyników do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="6e588-120">The number of results to return.</span></span> <span data-ttu-id="6e588-121">Wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="6e588-121">The default value is 20.</span></span> | <span data-ttu-id="6e588-122">-Zrób `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="6e588-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="6e588-123">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="6e588-123">Verbosity</span></span> | <span data-ttu-id="6e588-124">Poziom szczegółowości, który ma być wyświetlany w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6e588-124">The level of detail to display in the output.</span></span> <span data-ttu-id="6e588-125">Wartość domyślna to _normalny_.</span><span class="sxs-lookup"><span data-stu-id="6e588-125">The default is _normal_.</span></span> <span data-ttu-id="6e588-126">(Zobacz uwagi poniżej)</span><span class="sxs-lookup"><span data-stu-id="6e588-126">(See the note below)</span></span>  | <span data-ttu-id="6e588-127">-Poziom szczegółowości `<quiet\|normal\|detailed>`</span><span class="sxs-lookup"><span data-stu-id="6e588-127">-Verbosity `<quiet\|normal\|detailed>`</span></span> |
| <span data-ttu-id="6e588-128">Pomoc</span><span class="sxs-lookup"><span data-stu-id="6e588-128">Help</span></span> | <span data-ttu-id="6e588-129">Wyświetla informacje pomocy dla polecenia</span><span class="sxs-lookup"><span data-stu-id="6e588-129">Displays help information for the command</span></span> | <span data-ttu-id="6e588-130">-Pomoc</span><span class="sxs-lookup"><span data-stu-id="6e588-130">-Help</span></span> |

<span data-ttu-id="6e588-131">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6e588-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

<span data-ttu-id="6e588-132">__UWAGA__</span><span class="sxs-lookup"><span data-stu-id="6e588-132">__NOTE__</span></span>

<span data-ttu-id="6e588-133">Poziomy szczegółowości:</span><span class="sxs-lookup"><span data-stu-id="6e588-133">Verbosity Levels:</span></span>

* <span data-ttu-id="6e588-134">_cichy_ — identyfikator pakietu, wersja</span><span class="sxs-lookup"><span data-stu-id="6e588-134">_quiet_ - Package ID, Version</span></span>
* <span data-ttu-id="6e588-135">_normalny_ — identyfikator pakietu, wersja, pobieranie, wersja zapoznawcza opisu</span><span class="sxs-lookup"><span data-stu-id="6e588-135">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
* <span data-ttu-id="6e588-136">_szczegółowy_ — identyfikator pakietu, wersja, pobieranie, pełny opis, inne informacje, takie jak adres URL zapytania</span><span class="sxs-lookup"><span data-stu-id="6e588-136">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="6e588-137">Przykłady</span><span class="sxs-lookup"><span data-stu-id="6e588-137">Examples</span></span>

<span data-ttu-id="6e588-138">Wyszukaj pakiety powiązane z *rejestrowaniem*ze źródeł domyślnych:</span><span class="sxs-lookup"><span data-stu-id="6e588-138">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="6e588-139">Wyszukaj pakiety związane z *rejestrowaniem*ze szczegółowym szczegółowośćem:</span><span class="sxs-lookup"><span data-stu-id="6e588-139">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="6e588-140">Wyszukaj pakiety związane z *rejestrowaniem*i Pokaż tylko 5 najważniejszych wyników:</span><span class="sxs-lookup"><span data-stu-id="6e588-140">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="6e588-141">Wyszukaj pakiety powiązane ze standardem *JSON*, w tym wersje wstępne, z określonych źródeł/źródła danych:</span><span class="sxs-lookup"><span data-stu-id="6e588-141">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="6e588-142">Wyszukaj pakiety powiązane ze standardem *JSON*z wielu źródeł/źródeł:</span><span class="sxs-lookup"><span data-stu-id="6e588-142">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
