---
title: "Wypychanie i usunąć NuGet interfejsu API | Dokumentacja firmy Microsoft"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Usługa publikowania zezwala klientom na publikowanie nowych pakietów i unlist lub usunąć istniejące pakiety."
keywords: "Pakiet wypychania NuGet interfejsu API, interfejsu API NuGet usunąć pakiet, interfejsu API NuGet unlist pakietu NuGet API przekazywania pakietu, NuGet interfejsu API tworzenia pakietu"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 87970a701c63bce2b74c619069ec1d231ea77ab5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="c7a8d-104">Wypychanie i usuwania</span><span class="sxs-lookup"><span data-stu-id="c7a8d-104">Push and Delete</span></span>

<span data-ttu-id="c7a8d-105">Istnieje możliwość push, Usuń (lub unlist, w zależności od implementacji serwera) i ponownie wystaw pakiety przy użyciu interfejsu API programu NuGet w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="c7a8d-106">Operacje te są oparte na off z `PackagePublish` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c7a8d-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c7a8d-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="c7a8d-107">Versioning</span></span>

<span data-ttu-id="c7a8d-108">Następujące `@type` jest używana wartość:</span><span class="sxs-lookup"><span data-stu-id="c7a8d-108">The following `@type` value is used:</span></span>

<span data-ttu-id="c7a8d-109">@typewartość</span><span class="sxs-lookup"><span data-stu-id="c7a8d-109">@type value</span></span>          | <span data-ttu-id="c7a8d-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c7a8d-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="c7a8d-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="c7a8d-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="c7a8d-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="c7a8d-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="c7a8d-113">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="c7a8d-113">Base URL</span></span>

