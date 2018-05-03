---
title: Protokoły nuget.org
description: Protokoły nuget.org zmieniające się do interakcji z klientów NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nugetorg-protocols"></a>protokoły nuget.org

Wchodzić w interakcje z nuget.org, klienci muszą wykonać niektórych protokołów. Ponieważ rozwijają zachować te protokoły, klienci muszą identyfikują wersja protokołu używanego podczas wywoływania metody nuget.org określonych interfejsów API. Dzięki temu nuget.org wprowadzenie zmian w sposób nierozdzielające starego klientów.

> [!Note]
> Interfejsy API udokumentowany na tej stronie są specyficzne dla nuget.org i nie ma żadnych oczekiwania w innych implementacjach serwera NuGet dodać te interfejsy API. 

Informacje o interfejsie API NuGet szeroko implementowany w ekosystemie NuGet, zobacz [Przegląd interfejsu API](overview.md).

Ten temat zawiera listę różnych protokołów, jak i kiedy zaczynają istnienia.

## <a name="nuget-protocol-version-410"></a>Wersja protokołu NuGet 4.1.0

4.1.0 protokołu Określa użycie kluczy Sprawdź zakres do interakcji z usługami innych niż nuget.org pakietu do konta nuget.org. Należy pamiętać, że `4.1.0` wersji liczba to ciąg nieprzezroczyste, ale dzieje się pokrywa się z pierwszej wersji oficjalnego klienta NuGet, który obsługuje tego protokołu.

Sprawdzanie poprawności temu klucze interfejsu API utworzonych przez użytkownika są używane tylko z nuget.org i tej weryfikacji lub Weryfikacja od usługi innej firmy jest obsługiwana za pomocą kluczy Sprawdź zakres jednorazowego użytku. Te klucze Sprawdź zakres może służyć do sprawdzania, czy pakiet należy do określonego użytkownika (konto) na nuget.org.

### <a name="client-requirement"></a>Wymagania klienta

Klienci są wymagane do przekazania następujący nagłówek, podczas tworzenia wywołań interfejsu API **wypychania** pakietów do nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Należy pamiętać, że `X-NuGet-Client-Version` przypomina semantykę nagłówka, ale jest zarezerwowany do użycia tylko przez oficjalnego klienta NuGet. Innej klienci powinni używać `X-NuGet-Protocol-Version` nagłówek i podaną wartość.

**Wypychania** samego protokołu jest opisany w dokumentacji dotyczącej [ `PackagePublish` zasobów](package-publish-resource.md).

Jeśli klient współdziała z usług zewnętrznych i należy sprawdzić, czy pakiet należy do określonego użytkownika (konto), powinna używać protokołu następujące i używać kluczy Sprawdź zakres i nie klucze interfejsu API z nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>Interfejs API do żądania klucz Sprawdź zakres

Ten interfejs API jest używany do pobierania klucz, sprawdź, czy zakres autora nuget.org, można sprawdzić poprawności pakietu posiadanych przez nią.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ID             | Adres URL    | string | Tak      | Identidier pakiet, dla którego wymagany jest klucz Sprawdź zakres
WERSJA        | Adres URL    | string | Brak       | Wersja pakietu
X-NuGet-ApiKey | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Odpowiedź

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>Interfejs API, aby zweryfikować klucz Sprawdź zakres

Ten interfejs API jest używany do sprawdzania poprawności klucza zakresu Sprawdź posiadane przez autora nuget.org pakietu.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------  | ------ | ------ | -------- | -----
ID             | Adres URL    | string | Tak      | Identyfikator pakietu, dla którego wymagany jest klucz Sprawdź zakres
WERSJA        | Adres URL    | string | Brak       | Wersja pakietu
X-NuGet-ApiKey | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Ten klucz interfejsu API zakresu Sprawdź utraci ważność za dni lub przy pierwszym użyciu cokolwiek nastąpi najpierw.

#### <a name="response"></a>Odpowiedź

Kod stanu | Znaczenie
----------- | -------
200         | Klucz interfejsu API jest nieprawidłowa
403         | Klucz interfejsu API jest nieprawidłowa lub nie jest autoryzowany do wypychania na pakiecie
404         | Pakiet odwołuje się `ID` i `VERSION` (opcjonalnie) nie istnieje
