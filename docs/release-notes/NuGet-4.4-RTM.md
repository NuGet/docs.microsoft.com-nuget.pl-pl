---
title: Informacje o wersji 4.4 RTM NuGet
description: Informacje o wersji programu NuGet 4.3 RTM, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548417"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="a45b5-103">Informacje o wersji 4.4 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="a45b5-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="a45b5-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet w wersji 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="a45b5-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a45b5-105">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a45b5-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="a45b5-106">Problemy z platformą .NET Standard 2.0 przy użyciu platformy .NET Framework i NuGet</span><span class="sxs-lookup"><span data-stu-id="a45b5-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="a45b5-107">.NET standard i jego narzędzia zaprojektowano w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 może zużywać pakietów NuGet i projekty przeznaczone dla .NET Standard 2.0 lub wcześniejszej.</span><span class="sxs-lookup"><span data-stu-id="a45b5-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="a45b5-108">[W tym dokumencie](https://github.com/dotnet/standard/issues/481) znajduje się podsumowanie problemy dotyczące tego scenariusza, planowanie adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="a45b5-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="a45b5-109">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="a45b5-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="a45b5-110">Problem</span><span class="sxs-lookup"><span data-stu-id="a45b5-110">Issue</span></span>

<span data-ttu-id="a45b5-111">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a45b5-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="a45b5-112">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="a45b5-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="a45b5-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="a45b5-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="a45b5-114">Obejście</span><span class="sxs-lookup"><span data-stu-id="a45b5-114">Workaround</span></span>

<span data-ttu-id="a45b5-115">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a45b5-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="a45b5-116">Alternatywnie, spróbuj usunąć `project.lock.json` i przywrócić go ponownie.</span><span class="sxs-lookup"><span data-stu-id="a45b5-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="a45b5-117">Nie można wyświetlić, dodać ani zaktualizować składnika DotNetCLITools przy użyciu Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="a45b5-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="a45b5-118">Problem</span><span class="sxs-lookup"><span data-stu-id="a45b5-118">Issue</span></span>

<span data-ttu-id="a45b5-119">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="a45b5-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="a45b5-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="a45b5-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="a45b5-121">Obejście</span><span class="sxs-lookup"><span data-stu-id="a45b5-121">Workaround</span></span>

<span data-ttu-id="a45b5-122">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="a45b5-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="a45b5-123">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="a45b5-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="a45b5-124">Problem</span><span class="sxs-lookup"><span data-stu-id="a45b5-124">Issue</span></span>

<span data-ttu-id="a45b5-125">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a45b5-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="a45b5-126">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a45b5-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="a45b5-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="a45b5-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="a45b5-128">Obejście</span><span class="sxs-lookup"><span data-stu-id="a45b5-128">Workaround</span></span>

<span data-ttu-id="a45b5-129">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="a45b5-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="a45b5-130">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="a45b5-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="a45b5-131">Problem</span><span class="sxs-lookup"><span data-stu-id="a45b5-131">Issue</span></span>

