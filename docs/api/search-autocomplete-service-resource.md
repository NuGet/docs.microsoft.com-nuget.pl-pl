---
title: Autouzupełnianie, interfejs API NuGet
description: Usługa wyszukiwania autouzupełniania obsługuje interaktywne odnajdywanie identyfikatorów pakietów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488303"
---
# <a name="autocomplete"></a>Autouzupełnianie

Istnieje możliwość utworzenia identyfikatora pakietu i funkcji Autouzupełnianie wersji przy użyciu interfejsu API v3. Zasób używany do wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` zasobem znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Są używane `@type` następujące wartości:

@typewartościami                          | Uwagi
------------------------------------ | -----
SearchAutocompleteService            | Początkowa wersja
SearchAutocompleteService/3.0.0-beta | Alias`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias`SearchAutocompleteService`

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzoną z jedną z wyżej wymienionych wartości zasobów. `@type` W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego `{@id}` adresu URL.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują `GET` metody `HEAD`http i.

## <a name="search-for-package-ids"></a>Wyszukaj identyfikatory pakietów

Pierwszy interfejs API funkcji Autouzupełnianie obsługuje wyszukiwanie części ciągu identyfikatora pakietu. Jest to doskonałe rozwiązanie, jeśli chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika zintegrowanym ze źródłem pakietu NuGet.

Pakiet z tylko wersjami nieznajdującymi się na liście nie będzie wyświetlany w wynikach.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | string  | znaleziono       | Ciąg do porównania z identyfikatorami pakietów
Pomiń        | Adres URL    | integer | znaleziono       | Liczba wyników do pominięcia na stronie stronicowania
czasochłonn        | Adres URL    | integer | znaleziono       | Liczba wyników do zwrócenia, na stronie stronicowania
wersja wstępna  | Adres URL    | wartość logiczna | znaleziono       | `true`lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | znaleziono       | Ciąg wersji SemVer 1.0.0 

Zapytanie `q` autouzupełniania jest analizowane w sposób zdefiniowany przez implementację serwera. nuget.org obsługuje zapytania dotyczące prefiksu tokenów identyfikatora pakietu, które są częścią identyfikatora wygenerowanego przez podzielenie oryginalnego znaku przez notacji CamelCase wielkość liter i symboli.

Wartość `skip` domyślna parametru to 0.

`take` Parametr powinien być liczbą całkowitą większą od zera. Implementacja serwera może mieć wartość maksymalną.

Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.

Parametr zapytania jest używany do wybierania [pakietów SemVer 2.0.0.](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`
Jeśli ten parametr zapytania zostanie wykluczony, zostaną zwrócone tylko identyfikatory pakietów z zgodnymi wersjami programu SemVer 1.0.0 (ze standardowymi ograniczeniami [wersji programu NuGet](../concepts/package-versioning.md) , takimi jak ciągi wersji z 4 liczbami całkowitymi).
Jeśli `semVerLevel=2.0.0` jest podany, zwracane są zgodne z SemVer 1.0.0 i SemVer 2.0.0. Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokumentem JSON zawierającym do `take` wyników Autouzupełnianie.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | integer          | tak      | Łączna liczba dopasowań, odnoszących `skip` się do i`take`
dane      | Tablica ciągów | tak      | Identyfikatory pakietów dopasowane przez żądanie

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Wylicz wersje pakietów

Po znalezieniu identyfikatora pakietu przy użyciu poprzedniego interfejsu API klient może użyć interfejsu API autouzupełniania, aby wyliczyć wersje pakietu dla podanego identyfikatora pakietu.

Wersja pakietu, która nie znajduje się na liście, nie zostanie wyświetlona w wynikach.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
identyfikator          | Adres URL    | string  | tak      | Identyfikator pakietu, dla którego mają zostać pobrane wersje
wersja wstępna  | Adres URL    | wartość logiczna | znaleziono       | `true`lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | znaleziono       | Ciąg wersji SemVer 2.0.0 

Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.

Parametr `semVerLevel` zapytania jest używany do wybierania pakietów SemVer 2.0.0. Jeśli ten parametr zapytania jest wykluczony, zostaną zwrócone tylko wersje programu SemVer 1.0.0. Jeśli `semVerLevel=2.0.0` jest podany, zostaną zwrócone wersje SemVer 1.0.0 i SemVer 2.0.0. Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Odpowiedź

Odpowiedź to dokument JSON zawierający wszystkie wersje pakietu podanego identyfikatora pakietu, filtrowanie według podanych parametrów zapytania.

Główny obiekt JSON ma następującą właściwość:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
dane      | Tablica ciągów | tak      | Wersje pakietów dopasowane przez żądanie

Wersje pakietu w `data` tablicy mogą zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata`), `semVerLevel=2.0.0` jeśli są podane w ciągu zapytania.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
