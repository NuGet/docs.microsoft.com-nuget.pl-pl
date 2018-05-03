---
title: Informacje o wersji RC NuGet 4.0
description: Informacje o wersji programu NuGet 4.0 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-40-rc-release-notes"></a>Informacje o wersji RC NuGet 4.0

[Informacje o wersji 3.5 RTM NuGet](../release-notes/nuget-3.5-RTM.md)

[RC 4.0 NuGet dla programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na obsługę scenariuszy .NET Core, odpowiedzi na opinie klientów klucza i poprawia wydajność w wielu scenariuszach. Tej wersji wprowadzono kilka ulepszeń, takich jak obsługa PackageReference, polecenia, jako docelowych elementów MSBuild i tła przywracania pakietów NuGet.

## <a name="bug-fixes"></a>Poprawki błędów

- Zmiany zachowania `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- Przywracanie nuget.exe dla vs "15" tylko komputera nie powiodło się — [#3834](https://github.com/NuGet/Home/issues/3834)

- . NETCore pliku nowego projektu należy zablokować kompilacji podczas przywracania - [#3780](https://github.com/NuGet/Home/issues/3780)

- Aplikacja sieci web platformy ASP.NET Core, migracja z programu VS2015 do wersji programu VS "15", nie można przywrócić. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Błąd podczas badania] Nie można odinstalować pakietu "jQuery weryfikacji" przez interfejs użytkownika PM - [#3755](https://github.com/NuGet/Home/issues/3755)

- Po zainstalowaniu pakietu do platformy uniwersalnej systemu Windows `project.json`, również powinny zostać przywrócone projektów nadrzędny - [#3731](https://github.com/NuGet/Home/issues/3731)

- Zmodyfikuj elementy docelowe NuGet do rejestrowania źródeł pakietów jako wysoki poziom szczegółowości zamiast normalny - [#3719](https://github.com/NuGet/Home/issues/3719)

- DotNet
  - dotnetcore dodatkiem Service Pack 3 powinna zawierać dokumentację XML domyślnie - [#3698](https://github.com/NuGet/Home/issues/3698)

- Wsadowe aktualizacji nie powiedzie się z poziomu interfejsu użytkownika po wybraniu wszystkich źródła - i źródła bez pakietu zostanie najpierw [#3696](https://github.com/NuGet/Home/issues/3696)

- Polecenie pakietu Nuget nie zawiera wszystkie pliki - [#3678](https://github.com/NuGet/Home/issues/3678)

- Za mało pamięci problem - [#3661](https://github.com/NuGet/Home/issues/3661)

- ProjectFileDependencyGroups sekcji pliku zasobów należy używać nazwy biblioteki dla projektów - [#3611](https://github.com/NuGet/Home/issues/3611)

- "Przywracanie dotnet" i recursing katalogów - [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 błędy są rejestrowane jako ostrzeżenia zamiast błędy - [#3503](https://github.com/NuGet/Home/issues/3503)

- Problem TFS: "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Wpisz "nuget <packagename>" w programie vs pole wyszukiwania szybkiego uruchamiania śledzi prefiksu "nuget" - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Nierozpoznany element główny w części Core Properties. Wiersz 2, pozycji 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` o znaczeniu zmienionym &lt; lub &gt; pól w tekście już kompilacje - [#2651](https://github.com/NuGet/Home/issues/2651)

- Usuń nuget.exe nie monit o podanie poświadczeń (jest w trybie nieinterakcyjnym) - [#2626](https://github.com/NuGet/Home/issues/2626)

- Usuń nuget.exe ostrzeganie o klucz interfejsu API dla lokalnych źródeł, nawet jeśli nie ma sensu - [#2625](https://github.com/NuGet/Home/issues/2625)

- Słaby środowisko błąd podczas instalowania pakietu wersji pre - EF - [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio awarii próby po zmianie zaznaczenia w Menedżerze pakietów - [#2551](https://github.com/NuGet/Home/issues/2551)

- DotNet
  - Przywracanie dotnetcore wykonuje wyszukiwań identyfikator z uwzględnieniem wielkości liter na płaski listy repozytoriów lokalnych stosowania przestawne wersji — [#2516](https://github.com/NuGet/Home/issues/2516)

- Usuń nuget.exe został przerwany dla źródła danych w wersji 2 - [#2509](https://github.com/NuGet/Home/issues/2509)

- limit wypychania nuget.exe musi komunikat o błędzie lepsze - [#2503](https://github.com/NuGet/Home/issues/2503)

- Narzędzie przywracania bez odpowiedniego dyskretnie importuje kończy się niepowodzeniem. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet wyświetla monit o podanie poświadczeń, gdy jest prywatny źródła strumieniowego nawet w przypadku instalowania z nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)

- Pakiet ApplicationInsights 2.0 jest wyświetlane, ale nie istnieje jeszcze — [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay w programie VS "15" preview gałęzi 5 - [#3500](https://github.com/NuGet/Home/issues/3500)

- Pierwsze zdarzenie OnBuild zostało pominięte przywracane podczas kompilacji dla platformy uniwersalnej systemu Windows - [#3489](https://github.com/NuGet/Home/issues/3489)

- Podziały PowerShell5 EntityFramework zainstalować? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Dodawanie źródła danych do szczegółowe rejestrowanie (należy wziąć pod uwagę 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr NoCache nie honorowane w wersji klienta nuget 3.4 + - [#3074](https://github.com/NuGet/Home/issues/3074)

- W przypadku awarii Dostawca poświadczeń do załadowania w programie VS Nie dziel NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkcje

- Konfigurowanie elementu konfiguracji do uruchamiania x86- [#3868](https://github.com/NuGet/Home/issues/3868)

- Automatyczne przywracanie 3/3: z systemem innym niż blokujące elementy interfejsu użytkownika — [#3658](https://github.com/NuGet/Home/issues/3658)

- Automatyczne przywracanie 2/3: w tle przywracania na wyznaczenie - [#3657](https://github.com/NuGet/Home/issues/3657)

- Przywróć system plików refs projektu do dopasowania zachowanie kompilacji (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)

- DPL obsługi w programie VS "15" — minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Przenieś plik ustawień do plików programu - [#3613](https://github.com/NuGet/Home/issues/3613)

- Właściwości wygenerowanego przywracania i obiektów docelowych niezbędna jest obsługa udział przeznaczonych dla różnych - [#3496](https://github.com/NuGet/Home/issues/3496)

- Przywracanie NuGet obsługę PackageTargetFallback (f.k.a importów) - [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementacja ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 dla identyfikatora RID - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet interfejsu użytkownika Służącego do obsługi Dodaj/Usuń/aktualizacja PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)

- Automatyczne przywracanie 1/3: Implementacji wyznaczenie interfejsu API za pomocą buforowanie projektu przywrócić informacje - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet przywracanie zadań & cele — [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Włącz rozwiązania poziomu przywracania w programie MSBuild — [#2993](https://github.com/NuGet/Home/issues/2993)

- Obsługuje rozszerzalności publicznego dostawcy poświadczeń w programie Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)

- Przywracanie nuget cykliczne - [#2533](https://github.com/NuGet/Home/issues/2533)

- Nie można załadować Microsoft.TeamFoundation.Client na dev15, należy zaktualizować wersję Microsoft.TeamFoundation.Client do 15.0 dla wersji programu VS "15" wersja zapoznawcza — [#2392](https://github.com/NuGet/Home/issues/2392)

- Nie można zainstalować pakietu C++ do platformy uniwersalnej systemu Windows w języku C++ projektu w programie VS "15" wersja zapoznawcza — [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg musi obsługiwać folderu \buildCrossTargeting\ - i zaimportować `.targets`  /  `.props` dla "crosstargeting" MSBuild zakresu. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Projekt ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)

- Usuń NuGet interfejsu użytkownika Służącego do obsługi przywracania z PackageReferences w `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- Dodawanie przycisk Wyczyść pamięć podręczną, aby ustawienia Menedżera pakietów programu VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>Dcr

- Przywracanie rozwiązanie powinno zostać zablokowane podczas przywracania automatycznie wykonywane. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NetCore instalacji z interfejsu użytkownika Menedżera pakietów NuGet instaluje co TFM, zamiast tych, które obsługuje pakiet - [#3721](https://github.com/NuGet/Home/issues/3721)

- Przywróć nominator interfejsu API musi obsługiwać DotNetCliToolsReferences zbyt. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Oznacz naszych VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- Migracja z odwołujące się do MS. VS. Services.Client MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) powinny być przestrzegane na poziomie projektu przez przywrócenie - [#3618](https://github.com/NuGet/Home/issues/3618)

- Przywracanie do projektu z jednym TargetFramework musi nie warunku właściwości — [#3588](https://github.com/NuGet/Home/issues/3588)

- DotNet
  - dotnetcore restore3 foo.csproj należy wykonaj projectref zależności i przywrócić te zbyt. Podobnie jak kompilacji. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platformy" zależności reprezentowane jako "type": "pakietu" w pliku blokady - [#2695](https://github.com/NuGet/Home/issues/2695)

- Tryb informacji pełnej nuget.exe powinny być widoczne pobierania adresu url - [#2629](https://github.com/NuGet/Home/issues/2629)

- Przenieś NuGet xplat Microsoft.NetCore.App i netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push - powinno być możliwe do przesłonięcia serwera symboli w przypadku wypychania w wierszu polecenia - [#2348](https://github.com/NuGet/Home/issues/2348)

- Konsolidacja kodu do znajdowania globalnej pakietów ścieżka - [#2296](https://github.com/NuGet/Home/issues/2296)

- Należy nazwę lepszą niż suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Określić `project.json` Nazwa zależności dla projektów MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)

- Dodaj obsługę programu SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Zezwalaj na przechodnie zależności NuPkgs z `.targets` mają być dostępne w programie MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- Przywracanie NuGet w wierszu polecenia jest znacznie mniejsza niż VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- Wprowadź bez uwzględniania wielkości liter - porównania identyfikator i wersję pakietu [#2522](https://github.com/NuGet/Home/issues/2522)

- Opcja NoCache nie działa w przypadku `packages.config` (wartość GlobalPackagesFolder) - restore/Instalacja oparta na [#1406](https://github.com/NuGet/Home/issues/1406)

- Zasoby FindPackageByIdResource wymaga domyślny kontekst pamięci podręcznej i rejestratora — [#1357](https://github.com/NuGet/Home/issues/1357)
