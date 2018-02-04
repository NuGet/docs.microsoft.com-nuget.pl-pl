---
title: Funkcji AutoComplete, NuGet interfejsu API | Dokumentacja firmy Microsoft
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
description: "Usługa autouzupełniania wyszukiwania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersje."
keywords: "Interfejs API autouzupełniania NuGet, identyfikator pakietu NuGet wyszukiwania, podciąg identyfikator pakietu"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a><span data-ttu-id="845d3-104">Funkcji AutoComplete</span><span class="sxs-lookup"><span data-stu-id="845d3-104">Autocomplete</span></span>

<span data-ttu-id="845d3-105">Istnieje możliwość tworzenia pakietu identyfikator i wersja autouzupełniania środowisko przy użyciu interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="845d3-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="845d3-106">Zasoby używane do wykonywania kwerend autouzupełniania `SearchAutocompleteService` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="845d3-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="845d3-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="845d3-107">Versioning</span></span>

<span data-ttu-id="845d3-108">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="845d3-108">The following `@type` values are used:</span></span>

<span data-ttu-id="845d3-109">@typewartość</span><span class="sxs-lookup"><span data-stu-id="845d3-109">@type value</span></span>                          | <span data-ttu-id="845d3-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="845d3-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="845d3-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="845d3-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="845d3-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="845d3-112">The initial release</span></span>
<span data-ttu-id="845d3-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="845d3-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="845d3-114">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="845d3-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="845d3-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="845d3-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="845d3-116">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="845d3-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="845d3-117">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-117">Base URL</span></span>

<span data-ttu-id="845d3-118">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzone z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="845d3-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="845d3-119">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="845d3-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="845d3-120">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="845d3-120">HTTP Methods</span></span>

<span data-ttu-id="845d3-121">Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="845d3-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="845d3-122">Wyszukaj pakiet identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="845d3-122">Search for package IDs</span></span>

<span data-ttu-id="845d3-123">Pierwszy autouzupełniania interfejsu API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="845d3-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="845d3-124">Jest to doskonały, gdy chcesz zapewnić funkcji typeahead pakietu w interfejsie użytkownika zintegrowany ze źródłem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="845d3-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="845d3-125">Pakiet o tylko wersje nieznajdujące się na liście nie będą wyświetlane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="845d3-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="845d3-126">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="845d3-126">Request parameters</span></span>

