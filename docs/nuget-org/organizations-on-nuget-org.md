---
title: Twoja organizacja na NuGet.org
description: Organizacje na NuGet.org pomaga zarządzać pakietami publikowanych przez grupę lub w środowisku zespołowym, firmowym.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427540"
---
# <a name="your-organization-on-nugetorg"></a>Twoja organizacja na NuGet.org

Organizacje umożliwiają firmom i projektom typu open source współpracę nad pakietami przy użyciu jednej NuGet.org tożsamości. W przypadku konsumenta pakietu konto organizacji jest takie samo jak istniejące konto użytkownika w NuGet.org.

## <a name="organization-accounts-vs-individual-accounts"></a>Konta organizacji a konta indywidualne

Konto organizacji ma co najmniej jedno konto indywidualne (użytkownika) jako jego członków. Te elementy członkowskie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości dla własności.

Twoje indywidualne konto jest Twoją tożsamością w NuGet.org i może być członkiem dowolnej liczby organizacji. Pakiet może należeć do konta organizacji, tak jak może należeć do indywidualnego konta. Konsumenci pakietów nie widzą żadnej różnicy między kontem indywidualnym `owners`lub kontem organizacji: oba są wyświetlane jako pakiet.

## <a name="adding-a-new-organization"></a>Dodawanie nowej organizacji

Aby dodać nową organizację, wybierz swoje konto w NuGet.org, a następnie wybierz polecenie menu **Zarządzaj organizacjami...:**

![Opcja menu w NuGet.org dla organizacji menedżera](media/org-manage-option.png)

Na następnej stronie wybierz przycisk **Dodaj nową organizację:**

![Przycisk, aby utworzyć nową organizację na NuGet.org](media/org-add-new-option.png)

Na następnej stronie podaj nazwę organizacji i adres e-mail. Ponieważ konta organizacji mają ten sam obszar nazw co konta użytkowników, nazwa organizacji musi się różnić od innych istniejących kont organizacji lub użytkowników. Adres e-mail musi być również unikatowy na wszystkich kontach.

![Dodawanie nowej strony organizacji w NuGet.org](media/org-add-new-page.png)

Po utworzeniu konta instytucji jesteś administratorem i możesz przesyłać pakiety dla instytucji i dodawać członków instytucji.

### <a name="transform-existing-account-to-an-organization"></a>Przekształcanie istniejącego konta w organizację

> [!Warning]
> Konwersja konta jest nieodwracalna: nie można przekształcić organizacji z powrotem w konto użytkownika.

Jeśli zarządzasz pakietami jako zespół przy użyciu jednego konta użytkownika i chcesz przekonwertować je na organizację, użyj opcji **Przekształć swoje konto** w organizację na stronie **Zarządzanie organizacjami:**

![Opcja NuGet.org, aby przekształcić istniejące konto w organizację](media/org-transform-option.png)

Na następnej stronie określ inne konto użytkownika, które ma zostać przypisane jako administrator organizacji, a następnie wybierz pozycję **Przekształć**.

![Wprowadzanie informacji dotyczących przekształcania konta użytkownika w organizację](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Zarządzanie członkami instytucji

Jako administrator organizacji możesz dodawać członków, podając nazwę *konta użytkownika*NuGet.org każdego członka; nie można używać adresów e-mail. Następnie każdy członek oznacza jako współpracownika lub administratora z następującymi uprawnieniami:

| Uprawnienie | Współpracownik | Administrator |
| --- | --- | --- |
| Zarządzanie pakietami organizacji<br/>(przesyłać nowe pakiety, aktualizować lub wystawić istniejące pakiety) | Tak | Tak |
| Zmienianie metadanych organizacji<br/>(adres e-mail, ustawienia powiadomień) | Nie | Tak |
| Zarządzanie członkami instytucji | Nie | Tak |
| Żądanie lub działanie w sprawie żądań współwłasności dla pakietów organizacji | Nie | Tak |

## <a name="managing-packages"></a>Zarządzanie pakietami

Możesz wyświetlić wszystkie pakiety na swoim koncie i we wszystkich organizacjach, których jesteś członkiem, na stronie [Zarządzanie pakietami.](https://www.nuget.org/account/Packages) Aby wyświetlić pakiety specyficzne dla Twojego konta lub określonej organizacji, użyj filtru kont w prawym górnym rogu strony.

![Zarządzanie pakietami za pomocą filtru konta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Przenoszenie pakietów do organizacji
Jeśli chcesz przenieść niektóre pakiety do nowo utworzonej organizacji, możesz to zrobić, żądając od konta organizacji współwłasnego pakietu, a następnie usuwając siebie jako właściciela. Jeśli jesteś administratorem organizacji, nie ma potwierdzenia wymaganego do zaakceptowania własności. Jeśli jednak jesteś współpracownikiem, dodanie organizacji jako właściciela wymaga od jednego z administratorów zaakceptowania własności.

## <a name="publishing-packages"></a>Publikowanie pakietów

Publikujesz pakiety w organizacji, takiej jak publikowanie pakietów na konto użytkownika: przesyłając bezpośrednio pakiet `nuget push` do `dotnet nuget push` NuGet.org lub wypychając pakiet za pomocą poleceń lub interfejsu wiersza polecenia.

### <a name="uploading-packages"></a>Przesyłanie pakietów

Podczas bezpośredniego przekazywania nowego pakietu na stronie [przekazywania NuGet.org](https://www.nuget.org/packages/manage/upload) właściciel pakietu jest przypisywany do konta użytkownika lub organizacji:

![Przekaż pakiet z opcją konta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Korzystanie z kluczy interfejsu API

Aby wypchnąć `nuget push` pakiet `dotnet nuget push` za pośrednictwem poleceń lub interfejsu wiersza polecenia, należy uzyskać klucz interfejsu API wymagany przez te polecenia. Aby uzyskać szczegółowe informacje, zobacz [Publikowanie pakietu](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Podczas tworzenia nowego klucza interfejsu API wybierz odpowiednią organizację w rozwijanej właściciel **pakietu.** Każdy utworzony klucz interfejsu API ma zastosowanie tylko do wybranej organizacji:

![Klucz interfejsu API z opcją konta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Usuwanie organizacji

Jako użytkownik możesz usunąć siebie z organizacji, wybierając przycisk **X** wyświetlany przez członkostwo w organizacji:

![Usuwanie konta użytkownika z instytucji](media/org-remove-self-option.png)

Administratorzy mogą usuwać dowolnego członka instytucji, w tym innych administratorów. Jeśli jesteś jedynym administratorem organizacji, nie możesz usunąć siebie, chyba że dodasz innego członka jako administratora.

### <a name="deleting-an-organization-account"></a>Usuwanie konta instytucji

Konto organizacji można usunąć, klikając przycisk **Usuń** wyświetlany na stronie organizacji.

![Usuwanie organizacji](media/org-delete-option.png)

Aby usunąć organizatora, należy go potwierdzić, klikając przycisk Usuń potwierdzenie **organizacji.**
