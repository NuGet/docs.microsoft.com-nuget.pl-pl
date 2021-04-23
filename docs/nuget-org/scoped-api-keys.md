---
title: Klucze interfejsu API o zakresie
description: Przejmij kontrolę nad kluczami interfejsu API, których używasz do wypychania pakietów
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901593"
---
# <a name="scoped-api-keys"></a>Klucze interfejsu API o zakresie

Aby pakiet NuGet był bezpieczniejszym środowiskiem dystrybucji pakietów, możesz przejąć kontrolę nad kluczami interfejsu API, dodając zakresy.

Możliwość zapewnienia zakresu kluczy interfejsu API zapewnia lepszą kontrolę nad interfejsami API. Oto co możesz zrobić:

- Utwórz wiele kluczy interfejsu API o różnych zakresach, które mogą być używane dla różnych pakietów o różnych terminach wygaśnięcia.
- Uzyskiwanie kluczy interfejsu API w bezpieczny sposób.
- Edytuj istniejące klucze interfejsu API, aby zmienić możliwość stosowania pakietów.
- Odśwież lub usuń istniejące klucze interfejsu API bez zakłócania operacji przy użyciu innych kluczy.

## <a name="why-do-we-support-scoped-api-keys"></a>Dlaczego obsługujemy klucze interfejsu API o zakresie?

Obsługujemy zakresy kluczy interfejsu API, aby umożliwić bardziej precyzyjne uprawnienia. Wcześniej nuGet oferował jeden klucz interfejsu API dla konta i takie podejście miało kilka wad:

- **Jeden klucz interfejsu API do kontrolowania wszystkich pakietów**. W przypadku pojedynczego klucza interfejsu API, który jest używany do zarządzania wszystkimi pakietami, trudno jest bezpiecznie udostępnić klucz, gdy wielu deweloperów jest zaangażowanych w różne pakiety i gdy współużytkują konto wydawcy.
- **Wszystkie uprawnienia lub brak**. Każda osoba mająca dostęp do klucza interfejsu API ma wszystkie uprawnienia (publikowanie, wypychanie i cofanie listy) w pakietach. Często nie jest to pożądane w środowisku z wieloma zespołami.
- **Pojedynczy punkt awarii.** Pojedynczy klucz interfejsu API oznacza również single point of failure. W przypadku naruszenia zabezpieczeń klucza wszystkie pakiety skojarzone z kontem mogą zostać naruszone. Odświeżanie klucza interfejsu API jest jedynym sposobem na podłączenie wycieku i uniknięcie przerw w przepływie pracy ci/CD. Ponadto mogą wystąpić przypadki, w których chcesz odwołać dostęp do klucza interfejsu API dla osoby poszczególnych osób (na przykład gdy pracownik opuści organizację). Obecnie nie ma czystego sposobu, aby sobie z tym poradzić.

Za pomocą kluczy interfejsu API o zakresie próbujemy rozwiązać te problemy, jednocześnie upewniamy się, że żaden z istniejących przepływów pracy nie przerwie.

## <a name="acquire-an-api-key"></a>Pozyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Tworzenie kluczy interfejsu API o zakresie

W zależności od wymagań można utworzyć wiele kluczy interfejsu API. Klucz interfejsu API może dotyczyć co najmniej jednego pakietu, mieć różne zakresy, które przyznają określone uprawnienia, i mieć skojarzoną datę wygaśnięcia.

W poniższym przykładzie masz klucz interfejsu API o nazwie , który może służyć do wypychania pakietów dla określonych pakietów i jest ważny `Contoso service CI` `Contoso.Service` przez 365 dni. Jest to typowy scenariusz, w którym różne zespoły w tej samej organizacji pracują nad różnymi pakietami, a członkowie zespołu mają klucz, który przyznaje im uprawnienia tylko do pakietu, nad którym pracują. Wygaśnięcie służy jako mechanizm zapobiegania nieodświeżonym lub zapomnianym kluczom.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Używanie wzorców globów

Jeśli pracujesz nad wieloma pakietami i masz dużą listę pakietów do zarządzania, możesz użyć wzorców wieloselekcjowych, aby wybrać wiele pakietów jednocześnie. Jeśli na przykład chcesz przyznać określone zakresy kluczowi dla wszystkich pakietów, których identyfikator rozpoczyna się od , możesz to zrobić, określając w polu tekstowym `Fabrikam.Service` `fabrikam.service.*` **Wzorzec globu.**

![Tworzenie kluczy interfejsu API — 2](media/scoped-api-keys-glob-pattern.png)

