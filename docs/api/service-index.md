---
title: Indeks usługi, interfejs API NuGet
description: Indeks usługi jest punktem wejścia interfejsu API protokołu HTTP NuGet i wylicza możliwości serwera programu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775359"
---
# <a name="service-index"></a><span data-ttu-id="b62ff-103">Indeks usług</span><span class="sxs-lookup"><span data-stu-id="b62ff-103">Service index</span></span>

<span data-ttu-id="b62ff-104">Indeks usługi to dokument JSON, który jest punktem wejścia dla źródła pakietu NuGet i umożliwia implementacji klienta odnajdywanie możliwości źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="b62ff-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="b62ff-105">Indeks usługi jest obiektem JSON z dwiema wymaganymi właściwościami: `version` (wersja schematu indeksu usługi) i `resources`  (punkty końcowe lub możliwości źródła pakietu).</span><span class="sxs-lookup"><span data-stu-id="b62ff-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="b62ff-106">Pakiet NuGet. indeks usługi organizacji znajduje się w lokalizacji `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="b62ff-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="b62ff-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="b62ff-107">Versioning</span></span>

<span data-ttu-id="b62ff-108">`version`Wartość jest ciągiem wersji SemVer 2.0.0, który wskazuje wersję schematu indeksu usługi.</span><span class="sxs-lookup"><span data-stu-id="b62ff-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="b62ff-109">Interfejs API wymaga, aby ciąg wersji miał wersję główną `3` .</span><span class="sxs-lookup"><span data-stu-id="b62ff-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="b62ff-110">Ponieważ zmiany niekrytyczne są wprowadzane do schematu indeksu usługi, zostanie zwiększona wersja pomocnicza ciągu wersji.</span><span class="sxs-lookup"><span data-stu-id="b62ff-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="b62ff-111">Każdy zasób w indeksie usługi jest zależny od wersji schematu indeksu usługi.</span><span class="sxs-lookup"><span data-stu-id="b62ff-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="b62ff-112">Bieżąca wersja schematu to `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="b62ff-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="b62ff-113">`3.0.0`Wersja jest funkcjonalnie równoważna ze starszą `3.0.0-beta.1` wersją, ale powinna być preferowana, ponieważ bardziej wyraźnie komunikuje się stabilny, zdefiniowany schemat.</span><span class="sxs-lookup"><span data-stu-id="b62ff-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b62ff-114">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="b62ff-114">HTTP methods</span></span>

<span data-ttu-id="b62ff-115">Indeks usługi jest dostępny przy użyciu metod HTTP `GET` i `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="b62ff-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="b62ff-116">Zasoby</span><span class="sxs-lookup"><span data-stu-id="b62ff-116">Resources</span></span>

<span data-ttu-id="b62ff-117">`resources`Właściwość zawiera tablicę zasobów obsługiwaną przez to źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="b62ff-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="b62ff-118">Zasób</span><span class="sxs-lookup"><span data-stu-id="b62ff-118">Resource</span></span>

<span data-ttu-id="b62ff-119">Zasób jest obiektem w `resources` tablicy.</span><span class="sxs-lookup"><span data-stu-id="b62ff-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="b62ff-120">Reprezentuje możliwość wersji źródłowej pakietu.</span><span class="sxs-lookup"><span data-stu-id="b62ff-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="b62ff-121">Zasób ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="b62ff-121">A resource has the following properties:</span></span>

<span data-ttu-id="b62ff-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b62ff-122">Name</span></span>          | <span data-ttu-id="b62ff-123">Typ</span><span class="sxs-lookup"><span data-stu-id="b62ff-123">Type</span></span>   | <span data-ttu-id="b62ff-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b62ff-124">Required</span></span> | <span data-ttu-id="b62ff-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b62ff-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="b62ff-126">ciąg</span><span class="sxs-lookup"><span data-stu-id="b62ff-126">string</span></span> | <span data-ttu-id="b62ff-127">tak</span><span class="sxs-lookup"><span data-stu-id="b62ff-127">yes</span></span>      | <span data-ttu-id="b62ff-128">Adres URL zasobu</span><span class="sxs-lookup"><span data-stu-id="b62ff-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="b62ff-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="b62ff-129">string</span></span> | <span data-ttu-id="b62ff-130">tak</span><span class="sxs-lookup"><span data-stu-id="b62ff-130">yes</span></span>      | <span data-ttu-id="b62ff-131">Stała w postaci ciągu reprezentująca typ zasobu</span><span class="sxs-lookup"><span data-stu-id="b62ff-131">A string constant representing the resource type</span></span>
<span data-ttu-id="b62ff-132">komentarz</span><span class="sxs-lookup"><span data-stu-id="b62ff-132">comment</span></span>       | <span data-ttu-id="b62ff-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="b62ff-133">string</span></span> | <span data-ttu-id="b62ff-134">nie</span><span class="sxs-lookup"><span data-stu-id="b62ff-134">no</span></span>       | <span data-ttu-id="b62ff-135">Czytelny dla człowieka opis zasobu</span><span class="sxs-lookup"><span data-stu-id="b62ff-135">A human readable description of the resource</span></span>

<span data-ttu-id="b62ff-136">`@id`Jest adresem URL, który musi być bezwzględny i musi mieć schemat http lub https.</span><span class="sxs-lookup"><span data-stu-id="b62ff-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="b62ff-137">Służy `@type` do identyfikowania określonego protokołu, który ma być używany podczas korzystania z zasobów.</span><span class="sxs-lookup"><span data-stu-id="b62ff-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="b62ff-138">Typ zasobu jest nieprzezroczystym ciągiem, ale zazwyczaj ma format:</span><span class="sxs-lookup"><span data-stu-id="b62ff-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="b62ff-139">Klienci oczekują na `@type` poznanie zrozumiałych wartości i poszukaj ich w indeksie usługi źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="b62ff-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="b62ff-140">Dokładne `@type` wartości używane dzisiaj są wyliczane na poszczególnych dokumentach odwołań do zasobów wymienionych w temacie [Omówienie interfejsu API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="b62ff-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="b62ff-141">Ze względu na tę dokumentację dokumentacja dotycząca różnych zasobów zostanie zasadniczo pogrupowana według `{RESOURCE_NAME}` znalezionych w indeksie usługi, które są analogiczne do grupowania według scenariusza.</span><span class="sxs-lookup"><span data-stu-id="b62ff-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="b62ff-142">Nie istnieje wymóg, że każdy zasób ma unikatowy `@id` lub `@type` .</span><span class="sxs-lookup"><span data-stu-id="b62ff-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="b62ff-143">Jest to implementacja klienta, aby określić, który zasób ma być preferowany przez inny.</span><span class="sxs-lookup"><span data-stu-id="b62ff-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="b62ff-144">Jedną z możliwych implementacji jest to, że zasoby tego samego lub zgodne `@type` mogą być używane w sposób okrężny w przypadku awarii połączenia lub błędu serwera.</span><span class="sxs-lookup"><span data-stu-id="b62ff-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="b62ff-145">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="b62ff-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="b62ff-146">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="b62ff-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
