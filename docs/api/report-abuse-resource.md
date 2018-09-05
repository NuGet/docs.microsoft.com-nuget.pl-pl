---
title: Zgłoś nadużycie szablon adresu URL, interfejs API programu NuGet
description: Szablon adresu URL raportu nadużycie umożliwia klientom wyświetlane łącza zgłaszania nadużycia w jego interfejsie użytkownika.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549342"
---
# <a name="report-abuse-url-template"></a>Szablon adresu URL nadużycie raportu

Istnieje możliwość dla klientów utworzenie adresu URL, który może służyć przez użytkownika w celu Zgłoś nadużycie o określonym pakiecie. Jest to przydatne, gdy źródło pakietu chce umieszczenie wszystkich klienta (strona nawet 3) do delegowania nadużycie raporty do źródła pakietu.

Zasób, używana do tworzenia tego adresu URL jest `ReportAbuseUriTemplate` można znaleźć zasobu w [indeks usług](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@type Wartość                       | Uwagi
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | Wersja początkowa
ReportAbuseUriTemplate/3.0.0-rc   | Alias `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Szablon adresu URL

Adres URL dla następujący interfejs API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości.

## <a name="http-methods"></a>Metody HTTP

Mimo, że klient nie ma wysyłać żądania do adresu URL nadużycie raportu w imieniu użytkownika, strony sieci web powinien obsługiwać `GET` metodę umożliwiającą kliknięty adres URL łatwo można otworzyć w przeglądarce sieci web.

## <a name="construct-the-url"></a>Skonstruuj adres URL

Podany identyfikator znanych pakietu i wersję, implementacji klienta można skonstruować adres URL umożliwiający dostęp do interfejsu sieci web. Implementacja klienta powinien być wyświetlany ten utworzony adres URL (lub łączem) użytkowników, umożliwiając im Otwórz przeglądarkę sieci web do adresu URL i dowolny raport nadużycie niezbędne. Implementacja nadużycie formularz raportu jest określany przez implementację serwera.

Wartość `@id` jest zawierające dowolne z następujących znaczników symbolu zastępczego ciągu adresu URL:

### <a name="url-placeholders"></a>Symbole zastępcze adresu URL

Nazwa        | Typ    | Wymagane | Uwagi
----------- | ------- | -------- | -----
`{id}`      | string  | Brak       | Identyfikator pakietu w celu Zgłoś nadużycie odnośnie do
`{version}` | string  | Brak       | Wersja pakietu, który ma być Zgłoś nadużycie odnośnie do

`{id}` i `{version}` wartości interpretowane przez implementację serwera musi być bez uwzględniania wielkości liter i nie wrażliwe na tego, czy wersja jest znormalizować.

Na przykład szablon nadużycie raportu usługi nuget.org wygląda następująco:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Jeśli implementacji klienta wymaganych, aby wyświetlić łącza do formularza nadużycie raportu dla NuGet.Versioning 4.3.0, czy to w efekcie następujący adres URL i przekazać go do użytkownika:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
