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
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="b0625-104">Informacje o wersji 4.5 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="b0625-104">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="b0625-105">[Visual Studio 2017 15,5 cala RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="b0625-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b0625-106">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="b0625-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="b0625-107">Problemy z platformą .NET 2.0 standardowe z .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="b0625-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="b0625-108">.NET standard i jej narzędzi została zaprojektowana w taki sposób, że w projektach przeznaczonych dla platformy .NET Framework 4.6.1 może używać pakietów NuGet & projektach przeznaczonych dla platformy .NET Standard 2.0 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="b0625-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="b0625-109">[Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemy dotyczące tego scenariusza, plan adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="b0625-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="b0625-110">Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="b0625-110">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="b0625-111">Problem</span><span class="sxs-lookup"><span data-stu-id="b0625-111">Issue</span></span>

<span data-ttu-id="b0625-112">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="b0625-112">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="b0625-113">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="b0625-113">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="b0625-114">Obejście</span><span class="sxs-lookup"><span data-stu-id="b0625-114">Workaround</span></span>

<span data-ttu-id="b0625-115">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="b0625-115">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="b0625-116">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="b0625-116">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="b0625-117">Problem</span><span class="sxs-lookup"><span data-stu-id="b0625-117">Issue</span></span>

<span data-ttu-id="b0625-118">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0625-118">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="b0625-119">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="b0625-119">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="b0625-120">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="b0625-120">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="b0625-121">Obejście</span><span class="sxs-lookup"><span data-stu-id="b0625-121">Workaround</span></span>

<span data-ttu-id="b0625-122">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b0625-122">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="b0625-123">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="b0625-123">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="b0625-124">Problem</span><span class="sxs-lookup"><span data-stu-id="b0625-124">Issue</span></span>

<span data-ttu-id="b0625-125">Od czasu do czasu, gdy używasz pakietu, który zawiera zestaw z nieprawidłowym podpisem lub wersja pakietu jest ustawiona z typu "DateTime" znacznika powoduje Przywracanie automatycznego pakietu do uruchamiania w pętli nieskończonej [dotnet/project — system #1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="b0625-125">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="b0625-126">Obejście</span><span class="sxs-lookup"><span data-stu-id="b0625-126">Workaround</span></span>

<span data-ttu-id="b0625-127">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="b0625-127">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="b0625-128">Problemy, które usunięto w wersji RTM programu NuGet 4.5 przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="b0625-128">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="b0625-129">Problemy rozwiązane w wersji RTM 4.4 NuGet, można znaleźć na stronie [NuGet 4.4 RTM informacje o wersji](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="b0625-129">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="b0625-130">Funkcje</span><span class="sxs-lookup"><span data-stu-id="b0625-130">Features</span></span>

- <span data-ttu-id="b0625-131">Wyłącz automatyczne naciśnięcie pakietu symboli - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="b0625-131">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="b0625-132">Usterki</span><span class="sxs-lookup"><span data-stu-id="b0625-132">Bugs</span></span>

- <span data-ttu-id="b0625-133">[Regresja] w 15.5p1: pominięto Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="b0625-133">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="b0625-134">Po przywróceniu — Brak zasobów z pakietów [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="b0625-134">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="b0625-135">Dostawcy poświadczeń wtyczki nie współpracujesz z zawierających spacje identyfikatorów URI - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="b0625-135">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="b0625-136">Jeśli nie można przywrócić pakietu, powinien zostać wydrukowany błąd w danych wyjściowych, nawet w przypadku ON minimalny poziom szczegółowości - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="b0625-136">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="b0625-137">DotNet przywracania na poziomie rozwiązania nie wykonać ProjectReference z ReferenceOutputAssembly wiodące false, aby błędy kompilacji losowe — [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="b0625-137">dotnet restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="b0625-138">Funkcja automatycznego uzupełniania w PMC działa nieprawidłowo za pomocą metod obiektu - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="b0625-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="b0625-139">Przywracanie nuget.exe kończy się niepowodzeniem z zestawu narzędzi programu Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="b0625-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="b0625-140">wydajności - pmc jest kosztowna, można utworzyć wystąpienia w vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="b0625-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="b0625-141">Powolne można pobrać informacji o zależnościach na wolnego połączenia - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="b0625-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="b0625-142">Odinstaluj w pakiecie z - RemoveDependencies zakończy się niepowodzeniem, typowe zależności - udostępniania wielu pakietów [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="b0625-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="b0625-143">Finalizuj NuGet.Core.nupkg publikowania - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="b0625-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="b0625-144">Pakiet NuGet jest rozpoznawany jako identyfikator zależności od nazwy katalogu stosowania - IncludeProjectReferences csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="b0625-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="b0625-145">Inicjator typu dla "NuGet.ProxyCache" zgłosiła wyjątek - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="b0625-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="b0625-146">problem z wydajnością przywracania nuget z kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="b0625-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="b0625-147">Interfejs użytkownika klienta nie powiedzie się Pokaż jakiekolwiek błędy lub ostrzeżenia podczas wyszukiwania jest wcześniejsze rejestracji obiekty BLOB - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="b0625-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="b0625-148">Get-pakiety — aktualizacje generuje Niepoprawna kwerenda - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="b0625-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="b0625-149">Łącza do GitHub problemy rozwiązane w wersji 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="b0625-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="b0625-150">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="b0625-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
