---
title: Limity, interfejs API programu NuGet szybkości
description: Interfejsy API NuGet zostanie wymusić limity szybkości, aby zapobiec nadużyciu.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548680"
---
# <a name="rate-limits"></a><span data-ttu-id="ee115-103">Limity szybkości</span><span class="sxs-lookup"><span data-stu-id="ee115-103">Rate Limits</span></span>

<span data-ttu-id="ee115-104">Interfejs API NuGet.org wymusza, ograniczania szybkości, aby zapobiec nadużyciu.</span><span class="sxs-lookup"><span data-stu-id="ee115-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="ee115-105">Żądania, które przekraczają limit szybkości zwrócenie następującego błędu:</span><span class="sxs-lookup"><span data-stu-id="ee115-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="ee115-106">Oprócz ograniczania, przy użyciu ograniczeń liczby wywołań żądań niektóre interfejsy API wymuszania limitu przydziału.</span><span class="sxs-lookup"><span data-stu-id="ee115-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="ee115-107">Żądania, które przekraczają limit przydziału zwrócenie następującego błędu:</span><span class="sxs-lookup"><span data-stu-id="ee115-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="ee115-108">W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ee115-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="ee115-109">Wyszukiwanie pakietu</span><span class="sxs-lookup"><span data-stu-id="ee115-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="ee115-110">Firma Microsoft zaleca używanie usługi NuGet.org [interfejsów API w wersji 3](https://docs.microsoft.com/nuget/api/search-query-service-resource) wyszukiwania, które są wydajne i nie ma żadnych obecnie ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="ee115-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="ee115-111">Aby V1 i V2 Wyszukaj interfejsów API, limity followins mają zastosowanie:</span><span class="sxs-lookup"><span data-stu-id="ee115-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="ee115-112">interfejs API</span><span class="sxs-lookup"><span data-stu-id="ee115-112">API</span></span> | <span data-ttu-id="ee115-113">Typ ograniczenia</span><span class="sxs-lookup"><span data-stu-id="ee115-113">Limit Type</span></span> | <span data-ttu-id="ee115-114">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="ee115-114">Limit Value</span></span> | <span data-ttu-id="ee115-115">Usecase interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ee115-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="ee115-116">**POBIERZ** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="ee115-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="ee115-117">IP</span><span class="sxs-lookup"><span data-stu-id="ee115-117">IP</span></span> | <span data-ttu-id="ee115-118">1000 / minutę</span><span class="sxs-lookup"><span data-stu-id="ee115-118">1000 / minute</span></span> | <span data-ttu-id="ee115-119">Zapytanie metadanych pakietu NuGet za pomocą protokołu OData v1 `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="ee115-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="ee115-120">**POBIERZ** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="ee115-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="ee115-121">IP</span><span class="sxs-lookup"><span data-stu-id="ee115-121">IP</span></span> | <span data-ttu-id="ee115-122">3000 / minutę</span><span class="sxs-lookup"><span data-stu-id="ee115-122">3000 / minute</span></span> | <span data-ttu-id="ee115-123">Wyszukaj pakiety NuGet, za pośrednictwem punktu końcowego wyszukiwania 1</span><span class="sxs-lookup"><span data-stu-id="ee115-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="ee115-124">**POBIERZ** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="ee115-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="ee115-125">IP</span><span class="sxs-lookup"><span data-stu-id="ee115-125">IP</span></span> | <span data-ttu-id="ee115-126">20000 / minutę</span><span class="sxs-lookup"><span data-stu-id="ee115-126">20000 / minute</span></span> | <span data-ttu-id="ee115-127">Zapytanie metadanych pakietu NuGet za pośrednictwem usługi OData w wersji 2 `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="ee115-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="ee115-128">**POBIERZ** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="ee115-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="ee115-129">IP</span><span class="sxs-lookup"><span data-stu-id="ee115-129">IP</span></span> | <span data-ttu-id="ee115-130">100 / minutę</span><span class="sxs-lookup"><span data-stu-id="ee115-130">100 / minute</span></span> | <span data-ttu-id="ee115-131">Liczba pakietów NuGet za pośrednictwem usługi OData w wersji 2 zapytań `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="ee115-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="ee115-132">Pakiet wypychania i wyrejestrowanie</span><span class="sxs-lookup"><span data-stu-id="ee115-132">Package Push and Unlist</span></span>

| <span data-ttu-id="ee115-133">interfejs API</span><span class="sxs-lookup"><span data-stu-id="ee115-133">API</span></span> | <span data-ttu-id="ee115-134">Typ ograniczenia</span><span class="sxs-lookup"><span data-stu-id="ee115-134">Limit Type</span></span> | <span data-ttu-id="ee115-135">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="ee115-135">Limit Value</span></span> | <span data-ttu-id="ee115-136">Usecase interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ee115-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="ee115-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="ee115-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="ee115-138">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ee115-138">API Key</span></span> | <span data-ttu-id="ee115-139">250 / godzinę</span><span class="sxs-lookup"><span data-stu-id="ee115-139">250 / hour</span></span> | <span data-ttu-id="ee115-140">Przekazywanie nowego pakietu NuGet (wersja) za pośrednictwem punktu końcowego wypychania v2</span><span class="sxs-lookup"><span data-stu-id="ee115-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="ee115-141">**USUŃ** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="ee115-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="ee115-142">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ee115-142">API Key</span></span> | <span data-ttu-id="ee115-143">250 / godzinę</span><span class="sxs-lookup"><span data-stu-id="ee115-143">250 / hour</span></span> | <span data-ttu-id="ee115-144">Wyrejestrowanie pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2</span><span class="sxs-lookup"><span data-stu-id="ee115-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
