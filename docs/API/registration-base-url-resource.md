---
title: Pakiet NuGet interfejsu API metadanych | Dokumentacja firmy Microsoft
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
ms.assetid: 96b07019-c2e1-4f40-9290-f65ad71af3b1
description: "Pakiet rejestracyjny podstawowy adres URL umożliwia pobieranie metadanych dotyczących pakietów."
keywords: "Metadane pakietów NuGet interfejsu API, NuGet interfejsu API rejestracji, interfejsu API NuGet nieznajdujące się na liście pakietów"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1aabe6ae5c661e12b2639700813946e7a9a58b24
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="package-metadata"></a>Metadane pakietów

Istnieje możliwość pobrania metadane dotyczące pakiety dostępne w źródle pakietu przy użyciu interfejsu API w wersji 3 NuGet. Te metadane mogą być pobierane przy użyciu `RegistrationsBaseUrl` można znaleźć zasobu w [indeksu usługi](service-index.md).

Kolekcja dokumentów omówionych w artykule `RegistrationsBaseUrl` są często nazywane "rejestracji" lub "obiekty BLOB rejestracji". Zestaw dokumentów pod jedną `RegistrationsBaseUrl` nazywa się "hive rejestracji". Gałąź rejestracji zawiera wszystkie metadane dotyczące każdy pakiet dostępne w źródle pakietu.

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@typewartość                     | Uwagi
------------------------------- | -----
RegistrationsBaseUrl            | Początkowa wersja
RegistrationsBaseUrl/3.0.0-beta | Alias`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Odpowiedzi w formacie gzip
RegistrationsBaseUrl/3.6.0      | Zawiera pakiety programu SemVer 2.0.0

Reprezentuje trzy różne rejestracji gałęzie dostępne dla różnych wersji klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Te nie są kompresowane (co oznacza korzystają z domniemanym `Content-Encoding: identity`). Pakiety programu SemVer 2.0.0 **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Te są skompresowane za pomocą `Content-Encoding: gzip`. Pakiety programu SemVer 2.0.0 **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Te są skompresowane za pomocą `Content-Encoding: gzip`. Pakiety programu SemVer 2.0.0 **uwzględnione** w tej gałęzi.
Aby uzyskać więcej informacji na temat programu SemVer 2.0.0, zobacz [obsługę programu SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Podstawowy adres URL

Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartości. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.

## <a name="registration-index"></a>Indeks rejestracji

Grupy zasobów rejestracji pakietu metadanych według identyfikatora pakietu. Nie jest możliwe uzyskać dane o więcej niż jeden identyfikator pakietu w czasie. Ten zasób zapewnia nie można odnaleźć identyfikatorów pakietów. Zamiast tego klient zakłada się, że już znany identyfikator żądanego pakietu. Dostępne metadane dotyczące poszczególnych wersji pakietu jest zależna od implementacji serwera. Obiekty BLOB rejestracji pakietu ma następującą strukturę hierarchiczną:

- **Indeks**: punkt wejścia dla metadane pakietów, współużytkowana przez wszystkie pakiety w źródle z tego samego identyfikatora pakietu.
- **Strona**: Grupa wersje pakietów. Numer wersji pakietu na stronie zdefiniowano przez implementację serwera.
- **Liścia**: właściwe dla wersji pakietu pojedynczego dokumentu.

Adres URL rejestracji indeksu jest atrybutem wartości prognozowanych i można określić przez klienta podany identyfikator pakietu i zasobów rejestracji `@id` wartości z indeksu usługi. Adresy URL strony rejestracji i pozostawia są odnajdywane przez badanie indeksu rejestracji.

### <a name="registration-pages-and-leaves"></a>Strony rejestracji i pozostawia

Chociaż nie ściśle są wymagane dla wdrożenia serwera do przechowywania się, że rejestracja liści w dokumentach strony rejestracji odrębnych, jest zalecaną praktyką w celu zachowywania pamięci po stronie klienta. Zamiast ze śródwierszowaniem wszystkich rejestracji pozostawia w lub od razu przechowywania pozostawia w dokumentach strony indeksu, zaleca się, że implementacją serwera zdefiniować niektóre heurystyki wybrać dwa podejścia na podstawie numeru wersji pakietu lub pozostawia całkowity rozmiar pakietu.

Przechowywanie wszystkich wersji pakietu (pozostawia) w rejestracji zapisuje indeksu liczby żądań HTTP niezbędne do pobrania pakietu metadanych, ale oznacza, że jest większy dokument musi zostać pobrana i musi być przydzielona większa ilość pamięci klienta. Z drugiej strony jeśli implementacja serwera natychmiast przechowuje rejestracji pozostawia w dokumentach na osobnej stronie, klienta należy wykonać więcej żądań HTTP, aby uzyskać informacje, które są niezbędne.

Heurystyka, który używa nuget.org wygląda następująco: Jeśli istnieje co najmniej 128 wersji pakietu, Podziel liści na stronach o rozmiarze 64. Jeśli dostępne są wersje mniej niż 128, wbudowanego wszystkich pozostawia do indeksu rejestracji.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa     | W     | Typ    | Wymagane | Uwagi
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adres URL    | string  | Tak      | Identyfikator pakietu małej

`LOWER_ID` Wartość jest małej, za pomocą reguł wdrożonych przez identyfikator żądanego pakietu. W sieci [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokumentem JSON, który ma główny obiekt z następującymi właściwościami:

Nazwa  | Typ             | Wymagane | Uwagi
----- | ---------------- | -------- | -----
count | integer          | Tak      | Liczba stron rejestracji w indeksie
Elementy | Tablica obiektów | Tak      | Tablica stron rejestracji

Każdego elementu w obiekcie indeksu `items` tablica jest obiekt JSON reprezentujący stronę rejestracji.

#### <a name="registration-page-object"></a>Obiekt strony rejestracji

Obiekt strony rejestracji w indeksie rejestracyjnych ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | Tak      | Adres URL do strony rejestracji
count  | integer          | Tak      | Numer rejestracji pozostawia na stronie
Elementy  | Tablica obiektów | Brak       | Tablica rejestracji pozostawia i ich Skojarz metadanych
Niższe  | string           | Tak      | Najniższa wersja programu SemVer 2.0.0 na stronie (włącznie)
Nadrzędny | string           | Brak       | Adres URL do indeksu rejestracji
górny  | string           | Tak      | Najwyższa wersja programu SemVer 2.0.0 na stronie (włącznie)

`lower` i `upper` granice obiektu strony są przydatne, gdy potrzebne jest metadanych dla wersji określonej strony.
Te granice można pobrać strony rejestracji tylko wymagane. Ciągi wersja zgodna [reguły wersji NuGet](../reference/package-versioning.md). Ciągi wersji są znormalizowany i nie zawierają metadanych kompilacji. Zgodnie ze wszystkimi wersjami w ekosystemie NuGet porównania ciągów wersji jest implementowane za pomocą [reguły pierwszeństwo wersji programu SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

`parent` Właściwość będą wyświetlane tylko, jeśli obiekt strony rejestracji zawiera `items` właściwości.

Jeśli `items` nie ma właściwości w obiekcie strony rejestracji, adres URL określony w `@id` musi być używany do pobierania metadanych dotyczących wersje poszczególnych pakietów. `items` Tablicy czasami jest wykluczony z obiektu strony do optymalizacji. W przypadku bardzo dużej liczby wersji identyfikator pojedynczy pakiet rejestracji w dokumencie indeksu zostaną masowych i niepotrzebne do procesu klienta, który tylko dba o określonej wersji lub małe zakres wersji.

Należy pamiętać, że jeśli `items` ma właściwość `@id` właściwości nie może być używany, ponieważ wszystkie dane strony są już wbudowanego w `items` właściwości.

Każdego elementu w obiekcie strony `items` tablicy jest obiekt JSON reprezentuje liścia rejestracji i ma skojarzone metadane.

#### <a name="registration-leaf-object-in-a-page"></a>Obiekt typu liść rejestracji na stronie

Obiekt typu liść rejestracji na stronie rejestracji znaleziono ma następujące właściwości:

Nazwa           | Typ   | Wymagane | Uwagi
-------------- | ------ | -------- | -----
@id            | string | Tak      | Adres URL, który liścia rejestracji
catalogEntry   | object | Tak      | Wpis katalogu zawierającego metadane pakietów
packageContent | string | Tak      | Adres URL do zawartości pakietów (.nupkg)

Każdy obiekt typu liść rejestracji reprezentuje dane związane z wersją pojedynczy pakiet.

#### <a name="catalog-entry"></a>Wpis katalogu

`catalogEntry` Właściwości w obiekcie typu liść rejestracji ma następujące właściwości:

Nazwa                     | Typ                       | Wymagane | Uwagi
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | Tak      | Adres URL do dokumentu, używany do utworzenia tego obiektu
Autorzy                  | ciąg lub tablica ciągów | Brak       | 
dependencyGroups         | Tablica obiektów           | Brak       | Adres URL do zawartości pakietów (.nupkg)
opis              | string                     | Brak       | 
iconUrl                  | string                     | Brak       | 
identyfikator                       | string                     | Tak      | Identyfikator pakietu
licenseUrl               | string                     | Brak       | 
wymienione                   | wartość logiczna                    | Brak       | Należy traktować jak wymienionych w przypadku braku
Element MinClientVersion         | string                     | Brak       | 
adresem projectUrl               | string                     | Brak       | 
Opublikowane                | string                     | Brak       | Ciąg zawierający ISO 8601 sygnatura czasowa kiedy został opublikowany pakiet
RequireLicenseAcceptance | wartość logiczna                    | Brak       | 
podsumowanie                  | string                     | Brak       | 
tagi                     | ciąg lub tablica ciągów  | Brak       | 
Tytuł                    | string                     | Brak       | 
version                  | string                     | Tak      | Wersja pakietu

`dependencyGroups` Właściwość jest Tablica obiektów reprezentująca zależności pakietu, pogrupowane według platformy docelowej. Jeśli pakiet nie ma żadnych zależności `dependencyGroups` właściwości brakuje pustą tablicę lub `dependencies` właściwości wszystkich grup jest pusty lub Brak.

#### <a name="package-dependency-group"></a>Grupa zależności pakietu

Każdy obiekt grupy zależności ma następujące właściwości:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
targetFramework | string           | Brak       | Docelowe środowisko, które dotyczą te zależności
zależności    | Tablica obiektów | Brak       |

`targetFramework` Ciąg w formacie zaimplementowana przez bibliotekę .NET NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Jeśli nie `targetFramework` określono grupy zależności dotyczy wszystkich platform docelowych.

`dependencies` Właściwość jest Tablica obiektów, reprezentujący zależności pakietu bieżącego pakietu.

#### <a name="package-dependency"></a>Zależność pakietu

Poszczególne zależności pakietu ma następujące właściwości:

Nazwa         | Typ   | Wymagane | Uwagi
------------ | ------ | -------- | -----
identyfikator           | string | Tak      | Identyfikator zależności pakietu
range        | object | Brak       | Dozwolona [zakres wersji](../reference/package-versioning.md#version-ranges-and-wildcards) zależności
rejestracja | string | Brak       | Adres URL do indeksu rejestracji tej zależności

Jeśli `range` właściwości jest wyłączona lub pusty ciąg, klient powinien domyślny zakres wersji `(, )`. Oznacza to, że dowolna wersja zależność jest dozwolone.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź 

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

W tym przypadku indeks rejestracji ma wbudowane strony rejestracji, więc nie są wymagane żadne dodatkowe żądania można pobrać metadanych dotyczących wersje poszczególnych pakietów.

## <a name="registration-page"></a>Strony rejestracji

Strony rejestracji zawiera pozostawia rejestracji. Adres URL, aby pobrać strony rejestracji jest określany przez `@id` właściwości w [obiekt strony rejestracji](#registration-page-object) wymienionych powyżej.

Gdy `items` tablicy nie jest dostępny w indeksie rejestracyjnych, żądanie HTTP GET z `@id` wartość, którą będzie zwracać dokumentu JSON, który ma obiekt jako elementem głównym. Obiekt ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | Tak      | Adres URL do strony rejestracji
count  | integer          | Tak      | Numer rejestracji pozostawia na stronie
Elementy  | Tablica obiektów | Tak      | Tablica rejestracji pozostawia i ich Skojarz metadanych
Niższe  | string           | Tak      | Najniższa wersja programu SemVer 2.0.0 na stronie (włącznie)
Nadrzędny | string           | Tak      | Adres URL do indeksu rejestracji
górny  | string           | Tak      | Najwyższa wersja programu SemVer 2.0.0 na stronie (włącznie)

Kształt obiektów typu liść rejestracji jest taki sam jak indeks rejestracji [powyżej](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json
```

