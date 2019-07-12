---
ms.openlocfilehash: 5acdc54726e4cb07794f8ee07d5e0d357ff622a3
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842058"
---
1. [Zaloguj się do swojego konta w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) lub Utwórz konto Jeśli nie masz jeszcze takiego.

1. Wybierz swoją nazwę użytkownika (w prawym górnym rogu), a następnie wybierz **klucze interfejsu API**.

1. Wybierz **Utwórz**, podaj nazwę klucza, wybierz **wybierz zakresy > wypychania**. Wprowadzanie * dla **wzorzec Glob**, a następnie wybierz **Utwórz**. (Zobacz poniżej więcej informacji na temat zakresów).

1. Po utworzeniu klucza, wybierz **kopiowania** do pobrania jest dostęp do kluczy należy w interfejsie wiersza polecenia:

    ![Kopiowanie klucza interfejsu API do Schowka](../media/QS_Create-02-APIKey.png)

1. **Ważne**: Zapisać klucz w bezpiecznym miejscu, ponieważ nie można skopiować klucz ponownie na dalszym etapie. Po powrocie na stronę klucza interfejsu API, należy ponownie wygenerować klucza w celu skopiowania go. Można również usunąć klucza interfejsu API, jeśli nie chcesz już wypychania pakietów za pomocą interfejsu wiersza polecenia.

Wyznaczanie zakresu umożliwia tworzenie oddzielnych kluczy interfejsu API do różnych celów. Każdy klucz ma przedział czasu jego wygaśnięcia i może zostać obniżone do określonych pakietów (lub glob wzorców). Każdy klucz również jest ograniczone do określonych operacji: wypychane nowe pakiety i aktualizacje, wypychania tylko aktualizacje lub usunięcie. Za pomocą określania zakresu, można utworzyć klucze interfejsu API dla różnych osób, które zarządzać pakiety dla Twojej organizacji w taki sposób, że mają oni uprawnienia, które są im potrzebne. Aby uzyskać więcej informacji, zobacz [Introducing zakresu kluczy interfejsu API](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).