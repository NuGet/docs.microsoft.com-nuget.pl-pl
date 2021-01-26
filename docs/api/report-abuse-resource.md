---
title: Szablon adresu URL zgłaszania nadużycia, interfejs API NuGet
description: Szablon adresu URL niezgodnego raportu umożliwia klientom wyświetlanie linku nadużycia raportu w ich interfejsie użytkownika.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775223"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="94b46-103">Szablon adresu URL zgłaszania nadużycia</span><span class="sxs-lookup"><span data-stu-id="94b46-103">Report abuse URL template</span></span>

<span data-ttu-id="94b46-104">Jest możliwe, aby klient mógł utworzyć adres URL, który może być używany przez użytkownika do zgłaszania nadużycia określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="94b46-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="94b46-105">Jest to przydatne, gdy źródło pakietu chce włączyć wszystkie środowiska klienta (nawet inne firmy) do delegowania nadużycia raportów do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="94b46-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="94b46-106">Zasób używany do kompilowania tego adresu URL jest `ReportAbuseUriTemplate` zasobem znalezionym w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="94b46-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="94b46-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="94b46-107">Versioning</span></span>

<span data-ttu-id="94b46-108">`@type`Są używane następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="94b46-108">The following `@type` values are used:</span></span>

<span data-ttu-id="94b46-109">@type wartościami</span><span class="sxs-lookup"><span data-stu-id="94b46-109">@type value</span></span>                       | <span data-ttu-id="94b46-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="94b46-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="94b46-111">ReportAbuseUriTemplate/3.0.0 — beta</span><span class="sxs-lookup"><span data-stu-id="94b46-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="94b46-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="94b46-112">The initial release</span></span>
<span data-ttu-id="94b46-113">ReportAbuseUriTemplate/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="94b46-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="94b46-114">Alias `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="94b46-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="94b46-115">Szablon adresu URL</span><span class="sxs-lookup"><span data-stu-id="94b46-115">URL template</span></span>

<span data-ttu-id="94b46-116">Adres URL następującego interfejsu API to wartość `@id` Właściwości skojarzonej z jedną z wymienionych powyżej `@type` wartości zasobów.</span><span class="sxs-lookup"><span data-stu-id="94b46-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="94b46-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="94b46-117">HTTP methods</span></span>

<span data-ttu-id="94b46-118">Mimo że klient nie jest przeznaczony do żądania do adresu URL niezgodnego z raportem w imieniu użytkownika, Strona sieci Web powinna obsługiwać `GET` metodę, aby można było łatwo otworzyć kliknięty adres URL w przeglądarce sieci Web.</span><span class="sxs-lookup"><span data-stu-id="94b46-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="94b46-119">Konstruowanie adresu URL</span><span class="sxs-lookup"><span data-stu-id="94b46-119">Construct the URL</span></span>

<span data-ttu-id="94b46-120">Po otrzymaniu znanego identyfikatora pakietu i wersji implementacja klienta może utworzyć adres URL służący do uzyskiwania dostępu do interfejsu sieci Web.</span><span class="sxs-lookup"><span data-stu-id="94b46-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="94b46-121">W implementacji klienta powinien być wyświetlany ten skonstruowany adres URL (lub link z możliwością kliknięcia), dzięki któremu użytkownicy mogą otworzyć przeglądarkę sieci Web pod adresem URL i wprowadzić wszelkie niezbędne raporty dotyczące nadużycia.</span><span class="sxs-lookup"><span data-stu-id="94b46-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="94b46-122">Implementacja formularza raportu nadużycia jest określana przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="94b46-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="94b46-123">Wartość parametru `@id` jest ciągiem adresu URL zawierającym dowolny z następujących tokenów zastępczych:</span><span class="sxs-lookup"><span data-stu-id="94b46-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="94b46-124">Symbole zastępcze adresu URL</span><span class="sxs-lookup"><span data-stu-id="94b46-124">URL placeholders</span></span>

<span data-ttu-id="94b46-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="94b46-125">Name</span></span>        | <span data-ttu-id="94b46-126">Typ</span><span class="sxs-lookup"><span data-stu-id="94b46-126">Type</span></span>    | <span data-ttu-id="94b46-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="94b46-127">Required</span></span> | <span data-ttu-id="94b46-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="94b46-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="94b46-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="94b46-129">string</span></span>  | <span data-ttu-id="94b46-130">nie</span><span class="sxs-lookup"><span data-stu-id="94b46-130">no</span></span>       | <span data-ttu-id="94b46-131">Identyfikator pakietu służący do zgłaszania nadużycia</span><span class="sxs-lookup"><span data-stu-id="94b46-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="94b46-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="94b46-132">string</span></span>  | <span data-ttu-id="94b46-133">nie</span><span class="sxs-lookup"><span data-stu-id="94b46-133">no</span></span>       | <span data-ttu-id="94b46-134">Wersja pakietu do zgłaszania nadużycia</span><span class="sxs-lookup"><span data-stu-id="94b46-134">The package version to report abuse for</span></span>

<span data-ttu-id="94b46-135">`{id}`Wartości i `{version}` interpretowane przez implementację serwera muszą być bez uwzględniania wielkości liter i nie są poufne dla tego, czy wersja jest znormalizowana.</span><span class="sxs-lookup"><span data-stu-id="94b46-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="94b46-136">Na przykład szablon nieużywający raportów programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="94b46-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="94b46-137">Jeśli implementacja klienta musi wyświetlić link do formularza nadużycia w raporcie dla NuGet. przechowywanie wersji 4.3.0, spowoduje to utworzenie następującego adresu URL i udostępnienie go użytkownikowi:</span><span class="sxs-lookup"><span data-stu-id="94b46-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
