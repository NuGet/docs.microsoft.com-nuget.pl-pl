---
title: Informacje o wersji narzędzia NuGet 5,0 RTM
description: Informacje o wersji programu NuGet 5,0, w tym znane problemy, poprawki błędów, nowe funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 52c71c6fe1a1854d5aed229abf2ce7ddc2685ae9
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611338"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="e4cc0-103">Informacje o wersji narzędzia NuGet 5,0</span><span class="sxs-lookup"><span data-stu-id="e4cc0-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="e4cc0-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="e4cc0-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e4cc0-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="e4cc0-105">NuGet version</span></span> | <span data-ttu-id="e4cc0-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e4cc0-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e4cc0-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="e4cc0-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e4cc0-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="e4cc0-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e4cc0-109">Visual Studio 2019 w wersji 16,0</span><span class="sxs-lookup"><span data-stu-id="e4cc0-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e4cc0-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e4cc0-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="e4cc0-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="e4cc0-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e4cc0-112">Visual Studio 2019 w wersji 16.0.4</span><span class="sxs-lookup"><span data-stu-id="e4cc0-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e4cc0-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e4cc0-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="e4cc0-114"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="e4cc0-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="e4cc0-115"><sup>2</sup> Dostępne jako opcjonalna instalacja z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="e4cc0-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="e4cc0-116">Podsumowanie: co nowego w 5,0</span><span class="sxs-lookup"><span data-stu-id="e4cc0-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="e4cc0-117">Obsługa przywracania [filtrowanych rozwiązań](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019) w programie Visual Studio 2019 — [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-117">Support for restoring [filtered solutions](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="e4cc0-118">folder `BuildTransitive` umożliwia pakietom przechodnie Współtworzenie elementów docelowych/props do projektu hosta — [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="e4cc0-119">Lepsza obsługa scenariuszy PackageReference w interfejsach API NuGet użycie japońskich ideograficznych — [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="e4cc0-120">`nuget.exe pack project.json` przestarzałe — [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="e4cc0-121">Wtyczka dostawcy poświadczeń generacji 1 została zastąpiona przez [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) i wkrótce będzie przestarzała — [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e4cc0-122">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="e4cc0-122">Issues fixed in this release</span></span>

<span data-ttu-id="e4cc0-123">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="e4cc0-123">**Bugs**</span></span>

* <span data-ttu-id="e4cc0-124">Podczas wykonywania operacji przywracania aktualizujący nie działa należy unikać zapisu \*. dgspec. JSON w katalogu obj- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="e4cc0-125">Uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="e4cc0-126">`dotnet list package --outdated` nie działa ze źródłami wymagającymi uwierzytelniania [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="e4cc0-127">Pakiet NuGet. VisualStudio. IVsPackageInstaller — wywoływanie w projekcie bez odwołań do pakietów zawsze używa pliku Packages. config, nawet jeśli ustawieniem domyślnym jest PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="e4cc0-128">PMC: Aktualizacja pakietu aktualizacji nie powiodła się ("nie można znaleźć pakietu") w odniesieniu do pakietów z listą.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="e4cc0-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="e4cc0-130">Dodaj powiadomienie innej firmy w naszym repozytorium i VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="e4cc0-131">Pakiet NuGet. VisualStudio. IVsPackageInstaller. InstallPackage powinien instalować najnowszą wersję, gdy nie podaną w wersji — [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="e4cc0-132">--Interaktywna obsługa wypychania NuGet programu dotnet- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="e4cc0-133">Podczas przywracania przy użyciu pliku blokady nie należy zgłaszać ostrzeżenia NU1603.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="e4cc0-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="e4cc0-135">Pakiet NuGet nie powinien drukować ścieżki projektu podczas przywracania przy minimalnym rejestrowaniu — [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="e4cc0-136">--Interaktywna pomoc techniczna dotycząca usuwania pakietu dotnet- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="e4cc0-137">Dodaj wstecz NuGet. pakowanie. Core z TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="e4cc0-138">plugins_cache potrzebuje krótszej ścieżki do prawidłowego działania [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="e4cc0-139">Preferuj ścieżkę dla odnajdywania MSBuild, jeśli użytkownik nie poprosił o określoną wersję programu MSBuild — [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="e4cc0-140">`nuget.exe /?` powinna wyświetlać poprawne wersje programu MSBuild — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="e4cc0-141">NuGet. targets (498, 5): błąd: nie można odnaleźć części ścieżki "/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="e4cc0-142">przywrócenie niepotrzebnie wylicza zawartość wszystkich wersji pakietu, do którego istnieje odwołanie w pamięci podręcznej maszyn — [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="e4cc0-143">Funkcja automatycznego wykrywania programu MSBuild zawsze wybiera 16,0 po zainstalowaniu programu VS 2019 w wersji zapoznawczej — [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="e4cc0-144">pakiet listy dotnet w rozwiązaniu wyprowadza zduplikowane wpisy dla struktury — [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="e4cc0-145">Wyjątek "pusta nazwa ścieżki nie jest dozwolona" podczas wywoływania IVsPackageInstaller. InstallPackage w starych projektach i folderze Packages nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="e4cc0-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="e4cc0-147">MSBuild/t: Przywróć minimalny poziom szczegółowości powinien być bardziej minimalny- [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="e4cc0-148">Interfejs użytkownika NuGet programu VS 16.0 zawiera nieczytelne karty z powodu problemów z kolorem — [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="e4cc0-149">NuGet. Core & NuGet. klienci — wyjaśnienie licencji. txt — [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="e4cc0-150">Przywrócenie niekoniecznie wylicza folder pakietu globalnego podczas próby określenia typu [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="e4cc0-151">Błędy wymuszania blokady plików powinny być wyświetlane w Lista błędów oknie [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="e4cc0-152">Napraw pakiet NuGet. problemy z konfiguracją — [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="e4cc0-153">Dostosuj do programu MSBuild, aktualizując jego lokalizację instalacji — [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="e4cc0-154">NuGet. Build. Tasks. Pack musi być zależnością programistyczną — [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="e4cc0-155">Dodaj punkt rozszerzenia pakietu dla dołączania symboli debugowania — [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="e4cc0-156">`dotnet pack` powinna zachować zakres wersji zależności w utworzonym NUPKG (nawet jeśli używana jest wersja przestawna) — [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="e4cc0-157">`dotnet restore` nie powiodło się w przypadku uwierzytelnionego źródła, jeśli konfiguracja na poziomie użytkownika ma także [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="e4cc0-158">Pakiet nie powinien ograniczać zestawu BuildActions dla plików zawartości — [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="e4cc0-159">Przy użyciu elementu ProjectReference, który wymaga pomyślnego AssetTargetFallback, powinno być wyświetlane ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="e4cc0-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="e4cc0-161">Zakleszczenie ze względu na problemy z wątkami podczas wywoływania metody CPS (CommonProjectSystem) — [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="e4cc0-162">`dotnet add package` nie używa poświadczeń z konfiguracji globalnej dla źródła określonego w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="e4cc0-163">Problemy z wątkami z MEFem wywoływane w asynchronicznych ścieżkach kodu — [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="e4cc0-164">Podpisywanie: zgłoszono błąd dwukrotnie i bez stosu wywołań — [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="e4cc0-165">W przypadku instalowania pakietu podpisanego z niezaufanym certyfikatem podpisywania powinien zostać wyświetlony komunikat o błędzie [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="e4cc0-166">Przywracanie NuGet nie NoOps prawidłowo, gdy 2 projekty współużytkują katalog obj- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="e4cc0-167">Nie można użyć źródła danych z `dotnet restore` w systemie Linux z pakietami ze uwierzytelnionego kanału informacyjnego — [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="e4cc0-168">dotnet restore nie powiodło się z powodu wyłączenia kanału informacyjnego całego komputera — [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="e4cc0-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="e4cc0-169">**DCRs**</span></span>

* <span data-ttu-id="e4cc0-170">Ostrzegaj o przyszłym usunięciu elementu "dotnet Pack Project. JSON" — [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="e4cc0-171">Dodaj ostrzeżenie o zaniechaniu wtyczki poświadczeń Gen1 — [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="e4cc0-172">Podpisywanie: włączone repozytorium, aby wymagać weryfikacji klienta każdego pakietu jako podpisanego przez repozytorium — za pośrednictwem RepositorySignatures/5.0.0 zasobu — [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="e4cc0-173">Ogranicz liczbę żądań HTTP na źródło za pośrednictwem pliku NuGet. config — [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="e4cc0-174">Pakiet NuGet powinien wskazywać Net472 (aby ułatwić czyszczenie kompilacji 16,0 w VSIX) — [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="e4cc0-175">PMC: usuwanie OpenPackagePage polecenia [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="e4cc0-176">Tworzenie mapy NetCoreApp 3,0 w programie Standard 2,1 — [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="e4cc0-177">Dodaj obsługę programu Standard 2.0 do pakietu NuGet. \* pakiety — [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="e4cc0-178">Zezwalaj autorom pakietów na definiowanie zachowania przechodniego zasobów kompilacji — [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="e4cc0-179">Obsługa funkcji filtrowania rozwiązań VS 2019.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="e4cc0-180">Program obsługuje również projekty, które nie są w rozwiązaniu lub nie zostały zwolnione.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="e4cc0-181">Należy przywrócić kompletne rozwiązanie (za pomocą interfejsu wiersza polecenia lub VS) jako pierwsze [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="e4cc0-182">Zestawy NuGet 5,0 wymagające programu .NET 4.7.2 (za pośrednictwem zmiany TFM) — [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="e4cc0-183">NuGetLicenseData z NuGet. opakowanie powinno być typem publicznym.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="e4cc0-184">Aktualizowanie metadanych licencji pozyskanych z SPDX.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="e4cc0-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="e4cc0-186">Usuwanie przestarzałych ustawień API- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="e4cc0-187">Obejście limitów czasu przywracania w systemach z 1 [#6742](https://github.com/NuGet/Home/issues/6742) procesora CPU</span><span class="sxs-lookup"><span data-stu-id="e4cc0-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="e4cc0-188">Pakiet NuGet preferuje uwierzytelnianie NTLM, nawet jeśli istnieją poświadczenia w pliku NuGet. config — Dodaj opcję konfiguracji, aby filtrować typy uwierzytelniania dla poświadczeń — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="e4cc0-189">Włącz funkcję EmbedInteropTypes dla PackageReference (zgodna z pakietami Packages. config) — [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="e4cc0-190">**[Lista wszystkich problemów rozwiązanych w tym wydaniu — 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="e4cc0-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="e4cc0-191">Podsumowanie: co nowego w programie 5.0.2</span><span class="sxs-lookup"><span data-stu-id="e4cc0-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="e4cc0-192">Zabezpieczenia (w przypadku uruchamiania za pośrednictwem programu dotnet. exe lub mono. exe) — folder obj powinien zostać utworzony z prawidłowymi uprawnieniami [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="e4cc0-193">Przywracanie pliku NuGet. exe na platformie mono/MacOS kończy się niepowodzeniem z użyciem niestandardowych pakietów NuGet. config i `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="e4cc0-194">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="e4cc0-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="e4cc0-195">Pakiety w FallbackFolders zainstalowane przez zestaw .NET Core SDK są zainstalowane niestandardowo i nie można zweryfikować podpisu.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="e4cc0-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="e4cc0-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="e4cc0-197">Problem</span><span class="sxs-lookup"><span data-stu-id="e4cc0-197">Issue</span></span>
<span data-ttu-id="e4cc0-198">W przypadku korzystania z programu dotnet. exe 2. x w celu przywrócenia projektu, który ma wiele obiektów docelowych netcoreapp 1. x i netcoreapp 2. x, folder rezerwowy jest traktowany jako źródło plików.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="e4cc0-199">Oznacza to, że podczas przywracania program NuGet wybierze pakiet z folderu rezerwowego i spróbuje go zainstalować w folderze pakiety globalne i wykonać zwykłą weryfikację podpisywania, która kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="e4cc0-200">Obejście</span><span class="sxs-lookup"><span data-stu-id="e4cc0-200">Workaround</span></span>
<span data-ttu-id="e4cc0-201">Wyłącz użycie folderu rezerwowego, ustawiając dla `RestoreAdditionalProjectSources` wartość Nothing:</span><span class="sxs-lookup"><span data-stu-id="e4cc0-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="e4cc0-202">Należy to zrobić z ostrożnością, ponieważ pakiety, które zostałyby przywrócone z folderu rezerwowego, zostaną teraz pobrane z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e4cc0-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
