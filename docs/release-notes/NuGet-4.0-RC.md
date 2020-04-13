---
title: Informacje o wersji nuGet 4.0 RC
description: Informacje o wersji dla NuGet 4.0 RC, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496646"
---
# <a name="nuget-40-rc-release-notes"></a>Informacje o wersji nuGet 4.0 RC

[Informacje o wydaniu programu NuGet 3.5 RTM](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC dla programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na dodawaniu obsługi scenariuszy .NET Core, adresowaniu kluczowych opinii klientów i zwiększaniu wydajności w różnych scenariuszach. Ta wersja zawiera kilka ulepszeń, takich jak obsługa PackageReference, Polecenia NuGet jako obiekty docelowe MSBuild, przywracanie pakietu w tle i inne.

## <a name="bug-fixes"></a>Poprawki błędów

- Zmiany zachowań `dotnet pack --version-suffix foo`  - w [#3838](https://github.com/NuGet/Home/issues/3838)

- nuget.exe przywracanie na vs "15" komputer tylko nie powiedzie się - [#3834](https://github.com/NuGet/Home/issues/3834)

- . NetCore plik nowy projekt powinien blokować kompilacji podczas przywracania - [#3780](https://github.com/NuGet/Home/issues/3780)

- ASP.NET podstawowej aplikacji sieci web, migracji z VS2015 do VS "15", nie można przywrócić. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Błąd testu] Pakietu "jQuery Validation" nie można odinstalować przez interfejs użytkownika PM - [#3755](https://github.com/NuGet/Home/issues/3755)

- Gdy pakiet jest zainstalowany `project.json`na platformie UNIWERSALNEJ systemu Windows, projekty nadrzędne powinny również zostać przywrócone - [#3731](https://github.com/NuGet/Home/issues/3731)

- Zmodyfikuj obiekty docelowe NuGet, aby rejestrować źródła pakietu jako wysoka szczegółowość zamiast normalnych [— #3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore pack3 powinien domyślnie zawierać dokumentację XML - [#3698](https://github.com/NuGet/Home/issues/3698)

- Aktualizacja wsadowa kończy się niepowodzeniem z interfejsu użytkownika, gdy źródło bez pakietu jest pierwsze i wybrano wszystkie źródło - [#3696](https://github.com/NuGet/Home/issues/3696)

- Polecenie Nuget pack nie zawiera wszystkich plików - [#3678](https://github.com/NuGet/Home/issues/3678)

- Problem OOM - [#3661](https://github.com/NuGet/Home/issues/3661)

- ProjectFileDependencyGroups sekcji pliku zasobów należy użyć nazw bibliotek dla projektów - [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" i powtarzające się katalogi - [#3517](https://github.com/NuGet/Home/issues/3517)

- Błędy przywracania3 są rejestrowane jako ostrzeżenia zamiast błędów - [#3503](https://github.com/NuGet/Home/issues/3503)

- Problem z TFS: "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego" - [#2805](https://github.com/NuGet/Home/issues/2805)

- Wpisując "nuget <packagename>" w polu wyszukiwania vs quicklaunch zachowuje prefiks "nuget " - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Nierozpoznany element główny w części Właściwości rdzenia. Linia 2, pozycja 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec`z &lt; przestawną lub &gt; w polach tekstowych nie buduje - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe delete nie monituje o poświadczenia (jest w trybie nieinterakcyjnym) - [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete ostrzega o kluczu INTERFEJSU API dla źródeł lokalnych, mimo że nie ma sensu - [#2625](https://github.com/NuGet/Home/issues/2625)

- Podczas instalowania pakietu EF -pre package — [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio uległ awarii po zmianie wyboru w Menedżerze pakietów - [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - przywracanie dotnetcore wykonuje wyszukiwania identyfikatorów z uwzględnieniem wielkości liter w repozytoriach lokalnych z płaską listą, gdy używane są wersje przestawne — [#2516](https://github.com/NuGet/Home/issues/2516)

- nuget.exe delete jest uszkodzony dla kanału V2 - [#2509](https://github.com/NuGet/Home/issues/2509)

- limit czasu wypychania nuget.exe wymaga lepszego komunikatu o błędzie - [#2503](https://github.com/NuGet/Home/issues/2503)

- Przywracanie narzędzia bez prawidłowego importu po cichu kończy się niepowodzeniem. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet monituje o wprowadzenie poświadczeń, gdy istnieje prywatny kanał informacyjny, nawet podczas instalacji z nuget.org — [#2346](https://github.com/NuGet/Home/issues/2346)

- Pakiet ApplicationInsights 2.0 jest wymieniony, ale jeszcze nie istnieje — [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay w VS "15" podgląd 5 oddział - [#3500](https://github.com/NuGet/Home/issues/3500)

- Pierwsze zdarzenie OnBuild jest pomijane dla przywracania podczas kompilacji dla platformy uniwersalnej systemu i platformy uniwersalnej — [#3489](https://github.com/NuGet/Home/issues/3489)

- Program PowerShell5 przerywa instalację programu EntityFramework? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Dodaj źródło do szczegółowego rejestrowania (należy wziąć pod uwagę dla 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr NoCache nie jest honorowany w wersji klienta nuget 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)

- Gdy dostawca poświadczeń nie można załadować w programie VS, nie przerywaj nuget - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkcje

- Konfigurowanie ciągłego uruchamiania w celu uruchomienia x86 - [#3868](https://github.com/NuGet/Home/issues/3868)

- Automatyczne przywracanie 3/3: nieblokowanie interfejsu użytkownika - [#3658](https://github.com/NuGet/Home/issues/3658)

- Auto Restore 2/3: przywracanie tła przy nominacji - [#3657](https://github.com/NuGet/Home/issues/3657)

- Przywróć refs projektu, aby dopasować zachowanie kompilacji (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)

- Obsługa DPL w VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Przenieś plik ustawień do plików programu - [#3613](https://github.com/NuGet/Home/issues/3613)

- Wygenerowane rekwizyty i cele przywracania wymagają wsparcia uczestnictwa w przekroju - [#3496](https://github.com/NuGet/Home/issues/3496)

- Obsługa nuget restore dla PackageTargetFallback (f.k.a Imports) — [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementacja ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 dla rid - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet UI do obsługi dodaj/usuń/aktualizuj y packagerefs - [#3457](https://github.com/NuGet/Home/issues/3457)

- Auto Restore 1/3: Implemenation nominacji API za pośrednictwem buforowania project restore info - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] Cele & zadań przywracania nuget - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Włącz przywracanie poziomu rozwiązania w MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Publiczne rozszerzalność dostawcy poświadczeń pomocy technicznej w programie Visual Studio [— #2909](https://github.com/NuGet/Home/issues/2909)

- Rekursywne przywracanie nuget - [#2533](https://github.com/NuGet/Home/issues/2533)

- Nie można załadować microsoft.TeamFoundation.Client na dev15, trzeba zaktualizować wersję Microsoft.TeamFoundation.Client do 15.0 dla VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)

- Nie można zainstalować pakietu C++ w projekcie platformy uniwersalnej systemu Windows w programie VS "15" Preview — [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg musi obsługiwać folder \buildCrossTargeting\ i importować `.targets`  /  `.props` dla "crosstargeting" zakres MSBuild. - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)

- Napraw interfejs użytkownika NuGet do obsługi przywracania `.csproj`  - w/ PackageReferences w [#3455](https://github.com/NuGet/Home/issues/3455)

- Dodawanie przycisku wyczyść pamięć podręczną do ustawień menedżera pakietów VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DDR

- Przywracanie rozwiązania powinno być blokowane podczas automatycznego przywracania. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NetCore zainstalować z NuGet Package Manager UI instaluje się do każdego TFM , zamiast tych, które obsługuje pakiet - [#3721](https://github.com/NuGet/Home/issues/3721)

- Przywróć nominator API musi obsługiwać DotNetCliToolsReferences zbyt. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Oznacz vs "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- Migrowanie z odwoływania się do MS. Vs. Services.Client do MS. Vs. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) powinny być przestrzegane na poziomie projektu przez restore - [#3618](https://github.com/NuGet/Home/issues/3618)

- Przywracanie do projektu za pomocą pojedynczego targetframework nie może kondycjonować rekwizytów - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj powinien podążać za zależnościami projectref i przywracać te również. Jak budować. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": zależności "platformy" reprezentowane jako "typ":"pakiet" w pliku blokady - [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe Tryb verbose powinien pokazać adres URL pobierania - [#2629](https://github.com/NuGet/Home/issues/2629)

- Przenieś nuget xplat do microsoft.NetCore.App i netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push - Powinno być możliwe zastąpienie serwera symboli podczas wypychania z wiersza polecenia - [#2348](https://github.com/NuGet/Home/issues/2348)

- Skonsoliduj kod do znajdowania ścieżki pakietów globalnych — [#2296](https://github.com/NuGet/Home/issues/2296)

- Potrzebujesz lepszej nazwy niż suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Określanie `project.json` nazwy zależności do użycia dla projektów MSBuild — [#1914](https://github.com/NuGet/Home/issues/1914)

- Dodaj obsługę SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Zezwalaj na przechodnie zależności `.targets` NuPkgs z być dostępne w MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- Przywracanie NuGet z wiersza polecenia jest znacznie wolniejsze niż VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- Spraw, aby identyfikator pakietu i przypadek porównania wersji były niewrażliwe - [#2522](https://github.com/NuGet/Home/issues/2522)

- Opcja NoCache nie `packages.config` działa w przypadku przywracania/instalowania na podstawie (GlobalPackagesFolder) — [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdResource zasobów potrzebuje domyślnego kontekstu pamięci podręcznej i rejestratora - [#1357](https://github.com/NuGet/Home/issues/1357)
