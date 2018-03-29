1. [Zaloguj się do swojego konta nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) lub utworzyć konto, jeśli nie masz już.

1. Wybierz nazwę użytkownika (w prawym górnym rogu), a następnie wybierz **klucze interfejsu API**.

1. Wybierz **Utwórz**, podaj nazwę klucza, wybierz **wybierz zakresy > Push**. W obszarze **klucz interfejsu API**, wprowadź * dla **wzorzec Glob**, a następnie wybierz pozycję **Utwórz**. (Zobacz poniżej szczegółowe informacje na temat zakresów).

1. Po klucz zostanie utworzony, wybierz **kopiowania** można pobrać dostępu do klucza należy w interfejsu wiersza polecenia:

    ![Kopiowanie do Schowka klucz interfejsu API](../media/QS_Create-02-APIKey.png)

1. **Ważne**: zapisać klucz w bezpiecznej lokalizacji, ponieważ nie można skopiować klucza ponownie na dalszym etapie. Możesz powrócić do strony klucza interfejsu API, musisz ponownie wygenerować klucz, aby go skopiować. Można również usunąć klucz interfejsu API, jeśli nie chcesz push pakietów za pomocą interfejsu wiersza polecenia.

Określanie zakresu umożliwia tworzenie oddzielnych kluczy interfejsu API do różnych celów. Każdy klucz ma jego okres ważności i można ograniczone do określonych pakietów (lub wzorce glob). Każdy klucz ma również zakres z określonymi operacjami: zamówienie nowe pakiety i aktualizacje, wypychania tylko aktualizacje lub usunięcie. Za pomocą zakresu, można utworzyć klucze interfejsu API dla różnych osób zarządzających pakietów dla Twojej organizacji w taki sposób, że mają one uprawnienia, które są im potrzebne. Aby uzyskać więcej informacji, zobacz [Introducing zakres klucze interfejsu API](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).