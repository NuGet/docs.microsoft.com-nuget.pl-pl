---
title: Żądania danych użytkownika
description: Zasady dla żądania eksportu danych użytkownika i delete
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/04/2018
ms.locfileid: "33086218"
---
# <a name="user-data-requests"></a>Żądania danych użytkownika

nuget.org użytkownicy mogą przesyłać żądania usunięcia informacji i żądań eksportu informacji za pośrednictwem [nuget.org](https://www.nuget.org). Oba typy są przesyłane w formie obsługę żądań i są wykonywane przez administratorów nuget.org w ciągu 30 dni.

Następujące dane użytkownika jest bezpośrednio dostępny za pośrednictwem nuget.org:

* Dane, takie jak adres e-mail, konto logowania obraz profilu i ustawień powiadomień e-mail związanych z kontem
* Klucze należących do interfejsu API
* Lista pakietów należące do firmy

Te dane nie jest uwzględniony w dane wyeksportowane za pomocą żądania pomocy technicznej.

## <a name="identifying-customer-data"></a>Identyfikowanie danych klienta

Dane klienta może być zidentyfikowany jako nazwy kont użytkowników nuget.org.

## <a name="deleting-customer-data"></a>Usuwanie danych klienta

Żądanie usuwania danych użytkownika z nuget.org:

1. Użytkownik musi zalogować się do [nuget.org](https://www.nuget.org)
1. Użytkownik musi przesłać żądanie dla swojego konta do usunięcia [nuget.org/account/delete](https://www.nuget.org/account/delete)

Użytkownicy, którzy są jedynymi właścicielami pakietów zaleca się znaleźć właścicieli nowej przed zapytaniem, jego konto usunięte. Jeśli własność pakietu nie został przeniesiony, pakiet NuGet jest nieznajdujące się na liście, i w związku z tym nie jest już dostępne w zapytaniach wyszukiwania w programie Visual Studio lub w witrynie sieci Web nuget.org. Przed usunięciem konta, Administratorzy nuget.org pracują z użytkownika o znalezienie właścicieli nowych pakietów, w których są właścicielami.

Akcja usuwania konta zostało zakończone przez administratora nuget.org w ciągu 30 dni od daty żądania.

Po usunięciu konta jest usunięte wszystkie dane użytkownika z systemu nuget.org i są podejmowane następujące akcje:

* Usunięto konto staje się wyrejestrować z nuget.org
* Wszystkie należące do kluczy interfejsu API są usuwane.
* Wszystkie zastrzeżone przestrzenie nazw są wydawane
* Zostaną usunięte wszystkie własność pakietu

Pakiety należące do firmy są *nie* usunięte. Chociaż nieznajdujące się na liście wyników wyszukiwania, pozostają dostępne za pośrednictwem Przywracanie pakietu do projektów, które zależą od nich.

## <a name="exporting-customer-data"></a>Eksportowanie danych klienta

Po zalogowaniu do nuget.org, użytkownik może przesłać żądanie eksportu za pośrednictwem [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Dane wyeksportowane ma zostać udostępnione w ciągu 48 godzin dla użytkownika do pobrania za pośrednictwem obiektów Blob platformy Azure. Po 48 godzin dostępu wygasa, a użytkownik musi przesłać nowe żądanie eksportu, zgodnie z potrzebami.

Wyeksportowane dane obejmują:

* Żądania pomocy technicznej przez użytkownika
* Akcje użytkownika (opublikować pakietu, Utwórz konto) jako utrwalone w dziennikach inspekcji
* Informacje o użytkowniku, jak utrwalone w dziennikach usług IIS
