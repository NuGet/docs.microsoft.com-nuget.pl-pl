---
title: Informacje o wersji 4.5 RTM NuGet
description: Informacje o wersji programu NuGet 4.5 RTM, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 01ecd8c7de1a0f713766e3c413d889038522bac7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548299"
---
# <a name="nuget-45-rtm-release-notes"></a>Informacje o wersji 4.5 RTM NuGet

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) dołączono [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET Standard 2.0 przy użyciu platformy .NET Framework i NuGet 

.NET standard i jego narzędzia zaprojektowano w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 może zużywać pakietów NuGet i projekty przeznaczone dla .NET Standard 2.0 lub wcześniejszej. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) znajduje się podsumowanie problemy dotyczące tego scenariusza, planowanie adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania

#### <a name="issue"></a>Problem

Od czasu do czasu, gdy używasz pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika "DateTime", powoduje automatyczne przywracanie pakietu do działania w pętli nieskończonej [dotnet/project-system #1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problemy rozwiązane w wersji RTM 4.5 NuGet przedział czasu

Problemy rozwiązane w wersji RTM w wersji 4.4 NuGet, można znaleźć na stronie [4.4 RTM informacjach o wersji NuGet](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Funkcje

- Wyłącz automatyczne synchronizowaniu pakiet symboli — [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Usterki

- [Regresja] w 15.5p1: pominięto Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)
- Brak zasobów z pakietów po Przywracanie — [#5995](https://github.com/NuGet/Home/issues/5995)
- Dostawcy poświadczeń wtyczki nie będą działać z identyfikatorów URI zawierające spacje - [#5982](https://github.com/NuGet/Home/issues/5982)
- Jeśli pakiet nie można przywrócić, błąd ma być drukowana w danych wyjściowych, nawet w przypadku ON minimalny poziom szczegółowości - [#5658](https://github.com/NuGet/Home/issues/5658)
- polecenia DotNet
  - dotnetcore przywracania na poziomie rozwiązania nie postępuj zgodnie z elementu ProjectReference z ReferenceOutputAssembly false wiodących kompilacji losowe awarie - [#5490](https://github.com/NuGet/Home/issues/5490)
- Automatyczne uzupełnianie w konsoli zarządzania Pakietami działa nieprawidłowo za pomocą metod obiektów - [#4800](https://github.com/NuGet/Home/issues/4800)
- Przywracanie nuget.exe nie powiedzie się z zestawem narzędzi Visual Studio 2015 — [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc jest kosztowne do utworzenia wystąpienia w programie vs2017 — [#4205](https://github.com/NuGet/Home/issues/4205)
- Powolne uzyskać informacje o zależnościach wolnego połączenia - [#4089](https://github.com/NuGet/Home/issues/4089)
- Odinstaluj w pakiecie z - RemoveDependencies zakończy się niepowodzeniem, jeśli wiele pakietów mają wspólne zależności — [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalizowanie NuGet.Core.nupkg publikowania - [#3581](https://github.com/NuGet/Home/issues/3581)
- Pakiet NuGet jest rozpoznawana jako identyfikator zależności na podstawie nazwy katalogu stosowania - IncludeProjectReferences csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- Inicjator typu "NuGet.ProxyCache" zgłosiła wyjątek - [#3144](https://github.com/NuGet/Home/issues/3144)
- problem z wydajnością przywracania nuget za pomocą aparatu kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- Interfejs użytkownika klienta nie powiedzie się wyświetlać jakiekolwiek błędy lub ostrzeżenia, gdy wyszukiwanie jest wcześniejsze rejestracji obiektami blob — [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-pakietów — aktualizacje generuje niepoprawny kwerendę - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Linki na problemy usługi GitHub, rozwiązane w wersji 4.5 RTM

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
