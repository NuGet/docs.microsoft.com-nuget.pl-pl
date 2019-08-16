---
title: Szablon adresu URL szczegółów pakietu, interfejs API NuGet
description: Szablon adresu URL szczegółów pakietu umożliwia klientom wyświetlanie w ich interfejsie użytkownika linku internetowego do większej liczby szczegółów pakietu
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 6657536ea6c699a834f57494c66b2a7d741dfcb7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488169"
---
# <a name="package-details-url-template"></a>Szablon adresu URL szczegółów pakietu

Jest możliwe, aby klient mógł utworzyć adres URL, który może być używany przez użytkownika, aby wyświetlić więcej szczegółów pakietu w swojej przeglądarce sieci Web. Jest to przydatne, gdy źródło pakietu chce wyświetlić dodatkowe informacje dotyczące pakietu, który może nie pasować do zakresu działania aplikacji klienckiej NuGet.

Zasób używany do kompilowania tego adresu URL jest `PackageDetailsUriTemplate` zasobem znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Są używane `@type` następujące wartości:

@typewartościami                     | Uwagi
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Początkowa wersja

## <a name="url-template"></a>Szablon adresu URL

Adres URL następującego interfejsu API to wartość `@id` właściwości skojarzonej z jedną z wymienionych powyżej wartości zasobów. `@type`

## <a name="http-methods"></a>Metody HTTP

Mimo że klient nie jest przeznaczony do żądania do adresu URL informacji o pakiecie w imieniu użytkownika, na stronie sieci Web powinna być obsługiwana `GET` Metoda zezwalająca na otwarcie klikniętego adresu URL w przeglądarce internetowej.

## <a name="construct-the-url"></a>Konstruowanie adresu URL

Po otrzymaniu znanego identyfikatora pakietu i wersji implementacja klienta może utworzyć adres URL służący do uzyskiwania dostępu do interfejsu sieci Web. W implementacji klienta powinien być wyświetlany ten skonstruowany adres URL (lub link do kliknięcia), dzięki któremu użytkownicy mogą otworzyć przeglądarkę internetową pod adresem URL i dowiedzieć się więcej na temat pakietu. Zawartość strony Szczegóły pakietu jest określana przez implementację serwera.

Adres URL musi być bezwzględnym adresem URL, a schemat (protokół) musi być HTTPS.

Wartość `@id` w indeksie usługi jest ciągiem adresu URL zawierającym dowolny z następujących tokenów zastępczych:

### <a name="url-placeholders"></a>Symbole zastępcze adresu URL

Nazwa        | Typ    | Wymagane | Uwagi
----------- | ------- | -------- | -----
`{id}`      | string  | znaleziono       | Identyfikator pakietu, dla którego mają zostać pobrane szczegóły
`{version}` | string  | znaleziono       | Wersja pakietu, dla której mają zostać pobrane szczegóły

Serwer powinien akceptować `{id}` wartości `{version}` i zawierać dowolne wielkości liter. Ponadto serwer nie powinien być wrażliwy na to, czy wersja jest [znormalizowana](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers). Innymi słowy, serwer powinien akceptować również nieznormalizowane wersje.

Na przykład szablon Details programu NuGet. org wygląda następująco:

    https://www.nuget.org/packages/{id}/{version}

Jeśli implementacja klienta musi wyświetlić link do szczegółów pakietu NuGet. przechowywanie wersji 4.3.0, spowoduje to utworzenie następującego adresu URL i udostępnienie go użytkownikowi:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