<span data-ttu-id="c7a8d-114">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `PackagePublish/2.0.0` zasobów w źródle pakietów [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c7a8d-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="c7a8d-115">Poniżej dokumentację nuget.org adres URL jest używany.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="c7a8d-116">Należy wziąć pod uwagę `https://www.nuget.org/api/v2/package` jako symbol zastępczy `@id` wartość znajduje się w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="c7a8d-117">Należy pamiętać, że ten adres URL wskazuje do tej samej lokalizacji co starszego punktu końcowego wypychania V2, ponieważ protokół jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c7a8d-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="c7a8d-118">HTTP methods</span></span>

<span data-ttu-id="c7a8d-119">`PUT`, `POST` i `DELETE` metod HTTP obsługiwanych przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="c7a8d-120">Dla metod, które są obsługiwane na każdym punkcie końcowym są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="c7a8d-121">Wypychanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c7a8d-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="c7a8d-122">ma nuget.org [dodatkowe wymagania](NuGet-Protocols.md) do interakcji z punktem końcowym wypychania.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="c7a8d-123">nuget.org obsługuje położenia nowe pakiety przy użyciu następujących interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="c7a8d-124">Jeśli pakiet o identyfikatorze podana i wersji już istnieje, nuget.org spowoduje odrzucenie powiadomienia wypychanego.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="c7a8d-125">Inne źródła pakietu może obsługiwać, zastępując istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="c7a8d-126">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="c7a8d-126">Request parameters</span></span>

<span data-ttu-id="c7a8d-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7a8d-127">Name</span></span>           | <span data-ttu-id="c7a8d-128">W</span><span class="sxs-lookup"><span data-stu-id="c7a8d-128">In</span></span>     | <span data-ttu-id="c7a8d-129">Typ</span><span class="sxs-lookup"><span data-stu-id="c7a8d-129">Type</span></span>   | <span data-ttu-id="c7a8d-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c7a8d-130">Required</span></span> | <span data-ttu-id="c7a8d-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c7a8d-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c7a8d-132">ApiKey-X-NuGet</span><span class="sxs-lookup"><span data-stu-id="c7a8d-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="c7a8d-133">nagłówek</span><span class="sxs-lookup"><span data-stu-id="c7a8d-133">Header</span></span> | <span data-ttu-id="c7a8d-134">string</span><span class="sxs-lookup"><span data-stu-id="c7a8d-134">string</span></span> | <span data-ttu-id="c7a8d-135">Tak</span><span class="sxs-lookup"><span data-stu-id="c7a8d-135">yes</span></span>      | <span data-ttu-id="c7a8d-136">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="c7a8d-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="c7a8d-137">Klucz interfejsu API jest ciąg z ogólnym opisem zaakceptujesz ze źródła pakietów przez użytkownika i skonfigurowane do klienta.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="c7a8d-138">Nie określony ciąg formatu jest obowiązkowe, ale długość klucza interfejsu API nie może przekraczać uzasadnione rozmiaru dla wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="c7a8d-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c7a8d-139">Request body</span></span>

<span data-ttu-id="c7a8d-140">Treść żądania musi występować w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="c7a8d-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="c7a8d-141">Wieloczęściowych danych formularza</span><span class="sxs-lookup"><span data-stu-id="c7a8d-141">Multipart form data</span></span>

<span data-ttu-id="c7a8d-142">Nagłówek żądania `Content-Type` jest `multipart/form-data` i raw bajtów .nupkg przekazywanej pierwszego elementu w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="c7a8d-143">Kolejne elementy treści wieloczęściowej wiadomości są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="c7a8d-144">Nazwa pliku lub inne nagłówki elementów wieloczęściowego są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="c7a8d-145">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c7a8d-145">Response</span></span>

<span data-ttu-id="c7a8d-146">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="c7a8d-146">Status Code</span></span> | <span data-ttu-id="c7a8d-147">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="c7a8d-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="c7a8d-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="c7a8d-148">201, 202</span></span>    | <span data-ttu-id="c7a8d-149">Pakiet został pomyślnie przypisany.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-149">The package was successfully pushed</span></span>
<span data-ttu-id="c7a8d-150">400</span><span class="sxs-lookup"><span data-stu-id="c7a8d-150">400</span></span>         | <span data-ttu-id="c7a8d-151">Podany pakiet jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="c7a8d-151">The provided package is invalid</span></span>
<span data-ttu-id="c7a8d-152">409</span><span class="sxs-lookup"><span data-stu-id="c7a8d-152">409</span></span>         | <span data-ttu-id="c7a8d-153">Pakiet o identyfikatorze podana i wersji już istnieje.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="c7a8d-154">Implementacje serwera różnią się od kod stanu Powodzenie zwracany, gdy pakiet zostanie pomyślnie przeniesiona.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="c7a8d-155">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c7a8d-155">Delete a package</span></span>

<span data-ttu-id="c7a8d-156">nuget.org interpretowane jako żądanie usunięcia pakietu jako "unlist".</span><span class="sxs-lookup"><span data-stu-id="c7a8d-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="c7a8d-157">Oznacza to, że pakiet jest nadal dostępny dla istniejących konsumentów pakietu, ale pakiet nie będzie już wyświetlana w wynikach wyszukiwania lub interfejs sieci web.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="c7a8d-158">Aby uzyskać więcej informacji o tym rozwiązaniem, zobacz [usunięte pakiety](../policies/deleting-packages.md) zasad.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="c7a8d-159">Inne implementacje serwera mogą interpretować tego sygnału jako usuwania twardych, usunąć soft lub unlist.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="c7a8d-160">Na przykład [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (serwer obsługujący tylko starsze interfejsu API w wersji 2) obsługuje obsługi tego żądania jako unlist lub usuwania twardych, na podstawie opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="c7a8d-161">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="c7a8d-161">Request parameters</span></span>

<span data-ttu-id="c7a8d-162">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7a8d-162">Name</span></span>           | <span data-ttu-id="c7a8d-163">W</span><span class="sxs-lookup"><span data-stu-id="c7a8d-163">In</span></span>     | <span data-ttu-id="c7a8d-164">Typ</span><span class="sxs-lookup"><span data-stu-id="c7a8d-164">Type</span></span>   | <span data-ttu-id="c7a8d-165">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c7a8d-165">Required</span></span> | <span data-ttu-id="c7a8d-166">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c7a8d-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c7a8d-167">ID</span><span class="sxs-lookup"><span data-stu-id="c7a8d-167">ID</span></span>             | <span data-ttu-id="c7a8d-168">Adres URL</span><span class="sxs-lookup"><span data-stu-id="c7a8d-168">URL</span></span>    | <span data-ttu-id="c7a8d-169">string</span><span class="sxs-lookup"><span data-stu-id="c7a8d-169">string</span></span> | <span data-ttu-id="c7a8d-170">Tak</span><span class="sxs-lookup"><span data-stu-id="c7a8d-170">yes</span></span>      | <span data-ttu-id="c7a8d-171">Identyfikator pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="c7a8d-171">The ID of the package to delete</span></span>
<span data-ttu-id="c7a8d-172">WERSJA</span><span class="sxs-lookup"><span data-stu-id="c7a8d-172">VERSION</span></span>        | <span data-ttu-id="c7a8d-173">Adres URL</span><span class="sxs-lookup"><span data-stu-id="c7a8d-173">URL</span></span>    | <span data-ttu-id="c7a8d-174">string</span><span class="sxs-lookup"><span data-stu-id="c7a8d-174">string</span></span> | <span data-ttu-id="c7a8d-175">Tak</span><span class="sxs-lookup"><span data-stu-id="c7a8d-175">yes</span></span>      | <span data-ttu-id="c7a8d-176">Wersja pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="c7a8d-176">The version of the package to delete</span></span>
<span data-ttu-id="c7a8d-177">ApiKey-X-NuGet</span><span class="sxs-lookup"><span data-stu-id="c7a8d-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="c7a8d-178">nagłówek</span><span class="sxs-lookup"><span data-stu-id="c7a8d-178">Header</span></span> | <span data-ttu-id="c7a8d-179">string</span><span class="sxs-lookup"><span data-stu-id="c7a8d-179">string</span></span> | <span data-ttu-id="c7a8d-180">Tak</span><span class="sxs-lookup"><span data-stu-id="c7a8d-180">yes</span></span>      | <span data-ttu-id="c7a8d-181">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="c7a8d-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="c7a8d-182">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c7a8d-182">Response</span></span>

<span data-ttu-id="c7a8d-183">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="c7a8d-183">Status Code</span></span> | <span data-ttu-id="c7a8d-184">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="c7a8d-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="c7a8d-185">204</span><span class="sxs-lookup"><span data-stu-id="c7a8d-185">204</span></span>         | <span data-ttu-id="c7a8d-186">Pakiet został usunięty.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-186">The package was deleted</span></span>
<span data-ttu-id="c7a8d-187">404</span><span class="sxs-lookup"><span data-stu-id="c7a8d-187">404</span></span>         | <span data-ttu-id="c7a8d-188">Nie pakietu z dostarczonych `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="c7a8d-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="c7a8d-189">Wystaw ponownie pakietu</span><span class="sxs-lookup"><span data-stu-id="c7a8d-189">Relist a package</span></span>

<span data-ttu-id="c7a8d-190">Jeśli pakiet jest nieznajdujące się na liście, istnieje możliwość ponownie wyświetlić tego pakietu w wynikach wyszukiwania przy użyciu punktu końcowego "Wystaw ponownie".</span><span class="sxs-lookup"><span data-stu-id="c7a8d-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="c7a8d-191">Ten punkt końcowy ma ten sam kształt co [usunąć (unlist) punktu końcowego](#delete-a-package) , ale `POST` HTTP zamiast metody `DELETE` metody.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="c7a8d-192">Jeśli pakiet jest już na liście, żądanie nadal powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="c7a8d-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="c7a8d-193">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="c7a8d-193">Request parameters</span></span>

<span data-ttu-id="c7a8d-194">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7a8d-194">Name</span></span>           | <span data-ttu-id="c7a8d-195">W</span><span class="sxs-lookup"><span data-stu-id="c7a8d-195">In</span></span>     | <span data-ttu-id="c7a8d-196">Typ</span><span class="sxs-lookup"><span data-stu-id="c7a8d-196">Type</span></span>   | <span data-ttu-id="c7a8d-197">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c7a8d-197">Required</span></span> | <span data-ttu-id="c7a8d-198">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c7a8d-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c7a8d-199">ID</span><span class="sxs-lookup"><span data-stu-id="c7a8d-199">ID</span></span>             | <span data-ttu-id="c7a8d-200">Adres URL</span><span class="sxs-lookup"><span data-stu-id="c7a8d-200">URL</span></span>    | <span data-ttu-id="c7a8d-201">string</span><span class="sxs-lookup"><span data-stu-id="c7a8d-201">string</span></span> | <span data-ttu-id="c7a8d-202">Tak</span><span class="sxs-lookup"><span data-stu-id="c7a8d-202">yes</span></span>      | <span data-ttu-id="c7a8d-203">Identyfikator pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="c7a8d-203">The ID of the package to relist</span></span>
<span data-ttu-id="c7a8d-204">WERSJA</span><span class="sxs-lookup"><span data-stu-id="c7a8d-204">VERSION</span></span>        | <span data-ttu-id="c7a8d-205">Adres URL</span><span class="sxs-lookup"><span data-stu-id="c7a8d-205">URL</span></span>    | <span data-ttu-id="c7a8d-206">string</span><span class="sxs-lookup"><span data-stu-id="c7a8d-206">string</span></span> | <span data-ttu-id="c7a8d-207">Tak</span><span class="sxs-lookup"><span data-stu-id="c7a8d-207">yes</span></span>      | <span data-ttu-id="c7a8d-208">Wersja pakietu do ponownego wystawienia</span><span class="sxs-lookup"><span data-stu-id="c7a8d-208">The version of the package to relist</span></span>
<span data-ttu-id="c7a8d-209">ApiKey-X-NuGet</span><span class="sxs-lookup"><span data-stu-id="c7a8d-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="c7a8d-210">nagłówek</span><span class="sxs-lookup"><span data-stu-id="c7a8d-210">Header</span></span> | <span data-ttu-id="c7a8d-211">string</span><span class="sxs-lookup"><span data-stu-id="c7a8d-211">string</span></span> | <span data-ttu-id="c7a8d-212">Tak</span><span class="sxs-lookup"><span data-stu-id="c7a8d-212">yes</span></span>      | <span data-ttu-id="c7a8d-213">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="c7a8d-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="c7a8d-214">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c7a8d-214">Response</span></span>

<span data-ttu-id="c7a8d-215">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="c7a8d-215">Status Code</span></span> | <span data-ttu-id="c7a8d-216">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="c7a8d-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="c7a8d-217">204</span><span class="sxs-lookup"><span data-stu-id="c7a8d-217">204</span></span>         | <span data-ttu-id="c7a8d-218">Pakiet zostanie wyświetlony</span><span class="sxs-lookup"><span data-stu-id="c7a8d-218">The package is now listed</span></span>
<span data-ttu-id="c7a8d-219">404</span><span class="sxs-lookup"><span data-stu-id="c7a8d-219">404</span></span>         | <span data-ttu-id="c7a8d-220">Nie pakietu z dostarczonych `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="c7a8d-220">No package with the provided `ID` and `VERSION` exists</span></span>
