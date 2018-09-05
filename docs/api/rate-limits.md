---
title: Limity, interfejs API programu NuGet szybkości
description: Interfejsy API NuGet zostanie wymusić limity szybkości, aby zapobiec nadużyciu.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548680"
---
# <a name="rate-limits"></a>Limity szybkości

Interfejs API NuGet.org wymusza, ograniczania szybkości, aby zapobiec nadużyciu. Żądania, które przekraczają limit szybkości zwrócenie następującego błędu: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Oprócz ograniczania, przy użyciu ograniczeń liczby wywołań żądań niektóre interfejsy API wymuszania limitu przydziału. Żądania, które przekraczają limit przydziału zwrócenie następującego błędu:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.

## <a name="package-search"></a>Wyszukiwanie pakietu

> [!Note]
> Firma Microsoft zaleca używanie usługi NuGet.org [interfejsów API w wersji 3](https://docs.microsoft.com/nuget/api/search-query-service-resource) wyszukiwania, które są wydajne i nie ma żadnych obecnie ograniczenia. Aby V1 i V2 Wyszukaj interfejsów API, limity followins mają zastosowanie:


| interfejs API | Typ ograniczenia | Wartość limitu | Usecase interfejsu API |
|:---|:---|:---|:---|
**POBIERZ** `/api/v1/Packages` | IP | 1000 / minutę | Zapytanie metadanych pakietu NuGet za pomocą protokołu OData v1 `Packages` kolekcji |
**POBIERZ** `/api/v1/Search()` | IP | 3000 / minutę | Wyszukaj pakiety NuGet, za pośrednictwem punktu końcowego wyszukiwania 1 | 
**POBIERZ** `/api/v2/Packages` | IP | 20000 / minutę | Zapytanie metadanych pakietu NuGet za pośrednictwem usługi OData w wersji 2 `Packages` kolekcji | 
**POBIERZ** `/api/v2/Packages/$count` | IP | 100 / minutę | Liczba pakietów NuGet za pośrednictwem usługi OData w wersji 2 zapytań `Packages` kolekcji | 

## <a name="package-push-and-unlist"></a>Pakiet wypychania i wyrejestrowanie

| interfejs API | Typ ograniczenia | Wartość limitu | Usecase interfejsu API | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Klucz interfejsu API | 250 / godzinę | Przekazywanie nowego pakietu NuGet (wersja) za pośrednictwem punktu końcowego wypychania v2 
**USUŃ** `/api/v2/package/{id}/{version}` | Klucz interfejsu API | 250 / godzinę | Wyrejestrowanie pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2 
