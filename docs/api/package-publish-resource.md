---
title: Wypychanie i usuwanie, interfejs API NuGet
description: Usługa publikowania pozwala klientom na publikowanie nowych pakietów i usuwanie listy lub usunięcie istniejących pakietów.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773927"
---
# <a name="push-and-delete"></a><span data-ttu-id="94abd-103">Wypychanie i usuwanie</span><span class="sxs-lookup"><span data-stu-id="94abd-103">Push and Delete</span></span>

<span data-ttu-id="94abd-104">Możliwe jest wypchnięcie, usunięcie (lub wycofanie listy, w zależności od implementacji serwera) i ponownie wystawianie pakietów przy użyciu interfejsu API programu NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="94abd-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="94abd-105">Operacje te są oparte na `PackagePublish` zasobach znalezionych w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="94abd-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="94abd-106">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="94abd-106">Versioning</span></span>

<span data-ttu-id="94abd-107">`@type`Używana jest następująca wartość:</span><span class="sxs-lookup"><span data-stu-id="94abd-107">The following `@type` value is used:</span></span>

<span data-ttu-id="94abd-108">@type wartościami</span><span class="sxs-lookup"><span data-stu-id="94abd-108">@type value</span></span>          | <span data-ttu-id="94abd-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="94abd-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="94abd-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="94abd-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="94abd-111">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="94abd-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="94abd-112">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="94abd-112">Base URL</span></span>

<span data-ttu-id="94abd-113">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości `PackagePublish/2.0.0` zasobu w [indeksie usługi](service-index.md)źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="94abd-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="94abd-114">W poniższej dokumentacji znajduje się adres URL programu NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="94abd-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="94abd-115">Rozważmy `https://www.nuget.org/api/v2/package` jako symbol zastępczy dla `@id` wartości znalezionej w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="94abd-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="94abd-116">Należy zauważyć, że ten adres URL wskazuje tę samą lokalizację co starszy punkt końcowy w wersji 2, ponieważ protokół jest taki sam.</span><span class="sxs-lookup"><span data-stu-id="94abd-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="94abd-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="94abd-117">HTTP methods</span></span>

<span data-ttu-id="94abd-118">`PUT` `POST` `DELETE` Metody i są obsługiwane przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="94abd-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="94abd-119">Dla których metod są obsługiwane w każdym punkcie końcowym, zobacz poniżej.</span><span class="sxs-lookup"><span data-stu-id="94abd-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="94abd-120">Wypchnij pakiet</span><span class="sxs-lookup"><span data-stu-id="94abd-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="94abd-121">nuget.org ma [dodatkowe wymagania](NuGet-Protocols.md) dotyczące współpracy z punktem końcowym wypychania.</span><span class="sxs-lookup"><span data-stu-id="94abd-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="94abd-122">nuget.org obsługuje wypychanie nowych pakietów przy użyciu poniższego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="94abd-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="94abd-123">Jeśli pakiet o podanym IDENTYFIKATORze i wersji już istnieje, nuget.org odrzuci wypychanie.</span><span class="sxs-lookup"><span data-stu-id="94abd-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="94abd-124">Inne źródła pakietów mogą obsługiwać zastąpienie istniejącego pakietu.</span><span class="sxs-lookup"><span data-stu-id="94abd-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="94abd-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="94abd-125">Request parameters</span></span>

