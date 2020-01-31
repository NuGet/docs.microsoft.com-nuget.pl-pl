---
title: Limity szybkości, interfejs API NuGet
description: Interfejsy API NuGet będą miały wymuszone limity szybkości, aby zapobiec nadużyciu.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813198"
---
# <a name="rate-limits"></a>Limity szybkości

Interfejs API NuGet.org wymusza ograniczenie szybkości, aby zapobiec nadużyciu. Żądania, które przekraczają limit szybkości, zwracają następujący błąd: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Oprócz ograniczania żądań przy użyciu limitów szybkości niektóre interfejsy API wymuszają również przydział. Żądania, które przekraczają limit przydziału, zwracają następujący błąd:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.

## <a name="package-search"></a>Wyszukiwanie pakietów

> [!Note]
> Zalecamy używanie NuGet. [interfejsy API wyszukiwania](search-query-service-resource.md) w wersji 3 w organizacji nie są obecnie ograniczone. W przypadku interfejsów API wyszukiwania w wersji 1 i v2 obowiązują następujące ograniczenia:

| interfejs API | Typ limitu | Wartość limitu | Interfejs API UseCase |
|:---|:---|:---|:---|
**Pobierz** `/api/v1/Packages` | adres IP | 1000/minutę | Wysyłanie zapytań dotyczących metadanych pakietów NuGet za pośrednictwem usługi `Packages` OData w wersji 1 |
**Pobierz** `/api/v1/Search()` | adres IP | 3000/minutę | Wyszukaj pakiety NuGet za pomocą punktu końcowego wyszukiwania v1 | 
**Pobierz** `/api/v2/Packages` | adres IP | 20000/minutę | Wysyłanie zapytań dotyczących metadanych pakietów NuGet za pośrednictwem protokołu OData w wersji 2 `Packages` | 
**Pobierz** `/api/v2/Packages/$count` | adres IP | 100/minutę | Wykonaj zapytania o liczbę pakietów NuGet za pośrednictwem protokołu OData w wersji 2 `Packages` | 

## <a name="package-push-and-unlist"></a>Wypychanie pakietów i wylistowanie

| interfejs API | Typ limitu | Wartość limitu | Interfejs API UseCase | 
|:---|:---|:---|:--- |
**Umieść** `/api/v2/package` | Klucz interfejsu API | 350 za godzinę | Przekaż nowy pakiet NuGet (wersja) za pośrednictwem protokołu Endpoint push w wersji 2 
**Usuń** `/api/v2/package/{id}/{version}` | Klucz interfejsu API | 250 za godzinę | Wylistowanie pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2 
