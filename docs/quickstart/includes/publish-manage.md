---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495953"
---
W swoim profilu na nuget.org wybierz **pozycję Zarządzaj pakietami,** aby zobaczyć właśnie opublikowany profil. Otrzymasz również wiadomość e-mail z potwierdzeniem. Należy pamiętać, że może upłynąć trochę czasu, aby pakiet został zindeksowany i pojawił się w wynikach wyszukiwania, gdzie inni mogą go znaleźć. W tym czasie na stronie pakietu pojawi się poniższy komunikat:

![Ten pakiet nie został jeszcze zindeksowany. Pojawi się w wynikach wyszukiwania i będzie dostępny do zainstalowania/przywrócenia po zakończeniu indeksowania.](../media/QS_Create-03-NotIndexed.png)

I to wszystko. Właśnie opublikowano swój pierwszy pakiet NuGet, aby nuget.org, które inni deweloperzy mogą używać w swoich własnych projektach.

Jeśli w tym instruktażu utworzono pakiet, który w rzeczywistości nie jest przydatny (na przykład pakiet utworzony z pustą biblioteką klas), należy wycofać pakiet z *listy,* aby ukryć go w wynikach wyszukiwania:

1. Na nuget.org wybierz nazwę użytkownika (w prawym górnym rogu strony), a następnie wybierz pozycję **Zarządzaj pakietami**.

1. Znajdź pakiet, który chcesz odsunąć od listy w obszarze **Opublikowane** i wybierz ikonę kosza po prawej stronie:

    ![Ikona kosza wyświetlana dla aukcji pakietów na nuget.org](../media/qs_create-vs-03-trash-can.png)

1. Na następnej stronie wyczyść pole z etykietą **Lista (nazwa pakietu) w wynikach wyszukiwania** i wybierz pozycję **Zapisz:**

    ![Wyczyszczenie pola wyboru Lista dla pakietu na nuget.org](../media/qs_create-vs-04-unlist.png)