<span data-ttu-id="94abd-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="94abd-126">Name</span></span>           | <span data-ttu-id="94abd-127">W</span><span class="sxs-lookup"><span data-stu-id="94abd-127">In</span></span>     | <span data-ttu-id="94abd-128">Typ</span><span class="sxs-lookup"><span data-stu-id="94abd-128">Type</span></span>   | <span data-ttu-id="94abd-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="94abd-129">Required</span></span> | <span data-ttu-id="94abd-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="94abd-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="94abd-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="94abd-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="94abd-132">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="94abd-132">Header</span></span> | <span data-ttu-id="94abd-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="94abd-133">string</span></span> | <span data-ttu-id="94abd-134">tak</span><span class="sxs-lookup"><span data-stu-id="94abd-134">yes</span></span>      | <span data-ttu-id="94abd-135">Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="94abd-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="94abd-136">Klucz interfejsu API to nieprzezroczysty ciąg z źródła pakietu przez użytkownika i skonfigurowany na kliencie.</span><span class="sxs-lookup"><span data-stu-id="94abd-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="94abd-137">Żaden określony format ciągu nie jest dozwolony, ale długość klucza interfejsu API nie może przekroczyć rozsądnego rozmiaru wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="94abd-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="94abd-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="94abd-138">Request body</span></span>

<span data-ttu-id="94abd-139">Treść żądania musi mieć następującą formę:</span><span class="sxs-lookup"><span data-stu-id="94abd-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="94abd-140">Wieloczęściowe dane formularza</span><span class="sxs-lookup"><span data-stu-id="94abd-140">Multipart form data</span></span>

<span data-ttu-id="94abd-141">Nagłówek żądania `Content-Type` jest `multipart/form-data` i pierwszy element w treści żądania to nieprzetworzone bajty NUPKG.</span><span class="sxs-lookup"><span data-stu-id="94abd-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="94abd-142">Kolejne elementy w treści wieloczęściowej są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="94abd-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="94abd-143">Nazwa pliku lub wszystkie inne nagłówki elementów wieloczęściowych zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="94abd-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="94abd-144">Reakcja</span><span class="sxs-lookup"><span data-stu-id="94abd-144">Response</span></span>

<span data-ttu-id="94abd-145">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="94abd-145">Status Code</span></span> | <span data-ttu-id="94abd-146">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="94abd-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="94abd-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="94abd-147">201, 202</span></span>    | <span data-ttu-id="94abd-148">Pakiet został pomyślnie wypychany</span><span class="sxs-lookup"><span data-stu-id="94abd-148">The package was successfully pushed</span></span>
<span data-ttu-id="94abd-149">400</span><span class="sxs-lookup"><span data-stu-id="94abd-149">400</span></span>         | <span data-ttu-id="94abd-150">Podany pakiet jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="94abd-150">The provided package is invalid</span></span>
<span data-ttu-id="94abd-151">409</span><span class="sxs-lookup"><span data-stu-id="94abd-151">409</span></span>         | <span data-ttu-id="94abd-152">Pakiet z podanym IDENTYFIKATORem i wersją już istnieje</span><span class="sxs-lookup"><span data-stu-id="94abd-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="94abd-153">Implementacje serwera różnią się w zależności od kodu stanu sukcesu zwracanego po pomyślnym wypchnięciu pakietu.</span><span class="sxs-lookup"><span data-stu-id="94abd-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="94abd-154">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="94abd-154">Delete a package</span></span>

