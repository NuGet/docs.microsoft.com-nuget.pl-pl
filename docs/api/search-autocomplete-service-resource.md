---
title: Autouzupełnianie, interfejs API programu NuGet
description: Usługa wyszukiwania w funkcji autouzupełniania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911052"
---
# <a name="autocomplete"></a><span data-ttu-id="e8a90-103">Autouzupełnianie</span><span class="sxs-lookup"><span data-stu-id="e8a90-103">Autocomplete</span></span>

<span data-ttu-id="e8a90-104">Jest możliwe utworzenie pakietu identyfikator i wersja autouzupełniania doświadczenie w korzystaniu z interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="e8a90-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="e8a90-105">Zasób używane na potrzeby wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e8a90-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e8a90-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="e8a90-106">Versioning</span></span>

<span data-ttu-id="e8a90-107">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="e8a90-107">The following `@type` values are used:</span></span>

<span data-ttu-id="e8a90-108">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="e8a90-108">@type value</span></span>                          | <span data-ttu-id="e8a90-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8a90-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="e8a90-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="e8a90-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="e8a90-111">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="e8a90-111">The initial release</span></span>
<span data-ttu-id="e8a90-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="e8a90-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="e8a90-113">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e8a90-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="e8a90-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="e8a90-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="e8a90-115">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e8a90-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="e8a90-116">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-116">Base URL</span></span>

<span data-ttu-id="e8a90-117">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="e8a90-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="e8a90-118">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="e8a90-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e8a90-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="e8a90-119">HTTP Methods</span></span>

<span data-ttu-id="e8a90-120">Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="e8a90-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="e8a90-121">Wyszukaj pakiet identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="e8a90-121">Search for package IDs</span></span>

<span data-ttu-id="e8a90-122">Autouzupełnianie pierwszy interfejs API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8a90-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="e8a90-123">Jest to doskonałe, gdy chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika, zintegrowany z źródła pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e8a90-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="e8a90-124">Pakiet wersjom tylko nieznajdujące się na liście będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="e8a90-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e8a90-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="e8a90-125">Request parameters</span></span>

