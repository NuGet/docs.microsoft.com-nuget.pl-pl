---
title: Wypychanie i usunąć NuGet interfejsu API
description: Usługa publikowania zezwala klientom na publikowanie nowych pakietów i unlist lub usunąć istniejące pakiety.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819484"
---
# <a name="push-and-delete"></a><span data-ttu-id="426ea-103">Wypychanie i usuwania</span><span class="sxs-lookup"><span data-stu-id="426ea-103">Push and Delete</span></span>

<span data-ttu-id="426ea-104">Istnieje możliwość push, Usuń (lub unlist, w zależności od implementacji serwera) i ponownie wystaw pakiety przy użyciu interfejsu API programu NuGet w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="426ea-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="426ea-105">Operacje te są oparte na off z `PackagePublish` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="426ea-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="426ea-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="426ea-106">Versioning</span></span>

<span data-ttu-id="426ea-107">Następujące `@type` jest używana wartość:</span><span class="sxs-lookup"><span data-stu-id="426ea-107">The following `@type` value is used:</span></span>

<span data-ttu-id="426ea-108">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="426ea-108">@type value</span></span>          | <span data-ttu-id="426ea-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="426ea-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="426ea-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="426ea-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="426ea-111">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="426ea-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="426ea-112">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="426ea-112">Base URL</span></span>

