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
# <a name="nugetorg-protocols"></a>Protokoły nuget.org

Aby można było korzystać z nuget.org, klienci muszą przestrzegać określonych protokołów. Ponieważ te protokoły zapewniają rozwój, klienci muszą identyfikować wersję protokołu używaną podczas wywoływania określonych interfejsów API nuget.org. Pozwala to nuget.org wprowadzać zmiany w nieprzerwanym stopniu dla starych klientów.

> [!Note]
> Interfejsy API udokumentowane na tej stronie są specyficzne dla nuget.org i nie ma oczekiwań innych implementacji serwera NuGet do wprowadzenia tych interfejsów API. 

Aby uzyskać więcej informacji na temat interfejsu API NuGet wdrożonego w całym ekosystemie NuGet, zobacz [Omówienie interfejsu API](overview.md).

W tym temacie wymieniono różne protokoły w zależności od ich istnienia.

## <a name="nuget-protocol-version-410"></a>Wersja protokołu NuGet 4.1.0

Protokół 4.1.0 Określa użycie kluczy Weryfikuj-Scope do współdziałania z usługami innym niż nuget.org, aby sprawdzić poprawność pakietu przy użyciu konta nuget.org. Należy zauważyć, że `4.1.0` numer wersji to ciąg nieprzezroczysty, ale występuje zbieżność z pierwszą wersją oficjalnego klienta NuGet, który obsługuje ten protokół.

Sprawdzanie poprawności zapewnia, że klucze interfejsu API utworzone przez użytkownika są używane tylko z nuget.org i że inne weryfikacje lub Walidacja z usługi innej firmy są obsługiwane za pomocą jednorazowego użycia kluczy Weryfikuj-Scope. Te klucze Weryfikuj zakres mogą służyć do weryfikowania, czy pakiet należy do określonego użytkownika (konto) w witrynie nuget.org.

### <a name="client-requirement"></a>Wymaganie dotyczące klienta

Klienci muszą przekazać następujący nagłówek, gdy tworzą wywołania interfejsu API do **wypychania** pakietów do NuGet.org:

```
X-NuGet-Protocol-Version: 4.1.0
```

Należy zauważyć, że `X-NuGet-Client-Version` nagłówek ma podobną semantykę, ale jest zarezerwowany do użycia tylko przez oficjalnego klienta NuGet. Klienci innych firm powinni używać `X-NuGet-Protocol-Version` nagłówka i wartości.

Sam protokół **wypychania** został opisany w dokumentacji dotyczącej [ `PackagePublish` zasobu](package-publish-resource.md).

Jeśli klient współdziała z usługami zewnętrznymi i musi sprawdzić, czy pakiet należy do określonego użytkownika (konto), powinien używać następującego protokołu i używać kluczy Weryfikuj-Scope, a nie kluczy interfejsu API z nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>Interfejs API żądania weryfikacji klucza zakresu

Ten interfejs API służy do uzyskiwania klucza Weryfikuj-Scope dla autora nuget.org, aby sprawdzić poprawność pakietu należącego do niego.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ID (Identyfikator)             | Adres URL    | ciąg | tak      | Identidier pakietu, dla którego zażądano weryfikacji klucza zakresu
WERSJA        | Adres URL    | ciąg | nie       | Wersja pakietu
X-NuGet-ApiKey | Nagłówek | ciąg | tak      | Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Reakcja

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>Interfejs API do sprawdzania poprawności klucza zakresu

Ten interfejs API służy do sprawdzania poprawności klucza weryfikacji dla pakietu należącego do autora nuget.org.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------  | ------ | ------ | -------- | -----
ID (Identyfikator)             | Adres URL    | ciąg | tak      | Identyfikator pakietu, dla którego zażądano weryfikacji klucza zakresu
WERSJA        | Adres URL    | ciąg | nie       | Wersja pakietu
X-NuGet-ApiKey | Nagłówek | ciąg | tak      | Na przykład `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Ten klucz interfejsu API sprawdzania zakresu wygasa w czasie dnia lub po pierwszym użyciu, zależnie od tego, co się dzieje.

#### <a name="response"></a>Reakcja

Kod stanu | Znaczenie
----------- | -------
200         | Klucz interfejsu API jest prawidłowy
403         | Klucz interfejsu API jest nieprawidłowy lub nie jest autoryzowany do wypychania do pakietu
404         | Pakiet, do którego odwołuje się `ID` i `VERSION` (opcjonalnie) nie istnieje
