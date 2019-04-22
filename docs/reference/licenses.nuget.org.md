---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921562"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Racjonalne uzasadnienie

Wraz z wprowadzeniem [licencji wyrażeń](nuspec.md#license), wymaganie powstało mieć usługi reliable service zapewni tekst odwołania licencji poszczególnych identyfikatorów, identyfikatory wyjątek lub wyrażenia licencji.
Dodatkowe wymaganie wprowadzono dla tej usługi jest mają stabilny schemat adresu URL, który nie jest podatny na link rot, tak aby bezpiecznie używać go do zapewniania zgodności z poprzednimi wersjami starszych klientów.

Licenses.nuget.org spełnia tę rolę. Nuget.org używa go, aby zapewnić odwołanie tekst licencji dla pakietów, które określają licencję za pomocą wyrażenia licencji. `nuget pack` lub pakowania z innymi [narzędzi klienckich](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) ustaw [ `licenseUrl` ](nuspec.md#licenseurl) element, aby wskazywał licenses.nuget.org w celu zapewnienia wstecznej zgodności ze starszymi klientami, które nie obsługują `license` element.

## <a name="protocol"></a>Protokół

Licenses.nuget.org jest przeznaczony do przeglądania przez osoby w przeglądarkach, znajdują się odpowiedzi czytelnymi dla komputera.
Należy używać protokołu HTTPS, a żądania powinny zostać wykonane w określony sposób. Obsługuje on tylko `GET` żądań.
Akceptuje wyrażeń licencji lub licencji wyjątek identyfikatory jako dane wejściowe w sposób określony poniżej. Należy pamiętać, że wszystkie elementy wyrażenia licencji jest uwzględniana wielkość liter i w związku z tym wszystkie dane wejściowe do licenses.nuget.org jest uwzględniana wielkość liter jak również.

### <a name="license-expressions"></a>Wyrażenia licencji

#### <a name="request"></a>Request

Wyrażenia licencji (w tym proste przypadków, gdy wyrażenie składa się z pojedynczej licencji) muszą być [zakodowane w adresie URL](https://tools.ietf.org/html/rfc3986#section-2.1) i używane jako ścieżka w żądaniu licenses.nuget.org.

| Wyrażenie licencji | Adres URL do użycia |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL w wersji 2.0 — tylko przy użyciu Apache lub wyjątek FLTK-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Usługa obsługuje tylko identyfikatory licencji i licencji wyjątek identyfikatorów, które są akceptowane przez nuget.org. Wszystkie wyrażenia licencji zawierających identyfikatory nieobsługiwany licencji lub licencji wyjątek identyfikatorów lub który jest niezgodny ze składnią wyrażeń licencji są uznawane za nieprawidłowe.

#### <a name="response"></a>Odpowiedź

Licenses.nuget.org odpowiada na żądania zawierające wyrażenia prawidłowej licencji z kodem stanu HTTP 200 i strony sieci web zawierająca opis licencji wyrażenia:

* Jeśli podane wyrażenie licencji zawiera identyfikator licencji pojedynczej strony sieci web jest zwracane, który zawiera ten tekst odwołanie licencji;
* Jeśli nie dostarczono licencji wyrażenie jest wyrażeniem złożonego licencji, strony sieci web jest zwracany, który zawiera wyrażenie licencji wraz z łączami do poszczególnych licencji lub licencji wyjątek odwołania.

Wszystkie żądania, które zawierają wyrażenia Nieprawidłowa licencja wyniku w odpowiedzi HTTP 404.

### <a name="license-exceptions"></a>Wyjątki licencji

#### <a name="request"></a>Request

Identyfikatory wyjątek licencji musi być zakodowane w adresie URL i używane jako ścieżka w żądaniu licenses.nuget.org. Tylko identyfikator wyjątku licencją mogą być podawane w pojedynczym żądaniu. Żadne dodatkowe znaki, oprócz identyfikatora wyjątku licencji, stwarza część ścieżki adresu URL.

| Identyfikator wyjątku licencji | Adres URL do użycia |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Odpowiedź

Licenses.nuget.org odpowiada na żądanie z identyfikatorem wyjątek znanych licencji z odpowiedź HTTP 200 i strony sieci web zawierającej tekst odwołania, dla wyjątku jednostkom licencji.

Każde żądanie, zawierający identyfikator licencji nieobsługiwany wyjątek powoduje w odpowiedzi HTTP 404.