<span data-ttu-id="426ea-113">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `PackagePublish/2.0.0` zasobów w źródle pakietów [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="426ea-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="426ea-114">Poniżej dokumentację nuget.org adres URL jest używany.</span><span class="sxs-lookup"><span data-stu-id="426ea-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="426ea-115">Należy wziąć pod uwagę `https://www.nuget.org/api/v2/package` jako symbol zastępczy `@id` wartość znajduje się w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="426ea-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="426ea-116">Należy pamiętać, że ten adres URL wskazuje do tej samej lokalizacji co starszego punktu końcowego wypychania V2, ponieważ protokół jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="426ea-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="426ea-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="426ea-117">HTTP methods</span></span>

<span data-ttu-id="426ea-118">`PUT`, `POST` i `DELETE` metod HTTP obsługiwanych przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="426ea-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="426ea-119">Dla metod, które są obsługiwane na każdym punkcie końcowym są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="426ea-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="426ea-120">Wypychanie pakietu</span><span class="sxs-lookup"><span data-stu-id="426ea-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="426ea-121">ma nuget.org [dodatkowe wymagania](NuGet-Protocols.md) do interakcji z punktem końcowym wypychania.</span><span class="sxs-lookup"><span data-stu-id="426ea-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="426ea-122">nuget.org obsługuje położenia nowe pakiety przy użyciu następujących interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="426ea-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="426ea-123">Jeśli pakiet o identyfikatorze podana i wersji już istnieje, nuget.org spowoduje odrzucenie powiadomienia wypychanego.</span><span class="sxs-lookup"><span data-stu-id="426ea-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="426ea-124">Inne źródła pakietu może obsługiwać, zastępując istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="426ea-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="426ea-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="426ea-125">Request parameters</span></span>

<span data-ttu-id="426ea-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="426ea-126">Name</span></span>           | <span data-ttu-id="426ea-127">W</span><span class="sxs-lookup"><span data-stu-id="426ea-127">In</span></span>     | <span data-ttu-id="426ea-128">Typ</span><span class="sxs-lookup"><span data-stu-id="426ea-128">Type</span></span>   | <span data-ttu-id="426ea-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="426ea-129">Required</span></span> | <span data-ttu-id="426ea-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="426ea-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="426ea-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="426ea-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="426ea-132">nagłówek</span><span class="sxs-lookup"><span data-stu-id="426ea-132">Header</span></span> | <span data-ttu-id="426ea-133">string</span><span class="sxs-lookup"><span data-stu-id="426ea-133">string</span></span> | <span data-ttu-id="426ea-134">Tak</span><span class="sxs-lookup"><span data-stu-id="426ea-134">yes</span></span>      | <span data-ttu-id="426ea-135">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="426ea-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="426ea-136">Klucz interfejsu API jest ciąg z ogólnym opisem zaakceptujesz ze źródła pakietów przez użytkownika i skonfigurowane do klienta.</span><span class="sxs-lookup"><span data-stu-id="426ea-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="426ea-137">Nie określony ciąg formatu jest obowiązkowe, ale długość klucza interfejsu API nie może przekraczać uzasadnione rozmiaru dla wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="426ea-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="426ea-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="426ea-138">Request body</span></span>

<span data-ttu-id="426ea-139">Treść żądania musi występować w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="426ea-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="426ea-140">Wieloczęściowych danych formularza</span><span class="sxs-lookup"><span data-stu-id="426ea-140">Multipart form data</span></span>

<span data-ttu-id="426ea-141">Nagłówek żądania `Content-Type` jest `multipart/form-data` i raw bajtów .nupkg przekazywanej pierwszego elementu w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="426ea-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="426ea-142">Kolejne elementy treści wieloczęściowej wiadomości są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="426ea-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="426ea-143">Nazwa pliku lub inne nagłówki elementów wieloczęściowego są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="426ea-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="426ea-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="426ea-144">Response</span></span>

<span data-ttu-id="426ea-145">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="426ea-145">Status Code</span></span> | <span data-ttu-id="426ea-146">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="426ea-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="426ea-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="426ea-147">201, 202</span></span>    | <span data-ttu-id="426ea-148">Pakiet został pomyślnie przypisany.</span><span class="sxs-lookup"><span data-stu-id="426ea-148">The package was successfully pushed</span></span>
<span data-ttu-id="426ea-149">400</span><span class="sxs-lookup"><span data-stu-id="426ea-149">400</span></span>         | <span data-ttu-id="426ea-150">Podany pakiet jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="426ea-150">The provided package is invalid</span></span>
<span data-ttu-id="426ea-151">409</span><span class="sxs-lookup"><span data-stu-id="426ea-151">409</span></span>         | <span data-ttu-id="426ea-152">Pakiet o identyfikatorze podana i wersji już istnieje.</span><span class="sxs-lookup"><span data-stu-id="426ea-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="426ea-153">Implementacje serwera różnią się od kod stanu Powodzenie zwracany, gdy pakiet zostanie pomyślnie przeniesiona.</span><span class="sxs-lookup"><span data-stu-id="426ea-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="426ea-154">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="426ea-154">Delete a package</span></span>

<span data-ttu-id="426ea-155">nuget.org interpretowane jako żądanie usunięcia pakietu jako "unlist".</span><span class="sxs-lookup"><span data-stu-id="426ea-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="426ea-156">Oznacza to, że pakiet jest nadal dostępny dla istniejących konsumentów pakietu, ale pakiet nie będzie już wyświetlana w wynikach wyszukiwania lub interfejs sieci web.</span><span class="sxs-lookup"><span data-stu-id="426ea-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="426ea-157">Aby uzyskać więcej informacji o tym rozwiązaniem, zobacz [usunięte pakiety](../policies/deleting-packages.md) zasad.</span><span class="sxs-lookup"><span data-stu-id="426ea-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="426ea-158">Inne implementacje serwera mogą interpretować tego sygnału jako usuwania twardych, usunąć soft lub unlist.</span><span class="sxs-lookup"><span data-stu-id="426ea-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="426ea-159">Na przykład [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (serwer obsługujący tylko starsze interfejsu API w wersji 2) obsługuje obsługi tego żądania jako unlist lub usuwania twardych, na podstawie opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="426ea-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="426ea-160">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="426ea-160">Request parameters</span></span>

<span data-ttu-id="426ea-161">Nazwa</span><span class="sxs-lookup"><span data-stu-id="426ea-161">Name</span></span>           | <span data-ttu-id="426ea-162">W</span><span class="sxs-lookup"><span data-stu-id="426ea-162">In</span></span>     | <span data-ttu-id="426ea-163">Typ</span><span class="sxs-lookup"><span data-stu-id="426ea-163">Type</span></span>   | <span data-ttu-id="426ea-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="426ea-164">Required</span></span> | <span data-ttu-id="426ea-165">Uwagi</span><span class="sxs-lookup"><span data-stu-id="426ea-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="426ea-166">ID</span><span class="sxs-lookup"><span data-stu-id="426ea-166">ID</span></span>             | <span data-ttu-id="426ea-167">Adres URL</span><span class="sxs-lookup"><span data-stu-id="426ea-167">URL</span></span>    | <span data-ttu-id="426ea-168">string</span><span class="sxs-lookup"><span data-stu-id="426ea-168">string</span></span> | <span data-ttu-id="426ea-169">Tak</span><span class="sxs-lookup"><span data-stu-id="426ea-169">yes</span></span>      | <span data-ttu-id="426ea-170">Identyfikator pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="426ea-170">The ID of the package to delete</span></span>
<span data-ttu-id="426ea-171">WERSJA</span><span class="sxs-lookup"><span data-stu-id="426ea-171">VERSION</span></span>        | <span data-ttu-id="426ea-172">Adres URL</span><span class="sxs-lookup"><span data-stu-id="426ea-172">URL</span></span>    | <span data-ttu-id="426ea-173">string</span><span class="sxs-lookup"><span data-stu-id="426ea-173">string</span></span> | <span data-ttu-id="426ea-174">Tak</span><span class="sxs-lookup"><span data-stu-id="426ea-174">yes</span></span>      | <span data-ttu-id="426ea-175">Wersja pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="426ea-175">The version of the package to delete</span></span>
<span data-ttu-id="426ea-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="426ea-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="426ea-177">nagłówek</span><span class="sxs-lookup"><span data-stu-id="426ea-177">Header</span></span> | <span data-ttu-id="426ea-178">string</span><span class="sxs-lookup"><span data-stu-id="426ea-178">string</span></span> | <span data-ttu-id="426ea-179">Tak</span><span class="sxs-lookup"><span data-stu-id="426ea-179">yes</span></span>      | <span data-ttu-id="426ea-180">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="426ea-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="426ea-181">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="426ea-181">Response</span></span>

<span data-ttu-id="426ea-182">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="426ea-182">Status Code</span></span> | <span data-ttu-id="426ea-183">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="426ea-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="426ea-184">204</span><span class="sxs-lookup"><span data-stu-id="426ea-184">204</span></span>         | <span data-ttu-id="426ea-185">Pakiet został usunięty.</span><span class="sxs-lookup"><span data-stu-id="426ea-185">The package was deleted</span></span>
<span data-ttu-id="426ea-186">404</span><span class="sxs-lookup"><span data-stu-id="426ea-186">404</span></span>         | <span data-ttu-id="426ea-187">Nie pakietu z dostarczonych `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="426ea-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="426ea-188">Wystaw ponownie pakietu</span><span class="sxs-lookup"><span data-stu-id="426ea-188">Relist a package</span></span>

<span data-ttu-id="426ea-189">Jeśli pakiet jest nieznajdujące się na liście, istnieje możliwość ponownie wyświetlić tego pakietu w wynikach wyszukiwania przy użyciu punktu końcowego "Wystaw ponownie".</span><span class="sxs-lookup"><span data-stu-id="426ea-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="426ea-190">Ten punkt końcowy ma ten sam kształt co [usunąć (unlist) punktu końcowego](#delete-a-package) , ale `POST` HTTP zamiast metody `DELETE` metody.</span><span class="sxs-lookup"><span data-stu-id="426ea-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="426ea-191">Jeśli pakiet jest już na liście, żądanie nadal powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="426ea-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="426ea-192">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="426ea-192">Request parameters</span></span>

<span data-ttu-id="426ea-193">Nazwa</span><span class="sxs-lookup"><span data-stu-id="426ea-193">Name</span></span>           | <span data-ttu-id="426ea-194">W</span><span class="sxs-lookup"><span data-stu-id="426ea-194">In</span></span>     | <span data-ttu-id="426ea-195">Typ</span><span class="sxs-lookup"><span data-stu-id="426ea-195">Type</span></span>   | <span data-ttu-id="426ea-196">Wymagane</span><span class="sxs-lookup"><span data-stu-id="426ea-196">Required</span></span> | <span data-ttu-id="426ea-197">Uwagi</span><span class="sxs-lookup"><span data-stu-id="426ea-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="426ea-198">ID</span><span class="sxs-lookup"><span data-stu-id="426ea-198">ID</span></span>             | <span data-ttu-id="426ea-199">Adres URL</span><span class="sxs-lookup"><span data-stu-id="426ea-199">URL</span></span>    | <span data-ttu-id="426ea-200">string</span><span class="sxs-lookup"><span data-stu-id="426ea-200">string</span></span> | <span data-ttu-id="426ea-201">Tak</span><span class="sxs-lookup"><span data-stu-id="426ea-201">yes</span></span>      | <span data-ttu-id="426ea-202">Identyfikator pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="426ea-202">The ID of the package to relist</span></span>
<span data-ttu-id="426ea-203">WERSJA</span><span class="sxs-lookup"><span data-stu-id="426ea-203">VERSION</span></span>        | <span data-ttu-id="426ea-204">Adres URL</span><span class="sxs-lookup"><span data-stu-id="426ea-204">URL</span></span>    | <span data-ttu-id="426ea-205">string</span><span class="sxs-lookup"><span data-stu-id="426ea-205">string</span></span> | <span data-ttu-id="426ea-206">Tak</span><span class="sxs-lookup"><span data-stu-id="426ea-206">yes</span></span>      | <span data-ttu-id="426ea-207">Wersja pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="426ea-207">The version of the package to relist</span></span>
<span data-ttu-id="426ea-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="426ea-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="426ea-209">nagłówek</span><span class="sxs-lookup"><span data-stu-id="426ea-209">Header</span></span> | <span data-ttu-id="426ea-210">string</span><span class="sxs-lookup"><span data-stu-id="426ea-210">string</span></span> | <span data-ttu-id="426ea-211">Tak</span><span class="sxs-lookup"><span data-stu-id="426ea-211">yes</span></span>      | <span data-ttu-id="426ea-212">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="426ea-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="426ea-213">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="426ea-213">Response</span></span>

<span data-ttu-id="426ea-214">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="426ea-214">Status Code</span></span> | <span data-ttu-id="426ea-215">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="426ea-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="426ea-216">200</span><span class="sxs-lookup"><span data-stu-id="426ea-216">200</span></span>         | <span data-ttu-id="426ea-217">Pakiet zostanie wyświetlony</span><span class="sxs-lookup"><span data-stu-id="426ea-217">The package is now listed</span></span>
<span data-ttu-id="426ea-218">404</span><span class="sxs-lookup"><span data-stu-id="426ea-218">404</span></span>         | <span data-ttu-id="426ea-219">Nie pakietu z dostarczonych `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="426ea-219">No package with the provided `ID` and `VERSION` exists</span></span>
