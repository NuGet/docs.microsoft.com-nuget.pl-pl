---
title: Wyszukiwanie, interfejs API programu NuGet
description: Usługa wyszukiwania umożliwia klientom zapytania dla pakietów według słów kluczowych i filtrowania wyników w określonych polach pakietu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: cfcb52ba7689f1b392c782b4ad42ba820a76c8bf
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981135"
---
# <a name="search"></a>Wyszukaj

Istnieje możliwość wyszukać pakiety, które są dostępne w źródle pakietu przy użyciu interfejsu API w wersji 3. Zasób, używany do wyszukiwania jest `SearchQueryService` można znaleźć zasobu w [indeks usług](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@type Wartość                   | Uwagi
----------------------------- | -----
SearchQueryService            | Wersja początkowa
SearchQueryService/3.0.0-beta | Alias `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias `SearchQueryService`

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujący interfejs API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.

## <a name="search-for-packages"></a>Wyszukaj pakiety

Interfejs API wyszukiwania umożliwia klientowi zapytania dla strony pakietów pasujących do zapytania wyszukiwania. Interpretacja zapytanie wyszukiwania (np. tokenizacji wyszukiwane terminy) zależy od implementacji serwera, ale ogólne oczekuje się, że zapytanie wyszukiwania jest używany do dopasowywania identyfikatorów pakietu, tytułów, opisów i tagów. Mogą być również uwzględnione inne pola metadanych pakietu.

Pakiet nieznajdujące się na liście nigdy nie powinna zostać wyświetlona w wynikach wyszukiwania.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | string  | Brak       | Wyszukiwane terminy używane do filtrowania pakietów
Pomiń        | Adres URL    | integer | Brak       | Liczba wyników do pominięcia do dzielenia na strony
Wypełnij        | Adres URL    | integer | Brak       | Liczba wyników do zwrócenia do dzielenia na strony
wersja wstępna  | Adres URL    | wartość logiczna | Brak       | `true` lub `false` określająca, czy dołączać [pakiety w wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | Brak       | Ciąg wersji SemVer 1.0.0 

Zapytanie wyszukiwania `q` jest analizowany w taki sposób, który jest definiowany przez implementację serwera. obsługuje nuget.org, podstawowe filtrowanie [wiele pól](../consume-packages/finding-and-choosing-packages.md#search-syntax). Jeśli nie `q` zostanie podana, ma zostać zwrócone wszystkie pakiety w granicach nałożonych przez skip i take. Dzięki temu na karcie "Przegląd" w środowisku NuGet Visual Studio.

`skip` Domyślnych wartości parametrów na 0.

`take` Parametr powinien być liczbą całkowitą większą niż zero. Implementacja serwera może nałożyć wartość maksymalna.

Jeśli `prerelease` nie zostanie podana, pakiety w wersji wstępnej są wyłączone.

`semVerLevel` Parametru zapytania jest używana do wyrażenia zgody na [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Jeśli ten parametr zapytania jest wyłączona, zostaną zwrócone tylko pakiety z SemVer 1.0.0 zgodne wersje (z [standardowych wersji NuGet](../reference/package-versioning.md) zastrzeżenia, takich jak ciągi wersji z 4 elementów liczba całkowita).
Jeśli `semVerLevel=2.0.0` zostanie podana, zostaną zwrócone SemVer 1.0.0 i pakiety zgodne SemVer 2.0.0. Zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokument JSON zawierający do `take` wyników wyszukiwania. Wyniki wyszukiwania są pogrupowane według identyfikatora pakietu.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | integer          | Tak      | Całkowita liczba dopasowań, pomijając `skip` i `take`
dane      | Tablica obiektów | Tak      | Wyniki wyszukiwania dopasowane przez żądanie

### <a name="search-result"></a>Wynik wyszukiwania

Każdy element na `data` tablica jest obiekt JSON, składająca się z grupą wersji pakietu do udostępniania tego samego identyfikatora pakietu.
Obiekt ma następujące właściwości:

Nazwa           | Typ                       | Wymagane | Uwagi
-------------- | -------------------------- | -------- | -----
identyfikator             | string                     | Tak      | Identyfikator pakietu dopasowane
version        | string                     | Tak      | Pełny ciąg wersji SemVer 2.0.0 pakietu (może zawierać metadane kompilacji).
opis    | string                     | Brak       | 
wersje       | Tablica obiektów           | Tak      | Wszystkie wersje pakietu dopasowywania `prerelease` parametru
Autorzy        | ciąg lub tablicę ciągów | Brak       | 
IconUrl        | string                     | Brak       | 
licenseUrl     | string                     | Brak       | 
Właściciele         | ciąg lub tablicę ciągów | Brak       | 
projectUrl     | string                     | Brak       | 
rejestracja   | string                     | Brak       | Bezwzględny adres URL do powiązanych [indeksu rejestracji](registration-base-url-resource.md#registration-index)
podsumowanie        | string                     | Brak       | 
tagi           | ciąg lub tablicę ciągów | Brak       | 
Tytuł          | string                     | Brak       | 
totalDownloads | integer                    | Brak       | Tę wartość można wywnioskować przez sumę pliki do pobrania w `versions` tablicy
Zweryfikowano       | wartość logiczna                    | Brak       | JSON atrybut typu wartość logiczna wskazująca, czy pakiet jest [zweryfikowane](../reference/id-prefix-reservation.md)

W witrynie nuget.org zweryfikowaną pakietu jest taki, który ma identyfikator pakietu dopasowania zastrzeżony prefiks Identyfikatora i należące do właścicieli zastrzeżony prefiks. Aby uzyskać więcej informacji, zobacz [dokumentacji dotyczącej rezerwowanie prefiksów identyfikatorów](../reference/id-prefix-reservation.md).

Metadane zawartych w obiekcie wynikowym wyszukiwania jest pobierana z najnowszej wersji pakietu. Każdy element na `versions` tablica jest obiekt JSON z następującymi właściwościami:

Nazwa      | Typ    | Wymagane | Uwagi
--------- | ------- | -------- | -----
@id       | string  | Tak      | Bezwzględny adres URL do powiązanych [liścia rejestracji](registration-base-url-resource.md#registration-leaf)
version   | string  | Tak      | Pełny ciąg wersji SemVer 2.0.0 pakietu (może zawierać metadane kompilacji).
Pliki do pobrania | integer | Tak      | Liczba plików do pobrania w tej wersji określonego pakietu

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [search-result.json](./_data/search-result.json)]
