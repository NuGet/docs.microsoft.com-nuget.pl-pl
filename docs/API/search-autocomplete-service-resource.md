---
title: Funkcji AutoComplete, NuGet interfejsu API | Dokumentacja firmy Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Usługa autouzupełniania wyszukiwania obsługuje Odnajdowanie interaktywne pakietu identyfikatorów i wersje."
keywords: "Interfejs API autouzupełniania NuGet, identyfikator pakietu NuGet wyszukiwania, podciąg identyfikator pakietu"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a>Funkcji AutoComplete

Istnieje możliwość tworzenia pakietu identyfikator i wersja autouzupełniania środowisko przy użyciu interfejsu API w wersji 3. Zasoby używane do wykonywania kwerend autouzupełniania `SearchAutocompleteService` można znaleźć zasobu w [indeksu usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@typewartość                          | Uwagi
------------------------------------ | -----
SearchAutocompleteService            | Początkowa wersja
SearchAutocompleteService/3.0.0-beta | Alias`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias`SearchAutocompleteService`

## <a name="base-url"></a>Podstawowy adres URL

Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzone z jedną z wyżej wymienionych zasobów `@type` wartości. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.

## <a name="search-for-package-ids"></a>Wyszukaj pakiet identyfikatorów

Pierwszy autouzupełniania interfejsu API obsługuje wyszukiwanie część ciągu Identyfikatora pakietu. Jest to doskonały, gdy chcesz zapewnić funkcji typeahead pakietu w interfejsie użytkownika zintegrowany ze źródłem pakietu NuGet.

Pakiet o tylko wersje nieznajdujące się na liście nie będą wyświetlane w wynikach.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | string  | Brak       | Ciąg, aby porównać pakietu identyfikatorów
Pomiń        | Adres URL    | integer | Brak       | Liczba wyników, aby pominąć dla podział na strony
podejmij        | Adres URL    | integer | Brak       | Liczba wyników do zwrócenia do podział na strony
wydanie wstępne  | Adres URL    | wartość logiczna | Brak       | `true`lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | Brak       | Ciąg wersji programu SemVer 1.0.0 

Zapytanie autouzupełniania `q` jest analizowana w taki sposób, który jest zdefiniowany przez implementację serwera. nuget.org obsługuje wyszukiwanie prefiks tokeny Identyfikatora pakietu będące części identyfikatora utworzonego przez spliting oryginalnej camel znakami wielkość liter i symboli.

`skip` Domyślne wartości parametrów na 0.

`take` Parametr powinien być liczbą całkowitą większą niż zero. Implementacja serwera może nałożyć wartości maksymalnej.

Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.

`semVerLevel` Parametru zapytania jest używana do wyrazić zgodę na [pakiety programu SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko pakiet identyfikatory zgodne wersje programu SemVer 1.0.0 (z [standardowe versioning NuGet](../reference/package-versioning.md) ostrzeżenia, na przykład ciągi wersji z 4 elementy liczba całkowita).
Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i pakiety zgodne programu SemVer 2.0.0. Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokument JSON zawierający do `take` autouzupełniania wyników.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | integer          | Tak      | Całkowita liczba dopasowania, bez uwzględnienia `skip` i`take`
dane      | Tablica ciągów | Tak      | Identyfikatory są dopasowane wg żądania pakietu

### <a name="sample-request"></a>Przykładowe żądanie

GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Wyliczenie wersji pakietu

Po identyfikator pakietu został odnaleziony przy użyciu poprzedniej interfejsu API, klient może używać automatycznego uzupełniania interfejsu API wyliczyć wersji pakietu identyfikatora podany pakiet.

Wersja pakietu, który jest nieznajdujące się na liście nie będą widoczne w wynikach.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
identyfikator          | Adres URL    | string  | Tak      | Identyfikator pakietu, który można pobrać wersji
wydanie wstępne  | Adres URL    | wartość logiczna | Brak       | `true`lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | Brak       | Ciąg wersji programu SemVer 2.0.0 

Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.

`semVerLevel` Parametru zapytania jest używana w celu pakietów programu SemVer 2.0.0. Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko wersje programu SemVer 1.0.0. Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i wersje programu SemVer 2.0.0. Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokument JSON zawierający wszystkie wersje pakietu identyfikatora podany pakiet, filtrowanie według parametry określonego zapytania.

Główny obiekt JSON ma następującą właściwość:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
dane      | Tablica ciągów | Tak      | Wersje pakietów, które są dopasowane wg żądania

Wersje pakietu w `data` Tablica może zawierać metadane kompilacji programu SemVer 2.0.0 (np. `1.0.0+metadata`) Jeśli `semVerLevel=2.0.0` podany w ciągu zapytania.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
