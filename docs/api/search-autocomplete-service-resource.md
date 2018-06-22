---
title: Funkcji AutoComplete, NuGet interfejsu API
description: Usługa autouzupełniania wyszukiwania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersje.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822139"
---
# <a name="autocomplete"></a><span data-ttu-id="d9c0f-103">Funkcji AutoComplete</span><span class="sxs-lookup"><span data-stu-id="d9c0f-103">Autocomplete</span></span>

<span data-ttu-id="d9c0f-104">Istnieje możliwość tworzenia pakietu identyfikator i wersja autouzupełniania środowisko przy użyciu interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d9c0f-105">Zasoby używane do wykonywania kwerend autouzupełniania `SearchAutocompleteService` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d9c0f-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="d9c0f-106">Versioning</span></span>

<span data-ttu-id="d9c0f-107">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-107">The following `@type` values are used:</span></span>

<span data-ttu-id="d9c0f-108">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="d9c0f-108">@type value</span></span>                          | <span data-ttu-id="d9c0f-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d9c0f-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d9c0f-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d9c0f-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="d9c0f-111">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="d9c0f-111">The initial release</span></span>
<span data-ttu-id="d9c0f-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d9c0f-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d9c0f-113">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d9c0f-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d9c0f-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d9c0f-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d9c0f-115">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d9c0f-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="d9c0f-116">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-116">Base URL</span></span>

<span data-ttu-id="d9c0f-117">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzone z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d9c0f-118">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d9c0f-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="d9c0f-119">HTTP Methods</span></span>

<span data-ttu-id="d9c0f-120">Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d9c0f-121">Wyszukaj pakiet identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="d9c0f-121">Search for package IDs</span></span>

<span data-ttu-id="d9c0f-122">Pierwszy autouzupełniania interfejsu API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d9c0f-123">Jest to doskonały, gdy chcesz zapewnić funkcji typeahead pakietu w interfejsie użytkownika zintegrowany ze źródłem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d9c0f-124">Pakiet o tylko wersje nieznajdujące się na liście nie będą wyświetlane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d9c0f-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="d9c0f-125">Request parameters</span></span>

