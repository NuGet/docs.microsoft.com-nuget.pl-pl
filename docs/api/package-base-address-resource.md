---
title: Zawartość pakietu, interfejs API NuGet
description: Adres podstawowy pakietu jest prostym interfejsem do pobierania samego pakietu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094120"
---
# <a name="package-content"></a><span data-ttu-id="88dd5-103">Zawartość pakietu</span><span class="sxs-lookup"><span data-stu-id="88dd5-103">Package Content</span></span>

<span data-ttu-id="88dd5-104">Możliwe jest wygenerowanie adresu URL w celu pobrania zawartości dowolnego pakietu (plik. nupkg) przy użyciu interfejsu API v3.</span><span class="sxs-lookup"><span data-stu-id="88dd5-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="88dd5-105">Zasób używany do pobierania zawartości pakietu jest `PackageBaseAddress` zasobem znalezionym w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="88dd5-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="88dd5-106">Ten zasób umożliwia również odnajdywanie wszystkich wersji pakietu na liście lub niewymienionej liście.</span><span class="sxs-lookup"><span data-stu-id="88dd5-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="88dd5-107">Ten zasób jest często określany jako "adres podstawowy pakietu" lub "kontener płaski".</span><span class="sxs-lookup"><span data-stu-id="88dd5-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="88dd5-108">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="88dd5-108">Versioning</span></span>

<span data-ttu-id="88dd5-109">Używana jest `@type` następująca wartość:</span><span class="sxs-lookup"><span data-stu-id="88dd5-109">The following `@type` value is used:</span></span>

<span data-ttu-id="88dd5-110">@typewartościami</span><span class="sxs-lookup"><span data-stu-id="88dd5-110">@type value</span></span>              | <span data-ttu-id="88dd5-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="88dd5-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="88dd5-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="88dd5-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="88dd5-113">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="88dd5-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="88dd5-114">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="88dd5-114">Base URL</span></span>

<span data-ttu-id="88dd5-115">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzoną z wymienioną powyżej wartością zasobu. `@type`</span><span class="sxs-lookup"><span data-stu-id="88dd5-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="88dd5-116">W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego `{@id}` adresu URL.</span><span class="sxs-lookup"><span data-stu-id="88dd5-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="88dd5-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="88dd5-117">HTTP methods</span></span>

<span data-ttu-id="88dd5-118">Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują `GET` metody `HEAD`http i.</span><span class="sxs-lookup"><span data-stu-id="88dd5-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="88dd5-119">Wylicz wersje pakietów</span><span class="sxs-lookup"><span data-stu-id="88dd5-119">Enumerate package versions</span></span>

<span data-ttu-id="88dd5-120">Jeśli Klient zna identyfikator pakietu i chce wykryć wersje pakietów dostępne dla źródła pakietu, klient może skonstruować przewidywalny adres URL w celu wyliczenia wszystkich wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="88dd5-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="88dd5-121">Ta lista ma być "listą katalogów" dla interfejsu API zawartości pakietu wymienionego poniżej.</span><span class="sxs-lookup"><span data-stu-id="88dd5-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="88dd5-122">Ta lista zawiera listę wersji pakietów wymienionych i nieznajdujących się na liście.</span><span class="sxs-lookup"><span data-stu-id="88dd5-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="88dd5-123">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="88dd5-123">Request parameters</span></span>

<span data-ttu-id="88dd5-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="88dd5-124">Name</span></span>     | <span data-ttu-id="88dd5-125">W</span><span class="sxs-lookup"><span data-stu-id="88dd5-125">In</span></span>     | <span data-ttu-id="88dd5-126">Typ</span><span class="sxs-lookup"><span data-stu-id="88dd5-126">Type</span></span>    | <span data-ttu-id="88dd5-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="88dd5-127">Required</span></span> | <span data-ttu-id="88dd5-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="88dd5-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="88dd5-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="88dd5-129">LOWER_ID</span></span> | <span data-ttu-id="88dd5-130">Adres URL</span><span class="sxs-lookup"><span data-stu-id="88dd5-130">URL</span></span>    | <span data-ttu-id="88dd5-131">string</span><span class="sxs-lookup"><span data-stu-id="88dd5-131">string</span></span>  | <span data-ttu-id="88dd5-132">tak</span><span class="sxs-lookup"><span data-stu-id="88dd5-132">yes</span></span>      | <span data-ttu-id="88dd5-133">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="88dd5-133">The package ID, lowercased</span></span>

<span data-ttu-id="88dd5-134">`LOWER_ID` Wartość jest pożądanym identyfikatorem pakietu małymi literami przy użyciu reguł zaimplementowane przez. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda sieci.</span><span class="sxs-lookup"><span data-stu-id="88dd5-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="88dd5-135">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="88dd5-135">Response</span></span>

