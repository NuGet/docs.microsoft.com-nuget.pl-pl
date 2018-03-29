---
title: Katalog, API NuGet w wersji 3 | Dokumentacja firmy Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Katalog jest indeks wszystkich pakietów utworzony i usunięty w nuget.org.
keywords: Interfejsu API w wersji 3 NuGet katalogu, nuget.org dziennika transakcji, replikacji nuget.org nuget.org klonowania tylko Dołącz rekord nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ed502eee498f5ad0a014e3338503f2855396a5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="catalog"></a>Katalogu

**Katalogu** jest zasobem, który rejestruje wszystkie operacje pakietu w źródle pakietu, takich jak tworzenie i usuwanie. Zasób katalogu ma `Catalog` wpisz [indeksu usługi](service-index.md).

> [!Note]
> Ponieważ katalog nie jest używany przez klienta NuGet oficjalnego, nie wszystkie źródła pakietów implementuje katalogu.

> [!Note]
> Wykaz nuget.org nie jest obecnie dostępna w Chinach. Aby uzyskać więcej informacji, zobacz [NuGet/NuGetGallery#4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` jest używana wartość:

@type Wartość   | Uwagi
------------- | -----
Catalog/3.0.0 | Początkowa wersja

## <a name="base-url"></a>Podstawowy adres URL

Adres URL punktu wejścia dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartości. W tym temacie korzysta z adresu URL symbolu zastępczego `{@id}`.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL w obsługę katalogu zasobów znaleziono tylko metod HTTP `GET` i `HEAD`.

## <a name="catalog-index"></a>Indeks katalogu

Indeks katalogu jest dokumentu w dobrze znanej lokalizacji, która zawiera listę elementów katalogu, uporządkowanych w porządku chronologicznym. Jest punkt wejścia do zasobu katalogu.

Indeks składa się z katalogu stron. Każda strona katalogu zawiera elementy katalogu. Każdy element katalogu reprezentuje zdarzenia dotyczące pojedynczego pakietu w punkcie w czasie. Element katalogu może reprezentować pakietu, który został utworzony, nieznajdujące się na liście, ponownie wystawiony lub usunięty ze źródła pakietu. Przetwarzanie elementy katalogu w kolejności chronologicznej, klient można tworzyć aktualny widok każdy pakiet, który istnieje w źródle pakietów w wersji 3.

Krótko mówiąc obiekty BLOB katalogu ma następującą strukturę hierarchiczną:

- **Indeks**: punkt wejścia dla katalogu.
- **Strona**: grupowanie elementów katalogu.
- **Liścia**: dokument reprezentujący element katalogu, który jest migawką stanu pojedynczy pakiet.

Każdy obiekt katalogu ma właściwość o nazwie `commitTimeStamp` reprezentujący, gdy element został dodany do katalogu. Elementy katalogu są dodawane do strony katalogu w partiach o nazwie zatwierdzeń. Wszystkie elementy katalogu w tej samej zatwierdzania mieć tą samą sygnaturą czasową zatwierdzania (`commitTimeStamp`) i zatwierdź identyfikator (`commitId`). Elementy katalogu umieszczone w tej samej zatwierdzania reprezentują zdarzenia, które wystąpiły w okolicy tego samego punktu w czasie w źródle pakietu. Nie ma żadnych kolejności w ramach zatwierdzania katalogu.

Ponieważ każdy identyfikator pakietu i wersję jest unikatowa, nigdy nie będzie więcej niż jeden element katalogu na zatwierdzenie. Daje to pewność, że elementy katalogu w jednym pakiecie zawsze można jednoznacznie uporządkowana względem sygnatury czasowej zatwierdzania.

Jest nigdy nie będzie więcej niż jednego zatwierdzenia w katalogu na `commitTimeStamp`. Innymi słowy `commitId` jest nadmiarowy z `commitTimeStamp`.

Contrast do [pakietu zasobów metadanych](registration-base-url-resource.md), który jest indeksowany przez identyfikator pakietu, katalog jest indeksowany (oraz umożliwia zadawanie zapytań) jedynie przez czas.

Elementy katalogu są zawsze dodawane do katalogu w kolejności rosnącej monotonicznie, chronologicznym. Oznacza to, że jeśli zatwierdzenia katalogu zostanie dodany w czasie X następnie zatwierdzenia katalogu, nie będą dodawane czasu mniejsze niż lub równa X.

Następujące żądania pobiera indeks katalogu.

    GET {@id}

Indeks katalogu jest dokumentem JSON, który zawiera obiekt z następującymi właściwościami:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
commitId        | string           | Tak      | Unikatowy identyfikator skojarzony z ostatniego zatwierdzenia
commitTimeStamp | string           | Tak      | Sygnatura czasowa ostatniego zatwierdzenia
count           | integer          | Tak      | Liczba stron w indeksie
Elementy           | Tablica obiektów | Tak      | Tablica obiektów, każdy obiekt reprezentujący stronę

Każdy element `items` tablicy jest obiektem o niektórych minimalnego szczegółowe informacje dotyczące każdej strony. Te obiekty strony nie zawierają pozostawia katalogu (elementów). Nie zdefiniowano kolejność elementów w tej macierzy. Strony może zostać określona przez klienta w pamięci przy użyciu ich `commitTimeStamp` właściwości.

Ponieważ wprowadzane są nowe strony, `count` będą zwiększane i nowe obiekty będą wyświetlane w `items` tablicy.

Gdy elementy są dodawane do katalogu, indeks `commitId` ulegnie zmianie i `commitTimeStamp` wzrośnie. Te dwie właściwości są zasadniczo podsumowanie przez wszystkie strony `commitId` i `commitTimeStamp` wartości w `items` tablicy.

### <a name="catalog-page-object-in-the-index"></a>Obiekt strony katalogu w indeksie

Obiekty strony katalogu znalezione w indeksie katalogu `items` właściwość ma następujące właściwości:

Nazwa            | Typ    | Wymagane | Uwagi
--------------- | ------- | -------- | -----
@id             | string  | Tak      | Adres URL pobierania katalogu strony
commitId        | string  | Tak      | Unikatowy identyfikator skojarzony z ostatniego zatwierdzenia na tej stronie
commitTimeStamp | string  | Tak      | Sygnatura czasowa ostatniego zatwierdzenia na tej stronie
count           | integer | Tak      | Liczba elementów na stronie katalogu

Contrast do [pakietu zasobów metadanych](registration-base-url-resource.md) co w niektórych przypadkach inlines pozostawia do indeksu, pozostawia katalogu nigdy nie są wbudowane w indeksie i zawsze musi zostać pobrana korzystając ze strony `@id` adresu URL.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Strona katalogu

Strona katalogu jest kolekcja elementów katalogu. Jest to dokument pobrane przy użyciu jednej z `@id` wartości znalezione w indeksie katalogu. Adres URL strony katalogu nie jest przeznaczona do przewidywalną i powinny zostać wykryte przy użyciu tylko indeksu katalogu.

Nowe elementy katalogu są dodawane do strony indeksu katalogu tylko z najwyższą znacznik czasu zatwierdzenia lub do nowej strony. Po dodaniu strony z sygnaturą czasową wyższej zatwierdzania do katalogu starsze strony nigdy nie są dodawane do lub zmienione.

Dokument strony wykazu jest obiekt JSON z następującymi właściwościami:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
commitId        | string           | Tak      | Unikatowy identyfikator skojarzony z ostatniego zatwierdzenia na tej stronie
commitTimeStamp | string           | Tak      | Sygnatura czasowa ostatniego zatwierdzenia na tej stronie
count           | integer          | Tak      | Liczba elementów na stronie
Elementy           | Tablica obiektów | Tak      | Elementy katalogu na tej stronie
Nadrzędny          | string           | Tak      | Adres URL do indeksu katalogu

Każdy element `items` tablica jest obiekt z niektórych minimalnego szczegółowe informacje o elemencie katalogu. Te obiekty elementu nie zawierają wszystkie dane elementu katalogu. Kolejność elementów na stronie `items` tablicy nie jest zdefiniowany. Elementy może zostać określona przez klienta w pamięci przy użyciu ich `commitTimeStamp` właściwości.

Liczba elementów katalogu, na stronie zdefiniowano przez implementację serwera. Dla nuget.org ma co najwyżej 550 elementów w każdej stronie, mimo że rzeczywista liczba może być mniejsza dla niektórych stron, zależnie od wielkości następną partię zatwierdzania w punkcie w czasie.

Ponieważ wprowadzane są nowe elementy, `count` jest zwiększany i nowego katalogu elementu obiekty są wyświetlane w `items` tablicy.

Po dodaniu elementu na stronie `commitId` zmiany i `commitTimeStamp` zwiększa. Te dwie właściwości są zasadniczo podsumowanie w odniesieniu do wszystkich `commitId` i `commitTimeStamp` wartości w `items` tablicy.

### <a name="catalog-item-object-in-a-page"></a>Obiekt elementu na stronie katalogu

Obiekty elementu katalogu znaleźć na stronie katalogu `items` właściwość ma następujące właściwości:

Nazwa            | Typ    | Wymagane | Uwagi
--------------- | ------- | -------- | -----
@id             | string  | Tak      | Adres URL, aby pobrać element katalogu
@type           | string  | Tak      | Typ elementu katalogu
commitId        | string  | Tak      | Identyfikator zatwierdzenia skojarzone z tym elementem katalogu
commitTimeStamp | string  | Tak      | Sygnatura czasowa zatwierdzania tego elementu katalogu
nuget:ID        | string  | Tak      | Identyfikator pakietu powiązanej z tym liścia
nuget:Version   | string  | Tak      | Wersja pakietu powiązanej z tym liścia

`@type` Wartość będzie jedną z następujących dwóch wartości:

1. `nuget:PackageDetails`: odpowiada `PackageDetails` typu w katalogu dokumentu typu liść.
1. `nuget:PackageDelete`: odpowiada `PackageDelete` typu w katalogu dokumentu typu liść.

Aby uzyskać więcej informacji o oznacza każdy typ, zobacz [odpowiadającego elementów typu](#item-types) poniżej.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Liścia katalogu

Liścia katalogu zawiera metadanych o identyfikatorze określonego pakietu i wersja w pewnym momencie w czasie. Jest to dokument pobierane przy użyciu `@id` wartość znajduje się na stronie katalogu. Adres URL, który liścia katalogu nie jest przeznaczona do przewidywalną i powinny zostać wykryte przy użyciu strony katalogu.

Dokument liścia katalogu jest obiekt JSON z następującymi właściwościami:

Nazwa                    | Typ                       | Wymagane | Uwagi
----------------------- | -------------------------- | -------- | -----
@type                   | ciąg lub tablica ciągów | Tak      | Typy elementów katalogu
katalog: commitId        | string                     | Tak      | Identyfikator zatwierdzenia skojarzone z tym elementem katalogu
catalog:commitTimeStamp | string                     | Tak      | Sygnatura czasowa zatwierdzania tego elementu katalogu
identyfikator                      | string                     | Tak      | Identyfikator pakietu element katalogu
Opublikowane               | string                     | Tak      | Data opublikowania elementu katalogu pakietu
version                 | string                     | Tak      | Wersja pakietu elementu katalogu

### <a name="item-types"></a>Typy elementów

`@type` Właściwość jest string lub tablicy ciągów. Dla wygody Jeśli `@type` wartość jest ciągiem, powinny być traktowane jako tablicy o rozmiarze jeden. Nie wszystkie możliwe wartości `@type` są udokumentowane. Jednak każdy element katalogu ma dokładnie jeden z dwóch poniższych wartości typu ciągu:

1. `PackageDetails`: reprezentuje migawkę metadane pakietów
1. `PackageDelete`: reprezentuje pakiet, który został usunięty

### <a name="package-details-catalog-items"></a>Informacje szczegółowe dotyczące pakietu w katalogu elementów

Elementy typu katalogu `PackageDetails` zawierającego migawkę metadane pakietów dla określonego pakietu (identyfikator i wersja połączenie). Elementu katalogu szczegóły pakietu jest generowany, gdy źródło pakietu napotka żadnego z następujących scenariuszy:

1. Pakiet jest **wypchniętych**.
1. Pakiet jest **wymienione**.
1. Pakiet jest **nieznajdujące się na liście**.
1. Pakiet jest **dopasowywany**.

Pakiet ze zmianą ułożenia jest administracyjne gestu zasadniczo generujący fałszywy wypychania istniejącego pakietu bez zmian do samego pakietu. Na nuget.org ze zmianą ułożenia jest używany po usunięciu błędu w jednym z zadań w tle, które zużywają katalogu.

Aby określić, które z tych scenariuszy wyprodukowane element katalogu nie powinny podejmować klientów korzystających z elementów katalogu. Zamiast tego należy po prostu aktualizację klienta zapewnienia widoku ani indeksu z metadanymi zawarte w elemencie katalogu. Ponadto elementy katalogu zduplikowany lub nadmiarowy obsługi bezpiecznie (idempotently).

Elementy katalogu szczegóły pakietu mieć następujące właściwości oprócz tych [włączone wszystkie pozostawia katalogu](#catalog-leaf).

Nazwa                    | Typ                       | Wymagane | Uwagi
----------------------- | -------------------------- | -------- | -----
Autorzy                 | string                     | Brak       |
Utworzone                 | string                     | Tak      | Sygnatura czasowa najpierw utworzenia pakietu
dependencyGroups        | Tablica obiektów           | Brak       | Takie same w formacie [pakietu zasobów metadanych](registration-base-url-resource.md#package-dependency-group)
opis             | string                     | Brak       |
iconUrl                 | string                     | Brak       |
isPrerelease            | wartość logiczna                    | Tak      | Określa, czy jest wstępna wersja pakietu
język                | string                     | Brak       |
licenseUrl              | string                     | Brak       |
wymienione                  | wartość logiczna                    | Brak       | Określa, czy pakiet zostanie wyświetlony
Element MinClientVersion        | string                     | Brak       |
packageHash             | string                     | Tak      | Skrót pakietu, kodowanie przy użyciu [standardowe base 64.](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | Tak      |
packageSize             | integer                    | Tak      | Rozmiar .nupkg pakietu w bajtach
projectUrl              | string                     | Brak       |
releaseNotes            | string                     | Brak       |
requireLicenseAgreement | wartość logiczna                    | Brak       | Załóżmy `false` Jeśli wyłączone
podsumowanie                 | string                     | Brak       |
tagi                    | Tablica ciągów           | Brak       |
Tytuł                   | string                     | Brak       |
verbatimVersion         | string                     | Brak       | Ciąg wersji, ponieważ pierwotnie został znaleziony w .nuspec

Pakiet `version` właściwość jest ciągiem znormalizowane pełnej wersji. Oznacza to, że dane kompilacji programu SemVer 2.0.0 można uwzględnić w tym miejscu.

`created` Jest sygnatury czasowej, gdy pakiet został najpierw odbierany przez źródło pakietu, w którym jest zwykle przez krótki czas przed sygnatury czasowej zatwierdzania element katalogu.

`packageHashAlgorithm` Jest zdefiniowany przez implementację serwera reprezentujący algorytmu wyznaczania wartości skrótu używany w celu utworzenia `packageHash`. zawsze używana usługa nuget.org `packageHashAlgorithm` wartość `SHA512`.

`published` Sygnatury czasowej to czas, kiedy pakiet został wymieniony ostatnio.

> [!Note]
> Na nuget.org `published` ma wartość roku 1900, gdy pakiet jest nieznajdujące się na liście.

#### <a name="sample-request"></a>Przykładowe żądanie

POBIERZ https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Elementy katalogu usuwania pakietu

Elementy typu katalogu `PackageDelete` zawierać minimalny zestaw informacje wskazujące klientom katalogu, że pakiet został usunięty ze źródła pakietu i nie jest już dostępny do żadnej operacji pakietu (na przykład przywracanie).

> [!Note]
> Istnieje możliwość pakiet do usunięcia i później ponownie opublikować za pomocą tego samego identyfikator pakietu i wersję. Na nuget.org jest to bardzo rzadko przypadek, ponieważ przerywa oficjalnego klienta założenie, że identyfikator pakietu i wersję implikują zawartości określonego pakietu. Aby uzyskać więcej informacji na temat usuwania pakietu na nuget.org zobacz [naszymi zasadami](../policies/deleting-packages.md).

Elementy katalogu usuwania pakietu mają nie dodatkowych właściwości [włączone wszystkie pozostawia katalogu](#catalog-leaf).

`version` Właściwość jest oryginalny ciąg wersji w .nuspec pakietu.

`published` Właściwość jest czas, gdy pakiet został usunięty, jest zazwyczaj jako krótki czas przed sygnatury czasowej zatwierdzania element katalogu.

#### <a name="sample-request"></a>Przykładowe żądanie

POBIERZ https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Kursor

### <a name="overview"></a>Omówienie

W tej sekcji opisano pojęcia klienta, który, chociaż nie jest zawsze wymagany przez protokół, powinna być częścią katalogu praktyczne implementacji klienta.

Ponieważ katalog jest struktura danych tylko do dołączania indeksowane według czasu, przez klienta należy przechowywać **kursora** lokalnie, reprezentujący maksymalnie co punktu w czasie klient został przetworzony elementów katalogu. Należy pamiętać, że ta wartość kursora powinny być generowane nigdy nie, za pomocą zegara komputera klienta. Zamiast tego wartość powinna pochodzić z obiektu katalogu `commitTimestamp` wartość.

Za każdym razem, gdy klient chce przetwarzać nowych zdarzeń w źródle pakietu, musi zapytania katalogu dla wszystkich elementów katalogu z sygnaturą czasową zatwierdzania większa niż jego przechowywanych kursora. Po klient pomyślnie przetwarza wszystkie nowe elementy katalogu, rejestruje najnowsze sygnatury czasowej zatwierdzania elementów katalogu, po prostu przetwarzane jako jego nowa wartość kursora.

W ten sposób klient może być się, że nigdy nie pominąć wszelkie zdarzenia pakietu, które wystąpiły w źródle pakietu.
Ponadto klient nigdy ponownie przetworzyć starych zdarzeń przed sygnatury czasowej zarejestrowane zatwierdzania kursora.

Zaawansowane koncepcji kursory jest używany dla wielu zadań w tle nuget.org i służy do aktualności interfejsu API w wersji 3, sama. 

### <a name="initial-value"></a>Wartość początkowa

Gdy klient katalogu jest uruchamiana po raz pierwszy (i w związku z tym nie ma wartości kursora), korzystała domyślną wartość kursora. W sieci `System.DateTimeOffset.MinValue` lub takie analogiczne pojęcie minimalnej można przedstawić sygnatury czasowej.

### <a name="iterating-over-catalog-items"></a>Iterowanie po elementów katalogu

Dla następnego zestawu elementów katalogu do przetwarzania kwerendy, klient powinien:

1. Pobierz wartość kursora zarejestrowane z lokalnego magazynu.
1. Pobierz i deserializacji indeks katalogu.
1. Znajdź wszystkie strony z sygnaturą czasową zatwierdzania w katalogu *większe* kursora.
1. Deklarowanie pustej listy elementów katalogu, do przetworzenia.
1. Dla każdej strony katalogu dopasowywane w kroku 3:
   1. Pobierz i zdeserializować strona katalogu.
   1. Znajdź wszystkie elementy z sygnaturą czasową zatwierdzenia katalogu *większe* kursora.
   1. Dodaj wszystkie zgodne elementy katalogu, do listy zadeklarowany w kroku 4.
1. Aby posortować listę elementów katalogu, zatwierdzania sygnatury czasowej.
1. Proces każdego elementu katalogu w kolejności:
   1. Pobierz i deserializować element katalogu.
   1. Odpowiednio zareagować na typ elementów katalogu.
   1. Proces dokumentu elementów katalogu w sposób specyficzne dla klienta.
1. Zarejestruj sygnatury czasowej zatwierdzania ostatniego elementu katalogu jako nową wartość kursora.

Z tego algorytmu podstawowe implementacja klienta można tworzyć kompletne widoku wszystkich pakietów dostępne w źródle pakietu. Klienta należy wykonywać tylko ten algorytm okresowo, aby zawsze należy pamiętać o najnowsze zmiany do źródła pakietu.

> [!Note]
> To jest algorytm używa tego nuget.org do zachowania [metadane pakietów](registration-base-url-resource.md), [zawartość pakietu](package-base-address-resource.md), [wyszukiwania](search-query-service-resource.md) i [autouzupełniania](search-autocomplete-service-resource.md) zasoby na bieżąco.

### <a name="dependent-cursors"></a>Kursory zależne

Załóżmy, że istnieją dwa klientów katalogu mający związanego z używaniem zależności, których danych wyjściowych jednego klienta zależy od innego klienta w danych wyjściowych. 

#### <a name="example"></a>Przykład

Na przykład na nuget.org nowo opublikowanego pakietu nie mogą występować w zasobie wyszukiwania zanim pojawi się w zasobie metadanych pakietu. Jest to spowodowane "Przywracanie" wykonywanych przez oficjalnego klienta NuGet korzysta z pakietu zasobu metadanych. Jeśli klient wykryje pakietu przy użyciu usługi wyszukiwania, należy go pomyślnie przywrócić tego pakietu przy użyciu pakietu zasobu metadanych. Innymi słowy zasobów wyszukiwania zależy od zasobu metadanych pakietu. Każdy zasób ma katalogu zadania tła klienta aktualizacji tego zasobu. Każdy klient ma własną kursora.

Ponieważ oba zasoby są tworzone wylogowuje katalogu kursora klienta katalogu, który aktualizuje zasób wyszukiwania *musi wykracza poza* kursora klienta katalogu metadanych pakietu.

#### <a name="algorithm"></a>Algorytm

Aby zaimplementować to ograniczenie, po prostu zmodyfikuj powyżej, aby być algorytmu:

1. Pobierz wartość kursora zarejestrowane z lokalnego magazynu.
1. Pobierz i deserializacji indeks katalogu.
1. Znajdź wszystkie strony z sygnaturą czasową zatwierdzania w katalogu *większe* kursor **co najwyżej zależności kursora.**
1. Deklarowanie pustej listy elementów katalogu, do przetworzenia.
1. Dla każdej strony katalogu dopasowywane w kroku 3:
   1. Pobierz i zdeserializować strona katalogu.
   1. Znajdź wszystkie elementy z sygnaturą czasową zatwierdzenia katalogu *większe* kursor **co najwyżej zależności kursora.**
   1. Dodaj wszystkie zgodne elementy katalogu, do listy zadeklarowany w kroku 4.
1. Aby posortować listę elementów katalogu, zatwierdzania sygnatury czasowej.
1. Proces każdego elementu katalogu w kolejności:
   1. Pobierz i deserializować element katalogu.
   1. Odpowiednio zareagować na typ elementów katalogu.
   1. Proces dokumentu elementów katalogu w sposób specyficzne dla klienta.
1. Zarejestruj sygnatury czasowej zatwierdzania ostatniego elementu katalogu jako nową wartość kursora.

Przy użyciu tego algorytmu zmodyfikowane, można utworzyć systemu klientów zależnych katalogu wszystkich tworzenie własnych określonymi indeksami, artefakty itd.
