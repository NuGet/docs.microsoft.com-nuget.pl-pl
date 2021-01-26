---
title: Informacje o wersji narzędzia NuGet 3,2 RC
description: Informacje o wersji programu NuGet 3,2 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8132affb8273604ae79d4e1f85e6072d8eaf5ad6
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780287"
---
# <a name="nuget-32-rc-release-notes"></a>Informacje o wersji narzędzia NuGet 3,2 RC

Informacje o wersji [NuGet 3.1.1](../release-notes/nuget-3.1.1.md)  |  [Informacje o wersji narzędzia NuGet 3,2](../release-notes/nuget-3.2.md)

Pakiet NuGet 3,2 Release Candidate został zwolniony 2 września 2015 jako zbiór ulepszeń i poprawek w wersji 3.1.1.  Ponadto są to pierwsze wersje, które są publikowane w pierwszej kolejności w nowym repozytorium dist.nuget.org.

## <a name="new-features"></a>Nowe funkcje

* Projekty znajdujące się w tym samym folderze mogą teraz mieć różne `project.json` pliki w tym folderze, które są specyficzne dla każdego projektu.  Dla każdego projektu Nadaj nazwę `project.json` plikowi, `{ProjectName}.project.json` a pakiet NuGet prawidłowo odwołuje się do tej zawartości i będzie używać jej odpowiednio dla każdego projektu.  Obsługuje to nową funkcję  [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` obsługuje teraz globalPackagesFolder jako ścieżkę względną — [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Aktualizacje wiersza polecenia

Jest to pierwsza wersja klienta nuget.exe, która obsługuje serwery NuGet v3 i przywraca pakiety dla projektów zarządzanych przy użyciu `project.json` pliku.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Istniało wiele problemów z uwierzytelnionym źródłem danych, które zostały rozwiązane w tej wersji, aby zwiększyć interakcje z klientem.

* W przypadku interakcji z uwierzytelnianiem/przywróceniem tylko poświadczenia dla początkowego żądania wysłanego kanału informacyjnego — [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Polecenie push nie rozpoznaje poświadczeń z konfiguracji — [1248](https://github.com/NuGet/Home/issues/1248)
* Agent użytkownika i nagłówki są teraz przesyłane do repozytoriów NuGet w celu ułatwienia śledzenia statystyk — [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Wprowadziliśmy szereg ulepszeń w celu lepszego obsłużenia awarii sieci podczas próby pracy ze zdalnym repozytorium NuGet:

* Ulepszone komunikaty o błędach, gdy nie można nawiązać połączenia ze zdalnymi źródłami — [1238](https://github.com/NuGet/Home/issues/1238)
* Poprawiono polecenie przywracania NuGet w celu poprawnego zwrócenia 1 w przypadku wystąpienia błędu — [1186](https://github.com/NuGet/Home/issues/1186)
* Teraz ponawianie próby połączeń sieciowych co 200ms przez maksymalnie 5 prób w przypadku błędów 5xx HTTP — [1120](https://github.com/NuGet/Home/issues/1120)
* Ulepszona obsługa odpowiedzi przekierowania serwera podczas polecenia push- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` obsługuje teraz adres URL lub nazwę repozytorium z Nuget.Config jako argument- [1046](https://github.com/NuGet/Home/issues/1046)
* Brakujące pakiety, które nie znajdują się w repozytorium podczas przywracania, są teraz raportowane jako błędy zamiast ostrzeżeń [1038](https://github.com/NuGet/Home/issues/1038)
* Poprawiono obsługę multipartwebrequest z \r\n dla scenariuszy z systemami UNIX/Linux — [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Istnieje wiele poprawek dotyczących problemów z różnymi poleceniami:

* Polecenie push nie wykonuje już instrukcji GET przed PUT względem źródła pakietu — [1237](https://github.com/NuGet/Home/issues/1237)
* Polecenie listy nie powtarza już numerów wersji- [1185](https://github.com/NuGet/Home/issues/1185)
* Pakiet z argumentem-Build jest teraz prawidłowo obsługiwany w języku C# 6,0- [1107](https://github.com/NuGet/Home/issues/1107)
* Poprawione problemy podczas próby spakowania projektu języka F # skompilowanego z programem Visual Studio 2015 — [1048](https://github.com/NuGet/Home/issues/1048)
* Przywróć teraz nie — Ops, gdy pakiety już istnieją — [1040](https://github.com/NuGet/Home/issues/1040)
* Ulepszone komunikaty o błędach, gdy `packages.config` plik jest źle sformułowany — [1034](https://github.com/NuGet/Home/issues/1034)
* Poprawiono polecenie Restore z `-SolutionDirectory` przełącznikiem do pracy ze ścieżkami względnymi- [992](https://github.com/NuGet/Home/issues/992)
* Udoskonalono zaktualizowane polecenie do obsługi aktualizacji dla całego rozwiązania — [924](https://github.com/NuGet/Home/issues/924)

Pełną listę problemów rozwiązanych w tej wersji można znaleźć w obszarze [kontrolnym wiersza polecenia](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)narzędzia NuGet GitHub.

## <a name="visual-studio-extension-updates"></a>Aktualizacje rozszerzeń programu Visual Studio

### <a name="new-features-in-visual-studio"></a>Nowe funkcje w programie Visual Studio

* Nowy element menu kontekstowego został dodany do Eksplorator rozwiązań w węźle rozwiązania, który umożliwia przywrócenie pakietów bez kompilowania rozwiązania ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nowy element menu kontekstowego "Przywróć pakiety"](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aktualizacje i poprawki w programie Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Poprawki dla uwierzytelnionych kanałów informacyjnych zostały również zestawione i rozwiązany w rozszerzeniu.  Następujące elementy uwierzytelniania zostały również uwzględnione w rozszerzeniu:

* Teraz poprawnie Przetwarzaj uwierzytelnione źródła NuGet v3, a nie jako uwierzytelnione źródła w wersji 2 — [1216](https://github.com/NuGet/Home/issues/1216)
* Poprawiono żądanie poświadczeń uwierzytelniania w projektach używających `project.json` i komunikujących się ze źródłami w wersji 2 — [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Interfejs użytkownika w programie Visual Studio miał problemy z łącznością sieciową i zawiera następujące poprawki:

* Ulepszona obsługa lokalnej pamięci podręcznej wersji pakietu — [1096](https://github.com/NuGet/Home/issues/1096)
* Zmieniono zachowanie niepowodzenia podczas nawiązywania połączenia ze źródłem v3, aby nie podejmować prób traktowania go jako źródła danych 2 – [1253](https://github.com/NuGet/Home/issues/1253)
* Teraz zapobieganie błędom instalacji podczas instalacji pakietu z wieloma źródłami pakietów — [1183](https://github.com/NuGet/Home/issues/1183)

Ulepszono obsługę interakcji z operacjami kompilacji:

* Teraz kontynuowanie kompilowania projektów w przypadku niepowodzenia przywracania pakietów dla pojedynczego projektu — [1169](https://github.com/NuGet/Home/issues/1169)
* Zainstalowanie pakietu w projekcie, który jest zależny od innego projektu w rozwiązaniu, Wymusza ponowne skompilowanie rozwiązania- [981](https://github.com/NuGet/Home/issues/981)
* Poprawiono nieudane instalacje pakietów w celu poprawnego wycofania zmian w projekcie — [1265](https://github.com/NuGet/Home/issues/1265)
* Poprawiono Przypadkowe usunięcie `developmentDependency` atrybutu w pakiecie w `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Wywołania mają `install.ps1` teraz prawidłowy `$package.AssemblyReferences` obiekt przeszedł do- [1245](https://github.com/NuGet/Home/issues/1245)
* Nie uniemożliwia już odinstalowywania pakietów w projektach platformy UWP, gdy projekt jest w nieprawidłowym stanie — [1128](https://github.com/NuGet/Home/issues/1128)
* Rozwiązania zawierające mieszankę `packages.config` i `project.json` projekty są teraz prawidłowo zbudowane bez konieczności wykonywania drugiej operacji kompilacji — [1122](https://github.com/NuGet/Home/issues/1122)
* Poprawne Lokalizowanie plików app.config, jeśli są one połączone lub znajdują się w innym folderze- [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Projekty platformy UWP mogą teraz instalować nieznajdujące się na liście pakiety — [1109](https://github.com/NuGet/Home/issues/1109)
* Przywracanie pakietu jest teraz dozwolone, gdy rozwiązanie nie jest w stanie zapisanym — [1081](https://github.com/NuGet/Home/issues/1081)


Poprawiono obsługę aktualizacji plików konfiguracji:

* Nie usuwasz już pliku Target dostarczonego z pakietu w kolejnych kompilacjach `project.json` zarządzanego projektu — [1288](https://github.com/NuGet/Home/issues/1288)
* Nie jest już modyfikowany Nuget.Config plików podczas kompilacji rozwiązania ASP.NET 5 — [1201](https://github.com/NuGet/Home/issues/1201)
* Nie można już zmieniać ograniczeń wersji podczas aktualizacji pakietu — [1130](https://github.com/NuGet/Home/issues/1130)
* Pliki blokad są teraz zablokowane podczas kompilacji — [1127](https://github.com/NuGet/Home/issues/1127)
* Teraz modyfikowanie `packages.config` i niezapisywanie w trakcie aktualizacji — [585](https://github.com/NuGet/Home/issues/585)


Ulepszono interakcje z kontrolą źródła TFS:

* Nie można już instalować pakietów, które są powiązane z TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Poprawiono interfejs użytkownika NuGet umożliwiający integrację TFS 2013 — [1071](https://github.com/NuGet/Home/issues/1071)
* Poprawione odwołania do pakietów, które zostały przywrócone prawidłowo, pochodzą z folderu pakietów — [1004](https://github.com/NuGet/Home/issues/1004)

Na koniec Ulepszono również następujące elementy:

* Poziom szczegółowości komunikatów dziennika zredukowany dla `project.json` projektów zarządzanych — [1163](https://github.com/NuGet/Home/issues/1163)
* Teraz poprawnie wyświetlasz zainstalowaną wersję pakietu w interfejsie użytkownika — [1061](https://github.com/NuGet/Home/issues/1061)


Pełną listę problemów rozwiązanych z rozszerzeniem programu Visual Studio można znaleźć w obszarze [kontrolnym](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) usługi NuGet GitHub 3,2

## <a name="known-issues"></a>Znane problemy

Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)