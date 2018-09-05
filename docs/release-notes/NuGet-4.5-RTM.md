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
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="54651-103">Informacje o wersji 4.5 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="54651-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="54651-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) dołączono [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="54651-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="54651-105">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="54651-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="54651-106">Problemy z platformą .NET Standard 2.0 przy użyciu platformy .NET Framework i NuGet</span><span class="sxs-lookup"><span data-stu-id="54651-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="54651-107">.NET standard i jego narzędzia zaprojektowano w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 może zużywać pakietów NuGet i projekty przeznaczone dla .NET Standard 2.0 lub wcześniejszej.</span><span class="sxs-lookup"><span data-stu-id="54651-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="54651-108">[W tym dokumencie](https://github.com/dotnet/standard/issues/481) znajduje się podsumowanie problemy dotyczące tego scenariusza, planowanie adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="54651-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="54651-109">Nie można wyświetlić, dodać ani zaktualizować składnika DotNetCLITools przy użyciu Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="54651-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="54651-110">Problem</span><span class="sxs-lookup"><span data-stu-id="54651-110">Issue</span></span>

<span data-ttu-id="54651-111">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="54651-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="54651-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="54651-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="54651-113">Obejście</span><span class="sxs-lookup"><span data-stu-id="54651-113">Workaround</span></span>

<span data-ttu-id="54651-114">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="54651-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="54651-115">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="54651-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="54651-116">Problem</span><span class="sxs-lookup"><span data-stu-id="54651-116">Issue</span></span>

<span data-ttu-id="54651-117">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54651-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="54651-118">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="54651-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="54651-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="54651-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="54651-120">Obejście</span><span class="sxs-lookup"><span data-stu-id="54651-120">Workaround</span></span>

<span data-ttu-id="54651-121">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="54651-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="54651-122">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="54651-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="54651-123">Problem</span><span class="sxs-lookup"><span data-stu-id="54651-123">Issue</span></span>

<span data-ttu-id="54651-124">Od czasu do czasu, gdy używasz pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika "DateTime", powoduje automatyczne przywracanie pakietu do działania w pętli nieskończonej [dotnet/project-system #1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="54651-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="54651-125">Obejście</span><span class="sxs-lookup"><span data-stu-id="54651-125">Workaround</span></span>

<span data-ttu-id="54651-126">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="54651-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="54651-127">Problemy rozwiązane w wersji RTM 4.5 NuGet przedział czasu</span><span class="sxs-lookup"><span data-stu-id="54651-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="54651-128">Problemy rozwiązane w wersji RTM w wersji 4.4 NuGet, można znaleźć na stronie [4.4 RTM informacjach o wersji NuGet](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="54651-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="54651-129">Funkcje</span><span class="sxs-lookup"><span data-stu-id="54651-129">Features</span></span>

- <span data-ttu-id="54651-130">Wyłącz automatyczne synchronizowaniu pakiet symboli — [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="54651-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="54651-131">Usterki</span><span class="sxs-lookup"><span data-stu-id="54651-131">Bugs</span></span>

- <span data-ttu-id="54651-132">[Regresja] w 15.5p1: pominięto Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="54651-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="54651-133">Brak zasobów z pakietów po Przywracanie — [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="54651-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="54651-134">Dostawcy poświadczeń wtyczki nie będą działać z identyfikatorów URI zawierające spacje - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="54651-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="54651-135">Jeśli pakiet nie można przywrócić, błąd ma być drukowana w danych wyjściowych, nawet w przypadku ON minimalny poziom szczegółowości - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="54651-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="54651-136">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="54651-136">dotnet</span></span>
  - <span data-ttu-id="54651-137">dotnetcore przywracania na poziomie rozwiązania nie postępuj zgodnie z elementu ProjectReference z ReferenceOutputAssembly false wiodących kompilacji losowe awarie - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="54651-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="54651-138">Automatyczne uzupełnianie w konsoli zarządzania Pakietami działa nieprawidłowo za pomocą metod obiektów - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="54651-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="54651-139">Przywracanie nuget.exe nie powiedzie się z zestawem narzędzi Visual Studio 2015 — [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="54651-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="54651-140">perf - pmc jest kosztowne do utworzenia wystąpienia w programie vs2017 — [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="54651-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="54651-141">Powolne uzyskać informacje o zależnościach wolnego połączenia - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="54651-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="54651-142">Odinstaluj w pakiecie z - RemoveDependencies zakończy się niepowodzeniem, jeśli wiele pakietów mają wspólne zależności — [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="54651-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="54651-143">Finalizowanie NuGet.Core.nupkg publikowania - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="54651-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="54651-144">Pakiet NuGet jest rozpoznawana jako identyfikator zależności na podstawie nazwy katalogu stosowania - IncludeProjectReferences csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="54651-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="54651-145">Inicjator typu "NuGet.ProxyCache" zgłosiła wyjątek - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="54651-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="54651-146">problem z wydajnością przywracania nuget za pomocą aparatu kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="54651-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="54651-147">Interfejs użytkownika klienta nie powiedzie się wyświetlać jakiekolwiek błędy lub ostrzeżenia, gdy wyszukiwanie jest wcześniejsze rejestracji obiektami blob — [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="54651-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="54651-148">Get-pakietów — aktualizacje generuje niepoprawny kwerendę - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="54651-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="54651-149">Linki na problemy usługi GitHub, rozwiązane w wersji 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="54651-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="54651-150">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="54651-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
