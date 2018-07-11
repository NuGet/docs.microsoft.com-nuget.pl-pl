Błędy z `push` polecenia zazwyczaj wskazują na problem. Na przykład zapomniał zaktualizowania numeru wersji w twoim projekcie i w związku z tym próby opublikowania pakietu, która już istnieje.

Zostaną również wyświetlone błędy, podczas próby opublikowania pakietu przy użyciu identyfikatora, który już istnieje na hoście. Nazwa "AppLogger", na przykład, już istnieje. W takim przypadku `push` polecenie daje następujący błąd:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Ten komunikat oznacza konflikt nazw, który nie jest całkowicie jasne z częścią "uprawnienia" błąd, jeśli używasz prawidłowego klucza interfejsu API, który został utworzony. Zmienić identyfikator pakietu, ponownie skompilować projekt i Utwórz ponownie `.nupkg` pliku, a następnie ponów `push` polecenia.