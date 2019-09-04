---
title: Wyszukiwanie, interfejs API NuGet
description: Usługa Search umożliwia klientom wykonywanie zapytań o pakiety według słów kluczowych i filtrowanie wyników dla niektórych pól pakietu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235125"
---
# <a name="search"></a>Wyszukaj

Istnieje możliwość wyszukiwania pakietów dostępnych w źródle pakietów przy użyciu interfejsu API v3. Zasób używany do wyszukiwania jest `SearchQueryService` zasobem znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Są używane `@type` następujące wartości:

@typewartościami                   | Uwagi
----------------------------- | -----
SearchQueryService            | Początkowa wersja
SearchQueryService/3.0.0-beta | Alias`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias`SearchQueryService`

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL następującego interfejsu API to wartość `@id` właściwości skojarzonej z jedną z wymienionych powyżej wartości zasobów. `@type` W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego `{@id}` adresu URL.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują `GET` metody `HEAD`http i.

## <a name="search-for-packages"></a>Wyszukaj pakiety

Interfejs API wyszukiwania umożliwia klientowi wykonywanie zapytań dotyczących strony pakietów pasujących do określonego zapytania wyszukiwania. Interpretacja zapytania wyszukiwania (np. tokenizacji warunków wyszukiwania) jest określana przez implementację serwera, ale ogólnie oczekuje się, że zapytanie wyszukiwania jest używane do dopasowywania identyfikatorów pakietów, tytułów, opisów i tagów. Można również rozważyć inne pola metadanych pakietu.

Nieznajdujący się na liście pakiet nigdy nie powinien być wyświetlany w wynikach wyszukiwania.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | string  | znaleziono       | Terminy wyszukiwania używane do filtrowania pakietów
Pomiń        | Adres URL    | integer | znaleziono       | Liczba wyników do pominięcia na stronie stronicowania
czasochłonn        | Adres URL    | integer | znaleziono       | Liczba wyników do zwrócenia, na stronie stronicowania
wersja wstępna  | Adres URL    | wartość logiczna | znaleziono       | `true`lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | string  | znaleziono       | Ciąg wersji SemVer 1.0.0 

Zapytanie `q` wyszukiwania jest analizowane w sposób zdefiniowany przez implementację serwera. nuget.org obsługuje podstawowe filtrowanie w [różnych polach](../consume-packages/finding-and-choosing-packages.md#search-syntax). Jeśli nie `q` podano żadnego z nich, wszystkie pakiety powinny być zwracane, w granicach nałożonych przez Skip i Take. Spowoduje to włączenie karty "Przeglądaj" w środowisku NuGet programu Visual Studio.

Wartość `skip` domyślna parametru to 0.

`take` Parametr powinien być liczbą całkowitą większą od zera. Implementacja serwera może mieć wartość maksymalną.

Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.

Parametr zapytania jest używany do wybierania [pakietów SemVer 2.0.0.](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`
Jeśli ten parametr zapytania jest wykluczony, zwracane są tylko pakiety z wersjami zgodnymi z programem SemVer 1.0.0 (ze standardowymi ostrzeżeniami dotyczącymi [wersji NuGet](../concepts/package-versioning.md) , takimi jak ciągi wersji z 4 liczbami całkowitymi).
Jeśli `semVerLevel=2.0.0` jest podany, zwracane są zgodne z SemVer 1.0.0 i SemVer 2.0.0. Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Odpowiedź

Odpowiedź to dokument JSON zawierający do `take` wyników wyszukiwania. Wyniki wyszukiwania są pogrupowane według identyfikatora pakietu.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | integer          | tak      | Łączna liczba dopasowań, odnoszących `skip` się do i`take`
dane      | Tablica obiektów | tak      | Wyniki wyszukiwania dopasowane przez żądanie

### <a name="search-result"></a>Wynik wyszukiwania

Każdy element w `data` tablicy to obiekt JSON składający się z grupy wersji pakietu, które współużytkują ten sam identyfikator pakietu.
Obiekt ma następujące właściwości:

Nazwa           | Typ                       | Wymagane | Uwagi
-------------- | -------------------------- | -------- | -----
identyfikator             | string                     | tak      | Identyfikator dopasowanego pakietu
version        | string                     | tak      | Pełny SemVer 2.0.0 wersji pakietu (może zawierać metadane kompilacji)
opis    | string                     | znaleziono       | 
wersje       | Tablica obiektów           | tak      | Wszystkie wersje pakietu pasujące do `prerelease` parametru
autorów        | ciąg lub tablica ciągów | znaleziono       | 
iconUrl        | string                     | znaleziono       | 
licenseUrl     | string                     | znaleziono       | 
rzecz         | ciąg lub tablica ciągów | znaleziono       | 
projectUrl     | string                     | znaleziono       | 
rejestracja   | string                     | znaleziono       | Bezwzględny adres URL ze skojarzonym [indeksem rejestracji](registration-base-url-resource.md#registration-index)
podsumowanie        | string                     | znaleziono       | 
tagi           | ciąg lub tablica ciągów | znaleziono       | 
title          | string                     | znaleziono       | 
totalDownloads | integer                    | znaleziono       | Ta wartość może zostać wywnioskowana przez sumę pobrań w `versions` tablicy
sprawdzić       | wartość logiczna                    | znaleziono       | Wartość logiczna JSON wskazująca, czy pakiet jest [zweryfikowany](../nuget-org/id-prefix-reservation.md)

W systemie nuget.org zweryfikowany pakiet to taki, który ma identyfikator pakietu pasujący do zastrzeżonego prefiksu identyfikatora i należy do jednego z właścicieli zastrzeżonego prefiksu. Aby uzyskać więcej informacji, zobacz [dokumentację dotyczącą rezerwacji prefiksów identyfikatorów](../reference/id-prefix-reservation.md).

Metadane zawarte w obiekcie wynik wyszukiwania są pobierane z najnowszej wersji pakietu. Każdy element w `versions` tablicy jest obiektem JSON o następujących właściwościach:

Nazwa      | Typ    | Wymagane | Uwagi
--------- | ------- | -------- | -----
@id       | string  | tak      | Bezwzględny adres URL do skojarzonego [liścia rejestracji](registration-base-url-resource.md#registration-leaf)
version   | string  | tak      | Pełny SemVer 2.0.0 wersji pakietu (może zawierać metadane kompilacji)
proces | integer | tak      | Liczba pobrań dla tej konkretnej wersji pakietu

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [search-result.json](./_data/search-result.json)]
