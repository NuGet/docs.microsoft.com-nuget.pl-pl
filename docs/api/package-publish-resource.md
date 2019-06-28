---
title: Wypychanie i usuwanie, interfejs API programu NuGet
description: Usługa publikowania umożliwia klientom Opublikuj nowe pakiety i wyrejestrowanie lub usuń istniejące pakiety.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426721"
---
# <a name="push-and-delete"></a><span data-ttu-id="758ff-103">Wypychanie i usuwanie</span><span class="sxs-lookup"><span data-stu-id="758ff-103">Push and Delete</span></span>

<span data-ttu-id="758ff-104">Istnieje możliwość wypychania, Usuń (lub wyrejestrowanie, w zależności od implementacji serwera) i ponownie wystaw pakietów przy użyciu interfejsu API programu NuGet w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="758ff-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="758ff-105">Te operacje opierają się wylogować się z `PackagePublish` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="758ff-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="758ff-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="758ff-106">Versioning</span></span>

<span data-ttu-id="758ff-107">Następujące `@type` zostanie użyta wartość:</span><span class="sxs-lookup"><span data-stu-id="758ff-107">The following `@type` value is used:</span></span>

<span data-ttu-id="758ff-108">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="758ff-108">@type value</span></span>          | <span data-ttu-id="758ff-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="758ff-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="758ff-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="758ff-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="758ff-111">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="758ff-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="758ff-112">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="758ff-112">Base URL</span></span>

