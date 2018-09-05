---
title: Organizacje w witrynie nuget.org
description: Organizacje w witrynie nuget.org ułatwia zarządzanie pakietami publikowane przez grupę lub w zespole, środowisko firmy.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551231"
---
# <a name="organization-on-nugetorg"></a>Organizacji w witrynie nuget.org

Organizacje umożliwiają firmom i projektów typu open source do współpracy nad pakietów przy użyciu tożsamości jednym nuget.org. Konsument pakietu konto organizacji wyświetlany jest taka sama jak istniejącego konta użytkownika w witrynie nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Konta użytkowników i kont organizacji

Twoje konto użytkownika jest swoją tożsamość w witrynie nuget.org i może należeć do dowolnej liczby organizacji. Pakiet może należeć do organizacji, takich jak mogą należeć do konta użytkownika. Konsumentów pakietu nie jest widoczna różnica między kontem użytkownika lub konta organizacji: oba są wyświetlane jako pakiet `owners`.

Konto organizacji ma co najmniej jednego konta użytkownika jako elementy członkowskie. Członkowie mogą zarządzać zestaw pakietów przy zachowaniu jednej tożsamości dla własności.

## <a name="adding-a-new-organization"></a>Dodawanie nowej organizacji

Aby dodać nową organizację, wybierz swoje konto w witrynie nuget.org, a następnie wybierz **organizacjom zarządzanie...**  polecenia menu:

![Opcja menu w witrynie nuget.org dla organizacji Menedżera](media/org-manage-option.png)

Na następnej stronie wybierz **Dodaj nową organizację** przycisku:

![Przycisk, aby utworzyć nową organizację, w witrynie nuget.org](media/org-add-new-option.png)

Na następnej stronie Podaj adres nazwę i adres e-mail organizacji. Ponieważ konta organizacji używają tej samej przestrzeni nazw jako konta użytkownika, nazwę organizacji musi być różni się od innych istniejących organizacji lub kont użytkowników. Adres e-mail również musi być unikatowa dla wszystkich kont.

![Dodaj nową stronę organizacji w witrynie nuget.org](media/org-add-new-page.png)

Po utworzeniu konta organizacji, możesz jesteś administratorem i przesłać pakiety do organizacji i dodać członków organizacji.

### <a name="transform-existing-account-to-an-organization"></a>Przekształcanie istniejące konto organizacji

> [!Warning]
> Konwersja konta jest nieodwracalne: nie można przekształcić organizacji do konta użytkownika.

Jeśli pakiety zarządzania jako zespół przy użyciu jednego konta użytkownika, a chcesz przekonwertować to konto do organizacji, użyj **Przekształć swoje konto, aby organizacja** opcja **organizacjom zarządzanie** strony:

![Opcja w witrynie nuget.org do przekształcania istniejącego konta do organizacji](media/org-transform-option.png)

Na następnej stronie podaj inne konto użytkownika można przypisać jako administrator w organizacji, a następnie wybierz **Przekształcanie**.

![Wprowadzanie informacji do przekształcania konto użytkownika w organizacji](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Zarządzanie członkami organizacji

Jako administrator organizacji, możesz dodawać członków, podając adres nuget.org każdy element członkowski *nazwę konta użytkownika*; nie można używać adresów e-mail. Następnie oznacz każdy element członkowski jako współpracownika lub administrator z następującymi uprawnieniami:

| Uprawnienie | Współautor | Administrator |
| --- | --- | --- |
| Zarządzanie pakietami w organizacji<br/>(przesyłanie nowych pakietów, aktualizacji lub wyrejestrowanie istniejących pakietów) | Tak | Tak |
| Zmiana organizacji metadanych<br/>(adres e-mail, ustawienia powiadomień) | Nie | Tak |
| Zarządzanie członkami organizacji | Nie | Tak |
| Żądania lub reagowanie na żądania co-ownership pakietów organizacji | Nie | Tak |

## <a name="managing-packages"></a>Zarządzanie pakietami

Wszystkie pakiety można wyświetlić na swoje konto i wszystkie organizacje, których jesteś członkiem na [Zarządzanie pakietami](https://www.nuget.org/account/Packages) strony. Aby wyświetlić te pakiety, które są specyficzne dla swojego konta lub wszelkich konkretnej organizacji, użyj filtru kont w górnym rogu strony.

![Zarządzanie pakietami za pomocą filtru konta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Przenoszenie pakietów do organizacji
Jeśli chcesz przenieść niektórych pakietów do nowo utworzonego organizacji, możesz to zrobić, żądania konta organizacji do współwłaścicielami pakietu, a następnie usuwając siebie jako właściciela. Jeśli jesteś administratorem w organizacji, jest Brak potwierdzenia zaakceptowanie własność. Jeśli jesteś współpracownika, dodawanie organizacji jako właściciel wymaga jednak jeden z administratorów, aby zaakceptować własność.

## <a name="publishing-packages"></a>Publikowanie pakietów

Publikowanie pakietów dla organizacji, takich jak publikowanie pakietów do konta użytkownika: bezpośrednie przekazanie pakietu na stronie nuget.org lub wypychając pakiet za pośrednictwem `nuget push` lub `dotnet nuget push` poleceń interfejsu wiersza polecenia.

### <a name="uploading-packages"></a>Przekazywanie pakietów

Gdy możesz bezpośrednio przekazać nowy pakiet na [nuget.org przekazywania](https://www.nuget.org/packages/manage/upload) stronie przypisujesz właściciel pakietu do użytkownika lub konta organizacji:

![Przekaż pakiet za pomocą opcji konta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Przy użyciu kluczy interfejsu API

Aby wypchnąć pakiet za pośrednictwem `nuget push` lub `dotnet nuget push` poleceń interfejsu wiersza polecenia, należy uzyskać klucz interfejsu API wymagane przez tych poleceń. Aby uzyskać więcej informacji, zobacz [publikowanie pakietu](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Podczas tworzenia nowego klucza interfejsu API, wybierz odpowiednie organizacji w **właścicielem pakietu** listy rozwijanej. Dowolny klucz interfejsu API, które możesz utworzyć ma zastosowanie tylko do wybranych organizacji:

![Klucz interfejsu API za pomocą opcji konta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Usuwanie organizacji

Jako użytkownik, możesz usunąć siebie z organizacji, wybierając `X` przycisk wyświetlane przez członkostwo w Twojej organizacji:

![Usuwanie konta użytkownika z organizacji](media/org-remove-self-option.png)

Administratorzy mogą usuwać dowolnego elementu członkowskiego z organizacji, w tym innych administratorów. Jeśli jesteś jedynym administratorem w organizacji, nie możesz usunąć siebie chyba że dodasz inny użytkownik z uprawnieniami administratora.

### <a name="deleting-an-organization-account"></a>Trwa usuwanie konta organizacji

Ta funkcja będzie dostępna wkrótce.
