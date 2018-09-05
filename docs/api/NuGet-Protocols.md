---
title: Protokoły nuget.org
description: Protokoły nuget.org rozwijające się do interakcji z klientami NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547276"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="67026-103">protokoły nuget.org</span><span class="sxs-lookup"><span data-stu-id="67026-103">nuget.org protocols</span></span>

<span data-ttu-id="67026-104">Do interakcji z repozytorium nuget.org, klienci muszą wykonać pewne protokołów.</span><span class="sxs-lookup"><span data-stu-id="67026-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="67026-105">Ponieważ Utrzymaj rozwijające się tych protokołów, klienci muszą zidentyfikować wersja protokołu używanego podczas wywoływania określonych nuget.org interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="67026-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="67026-106">Dzięki temu nuget.org do wprowadzenia zmian w sposób niepowodujących niezgodności starych klientów.</span><span class="sxs-lookup"><span data-stu-id="67026-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="67026-107">Interfejsy API opisane na tej stronie są specyficzne dla nuget.org i nie ma żadnych oczekiwania dotyczące innych implementacji serwera NuGet wprowadzić te interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="67026-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="67026-108">Aby uzyskać informacje o interfejsie API NuGet szeroko zaimplementowane w ekosystemie NuGet, zobacz [omówienie interfejsu API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="67026-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="67026-109">Ten temat zawiera listę różnych protokołów, jak i kiedy pochodzą istnienia.</span><span class="sxs-lookup"><span data-stu-id="67026-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="67026-110">Protokołu NuGet w wersji 4.1.0</span><span class="sxs-lookup"><span data-stu-id="67026-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="67026-111">4.1.0 protokołu Określa użycie kluczy Sprawdź zakres do interakcji z usługami innymi niż nuget.org pakietu do konta w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="67026-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="67026-112">Należy pamiętać, że `4.1.0` wersji liczba to nieprzezroczysty ciąg, ale dzieje się pokrywają się z pierwszą wersję oficjalne klienta NuGet, który obsługuje ten protokół.</span><span class="sxs-lookup"><span data-stu-id="67026-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="67026-113">Sprawdzanie poprawności gwarantuje, że klucze interfejsu API utworzonej przez użytkownika są używane tylko w witrynie nuget.org, i tej weryfikacji lub Weryfikacja z usługi innej firmy odbywa się przy użyciu kluczy Sprawdź zakres jednorazowego użytku.</span><span class="sxs-lookup"><span data-stu-id="67026-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="67026-114">Te klucze Sprawdź zakres może służyć do sprawdzania, czy pakiet należy do określonego użytkownika (konto) w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="67026-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="67026-115">Wymagania klienta</span><span class="sxs-lookup"><span data-stu-id="67026-115">Client requirement</span></span>

<span data-ttu-id="67026-116">Klienci są wymagane do przekazania następujący nagłówek, w momencie wywołania interfejsu API do **wypychania** pakietów nuget.org:</span><span class="sxs-lookup"><span data-stu-id="67026-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="67026-117">Należy pamiętać, że `X-NuGet-Client-Version` nagłówka przypomina semantykę, ale jest zarezerwowany do użycia tylko przez oficjalne klienta programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="67026-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="67026-118">Innych firm, klienci powinni używać `X-NuGet-Protocol-Version` nagłówek i podaną wartość.</span><span class="sxs-lookup"><span data-stu-id="67026-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="67026-119">**Wypychania** samego protokołu jest opisane w dokumentacji dotyczącej [ `PackagePublish` zasobów](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="67026-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="67026-120">Jeśli klient korzysta z usług zewnętrznych i należy sprawdzić, czy pakiet należy do określonego użytkownika (konto), powinna używać następujących protokołu i klucze Sprawdź, czy zakres i nie klucze interfejsu API z repozytorium nuget.org.</span><span class="sxs-lookup"><span data-stu-id="67026-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="67026-121">Interfejs API, aby poprosić o klucz Sprawdź, czy zakres</span><span class="sxs-lookup"><span data-stu-id="67026-121">API to request a verify-scope key</span></span>

<span data-ttu-id="67026-122">Ten interfejs API umożliwia uzyskiwanie klucza Sprawdź, czy zakres dla autora nuget.org do sprawdzania poprawności pakietu posiadanych przez nią.</span><span class="sxs-lookup"><span data-stu-id="67026-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="67026-123">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="67026-123">Request parameters</span></span>

<span data-ttu-id="67026-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="67026-124">Name</span></span>           | <span data-ttu-id="67026-125">W</span><span class="sxs-lookup"><span data-stu-id="67026-125">In</span></span>     | <span data-ttu-id="67026-126">Typ</span><span class="sxs-lookup"><span data-stu-id="67026-126">Type</span></span>   | <span data-ttu-id="67026-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="67026-127">Required</span></span> | <span data-ttu-id="67026-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="67026-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="67026-129">ID</span><span class="sxs-lookup"><span data-stu-id="67026-129">ID</span></span>             | <span data-ttu-id="67026-130">Adres URL</span><span class="sxs-lookup"><span data-stu-id="67026-130">URL</span></span>    | <span data-ttu-id="67026-131">string</span><span class="sxs-lookup"><span data-stu-id="67026-131">string</span></span> | <span data-ttu-id="67026-132">Tak</span><span class="sxs-lookup"><span data-stu-id="67026-132">yes</span></span>      | <span data-ttu-id="67026-133">Identidier pakiet, dla którego żądana jest Sprawdź, czy klucz zakresu</span><span class="sxs-lookup"><span data-stu-id="67026-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="67026-134">WERSJA</span><span class="sxs-lookup"><span data-stu-id="67026-134">VERSION</span></span>        | <span data-ttu-id="67026-135">Adres URL</span><span class="sxs-lookup"><span data-stu-id="67026-135">URL</span></span>    | <span data-ttu-id="67026-136">string</span><span class="sxs-lookup"><span data-stu-id="67026-136">string</span></span> | <span data-ttu-id="67026-137">Brak</span><span class="sxs-lookup"><span data-stu-id="67026-137">no</span></span>       | <span data-ttu-id="67026-138">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="67026-138">The package version</span></span>
<span data-ttu-id="67026-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="67026-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="67026-140">nagłówek</span><span class="sxs-lookup"><span data-stu-id="67026-140">Header</span></span> | <span data-ttu-id="67026-141">string</span><span class="sxs-lookup"><span data-stu-id="67026-141">string</span></span> | <span data-ttu-id="67026-142">Tak</span><span class="sxs-lookup"><span data-stu-id="67026-142">yes</span></span>      | <span data-ttu-id="67026-143">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="67026-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="67026-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="67026-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="67026-145">Interfejs API, aby sprawdzić, sprawdź, czy klucz zakresu</span><span class="sxs-lookup"><span data-stu-id="67026-145">API to verify the verify scope key</span></span>

<span data-ttu-id="67026-146">Ten interfejs API jest używana do zweryfikowania klucza zakresu Sprawdź posiadane przez autora nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="67026-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="67026-147">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="67026-147">Request parameters</span></span>

<span data-ttu-id="67026-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="67026-148">Name</span></span>           | <span data-ttu-id="67026-149">W</span><span class="sxs-lookup"><span data-stu-id="67026-149">In</span></span>     | <span data-ttu-id="67026-150">Typ</span><span class="sxs-lookup"><span data-stu-id="67026-150">Type</span></span>   | <span data-ttu-id="67026-151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="67026-151">Required</span></span> | <span data-ttu-id="67026-152">Uwagi</span><span class="sxs-lookup"><span data-stu-id="67026-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="67026-153">ID</span><span class="sxs-lookup"><span data-stu-id="67026-153">ID</span></span>             | <span data-ttu-id="67026-154">Adres URL</span><span class="sxs-lookup"><span data-stu-id="67026-154">URL</span></span>    | <span data-ttu-id="67026-155">string</span><span class="sxs-lookup"><span data-stu-id="67026-155">string</span></span> | <span data-ttu-id="67026-156">Tak</span><span class="sxs-lookup"><span data-stu-id="67026-156">yes</span></span>      | <span data-ttu-id="67026-157">Identyfikator pakietu, dla którego żądana jest Sprawdź, czy klucz zakresu</span><span class="sxs-lookup"><span data-stu-id="67026-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="67026-158">WERSJA</span><span class="sxs-lookup"><span data-stu-id="67026-158">VERSION</span></span>        | <span data-ttu-id="67026-159">Adres URL</span><span class="sxs-lookup"><span data-stu-id="67026-159">URL</span></span>    | <span data-ttu-id="67026-160">string</span><span class="sxs-lookup"><span data-stu-id="67026-160">string</span></span> | <span data-ttu-id="67026-161">Brak</span><span class="sxs-lookup"><span data-stu-id="67026-161">no</span></span>       | <span data-ttu-id="67026-162">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="67026-162">The package version</span></span>
<span data-ttu-id="67026-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="67026-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="67026-164">nagłówek</span><span class="sxs-lookup"><span data-stu-id="67026-164">Header</span></span> | <span data-ttu-id="67026-165">string</span><span class="sxs-lookup"><span data-stu-id="67026-165">string</span></span> | <span data-ttu-id="67026-166">Tak</span><span class="sxs-lookup"><span data-stu-id="67026-166">yes</span></span>      | <span data-ttu-id="67026-167">Na przykład:`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="67026-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="67026-168">Ten klucz interfejsu API zakresu Sprawdź, czy utraci ważność za dni lub przy pierwszym użyciu zależnie co nastąpi wcześniej.</span><span class="sxs-lookup"><span data-stu-id="67026-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="67026-169">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="67026-169">Response</span></span>

<span data-ttu-id="67026-170">Kod stanu:</span><span class="sxs-lookup"><span data-stu-id="67026-170">Status Code</span></span> | <span data-ttu-id="67026-171">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="67026-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="67026-172">200</span><span class="sxs-lookup"><span data-stu-id="67026-172">200</span></span>         | <span data-ttu-id="67026-173">Klucz interfejsu API jest nieprawidłowa</span><span class="sxs-lookup"><span data-stu-id="67026-173">The API key is valid</span></span>
<span data-ttu-id="67026-174">403</span><span class="sxs-lookup"><span data-stu-id="67026-174">403</span></span>         | <span data-ttu-id="67026-175">Klucz interfejsu API jest nieprawidłowa lub nie jest autoryzowany do wypychania na pakiecie</span><span class="sxs-lookup"><span data-stu-id="67026-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="67026-176">404</span><span class="sxs-lookup"><span data-stu-id="67026-176">404</span></span>         | <span data-ttu-id="67026-177">Pakiet odwołuje się `ID` i `VERSION` (opcjonalnie) nie istnieje</span><span class="sxs-lookup"><span data-stu-id="67026-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
