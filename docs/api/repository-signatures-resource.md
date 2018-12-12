---
title: Podpisy repozytorium, interfejs API programu NuGet | Dokumentacja firmy Microsoft
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Zasób podpisów repozytorium umożliwia klientom źródła pakietu zawiera informacje o repozytorium, ich możliwości podpisywania.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248445"
---
# <a name="repository-signatures"></a>Podpisy repozytorium

Jeśli źródło pakietu obsługuje dodawanie podpisach repozytorium na opublikowane pakiety, istnieje możliwość dla klienta określić certyfikaty podpisywania, które są używane przez źródła pakietu. Ten zasób zezwala klientom na wykrywanie, czy repozytorium jest podpisany pakiet został zmodyfikowany lub ma nieoczekiwany certyfikat podpisywania.

Zasób, używany do pobierania tych informacji podpisu repozytorium jest `RepositorySignatures` można znaleźć zasobu w [indeks usług](service-index.md).

## <a name="versioning"></a>Obsługa wersji

Następujące `@type` zostanie użyta wartość:

@type Wartość                | Uwagi
-------------------------- | -----
RepositorySignatures/4.7.0 | Wersja początkowa
RepositorySignatures/4.9.0 | Umożliwia włączenie `allRepositorySigned`

## <a name="base-url"></a>Podstawowy adres URL

Adres URL punktu wejścia dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość. W tym temacie używany zastępczego adresu URL `{@id}`.

Należy pamiętać, że w przeciwieństwie do innych zasobów `{@id}` adres URL jest wymagany ma być obsługiwana za pośrednictwem protokołu HTTPS.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL w opisach repozytorium podpisów zasobów pomocy technicznej tylko protokół HTTP metod `GET` i `HEAD`.

## <a name="repository-signatures-index"></a>Repozytorium sygnatury indeksu

Indeks sygnatury repozytorium zawiera dwa rodzaje informacji:

1. Czy nie znaleziono w źródle wszystkie pakiety są podpisane przez tego źródła pakietów repozytorium.
1. Lista certyfikatów używanych przez źródła pakietu do podpisywania pakietów.

W większości przypadków zostaną tylko dołączone do listy certyfikatów. Nowe certyfikaty zostaną dodane do listy Jeśli poprzedni certyfikat podpisywania utracił ważność i źródła pakietu musi rozpocząć korzystanie z nowego certyfikatu podpisywania. Jeśli certyfikat został usunięty z listy, oznacza to, wszystkich podpisów pakietów utworzonych za pomocą usunięto certyfikat podpisywania powinny już być uważany za prawidłowy przez klienta. W tym przypadku podpisu pakietu (ale nie musi to być pakietu) jest nieprawidłowy. Zasady klienta może zezwalać na instalowanie pakietu jako bez znaku.

W przypadku odwołania certyfikatów (np. klucza naruszenia zabezpieczeń) źródła pakietu powinien ponownie podpisać wszystkie pakiety podpisane przez dotyczy certyfikatu. Ponadto źródła pakietu należy usunąć dotyczy certyfikatu z listy certyfikatów podpisywania.

Następujące żądanie pobiera indeks sygnatury repozytorium.

    GET {@id}

Indeks sygnatury repozytorium jest dokumentem JSON, który zawiera obiekt z następującymi właściwościami:

Nazwa                | Typ             | Wymagane | Uwagi
------------------- | ---------------- | -------- | -----
allRepositorySigned | wartość logiczna          | tak      | Musi być `false` na 4.7.0 zasobów
signingCertificates | Tablica obiektów | tak      | 

`allRepositorySigned` Atrybut typu wartość logiczna jest ustawiona na wartość false, jeśli źródło pakietu ma kilka pakietów, dla których brak podpisu w repozytorium. Jeśli wartość logiczna ma wartość true, wszystkie pakiety dostępne na źródło musi mieć podpis repozytorium utworzone za pomocą jednej z certyfikatów podpisywania, o których wspomniano w `signingCertificates`.

> [!Warning]
> `allRepositorySigned` Logiczna musi mieć wartość false, na 4.7.0 zasobów. Klienci programu NuGet v4.7 na i v4.8 nie może zainstalować pakiety ze źródeł, które mają `allRepositorySigned` ma wartość true.

Powinna istnieć co najmniej jednego certyfikatu podpisywania w `signingCertificates` tablicy, jeśli `allRepositorySigned` atrybut typu wartość logiczna jest ustawiona na wartość true. Jeśli tablica jest pusta i `allRepositorySigned` jest ustawiona na wartość true, wszystkie pakiety ze źródła należy uwzględnić nieprawidłowe, mimo że zasady klienta nadal zezwalają na użycie pakietów. Każdy element w tej tablicy jest obiekt JSON z następującymi właściwościami.

Nazwa         | Typ   | Wymagane | Uwagi
------------ | ------ | -------- | -----
contentUrl   | string | tak      | Bezwzględny adres URL do algorytmem DER certyfikatu publicznego
odciski palców | object | tak      |
Temat      | string | tak      | Nazwa wyróżniająca podmiotu z certyfikatu
issuer       | string | tak      | Nazwa wyróżniająca wystawcy certyfikatu
nie wcześniej niż    | string | tak      | Sygnatura czasowa początkowy okres ważności certyfikatu
nie później niż     | string | tak      | Sygnatura czasowa zakończenia okresu ważności certyfikatu

Należy pamiętać, że `contentUrl` musi być obsługiwana za pośrednictwem protokołu HTTPS. Ten adres URL ma nie określonemu wzorcowi URL i musi zostać dynamicznie odnalezione za pomocą tego dokumentu repozytorium sygnatury indeksu. 

Wszystkie właściwości w tym obiekcie (aside z `contentUrl`) musi być derivable z certyfikatu adrese `contentUrl`.
Te właściwości derivable są udostępniane dla wygody, aby zminimalizować liczbę rund.

`fingerprints` Obiekt ma następujące właściwości:

Nazwa                   | Typ   | Wymagane | Uwagi
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | tak      | Odcisk palca SHA-256.

Nazwa klucza `2.16.840.1.101.3.4.2.1` jest OID algorytmu wyznaczania wartości skrótu SHA-256.

Wszystkie wartości skrótu musi być mała litera, zakodowanego szesnastkowo ciągów reprezentujących szyfrowanego wyznaczania wartości skrótu.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
