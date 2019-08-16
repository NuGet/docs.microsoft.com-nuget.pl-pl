---
title: Metadane pakietu, interfejs API NuGet
description: Podstawowy adres URL rejestracji pakietu umożliwia pobieranie metadanych o pakietach.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488317"
---
# <a name="package-metadata"></a>Metadane pakietu

Możliwe jest pobranie metadanych o pakietach dostępnych w źródle pakietów przy użyciu interfejsu API programu NuGet v3. Te metadane można pobrać przy użyciu `RegistrationsBaseUrl` zasobu znalezionego w indeksie [usługi](service-index.md).

Kolekcja dokumentów znalezionych w obszarze `RegistrationsBaseUrl` jest często nazywana "rejestracjami" lub "Rejestracja obiektów BLOB". Zestaw dokumentów w ramach jednego `RegistrationsBaseUrl` elementu jest określany jako "gałąź rejestracji". Gałąź rejestracji zawiera wszystkie metadane dotyczące każdego pakietu dostępnego w źródle pakietu.

## <a name="versioning"></a>Przechowywanie wersji

Są używane `@type` następujące wartości:

@typewartościami                     | Uwagi
------------------------------- | -----
RegistrationsBaseUrl            | Początkowa wersja
RegistrationsBaseUrl/3.0.0-beta | Alias`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Odpowiedzi formacie gzip
RegistrationsBaseUrl/3.6.0      | Obejmuje pakiety 2.0.0 SemVer

Reprezentuje to trzy odrębne gałęzie rejestracji dostępne dla różnych wersji klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Te rejestracje nie są skompresowane (oznacza to, że używają one `Content-Encoding: identity`implikowane). Pakiety 2.0.0 SemVer są **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Te rejestracje są kompresowane przy `Content-Encoding: gzip`użyciu. Pakiety 2.0.0 SemVer są **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Te rejestracje są kompresowane przy `Content-Encoding: gzip`użyciu. Pakiety 2.0.0 SemVer są **zawarte** w tym elemencie Hive.
Aby uzyskać więcej informacji na temat SemVer 2.0.0, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API to wartość `@id` właściwości skojarzonej z wyżej wymienionymi wartościami zasobów. `@type` W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego `{@id}` adresu URL.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują `GET` metody `HEAD`http i.

## <a name="registration-index"></a>Indeks rejestracji

Metadane pakietu grup zasobów rejestracji według identyfikatora pakietu. Nie jest możliwe pobieranie danych o więcej niż jednym IDENTYFIKATORze pakietu jednocześnie. Ten zasób nie umożliwia odnajdywania identyfikatorów pakietów. Zamiast tego zakłada się, że klient ma już znać żądany identyfikator pakietu. Dostępne metadane dotyczące poszczególnych wersji pakietu różnią się w zależności od implementacji serwera. Obiekty blob rejestracji pakietu mają następującą strukturę hierarchiczną:

- **Index**: punkt wejścia dla metadanych pakietu, współużytkowany przez wszystkie pakiety w źródle o takim samym identyfikatorze.
- **Strona**: grupowanie wersji pakietu. Liczba wersji pakietu na stronie jest definiowana przez implementację serwera.
- **Liść**: dokument specyficzny dla jednej wersji pakietu.

Adres URL indeksu rejestracji jest przewidywalny i może być określony przez klienta z identyfikatorem pakietu i `@id` wartością zasobu rejestracji z indeksu usługi. Adresy URL stron rejestracji i liści są odnajdywane przez sprawdzenie indeksu rejestracji.

### <a name="registration-pages-and-leaves"></a>Strony rejestracji i opuszczenia

Chociaż nie jest to wymagane w przypadku implementacji serwera do przechowywania liści rejestracji w oddzielnych dokumentach stron rejestracji, zaleca się zapełnienie pamięci po stronie klienta. Zamiast wykreślania wszystkich liści rejestracji w indeksie lub natychmiastowego przechowywania pozostawianych w dokumentach na stronach zaleca się, aby implementacja serwera mogła wybrać jedną z dwóch metod na podstawie liczby wersji pakietu lub łączny rozmiar liści pakietów.

Przechowywanie wszystkich wersji pakietu (liście) w indeksie rejestracji oszczędza liczbę żądań HTTP wymaganych do pobrania metadanych pakietu, ale oznacza, że większy dokument musi być pobrany i należy przydzielać więcej pamięci klienta. Z drugiej strony, jeśli implementacja serwera natychmiast przechowuje rejestrację w oddzielnych dokumentach stron, klient musi wykonać więcej żądań HTTP w celu uzyskania potrzebnych informacji.

Algorytm heurystyczny, którego używa nuget.org, jest następujący: w przypadku 128 lub większej liczby wersji pakietu, należy przerwać pozostawianie liści na stronach o rozmiarze 64. Jeśli jest mniej niż 128 wersji, wszystkie w tym indeksie zostaną pozostawione.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry żądania

Nazwa     | W     | Typ    | Wymagane | Uwagi
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adres URL    | string  | tak      | Identyfikator pakietu, małe litery

`LOWER_ID` Wartość jest pożądanym identyfikatorem pakietu małymi literami przy użyciu reguł zaimplementowane przez. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda sieci.

### <a name="response"></a>Odpowiedź

Odpowiedź jest dokumentem JSON, który ma obiekt główny o następujących właściwościach:

Nazwa  | Typ             | Wymagane | Uwagi
----- | ---------------- | -------- | -----
count | integer          | tak      | Liczba stron rejestracji w indeksie
items | Tablica obiektów | tak      | Tablica stron rejestracji

Każdy element w `items` tablicy obiektu indeksu jest obiektem JSON reprezentującym stronę rejestracji.

#### <a name="registration-page-object"></a>Obiekt strony rejestracji

Obiekt strony rejestracji znaleziony w indeksie rejestracji ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | tak      | Adres URL strony rejestracji
count  | integer          | tak      | Liczba liści rejestracji na stronie
items  | Tablica obiektów | znaleziono       | Tablica liści rejestracji i ich skojarzone metadane
dołu  | string           | tak      | Najniższa wersja SemVer 2.0.0 na stronie (włącznie)
nadrzędny | string           | znaleziono       | Adres URL indeksu rejestracji
prawym górnym  | string           | tak      | Najwyższa wersja SemVer 2.0.0 na stronie (włącznie)

`lower` I`upper` granice obiektu strony są przydatne, gdy wymagana jest wartość metadanych określonej wersji strony.
Te ograniczenia mogą służyć do pobrania jedynej wymaganej strony rejestracji. Ciągi wersji są zgodne z [regułami wersji narzędzia NuGet](../concepts/package-versioning.md). Ciągi wersji są znormalizowane i nie zawierają metadanych kompilacji. Podobnie jak w przypadku wszystkich wersji ekosystemu NuGet porównanie ciągów wersji jest implementowane przy użyciu [reguł pierwszeństwa wersji SemVer 2.0.0](http://semver.org/spec/v2.0.0.html#spec-item-11).

Właściwość zostanie wyświetlona tylko wtedy, gdy obiekt strony rejestracji `items` ma właściwość. `parent`

Jeśli właściwość nie jest obecna w obiekcie strony rejestracji, adres URL określony `@id` w elemencie musi być używany do pobierania metadanych dotyczących poszczególnych wersji pakietu. `items` `items` Tablica jest czasami wykluczona z obiektu Page jako Optymalizacja. Jeśli liczba wersji pojedynczego identyfikatora pakietu jest bardzo duża, dokument indeksu rejestracji będzie ogromny i wasteful do przetwarzania dla klienta, który dba o określoną wersję lub w niewielkim zakresie wersji.

Należy pamiętać, że `items` Jeśli właściwość jest obecna `@id` , nie trzeba używać właściwości, ponieważ wszystkie dane strony są już wbudowane we `items` właściwości.

Każdy element w `items` tablicy obiektu strony jest obiektem JSON reprezentującym liścia rejestracji i jest skojarzonymi metadanymi.

#### <a name="registration-leaf-object-in-a-page"></a>Obiekt liścia rejestracji na stronie

Obiekt liścia rejestracji znaleziony na stronie rejestracji ma następujące właściwości:

Nazwa           | Typ   | Wymagane | Uwagi
-------------- | ------ | -------- | -----
@id            | string | tak      | Adres URL liścia rejestracji
catalogEntry   | object | tak      | Wpis katalogu zawierający metadane pakietu
packageContent | string | tak      | Adres URL zawartości pakietu (. nupkg)

Każdy obiekt liścia rejestracji reprezentuje dane skojarzone z pojedynczą wersją pakietu.

#### <a name="catalog-entry"></a>Wpis katalogu

`catalogEntry` Właściwość w obiekcie liścia rejestracji ma następujące właściwości:

Nazwa                     | Typ                       | Wymagane | Uwagi
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | tak      | Adres URL dokumentu używany do tworzenia tego obiektu
autorów                  | ciąg lub tablica ciągów | znaleziono       | 
dependencyGroups         | Tablica obiektów           | znaleziono       | Zależności pakietu pogrupowane według platformy docelowej
Amortyzacja              | object                     | znaleziono       | Wycofanie skojarzone z pakietem
opis              | string                     | znaleziono       | 
iconUrl                  | string                     | znaleziono       | 
identyfikator                       | string                     | tak      | Identyfikator pakietu
licenseUrl               | string                     | znaleziono       |
licenseExpression        | string                     | znaleziono       | 
wymienione                   | wartość logiczna                    | znaleziono       | Powinien być uważany za wymieniony, jeśli nie istnieje
minClientVersion         | string                     | znaleziono       | 
projectUrl               | string                     | znaleziono       | 
publikacj                | string                     | znaleziono       | Ciąg zawierający sygnaturę czasową ISO 8601, kiedy pakiet został opublikowany
requireLicenseAcceptance | wartość logiczna                    | znaleziono       | 
podsumowanie                  | string                     | znaleziono       | 
tagi                     | ciąg lub tablica ciągu  | znaleziono       | 
title                    | string                     | znaleziono       | 
version                  | string                     | tak      | Pełny ciąg wersji po normalizacji

Właściwość Package `version` jest pełnym ciągiem wersji po normalizacji. Oznacza to, że w tym miejscu można uwzględnić dane kompilacji SemVer 2.0.0.

`dependencyGroups` Właściwość jest tablicą obiektów reprezentujących zależności pakietu, pogrupowanych według platformy docelowej. Jeśli pakiet nie ma żadnych zależności, `dependencyGroups` brak właściwości, pusta tablica `dependencies` lub właściwość wszystkich grup jest pusta lub nie istnieje.

Wartość `licenseExpression` właściwości jest zgodna z [składnią wyrażenia licencji NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Grupa zależności pakietu

Każdy obiekt grupy zależności ma następujące właściwości:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
targetFramework | string           | znaleziono       | Platforma docelowa, do której mają zastosowanie te zależności
zależności    | Tablica obiektów | znaleziono       |

Ten `targetFramework` ciąg używa formatu zaimplementowanego przez pakiet NuGet biblioteki platformy .NET dla programu NuGet [. platformy](https://www.nuget.org/packages/NuGet.Frameworks/). Jeśli nie `targetFramework` zostanie określona, Grupa zależności ma zastosowanie do wszystkich platform docelowych.

`dependencies` Właściwość jest tablicą obiektów, z których każdy reprezentuje zależność pakietu bieżącego pakietu.

#### <a name="package-dependency"></a>Zależność pakietu

Każda zależność pakietu ma następujące właściwości:

Nazwa         | Typ   | Wymagane | Uwagi
------------ | ------ | -------- | -----
identyfikator           | string | tak      | Identyfikator zależności pakietu
range        | object | znaleziono       | Dozwolony [zakres wersji](../concepts/package-versioning.md#version-ranges-and-wildcards) zależności
rejestracja | string | znaleziono       | Adres URL indeksu rejestracji dla tej zależności

Jeśli właściwość jest wykluczona lub jest pustym ciągiem, klient powinien domyślnie mieć zakres `(, )`wersji. `range` Oznacza to, że jest dozwolona jakakolwiek wersja zależności.

#### <a name="package-deprecation"></a>Przestarzałe pakiety

Każde wycofanie pakietu ma następujące właściwości:

Nazwa             | Typ             | Wymagane | Uwagi
---------------- | ---------------- | -------- | -----
powodów          | Tablica ciągów | tak      | Przyczyny, dla których pakiet był przestarzały
— komunikat          | string           | znaleziono       | Dodatkowe szczegóły dotyczące tego wycofania
alternatePackage | object           | znaleziono       | Zależność pakietu, która powinna być używana zamiast tego

`reasons` Właściwość musi zawierać co najmniej jeden ciąg, a jedynie ciągi z następującej tabeli:

Przyczyna       | Opis             
------------ | -----------
Starsza wersja       | Pakiet nie jest już obsługiwany
CriticalBugs | Pakiet zawiera usterki, które nie są odpowiednie do użycia
Inne        | Pakiet jest przestarzały z powodu braku na tej liście

`reasons` Jeśli właściwość zawiera ciągi, które nie pochodzą z znanego zestawu, powinny być ignorowane. W ciągach nie jest rozróżniana wielkość liter `legacy` , dlatego powinna być traktowana `Legacy`tak samo jak. W tablicy nie ma ograniczeń kolejności, dlatego ciągi można rozmieścić w dowolnej kolejności. Ponadto, jeśli właściwość zawiera tylko ciągi, które nie pochodzą z znanego zestawu, powinien być traktowany tak, jakby zawierał tylko ciąg "Other".

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

W tym konkretnym przypadku indeks rejestracji ma zakreśloną stronę rejestracji, więc nie są potrzebne żadne dodatkowe żądania, aby pobrać metadane dotyczące poszczególnych wersji pakietu.

## <a name="registration-page"></a>Strona rejestracji

Strona Rejestracja zawiera wpisy rejestracji. Adres URL pobierania strony rejestracji jest określany na podstawie `@id` właściwości w [obiekcie strony rejestracji](#registration-page-object) wymienionym powyżej.

Gdy tablica nie zostanie podana w indeksie rejestracji, żądanie `@id` HTTP GET wartości zwróci dokument JSON, który ma obiekt jako element główny. `items` Obiekt ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | tak      | Adres URL strony rejestracji
count  | integer          | tak      | Liczba liści rejestracji na stronie
items  | Tablica obiektów | tak      | Tablica liści rejestracji i ich skojarzone metadane
dołu  | string           | tak      | Najniższa wersja SemVer 2.0.0 na stronie (włącznie)
nadrzędny | string           | tak      | Adres URL indeksu rejestracji
prawym górnym  | string           | tak      | Najwyższa wersja SemVer 2.0.0 na stronie (włącznie)

Kształt obiektów liścia rejestracji jest taki sam jak w powyższym indeksie [](#registration-leaf-object-in-a-page)rejestracji.

## <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Liść rejestracji

Liść rejestracji zawiera informacje o określonym IDENTYFIKATORze pakietu i jego wersji. Metadane dotyczące określonej wersji mogą być niedostępne w tym dokumencie. Metadane pakietu powinny być pobierane ze [indeksu rejestracji](#registration-index) lub [strony rejestracji](#registration-page) (wykryty przy użyciu indeksu rejestracji).

Adres URL służący do pobierania liścia rejestracji jest uzyskiwany z `@id` właściwości obiektu liścia rejestracji na stronie indeksu rejestracji lub rejestracji.

Liść rejestracji jest dokumentem JSON z obiektem głównym o następujących właściwościach:

Nazwa           | Typ    | Wymagane | Uwagi
-------------- | ------- | -------- | -----
@id            | string  | tak      | Adres URL liścia rejestracji
catalogEntry   | string  | znaleziono       | Adres URL wpisu katalogu, który wygenerował ten liść
wymienione         | wartość logiczna | znaleziono       | Powinien być uważany za wymieniony, jeśli nie istnieje
packageContent | string  | znaleziono       | Adres URL zawartości pakietu (. nupkg)
publikacj      | string  | znaleziono       | Ciąg zawierający sygnaturę czasową ISO 8601, kiedy pakiet został opublikowany
rejestracja   | string  | znaleziono       | Adres URL indeksu rejestracji

> [!Note]
> W przypadku NuGet.org `published` wartość jest ustawiana na Year 1900, gdy pakiet jest nieznajdujący się na liście.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
