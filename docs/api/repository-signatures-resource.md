---
title: Sygnatury repozytorium, interfejs API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Zasób sygnatur repozytorium umożliwia klientom źródła pakietów anonsowanie możliwości podpisywania repozytorium.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775334"
---
# <a name="repository-signatures"></a>Podpisy repozytorium

Jeśli źródło pakietu obsługuje dodawanie podpisów repozytorium do opublikowanych pakietów, możliwe jest, aby klient określił certyfikaty podpisywania używane przez źródło pakietu. Ten zasób umożliwia klientom wykrycie, czy podpisany pakiet repozytorium został naruszony, czy ma nieoczekiwany certyfikat podpisywania.

Zasób używany do pobierania informacji o sygnaturze tego repozytorium jest `RepositorySignatures` zasobem znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

`@type`Używana jest następująca wartość:

@type wartościami                | Uwagi
-------------------------- | -----
RepositorySignatures/4.7.0 | Początkowa wersja
RepositorySignatures/4.9.0 | Obsługiwane przez klienta NuGet v 4.9 +
RepositorySignatures/5.0.0 | Umożliwia włączenie funkcji `allRepositorySigned` . Obsługiwane przez klienta NuGet v 5.0 +

## <a name="base-url"></a>Podstawowy adres URL

Adres URL punktu wejścia dla następujących interfejsów API jest wartością `@id` Właściwości skojarzoną z wymienioną powyżej wartością zasobu `@type` . W tym temacie jest stosowany symbol zastępczy URL `{@id}` .

Należy pamiętać, że w przeciwieństwie do innych zasobów `{@id}` adres URL musi być obsługiwany za pośrednictwem protokołu HTTPS.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL Znalezione w zasobie sygnatur repozytorium obsługują tylko metody HTTP `GET` i `HEAD` .

## <a name="repository-signatures-index"></a>Indeks sygnatur repozytorium

Indeks sygnatur repozytorium zawiera dwie informacje:

1. Czy wszystkie pakiety Znalezione w źródle są podpisane przez to źródło pakietu.
1. Lista certyfikatów używanych przez źródło pakietu do podpisywania pakietów.

W większości przypadków Lista certyfikatów zostanie kiedykolwiek dołączona do programu. Nowe certyfikaty zostaną dodane do listy, gdy poprzedni certyfikat podpisywania wygasł, a źródło pakietu musi zacząć korzystać z nowego certyfikatu podpisywania. Jeśli certyfikat zostanie usunięty z listy, oznacza to, że wszystkie podpisy pakietu utworzone przy użyciu usuniętego certyfikatu podpisywania nie powinny już być uznawane za prawidłowe przez klienta. W takim przypadku podpis pakietu (ale niekoniecznie jest to pakiet) jest nieprawidłowy. Zasady klienta mogą zezwalać na instalowanie pakietu jako niepodpisane.

W przypadku odwoływania certyfikatów (np. złamania klucza) źródło pakietu powinno ponownie podpisać wszystkie pakiety podpisane przez odnośny certyfikat. Ponadto źródło pakietu powinno usunąć odnośny certyfikat z listy certyfikat podpisywania.

Poniższe żądanie Pobiera indeks sygnatur repozytorium.

```
GET {@id}
```

Indeks sygnatury repozytorium jest dokumentem JSON zawierającym obiekt o następujących właściwościach:

Nazwa                | Typ             | Wymagane | Uwagi
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | tak      | Musi znajdować się `false` w zasobach 4.7.0 i 4.9.0
signingCertificates | Tablica obiektów | tak      | 

Wartość `allRepositorySigned` logiczna jest ustawiona na false, jeśli źródło pakietu ma niektóre pakiety, które nie mają sygnatury repozytorium. Jeśli wartość logiczna ma wartość true, wszystkie pakiety dostępne w źródle muszą mieć sygnaturę repozytorium wygenerowaną przez jeden z certyfikatów podpisywania wymienionych w temacie `signingCertificates` .

> [!Warning]
> `allRepositorySigned`Wartość logiczna musi mieć wartość false w zasobach 4.7.0 i 4.9.0. Klienci programu NuGet v 4.7, v 4.8 i v 4.9 nie mogą instalować pakietów ze źródeł, `allRepositorySigned` dla których ustawiono wartość true.

`signingCertificates`Jeśli wartość logiczna ma wartość true, w tablicy powinien znajdować się co najmniej jeden certyfikat podpisywania `allRepositorySigned` . Jeśli tablica jest pusta i `allRepositorySigned` ma ustawioną wartość true, wszystkie pakiety ze źródła powinny być traktowane jako nieprawidłowe, mimo że zasady klienta nadal mogą zezwalać na użycie pakietów. Każdy element w tej tablicy jest obiektem JSON z poniższymi właściwościami.

Nazwa         | Typ   | Wymagane | Uwagi
------------ | ------ | -------- | -----
contentUrl   | ciąg | tak      | Bezwzględny adres URL do certyfikatu publicznego zakodowanego algorytmem DER
odcisków palców | object | tak      |
subject      | ciąg | tak      | Nazwa wyróżniająca podmiotu z certyfikatu
issuer       | ciąg | tak      | Nazwa wyróżniająca wystawcy certyfikatu
notBefore    | ciąg | tak      | Początkowe sygnatura czasowa okresu ważności certyfikatu
notAfter     | ciąg | tak      | Końcowe sygnatura czasowa okresu ważności certyfikatu

Należy pamiętać, że `contentUrl` jest to wymagane do objęcia usługą za pośrednictwem protokołu HTTPS. Ten adres URL nie ma określonego wzorca adresu URL i musi być dynamicznie odnajdywany przy użyciu tego dokumentu indeksu sygnatur repozytorium. 

Wszystkie właściwości w tym obiekcie (oprócz `contentUrl` ) muszą być wyprowadzane z certyfikatu znalezionego w `contentUrl` .
Te właściwości, które można uzyskać jako wygodę do minimalizowania rundy.

`fingerprints`Obiekt ma następujące właściwości:

Nazwa                   | Typ   | Wymagane | Uwagi
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | ciąg | tak      | Odcisk palca SHA-256

Nazwa klucza `2.16.840.1.101.3.4.2.1` jest identyfikatorem OID algorytmu wyznaczania wartości skrótu SHA-256.

Wszystkie wartości skrótu muszą być pisane małymi literami, kodowane w formacie szesnastkowym.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
