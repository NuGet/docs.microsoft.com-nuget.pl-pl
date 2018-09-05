---
title: Wypychanie i usuwanie, interfejs API programu NuGet
description: Usługa publikowania umożliwia klientom Opublikuj nowe pakiety i wyrejestrowanie lub usuń istniejące pakiety.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547524"
---
# <a name="push-and-delete"></a><span data-ttu-id="b0b42-103">Wypychanie i usuwanie</span><span class="sxs-lookup"><span data-stu-id="b0b42-103">Push and Delete</span></span>

<span data-ttu-id="b0b42-104">Istnieje możliwość wypychania, Usuń (lub wyrejestrowanie, w zależności od implementacji serwera) i ponownie wystaw pakietów przy użyciu interfejsu API programu NuGet w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="b0b42-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="b0b42-105">Te operacje opierają się wylogować się z `PackagePublish` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b0b42-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b0b42-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="b0b42-106">Versioning</span></span>

<span data-ttu-id="b0b42-107">Następujące `@type` zostanie użyta wartość:</span><span class="sxs-lookup"><span data-stu-id="b0b42-107">The following `@type` value is used:</span></span>

<span data-ttu-id="b0b42-108">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="b0b42-108">@type value</span></span>          | <span data-ttu-id="b0b42-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b0b42-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="b0b42-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="b0b42-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="b0b42-111">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="b0b42-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="b0b42-112">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="b0b42-112">Base URL</span></span>

