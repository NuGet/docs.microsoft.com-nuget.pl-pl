---
title: Autouzupełnianie, interfejs API NuGet
description: Usługa wyszukiwania autouzupełniania obsługuje interaktywne odnajdywanie identyfikatorów pakietów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773956"
---
# <a name="autocomplete"></a><span data-ttu-id="012ee-103">Autouzupełnianie</span><span class="sxs-lookup"><span data-stu-id="012ee-103">Autocomplete</span></span>

<span data-ttu-id="012ee-104">Istnieje możliwość utworzenia identyfikatora pakietu i funkcji Autouzupełnianie wersji przy użyciu interfejsu API v3.</span><span class="sxs-lookup"><span data-stu-id="012ee-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="012ee-105">Zasób używany do wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` zasobem znalezionym w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="012ee-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="012ee-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="012ee-106">Versioning</span></span>

<span data-ttu-id="012ee-107">`@type`Są używane następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="012ee-107">The following `@type` values are used:</span></span>

<span data-ttu-id="012ee-108">@type wartościami</span><span class="sxs-lookup"><span data-stu-id="012ee-108">@type value</span></span>                          | <span data-ttu-id="012ee-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="012ee-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="012ee-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="012ee-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="012ee-111">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="012ee-111">The initial release</span></span>
<span data-ttu-id="012ee-112">SearchAutocompleteService/3.0.0 — beta</span><span class="sxs-lookup"><span data-stu-id="012ee-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="012ee-113">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="012ee-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="012ee-114">SearchAutocompleteService/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="012ee-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="012ee-115">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="012ee-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="012ee-116">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="012ee-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="012ee-117">Obejmuje obsługę `packageType` parametru zapytania</span><span class="sxs-lookup"><span data-stu-id="012ee-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="012ee-118">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="012ee-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="012ee-119">Ta wersja wprowadza obsługę `packageType` parametru zapytania, umożliwiając filtrowanie według typów pakietów zdefiniowanych przez autora.</span><span class="sxs-lookup"><span data-stu-id="012ee-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="012ee-120">Jest w pełni zgodna z poprzednimi wersjami zapytań `SearchAutocompleteService` .</span><span class="sxs-lookup"><span data-stu-id="012ee-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="012ee-121">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-121">Base URL</span></span>

<span data-ttu-id="012ee-122">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` Właściwości skojarzoną z jedną z wyżej wymienionych `@type` wartości zasobów.</span><span class="sxs-lookup"><span data-stu-id="012ee-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="012ee-123">W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego adresu URL `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="012ee-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="012ee-124">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="012ee-124">HTTP Methods</span></span>

