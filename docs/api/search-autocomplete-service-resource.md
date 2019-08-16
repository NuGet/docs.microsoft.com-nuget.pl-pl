---
title: Autouzupełnianie, interfejs API NuGet
description: Usługa wyszukiwania autouzupełniania obsługuje interaktywne odnajdywanie identyfikatorów pakietów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488303"
---
# <a name="autocomplete"></a><span data-ttu-id="61d6a-103">Autouzupełnianie</span><span class="sxs-lookup"><span data-stu-id="61d6a-103">Autocomplete</span></span>

<span data-ttu-id="61d6a-104">Istnieje możliwość utworzenia identyfikatora pakietu i funkcji Autouzupełnianie wersji przy użyciu interfejsu API v3.</span><span class="sxs-lookup"><span data-stu-id="61d6a-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="61d6a-105">Zasób używany do wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` zasobem znalezionym w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="61d6a-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="61d6a-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="61d6a-106">Versioning</span></span>

<span data-ttu-id="61d6a-107">Są używane `@type` następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="61d6a-107">The following `@type` values are used:</span></span>

<span data-ttu-id="61d6a-108">@typewartościami</span><span class="sxs-lookup"><span data-stu-id="61d6a-108">@type value</span></span>                          | <span data-ttu-id="61d6a-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="61d6a-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="61d6a-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="61d6a-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="61d6a-111">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="61d6a-111">The initial release</span></span>
<span data-ttu-id="61d6a-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="61d6a-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="61d6a-113">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="61d6a-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="61d6a-114">SearchAutocompleteService/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="61d6a-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="61d6a-115">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="61d6a-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="61d6a-116">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-116">Base URL</span></span>

<span data-ttu-id="61d6a-117">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzoną z jedną z wyżej wymienionych wartości zasobów. `@type`</span><span class="sxs-lookup"><span data-stu-id="61d6a-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="61d6a-118">W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego `{@id}` adresu URL.</span><span class="sxs-lookup"><span data-stu-id="61d6a-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="61d6a-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="61d6a-119">HTTP Methods</span></span>

<span data-ttu-id="61d6a-120">Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują `GET` metody `HEAD`http i.</span><span class="sxs-lookup"><span data-stu-id="61d6a-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="61d6a-121">Wyszukaj identyfikatory pakietów</span><span class="sxs-lookup"><span data-stu-id="61d6a-121">Search for package IDs</span></span>

<span data-ttu-id="61d6a-122">Pierwszy interfejs API funkcji Autouzupełnianie obsługuje wyszukiwanie części ciągu identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="61d6a-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="61d6a-123">Jest to doskonałe rozwiązanie, jeśli chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika zintegrowanym ze źródłem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="61d6a-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="61d6a-124">Pakiet z tylko wersjami nieznajdującymi się na liście nie będzie wyświetlany w wynikach.</span><span class="sxs-lookup"><span data-stu-id="61d6a-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="61d6a-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="61d6a-125">Request parameters</span></span>