<span data-ttu-id="e8a90-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8a90-126">Name</span></span>        | <span data-ttu-id="e8a90-127">W</span><span class="sxs-lookup"><span data-stu-id="e8a90-127">In</span></span>     | <span data-ttu-id="e8a90-128">Typ</span><span class="sxs-lookup"><span data-stu-id="e8a90-128">Type</span></span>    | <span data-ttu-id="e8a90-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8a90-129">Required</span></span> | <span data-ttu-id="e8a90-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8a90-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e8a90-131">q</span><span class="sxs-lookup"><span data-stu-id="e8a90-131">q</span></span>           | <span data-ttu-id="e8a90-132">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-132">URL</span></span>    | <span data-ttu-id="e8a90-133">string</span><span class="sxs-lookup"><span data-stu-id="e8a90-133">string</span></span>  | <span data-ttu-id="e8a90-134">Brak</span><span class="sxs-lookup"><span data-stu-id="e8a90-134">no</span></span>       | <span data-ttu-id="e8a90-135">Ciąg do porównania pakietu identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="e8a90-135">The string to compare against package IDs</span></span>
<span data-ttu-id="e8a90-136">Pomiń</span><span class="sxs-lookup"><span data-stu-id="e8a90-136">skip</span></span>        | <span data-ttu-id="e8a90-137">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-137">URL</span></span>    | <span data-ttu-id="e8a90-138">integer</span><span class="sxs-lookup"><span data-stu-id="e8a90-138">integer</span></span> | <span data-ttu-id="e8a90-139">Brak</span><span class="sxs-lookup"><span data-stu-id="e8a90-139">no</span></span>       | <span data-ttu-id="e8a90-140">Liczba wyników do pominięcia do dzielenia na strony</span><span class="sxs-lookup"><span data-stu-id="e8a90-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="e8a90-141">Wypełnij</span><span class="sxs-lookup"><span data-stu-id="e8a90-141">take</span></span>        | <span data-ttu-id="e8a90-142">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-142">URL</span></span>    | <span data-ttu-id="e8a90-143">integer</span><span class="sxs-lookup"><span data-stu-id="e8a90-143">integer</span></span> | <span data-ttu-id="e8a90-144">Brak</span><span class="sxs-lookup"><span data-stu-id="e8a90-144">no</span></span>       | <span data-ttu-id="e8a90-145">Liczba wyników do zwrócenia do dzielenia na strony</span><span class="sxs-lookup"><span data-stu-id="e8a90-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="e8a90-146">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="e8a90-146">prerelease</span></span>  | <span data-ttu-id="e8a90-147">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-147">URL</span></span>    | <span data-ttu-id="e8a90-148">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="e8a90-148">boolean</span></span> | <span data-ttu-id="e8a90-149">Brak</span><span class="sxs-lookup"><span data-stu-id="e8a90-149">no</span></span>       | <span data-ttu-id="e8a90-150">`true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e8a90-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e8a90-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e8a90-151">semVerLevel</span></span> | <span data-ttu-id="e8a90-152">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-152">URL</span></span>    | <span data-ttu-id="e8a90-153">string</span><span class="sxs-lookup"><span data-stu-id="e8a90-153">string</span></span>  | <span data-ttu-id="e8a90-154">Brak</span><span class="sxs-lookup"><span data-stu-id="e8a90-154">no</span></span>       | <span data-ttu-id="e8a90-155">Ciąg wersji SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="e8a90-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="e8a90-156">Zapytanie autouzupełniania `q` jest analizowany w taki sposób, który jest definiowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="e8a90-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="e8a90-157">nuget.org obsługuje zapytania dla prefiksu tokeny Identyfikatora pakietu będące rodzajów identyfikator, który został utworzony przez spliting oryginalny pisane znakami wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="e8a90-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="e8a90-158">`skip` Domyślnych wartości parametrów na 0.</span><span class="sxs-lookup"><span data-stu-id="e8a90-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="e8a90-159">`take` Parametr powinien być liczbą całkowitą większą niż zero.</span><span class="sxs-lookup"><span data-stu-id="e8a90-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="e8a90-160">Implementacja serwera może nałożyć wartość maksymalna.</span><span class="sxs-lookup"><span data-stu-id="e8a90-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="e8a90-161">Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="e8a90-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e8a90-162">`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="e8a90-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="e8a90-163">Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko pakiet identyfikatory o SemVer 1.0.0 zgodne wersje (z [standardowych wersji NuGet](../reference/package-versioning.md) zastrzeżenia, takich jak ciągi wersji z 4 elementów liczba całkowita).</span><span class="sxs-lookup"><span data-stu-id="e8a90-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="e8a90-164">Jeśli `semVerLevel=2.0.0` zostanie podana, zostaną zwrócone SemVer 1.0.0 i pakiety zgodne SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="e8a90-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="e8a90-165">Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e8a90-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e8a90-166">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8a90-166">Response</span></span>

<span data-ttu-id="e8a90-167">Odpowiedź jest dokument JSON zawierający do `take` wyniki funkcji autouzupełniania.</span><span class="sxs-lookup"><span data-stu-id="e8a90-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="e8a90-168">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="e8a90-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="e8a90-169">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8a90-169">Name</span></span>      | <span data-ttu-id="e8a90-170">Typ</span><span class="sxs-lookup"><span data-stu-id="e8a90-170">Type</span></span>             | <span data-ttu-id="e8a90-171">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8a90-171">Required</span></span> | <span data-ttu-id="e8a90-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8a90-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e8a90-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="e8a90-173">totalHits</span></span> | <span data-ttu-id="e8a90-174">integer</span><span class="sxs-lookup"><span data-stu-id="e8a90-174">integer</span></span>          | <span data-ttu-id="e8a90-175">tak</span><span class="sxs-lookup"><span data-stu-id="e8a90-175">yes</span></span>      | <span data-ttu-id="e8a90-176">Całkowita liczba dopasowań, pomijając `skip` i `take`</span><span class="sxs-lookup"><span data-stu-id="e8a90-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="e8a90-177">dane</span><span class="sxs-lookup"><span data-stu-id="e8a90-177">data</span></span>      | <span data-ttu-id="e8a90-178">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="e8a90-178">array of strings</span></span> | <span data-ttu-id="e8a90-179">tak</span><span class="sxs-lookup"><span data-stu-id="e8a90-179">yes</span></span>      | <span data-ttu-id="e8a90-180">Identyfikatory dopasowane przez żądania pakietu</span><span class="sxs-lookup"><span data-stu-id="e8a90-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="e8a90-181">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="e8a90-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e8a90-182">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8a90-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="e8a90-183">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="e8a90-183">Enumerate package versions</span></span>

