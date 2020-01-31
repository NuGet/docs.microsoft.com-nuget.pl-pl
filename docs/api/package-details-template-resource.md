---
title: Szablon adresu URL szczegółów pakietu, interfejs API NuGet
description: Szablon adresu URL szczegółów pakietu umożliwia klientom wyświetlanie w ich interfejsie użytkownika linku internetowego do większej liczby szczegółów pakietu
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812938"
---
# <a name="package-details-url-template"></a>Szablon adresu URL szczegółów pakietu

Jest możliwe, aby klient mógł utworzyć adres URL, który może być używany przez użytkownika, aby wyświetlić więcej szczegółów pakietu w swojej przeglądarce sieci Web. Jest to przydatne, gdy źródło pakietu chce wyświetlić dodatkowe informacje dotyczące pakietu, który może nie pasować do zakresu działania aplikacji klienckiej NuGet.

Zasób używany do kompilowania tego adresu URL jest zasobem `PackageDetailsUriTemplate` znalezionym w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące wartości `@type` są używane:

wartość @type                     | Uwagi
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Początkowa wersja

## <a name="url-template"></a>Szablon adresu URL

Adres URL następującego interfejsu API to wartość właściwości `@id` skojarzona z jedną z powyższych wartości `@type` zasobów.

## <a name="http-methods"></a>Metody HTTP

Mimo że klient nie jest przeznaczony do żądania do adresu URL szczegółów pakietu w imieniu użytkownika, Strona sieci Web powinna obsługiwać metodę `GET`, aby umożliwić otwieranie adresu URL w przeglądarce internetowej.

## <a name="construct-the-url"></a>Konstruowanie adresu URL

Po otrzymaniu znanego identyfikatora pakietu i wersji implementacja klienta może utworzyć adres URL służący do uzyskiwania dostępu do interfejsu sieci Web. W implementacji klienta powinien być wyświetlany ten skonstruowany adres URL (lub link do kliknięcia), dzięki któremu użytkownicy mogą otworzyć przeglądarkę internetową pod adresem URL i dowiedzieć się więcej na temat pakietu. Zawartość strony Szczegóły pakietu jest określana przez implementację serwera.

Adres URL musi być bezwzględnym adresem URL, a schemat (protokół) musi być HTTPS.

Wartość `@id` w indeksie usługi jest ciągiem adresu URL zawierającym dowolny z następujących tokenów zastępczych:

### <a name="url-placeholders"></a>Symbole zastępcze adresu URL

Nazwa        | Typ    | Wymagane | Uwagi
----------- | ------- | -------- | -----
`{id}`      | string  | Znaleziono       | Identyfikator pakietu, dla którego mają zostać pobrane szczegóły
`{version}` | string  | Znaleziono       | Wersja pakietu, dla której mają zostać pobrane szczegóły

Serwer powinien akceptować `{id}` i `{version}` wartości przy użyciu dowolnej wielkości liter. Ponadto serwer nie powinien być wrażliwy na to, czy wersja jest [znormalizowana](../concepts/package-versioning.md#normalized-version-numbers). Innymi słowy, serwer powinien akceptować również nieznormalizowane wersje.

Na przykład szablon Details programu NuGet. org wygląda następująco:

    https://www.nuget.org/packages/{id}/{version}

Jeśli implementacja klienta musi wyświetlić link do szczegółów pakietu NuGet. przechowywanie wersji 4.3.0, spowoduje to utworzenie następującego adresu URL i udostępnienie go użytkownikowi:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
