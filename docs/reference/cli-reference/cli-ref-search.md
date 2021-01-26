---
title: Polecenie wyszukiwania interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia Search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779166"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="60517-103">Search — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="60517-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="60517-104">**Dotyczy:** &bullet; **obsługiwane wersje pakietów:** 5.8 +</span><span class="sxs-lookup"><span data-stu-id="60517-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="60517-105">Wyszukuje dane źródło przy użyciu podanego ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="60517-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="60517-106">Jeśli nie określono żadnych źródeł, używane są wszystkie źródła zdefiniowane w% AppData% \NuGet\NuGet.config.</span><span class="sxs-lookup"><span data-stu-id="60517-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="60517-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="60517-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="60517-108">gdzie terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów, tak jak w przypadku ich używania w programie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="60517-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="60517-109">Opcje</span><span class="sxs-lookup"><span data-stu-id="60517-109">Options</span></span>

| <span data-ttu-id="60517-110">Nazwa</span><span class="sxs-lookup"><span data-stu-id="60517-110">Name</span></span> | <span data-ttu-id="60517-111">Opis</span><span class="sxs-lookup"><span data-stu-id="60517-111">Description</span></span> | <span data-ttu-id="60517-112">Użycie</span><span class="sxs-lookup"><span data-stu-id="60517-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="60517-113">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="60517-113">PreRelease</span></span> | <span data-ttu-id="60517-114">Pakiety wersji wstępnej nie są uwzględniane domyślnie, ale mogą być dołączane za pomocą tego argumentu</span><span class="sxs-lookup"><span data-stu-id="60517-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="60517-115">-Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="60517-115">-PreRelease</span></span> |
| <span data-ttu-id="60517-116">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="60517-116">Source</span></span> | <span data-ttu-id="60517-117">Określone źródła pakietów do przeszukania zamiast wysyłania zapytań do domyślnych źródeł w __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="60517-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="60517-118">-Źródło `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="60517-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="60517-119">Take</span><span class="sxs-lookup"><span data-stu-id="60517-119">Take</span></span> | <span data-ttu-id="60517-120">Liczba wyników do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="60517-120">The number of results to return.</span></span> <span data-ttu-id="60517-121">Wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="60517-121">The default value is 20.</span></span> | <span data-ttu-id="60517-122">-Zrób `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="60517-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="60517-123">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="60517-123">Verbosity</span></span> | <span data-ttu-id="60517-124">Poziom szczegółowości, który ma być wyświetlany w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="60517-124">The level of detail to display in the output.</span></span> <span data-ttu-id="60517-125">Wartość domyślna to _normalny_.</span><span class="sxs-lookup"><span data-stu-id="60517-125">The default is _normal_.</span></span> <span data-ttu-id="60517-126">(Zobacz uwagi poniżej)</span><span class="sxs-lookup"><span data-stu-id="60517-126">(See the note below)</span></span>  | <span data-ttu-id="60517-127">-Poziom szczegółowości `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="60517-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="60517-128">Pomoc</span><span class="sxs-lookup"><span data-stu-id="60517-128">Help</span></span> | <span data-ttu-id="60517-129">Wyświetla informacje pomocy dla polecenia</span><span class="sxs-lookup"><span data-stu-id="60517-129">Displays help information for the command</span></span> | <span data-ttu-id="60517-130">-Pomoc</span><span class="sxs-lookup"><span data-stu-id="60517-130">-Help</span></span> |

<span data-ttu-id="60517-131">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="60517-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="60517-132">Poziomy szczegółowości:</span><span class="sxs-lookup"><span data-stu-id="60517-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="60517-133">_cichy_ — identyfikator pakietu, wersja</span><span class="sxs-lookup"><span data-stu-id="60517-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="60517-134">_normalny_ — identyfikator pakietu, wersja, pobieranie, wersja zapoznawcza opisu</span><span class="sxs-lookup"><span data-stu-id="60517-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="60517-135">_szczegółowy_ — identyfikator pakietu, wersja, pobieranie, pełny opis, inne informacje, takie jak adres URL zapytania</span><span class="sxs-lookup"><span data-stu-id="60517-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="60517-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="60517-136">Examples</span></span>

<span data-ttu-id="60517-137">Wyszukaj pakiety powiązane z *rejestrowaniem* ze źródeł domyślnych:</span><span class="sxs-lookup"><span data-stu-id="60517-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="60517-138">Wyszukaj pakiety związane z *rejestrowaniem* ze szczegółowym szczegółowośćem:</span><span class="sxs-lookup"><span data-stu-id="60517-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="60517-139">Wyszukaj pakiety związane z *rejestrowaniem* i Pokaż tylko 5 najważniejszych wyników:</span><span class="sxs-lookup"><span data-stu-id="60517-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="60517-140">Wyszukaj pakiety powiązane ze standardem *JSON*, w tym wersje wstępne, z określonych źródeł/źródła danych:</span><span class="sxs-lookup"><span data-stu-id="60517-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="60517-141">Wyszukaj pakiety powiązane ze standardem *JSON* z wielu źródeł/źródeł:</span><span class="sxs-lookup"><span data-stu-id="60517-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
