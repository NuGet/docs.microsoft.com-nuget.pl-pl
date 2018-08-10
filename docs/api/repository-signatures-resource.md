---
title: Podpisy repozytorium, interfejs API programu NuGet | Dokumentacja firmy Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Zasób podpisów repozytorium umożliwia klientom źródła pakietu zawiera informacje o repozytorium, ich możliwości podpisywania.
keywords: Podpisy repozytorium NuGet interfejsu API, nuget.org podpisywania certyfikatów, podpisywanie pakietów nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020572"
---
# <a name="repository-signatures"></a><span data-ttu-id="bf6f3-104">Podpisy repozytorium</span><span class="sxs-lookup"><span data-stu-id="bf6f3-104">Repository signatures</span></span>

<span data-ttu-id="bf6f3-105">Jeśli źródło pakietu obsługuje dodawanie podpisach repozytorium na opublikowane pakiety, istnieje możliwość dla klienta określić certyfikaty podpisywania, które są używane przez źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="bf6f3-106">Ten zasób zezwala klientom na wykrywanie, czy repozytorium jest podpisany pakiet został zmodyfikowany lub ma nieoczekiwany certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="bf6f3-107">Zasób, używany do pobierania tych informacji podpisu repozytorium jest `RepositorySignatures` można znaleźć zasobu w [indeks usług](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="bf6f3-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="bf6f3-108">NuGet.org rozpocznie się ogłoszenie `RepositorySignatures` zasobów w niedalekiej przyszłości.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="bf6f3-109">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="bf6f3-109">Versioning</span></span>

<span data-ttu-id="bf6f3-110">Następujące `@type` zostanie użyta wartość:</span><span class="sxs-lookup"><span data-stu-id="bf6f3-110">The following `@type` value is used:</span></span>

<span data-ttu-id="bf6f3-111">@type Wartość</span><span class="sxs-lookup"><span data-stu-id="bf6f3-111">@type value</span></span>                | <span data-ttu-id="bf6f3-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bf6f3-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="bf6f3-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="bf6f3-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="bf6f3-114">Wersja początkowa</span><span class="sxs-lookup"><span data-stu-id="bf6f3-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="bf6f3-115">Podstawowy adres URL</span><span class="sxs-lookup"><span data-stu-id="bf6f3-115">Base URL</span></span>

<span data-ttu-id="bf6f3-116">Adres URL punktu wejścia dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="bf6f3-117">W tym temacie używany zastępczego adresu URL `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="bf6f3-118">Należy pamiętać, że w przeciwieństwie do innych zasobów `{@id}` adres URL jest wymagany ma być obsługiwana za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="bf6f3-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="bf6f3-119">HTTP methods</span></span>

<span data-ttu-id="bf6f3-120">Wszystkie adresy URL w opisach repozytorium podpisów zasobów pomocy technicznej tylko protokół HTTP metod `GET` i `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="bf6f3-121">Repozytorium sygnatury indeksu</span><span class="sxs-lookup"><span data-stu-id="bf6f3-121">Repository signatures index</span></span>

<span data-ttu-id="bf6f3-122">Indeks sygnatury repozytorium zawiera dwa rodzaje informacji:</span><span class="sxs-lookup"><span data-stu-id="bf6f3-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="bf6f3-123">Czy nie znaleziono w źródle wszystkie pakiety są podpisane przez tego źródła pakietów repozytorium.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="bf6f3-124">Lista certyfikatów używanych przez źródła pakietu do podpisywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="bf6f3-125">W większości przypadków zostaną tylko dołączone do listy certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="bf6f3-126">Nowe certyfikaty zostaną dodane do listy Jeśli poprzedni certyfikat podpisywania utracił ważność i źródła pakietu musi rozpocząć korzystanie z nowego certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="bf6f3-127">Jeśli certyfikat został usunięty z listy, oznacza to, wszystkich podpisów pakietów utworzonych za pomocą usunięto certyfikat podpisywania powinny już być uważany za prawidłowy przez klienta.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="bf6f3-128">W tym przypadku podpisu pakietu (ale nie musi to być pakietu) jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="bf6f3-129">Zasady klienta może zezwalać na instalowanie pakietu jako bez znaku.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="bf6f3-130">W przypadku odwołania certyfikatów (np. klucza naruszenia zabezpieczeń) źródła pakietu powinien ponownie podpisać wszystkie pakiety podpisane przez dotyczy certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to resign all packages signed by the affected certificate.</span></span> <span data-ttu-id="bf6f3-131">Ponadto źródła pakietu należy usunąć dotyczy certyfikatu z listy certyfikatów podpisywania.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="bf6f3-132">Następujące żądanie pobiera indeks sygnatury repozytorium.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="bf6f3-133">Indeks sygnatury repozytorium jest dokumentem JSON, który zawiera obiekt z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="bf6f3-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="bf6f3-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bf6f3-134">Name</span></span>                | <span data-ttu-id="bf6f3-135">Typ</span><span class="sxs-lookup"><span data-stu-id="bf6f3-135">Type</span></span>             | <span data-ttu-id="bf6f3-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="bf6f3-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="bf6f3-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="bf6f3-137">allRepositorySigned</span></span> | <span data-ttu-id="bf6f3-138">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="bf6f3-138">boolean</span></span>          | <span data-ttu-id="bf6f3-139">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-139">yes</span></span>
<span data-ttu-id="bf6f3-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="bf6f3-140">signingCertificates</span></span> | <span data-ttu-id="bf6f3-141">Tablica obiektów</span><span class="sxs-lookup"><span data-stu-id="bf6f3-141">array of objects</span></span> | <span data-ttu-id="bf6f3-142">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-142">yes</span></span>

<span data-ttu-id="bf6f3-143">`allRepositorySigned` Atrybut typu wartość logiczna jest ustawiona na wartość false, jeśli źródło pakietu ma kilka pakietów, dla których brak podpisu w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="bf6f3-144">Jeśli wartość logiczna ma wartość true, wszystkie pakiety dostępne na źródło musi mieć podpis repozytorium utworzone za pomocą jednej z certyfikatów podpisywania, o których wspomniano w `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="bf6f3-145">Powinna istnieć co najmniej jednego certyfikatu podpisywania w `signingCertificates` tablicy, jeśli `allRepositorySigned` atrybut typu wartość logiczna jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="bf6f3-146">Jeśli tablica jest pusta i `allRepositorySigned` jest ustawiona na wartość true, wszystkie pakiety ze źródła należy uwzględnić nieprawidłowe, mimo że zasady klienta nadal zezwalają na użycie pakietów.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="bf6f3-147">Każdy element w tej tablicy jest obiekt JSON z następującymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="bf6f3-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bf6f3-148">Name</span></span>         | <span data-ttu-id="bf6f3-149">Typ</span><span class="sxs-lookup"><span data-stu-id="bf6f3-149">Type</span></span>   | <span data-ttu-id="bf6f3-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="bf6f3-150">Required</span></span> | <span data-ttu-id="bf6f3-151">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bf6f3-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="bf6f3-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="bf6f3-152">contentUrl</span></span>   | <span data-ttu-id="bf6f3-153">string</span><span class="sxs-lookup"><span data-stu-id="bf6f3-153">string</span></span> | <span data-ttu-id="bf6f3-154">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-154">yes</span></span>      | <span data-ttu-id="bf6f3-155">Bezwzględny adres URL do algorytmem DER certyfikatu publicznego</span><span class="sxs-lookup"><span data-stu-id="bf6f3-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="bf6f3-156">odciski palców</span><span class="sxs-lookup"><span data-stu-id="bf6f3-156">fingerprints</span></span> | <span data-ttu-id="bf6f3-157">object</span><span class="sxs-lookup"><span data-stu-id="bf6f3-157">object</span></span> | <span data-ttu-id="bf6f3-158">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-158">yes</span></span>      |
<span data-ttu-id="bf6f3-159">Temat</span><span class="sxs-lookup"><span data-stu-id="bf6f3-159">subject</span></span>      | <span data-ttu-id="bf6f3-160">string</span><span class="sxs-lookup"><span data-stu-id="bf6f3-160">string</span></span> | <span data-ttu-id="bf6f3-161">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-161">yes</span></span>      | <span data-ttu-id="bf6f3-162">Nazwa wyróżniająca podmiotu z certyfikatu</span><span class="sxs-lookup"><span data-stu-id="bf6f3-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="bf6f3-163">issuer</span><span class="sxs-lookup"><span data-stu-id="bf6f3-163">issuer</span></span>       | <span data-ttu-id="bf6f3-164">string</span><span class="sxs-lookup"><span data-stu-id="bf6f3-164">string</span></span> | <span data-ttu-id="bf6f3-165">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-165">yes</span></span>      | <span data-ttu-id="bf6f3-166">Nazwa wyróżniająca wystawcy certyfikatu</span><span class="sxs-lookup"><span data-stu-id="bf6f3-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="bf6f3-167">nie wcześniej niż</span><span class="sxs-lookup"><span data-stu-id="bf6f3-167">notBefore</span></span>    | <span data-ttu-id="bf6f3-168">string</span><span class="sxs-lookup"><span data-stu-id="bf6f3-168">string</span></span> | <span data-ttu-id="bf6f3-169">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-169">yes</span></span>      | <span data-ttu-id="bf6f3-170">Sygnatura czasowa początkowy okres ważności certyfikatu</span><span class="sxs-lookup"><span data-stu-id="bf6f3-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="bf6f3-171">nie później niż</span><span class="sxs-lookup"><span data-stu-id="bf6f3-171">notAfter</span></span>     | <span data-ttu-id="bf6f3-172">string</span><span class="sxs-lookup"><span data-stu-id="bf6f3-172">string</span></span> | <span data-ttu-id="bf6f3-173">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-173">yes</span></span>      | <span data-ttu-id="bf6f3-174">Sygnatura czasowa zakończenia okresu ważności certyfikatu</span><span class="sxs-lookup"><span data-stu-id="bf6f3-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="bf6f3-175">Należy pamiętać, że `contentUrl` musi być obsługiwana za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="bf6f3-176">Ten adres URL ma nie określonemu wzorcowi URL i musi zostać dynamicznie odnalezione za pomocą tego dokumentu repozytorium sygnatury indeksu.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="bf6f3-177">Wszystkie właściwości w tym obiekcie (aside z `contentUrl`) musi być derivable z certyfikatu adrese `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="bf6f3-178">Te właściwości derivable są udostępniane dla wygody, aby zminimalizować liczbę rund.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="bf6f3-179">`fingerprints` Obiekt ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="bf6f3-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="bf6f3-180">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bf6f3-180">Name</span></span>                   | <span data-ttu-id="bf6f3-181">Typ</span><span class="sxs-lookup"><span data-stu-id="bf6f3-181">Type</span></span>   | <span data-ttu-id="bf6f3-182">Wymagane</span><span class="sxs-lookup"><span data-stu-id="bf6f3-182">Required</span></span> | <span data-ttu-id="bf6f3-183">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bf6f3-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="bf6f3-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="bf6f3-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="bf6f3-185">string</span><span class="sxs-lookup"><span data-stu-id="bf6f3-185">string</span></span> | <span data-ttu-id="bf6f3-186">Tak</span><span class="sxs-lookup"><span data-stu-id="bf6f3-186">yes</span></span>      | <span data-ttu-id="bf6f3-187">Odcisk palca SHA-256.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="bf6f3-188">Nazwa klucza `2.16.840.1.101.3.4.2.1` jest OID algorytmu wyznaczania wartości skrótu SHA-256.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="bf6f3-189">Wszystkie wartości skrótu musi być mała litera, zakodowanego szesnastkowo ciągów reprezentujących szyfrowanego wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="bf6f3-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="bf6f3-190">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="bf6f3-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="bf6f3-191">Przykładowa odpowiedź</span><span class="sxs-lookup"><span data-stu-id="bf6f3-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
