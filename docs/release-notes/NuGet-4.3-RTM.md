---
title: Informacje o wersji narzędzia NuGet 4,3 RTM
description: Informacje o wersji dla programu NuGet 4,3 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e9b6d15584d875f59ed64fe662944db3e37aeabb
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780178"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="8dca2-103">Informacje o wersji narzędzia NuGet 4,3</span><span class="sxs-lookup"><span data-stu-id="8dca2-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="8dca2-104">[Program Visual Studio 2017 15,3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z pakietem NuGet 4,3 RTM, który dodaje obsługę nowych scenariuszy, takich jak .NET Standard 2.0/. NET Core 2,0, zawiera wiele poprawek dotyczących jakości i poprawia wydajność.</span><span class="sxs-lookup"><span data-stu-id="8dca2-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="8dca2-105">Ta wersja oferuje również kilka ulepszeń, takich jak obsługa 2.0.0 wersji semantycznej, integracja programu MSBuild z ostrzeżeniami i błędami NuGet oraz inne.</span><span class="sxs-lookup"><span data-stu-id="8dca2-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="8dca2-106">Podsumowanie: co nowego w programie 4.3.0</span><span class="sxs-lookup"><span data-stu-id="8dca2-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="8dca2-107">Podsumowanie: co nowego w 4.3.1</span><span class="sxs-lookup"><span data-stu-id="8dca2-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="8dca2-108">Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="8dca2-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="8dca2-109">Poprawka zabezpieczeń: pliki wewnątrz elementu NUPKGs mogą mieć ścieżkę względną powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="8dca2-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="8dca2-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="8dca2-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="8dca2-111">Przywracanie pakietów NuGet może w niektórych przypadkach traktować wyłączone źródła pakietów jako włączone</span><span class="sxs-lookup"><span data-stu-id="8dca2-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="8dca2-112">Problem</span><span class="sxs-lookup"><span data-stu-id="8dca2-112">Issue</span></span>

<span data-ttu-id="8dca2-113">Następujące techniki przywracania wiersza polecenia traktują wyłączone źródła pakietów jako włączone.</span><span class="sxs-lookup"><span data-stu-id="8dca2-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="8dca2-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="8dca2-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="8dca2-115">`dotnet restore` (z dotnet.exe, które są dostarczane z programem VS, lub z tym, który jest dostarczany z zestawem SDK 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="8dca2-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="8dca2-116">Obejście</span><span class="sxs-lookup"><span data-stu-id="8dca2-116">Workaround</span></span>

1. <span data-ttu-id="8dca2-117">Użyj programu Visual Studio (2017 15.3 lub nowszego) lub NuGet.exe (4.3.0 lub nowszego)</span><span class="sxs-lookup"><span data-stu-id="8dca2-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="8dca2-118">Usuń wyłączone źródła i dalej używaj programu msbuild lub programu dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="8dca2-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="8dca2-119">Na potrzeby rozwiązania możesz użyć polecenia „Clear” (Wyczyść) w pliku NuGet.config, a następnie zdefiniować źródła dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8dca2-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="8dca2-120">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="8dca2-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="8dca2-121">Problem</span><span class="sxs-lookup"><span data-stu-id="8dca2-121">Issue</span></span>

<span data-ttu-id="8dca2-122">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="8dca2-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="8dca2-123">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="8dca2-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="8dca2-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="8dca2-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="8dca2-125">Obejście</span><span class="sxs-lookup"><span data-stu-id="8dca2-125">Workaround</span></span>

<span data-ttu-id="8dca2-126">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8dca2-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="8dca2-127">Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.</span><span class="sxs-lookup"><span data-stu-id="8dca2-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="8dca2-128">Nie można wyświetlać, dodawać ani aktualizować składnika dotnetclitools przy użyciu Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="8dca2-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="8dca2-129">Problem</span><span class="sxs-lookup"><span data-stu-id="8dca2-129">Issue</span></span>

<span data-ttu-id="8dca2-130">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="8dca2-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="8dca2-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="8dca2-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="8dca2-132">Obejście</span><span class="sxs-lookup"><span data-stu-id="8dca2-132">Workaround</span></span>

<span data-ttu-id="8dca2-133">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8dca2-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="8dca2-134">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="8dca2-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="8dca2-135">Problem</span><span class="sxs-lookup"><span data-stu-id="8dca2-135">Issue</span></span>

<span data-ttu-id="8dca2-136">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8dca2-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="8dca2-137">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="8dca2-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="8dca2-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="8dca2-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="8dca2-139">Obejście</span><span class="sxs-lookup"><span data-stu-id="8dca2-139">Workaround</span></span>

<span data-ttu-id="8dca2-140">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8dca2-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="8dca2-141">Problemy rozwiązane w przedziale czasu NuGet 4,3 RTM</span><span class="sxs-lookup"><span data-stu-id="8dca2-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="8dca2-142">[Informacje o wersji programu nuget 4,0 RTM](../release-notes/nuget-4.0-RTM.md) — lista wszystkich problemów rozwiązanych w przypadku programu NuGet 4,0 RTM</span><span class="sxs-lookup"><span data-stu-id="8dca2-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="8dca2-143">Funkcje</span><span class="sxs-lookup"><span data-stu-id="8dca2-143">Features</span></span>

- <span data-ttu-id="8dca2-144">Poprawianie wydajności przywracania NuGet — implementowanie inteligentniejszej aktualizujący nie działa dla wiersza polecenia przywraca i [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="8dca2-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="8dca2-145">NET Core 2,0: interfejs wiersza polecenia VS/dotnet powinien zacząć korzystać z istniejących funkcji NuGet: foldery rezerwowe — [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="8dca2-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="8dca2-146">NET Core 2,0: zezwól użytkownikom na ignorowanie określonych ostrzeżeń przywracania (lub Podnieś do błędu) — [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="8dca2-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="8dca2-147">NET Core 2,0: zlokalizowane zestawy interfejsu wiersza polecenia — [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="8dca2-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="8dca2-148">NET Core 2,0: rejestruje wszystkie ostrzeżenia/błędy w pliku zasobów (w tym PackageTargetFallback) — [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="8dca2-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="8dca2-149">Włącz obsługę TFM: Standard 2.0, Tizen- [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="8dca2-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="8dca2-150">Zmniejsz liczbę pakietów NuGet. Core i NuGet. Projects (i bibliotek DLL) — [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="8dca2-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="8dca2-151">Dodawanie możliwości oznaczania ostrzeżeń NuGet jako błędów — [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="8dca2-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="8dca2-152">Usterki</span><span class="sxs-lookup"><span data-stu-id="8dca2-152">Bugs</span></span>

- <span data-ttu-id="8dca2-153">MSBuild/t: pakiet kończy się niepowodzeniem z parametrem "DevelopmentDependency" nie jest obsługiwany przez zadanie "PackTask" — [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="8dca2-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="8dca2-154">Struktura katalogów dla plików zawartości spłaszczonych bez dodawania separatora katalogów systemu Windows na końcu PackagePath- [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="8dca2-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="8dca2-155">projekty podstawowe nie obsługują ustawienia jako developmentDependency- [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="8dca2-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="8dca2-156">RestoreManagerPackage jest ładowany synchronicznie, który zablokowany wątek interfejsu użytkownika i zakleszczenie w programie VS- [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="8dca2-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="8dca2-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="8dca2-157">dotnet</span></span>
  - <span data-ttu-id="8dca2-158">dotnetcore Restore (& w związku z tym MSBuild/t: Restore) pomija projekty z jawną zależnością projektu rozwiązania [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="8dca2-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="8dca2-159">Jeśli rozwiązanie ma zawierających, które odwołuje się do tego samego projektu z inną wielkością liter, przywracanie może nie zadziałało.</span><span class="sxs-lookup"><span data-stu-id="8dca2-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="8dca2-160">Dotyczy to również różnych ścieżek względnych bez różnic w wielkości liter — [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="8dca2-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="8dca2-161">Pliki wykonywalne przywrócone z pakietów NuGet nie są już wykonywalne przy użyciu programu .NET Core 2,0- [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="8dca2-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="8dca2-162">NuGet.exee szczegóły wyjątku podczas analizowania pliku rozwiązania — [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="8dca2-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="8dca2-163">Pakiet umieszcza pliki zawartości w niewłaściwej lokalizacji, jeśli ContentTargetFolders zawiera ścieżkę kończącą się znakiem "/" w systemie Windows- [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="8dca2-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="8dca2-164">Nie można przywrócić elementu DotNetCliToolReference dla pakietu narzędzi, który jest przeznaczony dla netcoreapp 1.1- [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="8dca2-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="8dca2-165">Interfejs wiersza polecenia aktualizacji NuGet pozostawia stary stan wersji pakietu w pliku projektu (C++) — [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="8dca2-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="8dca2-166">DCR</span><span class="sxs-lookup"><span data-stu-id="8dca2-166">DCRs</span></span>

- <span data-ttu-id="8dca2-167">Odczytaj DotnetCliToolTargetFramework z CPS nomation- [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="8dca2-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="8dca2-168">Sprawdzenie TPMinV powinno być wykonane dla PJ style platformy UWP- [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="8dca2-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="8dca2-169">Popraw opis interfejsu użytkownika dla pakietów z obsługą autoreferencji — [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="8dca2-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="8dca2-170">Przywrócenie NuGet polega na wybraniu opcji Kompiluj elementy zawartości z środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="8dca2-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="8dca2-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="8dca2-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="8dca2-172">Umieść diagnostykę zależności w pliku blokady — [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="8dca2-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="8dca2-173">Linki do problemów z usługą GitHub rozwiązane w 4,3 RTM</span><span class="sxs-lookup"><span data-stu-id="8dca2-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="8dca2-174">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="8dca2-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
