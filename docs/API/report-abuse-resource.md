---
title: "Zgłoś nadużycie szablon adresu URL, NuGet interfejsu API | Dokumentacja firmy Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Szablon adresu URL nadużycia raport umożliwia klientom do wyświetlenia łącza nadużycia raportu w jego interfejsie użytkownika."
keywords: "Interfejs API NuGet zgłaszania nadużyć, NuGet interfejsu API plików zgodne, szablon adres URL raportu nuget.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: efbe5704e6e6028f9382fea3fe5ec453f573a2e9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="ce48a-104">Szablon adresu URL nadużycia raportu</span><span class="sxs-lookup"><span data-stu-id="ce48a-104">Report abuse URL template</span></span>

<span data-ttu-id="ce48a-105">Istnieje możliwość dla klienta do tworzenia adresów URL, które mogą być używane przez użytkownika do zgłaszania nadużyć o określonym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="ce48a-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="ce48a-106">Jest to przydatne, gdy źródło pakietu chce włączyć wszystkie delegować nadużycia raporty do źródła pakietu klienta środowiska (strona nawet 3).</span><span class="sxs-lookup"><span data-stu-id="ce48a-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="ce48a-107">Zasób używany do pobierania zawartości pakietu jest `ReportAbuseUriTemplate` można znaleźć zasobu w [indeksu usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ce48a-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ce48a-108">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="ce48a-108">Versioning</span></span>

<span data-ttu-id="ce48a-109">Następujące `@type` są używane wartości:</span><span class="sxs-lookup"><span data-stu-id="ce48a-109">The following `@type` values are used:</span></span>

<span data-ttu-id="ce48a-110">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="ce48a-110">@type value</span></span>                       | <span data-ttu-id="ce48a-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ce48a-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="ce48a-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="ce48a-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="ce48a-113">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="ce48a-113">The initial release</span></span>
<span data-ttu-id="ce48a-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="ce48a-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="ce48a-115">Alias `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="ce48a-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="ce48a-116">Szablon adresu URL</span><span class="sxs-lookup"><span data-stu-id="ce48a-116">URL template</span></span>

<span data-ttu-id="ce48a-117">Adres URL następujący interfejs API jest wartość `@id` właściwości skojarzone z jedną z wyżej wymienionych zasobów `@type` wartości.</span><span class="sxs-lookup"><span data-stu-id="ce48a-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ce48a-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="ce48a-118">HTTP methods</span></span>

<span data-ttu-id="ce48a-119">Mimo że klient nie jest przeznaczony na wysyłanie żądań do adresu URL programu report nadużyć w imieniu użytkownika, strony sieci web powinna obsługiwać `GET` metodę umożliwiającą klikniętej adres URL, który można łatwo otworzyć w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="ce48a-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="ce48a-120">Utworzyć adres URL</span><span class="sxs-lookup"><span data-stu-id="ce48a-120">Construct the URL</span></span>

<span data-ttu-id="ce48a-121">Podany identyfikator znanego pakietu i wersję, implementacja klienta można konstruować adresu URL, które umożliwiają dostęp do interfejsu sieci web.</span><span class="sxs-lookup"><span data-stu-id="ce48a-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="ce48a-122">Implementacja klienta powinien być wyświetlany tego utworzony adres URL (lub łączem) użytkownika, dzięki czemu Otwórz przeglądarkę sieci web do adresu URL i żadnych raportów na potrzeby nadużycia.</span><span class="sxs-lookup"><span data-stu-id="ce48a-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="ce48a-123">Implementacja formularz raportu nadużycia zależy od implementacji serwera.</span><span class="sxs-lookup"><span data-stu-id="ce48a-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="ce48a-124">Wartość `@id` jest zawierające dowolny z następujących znaczników symbol zastępczy ciągu adresu URL:</span><span class="sxs-lookup"><span data-stu-id="ce48a-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="ce48a-125">Symbole zastępcze adresu URL</span><span class="sxs-lookup"><span data-stu-id="ce48a-125">URL placeholders</span></span>

<span data-ttu-id="ce48a-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ce48a-126">Name</span></span>        | <span data-ttu-id="ce48a-127">Typ</span><span class="sxs-lookup"><span data-stu-id="ce48a-127">Type</span></span>    | <span data-ttu-id="ce48a-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ce48a-128">Required</span></span> | <span data-ttu-id="ce48a-129">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ce48a-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="ce48a-130">string</span><span class="sxs-lookup"><span data-stu-id="ce48a-130">string</span></span>  | <span data-ttu-id="ce48a-131">Brak</span><span class="sxs-lookup"><span data-stu-id="ce48a-131">no</span></span>       | <span data-ttu-id="ce48a-132">Identyfikator pakietu do zgłaszania nadużyć dla</span><span class="sxs-lookup"><span data-stu-id="ce48a-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="ce48a-133">string</span><span class="sxs-lookup"><span data-stu-id="ce48a-133">string</span></span>  | <span data-ttu-id="ce48a-134">Brak</span><span class="sxs-lookup"><span data-stu-id="ce48a-134">no</span></span>       | <span data-ttu-id="ce48a-135">Wersja pakietu do zgłaszania nadużyć dla</span><span class="sxs-lookup"><span data-stu-id="ce48a-135">The package version to report abuse for</span></span>

<span data-ttu-id="ce48a-136">`{id}` i `{version}` wartości interpretowane przez implementację serwera musi być bez uwzględniania wielkości liter i nie poufne czy normalizowane jest wersja.</span><span class="sxs-lookup"><span data-stu-id="ce48a-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="ce48a-137">Na przykład szablon nadużycia raportu nuget.org wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ce48a-137">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="ce48a-138">Jeśli implementacja klienta wymaga do wyświetlenia łącza do formularza nadużycia raport NuGet.Versioning 4.3.0, czy to utworzyć następujący adres URL i przekazywanie ich do użytkownika:</span><span class="sxs-lookup"><span data-stu-id="ce48a-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
