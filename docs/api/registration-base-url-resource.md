---
title: Metadane pakietu, interfejs API programu NuGet
description: Pakiet rejestracyjny podstawowy adres URL umożliwia pobieranie metadanych dotyczących pakietów.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 19a1f48164f65f1ff805e036e55abb110247aa72
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324867"
---
# <a name="package-metadata"></a>Metadane pakietu

Istnieje możliwość pobrania metadanych o pakietach, które są dostępne w źródle pakietu przy użyciu interfejsu API programu NuGet w wersji 3. Te metadane mogą być pobierane przy użyciu `RegistrationsBaseUrl` można znaleźć zasobu w [indeks usług](service-index.md).

Zbiór dokumentów, znajdują się w `RegistrationsBaseUrl` są często nazywane "rejestracje" lub "obiektów blob rejestracji". Zestaw dokumentów w ramach pojedynczej `RegistrationsBaseUrl` jest określany jako "gałąź rejestracji". Gałąź rejestracji zawiera wszystkie metadane dotyczące każdego pakietu dostępne w źródle pakietu.

## <a name="versioning"></a>Obsługa wersji

Następujące `@type` są używane wartości:

@type Wartość                     | Uwagi
------------------------------- | -----
RegistrationsBaseUrl            | Wersja początkowa
RegistrationsBaseUrl/3.0.0-beta | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Odpowiedzi w formacie gzip
RegistrationsBaseUrl/3.6.0      | Zawiera pakiety SemVer 2.0.0

