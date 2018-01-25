---
title: "Indeks usługi, NuGet interfejsu API | Dokumentacja firmy Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Indeks usługi jest punkt wejścia interfejsu API HTTP NuGet i wylicza możliwości serwera."
keywords: "Punkt wejścia NuGet interfejsu API, NuGetA PI odnajdowania punktu końcowego"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="service-index"></a><span data-ttu-id="0ccd9-104">Indeks usługi</span><span class="sxs-lookup"><span data-stu-id="0ccd9-104">Service index</span></span>

<span data-ttu-id="0ccd9-105">Indeks usługi jest dokumentem JSON, który jest punkt wejścia dla źródła pakietów NuGet i umożliwia implementacja klienta wykryć możliwości źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="0ccd9-106">Indeks usługi jest obiektem JSON z dwóch wymaganych właściwości: `version` (wersja schematu indeksu service) i `resources` (punktów końcowych lub możliwości źródła pakietu).</span><span class="sxs-lookup"><span data-stu-id="0ccd9-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="0ccd9-107">Indeks usługi nuget.org znajduje się pod adresem `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="0ccd9-108">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="0ccd9-108">Versioning</span></span>

<span data-ttu-id="0ccd9-109">`version` Wartość jest ciągiem parseable wersji programu SemVer 2.0.0, co oznacza wersji schematu indeksu usługi.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span>
<span data-ttu-id="0ccd9-110">Interfejs API wymaga, że ciąg wersji ma numer wersji głównej `3`.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="0ccd9-111">Nierozdzielające zmiany do schematu indeksu usługi, zostanie zwiększona wersja pomocnicza ciąg wersji.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="0ccd9-112">Każdy zasób w indeksie usługi jest kontrolą wersji niezależnie od wersji schematu indeksu usługi.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="0ccd9-113">Bieżąca wersja schematu jest `3.0.0-beta.1`.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-113">The current schema version is `3.0.0-beta.1`.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0ccd9-114">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="0ccd9-114">HTTP methods</span></span>

<span data-ttu-id="0ccd9-115">Indeks usługa jest dostępna przy użyciu metody HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="0ccd9-116">Resources</span><span class="sxs-lookup"><span data-stu-id="0ccd9-116">Resources</span></span>

<span data-ttu-id="0ccd9-117">`resources` Właściwość zawiera tablicę obsługiwane przez to źródło pakietu zasobów.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="0ccd9-118">Zasób</span><span class="sxs-lookup"><span data-stu-id="0ccd9-118">Resource</span></span>

<span data-ttu-id="0ccd9-119">Zasób jest obiektem w `resources` tablicy.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="0ccd9-120">Reprezentuje on określonej wersji możliwości źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="0ccd9-121">Zasób ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="0ccd9-121">A resource has the following properties:</span></span>

<span data-ttu-id="0ccd9-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0ccd9-122">Name</span></span>          | <span data-ttu-id="0ccd9-123">Typ</span><span class="sxs-lookup"><span data-stu-id="0ccd9-123">Type</span></span>   | <span data-ttu-id="0ccd9-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0ccd9-124">Required</span></span> | <span data-ttu-id="0ccd9-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="0ccd9-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="0ccd9-126">string</span><span class="sxs-lookup"><span data-stu-id="0ccd9-126">string</span></span> | <span data-ttu-id="0ccd9-127">Tak</span><span class="sxs-lookup"><span data-stu-id="0ccd9-127">yes</span></span>      | <span data-ttu-id="0ccd9-128">Adres URL do zasobu</span><span class="sxs-lookup"><span data-stu-id="0ccd9-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="0ccd9-129">string</span><span class="sxs-lookup"><span data-stu-id="0ccd9-129">string</span></span> | <span data-ttu-id="0ccd9-130">Tak</span><span class="sxs-lookup"><span data-stu-id="0ccd9-130">yes</span></span>      | <span data-ttu-id="0ccd9-131">Stała ciąg reprezentujący typ zasobu</span><span class="sxs-lookup"><span data-stu-id="0ccd9-131">A string constant representing the resource type</span></span>
<span data-ttu-id="0ccd9-132">komentarz</span><span class="sxs-lookup"><span data-stu-id="0ccd9-132">comment</span></span>       | <span data-ttu-id="0ccd9-133">string</span><span class="sxs-lookup"><span data-stu-id="0ccd9-133">string</span></span> | <span data-ttu-id="0ccd9-134">Brak</span><span class="sxs-lookup"><span data-stu-id="0ccd9-134">no</span></span>       | <span data-ttu-id="0ccd9-135">Czytelny dla ludzi opis zasobu</span><span class="sxs-lookup"><span data-stu-id="0ccd9-135">A human readable description of the resource</span></span>

<span data-ttu-id="0ccd9-136">`@id` Jest adres URL, który musi być bezwzględnym i musi mieć schemat HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="0ccd9-137">`@type` Służy do identyfikowania określonych protokół do użycia podczas interakcji z zasobów.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="0ccd9-138">Typ zasobu jest ciągiem nieprzezroczyste, ale ma zazwyczaj format:</span><span class="sxs-lookup"><span data-stu-id="0ccd9-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="0ccd9-139">Klienci powinni twardych kodu `@type` wartości zrozumieć i wyszukiwanie w indeksie usługi źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="0ccd9-140">Dokładnie `@type` wartości w obecnie są wyliczane w dokumentach odwołanie pojedynczego zasobu, na liście [Przegląd interfejsu API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="0ccd9-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="0ccd9-141">Dla niniejszej dokumentacji dokumentację dotyczącą różnych zasobów będą zasadniczo pogrupowane według `{RESOURCE_NAME}` znalezionych w indeksie usługi, która jest analogiczna do grupowania według scenariusza.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="0ccd9-142">Nie jest wymagane czy każdy zasób ma unikatową `@id` lub `@type`.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="0ccd9-143">Jest implementacja klienta, aby określić, którego zasobu należy użyć zamiast innego.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="0ccd9-144">Jest to jedna implementacja możliwe, że zasoby o tej samej lub zgodne `@type` mogą być używane w okrężne w przypadku awarii lub serwera błąd połączenia.</span><span class="sxs-lookup"><span data-stu-id="0ccd9-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0ccd9-145">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="0ccd9-145">Sample request</span></span>

<span data-ttu-id="0ccd9-146">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="0ccd9-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="0ccd9-147">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="0ccd9-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
