---
title: Limity szybkości, interfejs API NuGet
description: Interfejsy API NuGet będą miały wymuszone limity szybkości, aby zapobiec nadużyciu.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367937"
---
# <a name="rate-limits"></a><span data-ttu-id="e7556-103">Limity szybkości</span><span class="sxs-lookup"><span data-stu-id="e7556-103">Rate Limits</span></span>

<span data-ttu-id="e7556-104">Interfejs API NuGet.org wymusza ograniczenie szybkości, aby zapobiec nadużyciu.</span><span class="sxs-lookup"><span data-stu-id="e7556-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="e7556-105">Żądania, które przekraczają limit szybkości, zwracają następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="e7556-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="e7556-106">Oprócz ograniczania żądań przy użyciu limitów szybkości niektóre interfejsy API wymuszają również przydział.</span><span class="sxs-lookup"><span data-stu-id="e7556-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="e7556-107">Żądania, które przekraczają limit przydziału, zwracają następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="e7556-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="e7556-108">W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e7556-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="e7556-109">Wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="e7556-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="e7556-110">Zalecamy używanie NuGet. [interfejsy API wyszukiwania](search-query-service-resource.md) w wersji 3 w organizacji nie są obecnie ograniczone.</span><span class="sxs-lookup"><span data-stu-id="e7556-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="e7556-111">W przypadku interfejsów API wyszukiwania w wersji 1 i v2 obowiązują następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="e7556-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="e7556-112">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="e7556-112">API</span></span> | <span data-ttu-id="e7556-113">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="e7556-113">Limit Type</span></span> | <span data-ttu-id="e7556-114">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="e7556-114">Limit Value</span></span> | <span data-ttu-id="e7556-115">Przypadek użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e7556-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="e7556-116">**Pobierz**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="e7556-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="e7556-117">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e7556-117">IP</span></span> | <span data-ttu-id="e7556-118">1000/minutę</span><span class="sxs-lookup"><span data-stu-id="e7556-118">1000 / minute</span></span> | <span data-ttu-id="e7556-119">Wykonywanie zapytania dotyczącego metadanych pakietu NuGet za pomocą zbierania danych OData w wersji 1 `Packages`</span><span class="sxs-lookup"><span data-stu-id="e7556-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="e7556-120">**Pobierz**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="e7556-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="e7556-121">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e7556-121">IP</span></span> | <span data-ttu-id="e7556-122">3000/minutę</span><span class="sxs-lookup"><span data-stu-id="e7556-122">3000 / minute</span></span> | <span data-ttu-id="e7556-123">Wyszukaj pakiety NuGet za pomocą punktu końcowego wyszukiwania v1</span><span class="sxs-lookup"><span data-stu-id="e7556-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="e7556-124">**Pobierz**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="e7556-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="e7556-125">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e7556-125">IP</span></span> | <span data-ttu-id="e7556-126">20000/minutę</span><span class="sxs-lookup"><span data-stu-id="e7556-126">20000 / minute</span></span> | <span data-ttu-id="e7556-127">Wysyłanie zapytań dotyczących metadanych pakietów NuGet za pomocą zbierania danych OData w wersji 2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="e7556-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="e7556-128">**Pobierz**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="e7556-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="e7556-129">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e7556-129">IP</span></span> | <span data-ttu-id="e7556-130">100/minutę</span><span class="sxs-lookup"><span data-stu-id="e7556-130">100 / minute</span></span> | <span data-ttu-id="e7556-131">Wykonaj zapytania o liczbę pakietów NuGet za pomocą zbierania danych OData w wersji 2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="e7556-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="e7556-132">Wypychanie pakietów i wylistowanie</span><span class="sxs-lookup"><span data-stu-id="e7556-132">Package Push and Unlist</span></span>

| <span data-ttu-id="e7556-133">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="e7556-133">API</span></span> | <span data-ttu-id="e7556-134">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="e7556-134">Limit Type</span></span> | <span data-ttu-id="e7556-135">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="e7556-135">Limit Value</span></span> | <span data-ttu-id="e7556-136">Przypadek użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e7556-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="e7556-137">**Umieść**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="e7556-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="e7556-138">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e7556-138">API Key</span></span> | <span data-ttu-id="e7556-139">350 za godzinę</span><span class="sxs-lookup"><span data-stu-id="e7556-139">350 / hour</span></span> | <span data-ttu-id="e7556-140">Przekaż nowy pakiet NuGet (wersja) za pośrednictwem protokołu Endpoint push w wersji 2</span><span class="sxs-lookup"><span data-stu-id="e7556-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="e7556-141">**Usuń**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="e7556-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="e7556-142">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e7556-142">API Key</span></span> | <span data-ttu-id="e7556-143">250 za godzinę</span><span class="sxs-lookup"><span data-stu-id="e7556-143">250 / hour</span></span> | <span data-ttu-id="e7556-144">Wylistowanie pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2</span><span class="sxs-lookup"><span data-stu-id="e7556-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="e7556-145">nuget.org widoki stron witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="e7556-145">nuget.org website page views</span></span>

<span data-ttu-id="e7556-146">Jeśli uzyskujesz dostęp do stron sieci Web nuget.org programowo, rozważ badanie naszych udokumentowanych [interfejsów API v3](overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7556-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="e7556-147">Punkty końcowe umożliwiają łatwiejszy dostęp do metadanych i zawartości pakietu.</span><span class="sxs-lookup"><span data-stu-id="e7556-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="e7556-148">Interfejs API v3 ma lepszą dostępność i ma wyższą wydajność niż dostęp do stron sieci Web galerii NuGet, które są przeznaczone do interakcji z przeglądarką sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e7556-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="e7556-149">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="e7556-149">API</span></span> | <span data-ttu-id="e7556-150">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="e7556-150">Limit Type</span></span> | <span data-ttu-id="e7556-151">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="e7556-151">Limit Value</span></span> | <span data-ttu-id="e7556-152">Przypadek użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e7556-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="e7556-153">**Pobierz**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="e7556-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="e7556-154">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e7556-154">IP</span></span> | <span data-ttu-id="e7556-155">50/minutę</span><span class="sxs-lookup"><span data-stu-id="e7556-155">50 / minute</span></span> | <span data-ttu-id="e7556-156">Strona szczegółów pakietu wyświetlania (wersja).</span><span class="sxs-lookup"><span data-stu-id="e7556-156">Display package (version) details page.</span></span> 