<span data-ttu-id="845d3-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="845d3-127">Name</span></span>        | <span data-ttu-id="845d3-128">W</span><span class="sxs-lookup"><span data-stu-id="845d3-128">In</span></span>     | <span data-ttu-id="845d3-129">Typ</span><span class="sxs-lookup"><span data-stu-id="845d3-129">Type</span></span>    | <span data-ttu-id="845d3-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="845d3-130">Required</span></span> | <span data-ttu-id="845d3-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="845d3-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="845d3-132">q</span><span class="sxs-lookup"><span data-stu-id="845d3-132">q</span></span>           | <span data-ttu-id="845d3-133">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-133">URL</span></span>    | <span data-ttu-id="845d3-134">string</span><span class="sxs-lookup"><span data-stu-id="845d3-134">string</span></span>  | <span data-ttu-id="845d3-135">Brak</span><span class="sxs-lookup"><span data-stu-id="845d3-135">no</span></span>       | <span data-ttu-id="845d3-136">Ciąg, aby porównać pakietu identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="845d3-136">The string to compare against package IDs</span></span>
<span data-ttu-id="845d3-137">Pomiń</span><span class="sxs-lookup"><span data-stu-id="845d3-137">skip</span></span>        | <span data-ttu-id="845d3-138">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-138">URL</span></span>    | <span data-ttu-id="845d3-139">integer</span><span class="sxs-lookup"><span data-stu-id="845d3-139">integer</span></span> | <span data-ttu-id="845d3-140">Brak</span><span class="sxs-lookup"><span data-stu-id="845d3-140">no</span></span>       | <span data-ttu-id="845d3-141">Liczba wyników, aby pominąć dla podział na strony</span><span class="sxs-lookup"><span data-stu-id="845d3-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="845d3-142">podejmij</span><span class="sxs-lookup"><span data-stu-id="845d3-142">take</span></span>        | <span data-ttu-id="845d3-143">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-143">URL</span></span>    | <span data-ttu-id="845d3-144">integer</span><span class="sxs-lookup"><span data-stu-id="845d3-144">integer</span></span> | <span data-ttu-id="845d3-145">Brak</span><span class="sxs-lookup"><span data-stu-id="845d3-145">no</span></span>       | <span data-ttu-id="845d3-146">Liczba wyników do zwrócenia do podział na strony</span><span class="sxs-lookup"><span data-stu-id="845d3-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="845d3-147">wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="845d3-147">prerelease</span></span>  | <span data-ttu-id="845d3-148">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-148">URL</span></span>    | <span data-ttu-id="845d3-149">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="845d3-149">boolean</span></span> | <span data-ttu-id="845d3-150">Brak</span><span class="sxs-lookup"><span data-stu-id="845d3-150">no</span></span>       | <span data-ttu-id="845d3-151">`true`lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="845d3-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="845d3-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="845d3-152">semVerLevel</span></span> | <span data-ttu-id="845d3-153">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-153">URL</span></span>    | <span data-ttu-id="845d3-154">string</span><span class="sxs-lookup"><span data-stu-id="845d3-154">string</span></span>  | <span data-ttu-id="845d3-155">Brak</span><span class="sxs-lookup"><span data-stu-id="845d3-155">no</span></span>       | <span data-ttu-id="845d3-156">Ciąg wersji programu SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="845d3-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="845d3-157">Zapytanie autouzupełniania `q` jest analizowana w taki sposób, który jest zdefiniowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="845d3-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="845d3-158">nuget.org obsługuje wyszukiwanie prefiks tokeny Identyfikatora pakietu będące części identyfikatora utworzonego przez spliting oryginalnej camel znakami wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="845d3-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="845d3-159">`skip` Domyślne wartości parametrów na 0.</span><span class="sxs-lookup"><span data-stu-id="845d3-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="845d3-160">`take` Parametr powinien być liczbą całkowitą większą niż zero.</span><span class="sxs-lookup"><span data-stu-id="845d3-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="845d3-161">Implementacja serwera może nałożyć wartości maksymalnej.</span><span class="sxs-lookup"><span data-stu-id="845d3-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="845d3-162">Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="845d3-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="845d3-163">`semVerLevel` Parametru zapytania jest używana do wyrazić zgodę na [pakiety programu SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="845d3-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="845d3-164">Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko pakiet identyfikatory zgodne wersje programu SemVer 1.0.0 (z [standardowe versioning NuGet](../reference/package-versioning.md) ostrzeżenia, na przykład ciągi wersji z 4 elementy liczba całkowita).</span><span class="sxs-lookup"><span data-stu-id="845d3-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="845d3-165">Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i pakiety zgodne programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="845d3-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="845d3-166">Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="845d3-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="845d3-167">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="845d3-167">Response</span></span>

<span data-ttu-id="845d3-168">Odpowiedź jest dokument JSON zawierający do `take` autouzupełniania wyników.</span><span class="sxs-lookup"><span data-stu-id="845d3-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="845d3-169">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="845d3-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="845d3-170">Nazwa</span><span class="sxs-lookup"><span data-stu-id="845d3-170">Name</span></span>      | <span data-ttu-id="845d3-171">Typ</span><span class="sxs-lookup"><span data-stu-id="845d3-171">Type</span></span>             | <span data-ttu-id="845d3-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="845d3-172">Required</span></span> | <span data-ttu-id="845d3-173">Uwagi</span><span class="sxs-lookup"><span data-stu-id="845d3-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="845d3-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="845d3-174">totalHits</span></span> | <span data-ttu-id="845d3-175">integer</span><span class="sxs-lookup"><span data-stu-id="845d3-175">integer</span></span>          | <span data-ttu-id="845d3-176">Tak</span><span class="sxs-lookup"><span data-stu-id="845d3-176">yes</span></span>      | <span data-ttu-id="845d3-177">Całkowita liczba dopasowania, bez uwzględnienia `skip` i`take`</span><span class="sxs-lookup"><span data-stu-id="845d3-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="845d3-178">dane</span><span class="sxs-lookup"><span data-stu-id="845d3-178">data</span></span>      | <span data-ttu-id="845d3-179">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="845d3-179">array of strings</span></span> | <span data-ttu-id="845d3-180">Tak</span><span class="sxs-lookup"><span data-stu-id="845d3-180">yes</span></span>      | <span data-ttu-id="845d3-181">Identyfikatory są dopasowane wg żądania pakietu</span><span class="sxs-lookup"><span data-stu-id="845d3-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="845d3-182">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="845d3-182">Sample request</span></span>

<span data-ttu-id="845d3-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="845d3-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="845d3-184">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="845d3-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="845d3-185">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="845d3-185">Enumerate package versions</span></span>

