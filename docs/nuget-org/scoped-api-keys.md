---
title: Klucze interfejsu API o określonym zakresie
description: Przejmij kontrolę nad kluczami API używanymi do wypychania pakietów
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427501"
---
# <a name="scoped-api-keys"></a>Klucze interfejsu API o określonym zakresie

Aby nuGet bardziej bezpieczne środowisko dystrybucji pakietów, można przejąć kontrolę nad kluczami interfejsu API, dodając zakresy.

Możliwość zapewnienia zakresu kluczy interfejsu API zapewnia lepszą kontrolę nad interfejsami API. Możesz:

- Utwórz wiele kluczy interfejsu API o określonym zakresie, które mogą być używane dla różnych pakietów o różnych przedziałach czasowych wygaśnięcia.
- Uzyskaj bezpieczne klucze interfejsu API.
- Edytuj istniejące klucze interfejsu API, aby zmienić możliwość stosowania pakietu.
- Odświeżanie lub usuwanie istniejących kluczy interfejsu API bez utrudniania operacji przy użyciu innych kluczy.

## <a name="why-do-we-support-scoped-api-keys"></a>Dlaczego obsługujemy klucze interfejsu API o określonym zakresie?

Obsługujemy zakresy kluczy interfejsu API, aby umożliwić ci bardziej szczegółowe uprawnienia. Wcześniej NuGet oferowane jeden klucz interfejsu API dla konta, a to podejście miało kilka wad:

- **Jeden klucz interfejsu API do kontrolowania wszystkich pakietów**. Z jednego klucza interfejsu API, który jest używany do zarządzania wszystkimi pakietami, trudno jest bezpiecznie udostępnić klucz, gdy wielu deweloperów są zaangażowane w różnych pakietów i gdy współużytkują konto wydawcy.
- **Wszystkie uprawnienia lub brak**. Każdy, kto ma dostęp do klucza INTERFEJSU API ma wszystkie uprawnienia (publikować, wypychać i odsuwać listę) na pakietach. Często nie jest to pożądane w środowisku z wieloma zespołami.
- **Pojedynczy punkt awarii**. Pojedynczy klucz interfejsu API oznacza również pojedynczy punkt awarii. Jeśli klucz zostanie naruszony, wszystkie pakiety skojarzone z kontem mogą zostać naruszone. Odświeżanie klucza interfejsu API jest jedynym sposobem, aby podłączyć przeciek i uniknąć przerwy w przepływie pracy ciągłej integracji/ciągłego wdrażania. Ponadto mogą wystąpić przypadki, gdy chcesz odwołać dostęp do klucza interfejsu API dla danej osoby (na przykład, gdy pracownik opuszcza organizację). Nie ma dziś czystego sposobu radzenia sobie z tym.

Z kluczami interfejsu API o określonym zakresie, staramy się rozwiązać te problemy, upewniając się, że żaden z istniejących przepływów pracy przerwy.

## <a name="acquire-an-api-key"></a>Uzyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Tworzenie kluczy interfejsu API o określonym zakresie

Można utworzyć wiele kluczy interfejsu API na podstawie wymagań. Klucz interfejsu API można zastosować do jednego lub więcej pakietów, mają różne zakresy, które przyznają określone uprawnienia i mają datę wygaśnięcia skojarzone z nim.

W poniższym przykładzie masz klucz `Contoso service CI` interfejsu API o nazwie, `Contoso.Service` który może służyć do wypychania pakietów dla określonych pakietów i jest prawidłowy przez 365 dni. Jest to typowy scenariusz, w którym różne zespoły w tej samej organizacji pracują nad różnymi pakietami, a członkowie zespołu otrzymują klucz, który przyznaje im uprawnienia tylko dla pakietu, nad którym pracują. Wygaśnięcie służy jako mechanizm, aby zapobiec starych lub zapomnianych kluczy.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Użyj wzorów glob

Jeśli pracujesz nad wieloma pakietami i masz dużą listę pakietów do zarządzania, możesz użyć wzorców globbingu, aby wybrać wiele pakietów razem. Na przykład, jeśli chcesz udzielić określonych zakresów do klucza dla `Fabrikam.Service`wszystkich pakietów, których `fabrikam.service.*` identyfikator zaczyna się od , można to zrobić, określając w polu tekstowym **wzorca Glob.**

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-glob-pattern.png)

