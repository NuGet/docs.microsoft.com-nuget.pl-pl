---
title: Informacje o wersji RTM NuGet 4.5 | Dokumentacja firmy Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.5 NuGet.
keywords: NuGet 4.5 RTM informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbde7256ed5526761107272792d7c7cdc324a3ef
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-45-rtm-release-notes"></a>Informacje o wersji 4.5 RTM NuGet

[Visual Studio 2017 15,5 cala RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET 2.0 standardowe z .NET Framework & NuGet 

.NET standard i jej narzędzi została zaprojektowana w taki sposób, że w projektach przeznaczonych dla platformy .NET Framework 4.6.1 może używać pakietów NuGet & projektach przeznaczonych dla platformy .NET Standard 2.0 lub starszym. [Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemy dotyczące tego scenariusza, plan adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania

#### <a name="issue"></a>Problem

Od czasu do czasu, gdy używasz pakietu, który zawiera zestaw z nieprawidłowym podpisem lub wersja pakietu jest ustawiona z typu "DateTime" znacznika powoduje Przywracanie automatycznego pakietu do uruchamiania w pętli nieskończonej [dotnet/project — system #1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Obejście

Obecnie nie istnieje obejście tego problemu.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problemy, które usunięto w wersji RTM programu NuGet 4.5 przedziale czasu

Problemy rozwiązane w wersji RTM 4.4 NuGet, można znaleźć na stronie [NuGet 4.4 RTM informacje o wersji](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Funkcje

- Wyłącz automatyczne naciśnięcie pakietu symboli - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Usterki

- [Regresja] w 15.5p1: pominięto Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)
- Po przywróceniu — Brak zasobów z pakietów [#5995](https://github.com/NuGet/Home/issues/5995)
- Dostawcy poświadczeń wtyczki nie współpracujesz z zawierających spacje identyfikatorów URI - [#5982](https://github.com/NuGet/Home/issues/5982)
- Jeśli nie można przywrócić pakietu, powinien zostać wydrukowany błąd w danych wyjściowych, nawet w przypadku ON minimalny poziom szczegółowości - [#5658](https://github.com/NuGet/Home/issues/5658)
- DotNet przywracania na poziomie rozwiązania nie wykonać ProjectReference z ReferenceOutputAssembly wiodące false, aby błędy kompilacji losowe — [#5490](https://github.com/NuGet/Home/issues/5490)
- Funkcja automatycznego uzupełniania w PMC działa nieprawidłowo za pomocą metod obiektu - [#4800](https://github.com/NuGet/Home/issues/4800)
- Przywracanie nuget.exe kończy się niepowodzeniem z zestawu narzędzi programu Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)
- wydajności - pmc jest kosztowna, można utworzyć wystąpienia w vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)
- Powolne można pobrać informacji o zależnościach na wolnego połączenia - [#4089](https://github.com/NuGet/Home/issues/4089)
- Odinstaluj w pakiecie z - RemoveDependencies zakończy się niepowodzeniem, typowe zależności - udostępniania wielu pakietów [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalizuj NuGet.Core.nupkg publikowania - [#3581](https://github.com/NuGet/Home/issues/3581)
- Pakiet NuGet jest rozpoznawany jako identyfikator zależności od nazwy katalogu stosowania - IncludeProjectReferences csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- Inicjator typu dla "NuGet.ProxyCache" zgłosiła wyjątek - [#3144](https://github.com/NuGet/Home/issues/3144)
- problem z wydajnością przywracania nuget z kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- Interfejs użytkownika klienta nie powiedzie się Pokaż jakiekolwiek błędy lub ostrzeżenia podczas wyszukiwania jest wcześniejsze rejestracji obiekty BLOB - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-pakiety — aktualizacje generuje Niepoprawna kwerenda - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Łącza do GitHub problemy rozwiązane w wersji 4.5 RTM

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
