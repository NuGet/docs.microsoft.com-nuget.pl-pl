---
title: Pakiet zawartości, interfejs API programu NuGet
description: Adres podstawowy pakiet jest prosty interfejs Pobieranie pakietu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547157"
---
# <a name="package-content"></a>Zawartość pakietu

Istnieje możliwość wygenerować adres URL, aby pobrać zawartość dowolnego pakiet (plik .nupkg) przy użyciu interfejsu API w wersji 3. Zasób, używany do pobierania zawartości pakietu jest `PackageBaseAddress` można znaleźć zasobu w [indeks usług](service-index.md). Ten zasób umożliwia również odnajdywanie wszystkich wersji pakietu na liście lub nieznajdujące się na liście.

Ten zasób jest określany często jako albo "pakiet adres podstawowy" lub "container płaską".

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` zostanie użyta wartość:

@type Wartość              | Uwagi
------------------------ | -----
PackageBaseAddress/3.0.0 | Wersja początkowa

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości skojarzonej z wyżej wymienionych zasobów `@type` wartość. W następującym dokumencie symbol zastępczy bazowy adres URL `{@id}` będą używane.

## <a name="http-methods"></a>Metody HTTP

Wszystkie adresy URL, znaleziono w obsłudze zasobów rejestracji metod HTTP `GET` i `HEAD`.

## <a name="enumerate-package-versions"></a>Wyliczenie wersji pakietu

Jeśli klient zna identyfikator pakietu i chce dowiedzieć się, które pakietu wersji pakietu źródłowy jest dostępny, klient można skonstruować przewidywalne adresu URL, można wyliczyć wszystkie wersje pakietu. Ta lista jest przeznaczony jako "listing katalogu" dla interfejsu API zawartości pakietu wymienione poniżej.

> [!Note]
> Ta lista zawiera obie wersje pakietu listy i spoza niej.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry żądania

Nazwa     | W     | Typ    | Wymagane | Uwagi
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adres URL    | string  | Tak      | Identyfikator pakietu, małe litery

`LOWER_ID` Wartość jest pisany małymi literami, za pomocą reguł wdrożonych przez identyfikator żądanego pakietu. NET firmy [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

### <a name="response"></a>Odpowiedź

Jeśli źródło pakietu nie ma wersji identyfikatora podanego pakietu, zwracany jest kod stanu 404.

Jeśli źródło pakietu zawiera jedną lub kilka wersji, zwracany jest kod stanu 200. Treść odpowiedzi jest obiekt JSON z następującymi właściwościami:

Nazwa     | Typ             | Wymagane | Uwagi
-------- | ---------------- | -------- | -----
wersje | Tablica ciągów | Tak      | Pakiet dostępnych identyfikatorów

Ciągi w `versions` tablicy są wszystkie pisany małymi literami, [znormalizować ciągi wersji NuGet](../reference/package-versioning.md#normalized-version-numbers). Ciągi wersji nie zawierają żadnych metadanych kompilacji SemVer 2.0.0.

Celem jest, że ciągi wersji w tej tablicy mogą być używane verbatim dla `LOWER_VERSION` tokenów znaleźć w następujących punktów końcowych.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Pobierz zawartość pakietu (.nupkg)

Jeśli klient zna identyfikator pakietu i wersję i chce pobrać zawartość pakietu, wystarczy utworzyć następujący adres URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parametry żądania

Nazwa          | W     | Typ   | Wymagane | Uwagi
------------- | ------ | ------ | -------- | -----
LOWER_ID      | Adres URL    | string | Tak      | Identyfikator pakietu, małe litery
LOWER_VERSION | Adres URL    | string | Tak      | Wersja pakietu znormalizowane i pisany małymi literami

Zarówno `LOWER_ID` i `LOWER_VERSION` jest pisany małymi literami za pomocą reguł wdrożonych przez. NET firmy [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
Metoda.

`LOWER_VERSION` Jest wersja pakietu żądaną znormalizować przy użyciu wersji NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers). Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, który jest dozwolony przez specyfikację SemVer 2.0.0.

### <a name="response-body"></a>Treść odpowiedzi

Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200. Treść odpowiedzi będą samej zawartości pakietu.

Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Przykładowa odpowiedź

Strumień danych binarnych jest .nupkg dla Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Pobierz manifest pakietu (.nuspec)

Jeśli klient zna identyfikator pakietu i wersję i chce pobrać manifestu pakietu, wystarczy utworzyć następujący adres URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parametry żądania

Nazwa          | W     | Typ    | Wymagane | Uwagi
------------- | ------ | ------- | -------- | -----
LOWER_ID      | Adres URL    | string  | Tak      | Identyfikator pakietu, małe litery
LOWER_VERSION | Adres URL    | integer | Tak      | Wersja pakietu znormalizowane i pisany małymi literami

Zarówno `LOWER_ID` i `LOWER_VERSION` jest pisany małymi literami za pomocą reguł wdrożonych przez. NET firmy [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

`LOWER_VERSION` Jest wersja pakietu żądaną znormalizować przy użyciu wersji NuGet [reguł normalizacji](../reference/package-versioning.md#normalized-version-numbers). Oznacza to, że w takim przypadku należy wyłączyć tych metadanych kompilacji, który jest dozwolony przez specyfikację SemVer 2.0.0.

### <a name="response-body"></a>Treść odpowiedzi

Jeśli pakiet istnieje w źródle pakietu, zwracany jest kod stanu 200. Treść odpowiedzi będą manifestu pakietu, czyli .nuspec zawartych w odpowiedniej .nupkg. .nuspec jest dokument XML.

Jeśli pakiet nie istnieje w źródle pakietu, zwracany jest kod stanu 404.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
