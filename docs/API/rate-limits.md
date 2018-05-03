---
title: Limity, NuGet interfejsu API szybkości
description: Interfejsy API NuGet będzie wymusić limity szybkości, aby uniemożliwić nadużycia.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 3aaebef8fff670759c6484a5a8f90a2f4dd58c66
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="rate-limits"></a><span data-ttu-id="4aa77-103">Limity szybkości</span><span class="sxs-lookup"><span data-stu-id="4aa77-103">Rate Limits</span></span>

<span data-ttu-id="4aa77-104">Interfejs API NuGet.org wymusza, aby uniemożliwić nadużycia limitów szybkości.</span><span class="sxs-lookup"><span data-stu-id="4aa77-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="4aa77-105">Żądania, które przekraczają limit szybkości zwrócił następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="4aa77-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="4aa77-106">W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4aa77-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="4aa77-107">Wyszukaj pakiet</span><span class="sxs-lookup"><span data-stu-id="4aa77-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="4aa77-108">Firma Microsoft zaleca używanie NuGet.org [interfejsów API w wersji 3](https://docs.microsoft.com/nuget/api/search-query-service-resource) wyszukiwania, wydajności i nie ma żadnych obecnie ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="4aa77-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="4aa77-109">V1 i V2 wyszukiwania interfejsów API, followins ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="4aa77-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="4aa77-110">interfejs API</span><span class="sxs-lookup"><span data-stu-id="4aa77-110">API</span></span> | <span data-ttu-id="4aa77-111">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="4aa77-111">Limit Type</span></span> | <span data-ttu-id="4aa77-112">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="4aa77-112">Limit Value</span></span> | <span data-ttu-id="4aa77-113">Przypadków użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4aa77-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="4aa77-114">**POBIERZ** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="4aa77-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="4aa77-115">IP</span><span class="sxs-lookup"><span data-stu-id="4aa77-115">IP</span></span> | <span data-ttu-id="4aa77-116">1000 na minutę</span><span class="sxs-lookup"><span data-stu-id="4aa77-116">1000 / minute</span></span> | <span data-ttu-id="4aa77-117">Zapytanie metadanych pakietu NuGet za pośrednictwem v1 OData `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="4aa77-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="4aa77-118">**POBIERZ** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="4aa77-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="4aa77-119">IP</span><span class="sxs-lookup"><span data-stu-id="4aa77-119">IP</span></span> | <span data-ttu-id="4aa77-120">3000 na minutę</span><span class="sxs-lookup"><span data-stu-id="4aa77-120">3000 / minute</span></span> | <span data-ttu-id="4aa77-121">Wyszukaj pakietów NuGet za pośrednictwem punktu końcowego wyszukiwania v1</span><span class="sxs-lookup"><span data-stu-id="4aa77-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="4aa77-122">**POBIERZ** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="4aa77-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="4aa77-123">IP</span><span class="sxs-lookup"><span data-stu-id="4aa77-123">IP</span></span> | <span data-ttu-id="4aa77-124">20000 na minutę</span><span class="sxs-lookup"><span data-stu-id="4aa77-124">20000 / minute</span></span> | <span data-ttu-id="4aa77-125">Zapytanie metadanych pakietu NuGet za pośrednictwem v2 OData `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="4aa77-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="4aa77-126">**POBIERZ** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="4aa77-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="4aa77-127">IP</span><span class="sxs-lookup"><span data-stu-id="4aa77-127">IP</span></span> | <span data-ttu-id="4aa77-128">100 na minutę</span><span class="sxs-lookup"><span data-stu-id="4aa77-128">100 / minute</span></span> | <span data-ttu-id="4aa77-129">Zapytanie liczby pakietów NuGet za pośrednictwem v2 OData `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="4aa77-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="4aa77-130">Pakiet wypychania i Unlist</span><span class="sxs-lookup"><span data-stu-id="4aa77-130">Package Push and Unlist</span></span>

| <span data-ttu-id="4aa77-131">interfejs API</span><span class="sxs-lookup"><span data-stu-id="4aa77-131">API</span></span> | <span data-ttu-id="4aa77-132">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="4aa77-132">Limit Type</span></span> | <span data-ttu-id="4aa77-133">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="4aa77-133">Limit Value</span></span> | <span data-ttu-id="4aa77-134">APU przypadków użycia</span><span class="sxs-lookup"><span data-stu-id="4aa77-134">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="4aa77-135">**UMIEŚĆ** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="4aa77-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="4aa77-136">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4aa77-136">API Key</span></span> | <span data-ttu-id="4aa77-137">100 na minutę</span><span class="sxs-lookup"><span data-stu-id="4aa77-137">100 / minute</span></span> | <span data-ttu-id="4aa77-138">Przekaż nowy pakiet NuGet (wersja) za pośrednictwem punktu końcowego wypychania v2</span><span class="sxs-lookup"><span data-stu-id="4aa77-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="4aa77-139">**USUŃ** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="4aa77-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="4aa77-140">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4aa77-140">API Key</span></span> | <span data-ttu-id="4aa77-141">100 na minutę</span><span class="sxs-lookup"><span data-stu-id="4aa77-141">100 / minute</span></span> | <span data-ttu-id="4aa77-142">Unlist pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2</span><span class="sxs-lookup"><span data-stu-id="4aa77-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