<span data-ttu-id="845d3-186">Po identyfikator pakietu został odnaleziony przy użyciu poprzedniej interfejsu API, klient może używać automatycznego uzupełniania interfejsu API wyliczyć wersji pakietu identyfikatora podany pakiet.</span><span class="sxs-lookup"><span data-stu-id="845d3-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="845d3-187">Wersja pakietu, który jest nieznajdujące się na liście nie będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="845d3-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="845d3-188">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="845d3-188">Request parameters</span></span>

<span data-ttu-id="845d3-189">Nazwa</span><span class="sxs-lookup"><span data-stu-id="845d3-189">Name</span></span>        | <span data-ttu-id="845d3-190">W</span><span class="sxs-lookup"><span data-stu-id="845d3-190">In</span></span>     | <span data-ttu-id="845d3-191">Typ</span><span class="sxs-lookup"><span data-stu-id="845d3-191">Type</span></span>    | <span data-ttu-id="845d3-192">Wymagane</span><span class="sxs-lookup"><span data-stu-id="845d3-192">Required</span></span> | <span data-ttu-id="845d3-193">Uwagi</span><span class="sxs-lookup"><span data-stu-id="845d3-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="845d3-194">identyfikator</span><span class="sxs-lookup"><span data-stu-id="845d3-194">id</span></span>          | <span data-ttu-id="845d3-195">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-195">URL</span></span>    | <span data-ttu-id="845d3-196">string</span><span class="sxs-lookup"><span data-stu-id="845d3-196">string</span></span>  | <span data-ttu-id="845d3-197">Tak</span><span class="sxs-lookup"><span data-stu-id="845d3-197">yes</span></span>      | <span data-ttu-id="845d3-198">Identyfikator pakietu, który można pobrać wersji</span><span class="sxs-lookup"><span data-stu-id="845d3-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="845d3-199">wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="845d3-199">prerelease</span></span>  | <span data-ttu-id="845d3-200">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-200">URL</span></span>    | <span data-ttu-id="845d3-201">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="845d3-201">boolean</span></span> | <span data-ttu-id="845d3-202">Brak</span><span class="sxs-lookup"><span data-stu-id="845d3-202">no</span></span>       | <span data-ttu-id="845d3-203">`true`lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="845d3-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="845d3-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="845d3-204">semVerLevel</span></span> | <span data-ttu-id="845d3-205">Adres URL</span><span class="sxs-lookup"><span data-stu-id="845d3-205">URL</span></span>    | <span data-ttu-id="845d3-206">string</span><span class="sxs-lookup"><span data-stu-id="845d3-206">string</span></span>  | <span data-ttu-id="845d3-207">Brak</span><span class="sxs-lookup"><span data-stu-id="845d3-207">no</span></span>       | <span data-ttu-id="845d3-208">Ciąg wersji programu SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="845d3-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="845d3-209">Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="845d3-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="845d3-210">`semVerLevel` Parametru zapytania jest używana w celu pakietów programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="845d3-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="845d3-211">Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko wersje programu SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="845d3-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="845d3-212">Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i wersje programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="845d3-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="845d3-213">Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="845d3-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="845d3-214">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="845d3-214">Response</span></span>

<span data-ttu-id="845d3-215">Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podany pakiet, filtrowanie według parametry określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="845d3-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="845d3-216">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="845d3-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="845d3-217">Nazwa</span><span class="sxs-lookup"><span data-stu-id="845d3-217">Name</span></span>      | <span data-ttu-id="845d3-218">Typ</span><span class="sxs-lookup"><span data-stu-id="845d3-218">Type</span></span>             | <span data-ttu-id="845d3-219">Wymagane</span><span class="sxs-lookup"><span data-stu-id="845d3-219">Required</span></span> | <span data-ttu-id="845d3-220">Uwagi</span><span class="sxs-lookup"><span data-stu-id="845d3-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="845d3-221">dane</span><span class="sxs-lookup"><span data-stu-id="845d3-221">data</span></span>      | <span data-ttu-id="845d3-222">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="845d3-222">array of strings</span></span> | <span data-ttu-id="845d3-223">Tak</span><span class="sxs-lookup"><span data-stu-id="845d3-223">yes</span></span>      | <span data-ttu-id="845d3-224">Wersje pakietów, które są dopasowane wg żądania</span><span class="sxs-lookup"><span data-stu-id="845d3-224">The package versions matched by the request</span></span>

<span data-ttu-id="845d3-225">Wersje pakietu w `data` Tablica może zawierać metadane kompilacji programu SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` podany w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="845d3-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="845d3-226">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="845d3-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="845d3-227">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="845d3-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