Używanie wzorców globu do określania uprawnień klucza interfejsu API dotyczy również nowych pakietów pasujących do wzorca globu. Jeśli na przykład spróbujesz wypchnąć nowy pakiet o nazwie , możesz to zrobić przy użyciu utworzonego wcześniej klucza, ponieważ pakiet jest taki sam jak `Fabrikam.Service.Framework` wzorzec globu `fabrikam.service.*` .

## <a name="obtain-api-keys-securely"></a>Bezpieczne uzyskiwanie kluczy interfejsu API

Ze względów bezpieczeństwa nowo utworzony klucz nigdy nie jest wyświetlany na ekranie i jest dostępny tylko przy użyciu **przycisku** Kopiuj. Podobnie klucz nie jest dostępny po odświeżeniu strony.

![Tworzenie kluczy interfejsu API — 3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Edytowanie istniejących kluczy interfejsu API

Możesz również zaktualizować zakresy i uprawnienia klucza bez zmiany samego klucza. Jeśli masz klucz z określonymi zakresami dla pojedynczego pakietu, możesz zastosować te same zakresy do jednego lub wielu innych pakietów.

![Tworzenie kluczy interfejsu API — 4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Odświeżanie lub usuwanie istniejących kluczy interfejsu API

Właściciel konta może odświeżyć klucz. W takim przypadku uprawnienia (w pakietach), zakres i wygaśnięcie pozostają takie same, ale jest wystawiany nowy klucz, co czyni stary klucz bezużytelny. Jest to przydatne w przypadku zarządzania nieodświeżonymi kluczami lub sytuacji, w których istnieje ryzyko wycieku klucza interfejsu API.

![Tworzenie kluczy interfejsu API — 5](media/scoped-api-keys-refresh.png)

Możesz również usunąć te klucze, jeśli nie będą już potrzebne. Usunięcie klucza powoduje usunięcie klucza i sprawia, że jest on bezużytelny.

## <a name="faqs"></a>Często zadawane pytania

### <a name="what-happens-to-my-old-legacy-api-key"></a>Co się stanie z moim starym (starszym) kluczem interfejsu API?

Stary klucz interfejsu API (starsza wersja) nadal działa i może działać tak długo, jak chcesz, aby działał. Jednak te klucze zostaną wycofane, jeśli nie były używane przez więcej niż 365 dni do wypychania pakietu. Aby uzyskać więcej informacji, zobacz wpis w blogu [Changes to expiring API keys (Zmiany wygasających kluczy interfejsu API).](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html) Nie można już odświeżać tego klucza. Zamiast tego należy usunąć starszy klucz i utworzyć nowy klucz o zakresie.

> [!NOTE]
> Ten klucz ma wszystkie uprawnienia do wszystkich pakietów i nigdy nie wygasa. Należy rozważyć usunięcie tego klucza i utworzenie nowych kluczy z uprawnieniami o określonym zakresie i określonym wygaśnięciem.

### <a name="how-many-api-keys-can-i-create"></a>Ile kluczy interfejsu API mogę utworzyć?

Nie ma żadnego limitu liczby kluczy interfejsu API, które można utworzyć. Zalecamy jednak, aby zachować zarządzaną liczbę, aby nie mieć wielu nieaktualnych kluczy bez znajomości, gdzie i kto ich używa.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Czy mogę usunąć starszy klucz interfejsu API lub zaprzestać używania go teraz?

Tak. Możesz — i prawdopodobnie należy — usunąć starszy klucz interfejsu API.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Czy mogę odzyskać klucz interfejsu API, który został usunięty przez pomyłkę?

Nie. Po usunięciu można tworzyć tylko nowe klucze. Nie jest możliwe odzyskanie przypadkowo usuniętych kluczy.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Czy stary klucz interfejsu API nadal działa po odświeżeniu klucza interfejsu API?

Nie. Po odświeżeniu klucza generowany jest nowy klucz, który ma ten sam zakres, uprawnienia i wygaśnięcie co stary. Stary klucz przestanie istnieć.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Czy mogę udzielić większej liczby uprawnień do istniejącego klucza interfejsu API?

Nie można zmodyfikować zakresu, ale można edytować listę pakietów, do których ma zastosowanie.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Jak mogę się, czy którykolwiek z kluczy wygasł lub czy wygasł?

Jeśli jakikolwiek klucz wygaśnie, zostanie wyświetlony komunikat ostrzegawczy w górnej części strony. Wysyłamy również wiadomość e-mail z ostrzeżeniem do właściciela konta dziesięć dni przed wygaśnięciem klucza, aby można było z niego korzystać z wyprzedzeniem.