<span data-ttu-id="88dd5-136">Jeśli źródło pakietu nie ma wersji podanego identyfikatora pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="88dd5-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="88dd5-137">Jeśli źródło pakietu ma co najmniej jedną wersję, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="88dd5-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="88dd5-138">Treść odpowiedzi jest obiektem JSON z następującą właściwością:</span><span class="sxs-lookup"><span data-stu-id="88dd5-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="88dd5-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="88dd5-139">Name</span></span>     | <span data-ttu-id="88dd5-140">Typ</span><span class="sxs-lookup"><span data-stu-id="88dd5-140">Type</span></span>             | <span data-ttu-id="88dd5-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="88dd5-141">Required</span></span> | <span data-ttu-id="88dd5-142">Uwagi</span><span class="sxs-lookup"><span data-stu-id="88dd5-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="88dd5-143">wersje</span><span class="sxs-lookup"><span data-stu-id="88dd5-143">versions</span></span> | <span data-ttu-id="88dd5-144">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="88dd5-144">array of strings</span></span> | <span data-ttu-id="88dd5-145">tak</span><span class="sxs-lookup"><span data-stu-id="88dd5-145">yes</span></span>      | <span data-ttu-id="88dd5-146">Dostępne wersje</span><span class="sxs-lookup"><span data-stu-id="88dd5-146">The versions available</span></span>

