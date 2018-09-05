---
title: Pakiet zawartości, interfejs API programu NuGet
description: Adres podstawowy pakiet jest prosty interfejs Pobieranie pakietu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547157"
---
# <a name="package-content"></a><span data-ttu-id="7ac90-103">Zawartość pakietu</span><span class="sxs-lookup"><span data-stu-id="7ac90-103">Package Content</span></span>

<span data-ttu-id="7ac90-104">Istnieje możliwość wygenerować adres URL, aby pobrać zawartość dowolnego pakiet (plik .nupkg) przy użyciu interfejsu API w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="7ac90-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="7ac90-105">Zasób, używany do pobierania zawartości pakietu jest `PackageBaseAddress` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7ac90-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="7ac90-106">Ten zasób umożliwia również odnajdywanie wszystkich wersji pakietu na liście lub nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="7ac90-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="7ac90-107">Ten zasób jest określany często jako albo "pakiet adres podstawowy" lub "container płaską".</span><span class="sxs-lookup"><span data-stu-id="7ac90-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="7ac90-108">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="7ac90-108">Versioning</span></span>

<span data-ttu-id="7ac90-109">Następujące `@type` zostanie użyta wartość:</span><span class="sxs-lookup"><span data-stu-id="7ac90-109">The following `@type` value is used:</span></span>

<span data-ttu-id="7ac90-110">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="7ac90-110">@type value</span></span>              | <span data-ttu-id="7ac90-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7ac90-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="7ac90-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="7ac90-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="7ac90-113">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="7ac90-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="7ac90-114">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="7ac90-114">Base URL</span></span>

<span data-ttu-id="7ac90-115">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość.</span><span class="sxs-lookup"><span data-stu-id="7ac90-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="7ac90-116">W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.</span><span class="sxs-lookup"><span data-stu-id="7ac90-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7ac90-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="7ac90-117">HTTP methods</span></span>

<span data-ttu-id="7ac90-118">Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="7ac90-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="7ac90-119">Wyliczenie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="7ac90-119">Enumerate package versions</span></span>

<span data-ttu-id="7ac90-120">Jeśli klient zna identyfikator pakietu i chce dowiedzieć się, które pakietu wersji pakietu źródłowy jest dostępny, klient można skonstruować przewidywalne adresu URL, można wyliczyć wszystkie wersje pakietu.</span><span class="sxs-lookup"><span data-stu-id="7ac90-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="7ac90-121">Ta lista jest przeznaczony jako "listing katalogu" dla interfejsu API zawartości pakietu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="7ac90-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="7ac90-122">Ta lista zawiera obie wersje pakietu listy i spoza niej.</span><span class="sxs-lookup"><span data-stu-id="7ac90-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="7ac90-123">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="7ac90-123">Request parameters</span></span>

<span data-ttu-id="7ac90-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7ac90-124">Name</span></span>     | <span data-ttu-id="7ac90-125">W</span><span class="sxs-lookup"><span data-stu-id="7ac90-125">In</span></span>     | <span data-ttu-id="7ac90-126">Typ</span><span class="sxs-lookup"><span data-stu-id="7ac90-126">Type</span></span>    | <span data-ttu-id="7ac90-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7ac90-127">Required</span></span> | <span data-ttu-id="7ac90-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7ac90-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="7ac90-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7ac90-129">LOWER_ID</span></span> | <span data-ttu-id="7ac90-130">Adres URL</span><span class="sxs-lookup"><span data-stu-id="7ac90-130">URL</span></span>    | <span data-ttu-id="7ac90-131">string</span><span class="sxs-lookup"><span data-stu-id="7ac90-131">string</span></span>  | <span data-ttu-id="7ac90-132">Tak</span><span class="sxs-lookup"><span data-stu-id="7ac90-132">yes</span></span>      | <span data-ttu-id="7ac90-133">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="7ac90-133">The package ID, lowercase</span></span>

