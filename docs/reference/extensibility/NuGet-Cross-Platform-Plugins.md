---
title: NuGet cross platform wtyczek
description: NuGet cross platform wtyczek NuGet.exe, dotnet.exe, msbuild.exe i programu Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794199"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet cross platform wtyczek

W pakiecie NuGet 4.8 + została dodana obsługa wielu platform, wtyczki.
Osiągnięto to dzięki przez utworzenie nowego modelu rozszerzalności wtyczki, który ma być zgodna z ograniczeniami zestawu reguł działania.
Wtyczki są niezależne pliki wykonywalne (runnables w środowisku .NET Core), które klienci programu NuGet, uruchom w oddzielnym procesie.
Jest to wartość true, zapis raz uruchomić wszędzie, gdzie dodatku typu plug-in. Będzie ona współdziałać z wszystkich narzędzi klienta programu NuGet.
Wtyczki można .NET Framework (NuGet.exe, MSBuild.exe i programu Visual Studio) lub .NET Core (dotnet.exe).
Protokół komunikacyjny numerów wersji między klientem NuGet i wtyczka jest zdefiniowana. Podczas uzgadniania uruchamiania 2 procesy negocjowania protokołu wersji.

Aby uwzględnić wszystkie scenariusze narzędzia klienta NuGet, należałoby jednej wtyczki platformy .NET Core i .NET Framework.
Poniżej przedstawiono kombinacje klienta/framework wtyczki.

| Narzędzie klienta  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| DotNet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe na platformy Mono | .NET Framework |

## <a name="how-does-it-work"></a>Jak to działa

Przepływ pracy wysokiego poziomu, można przedstawić w następujący sposób:

1. NuGet odnajduje dostępne dodatki.
1. Jeśli ma to zastosowanie, NuGet, będzie ona przechodzić przez wtyczki w kolejności priorytetu i uruchamia je jeden po drugim.
1. NuGet użyje pierwszego wtyczkę, która może obsłużyć żądania.
1. Wtyczki zostanie zamknięty, gdy nie są już potrzebne.

## <a name="general-plugin-requirements"></a>Wymagania ogólne wtyczki

Bieżąca wersja protokołu jest *2.0.0*.
W tej wersji wymagania są następujące:

