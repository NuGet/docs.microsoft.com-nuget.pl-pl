---
title: Pakiety symboli wypychania, interfejs API NuGet | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Usługa publikowania pozwala klientom publikować nowe pakiety symboli.
keywords: Pakiet symboli wypychanych interfejsu API NuGet
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235110"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="c7df5-104">Pakiety symboli wypychania</span><span class="sxs-lookup"><span data-stu-id="c7df5-104">Push Symbol Packages</span></span>

<span data-ttu-id="c7df5-105">Można wypchnąć pakiety symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) za pomocą interfejsu API programu NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="c7df5-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="c7df5-106">Operacje te są oparte `SymbolPackagePublish` na zasobach znalezionych w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c7df5-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c7df5-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="c7df5-107">Versioning</span></span>

<span data-ttu-id="c7df5-108">Używana jest `@type` następująca wartość:</span><span class="sxs-lookup"><span data-stu-id="c7df5-108">The following `@type` value is used:</span></span>

<span data-ttu-id="c7df5-109">@typewartościami</span><span class="sxs-lookup"><span data-stu-id="c7df5-109">@type value</span></span>                 | <span data-ttu-id="c7df5-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c7df5-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="c7df5-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="c7df5-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="c7df5-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="c7df5-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="c7df5-113">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="c7df5-113">Base URL</span></span>

<span data-ttu-id="c7df5-114">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości `SymbolPackagePublish/4.9.0` zasobu w [indeksie usługi](service-index.md)źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="c7df5-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="c7df5-115">W poniższej dokumentacji znajduje się adres URL programu NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="c7df5-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="c7df5-116">Rozważmy `https://www.nuget.org/api/v2/symbolpackage` jako symbol zastępczy `@id` dla wartości znalezionej w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="c7df5-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c7df5-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="c7df5-117">HTTP methods</span></span>

<span data-ttu-id="c7df5-118">Metoda `PUT` http jest obsługiwana przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="c7df5-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="c7df5-119">Wypchnij pakiet symboli</span><span class="sxs-lookup"><span data-stu-id="c7df5-119">Push a symbol package</span></span>

<span data-ttu-id="c7df5-120">nuget.org obsługuje wypychanie nowych formatów symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) przy użyciu poniższego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c7df5-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="c7df5-121">Pakiety symboli o takim samym IDENTYFIKATORze i wersji mogą być przesyłane wiele razy.</span><span class="sxs-lookup"><span data-stu-id="c7df5-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="c7df5-122">Pakiet symboli zostanie odrzucony w następujących przypadkach.</span><span class="sxs-lookup"><span data-stu-id="c7df5-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="c7df5-123">Pakiet o takim samym IDENTYFIKATORze i wersji nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c7df5-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="c7df5-124">Pakiet symboli o takim samym IDENTYFIKATORze i wersji został wypchnięte, ale nie został jeszcze opublikowany.</span><span class="sxs-lookup"><span data-stu-id="c7df5-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="c7df5-125">Pakiet symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) jest nieprawidłowy (zobacz [ograniczenia pakietu symboli](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="c7df5-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="c7df5-126">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="c7df5-126">Request parameters</span></span>

<span data-ttu-id="c7df5-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7df5-127">Name</span></span>           | <span data-ttu-id="c7df5-128">W</span><span class="sxs-lookup"><span data-stu-id="c7df5-128">In</span></span>     | <span data-ttu-id="c7df5-129">Typ</span><span class="sxs-lookup"><span data-stu-id="c7df5-129">Type</span></span>   | <span data-ttu-id="c7df5-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c7df5-130">Required</span></span> | <span data-ttu-id="c7df5-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c7df5-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c7df5-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="c7df5-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="c7df5-133">nagłówek</span><span class="sxs-lookup"><span data-stu-id="c7df5-133">Header</span></span> | <span data-ttu-id="c7df5-134">string</span><span class="sxs-lookup"><span data-stu-id="c7df5-134">string</span></span> | <span data-ttu-id="c7df5-135">tak</span><span class="sxs-lookup"><span data-stu-id="c7df5-135">yes</span></span>      | <span data-ttu-id="c7df5-136">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="c7df5-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="c7df5-137">Klucz interfejsu API to nieprzezroczysty ciąg z źródła pakietu przez użytkownika i skonfigurowany na kliencie.</span><span class="sxs-lookup"><span data-stu-id="c7df5-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="c7df5-138">Żaden określony format ciągu nie jest dozwolony, ale długość klucza interfejsu API nie może przekroczyć rozsądnego rozmiaru wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="c7df5-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="c7df5-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c7df5-139">Request body</span></span>

<span data-ttu-id="c7df5-140">Treść żądania odnoszącego się do wypchnięcia symbol jest taka sama jak w przypadku treści żądania wypychania pakietu (zobacz [wypychanie i usuwanie pakietu](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="c7df5-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="c7df5-141">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c7df5-141">Response</span></span>

<span data-ttu-id="c7df5-142">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="c7df5-142">Status Code</span></span> | <span data-ttu-id="c7df5-143">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="c7df5-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="c7df5-144">201</span><span class="sxs-lookup"><span data-stu-id="c7df5-144">201</span></span>         | <span data-ttu-id="c7df5-145">Pakiet symboli został pomyślnie wypchnięci.</span><span class="sxs-lookup"><span data-stu-id="c7df5-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="c7df5-146">400</span><span class="sxs-lookup"><span data-stu-id="c7df5-146">400</span></span>         | <span data-ttu-id="c7df5-147">Podany pakiet symboli jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="c7df5-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="c7df5-148">401</span><span class="sxs-lookup"><span data-stu-id="c7df5-148">401</span></span>         | <span data-ttu-id="c7df5-149">Użytkownik nie ma autoryzacji do wykonania tej akcji.</span><span class="sxs-lookup"><span data-stu-id="c7df5-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="c7df5-150">404</span><span class="sxs-lookup"><span data-stu-id="c7df5-150">404</span></span>         | <span data-ttu-id="c7df5-151">Odpowiedni pakiet o podanym IDENTYFIKATORze i wersji nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c7df5-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="c7df5-152">409</span><span class="sxs-lookup"><span data-stu-id="c7df5-152">409</span></span>         | <span data-ttu-id="c7df5-153">Pakiet symboli o podanym IDENTYFIKATORze i wersji został wypchnięte, ale nie jest jeszcze dostępny.</span><span class="sxs-lookup"><span data-stu-id="c7df5-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="c7df5-154">413</span><span class="sxs-lookup"><span data-stu-id="c7df5-154">413</span></span>         | <span data-ttu-id="c7df5-155">Pakiet jest zbyt duży.</span><span class="sxs-lookup"><span data-stu-id="c7df5-155">The package is too large.</span></span>

