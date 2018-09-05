---
title: Dostawcy poświadczeń nuget.exe
description: dostawcy poświadczeń nuget.exe uwierzytelnianie za pomocą kanału informacyjnego i są implementowane jako zgodne z konwencjami określone pliki wykonywalne wiersza polecenia.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550192"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Uwierzytelnianie źródła danych za pomocą dostawcy poświadczeń nuget.exe

*NuGet 3.3+*

Gdy `nuget.exe` wymaga poświadczeń do uwierzytelniania za pomocą kanału informacyjnego, szuka je w następujący sposób:

1. NuGet najpierw szuka poświadczenia w `Nuget.Config` plików.
1. NuGet następnie używa dostawcy poświadczeń wtyczki, z zastrzeżeniem kolejności podanej poniżej. (I przykład [Visual Studio Team Services Dostawca poświadczeń](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet następnie monituje użytkownika o poświadczenia w wierszu polecenia.

Należy zauważyć, że dostawcy poświadczeń, opisane w tym miejscu działają tylko w `nuget.exe` , a nie w "dotnet restore" lub Visual Studio. Dostawcy poświadczeń za pomocą programu Visual Studio, można zobaczyć [nuget.exe dostawcy poświadczeń dla programu Visual Studio](nuget-credential-providers-for-visual-studio.md)

dostawcy poświadczeń nuget.exe może służyć w 3 sposoby:

- **Globalnie**: Aby udostępnić Dostawca poświadczeń do wszystkich wystąpień `nuget.exe` uruchomienia w ramach profilu bieżącego użytkownika, dodaj ją do `%LocalAppData%\NuGet\CredentialProviders`. Może być konieczne utworzenie `CredentialProviders` folderu. Dostawcy poświadczeń, można zainstalować w katalogu głównym `CredentialProviders` folder lub podfolder. Jeśli dostawca poświadczeń ma wiele plików/zestawów, można użyć podfoldery do zachowania dostawców zorganizowane.

- **Ze zmiennej środowiskowej**: dostawcy poświadczeń, które mogą być przechowywane w dowolnym miejscu i udostępniane `nuget.exe` , ustawiając `%NUGET_CREDENTIALPROVIDERS_PATH%` zmiennej środowiskowej, aby lokalizacja dostawcy. Ta zmienna może być rozdzielaną średnikami listę (na przykład `path1;path2`) Jeśli masz wiele lokalizacji.

- **Wraz z nuget.exe**: nuget.exe dostawcy poświadczeń, które można umieścić w tym samym folderze co `nuget.exe`.

Podczas ładowania dostawcy poświadczeń `nuget.exe` wyszukuje powyższych lokalizacjach, w kolejności, dowolne pliki o nazwie `credentialprovider*.exe`, następnie ładuje te pliki w kolejności one znajdują. Jeśli istnieje wielu dostawców poświadczeń w tym samym folderze, są one załadowane w kolejności alfabetycznej.

## <a name="creating-a-nugetexe-credential-provider"></a>Tworzenie dostawcy poświadczeń nuget.exe

Dostawca poświadczeń jest pliku wykonywalnego wiersza polecenia, o nazwie w postaci `CredentialProvider*.exe`, który zbiera dane wejściowe, uzyskuje poświadczenia zgodnie z potrzebami, a następnie zwraca kod stanu zakończenia odpowiednie i standardowe dane wyjściowe.

Dostawca musi wykonaj następujące czynności:

- Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI, przed zainicjowaniem pozyskiwanie poświadczeń. W przeciwnym razie powinien zostać zwrócony kod stanu 1 bez poświadczeń.
- Nie modyfikować `Nuget.Config` (na przykład istnieje ustawienie poświadczeń).
- Konfiguracja serwera proxy HTTP uchwytu na NuGet własne, jako nie zapewnia informacje o serwerze proxy do wtyczki.
- Zwróć poświadczeń lub szczegółów błędów do `nuget.exe` , pisząc obiekt odpowiedzi JSON (patrz poniżej) do stdout, przy użyciu kodowania UTF-8.
- Opcjonalnie emitować rejestrowanie śledzenia dodatkowe stderr. Nie wpisów tajnych nigdy nie będą zapisywane w stderr, ponieważ na poziomach szczegółowości "normal" lub "szczegółowe" takie ślady są powtarzane przez NuGet do konsoli.
- Nieoczekiwany parametry powinny być ignorowane, zapewniając zgodność z nowszymi wersjami z przyszłych wersji pakietu nuget.

### <a name="input-parameters"></a>Parametry wejściowe

| Parametr/przełącznika |Opis|
|----------------|-----------|
| Identyfikator URI {value} | Pakiet źródła wymagające poświadczenia identyfikatora URI.|
| Nieinterakcyjnym | Jeśli jest obecny, dostawca nie wystawia interaktywne monity. |
| isRetry | Jeśli jest obecny, oznacza ta próba ponowienia próby zakończyły się niepowodzeniem. Dostawcy zazwyczaj używają tej flagi zapewnienie Pomiń wszelkie istniejące pamięć podręczną i monit o nowe poświadczenia, jeśli jest to możliwe.|
| Poziom szczegółowości {value} | Jeśli jest obecny, jedną z następujących wartości: "normal", "quiet" lub "szczegóły". Jeśli nie dostarczono żadnej wartości, wartość domyślna to "normal". Dostawcy należy użyć tego wskazanie poziom rejestrowania opcjonalne aby emitować na Standardowy strumień błędów. |

### <a name="exit-codes"></a>Kody zakończenia

| Kod |Wynik | Opis |
|----------------|-----------|-----------|
| 0 | Powodzenie | Poświadczenia zostały pomyślnie uzyskano i został zapisany do strumienia wyjściowego stdout.|
| 1 | ProviderNotApplicable | Bieżący dostawca nie Podaj poświadczenia dla danego identyfikatora URI.|
| 2 | Błąd | Dostawca jest prawidłowy dostawca dla danego identyfikatora URI, ale nie można udostępnić poświadczeń. W takim przypadku nuget.exe nie podejmie kolejnej próby uwierzytelniania i zakończy się niepowodzeniem. Typowym przykładem jest, gdy użytkownik anuluje interakcyjnego logowania. |

### <a name="standard-output"></a>Standardowe dane wyjściowe

| Właściwość |Uwagi|
|----------------|-----------|
| Nazwa użytkownika | Nazwa użytkownika dla żądań uwierzytelnionych.|
| Hasło | Hasło dla żądań uwierzytelnionych.|
| Komunikat | Opcjonalne szczegółowe informacje dotyczące odpowiedzi używane tylko po to, aby wyświetlić dodatkowe informacje w przypadku awarii. |

Przykład stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Rozwiązywanie problemów z dostawcy poświadczeń

Obecnie NuGet nie zapewnia znacznie bezpośredniej pomocy technicznej dla debugowanie dostawców niestandardowych poświadczeń; [wystawiać 4598](https://github.com/NuGet/Home/issues/4598) służy do śledzenia tę pracę.

Można również wykonać następujące czynności:

- Uruchom nuget.exe z `-verbosity` przełącznika do wglądu w szczegółowe dane wyjściowe.
- Dodawać komunikaty debugowania do `stdout` w odpowiednich miejscach.
- Pamiętaj, że używasz nuget.exe 3.3 lub nowszej.
- Dołącz debuger po uruchomieniu na następujący fragment kodu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Aby uzyskać dalszą pomoc [przesłać żądanie pomocy technicznej nuget.org](https://www.nuget.org/policies/Contact).