Reprezentuje trzech odrębnych rejestracji gałęzie dostępne dla różnych wersji klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Nieskompresowane tyto registrace (co oznacza, korzystają z domniemanym `Content-Encoding: identity`). Pakiety SemVer 2.0.0 **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Tyto registrace są kompresowane, za pomocą `Content-Encoding: gzip`. Pakiety SemVer 2.0.0 **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Tyto registrace są kompresowane, za pomocą `Content-Encoding: gzip`. Pakiety SemVer 2.0.0 **uwzględnione** w tej gałęzi.
Aby uzyskać więcej informacji na temat SemVer 2.0.0 zobacz [SemVer 2.0.0 obsługę nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartości. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.

## <a name="registration-index"></a>Indeks rejestracji

Grupy zasobów rejestracji pakietu metadanych według identyfikatora pakietu. Nie jest możliwe uzyskać dane o więcej niż jeden identyfikator pakietu w danym momencie. Ten zasób zapewnia sposób odnajdywania identyfikatorów pakietu. Zamiast tego klient zakłada się, że już znasz identyfikator żądanego pakietu. Dostępne metadane dotyczące każdej wersji pakietu jest zależna od implementacji serwera. Obiekty BLOB rejestracji pakietu mają następującą strukturę hierarchiczną:

- **Indeks**: punkt wejścia dla metadanych pakietu, współużytkowane przez wszystkie pakiety w źródle, przy użyciu tego samego identyfikatora pakietu.
- **Strona**: grupowanie wersji pakietu. Numer wersji pakietu na stronie jest definiowany przez implementację serwera.
- **Liścia**: dokument wersji jednym pakiecie.

Adres URL indeksu rejestracji jest przewidywalne oraz można określić przez klienta podany identyfikator pakietu i zasobów rejestracji `@id` wartość indeksu usługi. Adresy URL strony rejestracji i pozostawia są wykrywane, sprawdzając indeksu rejestracji.

### <a name="registration-pages-and-leaves"></a>Strony rejestracji i pozostawia

Chociaż nie jest właściwie ma wymagane dla implementacji serwera, do przechowywania że rejestracji liści w dokumentach strony rejestracji odrębnych, jest zalecaną praktyką w celu zachowywania pamięci po stronie klienta. Zamiast wszystkich wbudowanie rejestracji pozostawia w indeksie lub od razu przechowywania pozostawia w dokumentach strony, zaleca się, że implementacja serwera zdefiniować niektóre heurystyki do wyboru dwie metody oparte na liczbie wersji pakietów lub pozostawia całkowity rozmiar pakietu.

Przechowywanie wszystkich wersji pakietu (pozostawia) w zapisuje indeksu rejestracji liczby żądań HTTP niezbędne do pobierania pakietu metadanych, ale oznacza, że dokumentu większe należy go najpierw pobrać i muszą być przydzielane więcej pamięci klienta. Z drugiej strony jeśli implementacja serwera natychmiast przechowuje rejestracji pozostawia w dokumentach na osobnej stronie, klienta, należy wykonać więcej żądań HTTP, aby uzyskać informacje, których potrzebuje.

Algorytm heurystyczny, który używa nuget.org jest następująca: Jeśli istnieje co najmniej 128 wersji pakietu, przerwania liści do stron o rozmiarze 64. W przypadku wersji mniej niż 128 wszystkie wbudowane pozostawia do indeksu rejestracji.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry żądania

Nazwa     | W     | Typ    | Wymagane | Uwagi
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adres URL    | string  | tak      | Identyfikator pakietu pisany małymi literami

`LOWER_ID` Wartość jest pisany małymi literami, za pomocą reguł wdrożonych przez identyfikator żądanego pakietu. NET firmy [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokumentem JSON, który jest obiektem głównym, z następującymi właściwościami:

Nazwa  | Typ             | Wymagane | Uwagi
----- | ---------------- | -------- | -----
count | integer          | tak      | Liczba stron rejestracji w indeksie
Elementy | Tablica obiektów | tak      | Tablica stron rejestracji

Każdy element w obiekcie indeksu `items` tablica jest obiektem JSON reprezentujący stronę rejestracji.

#### <a name="registration-page-object"></a>Obiekt strony rejestracji

Obiekt strony rejestracji w indeksie rejestracji ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | tak      | Adres URL do strony rejestracji
count  | integer          | tak      | Numer rejestracji pozostawia na stronie
Elementy  | Tablica obiektów | Brak       | Tablica pozostawia rejestracji i ich kojarzenie metadanych
Niższy  | string           | tak      | Najniższa wersja SemVer 2.0.0 na stronie (włącznie)
Nadrzędny | string           | Brak       | Adres URL do indeksu rejestracji
górny  | string           | tak      | Najwyższa wersja SemVer 2.0.0 na stronie (włącznie)

`lower` i `upper` granice obiektu strony są przydatne, jeśli potrzebne są metadane dla określonej strony wersji.
Te granice może służyć do pobrania na stronie rejestracji tylko potrzebne. Ciągi wersji stosować [reguły wersji NuGet](../reference/package-versioning.md). Ciągi wersji są znormalizowane i nie zawierają metadanych kompilacji. Zgodnie ze wszystkimi wersjami należący do ekosystemu NuGet Porównanie ciągów wersji jest implementowany przy użyciu [reguły pierwszeństwa wersji SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

`parent` Właściwości będą wyświetlane tylko wtedy, jeśli obiekt strony rejestracji ma `items` właściwości.

Jeśli `items` właściwość nie jest obecny w obiekcie strony rejestracji, adres URL określony w `@id` musi być używane do pobierania metadanych dotyczących wersje poszczególnych pakietów. `items` Tablicy czasami jest wykluczony z obiektu strony w ramach optymalizacji. W przypadku bardzo dużej liczby wersji identyfikator pojedynczy pakiet rejestracji dokumentu indeksu zostaną masowych i marnotrawstwa do procesu dla klienta, który tylko dba o określonej wersji lub niewielki zakres wersji.

Należy pamiętać, że jeśli `items` właściwość jest obecny, `@id` muszą nie można użyć właściwości, ponieważ wszystkie dane strony jest już śródwierszowe w `items` właściwości.

Każdy element w obiekcie strony `items` tablicy jest obiektem JSON reprezentujący liścia rejestracji i skojarzony z nim metadane.

#### <a name="registration-leaf-object-in-a-page"></a>Obiekt typu liść rejestracji na stronie

Obiekt typu liść rejestracji znaleźć na stronie rejestracji ma następujące właściwości:

Nazwa           | Typ   | Wymagane | Uwagi
-------------- | ------ | -------- | -----
@id            | string | tak      | Adres URL rejestracji typu liść
catalogEntry   | object | tak      | Wpis katalogu, zawierający metadane pakietu
packageContent | string | tak      | Adres URL do zawartości pakietów (.nupkg)

Każdy obiekt typu liść rejestracji reprezentuje dane skojarzone z wersją w jednym pakiecie.

#### <a name="catalog-entry"></a>Wpis katalogu

`catalogEntry` Właściwości w obiekcie typu liść rejestracji ma następujące właściwości:

Nazwa                     | Typ                       | Wymagane | Uwagi
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | tak      | Adres URL, aby dokument użyty do utworzenia tego obiektu
Autorzy                  | ciąg lub tablicę ciągów | Brak       | 
dependencyGroups         | Tablica obiektów           | Brak       | Zależności pakietu, pogrupowane według platformy docelowej
opis              | string                     | Brak       | 
iconUrl                  | string                     | Brak       | 
identyfikator                       | string                     | tak      | Identyfikator pakietu
licenseUrl               | string                     | Brak       |
licenseExpression        | string                     | Brak       | 
wymienione                   | wartość logiczna                    | Brak       | Powinny być traktowane jako wymienionych Jeśli go nie ma
Atrybut MinClientVersion         | string                     | Brak       | 
projectUrl               | string                     | Brak       | 
Opublikowane                | string                     | Brak       | Ciąg zawierający ISO 8601 sygnaturę czasową gdy pakiet został opublikowany
requireLicenseAcceptance | wartość logiczna                    | Brak       | 
podsumowanie                  | string                     | Brak       | 
tagi                     | ciąg lub tablica ciągów  | Brak       | 
tytuł                    | string                     | Brak       | 
version                  | string                     | tak      | Ciąg pełnej wersji po normalizacji

Pakiet `version` właściwości jest ciągiem pełnej wersji po normalizacji. Oznacza to, że dane kompilacji SemVer 2.0.0 można uwzględnić w tym miejscu.

`dependencyGroups` Właściwość jest Tablica obiektów reprezentująca zależności pakietu, pogrupowane według wartości docelowej. Jeśli pakiet nie ma zależności, `dependencyGroups` brakuje właściwości, pusta tablica lub `dependencies` właściwość wszystkich grup jest pusta lub Brak.

Wartość `licenseExpression` właściwość jest zgodny z [składni wyrażenia licencji NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Grupa zależności pakietu

Każdy obiekt grupy zależności ma następujące właściwości:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
targetFramework | string           | Brak       | Platforma docelowa, które dotyczą te zależności
zależności    | Tablica obiektów | Brak       |

`targetFramework` Ciąg w formacie implementowany przez NuGet biblioteki .NET [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Jeśli nie `targetFramework` jest określona grupa zależności, który ma zastosowanie do wszystkich platform docelowych.

`dependencies` Właściwość jest Tablica obiektów, każdy reprezentuje zależność pakietu bieżącego pakietu.

#### <a name="package-dependency"></a>Zależność pakietu

Poszczególne zależności pakietu ma następujące właściwości:

Nazwa         | Typ   | Wymagane | Uwagi
------------ | ------ | -------- | -----
identyfikator           | string | tak      | Identyfikator zależności pakietu
range        | object | Brak       | Dozwolona [zakres wersji](../reference/package-versioning.md#version-ranges-and-wildcards) zależności
rejestracja | string | Brak       | Adres URL do indeksu rejestracji dla tej zależności

Jeśli `range` właściwość jest wyłączona lub pustym ciągiem, klient powinien domyślnych do zakresu wersji `(, )`. Oznacza to, że dowolną wersję zależność jest dozwolone.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

W tym konkretnym przypadku indeks rejestracji ma śródwierszowych strony rejestracji, dzięki czemu żadne dodatkowe żądania są wymagane do pobierania metadanych dotyczących wersje poszczególnych pakietów.

## <a name="registration-page"></a>Strona rejestracji

Strona rejestracji zawiera pozostawia rejestracji. Adres URL, aby pobrać strony rejestracji jest określana przez `@id` właściwość [obiektu strony rejestracji](#registration-page-object) wymienionych powyżej.

Gdy `items` tablicy nie zostanie podany w indeksie rejestracji, żądanie HTTP GET z `@id` wartość zwróci dokument JSON, który ma obiektu jako jego katalogu głównego. Obiekt ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | tak      | Adres URL do strony rejestracji
count  | integer          | tak      | Numer rejestracji pozostawia na stronie
Elementy  | Tablica obiektów | tak      | Tablica pozostawia rejestracji i ich kojarzenie metadanych
Niższy  | string           | tak      | Najniższa wersja SemVer 2.0.0 na stronie (włącznie)
Nadrzędny | string           | tak      | Adres URL do indeksu rejestracji
górny  | string           | tak      | Najwyższa wersja SemVer 2.0.0 na stronie (włącznie)

Kształt obiektów typu liść rejestracji jest taka sama, jak indeksu rejestracji [powyżej](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Rejestracja typu liść

Liścia rejestracji zawiera informacje o identyfikatorze określonego pakietu i wersję. Metadane dotyczące określonej wersji może nie być dostępne w tym dokumencie. Metadane pakietu mają zostać pobrane z [indeksu rejestracji](#registration-index) lub [strony rejestracji](#registration-page) (który został odnaleziony przy użyciu indeksu rejestracji).

Adres URL, aby pobrać liścia rejestracji jest uzyskiwana z `@id` właściwości obiektu typu liść rejestracji w rejestracji indeksu lub strona rejestracji.

Liścia rejestracji to dokument JSON z obiektem głównym, z następującymi właściwościami:

Nazwa           | Typ    | Wymagane | Uwagi
-------------- | ------- | -------- | -----
@id            | string  | tak      | Adres URL rejestracji typu liść
catalogEntry   | string  | Brak       | Adres URL wpisu wykazu, który te typu liść
wymienione         | wartość logiczna | Brak       | Powinny być traktowane jako wymienionych Jeśli go nie ma
packageContent | string  | Brak       | Adres URL do zawartości pakietów (.nupkg)
Opublikowane      | string  | Brak       | Ciąg zawierający ISO 8601 sygnaturę czasową gdy pakiet został opublikowany
rejestracja   | string  | Brak       | Adres URL do indeksu rejestracji

> [!Note]
> W witrynie nuget.org `published` ma wartość roku 1900, gdy pakiet jest nieobecne na liście.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
