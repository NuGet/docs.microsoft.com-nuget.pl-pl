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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "Usługa autouzupełniania wyszukiwania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersje."
keywords: "Interfejs API autouzupełniania NuGet, identyfikator pakietu NuGet wyszukiwania, podciąg identyfikator pakietu"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a><span data-ttu-id="6a015-104">Funkcji AutoComplete</span><span class="sxs-lookup"><span data-stu-id="6a015-104">Autocomplete</span></span>

<span data-ttu-id="6a015-105">Istnieje możliwość tworzenia pakietu identyfikator i wersja autouzupełniania środowisko przy użyciu interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="6a015-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="6a015-106">Zasoby używane do wykonywania kwerend autouzupełniania `SearchAutocompleteService` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6a015-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6a015-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="6a015-107">Versioning</span></span>

<span data-ttu-id="6a015-108">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="6a015-108">The following `@type` values are used:</span></span>

<span data-ttu-id="6a015-109">@typewartość</span><span class="sxs-lookup"><span data-stu-id="6a015-109">@type value</span></span>                          | <span data-ttu-id="6a015-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6a015-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="6a015-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="6a015-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="6a015-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="6a015-112">The initial release</span></span>
<span data-ttu-id="6a015-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="6a015-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="6a015-114">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="6a015-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="6a015-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="6a015-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="6a015-116">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="6a015-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="6a015-117">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-117">Base URL</span></span>

<span data-ttu-id="6a015-118">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzone z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="6a015-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="6a015-119">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="6a015-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6a015-120">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="6a015-120">HTTP Methods</span></span>

<span data-ttu-id="6a015-121">Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="6a015-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="6a015-122">Wyszukaj pakiet identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="6a015-122">Search for package IDs</span></span>

<span data-ttu-id="6a015-123">Pierwszy autouzupełniania interfejsu API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="6a015-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="6a015-124">Jest to doskonały, gdy chcesz zapewnić funkcji typeahead pakietu w interfejsie użytkownika zintegrowany ze źródłem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="6a015-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="6a015-125">Pakiet o tylko wersje nieznajdujące się na liście nie będą wyświetlane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="6a015-125">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="6a015-126">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="6a015-126">Request parameters</span></span>

