---
title: Autouzupełnianie, interfejs API NuGet
description: Usługa wyszukiwania autouzupełniania obsługuje interaktywne odnajdywanie identyfikatorów pakietów i wersji.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773956"
---
# <a name="autocomplete"></a>Autouzupełnianie

Istnieje możliwość utworzenia identyfikatora pakietu i funkcji Autouzupełnianie wersji przy użyciu interfejsu API v3. Zasób używany do wykonywania zapytań autouzupełniania jest `SearchAutocompleteService` zasobem znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

`@type`Są używane następujące wartości:

@type wartościami                          | Uwagi
------------------------------------ | -----
SearchAutocompleteService            | Początkowa wersja
SearchAutocompleteService/3.0.0 — beta | Alias `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-RC   | Alias `SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | Obejmuje obsługę `packageType` parametru zapytania

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
Ta wersja wprowadza obsługę `packageType` parametru zapytania, umożliwiając filtrowanie według typów pakietów zdefiniowanych przez autora. Jest w pełni zgodna z poprzednimi wersjami zapytań `SearchAutocompleteService` .

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` Właściwości skojarzoną z jedną z wyżej wymienionych `@type` wartości zasobów. W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego adresu URL `{@id}` .

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują metody HTTP `GET` i `HEAD` .

## <a name="search-for-package-ids"></a>Wyszukaj identyfikatory pakietów

Pierwszy interfejs API funkcji Autouzupełnianie obsługuje wyszukiwanie części ciągu identyfikatora pakietu. Jest to doskonałe rozwiązanie, jeśli chcesz udostępnić funkcję typeahead pakietu w interfejsie użytkownika zintegrowanym ze źródłem pakietu NuGet.

Pakiet z tylko wersjami nieznajdującymi się na liście nie będzie wyświetlany w wynikach.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | ciąg  | nie       | Ciąg do porównania z identyfikatorami pakietów
Pomiń        | Adres URL    | liczba całkowita | nie       | Liczba wyników do pominięcia na stronie stronicowania
take (pobierz)        | Adres URL    | liczba całkowita | nie       | Liczba wyników do zwrócenia, na stronie stronicowania
wersja wstępna  | Adres URL    | boolean | nie       | `true` lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | ciąg  | nie       | Ciąg wersji SemVer 1.0.0 
packageType | Adres URL    | ciąg  | nie       | Typ pakietu, który ma być używany do filtrowania pakietów (dodana w `SearchAutocompleteService/3.5.0` )

Zapytanie autouzupełniania `q` jest analizowane w sposób zdefiniowany przez implementację serwera. nuget.org obsługuje zapytania dotyczące prefiksu tokenów identyfikatora pakietu, które są częścią identyfikatora wygenerowanego przez podzielenie oryginalnego znaku przez notacji CamelCase wielkość liter i symboli.

Wartość `skip` domyślna parametru to 0.

`take`Parametr powinien być liczbą całkowitą większą od zera. Implementacja serwera może mieć wartość maksymalną.

Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.

`semVerLevel`Parametr zapytania jest używany do wybierania [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Jeśli ten parametr zapytania zostanie wykluczony, zostaną zwrócone tylko identyfikatory pakietów z zgodnymi wersjami programu SemVer 1.0.0 (ze [standardowymi](../concepts/package-versioning.md) ograniczeniami wersji programu NuGet, takimi jak ciągi wersji z 4 liczbami całkowitymi).
Jeśli `semVerLevel=2.0.0` jest podany, zwracane są zgodne z SemVer 1.0.0 i SemVer 2.0.0. Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Ten `packageType` parametr służy do dokładniejszego filtrowania wyników autouzupełniania do pakietów, które mają co najmniej jeden typ pakietu pasujący do nazwy typu pakietu.
Jeśli podany typ pakietu nie jest prawidłowym typem pakietu zdefiniowanym przez [dokument typu pakietu](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), zostanie zwrócony pusty wynik.
Jeśli podany typ pakietu jest pusty, żaden filtr nie zostanie zastosowany. Innymi słowy, przekazywanie żadnej wartości do `packageType` parametru będzie zachowywać się tak, jakby parametr nie został przekazano.

### <a name="response"></a>Reakcja

Odpowiedź jest dokumentem JSON zawierającym do `take` wyników Autouzupełnianie.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | liczba całkowita          | tak      | Łączna liczba dopasowań, odnoszących się `skip` do i `take`
dane      | tablica ciągów | tak      | Identyfikatory pakietów dopasowane przez żądanie

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Wylicz wersje pakietów

Po znalezieniu identyfikatora pakietu przy użyciu poprzedniego interfejsu API klient może użyć interfejsu API autouzupełniania, aby wyliczyć wersje pakietu dla podanego identyfikatora pakietu.

Wersja pakietu, która nie znajduje się na liście, nie zostanie wyświetlona w wynikach.

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
identyfikator          | Adres URL    | ciąg  | tak      | Identyfikator pakietu, dla którego mają zostać pobrane wersje
wersja wstępna  | Adres URL    | boolean | nie       | `true` lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | ciąg  | nie       | Ciąg wersji SemVer 2.0.0 

Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.

`semVerLevel`Parametr zapytania jest używany do wybierania pakietów SemVer 2.0.0. Jeśli ten parametr zapytania jest wykluczony, zostaną zwrócone tylko wersje programu SemVer 1.0.0. Jeśli `semVerLevel=2.0.0` jest podany, zostaną zwrócone wersje SemVer 1.0.0 i SemVer 2.0.0. Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Reakcja

Odpowiedź to dokument JSON zawierający wszystkie wersje pakietu podanego identyfikatora pakietu, filtrowanie według podanych parametrów zapytania.

Główny obiekt JSON ma następującą właściwość:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
dane      | tablica ciągów | tak      | Wersje pakietów dopasowane przez żądanie

Wersje pakietu w `data` tablicy mogą zawierać metadane kompilacji SemVer 2.0.0 (np. `1.0.0+metadata` ), jeśli `semVerLevel=2.0.0` są podane w ciągu zapytania.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
