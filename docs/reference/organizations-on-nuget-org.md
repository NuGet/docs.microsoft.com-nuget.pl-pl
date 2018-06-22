---
title: Organizacje na nuget.org
description: Organizacje na nuget.org pomaga w zakresie zarządzania pakietami opublikowane przez grupę lub w zespole, środowisko firmy.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449581"
---
# <a name="organization-on-nugetorg"></a>Organizacji na nuget.org

Organizacje włączyć w firmach i open source projekty, współpracować nad pakiety przy użyciu tożsamości jednym nuget.org. Konsument pakietu konta organizacji wyświetlany jest taki sam jak istniejącego konta użytkownika na nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Konta użytkowników, a konta organizacji

Twoje konto użytkownika jest Twoją tożsamość na nuget.org i może być członkiem dowolnej liczby organizacji. Pakiet może należeć do konta organizacji, jak mogą należeć do konta użytkownika. Pakiet nie widzieli różnicę między konta użytkownika lub konta organizacji: znajdować się w pakiecie `owners`.

Konta organizacji ma co najmniej jednego konta użytkowników jako elementy członkowskie. Elementy te można zarządzać zestaw pakietów przy zachowaniu jednej tożsamości dla prawa własności.

## <a name="adding-a-new-organization"></a>Dodawanie nowej organizacji

Aby dodać nową organizację, wybierz konto na nuget.org, a następnie wybierz **zarządzanie organizacji...**  polecenie:

![Opcja menu na nuget.org dla organizacji Manager](media/org-manage-option.png)

Na następnej stronie wybierz **Dodaj nową organizację** przycisk:

![Przycisk, aby utworzyć nową organizację na nuget.org](media/org-add-new-option.png)

Na następnej stronie Podaj adres nazwę i adres e-mail organizacji. Ponieważ konta organizacji używają tego samego obszaru nazw jako konta użytkownika, nazwę organizacji musi się różnić od innych istniejącą organizację lub kont użytkowników. Adres e-mail musi być unikatowa również we wszystkich kont.

![Dodaj nową stronę organizacji na nuget.org](media/org-add-new-page.png)

Po utworzeniu konta organizacji jest administratorem i można przesłać pakiety do organizacji i dodać członków organizacji.

### <a name="transform-existing-account-to-an-organization"></a>Przekształcanie istniejącego konta organizacji

> [!Warning]
> Konwersja konta jest nieodwracalne: nie można przekształcić organizacji do konta użytkownika.

Jeśli w przypadku zarządzania pakietami w zespole za pomocą jednego konta użytkownika, a chcesz konwertować tego konta organizacji, użyj **Przekształcenie konta organizacji** opcja **zarządzanie organizacji** strony:

![Opcja na nuget.org do przekształcania istniejącego konta organizacji](media/org-transform-option.png)

Na następnej stronie podaj inne konto użytkownika do przypisania jako administrator w organizacji, a następnie wybierz **przekształcenie**.

![Wprowadzanie informacji do przekształcania konto użytkownika w organizacji](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Zarządzanie członków organizacji

Jako administrator w organizacji, możesz dodawać członków, zapewniając nuget.org każdy element członkowski *nazwę konta użytkownika*; nie można używać adresów e-mail. Następnie oznaczenie każdy element członkowski jako współautor lub administrator z następującymi uprawnieniami:

| Uprawnienie | Współautor | Administrator |
| --- | --- | --- |
| Zarządzaj pakietami organizacji<br/>(przesyłanie nowych pakietów, aktualizacji lub unlist istniejące pakiety) | Tak | Tak |
| Zmiana metadanych organizacji<br/>(adres e-mail, ustawienia powiadomień) | Nie | Tak |
| Zarządzanie członków organizacji | Nie | Tak |
| Żądanie lub działać w odpowiedzi na żądania co-ownership pakietów organizacji | Nie | Tak |

## <a name="managing-packages"></a>Zarządzanie pakietami

Wszystkie pakiety można wyświetlić na Twoje konto i wszystkich organizacji, w których jesteś członkiem na [Zarządzaj pakietami](https://www.nuget.org/account/Packages) strony. Aby wyświetlić specyficzne dla swojego konta lub dowolnego organizację określonych pakietów, użyj filtru konta u góry po prawej części strony.

![Zarządzanie pakietami z filtrem konta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transferu pakietów do organizacji
Jeśli chcesz przenieść niektórych pakietów do nowo utworzonej organizacji, możesz to zrobić przez żądania konta organizacji, aby wspólnie właścicielem pakietu i usuwanie siebie jako właściciela. Jeśli jesteś administratorem organizacji nie ma żadnych potwierdzenie, należy zaakceptować własności. Jednak w przypadku współpracownika dodawania organizacji jako właściciela wymaga jednego z administratorami w celu akceptowania własności.

## <a name="publishing-packages"></a>Publikowanie pakietów

Publikuj pakiety w organizacji, takich jak opublikować pakietów z kontem użytkownika: przekazując bezpośrednio pakietu do nuget.org lub przesyłając pakietu za pomocą `nuget push` lub `dotnet nuget push` polecenia interfejsu wiersza polecenia.

### <a name="uploading-packages"></a>Przekazywanie pakietów

Jeśli możesz bezpośrednio przekazać nowy pakiet na [nuget.org przekazywania](https://www.nuget.org/packages/manage/upload) strony, możesz przypisać właściciela pakietu na konto użytkownika lub organizację:

![Przekaż pakiet z opcją konta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Przy użyciu kluczy interfejsu API

Do dystrybuowania pakietu za pomocą `nuget push` lub `dotnet nuget push` polecenia interfejsu wiersza polecenia, należy uzyskać klucz interfejsu API wymagane przez tych poleceń. Aby uzyskać więcej informacji, zobacz [opublikowania pakietu](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Podczas tworzenia nowego klucza interfejsu API, wybierz odpowiednie organizacji w **właściciela pakietu** listy rozwijanej. Klucz interfejsu API, wszystkie utworzone ma zastosowanie tylko do wybranych organizacji:

![Klucz interfejsu API z opcji konta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Usuwanie organizacji

Jako użytkownik, możesz usunąć siebie z organizacji, wybierając `X` przycisk wyświetlane przez członkostwo w danej organizacji:

![Usuwanie konta użytkownika z organizacji](media/org-remove-self-option.png)

Administratorzy mogą usunąć członków z organizacji, w tym innych administratorów. Jeśli jesteś jedynym administratorem dla organizacji, nie możesz usunąć siebie, chyba że dodasz innego elementu członkowskiego jako administrator.

### <a name="deleting-an-organization-account"></a>Usunięcie konta organizacji

Ta funkcja będzie dostępna wkrótce.
