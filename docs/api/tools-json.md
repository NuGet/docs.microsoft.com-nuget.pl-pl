---
title: Tools.JSON nuget.exe wersji odnajdywania
description: Punkt końcowy
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546938"
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
nuget.exe | Tablica obiektów | Tak

Każdy obiekt w `nuget.exe` tablica ma następujące właściwości:

Nazwa     | Typ   | Wymagane | Uwagi
-------- | ------ | -------- | -----
version  | string | Tak      | Ciąg SemVer 2.0.0
adres URL      | string | Tak      | Bezwzględny adres URL pobierania tej wersji programu nuget.exe
etap    | string | Tak      | Ciąg typu wyliczeniowego
Przekazany | string | Tak      | Przybliżony sygnaturę czasową gdy wersja została udostępniona

Elementy w tablicy zostaną posortowane, malejąco według współczynnika SemVer 2.0.0. Gwarancja ta jest przeznaczona do odciążenia wyszukiwania dla najnowszej wersji klienta. 

`stage` Właściwość wskazuje, jak vettect to narzędzie jest wersja. 

etap              | Znaczenie
------------------ | ------
EarlyAccessPreview | Jeszcze nie są widoczne na [pobierania strony sieci web](https://www.nuget.org/downloads) i powinny być weryfikowane przez partnerów
Wydana           | Dostępne w witrynie pobierania, ale nie jest jeszcze zalecane w przypadku użycia rozprzestrzeniania się całej
ReleasedAndBlessed | Dostępne w witrynie pobierania i jest zalecane w przypadku użycia

Jeden proste podejście do posiadanie najnowszy, zalecana wersja ma mieć pierwszej wersji na liście, który ma `stage` wartość `ReleasedAndBlessed`.

`NuGet.CommandLine` Pakietu w witrynie nuget.org są zazwyczaj aktualizowane tylko przy użyciu `ReleasedAndBlessed` wersji.

### <a name="sample-request"></a>Przykładowe żądanie

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [tools-json.json](./_data/tools-json.json)]
