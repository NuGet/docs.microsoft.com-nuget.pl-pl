Błędy z `push` polecenia zwykle wskazywać problem. Na przykład zapomniał zaktualizować numer wersji w projekcie i w związku z tym próby publikowania pakietu, który już istnieje.

Możesz również sprawdzić błędy, podczas próby opublikowania pakietu przy użyciu identyfikatora, który już istnieje na hoście. Nazwa "AppLogger", na przykład, już istnieje. W takim przypadku `push` polecenia zawiera następujący błąd:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Ten komunikat oznacza konflikt nazw, który nie jest całkowicie Wyczyść z części "uprawnienia" błędu, jeśli używasz prawidłowy klucz interfejsu API, który został właśnie utworzony. Zmień identyfikator pakietu, skompiluj ponownie projekt, ponownie utwórz `.nupkg` pliku, a następnie spróbuj ponownie `push` polecenia.