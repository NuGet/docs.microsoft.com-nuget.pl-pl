---
title: Zasób katalogu, interfejs API programu NuGet v3
description: Katalog jest indeksem wszystkich pakietów utworzonych i usuniętych w nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 11485f583d6993919f6bb8acabcc87d9e4261975
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774153"
---
# <a name="catalog"></a>Wykaz

**Katalog** jest zasobem, który rejestruje wszystkie operacje pakietu w źródle pakietów, takie jak tworzenie i usuwanie. Zasób katalogu ma `Catalog` Typ w [indeksie usługi](service-index.md). Ten zasób służy do [wykonywania zapytań dotyczących wszystkich opublikowanych pakietów](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Ponieważ katalog nie jest używany przez oficjalnego klienta NuGet, nie wszystkie źródła pakietów implementują wykaz.

> [!Note]
> Obecnie katalog nuget.org nie jest dostępny w Chinach. Aby uzyskać więcej informacji, zobacz [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Przechowywanie wersji

`@type`Używana jest następująca wartość:

@type wartościami   | Uwagi
------------- | -----
Katalog/3.0.0 | Początkowa wersja

## <a name="base-url"></a>Podstawowy adres URL

Adres URL punktu wejścia dla następujących interfejsów API to wartość `@id` Właściwości skojarzonej z wyżej wymienionymi wartościami zasobów `@type` . W tym temacie jest stosowany symbol zastępczy URL `{@id}` .

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL znajdujące się w zasobów katalogu obsługują tylko metody HTTP `GET` i `HEAD` .

## <a name="catalog-index"></a>Indeks katalogu

Indeks wykazu jest dokumentem w dobrze znanej lokalizacji, która ma listę elementów katalogu uporządkowanych chronologicznie. Jest to punkt wejścia zasobu katalogu.

Indeks składa się ze stron wykazu. Każda Strona wykazu zawiera elementy katalogu. Każdy element katalogu reprezentuje zdarzenie dotyczące pojedynczego pakietu w danym momencie. Element katalogu może reprezentować pakiet, który został utworzony, niewyszczególniony, ponownie wystawiony lub usunięty ze źródła pakietu. Przez przetwarzanie elementów katalogu w kolejności chronologicznej klient może utworzyć aktualny widok każdego pakietu, który istnieje w źródle pakietów v3.

W skrócie obiekty blob wykazu mają następującą strukturę hierarchiczną:

- **Indeks**: punkt wejścia dla katalogu.
- **Strona**: grupowanie elementów katalogu.
- **Liść**: dokument reprezentujący element katalogu, który jest migawką stanu pojedynczego pakietu.

Każdy obiekt wykazu ma właściwość o nazwie `commitTimeStamp` reprezentującej, kiedy element został dodany do wykazu. Elementy katalogu są dodawane do strony wykazu w partiach o nazwie commits. Wszystkie elementy katalogu w tym samym zatwierdzeniu mają tę samą sygnaturę czasową zatwierdzenia ( `commitTimeStamp` ) i identyfikator zatwierdzenia ( `commitId` ). Elementy katalogu umieszczane w tym samym zatwierdzeniu reprezentują zdarzenia, które wystąpiły wokół tego samego punktu w czasie w źródle pakietu. Nie ma kolejności w zatwierdzeniu katalogu.

Ze względu na to, że każdy identyfikator pakietu i jego wersja są unikatowe, w zatwierdzeniu nigdy nie będzie więcej niż jeden element katalogu. Gwarantuje to, że elementy katalogu dla pojedynczego pakietu mogą być zawsze niejednoznaczne uporządkowane w odniesieniu do sygnatury czasowej zatwierdzenia.

Nie ma więcej niż jednego zatwierdzenia do wykazu na `commitTimeStamp` . Innymi słowy, `commitId` jest nadmiarowy za pomocą `commitTimeStamp` .

W przeciwieństwie do [zasobu metadanych pakietu](registration-base-url-resource.md), który jest INDEKSOWANY według identyfikatora pakietu, katalog jest indeksowany (i Queryable) tylko według czasu.

Elementy katalogu są zawsze dodawane do wykazu w monotonicznie rosnącej, chronologicznej kolejności. Oznacza to, że jeśli zostanie dodane zatwierdzenie katalogu w czasie X, żadne zatwierdzenie wykazu nie zostanie kiedykolwiek dodane o czasie mniejszym niż lub równym X.

Poniższe żądanie Pobiera indeks wykazu.

```
GET {@id}
```

Indeks wykazu jest dokumentem JSON zawierającym obiekt o następujących właściwościach:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
commitId        | ciąg           | tak      | Unikatowy identyfikator skojarzony z ostatnim zatwierdzeniem
commitTimeStamp | ciąg           | tak      | Sygnatura czasowa ostatniego zatwierdzenia
count           | liczba całkowita          | tak      | Liczba stron w indeksie
produktów           | Tablica obiektów | tak      | Tablica obiektów, każdy obiekt reprezentujący stronę

Każdy element w `items` tablicy jest obiektem z niektórymi minimalnymi szczegółami dotyczącymi każdej strony. Te obiekty strony nie zawierają liści wykazu (elementy). Kolejność elementów w tej tablicy nie jest zdefiniowana. Strony mogą być uporządkowane przez klienta w pamięci przy użyciu ich `commitTimeStamp` właściwości.

Po wprowadzeniu nowych stron `count` zostanie on zwiększony, a nowe obiekty pojawią się w `items` tablicy.

Po dodaniu elementów do wykazu indeks `commitId` zostanie zmieniony i `commitTimeStamp` zostanie zwiększony. Te dwie właściwości są zasadniczo podsumowaniem wszystkich stron `commitId` i `commitTimeStamp` wartości w `items` tablicy.

### <a name="catalog-page-object-in-the-index"></a>Obiekt strony katalogu w indeksie

Obiekty strony katalogu znalezione we właściwości indeksu wykazu `items` mają następujące właściwości:

Nazwa            | Typ    | Wymagane | Uwagi
--------------- | ------- | -------- | -----
@id             | ciąg  | tak      | Adres URL pobierania strony katalogu
commitId        | ciąg  | tak      | Unikatowy identyfikator skojarzony z ostatnim zatwierdzeniem na tej stronie
commitTimeStamp | ciąg  | tak      | Sygnatura czasowa ostatniego zatwierdzenia na tej stronie
count           | liczba całkowita | tak      | Liczba elementów na stronie katalogu

W przeciwieństwie do [zasobów metadanych pakietu](registration-base-url-resource.md) , które w niektórych przypadkach opuszczają indeks, liści wykazu nigdy nie są wbudowane w indeks i zawsze muszą być pobierane przy użyciu `@id` adresu URL strony.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Strona wykazu

Strona wykazu jest kolekcją elementów katalogu. Jest to dokument pobierany przy użyciu jednej z `@id` wartości znalezionych w indeksie wykazu. Adres URL strony wykazu nie może być przewidywalny i powinien zostać odnaleziony tylko przy użyciu indeksu wykazu.

Nowe elementy katalogu są dodawane do strony w indeksie katalogu tylko z najwyższym znacznikiem czasu zatwierdzania lub do nowej strony. Po dodaniu strony z wyższym znacznikiem czasu zatwierdzenia do wykazu starsze strony nigdy nie są dodawane do ani zmieniane.

Dokument strony wykazu jest obiektem JSON o następujących właściwościach:

Nazwa            | Typ             | Wymagane | Uwagi
--------------- | ---------------- | -------- | -----
commitId        | ciąg           | tak      | Unikatowy identyfikator skojarzony z ostatnim zatwierdzeniem na tej stronie
commitTimeStamp | ciąg           | tak      | Sygnatura czasowa ostatniego zatwierdzenia na tej stronie
count           | liczba całkowita          | tak      | Liczba elementów na stronie
produktów           | Tablica obiektów | tak      | Elementy katalogu na tej stronie
nadrzędny          | ciąg           | tak      | Adres URL indeksu katalogu

Każdy element w `items` tablicy jest obiektem z niektórymi minimalnymi szczegółami dotyczącymi elementu katalogu. Te obiekty elementów nie zawierają wszystkich danych elementu katalogu. Kolejność elementów w `items` tablicy strony nie jest zdefiniowana. Elementy mogą być uporządkowane przez klienta w pamięci przy użyciu ich `commitTimeStamp` właściwości.

Liczba elementów katalogu na stronie jest definiowana przez implementację serwera. W przypadku nuget.org na każdej stronie znajduje się maksymalnie 550 elementów, chociaż rzeczywista liczba może być mniejsza dla niektórych stron w zależności od rozmiaru następnej partii zatwierdzania w punkcie w czasie.

W miarę wprowadzania nowych elementów w `count` tablicy jest zwiększane i pojawiają się nowe obiekty elementów katalogu `items` .

Po dodaniu elementów na stronie `commitId` zmiany i `commitTimeStamp` zwiększenia. Te dwie właściwości są zasadniczo podsumowaniem wszystkich `commitId` i `commitTimeStamp` wartości w `items` tablicy.

### <a name="catalog-item-object-in-a-page"></a>Obiekt elementu katalogu na stronie

Obiekty elementów katalogu znalezione we właściwości strony wykazu `items` mają następujące właściwości:

Nazwa            | Typ    | Wymagane | Uwagi
--------------- | ------- | -------- | -----
@id             | ciąg  | tak      | Adres URL pobierania elementu katalogu
@type           | ciąg  | tak      | Typ elementu katalogu
commitId        | ciąg  | tak      | Identyfikator zatwierdzenia skojarzony z tym elementem katalogu
commitTimeStamp | ciąg  | tak      | Sygnatura czasowa zatwierdzeń tego elementu katalogu
Pakiet NuGet: Identyfikator        | ciąg  | tak      | Identyfikator pakietu, z którym powiązany jest ten liść
NuGet: wersja   | ciąg  | tak      | Wersja pakietu, z którą jest powiązany ten liść

`@type`Wartość będzie jedną z dwóch następujących wartości:

1. `nuget:PackageDetails`: odpowiada `PackageDetails` typu w dokumencie liścia katalogu.
1. `nuget:PackageDelete`: odpowiada `PackageDelete` typowi w dokumencie liścia katalogu.

Aby uzyskać więcej informacji na temat tego, co oznacza każdy typ, zobacz poniższe [elementy typu](#item-types) poniżej.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Liść katalogu

Liści wykazu zawiera metadane dotyczące określonego identyfikatora pakietu i wersji w pewnym momencie. Jest to dokument pobierany przy użyciu `@id` wartości znalezionej na stronie katalogu. Adres URL liścia wykazu nie może być przewidywalny i powinien zostać odnaleziony przy użyciu tylko strony katalogu.

Dokument liścia wykazu jest obiektem JSON o następujących właściwościach:

Nazwa                    | Typ                       | Wymagane | Uwagi
----------------------- | -------------------------- | -------- | -----
@type                   | ciąg lub tablica ciągów | tak      | Typy w elemencie katalogu
Katalog: commitId        | ciąg                     | tak      | Identyfikator zatwierdzenia skojarzony z tym elementem katalogu
Katalog: commitTimeStamp | ciąg                     | tak      | Sygnatura czasowa zatwierdzeń tego elementu katalogu
identyfikator                      | ciąg                     | tak      | Identyfikator pakietu elementu katalogu
publikacj               | ciąg                     | tak      | Data opublikowania elementu katalogu pakietów
Wersja                 | ciąg                     | tak      | Wersja pakietu elementu katalogu

### <a name="item-types"></a>Typy elementów

`@type`Właściwość jest ciągiem lub tablicą ciągów. Dla wygody, jeśli `@type` wartość jest ciągiem, powinna być traktowana jako tablica o rozmiarze jeden. Nie wszystkie możliwe wartości `@type` są udokumentowane. Jednak każdy element katalogu ma dokładnie jedną z dwóch następujących wartości typu String:

1. `PackageDetails`: reprezentuje migawkę metadanych pakietu
1. `PackageDelete`: reprezentuje pakiet, który został usunięty

### <a name="package-details-catalog-items"></a>Elementy katalogu szczegółów pakietu

Elementy katalogu z typem `PackageDetails` zawierają migawkę metadanych pakietu dla określonego pakietu (kombinacja identyfikatorów i wersji). Element katalogu szczegóły pakietu jest tworzony, gdy źródło pakietu napotka którykolwiek z następujących scenariuszy:

1. Pakiet jest **wypychany**.
1. Zostanie **wyświetlony** pakiet.
1. Pakiet nie znajduje się na **liście**.
1. Pakiet jest **przepływany** ponownie.

Ponowne przepływanie pakietu to gest administracyjny, który zasadniczo generuje fałszywe wypchnięcie istniejącego pakietu bez wprowadzania zmian w samym pakiecie. W przypadku nuget.org jest używany ponownie przepływ po naprawieniu błędu w jednym z zadań w tle, które wykorzystują wykaz.

Klienci korzystający z elementów wykazu nie powinni próbować ustalić, które z tych scenariuszy wygenerowały element katalogu. Zamiast tego klient powinien po prostu zaktualizować każdy obsługiwany widok lub indeks za pomocą metadanych zawartych w elemencie katalogu. Ponadto zduplikowane lub nadmiarowe elementy katalogu powinny być obsłużone bezpiecznie (idempotently).

Elementy katalogu szczegóły pakietu zawierają następujące właściwości oprócz tych [uwzględnionych we wszystkich liściach katalogu](#catalog-leaf).

Nazwa                    | Typ                       | Wymagane | Uwagi
----------------------- | -------------------------- | -------- | -----
autorów                 | ciąg                     | nie       |
utworzony                 | ciąg                     | nie       | Sygnatura czasowa pierwszego utworzenia pakietu. Właściwość rezerwowa: `published` .
dependencyGroups        | Tablica obiektów           | nie       | Zależności pakietu pogrupowane według platformy docelowej ([ten sam format, w którym znajduje się zasób metadanych pakietu](registration-base-url-resource.md#package-dependency-group))
Amortyzacja             | object                     | nie       | Zaniechano skojarzone z pakietem ([ten sam format, w którym znajduje się zasób metadanych pakietu](registration-base-url-resource.md#package-deprecation))
description (opis)             | ciąg                     | nie       |
iconUrl                 | ciąg                     | nie       |
isPrerelease            | boolean                    | nie       | Czy wersja pakietu jest w wersji wstępnej. Można wykryć z programu `version` .
language                | ciąg                     | nie       |
licenseUrl              | ciąg                     | nie       |
wymienione                  | boolean                    | nie       | Czy pakiet znajduje się na liście
minClientVersion        | ciąg                     | nie       |
packageHash             | ciąg                     | tak      | Skrót pakietu, kodowanie przy użyciu [standardowej bazowej 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | ciąg                     | tak      |
packageSize             | liczba całkowita                    | tak      | Rozmiar pakietu. NUPKG w bajtach
packageTypes            | Tablica obiektów           | nie       | Typy pakietów określone przez autora.
projectUrl              | ciąg                     | nie       |
releaseNotes            | ciąg                     | nie       |
requireLicenseAgreement | boolean                    | nie       | Przyjmij, `false` Jeśli wykluczone
Podsumowanie                 | ciąg                     | nie       |
tags                    | tablica ciągów           | nie       |
tytuł                   | ciąg                     | nie       |
verbatimVersion         | ciąg                     | nie       | Ciąg wersji, który został pierwotnie odnaleziony w. nuspec

Właściwość Package `version` jest pełnym ciągiem wersji po normalizacji. Oznacza to, że w tym miejscu można uwzględnić dane kompilacji SemVer 2.0.0.

`created`Sygnatura czasowa jest w momencie, gdy pakiet został po raz pierwszy odebrany przez źródło pakietu, czyli zwykle skracany przed upływem sygnatury czasowej zatwierdzania elementu katalogu.

`packageHashAlgorithm`Jest to ciąg zdefiniowany przez implementację serwera reprezentującą algorytm wyznaczania wartości skrótu używany do tworzenia `packageHash` . nuget.org zawsze używać `packageHashAlgorithm` wartości `SHA512` .

`packageTypes`Właściwość będzie obecna tylko wtedy, gdy typ pakietu został określony przez autora. Jeśli jest obecny, zawsze będzie mieć co najmniej jeden wpis (1). Każdy element w `packageTypes` tablicy jest obiektem JSON o następujących właściwościach:

Nazwa      | Typ    | Wymagane | Uwagi
--------- | ------- | -------- | -----
name      | ciąg  | tak      | Nazwa typu pakietu.
Wersja    | ciąg  | nie       | Wersja typu pakietu. Tylko wtedy, gdy autor jawnie określił wersję w nuspec.

`published`Sygnatura czasowa to godzina, o której pakiet był ostatnio wyświetlany.

> [!Note]
> W `published` przypadku NuGet.org wartość jest ustawiana na rok 1900, gdy pakiet zostanie wystawiony.

#### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Pakiet usuwania elementów katalogu

Elementy katalogu o typie `PackageDelete` zawierają minimalny zestaw informacji wskazujący klientom wykazu, że pakiet został usunięty ze źródła pakietu i nie jest już dostępny dla żadnej operacji pakietu (na przykład przywracania).

> [!NOTE]
> Istnieje możliwość usunięcia pakietu i jego późniejszej publikacji ponownie przy użyciu tego samego identyfikatora pakietu i wersji. W systemie nuget.org jest to bardzo rzadki przypadek, ponieważ przerwie oficjalne założenie klienta, że identyfikator pakietu i wersja implikują określoną zawartość pakietu. Aby uzyskać więcej informacji na temat usuwania pakietów na nuget.org, zobacz [nasze zasady](../nuget-org/policies/deleting-packages.md).

Elementy katalogu usuwania pakietów nie mają dodatkowych właściwości oprócz tych [uwzględnionych na liście liści wszystkich katalogów](#catalog-leaf).

`version`Właściwość to oryginalny ciąg wersji znaleziony w pakiecie. nuspec.

`published`Właściwość to czas, przez który został usunięty pakiet, który jest zazwyczaj krótszy niż czas przed zatwierdzeniem elementu katalogu.

#### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Biera

### <a name="overview"></a>Omówienie

W tej sekcji opisano koncepcje klienta, które mimo że nie jest to konieczne przez protokół, powinny być częścią każdej praktycznej implementacji klienta katalogu.

Ze względu na to, że katalog jest strukturą danych tylko do dołączenia indeksowanym przez czas, klient powinien przechowywać **kursor** lokalnie, co oznacza, że punkt w czasie klient przetworzył elementy katalogu. Należy pamiętać, że ta wartość kursora nigdy nie powinna być generowana przy użyciu zegara komputera klienta. Zamiast tego wartość powinna pochodzić z wartości obiektu katalogu `commitTimestamp` .

Za każdym razem, gdy klient chce przetwarzać nowe zdarzenia w źródle pakietów, musi tylko wysyłać zapytania do wykazu dla wszystkich elementów wykazu z sygnaturą czasową zatwierdzania większą niż jej przechowywany kursor. Gdy klient pomyślnie przetworzy wszystkie nowe elementy katalogu, rejestruje najnowsze sygnatury czasowe zatwierdzania elementów katalogu, które zostały przetworzone w postaci nowej wartości kursora.

Korzystając z tej metody, klient może zawsze pominąć wszystkie zdarzenia pakietu, które wystąpiły w źródle pakietu.
Ponadto klient nigdy nie musi ponownie przetwarzać starych zdarzeń przed zapisaną sygnaturą czasową zatwierdzania kursora.

Ta zaawansowana koncepcja kursorów jest używana dla wielu zadań w tle nuget.org i służy do zapewnienia aktualności interfejsu API v3. 

### <a name="initial-value"></a>Wartość początkowa

Gdy klient wykazu jest uruchamiany po raz pierwszy (i w związku z tym nie ma wartości kursora), powinien używać domyślnej wartości kursora. Sieć `System.DateTimeOffset.MinValue` lub inne analogiczne pojęcie dotyczące minimalnej reprezentacji sygnatury czasowej.

### <a name="iterating-over-catalog-items"></a>Iterowanie przez elementy katalogu

Aby wykonać zapytanie dotyczące następnego zestawu elementów katalogu do przetworzenia, klient powinien:

1. Pobierz wartość zapisanego kursora z lokalnego magazynu.
1. Pobierz i deserializacji indeks wykazu.
1. Znajdź wszystkie strony wykazu z sygnaturą czasową zatwierdzenia *większą od* kursora.
1. Zadeklaruj pustą listę elementów wykazu do przetworzenia.
1. Dla każdej strony katalogu dopasowanej w kroku 3:
   1. Pobierz i deserializacji stronę wykazu.
   1. Znajdź wszystkie elementy wykazu z sygnaturą czasową zatwierdzenia *większą niż* kursor.
   1. Dodaj wszystkie zgodne elementy katalogu do listy zadeklarowanej w kroku 4.
1. Posortuj listę elementów katalogu przez Zatwierdź sygnaturę czasową.
1. Przetwarzaj każdy element katalogu w sekwencji:
   1. Pobierz i deserializacji elementu katalogu.
   1. Odpowiednie reagowanie na typ elementu katalogu.
   1. Przetwarzanie dokumentu elementu katalogu w sposób specyficzny dla klienta.
1. Zapisz sygnaturę czasową zatwierdzenia ostatniego elementu katalogu jako nową wartość kursora.

Przy użyciu tego podstawowego algorytmu implementacja klienta może utworzyć pełny widok wszystkich pakietów dostępnych w źródle pakietu. Klient musi wykonywać ten algorytm okresowo tylko w celu uzyskania najnowszych zmian w źródle pakietu.

> [!Note]
> Jest to algorytm używany przez nuget.org do przechowywania [metadanych pakietu](registration-base-url-resource.md), [zawartości pakietu](package-base-address-resource.md), [wyszukiwania](search-query-service-resource.md) i [automatycznego uzupełniania](search-autocomplete-service-resource.md) zasobów.

### <a name="dependent-cursors"></a>Kursory zależne

Załóżmy, że istnieją dwaj klienci wykazu, którzy mają nieodłączną zależność, gdzie dane wyjściowe jednego klienta są zależne od innego klienta. 

#### <a name="example"></a>Przykład

Na przykład w przypadku nuget.org nowo opublikowany pakiet nie powinien być wyświetlany w zasobie wyszukiwania przed wyświetleniem go w zasobie metadanych pakietu. Wynika to z faktu, że operacja "Restore" wykonywana przez oficjalnego klienta NuGet używa zasobu metadanych pakietu. Jeśli klient odnajduje pakiet za pomocą usługi Search, powinien mieć możliwość pomyślnego przywrócenia tego pakietu przy użyciu zasobu metadanych pakietu. Innymi słowy, zasób wyszukiwania zależy od zasobu metadanych pakietu. Każdy zasób ma zadanie w tle klienta wykazujące aktualizację tego zasobu. Każdy klient ma swój własny kursor.

Ponieważ oba zasoby są zbudowane z wykazu, kursor klienta katalogu, który aktualizuje zasób wyszukiwania, *nie może wykraczać poza* kursor klienta katalogu metadanych pakietu.

#### <a name="algorithm"></a>Algorytm

Aby zaimplementować to ograniczenie, wystarczy zmodyfikować algorytm powyżej, aby:

1. Pobierz wartość zapisanego kursora z lokalnego magazynu.
1. Pobierz i deserializacji indeks wykazu.
1. Znajdź wszystkie strony wykazu z sygnaturą czasową zatwierdzania *większą niż* kursor **krótszy niż lub równy kursorowi zależności.**
1. Zadeklaruj pustą listę elementów wykazu do przetworzenia.
1. Dla każdej strony katalogu dopasowanej w kroku 3:
   1. Pobierz i deserializacji stronę wykazu.
   1. Znajdź wszystkie elementy wykazu z sygnaturą czasową zatwierdzenia *większą niż* kursor, który jest **mniejszy niż lub równy kursorowi zależności.**
   1. Dodaj wszystkie zgodne elementy katalogu do listy zadeklarowanej w kroku 4.
1. Posortuj listę elementów katalogu przez Zatwierdź sygnaturę czasową.
1. Przetwarzaj każdy element katalogu w sekwencji:
   1. Pobierz i deserializacji elementu katalogu.
   1. Odpowiednie reagowanie na typ elementu katalogu.
   1. Przetwarzanie dokumentu elementu katalogu w sposób specyficzny dla klienta.
1. Zapisz sygnaturę czasową zatwierdzenia ostatniego elementu katalogu jako nową wartość kursora.

Korzystając z tego zmodyfikowanego algorytmu, można utworzyć system zależnych klientów wykazu do tworzenia własnych określonych indeksów, artefaktów itp.
