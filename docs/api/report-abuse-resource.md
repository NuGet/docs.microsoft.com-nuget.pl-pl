---
title: Zgłoś nadużycie szablon adresu URL, interfejs API programu NuGet
description: Szablon adresu URL raportu nadużycie umożliwia klientom wyświetlane łącza zgłaszania nadużycia w jego interfejsie użytkownika.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020443"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="26e46-103">Szablon adresu URL nadużycie raportu</span><span class="sxs-lookup"><span data-stu-id="26e46-103">Report abuse URL template</span></span>

<span data-ttu-id="26e46-104">Istnieje możliwość dla klientów utworzenie adresu URL, który może służyć przez użytkownika w celu Zgłoś nadużycie o określonym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="26e46-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="26e46-105">Jest to przydatne, gdy źródło pakietu chce umieszczenie wszystkich klienta (strona nawet 3) do delegowania nadużycie raporty do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="26e46-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="26e46-106">Zasób, używana do tworzenia tego adresu URL jest `ReportAbuseUriTemplate` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="26e46-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="26e46-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="26e46-107">Versioning</span></span>

<span data-ttu-id="26e46-108">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="26e46-108">The following `@type` values are used:</span></span>

<span data-ttu-id="26e46-109">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="26e46-109">@type value</span></span>                       | <span data-ttu-id="26e46-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="26e46-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="26e46-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="26e46-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="26e46-112">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="26e46-112">The initial release</span></span>
<span data-ttu-id="26e46-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="26e46-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="26e46-114">Alias `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="26e46-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="26e46-115">Szablon adresu URL</span><span class="sxs-lookup"><span data-stu-id="26e46-115">URL template</span></span>

<span data-ttu-id="26e46-116">Adres URL dla następujący interfejs API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="26e46-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="26e46-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="26e46-117">HTTP methods</span></span>

<span data-ttu-id="26e46-118">Mimo, że klient nie ma wysyłać żądania do adresu URL nadużycie raportu w imieniu użytkownika, strony sieci web powinien obsługiwać `GET` metodę umożliwiającą kliknięty adres URL łatwo można otworzyć w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="26e46-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="26e46-119">Skonstruuj adres URL</span><span class="sxs-lookup"><span data-stu-id="26e46-119">Construct the URL</span></span>

<span data-ttu-id="26e46-120">Podany identyfikator znanych pakietu i wersję, implementacji klienta można skonstruować adres URL umożliwiający dostęp do interfejsu sieci web.</span><span class="sxs-lookup"><span data-stu-id="26e46-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="26e46-121">Implementacja klienta powinien być wyświetlany ten utworzony adres URL (lub łączem) użytkowników, umożliwiając im Otwórz przeglądarkę sieci web do adresu URL i dowolny raport nadużycie niezbędne.</span><span class="sxs-lookup"><span data-stu-id="26e46-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="26e46-122">Implementacja nadużycie formularz raportu jest określany przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="26e46-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="26e46-123">Wartość `@id` jest zawierające dowolne z następujących znaczników symbolu zastępczego ciągu adresu URL:</span><span class="sxs-lookup"><span data-stu-id="26e46-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="26e46-124">Symbole zastępcze adresu URL</span><span class="sxs-lookup"><span data-stu-id="26e46-124">URL placeholders</span></span>

<span data-ttu-id="26e46-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="26e46-125">Name</span></span>        | <span data-ttu-id="26e46-126">Typ</span><span class="sxs-lookup"><span data-stu-id="26e46-126">Type</span></span>    | <span data-ttu-id="26e46-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="26e46-127">Required</span></span> | <span data-ttu-id="26e46-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="26e46-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="26e46-129">string</span><span class="sxs-lookup"><span data-stu-id="26e46-129">string</span></span>  | <span data-ttu-id="26e46-130">Brak</span><span class="sxs-lookup"><span data-stu-id="26e46-130">no</span></span>       | <span data-ttu-id="26e46-131">Identyfikator pakietu w celu Zgłoś nadużycie odnośnie do</span><span class="sxs-lookup"><span data-stu-id="26e46-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="26e46-132">string</span><span class="sxs-lookup"><span data-stu-id="26e46-132">string</span></span>  | <span data-ttu-id="26e46-133">Brak</span><span class="sxs-lookup"><span data-stu-id="26e46-133">no</span></span>       | <span data-ttu-id="26e46-134">Wersja pakietu, który ma być Zgłoś nadużycie odnośnie do</span><span class="sxs-lookup"><span data-stu-id="26e46-134">The package version to report abuse for</span></span>

<span data-ttu-id="26e46-135">`{id}` i `{version}` wartości interpretowane przez implementację serwera musi być bez uwzględniania wielkości liter i nie wrażliwe na tego, czy wersja jest znormalizować.</span><span class="sxs-lookup"><span data-stu-id="26e46-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="26e46-136">Na przykład szablon nadużycie raportu usługi nuget.org wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="26e46-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="26e46-137">Jeśli implementacji klienta wymaganych, aby wyświetlić łącza do formularza nadużycie raportu dla NuGet.Versioning 4.3.0, czy to w efekcie następujący adres URL i przekazać go do użytkownika:</span><span class="sxs-lookup"><span data-stu-id="26e46-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
