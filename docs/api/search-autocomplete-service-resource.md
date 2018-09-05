---
title: Autouzupełnianie, interfejs API programu NuGet
description: Usługa wyszukiwania w funkcji autouzupełniania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549086"
---
# <a name="autocomplete"></a><span data-ttu-id="6ce21-103">Autouzupełnianie</span><span class="sxs-lookup"><span data-stu-id="6ce21-103">Autocomplete</span></span>

<span data-ttu-id="6ce21-104">Jest możliwe utworzenie pakietu identyfikator i wersja autouzupełniania doświadczenie w korzystaniu z interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="6ce21-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="6ce21-105">Zasób używane na potrzeby wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6ce21-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6ce21-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="6ce21-106">Versioning</span></span>

<span data-ttu-id="6ce21-107">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="6ce21-107">The following `@type` values are used:</span></span>

<span data-ttu-id="6ce21-108">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="6ce21-108">@type value</span></span>                          | <span data-ttu-id="6ce21-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6ce21-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="6ce21-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="6ce21-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="6ce21-111">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="6ce21-111">The initial release</span></span>
<span data-ttu-id="6ce21-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="6ce21-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="6ce21-113">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="6ce21-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="6ce21-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="6ce21-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="6ce21-115">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="6ce21-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="6ce21-116">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-116">Base URL</span></span>

<span data-ttu-id="6ce21-117">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="6ce21-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="6ce21-118">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="6ce21-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6ce21-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="6ce21-119">HTTP Methods</span></span>

<span data-ttu-id="6ce21-120">Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="6ce21-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="6ce21-121">Wyszukaj pakiet identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="6ce21-121">Search for package IDs</span></span>

<span data-ttu-id="6ce21-122">Autouzupełnianie pierwszy interfejs API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="6ce21-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="6ce21-123">Jest to doskonałe, gdy chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika, zintegrowany z źródła pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="6ce21-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="6ce21-124">Pakiet wersjom tylko nieznajdujące się na liście będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="6ce21-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="6ce21-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="6ce21-125">Request parameters</span></span>

