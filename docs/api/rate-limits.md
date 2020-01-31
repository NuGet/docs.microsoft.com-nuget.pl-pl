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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813198"
---
# <a name="rate-limits"></a><span data-ttu-id="c5540-103">Limity szybkości</span><span class="sxs-lookup"><span data-stu-id="c5540-103">Rate Limits</span></span>

<span data-ttu-id="c5540-104">Interfejs API NuGet.org wymusza ograniczenie szybkości, aby zapobiec nadużyciu.</span><span class="sxs-lookup"><span data-stu-id="c5540-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="c5540-105">Żądania, które przekraczają limit szybkości, zwracają następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="c5540-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="c5540-106">Oprócz ograniczania żądań przy użyciu limitów szybkości niektóre interfejsy API wymuszają również przydział.</span><span class="sxs-lookup"><span data-stu-id="c5540-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="c5540-107">Żądania, które przekraczają limit przydziału, zwracają następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="c5540-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="c5540-108">W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c5540-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="c5540-109">Wyszukiwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="c5540-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="c5540-110">Zalecamy używanie NuGet. [interfejsy API wyszukiwania](search-query-service-resource.md) w wersji 3 w organizacji nie są obecnie ograniczone.</span><span class="sxs-lookup"><span data-stu-id="c5540-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="c5540-111">W przypadku interfejsów API wyszukiwania w wersji 1 i v2 obowiązują następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="c5540-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="c5540-112">interfejs API</span><span class="sxs-lookup"><span data-stu-id="c5540-112">API</span></span> | <span data-ttu-id="c5540-113">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="c5540-113">Limit Type</span></span> | <span data-ttu-id="c5540-114">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="c5540-114">Limit Value</span></span> | <span data-ttu-id="c5540-115">Interfejs API UseCase</span><span class="sxs-lookup"><span data-stu-id="c5540-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="c5540-116">**Pobierz** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="c5540-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="c5540-117">adres IP</span><span class="sxs-lookup"><span data-stu-id="c5540-117">IP</span></span> | <span data-ttu-id="c5540-118">1000/minutę</span><span class="sxs-lookup"><span data-stu-id="c5540-118">1000 / minute</span></span> | <span data-ttu-id="c5540-119">Wysyłanie zapytań dotyczących metadanych pakietów NuGet za pośrednictwem usługi `Packages` OData w wersji 1</span><span class="sxs-lookup"><span data-stu-id="c5540-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="c5540-120">**Pobierz** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="c5540-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="c5540-121">adres IP</span><span class="sxs-lookup"><span data-stu-id="c5540-121">IP</span></span> | <span data-ttu-id="c5540-122">3000/minutę</span><span class="sxs-lookup"><span data-stu-id="c5540-122">3000 / minute</span></span> | <span data-ttu-id="c5540-123">Wyszukaj pakiety NuGet za pomocą punktu końcowego wyszukiwania v1</span><span class="sxs-lookup"><span data-stu-id="c5540-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="c5540-124">**Pobierz** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="c5540-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="c5540-125">adres IP</span><span class="sxs-lookup"><span data-stu-id="c5540-125">IP</span></span> | <span data-ttu-id="c5540-126">20000/minutę</span><span class="sxs-lookup"><span data-stu-id="c5540-126">20000 / minute</span></span> | <span data-ttu-id="c5540-127">Wysyłanie zapytań dotyczących metadanych pakietów NuGet za pośrednictwem protokołu OData w wersji 2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="c5540-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="c5540-128">**Pobierz** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="c5540-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="c5540-129">adres IP</span><span class="sxs-lookup"><span data-stu-id="c5540-129">IP</span></span> | <span data-ttu-id="c5540-130">100/minutę</span><span class="sxs-lookup"><span data-stu-id="c5540-130">100 / minute</span></span> | <span data-ttu-id="c5540-131">Wykonaj zapytania o liczbę pakietów NuGet za pośrednictwem protokołu OData w wersji 2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="c5540-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="c5540-132">Wypychanie pakietów i wylistowanie</span><span class="sxs-lookup"><span data-stu-id="c5540-132">Package Push and Unlist</span></span>

| <span data-ttu-id="c5540-133">interfejs API</span><span class="sxs-lookup"><span data-stu-id="c5540-133">API</span></span> | <span data-ttu-id="c5540-134">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="c5540-134">Limit Type</span></span> | <span data-ttu-id="c5540-135">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="c5540-135">Limit Value</span></span> | <span data-ttu-id="c5540-136">Interfejs API UseCase</span><span class="sxs-lookup"><span data-stu-id="c5540-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c5540-137">**Umieść** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="c5540-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="c5540-138">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c5540-138">API Key</span></span> | <span data-ttu-id="c5540-139">350 za godzinę</span><span class="sxs-lookup"><span data-stu-id="c5540-139">350 / hour</span></span> | <span data-ttu-id="c5540-140">Przekaż nowy pakiet NuGet (wersja) za pośrednictwem protokołu Endpoint push w wersji 2</span><span class="sxs-lookup"><span data-stu-id="c5540-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="c5540-141">**Usuń** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c5540-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="c5540-142">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c5540-142">API Key</span></span> | <span data-ttu-id="c5540-143">250 za godzinę</span><span class="sxs-lookup"><span data-stu-id="c5540-143">250 / hour</span></span> | <span data-ttu-id="c5540-144">Wylistowanie pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2</span><span class="sxs-lookup"><span data-stu-id="c5540-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
