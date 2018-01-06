---
title: "Pakiet zawartości, NuGet interfejsu API | Dokumentacja firmy Microsoft"
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
ms.assetid: ec68b5d1-a684-4995-b1a6-6210dbb24875
description: "Adres podstawowy pakiet jest prosty interfejs używany do pobierania samego pakietu."
keywords: "Płaskie NuGet kontenera, adres podstawowy pakietu NuGet, NuGet nupkg interfejsu API, wersje pakietu NuGet interfejsu API, interfejsu API NuGet nieznajdujące się na liście pakietów, nuspec pobierania NuGet interfejsu API"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: a581f9854410bc1a84d65310b38928a1d889ece2
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="package-content"></a>Zawartość pakietu

Istnieje możliwość wygenerowania adresu URL do pobrania zawartości dowolnego pakietu (pliku .nupkg) przy użyciu interfejsu API w wersji 3. Zasób używany do pobierania zawartości pakietu jest `PackageBaseAddress` można znaleźć zasobu w [indeksu usługi](service-index.md). Ten zasób umożliwia również odnajdywanie wszystkich wersji pakietu na liście lub nieznajdujące się na liście.

Ten zasób jest często określana jako albo "Pakiet podstawowy adres" lub "kontenera płaską".

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` jest używana wartość:

@typewartość              | Uwagi
------------------------ | -----
PackageBaseAddress/3.0.0 | Początkowa wersja

## <a name="base-url"></a>Podstawowy adres URL

Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL w obsługę zasobów rejestracji znaleziono metod HTTP `GET` i `HEAD`.

## <a name="enumerate-package-versions"></a>Wyliczenie wersji pakietu

Jeśli klient zna identyfikator pakietu i chce dowiedzieć się, które pakietu wersji pakietu źródłowy jest dostępny, klient można konstruować przewidywalną adresu URL wyliczyć wszystkie wersje pakietu. Ta lista jest przeznaczona do można "listy katalogów" dla interfejsu API zawartości pakietów wymienionych poniżej.

> [!Note]
> Ta lista zawiera obie wersje pakietu listy i spoza niej.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa     | W     | Typ    | Wymagane | Uwagi
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adres URL    | string  | Tak      | Identyfikator pakietu, małe litery

`LOWER_ID` Wartość jest małej, za pomocą reguł wdrożonych przez identyfikator żądanego pakietu. W sieci [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

### <a name="response"></a>Odpowiedź

Jeśli źródło pakietów nie ma wersji identyfikatora podany pakiet, zwracany jest kod stanu 404.

Jeśli źródło pakietu ma jedną lub kilka wersji, zwracany jest kod stanu 200. Treść odpowiedzi jest obiekt JSON z następującej właściwości:

Nazwa     | Typ             | Wymagane | Uwagi
-------- | ---------------- | -------- | -----
wersje | Tablica ciągów | Tak      | Pakiet dostępnych identyfikatorów

Ciągi w `versions` tablicy są wszystkie małej, [znormalizowany ciągów wersji NuGet](../reference/package-versioning.md#normalized-version-numbers). Ciągi wersji nie zawierają żadnych metadanych kompilacji programu SemVer 2.0.0.

Celem jest, że ciągów wersji znaleziony w tej tablicy mogą być używane verbatim dla `LOWER_VERSION` tokeny znaleźć w następujących punktów końcowych.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Pobierz zawartość pakietu (.nupkg)

Jeśli klient zna identyfikator pakietu i wersję i chce pobrać zawartość pakietu, potrzebują tylko utworzyć następujący adres URL:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa          | W     | Typ   | Wymagane | Uwagi
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adres URL    | string | Tak      | Identyfikator pakietu, małe litery
LOWER_VERSION | Adres URL    | string | Tak      | Wersja pakietu znormalizowany i małej

Zarówno `LOWER_ID` i `LOWER_VERSION` są małej za pomocą reguł wdrożonych przez. W sieci [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

`LOWER_VERSION` Jest wersja pakietu żądaną znormalizowany przy użyciu wersji narzędzia NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers). Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, która jest dozwolona przez specyfikację programu SemVer 2.0.0.

### <a name="response-body"></a>Treść odpowiedzi

Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200. Treść odpowiedzi będzie samej zawartości pakietu.

Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Przykładowa odpowiedź

Strumień binarny jest .nupkg dla Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Pobierz manifest pakietu (.nuspec)

Jeśli klient zna identyfikator pakietu i wersję i chce pobrać plik manifestu pakietu, potrzebują tylko utworzyć następujący adres URL:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa          | W     | Typ    | Wymagane | Uwagi
------------- | ------ | ------- | -------- | -----
LOWER_ID      | Adres URL    | string  | Tak      | Identyfikator pakietu, małe litery
LOWER_VERSION | Adres URL    | integer | Tak      | Wersja pakietu znormalizowany i małej

Zarówno `LOWER_ID` i `LOWER_VERSION` są małej za pomocą reguł wdrożonych przez. W sieci [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

`LOWER_VERSION` Jest wersja pakietu żądaną znormalizowany przy użyciu wersji narzędzia NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers). Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, która jest dozwolona przez specyfikację programu SemVer 2.0.0.

### <a name="response-body"></a>Treść odpowiedzi

Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200. Treść odpowiedzi będzie manifestu pakietu, który jest .nuspec zawartych w odpowiedniej .nupkg. .nuspec jest dokumentu XML.

Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
