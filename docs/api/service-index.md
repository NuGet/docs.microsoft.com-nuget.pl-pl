---
title: Indeks usługi, interfejs API NuGet
description: Indeks usługi jest punktem wejścia interfejsu API protokołu HTTP NuGet i wylicza możliwości serwera programu.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775359"
---
# <a name="service-index"></a>Indeks usług

Indeks usługi to dokument JSON, który jest punktem wejścia dla źródła pakietu NuGet i umożliwia implementacji klienta odnajdywanie możliwości źródła pakietu. Indeks usługi jest obiektem JSON z dwiema wymaganymi właściwościami: `version` (wersja schematu indeksu usługi) i `resources`  (punkty końcowe lub możliwości źródła pakietu).

Pakiet NuGet. indeks usługi organizacji znajduje się w lokalizacji `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Przechowywanie wersji

`version`Wartość jest ciągiem wersji SemVer 2.0.0, który wskazuje wersję schematu indeksu usługi. Interfejs API wymaga, aby ciąg wersji miał wersję główną `3` . Ponieważ zmiany niekrytyczne są wprowadzane do schematu indeksu usługi, zostanie zwiększona wersja pomocnicza ciągu wersji.

Każdy zasób w indeksie usługi jest zależny od wersji schematu indeksu usługi.

Bieżąca wersja schematu to `3.0.0` . `3.0.0`Wersja jest funkcjonalnie równoważna ze starszą `3.0.0-beta.1` wersją, ale powinna być preferowana, ponieważ bardziej wyraźnie komunikuje się stabilny, zdefiniowany schemat.

## <a name="http-methods"></a>Metody HTTP

Indeks usługi jest dostępny przy użyciu metod HTTP `GET` i `HEAD` .

## <a name="resources"></a>Zasoby

`resources`Właściwość zawiera tablicę zasobów obsługiwaną przez to źródło pakietu.

### <a name="resource"></a>Zasób

Zasób jest obiektem w `resources` tablicy. Reprezentuje możliwość wersji źródłowej pakietu. Zasób ma następujące właściwości:

Nazwa          | Typ   | Wymagane | Uwagi
------------- | ------ | -------- | -----
@id           | ciąg | tak      | Adres URL zasobu
@type         | ciąg | tak      | Stała w postaci ciągu reprezentująca typ zasobu
komentarz       | ciąg | nie       | Czytelny dla człowieka opis zasobu

`@id`Jest adresem URL, który musi być bezwzględny i musi mieć schemat http lub https.

Służy `@type` do identyfikowania określonego protokołu, który ma być używany podczas korzystania z zasobów. Typ zasobu jest nieprzezroczystym ciągiem, ale zazwyczaj ma format:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

Klienci oczekują na `@type` poznanie zrozumiałych wartości i poszukaj ich w indeksie usługi źródła pakietu. Dokładne `@type` wartości używane dzisiaj są wyliczane na poszczególnych dokumentach odwołań do zasobów wymienionych w temacie [Omówienie interfejsu API](overview.md#resources-and-schema).

Ze względu na tę dokumentację dokumentacja dotycząca różnych zasobów zostanie zasadniczo pogrupowana według `{RESOURCE_NAME}` znalezionych w indeksie usługi, które są analogiczne do grupowania według scenariusza. 

Nie istnieje wymóg, że każdy zasób ma unikatowy `@id` lub `@type` . Jest to implementacja klienta, aby określić, który zasób ma być preferowany przez inny. Jedną z możliwych implementacji jest to, że zasoby tego samego lub zgodne `@type` mogą być używane w sposób okrężny w przypadku awarii połączenia lub błędu serwera.

### <a name="sample-request"></a>Przykładowe żądanie

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Przykładowa odpowiedź

[!code-JSON [service-index.json](./_data/service-index.json)]
