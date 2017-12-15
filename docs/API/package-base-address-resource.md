---
title: "Pakiet zawartości, NuGet interfejsu API | Dokumentacja firmy Microsoft"
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
ms.assetid: ec68b5d1-a684-4995-b1a6-6210dbb24875
description: "Adres podstawowy pakiet jest prosty interfejs używany do pobierania samego pakietu."
keywords: "Płaskie NuGet kontenera, adres podstawowy pakietu NuGet, NuGet nupkg interfejsu API, wersje pakietu NuGet interfejsu API, interfejsu API NuGet nieznajdujące się na liście pakietów, nuspec pobierania NuGet interfejsu API"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 756001ff7376a8dd8d66bd2136408e90e6a85d19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="package-content"></a><span data-ttu-id="18f5e-104">Zawartość pakietu</span><span class="sxs-lookup"><span data-stu-id="18f5e-104">Package Content</span></span>

<span data-ttu-id="18f5e-105">Istnieje możliwość wygenerowania adresu URL do pobrania zawartości dowolnego pakietu (pliku .nupkg) przy użyciu interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="18f5e-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="18f5e-106">Zasób używany do pobierania zawartości pakietu jest `PackageBaseAddress` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="18f5e-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="18f5e-107">Ten zasób umożliwia również odnajdywanie wszystkich wersji pakietu na liście lub nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="18f5e-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="18f5e-108">Ten zasób jest często określana jako albo "Pakiet podstawowy adres" lub "kontenera płaską".</span><span class="sxs-lookup"><span data-stu-id="18f5e-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="18f5e-109">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="18f5e-109">Versioning</span></span>

<span data-ttu-id="18f5e-110">Następujące `@type` jest używana wartość:</span><span class="sxs-lookup"><span data-stu-id="18f5e-110">The following `@type` value is used:</span></span>

<span data-ttu-id="18f5e-111">@typewartość</span><span class="sxs-lookup"><span data-stu-id="18f5e-111">@type value</span></span>              | <span data-ttu-id="18f5e-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="18f5e-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="18f5e-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="18f5e-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="18f5e-114">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="18f5e-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="18f5e-115">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="18f5e-115">Base URL</span></span>

<span data-ttu-id="18f5e-116">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość.</span><span class="sxs-lookup"><span data-stu-id="18f5e-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="18f5e-117">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="18f5e-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="18f5e-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="18f5e-118">HTTP methods</span></span>

<span data-ttu-id="18f5e-119">Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="18f5e-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="18f5e-120">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="18f5e-120">Enumerate package versions</span></span>

<span data-ttu-id="18f5e-121">Jeśli klient zna identyfikator pakietu i chce dowiedzieć się, które pakietu wersji pakietu źródłowy jest dostępny, klient można konstruować przewidywalną adresu URL wyliczyć wszystkie wersje pakietu.</span><span class="sxs-lookup"><span data-stu-id="18f5e-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="18f5e-122">Ta lista jest przeznaczona do można "listy katalogów" dla interfejsu API zawartości pakietów wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="18f5e-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="18f5e-123">Ta lista zawiera obie wersje pakietu listy i spoza niej.</span><span class="sxs-lookup"><span data-stu-id="18f5e-123">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="18f5e-124">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="18f5e-124">Request parameters</span></span>

<span data-ttu-id="18f5e-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="18f5e-125">Name</span></span>     | <span data-ttu-id="18f5e-126">W</span><span class="sxs-lookup"><span data-stu-id="18f5e-126">In</span></span>     | <span data-ttu-id="18f5e-127">Typ</span><span class="sxs-lookup"><span data-stu-id="18f5e-127">Type</span></span>    | <span data-ttu-id="18f5e-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="18f5e-128">Required</span></span> | <span data-ttu-id="18f5e-129">Uwagi</span><span class="sxs-lookup"><span data-stu-id="18f5e-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="18f5e-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="18f5e-130">LOWER_ID</span></span> | <span data-ttu-id="18f5e-131">Adres URL</span><span class="sxs-lookup"><span data-stu-id="18f5e-131">URL</span></span>    | <span data-ttu-id="18f5e-132">string</span><span class="sxs-lookup"><span data-stu-id="18f5e-132">string</span></span>  | <span data-ttu-id="18f5e-133">Tak</span><span class="sxs-lookup"><span data-stu-id="18f5e-133">yes</span></span>      | <span data-ttu-id="18f5e-134">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="18f5e-134">The package ID, lowercase</span></span>