<span data-ttu-id="61d6a-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="61d6a-126">Name</span></span>        | <span data-ttu-id="61d6a-127">W</span><span class="sxs-lookup"><span data-stu-id="61d6a-127">In</span></span>     | <span data-ttu-id="61d6a-128">Typ</span><span class="sxs-lookup"><span data-stu-id="61d6a-128">Type</span></span>    | <span data-ttu-id="61d6a-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="61d6a-129">Required</span></span> | <span data-ttu-id="61d6a-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="61d6a-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="61d6a-131">q</span><span class="sxs-lookup"><span data-stu-id="61d6a-131">q</span></span>           | <span data-ttu-id="61d6a-132">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-132">URL</span></span>    | <span data-ttu-id="61d6a-133">string</span><span class="sxs-lookup"><span data-stu-id="61d6a-133">string</span></span>  | <span data-ttu-id="61d6a-134">znaleziono</span><span class="sxs-lookup"><span data-stu-id="61d6a-134">no</span></span>       | <span data-ttu-id="61d6a-135">Ciąg do porównania z identyfikatorami pakietów</span><span class="sxs-lookup"><span data-stu-id="61d6a-135">The string to compare against package IDs</span></span>
<span data-ttu-id="61d6a-136">Pomiń</span><span class="sxs-lookup"><span data-stu-id="61d6a-136">skip</span></span>        | <span data-ttu-id="61d6a-137">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-137">URL</span></span>    | <span data-ttu-id="61d6a-138">integer</span><span class="sxs-lookup"><span data-stu-id="61d6a-138">integer</span></span> | <span data-ttu-id="61d6a-139">znaleziono</span><span class="sxs-lookup"><span data-stu-id="61d6a-139">no</span></span>       | <span data-ttu-id="61d6a-140">Liczba wyników do pominięcia na stronie stronicowania</span><span class="sxs-lookup"><span data-stu-id="61d6a-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="61d6a-141">czasochłonn</span><span class="sxs-lookup"><span data-stu-id="61d6a-141">take</span></span>        | <span data-ttu-id="61d6a-142">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-142">URL</span></span>    | <span data-ttu-id="61d6a-143">integer</span><span class="sxs-lookup"><span data-stu-id="61d6a-143">integer</span></span> | <span data-ttu-id="61d6a-144">znaleziono</span><span class="sxs-lookup"><span data-stu-id="61d6a-144">no</span></span>       | <span data-ttu-id="61d6a-145">Liczba wyników do zwrócenia, na stronie stronicowania</span><span class="sxs-lookup"><span data-stu-id="61d6a-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="61d6a-146">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="61d6a-146">prerelease</span></span>  | <span data-ttu-id="61d6a-147">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-147">URL</span></span>    | <span data-ttu-id="61d6a-148">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="61d6a-148">boolean</span></span> | <span data-ttu-id="61d6a-149">znaleziono</span><span class="sxs-lookup"><span data-stu-id="61d6a-149">no</span></span>       | <span data-ttu-id="61d6a-150">`true`lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="61d6a-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="61d6a-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="61d6a-151">semVerLevel</span></span> | <span data-ttu-id="61d6a-152">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-152">URL</span></span>    | <span data-ttu-id="61d6a-153">string</span><span class="sxs-lookup"><span data-stu-id="61d6a-153">string</span></span>  | <span data-ttu-id="61d6a-154">znaleziono</span><span class="sxs-lookup"><span data-stu-id="61d6a-154">no</span></span>       | <span data-ttu-id="61d6a-155">Ciąg wersji SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="61d6a-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="61d6a-156">Zapytanie `q` autouzupełniania jest analizowane w sposób zdefiniowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="61d6a-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="61d6a-157">nuget.org obsługuje zapytania dotyczące prefiksu tokenów identyfikatora pakietu, które są częścią identyfikatora wygenerowanego przez podzielenie oryginalnego znaku przez notacji CamelCase wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="61d6a-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="61d6a-158">Wartość `skip` domyślna parametru to 0.</span><span class="sxs-lookup"><span data-stu-id="61d6a-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="61d6a-159">`take` Parametr powinien być liczbą całkowitą większą od zera.</span><span class="sxs-lookup"><span data-stu-id="61d6a-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="61d6a-160">Implementacja serwera może mieć wartość maksymalną.</span><span class="sxs-lookup"><span data-stu-id="61d6a-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="61d6a-161">Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.</span><span class="sxs-lookup"><span data-stu-id="61d6a-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="61d6a-162">Parametr zapytania jest używany do wybierania [pakietów SemVer 2.0.0.](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`</span><span class="sxs-lookup"><span data-stu-id="61d6a-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="61d6a-163">Jeśli ten parametr zapytania zostanie wykluczony, zostaną zwrócone tylko identyfikatory pakietów z zgodnymi wersjami programu SemVer 1.0.0 (ze standardowymi ograniczeniami [wersji programu NuGet](../concepts/package-versioning.md) , takimi jak ciągi wersji z 4 liczbami całkowitymi).</span><span class="sxs-lookup"><span data-stu-id="61d6a-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="61d6a-164">Jeśli `semVerLevel=2.0.0` jest podany, zwracane są zgodne z SemVer 1.0.0 i SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="61d6a-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="61d6a-165">Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="61d6a-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="61d6a-166">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="61d6a-166">Response</span></span>

