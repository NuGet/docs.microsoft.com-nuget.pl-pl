---
title: Szablon adresu URL szczegóły pakietu, interfejs API programu NuGet
description: Szablon adresu URL szczegóły pakietu umożliwia klientom do wyświetlenia w ich interfejsu użytkownika sieci web link, aby uzyskać więcej szczegółów pakietu
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638088"
---
# <a name="package-details-url-template"></a><span data-ttu-id="c1126-103">Szablon adresu URL szczegóły pakietu</span><span class="sxs-lookup"><span data-stu-id="c1126-103">Package details URL template</span></span>

<span data-ttu-id="c1126-104">Istnieje możliwość dla klientów utworzenie adresu URL, który może służyć przez użytkownika Aby wyświetlić więcej szczegółów pakietu w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="c1126-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="c1126-105">Jest to przydatne, gdy chce wyświetlić dodatkowe informacje na temat pakietu, który może nie być dopasowane w zakresie aplikacji klienckiej NuGet pokazuje źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="c1126-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="c1126-106">Zasób, używana do tworzenia tego adresu URL jest `PackageDetailsUriTemplate` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c1126-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c1126-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="c1126-107">Versioning</span></span>

<span data-ttu-id="c1126-108">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="c1126-108">The following `@type` values are used:</span></span>

<span data-ttu-id="c1126-109">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="c1126-109">@type value</span></span>                     | <span data-ttu-id="c1126-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c1126-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="c1126-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="c1126-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="c1126-112">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="c1126-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="c1126-113">Szablon adresu URL</span><span class="sxs-lookup"><span data-stu-id="c1126-113">URL template</span></span>

<span data-ttu-id="c1126-114">Adres URL dla następujący interfejs API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="c1126-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c1126-115">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="c1126-115">HTTP methods</span></span>

<span data-ttu-id="c1126-116">Mimo, że klient nie ma wysyłać żądania do adresu URL szczegóły pakietu w imieniu użytkownika, strony sieci web powinien obsługiwać `GET` metodę umożliwiającą kliknięty adres URL łatwo można otworzyć w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="c1126-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="c1126-117">Skonstruuj adres URL</span><span class="sxs-lookup"><span data-stu-id="c1126-117">Construct the URL</span></span>

<span data-ttu-id="c1126-118">Podany identyfikator znanych pakietu i wersję, implementacji klienta można skonstruować adres URL umożliwiający dostęp do interfejsu sieci web.</span><span class="sxs-lookup"><span data-stu-id="c1126-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="c1126-119">Implementacja klienta powinien być wyświetlany ten utworzony adres URL (lub łączem) użytkowników, umożliwiając im Otwórz przeglądarkę sieci web do adresu URL i Dowiedz się więcej o pakiecie.</span><span class="sxs-lookup"><span data-stu-id="c1126-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="c1126-120">Zawartość na stronie szczegółów pakietu jest określany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="c1126-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="c1126-121">Adres URL musi być bezwzględnym adresem URL i schematu (protokół) muszą być adresami HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c1126-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="c1126-122">Wartość `@id` w usłudze indeks jest zawierające dowolne z następujących znaczników symbolu zastępczego ciągu adresu URL:</span><span class="sxs-lookup"><span data-stu-id="c1126-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="c1126-123">Symbole zastępcze adresu URL</span><span class="sxs-lookup"><span data-stu-id="c1126-123">URL placeholders</span></span>

<span data-ttu-id="c1126-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c1126-124">Name</span></span>        | <span data-ttu-id="c1126-125">Typ</span><span class="sxs-lookup"><span data-stu-id="c1126-125">Type</span></span>    | <span data-ttu-id="c1126-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c1126-126">Required</span></span> | <span data-ttu-id="c1126-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c1126-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="c1126-128">string</span><span class="sxs-lookup"><span data-stu-id="c1126-128">string</span></span>  | <span data-ttu-id="c1126-129">Brak</span><span class="sxs-lookup"><span data-stu-id="c1126-129">no</span></span>       | <span data-ttu-id="c1126-130">Identyfikator pakietu, aby uzyskać szczegółowe informacje dla</span><span class="sxs-lookup"><span data-stu-id="c1126-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="c1126-131">string</span><span class="sxs-lookup"><span data-stu-id="c1126-131">string</span></span>  | <span data-ttu-id="c1126-132">Brak</span><span class="sxs-lookup"><span data-stu-id="c1126-132">no</span></span>       | <span data-ttu-id="c1126-133">Wersja pakietu, aby uzyskać szczegółowe informacje dla</span><span class="sxs-lookup"><span data-stu-id="c1126-133">The package version to get details for</span></span>

<span data-ttu-id="c1126-134">Serwer powinien akceptować `{id}` i `{version}` wartości za pomocą dowolnej wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="c1126-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="c1126-135">Ponadto serwer nie powinien być wrażliwe na wersja jest [znormalizowane](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c1126-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="c1126-136">Innymi słowy, serwer powinien akceptować także zaakceptować nieznormalizowanego wersji.</span><span class="sxs-lookup"><span data-stu-id="c1126-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="c1126-137">Na przykład szablon szczegóły pakietu usługi nuget.org wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c1126-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="c1126-138">Jeśli implementacji klienta wymaga wyświetlone łącze do szczegółów pakietu dla NuGet.Versioning 4.3.0, czy to w efekcie następujący adres URL i przekazać go do użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c1126-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
