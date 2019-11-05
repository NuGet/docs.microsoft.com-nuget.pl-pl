---
title: Metadane pakietu, interfejs API NuGet
description: Podstawowy adres URL rejestracji pakietu umożliwia pobieranie metadanych o pakietach.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: e98e8d1258377818b3852762d317750a6b3e59ad
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611033"
---
# <a name="package-metadata"></a>Metadane pakietu

Możliwe jest pobranie metadanych o pakietach dostępnych w źródle pakietów przy użyciu interfejsu API programu NuGet v3. Te metadane można pobrać przy użyciu zasobu `RegistrationsBaseUrl` znalezionego w [indeksie usługi](service-index.md).

Kolekcja dokumentów znalezionych w obszarze `RegistrationsBaseUrl` jest często nazywana "rejestracjami" lub "Rejestracja obiektów BLOB". Zestaw dokumentów w ramach jednego `RegistrationsBaseUrl` jest określany jako "gałąź rejestracji". Gałąź rejestracji zawiera wszystkie metadane dotyczące każdego pakietu dostępnego w źródle pakietu.

## <a name="versioning"></a>Przechowywanie wersji

Następujące wartości `@type` są używane:

wartość @type                     | Uwagi
------------------------------- | -----
RegistrationsBaseUrl            | Początkowa wersja
RegistrationsBaseUrl/3.0.0 — beta | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-RC   | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Odpowiedzi formacie gzip
RegistrationsBaseUrl/3.6.0      | Obejmuje pakiety 2.0.0 SemVer

