---
title: Informacje o wersji NuGet 5.0 RTM
description: Informacje o wersji dla programu NuGet 5.0, w tym znane problemy, poprawki usterek, nowe funkcje i kontrolery domeny.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901749"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="f3414-103">Informacje o wersji nuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="f3414-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="f3414-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="f3414-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f3414-105">Wersja nuGet</span><span class="sxs-lookup"><span data-stu-id="f3414-105">NuGet version</span></span> | <span data-ttu-id="f3414-106">Dostępne w Visual Studio wersji</span><span class="sxs-lookup"><span data-stu-id="f3414-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f3414-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="f3414-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f3414-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="f3414-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f3414-109">Visual Studio 2019 w wersji 16.0</span><span class="sxs-lookup"><span data-stu-id="f3414-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f3414-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="f3414-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="f3414-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="f3414-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f3414-112">Visual Studio 2019 w wersji 16.0.4</span><span class="sxs-lookup"><span data-stu-id="f3414-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f3414-113">[2.1.60x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.20x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="f3414-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="f3414-114"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 z obciążeniem .NET Core</span><span class="sxs-lookup"><span data-stu-id="f3414-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="f3414-115"><sup>2.</sup> Dostępna jako instalacja opcjonalna w programie Visual Studio 2019 z obciążeniem .NET Core</span><span class="sxs-lookup"><span data-stu-id="f3414-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="f3414-116">Podsumowanie: co nowego w 5.0</span><span class="sxs-lookup"><span data-stu-id="f3414-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="f3414-117">Obsługa przywracania [filtrowanych rozwiązań w](/visualstudio/ide/filtered-solutions) programie Visual Studio 2019 — [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="f3414-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="f3414-118">`BuildTransitive` folder umożliwia pakietom przechodnie współtwoście obiektów docelowych/propek w projekcie hosta [— #6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="f3414-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="f3414-119">Lepsza obsługa scenariuszy PackageReference w interfejsach API pakietów NuGet IVs [— #7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="f3414-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="f3414-120">`nuget.exe pack project.json` jest przestarzała [— #7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="f3414-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="f3414-121">Wtyczka gen 1 Dostawca poświadczeń została zastąpiona przez gen [2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) i wkrótce zostanie wycofana [—](https://github.com/NuGet/Home/issues/7819) #7819</span><span class="sxs-lookup"><span data-stu-id="f3414-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f3414-122">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="f3414-122">Issues fixed in this release</span></span>

<span data-ttu-id="f3414-123">**Błędów**</span><span class="sxs-lookup"><span data-stu-id="f3414-123">**Bugs**</span></span>

* <span data-ttu-id="f3414-124">Podczas wykonywania przywracania NoOp należy unikać \*.dgspec.jszapisu w katalogu obj — [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="f3414-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="f3414-125">Uprawnienia do plików utworzonych w pliku ~/.nuget są zbyt otwarte [— #7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="f3414-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="f3414-126">`dotnet list package --outdated` nie działa ze źródłami, które wymagają uwierzytelniania [— #7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="f3414-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="f3414-127">NuGet.VisualStudio.IVsPackageInstaller — wywoływanie w projekcie bez odwołań do pakietu zawsze używa packages.config, nawet jeśli wartość domyślna to PackageReference — [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="f3414-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="f3414-128">PMC: Update-Package ponownej instalacji nie powiedzie się ("Nie można odnaleźć pakietu") w pakietach wywłaszowanych.</span><span class="sxs-lookup"><span data-stu-id="f3414-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="f3414-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="f3414-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="f3414-130">Dodawanie powiadomienia innej firmy w naszym repo i VSIX — [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="f3414-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="f3414-131">Pakiet NuGet.VisualStudio.IVsPackageInstaller.InstallPackage powinien zostać zainstalowany w najnowszej wersji, jeśli nie podano wersji — [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="f3414-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="f3414-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="f3414-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="f3414-133">Podczas przywracania przy użyciu pliku blokady nie powinno być wyświetlane ostrzeżenie NU1603.</span><span class="sxs-lookup"><span data-stu-id="f3414-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="f3414-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="f3414-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="f3414-135">Program NuGet nie powinien drukować ścieżki projektu podczas przywracania przy minimalnym rejestrowaniu [— #7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="f3414-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="f3414-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="f3414-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="f3414-137">Dodaj ponownie element NuGet.Packaging.Core z elementem TypeForwardedTo attrs — [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="f3414-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="f3414-138">plugins_cache wymaga krótszej ścieżki do pracy — [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="f3414-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="f3414-139">Preferuj ścieżkę odnajdywania msbuild, jeśli użytkownik nie prosił o określoną wersję programu msbuild — [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="f3414-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="f3414-140">`nuget.exe /?` Powinien wyświetlić listę poprawnych wersji programu msbuild [— #7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="f3414-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="f3414-141">NuGet.targets(498,5): błąd: Nie można odnaleźć części ścieżki '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="f3414-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="f3414-142">Przywróć niepotrzebnie wylicza zawartość wszystkich wersji przywoływanego pakietu w pamięci podręcznej maszyny [—](https://github.com/NuGet/Home/issues/7639) #7639</span><span class="sxs-lookup"><span data-stu-id="f3414-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="f3414-143">Automatyczne wykrywanie w programie MSBuild zawsze wybiera 16.0 po zainstalowaniu programu VS 2019 (wersja [zapoznawcza)](https://github.com/NuGet/Home/issues/7621) — #7621</span><span class="sxs-lookup"><span data-stu-id="f3414-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="f3414-144">Dotnet list package on a solution outputs duplicate entries for framework - #7607 (Pakiet dotnet list rozwiązania wyprowadza zduplikowane wpisy dla struktury [— #7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="f3414-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="f3414-145">Wyjątek "Pusta nazwa ścieżki nie jest legalna" podczas wywoływania funkcji IVsPackageInstaller.InstallPackage w starych projektach i folderze pakietów nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f3414-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="f3414-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="f3414-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="f3414-147">Msbuild /t:restore minimalny poziom szczegółowości powinien być bardziej minimalny — [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="f3414-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="f3414-148">Interfejs użytkownika nuGet programu VS 16.0 ma nieczytelne karty z powodu problemów z kolorami [—](https://github.com/NuGet/Home/issues/7735) #7735</span><span class="sxs-lookup"><span data-stu-id="f3414-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="f3414-149">Wyjaśnienie License.txt NuGet.Core & NuGet.Clients — [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="f3414-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="f3414-150">Przywróć niepotrzebnie wylicza globalny folder pakietu w celu określenia typu [—](https://github.com/NuGet/Home/issues/7596) #7596</span><span class="sxs-lookup"><span data-stu-id="f3414-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="f3414-151">Błędy z wymuszania pliku blokady powinny być wyświetlane w oknie lista błędów [— #7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="f3414-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="f3414-152">Rozwiązywanie NuGet.Configproblemów z adresami [URL — #7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="f3414-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="f3414-153">Dostosowanie do aktualizacji lokalizacji instalacji programu MSBuild — [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="f3414-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="f3414-154">Pakiet NuGet.Build.Tasks.Pack powinien być zależnością deweloperska [— #7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="f3414-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="f3414-155">Dodawanie punktu rozszerzenia pakietu w celu uwzględnienia symboli debugowania [— #7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="f3414-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="f3414-156">`dotnet pack` należy zachować zakres wersji zależności w utworzonym nupkg (nawet jeśli jest używana wersja zmiennoprzecinkowa) — [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="f3414-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="f3414-157">`dotnet restore` kończy się niepowodzeniem w uwierzytelnionym źródle, gdy konfiguracja na poziomie użytkownika również ma [źródło — #7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="f3414-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="f3414-158">Pakiet nie powinien ograniczać zestawu akcji BuildAction dla plików zawartości [— #7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="f3414-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="f3414-159">W przypadku użycia składnika ProjectReference, które wymaga powodzenia funkcji AssetTargetFallback, należy ostrzec.</span><span class="sxs-lookup"><span data-stu-id="f3414-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="f3414-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="f3414-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="f3414-161">Zakleszczenie z powodu problemów z wątkami podczas wywoływania do systemu CPS (CommonProjectSystem) [— #7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="f3414-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="f3414-162">`dotnet add package` nie używa poświadczeń z konfiguracji globalnej dla źródła określonego w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="f3414-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="f3414-163">Problemy z wątkami dotyczące wywoływania mef w asynchronicznych ścieżkach kodu [— #6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="f3414-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="f3414-164">Podpisywanie: błąd zgłoszony dwukrotnie i bez stosu wywołań [— #6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="f3414-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="f3414-165">Instalowanie podpisanego pakietu z niezaufanymi certyfikatami podpisywania powinno pokazywać błąd [— #6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="f3414-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="f3414-166">Nieprawidłowe przywracanie NuGet NoOps, gdy 2 projekty współużytkują katalog obj — [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="f3414-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="f3414-167">Nie można użyć patu dostępu z `dotnet restore` w systemie Linux z pakietami z uwierzytelnionego źródła danych — [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="f3414-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="f3414-168">dotnet restore kończy się niepowodzeniem z powodu wyłączenia szerokiego źródła danych komputera [— #5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="f3414-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="f3414-169">**DcRs (Kontrolery domeny)**</span><span class="sxs-lookup"><span data-stu-id="f3414-169">**DCRs**</span></span>

* <span data-ttu-id="f3414-170">Ostrzeganie o przyszłym usunięciu "pakietu dotnet project.jssię" — [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="f3414-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="f3414-171">Dodawanie ostrzeżenia o cofaniu pracy dla wtyczki poświadczeń Gen1 [— #7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="f3414-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="f3414-172">Podpisywanie: włączone repozytorium, aby wymagać weryfikacji klienta każdego pakietu jako podpisanego repozytorium — za pośrednictwem zasobu RepositorySignatures/5.0.0 [—](https://github.com/NuGet/Home/issues/7759) #7759</span><span class="sxs-lookup"><span data-stu-id="f3414-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="f3414-173">ograniczanie liczby żądań HTTP na źródło za pośrednictwem NuGet.Config — [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="f3414-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="f3414-174">Program NuGet powinien być ukierunkowany na net472 (aby ułatwić oczyszczanie kompilacji 16.0 vsix) [— #7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="f3414-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="f3414-175">PMC: polecenie Remove OpenPackagePage — [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="f3414-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="f3414-176">Mapowanie aplikacji NetCoreApp 3.0 na netStandard 2.1 [— #7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="f3414-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="f3414-177">Dodanie obsługi netstandard2.0 do pakietów NuGet.\* — [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="f3414-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="f3414-178">Zezwalaj autorom pakietów na definiowanie zachowania przechodniego zasobów kompilacji [— #6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="f3414-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="f3414-179">Obsługa funkcji filtru rozwiązań programu VS 2019.</span><span class="sxs-lookup"><span data-stu-id="f3414-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="f3414-180">Obsługuje również projekt, który nie znajduje się w rozwiązaniu, lub niezaładowane projekty.</span><span class="sxs-lookup"><span data-stu-id="f3414-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="f3414-181">Najpierw należy przywrócić kompletne rozwiązanie (za pośrednictwem interfejsu wiersza polecenia lub programu VS) [— #5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="f3414-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="f3414-182">Zestawy NuGet 5.0 wymagające programu .NET 4.7.2 (za pośrednictwem zmiany tfm) [— #7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="f3414-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="f3414-183">NuGetLicenseData z nuGet.Packaging powinien być typem publicznym.</span><span class="sxs-lookup"><span data-stu-id="f3414-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="f3414-184">Aktualizowanie metadanych licencji pozyskanych z pliku spdx.</span><span class="sxs-lookup"><span data-stu-id="f3414-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="f3414-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="f3414-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="f3414-186">Usuwanie przestarzałych interfejsów API ustawień [— #7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="f3414-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="f3414-187">Obejście limitów czasu przywracania w systemach z 1 procesorem CPU [— #6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="f3414-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="f3414-188">NuGet preferuje uwierzytelnianie NTLM, nawet jeśli istnieją poświadczenia w NuGet.config — dodaj opcję konfiguracji, aby filtrować typy uwierzytelniania dla poświadczeń — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="f3414-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="f3414-189">Włączanie wartości EmbedInteropTypes dla funkcji PackageReference (dopasowywanie Packages.Config) — [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="f3414-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="f3414-190">**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="f3414-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="f3414-191">Podsumowanie: co nowego w 5.0.2</span><span class="sxs-lookup"><span data-stu-id="f3414-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="f3414-192">Zabezpieczenia (uruchamiane za pośrednictwem dotnet.exe lub mono.exe) — folder obj powinien [](https://github.com/NuGet/Home/issues/7908) zostać utworzony z prawidłowymi uprawnieniami #7908</span><span class="sxs-lookup"><span data-stu-id="f3414-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="f3414-193">nuget.exe przywracania w systemie mono/MacOS kończy się niepowodzeniem z niestandardowymi nuget.config i `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="f3414-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="f3414-194">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="f3414-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="f3414-195">Pakiety w programie FallbackFolders zainstalowane przez zestaw .NET Core SDK są instalowane niestandardowo i walidacja podpisu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="f3414-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="f3414-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="f3414-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="f3414-197">Problem</span><span class="sxs-lookup"><span data-stu-id="f3414-197">Issue</span></span>
<span data-ttu-id="f3414-198">W przypadku dotnet.exe 2.x w celu przywrócenia projektu, który zawiera wielo targets netcoreapp 1.x i netcoreapp 2.x, folder rezerwowy jest traktowany jako źródło danych plików.</span><span class="sxs-lookup"><span data-stu-id="f3414-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="f3414-199">Oznacza to, że podczas przywracania program NuGet wybierze pakiet z folderu rezerwowego i spróbuje go zainstalować w globalnym folderze pakietów i przejmie standardową walidację podpisywania, co zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="f3414-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="f3414-200">Obejście</span><span class="sxs-lookup"><span data-stu-id="f3414-200">Workaround</span></span>
<span data-ttu-id="f3414-201">Wyłącz użycie folderu rezerwowego, ustawiając dla opcji `RestoreAdditionalProjectSources` wartości nothing:</span><span class="sxs-lookup"><span data-stu-id="f3414-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="f3414-202">Należy zachować ostrożność, ponieważ pakiety, które zostaną przywrócone z folderu rezerwowego, zostaną teraz pobrane z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f3414-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>