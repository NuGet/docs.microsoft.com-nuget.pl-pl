---
title: Usługa Index, interfejs API programu NuGet
description: Indeks usług jest punkt wejścia interfejsu API protokołu HTTP NuGet i wylicza możliwości serwera.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324724"
---
# <a name="service-index"></a><span data-ttu-id="fd6ca-103">Indeks usług</span><span class="sxs-lookup"><span data-stu-id="fd6ca-103">Service index</span></span>

<span data-ttu-id="fd6ca-104">Indeks usług to dokument JSON, który jest punktem wejścia dla źródła pakietów NuGet i umożliwia implementacji klienta odkryć możliwości źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="fd6ca-105">Indeks usług jest obiekt JSON z dwoma wymagane właściwości: `version` (wersja schematu indeksu service) i `resources` (punkty końcowe lub możliwości źródła pakietu).</span><span class="sxs-lookup"><span data-stu-id="fd6ca-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="fd6ca-106">Indeks usług usługi nuget.org znajduje się w `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="fd6ca-107">Obsługa wersji</span><span class="sxs-lookup"><span data-stu-id="fd6ca-107">Versioning</span></span>

<span data-ttu-id="fd6ca-108">`version` Wartość jest ciągiem wersji parseable SemVer 2.0.0, który wskazuje wersję schematu indeksu usługi.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="fd6ca-109">Interfejs API określającemu, że ciąg wersji zawiera numer wersji głównej `3`.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="fd6ca-110">Wprowadzaniu zmian niepowodujących niezgodności na schemat indeksu service, wersja pomocnicza ciąg wersji zostanie zwiększona.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="fd6ca-111">Każdy zasób w indeksie usługi jest numery wersji niezależne od wersji schematu indeksu usługi.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="fd6ca-112">Bieżąca wersja schematu to `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="fd6ca-113">`3.0.0` Wersja jest funkcjonalnie równoważny ze starszą wersją `3.0.0-beta.1` wersji, ale powinien być preferowany, jak wyraźniej komunikuje się ona stabilny, definicja schematu.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fd6ca-114">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="fd6ca-114">HTTP methods</span></span>

<span data-ttu-id="fd6ca-115">Indeks usług jest dostępna przy użyciu metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="fd6ca-116">Resources</span><span class="sxs-lookup"><span data-stu-id="fd6ca-116">Resources</span></span>

<span data-ttu-id="fd6ca-117">`resources` Właściwość zawiera szereg zasobów obsługiwana przez tego źródła pakietów.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="fd6ca-118">Zasób</span><span class="sxs-lookup"><span data-stu-id="fd6ca-118">Resource</span></span>

<span data-ttu-id="fd6ca-119">Zasób jest obiektem w `resources` tablicy.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="fd6ca-120">Reprezentuje wersjonowany możliwości źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="fd6ca-121">Zasób ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fd6ca-121">A resource has the following properties:</span></span>

<span data-ttu-id="fd6ca-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fd6ca-122">Name</span></span>          | <span data-ttu-id="fd6ca-123">Typ</span><span class="sxs-lookup"><span data-stu-id="fd6ca-123">Type</span></span>   | <span data-ttu-id="fd6ca-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fd6ca-124">Required</span></span> | <span data-ttu-id="fd6ca-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fd6ca-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="fd6ca-126">string</span><span class="sxs-lookup"><span data-stu-id="fd6ca-126">string</span></span> | <span data-ttu-id="fd6ca-127">tak</span><span class="sxs-lookup"><span data-stu-id="fd6ca-127">yes</span></span>      | <span data-ttu-id="fd6ca-128">Adres URL do zasobu</span><span class="sxs-lookup"><span data-stu-id="fd6ca-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="fd6ca-129">string</span><span class="sxs-lookup"><span data-stu-id="fd6ca-129">string</span></span> | <span data-ttu-id="fd6ca-130">tak</span><span class="sxs-lookup"><span data-stu-id="fd6ca-130">yes</span></span>      | <span data-ttu-id="fd6ca-131">Stała typu string, reprezentujący typ zasobu</span><span class="sxs-lookup"><span data-stu-id="fd6ca-131">A string constant representing the resource type</span></span>
<span data-ttu-id="fd6ca-132">komentarz</span><span class="sxs-lookup"><span data-stu-id="fd6ca-132">comment</span></span>       | <span data-ttu-id="fd6ca-133">string</span><span class="sxs-lookup"><span data-stu-id="fd6ca-133">string</span></span> | <span data-ttu-id="fd6ca-134">Brak</span><span class="sxs-lookup"><span data-stu-id="fd6ca-134">no</span></span>       | <span data-ttu-id="fd6ca-135">Ludzi, czytelny opis zasobu</span><span class="sxs-lookup"><span data-stu-id="fd6ca-135">A human readable description of the resource</span></span>

<span data-ttu-id="fd6ca-136">`@id` Jest adres URL, który musi być bezwzględna i muszą mieć schemat HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="fd6ca-137">`@type` Służy do identyfikowania określonych protokół do użycia podczas interakcji z zasobów.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="fd6ca-138">Typ zasobu to nieprzezroczysty ciąg, ale zazwyczaj ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="fd6ca-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="fd6ca-139">Klienci powinni kodowi twardych `@type` wartości zrozumieć i wyszukiwać w indeksie usługi źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="fd6ca-140">Dokładnie `@type` wartości w obecnie są wyliczane na dokumenty referencyjne poszczególnych zasobów, które są wymienione w [omówienie interfejsu API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="fd6ca-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="fd6ca-141">Dla tej dokumentacji dokumentacji dotyczącej różnych zasobów zasadniczo można grupować według `{RESOURCE_NAME}` znaleziony w indeksie usługi, która jest analogiczna do grupowania według scenariusza.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="fd6ca-142">Nie jest wymagane, że każdy zasób ma unikatową `@id` lub `@type`.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="fd6ca-143">Jest implementacji klienta, aby określić zasoby, które preferowanie za pośrednictwem innego.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="fd6ca-144">Jest to jedna implementacja to możliwe, że zasoby o tej samej lub zgodny `@type` mogą być używane w okrężne w razie awarii lub serwera błąd połączenia.</span><span class="sxs-lookup"><span data-stu-id="fd6ca-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fd6ca-145">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="fd6ca-145">Sample request</span></span>

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a><span data-ttu-id="fd6ca-146">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="fd6ca-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