<span data-ttu-id="758ff-113">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `PackagePublish/2.0.0` zasobów w źródle pakietu [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="758ff-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="758ff-114">Poniższą dokumentacją używany jest adres URL usługi nuget.org.</span><span class="sxs-lookup"><span data-stu-id="758ff-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="758ff-115">Należy wziąć pod uwagę `https://www.nuget.org/api/v2/package` jako symbol zastępczy `@id` znaleziono wartości w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="758ff-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="758ff-116">Należy pamiętać, że ten adres URL wskazuje do tej samej lokalizacji, co starsze wypychania punktu końcowego V2, ponieważ protokół jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="758ff-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="758ff-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="758ff-117">HTTP methods</span></span>

<span data-ttu-id="758ff-118">`PUT`, `POST` i `DELETE` metod HTTP obsługiwanych przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="758ff-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="758ff-119">Dla metody, które są obsługiwane dla każdego punktu końcowego zobacz poniżej.</span><span class="sxs-lookup"><span data-stu-id="758ff-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="758ff-120">Wypychanie pakietu</span><span class="sxs-lookup"><span data-stu-id="758ff-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="758ff-121">ma adres nuget.org [dodatkowe wymagania](NuGet-Protocols.md) do interakcji z punktem końcowym wypychania.</span><span class="sxs-lookup"><span data-stu-id="758ff-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="758ff-122">nuget.org obsługuje wypychania nowych pakietów przy użyciu następujących interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="758ff-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="758ff-123">Jeśli pakiet o identyfikatorze podana i wersji już istnieje, nuget.org odrzuci wypychania.</span><span class="sxs-lookup"><span data-stu-id="758ff-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="758ff-124">Inne źródła pakietu może obsługiwać, zastępując istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="758ff-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="758ff-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="758ff-125">Request parameters</span></span>

<span data-ttu-id="758ff-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="758ff-126">Name</span></span>           | <span data-ttu-id="758ff-127">W</span><span class="sxs-lookup"><span data-stu-id="758ff-127">In</span></span>     | <span data-ttu-id="758ff-128">Typ</span><span class="sxs-lookup"><span data-stu-id="758ff-128">Type</span></span>   | <span data-ttu-id="758ff-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="758ff-129">Required</span></span> | <span data-ttu-id="758ff-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="758ff-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="758ff-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="758ff-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="758ff-132">nagłówek</span><span class="sxs-lookup"><span data-stu-id="758ff-132">Header</span></span> | <span data-ttu-id="758ff-133">string</span><span class="sxs-lookup"><span data-stu-id="758ff-133">string</span></span> | <span data-ttu-id="758ff-134">tak</span><span class="sxs-lookup"><span data-stu-id="758ff-134">yes</span></span>      | <span data-ttu-id="758ff-135">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="758ff-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="758ff-136">Klucz interfejsu API to nieprzezroczysty ciąg uzyskane ze źródła pakietu przez użytkownika i skonfigurowane do klienta.</span><span class="sxs-lookup"><span data-stu-id="758ff-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="758ff-137">Nie określonego ciągu formatu jest upoważnione, ale długość klucza interfejsu API nie może przekraczać rozmiaru uzasadnione wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="758ff-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="758ff-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="758ff-138">Request body</span></span>

<span data-ttu-id="758ff-139">Treść żądania musi występować w następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="758ff-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="758ff-140">Wieloczęściowych danych formularza</span><span class="sxs-lookup"><span data-stu-id="758ff-140">Multipart form data</span></span>

<span data-ttu-id="758ff-141">Nagłówek żądania `Content-Type` jest `multipart/form-data` i pierwszy element w treści żądania ma bajtów raw .nupkg wypychania.</span><span class="sxs-lookup"><span data-stu-id="758ff-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="758ff-142">Kolejne elementy treści wieloczęściowej wiadomości są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="758ff-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="758ff-143">Nazwa pliku lub innych nagłówków w wieloczęściowych elementów są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="758ff-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="758ff-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="758ff-144">Response</span></span>

<span data-ttu-id="758ff-145">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="758ff-145">Status Code</span></span> | <span data-ttu-id="758ff-146">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="758ff-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="758ff-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="758ff-147">201, 202</span></span>    | <span data-ttu-id="758ff-148">Pakiet został pomyślnie wypchnięto</span><span class="sxs-lookup"><span data-stu-id="758ff-148">The package was successfully pushed</span></span>
<span data-ttu-id="758ff-149">400</span><span class="sxs-lookup"><span data-stu-id="758ff-149">400</span></span>         | <span data-ttu-id="758ff-150">Podany pakiet jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="758ff-150">The provided package is invalid</span></span>
<span data-ttu-id="758ff-151">409</span><span class="sxs-lookup"><span data-stu-id="758ff-151">409</span></span>         | <span data-ttu-id="758ff-152">Pakiet o identyfikatorze podana i wersji już istnieje.</span><span class="sxs-lookup"><span data-stu-id="758ff-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="758ff-153">Implementacje Server różnią się na kod stanu powodzenia, które są zwracane, gdy pakiet zostanie pomyślnie przypisany.</span><span class="sxs-lookup"><span data-stu-id="758ff-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="758ff-154">Usuń pakiet</span><span class="sxs-lookup"><span data-stu-id="758ff-154">Delete a package</span></span>

<span data-ttu-id="758ff-155">nuget.org interpretuje żądanie usunięcia pakietu jako wiadomość "wyrejestrowanie".</span><span class="sxs-lookup"><span data-stu-id="758ff-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="758ff-156">Oznacza to, że pakiet jest nadal dostępna dla istniejących konsumentów pakietu, ale pakiet nie jest już wyświetlany w wynikach wyszukiwania lub w interfejsie sieci web.</span><span class="sxs-lookup"><span data-stu-id="758ff-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="758ff-157">Aby uzyskać więcej informacji na temat tej praktyką, zobacz [usunięte pakiety](../nuget-org/policies/deleting-packages.md) zasad.</span><span class="sxs-lookup"><span data-stu-id="758ff-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="758ff-158">Inne implementacje serwera są bezpłatne do interpretowania ten sygnał jako twardych delete, usuwanie nietrwałe lub wyrejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="758ff-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="758ff-159">Na przykład [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) obsługuje (tylko Obsługa starszych interfejsy API wersji 2 implementacji serwera), obsługujący żądanie jako unlist lub usuwania twardych na podstawie opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="758ff-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="758ff-160">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="758ff-160">Request parameters</span></span>

<span data-ttu-id="758ff-161">Nazwa</span><span class="sxs-lookup"><span data-stu-id="758ff-161">Name</span></span>           | <span data-ttu-id="758ff-162">W</span><span class="sxs-lookup"><span data-stu-id="758ff-162">In</span></span>     | <span data-ttu-id="758ff-163">Typ</span><span class="sxs-lookup"><span data-stu-id="758ff-163">Type</span></span>   | <span data-ttu-id="758ff-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="758ff-164">Required</span></span> | <span data-ttu-id="758ff-165">Uwagi</span><span class="sxs-lookup"><span data-stu-id="758ff-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="758ff-166">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="758ff-166">ID</span></span>             | <span data-ttu-id="758ff-167">Adres URL</span><span class="sxs-lookup"><span data-stu-id="758ff-167">URL</span></span>    | <span data-ttu-id="758ff-168">string</span><span class="sxs-lookup"><span data-stu-id="758ff-168">string</span></span> | <span data-ttu-id="758ff-169">tak</span><span class="sxs-lookup"><span data-stu-id="758ff-169">yes</span></span>      | <span data-ttu-id="758ff-170">Identyfikator pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="758ff-170">The ID of the package to delete</span></span>
<span data-ttu-id="758ff-171">WERSJA</span><span class="sxs-lookup"><span data-stu-id="758ff-171">VERSION</span></span>        | <span data-ttu-id="758ff-172">Adres URL</span><span class="sxs-lookup"><span data-stu-id="758ff-172">URL</span></span>    | <span data-ttu-id="758ff-173">string</span><span class="sxs-lookup"><span data-stu-id="758ff-173">string</span></span> | <span data-ttu-id="758ff-174">tak</span><span class="sxs-lookup"><span data-stu-id="758ff-174">yes</span></span>      | <span data-ttu-id="758ff-175">Wersja pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="758ff-175">The version of the package to delete</span></span>
<span data-ttu-id="758ff-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="758ff-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="758ff-177">nagłówek</span><span class="sxs-lookup"><span data-stu-id="758ff-177">Header</span></span> | <span data-ttu-id="758ff-178">string</span><span class="sxs-lookup"><span data-stu-id="758ff-178">string</span></span> | <span data-ttu-id="758ff-179">tak</span><span class="sxs-lookup"><span data-stu-id="758ff-179">yes</span></span>      | <span data-ttu-id="758ff-180">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="758ff-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="758ff-181">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="758ff-181">Response</span></span>

<span data-ttu-id="758ff-182">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="758ff-182">Status Code</span></span> | <span data-ttu-id="758ff-183">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="758ff-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="758ff-184">204</span><span class="sxs-lookup"><span data-stu-id="758ff-184">204</span></span>         | <span data-ttu-id="758ff-185">Pakiet został usunięty.</span><span class="sxs-lookup"><span data-stu-id="758ff-185">The package was deleted</span></span>
<span data-ttu-id="758ff-186">404</span><span class="sxs-lookup"><span data-stu-id="758ff-186">404</span></span>         | <span data-ttu-id="758ff-187">Nie pakietu z dostępnego `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="758ff-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="758ff-188">Wystaw ponownie pakiet</span><span class="sxs-lookup"><span data-stu-id="758ff-188">Relist a package</span></span>

<span data-ttu-id="758ff-189">Jeśli pakiet jest nieobecne na liście, jest możliwe ten pakiet ponownie widoczne w wynikach wyszukiwania przy użyciu punktu końcowego "Wystaw ponownie".</span><span class="sxs-lookup"><span data-stu-id="758ff-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="758ff-190">Ten punkt końcowy ma ten sam kształt co [Usuń (wyrejestrowanie) punktu końcowego](#delete-a-package) , ale używa `POST` protokołu HTTP zamiast metody `DELETE` metody.</span><span class="sxs-lookup"><span data-stu-id="758ff-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="758ff-191">Jeśli pakiet jest już na liście, żądanie nadal powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="758ff-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="758ff-192">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="758ff-192">Request parameters</span></span>

<span data-ttu-id="758ff-193">Nazwa</span><span class="sxs-lookup"><span data-stu-id="758ff-193">Name</span></span>           | <span data-ttu-id="758ff-194">W</span><span class="sxs-lookup"><span data-stu-id="758ff-194">In</span></span>     | <span data-ttu-id="758ff-195">Typ</span><span class="sxs-lookup"><span data-stu-id="758ff-195">Type</span></span>   | <span data-ttu-id="758ff-196">Wymagane</span><span class="sxs-lookup"><span data-stu-id="758ff-196">Required</span></span> | <span data-ttu-id="758ff-197">Uwagi</span><span class="sxs-lookup"><span data-stu-id="758ff-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="758ff-198">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="758ff-198">ID</span></span>             | <span data-ttu-id="758ff-199">Adres URL</span><span class="sxs-lookup"><span data-stu-id="758ff-199">URL</span></span>    | <span data-ttu-id="758ff-200">string</span><span class="sxs-lookup"><span data-stu-id="758ff-200">string</span></span> | <span data-ttu-id="758ff-201">tak</span><span class="sxs-lookup"><span data-stu-id="758ff-201">yes</span></span>      | <span data-ttu-id="758ff-202">Identyfikator pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="758ff-202">The ID of the package to relist</span></span>
<span data-ttu-id="758ff-203">WERSJA</span><span class="sxs-lookup"><span data-stu-id="758ff-203">VERSION</span></span>        | <span data-ttu-id="758ff-204">Adres URL</span><span class="sxs-lookup"><span data-stu-id="758ff-204">URL</span></span>    | <span data-ttu-id="758ff-205">string</span><span class="sxs-lookup"><span data-stu-id="758ff-205">string</span></span> | <span data-ttu-id="758ff-206">tak</span><span class="sxs-lookup"><span data-stu-id="758ff-206">yes</span></span>      | <span data-ttu-id="758ff-207">Wersja pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="758ff-207">The version of the package to relist</span></span>
<span data-ttu-id="758ff-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="758ff-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="758ff-209">nagłówek</span><span class="sxs-lookup"><span data-stu-id="758ff-209">Header</span></span> | <span data-ttu-id="758ff-210">string</span><span class="sxs-lookup"><span data-stu-id="758ff-210">string</span></span> | <span data-ttu-id="758ff-211">tak</span><span class="sxs-lookup"><span data-stu-id="758ff-211">yes</span></span>      | <span data-ttu-id="758ff-212">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="758ff-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="758ff-213">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="758ff-213">Response</span></span>

<span data-ttu-id="758ff-214">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="758ff-214">Status Code</span></span> | <span data-ttu-id="758ff-215">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="758ff-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="758ff-216">200</span><span class="sxs-lookup"><span data-stu-id="758ff-216">200</span></span>         | <span data-ttu-id="758ff-217">Pakiet znajduje się teraz</span><span class="sxs-lookup"><span data-stu-id="758ff-217">The package is now listed</span></span>
<span data-ttu-id="758ff-218">404</span><span class="sxs-lookup"><span data-stu-id="758ff-218">404</span></span>         | <span data-ttu-id="758ff-219">Nie pakietu z dostępnego `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="758ff-219">No package with the provided `ID` and `VERSION` exists</span></span>