<span data-ttu-id="61d6a-167">Odpowiedź jest dokumentem JSON zawierającym do `take` wyników Autouzupełnianie.</span><span class="sxs-lookup"><span data-stu-id="61d6a-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="61d6a-168">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="61d6a-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="61d6a-169">Nazwa</span><span class="sxs-lookup"><span data-stu-id="61d6a-169">Name</span></span>      | <span data-ttu-id="61d6a-170">Typ</span><span class="sxs-lookup"><span data-stu-id="61d6a-170">Type</span></span>             | <span data-ttu-id="61d6a-171">Wymagane</span><span class="sxs-lookup"><span data-stu-id="61d6a-171">Required</span></span> | <span data-ttu-id="61d6a-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="61d6a-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="61d6a-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="61d6a-173">totalHits</span></span> | <span data-ttu-id="61d6a-174">integer</span><span class="sxs-lookup"><span data-stu-id="61d6a-174">integer</span></span>          | <span data-ttu-id="61d6a-175">tak</span><span class="sxs-lookup"><span data-stu-id="61d6a-175">yes</span></span>      | <span data-ttu-id="61d6a-176">Łączna liczba dopasowań, odnoszących `skip` się do i`take`</span><span class="sxs-lookup"><span data-stu-id="61d6a-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="61d6a-177">dane</span><span class="sxs-lookup"><span data-stu-id="61d6a-177">data</span></span>      | <span data-ttu-id="61d6a-178">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="61d6a-178">array of strings</span></span> | <span data-ttu-id="61d6a-179">tak</span><span class="sxs-lookup"><span data-stu-id="61d6a-179">yes</span></span>      | <span data-ttu-id="61d6a-180">Identyfikatory pakietów dopasowane przez żądanie</span><span class="sxs-lookup"><span data-stu-id="61d6a-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="61d6a-181">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="61d6a-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="61d6a-182">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="61d6a-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="61d6a-183">Wylicz wersje pakietów</span><span class="sxs-lookup"><span data-stu-id="61d6a-183">Enumerate package versions</span></span>

<span data-ttu-id="61d6a-184">Po znalezieniu identyfikatora pakietu przy użyciu poprzedniego interfejsu API klient może użyć interfejsu API autouzupełniania, aby wyliczyć wersje pakietu dla podanego identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="61d6a-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="61d6a-185">Wersja pakietu, która nie znajduje się na liście, nie zostanie wyświetlona w wynikach.</span><span class="sxs-lookup"><span data-stu-id="61d6a-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="61d6a-186">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="61d6a-186">Request parameters</span></span>

