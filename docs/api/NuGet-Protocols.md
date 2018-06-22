---
title: Protokoły nuget.org
description: Protokoły nuget.org zmieniające się do interakcji z klientów NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822581"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="1e528-103">protokoły nuget.org</span><span class="sxs-lookup"><span data-stu-id="1e528-103">nuget.org protocols</span></span>

<span data-ttu-id="1e528-104">Wchodzić w interakcje z nuget.org, klienci muszą wykonać niektórych protokołów.</span><span class="sxs-lookup"><span data-stu-id="1e528-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="1e528-105">Ponieważ rozwijają zachować te protokoły, klienci muszą identyfikują wersja protokołu używanego podczas wywoływania metody nuget.org określonych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="1e528-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="1e528-106">Dzięki temu nuget.org wprowadzenie zmian w sposób nierozdzielające starego klientów.</span><span class="sxs-lookup"><span data-stu-id="1e528-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="1e528-107">Interfejsy API udokumentowany na tej stronie są specyficzne dla nuget.org i nie ma żadnych oczekiwania w innych implementacjach serwera NuGet dodać te interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="1e528-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="1e528-108">Informacje o interfejsie API NuGet szeroko implementowany w ekosystemie NuGet, zobacz [Przegląd interfejsu API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e528-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="1e528-109">Ten temat zawiera listę różnych protokołów, jak i kiedy zaczynają istnienia.</span><span class="sxs-lookup"><span data-stu-id="1e528-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="1e528-110">Wersja protokołu NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="1e528-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="1e528-111">4.1.0 protokołu Określa użycie kluczy Sprawdź zakres do interakcji z usługami innych niż nuget.org pakietu do konta nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1e528-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="1e528-112">Należy pamiętać, że `4.1.0` wersji liczba to ciąg nieprzezroczyste, ale dzieje się pokrywa się z pierwszej wersji oficjalnego klienta NuGet, który obsługuje tego protokołu.</span><span class="sxs-lookup"><span data-stu-id="1e528-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="1e528-113">Sprawdzanie poprawności temu klucze interfejsu API utworzonych przez użytkownika są używane tylko z nuget.org i tej weryfikacji lub Weryfikacja od usługi innej firmy jest obsługiwana za pomocą kluczy Sprawdź zakres jednorazowego użytku.</span><span class="sxs-lookup"><span data-stu-id="1e528-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="1e528-114">Te klucze Sprawdź zakres może służyć do sprawdzania, czy pakiet należy do określonego użytkownika (konto) na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1e528-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="1e528-115">Wymagania klienta</span><span class="sxs-lookup"><span data-stu-id="1e528-115">Client requirement</span></span>

<span data-ttu-id="1e528-116">Klienci są wymagane do przekazania następujący nagłówek, podczas tworzenia wywołań interfejsu API **wypychania** pakietów do nuget.org:</span><span class="sxs-lookup"><span data-stu-id="1e528-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="1e528-117">Należy pamiętać, że `X-NuGet-Client-Version` przypomina semantykę nagłówka, ale jest zarezerwowany do użycia tylko przez oficjalnego klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e528-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="1e528-118">Innej klienci powinni używać `X-NuGet-Protocol-Version` nagłówek i podaną wartość.</span><span class="sxs-lookup"><span data-stu-id="1e528-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="1e528-119">**Wypychania** samego protokołu jest opisany w dokumentacji dotyczącej [ `PackagePublish` zasobów](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1e528-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="1e528-120">Jeśli klient współdziała z usług zewnętrznych i należy sprawdzić, czy pakiet należy do określonego użytkownika (konto), powinna używać protokołu następujące i używać kluczy Sprawdź zakres i nie klucze interfejsu API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1e528-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="1e528-121">Interfejs API do żądania klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="1e528-121">API to request a verify-scope key</span></span>

<span data-ttu-id="1e528-122">Ten interfejs API jest używany do pobierania klucz, sprawdź, czy zakres autora nuget.org, można sprawdzić poprawności pakietu posiadanych przez nią.</span><span class="sxs-lookup"><span data-stu-id="1e528-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="1e528-123">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="1e528-123">Request parameters</span></span>

<span data-ttu-id="1e528-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1e528-124">Name</span></span>           | <span data-ttu-id="1e528-125">W</span><span class="sxs-lookup"><span data-stu-id="1e528-125">In</span></span>     | <span data-ttu-id="1e528-126">Typ</span><span class="sxs-lookup"><span data-stu-id="1e528-126">Type</span></span>   | <span data-ttu-id="1e528-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1e528-127">Required</span></span> | <span data-ttu-id="1e528-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1e528-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1e528-129">ID</span><span class="sxs-lookup"><span data-stu-id="1e528-129">ID</span></span>             | <span data-ttu-id="1e528-130">Adres URL</span><span class="sxs-lookup"><span data-stu-id="1e528-130">URL</span></span>    | <span data-ttu-id="1e528-131">string</span><span class="sxs-lookup"><span data-stu-id="1e528-131">string</span></span> | <span data-ttu-id="1e528-132">Tak</span><span class="sxs-lookup"><span data-stu-id="1e528-132">yes</span></span>      | <span data-ttu-id="1e528-133">Identidier pakiet, dla którego wymagany jest klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="1e528-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="1e528-134">WERSJA</span><span class="sxs-lookup"><span data-stu-id="1e528-134">VERSION</span></span>        | <span data-ttu-id="1e528-135">Adres URL</span><span class="sxs-lookup"><span data-stu-id="1e528-135">URL</span></span>    | <span data-ttu-id="1e528-136">string</span><span class="sxs-lookup"><span data-stu-id="1e528-136">string</span></span> | <span data-ttu-id="1e528-137">Brak</span><span class="sxs-lookup"><span data-stu-id="1e528-137">no</span></span>       | <span data-ttu-id="1e528-138">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="1e528-138">The package version</span></span>
<span data-ttu-id="1e528-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1e528-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1e528-140">nagłówek</span><span class="sxs-lookup"><span data-stu-id="1e528-140">Header</span></span> | <span data-ttu-id="1e528-141">string</span><span class="sxs-lookup"><span data-stu-id="1e528-141">string</span></span> | <span data-ttu-id="1e528-142">Tak</span><span class="sxs-lookup"><span data-stu-id="1e528-142">yes</span></span>      | <span data-ttu-id="1e528-143">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1e528-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="1e528-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="1e528-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="1e528-145">Interfejs API, aby zweryfikować klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="1e528-145">API to verify the verify scope key</span></span>

<span data-ttu-id="1e528-146">Ten interfejs API jest używany do sprawdzania poprawności klucza zakresu Sprawdź posiadane przez autora nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e528-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="1e528-147">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="1e528-147">Request parameters</span></span>

<span data-ttu-id="1e528-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1e528-148">Name</span></span>           | <span data-ttu-id="1e528-149">W</span><span class="sxs-lookup"><span data-stu-id="1e528-149">In</span></span>     | <span data-ttu-id="1e528-150">Typ</span><span class="sxs-lookup"><span data-stu-id="1e528-150">Type</span></span>   | <span data-ttu-id="1e528-151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1e528-151">Required</span></span> | <span data-ttu-id="1e528-152">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1e528-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="1e528-153">ID</span><span class="sxs-lookup"><span data-stu-id="1e528-153">ID</span></span>             | <span data-ttu-id="1e528-154">Adres URL</span><span class="sxs-lookup"><span data-stu-id="1e528-154">URL</span></span>    | <span data-ttu-id="1e528-155">string</span><span class="sxs-lookup"><span data-stu-id="1e528-155">string</span></span> | <span data-ttu-id="1e528-156">Tak</span><span class="sxs-lookup"><span data-stu-id="1e528-156">yes</span></span>      | <span data-ttu-id="1e528-157">Identyfikator pakietu, dla którego wymagany jest klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="1e528-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="1e528-158">WERSJA</span><span class="sxs-lookup"><span data-stu-id="1e528-158">VERSION</span></span>        | <span data-ttu-id="1e528-159">Adres URL</span><span class="sxs-lookup"><span data-stu-id="1e528-159">URL</span></span>    | <span data-ttu-id="1e528-160">string</span><span class="sxs-lookup"><span data-stu-id="1e528-160">string</span></span> | <span data-ttu-id="1e528-161">Brak</span><span class="sxs-lookup"><span data-stu-id="1e528-161">no</span></span>       | <span data-ttu-id="1e528-162">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="1e528-162">The package version</span></span>
<span data-ttu-id="1e528-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1e528-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1e528-164">nagłówek</span><span class="sxs-lookup"><span data-stu-id="1e528-164">Header</span></span> | <span data-ttu-id="1e528-165">string</span><span class="sxs-lookup"><span data-stu-id="1e528-165">string</span></span> | <span data-ttu-id="1e528-166">Tak</span><span class="sxs-lookup"><span data-stu-id="1e528-166">yes</span></span>      | <span data-ttu-id="1e528-167">Na przykład:`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1e528-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="1e528-168">Ten klucz interfejsu API zakresu Sprawdź utraci ważność za dni lub przy pierwszym użyciu cokolwiek nastąpi najpierw.</span><span class="sxs-lookup"><span data-stu-id="1e528-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="1e528-169">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="1e528-169">Response</span></span>

<span data-ttu-id="1e528-170">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="1e528-170">Status Code</span></span> | <span data-ttu-id="1e528-171">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="1e528-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="1e528-172">200</span><span class="sxs-lookup"><span data-stu-id="1e528-172">200</span></span>         | <span data-ttu-id="1e528-173">Klucz interfejsu API jest nieprawidłowa</span><span class="sxs-lookup"><span data-stu-id="1e528-173">The API key is valid</span></span>
<span data-ttu-id="1e528-174">403</span><span class="sxs-lookup"><span data-stu-id="1e528-174">403</span></span>         | <span data-ttu-id="1e528-175">Klucz interfejsu API jest nieprawidłowa lub nie jest autoryzowany do wypychania na pakiecie</span><span class="sxs-lookup"><span data-stu-id="1e528-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="1e528-176">404</span><span class="sxs-lookup"><span data-stu-id="1e528-176">404</span></span>         | <span data-ttu-id="1e528-177">Pakiet odwołuje się `ID` i `VERSION` (opcjonalnie) nie istnieje</span><span class="sxs-lookup"><span data-stu-id="1e528-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
