---
title: Tools. JSON do odnajdywania wersji NuGet. exe
description: Punkt końcowy dla
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611019"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools. JSON do odnajdywania wersji NuGet. exe

Obecnie istnieje kilka sposobów uzyskania najnowszej wersji pliku NuGet. exe na komputerze w sposób skryptowy. Na przykład możesz pobrać i wyodrębnić pakiet [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) z NuGet.org. Jest to pewna złożoność, ponieważ wymaga już posiadania pliku NuGet. exe (na potrzeby `nuget.exe install`) lub trzeba rozpakować NUPKG.

Jeśli masz już program NuGet. exe, możesz również użyć `nuget.exe update -self`, ale wymaga to również posiadania istniejącej kopii NuGet. exe. To podejście powoduje także aktualizację do najnowszej wersji. Nie zezwala na korzystanie z określonej wersji.

Punkt końcowy `tools.json` jest dostępny zarówno w celu rozwiązania problemu z uruchamianiem, jak i zapewnienia kontroli wersji programu NuGet. exe pobranej. Ta usługa może być używana w środowiskach ciągłej integracji/ciągłego wdrażania lub w skryptach niestandardowych w celu odnajdywania i pobierania dowolnej wydanej wersji programu NuGet. exe.

Punkt końcowy `tools.json` można pobrać przy użyciu nieuwierzytelnionego żądania HTTP (np. `Invoke-WebRequest` w programie PowerShell lub `wget`). Można go przeanalizować przy użyciu deserializacji JSON, a kolejne adresy URL pobierania NuGet. exe mogą być również pobierane przy użyciu nieuwierzytelnionych żądań HTTP.

Punkt końcowy można pobrać przy użyciu metody `GET`:

    GET https://dist.nuget.org/tools.json

[Schemat JSON](https://json-schema.org/) dla punktu końcowego jest dostępny tutaj:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Reakcji

Odpowiedź to dokument JSON zawierający wszystkie dostępne wersje programu NuGet. exe.

Główny obiekt JSON ma następującą właściwość:

Nazwa      | Typ             | Wymagane
--------- | ---------------- | --------
nuget.exe | Tablica obiektów | opcję

Każdy obiekt w tablicy `nuget.exe` ma następujące właściwości:

Nazwa     | Typ   | Wymagane | Uwagi
-------- | ------ | -------- | -----
version  | string | opcję      | Ciąg 2.0.0 SemVer
adres URL      | string | opcję      | Bezwzględny adres URL do pobierania tej wersji pliku NuGet. exe
Przygotowane    | string | opcję      | Ciąg wyliczeniowy
wysyłane | string | opcję      | Przybliżona sygnatura czasowa ISO 8601, gdy wersja została udostępniona

Elementy w tablicy zostaną posortowane w kolejności malejącej, SemVer 2.0.0. Gwarantuje to zmniejszenie obciążenia klienta, który ma największy numer wersji. Oznacza to jednak, że lista nie jest posortowana w kolejności chronologicznej. Na przykład jeśli niższa wersja główna jest obsługiwana w dacie późniejszej niż wyższa wersja główna, ta wersja serwisowa nie będzie widoczna w górnej części listy. Jeśli chcesz, aby Najnowsza wersja została wydana przez *sygnaturę czasową*, po prostu posortuj tablicę według ciągu `uploaded`. Dzieje się tak, ponieważ sygnatura czasowa `uploaded` jest w formacie [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , który można sortować chronologicznie przy użyciu sortowania lexicographical (tj. proste sortowanie ciągu).

Właściwość `stage` wskazuje, jak zbadane ta wersja narzędzia. 

Przygotowane              | Znaczenie
------------------ | ------
EarlyAccessPreview | Nie jest jeszcze widoczne na [stronie pobierania](https://www.nuget.org/downloads) i powinny być sprawdzone przez partnerów
Wydano           | Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane do użycia w szerokim zakresie.
ReleasedAndBlessed | Dostępne w witrynie pobierania i zalecane do użycia

Jednym z prostych podejścia do uzyskania najnowszej, zalecanej wersji jest wykonanie pierwszej wersji na liście, która ma `stage` wartość `ReleasedAndBlessed`. To działa, ponieważ wersje są sortowane w kolejności SemVer 2.0.0.

Pakiet `NuGet.CommandLine` na nuget.org jest zazwyczaj aktualizowany tylko z wersjami `ReleasedAndBlessed`.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [tools-json.json](./_data/tools-json.json)]
