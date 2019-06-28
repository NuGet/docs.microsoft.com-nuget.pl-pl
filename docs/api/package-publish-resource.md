---
title: Wypychanie i usuwanie, interfejs API programu NuGet
description: Usługa publikowania umożliwia klientom Opublikuj nowe pakiety i wyrejestrowanie lub usuń istniejące pakiety.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426721"
---
# <a name="push-and-delete"></a>Wypychanie i usuwanie

Istnieje możliwość wypychania, Usuń (lub wyrejestrowanie, w zależności od implementacji serwera) i ponownie wystaw pakietów przy użyciu interfejsu API programu NuGet w wersji 3. Te operacje opierają się wylogować się z `PackagePublish` można znaleźć zasobu w [indeks usług](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` zostanie użyta wartość:

@type Wartość          | Uwagi
-------------------- | -----
PackagePublish/2.0.0 | Wersja początkowa

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `PackagePublish/2.0.0` zasobów w źródle pakietu [indeks usług](service-index.md). Poniższą dokumentacją używany jest adres URL usługi nuget.org. Należy wziąć pod uwagę `https://www.nuget.org/api/v2/package` jako symbol zastępczy `@id` znaleziono wartości w indeksie usługi.

Należy pamiętać, że ten adres URL wskazuje do tej samej lokalizacji, co starsze wypychania punktu końcowego V2, ponieważ protokół jest taka sama.

## <a name="http-methods"></a>Metody HTTP

`PUT`, `POST` i `DELETE` metod HTTP obsługiwanych przez ten zasób. Dla metody, które są obsługiwane dla każdego punktu końcowego zobacz poniżej.

## <a name="push-a-package"></a>Wypychanie pakietu

> [!Note]
> ma adres nuget.org [dodatkowe wymagania](NuGet-Protocols.md) do interakcji z punktem końcowym wypychania.

nuget.org obsługuje wypychania nowych pakietów przy użyciu następujących interfejsu API. Jeśli pakiet o identyfikatorze podana i wersji już istnieje, nuget.org odrzuci wypychania. Inne źródła pakietu może obsługiwać, zastępując istniejący pakiet.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | nagłówek | string | tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

Klucz interfejsu API to nieprzezroczysty ciąg uzyskane ze źródła pakietu przez użytkownika i skonfigurowane do klienta. Nie określonego ciągu formatu jest upoważnione, ale długość klucza interfejsu API nie może przekraczać rozmiaru uzasadnione wartości nagłówka HTTP.

### <a name="request-body"></a>Treść żądania

Treść żądania musi występować w następującej postaci:

#### <a name="multipart-form-data"></a>Wieloczęściowych danych formularza

Nagłówek żądania `Content-Type` jest `multipart/form-data` i pierwszy element w treści żądania ma bajtów raw .nupkg wypychania. Kolejne elementy treści wieloczęściowej wiadomości są ignorowane. Nazwa pliku lub innych nagłówków w wieloczęściowych elementów są ignorowane.

### <a name="response"></a>Odpowiedź

Kod stanu: | Znaczenie
----------- | -------
201, 202    | Pakiet został pomyślnie wypchnięto
400         | Podany pakiet jest nieprawidłowy
409         | Pakiet o identyfikatorze podana i wersji już istnieje.

Implementacje Server różnią się na kod stanu powodzenia, które są zwracane, gdy pakiet zostanie pomyślnie przypisany.

## <a name="delete-a-package"></a>Usuń pakiet

nuget.org interpretuje żądanie usunięcia pakietu jako wiadomość "wyrejestrowanie". Oznacza to, że pakiet jest nadal dostępna dla istniejących konsumentów pakietu, ale pakiet nie jest już wyświetlany w wynikach wyszukiwania lub w interfejsie sieci web. Aby uzyskać więcej informacji na temat tej praktyką, zobacz [usunięte pakiety](../nuget-org/policies/deleting-packages.md) zasad. Inne implementacje serwera są bezpłatne do interpretowania ten sygnał jako twardych delete, usuwanie nietrwałe lub wyrejestrowanie. Na przykład [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) obsługuje (tylko Obsługa starszych interfejsy API wersji 2 implementacji serwera), obsługujący żądanie jako unlist lub usuwania twardych na podstawie opcji konfiguracji.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
Identyfikator             | Adres URL    | string | tak      | Identyfikator pakietu do usunięcia
WERSJA        | Adres URL    | string | tak      | Wersja pakietu do usunięcia
X-NuGet-ApiKey | nagłówek | string | tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Odpowiedź

Kod stanu: | Znaczenie
----------- | -------
204         | Pakiet został usunięty.
404         | Nie pakietu z dostępnego `ID` i `VERSION` istnieje

## <a name="relist-a-package"></a>Wystaw ponownie pakiet

Jeśli pakiet jest nieobecne na liście, jest możliwe ten pakiet ponownie widoczne w wynikach wyszukiwania przy użyciu punktu końcowego "Wystaw ponownie". Ten punkt końcowy ma ten sam kształt co [Usuń (wyrejestrowanie) punktu końcowego](#delete-a-package) , ale używa `POST` protokołu HTTP zamiast metody `DELETE` metody.

Jeśli pakiet jest już na liście, żądanie nadal powiedzie się.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
Identyfikator             | Adres URL    | string | tak      | Identyfikator pakietu do ponownego wystawienia
WERSJA        | Adres URL    | string | tak      | Wersja pakietu do ponownego wystawienia
X-NuGet-ApiKey | nagłówek | string | tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Odpowiedź

Kod stanu: | Znaczenie
----------- | -------
200         | Pakiet znajduje się teraz
404         | Nie pakietu z dostępnego `ID` i `VERSION` istnieje
