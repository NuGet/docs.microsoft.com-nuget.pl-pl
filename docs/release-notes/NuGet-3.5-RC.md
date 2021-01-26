---
title: Informacje o wersji 3,5 RC
description: Informacje o wersji programu NuGet 3,5 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780198"
---
# <a name="nuget-35-rc-release-notes"></a>Informacje o wersji narzędzia NuGet 3,5 RC

[NuGet 3,5 — informacje](../release-notes/nuget-3.5-Beta2.md)  |  o wersji beta2 Pakiet [NuGet 3,5 — informacje o wersji RTM](../release-notes/nuget-3.5-RTM.md)

Wersja 3,5 jest ukierunkowana na poprawę jakości i wydajności klientów programu NuGet. Ponadto firma Microsoft dostarczyła kilka funkcji, takich jak obsługa [folderów rezerwowych](https://github.com/NuGet/Home/issues/2899), obsługa elementów [PackageType](https://github.com/NuGet/Home/issues/2476) w `.nuspec` i innych.

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Poprawki błędów

* Instalowanie/przywracanie pakietu kończy się niepowodzeniem z "pakiet zawiera wiele `.nuspec` plików". - [#3231](https://github.com/NuGet/Home/issues/3231)

* Pakiet NuGet wymusza dodanie `.tt` plików do folderu Content niezależnie od tego, co [#3203](https://github.com/NuGet/Home/issues/3203)

* Pakiet NuGet csproj (z `project.json` ) ulega awarii, jeśli nie ma packOptions i właściciela w pliku JSON — [#3180](https://github.com/NuGet/Home/issues/3180)

* Pakiet NuGet dla `project.json` ignorowania tagów packOptions, takich jak podsumowanie, autorzy, właściciele itp., [#3161](https://github.com/NuGet/Home/issues/3161)

* Pakiet NuGet ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizacja wielu pakietów z wycofywaniem pozostawia projekt w stanie przerwania — [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles w obszarze any nie są dodawane do projektów standardowych, [#3118](https://github.com/NuGet/Home/issues/3118)

* Nie można prawidłowo spakować biblioteki dla platformy .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)

* Plik > nowy projekt — > Biblioteka klas (przenośna) kończy się niepowodzeniem w programu VS2015 i Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Błąd NuGet-1.0.0-* nie jest prawidłowym ciągiem wersji- [#3070](https://github.com/NuGet/Home/issues/3070)

* Nie można wyświetlić Find-Package, ale Install-Package działa [#3068](https://github.com/NuGet/Home/issues/3068)

* Błąd podczas "Install-Package jQuery. Validation" w dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Po zainstalowaniu programu VS 2015 Update 3 w programie VS, który korzysta z 3.5.0 w wersji NuGet, występuje błąd- [#3053](https://github.com/NuGet/Home/issues/3053)

* Interfejs użytkownika Menedżera pakietów: nie wyświetla nowej wersji po zaktualizowaniu pakietu — [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey w wierszu polecenia usuwania nie jest odczytywany/wysyłany w 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć w zależności od wersji wstępnej. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Tworzenie wyjątku NullRef w projekcie PCL (net46 i Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizacja NuGet powinna podawać komunikat informacyjny, gdy wyższa wersja jest ograniczona przez ograniczenie allowedVersions — [#3013](https://github.com/NuGet/Home/issues/3013)

* Wtyczka poświadczeń została zakończona z błędem-1/Pobieranie pakietu podczas korzystania z dostawców poświadczeń z wieloma źródłami — [#2885](https://github.com/NuGet/Home/issues/2885)

* Pakiet NuGet — brak Newtonsoft.Jsw zależności od pakietu — [#2876](https://github.com/NuGet/Home/issues/2876)

* Usterka w ExecuteSynchronizedCore w systemie Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* Program VS nie obsługuje zmiennych środowiskowych w programie repositoryPath (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)

* Rozwiązywanie problemów z ułatwieniami dostępu — [#2745](https://github.com/NuGet/Home/issues/2745)

* Platformy przenośne z zadzielonymi profilami są odrzucane. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Menedżer pakietów NuGet powinien wyczyścić, że lista opcji w szczegółach pakietów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Aktualizacja NuGet 3.3.0 kończy się niepowodzeniem z "dodatkowym ograniczeniem... zdefiniowane w packages.config uniemożliwia wykonanie tej operacji ". - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalowanie pakietu z lokalnego źródła, które nie istnieje, zgłasza fałszywe wiadomości [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "dostępne uaktualnienie" zawiera uaktualnienia, które naruszają ograniczenie wersji — [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Usprawnienia wydajności

* Wydajność: ulepszanie analizy struktury docelowej ContentModel — [#3162](https://github.com/NuGet/Home/issues/3162)

* Wydajność: należy unikać odczytywania `runtime.json` plików do przywracania, które nie mają identyfikatorów rid [#3150](https://github.com/NuGet/Home/issues/3150). Na komputerach CI można przywrócić przykładową aplikację sieci Web ASP.NET ograniczoną od ponad 15 sekund do 3 s.

* Wydajność: Konsola Menedżera pakietów init.ps1 czas ładowania [#2956](https://github.com/NuGet/Home/issues/2956). Czas, aby otworzyć PackageManagerConsole udoskonalony w niektórych przypadkach z 132S na dziesiątkach.

* Rozwiązywanie problemów z wydajnością w pakiecie NuGet Update- [#3044](https://github.com/NuGet/Home/issues/3044): w przykładowym projekcie czas potrzebny na zainstalowanie pakietów zredukowanych z 140S do 68s.

## <a name="dcrs"></a>DCR

* Pakiet NuGet musi poinformować użytkowników, że uaktualnianie/Instalowanie w formacie PCL opartym na platformie dotnet TFM może powodować problemy — [#3138](https://github.com/NuGet/Home/issues/3138)

* Ostrzegaj o złej instalacji/uaktualnieniu dla projektu w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Dodawanie obsługi netcoreapp11 i netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)

* Drukuj zawartość nagłówka NuGet-Warning w konsoli programu nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)

* Wykorzystanie atrybutu AssemblyMetadata dla `.nuspec` zamiany tokenów — [#2851](https://github.com/NuGet/Home/issues/2851)

* Usuń zablokowaną właściwość z pliku blokady — [#2379](https://github.com/NuGet/Home/issues/2379)

* Pakiety symboli nie powinny być używane w instalacji ani aktualizacji #2807

## <a name="features"></a>Funkcje

* Obsługa folderów pakietów powrotu — [#2899](https://github.com/NuGet/Home/issues/2899)

* Projektuj i Implementuj pojęcie typu pakietu do obsługi pakietów narzędzi — [#2476](https://github.com/NuGet/Home/issues/2476)

* Interfejs API umożliwiający uzyskanie ścieżki do folderu pakietów globalnych — [#2403](https://github.com/NuGet/Home/issues/2403)

* Obsługa aktualizacji pakietów natywnych — [#1291](https://github.com/NuGet/Home/issues/1291)
