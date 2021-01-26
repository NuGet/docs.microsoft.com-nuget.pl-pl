---
title: Żądania danych użytkownika
description: Zasady żądania eksportu i usuwania danych użytkownika
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775728"
---
# <a name="user-data-requests"></a>Żądania danych użytkownika

nuget.org użytkownicy mogą przesyłać żądania usunięcia informacji oraz żądania eksportu informacji za poorednictwem [NuGet.org](https://www.nuget.org). Oba typy są przesyłane w formie żądań pomocy technicznej i są wykonywane przez administratorów nuget.org w ciągu 30 dni.

Następujące dane użytkownika są bezpośrednio dostępne za pomocą nuget.org:

* Dane dotyczące konta, takie jak adres e-mail, konto logowania, obraz profilu i ustawienia powiadomień e-mail
* Posiadane klucze interfejsu API
* Lista posiadanych pakietów

Te dane nie są uwzględniane w danych wyeksportowanych przez żądanie obsługi.

## <a name="identifying-customer-data"></a>Identyfikowanie danych klienta

Dane klienta można zidentyfikować jako nazwy kont użytkowników nuget.org.

## <a name="deleting-customer-data"></a>Usuwanie danych klienta

Aby zażądać usunięcia danych użytkownika z nuget.org:

1. Użytkownik musi zalogować się do [NuGet.org](https://www.nuget.org)
1. Użytkownik musi przesłać żądanie usunięcia konta [NuGet.org/Account/Delete](https://www.nuget.org/account/delete)

Użytkownicy, którzy są jedynymi właścicielami pakietów, są zachęcani do znajdowania nowych właścicieli przed zapytaniem, czy konto zostało usunięte. Jeśli własność pakietu nie zostanie przetransferowana, pakiet NuGet nie zostanie wystawiony i w związku z tym nie jest już dostępny w zapytaniach wyszukiwania w programie Visual Studio ani w witrynie sieci Web nuget.org. Przed usunięciem konta Administratorzy nuget.org współpracują z użytkownikiem, aby znaleźć nowych właścicieli dla pakietów, których są właścicielami.

Akcja usuwania konta jest wykonywana przez administratora nuget.org w ciągu 30 dni od daty żądania.

Po usunięciu konta wszystkie dane użytkownika są usuwane z systemu nuget.org i są wykonywane następujące akcje:

* Usunięte konto zostanie wyrejestrowane z nuget.org
* Wszystkie należące do siebie klucze interfejsu API są usuwane
* Wszystkie zastrzeżone przestrzenie nazw są wydane
* Wszystkie prawa własności pakietu są usuwane

Należące do nich pakiety *nie* są usuwane. Mimo że nie są one wystawione na podstawie wyników wyszukiwania, są one dostępne za pośrednictwem przywracania pakietów do projektów, które są od nich zależne.

## <a name="exporting-customer-data"></a>Eksportowanie danych klienta

Po zalogowaniu się do nuget.org użytkownik może przesłać żądanie eksportu za pomocą [NuGet.org/policies/Contact](https://www.nuget.org/policies/Contact)

Dane eksportowane są udostępniane przez 48 godzin do użytkownika w celu pobrania przez obiekt blob platformy Azure. Po 48 godzinach dostępu wygasa i użytkownik musi przesłać nowe żądanie eksportu zgodnie z wymaganiami.

Eksportowane dane obejmują:

* Żądania obsługi użytkownika
* Akcje użytkownika (publikowanie pakietu, tworzenie konta) jako utrwalone w dziennikach inspekcji
* Wszelkie informacje o użytkowniku jako utrwalone w dziennikach usług IIS
