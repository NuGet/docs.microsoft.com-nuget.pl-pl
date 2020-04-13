---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "68419920"
---
1. [Zaloguj się na swoje konto nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) lub utwórz konto, jeśli jeszcze go nie masz.

   Aby uzyskać więcej informacji na temat tworzenia konta, zobacz [Indywidualne konta](../../nuget-org/individual-accounts.md).

1. Wybierz nazwę użytkownika (w prawym górnym rogu), a następnie wybierz pozycję **Klawisze INTERFEJSU API**.

1. Wybierz **pozycję Utwórz**, podaj nazwę klucza, wybierz **pozycję Wybierz zakresy > Wypychanie**. Wprowadź * dla **wzoru Glob**, a następnie wybierz pozycję **Utwórz**. (Zobacz poniżej, aby uzyskać więcej informacji na temat zakresów.)

1. Po utworzeniu klucza wybierz **pozycję Kopiuj,** aby pobrać klucz dostępu potrzebny w wierszu polecenia:

    ![Kopiowanie klucza INTERFEJSU API do schowka](../media/QS_Create-02-APIKey.png)

1. **Ważne:** Zapisz klucz w bezpiecznej lokalizacji, ponieważ nie można skopiować klucza później. Jeśli powrócisz do strony klucza interfejsu API, należy ponownie wygenerować klucz, aby go skopiować. Można również usunąć klucz interfejsu API, jeśli nie chcesz już wypychać pakietów za pośrednictwem interfejsu wiersza polecenia.

Określanie zakresu umożliwia tworzenie oddzielnych kluczy interfejsu API do różnych celów. Każdy klucz ma swój okres wygaśnięcia i może być objęty zakresem do określonych pakietów (lub wzorców glob). Każdy klucz jest również zakres do określonych operacji: wypychanie nowych pakietów i aktualizacji, wypychanie tylko aktualizacji lub delisting. Za pomocą zakresu można tworzyć klucze interfejsu API dla różnych osób, które zarządzają pakietami dla twojej organizacji, tak aby miały tylko uprawnienia, których potrzebują. Aby uzyskać więcej informacji, zobacz [klucze interfejsu API o określonym zakresie](../../nuget-org/scoped-api-keys.md).