<span data-ttu-id="61d6a-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="61d6a-187">Name</span></span>        | <span data-ttu-id="61d6a-188">W</span><span class="sxs-lookup"><span data-stu-id="61d6a-188">In</span></span>     | <span data-ttu-id="61d6a-189">Typ</span><span class="sxs-lookup"><span data-stu-id="61d6a-189">Type</span></span>    | <span data-ttu-id="61d6a-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="61d6a-190">Required</span></span> | <span data-ttu-id="61d6a-191">Uwagi</span><span class="sxs-lookup"><span data-stu-id="61d6a-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="61d6a-192">identyfikator</span><span class="sxs-lookup"><span data-stu-id="61d6a-192">id</span></span>          | <span data-ttu-id="61d6a-193">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-193">URL</span></span>    | <span data-ttu-id="61d6a-194">string</span><span class="sxs-lookup"><span data-stu-id="61d6a-194">string</span></span>  | <span data-ttu-id="61d6a-195">tak</span><span class="sxs-lookup"><span data-stu-id="61d6a-195">yes</span></span>      | <span data-ttu-id="61d6a-196">Identyfikator pakietu, dla którego mają zostać pobrane wersje</span><span class="sxs-lookup"><span data-stu-id="61d6a-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="61d6a-197">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="61d6a-197">prerelease</span></span>  | <span data-ttu-id="61d6a-198">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-198">URL</span></span>    | <span data-ttu-id="61d6a-199">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="61d6a-199">boolean</span></span> | <span data-ttu-id="61d6a-200">znaleziono</span><span class="sxs-lookup"><span data-stu-id="61d6a-200">no</span></span>       | <span data-ttu-id="61d6a-201">`true`lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="61d6a-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="61d6a-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="61d6a-202">semVerLevel</span></span> | <span data-ttu-id="61d6a-203">Adres URL</span><span class="sxs-lookup"><span data-stu-id="61d6a-203">URL</span></span>    | <span data-ttu-id="61d6a-204">string</span><span class="sxs-lookup"><span data-stu-id="61d6a-204">string</span></span>  | <span data-ttu-id="61d6a-205">znaleziono</span><span class="sxs-lookup"><span data-stu-id="61d6a-205">no</span></span>       | <span data-ttu-id="61d6a-206">Ciąg wersji SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="61d6a-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="61d6a-207">Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.</span><span class="sxs-lookup"><span data-stu-id="61d6a-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="61d6a-208">Parametr `semVerLevel` zapytania jest używany do wybierania pakietów SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="61d6a-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="61d6a-209">Jeśli ten parametr zapytania jest wykluczony, zostaną zwrócone tylko wersje programu SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="61d6a-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="61d6a-210">Jeśli `semVerLevel=2.0.0` jest podany, zostaną zwrócone wersje SemVer 1.0.0 i SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="61d6a-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="61d6a-211">Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="61d6a-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="61d6a-212">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="61d6a-212">Response</span></span>

<span data-ttu-id="61d6a-213">Odpowiedź to dokument JSON zawierający wszystkie wersje pakietu podanego identyfikatora pakietu, filtrowanie według podanych parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="61d6a-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="61d6a-214">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="61d6a-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="61d6a-215">Nazwa</span><span class="sxs-lookup"><span data-stu-id="61d6a-215">Name</span></span>      | <span data-ttu-id="61d6a-216">Typ</span><span class="sxs-lookup"><span data-stu-id="61d6a-216">Type</span></span>             | <span data-ttu-id="61d6a-217">Wymagane</span><span class="sxs-lookup"><span data-stu-id="61d6a-217">Required</span></span> | <span data-ttu-id="61d6a-218">Uwagi</span><span class="sxs-lookup"><span data-stu-id="61d6a-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="61d6a-219">dane</span><span class="sxs-lookup"><span data-stu-id="61d6a-219">data</span></span>      | <span data-ttu-id="61d6a-220">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="61d6a-220">array of strings</span></span> | <span data-ttu-id="61d6a-221">tak</span><span class="sxs-lookup"><span data-stu-id="61d6a-221">yes</span></span>      | <span data-ttu-id="61d6a-222">Wersje pakietów dopasowane przez żądanie</span><span class="sxs-lookup"><span data-stu-id="61d6a-222">The package versions matched by the request</span></span>

<span data-ttu-id="61d6a-223">Wersje pakietu w `data` tablicy mogą zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata`), `semVerLevel=2.0.0` jeśli są podane w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="61d6a-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="61d6a-224">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="61d6a-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="61d6a-225">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="61d6a-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
