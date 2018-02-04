---
title: Wyszukiwanie, NuGet interfejsu API | Dokumentacja firmy Microsoft
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
description: "Usługa wyszukiwania umożliwia klientom w zapytaniu dla pakietów według słów kluczowych i do wyników filtrowania dla niektórych pól pakietu."
keywords: "Interfejs API wyszukiwania NuGet, NuGet odnajdywanie pakietów, interfejs API do pakietów NuGet zapytania, aby przeglądać pakiety NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 612ce0f46b654335a29bb36a64b27525994162ed
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="search"></a>Wyszukaj

Istnieje możliwość wyszukiwania pakiety, które są dostępne w źródle pakietu przy użyciu interfejsu API w wersji 3. Zasób używany do wyszukiwania jest `SearchQueryService` można znaleźć zasobu w [indeksu usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@typewartość                   | Uwagi
----------------------------- | -----
SearchQueryService            | Początkowa wersja
SearchQueryService/3.0.0-beta | Alias`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias`SearchQueryService`

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsu API jest wartością `@id` właściwości skojarzone z jedną z wyżej wymienionych zasobów `@type` wartości. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.

## <a name="search-for-packages"></a>Wyszukaj pakietów

Wyszukiwanie interfejsu API umożliwia klientowi zapytania dla strony pakietów pasujących kwerendy wyszukiwania. Interpretacja zapytania wyszukiwania (np. tokenizacji terminy wyszukiwania) zależy od implementacji serwera, ale ogólne oczekuje się, że zapytania wyszukiwania służy do dopasowania identyfikatorów pakietów, tytułów, opisy i tagów. Mogą być również uwzględnione inne pola metadanych pakietu.

Pakiet nieznajdujące się na liście nigdy nie powinny być wyświetlane w wynikach wyszukiwania.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | string  | Brak       | Wyszukiwane terminy używane do filtrowania pakietów
Pomiń        | Adres URL    | integer | Brak       | Liczba wyników, aby pominąć dla podział na strony
podejmij        | Adres URL    | integer | Brak       | Liczba wyników do zwrócenia do podział na strony
wydanie wstępne  | Adres URL    | wartość logiczna | Brak       | `true`lub `false` określającą, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | Brak       | Ciąg wersji programu SemVer 1.0.0 

Zapytania wyszukiwania `q` jest analizowana w taki sposób, który jest zdefiniowany przez implementację serwera. obsługuje nuget.org podstawowe filtrowanie [wiele pól](../consume-packages/finding-and-choosing-packages.md#search-syntax). Jeśli nie `q` została podana, wszystkie pakiety powinny być zwracane w granicach powodowanego przez skip i take. Dzięki temu karta "Przeglądaj" w środowisku NuGet programu Visual Studio.

`skip` Domyślne wartości parametrów na 0.

`take` Parametr powinien być liczbą całkowitą większą niż zero. Implementacja serwera może nałożyć wartości maksymalnej.

Jeśli `prerelease` nie zostanie podany, pakiety wersji wstępnej są wyłączone.

`semVerLevel` Parametru zapytania jest używana do wyrazić zgodę na [pakiety programu SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Jeśli ten parametr zapytania jest wyłączone, zostaną zwrócone tylko pakiety programu SemVer 1.0.0 wersje zgodne (z [standardowe versioning NuGet](../reference/package-versioning.md) ostrzeżenia, na przykład ciągi wersji z 4 elementy liczba całkowita).
Jeśli `semVerLevel=2.0.0` została podana, zostanie zwrócony zarówno programu SemVer 1.0.0 i pakiety zgodne programu SemVer 2.0.0. Zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Aby uzyskać więcej informacji.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokument JSON zawierający do `take` wyników wyszukiwania. Wyniki wyszukiwania są pogrupowane według identyfikatora pakietu.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | integer          | Tak      | Całkowita liczba dopasowania, bez uwzględnienia `skip` i`take`
dane      | Tablica obiektów | Tak      | Wyniki wyszukiwania są dopasowane wg żądania

### <a name="search-result"></a>wynik wyszukiwania

Każdy element `data` tablica jest obiekt JSON składającej się z grupą wersji pakietu udostępnianie tego samego identyfikatora pakietu.
Obiekt ma następujące właściwości:

Nazwa           | Typ                       | Wymagane | Uwagi
-------------- | -------------------------- | -------- | -----
identyfikator             | string                     | Tak      | Identyfikator pakietu dopasowane
version        | string                     | Tak      | Pełny ciąg wersji programu SemVer 2.0.0 pakietu (może zawierać metadane kompilacji).
opis    | string                     | Brak       | 
wersje       | Tablica obiektów           | Tak      | Wszystkie wersje zgodnych pakietu `prerelease` parametru
Autorzy        | ciąg lub tablica ciągów | Brak       | 
iconUrl        | string                     | Brak       | 
licenseUrl     | string                     | Brak       | 
Właściciele         | ciąg lub tablica ciągów | Brak       | 
projectUrl     | string                     | Brak       | 
rejestracja   | string                     | Brak       | Bezwzględny adres URL do skojarzonego [indeksu rejestracji](registration-base-url-resource.md#registration-index)
podsumowanie        | string                     | Brak       | 
tagi           | ciąg lub tablica ciągów | Brak       | 
Tytuł          | string                     | Brak       | 
totalDownloads | integer                    | Brak       | Tę wartość można wywnioskować przez sumę pobierania w `versions` tablicy
Weryfikacji       | wartość logiczna                    | Brak       | Wartość wskazująca, czy pakiet jest logiczną JSON [weryfikacji](../reference/id-prefix-reservation.md)

Zweryfikowano pakietu na nuget.org, jest taki, który ma identyfikator pakietu dopasowania zastrzeżony prefiks Identyfikatora i należących do jednego z zarezerwowaną przestrzenią nazw właścicieli. Aby uzyskać więcej informacji, zobacz [dokumentację dotyczącą rezerwacji prefiks Identyfikatora](../reference/id-prefix-reservation.md).

Metadane zawarte w obiekcie wyników wyszukiwania jest pobierana z najnowszą wersję pakietu. Każdy element `versions` tablica jest obiekt JSON z następującymi właściwościami:

Nazwa      | Typ    | Wymagane | Uwagi
--------- | ------- | -------- | -----
@id       | string  | Tak      | Bezwzględny adres URL do skojarzonego [liścia rejestracji](registration-base-url-resource.md#registration-leaf)
version   | string  | Tak      | Pełny ciąg wersji programu SemVer 2.0.0 pakietu (może zawierać metadane kompilacji).
Pliki do pobrania | integer | Tak      | Liczbę pobrań dla tej wersji określonego pakietu

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [search-result.json](./_data/search-result.json)]
