---
title: nuget.exe dostawców poświadczeń
description: nuget.exe dostawców poświadczeń uwierzytelniają się ze źródłem danych i są zaimplementowane jako pliki wykonywalne wiersza polecenia, które przestrzegają określonych konwencji.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 285504508fa88c96f5c7a23f15ef14d81ebc21e1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777769"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Uwierzytelnianie kanałów informacyjnych za pomocą dostawców poświadczeń nuget.exe

W obszarze `3.3` Obsługa wersji została dodana dla `nuget.exe` określonych dostawców poświadczeń. Od tej pory w programie `4.8` Dodano [obsługę dostawców poświadczeń](NuGet-Cross-Platform-Authentication-Plugin.md) , którzy działają we wszystkich scenariuszach wiersza polecenia ( `nuget.exe` , `dotnet.exe` ,, `msbuild.exe` ).

Aby uzyskać szczegółowe informacje dotyczące wszystkich metod uwierzytelniania dla programu, zobacz artykuł wykorzystywanie [pakietów ze źródeł uwierzytelnionych](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) . `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe odnajdywania dostawcy poświadczeń

nuget.exe dostawców poświadczeń można używać na trzy sposoby:

- **Globalnie**: Aby udostępnić dostawcę poświadczeń wszystkim wystąpieniu `nuget.exe` uruchomienia w ramach profilu bieżącego użytkownika, należy dodać go do programu `%LocalAppData%\NuGet\CredentialProviders` . Może być konieczne utworzenie `CredentialProviders` folderu. Dostawców poświadczeń można zainstalować w katalogu głównym `CredentialProviders`  folderu lub w podfolderze. Jeśli Dostawca poświadczeń ma wiele plików/zestawów, można użyć podfolderów, aby zachować zorganizowanie dostawców.

- **Ze zmiennej środowiskowej**: dostawcy poświadczeń można przechowywać w dowolnym miejscu i uzyskiwać do nich dostęp `nuget.exe` przez ustawienie `%NUGET_CREDENTIALPROVIDERS_PATH%` zmiennej środowiskowej na lokalizację dostawcy. Ta zmienna może być rozdzielaną średnikami listą (na przykład `path1;path2` ), jeśli istnieje wiele lokalizacji.

- **Obok nuget.exe**: dostawcy poświadczeń nuget.exe można umieścić w tym samym folderze co `nuget.exe` .

Podczas ładowania dostawców poświadczeń program `nuget.exe` przeszukuje powyższe lokalizacje w podanej kolejności, `credentialprovider*.exe` a następnie ładuje te pliki w kolejności, w jakiej zostały znalezione. Jeśli w tym samym folderze istnieje wielu dostawców poświadczeń, są one ładowane w kolejności alfabetycznej.

## <a name="creating-a-nugetexe-credential-provider"></a>Tworzenie dostawcy poświadczeń nuget.exe

Dostawca poświadczeń to plik wykonywalny wiersza polecenia o nazwie w formularzu `CredentialProvider*.exe` , który zbiera dane wejściowe, uzyskuje poświadczenia zgodnie z potrzebami, a następnie zwraca odpowiedni kod stanu wyjścia i wyjście standardowe.

Dostawca musi wykonać następujące czynności:

- Przed zainicjowaniem pozyskiwania poświadczeń należy określić, czy może podać poświadczenia dla danego identyfikatora URI. Jeśli nie, powinien zwrócić kod stanu 1 bez poświadczeń.
- Nie należy modyfikować `Nuget.Config` (na przykład w przypadku ustawienia poświadczeń).
- Obsługa konfiguracji serwera proxy HTTP we własnym zakresie, ponieważ narzędzie NuGet nie udostępnia informacji o serwerze proxy do wtyczki.
- Zwróć poświadczenia lub szczegóły błędu `nuget.exe` , pisząc obiekt odpowiedzi JSON (patrz poniżej) do stdout przy użyciu kodowania UTF-8.
- Opcjonalnie można emitować dodatkowe rejestrowanie śledzenia do STDERR. Żadne wpisy tajne nie powinny być nigdy zapisywane w stderr, ponieważ na poziomie szczegółowości "normalny" lub "szczegółowe" takie ślady są wyświetlane przez program NuGet w konsoli programu.
- Nieoczekiwane parametry powinny być ignorowane, co zapewnia zgodność z przyszłymi wersjami NuGet.

### <a name="input-parameters"></a>Parametry wejściowe

| Parametr/przełącznik |Opis|
|----------------|-----------|
| Identyfikator URI {Value} | Źródłowy identyfikator URI pakietu wymaga poświadczeń.|
| Nieinteraktywnych | Jeśli jest obecny, dostawca nie wystawia interakcyjnych wierszy. |
| Isretry | Jeśli jest obecny, oznacza to, że próba wykonania poprzedniej nieudanej próby nie powiodła się. Dostawcy zazwyczaj używają tej flagi, aby upewnić się, że pomijają istniejącą pamięć podręczną i monitują o nowe poświadczenia, jeśli jest to możliwe.|
| Poziom szczegółowości {Value} | Jeśli jest obecny, jedna z następujących wartości: "normal", "quiet" lub "Detailed". Jeśli nie podano wartości, wartością domyślną jest "normal". Dostawcy powinni używać tego jako wskazanie poziomu opcjonalnego rejestrowania do emisji do standardowego strumienia błędów. |

### <a name="exit-codes"></a>Kody zakończenia

| Kod |Wynik | Opis |
|----------------|-----------|-----------|
| 0 | Powodzenie | Pomyślnie pobrano poświadczenia i zapisano je w strumieniu stdout.|
| 1 | ProviderNotApplicable | Bieżący dostawca nie dostarcza poświadczeń dla danego identyfikatora URI.|
| 2 | Niepowodzenie | Dostawca jest poprawnym dostawcą dla danego identyfikatora URI, ale nie może podawać poświadczeń. W takim przypadku nuget.exe nie spróbuje ponownie uwierzytelniania i zakończy się niepowodzeniem. Typowym przykładem jest to, że użytkownik anuluje Logowanie interakcyjne. |

### <a name="standard-output"></a>Wyjście standardowe

| Właściwość |Uwagi|
|----------------|-----------|
| Nazwa użytkownika | Nazwa użytkownika dla żądań uwierzytelnionych.|
| Hasło | Hasło dla żądań uwierzytelnionych.|
| Komunikat | Opcjonalne szczegóły dotyczące odpowiedzi używane tylko w celu wyświetlenia dodatkowych szczegółów w przypadku awarii. |

Przykład stdout:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Rozwiązywanie problemów z dostawcą poświadczeń

W tej chwili NuGet nie zapewnia wielu bezpośrednich obsłudze debugowania niestandardowych dostawców poświadczeń; [problem 4598](https://github.com/NuGet/Home/issues/4598) śledzi tę prace.

Ponadto można wykonać następujące czynności:

- Uruchom nuget.exe z `-verbosity` przełącznikiem, aby sprawdzić szczegółowe dane wyjściowe.
- Dodaj komunikaty debugowania do `stdout` w odpowiednich miejscach.
- Upewnij się, że korzystasz z nuget.exe 3,3 lub nowszej.
- Dołącz debuger podczas uruchamiania przy użyciu tego fragmentu kodu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
