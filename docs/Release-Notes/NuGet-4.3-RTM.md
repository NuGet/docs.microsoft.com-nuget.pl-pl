---
title: Informacje o wersji RTM NuGet 4.3 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.3 NuGet."
keywords: NuGet 4.3 RTM informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: a2b61d854f4a5f1490832dab9a272c3a13b56adf
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="5ffff-104">Informacje o wersji 4.3 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="5ffff-104">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="5ffff-105">[Visual Studio 2017 15 ustęp 3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z RTM 4.3 NuGet, który dodaje obsługę nowych scenariuszy, takich jak .NET Standard 2.0/.NET Core 2.0, zawiera wiele poprawek jakości i zwiększa wydajność.</span><span class="sxs-lookup"><span data-stu-id="5ffff-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="5ffff-106">Tej wersji wprowadzono również kilka ulepszeń, takich jak obsługa Wersjonowania semantycznego 2.0.0, integracja MSBuild NuGet ostrzeżeń i błędów i więcej.</span><span class="sxs-lookup"><span data-stu-id="5ffff-106">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5ffff-107">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="5ffff-107">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="5ffff-108">Przywracanie pakietów NuGet może w niektórych przypadkach traktować wyłączone źródła pakietów jako włączone</span><span class="sxs-lookup"><span data-stu-id="5ffff-108">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="5ffff-109">Problem</span><span class="sxs-lookup"><span data-stu-id="5ffff-109">Issue</span></span>

<span data-ttu-id="5ffff-110">Następujące techniki wiersza polecenia przywracania traktować pakiety wyłączone źródła jako włączona.</span><span class="sxs-lookup"><span data-stu-id="5ffff-110">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="5ffff-111">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="5ffff-111">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="5ffff-112">`dotnet restore` (albo dotnet.exe dostarczaną z programem VS lub ten, który jest dostarczany z zestawem SDK NetCore 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="5ffff-112">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="5ffff-113">Obejście</span><span class="sxs-lookup"><span data-stu-id="5ffff-113">Workaround</span></span>

1. <span data-ttu-id="5ffff-114">Użyj programu Visual Studio (2017 15.3 lub nowszego) lub NuGet.exe (4.3.0 lub nowszego)</span><span class="sxs-lookup"><span data-stu-id="5ffff-114">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="5ffff-115">Usuń wyłączone źródła i dalej używaj programu msbuild lub programu dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="5ffff-115">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="5ffff-116">Na potrzeby rozwiązania możesz użyć polecenia „Clear” (Wyczyść) w pliku NuGet.config, a następnie zdefiniować źródła dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5ffff-116">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="5ffff-117">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="5ffff-117">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="5ffff-118">Problem</span><span class="sxs-lookup"><span data-stu-id="5ffff-118">Issue</span></span>

<span data-ttu-id="5ffff-119">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5ffff-119">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="5ffff-120">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="5ffff-120">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="5ffff-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="5ffff-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="5ffff-122">Obejście</span><span class="sxs-lookup"><span data-stu-id="5ffff-122">Workaround</span></span>

<span data-ttu-id="5ffff-123">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5ffff-123">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="5ffff-124">Alternatywnie, spróbuj usunąć `project.lock.json` i przywracanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="5ffff-124">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="5ffff-125">Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="5ffff-125">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="5ffff-126">Problem</span><span class="sxs-lookup"><span data-stu-id="5ffff-126">Issue</span></span>

<span data-ttu-id="5ffff-127">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="5ffff-127">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="5ffff-128">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="5ffff-128">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="5ffff-129">Obejście</span><span class="sxs-lookup"><span data-stu-id="5ffff-129">Workaround</span></span>

<span data-ttu-id="5ffff-130">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="5ffff-130">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="5ffff-131">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="5ffff-131">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="5ffff-132">Problem</span><span class="sxs-lookup"><span data-stu-id="5ffff-132">Issue</span></span>

<span data-ttu-id="5ffff-133">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ffff-133">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="5ffff-134">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5ffff-134">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="5ffff-135">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="5ffff-135">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="5ffff-136">Obejście</span><span class="sxs-lookup"><span data-stu-id="5ffff-136">Workaround</span></span>

<span data-ttu-id="5ffff-137">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5ffff-137">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="5ffff-138">Problemy, które usunięto w wersji RTM programu NuGet 4.3 przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="5ffff-138">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="5ffff-139">[NuGet 4.0 RTM informacje o wersji](../release-notes/nuget-4.0-RTM.md) -Wyświetla wszystkie problemy, które są rozwiązywane RTM 4.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="5ffff-139">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="5ffff-140">Funkcje</span><span class="sxs-lookup"><span data-stu-id="5ffff-140">Features</span></span>

- <span data-ttu-id="5ffff-141">Poprawa wydajności przywracania NuGet — wdrożenie operacja inteligentny dla wiersza polecenia przywracania - i VS [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="5ffff-141">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="5ffff-142">NET Core 2.0: Programu VS/Dotnet interfejsu wiersza polecenia należy rozpocząć korzystanie z istniejące funkcje NuGet: rezerwowy foldery - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="5ffff-142">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="5ffff-143">NET Core 2.0: Umożliwić użytkownikom Ignoruj ostrzeżenia dotyczące przywracania określonego (lub podniesienia uprawnień do błędu) - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="5ffff-143">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="5ffff-144">NET Core 2.0: CLI zlokalizowane zestawy - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="5ffff-144">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="5ffff-145">NET Core 2.0: Zarejestruj wszystkie błędy/ostrzeżenia do pliku zasobów (takich jak PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="5ffff-145">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="5ffff-146">Włącz obsługę TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="5ffff-146">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="5ffff-147">Zmniejsz liczbę NuGet.Core NuGet.Client projektów (i w związku z tym bibliotek DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="5ffff-147">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="5ffff-148">Dodaj możliwość oznaczyć nuget ostrzeżenia jako błędy — [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="5ffff-148">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="5ffff-149">Usterki</span><span class="sxs-lookup"><span data-stu-id="5ffff-149">Bugs</span></span>

- <span data-ttu-id="5ffff-150">MSBUILD /t:pack kończy się niepowodzeniem z parametrem "DevelopmentDependency" nie jest obsługiwany przez zadanie "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="5ffff-150">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="5ffff-151">Struktura katalogów plików zawartości spłaszczone jeśli separatora katalogu systemu Windows nie jest dodawany na końcu PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="5ffff-151">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="5ffff-152">projekty netcore nie obsługuje ustawiania jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="5ffff-152">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="5ffff-153">RestoreManagerPackage ładowany synchronicznie co zablokowane wątku interfejsu użytkownika i zakleszczone VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="5ffff-153">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="5ffff-154">DotNet przywracania (i w związku z tym msbuild /t:restore) pomija projektów z zależności projektu rozwiązania jawne [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="5ffff-154">dotnet Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="5ffff-155">Jeśli rozwiązania jest projectreferences, która odwołuje się do tego samego projektu o innej wielkości znaków, przywracania może nie działać.</span><span class="sxs-lookup"><span data-stu-id="5ffff-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="5ffff-156">Wpływa to również na różnych ścieżek względnych bez różnica wielkością liter - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="5ffff-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="5ffff-157">Pliki wykonywalne przywrócone z pakietów NuGet nie są już pliku wykonywalnego z .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="5ffff-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="5ffff-158">NuGet.exe swallows szczegóły wyjątek podczas analizowania pliku rozwiązania — [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="5ffff-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="5ffff-159">Pakiet umieszcza pliki zawartości w niewłaściwej lokalizacji, jeżeli ContentTargetFolders zawiera ścieżkę, która kończy się z '/' w systemie Windows — [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="5ffff-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="5ffff-160">Nie można przywrócić DotNetCliToolReference narzędzia pakietów w tym netcoreapp1.1 cele - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="5ffff-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="5ffff-161">Aktualizacja Nuget interfejsu wiersza polecenia pozostawia starego warunek wersji pakietu w pliku projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="5ffff-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="5ffff-162">Dcr</span><span class="sxs-lookup"><span data-stu-id="5ffff-162">DCRs</span></span>

- <span data-ttu-id="5ffff-163">DotnetCliToolTargetFramework odczytu z CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="5ffff-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="5ffff-164">Sprawdź TPMinV powinny działać uzyskać stylu platformy uniwersalnej systemu Windows - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="5ffff-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="5ffff-165">Poprawa opis interfejsu użytkownika dla pakietów AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="5ffff-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="5ffff-166">Przywracanie NuGet jest wybranie zasoby kompilacji z sekcji środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="5ffff-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="5ffff-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="5ffff-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="5ffff-168">Diagnostyka zależności należy umieścić w pliku blokady - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="5ffff-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="5ffff-169">Łącza do usunięto w wersji 4.3 RTM zagadnienia GitHub</span><span class="sxs-lookup"><span data-stu-id="5ffff-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="5ffff-170">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="5ffff-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
