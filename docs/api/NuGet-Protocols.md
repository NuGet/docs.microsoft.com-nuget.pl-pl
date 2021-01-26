---
title: Protokoły nuget.org
description: Rozwijane protokoły nuget.org do współpracy z klientami NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773976"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="eeef5-103">Protokoły nuget.org</span><span class="sxs-lookup"><span data-stu-id="eeef5-103">nuget.org protocols</span></span>

<span data-ttu-id="eeef5-104">Aby można było korzystać z nuget.org, klienci muszą przestrzegać określonych protokołów.</span><span class="sxs-lookup"><span data-stu-id="eeef5-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="eeef5-105">Ponieważ te protokoły zapewniają rozwój, klienci muszą identyfikować wersję protokołu używaną podczas wywoływania określonych interfejsów API nuget.org.</span><span class="sxs-lookup"><span data-stu-id="eeef5-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="eeef5-106">Pozwala to nuget.org wprowadzać zmiany w nieprzerwanym stopniu dla starych klientów.</span><span class="sxs-lookup"><span data-stu-id="eeef5-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="eeef5-107">Interfejsy API udokumentowane na tej stronie są specyficzne dla nuget.org i nie ma oczekiwań innych implementacji serwera NuGet do wprowadzenia tych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="eeef5-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="eeef5-108">Aby uzyskać więcej informacji na temat interfejsu API NuGet wdrożonego w całym ekosystemie NuGet, zobacz [Omówienie interfejsu API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="eeef5-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="eeef5-109">W tym temacie wymieniono różne protokoły w zależności od ich istnienia.</span><span class="sxs-lookup"><span data-stu-id="eeef5-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="eeef5-110">Wersja protokołu NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="eeef5-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="eeef5-111">Protokół 4.1.0 Określa użycie kluczy Weryfikuj-Scope do współdziałania z usługami innym niż nuget.org, aby sprawdzić poprawność pakietu przy użyciu konta nuget.org.</span><span class="sxs-lookup"><span data-stu-id="eeef5-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="eeef5-112">Należy zauważyć, że `4.1.0` numer wersji to ciąg nieprzezroczysty, ale występuje zbieżność z pierwszą wersją oficjalnego klienta NuGet, który obsługuje ten protokół.</span><span class="sxs-lookup"><span data-stu-id="eeef5-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="eeef5-113">Sprawdzanie poprawności zapewnia, że klucze interfejsu API utworzone przez użytkownika są używane tylko z nuget.org i że inne weryfikacje lub Walidacja z usługi innej firmy są obsługiwane za pomocą jednorazowego użycia kluczy Weryfikuj-Scope.</span><span class="sxs-lookup"><span data-stu-id="eeef5-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="eeef5-114">Te klucze Weryfikuj zakres mogą służyć do weryfikowania, czy pakiet należy do określonego użytkownika (konto) w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="eeef5-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="eeef5-115">Wymaganie dotyczące klienta</span><span class="sxs-lookup"><span data-stu-id="eeef5-115">Client requirement</span></span>

<span data-ttu-id="eeef5-116">Klienci muszą przekazać następujący nagłówek, gdy tworzą wywołania interfejsu API do **wypychania** pakietów do NuGet.org:</span><span class="sxs-lookup"><span data-stu-id="eeef5-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="eeef5-117">Należy zauważyć, że `X-NuGet-Client-Version` nagłówek ma podobną semantykę, ale jest zarezerwowany do użycia tylko przez oficjalnego klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="eeef5-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="eeef5-118">Klienci innych firm powinni używać `X-NuGet-Protocol-Version` nagłówka i wartości.</span><span class="sxs-lookup"><span data-stu-id="eeef5-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="eeef5-119">Sam protokół **wypychania** został opisany w dokumentacji dotyczącej [ `PackagePublish` zasobu](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="eeef5-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="eeef5-120">Jeśli klient współdziała z usługami zewnętrznymi i musi sprawdzić, czy pakiet należy do określonego użytkownika (konto), powinien używać następującego protokołu i używać kluczy Weryfikuj-Scope, a nie kluczy interfejsu API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="eeef5-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="eeef5-121">Interfejs API żądania weryfikacji klucza zakresu</span><span class="sxs-lookup"><span data-stu-id="eeef5-121">API to request a verify-scope key</span></span>

<span data-ttu-id="eeef5-122">Ten interfejs API służy do uzyskiwania klucza Weryfikuj-Scope dla autora nuget.org, aby sprawdzić poprawność pakietu należącego do niego.</span><span class="sxs-lookup"><span data-stu-id="eeef5-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="eeef5-123">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="eeef5-123">Request parameters</span></span>

<span data-ttu-id="eeef5-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="eeef5-124">Name</span></span>           | <span data-ttu-id="eeef5-125">W</span><span class="sxs-lookup"><span data-stu-id="eeef5-125">In</span></span>     | <span data-ttu-id="eeef5-126">Typ</span><span class="sxs-lookup"><span data-stu-id="eeef5-126">Type</span></span>   | <span data-ttu-id="eeef5-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="eeef5-127">Required</span></span> | <span data-ttu-id="eeef5-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="eeef5-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="eeef5-129">ID (Identyfikator)</span><span class="sxs-lookup"><span data-stu-id="eeef5-129">ID</span></span>             | <span data-ttu-id="eeef5-130">Adres URL</span><span class="sxs-lookup"><span data-stu-id="eeef5-130">URL</span></span>    | <span data-ttu-id="eeef5-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="eeef5-131">string</span></span> | <span data-ttu-id="eeef5-132">tak</span><span class="sxs-lookup"><span data-stu-id="eeef5-132">yes</span></span>      | <span data-ttu-id="eeef5-133">Identidier pakietu, dla którego zażądano weryfikacji klucza zakresu</span><span class="sxs-lookup"><span data-stu-id="eeef5-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="eeef5-134">WERSJA</span><span class="sxs-lookup"><span data-stu-id="eeef5-134">VERSION</span></span>        | <span data-ttu-id="eeef5-135">Adres URL</span><span class="sxs-lookup"><span data-stu-id="eeef5-135">URL</span></span>    | <span data-ttu-id="eeef5-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="eeef5-136">string</span></span> | <span data-ttu-id="eeef5-137">nie</span><span class="sxs-lookup"><span data-stu-id="eeef5-137">no</span></span>       | <span data-ttu-id="eeef5-138">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="eeef5-138">The package version</span></span>
<span data-ttu-id="eeef5-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="eeef5-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="eeef5-140">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="eeef5-140">Header</span></span> | <span data-ttu-id="eeef5-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="eeef5-141">string</span></span> | <span data-ttu-id="eeef5-142">tak</span><span class="sxs-lookup"><span data-stu-id="eeef5-142">yes</span></span>      | <span data-ttu-id="eeef5-143">Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="eeef5-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="eeef5-144">Reakcja</span><span class="sxs-lookup"><span data-stu-id="eeef5-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="eeef5-145">Interfejs API do sprawdzania poprawności klucza zakresu</span><span class="sxs-lookup"><span data-stu-id="eeef5-145">API to verify the verify scope key</span></span>

<span data-ttu-id="eeef5-146">Ten interfejs API służy do sprawdzania poprawności klucza weryfikacji dla pakietu należącego do autora nuget.org.</span><span class="sxs-lookup"><span data-stu-id="eeef5-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="eeef5-147">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="eeef5-147">Request parameters</span></span>

<span data-ttu-id="eeef5-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="eeef5-148">Name</span></span>           | <span data-ttu-id="eeef5-149">W</span><span class="sxs-lookup"><span data-stu-id="eeef5-149">In</span></span>     | <span data-ttu-id="eeef5-150">Typ</span><span class="sxs-lookup"><span data-stu-id="eeef5-150">Type</span></span>   | <span data-ttu-id="eeef5-151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="eeef5-151">Required</span></span> | <span data-ttu-id="eeef5-152">Uwagi</span><span class="sxs-lookup"><span data-stu-id="eeef5-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="eeef5-153">ID (Identyfikator)</span><span class="sxs-lookup"><span data-stu-id="eeef5-153">ID</span></span>             | <span data-ttu-id="eeef5-154">Adres URL</span><span class="sxs-lookup"><span data-stu-id="eeef5-154">URL</span></span>    | <span data-ttu-id="eeef5-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="eeef5-155">string</span></span> | <span data-ttu-id="eeef5-156">tak</span><span class="sxs-lookup"><span data-stu-id="eeef5-156">yes</span></span>      | <span data-ttu-id="eeef5-157">Identyfikator pakietu, dla którego zażądano weryfikacji klucza zakresu</span><span class="sxs-lookup"><span data-stu-id="eeef5-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="eeef5-158">WERSJA</span><span class="sxs-lookup"><span data-stu-id="eeef5-158">VERSION</span></span>        | <span data-ttu-id="eeef5-159">Adres URL</span><span class="sxs-lookup"><span data-stu-id="eeef5-159">URL</span></span>    | <span data-ttu-id="eeef5-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="eeef5-160">string</span></span> | <span data-ttu-id="eeef5-161">nie</span><span class="sxs-lookup"><span data-stu-id="eeef5-161">no</span></span>       | <span data-ttu-id="eeef5-162">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="eeef5-162">The package version</span></span>
<span data-ttu-id="eeef5-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="eeef5-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="eeef5-164">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="eeef5-164">Header</span></span> | <span data-ttu-id="eeef5-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="eeef5-165">string</span></span> | <span data-ttu-id="eeef5-166">tak</span><span class="sxs-lookup"><span data-stu-id="eeef5-166">yes</span></span>      | <span data-ttu-id="eeef5-167">Na przykład `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="eeef5-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="eeef5-168">Ten klucz interfejsu API sprawdzania zakresu wygasa w czasie dnia lub po pierwszym użyciu, zależnie od tego, co się dzieje.</span><span class="sxs-lookup"><span data-stu-id="eeef5-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="eeef5-169">Reakcja</span><span class="sxs-lookup"><span data-stu-id="eeef5-169">Response</span></span>

<span data-ttu-id="eeef5-170">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="eeef5-170">Status Code</span></span> | <span data-ttu-id="eeef5-171">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="eeef5-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="eeef5-172">200</span><span class="sxs-lookup"><span data-stu-id="eeef5-172">200</span></span>         | <span data-ttu-id="eeef5-173">Klucz interfejsu API jest prawidłowy</span><span class="sxs-lookup"><span data-stu-id="eeef5-173">The API key is valid</span></span>
<span data-ttu-id="eeef5-174">403</span><span class="sxs-lookup"><span data-stu-id="eeef5-174">403</span></span>         | <span data-ttu-id="eeef5-175">Klucz interfejsu API jest nieprawidłowy lub nie jest autoryzowany do wypychania do pakietu</span><span class="sxs-lookup"><span data-stu-id="eeef5-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="eeef5-176">404</span><span class="sxs-lookup"><span data-stu-id="eeef5-176">404</span></span>         | <span data-ttu-id="eeef5-177">Pakiet, do którego odwołuje się `ID` i `VERSION` (opcjonalnie) nie istnieje</span><span class="sxs-lookup"><span data-stu-id="eeef5-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
