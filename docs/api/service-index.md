---
title: Usługa Index, interfejs API programu NuGet
description: Indeks usług jest punkt wejścia interfejsu API protokołu HTTP NuGet i wylicza możliwości serwera.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 478b74f98caafdc7c6b69423b9f9d72890c8d7cb
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545260"
---
# <a name="service-index"></a>Indeks usług

Indeks usług to dokument JSON, który jest punktem wejścia dla źródła pakietów NuGet i umożliwia implementacji klienta odkryć możliwości źródła pakietu. Indeks usług jest obiekt JSON z dwoma wymagane właściwości: `version` (wersja schematu indeksu service) i `resources` (punkty końcowe lub możliwości źródła pakietu).

Indeks usług usługi nuget.org znajduje się w `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Przechowywanie wersji

`version` Wartość jest ciągiem wersji parseable SemVer 2.0.0, który wskazuje wersję schematu indeksu usługi. Interfejs API określającemu, że ciąg wersji zawiera numer wersji głównej `3`. Wprowadzaniu zmian niepowodujących niezgodności na schemat indeksu service, wersja pomocnicza ciąg wersji zostanie zwiększona.

Każdy zasób w indeksie usługi jest numery wersji niezależne od wersji schematu indeksu usługi.

Bieżąca wersja schematu to `3.0.0`. `3.0.0` Wersja jest funkcjonalnie równoważny ze starszą wersją `3.0.0-beta.1` wersji, ale powinien być preferowany, jak wyraźniej komunikuje się ona stabilny, definicja schematu.

## <a name="http-methods"></a>Metody HTTP

Indeks usług jest dostępna przy użyciu metod HTTP `GET` i `HEAD`.

## <a name="resources"></a>Resources

`resources` Właściwość zawiera szereg zasobów obsługiwana przez tego źródła pakietów.

### <a name="resource"></a>Zasób

Zasób jest obiektem w `resources` tablicy. Reprezentuje wersjonowany możliwości źródła pakietu. Zasób ma następujące właściwości:

Nazwa          | Typ   | Wymagane | Uwagi
------------- | ------ | -------- | -----
@id           | string | Tak      | Adres URL do zasobu
@type         | string | Tak      | Stała typu string, reprezentujący typ zasobu
komentarz       | string | Brak       | Ludzi, czytelny opis zasobu

`@id` Jest adres URL, który musi być bezwzględna i muszą mieć schemat HTTP lub HTTPS.

`@type` Służy do identyfikowania określonych protokół do użycia podczas interakcji z zasobów. Typ zasobu to nieprzezroczysty ciąg, ale zazwyczaj ma następujący format:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Klienci powinni kodowi twardych `@type` wartości zrozumieć i wyszukiwać w indeksie usługi źródła pakietu. Dokładnie `@type` wartości w obecnie są wyliczane na dokumenty referencyjne poszczególnych zasobów, które są wymienione w [omówienie interfejsu API](overview.md#resources-and-schema).

Dla tej dokumentacji dokumentacji dotyczącej różnych zasobów zasadniczo można grupować według `{RESOURCE_NAME}` znaleziony w indeksie usługi, która jest analogiczna do grupowania według scenariusza. 

Nie jest wymagane, że każdy zasób ma unikatową `@id` lub `@type`. Jest implementacji klienta, aby określić zasoby, które preferowanie za pośrednictwem innego. Jest to jedna implementacja to możliwe, że zasoby o tej samej lub zgodny `@type` mogą być używane w okrężne w razie awarii lub serwera błąd połączenia.

### <a name="sample-request"></a>Przykładowe żądanie

POBIERZ https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [service-index.json](./_data/service-index.json)]
