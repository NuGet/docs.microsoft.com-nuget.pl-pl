---
title: Informacje o wersji nuGet 4.4 RTM
description: Informacje o wersji dla NuGet 4.3 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498702"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="eacbb-103">Informacje o wersji nuget 4.4</span><span class="sxs-lookup"><span data-stu-id="eacbb-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="eacbb-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="eacbb-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="eacbb-105">Krótki opis: Co nowego w 4.4.0</span><span class="sxs-lookup"><span data-stu-id="eacbb-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="eacbb-106">Krótki opis: Co nowego w 4.4.2</span><span class="sxs-lookup"><span data-stu-id="eacbb-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="eacbb-107">Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="eacbb-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="eacbb-108">Krótki opis: Co nowego w 4.4.3</span><span class="sxs-lookup"><span data-stu-id="eacbb-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="eacbb-109">Poprawka zabezpieczeń: Pliki wewnątrz nupkgs może mieć względną ścieżkę powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="eacbb-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="eacbb-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="eacbb-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="eacbb-111">Problemy z .NET Standard 2.0 z .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="eacbb-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="eacbb-112">.NET Standard & jego narzędzia został zaprojektowany w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla .NET Standard 2.0 lub wcześniejszych.</span><span class="sxs-lookup"><span data-stu-id="eacbb-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="eacbb-113">[W tym dokumencie](https://github.com/dotnet/standard/issues/481) podsumowano problemy związane z tym scenariuszem, plan ich rozwiązania i obejścia, które można wdrożyć przy dzisiejszym stanie narzędzia.</span><span class="sxs-lookup"><span data-stu-id="eacbb-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="eacbb-114">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="eacbb-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="eacbb-115">Problem</span><span class="sxs-lookup"><span data-stu-id="eacbb-115">Issue</span></span>

<span data-ttu-id="eacbb-116">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="eacbb-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="eacbb-117">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="eacbb-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="eacbb-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="eacbb-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="eacbb-119">Obejście</span><span class="sxs-lookup"><span data-stu-id="eacbb-119">Workaround</span></span>

<span data-ttu-id="eacbb-120">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="eacbb-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="eacbb-121">Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.</span><span class="sxs-lookup"><span data-stu-id="eacbb-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="eacbb-122">Nie można wyświetlać, dodawać ani aktualizować dotNetCLITools przy użyciu Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="eacbb-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="eacbb-123">Problem</span><span class="sxs-lookup"><span data-stu-id="eacbb-123">Issue</span></span>

<span data-ttu-id="eacbb-124">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="eacbb-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="eacbb-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="eacbb-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="eacbb-126">Obejście</span><span class="sxs-lookup"><span data-stu-id="eacbb-126">Workaround</span></span>

<span data-ttu-id="eacbb-127">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="eacbb-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="eacbb-128">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="eacbb-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="eacbb-129">Problem</span><span class="sxs-lookup"><span data-stu-id="eacbb-129">Issue</span></span>

<span data-ttu-id="eacbb-130">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eacbb-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="eacbb-131">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="eacbb-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="eacbb-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="eacbb-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="eacbb-133">Obejście</span><span class="sxs-lookup"><span data-stu-id="eacbb-133">Workaround</span></span>

<span data-ttu-id="eacbb-134">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="eacbb-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="eacbb-135">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="eacbb-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="eacbb-136">Problem</span><span class="sxs-lookup"><span data-stu-id="eacbb-136">Issue</span></span>

