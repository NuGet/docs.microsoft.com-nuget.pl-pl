---
title: 3.5 informacje o wersji RC
description: Informacje o wersji programu NuGet 3.5 RC obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548541"
---
# <a name="nuget-35-rc-release-notes"></a>Informacje o wersji programu NuGet 3.5 RC

[Informacje o wersji programu NuGet 3.5 Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 — informacje o wersji RTM](../release-notes/nuget-3.5-RTM.md)

3,5 wydanie koncentruje się na poprawie jakości i wydajności klientom programu NuGet. Ponadto zostały wydane dla kilku funkcji, takich jak obsługa [rezerwowego folderów](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) obsługi w `.nuspec` itd.

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Poprawki błędów

* Kończy się niepowodzeniem instalacji/Przywracanie pakietu "pakiet zawiera wiele `.nuspec` plików." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Pakiet nuget wymuszone dodaje `.tt` pliki do folderu zawartości, niezależnie od tego, co - [#3203](https://github.com/NuGet/Home/issues/3203)

* Pakiet nuget w pliku csproj (przy użyciu `project.json`) ulega awarii, jeśli istnieją nie packOptions i właściciela w pliku JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* Pakiet nuget dla `project.json` ignoruje packOptions tagów, takich jak podsumowanie, autorów, właściciele itd - [#3161](https://github.com/NuGet/Home/issues/3161)

* Pakiet nuget ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Trwa aktualizowanie wielu pakietów przy użyciu wycofywania pozostawia projektu w stanie uszkodzenia - [#3139](https://github.com/NuGet/Home/issues/3139)

* Pliki w żadnej nie są dodawane dla projektów netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Nie można utworzyć pakietu biblioteki przeznaczonych dla platformy .net Standard nieprawidłowo — [#3108](https://github.com/NuGet/Home/issues/3108)

* Plik -> Nowy Projekt -> Projekt Biblioteka klas (przenośna) kończy się niepowodzeniem w programie VS2015 i Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Błąd nuGet — 1.0.0-* nie jest prawidłowym ciągiem wersji - [#3070](https://github.com/NuGet/Home/issues/3070)

* Znajdź pakietu nie powiedzie się do wyświetlania, ale działa Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Błąd podczas "Jquery.validation Install-Package" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Gdy zainstalowanego programu VS 2015 z aktualizacją 3 przy użyciu, których używa NuGet, występuje błąd wersji 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Interfejs użytkownika Menedżera pakietów: nie jest wyświetlany po zaktualizowaniu pakietu nowej wersji — [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey w wierszu polecenia delete nie odczytu/wysyłane 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Niepoprawny ciąg: stabilną wersję pakietu nie powinien mieć na zależność wersji wstępnej. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Tworzenie projektu PCL (net46 i systemu windows 10) — get NullRef wyjątku. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizacja Nuget należy podać komunikat informacyjny w przypadku nowsza wersja jest ograniczony przez ograniczenie allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Wtyczka poświadczeń został zakończony z powodu błędu -1 / wystąpił błąd podczas pobierania pakietu podczas używania dostawcy poświadczeń z wielu źródeł - [#2885](https://github.com/NuGet/Home/issues/2885)

* Pakiet nuget — zależność pakietu Newtonsoft.Json Brak — [#2876](https://github.com/NuGet/Home/issues/2876)

* Błąd w ExecuteSynchronizedCore na systemie Linux/MacOS i platformy Mono — [#2860](https://github.com/NuGet/Home/issues/2860)

* Program VS nie obsługuje zmiennych środowiskowych w repositoryPath (nie nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Rozwiązywanie problemów dotyczących dostępności - [#2745](https://github.com/NuGet/Home/issues/2745)

* Przenośne platformy przy użyciu profilów podzielonym są odrzucane. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Menedżer pakietów NuGet powinny było jasne, że listy opcji w pakietach szczegółów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Aktualizacji NuGet 3.3.0 kończy się niepowodzeniem z "… dodatkowe ograniczenia zdefiniowane w pliku packages.config zapobiega tej operacji." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalowanie pakietu ze źródła lokalnego, która nie istnieje zgłasza sfałszowany komunikat o — [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "Dostępne dla uaktualnienie" przedstawia uaktualnień, które narusza ograniczenie wersji - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Usprawnienia wydajności

* Wydajność: Zwiększyć, element ContentModel target framework podczas analizowania - [#3162](https://github.com/NuGet/Home/issues/3162)

* Wydajność: Unikaj odczytu `runtime.json` plików, aby przeprowadzać operacje przywracania, które nie mają RID [#3150](https://github.com/NuGet/Home/issues/3150). Na maszynach CI przywrócenie przykładowej aplikacji sieci Web ASP.NET zmniejszone ponad 15 sekund do 3 sekund.

* Wydajność: Czas ładowania init.ps1 Konsola Menedżera pakietów [#2956](https://github.com/NuGet/Home/issues/2956). Czas otwierania PackageManagerConsole lepsza w niektórych przypadkach zapewniając z 132s 10s.

* Rozwiązywanie problemów z wydajnością ReSharper w aktualizacji programu NuGet — [#3044](https://github.com/NuGet/Home/issues/3044): nad projektem przykładowy czas potrzebny na instalowanie pakietów zmniejszonej z 140s do 68s.

## <a name="dcrs"></a>DCRs

* NuGet musi powiadomić użytkowników, że uaktualnienie/instalowanie tfm dotnet, na podstawie PCL może to spowodować problemy — [#3138](https://github.com/NuGet/Home/issues/3138)

* Ostrzegaj zły instalacja/Aktualizacja projektu z elementu tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Dodanie obsługi netcoreapp11 i netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Drukuj zawartość nagłówka ostrzeżenie NuGet do konsoli w nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Assemblymetadata — Wykorzystaj atrybut `.nuspec` token zamiany - [#2851](https://github.com/NuGet/Home/issues/2851)

* Usunąć zablokowanej właściwości z pliku blokady - [#2379](https://github.com/NuGet/Home/issues/2379)

* Pakiety symboli nie należy nigdy nie należy używać w Zainstaluj lub zaktualizuj #2807

## <a name="features"></a>Funkcje

* Obsługa folderów rezerwowego pakietu — [#2899](https://github.com/NuGet/Home/issues/2899)

* Projektowanie i implementowanie pojęcie typ pakietu do obsługi pakiety narzędzia - [#2476](https://github.com/NuGet/Home/issues/2476)

* Interfejs API, aby pobrać ścieżkę do folderu globalnymi pakietami - [#2403](https://github.com/NuGet/Home/issues/2403)

* Pakiety natywne zaktualizować pomoc techniczna — [#1291](https://github.com/NuGet/Home/issues/1291)
