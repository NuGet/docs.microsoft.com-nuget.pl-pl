---
title: Tools.JSON nuget.exe wersji odnajdywania
description: Punkt końcowy
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852536"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools.JSON nuget.exe wersji odnajdywania

Już dziś istnieje kilka sposobów, aby uzyskać najnowszą wersję programu nuget.exe na swojej maszynie w sposób za pomocą skryptów. Na przykład, Pobierz i Wyodrębnij [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pakietów z witryny nuget.org. Ma złożoność, ponieważ wymaga ona albo, że masz już nuget.exe (dla `nuget.exe install`) lub masz rozpakowywanie .nupkg przy użyciu narzędzia unzip podstawowe i znaleźć wewnątrz binarnego.

Jeśli masz już nuget.exe, można również użyć `nuget.exe update -self`, jednak wymaga to również, masz istniejącą kopię nuget.exe. Takie podejście również aktualizacji do najnowszej wersji. Nie zezwalaj na użycie określonej wersji.

`tools.json` Punkt końcowy jest dostępny dla obu problemu bootstrapping i zapewnić kontrolę wersji nuget.exe pobrany. To może służyć w środowiskach ciągłej integracji/ciągłego Dostarczania i niestandardowych skryptów do odnajdywania i Pobierz wszelkie wydanej wersji nuget.exe.

`tools.json` Punktu końcowego można pobrać za pomocą nieuwierzytelnione żądania HTTP (np. `Invoke-WebRequest` w programie PowerShell lub `wget`). Można analizować, przy użyciu deserializacji JSON i pobierania nuget.exe kolejne adresy URL można również pobrać za pomocą nieuwierzytelnione żądania HTTP.

Punkt końcowy można pobrać przy użyciu `GET` metody:

    GET https://dist.nuget.org/tools.json

[Schematu JSON](http://json-schema.org/) punkt końcowy jest dostępny tutaj:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Odpowiedź

Odpowiedź jest dokumentem JSON, zawierającą wszystkie dostępne wersje nuget.exe.

Główny obiekt JSON ma następującą właściwość:

Nazwa      | Typ             | Wymagane
--------- | ---------------- | --------
nuget.exe | Tablica obiektów | tak

Każdy obiekt w `nuget.exe` tablica ma następujące właściwości:

Nazwa     | Typ   | Wymagane | Uwagi
-------- | ------ | -------- | -----
version  | string | tak      | Ciąg SemVer 2.0.0
url      | string | tak      | Bezwzględny adres URL pobierania tej wersji programu nuget.exe
etap    | string | tak      | Ciąg typu wyliczeniowego
Przekazany | string | tak      | Przybliżony ISO 8601 sygnaturę czasową gdy wersja została udostępniona

Elementy w tablicy zostaną posortowane, malejąco według współczynnika SemVer 2.0.0. Gwarancja jest przeznaczone do zmniejszenia obciążenia klienta, który jest zainteresowany najwyższy numer wersji. Jednak oznacza to, że lista nie jest posortowana w kolejności chronologicznej. Na przykład jeśli starszej wersji głównych jest obsługiwane w terminie później niż w nowszej wersji głównej, ta wersja obsługiwanych nie pojawi się w górnej części listy. Jeśli chcesz, aby najnowszej wersji wydawanych przez *sygnatura czasowa*, po prostu posortować tablicę za `uploaded` ciągu. To działa, ponieważ `uploaded` jest sygnatura czasowa [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formatu, który być sortowane w porządku chronologicznym za pomocą sortowania lexicographical (czyli sortowania prostego ciągu).

`stage` Właściwość wskazuje, jak sprawdzonego jest ta wersja narzędzia. 

Etap              | Znaczenie
------------------ | ------
EarlyAccessPreview | Jeszcze nie są widoczne na [pobierania strony sieci web](https://www.nuget.org/downloads) i powinny być weryfikowane przez partnerów
Wydana           | Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane w przypadku użycia rozprzestrzeniania się całej
ReleasedAndBlessed | Dostępne w witrynie pobierania i jest zalecane w przypadku użycia

Jeden proste podejście do posiadanie najnowszy, zalecana wersja ma mieć pierwszej wersji na liście, który ma `stage` wartość `ReleasedAndBlessed`. To działa, ponieważ wersje są sortowane w kolejności SemVer 2.0.0.

`NuGet.CommandLine` Pakietu w witrynie nuget.org są zazwyczaj aktualizowane tylko przy użyciu `ReleasedAndBlessed` wersji.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [tools-json.json](./_data/tools-json.json)]
