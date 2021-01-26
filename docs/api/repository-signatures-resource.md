---
title: Sygnatury repozytorium, interfejs API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Zasób sygnatur repozytorium umożliwia klientom źródła pakietów anonsowanie możliwości podpisywania repozytorium.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775334"
---
# <a name="repository-signatures"></a><span data-ttu-id="3c7ca-103">Podpisy repozytorium</span><span class="sxs-lookup"><span data-stu-id="3c7ca-103">Repository signatures</span></span>

<span data-ttu-id="3c7ca-104">Jeśli źródło pakietu obsługuje dodawanie podpisów repozytorium do opublikowanych pakietów, możliwe jest, aby klient określił certyfikaty podpisywania używane przez źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="3c7ca-105">Ten zasób umożliwia klientom wykrycie, czy podpisany pakiet repozytorium został naruszony, czy ma nieoczekiwany certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="3c7ca-106">Zasób używany do pobierania informacji o sygnaturze tego repozytorium jest `RepositorySignatures` zasobem znalezionym w [indeksie usługi](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3c7ca-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="3c7ca-107">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="3c7ca-107">Versioning</span></span>

<span data-ttu-id="3c7ca-108">`@type`Używana jest następująca wartość:</span><span class="sxs-lookup"><span data-stu-id="3c7ca-108">The following `@type` value is used:</span></span>

<span data-ttu-id="3c7ca-109">@type wartościami</span><span class="sxs-lookup"><span data-stu-id="3c7ca-109">@type value</span></span>                | <span data-ttu-id="3c7ca-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3c7ca-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="3c7ca-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="3c7ca-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="3c7ca-112">Początkowa wersja</span><span class="sxs-lookup"><span data-stu-id="3c7ca-112">The initial release</span></span>
<span data-ttu-id="3c7ca-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="3c7ca-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="3c7ca-114">Obsługiwane przez klienta NuGet v 4.9 +</span><span class="sxs-lookup"><span data-stu-id="3c7ca-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="3c7ca-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="3c7ca-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="3c7ca-116">Umożliwia włączenie funkcji `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="3c7ca-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="3c7ca-117">Obsługiwane przez klienta NuGet v 5.0 +</span><span class="sxs-lookup"><span data-stu-id="3c7ca-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="3c7ca-118">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="3c7ca-118">Base URL</span></span>

<span data-ttu-id="3c7ca-119">Adres URL punktu wejścia dla następujących interfejsów API jest wartością `@id` Właściwości skojarzoną z wymienioną powyżej wartością zasobu `@type` .</span><span class="sxs-lookup"><span data-stu-id="3c7ca-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="3c7ca-120">W tym temacie jest stosowany symbol zastępczy URL `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="3c7ca-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="3c7ca-121">Należy pamiętać, że w przeciwieństwie do innych zasobów `{@id}` adres URL musi być obsługiwany za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3c7ca-122">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="3c7ca-122">HTTP methods</span></span>

<span data-ttu-id="3c7ca-123">Wszystkie adresy URL Znalezione w zasobie sygnatur repozytorium obsługują tylko metody HTTP `GET` i `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="3c7ca-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="3c7ca-124">Indeks sygnatur repozytorium</span><span class="sxs-lookup"><span data-stu-id="3c7ca-124">Repository signatures index</span></span>

<span data-ttu-id="3c7ca-125">Indeks sygnatur repozytorium zawiera dwie informacje:</span><span class="sxs-lookup"><span data-stu-id="3c7ca-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="3c7ca-126">Czy wszystkie pakiety Znalezione w źródle są podpisane przez to źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="3c7ca-127">Lista certyfikatów używanych przez źródło pakietu do podpisywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="3c7ca-128">W większości przypadków Lista certyfikatów zostanie kiedykolwiek dołączona do programu.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="3c7ca-129">Nowe certyfikaty zostaną dodane do listy, gdy poprzedni certyfikat podpisywania wygasł, a źródło pakietu musi zacząć korzystać z nowego certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="3c7ca-130">Jeśli certyfikat zostanie usunięty z listy, oznacza to, że wszystkie podpisy pakietu utworzone przy użyciu usuniętego certyfikatu podpisywania nie powinny już być uznawane za prawidłowe przez klienta.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="3c7ca-131">W takim przypadku podpis pakietu (ale niekoniecznie jest to pakiet) jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="3c7ca-132">Zasady klienta mogą zezwalać na instalowanie pakietu jako niepodpisane.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="3c7ca-133">W przypadku odwoływania certyfikatów (np. złamania klucza) źródło pakietu powinno ponownie podpisać wszystkie pakiety podpisane przez odnośny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="3c7ca-134">Ponadto źródło pakietu powinno usunąć odnośny certyfikat z listy certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="3c7ca-135">Poniższe żądanie Pobiera indeks sygnatur repozytorium.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="3c7ca-136">Indeks sygnatury repozytorium jest dokumentem JSON zawierającym obiekt o następujących właściwościach:</span><span class="sxs-lookup"><span data-stu-id="3c7ca-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="3c7ca-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3c7ca-137">Name</span></span>                | <span data-ttu-id="3c7ca-138">Typ</span><span class="sxs-lookup"><span data-stu-id="3c7ca-138">Type</span></span>             | <span data-ttu-id="3c7ca-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3c7ca-139">Required</span></span> | <span data-ttu-id="3c7ca-140">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3c7ca-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="3c7ca-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="3c7ca-141">allRepositorySigned</span></span> | <span data-ttu-id="3c7ca-142">boolean</span><span class="sxs-lookup"><span data-stu-id="3c7ca-142">boolean</span></span>          | <span data-ttu-id="3c7ca-143">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-143">yes</span></span>      | <span data-ttu-id="3c7ca-144">Musi znajdować się `false` w zasobach 4.7.0 i 4.9.0</span><span class="sxs-lookup"><span data-stu-id="3c7ca-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="3c7ca-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="3c7ca-145">signingCertificates</span></span> | <span data-ttu-id="3c7ca-146">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="3c7ca-146">array of objects</span></span> | <span data-ttu-id="3c7ca-147">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-147">yes</span></span>      | 

<span data-ttu-id="3c7ca-148">Wartość `allRepositorySigned` logiczna jest ustawiona na false, jeśli źródło pakietu ma niektóre pakiety, które nie mają sygnatury repozytorium.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="3c7ca-149">Jeśli wartość logiczna ma wartość true, wszystkie pakiety dostępne w źródle muszą mieć sygnaturę repozytorium wygenerowaną przez jeden z certyfikatów podpisywania wymienionych w temacie `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="3c7ca-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="3c7ca-150">`allRepositorySigned`Wartość logiczna musi mieć wartość false w zasobach 4.7.0 i 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="3c7ca-151">Klienci programu NuGet v 4.7, v 4.8 i v 4.9 nie mogą instalować pakietów ze źródeł, `allRepositorySigned` dla których ustawiono wartość true.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="3c7ca-152">`signingCertificates`Jeśli wartość logiczna ma wartość true, w tablicy powinien znajdować się co najmniej jeden certyfikat podpisywania `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="3c7ca-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="3c7ca-153">Jeśli tablica jest pusta i `allRepositorySigned` ma ustawioną wartość true, wszystkie pakiety ze źródła powinny być traktowane jako nieprawidłowe, mimo że zasady klienta nadal mogą zezwalać na użycie pakietów.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="3c7ca-154">Każdy element w tej tablicy jest obiektem JSON z poniższymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="3c7ca-155">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3c7ca-155">Name</span></span>         | <span data-ttu-id="3c7ca-156">Typ</span><span class="sxs-lookup"><span data-stu-id="3c7ca-156">Type</span></span>   | <span data-ttu-id="3c7ca-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3c7ca-157">Required</span></span> | <span data-ttu-id="3c7ca-158">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3c7ca-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="3c7ca-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="3c7ca-159">contentUrl</span></span>   | <span data-ttu-id="3c7ca-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="3c7ca-160">string</span></span> | <span data-ttu-id="3c7ca-161">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-161">yes</span></span>      | <span data-ttu-id="3c7ca-162">Bezwzględny adres URL do certyfikatu publicznego zakodowanego algorytmem DER</span><span class="sxs-lookup"><span data-stu-id="3c7ca-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="3c7ca-163">odcisków palców</span><span class="sxs-lookup"><span data-stu-id="3c7ca-163">fingerprints</span></span> | <span data-ttu-id="3c7ca-164">object</span><span class="sxs-lookup"><span data-stu-id="3c7ca-164">object</span></span> | <span data-ttu-id="3c7ca-165">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-165">yes</span></span>      |
<span data-ttu-id="3c7ca-166">subject</span><span class="sxs-lookup"><span data-stu-id="3c7ca-166">subject</span></span>      | <span data-ttu-id="3c7ca-167">ciąg</span><span class="sxs-lookup"><span data-stu-id="3c7ca-167">string</span></span> | <span data-ttu-id="3c7ca-168">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-168">yes</span></span>      | <span data-ttu-id="3c7ca-169">Nazwa wyróżniająca podmiotu z certyfikatu</span><span class="sxs-lookup"><span data-stu-id="3c7ca-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="3c7ca-170">issuer</span><span class="sxs-lookup"><span data-stu-id="3c7ca-170">issuer</span></span>       | <span data-ttu-id="3c7ca-171">ciąg</span><span class="sxs-lookup"><span data-stu-id="3c7ca-171">string</span></span> | <span data-ttu-id="3c7ca-172">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-172">yes</span></span>      | <span data-ttu-id="3c7ca-173">Nazwa wyróżniająca wystawcy certyfikatu</span><span class="sxs-lookup"><span data-stu-id="3c7ca-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="3c7ca-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="3c7ca-174">notBefore</span></span>    | <span data-ttu-id="3c7ca-175">ciąg</span><span class="sxs-lookup"><span data-stu-id="3c7ca-175">string</span></span> | <span data-ttu-id="3c7ca-176">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-176">yes</span></span>      | <span data-ttu-id="3c7ca-177">Początkowe sygnatura czasowa okresu ważności certyfikatu</span><span class="sxs-lookup"><span data-stu-id="3c7ca-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="3c7ca-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="3c7ca-178">notAfter</span></span>     | <span data-ttu-id="3c7ca-179">ciąg</span><span class="sxs-lookup"><span data-stu-id="3c7ca-179">string</span></span> | <span data-ttu-id="3c7ca-180">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-180">yes</span></span>      | <span data-ttu-id="3c7ca-181">Końcowe sygnatura czasowa okresu ważności certyfikatu</span><span class="sxs-lookup"><span data-stu-id="3c7ca-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="3c7ca-182">Należy pamiętać, że `contentUrl` jest to wymagane do objęcia usługą za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="3c7ca-183">Ten adres URL nie ma określonego wzorca adresu URL i musi być dynamicznie odnajdywany przy użyciu tego dokumentu indeksu sygnatur repozytorium.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="3c7ca-184">Wszystkie właściwości w tym obiekcie (oprócz `contentUrl` ) muszą być wyprowadzane z certyfikatu znalezionego w `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="3c7ca-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="3c7ca-185">Te właściwości, które można uzyskać jako wygodę do minimalizowania rundy.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="3c7ca-186">`fingerprints`Obiekt ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3c7ca-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="3c7ca-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3c7ca-187">Name</span></span>                   | <span data-ttu-id="3c7ca-188">Typ</span><span class="sxs-lookup"><span data-stu-id="3c7ca-188">Type</span></span>   | <span data-ttu-id="3c7ca-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3c7ca-189">Required</span></span> | <span data-ttu-id="3c7ca-190">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3c7ca-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="3c7ca-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="3c7ca-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="3c7ca-192">ciąg</span><span class="sxs-lookup"><span data-stu-id="3c7ca-192">string</span></span> | <span data-ttu-id="3c7ca-193">tak</span><span class="sxs-lookup"><span data-stu-id="3c7ca-193">yes</span></span>      | <span data-ttu-id="3c7ca-194">Odcisk palca SHA-256</span><span class="sxs-lookup"><span data-stu-id="3c7ca-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="3c7ca-195">Nazwa klucza `2.16.840.1.101.3.4.2.1` jest identyfikatorem OID algorytmu wyznaczania wartości skrótu SHA-256.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="3c7ca-196">Wszystkie wartości skrótu muszą być pisane małymi literami, kodowane w formacie szesnastkowym.</span><span class="sxs-lookup"><span data-stu-id="3c7ca-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3c7ca-197">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="3c7ca-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="3c7ca-198">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="3c7ca-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
