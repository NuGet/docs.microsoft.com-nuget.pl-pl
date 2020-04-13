---
title: Informacje o wydaniu programu NuGet 4.3 RTM
description: Informacje o wersji dla NuGet 4.3 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496591"
---
# <a name="nuget-43-release-notes"></a>Informacje o wersji nuget 4.3

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest wyposażony w NuGet 4.3 RTM, który dodaje obsługę nowych scenariuszy, takich jak .NET Standard 2.0/.NET Core 2.0, zawiera wiele poprawek jakości i zwiększa wydajność. Ta wersja zawiera również kilka ulepszeń, takich jak obsługa semantycznego przechowywania wersji 2.0.0, integracja MSBuild z ostrzeżeniami i błędami NuGet i inne.

## <a name="summary-whats-new-in-430"></a>Krótki opis: Co nowego w 4.3.0

## <a name="summary-whats-new-in-431"></a>Krótki opis: Co nowego w 4.3.1

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)
* Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Przywracanie pakietów NuGet może w niektórych przypadkach traktować wyłączone źródła pakietów jako włączone

#### <a name="issue"></a>Problem

Następujące techniki wiersza polecenia przywracania traktują wyłączone źródła pakietów jako włączone. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore`(albo z dotnet.exe, który jest dostarczany z VS, lub ten, który jest dostarczany z NetCore SDK 2.0.0)

#### <a name="workaround"></a>Obejście

1. Użyj programu Visual Studio (2017 15.3 lub nowszego) lub NuGet.exe (4.3.0 lub nowszego)
1. Usuń wyłączone źródła i dalej używaj programu msbuild lub programu dotnet.exe.
1. Na potrzeby rozwiązania możesz użyć polecenia „Clear” (Wyczyść) w pliku NuGet.config, a następnie zdefiniować źródła dla tego rozwiązania.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlać, dodawać ani aktualizować dotNetCLITools przy użyciu Menedżera pakietów Nuget

#### <a name="issue"></a>Problem

Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Obejście

Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense

#### <a name="issue"></a>Problem

Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio. Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Obejście

Wykonaj przywracanie ręczne.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Naprawiono problemy w ramach czasowych NuGet 4.3 RTM

[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Wyświetla listę wszystkich problemów rozwiązanych dla NuGet 4.0 RTM

### <a name="features"></a>Funkcje

- Usprawnij narzędzie Przywracanie NuGet — implementuj inteligentniejsze noop dla przywracania wiersza polecenia i VS — [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: VS/Dotnet CLI powinien rozpocząć korzystanie z istniejących funkcji NuGet: foldery FallBack - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: Włącz użytkownikom ignorowanie określonych ostrzeżeń przywracania (lub podniesienie poziomu błędu) — [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: Zlokalizowane przez CLI zespoły - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: zarejestruj wszystkie ostrzeżenia/błędy w pliku zasobów (w tym PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Włącz obsługę TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Zmniejsz liczbę projektów NuGet.Core i NuGet.Client (a tym samym bibliotek dll) — [#2446](https://github.com/NuGet/Home/issues/2446)

- Dodaj możliwość oznaczania ostrzeżeń nuget jako błędów - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Usterki

- msbuild /t:pack kończy się niepowodzeniem z parametrem "DevelopmentDependency" nie jest obsługiwany przez zadanie "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)

- Struktura katalogów dla plików zawartości spłaszczona, jeśli nie dodaje separatora katalogu systemu Windows na końcu Programu PackagePath — [#4795](https://github.com/NuGet/Home/issues/4795)

- projekty netcore nie obsługują ustawiania jako rozwojuZależność - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage jest ładowany synchronicznie, który zablokował wątek interfejsu użytkownika i zakleszczony VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnetcore Restore (& dlatego msbuild /t:restore) pomija projekty z jawną zależnością projektu rozwiązania [#4578](https://github.com/NuGet/Home/issues/4578)

- Jeśli rozwiązanie ma projectreferences, które odnoszą się do tego samego projektu, z różnych wielkości liter, przywracanie może nie działać. Wpływa to również na różne ścieżki względne, bez różnicy w obudowy - [#4574](https://github.com/NuGet/Home/issues/4574)

- Pliki wykonywalne przywrócone z pakietów NuGet nie są już wykonywalne za pomocą platformy .NET Core 2.0 — [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe połyka szczegóły wyjątku podczas analizowania pliku rozwiązania - [#4411](https://github.com/NuGet/Home/issues/4411)

- Pack umieszcza pliki zawartości w niewłaściwej lokalizacji, jeśli ContentTargetFolders zawiera ścieżkę, która kończy się na "/" w systemie Windows - [#4407](https://github.com/NuGet/Home/issues/4407)

- Nie można przywrócić DotNetCliToolReference dla pakietu narzędzi, który jest przeznaczony netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)

- Nuget update CLI pozostawia stary warunek wersji pakietu w pliku projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DDR

- Przeczytaj dotnetCliToolTargetFramework z nomacji CPS - [#5397](https://github.com/NuGet/Home/issues/5397)

- Sprawdzenie TPMinV powinno działać dla pj stylu UWP - [#4763](https://github.com/NuGet/Home/issues/4763)

- Popraw opis interfejsu użytkownika dla pakietów AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet restore wybiera zasoby kompilacji z sekcji środowiska wykonawczego. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Umieść diagnostykę zależności w pliku blokady - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Poprawiono łącze do gitHub w 4.3 RTM

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
