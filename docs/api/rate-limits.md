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
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367937"
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

| Interfejs API | Typ limitu | Wartość limitu | Przypadek użycia interfejsu API |
|:---|:---|:---|:---|
**Pobierz**`/api/v1/Packages` | Adres IP | 1000/minutę | Wykonywanie zapytania dotyczącego metadanych pakietu NuGet za pomocą zbierania danych OData w wersji 1 `Packages` |
**Pobierz**`/api/v1/Search()` | Adres IP | 3000/minutę | Wyszukaj pakiety NuGet za pomocą punktu końcowego wyszukiwania v1 | 
**Pobierz**`/api/v2/Packages` | Adres IP | 20000/minutę | Wysyłanie zapytań dotyczących metadanych pakietów NuGet za pomocą zbierania danych OData w wersji 2 `Packages` | 
**Pobierz**`/api/v2/Packages/$count` | Adres IP | 100/minutę | Wykonaj zapytania o liczbę pakietów NuGet za pomocą zbierania danych OData w wersji 2 `Packages` | 

## <a name="package-push-and-unlist"></a>Wypychanie pakietów i wylistowanie

| Interfejs API | Typ limitu | Wartość limitu | Przypadek użycia interfejsu API | 
|:---|:---|:---|:--- |
**Umieść**`/api/v2/package` | Klucz interfejsu API | 350 za godzinę | Przekaż nowy pakiet NuGet (wersja) za pośrednictwem protokołu Endpoint push w wersji 2 
**Usuń**`/api/v2/package/{id}/{version}` | Klucz interfejsu API | 250 za godzinę | Wylistowanie pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2 

## <a name="nugetorg-website-page-views"></a>nuget.org widoki stron witryny sieci Web

Jeśli uzyskujesz dostęp do stron sieci Web nuget.org programowo, rozważ badanie naszych udokumentowanych [interfejsów API v3](overview.md). Punkty końcowe umożliwiają łatwiejszy dostęp do metadanych i zawartości pakietu. Interfejs API v3 ma lepszą dostępność i ma wyższą wydajność niż dostęp do stron sieci Web galerii NuGet, które są przeznaczone do interakcji z przeglądarką sieci Web.

| Interfejs API | Typ limitu | Wartość limitu | Przypadek użycia interfejsu API | 
|:---|:---|:---|:--- |
**Pobierz**`/package/{id}/{version}` | Adres IP | 50/minutę | Strona szczegółów pakietu wyświetlania (wersja). 