## <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Liścia rejestracji

Liścia rejestracji zawiera informacje o określonym identyfikatorze i wersji. Metadane dotyczące określonej wersji nie mogą być dostępne w tym dokumencie. Metadane pakietów mają być pobierane z [indeksu rejestracji](#registration-index) lub [strony rejestracji](#registration-page) (który został odnaleziony przy użyciu indeksu rejestracji).

Adres URL, aby pobrać liścia rejestracji są uzyskiwane z `@id` właściwości obiektu typu liść rejestracji w indeksie rejestracyjnych lub strony rejestracji.

Liścia rejestracji jest dokumentem JSON z obiektem głównym z następującymi właściwościami:

Nazwa           | Typ    | Wymagane | Uwagi
-------------- | ------- | -------- | -----
@id            | string  | Tak      | Adres URL, który liścia rejestracji
catalogEntry   | string  | Brak       | Adres URL do wpisu wykazu wytworzonego te liścia
wymienione         | wartość logiczna | Brak       | Należy traktować jak wymienionych w przypadku braku
packageContent | string  | Brak       | Adres URL do zawartości pakietów (.nupkg)
Opublikowane      | string  | Brak       | Ciąg zawierający ISO 8601 sygnatura czasowa kiedy został opublikowany pakiet
rejestracja   | string  | Brak       | Adres URL do indeksu rejestracji

> [!Note]
> Na nuget.org `published` ma wartość roku 1900, gdy pakiet jest nieznajdujące się na liście.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
