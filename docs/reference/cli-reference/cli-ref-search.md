---
title: Polecenie wyszukiwania interfejsu wiersza polecenia nuGet
description: Odwołanie do polecenia nuget.exe wyszukiwania
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323664"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="5119d-103">search , polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="5119d-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="5119d-104">**Dotyczy: zużycie** pakietu &bullet; **Obsługiwane wersje:** 5.8+</span><span class="sxs-lookup"><span data-stu-id="5119d-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="5119d-105">Wyszukuje dane źródło przy użyciu podanego ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="5119d-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="5119d-106">Jeśli nie określono żadnych źródeł, wszystkie źródła zdefiniowane w %AppData%\NuGet\NuGet.Config są używane.</span><span class="sxs-lookup"><span data-stu-id="5119d-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="5119d-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="5119d-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="5119d-108">gdzie terminy wyszukiwania są stosowane do nazw pakietów, tagów i opisów pakietów tak samo, jak w przypadku używania ich w nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5119d-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="5119d-109">Opcje</span><span class="sxs-lookup"><span data-stu-id="5119d-109">Options</span></span>

| <span data-ttu-id="5119d-110">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5119d-110">Name</span></span> | <span data-ttu-id="5119d-111">Opis</span><span class="sxs-lookup"><span data-stu-id="5119d-111">Description</span></span> | <span data-ttu-id="5119d-112">Użycie</span><span class="sxs-lookup"><span data-stu-id="5119d-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="5119d-113">Wstępną</span><span class="sxs-lookup"><span data-stu-id="5119d-113">PreRelease</span></span> | <span data-ttu-id="5119d-114">Pakiety wersji wstępnej nie są domyślnie uwzględniane, ale mogą zostać dołączone przy użyciu tego argumentu</span><span class="sxs-lookup"><span data-stu-id="5119d-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="5119d-115">-PreRelease</span><span class="sxs-lookup"><span data-stu-id="5119d-115">-PreRelease</span></span> |
| <span data-ttu-id="5119d-116">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="5119d-116">Source</span></span> | <span data-ttu-id="5119d-117">Określone źródła pakietów do wyszukiwania zamiast wykonywania zapytań o domyślne źródła w __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="5119d-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="5119d-118">-Źródło `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="5119d-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="5119d-119">Take</span><span class="sxs-lookup"><span data-stu-id="5119d-119">Take</span></span> | <span data-ttu-id="5119d-120">Liczba wyników do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="5119d-120">The number of results to return.</span></span> <span data-ttu-id="5119d-121">Wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="5119d-121">The default value is 20.</span></span> | <span data-ttu-id="5119d-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="5119d-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="5119d-123">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="5119d-123">Verbosity</span></span> | <span data-ttu-id="5119d-124">Poziom szczegółowości do wyświetlenia w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5119d-124">The level of detail to display in the output.</span></span> <span data-ttu-id="5119d-125">Wartość domyślna to _normalna_.</span><span class="sxs-lookup"><span data-stu-id="5119d-125">The default is _normal_.</span></span> <span data-ttu-id="5119d-126">(Patrz uwaga poniżej)</span><span class="sxs-lookup"><span data-stu-id="5119d-126">(See the note below)</span></span>  | <span data-ttu-id="5119d-127">-Poziom szczegółowości `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="5119d-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="5119d-128">Help</span><span class="sxs-lookup"><span data-stu-id="5119d-128">Help</span></span> | <span data-ttu-id="5119d-129">Wyświetla informacje pomocy dotyczące polecenia</span><span class="sxs-lookup"><span data-stu-id="5119d-129">Displays help information for the command</span></span> | <span data-ttu-id="5119d-130">- Pomoc</span><span class="sxs-lookup"><span data-stu-id="5119d-130">-Help</span></span> |

<span data-ttu-id="5119d-131">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5119d-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="5119d-132">Poziomy szczegółowości:</span><span class="sxs-lookup"><span data-stu-id="5119d-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="5119d-133">_quiet_ — identyfikator pakietu, wersja</span><span class="sxs-lookup"><span data-stu-id="5119d-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="5119d-134">_normal_ — identyfikator pakietu, wersja, pliki do pobrania, wersja zapoznawcza opisu</span><span class="sxs-lookup"><span data-stu-id="5119d-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="5119d-135">_szczegółowe_ — identyfikator pakietu, wersja, pliki do pobrania, pełny opis, inne informacje, takie jak adres URL zapytania</span><span class="sxs-lookup"><span data-stu-id="5119d-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="5119d-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5119d-136">Examples</span></span>

<span data-ttu-id="5119d-137">Wyszukaj pakiety *związane z rejestrowaniem* z domyślnych źródeł:</span><span class="sxs-lookup"><span data-stu-id="5119d-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="5119d-138">Wyszukaj pakiety *związane z* rejestrowaniem ze szczegółowymi informacjami:</span><span class="sxs-lookup"><span data-stu-id="5119d-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="5119d-139">Wyszukaj pakiety *związane z* rejestrowaniem i wyświetl tylko 5 najlepszych wyników:</span><span class="sxs-lookup"><span data-stu-id="5119d-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="5119d-140">Wyszukaj pakiety *związane z kodem JSON,* w tym wersje wstępne, z określonego źródła/źródła danych:</span><span class="sxs-lookup"><span data-stu-id="5119d-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="5119d-141">Wyszukaj pakiety *związane z JSON* z wielu źródeł/źródeł danych:</span><span class="sxs-lookup"><span data-stu-id="5119d-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