<span data-ttu-id="94abd-155">nuget.org interpretuje żądanie usunięcia pakietu jako "unlisting".</span><span class="sxs-lookup"><span data-stu-id="94abd-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="94abd-156">Oznacza to, że pakiet jest nadal dostępny dla istniejących odbiorców pakietu, ale pakiet nie jest już wyświetlany w wynikach wyszukiwania ani w interfejsie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="94abd-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="94abd-157">Aby uzyskać więcej informacji na temat tego rozwiązania, zobacz zasady [usuwania pakietów](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="94abd-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="94abd-158">Inne implementacje serwera są bezpłatne, aby interpretować ten sygnał jako twarde usuwanie, usuwanie nietrwałe lub cofanie listy.</span><span class="sxs-lookup"><span data-stu-id="94abd-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="94abd-159">Na przykład plik [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (implementacja serwera obsługująca tylko starszy interfejs API v2) obsługuje obsługę tego żądania jako nielistę lub trwałego usunięcia na podstawie opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="94abd-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="94abd-160">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="94abd-160">Request parameters</span></span>

<span data-ttu-id="94abd-161">Nazwa</span><span class="sxs-lookup"><span data-stu-id="94abd-161">Name</span></span>           | <span data-ttu-id="94abd-162">W</span><span class="sxs-lookup"><span data-stu-id="94abd-162">In</span></span>     | <span data-ttu-id="94abd-163">Typ</span><span class="sxs-lookup"><span data-stu-id="94abd-163">Type</span></span>   | <span data-ttu-id="94abd-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="94abd-164">Required</span></span> | <span data-ttu-id="94abd-165">Uwagi</span><span class="sxs-lookup"><span data-stu-id="94abd-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="94abd-166">ID (Identyfikator)</span><span class="sxs-lookup"><span data-stu-id="94abd-166">ID</span></span>             | <span data-ttu-id="94abd-167">Adres URL</span><span class="sxs-lookup"><span data-stu-id="94abd-167">URL</span></span>    | <span data-ttu-id="94abd-168">ciąg</span><span class="sxs-lookup"><span data-stu-id="94abd-168">string</span></span> | <span data-ttu-id="94abd-169">tak</span><span class="sxs-lookup"><span data-stu-id="94abd-169">yes</span></span>      | <span data-ttu-id="94abd-170">Identyfikator pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="94abd-170">The ID of the package to delete</span></span>
<span data-ttu-id="94abd-171">WERSJA</span><span class="sxs-lookup"><span data-stu-id="94abd-171">VERSION</span></span>        | <span data-ttu-id="94abd-172">Adres URL</span><span class="sxs-lookup"><span data-stu-id="94abd-172">URL</span></span>    | <span data-ttu-id="94abd-173">ciąg</span><span class="sxs-lookup"><span data-stu-id="94abd-173">string</span></span> | <span data-ttu-id="94abd-174">tak</span><span class="sxs-lookup"><span data-stu-id="94abd-174">yes</span></span>      | <span data-ttu-id="94abd-175">Wersja pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="94abd-175">The version of the package to delete</span></span>
<span data-ttu-id="94abd-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="94abd-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="94abd-177">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="94abd-177">Header</span></span> | <span data-ttu-id="94abd-178">ciąg</span><span class="sxs-lookup"><span data-stu-id="94abd-178">string</span></span> | <span data-ttu-id="94abd-179">tak</span><span class="sxs-lookup"><span data-stu-id="94abd-179">yes</span></span>      | <span data-ttu-id="94abd-180">Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="94abd-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="94abd-181">Reakcja</span><span class="sxs-lookup"><span data-stu-id="94abd-181">Response</span></span>

<span data-ttu-id="94abd-182">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="94abd-182">Status Code</span></span> | <span data-ttu-id="94abd-183">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="94abd-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="94abd-184">204</span><span class="sxs-lookup"><span data-stu-id="94abd-184">204</span></span>         | <span data-ttu-id="94abd-185">Pakiet został usunięty</span><span class="sxs-lookup"><span data-stu-id="94abd-185">The package was deleted</span></span>
<span data-ttu-id="94abd-186">404</span><span class="sxs-lookup"><span data-stu-id="94abd-186">404</span></span>         | <span data-ttu-id="94abd-187">Nie ma pakietu z podanym elementem `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="94abd-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="94abd-188">Wystaw ponownie pakiet</span><span class="sxs-lookup"><span data-stu-id="94abd-188">Relist a package</span></span>

<span data-ttu-id="94abd-189">Jeśli pakiet nie jest wyświetlany na liście, można go ponownie wyświetlić w wynikach wyszukiwania przy użyciu punktu końcowego "relist".</span><span class="sxs-lookup"><span data-stu-id="94abd-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="94abd-190">Ten punkt końcowy ma ten sam kształt co [punkt końcowy Delete (unlisting)](#delete-a-package) , ale używa `POST` metody http zamiast `DELETE` metody.</span><span class="sxs-lookup"><span data-stu-id="94abd-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="94abd-191">Jeśli pakiet jest już wymieniony, żądanie nadal kończy się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="94abd-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="94abd-192">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="94abd-192">Request parameters</span></span>

<span data-ttu-id="94abd-193">Nazwa</span><span class="sxs-lookup"><span data-stu-id="94abd-193">Name</span></span>           | <span data-ttu-id="94abd-194">W</span><span class="sxs-lookup"><span data-stu-id="94abd-194">In</span></span>     | <span data-ttu-id="94abd-195">Typ</span><span class="sxs-lookup"><span data-stu-id="94abd-195">Type</span></span>   | <span data-ttu-id="94abd-196">Wymagane</span><span class="sxs-lookup"><span data-stu-id="94abd-196">Required</span></span> | <span data-ttu-id="94abd-197">Uwagi</span><span class="sxs-lookup"><span data-stu-id="94abd-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="94abd-198">ID (Identyfikator)</span><span class="sxs-lookup"><span data-stu-id="94abd-198">ID</span></span>             | <span data-ttu-id="94abd-199">Adres URL</span><span class="sxs-lookup"><span data-stu-id="94abd-199">URL</span></span>    | <span data-ttu-id="94abd-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="94abd-200">string</span></span> | <span data-ttu-id="94abd-201">tak</span><span class="sxs-lookup"><span data-stu-id="94abd-201">yes</span></span>      | <span data-ttu-id="94abd-202">Identyfikator pakietu do wyświetlenia ponownie</span><span class="sxs-lookup"><span data-stu-id="94abd-202">The ID of the package to relist</span></span>
<span data-ttu-id="94abd-203">WERSJA</span><span class="sxs-lookup"><span data-stu-id="94abd-203">VERSION</span></span>        | <span data-ttu-id="94abd-204">Adres URL</span><span class="sxs-lookup"><span data-stu-id="94abd-204">URL</span></span>    | <span data-ttu-id="94abd-205">ciąg</span><span class="sxs-lookup"><span data-stu-id="94abd-205">string</span></span> | <span data-ttu-id="94abd-206">tak</span><span class="sxs-lookup"><span data-stu-id="94abd-206">yes</span></span>      | <span data-ttu-id="94abd-207">Wersja pakietu do wyświetlenia ponownie</span><span class="sxs-lookup"><span data-stu-id="94abd-207">The version of the package to relist</span></span>
<span data-ttu-id="94abd-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="94abd-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="94abd-209">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="94abd-209">Header</span></span> | <span data-ttu-id="94abd-210">ciąg</span><span class="sxs-lookup"><span data-stu-id="94abd-210">string</span></span> | <span data-ttu-id="94abd-211">tak</span><span class="sxs-lookup"><span data-stu-id="94abd-211">yes</span></span>      | <span data-ttu-id="94abd-212">Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="94abd-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="94abd-213">Reakcja</span><span class="sxs-lookup"><span data-stu-id="94abd-213">Response</span></span>

<span data-ttu-id="94abd-214">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="94abd-214">Status Code</span></span> | <span data-ttu-id="94abd-215">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="94abd-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="94abd-216">200</span><span class="sxs-lookup"><span data-stu-id="94abd-216">200</span></span>         | <span data-ttu-id="94abd-217">Pakiet znajduje się teraz na liście</span><span class="sxs-lookup"><span data-stu-id="94abd-217">The package is now listed</span></span>
<span data-ttu-id="94abd-218">404</span><span class="sxs-lookup"><span data-stu-id="94abd-218">404</span></span>         | <span data-ttu-id="94abd-219">Nie ma pakietu z podanym elementem `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="94abd-219">No package with the provided `ID` and `VERSION` exists</span></span>
