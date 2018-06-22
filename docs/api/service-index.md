---
title: Indeks usługi, NuGet interfejsu API
description: Indeks usługi jest punkt wejścia interfejsu API HTTP NuGet i wylicza możliwości serwera.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822097"
---
# <a name="service-index"></a>Indeks usługi

Indeks usługi jest dokumentem JSON, który jest punkt wejścia dla źródła pakietów NuGet i umożliwia implementacja klienta wykryć możliwości źródła pakietu. Indeks usługi jest obiektem JSON z dwóch wymaganych właściwości: `version` (wersja schematu indeksu service) i `resources` (punktów końcowych lub możliwości źródła pakietu).

Indeks usługi nuget.org znajduje się pod adresem `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Przechowywanie wersji

`version` Wartość jest ciągiem parseable wersji programu SemVer 2.0.0, co oznacza wersji schematu indeksu usługi. Interfejs API wymaga, że ciąg wersji ma numer wersji głównej `3`. Nierozdzielające zmiany do schematu indeksu usługi, zostanie zwiększona wersja pomocnicza ciąg wersji.

Każdy zasób w indeksie usługi jest kontrolą wersji niezależnie od wersji schematu indeksu usługi.

Bieżąca wersja schematu jest `3.0.0`. `3.0.0` Jest funkcjonalnym odpowiednikiem starszej wersji `3.0.0-beta.1` wersji, ale powinien być preferowany, jak komunikuje się bardziej precyzyjnie stabilny, definicja schematu.

## <a name="http-methods"></a>Metody HTTP

Indeks usługa jest dostępna przy użyciu metody HTTP `GET` i `HEAD`.

## <a name="resources"></a>Zasoby

`resources` Właściwość zawiera tablicę obsługiwane przez to źródło pakietu zasobów.

### <a name="resource"></a>Zasób

Zasób jest obiektem w `resources` tablicy. Reprezentuje on określonej wersji możliwości źródła pakietu. Zasób ma następujące właściwości:

Nazwa          | Typ   | Wymagane | Uwagi
------------- | ------ | -------- | -----
@id           | string | Tak      | Adres URL do zasobu
@type         | string | Tak      | Stała ciąg reprezentujący typ zasobu
komentarz       | string | Brak       | Czytelny dla ludzi opis zasobu

`@id` Jest adres URL, który musi być bezwzględnym i musi mieć schemat HTTP lub HTTPS.

`@type` Służy do identyfikowania określonych protokół do użycia podczas interakcji z zasobów. Typ zasobu jest ciągiem nieprzezroczyste, ale ma zazwyczaj format:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Klienci powinni twardych kodu `@type` wartości zrozumieć i wyszukiwanie w indeksie usługi źródła pakietu. Dokładnie `@type` wartości w obecnie są wyliczane w dokumentach odwołanie pojedynczego zasobu, na liście [Przegląd interfejsu API](overview.md#resources-and-schema).

Dla niniejszej dokumentacji dokumentację dotyczącą różnych zasobów będą zasadniczo pogrupowane według `{RESOURCE_NAME}` znalezionych w indeksie usługi, która jest analogiczna do grupowania według scenariusza. 

Nie jest wymagane czy każdy zasób ma unikatową `@id` lub `@type`. Jest implementacja klienta, aby określić, którego zasobu należy użyć zamiast innego. Jest to jedna implementacja możliwe, że zasoby o tej samej lub zgodne `@type` mogą być używane w okrężne w przypadku awarii lub serwera błąd połączenia.

### <a name="sample-request"></a>Przykładowe żądanie

POBIERZ https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [service-index.json](./_data/service-index.json)]
