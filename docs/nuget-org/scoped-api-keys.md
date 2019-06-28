---
title: O określonym zakresie klucze interfejsu API
description: Przejmij kontrolę nad kluczy interfejsu API, które umożliwia wypychanie pakietów
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427501"
---
# <a name="scoped-api-keys"></a>O określonym zakresie klucze interfejsu API

Aby NuGet bezpieczniejsze środowisko do dystrybucji pakietów, może potrwać kontrolę nad kluczami interfejsu API przez dodanie zakresów.

Możliwość zapewnienia zakresu, aby zachować klucze interfejsu API zapewniają lepszą kontrolę w interfejsach API. Można:

- Utwórz wiele o określonym zakresie, które mogą służyć do różnych pakietach przy użyciu różnych harmonogramów wygaśnięcia kluczy interfejsu API.
- Bezpieczne uzyskanie kluczy interfejsu API.
- Edytuj istniejących kluczy interfejsu API można zmienić stosowania pakietu.
- Odśwież lub usunięcie istniejących kluczy interfejsu API bez zakłócania operacji przy użyciu innych kluczy.

## <a name="why-do-we-support-scoped-api-keys"></a>Dlaczego firma Microsoft obsługuje o określonym zakresie klucze interfejsu API?

Firma Microsoft obsługuje zakresów dla kluczy interfejsu API, które umożliwiają bardziej szczegółowych uprawnień. Wcześniej NuGet oferowane jednego klucza interfejsu API dla konta, a takie podejście ma kilka wady:

- **Jeden klucz interfejsu API do kontrolowania wszystkich pakietów**. Przy użyciu jednego klucza interfejsu API, który służy do zarządzania wszystkich pakietów trudno jest bezpiecznie udostępniaj klucza w przypadku wielu deweloperów związane z różnych pakietach, a po udostępnieniu konta wydawcy.
- **Wszystkie uprawnienia lub Brak**. Każda osoba mająca dostęp do klucza interfejsu API ma wszystkie uprawnienia (publikowania, wypychania i un-list) o pakiety. Często nie jest to pożądane w środowisku z wieloma zespołami.
- **Pojedynczy punkt awarii**. Jeden klucz interfejsu API oznacza również pojedynczy punkt awarii. Jeśli klucz zostanie naruszony, wszystkie pakiety skojarzone z kontem może być potencjalnie zagrożone. Odświeżanie klucza interfejsu API jest jedynym sposobem, aby podłączyć przecieku i uniknąć przerw w działaniu przepływu pracy ciągłej integracji/ciągłego wdrażania. Ponadto można wykluczyć sytuacji, gdy chcesz odwołać dostęp do klucza interfejsu API dla poszczególnych (na przykład, gdy pracownik odejdzie z organizacji). Nie ma eleganckie rozwiązanie do obsługi to już dziś.

Z kluczami interfejsu API o określonym zakresie podejmowane są próby zająć tymi problemami, pamiętając, Podziel przez żaden z istniejącymi przepływami pracy.

## <a name="acquire-an-api-key"></a>Uzyskiwanie klucza interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Tworzenie zakresu kluczy interfejsu API

Możesz utworzyć wiele kluczy interfejsu API, w zależności od wymagań. Klucza interfejsu API można zastosować do co najmniej jeden pakiet, mają różne zakresy, których przyznać określone uprawnienia i mają datę wygaśnięcia skojarzonych z nim.

W poniższym przykładzie, masz klucz interfejsu API o nazwie `Contoso service CI` można wypchnąć pakietów dla określonego `Contoso.Service` pakietów i jest ważny przez 365 dni. Jest to typowy scenariusz, gdzie znajdują się klucz, który przyznaje im uprawnienia tylko do pakietu, który pracuje nad zespołów w obrębie tej samej organizacji pracy w różnych pakietach i członków zespołu. Czas wygaśnięcia służy jako mechanizm, aby zapobiec starych lub zapomniane kluczy.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Użycie glob wzorców

Jeśli pracujesz na wielu pakietów, dużej listy pakietów do zarządzania można Użyj wzorców obsługi symboli wieloznacznych, aby wybrać wiele pakietów ze sobą. Na przykład, jeśli użytkownik chce udzielić określonych zakresów do klucza dla wszystkich pakietów którego Identyfikatora rozpoczyna się od ciągu `Fabrikam.Service`, można to zrobić, określając `fabrikam.service.*` w **wzorzec Glob** pola tekstowego.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-glob-pattern.png)