- Należy mieć prawidłowy i zaufanej Authenticode podpisu zestawów, które będzie działać w Windows i platformy Mono. Nie jest wymagane specjalne zaufania dla zestawów w systemie Linux i Mac jeszcze uruchomione. [Odpowiednie problem](https://github.com/NuGet/Home/issues/6702)
- Obsługa bezstanowych, uruchamiania w kontekście zabezpieczeń bieżącego narzędzia klienta programu NuGet. Na przykład narzędzia klienta programu NuGet nie będzie wykonywać podniesienia uprawnień lub dodatkowe inicjowania poza protokołu wtyczki opisanym w dalszej części.
- Być nieinterakcyjny, chyba że jawnie określony.
- Być zgodne z wersji protokołu wynegocjowanym wtyczki.
- Odpowiedz na wszystkie żądania w rozsądnym czasie.
- Honorować anulowania żądania dla każdej operacji w toku.

Specyfikacja techniczna jest opisany bardziej szczegółowo w specyfikacji następujące:

- [Wtyczka pobierania pakietu NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet krzyżowe wtyczki uwierzytelniania plat](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Klient — interakcji wtyczki

Narzędzia klienta programu NuGet i wtyczki komunikują się z JSON za pośrednictwem standardowych strumieni (stdin, stdout, stderr). Wszystkie dane muszą być zakodowane w formacie UTF-8.
Wtyczki są uruchamiane z argumentem "-wtyczki". W przypadku, gdy użytkownik uruchamia bezpośrednio pliku wykonywalnego bez tego argumentu wtyczki, wtyczka może dać komunikat informacyjny, zamiast czekać na uzgadnianie protokołu.
Upłynął limit czasu protokołu uzgadniania to 5 sekund. Wtyczka powinno zająć instalacji w jako ograniczony ilości, jak to możliwe.
Narzędzia klienta programu NuGet zapytanie obsługiwane operacje wtyczki, przekazując w indeksie usługi dla źródła pakietów NuGet. Wtyczki mogą używać indeksu usługi pod kątem obecności obsługiwanych typów usług.

Komunikacja między narzędzia klienta programu NuGet i wtyczka jest dwukierunkowy. Każde żądanie ma limit czasu równy 5 sekund. Jeśli operacje są powinien trwać dłużej odpowiedniego procesu powinien wysłać komunikat o postępie, aby uniemożliwić żądania z przekroczeniem limitu czasu. Po 1 min braku wtyczkę uznaje się bezczynności i jest wyłączony.

## <a name="plugin-installation-and-discovery"></a>Instalowanie wtyczki i odnajdywania

Wtyczki zostaną odnalezione za pośrednictwem struktury katalogów oparte na Konwencji.
Scenariusze ciągłej integracji/ciągłego Dostarczania i użytkownicy zaawansowani, można użyć zmiennej środowiskowej zastąpić zachowanie.

- `NUGET_PLUGIN_PATHS` -Definiuje wtyczki, który będzie używany dla tego procesu NuGet priorytet zastrzeżone. Jeśli ustawiono tę zmienną środowiskową, zastępuje ona odnajdywanie oparte na Konwencji.
-  Lokalizacja użytkownika, lokalizacji głównej NuGet w `%UserProfile%/.nuget/plugins`. Ta lokalizacja nie może zostać zastąpiony. Katalog główny różnych będzie używany dla wtyczek platformy .NET Core i .NET Framework.

| Framework | Lokalizacja odnajdywania główna  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Każdy dodatek typu plug-in powinien być zainstalowany w jego własnym folderze.
Punkt wejścia wtyczki będzie Nazwa zainstalowanego folderu, z rozszerzeniem dll dla platformy .NET Core i rozszerzenie .exe na platformie .NET.

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
> Obecnie jest nie scenariusza użytkownika do zainstalowania wtyczki. Jest tak proste, jak przenoszenie wymaganych plików do określonej lokalizacji.

## <a name="supported-operations"></a>Obsługiwane operacje

Dwie operacje są obsługiwane w ramach nowego protokołu wtyczki.

| Nazwa operacji | Wersja minimalna protokołu | Minimalna wersja klienta NuGet |
| -------------- | ----------------------- | --------------------- |
| Pobierz pakiet | 1.0.0 | 4.3.0 |
| [Uwierzytelnianie](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Uruchamiania wtyczek w obszarze poprawne środowiska uruchomieniowego

Dla pakietu NuGet w scenariuszach dotnet.exe wtyczek muszą być możliwe do wykonania w ramach tego określonego środowiska uruchomieniowego programu dotnet.exe.
Jest ona włączona dostawca wtyczki i konsumentów, upewnij się, że jest używana kombinacja dotnet.exe/plugin zgodny.
Potencjalny problem może wystąpić z wtyczek lokalizacji użytkownika, gdy na przykład, dotnet.exe w obszarze 2.0 środowiska uruchomieniowego próbuje użyć wtyczki, przeznaczony dla środowiska uruchomieniowego 2.1.

## <a name="capabilities-caching"></a>Funkcje pamięci podręcznej

Weryfikacja zabezpieczeń i wystąpienia wtyczki jest kosztowne. Operacja pobierania odbywa się sposób częściej niż operację uwierzytelniania, jednak średni użytkownik NuGet jest tylko może mieć wtyczki uwierzytelniania.
Aby ulepszyć środowisko pracy, NuGet będzie buforować oświadczeń operacji dla danego żądania. Ta pamięć podręczna odbywa się dla wtyczki za pomocą klucza wtyczka jest ścieżka wtyczki, a czas wygaśnięcia pamięci podręcznej tej możliwości wynosi 30 dni. 

Pamięć podręczna znajduje się w `%LocalAppData%/NuGet/plugins-cache` i zostać zastąpiona przez zmienną środowiskową `NUGET_PLUGINS_CACHE_PATH`. Aby wyczyścić to [pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jedno uruchomienie, aby zmienne polecenia `plugins-cache` opcji.
`all` Opcja lokalne teraz spowoduje również usunięcie pamięci podręcznej wtyczek. 

## <a name="protocol-messages-index"></a>Indeks komunikaty protokołu

Wersja protokołu *1.0.0* wiadomości:

1.  Zamknięcie
    * Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie zawiera ładunek
    * Brak odpowiedzi jest oczekiwany.  Właściwej odpowiedzi jest niezwłocznie zakończyć działanie procesu wtyczki.

2.  Skopiuj pliki w pakiecie
    * Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie będzie zawierać:
        * Identyfikator pakietu i wersję
        * repozytorium lokalizacji źródłowej pakietu
        * Ścieżka katalogu docelowego
        * Element wyliczalny z plików w pakiecie, który ma być kopiowana ścieżkę katalogu docelowego
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Element wyliczalny z pełnej ścieżki do kopiowanych plików w katalogu docelowym, jeśli operacja zakończyła się pomyślnie

3.  Skopiuj plik pakietu (.nupkg)
    * Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie będzie zawierać:
        * Identyfikator pakietu i wersję
        * repozytorium lokalizacji źródłowej pakietu
        * Ścieżka pliku docelowego
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji

4.  Uzyskiwanie poświadczeń
    * Żądanie kierunek: wtyczka -> NuGet
    * Żądanie będzie zawierać:
        * repozytorium lokalizacji źródłowej pakietu
        * Kod stanu HTTP, które są uzyskiwane z repozytorium źródłowym pakietu przy użyciu bieżących poświadczeń
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Nazwa użytkownika, jeśli jest dostępny
        * hasło, jeśli jest dostępny

5.  Pobierz pliki w pakiecie
    * Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie będzie zawierać:
        * Identyfikator pakietu i wersję
        * repozytorium lokalizacji źródłowej pakietu
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Element wyliczalny z ścieżki plików w pakiecie, jeśli operacja zakończyła się pomyślnie

6.  Rozpoczynanie operacji oświadczeń 
    * Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie będzie zawierać:
        * index.json usługi dla źródła pakietów
        * repozytorium lokalizacji źródłowej pakietu
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Element wyliczalny z obsługiwanych operacji (np.: Pobieranie pakietu) Jeśli operacja zakończyła się pomyślnie.  Jeśli wtyczka nie obsługuje źródło pakietów, wtyczka musi zwracać pusty zestaw obsługiwanych operacji.

> [!Note]
> Ten komunikat został zaktualizowany w wersji *2.0.0*. Jest na komputerze klienckim w celu zachowania zgodności z poprzednimi wersjami.

7.  Pobierz skrót pakietu
    * Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie będzie zawierać:
        * Identyfikator pakietu i wersję
        * repozytorium lokalizacji źródłowej pakietu
        * Algorytm wyznaczania wartości skrótu
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Skrót pliku pakietu, przy użyciu algorytmu mieszania żądanego, jeśli operacja zakończyła się pomyślnie

8.  Pobieranie wersji pakietu
    * Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie będzie zawierać:
        * Identyfikator pakietu
        * repozytorium lokalizacji źródłowej pakietu
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Element wyliczalny z wersji pakietu, jeśli operacja zakończyła się pomyślnie

9.  Pobierz indeks usług
    * Żądanie kierunek: wtyczka -> NuGet
    * Żądanie będzie zawierać:
        * repozytorium lokalizacji źródłowej pakietu
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Indeks usług, jeśli operacja zakończyła się pomyślnie

10.  Uzgadnianie
     * Żądanie kierunek: wtyczka NuGet <> —
     * Żądanie będzie zawierać:
         * Bieżąca wersja protokołu wtyczki
         * Minimalna obsługiwana wersja protokołu wtyczki
     * Odpowiedź będzie zawierać:
         * Kod odpowiedzi, wskazując wynik operacji
         * Wersja wynegocjowanym protokołem, jeśli operacja zakończyła się pomyślnie.  Błąd spowoduje zakończenie wtyczki.

11.  Inicjowanie
     * Żądanie kierunek: NuGet -> Wtyczki
     * Żądanie będzie zawierać:
         * wersja narzędzia NuGet klienta
         * NuGet narzędzia skuteczne języku klienta.  Trwa to pod uwagę ustawienie ForceEnglishOutput, jeśli używany.
         * Domyślny limit czasu żądania, która zastępuje domyślną protokołu.
     * Odpowiedź będzie zawierać:
         * Kod odpowiedzi, wskazując wynik operacji.  Błąd spowoduje zakończenie wtyczki.

12.  Log
     * Żądanie kierunek: wtyczka -> NuGet
     * Żądanie będzie zawierać:
         * poziom rejestrowania dla żądania
         * komunikat do zarejestrowania
     * Odpowiedź będzie zawierać:
         * Kod odpowiedzi, wskazując wynik operacji.

13.  Zakończenie procesu NuGet monitora
     * Żądanie kierunek: NuGet -> Wtyczki
     * Żądanie będzie zawierać:
         * Identyfikator procesu NuGet
     * Odpowiedź będzie zawierać:
         * Kod odpowiedzi, wskazując wynik operacji.

14.  Pakiet pobierania z wyprzedzeniem
     * Żądanie kierunek: NuGet -> Wtyczki
     * Żądanie będzie zawierać:
         * Identyfikator pakietu i wersję
         * repozytorium lokalizacji źródłowej pakietu
     * Odpowiedź będzie zawierać:
         * Kod odpowiedzi, wskazując wynik operacji

15.  Ustaw poświadczenia
     * Żądanie kierunek: NuGet -> Wtyczki
     * Żądanie będzie zawierać:
         * repozytorium lokalizacji źródłowej pakietu
         * ostatni znany pakiet źródła nazwę użytkownika, jeśli jest dostępny
         * ostatnie hasło źródła znanych pakietu, jeśli jest dostępny
         * ostatni znany nazwa użytkownika serwera proxy, jeśli jest dostępny
         * ostatnie hasło znanych serwera proxy, jeśli jest dostępny
     * Odpowiedź będzie zawierać:
         * Kod odpowiedzi, wskazując wynik operacji

16.  Ustaw poziom dziennika
     * Żądanie kierunek: NuGet -> Wtyczki
     * Żądanie będzie zawierać:
         * Domyślny poziom rejestrowania
     * Odpowiedź będzie zawierać:
         * Kod odpowiedzi, wskazując wynik operacji

Wersja protokołu *2.0.0* wiadomości

17. Rozpoczynanie operacji oświadczeń

* Żądanie kierunek: NuGet -> Wtyczki
    * Żądanie będzie zawierać:
        * index.json usługi dla źródła pakietów
        * repozytorium lokalizacji źródłowej pakietu
    * Odpowiedź będzie zawierać:
        * Kod odpowiedzi, wskazując wynik operacji
        * Element wyliczalny z obsługiwanych operacji, jeśli operacja zakończyła się pomyślnie.  Jeśli wtyczka nie obsługuje źródło pakietów, wtyczka musi zwracać pusty zestaw obsługiwanych operacji.

    Jeśli źródło indeks i pakiet usługi ma wartość null, wtyczka pozwala uzyskać odpowiedzi z uwierzytelnianiem.

18. Pobierz poświadczenia uwierzytelniania

* Żądanie kierunek: NuGet -> Wtyczki
* Żądanie będzie zawierać:
    * Identyfikator URI
    * isRetry
    * Nieinterakcyjnym
    * CanShowDialog
* Odpowiedź będzie zawierać
    * Nazwa użytkownika
    * Hasło
    * Komunikat
    * Lista typów uwierzytelniania
    * MessageResponseCode