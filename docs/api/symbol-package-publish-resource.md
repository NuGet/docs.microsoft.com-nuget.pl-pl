---
title: Pakiety symboli wypychania, interfejs API NuGet | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Usługa publikowania pozwala klientom publikować nowe pakiety symboli.
keywords: Pakiet symboli wypychanych interfejsu API NuGet
ms.reviewer: karann
ms.openlocfilehash: bd4a10cc976c9d0775a63cfe61c35327c196065c
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738880"
---
# <a name="push-symbol-packages"></a>Pakiety symboli wypychania

Można wypchnąć pakiety symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) za pomocą interfejsu API programu NuGet v3.
Operacje te są oparte na `SymbolPackagePublish` zasobach znalezionych w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

`@type`Używana jest następująca wartość:

@type wartościami                 | Uwagi
--------------------        | -----
SymbolPackagePublish/4.9.0  | Początkowa wersja

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości `SymbolPackagePublish/4.9.0` zasobu w [indeksie usługi](service-index.md)źródła pakietu. W poniższej dokumentacji znajduje się adres URL programu NuGet. org. Rozważmy `https://www.nuget.org/api/v2/symbolpackage` jako symbol zastępczy dla `@id` wartości znalezionej w indeksie usługi.

## <a name="http-methods"></a>Metody HTTP

`PUT`Metoda http jest obsługiwana przez ten zasób. 

## <a name="push-a-symbol-package"></a>Wypchnij pakiet symboli

nuget.org obsługuje wypychanie nowych formatów symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) przy użyciu poniższego interfejsu API. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Pakiety symboli o takim samym IDENTYFIKATORze i wersji mogą być przesyłane wiele razy. Pakiet symboli zostanie odrzucony w następujących przypadkach.
- Pakiet o takim samym IDENTYFIKATORze i wersji nie istnieje.
- Pakiet symboli o takim samym IDENTYFIKATORze i wersji został wypchnięte, ale nie został jeszcze opublikowany.
- Pakiet symboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) jest nieprawidłowy (zobacz [ograniczenia pakietu symboli](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Nagłówek | ciąg | tak      | Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`

Klucz interfejsu API to nieprzezroczysty ciąg z źródła pakietu przez użytkownika i skonfigurowany na kliencie. Żaden określony format ciągu nie jest dozwolony, ale długość klucza interfejsu API nie może przekroczyć rozsądnego rozmiaru wartości nagłówka HTTP.

### <a name="request-body"></a>Treść żądania

Treść żądania odnoszącego się do wypchnięcia symbol jest taka sama jak w przypadku treści żądania wypychania pakietu (zobacz [wypychanie i usuwanie pakietu](package-publish-resource.md)). 

### <a name="response"></a>Reakcja

Kod stanu | Znaczenie
----------- | -------
201         | Pakiet symboli został pomyślnie wypchnięci.
400         | Podany pakiet symboli jest nieprawidłowy.
401         | Użytkownik nie ma autoryzacji do wykonania tej akcji.
404         | Odpowiedni pakiet o podanym IDENTYFIKATORze i wersji nie istnieje.
409         | Pakiet symboli o podanym IDENTYFIKATORze i wersji został wypchnięte, ale nie jest jeszcze dostępny.
413         | Pakiet jest zbyt duży.

