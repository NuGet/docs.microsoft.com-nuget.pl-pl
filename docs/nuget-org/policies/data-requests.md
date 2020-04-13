---
title: Żądania danych użytkownika
description: Zasady żądania eksportowania i usuwania danych użytkownika
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427513"
---
# <a name="user-data-requests"></a>Żądania danych użytkownika

nuget.org użytkownicy mogą przesyłać żądania usuwania informacji i żądania eksportu informacji za pośrednictwem [nuget.org](https://www.nuget.org). Oba typy są przesyłane w formie żądań pomocy technicznej i są wykonywane przez administratorów nuget.org w ciągu 30 dni.

Następujące dane użytkownika są bezpośrednio dostępne za pośrednictwem nuget.org:

* Dane związane z kontem, takie jak adres e-mail, konto logowania, zdjęcie profilowe i ustawienia powiadomień e-mail
* Posiadane klucze interfejsu API
* Lista posiadanych pakietów

Te dane nie są uwzględniane w danych eksportowanych za pośrednictwem żądania pomocy technicznej.

## <a name="identifying-customer-data"></a>Identyfikowanie danych klientów

Dane klientów można zidentyfikować jako nuget.org nazwy kont użytkowników.

## <a name="deleting-customer-data"></a>Usuwanie danych klienta

Aby zażądać usunięcia danych użytkownika z nuget.org:

1. Użytkownik musi zalogować się do [nuget.org](https://www.nuget.org)
1. Użytkownik musi przesłać żądanie usunięcia swojego konta [nuget.org/account/delete](https://www.nuget.org/account/delete)

Użytkownicy, którzy są jedynymi właścicielami pakietów, są zachęcani do znalezienia nowych właścicieli przed prośbą o usunięcie konta. Jeśli własność pakietu nie jest przenoszona, pakiet NuGet jest niepubliczny i w rezultacie nie jest już dostępny w kwerendach wyszukiwania w programie Visual Studio lub w nuget.org stronie internetowej. Przed usunięciem konta administratorzy nuget.org współpracują z użytkownikiem w celu znalezienia nowych właścicieli pakietów, których są właścicielami.

Akcja usuwania konta jest wypełniana przez administratora nuget.org w ciągu 30 dni od daty żądania.

Po usunięciu konta wszystkie dane użytkownika zostaną usunięte z systemu nuget.org i podejmowane są następujące czynności:

* Usunięte konto zostanie wyrejestrowane za pomocą nuget.org
* Wszystkie posiadane klucze interfejsu API są usuwane
* Wszystkie zarezerwowane przestrzenie nazw są zwalniane
* Wszelkie własności pakietu są usuwane

Posiadane pakiety *nie* są usuwane. Mimo że nie są one publikowane w wynikach wyszukiwania, pozostają dostępne za pośrednictwem przywracania pakietu do projektów, które od nich zależą.

## <a name="exporting-customer-data"></a>Eksportowanie danych klientów

Po zalogowaniu się do nuget.org użytkownik może przesłać żądanie eksportu za pośrednictwem [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Eksportowane dane są udostępniane przez 48 godzin użytkownikowi do pobrania za pośrednictwem obiektu blob platformy Azure. Po 48 godzinach dostęp wygasa, a użytkownik musi przesłać nowe żądanie eksportu w razie potrzeby.

Wyeksportowane dane obejmują:

* Żądania pomocy technicznej użytkownika
* Akcje użytkownika (publikuj pakiet, utwórz konto) w dziennikach inspekcji
* Wszelkie informacje o użytkowniku, które zostały utrwalone w dziennikach usługi IIS
