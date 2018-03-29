---
title: Informacje o wersji RTM NuGet 4.4 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.3 NuGet.
keywords: NuGet 4.3 RTM informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6c122dc3d9b576a2ea5f094746a830e5fab5637e
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="449e9-104">Informacje o wersji 4.4 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="449e9-104">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="449e9-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="449e9-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="449e9-106">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="449e9-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="449e9-107">Problemy z platformą .NET 2.0 standardowe z .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="449e9-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="449e9-108">.NET standard i jej narzędzi została zaprojektowana w taki sposób, że w projektach przeznaczonych dla platformy .NET Framework 4.6.1 może używać pakietów NuGet & projektach przeznaczonych dla platformy .NET Standard 2.0 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="449e9-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="449e9-109">[Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemy dotyczące tego scenariusza, plan adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="449e9-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="449e9-110">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="449e9-110">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="449e9-111">Problem</span><span class="sxs-lookup"><span data-stu-id="449e9-111">Issue</span></span>

<span data-ttu-id="449e9-112">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="449e9-112">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="449e9-113">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="449e9-113">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="449e9-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="449e9-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="449e9-115">Obejście</span><span class="sxs-lookup"><span data-stu-id="449e9-115">Workaround</span></span>

<span data-ttu-id="449e9-116">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="449e9-116">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="449e9-117">Alternatywnie, spróbuj usunąć `project.lock.json` i przywracanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="449e9-117">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="449e9-118">Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="449e9-118">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="449e9-119">Problem</span><span class="sxs-lookup"><span data-stu-id="449e9-119">Issue</span></span>

<span data-ttu-id="449e9-120">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="449e9-120">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="449e9-121">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="449e9-121">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="449e9-122">Obejście</span><span class="sxs-lookup"><span data-stu-id="449e9-122">Workaround</span></span>

<span data-ttu-id="449e9-123">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="449e9-123">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="449e9-124">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="449e9-124">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="449e9-125">Problem</span><span class="sxs-lookup"><span data-stu-id="449e9-125">Issue</span></span>

<span data-ttu-id="449e9-126">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="449e9-126">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="449e9-127">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="449e9-127">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="449e9-128">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="449e9-128">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="449e9-129">Obejście</span><span class="sxs-lookup"><span data-stu-id="449e9-129">Workaround</span></span>

<span data-ttu-id="449e9-130">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="449e9-130">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="449e9-131">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="449e9-131">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="449e9-132">Problem</span><span class="sxs-lookup"><span data-stu-id="449e9-132">Issue</span></span>

