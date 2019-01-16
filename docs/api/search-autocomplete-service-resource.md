---
title: Autouzupełnianie, interfejs API programu NuGet
description: Usługa wyszukiwania w funkcji autouzupełniania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2d2b20c1ea439ec0a3225cf983d9a4d2eedb0333
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324763"
---
# <a name="autocomplete"></a><span data-ttu-id="a3b01-103">Autouzupełnianie</span><span class="sxs-lookup"><span data-stu-id="a3b01-103">Autocomplete</span></span>

<span data-ttu-id="a3b01-104">Jest możliwe utworzenie pakietu identyfikator i wersja autouzupełniania doświadczenie w korzystaniu z interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="a3b01-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="a3b01-105">Zasób używane na potrzeby wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="a3b01-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="a3b01-106">Obsługa wersji</span><span class="sxs-lookup"><span data-stu-id="a3b01-106">Versioning</span></span>

<span data-ttu-id="a3b01-107">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="a3b01-107">The following `@type` values are used:</span></span>

<span data-ttu-id="a3b01-108">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="a3b01-108">@type value</span></span>                          | <span data-ttu-id="a3b01-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a3b01-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="a3b01-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="a3b01-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="a3b01-111">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="a3b01-111">The initial release</span></span>
<span data-ttu-id="a3b01-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="a3b01-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="a3b01-113">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="a3b01-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="a3b01-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="a3b01-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="a3b01-115">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="a3b01-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="a3b01-116">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-116">Base URL</span></span>

<span data-ttu-id="a3b01-117">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="a3b01-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="a3b01-118">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="a3b01-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a3b01-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="a3b01-119">HTTP Methods</span></span>

<span data-ttu-id="a3b01-120">Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="a3b01-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="a3b01-121">Wyszukaj pakiet identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="a3b01-121">Search for package IDs</span></span>

<span data-ttu-id="a3b01-122">Autouzupełnianie pierwszy interfejs API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="a3b01-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="a3b01-123">Jest to doskonałe, gdy chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika, zintegrowany z źródła pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="a3b01-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="a3b01-124">Pakiet wersjom tylko nieznajdujące się na liście będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="a3b01-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="a3b01-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="a3b01-125">Request parameters</span></span>

