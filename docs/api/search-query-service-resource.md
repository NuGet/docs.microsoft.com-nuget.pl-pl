---
title: Wyszukiwanie, interfejs API NuGet
description: Usługa Search umożliwia klientom wykonywanie zapytań o pakiety według słów kluczowych i filtrowanie wyników dla niektórych pól pakietu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7047dfd48b7f93756bbb1491de1b7e65da2c12b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775416"
---
# <a name="search"></a>Wyszukaj

Istnieje możliwość wyszukiwania pakietów dostępnych w źródle pakietów przy użyciu interfejsu API v3. Zasób używany do wyszukiwania jest `SearchQueryService` zasobem znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

`@type`Są używane następujące wartości:

@type wartościami                   | Uwagi
----------------------------- | -----
SearchQueryService            | Początkowa wersja
SearchQueryService/3.0.0 — beta | Alias `SearchQueryService`
SearchQueryService/3.0.0-RC   | Alias `SearchQueryService`
SearchQueryService/3.5.0      | Obejmuje obsługę `packageType` parametru zapytania

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
Ta wersja wprowadza obsługę `packageType` parametrów zapytania i `packageTypes` właściwość Response, umożliwiając filtrowanie według typów pakietów zdefiniowanych przez autora. Jest w pełni zgodna z poprzednimi wersjami zapytań `SearchQueryService` .

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL następującego interfejsu API to wartość `@id` Właściwości skojarzonej z jedną z wymienionych powyżej `@type` wartości zasobów. W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego adresu URL `{@id}` .

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują metody HTTP `GET` i `HEAD` .

## <a name="search-for-packages"></a>Wyszukaj pakiety

Interfejs API wyszukiwania umożliwia klientowi wykonywanie zapytań dotyczących strony pakietów pasujących do określonego zapytania wyszukiwania. Interpretacja zapytania wyszukiwania (np. tokenizacji warunków wyszukiwania) jest określana przez implementację serwera, ale ogólnie oczekuje się, że zapytanie wyszukiwania jest używane do dopasowywania identyfikatorów pakietów, tytułów, opisów i tagów. Można również rozważyć inne pola metadanych pakietu.

Nieznajdujący się na liście pakiet nigdy nie powinien być wyświetlany w wynikach wyszukiwania.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa        | W     | Typ    | Wymagane | Uwagi
----------- | ------ | ------- | -------- | -----
q           | Adres URL    | ciąg  | nie       | Terminy wyszukiwania używane do filtrowania pakietów
Pomiń        | Adres URL    | liczba całkowita | nie       | Liczba wyników do pominięcia na stronie stronicowania
take (pobierz)        | Adres URL    | liczba całkowita | nie       | Liczba wyników do zwrócenia, na stronie stronicowania
wersja wstępna  | Adres URL    | boolean | nie       | `true` lub `false` określając, czy dołączać [pakiety wersji wstępnej](../create-packages/prerelease-packages.md)
semVerLevel | Adres URL    | ciąg  | nie       | Ciąg wersji SemVer 1.0.0 
packageType | Adres URL    | ciąg  | nie       | Typ pakietu, który ma być używany do filtrowania pakietów (dodana w `SearchQueryService/3.5.0` )

