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
# <a name="nuget-43-release-notes"></a><span data-ttu-id="2e802-103">Informacje o wersji nuget 4.3</span><span class="sxs-lookup"><span data-stu-id="2e802-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="2e802-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest wyposażony w NuGet 4.3 RTM, który dodaje obsługę nowych scenariuszy, takich jak .NET Standard 2.0/.NET Core 2.0, zawiera wiele poprawek jakości i zwiększa wydajność.</span><span class="sxs-lookup"><span data-stu-id="2e802-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="2e802-105">Ta wersja zawiera również kilka ulepszeń, takich jak obsługa semantycznego przechowywania wersji 2.0.0, integracja MSBuild z ostrzeżeniami i błędami NuGet i inne.</span><span class="sxs-lookup"><span data-stu-id="2e802-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="2e802-106">Krótki opis: Co nowego w 4.3.0</span><span class="sxs-lookup"><span data-stu-id="2e802-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="2e802-107">Krótki opis: Co nowego w 4.3.1</span><span class="sxs-lookup"><span data-stu-id="2e802-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="2e802-108">Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="2e802-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="2e802-109">Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="2e802-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="2e802-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="2e802-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="2e802-111">Przywracanie pakietów NuGet może w niektórych przypadkach traktować wyłączone źródła pakietów jako włączone</span><span class="sxs-lookup"><span data-stu-id="2e802-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="2e802-112">Problem</span><span class="sxs-lookup"><span data-stu-id="2e802-112">Issue</span></span>

<span data-ttu-id="2e802-113">Następujące techniki wiersza polecenia przywracania traktują wyłączone źródła pakietów jako włączone.</span><span class="sxs-lookup"><span data-stu-id="2e802-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="2e802-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="2e802-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="2e802-115">`dotnet restore`(albo z dotnet.exe, który jest dostarczany z VS, lub ten, który jest dostarczany z NetCore SDK 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="2e802-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="2e802-116">Obejście</span><span class="sxs-lookup"><span data-stu-id="2e802-116">Workaround</span></span>

1. <span data-ttu-id="2e802-117">Użyj programu Visual Studio (2017 15.3 lub nowszego) lub NuGet.exe (4.3.0 lub nowszego)</span><span class="sxs-lookup"><span data-stu-id="2e802-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="2e802-118">Usuń wyłączone źródła i dalej używaj programu msbuild lub programu dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="2e802-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="2e802-119">Na potrzeby rozwiązania możesz użyć polecenia „Clear” (Wyczyść) w pliku NuGet.config, a następnie zdefiniować źródła dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2e802-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="2e802-120">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="2e802-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="2e802-121">Problem</span><span class="sxs-lookup"><span data-stu-id="2e802-121">Issue</span></span>

<span data-ttu-id="2e802-122">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2e802-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="2e802-123">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="2e802-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="2e802-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="2e802-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="2e802-125">Obejście</span><span class="sxs-lookup"><span data-stu-id="2e802-125">Workaround</span></span>

<span data-ttu-id="2e802-126">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2e802-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="2e802-127">Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.</span><span class="sxs-lookup"><span data-stu-id="2e802-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="2e802-128">Nie można wyświetlać, dodawać ani aktualizować dotNetCLITools przy użyciu Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="2e802-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="2e802-129">Problem</span><span class="sxs-lookup"><span data-stu-id="2e802-129">Issue</span></span>

<span data-ttu-id="2e802-130">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="2e802-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="2e802-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="2e802-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="2e802-132">Obejście</span><span class="sxs-lookup"><span data-stu-id="2e802-132">Workaround</span></span>

<span data-ttu-id="2e802-133">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="2e802-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="2e802-134">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="2e802-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="2e802-135">Problem</span><span class="sxs-lookup"><span data-stu-id="2e802-135">Issue</span></span>

<span data-ttu-id="2e802-136">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e802-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="2e802-137">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2e802-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="2e802-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="2e802-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="2e802-139">Obejście</span><span class="sxs-lookup"><span data-stu-id="2e802-139">Workaround</span></span>

