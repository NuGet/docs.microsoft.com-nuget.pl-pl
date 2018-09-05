---
title: Protokoły nuget.org
description: Protokoły nuget.org rozwijające się do interakcji z klientami NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547276"
---
# <a name="nugetorg-protocols"></a>protokoły nuget.org

Do interakcji z repozytorium nuget.org, klienci muszą wykonać pewne protokołów. Ponieważ Utrzymaj rozwijające się tych protokołów, klienci muszą zidentyfikować wersja protokołu używanego podczas wywoływania określonych nuget.org interfejsów API. Dzięki temu nuget.org do wprowadzenia zmian w sposób niepowodujących niezgodności starych klientów.

> [!Note]
> Interfejsy API opisane na tej stronie są specyficzne dla nuget.org i nie ma żadnych oczekiwania dotyczące innych implementacji serwera NuGet wprowadzić te interfejsy API. 

Aby uzyskać informacje o interfejsie API NuGet szeroko zaimplementowane w ekosystemie NuGet, zobacz [omówienie interfejsu API](overview.md).

Ten temat zawiera listę różnych protokołów, jak i kiedy pochodzą istnienia.

## <a name="nuget-protocol-version-410"></a>Protokołu NuGet w wersji 4.1.0

4.1.0 protokołu Określa użycie kluczy Sprawdź zakres do interakcji z usługami innymi niż nuget.org pakietu do konta w witrynie nuget.org. Należy pamiętać, że `4.1.0` wersji liczba to nieprzezroczysty ciąg, ale dzieje się pokrywają się z pierwszą wersję oficjalne klienta NuGet, który obsługuje ten protokół.

Sprawdzanie poprawności gwarantuje, że klucze interfejsu API utworzonej przez użytkownika są używane tylko w witrynie nuget.org, i tej weryfikacji lub Weryfikacja z usługi innej firmy odbywa się przy użyciu kluczy Sprawdź zakres jednorazowego użytku. Te klucze Sprawdź zakres może służyć do sprawdzania, czy pakiet należy do określonego użytkownika (konto) w witrynie nuget.org.

### <a name="client-requirement"></a>Wymagania klienta

Klienci są wymagane do przekazania następujący nagłówek, w momencie wywołania interfejsu API do **wypychania** pakietów nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Należy pamiętać, że `X-NuGet-Client-Version` nagłówka przypomina semantykę, ale jest zarezerwowany do użycia tylko przez oficjalne klienta programu NuGet. Innych firm, klienci powinni używać `X-NuGet-Protocol-Version` nagłówek i podaną wartość.

**Wypychania** samego protokołu jest opisane w dokumentacji dotyczącej [ `PackagePublish` zasobów](package-publish-resource.md).

Jeśli klient korzysta z usług zewnętrznych i należy sprawdzić, czy pakiet należy do określonego użytkownika (konto), powinna używać następujących protokołu i klucze Sprawdź, czy zakres i nie klucze interfejsu API z repozytorium nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>Interfejs API, aby poprosić o klucz Sprawdź, czy zakres

Ten interfejs API umożliwia uzyskiwanie klucza Sprawdź, czy zakres dla autora nuget.org do sprawdzania poprawności pakietu posiadanych przez nią.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ID             | Adres URL    | string | Tak      | Identidier pakiet, dla którego żądana jest Sprawdź, czy klucz zakresu
WERSJA        | Adres URL    | string | Brak       | Wersja pakietu
X-NuGet-ApiKey | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Odpowiedź

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>Interfejs API, aby sprawdzić, sprawdź, czy klucz zakresu

Ten interfejs API jest używana do zweryfikowania klucza zakresu Sprawdź posiadane przez autora nuget.org pakietu.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------  | ------ | ------ | -------- | -----
ID             | Adres URL    | string | Tak      | Identyfikator pakietu, dla którego żądana jest Sprawdź, czy klucz zakresu
WERSJA        | Adres URL    | string | Brak       | Wersja pakietu
X-NuGet-ApiKey | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Ten klucz interfejsu API zakresu Sprawdź, czy utraci ważność za dni lub przy pierwszym użyciu zależnie co nastąpi wcześniej.

#### <a name="response"></a>Odpowiedź

Kod stanu: | Znaczenie
----------- | -------
200         | Klucz interfejsu API jest nieprawidłowa
403         | Klucz interfejsu API jest nieprawidłowa lub nie jest autoryzowany do wypychania na pakiecie
404         | Pakiet odwołuje się `ID` i `VERSION` (opcjonalnie) nie istnieje
