---
title: Wypychanie pakiety symboli, interfejs API programu NuGet | Dokumentacja firmy Microsoft
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Usługa publikowania pozwala klientom Opublikuj nowe pakiety symboli.
keywords: Pakiet programu NuGet interfejsu API wypychania symboli
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580453"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="24daa-104">Pakiety symboli wypychania</span><span class="sxs-lookup"><span data-stu-id="24daa-104">Push Symbol Packages</span></span>

<span data-ttu-id="24daa-105">Istnieje możliwość wypychania symbole pakietów ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) przy użyciu interfejsu API programu NuGet w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="24daa-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="24daa-106">Te operacje opierają się wylogować się z `SymbolPackagePublish` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="24daa-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="24daa-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="24daa-107">Versioning</span></span>

<span data-ttu-id="24daa-108">Następujące `@type` zostanie użyta wartość:</span><span class="sxs-lookup"><span data-stu-id="24daa-108">The following `@type` value is used:</span></span>

<span data-ttu-id="24daa-109">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="24daa-109">@type value</span></span>                 | <span data-ttu-id="24daa-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="24daa-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="24daa-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="24daa-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="24daa-112">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="24daa-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="24daa-113">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="24daa-113">Base URL</span></span>

<span data-ttu-id="24daa-114">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `SymbolPackagePublish/4.9.0` zasobów w źródle pakietu [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="24daa-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="24daa-115">Poniższą dokumentacją używany jest adres URL usługi nuget.org.</span><span class="sxs-lookup"><span data-stu-id="24daa-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="24daa-116">Należy wziąć pod uwagę `https://www.nuget.org/api/v2/symbolpackage` jako symbol zastępczy `@id` znaleziono wartości w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="24daa-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="24daa-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="24daa-117">HTTP methods</span></span>

<span data-ttu-id="24daa-118">`PUT` Metoda HTTP jest obsługiwana przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="24daa-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="24daa-119">Wypychanie pakiet symboli</span><span class="sxs-lookup"><span data-stu-id="24daa-119">Push a symbol package</span></span>

<span data-ttu-id="24daa-120">nuget.org obsługuje wypychania nowego formatu pakiety symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) przy użyciu następujących interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="24daa-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="24daa-121">Pakiety symboli o tym samym identyfikatorze i wersji można złożyć wiele razy.</span><span class="sxs-lookup"><span data-stu-id="24daa-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="24daa-122">Pakiet symboli, zostanie odrzucone w następujących przypadkach.</span><span class="sxs-lookup"><span data-stu-id="24daa-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="24daa-123">Pakiet o tej samej wersji i identyfikator nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="24daa-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="24daa-124">Pakiet symboli, o tym samym identyfikatorze i wersji został wypchnięty, ale nie został jeszcze opublikowany.</span><span class="sxs-lookup"><span data-stu-id="24daa-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="24daa-125">Pakiet symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) jest nieprawidłowy (zobacz [symboli ograniczenia pakietu](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="24daa-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="24daa-126">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="24daa-126">Request parameters</span></span>

<span data-ttu-id="24daa-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="24daa-127">Name</span></span>           | <span data-ttu-id="24daa-128">W</span><span class="sxs-lookup"><span data-stu-id="24daa-128">In</span></span>     | <span data-ttu-id="24daa-129">Typ</span><span class="sxs-lookup"><span data-stu-id="24daa-129">Type</span></span>   | <span data-ttu-id="24daa-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="24daa-130">Required</span></span> | <span data-ttu-id="24daa-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="24daa-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="24daa-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="24daa-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="24daa-133">nagłówek</span><span class="sxs-lookup"><span data-stu-id="24daa-133">Header</span></span> | <span data-ttu-id="24daa-134">string</span><span class="sxs-lookup"><span data-stu-id="24daa-134">string</span></span> | <span data-ttu-id="24daa-135">Tak</span><span class="sxs-lookup"><span data-stu-id="24daa-135">yes</span></span>      | <span data-ttu-id="24daa-136">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="24daa-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="24daa-137">Klucz interfejsu API to nieprzezroczysty ciąg uzyskane ze źródła pakietu przez użytkownika i skonfigurowane do klienta.</span><span class="sxs-lookup"><span data-stu-id="24daa-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="24daa-138">Nie określonego ciągu formatu jest upoważnione, ale długość klucza interfejsu API nie może przekraczać rozmiaru uzasadnione wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="24daa-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="24daa-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="24daa-139">Request body</span></span>

<span data-ttu-id="24daa-140">Treść żądania do wypychania symboli jest taka sama jak z treści żądania wypychanej pakietu (zobacz [wypychania pakietów i usuwania](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="24daa-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="24daa-141">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="24daa-141">Response</span></span>

<span data-ttu-id="24daa-142">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="24daa-142">Status Code</span></span> | <span data-ttu-id="24daa-143">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="24daa-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="24daa-144">201</span><span class="sxs-lookup"><span data-stu-id="24daa-144">201</span></span>         | <span data-ttu-id="24daa-145">Pakiet symboli pomyślnie został wypchnięty.</span><span class="sxs-lookup"><span data-stu-id="24daa-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="24daa-146">400</span><span class="sxs-lookup"><span data-stu-id="24daa-146">400</span></span>         | <span data-ttu-id="24daa-147">Pakiet podana symboli jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="24daa-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="24daa-148">401</span><span class="sxs-lookup"><span data-stu-id="24daa-148">401</span></span>         | <span data-ttu-id="24daa-149">Użytkownik nie ma uprawnień do wykonania tej akcji.</span><span class="sxs-lookup"><span data-stu-id="24daa-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="24daa-150">404</span><span class="sxs-lookup"><span data-stu-id="24daa-150">404</span></span>         | <span data-ttu-id="24daa-151">Nie ma odpowiedniego pakietu o identyfikatorze podana i wersji.</span><span class="sxs-lookup"><span data-stu-id="24daa-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="24daa-152">409</span><span class="sxs-lookup"><span data-stu-id="24daa-152">409</span></span>         | <span data-ttu-id="24daa-153">Pakiet symboli z podanego Identyfikatora i wersją został wypchnięty, ale go nie jest jeszcze dostępna.</span><span class="sxs-lookup"><span data-stu-id="24daa-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="24daa-154">413</span><span class="sxs-lookup"><span data-stu-id="24daa-154">413</span></span>         | <span data-ttu-id="24daa-155">Pakiet jest zbyt duży.</span><span class="sxs-lookup"><span data-stu-id="24daa-155">The package is too large.</span></span>