<span data-ttu-id="6ce21-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6ce21-126">Name</span></span>        | <span data-ttu-id="6ce21-127">W</span><span class="sxs-lookup"><span data-stu-id="6ce21-127">In</span></span>     | <span data-ttu-id="6ce21-128">Typ</span><span class="sxs-lookup"><span data-stu-id="6ce21-128">Type</span></span>    | <span data-ttu-id="6ce21-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ce21-129">Required</span></span> | <span data-ttu-id="6ce21-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6ce21-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="6ce21-131">q</span><span class="sxs-lookup"><span data-stu-id="6ce21-131">q</span></span>           | <span data-ttu-id="6ce21-132">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-132">URL</span></span>    | <span data-ttu-id="6ce21-133">string</span><span class="sxs-lookup"><span data-stu-id="6ce21-133">string</span></span>  | <span data-ttu-id="6ce21-134">Brak</span><span class="sxs-lookup"><span data-stu-id="6ce21-134">no</span></span>       | <span data-ttu-id="6ce21-135">Ciąg do porównania pakietu identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="6ce21-135">The string to compare against package IDs</span></span>
<span data-ttu-id="6ce21-136">Pomiń</span><span class="sxs-lookup"><span data-stu-id="6ce21-136">skip</span></span>        | <span data-ttu-id="6ce21-137">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-137">URL</span></span>    | <span data-ttu-id="6ce21-138">integer</span><span class="sxs-lookup"><span data-stu-id="6ce21-138">integer</span></span> | <span data-ttu-id="6ce21-139">Brak</span><span class="sxs-lookup"><span data-stu-id="6ce21-139">no</span></span>       | <span data-ttu-id="6ce21-140">Liczba wyników do pominięcia do dzielenia na strony</span><span class="sxs-lookup"><span data-stu-id="6ce21-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="6ce21-141">Wypełnij</span><span class="sxs-lookup"><span data-stu-id="6ce21-141">take</span></span>        | <span data-ttu-id="6ce21-142">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-142">URL</span></span>    | <span data-ttu-id="6ce21-143">integer</span><span class="sxs-lookup"><span data-stu-id="6ce21-143">integer</span></span> | <span data-ttu-id="6ce21-144">Brak</span><span class="sxs-lookup"><span data-stu-id="6ce21-144">no</span></span>       | <span data-ttu-id="6ce21-145">Liczba wyników do zwrócenia do dzielenia na strony</span><span class="sxs-lookup"><span data-stu-id="6ce21-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="6ce21-146">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="6ce21-146">prerelease</span></span>  | <span data-ttu-id="6ce21-147">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-147">URL</span></span>    | <span data-ttu-id="6ce21-148">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="6ce21-148">boolean</span></span> | <span data-ttu-id="6ce21-149">Brak</span><span class="sxs-lookup"><span data-stu-id="6ce21-149">no</span></span>       | <span data-ttu-id="6ce21-150">`true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6ce21-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="6ce21-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="6ce21-151">semVerLevel</span></span> | <span data-ttu-id="6ce21-152">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-152">URL</span></span>    | <span data-ttu-id="6ce21-153">string</span><span class="sxs-lookup"><span data-stu-id="6ce21-153">string</span></span>  | <span data-ttu-id="6ce21-154">Brak</span><span class="sxs-lookup"><span data-stu-id="6ce21-154">no</span></span>       | <span data-ttu-id="6ce21-155">Ciąg wersji SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="6ce21-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="6ce21-156">Zapytanie autouzupełniania `q` jest analizowany w taki sposób, który jest definiowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="6ce21-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="6ce21-157">nuget.org obsługuje zapytania dla prefiksu tokeny Identyfikatora pakietu będące rodzajów identyfikator, który został utworzony przez spliting oryginalny pisane znakami wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="6ce21-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="6ce21-158">`skip` Domyślnych wartości parametrów na 0.</span><span class="sxs-lookup"><span data-stu-id="6ce21-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="6ce21-159">`take` Parametr powinien być liczbą całkowitą większą niż zero.</span><span class="sxs-lookup"><span data-stu-id="6ce21-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="6ce21-160">Implementacja serwera może nałożyć wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="6ce21-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="6ce21-161">Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6ce21-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="6ce21-162">`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="6ce21-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="6ce21-163">Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko pakiet identyfikatory o SemVer 1.0.0 zgodne wersje (z [standardowych wersji NuGet](../reference/package-versioning.md) zastrzeżenia, takich jak ciągi wersji z 4 elementów liczba całkowita).</span><span class="sxs-lookup"><span data-stu-id="6ce21-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="6ce21-164">Jeśli `semVerLevel=2.0.0` zostanie podana, zostaną zwrócone SemVer 1.0.0 i pakiety zgodne SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6ce21-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="6ce21-165">Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="6ce21-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="6ce21-166">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6ce21-166">Response</span></span>

<span data-ttu-id="6ce21-167">Odpowiedź jest dokument JSON zawierający do `take` wyniki funkcji autouzupełniania.</span><span class="sxs-lookup"><span data-stu-id="6ce21-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="6ce21-168">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6ce21-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="6ce21-169">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6ce21-169">Name</span></span>      | <span data-ttu-id="6ce21-170">Typ</span><span class="sxs-lookup"><span data-stu-id="6ce21-170">Type</span></span>             | <span data-ttu-id="6ce21-171">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ce21-171">Required</span></span> | <span data-ttu-id="6ce21-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6ce21-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="6ce21-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="6ce21-173">totalHits</span></span> | <span data-ttu-id="6ce21-174">integer</span><span class="sxs-lookup"><span data-stu-id="6ce21-174">integer</span></span>          | <span data-ttu-id="6ce21-175">Tak</span><span class="sxs-lookup"><span data-stu-id="6ce21-175">yes</span></span>      | <span data-ttu-id="6ce21-176">Całkowita liczba dopasowań, pomijając `skip` i `take`</span><span class="sxs-lookup"><span data-stu-id="6ce21-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="6ce21-177">dane</span><span class="sxs-lookup"><span data-stu-id="6ce21-177">data</span></span>      | <span data-ttu-id="6ce21-178">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="6ce21-178">array of strings</span></span> | <span data-ttu-id="6ce21-179">Tak</span><span class="sxs-lookup"><span data-stu-id="6ce21-179">yes</span></span>      | <span data-ttu-id="6ce21-180">Identyfikatory dopasowane przez żądania pakietu</span><span class="sxs-lookup"><span data-stu-id="6ce21-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="6ce21-181">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="6ce21-181">Sample request</span></span>

<span data-ttu-id="6ce21-182">POBIERZ https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="6ce21-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="6ce21-183">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6ce21-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="6ce21-184">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="6ce21-184">Enumerate package versions</span></span>

