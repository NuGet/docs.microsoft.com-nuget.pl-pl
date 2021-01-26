---
title: Wypychanie i usuwanie, interfejs API NuGet
description: Usługa publikowania pozwala klientom na publikowanie nowych pakietów i usuwanie listy lub usunięcie istniejących pakietów.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773927"
---
# <a name="push-and-delete"></a>Wypychanie i usuwanie

Możliwe jest wypchnięcie, usunięcie (lub wycofanie listy, w zależności od implementacji serwera) i ponownie wystawianie pakietów przy użyciu interfejsu API programu NuGet v3. Operacje te są oparte na `PackagePublish` zasobach znalezionych w [indeksie usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

`@type`Używana jest następująca wartość:

@type wartościami          | Uwagi
-------------------- | -----
PackagePublish/2.0.0 | Początkowa wersja

## <a name="base-url"></a>Podstawowy adres URL

Podstawowy adres URL dla następujących interfejsów API jest wartością `@id` właściwości `PackagePublish/2.0.0` zasobu w [indeksie usługi](service-index.md)źródła pakietu. W poniższej dokumentacji znajduje się adres URL programu NuGet. org. Rozważmy `https://www.nuget.org/api/v2/package` jako symbol zastępczy dla `@id` wartości znalezionej w indeksie usługi.

Należy zauważyć, że ten adres URL wskazuje tę samą lokalizację co starszy punkt końcowy w wersji 2, ponieważ protokół jest taki sam.

## <a name="http-methods"></a>Metody HTTP

`PUT` `POST` `DELETE` Metody i są obsługiwane przez ten zasób. Dla których metod są obsługiwane w każdym punkcie końcowym, zobacz poniżej.

## <a name="push-a-package"></a>Wypchnij pakiet

> [!Note]
> nuget.org ma [dodatkowe wymagania](NuGet-Protocols.md) dotyczące współpracy z punktem końcowym wypychania.

nuget.org obsługuje wypychanie nowych pakietów przy użyciu poniższego interfejsu API. Jeśli pakiet o podanym IDENTYFIKATORze i wersji już istnieje, nuget.org odrzuci wypychanie. Inne źródła pakietów mogą obsługiwać zastąpienie istniejącego pakietu.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Nagłówek | ciąg | tak      | Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`

Klucz interfejsu API to nieprzezroczysty ciąg z źródła pakietu przez użytkownika i skonfigurowany na kliencie. Żaden określony format ciągu nie jest dozwolony, ale długość klucza interfejsu API nie może przekroczyć rozsądnego rozmiaru wartości nagłówka HTTP.

### <a name="request-body"></a>Treść żądania

Treść żądania musi mieć następującą formę:

#### <a name="multipart-form-data"></a>Wieloczęściowe dane formularza

Nagłówek żądania `Content-Type` jest `multipart/form-data` i pierwszy element w treści żądania to nieprzetworzone bajty NUPKG. Kolejne elementy w treści wieloczęściowej są ignorowane. Nazwa pliku lub wszystkie inne nagłówki elementów wieloczęściowych zostaną zignorowane.

### <a name="response"></a>Reakcja

Kod stanu | Znaczenie
----------- | -------
201, 202    | Pakiet został pomyślnie wypychany
400         | Podany pakiet jest nieprawidłowy
409         | Pakiet z podanym IDENTYFIKATORem i wersją już istnieje

Implementacje serwera różnią się w zależności od kodu stanu sukcesu zwracanego po pomyślnym wypchnięciu pakietu.

## <a name="delete-a-package"></a>Usuwanie pakietu

nuget.org interpretuje żądanie usunięcia pakietu jako "unlisting". Oznacza to, że pakiet jest nadal dostępny dla istniejących odbiorców pakietu, ale pakiet nie jest już wyświetlany w wynikach wyszukiwania ani w interfejsie sieci Web. Aby uzyskać więcej informacji na temat tego rozwiązania, zobacz zasady [usuwania pakietów](../nuget-org/policies/deleting-packages.md) . Inne implementacje serwera są bezpłatne, aby interpretować ten sygnał jako twarde usuwanie, usuwanie nietrwałe lub cofanie listy. Na przykład plik [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (implementacja serwera obsługująca tylko starszy interfejs API v2) obsługuje obsługę tego żądania jako nielistę lub trwałego usunięcia na podstawie opcji konfiguracji.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ID (Identyfikator)             | Adres URL    | ciąg | tak      | Identyfikator pakietu do usunięcia
WERSJA        | Adres URL    | ciąg | tak      | Wersja pakietu do usunięcia
X-NuGet-ApiKey | Nagłówek | ciąg | tak      | Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Reakcja

Kod stanu | Znaczenie
----------- | -------
204         | Pakiet został usunięty
404         | Nie ma pakietu z podanym elementem `ID` i `VERSION` istnieje

## <a name="relist-a-package"></a>Wystaw ponownie pakiet

Jeśli pakiet nie jest wyświetlany na liście, można go ponownie wyświetlić w wynikach wyszukiwania przy użyciu punktu końcowego "relist". Ten punkt końcowy ma ten sam kształt co [punkt końcowy Delete (unlisting)](#delete-a-package) , ale używa `POST` metody http zamiast `DELETE` metody.

Jeśli pakiet jest już wymieniony, żądanie nadal kończy się powodzeniem.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ID (Identyfikator)             | Adres URL    | ciąg | tak      | Identyfikator pakietu do wyświetlenia ponownie
WERSJA        | Adres URL    | ciąg | tak      | Wersja pakietu do wyświetlenia ponownie
X-NuGet-ApiKey | Nagłówek | ciąg | tak      | Na przykład `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Reakcja

Kod stanu | Znaczenie
----------- | -------
200         | Pakiet znajduje się teraz na liście
404         | Nie ma pakietu z podanym elementem `ID` i `VERSION` istnieje
