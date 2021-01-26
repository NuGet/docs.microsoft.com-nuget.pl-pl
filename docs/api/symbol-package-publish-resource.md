---
title: Pakiety symboli wypychania, interfejs API NuGet | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Usługa publikowania pozwala klientom publikować nowe pakiety symboli.
keywords: Pakiet symboli wypychanych interfejsu API NuGet
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773900"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="7301a-104">Pakiety symboli wypychania</span><span class="sxs-lookup"><span data-stu-id="7301a-104">Push Symbol Packages</span></span>

<span data-ttu-id="7301a-105">Można wypchnąć pakiety symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) za pomocą interfejsu API programu NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="7301a-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="7301a-106">Operacje te są oparte na `SymbolPackagePublish` zasobach znalezionych w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7301a-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7301a-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="7301a-107">Versioning</span></span>

<span data-ttu-id="7301a-108">`@type`Używana jest następująca wartość:</span><span class="sxs-lookup"><span data-stu-id="7301a-108">The following `@type` value is used:</span></span>

<span data-ttu-id="7301a-109">@type wartościami</span><span class="sxs-lookup"><span data-stu-id="7301a-109">@type value</span></span>                 | <span data-ttu-id="7301a-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7301a-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="7301a-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="7301a-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="7301a-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="7301a-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="7301a-113">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="7301a-113">Base URL</span></span>

<span data-ttu-id="7301a-114">Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości `SymbolPackagePublish/4.9.0` zasobu w [indeksie usługi](service-index.md)źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="7301a-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="7301a-115">W poniższej dokumentacji znajduje się adres URL programu NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="7301a-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="7301a-116">Rozważmy `https://www.nuget.org/api/v2/symbolpackage` jako symbol zastępczy dla `@id` wartości znalezionej w indeksie usługi.</span><span class="sxs-lookup"><span data-stu-id="7301a-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7301a-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="7301a-117">HTTP methods</span></span>

<span data-ttu-id="7301a-118">`PUT`Metoda http jest obsługiwana przez ten zasób.</span><span class="sxs-lookup"><span data-stu-id="7301a-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="7301a-119">Wypchnij pakiet symboli</span><span class="sxs-lookup"><span data-stu-id="7301a-119">Push a symbol package</span></span>

<span data-ttu-id="7301a-120">nuget.org obsługuje wypychanie nowych formatów symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) przy użyciu poniższego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="7301a-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

<span data-ttu-id="7301a-121">Pakiety symboli o takim samym IDENTYFIKATORze i wersji mogą być przesyłane wiele razy.</span><span class="sxs-lookup"><span data-stu-id="7301a-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="7301a-122">Pakiet symboli zostanie odrzucony w następujących przypadkach.</span><span class="sxs-lookup"><span data-stu-id="7301a-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="7301a-123">Pakiet o takim samym IDENTYFIKATORze i wersji nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7301a-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="7301a-124">Pakiet symboli o takim samym IDENTYFIKATORze i wersji został wypchnięte, ale nie został jeszcze opublikowany.</span><span class="sxs-lookup"><span data-stu-id="7301a-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="7301a-125">Pakiet symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) jest nieprawidłowy (zobacz [ograniczenia pakietu symboli](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="7301a-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="7301a-126">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="7301a-126">Request parameters</span></span>

<span data-ttu-id="7301a-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7301a-127">Name</span></span>           | <span data-ttu-id="7301a-128">W</span><span class="sxs-lookup"><span data-stu-id="7301a-128">In</span></span>     | <span data-ttu-id="7301a-129">Typ</span><span class="sxs-lookup"><span data-stu-id="7301a-129">Type</span></span>   | <span data-ttu-id="7301a-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7301a-130">Required</span></span> | <span data-ttu-id="7301a-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7301a-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7301a-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7301a-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7301a-133">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="7301a-133">Header</span></span> | <span data-ttu-id="7301a-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="7301a-134">string</span></span> | <span data-ttu-id="7301a-135">tak</span><span class="sxs-lookup"><span data-stu-id="7301a-135">yes</span></span>      | <span data-ttu-id="7301a-136">Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="7301a-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="7301a-137">Klucz interfejsu API to nieprzezroczysty ciąg z źródła pakietu przez użytkownika i skonfigurowany na kliencie.</span><span class="sxs-lookup"><span data-stu-id="7301a-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="7301a-138">Żaden określony format ciągu nie jest dozwolony, ale długość klucza interfejsu API nie może przekroczyć rozsądnego rozmiaru wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="7301a-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="7301a-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7301a-139">Request body</span></span>

<span data-ttu-id="7301a-140">Treść żądania odnoszącego się do wypchnięcia symbol jest taka sama jak w przypadku treści żądania wypychania pakietu (zobacz [wypychanie i usuwanie pakietu](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="7301a-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="7301a-141">Reakcja</span><span class="sxs-lookup"><span data-stu-id="7301a-141">Response</span></span>

<span data-ttu-id="7301a-142">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="7301a-142">Status Code</span></span> | <span data-ttu-id="7301a-143">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="7301a-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="7301a-144">201</span><span class="sxs-lookup"><span data-stu-id="7301a-144">201</span></span>         | <span data-ttu-id="7301a-145">Pakiet symboli został pomyślnie wypchnięci.</span><span class="sxs-lookup"><span data-stu-id="7301a-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="7301a-146">400</span><span class="sxs-lookup"><span data-stu-id="7301a-146">400</span></span>         | <span data-ttu-id="7301a-147">Podany pakiet symboli jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="7301a-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="7301a-148">401</span><span class="sxs-lookup"><span data-stu-id="7301a-148">401</span></span>         | <span data-ttu-id="7301a-149">Użytkownik nie ma autoryzacji do wykonania tej akcji.</span><span class="sxs-lookup"><span data-stu-id="7301a-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="7301a-150">404</span><span class="sxs-lookup"><span data-stu-id="7301a-150">404</span></span>         | <span data-ttu-id="7301a-151">Odpowiedni pakiet o podanym IDENTYFIKATORze i wersji nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7301a-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="7301a-152">409</span><span class="sxs-lookup"><span data-stu-id="7301a-152">409</span></span>         | <span data-ttu-id="7301a-153">Pakiet symboli o podanym IDENTYFIKATORze i wersji został wypchnięte, ale nie jest jeszcze dostępny.</span><span class="sxs-lookup"><span data-stu-id="7301a-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="7301a-154">413</span><span class="sxs-lookup"><span data-stu-id="7301a-154">413</span></span>         | <span data-ttu-id="7301a-155">Pakiet jest zbyt duży.</span><span class="sxs-lookup"><span data-stu-id="7301a-155">The package is too large.</span></span>