Przy użyciu wzorców glob, aby określić uprawnienia klucza interfejsu API dotyczy także nowe pakiety pasujących do wzorca glob. Na przykład, Jeśli spróbujesz wypchnąć nowy pakiet o nazwie `Fabrikam.Service.Framework`, możesz to zrobić przy użyciu klucza został wcześniej utworzony, ponieważ pakiet jest zgodny ze wzorcem glob `fabrikam.service.*`.

## <a name="obtain-api-keys-securely"></a>Bezpieczne uzyskanie kluczy interfejsu API

Dla bezpieczeństwa nowo utworzony klucz nigdy nie są wyświetlane na ekranie i jest tylko dostępne za pośrednictwem **kopiowania** przycisku. Podobnie klucz nie jest dostępny po odświeżeniu strony.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Edytuj istniejących kluczy interfejsu API

Można również zaktualizować uprawnienia klucza i zakresy bez wprowadzania zmian w samych kluczy. Jeśli masz klucz o określone zakresy dla jednego pakietu, można zastosować ten sam zakresy na jednej lub wielu pakietów.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Odśwież lub usuń istniejące klucze interfejsu API

Właściciel konta może wybrać, aby odświeżyć klucz, w którym to przypadku uprawnienia (pakiety), zakresu i wygaśnięcia pozostają takie same, ale wystawiono nowy klucz, co stary klucz nienadające się do użytku. Jest to przydatne w zarządzaniu starych kluczy lub w przypadku, gdy wszelkie ryzyko wycieku klucza interfejsu API.

![Tworzenie kluczy interfejsu API](media/scoped-api-keys-refresh.png)

Można również usunąć te klucze, jeśli nie są już potrzebne. Usuwanie klucza powoduje usunięcie klucza i sprawia, że korzystanie z niej.

## <a name="faqs"></a>Często zadawane pytania

### <a name="what-happens-to-my-old-legacy-api-key"></a>Co stanie się Moje starych (starszych) klucz interfejsu API?

Stary klucz interfejsu API (starsza wersja) w dalszym ciągu działać i może pracować tak długo, jak chcesz, aby pracować. Jednak te klucze zostaną wycofane, jeśli nie były używane przez więcej niż 365 dni do wypychania pakietu. Aby uzyskać więcej informacji, zobacz wpis w blogu [zmieni się na wygasających kluczy interfejsu API](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Nie można odświeżyć tego klucza. Musisz usunąć starszy klucz i zamiast tego utwórz nowy klucz o określonym zakresie.

> [!NOTE]
> Ten klucz ma wszystkie uprawnienia na wszystkich pakietów i nigdy nie wygasa. Należy rozważyć usunięcie tego klucza, a następnie tworzenia nowych kluczy z zakresu uprawnień i utraty ważności określony.

### <a name="how-many-api-keys-can-i-create"></a>Jak wiele kluczy interfejsu API można utworzyć?

Nie ma żadnego limitu liczby kluczy interfejsu API, które można utworzyć. Jednak zaleca się można zachować w zarządzaniu liczby tak, aby nie znajdą posiadanie wielu starych kluczy nie wie, gdzie i kto korzysta z nich.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Czy mogę usunąć mój starszy klucz interfejsu API lub zaprzestać używania teraz?

Tak. Możesz — i prawdopodobnie Usuń starszy klucz interfejsu API.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Czy mogę wrócić mój klucz interfejsu API, który został usunięty przez pomyłkę?

Nie. Po usunięciu może tylko tworzyć nowe klucze. Możliwe przypadkowo usuniętych kluczy jest brak odzyskiwania.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Stary klucz interfejsu API będzie działać podczas odświeżania klucza interfejsu API?

Nie. Po odświeżeniu klucz pobiera wygenerowany nowy klucz, który ma ten sam zakres, uprawnienia i wygaśnięcia jak stary. Stary klucz przestanie istnieć.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Można podać więcej uprawnień do istniejącego klucza interfejsu API?

Nie można modyfikować zakres, ale można edytować listy pakietów, które ma zastosowanie do.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Jak sprawdzić, dowolny Moje klucze wygasła lub pobierania wygasł?

Jeśli dowolny klawisz, wygaśnie, firma Microsoft powiadomi Cię za pośrednictwem komunikat ostrzegawczy w górnej części strony. Ponadto wprowadzono wysyłanie wiadomości e-mail z ostrzeżenie do właściciela konta dziesięć dni przed wygaśnięciem klucza, dzięki czemu może działać na nim również z wyprzedzeniem.