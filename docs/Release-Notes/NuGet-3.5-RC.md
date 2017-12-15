---
title: 3.5 informacje o wersji RC | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 75a9b496-5762-48b6-922f-fdddf1369c45
description: "Informacje o wersji programu NuGet 3.5 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.5 informacje o wersji RC, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09d566de6f53bc0f0ddd8049143dc647f3075671
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
#<a name="35-rc-release-notes"></a>3.5 informacje o wersji RC

[Informacje o wersji 3.5 Beta2 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 — informacje o wersji RTM](../release-notes/nuget-3.5-RTM.md)

3.5 wydanie koncentruje się na poprawie jakości i wydajności klientów NuGet. Ponadto zostały dostarczone kilka funkcji, takich jak obsługa [rezerwowy folderów](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) obsługuje w `.nuspec` itd.

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a>Poprawki błędów

* Instalacja/przywracania pakietu nie powiodło się "pakiet zawiera wiele `.nuspec` pliki." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Pakiet nuget wymuszone dodaje `.tt` plików do folderu zawartości bez względu na okoliczności - [#3203](https://github.com/NuGet/Home/issues/3203)

* csproj pakiet nuget (z `project.json`) ulega awarii, jeśli istnieją nie packOptions i właściciel w pliku JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* Pakiet nuget `project.json` ignoruje tagi packOptions podsumowanie, autorzy, właściciele itp - [#3161](https://github.com/NuGet/Home/issues/3161)

* Pakiet nuget ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizowania wielu pakietów z wycofywania pozostawia projektu w stan przerwane — [#3139](https://github.com/NuGet/Home/issues/3139)

* Nie dodano pliki we wszystkich projektów krótkich nazw netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Nie można spakować biblioteki przeznaczonych dla platformy .net Standard poprawnie - [#3108](https://github.com/NuGet/Home/issues/3108)

* Plik -> Nowy Projekt -> projektu biblioteki klas (przenośna) kończy się niepowodzeniem w programie VS2015 i Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Błąd nuGet — 1.0.0-* nie jest prawidłowym ciągiem wersji - [#3070](https://github.com/NuGet/Home/issues/3070)

* Znajdź pakietu nie powiedzie się do wyświetlania, ale działa Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Błąd podczas "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Gdy zainstalowanej wersji programu VS 2015 Aktualizacja 3 w wersji programu VS używane NuGet występuje błąd wersji 3.5.0 — [#3053](https://github.com/NuGet/Home/issues/3053)

* Pakiet interfejsu użytkownika Menedżera: nie są wyświetlane po zaktualizowaniu pakietu nowej wersji — [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey w wierszu polecenia delete nie odczytu/wysyłane 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć na zależność wersji wstępnej. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Tworzenie PCL (net46 i windows 10) projektu get NullRef wyjątku. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizacja Nuget należy podać komunikat informacyjny w przypadku nowszej wersji jest ograniczony przez ograniczenie allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Dodatek poświadczeń został zakończony z powodu błędu -1 / błąd podczas pobierania pakietu podczas używania dostawcy poświadczeń z wielu źródeł - [#2885](https://github.com/NuGet/Home/issues/2885)

* Pakiet nuget - Brak Newtonsoft.Json zależność pakietu - [#2876](https://github.com/NuGet/Home/issues/2876)

* Błąd w ExecuteSynchronizedCore w systemie Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS nie obsługuje zmiennych środowiskowych w repositoryPath (nie nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Rozwiąż problemy dotyczące ułatwień dostępu — [#2745](https://github.com/NuGet/Home/issues/2745)

* Przenośne platformy przy użyciu profilów podzielonym są odrzucane. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Menedżer pakietów NuGet powinien stał się wyczyścić tej listy opcji w pakietach szczegółów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Aktualizacja NuGet 3.3.0 "... dodatkowe ograniczenie zdefiniowane w pliku packages.config uniemożliwia wykonanie tej operacji." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalowanie pakietu z lokalnego źródła, które nie istnieje zgłasza sfałszowany komunikat - [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "Dostępne uaktualnienia" pokazuje uaktualnień, które narusza ograniczenie wersji - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Usprawnienia wydajności

* Wydajność: Zwiększyć ContentModel docelowej framework analizowania - [#3162](https://github.com/NuGet/Home/issues/3162)

* Wydajność: Unikaj odczytu `runtime.json` plików dla operacji przywracania, które nie mają identyfikatorów RID [#3150](https://github.com/NuGet/Home/issues/3150). Na maszynach CI przywrócić przykładowej aplikacji sieci Web ASP.NET zmniejszone ponad 15 sekund do 3 w sekundach.

* Wydajność: Czas ładowania init.ps1 w konsoli Menedżera pakietów [#2956](https://github.com/NuGet/Home/issues/2956). Czas, aby otworzyć PackageManagerConsole zwiększona w niektórych przypadkach z 132s 10s.

* Rozwiązać problemy z wydajnością ReSharper w aktualizacji NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): na przykładowy projekt, czas trwania, aby zainstalować pakiety zredukować z 140s 68s.

## <a name="dcrs"></a>Dcr

* Należy powiadomić użytkowników, że uaktualnienie/instalowanie tfm dotnet, na podstawie PCL może to spowodować problemy — NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* Ostrzegaj zły instalacja/aktualizacja dla projektu z tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Dodawanie obsługi netcoreapp11 i netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Drukuj zawartość nagłówka ostrzeżenie NuGet do konsoli w nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Wykorzystywanie assemblymetadata — atrybut `.nuspec` token zamiany - [#2851](https://github.com/NuGet/Home/issues/2851)

* Usuń właściwość locked z pliku blokady - [#2379](https://github.com/NuGet/Home/issues/2379)

* Pakiety symboli nigdy nie należy używać w instalacji lub aktualizacji #2807

## <a name="features"></a>Funkcje

* Obsługi rezerwowego pakietu folderów - [#2899](https://github.com/NuGet/Home/issues/2899)

* Projektowania i implementacji pojęcie typu pakietu do obsługi pakietów narzędzie - [#2476](https://github.com/NuGet/Home/issues/2476)

* Interfejsu API można pobrać ścieżki do folderu pakietów globalne - [#2403](https://github.com/NuGet/Home/issues/2403)

* Oryginalne pakiety aktualizacji support — [#1291](https://github.com/NuGet/Home/issues/1291)
