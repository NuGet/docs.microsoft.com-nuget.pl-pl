---
title: Informacje o wersji narzędzia NuGet 4,4 RTM
description: Informacje o wersji dla programu NuGet 4,3 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 970a920a401b8a74c04d84cbad9933c54e3cd19e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776287"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="880e6-103">Informacje o wersji narzędzia NuGet 4,4</span><span class="sxs-lookup"><span data-stu-id="880e6-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="880e6-104">[Program Visual Studio 2017 15,4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z pakietem NuGet 4,4 RTM.</span><span class="sxs-lookup"><span data-stu-id="880e6-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="880e6-105">Podsumowanie: co nowego w programie 4.4.0</span><span class="sxs-lookup"><span data-stu-id="880e6-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="880e6-106">Podsumowanie: co nowego w programie 4.4.2</span><span class="sxs-lookup"><span data-stu-id="880e6-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="880e6-107">Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="880e6-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="880e6-108">Podsumowanie: co nowego w programie 4.4.3 moc</span><span class="sxs-lookup"><span data-stu-id="880e6-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="880e6-109">Poprawka zabezpieczeń: pliki wewnątrz elementu NUPKGs mogą mieć ścieżkę względną powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="880e6-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="880e6-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="880e6-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="880e6-111">Problemy z .NET Standard 2,0 z pakietem NuGet .NET Framework &</span><span class="sxs-lookup"><span data-stu-id="880e6-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="880e6-112">.NET Standard & narzędzia zostały zaprojektowane tak, aby projekty ukierunkowane na .NET Framework 4.6.1 mogły korzystać z pakietów NuGet & projekty przeznaczone do .NET Standard 2,0 lub wcześniejszych.</span><span class="sxs-lookup"><span data-stu-id="880e6-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="880e6-113">[Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemów związanych z tym scenariuszem, planu ich rozwiązywania oraz obejścia, które można wdrożyć przy użyciu dzisiejszego stanu narzędzi.</span><span class="sxs-lookup"><span data-stu-id="880e6-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="880e6-114">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="880e6-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="880e6-115">Problem</span><span class="sxs-lookup"><span data-stu-id="880e6-115">Issue</span></span>

<span data-ttu-id="880e6-116">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="880e6-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="880e6-117">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="880e6-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="880e6-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="880e6-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="880e6-119">Obejście</span><span class="sxs-lookup"><span data-stu-id="880e6-119">Workaround</span></span>

<span data-ttu-id="880e6-120">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="880e6-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="880e6-121">Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.</span><span class="sxs-lookup"><span data-stu-id="880e6-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="880e6-122">Nie można wyświetlać, dodawać ani aktualizować składnika dotnetclitools przy użyciu Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="880e6-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="880e6-123">Problem</span><span class="sxs-lookup"><span data-stu-id="880e6-123">Issue</span></span>

<span data-ttu-id="880e6-124">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="880e6-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="880e6-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="880e6-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="880e6-126">Obejście</span><span class="sxs-lookup"><span data-stu-id="880e6-126">Workaround</span></span>

<span data-ttu-id="880e6-127">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="880e6-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="880e6-128">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="880e6-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="880e6-129">Problem</span><span class="sxs-lookup"><span data-stu-id="880e6-129">Issue</span></span>

<span data-ttu-id="880e6-130">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="880e6-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="880e6-131">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="880e6-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="880e6-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="880e6-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="880e6-133">Obejście</span><span class="sxs-lookup"><span data-stu-id="880e6-133">Workaround</span></span>

<span data-ttu-id="880e6-134">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="880e6-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="880e6-135">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="880e6-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="880e6-136">Problem</span><span class="sxs-lookup"><span data-stu-id="880e6-136">Issue</span></span>

<span data-ttu-id="880e6-137">W przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie czasem uruchamiane w pętli nieskończonej (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="880e6-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="880e6-138">Obejście</span><span class="sxs-lookup"><span data-stu-id="880e6-138">Workaround</span></span>

<span data-ttu-id="880e6-139">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="880e6-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="880e6-140">Problemy rozwiązane w przedziale czasu NuGet 4,4 RTM</span><span class="sxs-lookup"><span data-stu-id="880e6-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="880e6-141">[Informacje o wersji programu nuget 4,3 RTM](../release-notes/nuget-4.3-RTM.md) — lista wszystkich problemów rozwiązanych w przypadku programu NuGet 4,3 RTM</span><span class="sxs-lookup"><span data-stu-id="880e6-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="880e6-142">Funkcje</span><span class="sxs-lookup"><span data-stu-id="880e6-142">Features</span></span>

- <span data-ttu-id="880e6-143">Obsługa uproszczonego ładowania rozwiązań w scenariuszach interfejsu użytkownika w programie PMC i NuGet — [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="880e6-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="880e6-144">Element docelowy pakietu MSBuild powinien mieć publiczny punkt zaczepienia dla uruchomionych obiektów docelowych użytkownika przed jego użyciem [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="880e6-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="880e6-145">Funkcja: Add dependencyVersion Switch to the NuGet Install- [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="880e6-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="880e6-146">UAP 10.0. wyk. 0 powinien mapować do .NET Standard 2,0 dla NuGet — [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="880e6-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="880e6-147">Obsługa Visual Studio Build Tools SKU przy użyciu programu MSBuild/t: Restore- [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="880e6-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="880e6-148">Podczas przywracania Generuj błąd, jeśli program .NET 4.6.1 obsługuje .NET Standard 2,0 jest wymagany, ale nie został zainstalowany — [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="880e6-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="880e6-149">Prefiks identyfikatora pakietu dla interfejsu użytkownika klienta rezerwacji [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="880e6-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="880e6-150">Dostarcz zlokalizowane składniki NuGet do obsługi lokalizacji dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="880e6-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="880e6-151">Usterki</span><span class="sxs-lookup"><span data-stu-id="880e6-151">Bugs</span></span>

- <span data-ttu-id="880e6-152">Różne obudowy ścieżki projektu mogą spowodować utratę składnika packagereferences [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="880e6-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="880e6-153">Przenieś kody błędów z numerami ostrzegawczymi do zakresu błędu — [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="880e6-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="880e6-154">Błąd mylący, gdy wersja .NET Standard nie jest znana pod kątem zgodności z platformą docelową — [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="880e6-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="880e6-155">Pliki testowe z niemylącymi licencjami — [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="880e6-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="880e6-156">Brakujące nagłówki licencji w szablonach testów EndToEnd — [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="880e6-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="880e6-157">packages.config Restore wyświetla błędy jako NU1000- [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="880e6-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="880e6-158">Instalacja nuget.exe powinna mieć DisableParallelProcessing na mono- [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="880e6-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="880e6-159">nuget.exe instalacja niepoprawnie wyłącza buforowanie [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="880e6-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="880e6-160">A uruchomienie polecenia Restore dla packages.config, gdy polecenie Restore jest wyłączone wyświetla komunikat o niepoprawnym [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="880e6-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="880e6-161">LOKALNE Uruchomienie polecenia Restore, gdy przywracanie jest wyłączone, powoduje wyświetlenie komunikatu o pomyłki [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="880e6-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="880e6-162">GetRestoreDotnetCliToolsTask kończy się niepowodzeniem w przypadku braku metadanych wersji — [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="880e6-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="880e6-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="880e6-163">dotnet</span></span>
  - <span data-ttu-id="880e6-164">dotnetcore Dodawanie pakietu może czyścić puste wiersze z csproj- [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="880e6-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="880e6-165">Nazwy źródłowe ustawień poświadczeń w NuGet.Config uwzględnia wielkość liter — [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="880e6-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="880e6-166">Włączenie GeneratePackageOnBuild usuniętej całej historii pakietów — [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="880e6-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="880e6-167">Polecenie Restore nie spowoduje przywrócenia pakietów mono. Cecil lub semver, ale wszystkie pozostałe pakiety zostaną przywrócone.</span><span class="sxs-lookup"><span data-stu-id="880e6-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="880e6-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="880e6-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="880e6-169">Błędy i ostrzeżenia — zły błąd, jeśli źródło jest niedostępne.</span><span class="sxs-lookup"><span data-stu-id="880e6-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="880e6-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="880e6-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="880e6-171">[DesignConsistency] Tekst stanu instalacji pakietu NuGet nie jest obecnie prawidłowy dla ciemnego motywu.</span><span class="sxs-lookup"><span data-stu-id="880e6-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="880e6-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="880e6-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="880e6-173">Aktualizuj pakiety w ramach aktualizacji rozwiązania/instalacji dla wszystkich projektów — [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="880e6-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="880e6-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="880e6-174">dotnet</span></span>
  - <span data-ttu-id="880e6-175">Pakiet dotnetcore działa inaczej w zależności od TargetFramework vs TargetFrameworks- [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="880e6-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="880e6-176">Dołączone biblioteki DLL w folderze Tools throw Warnings- [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="880e6-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="880e6-177">NuGet. ContentModel zużywa zbyt dużo pamięci dla operacji na ciągach — [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="880e6-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="880e6-178">RuntimeEnvironmentHelper. islinux zwraca wartość true dla OSX- [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="880e6-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="880e6-179">element "dotnet Pack" umieszcza nuspec w obiekcie obj zamiast obj\Debug- [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="880e6-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="880e6-180">Uaktualnienie pakietu NuGet bardzo powolne — [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="880e6-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="880e6-181">Niezsynchronizowany serwer CPS z funkcją przywracania z większymi rozwiązaniami, które nie zostały włączone SKRÓCONO (uproszczone przywracanie rozwiązań) — [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="880e6-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="880e6-182">SemVer 2,0 — pakiet NuGet z podaną wersją ignoruje metadane (3.5.0-RTM-1938) — [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="880e6-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="880e6-183">Nuget.exe (3. +) pakiet instalacyjny z numerem wersji i flagą ExcludeVersion nie aktualizuje pakietu do nowszej wersji — [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="880e6-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="880e6-184">Project.jspodczas przywracania powinny ostrzegać, gdy pakiety najwyższego poziomu naruszają ograniczenia — [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="880e6-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="880e6-185">-ConfigFile nie ustawia niestandardowej konfiguracji przy instalacji polecenie- [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="880e6-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="880e6-186">nuget.exe instalacji nie honoruje przełącznika "-DisableParallelProcessing" — [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="880e6-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="880e6-187">Wyłączone źródła nadal używane przez DotNet.exe lub msbuild.exe [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="880e6-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="880e6-188">Rozwiązanie zawiesza się w scenariuszu SKRÓCONO — [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="880e6-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="880e6-189">DCR</span><span class="sxs-lookup"><span data-stu-id="880e6-189">DCRs</span></span>

- <span data-ttu-id="880e6-190">nuget.exe zainstalować obsługę TargetFramework — [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="880e6-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="880e6-191">Dodawanie różnych ciągów UserAgent zadań programu MSBuild (Visual Core vs Desktop MSBuild) — [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="880e6-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="880e6-192">PackagePathResolver. GetPackageDirectoryName powinna być wirtualna- [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="880e6-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="880e6-193">[DesignConsistency] Komunikat mylący podczas dodawania pakietu NuGet — [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="880e6-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="880e6-194">[Ostrzeżenia i błędy] Nowarn nie przepływ przechodnie za poorednictwem odwołań P2P- [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="880e6-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="880e6-195">Uproszczone ładowanie rozwiązań: wspólne rdzeń dla interfejsu użytkownika PM, PMC i użycie japońskich ideograficznych — [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="880e6-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="880e6-196">Uproszczone ładowanie rozwiązań: support-PMC- [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="880e6-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="880e6-197">Dodano obsługę przed przywróceniem elementu docelowego programu MSBuild, który jest wyzwalany przez program Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="880e6-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="880e6-198">Dodaj publiczny cel do NuGet. targets, do których można odwoływać się za pomocą BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="880e6-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="880e6-199">Obiekt docelowy Pack nie może utworzyć contentFiles z akcją kompilacji prawidłowo — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="880e6-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="880e6-200">Wątki puli wątków RestoreOperationLogger.Do Blocks — [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="880e6-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="880e6-201">Docs</span><span class="sxs-lookup"><span data-stu-id="880e6-201">Docs</span></span>

- <span data-ttu-id="880e6-202">Dokumentacja dla poleceń Install DependencyVersion i Frameworks- [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="880e6-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="880e6-203">Aktualizowanie do dokumentów na temat ostrzeżeń i błędów narzędzia NuGet — [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="880e6-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="880e6-204">Linki do problemów z usługą GitHub rozwiązane w 4,4 RTM</span><span class="sxs-lookup"><span data-stu-id="880e6-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="880e6-205">Lista problemów 1</span><span class="sxs-lookup"><span data-stu-id="880e6-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="880e6-206">Lista problemów 2</span><span class="sxs-lookup"><span data-stu-id="880e6-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="880e6-207">Lista problemów 3</span><span class="sxs-lookup"><span data-stu-id="880e6-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
