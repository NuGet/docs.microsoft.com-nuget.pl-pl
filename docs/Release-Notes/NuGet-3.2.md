---
title: Informacje o wersji NuGet 3.2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 3.2 NuGet."
keywords: NuGet 3.2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1728a5c0d83be84686e7ab1394cfc4f8f809987c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-32-release-notes"></a>Informacje o wersji 3.2 NuGet

[Informacje o wersji 3.2 RC NuGet](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 informacje o wersji](../release-notes/nuget-3.2.1.md)

NuGet 3.2 wydanej wersji 16 września 2015 roku jako kolekcja ulepszeń i poprawek dla 3.1.1 i jest dostępny z obu [dist.nuget.org](http://dist.nuget.org/index.html) i [galerii programu Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Nowe funkcje

* Teraz można mają inne projekty, które znajdują się w tym samym folderze `project.json` pliki w tym folderze, które są specyficzne dla każdego projektu.  Dla każdego projektu nazwa `project.json` pliku `{ProjectName}.project.json` i NuGet odpowiednio zapewni preferencji w tej konfiguracji dla każdego projektu.  Jest to możliwe tylko z zainstalowany - narzędzi systemu Windows 10 w wersji 1.1 [1102](https://github.com/NuGet/Home/issues/1102)
* Klienci NuGet obsługuje określanie globalnych zmiennej środowiskowej NUGET_PACKAGES do określenia lokalizacji folderu udostępnionego pakietów globalnego używane w `project.json` zarządzanych projektów z narzędzi systemu Windows 10 w wersji 1.1.

## <a name="command-line-updates"></a>Aktualizacje wiersza polecenia

Jest to pierwsza wersja klienta nuget.exe, który obsługuje serwery NuGet w wersji 3 i przywracanie pakietów dla projektów zarządzanych za pomocą `project.json` pliku.

Znaleziono wiele uwierzytelnionych źródła problemów, które zostały opisane w tej wersji w celu zwiększenia interakcji z klientem.

* Zainstaluj / przywracania interakcje kierować tylko poświadczenia początkowe żądanie uwierzytelniony podawanie - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Polecenie wypychania nie rozpoznaje poświadczeń z konfiguracji — [1248](https://github.com/NuGet/Home/issues/1248)
* Agent użytkownika i nagłówków, teraz są przesyłane do repozytoria NuGet, które ułatwiają monitorowanie statystyki — [929](https://github.com/NuGet/Home/issues/929)

Wprowadziliśmy wiele ulepszeń w celu ulepszenia obsługi awarie sieci podczas próby pracować ze zdalnego repozytorium NuGet:

* Ulepszone komunikaty o błędach, gdy nie można nawiązać zdalnego źródła danych - [1238](https://github.com/NuGet/Home/issues/1238)
* Skorygowane polecenia restore NuGet poprawnie zwracane 1 w przypadku wystąpienia błędu - [1186](https://github.com/NuGet/Home/issues/1186)
* Teraz ponawianie próby połączenia sieciowe co 200 MS maksymalnie 5 prób w przypadku HTTP 5xx błędy — [1120](https://github.com/NuGet/Home/issues/1120)
* Ulepszona obsługa odpowiedzi przekierowania serwera podczas polecenie wypychania - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`adres URL lub repozytorium nazwy z pliku Nuget.Config jako argument - obsługuje teraz [1046](https://github.com/NuGet/Home/issues/1046)
* Brakuje pakietów, które nie znajdowały się w repozytorium podczas przywracania są teraz raportowane klientowi jako błędy zamiast ostrzeżenia [1038](https://github.com/NuGet/Home/issues/1038)
* Poprawiona obsługa multipartwebrequest \r\n dla scenariuszy systemu Unix/Linux — [776](https://github.com/NuGet/Home/issues/776)

Istnieje wiele poprawek problemy z różnych poleceń:

* Polecenie wypychania już nie GET przed PUT względem źródła pakietu - [1237](https://github.com/NuGet/Home/issues/1237)
* Lista polecenie powtarza już numery wersji - [1185](https://github.com/NuGet/Home/issues/1185)
* Pakiet z argumentem - kompilacji teraz poprawnie obsługuje C# w wersji 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Poprawiony problemów podjęto próbę pakiecie projektów F # skompilowanej za pomocą programu Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Przywróć teraz nie-ops podczas pakietów już istnieje — [1040](https://github.com/NuGet/Home/issues/1040)
* Ulepszone komunikaty o błędach podczas `packages.config` pliku jest nieprawidłowo sformułowany - [1034](https://github.com/NuGet/Home/issues/1034)
* Skorygowane polecenia restore z przełącznikiem - SolutionDirectory do pracy z ścieżek względnych - [992](https://github.com/NuGet/Home/issues/992)
* Ulepszone polecenie zaktualizowane do obsługi aktualizacji całym rozwiązaniu — [924](https://github.com/NuGet/Home/issues/924)

Pełna lista problemów, które zostały omówione w tej wersji można znaleźć w witrynie NuGet GitHub [wiersza polecenia punkt kontrolny](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Aktualizacje rozszerzenia usługi Visual Studio

### <a name="new-features-in-visual-studio"></a>Nowe funkcje w programie Visual Studio

* Nowy element menu kontekstowe został dodany do Eksploratora rozwiązań w węźle rozwiązanie umożliwiający pakietów do przywrócenia bez tworzenia rozwiązania ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nowy "Przywracania pakietów" w Menu kontekstowym](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aktualizacje i poprawki programu Visual Studio

Poprawki dla źródeł uwierzytelnionych zostały rzutowane i rozwiązany również do rozszerzenia.  Następujące elementy uwierzytelniania również zostały uwzględnione w rozszerzeniu:

* Teraz prawidłowo traktowanie NuGet w wersji 3 uwierzytelniony źródła poprawnie, zamiast jako źródła danych - uwierzytelniona v2 [1216](https://github.com/NuGet/Home/issues/1216)
* Żądanie poprawiony poświadczeń uwierzytelniania w projektach przy użyciu `project.json` i komunikacji z źródeł danych w wersji 2 - [1082](https://github.com/NuGet/Home/issues/1082)

Połączenie sieciowe ma wpływ na interfejs użytkownika w programie Visual Studio, a rozwiązaliśmy to następujące poprawki:

* Ulepszone konserwacji w lokalnej pamięci podręcznej wersji pakietu - [1096](https://github.com/NuGet/Home/issues/1096)
* Zmienić zachowanie niepowodzenia podczas nawiązywania połączenia v3, źródła danych do już próba traktować go jako źródło danych w wersji 2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Zapobieganie teraz zainstalować błędy podczas instalowania pakietu z wieloma źródłami pakietu — [1183](https://github.com/NuGet/Home/issues/1183)

Firma Microsoft Ulepszona obsługa interakcji z operacji kompilacji:

* Teraz kontynuowanie w projektach kompilacji, jeśli trwa przywracanie pakietów dla jednego projektu nie powiodło się — [1169](https://github.com/NuGet/Home/issues/1169)
* Instalowanie pakietu do projektu, który jest zależny od innego projektu w rozwiązaniu wymusza kompilowania rozwiązania — [981](https://github.com/NuGet/Home/issues/981)
* Skorygowane instaluje pakietu nie powiodło się, aby poprawnie wycofać zmian na projekt — [1265](https://github.com/NuGet/Home/issues/1265)
* Skorygowane przypadkowego usunięcia `developmentDependency` atrybut pakietu w `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Wywołuje się `install.ps1` ma poprawne `$package.AssemblyReferences` obiekt przekazany - [1245](https://github.com/NuGet/Home/issues/1245)
* Nie uniemożliwia odinstalowuje pakietów w projektach platformy uniwersalnej systemu Windows, gdy projekt jest w złym stanie - [1128](https://github.com/NuGet/Home/issues/1128)
* Rozwiązania, zawierające kombinację `packages.config` i `project.json` są teraz prawidłowo skompilowane projekty bez konieczności drugiej kompilacji operacji - [1122](https://github.com/NuGet/Home/issues/1122)
* Poprawnie lokalizowanie plików app.config, jeśli są połączone lub znajduje się w innym folderze - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Projekty platformy UWP mogą teraz instalować pakiety nieznajdujące się na liście - [1109](https://github.com/NuGet/Home/issues/1109)
* Przywracanie pakietu teraz jest dozwolone, gdy rozwiązanie nie jest w stanie zapisanym - [1081](https://github.com/NuGet/Home/issues/1081)

Obsługa aktualizacji konfiguracji, które pliki są usuwane:

* Nie jest już usunięcie pliku elementy docelowe dostarczone z pakietu w kolejnych wersjach systemu `project.json` zarządzanego projektu - [1288](https://github.com/NuGet/Home/issues/1288)
* Nie jest już modyfikowania pliku Nuget.Config plików podczas kompilowania rozwiązania ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Można już zmienić ograniczenia wersji podczas aktualizacji pakietu - [1130](https://github.com/NuGet/Home/issues/1130)
* Pliki blokady teraz pozostać zablokowane podczas kompilacji - [1127](https://github.com/NuGet/Home/issues/1127)
* Obecnie modyfikuje `packages.config` i nie ponowne zapisywanie podczas aktualizacji - [585](https://github.com/NuGet/Home/issues/585)

Zwiększona interakcji z kontroli źródła TFS:

* Nie jest już niepowodzenie instalacji dla pakietów, które są powiązane z programem TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Poprawiony interfejs użytkownika NuGet, które umożliwiają integrację TFS 2013 — [1071](https://github.com/NuGet/Home/issues/1071)
* Usunąć odwołania do pakietów przywrócone prawidłowo pochodzą z folderu pakietów - [1004](https://github.com/NuGet/Home/issues/1004)

Na koniec mamy ulepszono również te elementy:

* Zmniejszona szczegółowości komunikaty dziennika `project.json` zarządzane projektów - [1163](https://github.com/NuGet/Home/issues/1163)
* Teraz prawidłowo wyświetlanie zainstalowanych wersji pakietu w interfejsie użytkownika - [1061](https://github.com/NuGet/Home/issues/1061)
* Pakiety z zakresu zależności określonego ich nuspec teraz zawierają wersje wstępne tych zależności zainstalowanych wersji pakietu stabilna - [1304](https://github.com/NuGet/Home/issues/1304)

Pełną listę problemów skierowana dla rozszerzenia Visual Studio można znaleźć w witrynie NuGet GitHub [3.2 punktu kontrolnego](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu do śledzenia problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)