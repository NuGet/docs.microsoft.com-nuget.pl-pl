---
title: nuget.exe dostawcy poświadczeń
description: nuget.exe uwierzytelniają się za pomocą kanału informacyjnego i są implementowane jako pliki wykonywalne wiersza polecenia zgodne z określonymi konwencjami.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323833"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Uwierzytelnianie źródeł danych za pomocą nuget.exe poświadczeń

W wersji `3.3` dodano obsługę określonych `nuget.exe` dostawców poświadczeń. Od tego czasu dodano obsługę wersji `4.8` [dostawców poświadczeń,](NuGet-Cross-Platform-Authentication-Plugin.md) którzy działają we wszystkich scenariuszach wiersza polecenia ( `nuget.exe` , , `dotnet.exe` `msbuild.exe` ).

Zobacz [Korzystanie z pakietów z uwierzytelnionych źródeł danych,](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) aby uzyskać więcej informacji na temat wszystkich metod uwierzytelniania dla `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe odnajdywania dostawcy poświadczeń

nuget.exe poświadczeń można używać na 3 sposoby:

- **Globalnie:** aby udostępnić dostawcę poświadczeń dla wszystkich wystąpień uruchamiania w profilu bieżącego `nuget.exe` użytkownika, dodaj go do . `%LocalAppData%\NuGet\CredentialProviders` Może być konieczne utworzenie `CredentialProviders` folderu . Dostawców poświadczeń można zainstalować w katalogu głównym `CredentialProviders`  folderu lub w podfolderze. Jeśli dostawca poświadczeń ma wiele plików/zestawów, można użyć podfolderów, aby zachować zorganizowaność dostawców.

- **Ze zmiennej środowiskowej**: Dostawcy poświadczeń mogą być przechowywani w dowolnym miejscu i dostępni do nich przez ustawienie zmiennej środowiskowej `nuget.exe` na `%NUGET_CREDENTIALPROVIDERS_PATH%` lokalizację dostawcy. Ta zmienna może być listą rozdzieloną średnikami (na przykład `path1;path2` ), jeśli masz wiele lokalizacji.

- **Oprócz nuget.exe:** nuget.exe poświadczeń można umieścić w tym samym folderze, w którym znajduje się folder `nuget.exe` .

Podczas ładowania dostawców poświadczeń program wyszukuje w powyższych lokalizacjach dowolny plik o nazwie , a następnie ładuje te pliki w kolejności, w których `nuget.exe` `credentialprovider*.exe` zostały znalezione. Jeśli w tym samym folderze istnieje wielu dostawców poświadczeń, są one ładowane w kolejności alfabetycznej.

## <a name="creating-a-nugetexe-credential-provider"></a>Tworzenie dostawcy nuget.exe poświadczeń

Dostawca poświadczeń to plik wykonywalny wiersza polecenia o nazwie w postaci , który zbiera dane wejściowe, uzyskuje odpowiednie poświadczenia, a następnie zwraca odpowiedni kod stanu zakończenia i standardowe `CredentialProvider*.exe` dane wyjściowe.

Dostawca musi wykonać następujące czynności:

- Określ, czy można podać poświadczenia dla docelowego URI przed zainicjowanie pozyskiwania poświadczeń. Jeśli nie, powinien zostać zwrócony kod stanu 1 bez poświadczeń.
- Nie modyfikuj (na przykład w tym miejscu `NuGet.Config` ustawiaj poświadczenia).
- Samodzielnie obsługuj konfigurację serwera proxy HTTP, ponieważ nuGet nie dostarcza informacji o serwerze proxy do wtyczki.
- Zwróć poświadczenia lub szczegóły błędu do obiektu , zapisując obiekt odpowiedzi JSON (patrz poniżej) w obiekcie `nuget.exe` stdout przy użyciu kodowania UTF-8.
- Opcjonalnie emituj dodatkowe rejestrowanie śledzenia do stderr. Nie należy kiedykolwiek zapisywać wpisów tajnych w programie stderr, ponieważ na poziomie szczegółowości "normalne" lub "szczegółowe" takie ślady są powtarzane w konsoli przez program NuGet.
- Nieoczekiwane parametry powinny być ignorowane, zapewniając zgodność z przyszłymi wersjami pakietu NuGet.

### <a name="input-parameters"></a>Parametry wejściowe

| Parametr/przełącznik |Opis|
|----------------|-----------|
| Identyfikator URI {value} | Źródłowy kod URI pakietu wymagający poświadczeń.|
| Nieinteraktywnych | Jeśli jest obecny, dostawca nie wyświetla monitów interakcyjnych. |
| IsRetry | Jeśli istnieje, wskazuje, że ta próba jest ponowieniem próby, która wcześniej zakończyła się niepowodzeniem. Dostawcy zwykle używają tej flagi, aby upewnić się, że pomijają istniejącą pamięć podręczną i w miarę możliwości monitują o nowe poświadczenia.|
| Szczegółowość {value} | Jeśli jest obecna, jedna z następujących wartości: "normal", "quiet" lub "detailed". Jeśli żadna wartość nie zostanie dostarczona, wartość domyślna to "normal". Dostawcy powinni używać tego jako wskazania poziomu opcjonalnego rejestrowania do emitowania do standardowego strumienia błędów. |

### <a name="exit-codes"></a>Kody zakończenia

| Kod |Wynik | Opis |
|----------------|-----------|-----------|
| 0 | Powodzenie | Poświadczenia zostały pomyślnie uzyskane i zapisane w stdout.|
| 1 | DostawcaNotApplicable | Bieżący dostawca nie podaje poświadczeń dla danego URI.|
| 2 | Niepowodzenie | Dostawca jest poprawnym dostawcą dla danego URI, ale nie może podać poświadczeń. W takim przypadku metoda nuget.exe ponowi próbę uwierzytelnienia i nie powiedzie się. Typowym przykładem jest anulowanie logowania interakcyjnego przez użytkownika. |

### <a name="standard-output"></a>Wyjście standardowe

| Właściwość |Uwagi|
|----------------|-----------|
| Nazwa użytkownika | Nazwa użytkownika dla uwierzytelnionych żądań.|
| Hasło | Hasło dla uwierzytelnionych żądań.|
| Komunikat | Opcjonalne szczegóły dotyczące odpowiedzi, używane tylko do pokazywania dodatkowych szczegółów w przypadkach awarii. |

Przykład stdout:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Rozwiązywanie problemów z dostawcą poświadczeń

Obecnie narzędzie NuGet nie zapewnia bezpośredniej obsługi debugowania niestandardowych dostawców poświadczeń. [problem 4598 śledzi](https://github.com/NuGet/Home/issues/4598) tę pracę.

Ponadto można wykonać następujące czynności:

- Uruchom nuget.exe z `-verbosity` przełącznikiem , aby sprawdzić szczegółowe dane wyjściowe.
- Dodaj komunikaty debugowania `stdout` do polecenia w odpowiednich miejscach.
- Upewnij się, że używasz usługi nuget.exe 3.3 lub wyższej.
- Dołącz debuger podczas uruchamiania za pomocą tego fragmentu kodu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