<span data-ttu-id="d9c0f-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d9c0f-126">Name</span></span>        | <span data-ttu-id="d9c0f-127">W</span><span class="sxs-lookup"><span data-stu-id="d9c0f-127">In</span></span>     | <span data-ttu-id="d9c0f-128">Typ</span><span class="sxs-lookup"><span data-stu-id="d9c0f-128">Type</span></span>    | <span data-ttu-id="d9c0f-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d9c0f-129">Required</span></span> | <span data-ttu-id="d9c0f-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d9c0f-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d9c0f-131">q</span><span class="sxs-lookup"><span data-stu-id="d9c0f-131">q</span></span>           | <span data-ttu-id="d9c0f-132">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-132">URL</span></span>    | <span data-ttu-id="d9c0f-133">string</span><span class="sxs-lookup"><span data-stu-id="d9c0f-133">string</span></span>  | <span data-ttu-id="d9c0f-134">Brak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-134">no</span></span>       | <span data-ttu-id="d9c0f-135">Ciąg, aby porównać pakietu identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="d9c0f-135">The string to compare against package IDs</span></span>
<span data-ttu-id="d9c0f-136">Pomiń</span><span class="sxs-lookup"><span data-stu-id="d9c0f-136">skip</span></span>        | <span data-ttu-id="d9c0f-137">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-137">URL</span></span>    | <span data-ttu-id="d9c0f-138">integer</span><span class="sxs-lookup"><span data-stu-id="d9c0f-138">integer</span></span> | <span data-ttu-id="d9c0f-139">Brak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-139">no</span></span>       | <span data-ttu-id="d9c0f-140">Liczba wyników, aby pominąć dla podział na strony</span><span class="sxs-lookup"><span data-stu-id="d9c0f-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d9c0f-141">podejmij</span><span class="sxs-lookup"><span data-stu-id="d9c0f-141">take</span></span>        | <span data-ttu-id="d9c0f-142">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-142">URL</span></span>    | <span data-ttu-id="d9c0f-143">integer</span><span class="sxs-lookup"><span data-stu-id="d9c0f-143">integer</span></span> | <span data-ttu-id="d9c0f-144">Brak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-144">no</span></span>       | <span data-ttu-id="d9c0f-145">Liczba wyników do zwrócenia do podział na strony</span><span class="sxs-lookup"><span data-stu-id="d9c0f-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="d9c0f-146">wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="d9c0f-146">prerelease</span></span>  | <span data-ttu-id="d9c0f-147">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-147">URL</span></span>    | <span data-ttu-id="d9c0f-148">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="d9c0f-148">boolean</span></span> | <span data-ttu-id="d9c0f-149">Brak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-149">no</span></span>       | <span data-ttu-id="d9c0f-150">`true` lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d9c0f-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d9c0f-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d9c0f-151">semVerLevel</span></span> | <span data-ttu-id="d9c0f-152">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-152">URL</span></span>    | <span data-ttu-id="d9c0f-153">string</span><span class="sxs-lookup"><span data-stu-id="d9c0f-153">string</span></span>  | <span data-ttu-id="d9c0f-154">Brak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-154">no</span></span>       | <span data-ttu-id="d9c0f-155">Ciąg wersji programu SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="d9c0f-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d9c0f-156">Zapytanie autouzupełniania `q` jest analizowana w taki sposób, który jest zdefiniowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d9c0f-157">nuget.org obsługuje wyszukiwanie prefiks tokeny Identyfikatora pakietu będące części identyfikatora utworzonego przez spliting oryginalnej camel znakami wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d9c0f-158">`skip` Domyślne wartości parametrów na 0.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d9c0f-159">`take` Parametr powinien być liczbą całkowitą większą niż zero.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d9c0f-160">Implementacja serwera może nałożyć wartości maksymalnej.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d9c0f-161">Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d9c0f-162">`semVerLevel` Parametru zapytania jest używana do wyrazić zgodę na [pakiety programu SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d9c0f-163">Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko pakiet identyfikatory zgodne wersje programu SemVer 1.0.0 (z [standardowe versioning NuGet](../reference/package-versioning.md) ostrzeżenia, na przykład ciągi wersji z 4 elementy liczba całkowita).</span><span class="sxs-lookup"><span data-stu-id="d9c0f-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d9c0f-164">Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i pakiety zgodne programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d9c0f-165">Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d9c0f-166">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="d9c0f-166">Response</span></span>

<span data-ttu-id="d9c0f-167">Odpowiedź jest dokument JSON zawierający do `take` autouzupełniania wyników.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d9c0f-168">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d9c0f-169">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d9c0f-169">Name</span></span>      | <span data-ttu-id="d9c0f-170">Typ</span><span class="sxs-lookup"><span data-stu-id="d9c0f-170">Type</span></span>             | <span data-ttu-id="d9c0f-171">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d9c0f-171">Required</span></span> | <span data-ttu-id="d9c0f-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d9c0f-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d9c0f-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="d9c0f-173">totalHits</span></span> | <span data-ttu-id="d9c0f-174">integer</span><span class="sxs-lookup"><span data-stu-id="d9c0f-174">integer</span></span>          | <span data-ttu-id="d9c0f-175">Tak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-175">yes</span></span>      | <span data-ttu-id="d9c0f-176">Całkowita liczba dopasowania, bez uwzględnienia `skip` i `take`</span><span class="sxs-lookup"><span data-stu-id="d9c0f-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d9c0f-177">dane</span><span class="sxs-lookup"><span data-stu-id="d9c0f-177">data</span></span>      | <span data-ttu-id="d9c0f-178">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="d9c0f-178">array of strings</span></span> | <span data-ttu-id="d9c0f-179">Tak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-179">yes</span></span>      | <span data-ttu-id="d9c0f-180">Identyfikatory są dopasowane wg żądania pakietu</span><span class="sxs-lookup"><span data-stu-id="d9c0f-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d9c0f-181">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="d9c0f-181">Sample request</span></span>

<span data-ttu-id="d9c0f-182">POBIERZ https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="d9c0f-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="d9c0f-183">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="d9c0f-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d9c0f-184">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="d9c0f-184">Enumerate package versions</span></span>

<span data-ttu-id="d9c0f-185">Po identyfikator pakietu został odnaleziony przy użyciu poprzedniej interfejsu API, klient może używać automatycznego uzupełniania interfejsu API wyliczyć wersji pakietu identyfikatora podany pakiet.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d9c0f-186">Wersja pakietu, który jest nieznajdujące się na liście nie będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d9c0f-187">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="d9c0f-187">Request parameters</span></span>

<span data-ttu-id="d9c0f-188">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d9c0f-188">Name</span></span>        | <span data-ttu-id="d9c0f-189">W</span><span class="sxs-lookup"><span data-stu-id="d9c0f-189">In</span></span>     | <span data-ttu-id="d9c0f-190">Typ</span><span class="sxs-lookup"><span data-stu-id="d9c0f-190">Type</span></span>    | <span data-ttu-id="d9c0f-191">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d9c0f-191">Required</span></span> | <span data-ttu-id="d9c0f-192">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d9c0f-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d9c0f-193">identyfikator</span><span class="sxs-lookup"><span data-stu-id="d9c0f-193">id</span></span>          | <span data-ttu-id="d9c0f-194">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-194">URL</span></span>    | <span data-ttu-id="d9c0f-195">string</span><span class="sxs-lookup"><span data-stu-id="d9c0f-195">string</span></span>  | <span data-ttu-id="d9c0f-196">Tak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-196">yes</span></span>      | <span data-ttu-id="d9c0f-197">Identyfikator pakietu, który można pobrać wersji</span><span class="sxs-lookup"><span data-stu-id="d9c0f-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="d9c0f-198">wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="d9c0f-198">prerelease</span></span>  | <span data-ttu-id="d9c0f-199">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-199">URL</span></span>    | <span data-ttu-id="d9c0f-200">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="d9c0f-200">boolean</span></span> | <span data-ttu-id="d9c0f-201">Brak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-201">no</span></span>       | <span data-ttu-id="d9c0f-202">`true` lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d9c0f-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d9c0f-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d9c0f-203">semVerLevel</span></span> | <span data-ttu-id="d9c0f-204">Adres URL</span><span class="sxs-lookup"><span data-stu-id="d9c0f-204">URL</span></span>    | <span data-ttu-id="d9c0f-205">string</span><span class="sxs-lookup"><span data-stu-id="d9c0f-205">string</span></span>  | <span data-ttu-id="d9c0f-206">Brak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-206">no</span></span>       | <span data-ttu-id="d9c0f-207">Ciąg wersji programu SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9c0f-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d9c0f-208">Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d9c0f-209">`semVerLevel` Parametru zapytania jest używana w celu pakietów programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d9c0f-210">Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko wersje programu SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d9c0f-211">Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i wersje programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d9c0f-212">Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d9c0f-213">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="d9c0f-213">Response</span></span>

<span data-ttu-id="d9c0f-214">Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podany pakiet, filtrowanie według parametry określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d9c0f-215">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="d9c0f-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="d9c0f-216">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d9c0f-216">Name</span></span>      | <span data-ttu-id="d9c0f-217">Typ</span><span class="sxs-lookup"><span data-stu-id="d9c0f-217">Type</span></span>             | <span data-ttu-id="d9c0f-218">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d9c0f-218">Required</span></span> | <span data-ttu-id="d9c0f-219">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d9c0f-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d9c0f-220">dane</span><span class="sxs-lookup"><span data-stu-id="d9c0f-220">data</span></span>      | <span data-ttu-id="d9c0f-221">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="d9c0f-221">array of strings</span></span> | <span data-ttu-id="d9c0f-222">Tak</span><span class="sxs-lookup"><span data-stu-id="d9c0f-222">yes</span></span>      | <span data-ttu-id="d9c0f-223">Wersje pakietów, które są dopasowane wg żądania</span><span class="sxs-lookup"><span data-stu-id="d9c0f-223">The package versions matched by the request</span></span>

<span data-ttu-id="d9c0f-224">Wersje pakietu w `data` Tablica może zawierać metadane kompilacji programu SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` podany w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="d9c0f-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d9c0f-225">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="d9c0f-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d9c0f-226">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="d9c0f-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
