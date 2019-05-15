---
title: Informacje o wersji 5.0 RTM NuGet
description: Informacje o wersji programu NuGet 5.0 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610659"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="54f78-103">Informacje o wersji 5.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="54f78-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="54f78-104">NuGet pojazdów dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="54f78-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="54f78-105">NuGet w wersji</span><span class="sxs-lookup"><span data-stu-id="54f78-105">NuGet version</span></span> | <span data-ttu-id="54f78-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54f78-106">Available in Visual Studio version</span></span>| <span data-ttu-id="54f78-107">Dostępne w zestawów SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="54f78-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="54f78-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="54f78-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="54f78-109">Visual Studio 2019 version 16.0</span><span class="sxs-lookup"><span data-stu-id="54f78-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="54f78-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="54f78-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="54f78-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="54f78-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="54f78-112">Visual Studio 2019 version 16.0.4</span><span class="sxs-lookup"><span data-stu-id="54f78-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="54f78-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="54f78-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="54f78-114"><sup>1</sup>instalowane z Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="54f78-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="54f78-115"><sup>2</sup>jest dostępna jako opcjonalna instalacja przy użyciu programu Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="54f78-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="54f78-116">Podsumowanie: Co nowego w wersji 5.0</span><span class="sxs-lookup"><span data-stu-id="54f78-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="54f78-117">Obsługa przywracania [filtrowane rozwiązania](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) w programie Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="54f78-117">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="54f78-118">`BuildTransitive` folder umożliwia pakietów została przechodnio współtworzyć celów/arkuszy właściwości do projektu hosta — [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="54f78-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="54f78-119">Lepsza obsługa scenariuszy PackageReference w interfejsach API wektory NuGet — [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="54f78-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="54f78-120">`nuget.exe pack project.json` jest przestarzała - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="54f78-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="54f78-121">Dodatek dostawcy poświadczeń Gen 1 została zastąpiona przez [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) i zostanie wkrótce staną się przestarzałe — [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="54f78-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="54f78-122">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="54f78-122">Issues fixed in this release</span></span>

<span data-ttu-id="54f78-123">**Błędy**</span><span class="sxs-lookup"><span data-stu-id="54f78-123">**Bugs**</span></span>

* <span data-ttu-id="54f78-124">W trakcie przywracania aktualizujący nie działa, należy unikać \*. dgspec.json zapisu w katalogu obj — [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="54f78-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="54f78-125">Uprawnień do plików utworzony wewnątrz ~/.nuget są zbyt otwarte — [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="54f78-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="54f78-126">`dotnet list package --outdated` nie działa ze źródeł, które wymagają uwierzytelniania - [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="54f78-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="54f78-127">NuGet.VisualStudio.IVsPackageInstaller — wywoływania nad projektem przy użyciu pakietu nie odwołuje się zawsze używa pliku packages.config, nawet wtedy, gdy są ustawione wartości domyślne do elementu PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="54f78-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="54f78-128">PMC: Pakiet aktualizacji na pakiety delisted ponownie zainstalować kończy się niepowodzeniem ("nie można odnaleźć pakietu").</span><span class="sxs-lookup"><span data-stu-id="54f78-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="54f78-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="54f78-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="54f78-130">Dodaj uwagi dotyczące innych firm w naszym repozytorium i VSIX — [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="54f78-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="54f78-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage należy zainstalować najnowszą wersję, gdy nie została zainstalowana wersja podane - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="54f78-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="54f78-132">— interakcyjne obsługę wypychania nuget dotnet - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="54f78-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="54f78-133">Podczas przywracania przy użyciu pliku blokady, nie należy wygenerowany NU1603 ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="54f78-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="54f78-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="54f78-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="54f78-135">NuGet nie powinno wyświetlić ścieżkę projektu podczas przywracania z minimalnym rejestrowaniem - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="54f78-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="54f78-136">— interakcyjne pomocy technicznej dla platformy dotnet, usuń pakiet - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="54f78-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="54f78-137">Dodaj kopię NuGet.Packaging.Core z TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="54f78-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="54f78-138">plugins_cache musi krótszą ścieżkę, aby działać prawidłowo - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="54f78-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="54f78-139">Preferuj ścieżki programu msbuild odnajdywania, jeśli użytkownik przychodzą msbuild określonych wersji — [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="54f78-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="54f78-140">`nuget.exe /?` pomysłem jest wystawienie msbuild poprawne wersje — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="54f78-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="54f78-141">NuGet.targets(498,5): błąd: Nie można odnaleźć części ścieżki "/ tmp/NuGetScratch — na mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="54f78-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="54f78-142">Przywracanie niepotrzebnie uwzględnia zawartość wszystkich wersji pakietu odwołanie w pamięci podręcznej maszyny — [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="54f78-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="54f78-143">Po instalacji programu VS 2019 r w wersji zapoznawczej — automatyczne wykrywanie MSBuild zawsze wybiera 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="54f78-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="54f78-144">DotNet wyświetlenia listy pakietów na rozwiązanie generuje zduplikowanych wpisów dla framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="54f78-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="54f78-145">Wyjątek "Nazwa pustej ścieżki jest niedozwolona" podczas wywoływania IVsPackageInstaller.InstallPackage na starym projektów, a następnie umieszcza folder nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="54f78-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="54f78-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="54f78-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="54f78-147">minimalny poziom szczegółowości MSBuild /t:restore powinny być mniejsze - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="54f78-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="54f78-148">VS firmy 16.0 NuGet interfejsu użytkownika ma nie można go odczytać karty z powodu problemów z kolorem - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="54f78-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="54f78-149">NuGet.Core & wyjaśnienie NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="54f78-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="54f78-150">Przywracanie niepotrzebnie uwzględnia folderu pakietu globalne próbę określenia typu — [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="54f78-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="54f78-151">Błędy z wymuszania pliku blokady powinny być teraz widoczne w oknie Lista błędów - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="54f78-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="54f78-152">Rozwiązywanie problemów z NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="54f78-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="54f78-153">Dostosowanie do aktualizowania swoich instalacji programu MSBuild lokalizacji — [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="54f78-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="54f78-154">NuGet.Build.Tasks.Pack powinny być zależnością programistyczną - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="54f78-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="54f78-155">Dodaj pakiet rozszerzenia punktu, w tym debugowania symbole - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="54f78-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="54f78-156">`dotnet pack` zakres wersji zależności w utworzonej nupkg powinno zachować (nawet jeśli jest używana wersja zmiennoprzecinkowego) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="54f78-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="54f78-157">`dotnet restore` kończy się niepowodzeniem w źródle uwierzytelnionego podczas konfiguracji na poziomie użytkownika ma również źródłem — [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="54f78-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="54f78-158">Pakiet, nie należy ograniczyć zestaw BuildActions dla plików zawartości — [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="54f78-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="54f78-159">Za pomocą elementu ProjectReference, co wymaga AssetTargetFallback została wykonana pomyślnie, należy ostrzec.</span><span class="sxs-lookup"><span data-stu-id="54f78-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="54f78-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="54f78-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="54f78-161">Zakleszczenie spowodowane wątkowości problemy podczas wywoływania w systemie CPS (CommonProjectSystem) — [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="54f78-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="54f78-162">`dotnet add package` nie używa poświadczeń z globalnej konfiguracji dla źródła, określony w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="54f78-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="54f78-163">Wątkowości problemy związane z MEF wywoływane na asynchronicznej kodu ścieżki - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="54f78-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="54f78-164">Podpisywania: zgłoszony dwa razy i bez stosu wywołań — błąd [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="54f78-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="54f78-165">Instalowanie pakietu podpisane za pomocą niezaufanego certyfikatu podpisywania powinien zostać wyświetlony błąd - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="54f78-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="54f78-166">Przywracanie NuGet nieprawidłowo NoOps podczas udostępniania katalogu - 2 projektów [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="54f78-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="54f78-167">Nie można użyć osobisty token dostępu z `dotnet restore` w systemie Linux przy użyciu pakietów uwierzytelnionego - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="54f78-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="54f78-168">DotNet restore kończy się niepowodzeniem z powodu wyłączenia maszyny szerokiego źródła danych — [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="54f78-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="54f78-169">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="54f78-169">**DCRs**</span></span>

* <span data-ttu-id="54f78-170">Ostrzega o usunięcia "pakietu dotnet project.json" — w przyszłości [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="54f78-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="54f78-171">Dodaj ostrzeżenie o zakończeniu obsługi dla wtyczki poświadczeń Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="54f78-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="54f78-172">Signing: Włączone repozytorium, aby wymagać weryfikacji klienta dla każdego pakietu jako repozytorium podpisane — za pośrednictwem zasobów RepositorySignatures/5.0.0 - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="54f78-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="54f78-173">Ogranicz liczbę żądań http na źródłowym za pośrednictwem pliku NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="54f78-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="54f78-174">NuGet powinien dotyczyć Net472 (ułatwiające oczyszczania 16,0 kompilacji VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="54f78-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="54f78-175">PMC: Usuń polecenie OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="54f78-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="54f78-176">Marka NetCoreApp 3.0 mapę, aby NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="54f78-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="54f78-177">Dodanie obsługi netstandard2.0 do pakietów NuGet.\* - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="54f78-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="54f78-178">Umożliwia autorom pakietów do definiowania zachowania przechodnie zasoby kompilacji - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="54f78-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="54f78-179">Obsługa funkcji Filtr rozwiązania 2019 programu VS.</span><span class="sxs-lookup"><span data-stu-id="54f78-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="54f78-180">Obsługuje również projektu nie w rozwiązaniu lub zwolnione projektów.</span><span class="sxs-lookup"><span data-stu-id="54f78-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="54f78-181">Konieczność jego przywrócenia kompletnego rozwiązania (za pośrednictwem interfejsu wiersza polecenia lub programu VS), najpierw - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="54f78-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="54f78-182">Zestawy NuGet w wersji 5.0, będą musieli .NET 4.7.2 (za pośrednictwem elementu TFM zmiana) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="54f78-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="54f78-183">NuGetLicenseData z NuGet.Packaging powinien być typem publicznym.</span><span class="sxs-lookup"><span data-stu-id="54f78-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="54f78-184">Zaktualizuj metadane licencji pozyskanych z spdx.</span><span class="sxs-lookup"><span data-stu-id="54f78-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="54f78-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="54f78-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="54f78-186">Usuń przestarzałe ustawienia interfejsy API — [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="54f78-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="54f78-187">Obejście problemu Przywróć przekroczeń limitu czasu w systemach z 1 procesor cpu — [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="54f78-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="54f78-188">NuGet preferuje uwierzytelniania NTLM, nawet jeśli występują poświadczenia w pliku NuGet.config — dodaj opcję konfiguracji do filtrowania typów uwierzytelniania, aby uzyskać poświadczenia — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="54f78-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="54f78-189">Włącz EmbedInteropTypes dla funkcji PackageReference (pasującego pliku Packages.Config możliwość) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="54f78-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="54f78-190">**[Lista wszystkie problemy rozwiązane w tej wersji - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="54f78-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="54f78-191">Podsumowanie: What's New in 5.0.2</span><span class="sxs-lookup"><span data-stu-id="54f78-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="54f78-192">Zabezpieczenia (uruchamiania za pośrednictwem dotnet.exe lub mono.exe) — obj folder należy utworzyć z odpowiednimi uprawnieniami [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="54f78-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="54f78-193">Przywracanie nuget.exe dla platformy mono/MacOS kończy się niepowodzeniem z niestandardowego pliku nuget.config i `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="54f78-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="54f78-194">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="54f78-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="54f78-195">Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="54f78-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="54f78-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="54f78-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="54f78-197">Problem</span><span class="sxs-lookup"><span data-stu-id="54f78-197">Issue</span></span>
<span data-ttu-id="54f78-198">Korzystając z dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych.</span><span class="sxs-lookup"><span data-stu-id="54f78-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="54f78-199">Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="54f78-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="54f78-200">Obejście</span><span class="sxs-lookup"><span data-stu-id="54f78-200">Workaround</span></span>
<span data-ttu-id="54f78-201">Wyłącz użycie folderu rezerwowy, ustawiając `RestoreAdditionalProjectSources` na wartość nothing:</span><span class="sxs-lookup"><span data-stu-id="54f78-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="54f78-202">Korzystaj z niej ostrożnie jak pakiety, które zostaną przywrócone z folderu rezerwowego teraz zostaną pobrane z witryny NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="54f78-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