<span data-ttu-id="a3b01-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3b01-126">Name</span></span>        | <span data-ttu-id="a3b01-127">W</span><span class="sxs-lookup"><span data-stu-id="a3b01-127">In</span></span>     | <span data-ttu-id="a3b01-128">Typ</span><span class="sxs-lookup"><span data-stu-id="a3b01-128">Type</span></span>    | <span data-ttu-id="a3b01-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3b01-129">Required</span></span> | <span data-ttu-id="a3b01-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a3b01-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="a3b01-131">q</span><span class="sxs-lookup"><span data-stu-id="a3b01-131">q</span></span>           | <span data-ttu-id="a3b01-132">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-132">URL</span></span>    | <span data-ttu-id="a3b01-133">string</span><span class="sxs-lookup"><span data-stu-id="a3b01-133">string</span></span>  | <span data-ttu-id="a3b01-134">Brak</span><span class="sxs-lookup"><span data-stu-id="a3b01-134">no</span></span>       | <span data-ttu-id="a3b01-135">Ciąg do porównania pakietu identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="a3b01-135">The string to compare against package IDs</span></span>
<span data-ttu-id="a3b01-136">Pomiń</span><span class="sxs-lookup"><span data-stu-id="a3b01-136">skip</span></span>        | <span data-ttu-id="a3b01-137">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-137">URL</span></span>    | <span data-ttu-id="a3b01-138">integer</span><span class="sxs-lookup"><span data-stu-id="a3b01-138">integer</span></span> | <span data-ttu-id="a3b01-139">Brak</span><span class="sxs-lookup"><span data-stu-id="a3b01-139">no</span></span>       | <span data-ttu-id="a3b01-140">Liczba wyników do pominięcia do dzielenia na strony</span><span class="sxs-lookup"><span data-stu-id="a3b01-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="a3b01-141">Wypełnij</span><span class="sxs-lookup"><span data-stu-id="a3b01-141">take</span></span>        | <span data-ttu-id="a3b01-142">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-142">URL</span></span>    | <span data-ttu-id="a3b01-143">integer</span><span class="sxs-lookup"><span data-stu-id="a3b01-143">integer</span></span> | <span data-ttu-id="a3b01-144">Brak</span><span class="sxs-lookup"><span data-stu-id="a3b01-144">no</span></span>       | <span data-ttu-id="a3b01-145">Liczba wyników do zwrócenia do dzielenia na strony</span><span class="sxs-lookup"><span data-stu-id="a3b01-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="a3b01-146">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="a3b01-146">prerelease</span></span>  | <span data-ttu-id="a3b01-147">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-147">URL</span></span>    | <span data-ttu-id="a3b01-148">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a3b01-148">boolean</span></span> | <span data-ttu-id="a3b01-149">Brak</span><span class="sxs-lookup"><span data-stu-id="a3b01-149">no</span></span>       | <span data-ttu-id="a3b01-150">`true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a3b01-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="a3b01-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="a3b01-151">semVerLevel</span></span> | <span data-ttu-id="a3b01-152">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-152">URL</span></span>    | <span data-ttu-id="a3b01-153">string</span><span class="sxs-lookup"><span data-stu-id="a3b01-153">string</span></span>  | <span data-ttu-id="a3b01-154">Brak</span><span class="sxs-lookup"><span data-stu-id="a3b01-154">no</span></span>       | <span data-ttu-id="a3b01-155">Ciąg wersji SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="a3b01-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="a3b01-156">Zapytanie autouzupełniania `q` jest analizowany w taki sposób, który jest definiowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="a3b01-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="a3b01-157">nuget.org obsługuje zapytania dla prefiksu tokeny Identyfikatora pakietu będące rodzajów identyfikator, który został utworzony przez spliting oryginalny pisane znakami wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="a3b01-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="a3b01-158">`skip` Domyślnych wartości parametrów na 0.</span><span class="sxs-lookup"><span data-stu-id="a3b01-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="a3b01-159">`take` Parametr powinien być liczbą całkowitą większą niż zero.</span><span class="sxs-lookup"><span data-stu-id="a3b01-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="a3b01-160">Implementacja serwera może nałożyć wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="a3b01-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="a3b01-161">Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="a3b01-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="a3b01-162">`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="a3b01-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="a3b01-163">Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko pakiet identyfikatory o SemVer 1.0.0 zgodne wersje (z [standardowych wersji NuGet](../reference/package-versioning.md) zastrzeżenia, takich jak ciągi wersji z 4 elementów liczba całkowita).</span><span class="sxs-lookup"><span data-stu-id="a3b01-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="a3b01-164">Jeśli `semVerLevel=2.0.0` zostanie podana, zostaną zwrócone SemVer 1.0.0 i pakiety zgodne SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a3b01-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="a3b01-165">Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a3b01-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="a3b01-166">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="a3b01-166">Response</span></span>

<span data-ttu-id="a3b01-167">Odpowiedź jest dokument JSON zawierający do `take` wyniki funkcji autouzupełniania.</span><span class="sxs-lookup"><span data-stu-id="a3b01-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="a3b01-168">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="a3b01-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="a3b01-169">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3b01-169">Name</span></span>      | <span data-ttu-id="a3b01-170">Typ</span><span class="sxs-lookup"><span data-stu-id="a3b01-170">Type</span></span>             | <span data-ttu-id="a3b01-171">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3b01-171">Required</span></span> | <span data-ttu-id="a3b01-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a3b01-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="a3b01-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="a3b01-173">totalHits</span></span> | <span data-ttu-id="a3b01-174">integer</span><span class="sxs-lookup"><span data-stu-id="a3b01-174">integer</span></span>          | <span data-ttu-id="a3b01-175">tak</span><span class="sxs-lookup"><span data-stu-id="a3b01-175">yes</span></span>      | <span data-ttu-id="a3b01-176">Całkowita liczba dopasowań, pomijając `skip` i `take`</span><span class="sxs-lookup"><span data-stu-id="a3b01-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="a3b01-177">dane</span><span class="sxs-lookup"><span data-stu-id="a3b01-177">data</span></span>      | <span data-ttu-id="a3b01-178">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="a3b01-178">array of strings</span></span> | <span data-ttu-id="a3b01-179">tak</span><span class="sxs-lookup"><span data-stu-id="a3b01-179">yes</span></span>      | <span data-ttu-id="a3b01-180">Identyfikatory dopasowane przez żądania pakietu</span><span class="sxs-lookup"><span data-stu-id="a3b01-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="a3b01-181">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a3b01-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="a3b01-182">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="a3b01-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="a3b01-183">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="a3b01-183">Enumerate package versions</span></span>

