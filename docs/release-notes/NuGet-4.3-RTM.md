---
title: Informacje o wersji 4.3 RTM NuGet
description: Informacje o wersji programu NuGet 4.3 RTM, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 4bee32995884f4c003ebb963d2fd5b2d04363bab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551627"
---
# <a name="nuget-43-rtm-release-notes"></a>Informacje o wersji 4.3 RTM NuGet

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) dołączono RTM 4.3 NuGet, który dodaje obsługę nowych scenariuszy, takich jak .NET Standard 2.0/.NET Core 2.0, zawiera wiele poprawki jakości i poprawia wydajność. Ta wersja oferuje również kilka udoskonaleń, takich jak obsługa Semantic Versioning 2.0.0, integrację MSBuild NuGet ostrzeżeń i błędów i innych.

## <a name="known-issues"></a>Znane problemy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Przywracanie pakietów NuGet może w niektórych przypadkach traktować wyłączone źródła pakietów jako włączone

#### <a name="issue"></a>Problem

Następujące techniki przywracania wiersza polecenia traktowały wyłączone źródła pakietów jako włączone. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (albo za pomocą dotnet.exe dostarczanego z programem VS lub ten, który jest dostarczany z zestawem SDK NetCore 2.0.0)

#### <a name="workaround"></a>Obejście

1. Użyj programu Visual Studio (2017 15.3 lub nowszego) lub NuGet.exe (4.3.0 lub nowszego)
1. Usuń wyłączone źródła i dalej używaj programu msbuild lub programu dotnet.exe.
1. Na potrzeby rozwiązania możesz użyć polecenia „Clear” (Wyczyść) w pliku NuGet.config, a następnie zdefiniować źródła dla tego rozwiązania.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”

#### <a name="issue"></a>Problem

Czasami klawisz Enter nie działa w konsoli Menedżera pakietów. Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Obejście

Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania. Alternatywnie, spróbuj usunąć `project.lock.json` i przywrócić go ponownie.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nie można wyświetlić, dodać ani zaktualizować składnika DotNetCLITools przy użyciu Menedżera pakietów Nuget

#### <a name="issue"></a>Problem

Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Obejście

Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense

#### <a name="issue"></a>Problem

Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio. Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Obejście

Wykonaj przywracanie ręczne.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problemy rozwiązane w wersji RTM 4.3 NuGet przedział czasu

[4.0 RTM informacjach o wersji NuGet](../release-notes/nuget-4.0-RTM.md) -Wyświetla wszystkie problemy rozwiązane programu NuGet 4.0 RTM

### <a name="features"></a>Funkcje

- Poprawa wydajności przywracania NuGet — Implementowanie inteligentniejsze aktualizujący nie działa dla wiersza polecenia przywraca — i VS [#5080](https://github.com/NuGet/Home/issues/5080)

- .NET Core 2.0: Programu VS/wiersz polecenia Dotnet powinien rozpocząć korzystanie z istniejących funkcji NuGet: rezerwowy foldery - [#4939](https://github.com/NuGet/Home/issues/4939)

- .NET Core 2.0: Umożliwianie użytkownikom Ignoruj ostrzeżenia o określonych przywracania (albo podnoszenie poziomu do błędów) - [#4898](https://github.com/NuGet/Home/issues/4898)

- .NET Core 2.0: Interfejs wiersza polecenia zlokalizowane zestawy — [#4896](https://github.com/NuGet/Home/issues/4896)

- .NET Core 2.0: Zarejestruj wszystkie ostrzeżenia/błędy do pliku zasobów (w tym PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Włącz obsługę TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Zmniejsz liczbę NuGet.Core NuGet.Client projektów (i tym samym biblioteki dll) - [#2446](https://github.com/NuGet/Home/issues/2446)

- Dodaj możliwości, aby oznaczyć nuget ostrzeżenia jako błędy — [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Usterki

- Program MSBuild /t:pack kończy się niepowodzeniem z parametrem "DevelopmentDependency" nie jest obsługiwany przez zadanie "PackTask" — [#5584](https://github.com/NuGet/Home/issues/5584)

- Spłaszczone struktury katalogów plików zawartości, jeśli nie zostaną dodane na końcu PackagePath - separatorem katalogu Windows [#4795](https://github.com/NuGet/Home/issues/4795)

- projekty netcore nie obsługuje ustawiania jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage ładowany synchronicznie który zablokowany wątek interfejsu użytkownika, a zakleszczone VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- polecenia DotNet
  - dotnetcore przywracania (i w związku z tym msbuild /t:restore) pomija projektów z zależnością projektu jawne rozwiązanie [#4578](https://github.com/NuGet/Home/issues/4578)

- Jeśli rozwiązanie ma odwołania do projektu, odwołując się do tego samego projektu z inną wielkością liter, Przywracanie może nie działać. Dotyczy to również różnych ścieżek względnych bez różnic w wielkości liter — [#4574](https://github.com/NuGet/Home/issues/4574)

- Pliki wykonywalne przywrócone z pakietów NuGet nie są już pliku wykonywalnego przy użyciu platformy .NET Core 2.0 — [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe obiekt szczegółów wyjątku podczas analizowania pliku rozwiązania — [#4411](https://github.com/NuGet/Home/issues/4411)

- Pakiet umieszcza pliki zawartości w niewłaściwej lokalizacji, jeśli ContentTargetFolders zawiera ścieżkę, która kończy się "/" na Windows - [#4407](https://github.com/NuGet/Home/issues/4407)

- Nie można przywrócić DotNetCliToolReference narzędzia pakietów w tym netcoreapp1.1 cele — [#4396](https://github.com/NuGet/Home/issues/4396)

- Nuget aktualizację interfejsu wiersza polecenia platformy pozostawi stary stan wersji pakietu w pliku projektu (C++) — [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCRs

- DotnetCliToolTargetFramework odczytu z CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)

- Sprawdzanie TPMinV powinny działać pj stylu platformy uniwersalnej systemu Windows — [#4763](https://github.com/NuGet/Home/issues/4763)

- Poprawa opisu interfejsu użytkownika dla pakietów AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- Przywracanie pakietów NuGet jest wybór zasobów kompilacji w sekcji środowiska uruchomieniowego. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Diagnostyka zależności należy umieścić w pliku blokady - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Linki do serwisu GitHub problemy rozwiązane w wersji 4.3 RTM

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
