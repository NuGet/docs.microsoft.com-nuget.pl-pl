---
title: Zawartość pakietu, NuGet interfejsu API
description: Adres podstawowy pakiet jest prosty interfejs używany do pobierania samego pakietu.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a><span data-ttu-id="e8d46-103">Zawartość pakietu</span><span class="sxs-lookup"><span data-stu-id="e8d46-103">Package Content</span></span>

<span data-ttu-id="e8d46-104">Istnieje możliwość wygenerowania adresu URL do pobrania zawartości dowolnego pakietu (pliku .nupkg) przy użyciu interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="e8d46-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="e8d46-105">Zasób używany do pobierania zawartości pakietu jest `PackageBaseAddress` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e8d46-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="e8d46-106">Ten zasób umożliwia również odnajdywanie wszystkich wersji pakietu na liście lub nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="e8d46-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="e8d46-107">Ten zasób jest często określana jako albo "Pakiet podstawowy adres" lub "kontenera płaską".</span><span class="sxs-lookup"><span data-stu-id="e8d46-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="e8d46-108">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="e8d46-108">Versioning</span></span>

<span data-ttu-id="e8d46-109">Następujące `@type` jest używana wartość:</span><span class="sxs-lookup"><span data-stu-id="e8d46-109">The following `@type` value is used:</span></span>

<span data-ttu-id="e8d46-110">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="e8d46-110">@type value</span></span>              | <span data-ttu-id="e8d46-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8d46-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="e8d46-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="e8d46-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="e8d46-113">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="e8d46-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="e8d46-114">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="e8d46-114">Base URL</span></span>

<span data-ttu-id="e8d46-115">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość.</span><span class="sxs-lookup"><span data-stu-id="e8d46-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="e8d46-116">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="e8d46-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e8d46-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="e8d46-117">HTTP methods</span></span>

<span data-ttu-id="e8d46-118">Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="e8d46-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="e8d46-119">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="e8d46-119">Enumerate package versions</span></span>

<span data-ttu-id="e8d46-120">Jeśli klient zna identyfikator pakietu i chce dowiedzieć się, które pakietu wersji pakietu źródłowy jest dostępny, klient można konstruować przewidywalną adresu URL wyliczyć wszystkie wersje pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8d46-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="e8d46-121">Ta lista jest przeznaczona do można "listy katalogów" dla interfejsu API zawartości pakietów wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="e8d46-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="e8d46-122">Ta lista zawiera obie wersje pakietu listy i spoza niej.</span><span class="sxs-lookup"><span data-stu-id="e8d46-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="e8d46-123">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="e8d46-123">Request parameters</span></span>

<span data-ttu-id="e8d46-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8d46-124">Name</span></span>     | <span data-ttu-id="e8d46-125">W</span><span class="sxs-lookup"><span data-stu-id="e8d46-125">In</span></span>     | <span data-ttu-id="e8d46-126">Typ</span><span class="sxs-lookup"><span data-stu-id="e8d46-126">Type</span></span>    | <span data-ttu-id="e8d46-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8d46-127">Required</span></span> | <span data-ttu-id="e8d46-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8d46-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="e8d46-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="e8d46-129">LOWER_ID</span></span> | <span data-ttu-id="e8d46-130">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8d46-130">URL</span></span>    | <span data-ttu-id="e8d46-131">string</span><span class="sxs-lookup"><span data-stu-id="e8d46-131">string</span></span>  | <span data-ttu-id="e8d46-132">Tak</span><span class="sxs-lookup"><span data-stu-id="e8d46-132">yes</span></span>      | <span data-ttu-id="e8d46-133">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="e8d46-133">The package ID, lowercase</span></span>

