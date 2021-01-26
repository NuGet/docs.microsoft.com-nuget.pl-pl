---
title: tools.jsna potrzeby odnajdywania nuget.exe wersji
description: Punkt końcowy dla
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773813"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.jsna potrzeby odnajdywania nuget.exe wersji

Obecnie istnieje kilka sposobów uzyskania najnowszej wersji nuget.exe na komputerze w sposób skryptowy. Na przykład możesz pobrać i wyodrębnić [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) pakiet z NuGet.org. Jest to pewna złożoność, ponieważ wymaga już nuget.exe (dla `nuget.exe install` ) lub trzeba rozpakować plik. nupkg przy użyciu podstawowego narzędzia rozpakować i znaleźć dane binarne wewnątrz.

Jeśli masz już nuget.exe, możesz również użyć programu `nuget.exe update -self` , ale wymaga to również istniejącej kopii nuget.exe. To podejście powoduje także aktualizację do najnowszej wersji. Nie zezwala na korzystanie z określonej wersji.

`tools.json`Punkt końcowy jest dostępny zarówno w celu rozwiązywania problemów z uruchamianiem programu, jak i zapewnienia kontroli wersji pobieranych nuget.exe. Ta usługa może być używana w środowiskach ciągłej integracji/ciągłego wdrażania lub w skryptach niestandardowych w celu odnajdywania i pobierania dowolnej wydanej wersji nuget.exe.

`tools.json`Punkt końcowy można pobrać przy użyciu nieuwierzytelnionego żądania HTTP (np. `Invoke-WebRequest` w programie PowerShell lub `wget` ). Można ją analizować przy użyciu deserializacji JSON, a kolejne adresy URL pobierania nuget.exe można także pobrać przy użyciu nieuwierzytelnionych żądań HTTP.

Punkt końcowy można pobrać przy użyciu `GET` metody:

```
GET https://dist.nuget.org/tools.json
```

[Schemat JSON](https://json-schema.org/) dla punktu końcowego jest dostępny tutaj:

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>Reakcja

Odpowiedź to dokument JSON zawierający wszystkie dostępne wersje nuget.exe.

Główny obiekt JSON ma następującą właściwość:

Nazwa      | Typ             | Wymagane
--------- | ---------------- | --------
nuget.exe | Tablica obiektów | tak

Każdy obiekt w `nuget.exe` tablicy ma następujące właściwości:

Nazwa     | Typ   | Wymagane | Uwagi
-------- | ------ | -------- | -----
Wersja  | ciąg | tak      | Ciąg 2.0.0 SemVer
url      | ciąg | tak      | Bezwzględny adres URL pobierania tej wersji nuget.exe
etap    | ciąg | tak      | Ciąg wyliczeniowy
wysyłane | ciąg | tak      | Przybliżona sygnatura czasowa ISO 8601, gdy wersja została udostępniona

Elementy w tablicy zostaną posortowane w kolejności malejącej, SemVer 2.0.0. Gwarantuje to zmniejszenie obciążenia klienta, który ma największy numer wersji. Oznacza to jednak, że lista nie jest posortowana w kolejności chronologicznej. Na przykład jeśli niższa wersja główna jest obsługiwana w dacie późniejszej niż wyższa wersja główna, ta wersja serwisowa nie będzie widoczna w górnej części listy. Jeśli chcesz, aby Najnowsza wersja została wydana przez *sygnaturę czasową*, po prostu posortuj tablicę według `uploaded` ciągu. Dzieje się tak, ponieważ `uploaded` sygnatura czasowa znajduje się w formacie [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , który można sortować chronologicznie przy użyciu sortowania lexicographical (tj. proste sortowanie ciągu).

`stage`Właściwość wskazuje, jak zbadane ta wersja narzędzia. 

Etap              | Znaczenie
------------------ | ------
EarlyAccessPreview | Nie jest jeszcze widoczne na [stronie pobierania](https://www.nuget.org/downloads) i powinny być sprawdzone przez partnerów
Wydano           | Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane do użycia w szerokim zakresie.
ReleasedAndBlessed | Dostępne w witrynie pobierania i zalecane do użycia

Jednym z prostych podejścia do uzyskania najnowszej, zalecanej wersji jest wykonanie pierwszej wersji na liście, która ma `stage` wartość `ReleasedAndBlessed` . To działa, ponieważ wersje są sortowane w kolejności SemVer 2.0.0.

`NuGet.CommandLine`Pakiet w programie NuGet.org jest zazwyczaj aktualizowany tylko przy użyciu `ReleasedAndBlessed` wersji.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [tools-json.json](./_data/tools-json.json)]
