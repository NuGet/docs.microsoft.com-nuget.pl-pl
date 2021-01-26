---
title: Szablon adresu URL zgłaszania nadużycia, interfejs API NuGet
description: Szablon adresu URL niezgodnego raportu umożliwia klientom wyświetlanie linku nadużycia raportu w ich interfejsie użytkownika.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775223"
---
# <a name="report-abuse-url-template"></a>Szablon adresu URL zgłaszania nadużycia

Jest możliwe, aby klient mógł utworzyć adres URL, który może być używany przez użytkownika do zgłaszania nadużycia określonego pakietu. Jest to przydatne, gdy źródło pakietu chce włączyć wszystkie środowiska klienta (nawet inne firmy) do delegowania nadużycia raportów do źródła pakietu.

Zasób używany do kompilowania tego adresu URL jest `ReportAbuseUriTemplate` zasobem znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

`@type`Są używane następujące wartości:

@type wartościami                       | Uwagi
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0 — beta | Początkowa wersja
ReportAbuseUriTemplate/3.0.0-RC   | Alias `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Szablon adresu URL

Adres URL następującego interfejsu API to wartość `@id` Właściwości skojarzonej z jedną z wymienionych powyżej `@type` wartości zasobów.

## <a name="http-methods"></a>Metody HTTP

Mimo że klient nie jest przeznaczony do żądania do adresu URL niezgodnego z raportem w imieniu użytkownika, Strona sieci Web powinna obsługiwać `GET` metodę, aby można było łatwo otworzyć kliknięty adres URL w przeglądarce sieci Web.

## <a name="construct-the-url"></a>Konstruowanie adresu URL

Po otrzymaniu znanego identyfikatora pakietu i wersji implementacja klienta może utworzyć adres URL służący do uzyskiwania dostępu do interfejsu sieci Web. W implementacji klienta powinien być wyświetlany ten skonstruowany adres URL (lub link z możliwością kliknięcia), dzięki któremu użytkownicy mogą otworzyć przeglądarkę sieci Web pod adresem URL i wprowadzić wszelkie niezbędne raporty dotyczące nadużycia. Implementacja formularza raportu nadużycia jest określana przez implementację serwera.

Wartość parametru `@id` jest ciągiem adresu URL zawierającym dowolny z następujących tokenów zastępczych:

### <a name="url-placeholders"></a>Symbole zastępcze adresu URL

Nazwa        | Typ    | Wymagane | Uwagi
----------- | ------- | -------- | -----
`{id}`      | ciąg  | nie       | Identyfikator pakietu służący do zgłaszania nadużycia
`{version}` | ciąg  | nie       | Wersja pakietu do zgłaszania nadużycia

`{id}`Wartości i `{version}` interpretowane przez implementację serwera muszą być bez uwzględniania wielkości liter i nie są poufne dla tego, czy wersja jest znormalizowana.

Na przykład szablon nieużywający raportów programu NuGet.

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Jeśli implementacja klienta musi wyświetlić link do formularza nadużycia w raporcie dla NuGet. przechowywanie wersji 4.3.0, spowoduje to utworzenie następującego adresu URL i udostępnienie go użytkownikowi:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