<span data-ttu-id="e8d46-134">`LOWER_ID` Wartość jest małej, za pomocą reguł wdrożonych przez identyfikator żądanego pakietu. W sieci [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.</span><span class="sxs-lookup"><span data-stu-id="e8d46-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="e8d46-135">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8d46-135">Response</span></span>

<span data-ttu-id="e8d46-136">Jeśli źródło pakietów nie ma wersji identyfikatora podany pakiet, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="e8d46-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="e8d46-137">Jeśli źródło pakietu ma jedną lub kilka wersji, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="e8d46-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="e8d46-138">Treść odpowiedzi jest obiekt JSON z następującej właściwości:</span><span class="sxs-lookup"><span data-stu-id="e8d46-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="e8d46-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8d46-139">Name</span></span>     | <span data-ttu-id="e8d46-140">Typ</span><span class="sxs-lookup"><span data-stu-id="e8d46-140">Type</span></span>             | <span data-ttu-id="e8d46-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8d46-141">Required</span></span> | <span data-ttu-id="e8d46-142">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8d46-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="e8d46-143">wersje</span><span class="sxs-lookup"><span data-stu-id="e8d46-143">versions</span></span> | <span data-ttu-id="e8d46-144">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="e8d46-144">array of strings</span></span> | <span data-ttu-id="e8d46-145">Tak</span><span class="sxs-lookup"><span data-stu-id="e8d46-145">yes</span></span>      | <span data-ttu-id="e8d46-146">Pakiet dostępnych identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="e8d46-146">The package IDs available</span></span>

<span data-ttu-id="e8d46-147">Ciągi w `versions` tablicy są wszystkie małej, [znormalizowany ciągów wersji NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="e8d46-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e8d46-148">Ciągi wersji nie zawierają żadnych metadanych kompilacji programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="e8d46-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="e8d46-149">Celem jest, że ciągów wersji znaleziony w tej tablicy mogą być używane verbatim dla `LOWER_VERSION` tokeny znaleźć w następujących punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="e8d46-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e8d46-150">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="e8d46-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="e8d46-151">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8d46-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="e8d46-152">Pobierz zawartość pakietu (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="e8d46-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="e8d46-153">Jeśli klient zna identyfikator pakietu i wersję i chce pobrać zawartość pakietu, potrzebują tylko utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="e8d46-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="e8d46-154">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="e8d46-154">Request parameters</span></span>

<span data-ttu-id="e8d46-155">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8d46-155">Name</span></span>          | <span data-ttu-id="e8d46-156">W</span><span class="sxs-lookup"><span data-stu-id="e8d46-156">In</span></span>     | <span data-ttu-id="e8d46-157">Typ</span><span class="sxs-lookup"><span data-stu-id="e8d46-157">Type</span></span>   | <span data-ttu-id="e8d46-158">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8d46-158">Required</span></span> | <span data-ttu-id="e8d46-159">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8d46-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e8d46-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="e8d46-160">LOWER_ID</span></span>      | <span data-ttu-id="e8d46-161">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8d46-161">URL</span></span>    | <span data-ttu-id="e8d46-162">string</span><span class="sxs-lookup"><span data-stu-id="e8d46-162">string</span></span> | <span data-ttu-id="e8d46-163">Tak</span><span class="sxs-lookup"><span data-stu-id="e8d46-163">yes</span></span>      | <span data-ttu-id="e8d46-164">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="e8d46-164">The package ID, lowercase</span></span>
<span data-ttu-id="e8d46-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="e8d46-165">LOWER_VERSION</span></span> | <span data-ttu-id="e8d46-166">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8d46-166">URL</span></span>    | <span data-ttu-id="e8d46-167">string</span><span class="sxs-lookup"><span data-stu-id="e8d46-167">string</span></span> | <span data-ttu-id="e8d46-168">Tak</span><span class="sxs-lookup"><span data-stu-id="e8d46-168">yes</span></span>      | <span data-ttu-id="e8d46-169">Wersja pakietu znormalizowany i małej</span><span class="sxs-lookup"><span data-stu-id="e8d46-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="e8d46-170">Zarówno `LOWER_ID` i `LOWER_VERSION` są małej za pomocą reguł wdrożonych przez. W sieci [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.</span><span class="sxs-lookup"><span data-stu-id="e8d46-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="e8d46-171">`LOWER_VERSION` Jest wersja pakietu żądaną znormalizowany przy użyciu wersji narzędzia NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="e8d46-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e8d46-172">Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, która jest dozwolona przez specyfikację programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="e8d46-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="e8d46-173">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e8d46-173">Response body</span></span>

<span data-ttu-id="e8d46-174">Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="e8d46-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="e8d46-175">Treść odpowiedzi będzie samej zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8d46-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="e8d46-176">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="e8d46-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e8d46-177">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="e8d46-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="e8d46-178">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8d46-178">Sample response</span></span>

<span data-ttu-id="e8d46-179">Strumień binarny jest .nupkg dla Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="e8d46-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="e8d46-180">Pobierz manifest pakietu (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="e8d46-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="e8d46-181">Jeśli klient zna identyfikator pakietu i wersję i chce pobrać plik manifestu pakietu, potrzebują tylko utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="e8d46-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="e8d46-182">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="e8d46-182">Request parameters</span></span>

<span data-ttu-id="e8d46-183">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e8d46-183">Name</span></span>          | <span data-ttu-id="e8d46-184">W</span><span class="sxs-lookup"><span data-stu-id="e8d46-184">In</span></span>     | <span data-ttu-id="e8d46-185">Typ</span><span class="sxs-lookup"><span data-stu-id="e8d46-185">Type</span></span>    | <span data-ttu-id="e8d46-186">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e8d46-186">Required</span></span> | <span data-ttu-id="e8d46-187">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e8d46-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="e8d46-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="e8d46-188">LOWER_ID</span></span>      | <span data-ttu-id="e8d46-189">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8d46-189">URL</span></span>    | <span data-ttu-id="e8d46-190">string</span><span class="sxs-lookup"><span data-stu-id="e8d46-190">string</span></span>  | <span data-ttu-id="e8d46-191">Tak</span><span class="sxs-lookup"><span data-stu-id="e8d46-191">yes</span></span>      | <span data-ttu-id="e8d46-192">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="e8d46-192">The package ID, lowercase</span></span>
<span data-ttu-id="e8d46-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="e8d46-193">LOWER_VERSION</span></span> | <span data-ttu-id="e8d46-194">Adres URL</span><span class="sxs-lookup"><span data-stu-id="e8d46-194">URL</span></span>    | <span data-ttu-id="e8d46-195">integer</span><span class="sxs-lookup"><span data-stu-id="e8d46-195">integer</span></span> | <span data-ttu-id="e8d46-196">Tak</span><span class="sxs-lookup"><span data-stu-id="e8d46-196">yes</span></span>      | <span data-ttu-id="e8d46-197">Wersja pakietu znormalizowany i małej</span><span class="sxs-lookup"><span data-stu-id="e8d46-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="e8d46-198">Zarówno `LOWER_ID` i `LOWER_VERSION` są małej za pomocą reguł wdrożonych przez. W sieci [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.</span><span class="sxs-lookup"><span data-stu-id="e8d46-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="e8d46-199">`LOWER_VERSION` Jest wersja pakietu żądaną znormalizowany przy użyciu wersji narzędzia NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="e8d46-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e8d46-200">Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, która jest dozwolona przez specyfikację programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="e8d46-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="e8d46-201">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e8d46-201">Response body</span></span>

<span data-ttu-id="e8d46-202">Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="e8d46-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="e8d46-203">Treść odpowiedzi będzie manifestu pakietu, który jest .nuspec zawartych w odpowiedniej .nupkg.</span><span class="sxs-lookup"><span data-stu-id="e8d46-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="e8d46-204">.nuspec jest dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="e8d46-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="e8d46-205">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="e8d46-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e8d46-206">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="e8d46-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="e8d46-207">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="e8d46-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
