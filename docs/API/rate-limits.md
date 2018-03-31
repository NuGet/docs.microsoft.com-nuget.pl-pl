---
title: Limity szybkości | Dokumentacja firmy Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Interfejsy API NuGet będzie wymusić limity szybkości, aby uniemożliwić nadużycia.
keywords: Oceń NuGet interfejsu API, ograniczanie
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="34a25-104">Limity szybkości</span><span class="sxs-lookup"><span data-stu-id="34a25-104">Rate Limits</span></span>

<span data-ttu-id="34a25-105">Interfejs API NuGet.org wymusza, aby uniemożliwić nadużycia limitów szybkości.</span><span class="sxs-lookup"><span data-stu-id="34a25-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="34a25-106">Żądania, które przekraczają limit szybkości zwrócił następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="34a25-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="34a25-107">W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="34a25-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="34a25-108">Wyszukaj pakiet</span><span class="sxs-lookup"><span data-stu-id="34a25-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="34a25-109">Firma Microsoft zaleca używanie NuGet.org [interfejsów API w wersji 3](https://docs.microsoft.com/nuget/api/search-query-service-resource) wyszukiwania, wydajności i nie ma żadnych obecnie ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="34a25-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="34a25-110">V1 i V2 wyszukiwania interfejsów API, followins ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="34a25-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="34a25-111">interfejs API</span><span class="sxs-lookup"><span data-stu-id="34a25-111">API</span></span> | <span data-ttu-id="34a25-112">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="34a25-112">Limit Type</span></span> | <span data-ttu-id="34a25-113">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="34a25-113">Limit Value</span></span> | <span data-ttu-id="34a25-114">Przypadków użycia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="34a25-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="34a25-115">**POBIERZ** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="34a25-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="34a25-116">IP</span><span class="sxs-lookup"><span data-stu-id="34a25-116">IP</span></span> | <span data-ttu-id="34a25-117">1000 na minutę</span><span class="sxs-lookup"><span data-stu-id="34a25-117">1000 / minute</span></span> | <span data-ttu-id="34a25-118">Zapytanie metadanych pakietu NuGet za pośrednictwem v1 OData `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="34a25-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="34a25-119">**POBIERZ** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="34a25-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="34a25-120">IP</span><span class="sxs-lookup"><span data-stu-id="34a25-120">IP</span></span> | <span data-ttu-id="34a25-121">3000 na minutę</span><span class="sxs-lookup"><span data-stu-id="34a25-121">3000 / minute</span></span> | <span data-ttu-id="34a25-122">Wyszukaj pakietów NuGet za pośrednictwem punktu końcowego wyszukiwania v1</span><span class="sxs-lookup"><span data-stu-id="34a25-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="34a25-123">**POBIERZ** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="34a25-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="34a25-124">IP</span><span class="sxs-lookup"><span data-stu-id="34a25-124">IP</span></span> | <span data-ttu-id="34a25-125">20000 na minutę</span><span class="sxs-lookup"><span data-stu-id="34a25-125">20000 / minute</span></span> | <span data-ttu-id="34a25-126">Zapytanie metadanych pakietu NuGet za pośrednictwem v2 OData `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="34a25-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="34a25-127">**POBIERZ** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="34a25-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="34a25-128">IP</span><span class="sxs-lookup"><span data-stu-id="34a25-128">IP</span></span> | <span data-ttu-id="34a25-129">100 na minutę</span><span class="sxs-lookup"><span data-stu-id="34a25-129">100 / minute</span></span> | <span data-ttu-id="34a25-130">Zapytanie liczby pakietów NuGet za pośrednictwem v2 OData `Packages` kolekcji</span><span class="sxs-lookup"><span data-stu-id="34a25-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="34a25-131">Pakiet wypychania i Unlist</span><span class="sxs-lookup"><span data-stu-id="34a25-131">Package Push and Unlist</span></span>

| <span data-ttu-id="34a25-132">interfejs API</span><span class="sxs-lookup"><span data-stu-id="34a25-132">API</span></span> | <span data-ttu-id="34a25-133">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="34a25-133">Limit Type</span></span> | <span data-ttu-id="34a25-134">Wartość limitu</span><span class="sxs-lookup"><span data-stu-id="34a25-134">Limit Value</span></span> | <span data-ttu-id="34a25-135">APU przypadków użycia</span><span class="sxs-lookup"><span data-stu-id="34a25-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="34a25-136">**UMIEŚĆ** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="34a25-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="34a25-137">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="34a25-137">API Key</span></span> | <span data-ttu-id="34a25-138">100 na minutę</span><span class="sxs-lookup"><span data-stu-id="34a25-138">100 / minute</span></span> | <span data-ttu-id="34a25-139">Przekaż nowy pakiet NuGet (wersja) za pośrednictwem punktu końcowego wypychania v2</span><span class="sxs-lookup"><span data-stu-id="34a25-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="34a25-140">**USUŃ** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="34a25-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="34a25-141">Klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="34a25-141">API Key</span></span> | <span data-ttu-id="34a25-142">100 na minutę</span><span class="sxs-lookup"><span data-stu-id="34a25-142">100 / minute</span></span> | <span data-ttu-id="34a25-143">Unlist pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2</span><span class="sxs-lookup"><span data-stu-id="34a25-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