<span data-ttu-id="e8a90-184">Po odnalezieniu Identyfikatora pakietu za pomocą poprzedniej interfejsu API klient może używać interfejsu API automatycznego uzupełniania wyliczyć wersji pakietu dla identyfikatora podanego pakietu</span><span class="sxs-lookup"><span data-stu-id="e8a90-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="e8a90-185">Wersja pakietu, który jest nieobecne na liście będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="e8a90-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e8a90-186">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="e8a90-186">Request parameters</span></span>

<span data-ttu-id="e8a90-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8a90-187">Name</span></span>        | <span data-ttu-id="e8a90-188">W</span><span class="sxs-lookup"><span data-stu-id="e8a90-188">In</span></span>     | <span data-ttu-id="e8a90-189">Typ</span><span class="sxs-lookup"><span data-stu-id="e8a90-189">Type</span></span>    | <span data-ttu-id="e8a90-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8a90-190">Required</span></span> | <span data-ttu-id="e8a90-191">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8a90-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e8a90-192">identyfikator</span><span class="sxs-lookup"><span data-stu-id="e8a90-192">id</span></span>          | <span data-ttu-id="e8a90-193">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-193">URL</span></span>    | <span data-ttu-id="e8a90-194">string</span><span class="sxs-lookup"><span data-stu-id="e8a90-194">string</span></span>  | <span data-ttu-id="e8a90-195">tak</span><span class="sxs-lookup"><span data-stu-id="e8a90-195">yes</span></span>      | <span data-ttu-id="e8a90-196">Identyfikator pakietu można pobrać wersji</span><span class="sxs-lookup"><span data-stu-id="e8a90-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="e8a90-197">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="e8a90-197">prerelease</span></span>  | <span data-ttu-id="e8a90-198">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-198">URL</span></span>    | <span data-ttu-id="e8a90-199">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="e8a90-199">boolean</span></span> | <span data-ttu-id="e8a90-200">Brak</span><span class="sxs-lookup"><span data-stu-id="e8a90-200">no</span></span>       | <span data-ttu-id="e8a90-201">`true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e8a90-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e8a90-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e8a90-202">semVerLevel</span></span> | <span data-ttu-id="e8a90-203">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8a90-203">URL</span></span>    | <span data-ttu-id="e8a90-204">string</span><span class="sxs-lookup"><span data-stu-id="e8a90-204">string</span></span>  | <span data-ttu-id="e8a90-205">Brak</span><span class="sxs-lookup"><span data-stu-id="e8a90-205">no</span></span>       | <span data-ttu-id="e8a90-206">Ciąg wersji SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="e8a90-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="e8a90-207">Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="e8a90-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e8a90-208">`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na pakiety SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="e8a90-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="e8a90-209">Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko wersje SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="e8a90-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="e8a90-210">Jeśli `semVerLevel=2.0.0` zostanie podana, zostanie zwrócony SemVer 1.0.0 i SemVer 2.0.0 wersji.</span><span class="sxs-lookup"><span data-stu-id="e8a90-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="e8a90-211">Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e8a90-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e8a90-212">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8a90-212">Response</span></span>

<span data-ttu-id="e8a90-213">Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podanego pakietu, filtrowanie według parametrów określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="e8a90-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="e8a90-214">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="e8a90-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="e8a90-215">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8a90-215">Name</span></span>      | <span data-ttu-id="e8a90-216">Typ</span><span class="sxs-lookup"><span data-stu-id="e8a90-216">Type</span></span>             | <span data-ttu-id="e8a90-217">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8a90-217">Required</span></span> | <span data-ttu-id="e8a90-218">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8a90-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e8a90-219">dane</span><span class="sxs-lookup"><span data-stu-id="e8a90-219">data</span></span>      | <span data-ttu-id="e8a90-220">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="e8a90-220">array of strings</span></span> | <span data-ttu-id="e8a90-221">tak</span><span class="sxs-lookup"><span data-stu-id="e8a90-221">yes</span></span>      | <span data-ttu-id="e8a90-222">Wersje pakietów dopasowane przez żądanie</span><span class="sxs-lookup"><span data-stu-id="e8a90-222">The package versions matched by the request</span></span>

<span data-ttu-id="e8a90-223">Wersje pakietów w `data` Tablica może zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` znajduje się w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="e8a90-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e8a90-224">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="e8a90-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e8a90-225">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8a90-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
