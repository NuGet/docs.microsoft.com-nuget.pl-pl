---
title: Podpisy repozytorium, interfejs API programu NuGet | Dokumentacja firmy Microsoft
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Zasób podpisów repozytorium umożliwia klientom źródła pakietu zawiera informacje o repozytorium, ich możliwości podpisywania.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547984"
---
# <a name="repository-signatures"></a><span data-ttu-id="6f4e9-103">Podpisy repozytorium</span><span class="sxs-lookup"><span data-stu-id="6f4e9-103">Repository signatures</span></span>

<span data-ttu-id="6f4e9-104">Jeśli źródło pakietu obsługuje dodawanie podpisach repozytorium na opublikowane pakiety, istnieje możliwość dla klienta określić certyfikaty podpisywania, które są używane przez źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="6f4e9-105">Ten zasób zezwala klientom na wykrywanie, czy repozytorium jest podpisany pakiet został zmodyfikowany lub ma nieoczekiwany certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="6f4e9-106">Zasób, używany do pobierania tych informacji podpisu repozytorium jest `RepositorySignatures` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6f4e9-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="6f4e9-107">NuGet.org rozpocznie się ogłoszenie `RepositorySignatures` zasobów w niedalekiej przyszłości.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="6f4e9-108">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="6f4e9-108">Versioning</span></span>

<span data-ttu-id="6f4e9-109">Następujące `@type` zostanie użyta wartość:</span><span class="sxs-lookup"><span data-stu-id="6f4e9-109">The following `@type` value is used:</span></span>

<span data-ttu-id="6f4e9-110">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="6f4e9-110">@type value</span></span>                | <span data-ttu-id="6f4e9-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6f4e9-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="6f4e9-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="6f4e9-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="6f4e9-113">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="6f4e9-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="6f4e9-114">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="6f4e9-114">Base URL</span></span>

<span data-ttu-id="6f4e9-115">Adres URL punktu wejścia dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="6f4e9-116">W tym temacie używany zastępczego adresu URL `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="6f4e9-117">Należy pamiętać, że w przeciwieństwie do innych zasobów `{@id}` adres URL jest wymagany ma być obsługiwana za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6f4e9-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="6f4e9-118">HTTP methods</span></span>

<span data-ttu-id="6f4e9-119">Wszystkie adresy URL w opisach repozytorium podpisów zasobów pomocy technicznej tylko protokół HTTP metod `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="6f4e9-120">Repozytorium sygnatury indeksu</span><span class="sxs-lookup"><span data-stu-id="6f4e9-120">Repository signatures index</span></span>

<span data-ttu-id="6f4e9-121">Indeks sygnatury repozytorium zawiera dwa rodzaje informacji:</span><span class="sxs-lookup"><span data-stu-id="6f4e9-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="6f4e9-122">Czy nie znaleziono w źródle wszystkie pakiety są podpisane przez tego źródła pakietów repozytorium.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="6f4e9-123">Lista certyfikatów używanych przez źródła pakietu do podpisywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="6f4e9-124">W większości przypadków zostaną tylko dołączone do listy certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="6f4e9-125">Nowe certyfikaty zostaną dodane do listy Jeśli poprzedni certyfikat podpisywania utracił ważność i źródła pakietu musi rozpocząć korzystanie z nowego certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="6f4e9-126">Jeśli certyfikat został usunięty z listy, oznacza to, wszystkich podpisów pakietów utworzonych za pomocą usunięto certyfikat podpisywania powinny już być uważany za prawidłowy przez klienta.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="6f4e9-127">W tym przypadku podpisu pakietu (ale nie musi to być pakietu) jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="6f4e9-128">Zasady klienta może zezwalać na instalowanie pakietu jako bez znaku.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="6f4e9-129">W przypadku odwołania certyfikatów (np. klucza naruszenia zabezpieczeń) źródła pakietu powinien ponownie podpisać wszystkie pakiety podpisane przez dotyczy certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="6f4e9-130">Ponadto źródła pakietu należy usunąć dotyczy certyfikatu z listy certyfikatów podpisywania.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="6f4e9-131">Następujące żądanie pobiera indeks sygnatury repozytorium.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="6f4e9-132">Indeks sygnatury repozytorium jest dokumentem JSON, który zawiera obiekt z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="6f4e9-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="6f4e9-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6f4e9-133">Name</span></span>                | <span data-ttu-id="6f4e9-134">Typ</span><span class="sxs-lookup"><span data-stu-id="6f4e9-134">Type</span></span>             | <span data-ttu-id="6f4e9-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6f4e9-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="6f4e9-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="6f4e9-136">allRepositorySigned</span></span> | <span data-ttu-id="6f4e9-137">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="6f4e9-137">boolean</span></span>          | <span data-ttu-id="6f4e9-138">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-138">yes</span></span>
<span data-ttu-id="6f4e9-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="6f4e9-139">signingCertificates</span></span> | <span data-ttu-id="6f4e9-140">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="6f4e9-140">array of objects</span></span> | <span data-ttu-id="6f4e9-141">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-141">yes</span></span>

