---
title: Dostawcy poświadczeń nuget.exe
description: nuget.exe dostawcy poświadczeń uwierzytelniania za pomocą źródło danych i są zaimplementowane jako zgodne z konwencjami określone elementy wykonywalne wiersza polecenia.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: ebd3354c298eae8bc8158a987327374ac4a8d4f0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818763"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Źródła danych za pomocą nuget.exe dostawcy poświadczeń uwierzytelniania

*NuGet 3.3+*

Gdy `nuget.exe` potrzebuje poświadczeń do uwierzytelniania źródło szuka je w następujący sposób:

1. NuGet najpierw szuka poświadczeń w `Nuget.Config` plików.
1. Następnie NuGet używa dostawcy poświadczeń wtyczki, mogą ulec kolejności podanej poniżej. (I przykład [programu Visual Studio Team Services Dostawca poświadczeń](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet następnie monituje użytkownika o poświadczenia w wierszu polecenia.

Należy pamiętać, że dostawcy poświadczeń opisanych tutaj działa tylko w `nuget.exe` , a nie w "dotnet restore" lub Visual Studio. Dla dostawcy poświadczeń z programem Visual Studio, zobacz [nuget.exe dostawcy poświadczeń dla programu Visual Studio](nuget-credential-providers-for-visual-studio.md)

dostawcy poświadczeń nuget.exe mogą być używane na 3 sposoby:

- **Globalny**: Aby dostawca poświadczeń dostępne dla wszystkich wystąpień `nuget.exe` uruchamiana profilu bieżącego użytkownika, dodaj go do `%LocalAppData%\NuGet\CredentialProviders`. Może być konieczne utworzenie `CredentialProviders` folderu. Dostawcy poświadczeń można zainstalować w katalogu głównym `CredentialProviders` folder lub podfolder. Jeśli dostawca poświadczeń ma wiele plików/zestawów, można użyć podfoldery do zachowania dostawców organizowane.

- **Ze zmiennej środowiskowej**: może być przechowywany w dowolnym miejscu i dostępny dla dostawcy poświadczeń `nuget.exe` przez ustawienie `%NUGET_CREDENTIALPROVIDERS_PATH%` zmiennej środowiskowej do lokalizacji dostawcy. Ta zmienna może być rozdzielana średnikami lista (na przykład `path1;path2`) Jeśli masz wiele lokalizacji.

- **Obok nuget.exe**: nuget.exe dostawcy poświadczeń można umieścić w tym samym folderze co `nuget.exe`.

Podczas ładowania dostawcy poświadczeń `nuget.exe` wyszukuje powyższych lokalizacjach, w kolejności, dowolne pliki o nazwie `credentialprovider*.exe`, następnie ładuje tych plików w kolejności, w przypadku można odnaleźć. Jeśli istnieje wielu dostawców poświadczeń w tym samym folderze, są one ładowane w kolejności alfabetycznej.

## <a name="creating-a-nugetexe-credential-provider"></a>Tworzenie dostawcy poświadczeń nuget.exe

Dostawca poświadczeń jest pliku wykonywalnego wiersza polecenia o nazwie w postaci `CredentialProvider*.exe`, która gromadzi dane wejściowe, uzyskuje poświadczenia zależnie od potrzeb, a następnie zwraca kod stanu zakończenia odpowiednie i wyjścia standardowego.

Dostawca, wykonaj następujące czynności:

- Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI przed zainicjowaniem przejęcie poświadczeń. Jeśli nie, powinien zostać zwrócony kod stanu 1 bez poświadczeń.
- Nie modyfikować `Nuget.Config` (na przykład istnieje ustawienie poświadczeń).
- Konfiguracja serwera proxy obsługi HTTP na jego własnej jako NuGet nie zawiera informacje o serwerze proxy do wtyczki.
- Zwraca poświadczeń lub szczegółów błędów do `nuget.exe` pisząc obiekt odpowiedzi JSON (patrz poniżej) do stdout, przy użyciu kodowania UTF-8.
- Opcjonalnie Emituj rejestrowanie śledzenia dodatkowe stderr. Nie kluczy tajnych kiedykolwiek powinna być zapisana stderr, ponieważ na poziomie szczegółowości "normal" lub "szczegółowe" takie śladów powtarzana przez narzędzie NuGet w konsoli.
- Nieoczekiwany parametrów powinny być ignorowane, zapewniając zgodność z nowszymi wersjami w przyszłych wersjach programu NuGet.

### <a name="input-parameters"></a>Parametry wejściowe

| Parametr/przełącznika |Opis|
|----------------|-----------|
| Identyfikator URI {value} | Pakiet źródłowe poświadczenia wymagające identyfikatora URI.|
| Nieinterakcyjne | Jeśli jest obecny, dostawcy nie wystawiać interaktywne monity. |
| IsRetry | Jeśli jest obecny, wskazuje ta próba ponowienia wcześniej nieudanej próby. Zazwyczaj dostawcy używają tej flagi Aby pominąć wszystkie istniejące pamięci podręcznej i monit o podanie poświadczeń nowe, jeśli to możliwe.|
| Poziom szczegółowości {value} | Jeśli nie istnieje jeden z następujących wartości: "normal", "quiet" lub "szczegóły". Jeśli nie dostarczono żadnej wartości, domyślnie "normal". Dostawców należy użyć tego wskaźnik poziomu rejestrowania opcjonalne do wysyłania do Standardowy strumień błędów. |

### <a name="exit-codes"></a>Kody zakończenia

| Kod |Wynik | Opis |
|----------------|-----------|-----------|
| 0 | Powodzenie | Poświadczenia zostały pomyślnie uzyskano i zapisano do stdout.|
| 1 | ProviderNotApplicable | Bieżący dostawca nie Podaj poświadczenia dla danego identyfikatora URI.|
| 2 | Błąd | Dostawca jest poprawna dostawca dla danego identyfikatora URI, ale nie można udostępnić poświadczeń. W takim przypadku nuget.exe nie podejmie kolejnej próby uwierzytelniania i zakończy się niepowodzeniem. Typowym przykładem jest, gdy użytkownik anuluje interakcyjnego logowania. |

### <a name="standard-output"></a>Standardowe dane wyjściowe

| Właściwość |Uwagi|
|----------------|-----------|
| Nazwa użytkownika | Nazwa użytkownika dla żądań uwierzytelnionych.|
| Hasło | Hasło dla żądań uwierzytelnionych.|
| Komunikat | Opcjonalne szczegóły dotyczące odpowiedzi służą wyłącznie do zawierają dodatkowe szczegółowe informacje w przypadku awarii. |

Przykład stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Rozwiązywanie problemów z dostawcy poświadczeń

Obecnie NuGet nie obsługują wiele bezpośredniego debugowanie dostawców niestandardowych poświadczeń; [wystawiać 4598](https://github.com/NuGet/Home/issues/4598) służy do śledzenia tę pracę.

Można również wykonać następujące czynności:

- Uruchom nuget.exe z `-verbosity` przełącznik, aby sprawdzić szczegółowe dane wyjściowe.
- Komunikaty debugowania, aby dodać `stdout` w odpowiednich miejscach.
- Pamiętaj, że używasz nuget.exe 3.3 lub nowszej.
- Dołącz debugera przy uruchamianiu z następujący fragment kodu:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Aby uzyskać dalszą pomoc [przesłać żądanie obsługi nuget.org](https://www.nuget.org/policies/Contact).