<span data-ttu-id="b0b42-113">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `PackagePublish/2.0.0` zasobów w źródle pakietu [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b0b42-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="b0b42-114">Poniższą dokumentacją używany jest adres URL usługi nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b0b42-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="b0b42-115">Należy wziąć pod uwagę `https://www.nuget.org/api/v2/package` jako symbol zastępczy `@id` znaleziono wartości w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="b0b42-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="b0b42-116">Należy pamiętać, że ten adres URL wskazuje do tej samej lokalizacji, co starsze wypychania punktu końcowego V2, ponieważ protokół jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="b0b42-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b0b42-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="b0b42-117">HTTP methods</span></span>

<span data-ttu-id="b0b42-118">`PUT`, `POST` i `DELETE` metod HTTP obsługiwanych przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="b0b42-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="b0b42-119">Dla metody, które są obsługiwane dla każdego punktu końcowego zobacz poniżej.</span><span class="sxs-lookup"><span data-stu-id="b0b42-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="b0b42-120">Wypychanie pakietu</span><span class="sxs-lookup"><span data-stu-id="b0b42-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="b0b42-121">ma adres nuget.org [dodatkowe wymagania](NuGet-Protocols.md) do interakcji z punktem końcowym wypychania.</span><span class="sxs-lookup"><span data-stu-id="b0b42-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="b0b42-122">nuget.org obsługuje wypychania nowych pakietów przy użyciu następujących interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b0b42-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="b0b42-123">Jeśli pakiet o identyfikatorze podana i wersji już istnieje, nuget.org odrzuci wypychania.</span><span class="sxs-lookup"><span data-stu-id="b0b42-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="b0b42-124">Inne źródła pakietu może obsługiwać, zastępując istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="b0b42-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="b0b42-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="b0b42-125">Request parameters</span></span>

<span data-ttu-id="b0b42-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b0b42-126">Name</span></span>           | <span data-ttu-id="b0b42-127">W</span><span class="sxs-lookup"><span data-stu-id="b0b42-127">In</span></span>     | <span data-ttu-id="b0b42-128">Typ</span><span class="sxs-lookup"><span data-stu-id="b0b42-128">Type</span></span>   | <span data-ttu-id="b0b42-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b0b42-129">Required</span></span> | <span data-ttu-id="b0b42-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b0b42-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b0b42-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b0b42-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b0b42-132">nagłówek</span><span class="sxs-lookup"><span data-stu-id="b0b42-132">Header</span></span> | <span data-ttu-id="b0b42-133">string</span><span class="sxs-lookup"><span data-stu-id="b0b42-133">string</span></span> | <span data-ttu-id="b0b42-134">Tak</span><span class="sxs-lookup"><span data-stu-id="b0b42-134">yes</span></span>      | <span data-ttu-id="b0b42-135">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b0b42-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="b0b42-136">Klucz interfejsu API to nieprzezroczysty ciąg uzyskane ze źródła pakietu przez użytkownika i skonfigurowane do klienta.</span><span class="sxs-lookup"><span data-stu-id="b0b42-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="b0b42-137">Nie określonego ciągu formatu jest upoważnione, ale długość klucza interfejsu API nie może przekraczać rozmiaru uzasadnione wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="b0b42-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="b0b42-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b0b42-138">Request body</span></span>

<span data-ttu-id="b0b42-139">Treść żądania musi występować w następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="b0b42-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="b0b42-140">Wieloczęściowych danych formularza</span><span class="sxs-lookup"><span data-stu-id="b0b42-140">Multipart form data</span></span>

<span data-ttu-id="b0b42-141">Nagłówek żądania `Content-Type` jest `multipart/form-data` i pierwszy element w treści żądania ma bajtów raw .nupkg wypychania.</span><span class="sxs-lookup"><span data-stu-id="b0b42-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="b0b42-142">Kolejne elementy treści wieloczęściowej wiadomości są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="b0b42-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="b0b42-143">Nazwa pliku lub innych nagłówków w wieloczęściowych elementów są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="b0b42-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="b0b42-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="b0b42-144">Response</span></span>

<span data-ttu-id="b0b42-145">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="b0b42-145">Status Code</span></span> | <span data-ttu-id="b0b42-146">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="b0b42-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="b0b42-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="b0b42-147">201, 202</span></span>    | <span data-ttu-id="b0b42-148">Pakiet został pomyślnie wypchnięto</span><span class="sxs-lookup"><span data-stu-id="b0b42-148">The package was successfully pushed</span></span>
<span data-ttu-id="b0b42-149">400</span><span class="sxs-lookup"><span data-stu-id="b0b42-149">400</span></span>         | <span data-ttu-id="b0b42-150">Podany pakiet jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="b0b42-150">The provided package is invalid</span></span>
<span data-ttu-id="b0b42-151">409</span><span class="sxs-lookup"><span data-stu-id="b0b42-151">409</span></span>         | <span data-ttu-id="b0b42-152">Pakiet o identyfikatorze podana i wersji już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b0b42-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="b0b42-153">Implementacje Server różnią się na kod stanu powodzenia, które są zwracane, gdy pakiet zostanie pomyślnie przypisany.</span><span class="sxs-lookup"><span data-stu-id="b0b42-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="b0b42-154">Usuń pakiet</span><span class="sxs-lookup"><span data-stu-id="b0b42-154">Delete a package</span></span>

<span data-ttu-id="b0b42-155">nuget.org interpretuje żądanie usunięcia pakietu jako wiadomość "wyrejestrowanie".</span><span class="sxs-lookup"><span data-stu-id="b0b42-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="b0b42-156">Oznacza to, że pakiet jest nadal dostępna dla istniejących konsumentów pakietu, ale pakiet nie jest już wyświetlany w wynikach wyszukiwania lub w interfejsie sieci web.</span><span class="sxs-lookup"><span data-stu-id="b0b42-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="b0b42-157">Aby uzyskać więcej informacji na temat tej praktyką, zobacz [usunięte pakiety](../policies/deleting-packages.md) zasad.</span><span class="sxs-lookup"><span data-stu-id="b0b42-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="b0b42-158">Inne implementacje serwera są bezpłatne do interpretowania ten sygnał jako twardych delete, usuwanie nietrwałe lub wyrejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="b0b42-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="b0b42-159">Na przykład [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) obsługuje (tylko Obsługa starszych interfejsy API wersji 2 implementacji serwera), obsługujący żądanie jako unlist lub usuwania twardych na podstawie opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b0b42-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="b0b42-160">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="b0b42-160">Request parameters</span></span>

<span data-ttu-id="b0b42-161">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b0b42-161">Name</span></span>           | <span data-ttu-id="b0b42-162">W</span><span class="sxs-lookup"><span data-stu-id="b0b42-162">In</span></span>     | <span data-ttu-id="b0b42-163">Typ</span><span class="sxs-lookup"><span data-stu-id="b0b42-163">Type</span></span>   | <span data-ttu-id="b0b42-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b0b42-164">Required</span></span> | <span data-ttu-id="b0b42-165">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b0b42-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b0b42-166">ID</span><span class="sxs-lookup"><span data-stu-id="b0b42-166">ID</span></span>             | <span data-ttu-id="b0b42-167">Adres URL</span><span class="sxs-lookup"><span data-stu-id="b0b42-167">URL</span></span>    | <span data-ttu-id="b0b42-168">string</span><span class="sxs-lookup"><span data-stu-id="b0b42-168">string</span></span> | <span data-ttu-id="b0b42-169">Tak</span><span class="sxs-lookup"><span data-stu-id="b0b42-169">yes</span></span>      | <span data-ttu-id="b0b42-170">Identyfikator pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="b0b42-170">The ID of the package to delete</span></span>
<span data-ttu-id="b0b42-171">WERSJA</span><span class="sxs-lookup"><span data-stu-id="b0b42-171">VERSION</span></span>        | <span data-ttu-id="b0b42-172">Adres URL</span><span class="sxs-lookup"><span data-stu-id="b0b42-172">URL</span></span>    | <span data-ttu-id="b0b42-173">string</span><span class="sxs-lookup"><span data-stu-id="b0b42-173">string</span></span> | <span data-ttu-id="b0b42-174">Tak</span><span class="sxs-lookup"><span data-stu-id="b0b42-174">yes</span></span>      | <span data-ttu-id="b0b42-175">Wersja pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="b0b42-175">The version of the package to delete</span></span>
<span data-ttu-id="b0b42-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b0b42-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b0b42-177">nagłówek</span><span class="sxs-lookup"><span data-stu-id="b0b42-177">Header</span></span> | <span data-ttu-id="b0b42-178">string</span><span class="sxs-lookup"><span data-stu-id="b0b42-178">string</span></span> | <span data-ttu-id="b0b42-179">Tak</span><span class="sxs-lookup"><span data-stu-id="b0b42-179">yes</span></span>      | <span data-ttu-id="b0b42-180">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b0b42-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b0b42-181">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="b0b42-181">Response</span></span>

<span data-ttu-id="b0b42-182">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="b0b42-182">Status Code</span></span> | <span data-ttu-id="b0b42-183">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="b0b42-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="b0b42-184">204</span><span class="sxs-lookup"><span data-stu-id="b0b42-184">204</span></span>         | <span data-ttu-id="b0b42-185">Pakiet został usunięty.</span><span class="sxs-lookup"><span data-stu-id="b0b42-185">The package was deleted</span></span>
<span data-ttu-id="b0b42-186">404</span><span class="sxs-lookup"><span data-stu-id="b0b42-186">404</span></span>         | <span data-ttu-id="b0b42-187">Nie pakietu z dostępnego `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="b0b42-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="b0b42-188">Wystaw ponownie pakiet</span><span class="sxs-lookup"><span data-stu-id="b0b42-188">Relist a package</span></span>

<span data-ttu-id="b0b42-189">Jeśli pakiet jest nieobecne na liście, jest możliwe ten pakiet ponownie widoczne w wynikach wyszukiwania przy użyciu punktu końcowego "Wystaw ponownie".</span><span class="sxs-lookup"><span data-stu-id="b0b42-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="b0b42-190">Ten punkt końcowy ma ten sam kształt co [Usuń (wyrejestrowanie) punktu końcowego](#delete-a-package) , ale używa `POST` protokołu HTTP zamiast metody `DELETE` metody.</span><span class="sxs-lookup"><span data-stu-id="b0b42-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="b0b42-191">Jeśli pakiet jest już na liście, żądanie nadal powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="b0b42-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="b0b42-192">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="b0b42-192">Request parameters</span></span>

<span data-ttu-id="b0b42-193">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b0b42-193">Name</span></span>           | <span data-ttu-id="b0b42-194">W</span><span class="sxs-lookup"><span data-stu-id="b0b42-194">In</span></span>     | <span data-ttu-id="b0b42-195">Typ</span><span class="sxs-lookup"><span data-stu-id="b0b42-195">Type</span></span>   | <span data-ttu-id="b0b42-196">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b0b42-196">Required</span></span> | <span data-ttu-id="b0b42-197">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b0b42-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b0b42-198">ID</span><span class="sxs-lookup"><span data-stu-id="b0b42-198">ID</span></span>             | <span data-ttu-id="b0b42-199">Adres URL</span><span class="sxs-lookup"><span data-stu-id="b0b42-199">URL</span></span>    | <span data-ttu-id="b0b42-200">string</span><span class="sxs-lookup"><span data-stu-id="b0b42-200">string</span></span> | <span data-ttu-id="b0b42-201">Tak</span><span class="sxs-lookup"><span data-stu-id="b0b42-201">yes</span></span>      | <span data-ttu-id="b0b42-202">Identyfikator pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="b0b42-202">The ID of the package to relist</span></span>
<span data-ttu-id="b0b42-203">WERSJA</span><span class="sxs-lookup"><span data-stu-id="b0b42-203">VERSION</span></span>        | <span data-ttu-id="b0b42-204">Adres URL</span><span class="sxs-lookup"><span data-stu-id="b0b42-204">URL</span></span>    | <span data-ttu-id="b0b42-205">string</span><span class="sxs-lookup"><span data-stu-id="b0b42-205">string</span></span> | <span data-ttu-id="b0b42-206">Tak</span><span class="sxs-lookup"><span data-stu-id="b0b42-206">yes</span></span>      | <span data-ttu-id="b0b42-207">Wersja pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="b0b42-207">The version of the package to relist</span></span>
<span data-ttu-id="b0b42-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b0b42-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b0b42-209">nagłówek</span><span class="sxs-lookup"><span data-stu-id="b0b42-209">Header</span></span> | <span data-ttu-id="b0b42-210">string</span><span class="sxs-lookup"><span data-stu-id="b0b42-210">string</span></span> | <span data-ttu-id="b0b42-211">Tak</span><span class="sxs-lookup"><span data-stu-id="b0b42-211">yes</span></span>      | <span data-ttu-id="b0b42-212">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b0b42-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b0b42-213">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="b0b42-213">Response</span></span>

<span data-ttu-id="b0b42-214">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="b0b42-214">Status Code</span></span> | <span data-ttu-id="b0b42-215">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="b0b42-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="b0b42-216">200</span><span class="sxs-lookup"><span data-stu-id="b0b42-216">200</span></span>         | <span data-ttu-id="b0b42-217">Pakiet znajduje się teraz</span><span class="sxs-lookup"><span data-stu-id="b0b42-217">The package is now listed</span></span>
<span data-ttu-id="b0b42-218">404</span><span class="sxs-lookup"><span data-stu-id="b0b42-218">404</span></span>         | <span data-ttu-id="b0b42-219">Nie pakietu z dostępnego `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="b0b42-219">No package with the provided `ID` and `VERSION` exists</span></span>
