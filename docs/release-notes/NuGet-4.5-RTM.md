---
title: Informacje o wydaniu nuGet 4.5 RTM
description: Informacje o wersji dla NuGet 4.5 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496579"
---
# <a name="nuget-45-release-notes"></a>Informacje o wersji NuGet 4.5

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="summary-whats-new-in-450"></a>Krótki opis: Co nowego w 4.5.0

## <a name="summary-whats-new-in-452"></a>Krótki opis: Co nowego w 4.5.2

* Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-453"></a>Krótki opis: Co nowego w 4.5.3

* Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z .NET Standard 2.0 z .NET Framework & NuGet 

.NET Standard & jego narzędzia został zaprojektowany w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla .NET Standard 2.0 lub wcześniejszych. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) podsumowano problemy związane z tym scenariuszem, plan ich rozwiązania i obejścia, które można wdrożyć przy dzisiejszym stanie narzędzia.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania

#### <a name="issue"></a>Problem

Od czasu do czasu, gdy używasz pakietu, który zawiera zestaw z nieprawidłowym podpisem lub gdy wersja pakietu jest ustawiona za pomocą znacznika "DateTime", powoduje to automatyczne przywracanie pakietu do uruchomienia w nieskończonej pętli [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Naprawiono problemy w ramach czasowych NuGet 4.5 RTM

W przypadku problemów rozwiązanych w NuGet 4.4 RTM, zapoznaj się [z NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Funkcje

- Wyłącz automatyczne wypychanie pakietu symboli - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Usterki

- [Regresja] w 15.5p1: Portable0.0 jest pomijany - [#6105](https://github.com/NuGet/Home/issues/6105)
- Zasoby z pakietów brakuje po przywróceniu - [#5995](https://github.com/NuGet/Home/issues/5995)
- Dostawcy poświadczeń wtyczek nie działają z identyfikatorami URI zawierającymi spacje - [#5982](https://github.com/NuGet/Home/issues/5982)
- Jeśli nie udało się przywrócić pakietu, błąd powinien być wydrukowany na wyjściu, nawet przy minimalnej szczegółowości on - [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - przywracanie dotnetcore na poziomie rozwiązania nie jest zgodne z ProjectReference z ReferenceOutputAssembly false prowadzi do losowych błędów kompilacji - [#5490](https://github.com/NuGet/Home/issues/5490)
- Auto-complete w PMC działa niepoprawnie z metodami obiektów - [#4800](https://github.com/NuGet/Home/issues/4800)
- przywracanie nuget.exe kończy się niepowodzeniem z zestawem narzędzi programu Visual Studio 2015 — [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc jest kosztowne do wystąpienia w vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)
- Powolne, aby uzyskać informacje o zależności na wolnym połączeniu - [#4089](https://github.com/NuGet/Home/issues/4089)
- uninstall-package w/ -RemoveDependencies zakończy się niepowodzeniem, jeśli wiele pakietów ma wspólną zależność - [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalizuj NuGet.Core.nupkg do publikowania - [#3581](https://github.com/NuGet/Home/issues/3581)
- NuGet pack rozpoznaje identyfikator zależności z nazwy katalogu, gdy -IncludeProjectReferences jest używany dla csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- Inicjator typu dla "NuGet.ProxyCache" zgłosił wyjątek - [#3144](https://github.com/NuGet/Home/issues/3144)
- nuget przywrócić problem z wydajnością kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- Klient interfejsu użytkownika nie pokazuje żadnego błędu lub ostrzeżenia, gdy wyszukiwanie jest przed identyfikatorami blob rejestracji - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages -Aktualizacje generuje niepoprawną kwerendę - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Poprawiono łącze do gitHub w 4.5 RTM

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