<span data-ttu-id="6a015-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6a015-127">Name</span></span>        | <span data-ttu-id="6a015-128">W</span><span class="sxs-lookup"><span data-stu-id="6a015-128">In</span></span>     | <span data-ttu-id="6a015-129">Typ</span><span class="sxs-lookup"><span data-stu-id="6a015-129">Type</span></span>    | <span data-ttu-id="6a015-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a015-130">Required</span></span> | <span data-ttu-id="6a015-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6a015-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="6a015-132">q</span><span class="sxs-lookup"><span data-stu-id="6a015-132">q</span></span>           | <span data-ttu-id="6a015-133">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-133">URL</span></span>    | <span data-ttu-id="6a015-134">string</span><span class="sxs-lookup"><span data-stu-id="6a015-134">string</span></span>  | <span data-ttu-id="6a015-135">Brak</span><span class="sxs-lookup"><span data-stu-id="6a015-135">no</span></span>       | <span data-ttu-id="6a015-136">Ciąg, aby porównać pakietu identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="6a015-136">The string to compare against package IDs</span></span>
<span data-ttu-id="6a015-137">Pomiń</span><span class="sxs-lookup"><span data-stu-id="6a015-137">skip</span></span>        | <span data-ttu-id="6a015-138">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-138">URL</span></span>    | <span data-ttu-id="6a015-139">integer</span><span class="sxs-lookup"><span data-stu-id="6a015-139">integer</span></span> | <span data-ttu-id="6a015-140">Brak</span><span class="sxs-lookup"><span data-stu-id="6a015-140">no</span></span>       | <span data-ttu-id="6a015-141">Liczba wyników, aby pominąć dla podział na strony</span><span class="sxs-lookup"><span data-stu-id="6a015-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="6a015-142">podejmij</span><span class="sxs-lookup"><span data-stu-id="6a015-142">take</span></span>        | <span data-ttu-id="6a015-143">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-143">URL</span></span>    | <span data-ttu-id="6a015-144">integer</span><span class="sxs-lookup"><span data-stu-id="6a015-144">integer</span></span> | <span data-ttu-id="6a015-145">Brak</span><span class="sxs-lookup"><span data-stu-id="6a015-145">no</span></span>       | <span data-ttu-id="6a015-146">Liczba wyników do zwrócenia do podział na strony</span><span class="sxs-lookup"><span data-stu-id="6a015-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="6a015-147">wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="6a015-147">prerelease</span></span>  | <span data-ttu-id="6a015-148">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-148">URL</span></span>    | <span data-ttu-id="6a015-149">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="6a015-149">boolean</span></span> | <span data-ttu-id="6a015-150">Brak</span><span class="sxs-lookup"><span data-stu-id="6a015-150">no</span></span>       | <span data-ttu-id="6a015-151">`true`lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6a015-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="6a015-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="6a015-152">semVerLevel</span></span> | <span data-ttu-id="6a015-153">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-153">URL</span></span>    | <span data-ttu-id="6a015-154">string</span><span class="sxs-lookup"><span data-stu-id="6a015-154">string</span></span>  | <span data-ttu-id="6a015-155">Brak</span><span class="sxs-lookup"><span data-stu-id="6a015-155">no</span></span>       | <span data-ttu-id="6a015-156">Ciąg wersji programu SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="6a015-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="6a015-157">Zapytanie autouzupełniania `q` jest analizowana w taki sposób, który jest zdefiniowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="6a015-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="6a015-158">nuget.org obsługuje wyszukiwanie prefiks tokeny Identyfikatora pakietu będące części identyfikatora utworzonego przez spliting oryginalnej camel znakami wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="6a015-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="6a015-159">`skip` Domyślne wartości parametrów na 0.</span><span class="sxs-lookup"><span data-stu-id="6a015-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="6a015-160">`take` Parametr powinien być liczbą całkowitą większą niż zero.</span><span class="sxs-lookup"><span data-stu-id="6a015-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="6a015-161">Implementacja serwera może nałożyć wartości maksymalnej.</span><span class="sxs-lookup"><span data-stu-id="6a015-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="6a015-162">Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6a015-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="6a015-163">`semVerLevel` Parametru zapytania jest używana do wyrazić zgodę na [pakiety programu SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="6a015-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="6a015-164">Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko pakiet identyfikatory zgodne wersje programu SemVer 1.0.0 (z [standardowe versioning NuGet](../reference/package-versioning.md) ostrzeżenia, na przykład ciągi wersji z 4 elementy liczba całkowita).</span><span class="sxs-lookup"><span data-stu-id="6a015-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="6a015-165">Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i pakiety zgodne programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6a015-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="6a015-166">Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="6a015-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="6a015-167">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6a015-167">Response</span></span>

<span data-ttu-id="6a015-168">Odpowiedź jest dokument JSON zawierający do `take` autouzupełniania wyników.</span><span class="sxs-lookup"><span data-stu-id="6a015-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="6a015-169">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6a015-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="6a015-170">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6a015-170">Name</span></span>      | <span data-ttu-id="6a015-171">Typ</span><span class="sxs-lookup"><span data-stu-id="6a015-171">Type</span></span>             | <span data-ttu-id="6a015-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a015-172">Required</span></span> | <span data-ttu-id="6a015-173">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6a015-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="6a015-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="6a015-174">totalHits</span></span> | <span data-ttu-id="6a015-175">integer</span><span class="sxs-lookup"><span data-stu-id="6a015-175">integer</span></span>          | <span data-ttu-id="6a015-176">Tak</span><span class="sxs-lookup"><span data-stu-id="6a015-176">yes</span></span>      | <span data-ttu-id="6a015-177">Całkowita liczba dopasowania, bez uwzględnienia `skip` i`take`</span><span class="sxs-lookup"><span data-stu-id="6a015-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="6a015-178">dane</span><span class="sxs-lookup"><span data-stu-id="6a015-178">data</span></span>      | <span data-ttu-id="6a015-179">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="6a015-179">array of strings</span></span> | <span data-ttu-id="6a015-180">Tak</span><span class="sxs-lookup"><span data-stu-id="6a015-180">yes</span></span>      | <span data-ttu-id="6a015-181">Identyfikatory są dopasowane wg żądania pakietu</span><span class="sxs-lookup"><span data-stu-id="6a015-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="6a015-182">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="6a015-182">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="6a015-183">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6a015-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="6a015-184">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="6a015-184">Enumerate package versions</span></span>