<span data-ttu-id="a3b01-184">Po odnalezieniu Identyfikatora pakietu za pomocą poprzedniej interfejsu API klient może używać interfejsu API automatycznego uzupełniania wyliczyć wersji pakietu dla identyfikatora podanego pakietu</span><span class="sxs-lookup"><span data-stu-id="a3b01-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="a3b01-185">Wersja pakietu, który jest nieobecne na liście będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="a3b01-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="a3b01-186">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="a3b01-186">Request parameters</span></span>

<span data-ttu-id="a3b01-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3b01-187">Name</span></span>        | <span data-ttu-id="a3b01-188">W</span><span class="sxs-lookup"><span data-stu-id="a3b01-188">In</span></span>     | <span data-ttu-id="a3b01-189">Typ</span><span class="sxs-lookup"><span data-stu-id="a3b01-189">Type</span></span>    | <span data-ttu-id="a3b01-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3b01-190">Required</span></span> | <span data-ttu-id="a3b01-191">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a3b01-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="a3b01-192">identyfikator</span><span class="sxs-lookup"><span data-stu-id="a3b01-192">id</span></span>          | <span data-ttu-id="a3b01-193">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-193">URL</span></span>    | <span data-ttu-id="a3b01-194">string</span><span class="sxs-lookup"><span data-stu-id="a3b01-194">string</span></span>  | <span data-ttu-id="a3b01-195">tak</span><span class="sxs-lookup"><span data-stu-id="a3b01-195">yes</span></span>      | <span data-ttu-id="a3b01-196">Identyfikator pakietu można pobrać wersji</span><span class="sxs-lookup"><span data-stu-id="a3b01-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="a3b01-197">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="a3b01-197">prerelease</span></span>  | <span data-ttu-id="a3b01-198">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-198">URL</span></span>    | <span data-ttu-id="a3b01-199">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a3b01-199">boolean</span></span> | <span data-ttu-id="a3b01-200">Brak</span><span class="sxs-lookup"><span data-stu-id="a3b01-200">no</span></span>       | <span data-ttu-id="a3b01-201">`true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a3b01-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="a3b01-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="a3b01-202">semVerLevel</span></span> | <span data-ttu-id="a3b01-203">Adres URL</span><span class="sxs-lookup"><span data-stu-id="a3b01-203">URL</span></span>    | <span data-ttu-id="a3b01-204">string</span><span class="sxs-lookup"><span data-stu-id="a3b01-204">string</span></span>  | <span data-ttu-id="a3b01-205">Brak</span><span class="sxs-lookup"><span data-stu-id="a3b01-205">no</span></span>       | <span data-ttu-id="a3b01-206">Ciąg wersji SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="a3b01-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="a3b01-207">Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="a3b01-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="a3b01-208">`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na pakiety SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a3b01-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="a3b01-209">Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko wersje SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a3b01-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="a3b01-210">Jeśli `semVerLevel=2.0.0` zostanie podana, zostanie zwrócony SemVer 1.0.0 i SemVer 2.0.0 wersji.</span><span class="sxs-lookup"><span data-stu-id="a3b01-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="a3b01-211">Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a3b01-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="a3b01-212">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="a3b01-212">Response</span></span>

<span data-ttu-id="a3b01-213">Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podanego pakietu, filtrowanie według parametrów określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="a3b01-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="a3b01-214">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="a3b01-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="a3b01-215">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a3b01-215">Name</span></span>      | <span data-ttu-id="a3b01-216">Typ</span><span class="sxs-lookup"><span data-stu-id="a3b01-216">Type</span></span>             | <span data-ttu-id="a3b01-217">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a3b01-217">Required</span></span> | <span data-ttu-id="a3b01-218">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a3b01-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="a3b01-219">dane</span><span class="sxs-lookup"><span data-stu-id="a3b01-219">data</span></span>      | <span data-ttu-id="a3b01-220">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="a3b01-220">array of strings</span></span> | <span data-ttu-id="a3b01-221">tak</span><span class="sxs-lookup"><span data-stu-id="a3b01-221">yes</span></span>      | <span data-ttu-id="a3b01-222">Wersje pakietów dopasowane przez żądanie</span><span class="sxs-lookup"><span data-stu-id="a3b01-222">The package versions matched by the request</span></span>

<span data-ttu-id="a3b01-223">Wersje pakietów w `data` tablicy mogą zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` została podana w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="a3b01-223">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a3b01-224">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a3b01-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="a3b01-225">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="a3b01-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
