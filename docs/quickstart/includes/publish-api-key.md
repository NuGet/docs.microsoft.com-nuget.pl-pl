---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419920"
---
1. [Zaloguj się do swojego konta NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) lub Utwórz konto, jeśli jeszcze go nie masz.

   Aby uzyskać więcej informacji na temat tworzenia konta, zobacz [poszczególne konta](../../nuget-org/individual-accounts.md).

1. Wybierz nazwę użytkownika (w prawym górnym rogu), a następnie wybierz pozycję **klucze interfejsu API**.

1. Wybierz pozycję **Utwórz**, podaj nazwę klucza, wybierz pozycję **Wybierz zakresy > wypychania**. Wprowadź ciąg * for **globalizowania**, a następnie wybierz pozycję **Utwórz**. (Zobacz poniżej, aby uzyskać więcej informacji na temat zakresów).

1. Po utworzeniu klucza wybierz pozycję **Kopiuj** , aby pobrać wymagany klucz dostępu w interfejsie wiersza polecenia:

    ![Kopiowanie klucza interfejsu API do schowka](../media/QS_Create-02-APIKey.png)

1. **Ważne**: Zapisz klucz w bezpiecznej lokalizacji, ponieważ nie można później skopiować klucza. W przypadku powrotu do strony klucza interfejsu API należy ponownie wygenerować klucz, aby go skopiować. Możesz również usunąć klucz interfejsu API, jeśli nie chcesz już wysyłać pakietów za pośrednictwem interfejsu wiersza polecenia.

Określanie zakresu umożliwia tworzenie oddzielnych kluczy interfejsu API do różnych celów. Każdy klucz ma przedział czasu wygaśnięcia i może być objęty zakresem określonych pakietów (lub wzorców globalizowania). Każdy klucz jest również objęty zakresem określonych operacji: wypychanie nowych pakietów i aktualizacji, tylko wypychanie aktualizacji lub odlistowanie. Dzięki funkcji określania zakresu można utworzyć klucze interfejsu API dla różnych osób, które zarządzają pakietami w organizacji, tak aby mieli tylko wymagane uprawnienia. Aby uzyskać więcej informacji, zobacz [klucze interfejsu API w zakresie](../../nuget-org/scoped-api-keys.md).