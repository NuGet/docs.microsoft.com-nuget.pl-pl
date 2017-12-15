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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="4d70c-104">Wypychanie i usuwania</span><span class="sxs-lookup"><span data-stu-id="4d70c-104">Push and Delete</span></span>

<span data-ttu-id="4d70c-105">Istnieje możliwość wypychania i usunąć (lub unlist, w zależności od implementacji serwera) pakietów przy użyciu interfejsu API w wersji 3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d70c-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="4d70c-106">Obie operacje są oparte na off z `PackagePublish` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4d70c-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="4d70c-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="4d70c-107">Versioning</span></span>

<span data-ttu-id="4d70c-108">Następujące `@type` jest używana wartość:</span><span class="sxs-lookup"><span data-stu-id="4d70c-108">The following `@type` value is used:</span></span>

<span data-ttu-id="4d70c-109">@typewartość</span><span class="sxs-lookup"><span data-stu-id="4d70c-109">@type value</span></span>          | <span data-ttu-id="4d70c-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4d70c-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="4d70c-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="4d70c-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="4d70c-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="4d70c-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="4d70c-113">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="4d70c-113">Base URL</span></span>

<span data-ttu-id="4d70c-114">Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `PackagePublish/2.0.0` zasobów w źródle pakietów [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4d70c-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="4d70c-115">Poniżej dokumentację nuget.org adres URL jest używany.</span><span class="sxs-lookup"><span data-stu-id="4d70c-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="4d70c-116">Należy wziąć pod uwagę `https://www.nuget.org/api/v2/package` jako symbol zastępczy `@id` wartość znajduje się w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="4d70c-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="4d70c-117">Należy pamiętać, że ten adres URL wskazuje do tej samej lokalizacji co starszego punktu końcowego wypychania V2, ponieważ protokół jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="4d70c-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4d70c-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="4d70c-118">HTTP methods</span></span>

<span data-ttu-id="4d70c-119">`PUT` i `DELETE` metod HTTP obsługiwanych przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="4d70c-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="4d70c-120">Dla metod, które są obsługiwane na każdym punkcie końcowym są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="4d70c-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="4d70c-121">Wypychanie pakietu</span><span class="sxs-lookup"><span data-stu-id="4d70c-121">Push a package</span></span>

<span data-ttu-id="4d70c-122">nuget.org obsługuje położenia nowe pakiety przy użyciu następujących interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4d70c-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="4d70c-123">Jeśli pakiet o identyfikatorze podana i wersji już istnieje, nuget.org spowoduje odrzucenie powiadomienia wypychanego.</span><span class="sxs-lookup"><span data-stu-id="4d70c-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="4d70c-124">Inne źródła pakietu może obsługiwać, zastępując istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="4d70c-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="4d70c-125">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="4d70c-125">Request parameters</span></span>

<span data-ttu-id="4d70c-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4d70c-126">Name</span></span>           | <span data-ttu-id="4d70c-127">W</span><span class="sxs-lookup"><span data-stu-id="4d70c-127">In</span></span>     | <span data-ttu-id="4d70c-128">Typ</span><span class="sxs-lookup"><span data-stu-id="4d70c-128">Type</span></span>   | <span data-ttu-id="4d70c-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4d70c-129">Required</span></span> | <span data-ttu-id="4d70c-130">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4d70c-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="4d70c-131">ApiKey-X-NuGet</span><span class="sxs-lookup"><span data-stu-id="4d70c-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="4d70c-132">nagłówek</span><span class="sxs-lookup"><span data-stu-id="4d70c-132">Header</span></span> | <span data-ttu-id="4d70c-133">string</span><span class="sxs-lookup"><span data-stu-id="4d70c-133">string</span></span> | <span data-ttu-id="4d70c-134">Tak</span><span class="sxs-lookup"><span data-stu-id="4d70c-134">yes</span></span>      | <span data-ttu-id="4d70c-135">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="4d70c-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="4d70c-136">Klucz interfejsu API jest ciąg z ogólnym opisem zaakceptujesz ze źródła pakietów przez użytkownika i skonfigurowane do klienta.</span><span class="sxs-lookup"><span data-stu-id="4d70c-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="4d70c-137">Nie określony ciąg formatu jest obowiązkowe, ale długość klucza interfejsu API nie może przekraczać uzasadnione rozmiaru dla wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="4d70c-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="4d70c-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4d70c-138">Request body</span></span>

<span data-ttu-id="4d70c-139">Treść żądania musi występować w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="4d70c-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="4d70c-140">Wieloczęściowych danych formularza</span><span class="sxs-lookup"><span data-stu-id="4d70c-140">Multipart form data</span></span>

<span data-ttu-id="4d70c-141">Nagłówek żądania `Content-Type` jest `multipart/form-data` i raw bajtów .nupkg przekazywanej pierwszego elementu w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="4d70c-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="4d70c-142">Kolejne elementy treści wieloczęściowej wiadomości są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="4d70c-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="4d70c-143">Nazwa pliku lub inne nagłówki elementów wieloczęściowego są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="4d70c-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="4d70c-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4d70c-144">Response</span></span>

<span data-ttu-id="4d70c-145">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="4d70c-145">Status Code</span></span> | <span data-ttu-id="4d70c-146">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="4d70c-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="4d70c-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="4d70c-147">201, 202</span></span>    | <span data-ttu-id="4d70c-148">Pakiet został pomyślnie przypisany.</span><span class="sxs-lookup"><span data-stu-id="4d70c-148">The package was successfully pushed</span></span>
<span data-ttu-id="4d70c-149">400</span><span class="sxs-lookup"><span data-stu-id="4d70c-149">400</span></span>         | <span data-ttu-id="4d70c-150">Podany pakiet jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="4d70c-150">The provided package is invalid</span></span>
<span data-ttu-id="4d70c-151">409</span><span class="sxs-lookup"><span data-stu-id="4d70c-151">409</span></span>         | <span data-ttu-id="4d70c-152">Pakiet o identyfikatorze podana i wersji już istnieje.</span><span class="sxs-lookup"><span data-stu-id="4d70c-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="4d70c-153">Implementacje serwera różnią się od kod stanu Powodzenie zwracany, gdy pakiet zostanie pomyślnie przeniesiona.</span><span class="sxs-lookup"><span data-stu-id="4d70c-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="4d70c-154">Usuwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="4d70c-154">Delete a package</span></span>

<span data-ttu-id="4d70c-155">nuget.org interpretowane jako żądanie usunięcia pakietu jako "unlist".</span><span class="sxs-lookup"><span data-stu-id="4d70c-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="4d70c-156">Oznacza to, że pakiet jest nadal dostępny dla istniejących konsumentów pakietu, ale pakiet nie będzie już wyświetlana w wynikach wyszukiwania lub interfejs sieci web.</span><span class="sxs-lookup"><span data-stu-id="4d70c-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="4d70c-157">Aby uzyskać więcej informacji o tym rozwiązaniem, zobacz [usunięte pakiety](../policies/deleting-packages.md) zasad.</span><span class="sxs-lookup"><span data-stu-id="4d70c-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="4d70c-158">Inne implementacje serwera mogą interpretować tego sygnału jako usuwania twardych, usunąć soft lub unlist.</span><span class="sxs-lookup"><span data-stu-id="4d70c-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="4d70c-159">Na przykład [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (serwer obsługujący tylko starsze interfejsu API w wersji 2) obsługuje obsługi tego żądania jako unlist lub usuwania twardych, na podstawie opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4d70c-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="4d70c-160">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="4d70c-160">Request parameters</span></span>

<span data-ttu-id="4d70c-161">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4d70c-161">Name</span></span>           | <span data-ttu-id="4d70c-162">W</span><span class="sxs-lookup"><span data-stu-id="4d70c-162">In</span></span>     | <span data-ttu-id="4d70c-163">Typ</span><span class="sxs-lookup"><span data-stu-id="4d70c-163">Type</span></span>   | <span data-ttu-id="4d70c-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4d70c-164">Required</span></span> | <span data-ttu-id="4d70c-165">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4d70c-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="4d70c-166">ID</span><span class="sxs-lookup"><span data-stu-id="4d70c-166">ID</span></span>             | <span data-ttu-id="4d70c-167">Adres URL</span><span class="sxs-lookup"><span data-stu-id="4d70c-167">URL</span></span>    | <span data-ttu-id="4d70c-168">string</span><span class="sxs-lookup"><span data-stu-id="4d70c-168">string</span></span> | <span data-ttu-id="4d70c-169">Tak</span><span class="sxs-lookup"><span data-stu-id="4d70c-169">yes</span></span>      | <span data-ttu-id="4d70c-170">Identyfikator pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="4d70c-170">The ID of the package to delete</span></span>
<span data-ttu-id="4d70c-171">WERSJA</span><span class="sxs-lookup"><span data-stu-id="4d70c-171">VERSION</span></span>        | <span data-ttu-id="4d70c-172">Adres URL</span><span class="sxs-lookup"><span data-stu-id="4d70c-172">URL</span></span>    | <span data-ttu-id="4d70c-173">string</span><span class="sxs-lookup"><span data-stu-id="4d70c-173">string</span></span> | <span data-ttu-id="4d70c-174">Tak</span><span class="sxs-lookup"><span data-stu-id="4d70c-174">yes</span></span>      | <span data-ttu-id="4d70c-175">Wersja pakietu do usunięcia</span><span class="sxs-lookup"><span data-stu-id="4d70c-175">The version of the package to delete</span></span>
<span data-ttu-id="4d70c-176">ApiKey-X-NuGet</span><span class="sxs-lookup"><span data-stu-id="4d70c-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="4d70c-177">nagłówek</span><span class="sxs-lookup"><span data-stu-id="4d70c-177">Header</span></span> | <span data-ttu-id="4d70c-178">string</span><span class="sxs-lookup"><span data-stu-id="4d70c-178">string</span></span> | <span data-ttu-id="4d70c-179">Tak</span><span class="sxs-lookup"><span data-stu-id="4d70c-179">yes</span></span>      | <span data-ttu-id="4d70c-180">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="4d70c-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="4d70c-181">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4d70c-181">Response</span></span>

<span data-ttu-id="4d70c-182">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="4d70c-182">Status Code</span></span> | <span data-ttu-id="4d70c-183">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="4d70c-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="4d70c-184">204</span><span class="sxs-lookup"><span data-stu-id="4d70c-184">204</span></span>         | <span data-ttu-id="4d70c-185">Pakiet został usunięty.</span><span class="sxs-lookup"><span data-stu-id="4d70c-185">The package was deleted</span></span>
<span data-ttu-id="4d70c-186">404</span><span class="sxs-lookup"><span data-stu-id="4d70c-186">404</span></span>         | <span data-ttu-id="4d70c-187">Nie pakietu z dostarczonych `ID` i `VERSION` istnieje</span><span class="sxs-lookup"><span data-stu-id="4d70c-187">No package with the provided `ID` and `VERSION` exists</span></span>
