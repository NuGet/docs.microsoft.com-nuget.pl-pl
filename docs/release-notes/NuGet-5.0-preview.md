---
title: Informacje o wersji zapoznawczej 5.0 pakietów NuGet
description: Informacje o wersji dotyczące wersji zapoznawczych NuGet w wersji 5.0 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196203"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="20305-103">Informacje o wersji programu NuGet 5.0 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="20305-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="20305-104">Wersje zapoznawcze NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="20305-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="20305-105">27 lutego 2010 — [NuGet w wersji 5.0 w wersji zapoznawczej 4](#summary-whats-new-in-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="20305-105">February 27, 2010 - [NuGet 5.0 Preview 4](#summary-whats-new-in-50-preview-4)</span></span>
* <span data-ttu-id="20305-106">13 lutego 2019 - [NuGet w wersji 5.0 (wersja zapoznawcza) 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="20305-106">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="20305-107">23 stycznia 2019 - [NuGet w wersji 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="20305-107">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="20305-108">Podsumowanie: Co nowego w wersji zapoznawczej NuGet w wersji 5.0 4</span><span class="sxs-lookup"><span data-stu-id="20305-108">Summary: What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="20305-109">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="20305-109">Issues fixed in this release</span></span>

<span data-ttu-id="20305-110">**Błędy:**</span><span class="sxs-lookup"><span data-stu-id="20305-110">**Bugs:**</span></span>

* <span data-ttu-id="20305-111">NuGet.VisualStudio.IVsPackageInstaller — wywoływania nad projektem przy użyciu pakietu nie odwołuje się zawsze używa pliku packages.config, nawet wtedy, gdy są ustawione wartości domyślne do elementu PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="20305-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="20305-112">PMC: Pakiet aktualizacji na pakiety delisted ponownie zainstalować kończy się niepowodzeniem ("nie można odnaleźć pakietu").</span><span class="sxs-lookup"><span data-stu-id="20305-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="20305-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="20305-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="20305-114">Dodaj uwagi dotyczące innych firm w naszym repozytorium i VSIX — [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="20305-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="20305-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage należy zainstalować najnowszą wersję, gdy nie została zainstalowana wersja podane - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="20305-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="20305-116">— interakcyjne obsługę wypychania nuget dotnet - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="20305-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="20305-117">Podczas przywracania przy użyciu pliku blokady, nie należy wygenerowany NU1603 ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="20305-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="20305-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="20305-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="20305-119">NuGet nie powinno wyświetlić ścieżkę projektu podczas przywracania z minimalnym rejestrowaniem - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="20305-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="20305-120">— interakcyjne pomocy technicznej dla platformy dotnet, usuń pakiet - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="20305-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="20305-121">Dodaj kopię NuGet.Packaging.Core z TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="20305-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="20305-122">plugins_cache musi krótszą ścieżkę, aby działać prawidłowo - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="20305-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="20305-123">Preferuj ścieżki programu msbuild odnajdywania, jeśli użytkownik przychodzą msbuild określonych wersji — [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="20305-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="20305-124">**DCRs:**</span><span class="sxs-lookup"><span data-stu-id="20305-124">**DCRs:**</span></span>

* <span data-ttu-id="20305-125">Ogranicz liczbę żądań http na źródłowym za pośrednictwem pliku NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="20305-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="20305-126">NuGet powinien dotyczyć Net472 (ułatwiające oczyszczania 16,0 kompilacji VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="20305-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="20305-127">PMC: Usuń polecenie OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="20305-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="20305-128">Marka NetCoreApp 3.0 mapę, aby NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="20305-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="20305-129">Dodanie obsługi netstandard2.0 do pakietów NuGet.\* - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="20305-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="20305-130">Podsumowanie: Co nowego w wersji zapoznawczej NuGet w wersji 5.0 3</span><span class="sxs-lookup"><span data-stu-id="20305-130">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="20305-131">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="20305-131">Issues fixed in this release</span></span> 

<span data-ttu-id="20305-132">**Błędy:**</span><span class="sxs-lookup"><span data-stu-id="20305-132">**Bugs:**</span></span>

* <span data-ttu-id="20305-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="20305-133">nuget.exe /?</span></span> <span data-ttu-id="20305-134">pomysłem jest wystawienie msbuild poprawne wersje — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="20305-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="20305-135">NuGet.targets(498,5): błąd: Nie można odnaleźć części ścieżki "/ tmp/NuGetScratch — na mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="20305-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="20305-136">Przywracanie niepotrzebnie uwzględnia zawartość wszystkich wersji pakietu odwołanie w pamięci podręcznej maszyny — [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="20305-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="20305-137">Po instalacji programu VS 2019 r w wersji zapoznawczej — automatyczne wykrywanie MSBuild zawsze wybiera 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="20305-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="20305-138">DotNet wyświetlenia listy pakietów na rozwiązanie generuje zduplikowanych wpisów dla framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="20305-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="20305-139">Wyjątek "Nazwa pustej ścieżki jest niedozwolona" podczas wywoływania IVsPackageInstaller.InstallPackage na starym projektów, a następnie umieszcza folder nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="20305-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="20305-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="20305-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="20305-141">minimalny poziom szczegółowości MSBuild /t:restore powinny być mniejsze - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="20305-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="20305-142">**DCRs:**</span><span class="sxs-lookup"><span data-stu-id="20305-142">**DCRs:**</span></span>

* <span data-ttu-id="20305-143">Umożliwia autorom pakietów do definiowania zachowania przechodnie zasoby kompilacji - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="20305-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="20305-144">Włączanie funkcji przywracania w programie VS się powieść, jeśli projekt nie jest częścią rozwiązania lub nie jest załadowany, ale została wcześniej przywrócona - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="20305-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="20305-145">Podsumowanie: Co nowego w wersji 5.0 2</span><span class="sxs-lookup"><span data-stu-id="20305-145">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="20305-146">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="20305-146">Issues fixed in this release</span></span>

<span data-ttu-id="20305-147">**Błędy:**</span><span class="sxs-lookup"><span data-stu-id="20305-147">**Bugs:**</span></span>

* <span data-ttu-id="20305-148">VS firmy 16.0 NuGet interfejsu użytkownika ma nie można go odczytać karty z powodu problemów z kolorem - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="20305-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="20305-149">NuGet.Core & wyjaśnienie NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="20305-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="20305-150">Przywracanie niepotrzebnie uwzględnia folderu pakietu globalne próbę określenia typu — [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="20305-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="20305-151">Błędy z wymuszania pliku blokady powinny być teraz widoczne w oknie Lista błędów - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="20305-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="20305-152">Rozwiązywanie problemów z NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="20305-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="20305-153">Dostosowanie do aktualizowania MSBuild go w lokalizacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="20305-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="20305-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="20305-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="20305-155">NuGet.Build.Tasks.Pack powinny być zależnością programistyczną - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="20305-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="20305-156">Dodaj pakiet rozszerzenia punktu, w tym debugowania symbole - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="20305-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="20305-157">pakietu DotNet powinno zachować zależności zakres wersji w nupkg utworzony.</span><span class="sxs-lookup"><span data-stu-id="20305-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="20305-158">(nawet jeśli jest używana wersja zmiennoprzecinkowego) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="20305-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="20305-159">DotNet restore kończy się niepowodzeniem w źródle uwierzytelnionego podczas konfiguracji na poziomie użytkownika ma również źródłem — [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="20305-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="20305-160">Pakiet, nie należy ograniczyć zestaw BuildActions dla plików zawartości — [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="20305-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="20305-161">Za pomocą elementu projectreference, co wymaga AssetTargetFallback została wykonana pomyślnie, należy ostrzec.</span><span class="sxs-lookup"><span data-stu-id="20305-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="20305-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="20305-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="20305-163">Zakleszczenie spowodowane wątkowości problemy podczas wywoływania w systemie CPS (CommonProjectSystem) — [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="20305-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="20305-164">polecenia DotNet Dodaj pakiet nie używać poświadczeń z globalnej konfiguracji dla źródła, określony w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="20305-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="20305-165">Wątkowość problemy związane z MEF jest wywoływana dla ścieżek codepath async - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="20305-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="20305-166">Podpisywania: zgłoszony dwa razy i bez stosu wywołań — błąd [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="20305-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="20305-167">Instalowanie pakietu podpisane za pomocą niezaufanego certyfikatu podpisywania powinien zostać wyświetlony błąd - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="20305-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="20305-168">Przywracanie NuGet nieprawidłowo NoOps podczas udostępniania katalogu - 2 projektów [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="20305-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="20305-169">Nie można używać osobisty token dostępu z przywracania dotnet w systemie Linux przy użyciu pakietów uwierzytelnionego - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="20305-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="20305-170">DotNet restore kończy się niepowodzeniem z powodu wyłączenia maszyny szerokiego źródła danych — [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="20305-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="20305-171">**DCRs:**</span><span class="sxs-lookup"><span data-stu-id="20305-171">**DCRs:**</span></span>

* <span data-ttu-id="20305-172">Zestawy NuGet w wersji 5.0, będą musieli .NET 4.7.2 (za pośrednictwem elementu TFM zmiana) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="20305-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="20305-173">NuGetLicenseData z NuGet.Packaging powinien być typem publicznym.</span><span class="sxs-lookup"><span data-stu-id="20305-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="20305-174">Zaktualizuj metadane licencji pozyskanych z spdx.</span><span class="sxs-lookup"><span data-stu-id="20305-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="20305-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="20305-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="20305-176">Usuń przestarzałe ustawienia interfejsy API — [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="20305-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="20305-177">Obejście problemu Przywróć przekroczeń limitu czasu w systemach z 1 procesor cpu — [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="20305-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="20305-178">NuGet preferuje uwierzytelniania NTLM, nawet jeśli występują poświadczenia w pliku NuGet.config — dodaj opcję konfiguracji do filtrowania typów uwierzytelniania, aby uzyskać poświadczenia — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="20305-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="20305-179">Włącz EmbedInteropTypes dla funkcji PackageReference (pasującego pliku Packages.Config możliwość) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="20305-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="20305-180">Lista wszystkie problemy rozwiązane w tej wersji 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="20305-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="20305-181">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="20305-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="20305-182">Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="20305-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="20305-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="20305-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="20305-184">**Problem** przy użyciu dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych.</span><span class="sxs-lookup"><span data-stu-id="20305-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="20305-185">Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="20305-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="20305-186">**Obejście** wyłączyć użycie folderu rezerwowego przez ustawienie `RestoreAdditionalProjectSources` na wartość nothing.</span><span class="sxs-lookup"><span data-stu-id="20305-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="20305-187">`<RestoreAdditionalProjectSources/>` Korzystanie z rozwagą, ponieważ spowoduje to wiele pakietów, które mają być pobrane z repozytorium NuGet.org, które w przeciwnym razie byłoby zostały przywrócone z folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="20305-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