<span data-ttu-id="7ac90-134">`LOWER_ID` Wartość jest pisany małymi literami, za pomocą reguł wdrożonych przez identyfikator żądanego pakietu. NET firmy [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.</span><span class="sxs-lookup"><span data-stu-id="7ac90-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="7ac90-135">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="7ac90-135">Response</span></span>

<span data-ttu-id="7ac90-136">Jeśli źródło pakietu nie ma wersji identyfikatora podanego pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="7ac90-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="7ac90-137">Jeśli źródło pakietu zawiera jedną lub kilka wersji, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="7ac90-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="7ac90-138">Treść odpowiedzi jest obiekt JSON z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="7ac90-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="7ac90-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7ac90-139">Name</span></span>     | <span data-ttu-id="7ac90-140">Typ</span><span class="sxs-lookup"><span data-stu-id="7ac90-140">Type</span></span>             | <span data-ttu-id="7ac90-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7ac90-141">Required</span></span> | <span data-ttu-id="7ac90-142">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7ac90-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="7ac90-143">wersje</span><span class="sxs-lookup"><span data-stu-id="7ac90-143">versions</span></span> | <span data-ttu-id="7ac90-144">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="7ac90-144">array of strings</span></span> | <span data-ttu-id="7ac90-145">Tak</span><span class="sxs-lookup"><span data-stu-id="7ac90-145">yes</span></span>      | <span data-ttu-id="7ac90-146">Pakiet dostępnych identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="7ac90-146">The package IDs available</span></span>

<span data-ttu-id="7ac90-147">Ciągi w `versions` tablicy są wszystkie pisany małymi literami, [znormalizować ciągi wersji NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7ac90-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7ac90-148">Ciągi wersji nie zawierają żadnych metadanych kompilacji SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7ac90-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="7ac90-149">Celem jest, że ciągi wersji w tej tablicy mogą być używane verbatim dla `LOWER_VERSION` tokenów znaleźć w następujących punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="7ac90-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7ac90-150">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="7ac90-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="7ac90-151">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="7ac90-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="7ac90-152">Pobierz zawartość pakietu (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="7ac90-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="7ac90-153">Jeśli klient zna identyfikator pakietu i wersję i chce pobrać zawartość pakietu, wystarczy utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="7ac90-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="7ac90-154">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="7ac90-154">Request parameters</span></span>

<span data-ttu-id="7ac90-155">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7ac90-155">Name</span></span>          | <span data-ttu-id="7ac90-156">W</span><span class="sxs-lookup"><span data-stu-id="7ac90-156">In</span></span>     | <span data-ttu-id="7ac90-157">Typ</span><span class="sxs-lookup"><span data-stu-id="7ac90-157">Type</span></span>   | <span data-ttu-id="7ac90-158">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7ac90-158">Required</span></span> | <span data-ttu-id="7ac90-159">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7ac90-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7ac90-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7ac90-160">LOWER_ID</span></span>      | <span data-ttu-id="7ac90-161">Adres URL</span><span class="sxs-lookup"><span data-stu-id="7ac90-161">URL</span></span>    | <span data-ttu-id="7ac90-162">string</span><span class="sxs-lookup"><span data-stu-id="7ac90-162">string</span></span> | <span data-ttu-id="7ac90-163">Tak</span><span class="sxs-lookup"><span data-stu-id="7ac90-163">yes</span></span>      | <span data-ttu-id="7ac90-164">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="7ac90-164">The package ID, lowercase</span></span>
<span data-ttu-id="7ac90-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="7ac90-165">LOWER_VERSION</span></span> | <span data-ttu-id="7ac90-166">Adres URL</span><span class="sxs-lookup"><span data-stu-id="7ac90-166">URL</span></span>    | <span data-ttu-id="7ac90-167">string</span><span class="sxs-lookup"><span data-stu-id="7ac90-167">string</span></span> | <span data-ttu-id="7ac90-168">Tak</span><span class="sxs-lookup"><span data-stu-id="7ac90-168">yes</span></span>      | <span data-ttu-id="7ac90-169">Wersja pakietu znormalizowane i pisany małymi literami</span><span class="sxs-lookup"><span data-stu-id="7ac90-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="7ac90-170">Zarówno `LOWER_ID` i `LOWER_VERSION` jest pisany małymi literami za pomocą reguł wdrożonych przez. NET firmy [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="7ac90-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="7ac90-171">Metoda.</span><span class="sxs-lookup"><span data-stu-id="7ac90-171">method.</span></span>

<span data-ttu-id="7ac90-172">`LOWER_VERSION` Jest wersja pakietu żądaną znormalizować przy użyciu wersji NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7ac90-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7ac90-173">Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, który jest dozwolony przez specyfikację SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7ac90-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="7ac90-174">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7ac90-174">Response body</span></span>

<span data-ttu-id="7ac90-175">Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="7ac90-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="7ac90-176">Treść odpowiedzi będą samej zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="7ac90-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="7ac90-177">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="7ac90-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7ac90-178">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="7ac90-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="7ac90-179">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="7ac90-179">Sample response</span></span>

<span data-ttu-id="7ac90-180">Strumień danych binarnych jest .nupkg dla Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="7ac90-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="7ac90-181">Pobierz manifest pakietu (.nuspec)</span><span class="sxs-lookup"><span data-stu-id="7ac90-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="7ac90-182">Jeśli klient zna identyfikator pakietu i wersję i chce pobrać manifestu pakietu, wystarczy utworzyć następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="7ac90-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="7ac90-183">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="7ac90-183">Request parameters</span></span>

<span data-ttu-id="7ac90-184">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7ac90-184">Name</span></span>          | <span data-ttu-id="7ac90-185">W</span><span class="sxs-lookup"><span data-stu-id="7ac90-185">In</span></span>     | <span data-ttu-id="7ac90-186">Typ</span><span class="sxs-lookup"><span data-stu-id="7ac90-186">Type</span></span>    | <span data-ttu-id="7ac90-187">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7ac90-187">Required</span></span> | <span data-ttu-id="7ac90-188">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7ac90-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="7ac90-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7ac90-189">LOWER_ID</span></span>      | <span data-ttu-id="7ac90-190">Adres URL</span><span class="sxs-lookup"><span data-stu-id="7ac90-190">URL</span></span>    | <span data-ttu-id="7ac90-191">string</span><span class="sxs-lookup"><span data-stu-id="7ac90-191">string</span></span>  | <span data-ttu-id="7ac90-192">Tak</span><span class="sxs-lookup"><span data-stu-id="7ac90-192">yes</span></span>      | <span data-ttu-id="7ac90-193">Identyfikator pakietu, małe litery</span><span class="sxs-lookup"><span data-stu-id="7ac90-193">The package ID, lowercase</span></span>
<span data-ttu-id="7ac90-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="7ac90-194">LOWER_VERSION</span></span> | <span data-ttu-id="7ac90-195">Adres URL</span><span class="sxs-lookup"><span data-stu-id="7ac90-195">URL</span></span>    | <span data-ttu-id="7ac90-196">integer</span><span class="sxs-lookup"><span data-stu-id="7ac90-196">integer</span></span> | <span data-ttu-id="7ac90-197">Tak</span><span class="sxs-lookup"><span data-stu-id="7ac90-197">yes</span></span>      | <span data-ttu-id="7ac90-198">Wersja pakietu znormalizowane i pisany małymi literami</span><span class="sxs-lookup"><span data-stu-id="7ac90-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="7ac90-199">Zarówno `LOWER_ID` i `LOWER_VERSION` jest pisany małymi literami za pomocą reguł wdrożonych przez. NET firmy [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.</span><span class="sxs-lookup"><span data-stu-id="7ac90-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="7ac90-200">`LOWER_VERSION` Jest wersja pakietu żądaną znormalizować przy użyciu wersji NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7ac90-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7ac90-201">Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, który jest dozwolony przez specyfikację SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7ac90-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="7ac90-202">Treść odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7ac90-202">Response body</span></span>

<span data-ttu-id="7ac90-203">Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="7ac90-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="7ac90-204">Treść odpowiedzi będą manifestu pakietu, czyli .nuspec zawartych w odpowiedniej .nupkg.</span><span class="sxs-lookup"><span data-stu-id="7ac90-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="7ac90-205">.nuspec jest dokument XML.</span><span class="sxs-lookup"><span data-stu-id="7ac90-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="7ac90-206">Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.</span><span class="sxs-lookup"><span data-stu-id="7ac90-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7ac90-207">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="7ac90-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="7ac90-208">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="7ac90-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
