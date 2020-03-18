---
title: Wtyczki Międzyplatformowe NuGet
description: Dodatki Międzyplatformowe NuGet dla NuGet. exe, dotnet. exe, MSBuild. exe i Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429109"
---
# <a name="nuget-cross-platform-plugins"></a>Wtyczki Międzyplatformowe NuGet

W NuGet 4.8 + Obsługa wtyczek międzyplatformowych została dodana.
Osiągnięto to przez utworzenie nowego modelu rozszerzalności wtyczki, który musi być zgodny z rygorystycznym zestawem reguł operacji.
Wtyczki to samodzielne pliki wykonywalne (runnables w środowisku .NET Core), które klienci NuGet uruchamiają w osobnym procesie.
Jest to jednokrotne zapis, uruchom wszędzie. Będzie on działał ze wszystkimi narzędziami klienta NuGet.
Wtyczki mogą być albo .NET Framework (NuGet. exe, MSBuild. exe i Visual Studio) lub .NET Core (dotnet. exe).
Jest zdefiniowany protokół komunikacji z wersjami między klientem NuGet a wtyczką. Podczas uzgadniania uruchamiania, 2 procesy negocjują wersję protokołu.

Aby uwzględnić wszystkie scenariusze narzędzi klienta NuGet, trzeba mieć zarówno .NET Framework, jak i wtyczkę .NET Core.
Poniżej opisano kombinacje klienta/struktury wtyczek.

| Narzędzie klienta  | .NET Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet. exe | .NET Framework |
| MSBuild. exe | .NET Framework |
| NuGet. exe na mono | .NET Framework |

## <a name="how-does-it-work"></a>Jak to działa

Przepływ pracy wysokiego poziomu można opisać w następujący sposób:

1. Pakiet NuGet odnajduje dostępne wtyczki.
1. Jeśli ma to zastosowanie, pakiet NuGet przejdzie iterację na wtyczkach w kolejności priorytetu i uruchomi je po jednym.
1. Pakiet NuGet użyje pierwszej wtyczki, która może obsłużyć żądanie.
1. Wtyczki zostaną wyłączone, gdy nie będą już potrzebne.

## <a name="general-plugin-requirements"></a>Ogólne wymagania wtyczki

Bieżąca wersja protokołu to *2.0.0*.
W tej wersji wymagania są następujące:

- Mają prawidłowy zestaw zaufanych podpisów Authenticode, które będą uruchamiane w systemie Windows i mono. Nie ma jeszcze specjalnych wymagań zaufania dla zestawów uruchomionych w systemach Linux i Mac. [Istotny problem](https://github.com/NuGet/Home/issues/6702)
- Obsługa bezstanowego uruchamiania w ramach bieżącego kontekstu zabezpieczeń narzędzi klienckich programu NuGet. Na przykład narzędzia klienta NuGet nie będą wykonywały podniesienia uprawnień ani dodatkowego inicjowania poza protokołem wtyczki opisanym w dalszej części.
- Nie jest interaktywny, chyba że zostanie jawnie określony.
- Zgodność z wynegocjowaną wersją protokołu wtyczki.
- Odpowiadanie na wszystkie żądania w rozsądnym czasie.
- Honorować żądania anulowania dla każdej operacji w toku.

Specyfikacja techniczna została szczegółowo opisana w następujących kwestiach:

- [Wtyczka pobierania pakietu NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Wtyczka do uwierzytelniania między płytkami NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Interakcja klienta — wtyczka

Narzędzia klienta i wtyczki programu NuGet komunikują się z notacją JSON przez strumienie standardowe (stdin, stdout, stderr). Wszystkie dane muszą być kodowane w formacie UTF-8.
Wtyczki są uruchamiane z argumentem "-plugin". W przypadku, gdy użytkownik bezpośrednio uruchamia plik wykonywalny wtyczki bez tego argumentu, wtyczka może dać komunikat informacyjny, a nie oczekuje na uzgadnianie protokołu.
Limit czasu uzgadniania protokołu wynosi 5 sekund. Wtyczka powinna zakończyć instalację tak jak najkrótszej ilości, jak to możliwe.
Narzędzia klienta NuGet będą badać obsługiwane operacje wtyczki, przekazując indeks usługi dla źródła NuGet. Wtyczka może użyć indeksu usługi, aby sprawdzić obecność obsługiwanych typów usług.

Komunikacja między narzędziami klienta NuGet a wtyczką jest dwukierunkowa. Każde żądanie ma limit czasu wynoszący 5 sekund. Jeśli operacje mają trwać dłużej, proces powinien wysłać komunikat o postępie, aby zapobiec przekroczeniu limitu czasu żądania. Po 1 minucie braku aktywności wtyczka jest uważana za bezczynną i jest zamykana.

## <a name="plugin-installation-and-discovery"></a>Instalowanie i odnajdywanie wtyczki

Wtyczki zostaną odnalezione za pośrednictwem struktury katalogów na podstawie Konwencji.
Scenariusze ciągłej integracji/ciągłego wdrażania i Użytkownicy zaawansowani mogą używać zmiennych środowiskowych, aby przesłonić zachowanie. W przypadku używania zmiennych środowiskowych dozwolone są tylko ścieżki bezwzględne. Należy pamiętać, że `NUGET_NETFX_PLUGIN_PATHS` i `NUGET_NETCORE_PLUGIN_PATHS` są dostępne tylko w przypadku używania 5.3 + wersji narzędzi NuGet i nowszych.

- `NUGET_NETFX_PLUGIN_PATHS` — definiuje wtyczki, które będą używane przez narzędzia oparte na .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio). Ma pierwszeństwo przed `NUGET_PLUGIN_PATHS`. (Tylko wersja 5.3 programu NuGet)
- `NUGET_NETCORE_PLUGIN_PATHS` — definiuje wtyczki, które będą używane przez narzędzia oparte na oprogramowaniu .NET Core (dotnet. exe). Ma pierwszeństwo przed `NUGET_PLUGIN_PATHS`. (Tylko wersja 5.3 programu NuGet)
- `NUGET_PLUGIN_PATHS` — definiuje wtyczki, które będą używane dla tego procesu NuGet, a priorytet zachowano. Jeśli ta zmienna środowiskowa jest ustawiona, zastępuje ona metodę odnajdywania opartą na Konwencji. Ignorowany, jeśli określono jedną z zmiennych określonych dla struktury.
-  Lokalizacja użytkownika — lokalizacja główna narzędzia NuGet w `%UserProfile%/.nuget/plugins`. Ta lokalizacja nie może być przesłonięta. Dla wtyczek platformy .NET Core i .NET Framework zostanie użyty inny katalog główny.

| .NET Framework | Główna lokalizacja odnajdowania  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Każda wtyczka powinna być zainstalowana we własnym folderze.
Punkt wejścia wtyczki będzie nazwą zainstalowanego folderu z rozszerzeniami dll dla programu .NET Core i rozszerzeniem exe dla .NET Framework.

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> Obecnie nie ma żadnego scenariusza użytkownika dla instalacji wtyczek. Jest to proste przeniesienie wymaganych plików do wstępnie wskazanej lokalizacji.

## <a name="supported-operations"></a>Obsługiwane operacje

W ramach nowego protokołu wtyczki są obsługiwane dwie operacje.

| Nazwa operacji | Minimalna wersja protokołu | Minimalna wersja klienta NuGet |
| -------------- | ----------------------- | --------------------- |
| Pobierz pakiet | 1.0.0 | 4.3.0 |
| [Uwierzytelnianie](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Uruchamianie wtyczek w prawidłowym środowisku uruchomieniowym

W przypadku pakietu NuGet w scenariuszach programu dotnet. exe wtyczki muszą być w stanie wykonać w tym konkretnym czasie wykonywania programu dotnet. exe.
Jest on dostawcą wtyczki i konsumentem, aby upewnić się, że jest używana kombinacja dotnet. exe/wtyczka.
Potencjalny problem może wystąpić w przypadku wtyczek do lokalizacji użytkownika, gdy na przykład program dotnet. exe w środowisku uruchomieniowym 2,0 próbuje użyć wtyczki zarejestrowanej dla środowiska uruchomieniowego 2,1.

## <a name="capabilities-caching"></a>Buforowanie możliwości

Weryfikacja zabezpieczeń i Tworzenie wystąpień wtyczek jest kosztowne. Operacja pobierania odbywa się częściej niż operacja uwierzytelniania, jednak średni użytkownik programu NuGet może mieć tylko wtyczkę uwierzytelniania.
Aby ulepszyć środowisko, pakiet NuGet będzie buforować oświadczenia operacji dla danego żądania. Ta pamięć podręczna jest na wtyczkę z kluczem wtyczki w ścieżce wtyczki, a okres ważności tej pamięci podręcznej to 30 dni. 

Pamięć podręczna znajduje się w `%LocalAppData%/NuGet/plugins-cache` i przesłonięta ze zmienną środowiskową `NUGET_PLUGINS_CACHE_PATH`. Aby wyczyścić tę [pamięć podręczną](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jeden może uruchomić polecenie Locals z opcją `plugins-cache`.
Opcja `all` locales spowoduje teraz również usunięcie pamięci podręcznej dodatków. 

## <a name="protocol-messages-index"></a>Indeks komunikatów protokołu

Komunikaty o wersji protokołu *1.0.0* :

1.  Zamykanie
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie nie będzie zawierać ładunku
    * Nie oczekiwano odpowiedzi.  Właściwa odpowiedź dotyczy procesu wtyczki, aby zakończyć pracę.

2.  Kopiuj pliki w pakiecie
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Identyfikator i wersja pakietu
        * Lokalizacja repozytorium źródłowego pakietu
        * ścieżka katalogu docelowego
        * wyliczalne pliki w pakiecie do skopiowania do ścieżki katalogu docelowego
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * wyliczalne pełne ścieżki dla skopiowanych plików w katalogu docelowym, jeśli operacja zakończyła się pomyślnie

3.  Kopiuj plik pakietu (. nupkg)
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Identyfikator i wersja pakietu
        * Lokalizacja repozytorium źródłowego pakietu
        * ścieżka pliku docelowego
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji

4.  Pobieranie poświadczeń
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Lokalizacja repozytorium źródłowego pakietu
        * kod stanu HTTP uzyskany z repozytorium źródłowego pakietu przy użyciu bieżących poświadczeń
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * Nazwa użytkownika, jeśli jest dostępna
        * hasło, jeśli jest dostępne

5.  Pobierz pliki w pakiecie
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Identyfikator i wersja pakietu
        * Lokalizacja repozytorium źródłowego pakietu
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * wyliczalne ścieżki plików w pakiecie, jeśli operacja zakończyła się pomyślnie

6.  Pobierz oświadczenia operacji 
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Usługa index. JSON dla źródła pakietu
        * Lokalizacja repozytorium źródłowego pakietu
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * wyliczalne obsługiwane operacje (np.: Pobieranie pakietu), jeśli operacja zakończyła się pomyślnie.  Jeśli wtyczka nie obsługuje źródła pakietu, wtyczka musi zwrócić pusty zestaw obsługiwanych operacji.

> [!Note]
> Ten komunikat został zaktualizowany w wersji *2.0.0*. Klient zachowuje zgodność z poprzednimi wersjami.

7.  Pobierz skrót pakietu
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Identyfikator i wersja pakietu
        * Lokalizacja repozytorium źródłowego pakietu
        * algorytm wyznaczania wartości skrótu
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * skrót pliku pakietu przy użyciu żądanego algorytmu wyznaczania wartości skrótu, jeśli operacja zakończyła się pomyślnie

8.  Pobierz wersje pakietu
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Identyfikator pakietu
        * Lokalizacja repozytorium źródłowego pakietu
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * wyliczalne wersje pakietów, jeśli operacja zakończyła się pomyślnie

9.  Pobierz indeks usługi
    * Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Lokalizacja repozytorium źródłowego pakietu
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * indeks usługi, jeśli operacja zakończyła się pomyślnie

10.  Uzgadniania
     * Kierunek żądania: < NuGet — wtyczka >
     * Żądanie będzie zawierać:
         * Bieżąca wersja protokołu wtyczki
         * Minimalna obsługiwana wersja protokołu wtyczki
     * Odpowiedź będzie zawierać:
         * kod odpowiedzi wskazujący wynik operacji
         * wynegocjowana wersja protokołu, jeśli operacja zakończyła się pomyślnie.  Niepowodzenie spowoduje zakończenie wtyczki.

11.  Initialize
     * Kierunek żądania: wtyczka > NuGet
     * Żądanie będzie zawierać:
         * wersja narzędzia klienta NuGet
         * efektywny język narzędzia klienckiego NuGet.  Uwzględnia to ustawienie ForceEnglishOutput, jeśli jest używane.
         * domyślny limit czasu żądania, który zastępuje domyślny protokół.
     * Odpowiedź będzie zawierać:
         * kod odpowiedzi wskazujący wynik operacji.  Niepowodzenie spowoduje zakończenie wtyczki.

12.  Log
     * Kierunek żądania: wtyczka > NuGet
     * Żądanie będzie zawierać:
         * poziom rejestrowania żądania
         * komunikat do zarejestrowania
     * Odpowiedź będzie zawierać:
         * kod odpowiedzi wskazujący wynik operacji.

13.  Wyjdź z monitorowania procesu NuGet
     * Kierunek żądania: wtyczka > NuGet
     * Żądanie będzie zawierać:
         * Identyfikator procesu NuGet
     * Odpowiedź będzie zawierać:
         * kod odpowiedzi wskazujący wynik operacji.

14.  Pakiet pobierania z wyprzedzeniem
     * Kierunek żądania: wtyczka > NuGet
     * Żądanie będzie zawierać:
         * Identyfikator i wersja pakietu
         * Lokalizacja repozytorium źródłowego pakietu
     * Odpowiedź będzie zawierać:
         * kod odpowiedzi wskazujący wynik operacji

15.  Ustawianie poświadczeń
     * Kierunek żądania: wtyczka > NuGet
     * Żądanie będzie zawierać:
         * Lokalizacja repozytorium źródłowego pakietu
         * Ostatnia znana nazwa użytkownika źródła pakietu, jeśli jest dostępna
         * ostatnie znane hasło źródłowe pakietu, jeśli jest dostępne
         * Ostatnia znana nazwa użytkownika serwera proxy, jeśli jest dostępna
         * ostatnie znane hasło serwera proxy, jeśli jest dostępne
     * Odpowiedź będzie zawierać:
         * kod odpowiedzi wskazujący wynik operacji

16.  Ustawianie poziomu dziennika
     * Kierunek żądania: wtyczka > NuGet
     * Żądanie będzie zawierać:
         * domyślny poziom dziennika
     * Odpowiedź będzie zawierać:
         * kod odpowiedzi wskazujący wynik operacji

Komunikaty *2.0.0* w wersji protokołu

17. Pobierz oświadczenia operacji

* Kierunek żądania: wtyczka > NuGet
    * Żądanie będzie zawierać:
        * Usługa index. JSON dla źródła pakietu
        * Lokalizacja repozytorium źródłowego pakietu
    * Odpowiedź będzie zawierać:
        * kod odpowiedzi wskazujący wynik operacji
        * wyliczalne obsługiwane operacje, jeśli operacja zakończyła się pomyślnie.  Jeśli wtyczka nie obsługuje źródła pakietu, wtyczka musi zwrócić pusty zestaw obsługiwanych operacji.

    Jeśli indeks usługi i źródło pakietu mają wartość null, wtyczka może odpowiedzieć na uwierzytelnianie.

18. Uzyskiwanie poświadczeń uwierzytelniania

* Kierunek żądania: wtyczka > NuGet
* Żądanie będzie zawierać:
    * URI
    * Isretry
    * NonInteractive
    * Zashowdialog
* Odpowiedź będzie zawierać
    * Nazwa użytkownika
    * Hasło
    * Komunikat
    * Lista typów uwierzytelniania
    * MessageResponseCode
