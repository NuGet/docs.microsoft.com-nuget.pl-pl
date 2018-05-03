---
title: Informacje o wersji 4.4 RTM NuGet
description: Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.3 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="a19c7-103">Informacje o wersji 4.4 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="a19c7-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="a19c7-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="a19c7-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a19c7-105">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a19c7-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="a19c7-106">Problemy z platformą .NET 2.0 standardowe z .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="a19c7-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="a19c7-107">.NET standard i jej narzędzi została zaprojektowana w taki sposób, że w projektach przeznaczonych dla platformy .NET Framework 4.6.1 może używać pakietów NuGet & projektach przeznaczonych dla platformy .NET Standard 2.0 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="a19c7-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="a19c7-108">[Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemy dotyczące tego scenariusza, plan adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="a19c7-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="a19c7-109">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="a19c7-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="a19c7-110">Problem</span><span class="sxs-lookup"><span data-stu-id="a19c7-110">Issue</span></span>

<span data-ttu-id="a19c7-111">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a19c7-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="a19c7-112">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="a19c7-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="a19c7-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="a19c7-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="a19c7-114">Obejście</span><span class="sxs-lookup"><span data-stu-id="a19c7-114">Workaround</span></span>

<span data-ttu-id="a19c7-115">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a19c7-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="a19c7-116">Alternatywnie, spróbuj usunąć `project.lock.json` i przywracanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="a19c7-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="a19c7-117">Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="a19c7-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="a19c7-118">Problem</span><span class="sxs-lookup"><span data-stu-id="a19c7-118">Issue</span></span>

<span data-ttu-id="a19c7-119">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="a19c7-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="a19c7-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="a19c7-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="a19c7-121">Obejście</span><span class="sxs-lookup"><span data-stu-id="a19c7-121">Workaround</span></span>

<span data-ttu-id="a19c7-122">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="a19c7-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="a19c7-123">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="a19c7-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="a19c7-124">Problem</span><span class="sxs-lookup"><span data-stu-id="a19c7-124">Issue</span></span>

<span data-ttu-id="a19c7-125">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a19c7-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="a19c7-126">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a19c7-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="a19c7-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="a19c7-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="a19c7-128">Obejście</span><span class="sxs-lookup"><span data-stu-id="a19c7-128">Workaround</span></span>

<span data-ttu-id="a19c7-129">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="a19c7-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="a19c7-130">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="a19c7-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="a19c7-131">Problem</span><span class="sxs-lookup"><span data-stu-id="a19c7-131">Issue</span></span>

<span data-ttu-id="a19c7-132">Od czasu do czasu gdy używasz pakietu, który zawiera zestaw z nieprawidłowym podpisem lub wersja pakietu jest ustawiona z typu "DateTime" znacznika powoduje Przywracanie automatycznego pakietu do uruchamiania w nieskończonej pętli (dotnet/project — system #1457).</span><span class="sxs-lookup"><span data-stu-id="a19c7-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="a19c7-133">Obejście</span><span class="sxs-lookup"><span data-stu-id="a19c7-133">Workaround</span></span>

<span data-ttu-id="a19c7-134">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="a19c7-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="a19c7-135">Problemy, które usunięto w wersji RTM programu NuGet 4.4 przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="a19c7-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="a19c7-136">[NuGet 4.3 RTM informacje o wersji](../release-notes/nuget-4.3-RTM.md) -Wyświetla wszystkie problemy, które są rozwiązywane RTM 4.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="a19c7-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="a19c7-137">Funkcje</span><span class="sxs-lookup"><span data-stu-id="a19c7-137">Features</span></span>

- <span data-ttu-id="a19c7-138">Obsługa protokołu Lightweight ładowania rozwiązania w scenariuszach PMC i NuGet PM interfejsu użytkownika — [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="a19c7-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="a19c7-139">Element docelowy programu msbuild pakietu powinien mieć publicznego punktu zaczepienia dla uruchomionego celów użytkownika przed sam - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="a19c7-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="a19c7-140">Funkcja: Dodać przełącznik dependencyVersion nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="a19c7-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="a19c7-141">uap10.0.ToDo.0 powinny być mapowane na .NET 2.0 standardowy programu NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="a19c7-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="a19c7-142">Obsługuje SKU z narzędzia kompilacji programu Visual Studio z msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="a19c7-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="a19c7-143">Podczas przywracania, generuje błąd, jeśli .NET 4.6.1 Obsługa .NET 2.0 standardowe jest wymagana, ale nie jest zainstalowany - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="a19c7-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="a19c7-144">Interfejs użytkownika — klienta rezerwacji prefiks Identyfikatora pakietu [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="a19c7-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="a19c7-145">dostarczanie składników zlokalizowanych nuget w celu obsługi lokalizacja dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="a19c7-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="a19c7-146">Usterki</span><span class="sxs-lookup"><span data-stu-id="a19c7-146">Bugs</span></span>

- <span data-ttu-id="a19c7-147">Obudowy ścieżki inny projekt może spowodować utratę PackageReferences — po ukończeniu przywracania [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="a19c7-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="a19c7-148">Przenieś kodów błędów z numerów ostrzeżeń, które zakresowi błąd - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="a19c7-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="a19c7-149">Błąd błąd, gdy wersja platformy .NET Standard nie jest znany aby był zgodny z platformy docelowej - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="a19c7-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="a19c7-150">Testowanie plików z licencjami mylące - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="a19c7-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="a19c7-151">Brak nagłówków licencji w EndToEnd testowanie szablonów - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="a19c7-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="a19c7-152">Przywracanie pliku Packages.config pokazuje błędy jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="a19c7-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="a19c7-153">Zainstaluj nuget.exe powinny mieć DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="a19c7-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="a19c7-154">Zainstaluj nuget.exe niepoprawnie wyłącza buforowanie - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="a19c7-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="a19c7-155">VS polecenia przywracania dla pliku packages.config podczas przywracania jest wyłączona, zostanie wyświetlony komunikat niepoprawne - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="a19c7-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="a19c7-156">VS; Polecenia restore podczas przywracania jest wyłączona, zostanie wyświetlony komunikat mylące - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="a19c7-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="a19c7-157">GetRestoreDotnetCliToolsTask ulegnie awarii, gdy brak metadanych wersji - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="a19c7-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="a19c7-158">DotNet</span><span class="sxs-lookup"><span data-stu-id="a19c7-158">dotnet</span></span>
  - <span data-ttu-id="a19c7-159">Dodaj dotnetcore pakietu można wyczyścić puste wiersze z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="a19c7-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="a19c7-160">Nazwy źródeł ustawień poświadczeń w pliku NuGet.Config jest uwzględniana wielkość liter - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="a19c7-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="a19c7-161">Włączanie GeneratePackageOnBuild usunięte Moje całej historii pakiety - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="a19c7-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="a19c7-162">Przywracanie nie przywróci mono.cecil lub programu semver pakietów, ale inne pakiety pobrać przywrócony.</span><span class="sxs-lookup"><span data-stu-id="a19c7-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="a19c7-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="a19c7-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="a19c7-164">Błędy i ostrzeżenia - zły błąd podczas źródła niedostępne.</span><span class="sxs-lookup"><span data-stu-id="a19c7-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="a19c7-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="a19c7-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="a19c7-166">[DesignConsistency] Obecnie nie wygląda prawidłowe na ciemny motyw tekst stanu instalacji NuGet.</span><span class="sxs-lookup"><span data-stu-id="a19c7-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="a19c7-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="a19c7-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="a19c7-168">Aktualizowanie pakietów w aktualizacji rozwiązania/instaluje we wszystkich projektach — [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="a19c7-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="a19c7-169">DotNet</span><span class="sxs-lookup"><span data-stu-id="a19c7-169">dotnet</span></span>
  - <span data-ttu-id="a19c7-170">Pakiet dotnetcore zachowuje się inaczej w zależności od vs TargetFramework TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="a19c7-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="a19c7-171">Objąć biblioteki DLL narzędzia folderu throw ostrzeżenia - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="a19c7-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="a19c7-172">NuGet.ContentModel zużywa zbyt dużej ilości pamięci dla operacji na ciągach - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="a19c7-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="a19c7-173">RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla systemu OS x - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="a19c7-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="a19c7-174">"pakiet dotnet" umieszcza nuspec w obszarze obj zamiast obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="a19c7-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="a19c7-175">Nuget bardzo wolno uaktualniania pakietu - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="a19c7-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="a19c7-176">Zsynchronizowane procedury CPS przywracania większe rozwiązania, których nie włączono LSL (Przywracanie lekkie rozwiązanie) - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="a19c7-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="a19c7-177">Programu SemVer 2.0 — nuget pakietu z warunkiem wersja ignoruje metadanych (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="a19c7-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="a19c7-178">Nuget.exe (3 +) zainstaluj pakiet o numerze wersji i flagi ExcludeVersion nie powoduje aktualizacji pakietu do nowszej wersji — [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="a19c7-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="a19c7-179">Przywracanie Project.JSON powinien Ostrzegaj, gdy pakiety najwyższego poziomu narusza ograniczenia — [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="a19c7-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="a19c7-180">-ConfigFile nie jest ustawienie niestandardowej konfiguracji polecenia install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="a19c7-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="a19c7-181">Zainstaluj nuget.exe honoruje "-DisableParallelProcessing" przełącznika - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="a19c7-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="a19c7-182">Wyłączone źródeł nadal używane przez DotNet.exe lub msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="a19c7-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="a19c7-183">Usuń zawiesza się na scenariuszu LSL - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="a19c7-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="a19c7-184">Dcr</span><span class="sxs-lookup"><span data-stu-id="a19c7-184">DCRs</span></span>

- <span data-ttu-id="a19c7-185">nuget.exe Zainstaluj obsługę TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="a19c7-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="a19c7-186">Dodaj inny msbuild zadania agenta użytkownika ciągi (msbuild pulpitu netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="a19c7-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="a19c7-187">PackagePathResolver.GetPackageDirectoryName powinny być wirtualna - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="a19c7-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="a19c7-188">[DesignConsistency] Skomplikowana komunikat podczas dodawania pakietu NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="a19c7-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="a19c7-189">[Ostrzeżeń i błędów] NoWarn nie przechodnie przepływać przez odwołania P2P - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="a19c7-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="a19c7-190">Ładowania rozwiązania lekkie: Core wspólnego PM interfejsu użytkownika, PMC i wektory inicjacji-- [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="a19c7-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="a19c7-191">Obciążenia lekkie rozwiązanie: Obsługuje - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="a19c7-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="a19c7-192">Dodaj obsługę wstępnie przywrócić docelowy programu MSBuild, który wyzwala Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="a19c7-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="a19c7-193">Dodaj publiczny docelowych do NuGet.targets, który można odwoływać się przy użyciu BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="a19c7-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="a19c7-194">Docelowy pakiet nie można utworzyć pliki z akcjami kompilacji nieprawidłowo — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="a19c7-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="a19c7-195">RestoreOperationLogger.Do blokuje wątków z puli wątków - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="a19c7-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="a19c7-196">Docs</span><span class="sxs-lookup"><span data-stu-id="a19c7-196">Docs</span></span>

- <span data-ttu-id="a19c7-197">Dokumentacja instalacji poleceń flagi DependencyVersion i Framework — [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="a19c7-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="a19c7-198">Aktualizacja do dokumentów na NuGet ostrzeżeń i błędów - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="a19c7-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="a19c7-199">Łącza do usunięto w wersji 4.4 RTM zagadnienia GitHub</span><span class="sxs-lookup"><span data-stu-id="a19c7-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="a19c7-200">Listę problemów 1</span><span class="sxs-lookup"><span data-stu-id="a19c7-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="a19c7-201">Listę problemów 2</span><span class="sxs-lookup"><span data-stu-id="a19c7-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="a19c7-202">Listę problemów 3</span><span class="sxs-lookup"><span data-stu-id="a19c7-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
