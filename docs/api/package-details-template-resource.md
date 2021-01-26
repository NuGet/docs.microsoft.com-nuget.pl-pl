---
title: Szablon adresu URL szczegółów pakietu, interfejs API NuGet
description: Szablon adresu URL szczegółów pakietu umożliwia klientom wyświetlanie w ich interfejsie użytkownika linku internetowego do większej liczby szczegółów pakietu
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773952"
---
# <a name="package-details-url-template"></a><span data-ttu-id="f4895-103">Szablon adresu URL szczegółów pakietu</span><span class="sxs-lookup"><span data-stu-id="f4895-103">Package details URL template</span></span>

<span data-ttu-id="f4895-104">Jest możliwe, aby klient mógł utworzyć adres URL, który może być używany przez użytkownika, aby wyświetlić więcej szczegółów pakietu w swojej przeglądarce sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f4895-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="f4895-105">Jest to przydatne, gdy źródło pakietu chce wyświetlić dodatkowe informacje dotyczące pakietu, który może nie pasować do zakresu działania aplikacji klienckiej NuGet.</span><span class="sxs-lookup"><span data-stu-id="f4895-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="f4895-106">Zasób używany do kompilowania tego adresu URL jest `PackageDetailsUriTemplate` zasobem znalezionym w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="f4895-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="f4895-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="f4895-107">Versioning</span></span>

<span data-ttu-id="f4895-108">`@type`Są używane następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="f4895-108">The following `@type` values are used:</span></span>

<span data-ttu-id="f4895-109">@type wartościami</span><span class="sxs-lookup"><span data-stu-id="f4895-109">@type value</span></span>                     | <span data-ttu-id="f4895-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f4895-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="f4895-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="f4895-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="f4895-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="f4895-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="f4895-113">Szablon adresu URL</span><span class="sxs-lookup"><span data-stu-id="f4895-113">URL template</span></span>

<span data-ttu-id="f4895-114">Adres URL następującego interfejsu API to wartość `@id` Właściwości skojarzonej z jedną z wymienionych powyżej `@type` wartości zasobów.</span><span class="sxs-lookup"><span data-stu-id="f4895-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f4895-115">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="f4895-115">HTTP methods</span></span>

<span data-ttu-id="f4895-116">Mimo że klient nie jest przeznaczony do żądania do adresu URL informacji o pakiecie w imieniu użytkownika, na stronie sieci Web powinna być obsługiwana `GET` Metoda zezwalająca na otwarcie klikniętego adresu URL w przeglądarce internetowej.</span><span class="sxs-lookup"><span data-stu-id="f4895-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="f4895-117">Konstruowanie adresu URL</span><span class="sxs-lookup"><span data-stu-id="f4895-117">Construct the URL</span></span>

<span data-ttu-id="f4895-118">Po otrzymaniu znanego identyfikatora pakietu i wersji implementacja klienta może utworzyć adres URL służący do uzyskiwania dostępu do interfejsu sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f4895-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="f4895-119">W implementacji klienta powinien być wyświetlany ten skonstruowany adres URL (lub link do kliknięcia), dzięki któremu użytkownicy mogą otworzyć przeglądarkę internetową pod adresem URL i dowiedzieć się więcej na temat pakietu.</span><span class="sxs-lookup"><span data-stu-id="f4895-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="f4895-120">Zawartość strony Szczegóły pakietu jest określana przez implementację serwera.</span><span class="sxs-lookup"><span data-stu-id="f4895-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="f4895-121">Adres URL musi być bezwzględnym adresem URL, a schemat (protokół) musi być HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f4895-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="f4895-122">Wartość `@id` w indeksie usługi jest ciągiem adresu URL zawierającym dowolny z następujących tokenów zastępczych:</span><span class="sxs-lookup"><span data-stu-id="f4895-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="f4895-123">Symbole zastępcze adresu URL</span><span class="sxs-lookup"><span data-stu-id="f4895-123">URL placeholders</span></span>

<span data-ttu-id="f4895-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4895-124">Name</span></span>        | <span data-ttu-id="f4895-125">Typ</span><span class="sxs-lookup"><span data-stu-id="f4895-125">Type</span></span>    | <span data-ttu-id="f4895-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4895-126">Required</span></span> | <span data-ttu-id="f4895-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f4895-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="f4895-128">ciąg</span><span class="sxs-lookup"><span data-stu-id="f4895-128">string</span></span>  | <span data-ttu-id="f4895-129">nie</span><span class="sxs-lookup"><span data-stu-id="f4895-129">no</span></span>       | <span data-ttu-id="f4895-130">Identyfikator pakietu, dla którego mają zostać pobrane szczegóły</span><span class="sxs-lookup"><span data-stu-id="f4895-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="f4895-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="f4895-131">string</span></span>  | <span data-ttu-id="f4895-132">nie</span><span class="sxs-lookup"><span data-stu-id="f4895-132">no</span></span>       | <span data-ttu-id="f4895-133">Wersja pakietu, dla której mają zostać pobrane szczegóły</span><span class="sxs-lookup"><span data-stu-id="f4895-133">The package version to get details for</span></span>

<span data-ttu-id="f4895-134">Serwer powinien akceptować `{id}` `{version}` wartości i zawierać dowolne wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="f4895-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="f4895-135">Ponadto serwer nie powinien być wrażliwy na to, czy wersja jest [znormalizowana](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="f4895-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="f4895-136">Innymi słowy, serwer powinien akceptować również nieznormalizowane wersje.</span><span class="sxs-lookup"><span data-stu-id="f4895-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="f4895-137">Na przykład szablon Details programu NuGet. org wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="f4895-137">For example, nuget.org's package details template looks like this:</span></span>

```http
https://www.nuget.org/packages/{id}/{version}
```

<span data-ttu-id="f4895-138">Jeśli implementacja klienta musi wyświetlić link do szczegółów pakietu NuGet. przechowywanie wersji 4.3.0, spowoduje to utworzenie następującego adresu URL i udostępnienie go użytkownikowi:</span><span class="sxs-lookup"><span data-stu-id="f4895-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