<span data-ttu-id="eacbb-137">W przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie czasem uruchamiane w pętli nieskończonej (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="eacbb-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="eacbb-138">Obejście</span><span class="sxs-lookup"><span data-stu-id="eacbb-138">Workaround</span></span>

<span data-ttu-id="eacbb-139">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="eacbb-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="eacbb-140">Naprawiono problemy w ramach czasowych NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="eacbb-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="eacbb-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Wyświetla listę wszystkich problemów rozwiązanych dla NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="eacbb-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="eacbb-142">Funkcje</span><span class="sxs-lookup"><span data-stu-id="eacbb-142">Features</span></span>

- <span data-ttu-id="eacbb-143">Obsługa lekkiego ładowania rozwiązań w scenariuszach interfejsu użytkownika PM PM i NuGet - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="eacbb-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="eacbb-144">Obiekt docelowy pakietu msbuild powinien mieć publiczny hak do uruchamiania obiektów docelowych użytkownika przed sobą — [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="eacbb-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="eacbb-145">Funkcja: Dodaj przełącznik konwersjiVersion do instalacji nuget - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="eacbb-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="eacbb-146">uap10.0.TODO.0 powinien zostać zamapowana na .NET Standard 2.0 dla NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="eacbb-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="eacbb-147">Obsługa jednostki SKU narzędzi kompilacji programu Visual Studio za pomocą usługi msbuild /t:restore — [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="eacbb-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="eacbb-148">Podczas przywracania wygeneruj błąd, jeśli jest wymagana obsługa platformy .NET 4.6.1 dla platformy .NET Standard 2.0, ale nie zainstalowana — [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="eacbb-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="eacbb-149">Interfejs użytkownika klienta prefiksu identyfikatora pakietu — [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="eacbb-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="eacbb-150">dostarczać zlokalizowane składniki nuget do obsługi lokalizacji dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="eacbb-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="eacbb-151">Usterki</span><span class="sxs-lookup"><span data-stu-id="eacbb-151">Bugs</span></span>

- <span data-ttu-id="eacbb-152">Różne wielkości liter ścieżki projektu może spowodować przywrócenie do utraty PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="eacbb-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="eacbb-153">Przenieś kody błędów z numerami ostrzeżeń do zakresu błędów - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="eacbb-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="eacbb-154">Błąd wprowadzający w błąd, gdy nie wiadomo, że wersja .NET Standard jest zgodna z platformą docelową - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="eacbb-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="eacbb-155">Pliki testowe z mylącymi licencjami - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="eacbb-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="eacbb-156">Brak nagłówków licencji w szablonach testów EndToEnd — [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="eacbb-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="eacbb-157">packages.config restore pokazuje błędy jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="eacbb-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="eacbb-158">nuget.exe zainstalować powinien mieć DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="eacbb-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="eacbb-159">nuget.exe zainstalować niepoprawnie wyłącza buforowanie - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="eacbb-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="eacbb-160">Vs Uruchomienie polecenia przywracania dla packages.config po wyłączeniu przywracania wyświetla niepoprawny komunikat - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="eacbb-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="eacbb-161">VS; Uruchamianie polecenia przywracania po wyłączeniu przywracania wyświetla mylący komunikat - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="eacbb-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="eacbb-162">GetRestoreDotnetCliToolsTask nie powiedzie się, gdy brakuje metadanych wersji - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="eacbb-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="eacbb-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="eacbb-163">dotnet</span></span>
  - <span data-ttu-id="eacbb-164">dotnetcore dodać pakiet można wyczyścić puste linie z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="eacbb-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="eacbb-165">Nazwy źródeł ustawień poświadczeń w nuget.config są rozróżniane wielkość liter - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="eacbb-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="eacbb-166">Włączenie GeneratePackageOnBuild usunął całą moją historię pakietów - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="eacbb-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="eacbb-167">Przywracanie nie przywróci pakietów mono.cecil lub semver, ale wszystkie inne pakiety zostaną przywrócone.</span><span class="sxs-lookup"><span data-stu-id="eacbb-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="eacbb-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="eacbb-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="eacbb-169">Błędy i ostrzeżenia — zły błąd, gdy źródło jest niedostępne.</span><span class="sxs-lookup"><span data-stu-id="eacbb-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="eacbb-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="eacbb-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="eacbb-171">[DesignConsistency] Tekst stanu instalacji NuGet nie wygląda poprawnie w ciemnym motywie.</span><span class="sxs-lookup"><span data-stu-id="eacbb-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="eacbb-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="eacbb-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="eacbb-173">Aktualizuj pakiety w aktualizacjach/instalacjach rozwiązania dla wszystkich projektów - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="eacbb-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="eacbb-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="eacbb-174">dotnet</span></span>
  - <span data-ttu-id="eacbb-175">pakiet dotnetcore zachowuje się inaczej w zależności od TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="eacbb-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="eacbb-176">Dołączone biblioteki DLL wewnątrz folderu Tools rzucają ostrzeżenia - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="eacbb-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="eacbb-177">NuGet.ContentModel zużywa zbyt dużo pamięci dla operacji ciągu - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="eacbb-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="eacbb-178">RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="eacbb-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="eacbb-179">'dotnet pack' stawia nuspec pod obj zamiast obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="eacbb-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="eacbb-180">Nuget bardzo powolne uaktualnienie pakietu - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="eacbb-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="eacbb-181">CPS niezsynchronizowane z przywracanie z większych rozwiązań, które nie zostały włączone LSL (lekkie przywracanie rozwiązania) - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="eacbb-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="eacbb-182">SemVer 2.0 - nuget pack z dostarczoną wersją ignoruje metadane (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="eacbb-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="eacbb-183">Nuget.exe (3.+) zainstalować pakiet z numerem wersji i ExcludeVersion flagi nie aktualizuje pakietu do nowszej wersji - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="eacbb-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="eacbb-184">Przywracanie project.json powinien ostrzegać, gdy pakiety najwyższego poziomu naruszają ograniczenia - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="eacbb-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="eacbb-185">-ConfigFile nie ustawia niestandardowego configu na komendzie install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="eacbb-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="eacbb-186">nuget.exe install nie honoruje przełącznika '-DisableParallelProcessing' - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="eacbb-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="eacbb-187">Wyłączone źródła nadal używane przez DotNet.exe lub msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="eacbb-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="eacbb-188">Napraw zawiesza się w scenariuszu LSL - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="eacbb-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="eacbb-189">DDR</span><span class="sxs-lookup"><span data-stu-id="eacbb-189">DCRs</span></span>

- <span data-ttu-id="eacbb-190">nuget.exe zainstalować Obsługę TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="eacbb-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="eacbb-191">Dodaj różne parametry useragent zadania msbuild (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="eacbb-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="eacbb-192">PackagePathResolver.GetPackageDirectoryName powinien być wirtualny - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="eacbb-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="eacbb-193">[DesignConsistency] Mylący komunikat podczas dodawania pakietu NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="eacbb-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="eacbb-194">[Ostrzeżenia i błędy] NoWarn nie przepływa przechodnie przez odniesienia P2P - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="eacbb-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="eacbb-195">Lekkie obciążenie rozwiązania: Wspólny rdzeń dla pm ui, PMC i IV- - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="eacbb-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="eacbb-196">Lekkie obciążenie rozwiązania: Wsparcie - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="eacbb-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="eacbb-197">Dodaj obsługę wstępnie przywrócić obiekt docelowy MSBuild, który wyzwala program Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="eacbb-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="eacbb-198">Dodaj publiczny obiekt docelowy do obiektów docelowych NuGet.targets, do których można się odwoływać przy użyciu beforetargets — [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="eacbb-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="eacbb-199">Miejsce docelowe pakietu nie może poprawnie utworzyć contentFiles z akcjami kompilacji — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="eacbb-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="eacbb-200">RestoreOperationLogger.Do blokuje wątki puli gwintów - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="eacbb-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="eacbb-201">Docs</span><span class="sxs-lookup"><span data-stu-id="eacbb-201">Docs</span></span>

- <span data-ttu-id="eacbb-202">Flagi Docs for Install command DependencyVersion i Framework — [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="eacbb-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="eacbb-203">Aktualizacja do dokumentów na NuGet ostrzeżenia i błędy - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="eacbb-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="eacbb-204">Poprawiono łącze do gitHub w 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="eacbb-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="eacbb-205">Lista problemów 1</span><span class="sxs-lookup"><span data-stu-id="eacbb-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="eacbb-206">Lista problemów 2</span><span class="sxs-lookup"><span data-stu-id="eacbb-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="eacbb-207">Lista problemów 3</span><span class="sxs-lookup"><span data-stu-id="eacbb-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