<span data-ttu-id="a45b5-132">Od czasu do czasu gdy używasz pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika "DateTime", powoduje automatyczne przywracanie pakietu do działania w pętli nieskończonej (dotnet/project-system #1457).</span><span class="sxs-lookup"><span data-stu-id="a45b5-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="a45b5-133">Obejście</span><span class="sxs-lookup"><span data-stu-id="a45b5-133">Workaround</span></span>

<span data-ttu-id="a45b5-134">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="a45b5-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="a45b5-135">Problemy rozwiązane w wersji RTM w wersji 4.4 NuGet przedział czasu</span><span class="sxs-lookup"><span data-stu-id="a45b5-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="a45b5-136">[4.3 RTM informacjach o wersji NuGet](../release-notes/nuget-4.3-RTM.md) — Wyświetla listę wszystkich problemów naprawione w wersji RTM 4.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="a45b5-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="a45b5-137">Funkcje</span><span class="sxs-lookup"><span data-stu-id="a45b5-137">Features</span></span>

- <span data-ttu-id="a45b5-138">Obsługa uproszczonego ładowania rozwiązań w scenariuszach PMC i NuGet PM interfejsu użytkownika — [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="a45b5-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="a45b5-139">Element docelowy programu msbuild pakiet powinien mieć publicznego punktu zaczepienia dla uruchomionej docelowi przed sam - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="a45b5-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="a45b5-140">Funkcja: Dodanie przełącznika dependencyVersion instalacji nuget — [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="a45b5-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="a45b5-141">uap10.0.ToDo.0 powinny być mapowane na .NET Standard 2.0 dla NuGet — [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="a45b5-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="a45b5-142">Obsługuje program Visual Studio narzędziach do kompilacji SKU z msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="a45b5-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="a45b5-143">Podczas przywracania, generuje błąd, jeśli .NET 4.6.1 Pomoc techniczna dla platformy .NET Standard 2.0 jest wymagana, ale nie jest zainstalowany - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="a45b5-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="a45b5-144">Interfejs użytkownika — klienta rezerwacji prefiks Identyfikatora pakietu [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="a45b5-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="a45b5-145">dostarczanie składników zlokalizowanej nuget w celu obsługi lokalizacji dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="a45b5-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="a45b5-146">Usterki</span><span class="sxs-lookup"><span data-stu-id="a45b5-146">Bugs</span></span>

- <span data-ttu-id="a45b5-147">Obudowy ścieżki innego projektu może spowodować, że przywracanie utratę PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="a45b5-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="a45b5-148">Przenieś kodów błędów z numery ostrzeżeń do zakres błędów — [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="a45b5-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="a45b5-149">Mylące błąd, gdy .NET Standard w wersji nie jest znany ma być kompatybilna platformę docelową — [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="a45b5-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="a45b5-150">Pliki z licencjami mylące - testu [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="a45b5-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="a45b5-151">Brak nagłówków licencji EndToEnd testowanie szablonów — [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="a45b5-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="a45b5-152">błędy w pliku Packages.config przywracania jest wyświetlany jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="a45b5-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="a45b5-153">Zainstaluj nuget.exe powinna mieć DisableParallelProcessing na mono — [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="a45b5-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="a45b5-154">Zainstaluj nuget.exe niepoprawnie wyłącza buforowanie - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="a45b5-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="a45b5-155">VS polecenia przywracania dla pliku packages.config po wyłączeniu przywracania Wyświetla niepoprawny komunikat - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="a45b5-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="a45b5-156">VS; Uruchomienie polecenia przywracania po wyłączeniu przywracania wyświetla komunikat mylące - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="a45b5-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="a45b5-157">GetRestoreDotnetCliToolsTask ulegnie awarii, gdy brak metadanych wersji - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="a45b5-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="a45b5-158">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="a45b5-158">dotnet</span></span>
  - <span data-ttu-id="a45b5-159">dotnetcore Dodawanie pakietów można wyczyścić puste wiersze z pliku csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="a45b5-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="a45b5-160">Źródło nazwy ustawienia poświadczeń w pliku NuGet.Config jest uwzględniana wielkość liter — [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="a45b5-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="a45b5-161">Włączanie GeneratePackageOnBuild usunięte całej historii pakietów - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="a45b5-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="a45b5-162">Przywracanie nie spowoduje przywrócenia pakietów mono.cecil lub semver, ale inne pakiety pobrać przywrócony.</span><span class="sxs-lookup"><span data-stu-id="a45b5-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="a45b5-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="a45b5-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="a45b5-164">Błędy i ostrzeżenia — zła podczas źródło niedostępne.</span><span class="sxs-lookup"><span data-stu-id="a45b5-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="a45b5-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="a45b5-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="a45b5-166">[DesignConsistency] Obecnie tekst stanu instalacji NuGet wygląda prawidłowe na ciemny.</span><span class="sxs-lookup"><span data-stu-id="a45b5-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="a45b5-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="a45b5-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="a45b5-168">Aktualizowanie pakietów w rozwiązaniu aktualizacji/instalacje dla wszystkich projektów — [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="a45b5-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="a45b5-169">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="a45b5-169">dotnet</span></span>
  - <span data-ttu-id="a45b5-170">Pakiet dotnetcore zachowuje się inaczej w zależności od tego, vs TargetFramework TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="a45b5-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="a45b5-171">Uwzględnione biblioteki DLL wewnątrz ostrzeżenia throw folderu narzędzia - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="a45b5-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="a45b5-172">NuGet.ContentModel zużywa zbyt dużej ilości pamięci dla operacji na ciągach - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="a45b5-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="a45b5-173">RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla systemu OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="a45b5-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="a45b5-174">"pakietu dotnet" umieszcza nuspec w obszarze obj zamiast obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="a45b5-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="a45b5-175">Nuget bardzo wolno uaktualnienie pakietu - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="a45b5-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="a45b5-176">Dokument CPS zsynchronizowany przy użyciu przywracania z większych rozwiązania, które nie zostały włączone LSL (Przywracanie uproszczone ładowanie rozwiązań) — [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="a45b5-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="a45b5-177">SemVer 2.0 - nuget pakietu z podana wersja ignoruje metadanych (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="a45b5-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="a45b5-178">Nuget.exe (3 i nowsze): Zainstaluj pakiet przy użyciu numeru wersji i Flaga ExcludeVersion nie powoduje aktualizacji pakietu do nowszej wersji — [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="a45b5-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="a45b5-179">Przywracanie pliku Project.JSON powinien Ostrzegaj, gdy najwyższego pakiety narusza ograniczenia - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="a45b5-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="a45b5-180">-ConfigFile nie jest ustawienie niestandardowej konfiguracji polecenia install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="a45b5-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="a45b5-181">Zainstaluj nuget.exe nie uznaje "-DisableParallelProcessing" przełącznika - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="a45b5-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="a45b5-182">Wyłączone źródła nadal używany przez DotNet.exe lub msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="a45b5-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="a45b5-183">Usuń zawiesza się na scenariusz LSL — [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="a45b5-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="a45b5-184">DCRs</span><span class="sxs-lookup"><span data-stu-id="a45b5-184">DCRs</span></span>

- <span data-ttu-id="a45b5-185">nuget.exe nainstalovat podporu TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="a45b5-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="a45b5-186">Dodaj inny msbuild zadań UserAgent ciągi (msbuild pulpitu netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="a45b5-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="a45b5-187">PackagePathResolver.GetPackageDirectoryName powinny być wirtualne — [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="a45b5-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="a45b5-188">[DesignConsistency] Mylenie komunikat podczas dodawania pakietów NuGet — [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="a45b5-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="a45b5-189">[Ostrzeżenia i błędy] NoWarn nie przekazywane, realizowane w sposób przechodni odwołania P2P - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="a45b5-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="a45b5-190">Uproszczone ładowanie rozwiązania: Typowych podstawowe dla interfejsu użytkownika PM, konsolę zarządzania Pakietami, a następnie wektory - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="a45b5-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="a45b5-191">Uproszczone ładowanie rozwiązania: Obsługi - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="a45b5-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="a45b5-192">Dodano obsługę wstępnie przywrócić docelowy programu MSBuild, która powoduje uruchomienie programu Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="a45b5-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="a45b5-193">Dodanie elementu docelowego publicznej do NuGet.targets, która może znajdować się za pomocą BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="a45b5-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="a45b5-194">Pakiet docelowy nie może utworzyć pliki za pomocą akcji kompilacji nieprawidłowo — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="a45b5-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="a45b5-195">RestoreOperationLogger.Do blokuje wątków z puli wątków - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="a45b5-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="a45b5-196">Docs</span><span class="sxs-lookup"><span data-stu-id="a45b5-196">Docs</span></span>

- <span data-ttu-id="a45b5-197">Dokumenty dotyczące instalacji polecenie DependencyVersion i struktury flagi - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="a45b5-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="a45b5-198">Aktualizacja do dokumentów w ostrzeżenia i błędy - NuGet [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="a45b5-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="a45b5-199">Linki na problemy usługi GitHub, rozwiązane w wersji 4.4 lub RTM</span><span class="sxs-lookup"><span data-stu-id="a45b5-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="a45b5-200">Problemy z listy 1</span><span class="sxs-lookup"><span data-stu-id="a45b5-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="a45b5-201">Problemy z listy 2</span><span class="sxs-lookup"><span data-stu-id="a45b5-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="a45b5-202">Problemy z listy 3</span><span class="sxs-lookup"><span data-stu-id="a45b5-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