<span data-ttu-id="18f5e-135">`LOWER_ID` Wartość jest małej, za pomocą reguł wdrożonych przez identyfikator żądanego pakietu. W sieci [ `System.String.ToLowerInvariant()` ](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="18f5e-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) method.</span></span>

### <a name="response"></a><span data-ttu-id="18f5e-136">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="18f5e-136">Response</span></span>

<span data-ttu-id="18f5e-137">Jeśli źródło pakietów nie ma wersji identyfikatora podany pakiet, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="18f5e-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="18f5e-138">Jeśli źródło pakietu ma jedną lub kilka wersji, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="18f5e-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="18f5e-139">Treść odpowiedzi jest obiekt JSON z następującej właściwości:</span><span class="sxs-lookup"><span data-stu-id="18f5e-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="18f5e-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="18f5e-140">Name</span></span>     | <span data-ttu-id="18f5e-141">Typ</span><span class="sxs-lookup"><span data-stu-id="18f5e-141">Type</span></span>             | <span data-ttu-id="18f5e-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="18f5e-142">Required</span></span> | <span data-ttu-id="18f5e-143">Uwagi</span><span class="sxs-lookup"><span data-stu-id="18f5e-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="18f5e-144">wersje</span><span class="sxs-lookup"><span data-stu-id="18f5e-144">versions</span></span> | <span data-ttu-id="18f5e-145">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="18f5e-145">array of strings</span></span> | <span data-ttu-id="18f5e-146">Tak</span><span class="sxs-lookup"><span data-stu-id="18f5e-146">yes</span></span>      | <span data-ttu-id="18f5e-147">Pakiet dostępnych identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="18f5e-147">The package IDs available</span></span>

<span data-ttu-id="18f5e-148">Ciągi w `versions` tablicy są wszystkie małej, [znormalizowany ciągów wersji NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="18f5e-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="18f5e-149">Ciągi wersji nie zawierają żadnych metadanych kompilacji programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="18f5e-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="18f5e-150">Celem jest, że ciągów wersji znaleziony w tej tablicy mogą być używane verbatim dla `LOWER_VERSION` tokeny znaleźć w następujących punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="18f5e-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="18f5e-151">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="18f5e-151">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="18f5e-152">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="18f5e-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="18f5e-153">Pobierz zawartość pakietu (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="18f5e-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="18f5e-154">Jeśli klient zna identyfikator pakietu i wersję i chce pobrać zawartość pakietu, potrzebują tylko utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="18f5e-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="18f5e-155">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="18f5e-155">Request parameters</span></span>

<span data-ttu-id="18f5e-156">Nazwa</span><span class="sxs-lookup"><span data-stu-id="18f5e-156">Name</span></span>          | <span data-ttu-id="18f5e-157">W</span><span class="sxs-lookup"><span data-stu-id="18f5e-157">In</span></span>     | <span data-ttu-id="18f5e-158">Typ</span><span class="sxs-lookup"><span data-stu-id="18f5e-158">Type</span></span>   | <span data-ttu-id="18f5e-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="18f5e-159">Required</span></span> | <span data-ttu-id="18f5e-160">Uwagi</span><span class="sxs-lookup"><span data-stu-id="18f5e-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="18f5e-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="18f5e-161">LOWER_ID</span></span>      | <span data-ttu-id="18f5e-162">Adres URL</span><span class="sxs-lookup"><span data-stu-id="18f5e-162">URL</span></span>    | <span data-ttu-id="18f5e-163">string</span><span class="sxs-lookup"><span data-stu-id="18f5e-163">string</span></span> | <span data-ttu-id="18f5e-164">Tak</span><span class="sxs-lookup"><span data-stu-id="18f5e-164">yes</span></span>      | <span data-ttu-id="18f5e-165">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="18f5e-165">The package ID, lowercase</span></span>
<span data-ttu-id="18f5e-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="18f5e-166">LOWER_VERSION</span></span> | <span data-ttu-id="18f5e-167">Adres URL</span><span class="sxs-lookup"><span data-stu-id="18f5e-167">URL</span></span>    | <span data-ttu-id="18f5e-168">string</span><span class="sxs-lookup"><span data-stu-id="18f5e-168">string</span></span> | <span data-ttu-id="18f5e-169">Tak</span><span class="sxs-lookup"><span data-stu-id="18f5e-169">yes</span></span>      | <span data-ttu-id="18f5e-170">Wersja pakietu znormalizowany i małej</span><span class="sxs-lookup"><span data-stu-id="18f5e-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="18f5e-171">Zarówno `LOWER_ID` i `LOWER_VERSION` są małej za pomocą reguł wdrożonych przez. W sieci [ `System.String.ToLowerInvariant()` ](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="18f5e-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) method.</span></span>

<span data-ttu-id="18f5e-172">`LOWER_VERSION` Jest wersja pakietu żądaną znormalizowany przy użyciu wersji narzędzia NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="18f5e-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="18f5e-173">Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, która jest dozwolona przez specyfikację programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="18f5e-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="18f5e-174">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="18f5e-174">Response body</span></span>

<span data-ttu-id="18f5e-175">Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="18f5e-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="18f5e-176">Treść odpowiedzi będzie samej zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="18f5e-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="18f5e-177">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="18f5e-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="18f5e-178">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="18f5e-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="18f5e-179">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="18f5e-179">Sample response</span></span>

<span data-ttu-id="18f5e-180">Strumień binarny jest .nupkg dla Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="18f5e-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="18f5e-181">Pobierz manifest pakietu (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="18f5e-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="18f5e-182">Jeśli klient zna identyfikator pakietu i wersję i chce pobrać plik manifestu pakietu, potrzebują tylko utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="18f5e-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="18f5e-183">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="18f5e-183">Request parameters</span></span>

<span data-ttu-id="18f5e-184">Nazwa</span><span class="sxs-lookup"><span data-stu-id="18f5e-184">Name</span></span>          | <span data-ttu-id="18f5e-185">W</span><span class="sxs-lookup"><span data-stu-id="18f5e-185">In</span></span>     | <span data-ttu-id="18f5e-186">Typ</span><span class="sxs-lookup"><span data-stu-id="18f5e-186">Type</span></span>    | <span data-ttu-id="18f5e-187">Wymagane</span><span class="sxs-lookup"><span data-stu-id="18f5e-187">Required</span></span> | <span data-ttu-id="18f5e-188">Uwagi</span><span class="sxs-lookup"><span data-stu-id="18f5e-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="18f5e-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="18f5e-189">LOWER_ID</span></span>      | <span data-ttu-id="18f5e-190">Adres URL</span><span class="sxs-lookup"><span data-stu-id="18f5e-190">URL</span></span>    | <span data-ttu-id="18f5e-191">string</span><span class="sxs-lookup"><span data-stu-id="18f5e-191">string</span></span>  | <span data-ttu-id="18f5e-192">Tak</span><span class="sxs-lookup"><span data-stu-id="18f5e-192">yes</span></span>      | <span data-ttu-id="18f5e-193">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="18f5e-193">The package ID, lowercase</span></span>
<span data-ttu-id="18f5e-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="18f5e-194">LOWER_VERSION</span></span> | <span data-ttu-id="18f5e-195">Adres URL</span><span class="sxs-lookup"><span data-stu-id="18f5e-195">URL</span></span>    | <span data-ttu-id="18f5e-196">integer</span><span class="sxs-lookup"><span data-stu-id="18f5e-196">integer</span></span> | <span data-ttu-id="18f5e-197">Tak</span><span class="sxs-lookup"><span data-stu-id="18f5e-197">yes</span></span>      | <span data-ttu-id="18f5e-198">Wersja pakietu znormalizowany i małej</span><span class="sxs-lookup"><span data-stu-id="18f5e-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="18f5e-199">Zarówno `LOWER_ID` i `LOWER_VERSION` są małej za pomocą reguł wdrożonych przez. W sieci [ `System.String.ToLowerInvariant()` ](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="18f5e-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx) method.</span></span>

<span data-ttu-id="18f5e-200">`LOWER_VERSION` Jest wersja pakietu żądaną znormalizowany przy użyciu wersji narzędzia NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="18f5e-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="18f5e-201">Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, która jest dozwolona przez specyfikację programu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="18f5e-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="18f5e-202">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="18f5e-202">Response body</span></span>

<span data-ttu-id="18f5e-203">Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="18f5e-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="18f5e-204">Treść odpowiedzi będzie manifestu pakietu, który jest .nuspec zawartych w odpowiedniej .nupkg.</span><span class="sxs-lookup"><span data-stu-id="18f5e-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="18f5e-205">.nuspec jest dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="18f5e-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="18f5e-206">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="18f5e-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="18f5e-207">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="18f5e-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="18f5e-208">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="18f5e-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
