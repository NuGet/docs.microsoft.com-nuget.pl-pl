---
title: "Protokoły nuget.org | Dokumentacja firmy Microsoft"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Protokoły nuget.org zmieniające się do interakcji z klientów NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="731af-103">Protokoły nuget.org</span><span class="sxs-lookup"><span data-stu-id="731af-103">nuget.org Protocols</span></span>

<span data-ttu-id="731af-104">Wchodzić w interakcje z nuget.org, klienci muszą wykonać niektórych protokołów.</span><span class="sxs-lookup"><span data-stu-id="731af-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="731af-105">Ponieważ rozwijają zachować te protokoły, klienci muszą identyfikują wersja protokołu używanego podczas wywoływania metody nuget.org określonych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="731af-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="731af-106">Dzięki temu nuget.org wprowadzenie zmian w sposób nierozdzielające starego klientów.</span><span class="sxs-lookup"><span data-stu-id="731af-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="731af-107">Interfejsy API udokumentowany na tej stronie są specyficzne dla nuget.org i nie ma żadnych oczekiwania w innych implementacjach serwera NuGet dodać te interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="731af-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="731af-108">Informacje o interfejsie API NuGet szeroko implementowany w ekosystemie NuGet, zobacz [Przegląd interfejsu API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="731af-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="731af-109">Ten temat zawiera listę różnych protokołów, jak i kiedy zaczynają istnienia.</span><span class="sxs-lookup"><span data-stu-id="731af-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="731af-110">Wersja protokołu NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="731af-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="731af-111">4.1.0 protokołu Określa użycie kluczy Sprawdź zakres do interakcji z usługami innych niż nuget.org pakietu do konta nuget.org.</span><span class="sxs-lookup"><span data-stu-id="731af-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="731af-112">Należy pamiętać, że `4.1.0` wersji liczba to ciąg nieprzezroczyste, ale dzieje się pokrywa się z pierwszej wersji oficjalnego klienta NuGet, który obsługuje tego protokołu.</span><span class="sxs-lookup"><span data-stu-id="731af-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="731af-113">Sprawdzanie poprawności temu klucze interfejsu API utworzonych przez użytkownika są używane tylko z nuget.org i tej weryfikacji lub Weryfikacja od usługi innej firmy jest obsługiwana za pomocą kluczy Sprawdź zakres jednorazowego użytku.</span><span class="sxs-lookup"><span data-stu-id="731af-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="731af-114">Te klucze Sprawdź zakres może służyć do sprawdzania, czy pakiet należy do określonego użytkownika (konto) na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="731af-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="731af-115">Wymagania klienta</span><span class="sxs-lookup"><span data-stu-id="731af-115">Client requirement</span></span>

<span data-ttu-id="731af-116">Klienci są wymagane do przekazania następujący nagłówek, podczas tworzenia wywołań interfejsu API **wypychania** pakietów do nuget.org:</span><span class="sxs-lookup"><span data-stu-id="731af-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="731af-117">Należy pamiętać, że istniejące `X-NuGet-Client-Version` nagłówka ma tę samą funkcję, ale jest teraz przestarzałe i nie powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="731af-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="731af-118">**Wypychania** samego protokołu jest opisany w dokumentacji dotyczącej [ `PackagePublish` zasobów](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="731af-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="731af-119">Jeśli klient współdziała z usług zewnętrznych i należy sprawdzić, czy pakiet należy do określonego użytkownika (konto), powinna używać protokołu następujące i używać kluczy Sprawdź zakres i nie klucze interfejsu API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="731af-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="731af-120">Interfejs API do żądania klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="731af-120">API to request a verify-scope key</span></span>

<span data-ttu-id="731af-121">Ten interfejs API jest używany do pobierania klucz, sprawdź, czy zakres autora nuget.org, można sprawdzić poprawności pakietu posiadanych przez nią.</span><span class="sxs-lookup"><span data-stu-id="731af-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="731af-122">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="731af-122">Request parameters</span></span>

<span data-ttu-id="731af-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="731af-123">Name</span></span>           | <span data-ttu-id="731af-124">W</span><span class="sxs-lookup"><span data-stu-id="731af-124">In</span></span>     | <span data-ttu-id="731af-125">Typ</span><span class="sxs-lookup"><span data-stu-id="731af-125">Type</span></span>   | <span data-ttu-id="731af-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="731af-126">Required</span></span> | <span data-ttu-id="731af-127">Uwagi</span><span class="sxs-lookup"><span data-stu-id="731af-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="731af-128">ID</span><span class="sxs-lookup"><span data-stu-id="731af-128">ID</span></span>             | <span data-ttu-id="731af-129">Adres URL</span><span class="sxs-lookup"><span data-stu-id="731af-129">URL</span></span>    | <span data-ttu-id="731af-130">string</span><span class="sxs-lookup"><span data-stu-id="731af-130">string</span></span> | <span data-ttu-id="731af-131">Tak</span><span class="sxs-lookup"><span data-stu-id="731af-131">yes</span></span>      | <span data-ttu-id="731af-132">Identidier pakiet, dla którego wymagany jest klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="731af-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="731af-133">WERSJA</span><span class="sxs-lookup"><span data-stu-id="731af-133">VERSION</span></span>        | <span data-ttu-id="731af-134">Adres URL</span><span class="sxs-lookup"><span data-stu-id="731af-134">URL</span></span>    | <span data-ttu-id="731af-135">string</span><span class="sxs-lookup"><span data-stu-id="731af-135">string</span></span> | <span data-ttu-id="731af-136">Brak</span><span class="sxs-lookup"><span data-stu-id="731af-136">no</span></span>       | <span data-ttu-id="731af-137">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="731af-137">The package version</span></span>
<span data-ttu-id="731af-138">ApiKey-X-NuGet</span><span class="sxs-lookup"><span data-stu-id="731af-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="731af-139">nagłówek</span><span class="sxs-lookup"><span data-stu-id="731af-139">Header</span></span> | <span data-ttu-id="731af-140">string</span><span class="sxs-lookup"><span data-stu-id="731af-140">string</span></span> | <span data-ttu-id="731af-141">Tak</span><span class="sxs-lookup"><span data-stu-id="731af-141">yes</span></span>      | <span data-ttu-id="731af-142">Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="731af-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="731af-143">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="731af-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="731af-144">Interfejs API, aby zweryfikować klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="731af-144">API to verify the verify scope key</span></span>

<span data-ttu-id="731af-145">Ten interfejs API jest używany do sprawdzania poprawności klucza zakresu Sprawdź posiadane przez autora nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="731af-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="731af-146">Parametry żądania</span><span class="sxs-lookup"><span data-stu-id="731af-146">Request parameters</span></span>

<span data-ttu-id="731af-147">Nazwa</span><span class="sxs-lookup"><span data-stu-id="731af-147">Name</span></span>           | <span data-ttu-id="731af-148">W</span><span class="sxs-lookup"><span data-stu-id="731af-148">In</span></span>     | <span data-ttu-id="731af-149">Typ</span><span class="sxs-lookup"><span data-stu-id="731af-149">Type</span></span>   | <span data-ttu-id="731af-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="731af-150">Required</span></span> | <span data-ttu-id="731af-151">Uwagi</span><span class="sxs-lookup"><span data-stu-id="731af-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="731af-152">ID</span><span class="sxs-lookup"><span data-stu-id="731af-152">ID</span></span>             | <span data-ttu-id="731af-153">Adres URL</span><span class="sxs-lookup"><span data-stu-id="731af-153">URL</span></span>    | <span data-ttu-id="731af-154">string</span><span class="sxs-lookup"><span data-stu-id="731af-154">string</span></span> | <span data-ttu-id="731af-155">Tak</span><span class="sxs-lookup"><span data-stu-id="731af-155">yes</span></span>      | <span data-ttu-id="731af-156">Identyfikator pakietu, dla którego wymagany jest klucz Sprawdź zakres</span><span class="sxs-lookup"><span data-stu-id="731af-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="731af-157">WERSJA</span><span class="sxs-lookup"><span data-stu-id="731af-157">VERSION</span></span>        | <span data-ttu-id="731af-158">Adres URL</span><span class="sxs-lookup"><span data-stu-id="731af-158">URL</span></span>    | <span data-ttu-id="731af-159">string</span><span class="sxs-lookup"><span data-stu-id="731af-159">string</span></span> | <span data-ttu-id="731af-160">Brak</span><span class="sxs-lookup"><span data-stu-id="731af-160">no</span></span>       | <span data-ttu-id="731af-161">Wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="731af-161">The package version</span></span>
<span data-ttu-id="731af-162">ApiKey-X-NuGet</span><span class="sxs-lookup"><span data-stu-id="731af-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="731af-163">nagłówek</span><span class="sxs-lookup"><span data-stu-id="731af-163">Header</span></span> | <span data-ttu-id="731af-164">string</span><span class="sxs-lookup"><span data-stu-id="731af-164">string</span></span> | <span data-ttu-id="731af-165">Tak</span><span class="sxs-lookup"><span data-stu-id="731af-165">yes</span></span>      | <span data-ttu-id="731af-166">Na przykład:`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="731af-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="731af-167">Ten klucz interfejsu API zakresu Sprawdź utraci ważność za dni lub przy pierwszym użyciu cokolwiek nastąpi najpierw.</span><span class="sxs-lookup"><span data-stu-id="731af-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="731af-168">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="731af-168">Response</span></span>

<span data-ttu-id="731af-169">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="731af-169">Status Code</span></span> | <span data-ttu-id="731af-170">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="731af-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="731af-171">200</span><span class="sxs-lookup"><span data-stu-id="731af-171">200</span></span>         | <span data-ttu-id="731af-172">Klucz interfejsu API jest nieprawidłowa</span><span class="sxs-lookup"><span data-stu-id="731af-172">The API key is valid</span></span>
<span data-ttu-id="731af-173">403</span><span class="sxs-lookup"><span data-stu-id="731af-173">403</span></span>         | <span data-ttu-id="731af-174">Klucz interfejsu API jest nieprawidłowa lub nie jest autoryzowany do wypychania na pakiecie</span><span class="sxs-lookup"><span data-stu-id="731af-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="731af-175">404</span><span class="sxs-lookup"><span data-stu-id="731af-175">404</span></span>         | <span data-ttu-id="731af-176">Pakiet odwołuje się `ID` i `VERSION` (opcjonalnie) nie istnieje</span><span class="sxs-lookup"><span data-stu-id="731af-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