<span data-ttu-id="6a015-185">Po identyfikator pakietu został odnaleziony przy użyciu poprzedniej interfejsu API, klient może używać automatycznego uzupełniania interfejsu API wyliczyć wersji pakietu identyfikatora podany pakiet.</span><span class="sxs-lookup"><span data-stu-id="6a015-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="6a015-186">Wersja pakietu, który jest nieznajdujące się na liście nie będą widoczne w wynikach.</span><span class="sxs-lookup"><span data-stu-id="6a015-186">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="6a015-187">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="6a015-187">Request parameters</span></span>

<span data-ttu-id="6a015-188">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6a015-188">Name</span></span>        | <span data-ttu-id="6a015-189">W</span><span class="sxs-lookup"><span data-stu-id="6a015-189">In</span></span>     | <span data-ttu-id="6a015-190">Typ</span><span class="sxs-lookup"><span data-stu-id="6a015-190">Type</span></span>    | <span data-ttu-id="6a015-191">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a015-191">Required</span></span> | <span data-ttu-id="6a015-192">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6a015-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="6a015-193">identyfikator</span><span class="sxs-lookup"><span data-stu-id="6a015-193">id</span></span>          | <span data-ttu-id="6a015-194">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-194">URL</span></span>    | <span data-ttu-id="6a015-195">string</span><span class="sxs-lookup"><span data-stu-id="6a015-195">string</span></span>  | <span data-ttu-id="6a015-196">Tak</span><span class="sxs-lookup"><span data-stu-id="6a015-196">yes</span></span>      | <span data-ttu-id="6a015-197">Identyfikator pakietu, który można pobrać wersji</span><span class="sxs-lookup"><span data-stu-id="6a015-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="6a015-198">wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="6a015-198">prerelease</span></span>  | <span data-ttu-id="6a015-199">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-199">URL</span></span>    | <span data-ttu-id="6a015-200">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="6a015-200">boolean</span></span> | <span data-ttu-id="6a015-201">Brak</span><span class="sxs-lookup"><span data-stu-id="6a015-201">no</span></span>       | <span data-ttu-id="6a015-202">`true`lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6a015-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="6a015-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="6a015-203">semVerLevel</span></span> | <span data-ttu-id="6a015-204">Adres URL</span><span class="sxs-lookup"><span data-stu-id="6a015-204">URL</span></span>    | <span data-ttu-id="6a015-205">string</span><span class="sxs-lookup"><span data-stu-id="6a015-205">string</span></span>  | <span data-ttu-id="6a015-206">Brak</span><span class="sxs-lookup"><span data-stu-id="6a015-206">no</span></span>       | <span data-ttu-id="6a015-207">Ciąg wersji programu SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="6a015-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="6a015-208">Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6a015-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="6a015-209">`semVerLevel` Parametru zapytania jest używana w celu pakietów programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6a015-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="6a015-210">Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko wersje programu SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="6a015-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="6a015-211">Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i wersje programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="6a015-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="6a015-212">Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="6a015-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="6a015-213">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6a015-213">Response</span></span>

<span data-ttu-id="6a015-214">Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podany pakiet, filtrowanie według parametry określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="6a015-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="6a015-215">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="6a015-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="6a015-216">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6a015-216">Name</span></span>      | <span data-ttu-id="6a015-217">Typ</span><span class="sxs-lookup"><span data-stu-id="6a015-217">Type</span></span>             | <span data-ttu-id="6a015-218">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6a015-218">Required</span></span> | <span data-ttu-id="6a015-219">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6a015-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="6a015-220">dane</span><span class="sxs-lookup"><span data-stu-id="6a015-220">data</span></span>      | <span data-ttu-id="6a015-221">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="6a015-221">array of strings</span></span> | <span data-ttu-id="6a015-222">Tak</span><span class="sxs-lookup"><span data-stu-id="6a015-222">yes</span></span>      | <span data-ttu-id="6a015-223">Wersje pakietów, które są dopasowane wg żądania</span><span class="sxs-lookup"><span data-stu-id="6a015-223">The package versions matched by the request</span></span>

<span data-ttu-id="6a015-224">Wersje pakietu w `data` Tablica może zawierać metadane kompilacji programu SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` podany w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="6a015-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6a015-225">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="6a015-225">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="6a015-226">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6a015-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
