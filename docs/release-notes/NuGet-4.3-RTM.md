---
title: Informacje o wersji narzędzia NuGet 4,3 RTM
description: Informacje o wersji dla programu NuGet 4,3 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e9b6d15584d875f59ed64fe662944db3e37aeabb
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780178"
---
# <a name="nuget-43-release-notes"></a>Informacje o wersji narzędzia NuGet 4,3

[Program Visual Studio 2017 15,3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z pakietem NuGet 4,3 RTM, który dodaje obsługę nowych scenariuszy, takich jak .NET Standard 2.0/. NET Core 2,0, zawiera wiele poprawek dotyczących jakości i poprawia wydajność. Ta wersja oferuje również kilka ulepszeń, takich jak obsługa 2.0.0 wersji semantycznej, integracja programu MSBuild z ostrzeżeniami i błędami NuGet oraz inne.

## <a name="summary-whats-new-in-430"></a>Podsumowanie: co nowego w programie 4.3.0

## <a name="summary-whats-new-in-431"></a>Podsumowanie: co nowego w 4.3.1

* Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)
* Poprawka zabezpieczeń: pliki wewnątrz elementu NUPKGs mogą mieć ścieżkę względną powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Przywracanie pakietów NuGet może w niektórych przypadkach traktować wyłączone źródła pakietów jako włączone

#### <a name="issue"></a>Problem

Następujące techniki przywracania wiersza polecenia traktują wyłączone źródła pakietów jako włączone. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (z dotnet.exe, które są dostarczane z programem VS, lub z tym, który jest dostarczany z zestawem SDK 2.0.0)

#### <a name="workaround"></a>Obejście

1. Użyj programu Visual Studio (2017 15.3 lub nowszego) lub NuGet.exe (4.3.0 lub nowszego)
1. Usuń wyłączone źródła i dalej używaj programu msbuild lub programu dotnet.exe.
1. Na potrzeby rozwiązania możesz użyć polecenia „Clear” (Wyczyść) w pliku NuGet.config, a następnie zdefiniować źródła dla tego rozwiązania.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlać, dodawać ani aktualizować składnika dotnetclitools przy użyciu Menedżera pakietów NuGet

#### <a name="issue"></a>Problem

Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Obejście

Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense

#### <a name="issue"></a>Problem

Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio. Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Obejście

Wykonaj przywracanie ręczne.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problemy rozwiązane w przedziale czasu NuGet 4,3 RTM

[Informacje o wersji programu nuget 4,0 RTM](../release-notes/nuget-4.0-RTM.md) — lista wszystkich problemów rozwiązanych w przypadku programu NuGet 4,0 RTM

### <a name="features"></a>Funkcje

- Poprawianie wydajności przywracania NuGet — implementowanie inteligentniejszej aktualizujący nie działa dla wiersza polecenia przywraca i [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2,0: interfejs wiersza polecenia VS/dotnet powinien zacząć korzystać z istniejących funkcji NuGet: foldery rezerwowe — [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2,0: zezwól użytkownikom na ignorowanie określonych ostrzeżeń przywracania (lub Podnieś do błędu) — [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2,0: zlokalizowane zestawy interfejsu wiersza polecenia — [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2,0: rejestruje wszystkie ostrzeżenia/błędy w pliku zasobów (w tym PackageTargetFallback) — [#4895](https://github.com/NuGet/Home/issues/4895)

- Włącz obsługę TFM: Standard 2.0, Tizen- [#4892](https://github.com/NuGet/Home/issues/4892)

- Zmniejsz liczbę pakietów NuGet. Core i NuGet. Projects (i bibliotek DLL) — [#2446](https://github.com/NuGet/Home/issues/2446)

- Dodawanie możliwości oznaczania ostrzeżeń NuGet jako błędów — [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Usterki

- MSBuild/t: pakiet kończy się niepowodzeniem z parametrem "DevelopmentDependency" nie jest obsługiwany przez zadanie "PackTask" — [#5584](https://github.com/NuGet/Home/issues/5584)

- Struktura katalogów dla plików zawartości spłaszczonych bez dodawania separatora katalogów systemu Windows na końcu PackagePath- [#4795](https://github.com/NuGet/Home/issues/4795)

- projekty podstawowe nie obsługują ustawienia jako developmentDependency- [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage jest ładowany synchronicznie, który zablokowany wątek interfejsu użytkownika i zakleszczenie w programie VS- [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnetcore Restore (& w związku z tym MSBuild/t: Restore) pomija projekty z jawną zależnością projektu rozwiązania [#4578](https://github.com/NuGet/Home/issues/4578)

- Jeśli rozwiązanie ma zawierających, które odwołuje się do tego samego projektu z inną wielkością liter, przywracanie może nie zadziałało. Dotyczy to również różnych ścieżek względnych bez różnic w wielkości liter — [#4574](https://github.com/NuGet/Home/issues/4574)

- Pliki wykonywalne przywrócone z pakietów NuGet nie są już wykonywalne przy użyciu programu .NET Core 2,0- [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exee szczegóły wyjątku podczas analizowania pliku rozwiązania — [#4411](https://github.com/NuGet/Home/issues/4411)

- Pakiet umieszcza pliki zawartości w niewłaściwej lokalizacji, jeśli ContentTargetFolders zawiera ścieżkę kończącą się znakiem "/" w systemie Windows- [#4407](https://github.com/NuGet/Home/issues/4407)

- Nie można przywrócić elementu DotNetCliToolReference dla pakietu narzędzi, który jest przeznaczony dla netcoreapp 1.1- [#4396](https://github.com/NuGet/Home/issues/4396)

- Interfejs wiersza polecenia aktualizacji NuGet pozostawia stary stan wersji pakietu w pliku projektu (C++) — [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- Odczytaj DotnetCliToolTargetFramework z CPS nomation- [#5397](https://github.com/NuGet/Home/issues/5397)

- Sprawdzenie TPMinV powinno być wykonane dla PJ style platformy UWP- [#4763](https://github.com/NuGet/Home/issues/4763)

- Popraw opis interfejsu użytkownika dla pakietów z obsługą autoreferencji — [#4471](https://github.com/NuGet/Home/issues/4471)

- Przywrócenie NuGet polega na wybraniu opcji Kompiluj elementy zawartości z środowiska uruchomieniowego. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Umieść diagnostykę zależności w pliku blokady — [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Linki do problemów z usługą GitHub rozwiązane w 4,3 RTM

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
