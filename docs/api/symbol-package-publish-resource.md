---
title: Wypychanie pakiety symboli, interfejs API programu NuGet | Dokumentacja firmy Microsoft
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Usługa publikowania pozwala klientom Opublikuj nowe pakiety symboli.
keywords: Pakiet programu NuGet interfejsu API wypychania symboli
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580453"
---
# <a name="push-symbol-packages"></a>Pakiety symboli wypychania

Istnieje możliwość wypychania symbole pakietów ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) przy użyciu interfejsu API programu NuGet w wersji 3.
Te operacje opierają się wylogować się z `SymbolPackagePublish` można znaleźć zasobu w [indeks usług](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` zostanie użyta wartość:

@type Wartość                 | Uwagi
--------------------        | -----
SymbolPackagePublish/4.9.0  | Wersja początkowa

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `SymbolPackagePublish/4.9.0` zasobów w źródle pakietu [indeks usług](service-index.md). Poniższą dokumentacją używany jest adres URL usługi nuget.org. Należy wziąć pod uwagę `https://www.nuget.org/api/v2/symbolpackage` jako symbol zastępczy `@id` znaleziono wartości w indeksie usługi.

## <a name="http-methods"></a>Metody HTTP

`PUT` Metoda HTTP jest obsługiwana przez ten zasób. 

## <a name="push-a-symbol-package"></a>Wypychanie pakiet symboli

nuget.org obsługuje wypychania nowego formatu pakiety symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) przy użyciu następujących interfejsu API. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Pakiety symboli o tym samym identyfikatorze i wersji można złożyć wiele razy. Pakiet symboli, zostanie odrzucone w następujących przypadkach.
- Pakiet o tej samej wersji i identyfikator nie istnieje.
- Pakiet symboli, o tym samym identyfikatorze i wersji został wypchnięty, ale nie został jeszcze opublikowany.
- Pakiet symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) jest nieprawidłowy (zobacz [symboli ograniczenia pakietu](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

Klucz interfejsu API to nieprzezroczysty ciąg uzyskane ze źródła pakietu przez użytkownika i skonfigurowane do klienta. Nie określonego ciągu formatu jest upoważnione, ale długość klucza interfejsu API nie może przekraczać rozmiaru uzasadnione wartości nagłówka HTTP.

### <a name="request-body"></a>Treść żądania

Treść żądania do wypychania symboli jest taka sama jak z treści żądania wypychanej pakietu (zobacz [wypychania pakietów i usuwania](package-publish-resource.md)). 

### <a name="response"></a>Odpowiedź

Kod stanu: | Znaczenie
----------- | -------
201         | Pakiet symboli pomyślnie został wypchnięty.
400         | Pakiet podana symboli jest nieprawidłowa.
401         | Użytkownik nie ma uprawnień do wykonania tej akcji.
404         | Nie ma odpowiedniego pakietu o identyfikatorze podana i wersji.
409         | Pakiet symboli z podanego Identyfikatora i wersją został wypchnięty, ale go nie jest jeszcze dostępna.
413         | Pakiet jest zbyt duży.

