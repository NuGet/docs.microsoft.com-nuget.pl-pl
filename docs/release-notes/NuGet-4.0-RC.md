---
title: Informacje o wersji programu NuGet 4.0 RC
description: Informacje o wersji NuGet 4.0 RC obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549249"
---
# <a name="nuget-40-rc-release-notes"></a>Informacje o wersji programu NuGet 4.0 RC

[Informacje o wersji programu NuGet 3.5 RTM](../release-notes/nuget-3.5-RTM.md)

[Program NuGet 4.0 RC programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na dodano obsługę scenariuszy .NET Core, odnoszący się opinie klientów i zwiększanie wydajności w różnych scenariuszach. Ta wersja oferuje kilka udoskonaleń, takich jak obsługa PackageReference, NuGet polecenia jako elementy docelowe programu MSBuild, przywracania pakietów w tle i nie tylko.

## <a name="bug-fixes"></a>Poprawki błędów

- Zmiany zachowania w `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- Przywracanie nuget.exe dla programu vs "15" tylko komputera nie powiodło się — [#3834](https://github.com/NuGet/Home/issues/3834)

- . Nowy projekt pliku NETCore powinna blokować kompilacji podczas przywracania - [#3780](https://github.com/NuGet/Home/issues/3780)

- Aplikacja sieci web platformy ASP.NET Core, poddane migracji z programu VS2015 VS "15", nie można przywrócić. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Niepowodzenie testu] Nie można odinstalować pakietu "jQuery weryfikacji" przez interfejs użytkownika PM - [#3755](https://github.com/NuGet/Home/issues/3755)

- Po zainstalowaniu pakietu do platformy uniwersalnej systemu Windows `project.json`, projekty nadrzędnego powinny również zostanie przywrócony - [#3731](https://github.com/NuGet/Home/issues/3731)

- Modyfikowanie cele NuGet logowania źródła pakietów jako wysoki poziom szczegółowości zamiast normalny - [#3719](https://github.com/NuGet/Home/issues/3719)

- polecenia DotNet
  - dotnetcore dodatkiem Service Pack 3 powinna zawierać dokumentację XML domyślnie - [#3698](https://github.com/NuGet/Home/issues/3698)

- Batch aktualizacja nie powiodła się z poziomu interfejsu użytkownika po wybraniu wszystkich źródła - i źródła bez pakietu jest pierwszy [#3696](https://github.com/NuGet/Home/issues/3696)

- Polecenie pakietu Nuget nie zawiera wszystkie pliki - [#3678](https://github.com/NuGet/Home/issues/3678)

- Za mało pamięci problemu — [#3661](https://github.com/NuGet/Home/issues/3661)

- Sekcja ProjectFileDependencyGroups pliku zasobów, należy użyć nazwy bibliotek dla projekty — [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" i recursing katalogów - [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 błędy są rejestrowane jako ostrzeżenia zamiast błędów — [#3503](https://github.com/NuGet/Home/issues/3503)

- Problem z TFS: "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Wpisywanie "nuget <packagename>" w programie vs pole wyszukiwania szybkiego uruchamiania utrzymuje prefiksu "nuget" - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Element główny nierozpoznaną część podstawowe właściwości. Wiersz 2, pozycji 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` za pomocą ucieczki &lt; lub &gt; pól w tekście nie umożliwia już skompilowania - [#2651](https://github.com/NuGet/Home/issues/2651)

- Usuń nuget.exe nie Monituj o poświadczenia, (jest w trybie nieinterakcyjnym) - [#2626](https://github.com/NuGet/Home/issues/2626)

- Usuń nuget.exe ostrzega o klucz interfejsu API dla źródeł lokalnych, nawet jeśli nie ma sensu — [#2625](https://github.com/NuGet/Home/issues/2625)

- Niska środowisko błąd podczas instalowania programu EF - pre package — [#2566](https://github.com/NuGet/Home/issues/2566)

- Program Visual Studio uległ awarii, próby po zmianie wyboru w Menedżerze pakietów - [#2551](https://github.com/NuGet/Home/issues/2551)

- polecenia DotNet
  - Przywracanie dotnetcore wykonuje z uwzględnieniem wielkości liter wyszukiwania identyfikatora kwerendy płaskiej listy repozytoriów lokalnych podczas korzystania z wersji zmiennoprzecinkowy — [#2516](https://github.com/NuGet/Home/issues/2516)

- Usuń nuget.exe nie działa dla źródła danych w wersji 2 - [#2509](https://github.com/NuGet/Home/issues/2509)

- limit czasu wypychania nuget.exe musi udoskonalony komunikat o błędzie - [#2503](https://github.com/NuGet/Home/issues/2503)

- Narzędzie przywracania bez odpowiedniego dyskretnie importuje kończy się niepowodzeniem. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet wyświetla monit o podanie poświadczeń, gdy istnieje prywatne źródło danych nawet wtedy, gdy instalowanie z repozytorium nuget.org — [#2346](https://github.com/NuGet/Home/issues/2346)

- Pakiet dotycząca usługi Application Insights w wersji 2.0, znajduje się na liście, ale nie istnieje jeszcze - [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay w programie VS "15" w wersji zapoznawczej 5 gałąź — [#3500](https://github.com/NuGet/Home/issues/3500)

- Pierwsze zdarzenie OnBuild brakuje przywracane podczas kompilacji dla platformy uniwersalnej systemu Windows — [#3489](https://github.com/NuGet/Home/issues/3489)

- Podziały PowerShell5 EntityFramework instalacji? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Dodawanie źródła danych do szczegółowe rejestrowanie (należy wziąć pod uwagę 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr Właściwość NoCache nie honorowane w wersji klienta nuget 3.4. + - [#3074](https://github.com/NuGet/Home/issues/3074)

- Gdy dostawca poświadczeń nie można załadować w programie VS, nie DZIEL NuGet — [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkcje

- Konfigurowanie ciągłej integracji na potrzeby uruchamiania x86- [#3868](https://github.com/NuGet/Home/issues/3868)

- Automatycznego przywracania 3/3: bez blokujące elementy interfejsu użytkownika — [#3658](https://github.com/NuGet/Home/issues/3658)

- Automatycznego przywracania 2/3: przywracanie dla nominacji — w tle [#3657](https://github.com/NuGet/Home/issues/3657)

- Przywracanie projektu systemu plików refs, aby dopasować zachowanie kompilacji (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)

- DPL obsługi w programie VS "15" — minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Przenieś plik ustawień Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)

- Cele i właściwości wygenerowanej przywracania potrzebujesz przeznaczonych dla wielu współdziałania ze strony pomocy technicznej — [#3496](https://github.com/NuGet/Home/issues/3496)

- Przywracanie NuGet obsługę PackageTargetFallback (f.k.a Importy) - [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementacja ToolsRef — [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 dla identyfikatora RID - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet interfejsu użytkownika w celu obsługi Dodaj/Usuń/zaktualizuj PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)

- Automatycznego przywracania 1/3: Implementacji nominacji interfejsu API za pośrednictwem buforowanie projektu przywracanie informacji - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet Restore, zadania i elementy docelowe — [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Włącz Przywracanie na poziomie rozwiązania w programie MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Obsługuje rozszerzalność publicznego dostawcy poświadczeń w programie Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)

- Przywracanie pakietów nuget cykliczne - [#2533](https://github.com/NuGet/Home/issues/2533)

- Nie można załadować Microsoft.TeamFoundation.Client dev15, trzeba zaktualizować Microsoft.TeamFoundation.Client w wersji 15.0 dla programu VS "15" (wersja zapoznawcza) — [#2392](https://github.com/NuGet/Home/issues/2392)

- Nie można zainstalować pakiet języka C++ platformy uniwersalnej systemu Windows w języku C++ projektu w programie VS "15" (wersja zapoznawcza) — [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg musi obsługiwać folder \buildCrossTargeting\ — i zaimportować `.targets`  /  `.props` dla "crosstargeting" zakresu programu MSBuild. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Projekt ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)

- Napraw NuGet interfejsu użytkownika, która obsługuje Przywracanie z PackageReferences w `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- Dodawanie przycisk Wyczyść pamięć podręczną, aby ustawienia Menedżera pakietów programu VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCRs

- Rozwiązanie Przywróć powinien być blokowany podczas automatycznego przywracania. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NetCore instalacji z poziomu interfejsu użytkownika Menedżera pakietów NuGet instaluje co TFM, a nie te, które obsługuje pakiet - [#3721](https://github.com/NuGet/Home/issues/3721)

- Przywróć nominator interfejsu API musi obsługiwać DotNetCliToolsReferences zbyt. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Oznacz naszych VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- Przeprowadź migrację z odwołujące się do MS. VS. Services.Client MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) powinny być przestrzegane na poziomie projektu przez Przywracanie — [#3618](https://github.com/NuGet/Home/issues/3618)

- Przywracanie projektu za pomocą pojedynczego TargetFramework nie musi warunku właściwości - [#3588](https://github.com/NuGet/Home/issues/3588)

- polecenia DotNet
  - dotnetcore restore3 foo.csproj powinny wykonaj projectref zależności, a także przywrócić te zbyt. Podobnie jak kompilacji. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platforma" zależności reprezentowane jako "type": "pakiet" w pliku blokady - [#2695](https://github.com/NuGet/Home/issues/2695)

- Tryb informacji pełnej nuget.exe powinien być wyświetlony pobierania adresa url – [#2629](https://github.com/NuGet/Home/issues/2629)

- Przenieś NuGet xplat pakietów Microsoft.NetCore.App i netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push — powinno być możliwe do przesłonięcia serwera symboli, podczas wypychania z wiersza polecenia — [#2348](https://github.com/NuGet/Home/issues/2348)

- Skonsolidować kodu do znajdowania globalnego pakietów ścieżka - [#2296](https://github.com/NuGet/Home/issues/2296)

- Potrzebujesz nazwę lepsze niż suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Określić `project.json` Nazwa zależności dla projektów programu MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)

- Dodano obsługę SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Zezwalaj na przechodnie zależności NuPkgs z `.targets` mają być dostępne w programie MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- Przywracanie pakietów NuGet z wiersza polecenia jest znacznie wolniejsze niż VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- Wprowadź bez uwzględniania wielkości liter — porównanie identyfikator i wersja pakietu [#2522](https://github.com/NuGet/Home/issues/2522)

- Właściwość NoCache opcji nie działa w przypadku `packages.config` przywracania/instalacja (GlobalPackagesFolder) — oparta na [#1406](https://github.com/NuGet/Home/issues/1406)

- Wymagane przez zasoby FindPackageByIdResource domyślny kontekst pamięci podręcznej i rejestratora - [#1357](https://github.com/NuGet/Home/issues/1357)
