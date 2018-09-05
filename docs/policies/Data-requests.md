---
title: Żądania danych użytkownika
description: Zasady dla żądania eksportu danych użytkownika i Usuń
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548057"
---
# <a name="user-data-requests"></a>Żądania danych użytkownika

nuget.org, użytkownicy będą mogli wysyłać żądania usunięcia informacji i żądań eksportu informacji za pośrednictwem [nuget.org](https://www.nuget.org). Oba typy są przesyłane w formie obsługę żądań i są wykonywane przez administratorów nuget.org w ciągu 30 dni.

Następujące dane użytkownika są bezpośrednio dostępne za pośrednictwem nuget.org:

* Konto powiązanych danych, takich jak adres e-mail konta logowania, zdjęcie profilowe i ustawienia powiadomień e-mail
* Klucze interfejsu API należące do firmy
* Lista pakietów należące do firmy

Te dane nie są objęte dane wyeksportowane za pomocą żądania pomocy technicznej.

## <a name="identifying-customer-data"></a>Identyfikowanie danych klienta

Dane klienta mogą zostać określone jako nazwy kont użytkowników w witrynie nuget.org.

## <a name="deleting-customer-data"></a>Usuwanie danych klienta

Aby zażądać usuwania danych użytkownika z witryny nuget.org:

1. Użytkownik musi zalogować się do [nuget.org](https://www.nuget.org)
1. Użytkownik musi przesłać żądanie do swojego konta do usunięcia [nuget.org/account/delete](https://www.nuget.org/account/delete)

Użytkownicy, którzy są właścicielami jedyny pakietów zaleca się znaleźć nowym właścicielom przed zadaniem ich konta usunięte. Jeśli własność pakietu nie są przesyłane, pakiet NuGet jest nieznajdujące się na liście, i w rezultacie nie jest już dostępna w zapytaniach wyszukiwania w programie Visual Studio lub w witrynie nuget.org. Przed usunięciem konta administratorów nuget.org pracować użytkownika o znalezienie nowym właścicielom pakietów, które są właścicielami.

Nuget.org administrator wykonać akcję usuwania konta w ciągu 30 dni od daty żądania.

Po usunięciu konta jest usunięte wszystkie dane użytkownika z systemu nuget.org, i są podejmowane następujące akcje:

* Usunięte konto staje się wyrejestrować z repozytorium nuget.org
* Wszystkie należące do kluczy interfejsu API są usuwane.
* Wszystkie obszary nazw zastrzeżonych zostaną zwolnione.
* Własność dowolnego pakietu są usuwane.

Pakiety należące do firmy są *nie* usunięte. Chociaż nieznajdujące się na liście wyników wyszukiwania, pozostają dostępne za pośrednictwem Przywracanie pakietu do projektów, które zależą od nich.

## <a name="exporting-customer-data"></a>Eksportowanie danych klienta

Po zalogowaniu się w witrynie nuget.org, użytkownik może przesłać żądanie eksportu za pośrednictwem [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Eksportowanie danych ma zostać udostępnione w ciągu 48 godzin do użytkownika do pobrania za pośrednictwem obiektu Blob platformy Azure. Po upływie 48 godzin dostępu wygasa, a użytkownik musi przesłać nowe żądanie eksportu, zgodnie z potrzebami.

Wyeksportowane dane obejmują:

* Żądania pomocy technicznej przez użytkownika
* Czynności wykonywanych przez użytkownika (publikowanie pakietu, Utwórz konto) jako utrwalone w dziennikach inspekcji
* Informacje o użytkowniku jako utrwalone w dziennikach usług IIS
