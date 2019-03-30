---
title: Szablon adresu URL szczegóły pakietu, interfejs API programu NuGet
description: Szablon adresu URL szczegóły pakietu umożliwia klientom do wyświetlenia w ich interfejsu użytkownika sieci web link, aby uzyskać więcej szczegółów pakietu
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638088"
---
# <a name="package-details-url-template"></a>Szablon adresu URL szczegóły pakietu

Istnieje możliwość dla klientów utworzenie adresu URL, który może służyć przez użytkownika Aby wyświetlić więcej szczegółów pakietu w przeglądarce sieci web. Jest to przydatne, gdy chce wyświetlić dodatkowe informacje na temat pakietu, który może nie być dopasowane w zakresie aplikacji klienckiej NuGet pokazuje źródła pakietu.

Zasób, używana do tworzenia tego adresu URL jest `PackageDetailsUriTemplate` można znaleźć zasobu w [indeks usług](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@type Wartość                     | Uwagi
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Wersja początkowa

## <a name="url-template"></a>Szablon adresu URL

Adres URL dla następujący interfejs API jest wartością `@id` właściwości skojarzonej z jedną z wyżej wymienionych zasobów `@type` wartości.

## <a name="http-methods"></a>Metody HTTP

Mimo, że klient nie ma wysyłać żądania do adresu URL szczegóły pakietu w imieniu użytkownika, strony sieci web powinien obsługiwać `GET` metodę umożliwiającą kliknięty adres URL łatwo można otworzyć w przeglądarce sieci web.

## <a name="construct-the-url"></a>Skonstruuj adres URL

Podany identyfikator znanych pakietu i wersję, implementacji klienta można skonstruować adres URL umożliwiający dostęp do interfejsu sieci web. Implementacja klienta powinien być wyświetlany ten utworzony adres URL (lub łączem) użytkowników, umożliwiając im Otwórz przeglądarkę sieci web do adresu URL i Dowiedz się więcej o pakiecie. Zawartość na stronie szczegółów pakietu jest określany przez implementację serwera.

Adres URL musi być bezwzględnym adresem URL i schematu (protokół) muszą być adresami HTTPS.

Wartość `@id` w usłudze indeks jest zawierające dowolne z następujących znaczników symbolu zastępczego ciągu adresu URL:

### <a name="url-placeholders"></a>Symbole zastępcze adresu URL

Nazwa        | Typ    | Wymagane | Uwagi
----------- | ------- | -------- | -----
`{id}`      | string  | Brak       | Identyfikator pakietu, aby uzyskać szczegółowe informacje dla
`{version}` | string  | Brak       | Wersja pakietu, aby uzyskać szczegółowe informacje dla

Serwer powinien akceptować `{id}` i `{version}` wartości za pomocą dowolnej wielkości liter. Ponadto serwer nie powinien być wrażliwe na wersja jest [znormalizowane](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). Innymi słowy, serwer powinien akceptować także zaakceptować nieznormalizowanego wersji.

Na przykład szablon szczegóły pakietu usługi nuget.org wygląda następująco:

    https://www.nuget.org/packages/{id}/{version}

Jeśli implementacji klienta wymaga wyświetlone łącze do szczegółów pakietu dla NuGet.Versioning 4.3.0, czy to w efekcie następujący adres URL i przekazać go do użytkownika:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
