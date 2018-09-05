---
title: Informacje o wersji 3.2 NuGet
description: Informacje o wersji programu NuGet 3.2, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549525"
---
# <a name="nuget-32-release-notes"></a>Informacje o wersji 3.2 NuGet

[Informacje o wersji 3.2 RC NuGet](../release-notes/nuget-3.2-RC.md) | [informacjach o wersji NuGet 3.2.1](../release-notes/nuget-3.2.1.md)

NuGet 3.2 wydanej wersji 16 września 2015 roku jako kolekcja ulepszenia i poprawki dla 3.1.1 i jest dostępny z obu [dist.nuget.org](http://dist.nuget.org/index.html) i [galerii Visual Studio](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).

## <a name="new-features"></a>Nowe funkcje

* Projekty, które znajdują się w tym samym folderze mogą teraz zawierać różne `project.json` pliki w tym folderze, które są specyficzne dla każdego projektu.  Dla każdego projektu, nazwij `project.json` pliku `{ProjectName}.project.json` i NuGet odpowiednio zapewni preferencji w tej konfiguracji dla każdego projektu.  Jest to obsługiwane tylko za pomocą installed — narzędzia dla systemu Windows 10 w wersji 1.1 [1102](https://github.com/NuGet/Home/issues/1102)
* Klienci programu NuGet obsługuje określanie globalnych zmiennej środowiskowej NUGET_PACKAGES do określenia lokalizacji folderu udostępnionego globalnymi pakietami używane w `project.json` zarządzanych projektów za pomocą narzędzi systemu Windows 10 w wersji 1.1.

## <a name="command-line-updates"></a>Aktualizacje wiersza polecenia

Jest to pierwsza wersja klienta nuget.exe, który obsługuje serwery v3 NuGet i przywracanie pakietów dla projektów zarządzanych przy użyciu `project.json` pliku.

Wystąpiło wiele uwierzytelnionych kanału informacyjnego problemy, które zostały rozwiązane w tej wersji w celu interakcji z klientem.

* Instalowanie / przywracania interakcje przesłać tylko poświadczenia na potrzeby początkowego żądania do uwierzytelnionego kanał — [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Polecenie wypychania nie zostanie rozpoznana poświadczeń z konfiguracji — [1248](https://github.com/NuGet/Home/issues/1248)
* Agent użytkownika i nagłówki są teraz przesyłane do repozytoria NuGet ułatwiające wykonywanie śledzenia statystyki - [929](https://github.com/NuGet/Home/issues/929)

Wprowadziliśmy wiele ulepszeń efektywniej obsługiwać awarie sieci podczas próby wykonania do pracy ze zdalnym repozytorium NuGet:

* Ulepszone komunikaty o błędach, gdy nie można nawiązać zdalnego źródła danych — [1238](https://github.com/NuGet/Home/issues/1238)
* Poprawione polecenie przywracania NuGet, aby prawidłowo zwraca wartość 1, jeśli wystąpi błąd - [1186](https://github.com/NuGet/Home/issues/1186)
* Teraz ponawianie próby połączenia sieciowego każdego 200 ms dla maksymalnie 5 próbach w przypadku awarii 5xx protokołu HTTP - [1120](https://github.com/NuGet/Home/issues/1120)
* Ulepszona obsługa odpowiedzi przekierowania serwera podczas polecenia push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` obsługuje teraz nazwę adresu URL lub repozytorium z pliku Nuget.Config jako argument - [1046](https://github.com/NuGet/Home/issues/1046)
* Brakujące pakiety, które nie znajdowały się w repozytorium podczas przywracania teraz są zgłaszane jako błędy ostrzeżenia — zamiast [1038](https://github.com/NuGet/Home/issues/1038)
* Poprawiona obsługa multipartwebrequest \r\n scenariuszach systemu Unix/Linux — [776](https://github.com/NuGet/Home/issues/776)

Istnieje szereg poprawek na problemy z różnymi poleceniami:

* Polecenie wypychania już nie występuje GET przed PUT względem źródła pakietu - [1237](https://github.com/NuGet/Home/issues/1237)
* Lista, polecenie nie jest już powtarza numery wersji - [1185](https://github.com/NuGet/Home/issues/1185)
* Pakietu z argumentem - kompilacji teraz poprawnie obsługuje język C# 6.0 — [1107](https://github.com/NuGet/Home/issues/1107)
* Poprawiony problemów próby pakietu projektu języka F # utworzonych za pomocą programu Visual Studio 2015 — [1048](https://github.com/NuGet/Home/issues/1048)
* Przywrócenie żadnych operacji teraz, gdy pakiety już istnieje — [1040](https://github.com/NuGet/Home/issues/1040)
* Ulepszone komunikaty o błędach podczas `packages.config` plik jest źle sformułowany - [1034](https://github.com/NuGet/Home/issues/1034)
* Poprawione polecenia restore z przełącznikiem - SolutionDirectory do pracy z ścieżek względnych - [992](https://github.com/NuGet/Home/issues/992)
* Ulepszone polecenie zaktualizowany do obsługi całego rozwiązania update - [924](https://github.com/NuGet/Home/issues/924)

Pełną listę problemów rozwiązanych w tej wersji można znaleźć w witrynie NuGet GitHub [wiersza polecenia punkt kontrolny](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Aktualizacje rozszerzeń programu Visual Studio

### <a name="new-features-in-visual-studio"></a>Nowe funkcje w programie Visual Studio

* Nowy element menu kontekstowego został dodany do Eksploratora rozwiązań w węźle rozwiązania, który zezwala na pakiety do przywrócenia bez kompilowania rozwiązania ([1274](https://github.com/NuGet/Home/issues/1274)).

![Nowy element Menu kontekstowego "Przywracanie pakietów"](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Aktualizacje i poprawki w programie Visual Studio

Poprawki dla uwierzytelnione kanały informacyjne były rzutowane i które zostały rozwiązane w również rozszerzenie.  Następujące elementy uwierzytelniania również zostało zmodyfikowanych w rozszerzeniu:

* Teraz poprawnie traktowanie NuGet w wersji 3 uwierzytelnione kanały informacyjne prawidłowo, a nie jako v2 uwierzytelnione kanały informacyjne - [1216](https://github.com/NuGet/Home/issues/1216)
* Poprawiony żądanie dotyczące poświadczeń uwierzytelniania w projektach przy użyciu `project.json` i komunikacji z kanałów informacyjnych w wersji 2 - [1082](https://github.com/NuGet/Home/issues/1082)

Łączność sieciowa miała wpływ na interfejs użytkownika w programie Visual Studio, a następnie rozwiązaliśmy to następujące poprawki:

* Ulepszone konserwację w lokalnej pamięci podręcznej wersji pakietu - [1096](https://github.com/NuGet/Home/issues/1096)
* Zmienić zachowanie błąd podczas nawiązywania połączenia v3, kanał informacyjny do już próba jej traktowała jako źródło danych w wersji 2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Teraz uniemożliwić instalowanie błędy podczas instalowania pakietu z wieloma źródłami pakietów - [1183](https://github.com/NuGet/Home/issues/1183)

Wprowadziliśmy ulepszoną obsługę interakcji z operacji kompilacji:

* Teraz kompilowanie projektów, jeśli trwa przywracanie pakietów dla jednego projektu nie powiodło się — w dalszym ciągu [1169](https://github.com/NuGet/Home/issues/1169)
* Instalowanie pakietu do projektu, który jest zależna od innego projektu w rozwiązaniu wymusza ponownej kompilacji rozwiązań — [981](https://github.com/NuGet/Home/issues/981)
* Poprawione instaluje pakietu nie powiodło się, aby poprawnie wycofać zmian do projektu — [1265](https://github.com/NuGet/Home/issues/1265)
* Poprawione przypadkowego usunięcia `developmentDependency` atrybut pakiet w `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Wywołania `install.ps1` powstał odpowiedniego `$package.AssemblyReferences` obiekt przekazany - [1245](https://github.com/NuGet/Home/issues/1245)
* Zabrania już odinstalowuje pakietów w projektach platformy uniwersalnej systemu Windows, gdy projekt jest w nieprawidłowym stanie - [1128](https://github.com/NuGet/Home/issues/1128)
* Rozwiązania zawierającego kombinację `packages.config` i `project.json` są teraz prawidłowo skompilowane projekty bez konieczności sekundy kompilacji operacji - [1122](https://github.com/NuGet/Home/issues/1122)
* Lokalizowanie pliki app.config prawidłowo, jeśli są one połączone lub znajduje się w innym folderze — [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Projekty platformy uniwersalnej systemu Windows można teraz zainstalować nieznajdujące się na liście pakietów - [1109](https://github.com/NuGet/Home/issues/1109)
* Przywracanie pakietu teraz jest dozwolona, gdy to rozwiązanie nie jest w stanie zapisanym - [1081](https://github.com/NuGet/Home/issues/1081)

Obsługa aktualizacji konfiguracji, które pliki są usuwane:

* Nie jest już usuwania pliku obiektów docelowych dostarczanych z poziomu pakietu na kolejne kompilacje `project.json` zarządzanego projektu - [1288](https://github.com/NuGet/Home/issues/1288)
* Nie jest już modyfikacji plików Nuget.Config podczas kompilacji rozwiązania platformy ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Można już zmienić ograniczenia wersji podczas aktualizacji pakietu - [1130](https://github.com/NuGet/Home/issues/1130)
* Blokowanie plików teraz pozostać zablokowane podczas kompilacji - [1127](https://github.com/NuGet/Home/issues/1127)
* Obecnie modyfikuje `packages.config` i nie ponowne napisanie podczas aktualizacji - [585](https://github.com/NuGet/Home/issues/585)

Zwiększono interakcji z kontroli źródła w programie TFS:

* Nie jest już niepowodzenie instalacji pakietów, które są powiązane z TFS — [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Poprawiony interfejsu użytkownika NuGet umożliwia integrację z programem TFS 2013 — [1071](https://github.com/NuGet/Home/issues/1071)
* Poprawione odwołania do pakietów przywrócić prawidłowo pochodzą packages folder - [1004](https://github.com/NuGet/Home/issues/1004)

Na koniec poprawiono również następujące elementy:

* Poziom szczegółowości komunikaty w dzienniku zmniejszone dla `project.json` zarządzanych projektów — [1163](https://github.com/NuGet/Home/issues/1163)
* Teraz poprawnie wyświetlanie zainstalowanej wersji pakietu w interfejsie użytkownika - [1061](https://github.com/NuGet/Home/issues/1061)
* Pakiety z zakresami zależności określona w ich nuspec teraz mieć wersje wstępne tych zależności zainstalowana wersja stabilny pakiet - [1304](https://github.com/NuGet/Home/issues/1304)

Pełną listę problemów rozwiązanych dla rozszerzenia programu Visual Studio można znaleźć w witrynie NuGet GitHub [3,2 punkt kontrolny](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)