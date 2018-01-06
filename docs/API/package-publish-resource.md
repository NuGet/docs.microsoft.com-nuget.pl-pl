---
title: "Wypychanie i usunąć NuGet interfejsu API | Dokumentacja firmy Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Usługa publikowania zezwala klientom na publikowanie nowych pakietów i unlist lub usunąć istniejące pakiety."
keywords: "Pakiet wypychania NuGet interfejsu API, interfejsu API NuGet usunąć pakiet, interfejsu API NuGet unlist pakietu NuGet API przekazywania pakietu, NuGet interfejsu API tworzenia pakietu"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 87970a701c63bce2b74c619069ec1d231ea77ab5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="push-and-delete"></a>Wypychanie i usuwania

Istnieje możliwość push, Usuń (lub unlist, w zależności od implementacji serwera) i ponownie wystaw pakiety przy użyciu interfejsu API programu NuGet w wersji 3. Operacje te są oparte na off z `PackagePublish` można znaleźć zasobu w [indeksu usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` jest używana wartość:

@typewartość          | Uwagi
-------------------- | -----
PackagePublish/2.0.0 | Początkowa wersja

## <a name="base-url"></a>Podstawowy adres URL

Bazowy adres URL dla następujących interfejsów API jest wartością `@id` właściwość `PackagePublish/2.0.0` zasobów w źródle pakietów [indeksu usługi](service-index.md). Poniżej dokumentację nuget.org adres URL jest używany. Należy wziąć pod uwagę `https://www.nuget.org/api/v2/package` jako symbol zastępczy `@id` wartość znajduje się w indeksie usługi.

Należy pamiętać, że ten adres URL wskazuje do tej samej lokalizacji co starszego punktu końcowego wypychania V2, ponieważ protokół jest taka sama.

## <a name="http-methods"></a>Metody HTTP

`PUT`, `POST` i `DELETE` metod HTTP obsługiwanych przez ten zasób. Dla metod, które są obsługiwane na każdym punkcie końcowym są wymienione poniżej.

## <a name="push-a-package"></a>Wypychanie pakietu

> [!Note]
> ma nuget.org [dodatkowe wymagania](NuGet-Protocols.md) do interakcji z punktem końcowym wypychania.

nuget.org obsługuje położenia nowe pakiety przy użyciu następujących interfejsu API. Jeśli pakiet o identyfikatorze podana i wersji już istnieje, nuget.org spowoduje odrzucenie powiadomienia wypychanego. Inne źródła pakietu może obsługiwać, zastępując istniejący pakiet.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ApiKey-X-NuGet | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

Klucz interfejsu API jest ciąg z ogólnym opisem zaakceptujesz ze źródła pakietów przez użytkownika i skonfigurowane do klienta. Nie określony ciąg formatu jest obowiązkowe, ale długość klucza interfejsu API nie może przekraczać uzasadnione rozmiaru dla wartości nagłówka HTTP.

### <a name="request-body"></a>Treść żądania

Treść żądania musi występować w następującym formacie:

#### <a name="multipart-form-data"></a>Wieloczęściowych danych formularza

Nagłówek żądania `Content-Type` jest `multipart/form-data` i raw bajtów .nupkg przekazywanej pierwszego elementu w treści żądania. Kolejne elementy treści wieloczęściowej wiadomości są ignorowane. Nazwa pliku lub inne nagłówki elementów wieloczęściowego są ignorowane.

### <a name="response"></a>Odpowiedź

Kod stanu | Znaczenie
----------- | -------
201, 202    | Pakiet został pomyślnie przypisany.
400         | Podany pakiet jest nieprawidłowy
409         | Pakiet o identyfikatorze podana i wersji już istnieje.

Implementacje serwera różnią się od kod stanu Powodzenie zwracany, gdy pakiet zostanie pomyślnie przeniesiona.

## <a name="delete-a-package"></a>Usuwanie pakietu

nuget.org interpretowane jako żądanie usunięcia pakietu jako "unlist". Oznacza to, że pakiet jest nadal dostępny dla istniejących konsumentów pakietu, ale pakiet nie będzie już wyświetlana w wynikach wyszukiwania lub interfejs sieci web. Aby uzyskać więcej informacji o tym rozwiązaniem, zobacz [usunięte pakiety](../policies/deleting-packages.md) zasad. Inne implementacje serwera mogą interpretować tego sygnału jako usuwania twardych, usunąć soft lub unlist. Na przykład [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (serwer obsługujący tylko starsze interfejsu API w wersji 2) obsługuje obsługi tego żądania jako unlist lub usuwania twardych, na podstawie opcji konfiguracji.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ID             | Adres URL    | string | Tak      | Identyfikator pakietu do usunięcia
WERSJA        | Adres URL    | string | Tak      | Wersja pakietu do usunięcia
ApiKey-X-NuGet | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Odpowiedź

Kod stanu | Znaczenie
----------- | -------
204         | Pakiet został usunięty.
404         | Nie pakietu z dostarczonych `ID` i `VERSION` istnieje

## <a name="relist-a-package"></a>Wystaw ponownie pakietu

Jeśli pakiet jest nieznajdujące się na liście, istnieje możliwość ponownie wyświetlić tego pakietu w wynikach wyszukiwania przy użyciu punktu końcowego "Wystaw ponownie". Ten punkt końcowy ma ten sam kształt co [usunąć (unlist) punktu końcowego](#delete-a-package) , ale `POST` HTTP zamiast metody `DELETE` metody.

Jeśli pakiet jest już na liście, żądanie nadal powiedzie się.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametry żądania

Nazwa           | W     | Typ   | Wymagane | Uwagi
-------------- | ------ | ------ | -------- | -----
ID             | Adres URL    | string | Tak      | Identyfikator pakietu do ponownego wystawienia
WERSJA        | Adres URL    | string | Tak      | Wersja pakietu do ponownego wystawienia
ApiKey-X-NuGet | nagłówek | string | Tak      | Na przykład:`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Odpowiedź

Kod stanu | Znaczenie
----------- | -------
204         | Pakiet zostanie wyświetlony
404         | Nie pakietu z dostarczonych `ID` i `VERSION` istnieje
