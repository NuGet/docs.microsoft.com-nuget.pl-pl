---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427552"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="0e06b-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="0e06b-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="0e06b-103">Uzasadnienie</span><span class="sxs-lookup"><span data-stu-id="0e06b-103">Rationale</span></span>

<span data-ttu-id="0e06b-104">Wraz z wprowadzeniem [wyrażeń licencji](../reference/nuspec.md#license)pojawił się wymóg posiadania niezawodnej usługi, która zapewniałaby tekst referencyjny dla poszczególnych identyfikatorów licencji, identyfikatorów wyjątków lub wyrażeń licencji.</span><span class="sxs-lookup"><span data-stu-id="0e06b-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="0e06b-105">Dodatkowym wymaganiem dla tej usługi jest mieć stabilny schemat adresu URL, który nie jest podatny na gnicie łącza, dzięki czemu możemy bezpiecznie używać go do zapewnienia zgodności wstecznej dla starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="0e06b-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="0e06b-106">Licenses.nuget.org spełnia tę rolę.</span><span class="sxs-lookup"><span data-stu-id="0e06b-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="0e06b-107">Nuget.org używa go do dostarczenia odwołania tekstowego licencji dla pakietów, które określają ich licencji przy użyciu wyrażenia licencji.</span><span class="sxs-lookup"><span data-stu-id="0e06b-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="0e06b-108">`nuget pack`lub pakowania z innymi [narzędziami klienta](../install-nuget-client-tools.md) ustawić [`licenseUrl`](../reference/nuspec.md#licenseurl) element, aby wskazać licenses.nuget.org, aby zapewnić zgodność wsteczna `license` ze starszymi klientami, które nie obsługują elementu.</span><span class="sxs-lookup"><span data-stu-id="0e06b-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="0e06b-109">Protocol (Protokół)</span><span class="sxs-lookup"><span data-stu-id="0e06b-109">Protocol</span></span>

<span data-ttu-id="0e06b-110">Licenses.nuget.org jest przeznaczony do przeglądania przez osoby w ich przeglądarkach, nie są dostarczane odpowiedzi nadajalne maszynowo.</span><span class="sxs-lookup"><span data-stu-id="0e06b-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="0e06b-111">Protokół HTTPS musi być używany, a żądania powinny być konstruowane w określony sposób.</span><span class="sxs-lookup"><span data-stu-id="0e06b-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="0e06b-112">Obsługuje `GET` tylko żądania.</span><span class="sxs-lookup"><span data-stu-id="0e06b-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="0e06b-113">Akceptuje wyrażenia licencji lub identyfikatory wyjątków licencji jako dane wejściowe w sposób określony poniżej.</span><span class="sxs-lookup"><span data-stu-id="0e06b-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="0e06b-114">Należy pamiętać, że we wszystkich elementach wyrażeń licencji rozróżniana jest wielkość liter, a zatem wszystkie dane wejściowe do licenses.nuget.org jest również rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="0e06b-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="0e06b-115">Wyrażenia licencji</span><span class="sxs-lookup"><span data-stu-id="0e06b-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="0e06b-116">Żądanie</span><span class="sxs-lookup"><span data-stu-id="0e06b-116">Request</span></span>

<span data-ttu-id="0e06b-117">Wyrażenia licencji (w tym trywialne przypadki, gdy wyrażenie składa się z jednej licencji) muszą być [zakodowane w adresie URL](https://tools.ietf.org/html/rfc3986#section-2.1) i używane jako ścieżka w żądaniu licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0e06b-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="0e06b-118">Wyrażenie licencji</span><span class="sxs-lookup"><span data-stu-id="0e06b-118">License expression</span></span> | <span data-ttu-id="0e06b-119">Adres URL do użycia</span><span class="sxs-lookup"><span data-stu-id="0e06b-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="0e06b-120">MIT</span><span class="sxs-lookup"><span data-stu-id="0e06b-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="0e06b-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="0e06b-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="0e06b-122">(LGPL-2.0-tylko z wyjątkiem FLTK lub Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="0e06b-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="0e06b-123">Usługa obsługuje tylko identyfikatory licencji i identyfikatory wyjątków licencji, które są akceptowane przez nuget.org. Wszystkie wyrażenia licencji, które zawierają nieobsługiwały identyfikatory licencji lub identyfikatory wyjątków licencji lub które nie są zgodne ze składnią wyrażenia licencji, są uznawane za nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="0e06b-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="0e06b-124">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="0e06b-124">Response</span></span>

<span data-ttu-id="0e06b-125">Licenses.nuget.org odpowiada na żądania zawierające prawidłowe wyrażenia licencji za pomocą kodu stanu HTTP 200 i strony sieci Web zawierającej opis wyrażenia licencji:</span><span class="sxs-lookup"><span data-stu-id="0e06b-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="0e06b-126">jeśli dostarczone wyrażenie licencji zawiera pojedynczy identyfikator licencji, zwracana jest strona internetowa zawierająca ten tekst referencyjny licencji;</span><span class="sxs-lookup"><span data-stu-id="0e06b-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="0e06b-127">jeśli dostarczone wyrażenie licencji jest wyrażeniem licencji złożonej, zwracana jest strona sieci web zawierająca wyrażenie licencji z łączami do indywidualnych odwołań do wyjątków licencji lub licencji.</span><span class="sxs-lookup"><span data-stu-id="0e06b-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="0e06b-128">Wszystkie żądania zawierające nieprawidłowe wyrażenie licencji skutkują odpowiedzią HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="0e06b-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="0e06b-129">Wyjątki licencji</span><span class="sxs-lookup"><span data-stu-id="0e06b-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="0e06b-130">Żądanie</span><span class="sxs-lookup"><span data-stu-id="0e06b-130">Request</span></span>

<span data-ttu-id="0e06b-131">Identyfikatory wyjątków licencji muszą być zakodowane w adresie URL i używane jako ścieżka w żądaniu do licenses.nuget.org. Tylko jeden identyfikator wyjątku licencji może być dostarczony w jednym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="0e06b-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="0e06b-132">W części ścieżki adresu URL nie mogą znajdować się żadne dodatkowe znaki oprócz identyfikatora wyjątku licencji.</span><span class="sxs-lookup"><span data-stu-id="0e06b-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="0e06b-133">Identyfikator wyjątku licencji</span><span class="sxs-lookup"><span data-stu-id="0e06b-133">License exception identifier</span></span> | <span data-ttu-id="0e06b-134">Adres URL do użycia</span><span class="sxs-lookup"><span data-stu-id="0e06b-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="0e06b-135">FLTK-wyjątek</span><span class="sxs-lookup"><span data-stu-id="0e06b-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="0e06b-136">openvpn-openssl-wyjątek</span><span class="sxs-lookup"><span data-stu-id="0e06b-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="0e06b-137">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="0e06b-137">Response</span></span>

<span data-ttu-id="0e06b-138">Licenses.nuget.org odpowiada na żądanie o znanym identyfikatorze wyjątku licencji z odpowiedzią HTTP 200 i stroną sieci web zawierającą tekst referencyjny dla określonego wyjątku licencji.</span><span class="sxs-lookup"><span data-stu-id="0e06b-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="0e06b-139">Każde żądanie zawierające nieobsługicony identyfikator wyjątku licencji powoduje odpowiedź HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="0e06b-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>