<span data-ttu-id="88dd5-147">Ciągi w `versions` tablicy to wszystkie małe litery, [znormalizowane ciągi wersji NuGet](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="88dd5-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="88dd5-148">Ciągi wersji nie zawierają żadnych metadanych kompilacji SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="88dd5-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="88dd5-149">Zamiarem jest to, że ciągi wersji Znalezione w tej tablicy mogą być używane Verbatim `LOWER_VERSION` dla tokenów znalezionych w następujących punktach końcowych.</span><span class="sxs-lookup"><span data-stu-id="88dd5-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="88dd5-150">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="88dd5-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="88dd5-151">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="88dd5-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="88dd5-152">Pobierz zawartość pakietu (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="88dd5-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="88dd5-153">Jeśli Klient zna identyfikator pakietu i wersję, a następnie chce pobrać zawartość pakietu, musi jedynie utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="88dd5-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="88dd5-154">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="88dd5-154">Request parameters</span></span>

<span data-ttu-id="88dd5-155">Nazwa</span><span class="sxs-lookup"><span data-stu-id="88dd5-155">Name</span></span>          | <span data-ttu-id="88dd5-156">W</span><span class="sxs-lookup"><span data-stu-id="88dd5-156">In</span></span>     | <span data-ttu-id="88dd5-157">Typ</span><span class="sxs-lookup"><span data-stu-id="88dd5-157">Type</span></span>   | <span data-ttu-id="88dd5-158">Wymagane</span><span class="sxs-lookup"><span data-stu-id="88dd5-158">Required</span></span> | <span data-ttu-id="88dd5-159">Uwagi</span><span class="sxs-lookup"><span data-stu-id="88dd5-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="88dd5-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="88dd5-160">LOWER_ID</span></span>      | <span data-ttu-id="88dd5-161">Adres URL</span><span class="sxs-lookup"><span data-stu-id="88dd5-161">URL</span></span>    | <span data-ttu-id="88dd5-162">string</span><span class="sxs-lookup"><span data-stu-id="88dd5-162">string</span></span> | <span data-ttu-id="88dd5-163">tak</span><span class="sxs-lookup"><span data-stu-id="88dd5-163">yes</span></span>      | <span data-ttu-id="88dd5-164">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="88dd5-164">The package ID, lowercase</span></span>
<span data-ttu-id="88dd5-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="88dd5-165">LOWER_VERSION</span></span> | <span data-ttu-id="88dd5-166">Adres URL</span><span class="sxs-lookup"><span data-stu-id="88dd5-166">URL</span></span>    | <span data-ttu-id="88dd5-167">string</span><span class="sxs-lookup"><span data-stu-id="88dd5-167">string</span></span> | <span data-ttu-id="88dd5-168">tak</span><span class="sxs-lookup"><span data-stu-id="88dd5-168">yes</span></span>      | <span data-ttu-id="88dd5-169">Wersja pakietu, znormalizowana i mała</span><span class="sxs-lookup"><span data-stu-id="88dd5-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="88dd5-170">Oba `LOWER_ID` i`LOWER_VERSION` są małymi literami przy użyciu reguł zaimplementowane przez. Sieć[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="88dd5-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="88dd5-171">Method.</span><span class="sxs-lookup"><span data-stu-id="88dd5-171">method.</span></span>

<span data-ttu-id="88dd5-172">Jest `LOWER_VERSION` to żądana wersja pakietu, znormalizowana przy użyciu [reguł normalizacji](../concepts/package-versioning.md#normalized-version-numbers)wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="88dd5-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="88dd5-173">Oznacza to, że w tym przypadku należy wykluczyć metadane kompilacji, które są dozwolone w specyfikacji SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="88dd5-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="88dd5-174">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88dd5-174">Response body</span></span>

<span data-ttu-id="88dd5-175">Jeśli pakiet istnieje w źródle pakietów, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="88dd5-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="88dd5-176">Treść odpowiedzi będzie samą zawartością pakietu.</span><span class="sxs-lookup"><span data-stu-id="88dd5-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="88dd5-177">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="88dd5-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="88dd5-178">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="88dd5-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="88dd5-179">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="88dd5-179">Sample response</span></span>

<span data-ttu-id="88dd5-180">Strumień binarny, który jest plikiem. nupkg dla Newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="88dd5-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="88dd5-181">Pobierz manifest pakietu (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="88dd5-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="88dd5-182">Jeśli Klient zna identyfikator pakietu i wersję i chce pobrać manifest pakietu, musi jedynie utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="88dd5-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="88dd5-183">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="88dd5-183">Request parameters</span></span>

<span data-ttu-id="88dd5-184">Nazwa</span><span class="sxs-lookup"><span data-stu-id="88dd5-184">Name</span></span>          | <span data-ttu-id="88dd5-185">W</span><span class="sxs-lookup"><span data-stu-id="88dd5-185">In</span></span>     | <span data-ttu-id="88dd5-186">Typ</span><span class="sxs-lookup"><span data-stu-id="88dd5-186">Type</span></span>   | <span data-ttu-id="88dd5-187">Wymagane</span><span class="sxs-lookup"><span data-stu-id="88dd5-187">Required</span></span> | <span data-ttu-id="88dd5-188">Uwagi</span><span class="sxs-lookup"><span data-stu-id="88dd5-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="88dd5-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="88dd5-189">LOWER_ID</span></span>      | <span data-ttu-id="88dd5-190">Adres URL</span><span class="sxs-lookup"><span data-stu-id="88dd5-190">URL</span></span>    | <span data-ttu-id="88dd5-191">string</span><span class="sxs-lookup"><span data-stu-id="88dd5-191">string</span></span> | <span data-ttu-id="88dd5-192">tak</span><span class="sxs-lookup"><span data-stu-id="88dd5-192">yes</span></span>      | <span data-ttu-id="88dd5-193">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="88dd5-193">The package ID, lowercase</span></span>
<span data-ttu-id="88dd5-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="88dd5-194">LOWER_VERSION</span></span> | <span data-ttu-id="88dd5-195">Adres URL</span><span class="sxs-lookup"><span data-stu-id="88dd5-195">URL</span></span>    | <span data-ttu-id="88dd5-196">string</span><span class="sxs-lookup"><span data-stu-id="88dd5-196">string</span></span> | <span data-ttu-id="88dd5-197">tak</span><span class="sxs-lookup"><span data-stu-id="88dd5-197">yes</span></span>      | <span data-ttu-id="88dd5-198">Wersja pakietu, znormalizowana i mała</span><span class="sxs-lookup"><span data-stu-id="88dd5-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="88dd5-199">Oba `LOWER_ID` i`LOWER_VERSION` są małymi literami przy użyciu reguł zaimplementowane przez. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda sieci.</span><span class="sxs-lookup"><span data-stu-id="88dd5-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="88dd5-200">Jest `LOWER_VERSION` to żądana wersja pakietu, znormalizowana przy użyciu [reguł normalizacji](../concepts/package-versioning.md#normalized-version-numbers)wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="88dd5-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="88dd5-201">Oznacza to, że w tym przypadku należy wykluczyć metadane kompilacji, które są dozwolone w specyfikacji SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="88dd5-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="88dd5-202">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88dd5-202">Response body</span></span>

<span data-ttu-id="88dd5-203">Jeśli pakiet istnieje w źródle pakietów, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="88dd5-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="88dd5-204">Treść odpowiedzi będzie manifestem pakietu, który jest nuspec zawarty w odpowiedniej. nupkg.</span><span class="sxs-lookup"><span data-stu-id="88dd5-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="88dd5-205">Plik. nuspec jest dokumentem XML.</span><span class="sxs-lookup"><span data-stu-id="88dd5-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="88dd5-206">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="88dd5-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="88dd5-207">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="88dd5-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="88dd5-208">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="88dd5-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