Za pomocą wzorców glob do określenia uprawnień klucza interfejsu API stosuje się również do nowych pakietów pasujących do wzorca glob. Na przykład, jeśli spróbujesz wypchnąć nowy pakiet o nazwie `Fabrikam.Service.Framework`, można to zrobić `fabrikam.service.*`z kluczem utworzonym wcześniej, ponieważ pakiet pasuje do wzorca glob .

## <a name="obtain-api-keys-securely"></a>Bezpieczne uzyskiwanie kluczy interfejsu API

Ze względów bezpieczeństwa nowo utworzony klucz nigdy nie jest wyświetlany na ekranie i jest dostępny tylko za pomocą przycisku **Kopiuj.** Podobnie klucz nie jest dostępny po odświeżeniu strony.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Edytowanie istniejących kluczy interfejsu API

Można również zaktualizować uprawnienia klucza i zakresy bez zmiany samego klucza. Jeśli masz klucz z określonymi zakresami dla pojedynczego pakietu, możesz zastosować te same zakresy na jednym lub wielu innych pakietach.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Odświeżanie lub usuwanie istniejących kluczy interfejsu API

Właściciel konta może wybrać odświeżenie klucza, w którym to przypadku uprawnienie (na pakiety), zakres i wygaśnięcie pozostają takie same, ale nowy klucz jest wystawiany, dzięki czemu stary klucz nie nadaje się do bezużyteczny. Jest to przydatne w zarządzaniu nieaktualne klucze lub gdzie istnieje możliwość wycieku klucza interfejsu API.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-refresh.png)

Można również usunąć te klucze, jeśli nie są już potrzebne. Usunięcie klucza powoduje usunięcie klucza i uniemożliwia jego użytecznie.

## <a name="faqs"></a>Często zadawane pytania

### <a name="what-happens-to-my-old-legacy-api-key"></a>Co się stanie z moim starym (starszym) kluczem interfejsu API?

Twój stary klucz interfejsu API (starszy) nadal działa i może działać tak długo, jak chcesz, aby działał. Jednak te klucze zostaną wycofane, jeśli nie były używane przez więcej niż 365 dni do wypychania pakietu. Aby uzyskać więcej informacji, zobacz wpis w blogu [Zmiany wygasające klucze interfejsu API](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Nie można już odświeżyć tego klucza. Należy usunąć starszy klucz i zamiast tego utworzyć nowy klucz o określonym zakresie.

> [!NOTE]
> Ten klucz ma wszystkie uprawnienia do wszystkich pakietów i nigdy nie wygasa. Należy rozważyć usunięcie tego klucza i tworzenie nowych kluczy z uprawnieniami o określonym zakresie i określonym wygaśnięciem.

### <a name="how-many-api-keys-can-i-create"></a>Ile kluczy interfejsu API można utworzyć?

Nie ma limitu liczby kluczy interfejsu API, które można utworzyć. Radzimy jednak, aby utrzymać go w zarządzaniu liczyć tak, że nie kończy się o wiele starych kluczy bez wiedzy, gdzie i kto z nich korzysta.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Czy mogę usunąć mój starszy klucz interfejsu API lub zaprzestać używania teraz?

Tak. Możesz — i prawdopodobnie powinieneś - usunąć starszy klucz interfejsu API.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Czy mogę odzyskać klucz interfejsu API, który został usunięty przez pomyłkę?

Nie. Po usunięciu można tworzyć tylko nowe klucze. Nie ma możliwości odzyskania przypadkowo usuniętych kluczy.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Czy stary klucz interfejsu API nadal działa po odświeżeniu klucza interfejsu API?

Nie. Po odświeżeniu klucza zostanie wygenerowany nowy klucz, który ma ten sam zakres, uprawnienie i wygaśnięcie, co stary. Stary klucz przestaje istnieć.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Czy mogę nadać więcej uprawnień istniejącemu kluczowi interfejsu API?

Nie można zmodyfikować zakresu, ale można edytować listę pakietów, do której ma zastosowanie.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Skąd mam wiedzieć, czy którykolwiek z moich kluczy wygasł lub wygasł?

Jeśli dowolny klucz wygaśnie, poinformujemy Cię o tym za pośrednictwem komunikatu ostrzegawczego u góry strony. Wysyłamy również e-mail z ostrzeżeniem do posiadacza konta na dziesięć dni przed wygaśnięciem klucza, aby można było na nim działać z dużym wyprzedzeniem.