<span data-ttu-id="6ce21-185">Po odnalezieniu Identyfikatora pakietu za pomocą poprzedniej interfejsu API klient może używać interfejsu API automatycznego uzupełniania wyliczyć wersji pakietu dla identyfikatora podanego pakietu</span><span class="sxs-lookup"><span data-stu-id="6ce21-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="6ce21-186">Wersja pakietu, który jest nieobecne na liście będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="6ce21-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="6ce21-187">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="6ce21-187">Request parameters</span></span>

<span data-ttu-id="6ce21-188">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6ce21-188">Name</span></span>        | <span data-ttu-id="6ce21-189">W</span><span class="sxs-lookup"><span data-stu-id="6ce21-189">In</span></span>     | <span data-ttu-id="6ce21-190">Typ</span><span class="sxs-lookup"><span data-stu-id="6ce21-190">Type</span></span>    | <span data-ttu-id="6ce21-191">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ce21-191">Required</span></span> | <span data-ttu-id="6ce21-192">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6ce21-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="6ce21-193">identyfikator</span><span class="sxs-lookup"><span data-stu-id="6ce21-193">id</span></span>          | <span data-ttu-id="6ce21-194">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-194">URL</span></span>    | <span data-ttu-id="6ce21-195">string</span><span class="sxs-lookup"><span data-stu-id="6ce21-195">string</span></span>  | <span data-ttu-id="6ce21-196">Tak</span><span class="sxs-lookup"><span data-stu-id="6ce21-196">yes</span></span>      | <span data-ttu-id="6ce21-197">Identyfikator pakietu można pobrać wersji</span><span class="sxs-lookup"><span data-stu-id="6ce21-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="6ce21-198">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="6ce21-198">prerelease</span></span>  | <span data-ttu-id="6ce21-199">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-199">URL</span></span>    | <span data-ttu-id="6ce21-200">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="6ce21-200">boolean</span></span> | <span data-ttu-id="6ce21-201">Brak</span><span class="sxs-lookup"><span data-stu-id="6ce21-201">no</span></span>       | <span data-ttu-id="6ce21-202">`true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6ce21-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="6ce21-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="6ce21-203">semVerLevel</span></span> | <span data-ttu-id="6ce21-204">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6ce21-204">URL</span></span>    | <span data-ttu-id="6ce21-205">string</span><span class="sxs-lookup"><span data-stu-id="6ce21-205">string</span></span>  | <span data-ttu-id="6ce21-206">Brak</span><span class="sxs-lookup"><span data-stu-id="6ce21-206">no</span></span>       | <span data-ttu-id="6ce21-207">Ciąg wersji SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="6ce21-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="6ce21-208">Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6ce21-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="6ce21-209">`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na pakiety SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6ce21-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="6ce21-210">Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko wersje SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="6ce21-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="6ce21-211">Jeśli `semVerLevel=2.0.0` zostanie podana, zostanie zwrócony SemVer 1.0.0 i SemVer 2.0.0 wersji.</span><span class="sxs-lookup"><span data-stu-id="6ce21-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="6ce21-212">Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="6ce21-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="6ce21-213">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6ce21-213">Response</span></span>

<span data-ttu-id="6ce21-214">Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podanego pakietu, filtrowanie według parametrów określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="6ce21-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="6ce21-215">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="6ce21-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="6ce21-216">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6ce21-216">Name</span></span>      | <span data-ttu-id="6ce21-217">Typ</span><span class="sxs-lookup"><span data-stu-id="6ce21-217">Type</span></span>             | <span data-ttu-id="6ce21-218">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6ce21-218">Required</span></span> | <span data-ttu-id="6ce21-219">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6ce21-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="6ce21-220">dane</span><span class="sxs-lookup"><span data-stu-id="6ce21-220">data</span></span>      | <span data-ttu-id="6ce21-221">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="6ce21-221">array of strings</span></span> | <span data-ttu-id="6ce21-222">Tak</span><span class="sxs-lookup"><span data-stu-id="6ce21-222">yes</span></span>      | <span data-ttu-id="6ce21-223">Wersje pakietów dopasowane przez żądanie</span><span class="sxs-lookup"><span data-stu-id="6ce21-223">The package versions matched by the request</span></span>

<span data-ttu-id="6ce21-224">Wersje pakietów w `data` tablicy mogą zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` została podana w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="6ce21-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6ce21-225">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="6ce21-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="6ce21-226">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6ce21-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