Zapytanie wyszukiwania `q` jest analizowane w sposób zdefiniowany przez implementację serwera. nuget.org obsługuje podstawowe filtrowanie w [różnych polach](../consume-packages/finding-and-choosing-packages.md#search-syntax). Jeśli nie `q` podano żadnego z nich, wszystkie pakiety powinny być zwracane, w granicach nałożonych przez Skip i Take. Spowoduje to włączenie karty "Przeglądaj" w środowisku NuGet programu Visual Studio.

Wartość `skip` domyślna parametru to 0.

`take`Parametr powinien być liczbą całkowitą większą od zera. Implementacja serwera może mieć wartość maksymalną.

Jeśli `prerelease` nie jest podany, pakiety wersji wstępnej są wykluczone.

`semVerLevel`Parametr zapytania jest używany do wybierania [pakietów SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Jeśli ten parametr zapytania jest wykluczony, zwracane są tylko pakiety z wersjami zgodnymi z programem SemVer 1.0.0 (ze standardowymi ostrzeżeniami dotyczącymi [wersji NuGet](../concepts/package-versioning.md) , takimi jak ciągi wersji z 4 liczbami całkowitymi).
Jeśli `semVerLevel=2.0.0` jest podany, zwracane są zgodne z SemVer 1.0.0 i SemVer 2.0.0. Aby uzyskać więcej informacji, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

Ten `packageType` parametr służy do dalszej odfiltrowania wyników wyszukiwania tylko do pakietów, które mają co najmniej jeden typ pakietu zgodny z nazwą typu pakietu.
Jeśli podany typ pakietu nie jest prawidłowym typem pakietu zdefiniowanym przez [dokument typu pakietu](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), zostanie zwrócony pusty wynik.
Jeśli podany typ pakietu jest pusty, żaden filtr nie zostanie zastosowany. Innymi słowy, przekazywanie żadnej wartości do parametru PackageType będzie zachowywać się tak, jakby parametr nie został przekazano.

### <a name="response"></a>Reakcja

Odpowiedź to dokument JSON zawierający do `take` wyników wyszukiwania. Wyniki wyszukiwania są pogrupowane według identyfikatora pakietu.

Główny obiekt JSON ma następujące właściwości:

Nazwa      | Typ             | Wymagane | Uwagi
--------- | ---------------- | -------- | -----
totalHits | liczba całkowita          | tak      | Łączna liczba dopasowań, odnoszących się `skip` do i `take`
dane      | Tablica obiektów | tak      | Wyniki wyszukiwania dopasowane przez żądanie

### <a name="search-result"></a>Wynik wyszukiwania

Każdy element w `data` tablicy to obiekt JSON składający się z grupy wersji pakietu, które współużytkują ten sam identyfikator pakietu.
Obiekt ma następujące właściwości:

Nazwa           | Typ                       | Wymagane | Uwagi
-------------- | -------------------------- | -------- | -----
identyfikator             | ciąg                     | tak      | Identyfikator dopasowanego pakietu
Wersja        | ciąg                     | tak      | Pełny SemVer 2.0.0 wersji pakietu (może zawierać metadane kompilacji)
description (opis)    | ciąg                     | nie       | 
versions (wersje)       | Tablica obiektów           | tak      | Wszystkie wersje pakietu pasujące do `prerelease` parametru
autorów        | ciąg lub tablica ciągów | nie       | 
iconUrl        | ciąg                     | nie       | 
licenseUrl     | ciąg                     | nie       | 
rzecz         | ciąg lub tablica ciągów | nie       | 
projectUrl     | ciąg                     | nie       | 
rejestracja   | ciąg                     | nie       | Bezwzględny adres URL ze skojarzonym [indeksem rejestracji](registration-base-url-resource.md#registration-index)
Podsumowanie        | ciąg                     | nie       | 
tags           | ciąg lub tablica ciągów | nie       | 
tytuł          | ciąg                     | nie       | 
totalDownloads | liczba całkowita                    | nie       | Ta wartość może zostać wywnioskowana przez sumę pobrań w `versions` tablicy
sprawdzić       | boolean                    | nie       | Wartość logiczna JSON wskazująca, czy pakiet jest [zweryfikowany](../nuget-org/id-prefix-reservation.md)
packageTypes   | Tablica obiektów           | tak      | Typy pakietów zdefiniowane przez autora pakietu (dodane w `SearchQueryService/3.5.0` )

W systemie nuget.org zweryfikowany pakiet to taki, który ma identyfikator pakietu pasujący do zastrzeżonego prefiksu identyfikatora i należy do jednego z właścicieli zastrzeżonego prefiksu. Aby uzyskać więcej informacji, zobacz [dokumentację dotyczącą rezerwacji prefiksów identyfikatorów](../nuget-org/id-prefix-reservation.md).

Metadane zawarte w obiekcie wynik wyszukiwania są pobierane z najnowszej wersji pakietu. Każdy element w `versions` tablicy jest obiektem JSON o następujących właściwościach:

Nazwa      | Typ    | Wymagane | Uwagi
--------- | ------- | -------- | -----
@id       | ciąg  | tak      | Bezwzględny adres URL do skojarzonego [liścia rejestracji](registration-base-url-resource.md#registration-leaf)
Wersja   | ciąg  | tak      | Pełny SemVer 2.0.0 wersji pakietu (może zawierać metadane kompilacji)
pliki do pobrania | liczba całkowita | tak      | Liczba pobrań dla tej konkretnej wersji pakietu

`packageTypes`Tablica będzie zawsze składać się z co najmniej jednego elementu (1). Typ pakietu dla danego identyfikatora pakietu jest uznawany za typy pakietów zdefiniowane przez najnowszą wersję pakietu w odniesieniu do innych parametrów wyszukiwania. Każdy element w `packageTypes` tablicy jest obiektem JSON o następujących właściwościach:

Nazwa      | Typ    | Wymagane | Uwagi
--------- | ------- | -------- | -----
name      | ciąg  | tak      | Nazwa typu pakietu.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [search-result.json](./_data/search-result.json)]