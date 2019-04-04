---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921562"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="32c93-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="32c93-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="32c93-103">Racjonalne uzasadnienie</span><span class="sxs-lookup"><span data-stu-id="32c93-103">Rationale</span></span>

<span data-ttu-id="32c93-104">Wraz z wprowadzeniem [licencji wyrażeń](nuspec.md#license), wymaganie powstało mieć usługi reliable service zapewni tekst odwołania licencji poszczególnych identyfikatorów, identyfikatory wyjątek lub wyrażenia licencji.</span><span class="sxs-lookup"><span data-stu-id="32c93-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="32c93-105">Dodatkowe wymaganie wprowadzono dla tej usługi jest mają stabilny schemat adresu URL, który nie jest podatny na link rot, tak aby bezpiecznie używać go do zapewniania zgodności z poprzednimi wersjami starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="32c93-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="32c93-106">Licenses.nuget.org spełnia tę rolę.</span><span class="sxs-lookup"><span data-stu-id="32c93-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="32c93-107">Nuget.org używa go, aby zapewnić odwołanie tekst licencji dla pakietów, które określają licencję za pomocą wyrażenia licencji.</span><span class="sxs-lookup"><span data-stu-id="32c93-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> `nuget pack` <span data-ttu-id="32c93-108">lub pakowania z innymi [narzędzi klienckich](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) ustaw [ `licenseUrl` ](nuspec.md#licenseurl) element, aby wskazywał licenses.nuget.org w celu zapewnienia wstecznej zgodności ze starszymi klientami, które nie obsługują `license` element.</span><span class="sxs-lookup"><span data-stu-id="32c93-108">or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="32c93-109">Protokół</span><span class="sxs-lookup"><span data-stu-id="32c93-109">Protocol</span></span>

<span data-ttu-id="32c93-110">Licenses.nuget.org jest przeznaczony do przeglądania przez osoby w przeglądarkach, znajdują się odpowiedzi czytelnymi dla komputera.</span><span class="sxs-lookup"><span data-stu-id="32c93-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="32c93-111">Należy używać protokołu HTTPS, a żądania powinny zostać wykonane w określony sposób.</span><span class="sxs-lookup"><span data-stu-id="32c93-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="32c93-112">Obsługuje on tylko `GET` żądań.</span><span class="sxs-lookup"><span data-stu-id="32c93-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="32c93-113">Akceptuje wyrażeń licencji lub licencji wyjątek identyfikatory jako dane wejściowe w sposób określony poniżej.</span><span class="sxs-lookup"><span data-stu-id="32c93-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="32c93-114">Należy pamiętać, że wszystkie elementy wyrażenia licencji jest uwzględniana wielkość liter i w związku z tym wszystkie dane wejściowe do licenses.nuget.org jest uwzględniana wielkość liter jak również.</span><span class="sxs-lookup"><span data-stu-id="32c93-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="32c93-115">Wyrażenia licencji</span><span class="sxs-lookup"><span data-stu-id="32c93-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="32c93-116">Request</span><span class="sxs-lookup"><span data-stu-id="32c93-116">Request</span></span>

<span data-ttu-id="32c93-117">Wyrażenia licencji (w tym proste przypadków, gdy wyrażenie składa się z pojedynczej licencji) muszą być [zakodowane w adresie URL](https://tools.ietf.org/html/rfc3986#section-2.1) i używane jako ścieżka w żądaniu licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="32c93-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="32c93-118">Wyrażenie licencji</span><span class="sxs-lookup"><span data-stu-id="32c93-118">License expression</span></span> | <span data-ttu-id="32c93-119">Adres URL do użycia</span><span class="sxs-lookup"><span data-stu-id="32c93-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="32c93-120">MIT</span><span class="sxs-lookup"><span data-stu-id="32c93-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="32c93-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="32c93-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="32c93-122">(LGPL w wersji 2.0 — tylko przy użyciu Apache lub wyjątek FLTK-2.0+)</span><span class="sxs-lookup"><span data-stu-id="32c93-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="32c93-123">Usługa obsługuje tylko identyfikatory licencji i licencji wyjątek identyfikatorów, które są akceptowane przez nuget.org. Wszystkie wyrażenia licencji zawierających identyfikatory nieobsługiwany licencji lub licencji wyjątek identyfikatorów lub który jest niezgodny ze składnią wyrażeń licencji są uznawane za nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="32c93-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="32c93-124">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="32c93-124">Response</span></span>

<span data-ttu-id="32c93-125">Licenses.nuget.org odpowiada na żądania zawierające wyrażenia prawidłowej licencji z kodem stanu HTTP 200 i strony sieci web zawierająca opis licencji wyrażenia:</span><span class="sxs-lookup"><span data-stu-id="32c93-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="32c93-126">Jeśli podane wyrażenie licencji zawiera identyfikator licencji pojedynczej strony sieci web jest zwracane, który zawiera ten tekst odwołanie licencji;</span><span class="sxs-lookup"><span data-stu-id="32c93-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="32c93-127">Jeśli nie dostarczono licencji wyrażenie jest wyrażeniem złożonego licencji, strony sieci web jest zwracany, który zawiera wyrażenie licencji wraz z łączami do poszczególnych licencji lub licencji wyjątek odwołania.</span><span class="sxs-lookup"><span data-stu-id="32c93-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="32c93-128">Wszystkie żądania, które zawierają wyrażenia Nieprawidłowa licencja wyniku w odpowiedzi HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="32c93-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="32c93-129">Wyjątki licencji</span><span class="sxs-lookup"><span data-stu-id="32c93-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="32c93-130">Request</span><span class="sxs-lookup"><span data-stu-id="32c93-130">Request</span></span>

<span data-ttu-id="32c93-131">Identyfikatory wyjątek licencji musi być zakodowane w adresie URL i używane jako ścieżka w żądaniu licenses.nuget.org. Tylko identyfikator wyjątku licencją mogą być podawane w pojedynczym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="32c93-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="32c93-132">Żadne dodatkowe znaki, oprócz identyfikatora wyjątku licencji, stwarza część ścieżki adresu URL.</span><span class="sxs-lookup"><span data-stu-id="32c93-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="32c93-133">Identyfikator wyjątku licencji</span><span class="sxs-lookup"><span data-stu-id="32c93-133">License exception identifier</span></span> | <span data-ttu-id="32c93-134">Adres URL do użycia</span><span class="sxs-lookup"><span data-stu-id="32c93-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="32c93-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="32c93-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="32c93-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="32c93-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="32c93-137">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="32c93-137">Response</span></span>

<span data-ttu-id="32c93-138">Licenses.nuget.org odpowiada na żądanie z identyfikatorem wyjątek znanych licencji z odpowiedź HTTP 200 i strony sieci web zawierającej tekst odwołania, dla wyjątku jednostkom licencji.</span><span class="sxs-lookup"><span data-stu-id="32c93-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="32c93-139">Każde żądanie, zawierający identyfikator licencji nieobsługiwany wyjątek powoduje w odpowiedzi HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="32c93-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>