Reprezentuje to trzy odrębne gałęzie rejestracji dostępne dla różnych wersji klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Te rejestracje nie są skompresowane (oznacza to, że używają one `Content-Encoding: identity`implikowane). Pakiety 2.0.0 SemVer są **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Te rejestracje są kompresowane przy użyciu `Content-Encoding: gzip`. Pakiety 2.0.0 SemVer są **wykluczone** z tej gałęzi.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Te rejestracje są kompresowane przy użyciu `Content-Encoding: gzip`. Pakiety 2.0.0 SemVer są **zawarte** w tym elemencie Hive.
Aby uzyskać więcej informacji na temat SemVer 2.0.0, zobacz [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API to wartość właściwości `@id` skojarzona z wymienionymi wyżej wartościami `@type` zasobów. W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego adresu URL `{@id}`.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL Znalezione w zasobie rejestracji obsługują metody HTTP `GET` i `HEAD`.

## <a name="registration-index"></a>Indeks rejestracji

Metadane pakietu grup zasobów rejestracji według identyfikatora pakietu. Nie jest możliwe pobieranie danych o więcej niż jednym IDENTYFIKATORze pakietu jednocześnie. Ten zasób nie umożliwia odnajdywania identyfikatorów pakietów. Zamiast tego zakłada się, że klient ma już znać żądany identyfikator pakietu. Dostępne metadane dotyczące poszczególnych wersji pakietu różnią się w zależności od implementacji serwera. Obiekty blob rejestracji pakietu mają następującą strukturę hierarchiczną:

- **Index**: punkt wejścia dla metadanych pakietu, współużytkowany przez wszystkie pakiety w źródle o takim samym identyfikatorze.
- **Strona**: grupowanie wersji pakietu. Liczba wersji pakietu na stronie jest definiowana przez implementację serwera.
- **Liść**: dokument specyficzny dla jednej wersji pakietu.

Adres URL indeksu rejestracji jest przewidywalny i może być określony przez klienta z IDENTYFIKATORem pakietu i wartością `@id` zasobu rejestracji z indeksu usługi. Adresy URL stron rejestracji i liści są odnajdywane przez sprawdzenie indeksu rejestracji.

### <a name="registration-pages-and-leaves"></a>Strony rejestracji i opuszczenia

Chociaż nie jest to wymagane w przypadku implementacji serwera do przechowywania liści rejestracji w oddzielnych dokumentach stron rejestracji, zaleca się zapełnienie pamięci po stronie klienta. Zamiast wykreślania wszystkich liści rejestracji w indeksie lub natychmiastowego przechowywania pozostawianych w dokumentach na stronach zaleca się, aby implementacja serwera mogła wybrać jedną z dwóch metod na podstawie liczby wersji pakietu lub łączny rozmiar liści pakietów.

Przechowywanie wszystkich wersji pakietu (liście) w indeksie rejestracji oszczędza liczbę żądań HTTP wymaganych do pobrania metadanych pakietu, ale oznacza, że większy dokument musi być pobrany i należy przydzielać więcej pamięci klienta. Z drugiej strony, jeśli implementacja serwera natychmiast przechowuje rejestrację w oddzielnych dokumentach stron, klient musi wykonać więcej żądań HTTP w celu uzyskania potrzebnych informacji.

Algorytm heurystyczny, którego używa nuget.org, jest następujący: w przypadku 128 lub większej liczby wersji pakietu, należy przerwać pozostawianie liści na stronach o rozmiarze 64. Jeśli jest mniej niż 128 wersji, wszystkie w tym indeksie zostaną pozostawione.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry żądania

Nazwa     | W     | Typ    | Wymagane | Uwagi
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adres URL    | string  | opcję      | Identyfikator pakietu, małe litery

Wartość `LOWER_ID` jest pożądanym IDENTYFIKATORem pakietu małymi literami przy użyciu reguł zaimplementowane przez. Metoda [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) sieci.

### <a name="response"></a>Reakcji

Odpowiedź jest dokumentem JSON, który ma obiekt główny o następujących właściwościach:

Nazwa  | Typ             | Wymagane | Uwagi
----- | ---------------- | -------- | -----
count | integer          | opcję      | Liczba stron rejestracji w indeksie
produktów | Tablica obiektów | opcję      | Tablica stron rejestracji

Każdy element w tablicy `items` obiektu indeksu jest obiektem JSON reprezentującym stronę rejestracji.

#### <a name="registration-page-object"></a>Obiekt strony rejestracji

Obiekt strony rejestracji znaleziony w indeksie rejestracji ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | opcję      | Adres URL strony rejestracji
count  | integer          | opcję      | Liczba liści rejestracji na stronie
produktów  | Tablica obiektów | znaleziono       | Tablica liści rejestracji i ich skojarzone metadane
Dołu  | string           | opcję      | Najniższa wersja SemVer 2.0.0 na stronie (włącznie)
nadrzędny | string           | znaleziono       | Adres URL indeksu rejestracji
prawym górnym  | string           | opcję      | Najwyższa wersja SemVer 2.0.0 na stronie (włącznie)

`lower` i `upper` granice obiektu strony są przydatne, gdy wymagana jest wartość metadanych określonej wersji strony.
Te ograniczenia mogą służyć do pobrania jedynej wymaganej strony rejestracji. Ciągi wersji są zgodne z [regułami wersji narzędzia NuGet](../concepts/package-versioning.md). Ciągi wersji są znormalizowane i nie zawierają metadanych kompilacji. Podobnie jak w przypadku wszystkich wersji ekosystemu NuGet porównanie ciągów wersji jest implementowane przy użyciu [reguł pierwszeństwa wersji SemVer 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11).

Właściwość `parent` zostanie wyświetlona tylko wtedy, gdy obiekt strony rejestracji ma właściwość `items`.

Jeśli właściwość `items` nie występuje w obiekcie strony rejestracji, adres URL określony w `@id` musi być używany do pobierania metadanych dotyczących poszczególnych wersji pakietu. Tablica `items` jest czasami wykluczona z obiektu Page jako Optymalizacja. Jeśli liczba wersji pojedynczego identyfikatora pakietu jest bardzo duża, dokument indeksu rejestracji będzie ogromny i wasteful do przetwarzania dla klienta, który dba o określoną wersję lub w niewielkim zakresie wersji.

Należy pamiętać, że jeśli właściwość `items` jest obecna, właściwość `@id` nie musi być użyta, ponieważ wszystkie dane strony znajdują się już w `items` właściwości.

Każdy element w tablicy `items` obiektu jest obiektem JSON reprezentującym liścia rejestracji i jest skojarzonymi metadanymi.

#### <a name="registration-leaf-object-in-a-page"></a>Obiekt liścia rejestracji na stronie

Obiekt liścia rejestracji znaleziony na stronie rejestracji ma następujące właściwości:

Nazwa           | Typ   | Wymagane | Uwagi
-------------- | ------ | -------- | -----
@id            | string | opcję      | Adres URL liścia rejestracji
catalogEntry   | object | opcję      | Wpis katalogu zawierający metadane pakietu
packageContent | string | opcję      | Adres URL zawartości pakietu (. nupkg)

Każdy obiekt liścia rejestracji reprezentuje dane skojarzone z pojedynczą wersją pakietu.

#### <a name="catalog-entry"></a>Wpis katalogu

Właściwość `catalogEntry` w obiekcie liścia rejestracji ma następujące właściwości:

Nazwa                     | Typ                       | Wymagane | Uwagi
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | opcję      | Adres URL dokumentu używany do tworzenia tego obiektu
Autorów                  | ciąg lub tablica ciągów | znaleziono       | 
dependencyGroups         | Tablica obiektów           | znaleziono       | Zależności pakietu pogrupowane według platformy docelowej
Amortyzacja              | object                     | znaleziono       | Wycofanie skojarzone z pakietem
opis              | string                     | znaleziono       | 
iconUrl                  | string                     | znaleziono       | 
identyfikator                       | string                     | opcję      | Identyfikator pakietu
licenseUrl               | string                     | znaleziono       |
licenseExpression        | string                     | znaleziono       | 
wymienione                   | wartość logiczna                    | znaleziono       | Powinien być uważany za wymieniony, jeśli nie istnieje
MinClientVersion         | string                     | znaleziono       | 
projectUrl               | string                     | znaleziono       | 
publikacj                | string                     | znaleziono       | Ciąg zawierający sygnaturę czasową ISO 8601, kiedy pakiet został opublikowany
requireLicenseAcceptance | wartość logiczna                    | znaleziono       | 
podsumowanie                  | string                     | znaleziono       | 
tagi                     | ciąg lub tablica ciągu  | znaleziono       | 
tytuły                    | string                     | znaleziono       | 
version                  | string                     | opcję      | Pełny ciąg wersji po normalizacji

Właściwość Package `version` jest pełnym ciągiem wersji po normalizacji. Oznacza to, że w tym miejscu można uwzględnić dane kompilacji SemVer 2.0.0.

Właściwość `dependencyGroups` jest tablicą obiektów reprezentujących zależności pakietu, pogrupowanych według platformy docelowej. Jeśli pakiet nie ma żadnych zależności, brak właściwości `dependencyGroups`, pusta tablica lub właściwość `dependencies` wszystkich grup jest pusta lub nie istnieje.

Wartość właściwości `licenseExpression` jest zgodna z [składnią wyrażenia licencji NuGet](https://docs.microsoft.com/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Grupa zależności pakietu

Każdy obiekt grupy zależności ma następujące właściwości:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
targetFramework | string           | znaleziono       | Platforma docelowa, do której mają zastosowanie te zależności
zależności    | Tablica obiektów | znaleziono       |

Ciąg `targetFramework` używa formatu zaimplementowane przez pakiet NuGet biblioteki platformy .NET dla programu NuGet [. platformy](https://www.nuget.org/packages/NuGet.Frameworks/). Jeśli żadna `targetFramework` nie zostanie określona, Grupa zależności będzie stosowana do wszystkich platform docelowych.

Właściwość `dependencies` jest tablicą obiektów, z których każdy reprezentuje zależność pakietu bieżącego pakietu.

#### <a name="package-dependency"></a>Zależność pakietu

Każda zależność pakietu ma następujące właściwości:

Nazwa         | Typ   | Wymagane | Uwagi
------------ | ------ | -------- | -----
identyfikator           | string | opcję      | Identyfikator zależności pakietu
range        | object | znaleziono       | Dozwolony [zakres wersji](../concepts/package-versioning.md#version-ranges-and-wildcards) zależności
rejestracja | string | znaleziono       | Adres URL indeksu rejestracji dla tej zależności

Jeśli właściwość `range` jest wykluczona lub pusty ciąg, klient powinien domyślnie mieć zakres wersji `(, )`. Oznacza to, że jest dozwolona jakakolwiek wersja zależności.

#### <a name="package-deprecation"></a>Przestarzałe pakiety

Każde wycofanie pakietu ma następujące właściwości:

Nazwa             | Typ             | Wymagane | Uwagi
---------------- | ---------------- | -------- | -----
powodów          | Tablica ciągów | opcję      | Przyczyny, dla których pakiet był przestarzały
— komunikat          | string           | znaleziono       | Dodatkowe szczegóły dotyczące tego wycofania
alternatePackage | object           | znaleziono       | Zależność pakietu, która powinna być używana zamiast tego

Właściwość `reasons` musi zawierać co najmniej jeden ciąg, a jedynie ciągi z następującej tabeli:

Przyczyna       | Opis             
------------ | -----------
Starsza wersja       | Pakiet nie jest już obsługiwany
CriticalBugs | Pakiet zawiera usterki, które nie są odpowiednie do użycia
Inne        | Pakiet jest przestarzały z powodu braku na tej liście

Jeśli właściwość `reasons` zawiera ciągi, które nie pochodzą z znanego zestawu, powinny być ignorowane. W ciągach nie jest rozróżniana wielkość liter, dlatego `legacy` powinna być traktowana tak samo jak `Legacy`. W tablicy nie ma ograniczeń kolejności, dlatego ciągi można rozmieścić w dowolnej kolejności. Ponadto, jeśli właściwość zawiera tylko ciągi, które nie pochodzą z znanego zestawu, powinien być traktowany tak, jakby zawierał tylko ciąg "Other".

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

W tym konkretnym przypadku indeks rejestracji ma zakreśloną stronę rejestracji, więc nie są potrzebne żadne dodatkowe żądania, aby pobrać metadane dotyczące poszczególnych wersji pakietu.

## <a name="registration-page"></a>Strona rejestracji

Strona Rejestracja zawiera wpisy rejestracji. Adres URL pobierania strony rejestracji jest określany przez właściwość `@id` w [obiekcie strony rejestracji](#registration-page-object) wymienionym powyżej.

Gdy w indeksie rejestracji nie podano tablicy `items`, żądanie HTTP GET wartości `@id` zwróci dokument JSON, który ma obiekt jako element główny. Obiekt ma następujące właściwości:

Nazwa   | Typ             | Wymagane | Uwagi
------ | ---------------- | -------- | -----
@id    | string           | opcję      | Adres URL strony rejestracji
count  | integer          | opcję      | Liczba liści rejestracji na stronie
produktów  | Tablica obiektów | opcję      | Tablica liści rejestracji i ich skojarzone metadane
Dołu  | string           | opcję      | Najniższa wersja SemVer 2.0.0 na stronie (włącznie)
nadrzędny | string           | opcję      | Adres URL indeksu rejestracji
prawym górnym  | string           | opcję      | Najwyższa wersja SemVer 2.0.0 na stronie (włącznie)

Kształt obiektów liścia rejestracji jest taki sam jak w [powyższym](#registration-leaf-object-in-a-page)indeksie rejestracji.

## <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Liść rejestracji

Liść rejestracji zawiera informacje o określonym IDENTYFIKATORze pakietu i jego wersji. Metadane dotyczące określonej wersji mogą być niedostępne w tym dokumencie. Metadane pakietu powinny być pobierane ze [indeksu rejestracji](#registration-index) lub [strony rejestracji](#registration-page) (wykryty przy użyciu indeksu rejestracji).

Adres URL służący do pobierania liścia rejestracji jest uzyskiwany z właściwości `@id` obiektu liścia rejestracji na stronie indeksu rejestracji lub rejestracji.

Liść rejestracji jest dokumentem JSON z obiektem głównym o następujących właściwościach:

Nazwa           | Typ    | Wymagane | Uwagi
-------------- | ------- | -------- | -----
@id            | string  | opcję      | Adres URL liścia rejestracji
catalogEntry   | string  | znaleziono       | Adres URL wpisu katalogu, który wygenerował ten liść
wymienione         | wartość logiczna | znaleziono       | Powinien być uważany za wymieniony, jeśli nie istnieje
packageContent | string  | znaleziono       | Adres URL zawartości pakietu (. nupkg)
publikacj      | string  | znaleziono       | Ciąg zawierający sygnaturę czasową ISO 8601, kiedy pakiet został opublikowany
rejestracja   | string  | znaleziono       | Adres URL indeksu rejestracji

> [!Note]
> W przypadku nuget.org wartość `published` jest ustawiana na Year 1900, gdy pakiet jest nieznajdujący się na liście.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
