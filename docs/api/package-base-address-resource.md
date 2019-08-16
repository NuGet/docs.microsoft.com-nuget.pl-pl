---
title: Zawartość pakietu, interfejs API NuGet
description: Adres podstawowy pakietu jest prostym interfejsem do pobierania samego pakietu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488217"
---
# <a name="package-content"></a>Zawartość pakietu

Możliwe jest wygenerowanie adresu URL w celu pobrania zawartości dowolnego pakietu (plik. nupkg) przy użyciu interfejsu API v3. Zasób używany do pobierania zawartości pakietu jest `PackageBaseAddress` zasobem znalezionym w indeksie [usługi](service-index.md). Ten zasób umożliwia również odnajdywanie wszystkich wersji pakietu na liście lub niewymienionej liście.

Ten zasób jest często określany jako "adres podstawowy pakietu" lub "kontener płaski".

## <a name="versioning"></a>Przechowywanie wersji

Używana jest `@type` następująca wartość:

@typewartościami              | Uwagi
------------------------ | -----
PackageBaseAddress/3.0.0 | Początkowa wersja

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzoną z wymienioną powyżej wartością zasobu. `@type` W poniższym dokumencie zostanie użyty symbol zastępczy podstawowego `{@id}` adresu URL.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL znajdujące się w zasobie rejestracji obsługują `GET` metody `HEAD`http i.

## <a name="enumerate-package-versions"></a>Wylicz wersje pakietów

Jeśli Klient zna identyfikator pakietu i chce wykryć wersje pakietów dostępne dla źródła pakietu, klient może skonstruować przewidywalny adres URL w celu wyliczenia wszystkich wersji pakietu. Ta lista ma być "listą katalogów" dla interfejsu API zawartości pakietu wymienionego poniżej.

> [!Note]
> Ta lista zawiera listę wersji pakietów wymienionych i nieznajdujących się na liście.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry żądania

Nazwa     | W     | Typ    | Wymagane | Uwagi
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adres URL    | string  | tak      | Identyfikator pakietu, małe litery

`LOWER_ID` Wartość jest pożądanym identyfikatorem pakietu małymi literami przy użyciu reguł zaimplementowane przez. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda sieci.

### <a name="response"></a>Odpowiedź

Jeśli źródło pakietu nie ma wersji podanego identyfikatora pakietu, zwracany jest kod stanu 404.

Jeśli źródło pakietu ma co najmniej jedną wersję, zwracany jest kod stanu 200. Treść odpowiedzi jest obiektem JSON z następującą właściwością:

Nazwa     | Typ             | Wymagane | Uwagi
-------- | ---------------- | -------- | -----
wersje | Tablica ciągów | tak      | Dostępne identyfikatory pakietów

Ciągi w `versions` tablicy to wszystkie małe litery, [znormalizowane ciągi wersji NuGet](../concepts/package-versioning.md#normalized-version-numbers). Ciągi wersji nie zawierają żadnych metadanych kompilacji SemVer 2.0.0.

Zamiarem jest to, że ciągi wersji Znalezione w tej tablicy mogą być używane Verbatim `LOWER_VERSION` dla tokenów znalezionych w następujących punktach końcowych.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Pobierz zawartość pakietu (. nupkg)

Jeśli Klient zna identyfikator pakietu i wersję, a następnie chce pobrać zawartość pakietu, musi jedynie utworzyć następujący adres URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parametry żądania

Nazwa          | W     | Typ   | Wymagane | Uwagi
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adres URL    | string | tak      | Identyfikator pakietu, małe litery
LOWER_VERSION | Adres URL    | string | tak      | Wersja pakietu, znormalizowana i mała

Oba `LOWER_ID` i`LOWER_VERSION` są małymi literami przy użyciu reguł zaimplementowane przez. Sieć[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
Method.

Jest `LOWER_VERSION` to żądana wersja pakietu, znormalizowana przy użyciu [reguł normalizacji](../concepts/package-versioning.md#normalized-version-numbers)wersji programu NuGet. Oznacza to, że w tym przypadku należy wykluczyć metadane kompilacji, które są dozwolone w specyfikacji SemVer 2.0.0.

### <a name="response-body"></a>Treść odpowiedzi

Jeśli pakiet istnieje w źródle pakietów, zwracany jest kod stanu 200. Treść odpowiedzi będzie samą zawartością pakietu.

Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Przykładowa odpowiedź

Strumień binarny, który jest plikiem. nupkg dla Newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Pobierz manifest pakietu (. nuspec)

Jeśli Klient zna identyfikator pakietu i wersję i chce pobrać manifest pakietu, musi jedynie utworzyć następujący adres URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parametry żądania

Nazwa          | W     | Typ   | Wymagane | Uwagi
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adres URL    | string | tak      | Identyfikator pakietu, małe litery
LOWER_VERSION | Adres URL    | string | tak      | Wersja pakietu, znormalizowana i mała

Oba `LOWER_ID` i`LOWER_VERSION` są małymi literami przy użyciu reguł zaimplementowane przez. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda sieci.

Jest `LOWER_VERSION` to żądana wersja pakietu, znormalizowana przy użyciu [reguł normalizacji](../concepts/package-versioning.md#normalized-version-numbers)wersji programu NuGet. Oznacza to, że w tym przypadku należy wykluczyć metadane kompilacji, które są dozwolone w specyfikacji SemVer 2.0.0.

### <a name="response-body"></a>Treść odpowiedzi

Jeśli pakiet istnieje w źródle pakietów, zwracany jest kod stanu 200. Treść odpowiedzi będzie manifestem pakietu, który jest nuspec zawarty w odpowiedniej. nupkg. Plik. nuspec jest dokumentem XML.

Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