<span data-ttu-id="012ee-125">Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują metody HTTP `GET` i `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="012ee-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="012ee-126">Wyszukaj identyfikatory pakietów</span><span class="sxs-lookup"><span data-stu-id="012ee-126">Search for package IDs</span></span>

<span data-ttu-id="012ee-127">Pierwszy interfejs API funkcji Autouzupełnianie obsługuje wyszukiwanie części ciągu identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="012ee-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="012ee-128">Jest to doskonałe rozwiązanie, jeśli chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika zintegrowanym ze źródłem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="012ee-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="012ee-129">Pakiet z tylko wersjami nieznajdującymi się na liście nie będzie wyświetlany w wynikach.</span><span class="sxs-lookup"><span data-stu-id="012ee-129">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a><span data-ttu-id="012ee-130">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="012ee-130">Request parameters</span></span>

<span data-ttu-id="012ee-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="012ee-131">Name</span></span>        | <span data-ttu-id="012ee-132">W</span><span class="sxs-lookup"><span data-stu-id="012ee-132">In</span></span>     | <span data-ttu-id="012ee-133">Typ</span><span class="sxs-lookup"><span data-stu-id="012ee-133">Type</span></span>    | <span data-ttu-id="012ee-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="012ee-134">Required</span></span> | <span data-ttu-id="012ee-135">Uwagi</span><span class="sxs-lookup"><span data-stu-id="012ee-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="012ee-136">q</span><span class="sxs-lookup"><span data-stu-id="012ee-136">q</span></span>           | <span data-ttu-id="012ee-137">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-137">URL</span></span>    | <span data-ttu-id="012ee-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="012ee-138">string</span></span>  | <span data-ttu-id="012ee-139">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-139">no</span></span>       | <span data-ttu-id="012ee-140">Ciąg do porównania z identyfikatorami pakietów</span><span class="sxs-lookup"><span data-stu-id="012ee-140">The string to compare against package IDs</span></span>
<span data-ttu-id="012ee-141">Pomiń</span><span class="sxs-lookup"><span data-stu-id="012ee-141">skip</span></span>        | <span data-ttu-id="012ee-142">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-142">URL</span></span>    | <span data-ttu-id="012ee-143">liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="012ee-143">integer</span></span> | <span data-ttu-id="012ee-144">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-144">no</span></span>       | <span data-ttu-id="012ee-145">Liczba wyników do pominięcia na stronie stronicowania</span><span class="sxs-lookup"><span data-stu-id="012ee-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="012ee-146">take (pobierz)</span><span class="sxs-lookup"><span data-stu-id="012ee-146">take</span></span>        | <span data-ttu-id="012ee-147">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-147">URL</span></span>    | <span data-ttu-id="012ee-148">liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="012ee-148">integer</span></span> | <span data-ttu-id="012ee-149">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-149">no</span></span>       | <span data-ttu-id="012ee-150">Liczba wyników do zwrócenia, na stronie stronicowania</span><span class="sxs-lookup"><span data-stu-id="012ee-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="012ee-151">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="012ee-151">prerelease</span></span>  | <span data-ttu-id="012ee-152">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-152">URL</span></span>    | <span data-ttu-id="012ee-153">boolean</span><span class="sxs-lookup"><span data-stu-id="012ee-153">boolean</span></span> | <span data-ttu-id="012ee-154">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-154">no</span></span>       | <span data-ttu-id="012ee-155">`true` lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="012ee-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="012ee-156">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="012ee-156">semVerLevel</span></span> | <span data-ttu-id="012ee-157">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-157">URL</span></span>    | <span data-ttu-id="012ee-158">ciąg</span><span class="sxs-lookup"><span data-stu-id="012ee-158">string</span></span>  | <span data-ttu-id="012ee-159">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-159">no</span></span>       | <span data-ttu-id="012ee-160">Ciąg wersji SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="012ee-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="012ee-161">packageType</span><span class="sxs-lookup"><span data-stu-id="012ee-161">packageType</span></span> | <span data-ttu-id="012ee-162">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-162">URL</span></span>    | <span data-ttu-id="012ee-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="012ee-163">string</span></span>  | <span data-ttu-id="012ee-164">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-164">no</span></span>       | <span data-ttu-id="012ee-165">Typ pakietu, który ma być używany do filtrowania pakietów (dodana w `SearchAutocompleteService/3.5.0` )</span><span class="sxs-lookup"><span data-stu-id="012ee-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="012ee-166">Zapytanie autouzupełniania `q` jest analizowane w sposób zdefiniowany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="012ee-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="012ee-167">nuget.org obsługuje zapytania dotyczące prefiksu tokenów identyfikatora pakietu, które są częścią identyfikatora wygenerowanego przez podzielenie oryginalnego znaku przez notacji CamelCase wielkość liter i symboli.</span><span class="sxs-lookup"><span data-stu-id="012ee-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="012ee-168">Wartość `skip` domyślna parametru to 0.</span><span class="sxs-lookup"><span data-stu-id="012ee-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="012ee-169">`take`Parametr powinien być liczbą całkowitą większą od zera.</span><span class="sxs-lookup"><span data-stu-id="012ee-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="012ee-170">Implementacja serwera może mieć wartość maksymalną.</span><span class="sxs-lookup"><span data-stu-id="012ee-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="012ee-171">Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.</span><span class="sxs-lookup"><span data-stu-id="012ee-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="012ee-172">`semVerLevel`Parametr zapytania jest używany do wybierania [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="012ee-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="012ee-173">Jeśli ten parametr zapytania zostanie wykluczony, zostaną zwrócone tylko identyfikatory pakietów z zgodnymi wersjami programu SemVer 1.0.0 (ze [standardowymi](../concepts/package-versioning.md) ograniczeniami wersji programu NuGet, takimi jak ciągi wersji z 4 liczbami całkowitymi).</span><span class="sxs-lookup"><span data-stu-id="012ee-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="012ee-174">Jeśli `semVerLevel=2.0.0` jest podany, zwracane są zgodne z SemVer 1.0.0 i SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="012ee-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="012ee-175">Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="012ee-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="012ee-176">Ten `packageType` parametr służy do dokładniejszego filtrowania wyników autouzupełniania do pakietów, które mają co najmniej jeden typ pakietu pasujący do nazwy typu pakietu.</span><span class="sxs-lookup"><span data-stu-id="012ee-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="012ee-177">Jeśli podany typ pakietu nie jest prawidłowym typem pakietu zdefiniowanym przez [dokument typu pakietu](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), zostanie zwrócony pusty wynik.</span><span class="sxs-lookup"><span data-stu-id="012ee-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="012ee-178">Jeśli podany typ pakietu jest pusty, żaden filtr nie zostanie zastosowany.</span><span class="sxs-lookup"><span data-stu-id="012ee-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="012ee-179">Innymi słowy, przekazywanie żadnej wartości do `packageType` parametru będzie zachowywać się tak, jakby parametr nie został przekazano.</span><span class="sxs-lookup"><span data-stu-id="012ee-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="012ee-180">Reakcja</span><span class="sxs-lookup"><span data-stu-id="012ee-180">Response</span></span>

<span data-ttu-id="012ee-181">Odpowiedź jest dokumentem JSON zawierającym do `take` wyników Autouzupełnianie.</span><span class="sxs-lookup"><span data-stu-id="012ee-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="012ee-182">Główny obiekt JSON ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="012ee-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="012ee-183">Nazwa</span><span class="sxs-lookup"><span data-stu-id="012ee-183">Name</span></span>      | <span data-ttu-id="012ee-184">Typ</span><span class="sxs-lookup"><span data-stu-id="012ee-184">Type</span></span>             | <span data-ttu-id="012ee-185">Wymagane</span><span class="sxs-lookup"><span data-stu-id="012ee-185">Required</span></span> | <span data-ttu-id="012ee-186">Uwagi</span><span class="sxs-lookup"><span data-stu-id="012ee-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="012ee-187">totalHits</span><span class="sxs-lookup"><span data-stu-id="012ee-187">totalHits</span></span> | <span data-ttu-id="012ee-188">liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="012ee-188">integer</span></span>          | <span data-ttu-id="012ee-189">tak</span><span class="sxs-lookup"><span data-stu-id="012ee-189">yes</span></span>      | <span data-ttu-id="012ee-190">Łączna liczba dopasowań, odnoszących się `skip` do i `take`</span><span class="sxs-lookup"><span data-stu-id="012ee-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="012ee-191">dane</span><span class="sxs-lookup"><span data-stu-id="012ee-191">data</span></span>      | <span data-ttu-id="012ee-192">tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="012ee-192">array of strings</span></span> | <span data-ttu-id="012ee-193">tak</span><span class="sxs-lookup"><span data-stu-id="012ee-193">yes</span></span>      | <span data-ttu-id="012ee-194">Identyfikatory pakietów dopasowane przez żądanie</span><span class="sxs-lookup"><span data-stu-id="012ee-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="012ee-195">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="012ee-195">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="012ee-196">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="012ee-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="012ee-197">Wylicz wersje pakietów</span><span class="sxs-lookup"><span data-stu-id="012ee-197">Enumerate package versions</span></span>

<span data-ttu-id="012ee-198">Po znalezieniu identyfikatora pakietu przy użyciu poprzedniego interfejsu API klient może użyć interfejsu API autouzupełniania, aby wyliczyć wersje pakietu dla podanego identyfikatora pakietu.</span><span class="sxs-lookup"><span data-stu-id="012ee-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="012ee-199">Wersja pakietu, która nie znajduje się na liście, nie zostanie wyświetlona w wynikach.</span><span class="sxs-lookup"><span data-stu-id="012ee-199">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="012ee-200">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="012ee-200">Request parameters</span></span>

<span data-ttu-id="012ee-201">Nazwa</span><span class="sxs-lookup"><span data-stu-id="012ee-201">Name</span></span>        | <span data-ttu-id="012ee-202">W</span><span class="sxs-lookup"><span data-stu-id="012ee-202">In</span></span>     | <span data-ttu-id="012ee-203">Typ</span><span class="sxs-lookup"><span data-stu-id="012ee-203">Type</span></span>    | <span data-ttu-id="012ee-204">Wymagane</span><span class="sxs-lookup"><span data-stu-id="012ee-204">Required</span></span> | <span data-ttu-id="012ee-205">Uwagi</span><span class="sxs-lookup"><span data-stu-id="012ee-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="012ee-206">identyfikator</span><span class="sxs-lookup"><span data-stu-id="012ee-206">id</span></span>          | <span data-ttu-id="012ee-207">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-207">URL</span></span>    | <span data-ttu-id="012ee-208">ciąg</span><span class="sxs-lookup"><span data-stu-id="012ee-208">string</span></span>  | <span data-ttu-id="012ee-209">tak</span><span class="sxs-lookup"><span data-stu-id="012ee-209">yes</span></span>      | <span data-ttu-id="012ee-210">Identyfikator pakietu, dla którego mają zostać pobrane wersje</span><span class="sxs-lookup"><span data-stu-id="012ee-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="012ee-211">wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="012ee-211">prerelease</span></span>  | <span data-ttu-id="012ee-212">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-212">URL</span></span>    | <span data-ttu-id="012ee-213">boolean</span><span class="sxs-lookup"><span data-stu-id="012ee-213">boolean</span></span> | <span data-ttu-id="012ee-214">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-214">no</span></span>       | <span data-ttu-id="012ee-215">`true` lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="012ee-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="012ee-216">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="012ee-216">semVerLevel</span></span> | <span data-ttu-id="012ee-217">Adres URL</span><span class="sxs-lookup"><span data-stu-id="012ee-217">URL</span></span>    | <span data-ttu-id="012ee-218">ciąg</span><span class="sxs-lookup"><span data-stu-id="012ee-218">string</span></span>  | <span data-ttu-id="012ee-219">nie</span><span class="sxs-lookup"><span data-stu-id="012ee-219">no</span></span>       | <span data-ttu-id="012ee-220">Ciąg wersji SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="012ee-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="012ee-221">Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.</span><span class="sxs-lookup"><span data-stu-id="012ee-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="012ee-222">`semVerLevel`Parametr zapytania jest używany do wybierania pakietów SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="012ee-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="012ee-223">Jeśli ten parametr zapytania jest wykluczony, zostaną zwrócone tylko wersje programu SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="012ee-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="012ee-224">Jeśli `semVerLevel=2.0.0` jest podany, zostaną zwrócone wersje SemVer 1.0.0 i SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="012ee-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="012ee-225">Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="012ee-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="012ee-226">Reakcja</span><span class="sxs-lookup"><span data-stu-id="012ee-226">Response</span></span>

<span data-ttu-id="012ee-227">Odpowiedź to dokument JSON zawierający wszystkie wersje pakietu podanego identyfikatora pakietu, filtrowanie według podanych parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="012ee-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="012ee-228">Główny obiekt JSON ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="012ee-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="012ee-229">Nazwa</span><span class="sxs-lookup"><span data-stu-id="012ee-229">Name</span></span>      | <span data-ttu-id="012ee-230">Typ</span><span class="sxs-lookup"><span data-stu-id="012ee-230">Type</span></span>             | <span data-ttu-id="012ee-231">Wymagane</span><span class="sxs-lookup"><span data-stu-id="012ee-231">Required</span></span> | <span data-ttu-id="012ee-232">Uwagi</span><span class="sxs-lookup"><span data-stu-id="012ee-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="012ee-233">dane</span><span class="sxs-lookup"><span data-stu-id="012ee-233">data</span></span>      | <span data-ttu-id="012ee-234">tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="012ee-234">array of strings</span></span> | <span data-ttu-id="012ee-235">tak</span><span class="sxs-lookup"><span data-stu-id="012ee-235">yes</span></span>      | <span data-ttu-id="012ee-236">Wersje pakietów dopasowane przez żądanie</span><span class="sxs-lookup"><span data-stu-id="012ee-236">The package versions matched by the request</span></span>

<span data-ttu-id="012ee-237">Wersje pakietu w `data` tablicy mogą zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata` ), jeśli `semVerLevel=2.0.0` są podane w ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="012ee-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="012ee-238">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="012ee-238">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="012ee-239">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="012ee-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
