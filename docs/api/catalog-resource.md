---
title: Zasób katalogu, NuGet w wersji 3 interfejsu API
description: Katalog jest indeks wszystkie pakiety utworzone i usunięte w witrynie nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 4884de71151ee1ae3c0a78b803c9222f9c1d86ec
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266361"
---
# <a name="catalog"></a>Wykaz

**Katalogu** jest zasobem, który rejestruje wszystkie operacje pakietu w źródle pakietu, takie jak operacje tworzenia i usuwania. Zasób katalogu ma `Catalog` wpisać [indeks usług](service-index.md). Można użyć tego zasobu do [zapytania dla wszystkie opublikowane pakiety](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Ponieważ katalog nie jest używany przez oficjalne klienta programu NuGet, nie wszystkie źródła pakietów zaimplementować katalogu.

> [!Note]
> Wykaz nuget.org nie jest obecnie dostępna w Chinach. Aby uzyskać więcej informacji, zobacz [NuGet/NuGetGallery#4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` zostanie użyta wartość:

@type Wartość   | Uwagi
------------- | -----
Catalog/3.0.0 | Wersja początkowa

## <a name="base-url"></a>Podstawowy adres URL

Adres URL punktu wejścia dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartości. W tym temacie używany zastępczego adresu URL `{@id}`.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL w obsługę zasobów katalogu znaleziono tylko metody HTTP `GET` i `HEAD`.

## <a name="catalog-index"></a>Indeks katalogu

Indeks wykazu jest dokument w lokalizacji dobrze znanego, która zawiera listę elementów katalogu, uporządkowanych w porządku chronologicznym. Jest punkt wejścia do zasobu katalogu.

Indeks składa się z strony katalogu. Każda strona katalogu zawiera elementy katalogu. Każdy element katalogu przedstawia zdarzenie dotyczące pojedynczego pakietu w punkcie w czasie. Element katalogu może reprezentować pakiet, który został utworzony, nieznajdujące się na liście, ponownie wystawiony lub został usunięty ze źródła pakietu. Przez przetwarzanie elementów katalogu, w kolejności chronologicznej, klienta można tworzyć aktualny widok każdego pakietu, który istnieje w źródle pakietu V3.

Krótko mówiąc obiekty BLOB katalogu mają następującą strukturę hierarchiczną:

- **Indeks**: punkt wejścia dla katalogu.
- **Strona**: grupowanie elementów katalogu.
- **Liścia**: dokument reprezentujący element katalogu, który jest migawką stanu w jednym pakiecie.

Każdy obiekt katalogu ma właściwość o nazwie `commitTimeStamp` reprezentujący, gdy element została dodana do wykazu. Elementy katalogu są dodawane do strony katalogu w partiach, nazywanych zatwierdzeniami. Wszystkie elementy katalogu, w tym samym zatwierdzeniu mają tą samą sygnaturą czasową zatwierdzenia (`commitTimeStamp`) i identyfikator zatwierdzenia (`commitId`). Elementy katalogu, umieszczane w tym samym zatwierdzeniu reprezentują zdarzenia, które wystąpiły w okolicy tego samego punktu w czasie w źródle pakietu. Nie ma żadnych kolejności w ramach zatwierdzenia katalogu.

Ponieważ każdy identyfikator pakietu i wersję jest unikatowy, nigdy nie będzie więcej niż jeden element katalogu na zatwierdzenie. Daje to gwarancję, że elementy katalogu w jednym pakiecie zawsze może jednoznacznie uporządkowane względem sygnatury czasowej zatwierdzenia.

Istnieje już nigdy nie będzie więcej niż jednego zatwierdzenia do katalogu na `commitTimeStamp`. Innymi słowy `commitId` jest nadmiarowa z `commitTimeStamp`.

W przeciwieństwie do [zasób metadanych pakietu](registration-base-url-resource.md), która jest indeksowana przez identyfikator pakietu, katalog jest indeksowane (i obsługą zapytań) tylko przez czas.

Elementy katalogu są zawsze dodawane do katalogu, w kolejności rosnącej monotonicznie, chronologicznym. Oznacza to, że jeśli zatwierdzenie wykazu jest dodawana w czasie X następnie Brak zatwierdzeń katalogu będą dodawane z czasem mniejszą lub równą X.

Następujące żądanie pobiera indeks katalogu.

    GET {@id}

Indeks katalogu jest dokumentem JSON, który zawiera obiekt z następującymi właściwościami:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
commitId        | string           | tak      | Unikatowy identyfikator skojarzony z ostatnie zatwierdzenie
commitTimeStamp | string           | tak      | Sygnatura czasowa najnowsze zatwierdzenia
count           | integer          | tak      | Liczba stron w indeksie
items           | Tablica obiektów | tak      | Tablica obiektów, każdy obiekt reprezentujący stronę

Każdy element w `items` tablica jest obiekt z niektóre minimalne szczegółowe informacje o każdej strony. Obiekty te strony nie zawierają pozostawia katalogu (elementy). Nie zdefiniowano kolejność elementów w tej tablicy. Strony może zostać określona przez klienta w pamięci przy użyciu ich `commitTimeStamp` właściwości.

Wprowadzoną nowych stron `count` jest zwiększany i nowe obiekty będą wyświetlane w `items` tablicy.

Po dodaniu elementu do wykazu, indeks `commitId` ulegnie zmianie i `commitTimeStamp` więc ceny wzrosną. Te dwie właściwości są zasadniczo podsumowania na stronie wszystkie `commitId` i `commitTimeStamp` wartości w `items` tablicy.

### <a name="catalog-page-object-in-the-index"></a>Obiekt strony katalogu w indeksie

Obiekty strony katalogu znalezione w indeksie katalogu `items` właściwości mają następujące właściwości:

Nazwa            | Typ    | Wymagane | Uwagi
--------------- | ------- | -------- | -----
@id             | string  | tak      | Adres URL do strony katalogu pobierania
commitId        | string  | tak      | Unikatowy identyfikator skojarzony z najnowsze zatwierdzenie na tej stronie
commitTimeStamp | string  | tak      | Sygnaturę czasową najnowsze zatwierdzenie na tej stronie
count           | integer | tak      | Liczba elementów na stronie katalogu

W przeciwieństwie do [zasób metadanych pakietu](registration-base-url-resource.md) co w niektórych przypadkach inlines pozostawia do indeksu, pozostawia katalogu nigdy nie jest wbudowana w indeksie i zawsze musi zostać pobrana przy użyciu strony `@id` adresu URL.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Strona katalogu

Na stronie katalog to kolekcja elementów katalogu. Jest to dokument pobrana przy użyciu jednej z `@id` znaleziono wartości w indeksie katalogu. Adres URL do strony katalogu nie ma być przewidywalny i powinny zostać wykryte przy użyciu tylko katalog indeksu.

Nowe elementy katalogu są dodawane do strony indeksu katalogu tylko z najwyższą sygnatura czasowa zatwierdzenia lub do nowej strony. Po dodaniu strony z wyższym sygnaturą czasową zatwierdzenia do wykazu starsze strony nigdy nie są dodawane do lub zmienione.

Dokument strony katalogu jest obiekt JSON z następującymi właściwościami:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
commitId        | string           | tak      | Unikatowy identyfikator skojarzony z najnowsze zatwierdzenie na tej stronie
commitTimeStamp | string           | tak      | Sygnaturę czasową najnowsze zatwierdzenie na tej stronie
count           | integer          | tak      | Liczba elementów na stronie
items           | Tablica obiektów | tak      | Elementy katalogu na tej stronie
Nadrzędny          | string           | tak      | Adres URL do indeksu katalogu

Każdy element w `items` tablica jest obiekt z niektóre minimalne szczegółowe informacje o elemencie katalogu. Te obiekty elementu nie zawierają wszystkie dane elementu katalogu. Kolejność elementów na stronie `items` tablicy nie jest zdefiniowany. Elementy może zostać określona przez klienta w pamięci przy użyciu ich `commitTimeStamp` właściwości.

Liczba elementów katalogu, na stronie jest definiowany przez implementację serwera. Dla nuget.org istnieją co najwyżej 550 elementów na każdej stronie, mimo że rzeczywista liczba może być mniejszy dla niektórych stron, w zależności od rozmiaru następna partia zatwierdzenia w punkcie, w czasie.

Ponieważ nowe elementy zostały wprowadzone, `count` jest zwiększona i nowy wykaz elementów obiekty są wyświetlane w `items` tablicy.

Po dodaniu elementu do strony, `commitId` zmiany i `commitTimeStamp` zwiększa się. Te dwie właściwości są zasadniczo podsumowanie wszystkich `commitId` i `commitTimeStamp` wartości w `items` tablicy.

### <a name="catalog-item-object-in-a-page"></a>Obiekt elementu na stronie sieci w katalogu

Obiekty elementów katalogu znaleźć na stronie katalogu `items` właściwości mają następujące właściwości:

Nazwa            | Typ    | Wymagane | Uwagi
--------------- | ------- | -------- | -----
@id             | string  | tak      | Adres URL, aby pobrać element katalogu
@type           | string  | tak      | Typ elementu katalogu
commitId        | string  | tak      | Identyfikator zatwierdzenia skojarzone z tym elementem katalogu
commitTimeStamp | string  | tak      | Sygnatura czasowa zatwierdzenia tego elementu katalogu
nuget:ID        | string  | tak      | Identyfikator pakietu, który dotyczy tego typu liść
nuget:Version   | string  | tak      | Wersja pakietu, który dotyczy tego typu liść

`@type` Wartość będzie jedną z następujących dwóch wartości:

1. `nuget:PackageDetails`: odpowiada to `PackageDetails` typu w dokumencie liścia katalogu.
1. `nuget:PackageDelete`: odpowiada to `PackageDelete` typu w dokumencie liścia katalogu.

Aby uzyskać więcej informacji o oznacza każdy typ, zobacz [odpowiadające elementy typu](#item-types) poniżej.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Wykaz liścia

Liścia wykazu zawiera metadane dotyczące określonego pakietu, identyfikator i wersja w pewnym momencie w czasie. Jest to dokument pobierane przy użyciu `@id` wartość znaleźć na stronie katalogu. Adres URL na liść katalogu nie ma być przewidywalny i powinny zostać wykryte przy użyciu tylko katalog strony.

Dokument liścia wykazu jest obiekt JSON z następującymi właściwościami:

Nazwa                    | Typ                       | Wymagane | Uwagi
----------------------- | -------------------------- | -------- | -----
@type                   | ciąg lub tablicę ciągów | tak      | Typy elementu katalogu
catalog:commitId        | string                     | tak      | Identyfikator zatwierdzenia skojarzone z tym elementem katalogu
catalog:commitTimeStamp | string                     | tak      | Sygnatura czasowa zatwierdzenia tego elementu katalogu
identyfikator                      | string                     | tak      | Identyfikator pakietu element katalogu
Opublikowane               | string                     | tak      | Data opublikowania elementu katalogu pakietu
version                 | string                     | tak      | Wersja pakietu element katalogu

### <a name="item-types"></a>Typy elementów

`@type` Właściwość jest ciąg lub tablicę ciągów. Dla wygody Jeśli `@type` wartość jest ciągiem, powinny być traktowane jako tablica dowolnego rozmiaru, jeden. Nie wszystkie możliwe wartości `@type` są udokumentowane. Jednak każdy element katalogu ma dokładnie jeden z dwóch następujących wartości typu ciąg:

1. `PackageDetails`: reprezentuje migawkę metadane pakietu
1. `PackageDelete`: reprezentuje pakiet, który został usunięty

### <a name="package-details-catalog-items"></a>Elementy katalogu szczegóły pakietu

Elementy z typem katalogu `PackageDetails` zawierają migawkę metadane pakietu dla określonego pakietu (identyfikator i wersja połączenia). Element katalogu szczegóły pakietu jest generowana, gdy źródło pakietu wystąpi dowolne z następujących scenariuszy:

1. Pakiet jest **wypchnięcie**.
1. Pakiet jest **wymienione**.
1. Pakiet jest **nieznajdujące się na liście**.
1. Pakiet jest **dopasowywany**.

Pakiet ze zmianą ułożenia jest administracyjne gestu, zasadniczo generujący fałszywych synchronizowaniu istniejącego pakietu, bez konieczności wprowadzania zmian do samego pakietu. W witrynie nuget.org ze zmianą ułożenia jest używany po naprawieniu błędu w jednym z zadań w tle, które zużywają katalogu.

Klientom korzystanie z elementów katalogu, nie należy próbować ustalić, który z tych scenariuszy wyprodukowany element katalogu. Zamiast tego klienta należy po prostu zaktualizuj ani utrzymywane w dobrym stanie widoku indeksu przy użyciu metadanych zawartych w elemencie katalogu. Ponadto elementy katalogu zduplikowane lub nadmiarowe z niepoprawnymi bez problemu zmieniała (idempotently).

Elementy katalogu szczegóły pakietu mają następujące właściwości oprócz tych [uwzględnione na wszystkich pozostawia katalogu](#catalog-leaf).

Nazwa                    | Typ                       | Wymagane | Uwagi
----------------------- | -------------------------- | -------- | -----
Autorzy                 | string                     | Brak       |
Utworzone                 | string                     | Brak       | Sygnatura czasowa systemu, gdy pakiet został utworzony po raz pierwszy. Właściwości rezerwowego: `published`.
dependencyGroups        | Tablica obiektów           | Brak       | Takiego samego formatu jak [zasób metadanych pakietu](registration-base-url-resource.md#package-dependency-group)
opis             | string                     | Brak       |
iconUrl                 | string                     | Brak       |
isPrerelease            | wartość logiczna                    | Brak       | Określa, czy wersja pakietu jest wstępna. Może zostać wykryte z `version`.
język                | string                     | Brak       |
licenseUrl              | string                     | Brak       |
wymienione                  | wartość logiczna                    | Brak       | Określa, czy pakiet zostanie wyświetlony
Atrybut MinClientVersion        | string                     | Brak       |
packageHash             | string                     | tak      | Skrót pakietu, kodowanie za pomocą [standardowa base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | tak      |
packageSize             | integer                    | tak      | Rozmiar .nupkg pakietu w bajtach
projectUrl              | string                     | Brak       |
releaseNotes            | string                     | Brak       |
requireLicenseAgreement | wartość logiczna                    | Brak       | Załóżmy `false` Jeśli wykluczone
podsumowanie                 | string                     | Brak       |
tagi                    | Tablica ciągów           | Brak       |
tytuł                   | string                     | Brak       |
verbatimVersion         | string                     | Brak       | Ciąg wersji, ponieważ pierwotnie został znaleziony w .nuspec

Pakiet `version` właściwości jest ciągiem pełnej wersji po normalizacji. Oznacza to, że dane kompilacji SemVer 2.0.0 można uwzględnić w tym miejscu.

`created` Sygnatura czasowa jest pakiet najpierw zostało odebrane przez źródło pakietu, który jest zazwyczaj przez krótki czas przed elementami katalogu zatwierdzenia z sygnaturą czasową.

`packageHashAlgorithm` Jest ciągiem, który został zdefiniowany przez implementację serwera reprezentujący algorytmu wyznaczania wartości skrótu, użyta do wyprodukowania `packageHash`. zawsze używane w witrynie nuget.org `packageHashAlgorithm` wartość `SHA512`.

`published` Sygnatura czasowa jest czas, gdy pakiet został wymieniony ostatnio.

> [!Note]
> W witrynie nuget.org `published` ma wartość roku 1900, gdy pakiet jest nieobecne na liście.

#### <a name="sample-request"></a>Przykładowe żądanie

POBIERZ https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Elementy katalogu usuwania pakietów

Elementy z typem katalogu `PackageDelete` zawierać minimalny zestaw informacji wskazujących klientom katalogu, że pakiet został usunięty ze źródła pakietu i nie jest już dostępna w kontekście operacji pakietu (np. przywracanie).

> [!Note]
> Istnieje możliwość pakietu do usunięcia i później ponownie opublikować przy użyciu tego samego Identyfikatora pakietu i wersję. W witrynie nuget.org jest to bardzo rzadkich przypadkach, ponieważ powoduje przerwanie oficjalne klienta założenie, że identyfikator pakietu i wersję implikują zawartości określonego pakietu. Aby uzyskać więcej informacji na temat usuwania pakietów w witrynie nuget.org, zobacz [nasze zasady](../policies/deleting-packages.md).

Elementy katalogu usuwania pakietu mają żadne dodatkowe właściwości, oprócz tych [uwzględnione na wszystkich pozostawia katalogu](#catalog-leaf).

`version` Właściwość jest oryginalny ciąg wersji w .nuspec pakietu.

`published` Właściwość jest czas, gdy pakiet został usunięty, jest zazwyczaj krótki czas przed elementami katalogu zatwierdzenia z sygnaturą czasową.

#### <a name="sample-request"></a>Przykładowe żądanie

POBIERZ https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Kursor

### <a name="overview"></a>Omówienie

W tej sekcji opisano pojęcia klienta, który, chociaż nie jest zawsze wymagany przez protokół, powinien należeć implementacji klienta praktyczne katalogu.

Ponieważ katalog jest strukturą danych tylko do dołączania indeksowane według czasu, klienta należy przechowywać **kursora** lokalnie, nawet w jakim punkcie czasu klienta został przetworzony elementów katalogu. Należy pamiętać o tym, czy ta wartość kursora powinny nigdy nie są generowane przy użyciu zegar komputera klienta. Zamiast tego wartość powinny pochodzić z obiekt wykazu `commitTimestamp` wartość.

Za każdym razem, gdy klient chce przetwarzać nowych zdarzeń w źródle pakietu, musi on zapytania katalogu dla wszystkich elementów wykazu z sygnaturą czasową zatwierdzenia większa niż jego przechowywanej kursora. Po klient pomyślnie przetwarza wszystkie nowe elementy katalogu, rejestruje najnowszą sygnaturę czasową zatwierdzania elementów katalogu, po prostu są przetwarzane jako jego nowej wartości kursora.

W ten sposób klient mieć pewność, że nigdy nie przegap wszelkie zdarzenia pakietu, które wystąpiły w źródle pakietu.
Ponadto klient nigdy nie ma ponownie przetworzyć starych zdarzeń przed sygnatura czasowa zarejestrowane zatwierdzenia znajduje się kursor.

Zaawansowanych koncepcji kursory jest używany dla wielu zadań w tle nuget.org i jest używana w celu zapewnienia aktualności sam interfejs API w wersji 3. 

### <a name="initial-value"></a>Wartość początkowa

Gdy klient wykazu jest uruchamiana po raz pierwszy (i w związku z tym nie ma wartości kursora), powinna korzystać domyślną wartość kursora. NET firmy `System.DateTimeOffset.MinValue` lub takie analogiczne pojęcie minimalnych stałego sygnatury czasowej.

### <a name="iterating-over-catalog-items"></a>Iterowanie po elementów katalogu

Aby wyszukać kolejny zbiór elementów katalogu do przetwarzania, klient powinien:

1. Pobierz wartość zarejestrowane kursora z lokalnego magazynu.
1. Pobierz i deserializować indeks katalogu.
1. Znajdź wszystkie strony z sygnaturą czasową zatwierdzenia z katalogu *większa* kursora.
1. Deklarować pustej listy elementów katalogu do przetworzenia.
1. Dla każdej strony katalogu dopasowywane w kroku 3:
   1. Pobierz i zdeserializować strony katalogu.
   1. Znajdź wszystkie elementy z sygnaturą czasową zatwierdzenia katalogu *większa* kursora.
   1. Dodaj wszystkie zgodne elementy katalogu, do listy zadeklarowane w kroku 4.
1. Sortowanie listy elementów katalogu według sygnatur czasowych zatwierdzenia.
1. Proces każdego elementu katalogu, w kolejności:
   1. Pobierz i wykonać deserializacji elementu katalogu.
   1. Reagować odpowiednio do typu elementu wykazu.
   1. Proces dokumentu elementów katalogu w sposób specyficzne dla klienta.
1. Zapisz znacznik czasu: ostatni element katalogu zatwierdzenia jako nową wartość kursora.

Z tego podstawowego algorytmu implementacji klienta mogą kumulować się pełny przegląd wszystkich pakietów dostępny w źródle pakietu. Klienta należy wykonywać tylko ten algorytm okresowo, aby zawsze pamiętaj o najnowsze zmiany do źródła pakietu.

> [!Note]
> Jest to algorytm korzysta z tego repozytorium nuget.org zapewnienie [metadane pakietów](registration-base-url-resource.md), [zawartość pakietu](package-base-address-resource.md), [wyszukiwania](search-query-service-resource.md) i [autouzupełniania](search-autocomplete-service-resource.md) zasoby na bieżąco.

### <a name="dependent-cursors"></a>Kursory zależne

Załóżmy, że istnieją dwóch klientów katalogu, które mają zależności związane, w których danych wyjściowych jednego klienta zależy od innego klienta w danych wyjściowych. 

#### <a name="example"></a>Przykład

Na przykład w witrynie nuget.org nowo opublikowany pakiet nie powinny być wyświetlane w zasobie wyszukiwania przed wyświetleniem zasób metadanych pakietu. Jest to spowodowane "Przywracanie" wykonywane przez oficjalne klienta programu NuGet korzysta z zasobów metadanych pakietu. Jeśli klient wykryje pakiet przy użyciu usługi search, należy można pomyślnie przywrócić tego pakietu przy użyciu zasób metadanych pakietu. Innymi słowy zasobów wyszukiwania zależy od zasobu metadanych pakietu. Każdy zasób ma wykazu klienta zadania w tle aktualizacji tego zasobu. Każdy klient ma swój własny kursora.

Ponieważ oba zasoby są tworzone zniżki w stosunku do katalogu, kursor klienta katalogu, który aktualizuje zasób wyszukiwania *musi wykracza poza* kursora klienta wykazu metadanych pakietu.

#### <a name="algorithm"></a>Algorytm

Aby zaimplementować to ograniczenie, po prostu zmodyfikuj powyżej, aby być algorytmu:

1. Pobierz wartość zarejestrowane kursora z lokalnego magazynu.
1. Pobierz i deserializować indeks katalogu.
1. Znajdź wszystkie strony z sygnaturą czasową zatwierdzenia z katalogu *większa* kursor **mniejsze niż lub równe kursora zależności.**
1. Deklarować pustej listy elementów katalogu do przetworzenia.
1. Dla każdej strony katalogu dopasowywane w kroku 3:
   1. Pobierz i zdeserializować strony katalogu.
   1. Znajdź wszystkie elementy z sygnaturą czasową zatwierdzenia katalogu *większa* kursor **mniejsze niż lub równe kursora zależności.**
   1. Dodaj wszystkie zgodne elementy katalogu, do listy zadeklarowane w kroku 4.
1. Sortowanie listy elementów katalogu według sygnatur czasowych zatwierdzenia.
1. Proces każdego elementu katalogu, w kolejności:
   1. Pobierz i wykonać deserializacji elementu katalogu.
   1. Reagować odpowiednio do typu elementu wykazu.
   1. Proces dokumentu elementów katalogu w sposób specyficzne dla klienta.
1. Zapisz znacznik czasu: ostatni element katalogu zatwierdzenia jako nową wartość kursora.

Przy użyciu tego algorytmu zmodyfikowane, możesz tworzyć system klientów zależnych wykaz wszystkich tworzenie własnych określonych indeksów, artefakty, itp.
