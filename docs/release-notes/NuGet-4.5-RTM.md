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
# <a name="nuget-45-release-notes"></a><span data-ttu-id="facf1-103">Informacje o wersji NuGet 4.5</span><span class="sxs-lookup"><span data-stu-id="facf1-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="facf1-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="facf1-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="facf1-105">Krótki opis: Co nowego w 4.5.0</span><span class="sxs-lookup"><span data-stu-id="facf1-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="facf1-106">Krótki opis: Co nowego w 4.5.2</span><span class="sxs-lookup"><span data-stu-id="facf1-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="facf1-107">Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="facf1-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="facf1-108">Krótki opis: Co nowego w 4.5.3</span><span class="sxs-lookup"><span data-stu-id="facf1-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="facf1-109">Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="facf1-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="facf1-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="facf1-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="facf1-111">Problemy z .NET Standard 2.0 z .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="facf1-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="facf1-112">.NET Standard & jego narzędzia został zaprojektowany w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla .NET Standard 2.0 lub wcześniejszych.</span><span class="sxs-lookup"><span data-stu-id="facf1-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="facf1-113">[W tym dokumencie](https://github.com/dotnet/standard/issues/481) podsumowano problemy związane z tym scenariuszem, plan ich rozwiązania i obejścia, które można wdrożyć przy dzisiejszym stanie narzędzia.</span><span class="sxs-lookup"><span data-stu-id="facf1-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="facf1-114">Nie można wyświetlać, dodawać ani aktualizować dotNetCLITools przy użyciu Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="facf1-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="facf1-115">Problem</span><span class="sxs-lookup"><span data-stu-id="facf1-115">Issue</span></span>

<span data-ttu-id="facf1-116">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="facf1-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="facf1-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="facf1-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="facf1-118">Obejście</span><span class="sxs-lookup"><span data-stu-id="facf1-118">Workaround</span></span>

<span data-ttu-id="facf1-119">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="facf1-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="facf1-120">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="facf1-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="facf1-121">Problem</span><span class="sxs-lookup"><span data-stu-id="facf1-121">Issue</span></span>

<span data-ttu-id="facf1-122">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="facf1-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="facf1-123">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="facf1-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="facf1-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="facf1-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="facf1-125">Obejście</span><span class="sxs-lookup"><span data-stu-id="facf1-125">Workaround</span></span>

<span data-ttu-id="facf1-126">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="facf1-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="facf1-127">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="facf1-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="facf1-128">Problem</span><span class="sxs-lookup"><span data-stu-id="facf1-128">Issue</span></span>

<span data-ttu-id="facf1-129">Od czasu do czasu, gdy używasz pakietu, który zawiera zestaw z nieprawidłowym podpisem lub gdy wersja pakietu jest ustawiona za pomocą znacznika "DateTime", powoduje to automatyczne przywracanie pakietu do uruchomienia w nieskończonej pętli [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="facf1-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="facf1-130">Obejście</span><span class="sxs-lookup"><span data-stu-id="facf1-130">Workaround</span></span>

<span data-ttu-id="facf1-131">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="facf1-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="facf1-132">Naprawiono problemy w ramach czasowych NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="facf1-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="facf1-133">W przypadku problemów rozwiązanych w NuGet 4.4 RTM, zapoznaj się [z NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="facf1-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="facf1-134">Funkcje</span><span class="sxs-lookup"><span data-stu-id="facf1-134">Features</span></span>

- <span data-ttu-id="facf1-135">Wyłącz automatyczne wypychanie pakietu symboli - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="facf1-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="facf1-136">Usterki</span><span class="sxs-lookup"><span data-stu-id="facf1-136">Bugs</span></span>

- <span data-ttu-id="facf1-137">[Regresja] w 15.5p1: Portable0.0 jest pomijany - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="facf1-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="facf1-138">Zasoby z pakietów brakuje po przywróceniu - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="facf1-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="facf1-139">Dostawcy poświadczeń wtyczek nie działają z identyfikatorami URI zawierającymi spacje - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="facf1-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="facf1-140">Jeśli nie udało się przywrócić pakietu, błąd powinien być wydrukowany na wyjściu, nawet przy minimalnej szczegółowości on - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="facf1-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="facf1-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="facf1-141">dotnet</span></span>
  - <span data-ttu-id="facf1-142">przywracanie dotnetcore na poziomie rozwiązania nie jest zgodne z ProjectReference z ReferenceOutputAssembly false prowadzi do losowych błędów kompilacji - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="facf1-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="facf1-143">Auto-complete w PMC działa niepoprawnie z metodami obiektów - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="facf1-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="facf1-144">przywracanie nuget.exe kończy się niepowodzeniem z zestawem narzędzi programu Visual Studio 2015 — [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="facf1-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="facf1-145">perf - pmc jest kosztowne do wystąpienia w vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="facf1-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="facf1-146">Powolne, aby uzyskać informacje o zależności na wolnym połączeniu - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="facf1-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="facf1-147">uninstall-package w/ -RemoveDependencies zakończy się niepowodzeniem, jeśli wiele pakietów ma wspólną zależność - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="facf1-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="facf1-148">Finalizuj NuGet.Core.nupkg do publikowania - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="facf1-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="facf1-149">NuGet pack rozpoznaje identyfikator zależności z nazwy katalogu, gdy -IncludeProjectReferences jest używany dla csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="facf1-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="facf1-150">Inicjator typu dla "NuGet.ProxyCache" zgłosił wyjątek - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="facf1-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="facf1-151">nuget przywrócić problem z wydajnością kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="facf1-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="facf1-152">Klient interfejsu użytkownika nie pokazuje żadnego błędu lub ostrzeżenia, gdy wyszukiwanie jest przed identyfikatorami blob rejestracji - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="facf1-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="facf1-153">Get-Packages -Aktualizacje generuje niepoprawną kwerendę - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="facf1-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="facf1-154">Poprawiono łącze do gitHub w 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="facf1-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="facf1-155">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="facf1-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
