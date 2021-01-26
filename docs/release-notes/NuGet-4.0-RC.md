---
title: Informacje o wersji narzędzia NuGet 4,0 RC
description: Informacje o wersji programu NuGet 4,0 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780192"
---
# <a name="nuget-40-rc-release-notes"></a>Informacje o wersji narzędzia NuGet 4,0 RC

[Informacje o wersji narzędzia NuGet 3,5 RTM](../release-notes/nuget-3.5-RTM.md)

Pakiet [NuGet 4,0 RC dla programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na dodawaniu obsługi scenariuszy platformy .NET Core, rozwiązywaniu kluczowych opinii klientów i ulepszaniu wydajności w różnych scenariuszach. W tej wersji wprowadzono kilka ulepszeń, takich jak obsługa PackageReference, poleceń NuGet jako obiektów docelowych programu MSBuild, przywracania pakietów w tle i innych.

## <a name="bug-fixes"></a>Poprawki błędów

- Zmiany zachowania w `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- nuget.exe przywracania na komputerze vs "15" kończy się niepowodzeniem — [#3834](https://github.com/NuGet/Home/issues/3834)

- . Nowy projekt pliku podstawowego powinien blokować kompilację podczas przywracania [#3780](https://github.com/NuGet/Home/issues/3780)

- Nie można przywrócić ASP.NET Core aplikacji sieci Web migrowanej z programu VS2015 do programu VS "15". - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Niepowodzenie testu] Nie można odinstalować pakietu "jQuery Validation" przy użyciu interfejsu użytkownika PM — [#3755](https://github.com/NuGet/Home/issues/3755)

- Gdy pakiet jest zainstalowany w platformy UWP `project.json` , należy również przywrócić projekty nadrzędne — [#3731](https://github.com/NuGet/Home/issues/3731)

- Zmodyfikuj cele NuGet, aby rejestrować źródła pakietów jako wysoki poziom szczegółowości zamiast normalnej [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore Pack3 powinien domyślnie zawierać dokumentację XML — [#3698](https://github.com/NuGet/Home/issues/3698)

- Aktualizacja usługi Batch kończy się niepowodzeniem z poziomu interfejsu użytkownika, gdy źródło bez pakietu jest wybrane — [#3696](https://github.com/NuGet/Home/issues/3696)

- Polecenie pakietu NuGet nie obejmuje wszystkich plików — [#3678](https://github.com/NuGet/Home/issues/3678)

- Problem z OOM — [#3661](https://github.com/NuGet/Home/issues/3661)

- Sekcja ProjectFileDependencyGroups pliku Assets powinna używać nazw bibliotek dla projektów — [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" i powtarzanie katalogów — [#3517](https://github.com/NuGet/Home/issues/3517)

- Błędy Restore3 są rejestrowane jako ostrzeżenia zamiast błędów — [#3503](https://github.com/NuGet/Home/issues/3503)

- Problem z TFS: "[plik] nie został znaleziony w Twoim obszarze roboczym lub nie masz uprawnień dostępu do niego"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Wpisanie słowa "NuGet <packagename> " w polu wyszukiwania programu vs — umożliwia zachowanie prefiksu "NuGet" — [#2719](https://github.com/NuGet/Home/issues/2719)

- Wyjątek System.Xml.Xml: nierozpoznany element główny w części Core Properties. Wiersz 2, pozycja 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` w przypadku &lt; , gdy &gt; w polach tekstowych nie są już kompilacje — [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe usuwania nie będzie monitować o poświadczenia (jest w trybie nieinteraktywnym) — [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe Delete ostrzega o kluczu interfejsu API dla źródeł lokalnych, nawet jeśli nie ma sensu [#2625](https://github.com/NuGet/Home/issues/2625)

- Wystąpił błąd podczas instalowania pakietu EF-pre- [#2566](https://github.com/NuGet/Home/issues/2566)

- Program Visual Studio uległ awarii po zmianie zaznaczenia w Menedżerze pakietów — [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - Funkcja przywracania dotnetcore wykonuje wyszukiwania identyfikatorów z uwzględnieniem wielkości liter w lokalnych repozytoriach na płaskich listach, gdy są używane wersje zmiennoprzecinkowe — [#2516](https://github.com/NuGet/Home/issues/2516)

- nuget.exe usunięcie jest zerwane dla źródła danych w wersji 2 [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe przekroczenie limitu czasu wypychania wymaga lepszego komunikatu o błędzie — [#2503](https://github.com/NuGet/Home/issues/2503)

- Przywracanie narzędzia bez odpowiednich importów w trybie dyskretnym nie powiodło się. - [#2462](https://github.com/NuGet/Home/issues/2462)

- Pakiet NuGet monituje o wprowadzenie poświadczeń, gdy istnieje prywatne źródło danych nawet podczas instalacji z nuget.org- [#2346](https://github.com/NuGet/Home/issues/2346)

- Pakiet ApplicationInsights 2,0 jest wymieniony, ale jeszcze nie istnieje — [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay w programie VS "15" (wersja zapoznawcza 5) — [#3500](https://github.com/NuGet/Home/issues/3500)

- Nie pominięto pierwszego zdarzenia onbuild dla przywracania podczas kompilacji dla platformy UWP- [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 przerwań instalacji EntityFramework? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Dodaj źródło do szczegółowego rejestrowania (Rozważ 3,5) — [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr nocache nie został uznany w kliencie NuGet w wersji 3.4 +- [#3074](https://github.com/NuGet/Home/issues/3074)

- W przypadku niepowodzenia ładowania dostawcy poświadczeń w programie VS nie należy dzielić narzędzia NuGet- [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkcje

- Skonfiguruj CI do uruchamiania architektury x86 [#3868](https://github.com/NuGet/Home/issues/3868)

- Autoprzywracanie 3/3: nie blokuje interfejsu użytkownika [#3658](https://github.com/NuGet/Home/issues/3658)

- Autoprzywracanie 2/3: przywracanie w tle w wyznaczonym [#3657](https://github.com/NuGet/Home/issues/3657)

- Przywróć odwołania projektu w celu dopasowania do zachowania kompilacji (rekursywnie) — [#3615](https://github.com/NuGet/Home/issues/3615)

- Obsługa DPL w programie VS "15"-minbar- [#3614](https://github.com/NuGet/Home/issues/3614)

- Przenoszenie pliku ustawień do plików programu — [#3613](https://github.com/NuGet/Home/issues/3613)

- Wygenerowane właściwości przywracania i elementy docelowe wymagają obsługi partycypacji obejmującej wiele elementów docelowych — [#3496](https://github.com/NuGet/Home/issues/3496)

- Obsługa przywracania NuGet dla PackageTargetFallback (f. k. a Imports) — [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementacja ToolsRef — [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 identyfikatorów RID [#3465](https://github.com/NuGet/Home/issues/3465)

- Interfejs użytkownika narzędzia NuGet do obsługi dodawania/usuwania/aktualizowania PackageRefs- [#3457](https://github.com/NuGet/Home/issues/3457)

- Automatyczne przywracanie 1/3: implementacji interfejsu API wyznaczania przez buforowanie informacji o przywracaniu projektu — [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] zadanie przywracania NuGet & cele — [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Włącz przywracanie na poziomie rozwiązania w programie MSBuild — [#2993](https://github.com/NuGet/Home/issues/2993)

- Obsługa publicznej rozszerzalności dostawcy poświadczeń w programie Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)

- Rekursywne przywracanie NuGet — [#2533](https://github.com/NuGet/Home/issues/2533)

- Nie można załadować Microsoft. TeamFoundation. Client on dev15, należy zaktualizować wersję Microsoft. TeamFoundation. Client do 15,0 dla programu VS "15" (wersja zapoznawcza) [#2392](https://github.com/NuGet/Home/issues/2392)

- Nie można zainstalować pakietu C++ do projektu C++ platformy UWP w programie VS "15" (wersja zapoznawcza) — [#2369](https://github.com/NuGet/Home/issues/2369)

- NUPKG musi obsługiwać folder \buildCrossTargeting\ i importować `.targets`  /  `.props` dla zakresu programu MSBuild "crosstargeting". - [#3499](https://github.com/NuGet/Home/issues/3499)

- Projekt ToolsReference — [#3462](https://github.com/NuGet/Home/issues/3462)

- Napraw interfejs użytkownika NuGet, aby obsługiwał przywracanie z/składnika packagereferences w `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- Dodawanie przycisku Wyczyść pamięć podręczną do ustawień Menedżera pakietów programu VS — [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- Przywracanie rozwiązania powinno być blokowane, gdy jest wykonywane Autoprzywracanie. - [#3797](https://github.com/NuGet/Home/issues/3797)

- Instalacja programu servicecore z poziomu interfejsu użytkownika Menedżera pakietów NuGet jest instalowana do każdego TFMu, a nie do tych, które są obsługiwane przez pakiet — [#3721](https://github.com/NuGet/Home/issues/3721)

- Interfejs API przywracania nominowania musi również obsługiwać DotNetCliToolsReferences. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Oznacz nasz plik VSIX programu VS "15" jako SystemComponent [#3700](https://github.com/NuGet/Home/issues/3700)

- Migruj z odwołującego się do MS. Lokalne. Services. Client do MS. Lokalne. Services. Client. Interactive — [#3670](https://github.com/NuGet/Home/issues/3670)

- Wartość $ (RestoreLegacyPackagesDirectory) powinna być przestrzegana na poziomie projektu przez przywrócenie [#3618](https://github.com/NuGet/Home/issues/3618)

- Przywracanie do projektu z pojedynczym TargetFrameworkem nie może mieć warunku- [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo. csproj powinna być zgodna z zależnościami projectref i przywrócić te. Podobnie jak kompilacja. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "Type": zależności "platform" reprezentowane jako "Type": "Package" w pliku blokady — [#2695](https://github.com/NuGet/Home/issues/2695)

- W trybie pełny nuget.exe powinien zostać wyświetlony adres URL pobierania — [#2629](https://github.com/NuGet/Home/issues/2629)

- Przenoszenie NuGet Xplat do Microsoft. WebCore. app i netcoreapp 1.0- [#2483](https://github.com/NuGet/Home/issues/2483)

- Wypychanie — powinno być możliwe przesłonięcie serwera symboli podczas wypychania z wiersza polecenia — [#2348](https://github.com/NuGet/Home/issues/2348)

- Konsolidowanie kodu do znajdowania ścieżki pakietów globalnych — [#2296](https://github.com/NuGet/Home/issues/2296)

- Potrzebna lepsza nazwa niż suppressParent — [#2196](https://github.com/NuGet/Home/issues/2196)

- Określanie `project.json` nazwy zależności, która ma być używana dla projektów MSBuild — [#1914](https://github.com/NuGet/Home/issues/1914)

- Dodawanie obsługi SemVer 2.0.0 do narzędzia NuGet. Core — [#3383](https://github.com/NuGet/Home/issues/3383)

- Zezwalaj na użycie przechodniej NuPkgs zależności `.targets` w programie MSBuild — [#3342](https://github.com/NuGet/Home/issues/3342)

- Przywracanie NuGet z wiersza polecenia jest znacznie wolniejsze niż VS- [#3330](https://github.com/NuGet/Home/issues/3330)

- Ustaw identyfikator pakietu i wersję z uwzględnieniem wielkości liter — [#2522](https://github.com/NuGet/Home/issues/2522)

- Opcja NoCache nie działa na `packages.config` podstawie przywracania/instalacji (GlobalPackagesFolder) — [#1406](https://github.com/NuGet/Home/issues/1406)

- Zasoby FindPackageByIdResource potrzebują domyślnego kontekstu pamięci podręcznej i rejestratora [#1357](https://github.com/NuGet/Home/issues/1357)