<span data-ttu-id="2e802-140">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="2e802-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="2e802-141">Naprawiono problemy w ramach czasowych NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="2e802-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="2e802-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Wyświetla listę wszystkich problemów rozwiązanych dla NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="2e802-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="2e802-143">Funkcje</span><span class="sxs-lookup"><span data-stu-id="2e802-143">Features</span></span>

- <span data-ttu-id="2e802-144">Usprawnij narzędzie Przywracanie NuGet — implementuj inteligentniejsze noop dla przywracania wiersza polecenia i VS — [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="2e802-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="2e802-145">NET Core 2.0: VS/Dotnet CLI powinien rozpocząć korzystanie z istniejących funkcji NuGet: foldery FallBack - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="2e802-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="2e802-146">NET Core 2.0: Włącz użytkownikom ignorowanie określonych ostrzeżeń przywracania (lub podniesienie poziomu błędu) — [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="2e802-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="2e802-147">NET Core 2.0: Zlokalizowane przez CLI zespoły - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="2e802-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="2e802-148">NET Core 2.0: zarejestruj wszystkie ostrzeżenia/błędy w pliku zasobów (w tym PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="2e802-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="2e802-149">Włącz obsługę TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="2e802-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="2e802-150">Zmniejsz liczbę projektów NuGet.Core i NuGet.Client (a tym samym bibliotek dll) — [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="2e802-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="2e802-151">Dodaj możliwość oznaczania ostrzeżeń nuget jako błędów - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="2e802-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="2e802-152">Usterki</span><span class="sxs-lookup"><span data-stu-id="2e802-152">Bugs</span></span>

- <span data-ttu-id="2e802-153">msbuild /t:pack kończy się niepowodzeniem z parametrem "DevelopmentDependency" nie jest obsługiwany przez zadanie "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="2e802-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="2e802-154">Struktura katalogów dla plików zawartości spłaszczona, jeśli nie dodaje separatora katalogu systemu Windows na końcu Programu PackagePath — [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="2e802-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="2e802-155">projekty netcore nie obsługują ustawiania jako rozwojuZależność - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="2e802-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="2e802-156">RestoreManagerPackage jest ładowany synchronicznie, który zablokował wątek interfejsu użytkownika i zakleszczony VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="2e802-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="2e802-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="2e802-157">dotnet</span></span>
  - <span data-ttu-id="2e802-158">dotnetcore Restore (& dlatego msbuild /t:restore) pomija projekty z jawną zależnością projektu rozwiązania [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="2e802-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="2e802-159">Jeśli rozwiązanie ma projectreferences, które odnoszą się do tego samego projektu, z różnych wielkości liter, przywracanie może nie działać.</span><span class="sxs-lookup"><span data-stu-id="2e802-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="2e802-160">Wpływa to również na różne ścieżki względne, bez różnicy w obudowy - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="2e802-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="2e802-161">Pliki wykonywalne przywrócone z pakietów NuGet nie są już wykonywalne za pomocą platformy .NET Core 2.0 — [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="2e802-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="2e802-162">NuGet.exe połyka szczegóły wyjątku podczas analizowania pliku rozwiązania - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="2e802-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="2e802-163">Pack umieszcza pliki zawartości w niewłaściwej lokalizacji, jeśli ContentTargetFolders zawiera ścieżkę, która kończy się na "/" w systemie Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="2e802-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="2e802-164">Nie można przywrócić DotNetCliToolReference dla pakietu narzędzi, który jest przeznaczony netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="2e802-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="2e802-165">Nuget update CLI pozostawia stary warunek wersji pakietu w pliku projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="2e802-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="2e802-166">DDR</span><span class="sxs-lookup"><span data-stu-id="2e802-166">DCRs</span></span>

- <span data-ttu-id="2e802-167">Przeczytaj dotnetCliToolTargetFramework z nomacji CPS - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="2e802-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="2e802-168">Sprawdzenie TPMinV powinno działać dla pj stylu UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="2e802-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="2e802-169">Popraw opis interfejsu użytkownika dla pakietów AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="2e802-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="2e802-170">NuGet restore wybiera zasoby kompilacji z sekcji środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="2e802-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="2e802-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="2e802-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="2e802-172">Umieść diagnostykę zależności w pliku blokady - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="2e802-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="2e802-173">Poprawiono łącze do gitHub w 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="2e802-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="2e802-174">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="2e802-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
