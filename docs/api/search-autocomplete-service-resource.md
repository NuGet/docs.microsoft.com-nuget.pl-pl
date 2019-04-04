---
title: Autouzupełnianie, interfejs API programu NuGet
description: Usługa wyszukiwania w funkcji autouzupełniania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911052"
---
# <a name="autocomplete"></a>Autouzupełnianie

Jest możliwe utworzenie pakietu identyfikator i wersja autouzupełniania doświadczenie w korzystaniu z interfejsu API w wersji 3. Zasób używane na potrzeby wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` można znaleźć zasobu w [indeks usług](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@type Wartość                          | Uwagi
------------------------------------ | -----
SearchAutocompleteService            | Wersja początkowa
SearchAutocompleteService/3.0.0-beta | Alias `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias `SearchAutocompleteService`

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.

## <a name="search-for-package-ids"></a>Wyszukaj pakiet identyfikatorów

Autouzupełnianie pierwszy interfejs API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu. Jest to doskonałe, gdy chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika, zintegrowany z źródła pakietu NuGet.

Pakiet wersjom tylko nieznajdujące się na liście będą widoczne w wynikach.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | string  | Brak       | Ciąg do porównania pakietu identyfikatorów
Pomiń        | Adres URL    | integer | Brak       | Liczba wyników do pominięcia do dzielenia na strony
Wypełnij        | Adres URL    | integer | Brak       | Liczba wyników do zwrócenia do dzielenia na strony
wersja wstępna  | Adres URL    | wartość logiczna | Brak       | `true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | Brak       | Ciąg wersji SemVer 1.0.0 

Zapytanie autouzupełniania `q` jest analizowany w taki sposób, który jest definiowany przez implementację serwera. nuget.org obsługuje zapytania dla prefiksu tokeny Identyfikatora pakietu będące rodzajów identyfikator, który został utworzony przez spliting oryginalny pisane znakami wielkość liter i symboli.

`skip` Domyślnych wartości parametrów na 0.

`take` Parametr powinien być liczbą całkowitą większą niż zero. Implementacja serwera może nałożyć wartość maksymalna.

Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.

`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko pakiet identyfikatory o SemVer 1.0.0 zgodne wersje (z [standardowych wersji NuGet](../reference/package-versioning.md) zastrzeżenia, takich jak ciągi wersji z 4 elementów liczba całkowita).
Jeśli `semVerLevel=2.0.0` zostanie podana, zostaną zwrócone SemVer 1.0.0 i pakiety zgodne SemVer 2.0.0. Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokument JSON zawierający do `take` wyniki funkcji autouzupełniania.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | integer          | tak      | Całkowita liczba dopasowań, pomijając `skip` i `take`
dane      | Tablica ciągów | tak      | Identyfikatory dopasowane przez żądania pakietu

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Wyliczenie wersji pakietu

Po odnalezieniu Identyfikatora pakietu za pomocą poprzedniej interfejsu API klient może używać interfejsu API automatycznego uzupełniania wyliczyć wersji pakietu dla identyfikatora podanego pakietu

Wersja pakietu, który jest nieobecne na liście będą widoczne w wynikach.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
identyfikator          | Adres URL    | string  | tak      | Identyfikator pakietu można pobrać wersji
wersja wstępna  | Adres URL    | wartość logiczna | Brak       | `true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | Brak       | Ciąg wersji SemVer 2.0.0 

Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.

`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na pakiety SemVer 2.0.0. Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko wersje SemVer 1.0.0. Jeśli `semVerLevel=2.0.0` zostanie podana, zostanie zwrócony SemVer 1.0.0 i SemVer 2.0.0 wersji. Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podanego pakietu, filtrowanie według parametrów określonego zapytania.

Główny obiekt JSON ma następującą właściwość:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
dane      | Tablica ciągów | tak      | Wersje pakietów dopasowane przez żądanie

Wersje pakietów w `data` Tablica może zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` znajduje się w ciągu zapytania.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
