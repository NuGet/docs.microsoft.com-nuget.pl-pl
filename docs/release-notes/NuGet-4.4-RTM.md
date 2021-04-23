---
title: Informacje o wersji nuGet 4.4 RTM
description: Informacje o wersji nuGet 4.4 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 980afffcd4202e019ffa87de5dccf947300a9c13
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901710"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="5e36a-103">Informacje o wersji nuGet 4.4</span><span class="sxs-lookup"><span data-stu-id="5e36a-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="5e36a-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z programem NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="5e36a-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="5e36a-105">Podsumowanie: co nowego w 4.4.0</span><span class="sxs-lookup"><span data-stu-id="5e36a-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="5e36a-106">Podsumowanie: co nowego w programie 4.4.2</span><span class="sxs-lookup"><span data-stu-id="5e36a-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="5e36a-107">Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz pliku ~/.nuget są zbyt [otwarte #7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="5e36a-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="5e36a-108">Podsumowanie: co nowego w 4.4.3</span><span class="sxs-lookup"><span data-stu-id="5e36a-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="5e36a-109">Poprawka zabezpieczeń: Pliki wewnątrz NUPKG mogą mieć ścieżkę względną powyżej katalogu NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="5e36a-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="5e36a-110">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="5e36a-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="5e36a-111">Problemy z .NET Standard 2.0 za pomocą .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="5e36a-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="5e36a-112">.NET Standard & narzędzia zostały zaprojektowane w taki sposób, że projekty przeznaczone dla wersji .NET Framework 4.6.1 mogą korzystać z pakietów NuGet & projektów przeznaczonych dla wersji .NET Standard 2.0 lub starszej.</span><span class="sxs-lookup"><span data-stu-id="5e36a-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="5e36a-113">[Ten dokument](https://github.com/dotnet/standard/issues/481) zawiera podsumowanie problemów związanych z tym scenariuszem, plan ich rozwiązania oraz obejścia, które można wdrożyć przy użyciu dzisiejszego stanu narzędzi.</span><span class="sxs-lookup"><span data-stu-id="5e36a-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="5e36a-114">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="5e36a-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="5e36a-115">Problem</span><span class="sxs-lookup"><span data-stu-id="5e36a-115">Issue</span></span>

<span data-ttu-id="5e36a-116">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5e36a-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="5e36a-117">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="5e36a-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="5e36a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="5e36a-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="5e36a-119">Obejście</span><span class="sxs-lookup"><span data-stu-id="5e36a-119">Workaround</span></span>

<span data-ttu-id="5e36a-120">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5e36a-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="5e36a-121">Alternatywnie spróbuj usunąć i `project.lock.json` przywrócić ponownie.</span><span class="sxs-lookup"><span data-stu-id="5e36a-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="5e36a-122">Nie można wyświetlić, dodać ani zaktualizować aplikacji DotNetCLITools przy użyciu narzędzia Nuget Menedżer pakietów</span><span class="sxs-lookup"><span data-stu-id="5e36a-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="5e36a-123">Problem</span><span class="sxs-lookup"><span data-stu-id="5e36a-123">Issue</span></span>

<span data-ttu-id="5e36a-124">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="5e36a-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="5e36a-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="5e36a-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="5e36a-126">Obejście</span><span class="sxs-lookup"><span data-stu-id="5e36a-126">Workaround</span></span>

<span data-ttu-id="5e36a-127">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="5e36a-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="5e36a-128">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="5e36a-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="5e36a-129">Problem</span><span class="sxs-lookup"><span data-stu-id="5e36a-129">Issue</span></span>

<span data-ttu-id="5e36a-130">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e36a-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="5e36a-131">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5e36a-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="5e36a-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="5e36a-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="5e36a-133">Obejście</span><span class="sxs-lookup"><span data-stu-id="5e36a-133">Workaround</span></span>

<span data-ttu-id="5e36a-134">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5e36a-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="5e36a-135">Pakiet w projekcie .NET Core, który zawiera zestaw z nieprawidłowym podpisem, może spowodować pętlę nieskończoną przywracania</span><span class="sxs-lookup"><span data-stu-id="5e36a-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="5e36a-136">Problem</span><span class="sxs-lookup"><span data-stu-id="5e36a-136">Issue</span></span>

<span data-ttu-id="5e36a-137">W przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie czasem uruchamiane w pętli nieskończonej (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="5e36a-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="5e36a-138">Obejście</span><span class="sxs-lookup"><span data-stu-id="5e36a-138">Workaround</span></span>

<span data-ttu-id="5e36a-139">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="5e36a-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="5e36a-140">Problemy rozwiązane w harmonogramie NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="5e36a-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="5e36a-141">[Informacje o wersji NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) — lista wszystkich problemów rozwiązanych dla wersji NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="5e36a-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="5e36a-142">Funkcje</span><span class="sxs-lookup"><span data-stu-id="5e36a-142">Features</span></span>

- <span data-ttu-id="5e36a-143">Obsługa uproszczonego ładowania rozwiązań w scenariuszach interfejsu użytkownika PMC i NuGet PM — [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="5e36a-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="5e36a-144">Element docelowy pakietu msbuild powinien mieć publiczny element zaczepienia do uruchamiania obiektów docelowych użytkownika przed samym [sobą — #5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="5e36a-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="5e36a-145">Funkcja: Dodawanie przełącznika dependencyVersion do instalacji nuget [— #1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="5e36a-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="5e36a-146">uap10.0.TODO.0 powinien być mapowy do .NET Standard 2.0 dla nuGet — [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="5e36a-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="5e36a-147">Obsługa Visual Studio Build Tools SKU za pomocą msbuild /t:restore — [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="5e36a-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="5e36a-148">Podczas przywracania wygeneruj błąd, jeśli obsługa platform .NET 4.6.1 dla .NET Standard 2.0 jest wymagana, ale nie jest zainstalowana — [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="5e36a-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="5e36a-149">Interfejs użytkownika klienta rezerwacji prefiksu pakietu [— #5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="5e36a-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="5e36a-150">dostarczanie zlokalizowanych składników nuget do dotnet.exe lokalizacji — [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="5e36a-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="5e36a-151">Usterki</span><span class="sxs-lookup"><span data-stu-id="5e36a-151">Bugs</span></span>

- <span data-ttu-id="5e36a-152">Różne wielkości obudowy ścieżek projektu mogą spowodować utratę odszukań packageReferences — [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="5e36a-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="5e36a-153">Przenoszenie kodów błędów z numerami ostrzegawczymi do zakresu błędów [— #5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="5e36a-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="5e36a-154">Mylący błąd, .NET Standard wersja nie jest zgodna z platformą docelową — [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="5e36a-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="5e36a-155">Pliki testowe z mylącymi licencjami [— #5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="5e36a-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="5e36a-156">Brak nagłówków licencji w szablonach testowych EndToEnd [— #5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="5e36a-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="5e36a-157">packages.config przywracania są błędy jako NU1000 [— #5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="5e36a-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="5e36a-158">nuget.exe instalacji powinna mieć ustawienie DisableParallelProcessing na mono [— #5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="5e36a-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="5e36a-159">nuget.exe nieprawidłowo wyłącza buforowanie — [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="5e36a-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="5e36a-160">Program VS uruchamia polecenie przywracania dla packages.config gdy przywracanie jest wyłączone, wyświetla niepoprawny [komunikat — #5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="5e36a-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="5e36a-161">VS; Uruchomienie polecenia przywracania, gdy przywracanie jest wyłączone, powoduje wyświetlenie mylącego [komunikatu — #5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="5e36a-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="5e36a-162">GetRestoreDotnetCliToolsTask kończy się niepowodzeniem, gdy brakuje metadanych wersji — [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="5e36a-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="5e36a-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="5e36a-163">dotnet</span></span>
  - <span data-ttu-id="5e36a-164">Dotnetcore add package can clear empty lines from a csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="5e36a-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="5e36a-165">W nazwach źródeł ustawień poświadczeń w NuGet.Config jest zróżnicowa wielkość [liter — #5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="5e36a-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="5e36a-166">Włączenie funkcji GeneratePackageOnBuild usunęła całą historię pakietów [— #5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="5e36a-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="5e36a-167">Przywracanie nie spowoduje przywrócenia pakietów mono.debianil ani semver, ale wszystkie inne pakiety zostaną przywrócone.</span><span class="sxs-lookup"><span data-stu-id="5e36a-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="5e36a-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="5e36a-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="5e36a-169">Błędy i ostrzeżenia — zły błąd, gdy źródło jest niedostępne.</span><span class="sxs-lookup"><span data-stu-id="5e36a-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="5e36a-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="5e36a-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="5e36a-171">[DesignConsistency] Tekst stanu instalacji nuGet obecnie nie wygląda poprawnie w ciemnym motywie.</span><span class="sxs-lookup"><span data-stu-id="5e36a-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="5e36a-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="5e36a-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="5e36a-173">Aktualizowanie pakietów przy aktualizacjach/instalacjach rozwiązań dla wszystkich projektów — [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="5e36a-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="5e36a-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="5e36a-174">dotnet</span></span>
  - <span data-ttu-id="5e36a-175">Dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="5e36a-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="5e36a-176">Uwzględnione biblioteki DLL w folderze Tools zgłaszają ostrzeżenia [— #5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="5e36a-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="5e36a-177">Model NuGet.ContentModel zużywa zbyt dużo pamięci na operacje na ciągach [— #4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="5e36a-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="5e36a-178">RuntimeEnvironmentHelper.IsLinux zwraca wartość true dla systemu OSX [— #4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="5e36a-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="5e36a-179">Polecenie "dotnet pack" umieszcza nuspec w obszarze obj zamiast obj\Debug — [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="5e36a-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="5e36a-180">Bardzo powolne uaktualnianie pakietu Nuget [— #4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="5e36a-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="5e36a-181">CpS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="5e36a-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="5e36a-182">SemVer 2.0 — pakiet NuGet z podaną wersją ignoruje metadane (3.5.0-rtm-1938) [— #3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="5e36a-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="5e36a-183">Nuget.exe (3.+) z numerem wersji i flagą ExcludeVersion nie aktualizuje pakietu do nowszej wersji [—](https://github.com/NuGet/Home/issues/2405) #2405</span><span class="sxs-lookup"><span data-stu-id="5e36a-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="5e36a-184">Project.jsprzywracania powinien być ostrzegany, gdy pakiety najwyższego poziomu naruszają ograniczenia — [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="5e36a-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="5e36a-185">-ConfigFile nie jest ustawienie niestandardowej konfiguracji polecenia instalacji — [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="5e36a-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="5e36a-186">nuget.exe nie honoruje przełącznika "-DisableParallelProcessing" — [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="5e36a-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="5e36a-187">Wyłączone źródła nadal używane przez DotNet.exe lub msbuild.exe — [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="5e36a-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="5e36a-188">Rozwiązywanie problemów z zawiesza się w scenariuszu LSL [— #5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="5e36a-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="5e36a-189">Kontrolery domeny</span><span class="sxs-lookup"><span data-stu-id="5e36a-189">DCRs</span></span>

- <span data-ttu-id="5e36a-190">nuget.exe zainstalować obsługę obiektu TargetFramework [— #5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="5e36a-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="5e36a-191">Dodawanie różnych ciągów UserAgent zadania msbuild (netcore a desktop msbuild) — [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="5e36a-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="5e36a-192">Parametr PackagePathResolver.GetPackageDirectoryName powinien być wirtualny — [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="5e36a-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="5e36a-193">[DesignConsistency] Mylący komunikat podczas dodawania pakietu NuGet [— #5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="5e36a-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="5e36a-194">[Ostrzeżenia i błędy] NoWarn nie przepływa przechodnie przez odwołania P2P — [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="5e36a-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="5e36a-195">Uproszczone ładowanie rozwiązań: Podstawowe funkcje interfejsu użytkownika PM, PMC i IV — [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="5e36a-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="5e36a-196">Uproszczone ładowanie rozwiązań: obsługa — PMC [— #5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="5e36a-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="5e36a-197">Dodawania obsługi wstępnego przywracania obiektu docelowego MSBuild, Visual Studio wyzwalaczy — [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="5e36a-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="5e36a-198">Dodawanie publicznego obiektu docelowego do obiektu NuGet.targets, do których można się odwoływać przy użyciu funkcji BeforeTargets — [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="5e36a-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="5e36a-199">Element docelowy pakietu nie może poprawnie tworzyć plików z akcjami kompilacji — [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="5e36a-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="5e36a-200">RestoreOperationLogger.Do bloków wątków puli wątków [— #5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="5e36a-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="5e36a-201">Docs</span><span class="sxs-lookup"><span data-stu-id="5e36a-201">Docs</span></span>

- <span data-ttu-id="5e36a-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="5e36a-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="5e36a-203">Aktualizacja do dokumentów dotyczących ostrzeżeń i błędów nuGet — [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="5e36a-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="5e36a-204">Linki do problemów z serwisem GitHub rozwiązanych w wersji 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="5e36a-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="5e36a-205">Lista problemów 1</span><span class="sxs-lookup"><span data-stu-id="5e36a-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="5e36a-206">Lista problemów 2</span><span class="sxs-lookup"><span data-stu-id="5e36a-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="5e36a-207">Lista problemów 3</span><span class="sxs-lookup"><span data-stu-id="5e36a-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