<span data-ttu-id="449e9-133">Od czasu do czasu gdy używasz pakietu, który zawiera zestaw z nieprawidłowym podpisem lub wersja pakietu jest ustawiona z typu "DateTime" znacznika powoduje Przywracanie automatycznego pakietu do uruchamiania w nieskończonej pętli (dotnet/project — system #1457).</span><span class="sxs-lookup"><span data-stu-id="449e9-133">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="449e9-134">Obejście</span><span class="sxs-lookup"><span data-stu-id="449e9-134">Workaround</span></span>

<span data-ttu-id="449e9-135">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="449e9-135">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="449e9-136">Problemy, które usunięto w wersji RTM programu NuGet 4.4 przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="449e9-136">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="449e9-137">[NuGet 4.3 RTM informacje o wersji](../release-notes/nuget-4.3-RTM.md) -Wyświetla wszystkie problemy, które są rozwiązywane RTM 4.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="449e9-137">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="449e9-138">Funkcje</span><span class="sxs-lookup"><span data-stu-id="449e9-138">Features</span></span>

- <span data-ttu-id="449e9-139">Obsługa protokołu Lightweight ładowania rozwiązania w scenariuszach PMC i NuGet PM interfejsu użytkownika — [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="449e9-139">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="449e9-140">Element docelowy programu msbuild pakietu powinien mieć publicznego punktu zaczepienia dla uruchomionego celów użytkownika przed sam - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="449e9-140">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="449e9-141">Funkcja: Dodać przełącznik dependencyVersion nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="449e9-141">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="449e9-142">uap10.0.ToDo.0 powinny być mapowane na .NET 2.0 standardowy programu NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="449e9-142">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="449e9-143">Obsługuje SKU z narzędzia kompilacji programu Visual Studio z msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="449e9-143">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="449e9-144">Podczas przywracania, generuje błąd, jeśli .NET 4.6.1 Obsługa .NET 2.0 standardowe jest wymagana, ale nie jest zainstalowany - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="449e9-144">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="449e9-145">Interfejs użytkownika — klienta rezerwacji prefiks Identyfikatora pakietu [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="449e9-145">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="449e9-146">dostarczanie składników zlokalizowanych nuget w celu obsługi lokalizacja dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="449e9-146">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="449e9-147">Usterki</span><span class="sxs-lookup"><span data-stu-id="449e9-147">Bugs</span></span>

- <span data-ttu-id="449e9-148">Obudowy ścieżki inny projekt może spowodować utratę PackageReferences — po ukończeniu przywracania [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="449e9-148">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="449e9-149">Przenieś kodów błędów z numerów ostrzeżeń, które zakresowi błąd - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="449e9-149">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="449e9-150">Błąd błąd, gdy wersja platformy .NET Standard nie jest znany aby był zgodny z platformy docelowej - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="449e9-150">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="449e9-151">Testowanie plików z licencjami mylące - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="449e9-151">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="449e9-152">Brak nagłówków licencji w EndToEnd testowanie szablonów - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="449e9-152">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="449e9-153">Przywracanie pliku Packages.config pokazuje błędy jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="449e9-153">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="449e9-154">Zainstaluj nuget.exe powinny mieć DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="449e9-154">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="449e9-155">Zainstaluj nuget.exe niepoprawnie wyłącza buforowanie - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="449e9-155">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="449e9-156">VS polecenia przywracania dla pliku packages.config podczas przywracania jest wyłączona, zostanie wyświetlony komunikat niepoprawne - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="449e9-156">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="449e9-157">VS; Polecenia restore podczas przywracania jest wyłączona, zostanie wyświetlony komunikat mylące - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="449e9-157">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="449e9-158">GetRestoreDotnetCliToolsTask ulegnie awarii, gdy brak metadanych wersji - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="449e9-158">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="449e9-159">Dodaj DotNet pakietu można wyczyścić puste wiersze z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="449e9-159">dotnet add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="449e9-160">Nazwy źródeł ustawień poświadczeń w pliku NuGet.Config jest uwzględniana wielkość liter - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="449e9-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="449e9-161">Włączanie GeneratePackageOnBuild usunięte Moje całej historii pakiety - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="449e9-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="449e9-162">Przywracanie nie przywróci mono.cecil lub programu semver pakietów, ale inne pakiety pobrać przywrócony.</span><span class="sxs-lookup"><span data-stu-id="449e9-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="449e9-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="449e9-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="449e9-164">Błędy i ostrzeżenia - zły błąd podczas źródła niedostępne.</span><span class="sxs-lookup"><span data-stu-id="449e9-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="449e9-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="449e9-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="449e9-166">[DesignConsistency] Obecnie nie wygląda prawidłowe na ciemny motyw tekst stanu instalacji NuGet.</span><span class="sxs-lookup"><span data-stu-id="449e9-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="449e9-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="449e9-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="449e9-168">Aktualizowanie pakietów w aktualizacji rozwiązania/instaluje we wszystkich projektach — [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="449e9-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="449e9-169">Pakiet DotNet zachowuje się inaczej w zależności od vs TargetFramework TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="449e9-169">dotnet pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="449e9-170">Objąć biblioteki DLL narzędzia folderu throw ostrzeżenia - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="449e9-170">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="449e9-171">NuGet.ContentModel zużywa zbyt dużej ilości pamięci dla operacji na ciągach - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="449e9-171">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="449e9-172">RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla systemu OS x - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="449e9-172">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="449e9-173">"pakiet dotnet" umieszcza nuspec w obszarze obj zamiast obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="449e9-173">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="449e9-174">Nuget bardzo wolno uaktualniania pakietu - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="449e9-174">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="449e9-175">Zsynchronizowane procedury CPS przywracania większe rozwiązania, których nie włączono LSL (Przywracanie lekkie rozwiązanie) - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="449e9-175">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="449e9-176">Programu SemVer 2.0 — nuget pakietu z warunkiem wersja ignoruje metadanych (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="449e9-176">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="449e9-177">Nuget.exe (3 +) zainstaluj pakiet o numerze wersji i flagi ExcludeVersion nie powoduje aktualizacji pakietu do nowszej wersji — [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="449e9-177">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="449e9-178">Przywracanie Project.JSON powinien Ostrzegaj, gdy pakiety najwyższego poziomu narusza ograniczenia — [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="449e9-178">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="449e9-179">-ConfigFile nie jest ustawienie niestandardowej konfiguracji polecenia install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="449e9-179">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="449e9-180">Zainstaluj nuget.exe honoruje "-DisableParallelProcessing" przełącznika - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="449e9-180">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="449e9-181">Wyłączone źródeł nadal używane przez DotNet.exe lub msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="449e9-181">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="449e9-182">Usuń zawiesza się na scenariuszu LSL - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="449e9-182">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="449e9-183">Dcr</span><span class="sxs-lookup"><span data-stu-id="449e9-183">DCRs</span></span>

- <span data-ttu-id="449e9-184">nuget.exe Zainstaluj obsługę TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="449e9-184">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="449e9-185">Dodaj inny msbuild zadania agenta użytkownika ciągi (msbuild pulpitu netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="449e9-185">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="449e9-186">PackagePathResolver.GetPackageDirectoryName powinny być wirtualna - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="449e9-186">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="449e9-187">[DesignConsistency] Skomplikowana komunikat podczas dodawania pakietu NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="449e9-187">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="449e9-188">[Ostrzeżeń i błędów] NoWarn nie przechodnie przepływać przez odwołania P2P - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="449e9-188">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="449e9-189">Ładowania rozwiązania lekkie: Core wspólnego PM interfejsu użytkownika, PMC i wektory inicjacji-- [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="449e9-189">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="449e9-190">Obciążenia lekkie rozwiązanie: Obsługuje - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="449e9-190">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="449e9-191">Dodaj obsługę wstępnie przywrócić docelowy programu MSBuild, który wyzwala Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="449e9-191">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="449e9-192">Dodaj publiczny docelowych do NuGet.targets, który można odwoływać się przy użyciu BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="449e9-192">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="449e9-193">Docelowy pakiet nie można utworzyć pliki z akcjami kompilacji nieprawidłowo — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="449e9-193">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="449e9-194">RestoreOperationLogger.Do blokuje wątków z puli wątków - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="449e9-194">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="449e9-195">Docs</span><span class="sxs-lookup"><span data-stu-id="449e9-195">Docs</span></span>

- <span data-ttu-id="449e9-196">Dokumentacja instalacji poleceń flagi DependencyVersion i Framework — [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="449e9-196">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="449e9-197">Aktualizacja do dokumentów na NuGet ostrzeżeń i błędów - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="449e9-197">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="449e9-198">Łącza do usunięto w wersji 4.4 RTM zagadnienia GitHub</span><span class="sxs-lookup"><span data-stu-id="449e9-198">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="449e9-199">Listę problemów 1</span><span class="sxs-lookup"><span data-stu-id="449e9-199">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="449e9-200">Listę problemów 2</span><span class="sxs-lookup"><span data-stu-id="449e9-200">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="449e9-201">Listę problemów 3</span><span class="sxs-lookup"><span data-stu-id="449e9-201">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
