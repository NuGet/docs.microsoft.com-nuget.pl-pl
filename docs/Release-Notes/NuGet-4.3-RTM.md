---
title: Informacje o wersji 4.3 RTM NuGet
description: Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.3 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cb44f47ef0b3bd086f0a681cb2fedc7c5afc42fa
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-43-rtm-release-notes"></a>Informacje o wersji 4.3 RTM NuGet

[Visual Studio 2017 15 ustęp 3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z RTM 4.3 NuGet, który dodaje obsługę nowych scenariuszy, takich jak .NET Standard 2.0/.NET Core 2.0, zawiera wiele poprawek jakości i zwiększa wydajność. Tej wersji wprowadzono również kilka ulepszeń, takich jak obsługa Wersjonowania semantycznego 2.0.0, integracja MSBuild NuGet ostrzeżeń i błędów i więcej.

## <a name="known-issues"></a>Znane problemy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Przywracanie pakietów NuGet może w niektórych przypadkach traktować wyłączone źródła pakietów jako włączone

#### <a name="issue"></a>Problem

Następujące techniki wiersza polecenia przywracania traktować pakiety wyłączone źródła jako włączona. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (albo dotnet.exe dostarczaną z programem VS lub ten, który jest dostarczany z zestawem SDK NetCore 2.0.0)

#### <a name="workaround"></a>Obejście

1. Użyj programu Visual Studio (2017 15.3 lub nowszego) lub NuGet.exe (4.3.0 lub nowszego)
1. Usuń wyłączone źródła i dalej używaj programu msbuild lub programu dotnet.exe.
1. Na potrzeby rozwiązania możesz użyć polecenia „Clear” (Wyczyść) w pliku NuGet.config, a następnie zdefiniować źródła dla tego rozwiązania.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie, spróbuj usunąć `project.lock.json` i przywracanie ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget

#### <a name="issue"></a>Problem

Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Obejście

Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense

#### <a name="issue"></a>Problem

Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio. Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Obejście

Wykonaj przywracanie ręczne.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problemy, które usunięto w wersji RTM programu NuGet 4.3 przedziale czasu

[NuGet 4.0 RTM informacje o wersji](../release-notes/nuget-4.0-RTM.md) -Wyświetla wszystkie problemy, które są rozwiązywane RTM 4.0 NuGet

### <a name="features"></a>Funkcje

- Poprawa wydajności przywracania NuGet — wdrożenie operacja inteligentny dla wiersza polecenia przywracania - i VS [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: Programu VS/Dotnet interfejsu wiersza polecenia należy rozpocząć korzystanie z istniejące funkcje NuGet: rezerwowy foldery - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: Umożliwić użytkownikom Ignoruj ostrzeżenia dotyczące przywracania określonego (lub podniesienia uprawnień do błędu) - [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: CLI zlokalizowane zestawy - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: Zarejestruj wszystkie błędy/ostrzeżenia do pliku zasobów (takich jak PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Włącz obsługę TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Zmniejsz liczbę NuGet.Core NuGet.Client projektów (i w związku z tym bibliotek DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)

- Dodaj możliwość oznaczyć nuget ostrzeżenia jako błędy — [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Usterki

- MSBUILD /t:pack kończy się niepowodzeniem z parametrem "DevelopmentDependency" nie jest obsługiwany przez zadanie "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)

- Struktura katalogów plików zawartości spłaszczone jeśli separatora katalogu systemu Windows nie jest dodawany na końcu PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)

- projekty netcore nie obsługuje ustawiania jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage ładowany synchronicznie co zablokowane wątku interfejsu użytkownika i zakleszczone VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- DotNet
  - dotnetcore przywracania (i w związku z tym msbuild /t:restore) pomija projektów z zależności projektu rozwiązania jawne [#4578](https://github.com/NuGet/Home/issues/4578)

- Jeśli rozwiązania jest projectreferences, która odwołuje się do tego samego projektu o innej wielkości znaków, przywracania może nie działać. Wpływa to również na różnych ścieżek względnych bez różnica wielkością liter - [#4574](https://github.com/NuGet/Home/issues/4574)

- Pliki wykonywalne przywrócone z pakietów NuGet nie są już pliku wykonywalnego z .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe swallows szczegóły wyjątek podczas analizowania pliku rozwiązania — [#4411](https://github.com/NuGet/Home/issues/4411)

- Pakiet umieszcza pliki zawartości w niewłaściwej lokalizacji, jeżeli ContentTargetFolders zawiera ścieżkę, która kończy się z '/' w systemie Windows — [#4407](https://github.com/NuGet/Home/issues/4407)

- Nie można przywrócić DotNetCliToolReference narzędzia pakietów w tym netcoreapp1.1 cele - [#4396](https://github.com/NuGet/Home/issues/4396)

- Aktualizacja Nuget interfejsu wiersza polecenia pozostawia starego warunek wersji pakietu w pliku projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>Dcr

- DotnetCliToolTargetFramework odczytu z CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)

- Sprawdź TPMinV powinny działać uzyskać stylu platformy uniwersalnej systemu Windows - [#4763](https://github.com/NuGet/Home/issues/4763)

- Poprawa opis interfejsu użytkownika dla pakietów AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- Przywracanie NuGet jest wybranie zasoby kompilacji z sekcji środowiska wykonawczego. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Diagnostyka zależności należy umieścić w pliku blokady - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Łącza do usunięto w wersji 4.3 RTM zagadnienia GitHub

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
