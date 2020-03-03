---
title: Dostawcy poświadczeń NuGet. exe
description: dostawcy poświadczeń NuGet. exe uwierzytelniają się ze źródłem danych i są implementowane jako pliki wykonywalne wiersza polecenia, które przestrzegają określonych konwencji.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230788"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Uwierzytelnianie kanałów informacyjnych przy użyciu programu NuGet. exe dostawcy poświadczeń

W wersji `3.3` dodano obsługę dla `nuget.exe` określonych dostawców poświadczeń. Od tego czasu w programie w wersji `4.8` [obsługiwane są dostawcy poświadczeń](NuGet-Cross-Platform-Authentication-Plugin.md) , którzy działają we wszystkich scenariuszach wiersza polecenia (`nuget.exe`, `dotnet.exe`, `msbuild.exe`).

Aby uzyskać szczegółowe informacje [na temat wszystkich](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) metod uwierzytelniania `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>odnajdywanie dostawcy poświadczeń NuGet. exe

dostawcy poświadczeń NuGet. exe można używać na trzy sposoby:

- **Globalnie**: Aby udostępnić dostawcę poświadczeń wszystkim wystąpieniu `nuget.exe` uruchomionych w ramach profilu bieżącego użytkownika, należy dodać go do `%LocalAppData%\NuGet\CredentialProviders`. Może być konieczne utworzenie folderu `CredentialProviders`. Dostawców poświadczeń można zainstalować w folderze głównym folderu `CredentialProviders` lub w podfolderze. Jeśli Dostawca poświadczeń ma wiele plików/zestawów, można użyć podfolderów, aby zachować zorganizowanie dostawców.

- **Ze zmiennej środowiskowej**: dostawcy poświadczeń można przechowywać w dowolnym miejscu i uzyskiwać dostęp do `nuget.exe` przez ustawienie zmiennej środowiskowej `%NUGET_CREDENTIALPROVIDERS_PATH%` na lokalizację dostawcy. Ta zmienna może być rozdzielaną średnikami listą (na przykład `path1;path2`), jeśli istnieje wiele lokalizacji.

- Wraz z pakietem **NuGet. exe**: dostawcy poświadczeń NuGet. exe można umieścić w tym samym folderze co `nuget.exe`.

Podczas ładowania dostawców poświadczeń `nuget.exe` przeszukuje powyższe lokalizacje, w kolejności, dla każdego pliku o nazwie `credentialprovider*.exe`, ładuje te pliki w kolejności, w jakiej zostały znalezione. Jeśli w tym samym folderze istnieje wielu dostawców poświadczeń, są one ładowane w kolejności alfabetycznej.

## <a name="creating-a-nugetexe-credential-provider"></a>Tworzenie dostawcy poświadczeń NuGet. exe

Dostawca poświadczeń to plik wykonywalny wiersza polecenia o nazwie w formularzu `CredentialProvider*.exe`, który zbiera dane wejściowe, uzyskuje poświadczenia zgodnie z potrzebami, a następnie zwraca odpowiedni kod stanu wyjścia i wyjście standardowe.

Dostawca musi wykonać następujące czynności:

- Przed zainicjowaniem pozyskiwania poświadczeń należy określić, czy może podać poświadczenia dla danego identyfikatora URI. Jeśli nie, powinien zwrócić kod stanu 1 bez poświadczeń.
- Nie należy modyfikować `Nuget.Config` (takich jak ustawienia w tym miejscu).
- Obsługa konfiguracji serwera proxy HTTP we własnym zakresie, ponieważ narzędzie NuGet nie udostępnia informacji o serwerze proxy do wtyczki.
- Zwróć informacje o poświadczeniach lub błędach do `nuget.exe` przez zapisanie obiektu odpowiedzi JSON (patrz poniżej) do strumienia stdout przy użyciu kodowania UTF-8.
- Opcjonalnie można emitować dodatkowe rejestrowanie śledzenia do STDERR. Żadne wpisy tajne nie powinny być nigdy zapisywane w stderr, ponieważ na poziomie szczegółowości "normalny" lub "szczegółowe" takie ślady są wyświetlane przez program NuGet w konsoli programu.
- Nieoczekiwane parametry powinny być ignorowane, co zapewnia zgodność z przyszłymi wersjami NuGet.

### <a name="input-parameters"></a>Parametry wejściowe

| Parametr/przełącznik |Opis|
|----------------|-----------|
| Identyfikator URI {Value} | Źródłowy identyfikator URI pakietu wymaga poświadczeń.|
| NonInteractive | Jeśli jest obecny, dostawca nie wystawia interakcyjnych wierszy. |
| Isretry | Jeśli jest obecny, oznacza to, że próba wykonania poprzedniej nieudanej próby nie powiodła się. Dostawcy zazwyczaj używają tej flagi, aby upewnić się, że pomijają istniejącą pamięć podręczną i monitują o nowe poświadczenia, jeśli jest to możliwe.|
| Poziom szczegółowości {Value} | Jeśli jest obecny, jedna z następujących wartości: "normal", "quiet" lub "Detailed". Jeśli nie podano wartości, wartością domyślną jest "normal". Dostawcy powinni używać tego jako wskazanie poziomu opcjonalnego rejestrowania do emisji do standardowego strumienia błędów. |

### <a name="exit-codes"></a>Kody zakończenia

| Kod |Wynik | Opis |
|----------------|-----------|-----------|
| 0 | Powodzenie | Pomyślnie pobrano poświadczenia i zapisano je w strumieniu stdout.|
| 1 | ProviderNotApplicable | Bieżący dostawca nie dostarcza poświadczeń dla danego identyfikatora URI.|
| 2 | Niepowodzenie | Dostawca jest poprawnym dostawcą dla danego identyfikatora URI, ale nie może podawać poświadczeń. W takim przypadku NuGet. exe nie będzie ponawiać uwierzytelniania i zakończy się niepowodzeniem. Typowym przykładem jest to, że użytkownik anuluje Logowanie interakcyjne. |

### <a name="standard-output"></a>Wyjście standardowe

| Właściwość |Uwagi|
|----------------|-----------|
| Nazwa użytkownika | Nazwa użytkownika dla żądań uwierzytelnionych.|
| Hasło | Hasło dla żądań uwierzytelnionych.|
| Komunikat | Opcjonalne szczegóły dotyczące odpowiedzi używane tylko w celu wyświetlenia dodatkowych szczegółów w przypadku awarii. |

Przykład stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Rozwiązywanie problemów z dostawcą poświadczeń

W tej chwili NuGet nie zapewnia wielu bezpośrednich obsłudze debugowania niestandardowych dostawców poświadczeń; [problem 4598](https://github.com/NuGet/Home/issues/4598) śledzi tę prace.

Można również wykonać następujące czynności:

- Uruchom plik NuGet. exe z przełącznikiem `-verbosity`, aby sprawdzić szczegółowe dane wyjściowe.
- Dodaj komunikaty debugowania do `stdout` w odpowiednich miejscach.
- Upewnij się, że używasz programu NuGet. exe 3,3 lub nowszego.
- Dołącz debuger podczas uruchamiania przy użyciu tego fragmentu kodu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
