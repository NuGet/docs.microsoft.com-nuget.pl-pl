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
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Uzasadnienie

Wraz z wprowadzeniem [wyrażeń licencji](../reference/nuspec.md#license)pojawił się wymóg posiadania niezawodnej usługi, która zapewniałaby tekst referencyjny dla poszczególnych identyfikatorów licencji, identyfikatorów wyjątków lub wyrażeń licencji.
Dodatkowym wymaganiem dla tej usługi jest mieć stabilny schemat adresu URL, który nie jest podatny na gnicie łącza, dzięki czemu możemy bezpiecznie używać go do zapewnienia zgodności wstecznej dla starszych klientów.

Licenses.nuget.org spełnia tę rolę. Nuget.org używa go do dostarczenia odwołania tekstowego licencji dla pakietów, które określają ich licencji przy użyciu wyrażenia licencji. `nuget pack`lub pakowania z innymi [narzędziami klienta](../install-nuget-client-tools.md) ustawić [`licenseUrl`](../reference/nuspec.md#licenseurl) element, aby wskazać licenses.nuget.org, aby zapewnić zgodność wsteczna `license` ze starszymi klientami, które nie obsługują elementu.

## <a name="protocol"></a>Protocol (Protokół)

Licenses.nuget.org jest przeznaczony do przeglądania przez osoby w ich przeglądarkach, nie są dostarczane odpowiedzi nadajalne maszynowo.
Protokół HTTPS musi być używany, a żądania powinny być konstruowane w określony sposób. Obsługuje `GET` tylko żądania.
Akceptuje wyrażenia licencji lub identyfikatory wyjątków licencji jako dane wejściowe w sposób określony poniżej. Należy pamiętać, że we wszystkich elementach wyrażeń licencji rozróżniana jest wielkość liter, a zatem wszystkie dane wejściowe do licenses.nuget.org jest również rozróżniana wielkość liter.

### <a name="license-expressions"></a>Wyrażenia licencji

#### <a name="request"></a>Żądanie

Wyrażenia licencji (w tym trywialne przypadki, gdy wyrażenie składa się z jednej licencji) muszą być [zakodowane w adresie URL](https://tools.ietf.org/html/rfc3986#section-2.1) i używane jako ścieżka w żądaniu licenses.nuget.org.

| Wyrażenie licencji | Adres URL do użycia |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-tylko z wyjątkiem FLTK lub Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Usługa obsługuje tylko identyfikatory licencji i identyfikatory wyjątków licencji, które są akceptowane przez nuget.org. Wszystkie wyrażenia licencji, które zawierają nieobsługiwały identyfikatory licencji lub identyfikatory wyjątków licencji lub które nie są zgodne ze składnią wyrażenia licencji, są uznawane za nieprawidłowe.

#### <a name="response"></a>Odpowiedź

Licenses.nuget.org odpowiada na żądania zawierające prawidłowe wyrażenia licencji za pomocą kodu stanu HTTP 200 i strony sieci Web zawierającej opis wyrażenia licencji:

* jeśli dostarczone wyrażenie licencji zawiera pojedynczy identyfikator licencji, zwracana jest strona internetowa zawierająca ten tekst referencyjny licencji;
* jeśli dostarczone wyrażenie licencji jest wyrażeniem licencji złożonej, zwracana jest strona sieci web zawierająca wyrażenie licencji z łączami do indywidualnych odwołań do wyjątków licencji lub licencji.

Wszystkie żądania zawierające nieprawidłowe wyrażenie licencji skutkują odpowiedzią HTTP 404.

### <a name="license-exceptions"></a>Wyjątki licencji

#### <a name="request"></a>Żądanie

Identyfikatory wyjątków licencji muszą być zakodowane w adresie URL i używane jako ścieżka w żądaniu do licenses.nuget.org. Tylko jeden identyfikator wyjątku licencji może być dostarczony w jednym żądaniu. W części ścieżki adresu URL nie mogą znajdować się żadne dodatkowe znaki oprócz identyfikatora wyjątku licencji.

| Identyfikator wyjątku licencji | Adres URL do użycia |
|:---|:---|
|FLTK-wyjątek            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-wyjątek | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Odpowiedź

Licenses.nuget.org odpowiada na żądanie o znanym identyfikatorze wyjątku licencji z odpowiedzią HTTP 200 i stroną sieci web zawierającą tekst referencyjny dla określonego wyjątku licencji.

Każde żądanie zawierające nieobsługicony identyfikator wyjątku licencji powoduje odpowiedź HTTP 404.