<span data-ttu-id="6f4e9-142">`allRepositorySigned` Atrybut typu wartość logiczna jest ustawiona na wartość false, jeśli źródło pakietu ma kilka pakietów, dla których brak podpisu w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="6f4e9-143">Jeśli wartość logiczna ma wartość true, wszystkie pakiety dostępne na źródło musi mieć podpis repozytorium utworzone za pomocą jednej z certyfikatów podpisywania, o których wspomniano w `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="6f4e9-144">Powinna istnieć co najmniej jednego certyfikatu podpisywania w `signingCertificates` tablicy, jeśli `allRepositorySigned` atrybut typu wartość logiczna jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="6f4e9-145">Jeśli tablica jest pusta i `allRepositorySigned` jest ustawiona na wartość true, wszystkie pakiety ze źródła należy uwzględnić nieprawidłowe, mimo że zasady klienta nadal zezwalają na użycie pakietów.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="6f4e9-146">Każdy element w tej tablicy jest obiekt JSON z następującymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="6f4e9-147">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6f4e9-147">Name</span></span>         | <span data-ttu-id="6f4e9-148">Typ</span><span class="sxs-lookup"><span data-stu-id="6f4e9-148">Type</span></span>   | <span data-ttu-id="6f4e9-149">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6f4e9-149">Required</span></span> | <span data-ttu-id="6f4e9-150">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6f4e9-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="6f4e9-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="6f4e9-151">contentUrl</span></span>   | <span data-ttu-id="6f4e9-152">string</span><span class="sxs-lookup"><span data-stu-id="6f4e9-152">string</span></span> | <span data-ttu-id="6f4e9-153">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-153">yes</span></span>      | <span data-ttu-id="6f4e9-154">Bezwzględny adres URL do algorytmem DER certyfikatu publicznego</span><span class="sxs-lookup"><span data-stu-id="6f4e9-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="6f4e9-155">odciski palców</span><span class="sxs-lookup"><span data-stu-id="6f4e9-155">fingerprints</span></span> | <span data-ttu-id="6f4e9-156">object</span><span class="sxs-lookup"><span data-stu-id="6f4e9-156">object</span></span> | <span data-ttu-id="6f4e9-157">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-157">yes</span></span>      |
<span data-ttu-id="6f4e9-158">Temat</span><span class="sxs-lookup"><span data-stu-id="6f4e9-158">subject</span></span>      | <span data-ttu-id="6f4e9-159">string</span><span class="sxs-lookup"><span data-stu-id="6f4e9-159">string</span></span> | <span data-ttu-id="6f4e9-160">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-160">yes</span></span>      | <span data-ttu-id="6f4e9-161">Nazwa wyróżniająca podmiotu z certyfikatu</span><span class="sxs-lookup"><span data-stu-id="6f4e9-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="6f4e9-162">issuer</span><span class="sxs-lookup"><span data-stu-id="6f4e9-162">issuer</span></span>       | <span data-ttu-id="6f4e9-163">string</span><span class="sxs-lookup"><span data-stu-id="6f4e9-163">string</span></span> | <span data-ttu-id="6f4e9-164">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-164">yes</span></span>      | <span data-ttu-id="6f4e9-165">Nazwa wyróżniająca wystawcy certyfikatu</span><span class="sxs-lookup"><span data-stu-id="6f4e9-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="6f4e9-166">nie wcześniej niż</span><span class="sxs-lookup"><span data-stu-id="6f4e9-166">notBefore</span></span>    | <span data-ttu-id="6f4e9-167">string</span><span class="sxs-lookup"><span data-stu-id="6f4e9-167">string</span></span> | <span data-ttu-id="6f4e9-168">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-168">yes</span></span>      | <span data-ttu-id="6f4e9-169">Sygnatura czasowa początkowy okres ważności certyfikatu</span><span class="sxs-lookup"><span data-stu-id="6f4e9-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="6f4e9-170">nie później niż</span><span class="sxs-lookup"><span data-stu-id="6f4e9-170">notAfter</span></span>     | <span data-ttu-id="6f4e9-171">string</span><span class="sxs-lookup"><span data-stu-id="6f4e9-171">string</span></span> | <span data-ttu-id="6f4e9-172">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-172">yes</span></span>      | <span data-ttu-id="6f4e9-173">Sygnatura czasowa zakończenia okresu ważności certyfikatu</span><span class="sxs-lookup"><span data-stu-id="6f4e9-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="6f4e9-174">Należy pamiętać, że `contentUrl` musi być obsługiwana za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="6f4e9-175">Ten adres URL ma nie określonemu wzorcowi URL i musi zostać dynamicznie odnalezione za pomocą tego dokumentu repozytorium sygnatury indeksu.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="6f4e9-176">Wszystkie właściwości w tym obiekcie (aside z `contentUrl`) musi być derivable z certyfikatu adrese `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="6f4e9-177">Te właściwości derivable są udostępniane dla wygody, aby zminimalizować liczbę rund.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="6f4e9-178">`fingerprints` Obiekt ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6f4e9-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="6f4e9-179">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6f4e9-179">Name</span></span>                   | <span data-ttu-id="6f4e9-180">Typ</span><span class="sxs-lookup"><span data-stu-id="6f4e9-180">Type</span></span>   | <span data-ttu-id="6f4e9-181">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6f4e9-181">Required</span></span> | <span data-ttu-id="6f4e9-182">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6f4e9-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="6f4e9-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="6f4e9-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="6f4e9-184">string</span><span class="sxs-lookup"><span data-stu-id="6f4e9-184">string</span></span> | <span data-ttu-id="6f4e9-185">Tak</span><span class="sxs-lookup"><span data-stu-id="6f4e9-185">yes</span></span>      | <span data-ttu-id="6f4e9-186">Odcisk palca SHA-256.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="6f4e9-187">Nazwa klucza `2.16.840.1.101.3.4.2.1` jest OID algorytmu wyznaczania wartości skrótu SHA-256.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="6f4e9-188">Wszystkie wartości skrótu musi być mała litera, zakodowanego szesnastkowo ciągów reprezentujących szyfrowanego wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="6f4e9-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6f4e9-189">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="6f4e9-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="6f4e9-190">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="6f4e9-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
