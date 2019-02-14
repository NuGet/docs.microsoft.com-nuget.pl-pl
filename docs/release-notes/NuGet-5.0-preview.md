---
title: Informacje o wersji zapoznawczej 5.0 pakietów NuGet
description: Informacje o wersji dotyczące wersji zapoznawczych NuGet w wersji 5.0 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247662"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="71c4f-103">Informacje o wersji programu NuGet 5.0 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="71c4f-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="71c4f-104">Wersje zapoznawcze NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="71c4f-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="71c4f-105">13 lutego 2019 - [NuGet w wersji 5.0 (wersja zapoznawcza) 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="71c4f-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="71c4f-106">23 stycznia 2019 - [NuGet w wersji 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="71c4f-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="71c4f-107">Podsumowanie: Co nowego w wersji zapoznawczej NuGet w wersji 5.0 3</span><span class="sxs-lookup"><span data-stu-id="71c4f-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="71c4f-108">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="71c4f-108">Issues fixed in this release</span></span> 

<span data-ttu-id="71c4f-109">**Błędy:**</span><span class="sxs-lookup"><span data-stu-id="71c4f-109">**Bugs:**</span></span>

* <span data-ttu-id="71c4f-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="71c4f-110">nuget.exe /?</span></span> <span data-ttu-id="71c4f-111">pomysłem jest wystawienie msbuild poprawne wersje — [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="71c4f-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="71c4f-112">NuGet.targets(498,5): błąd: Nie można odnaleźć części ścieżki "/ tmp/NuGetScratch — na mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="71c4f-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="71c4f-113">Przywracanie niepotrzebnie uwzględnia zawartość wszystkich wersji pakietu odwołanie w pamięci podręcznej maszyny — [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="71c4f-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="71c4f-114">Po instalacji programu VS 2019 r w wersji zapoznawczej — automatyczne wykrywanie MSBuild zawsze wybiera 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="71c4f-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="71c4f-115">DotNet wyświetlenia listy pakietów na rozwiązanie generuje zduplikowanych wpisów dla framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="71c4f-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="71c4f-116">Wyjątek "Nazwa pustej ścieżki jest niedozwolona" podczas wywoływania IVsPackageInstaller.InstallPackage na starym projektów, a następnie umieszcza folder nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="71c4f-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="71c4f-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="71c4f-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="71c4f-118">minimalny poziom szczegółowości MSBuild /t:restore powinny być mniejsze - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="71c4f-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="71c4f-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="71c4f-119">**DCRs**</span></span>

* <span data-ttu-id="71c4f-120">Umożliwia autorom pakietów do definiowania zachowania przechodnie zasoby kompilacji - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="71c4f-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="71c4f-121">Włączanie funkcji przywracania w programie VS się powieść, jeśli projekt nie jest częścią rozwiązania lub nie jest załadowany, ale została wcześniej przywrócona - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="71c4f-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="71c4f-122">Podsumowanie: Co nowego w wersji 5.0 2</span><span class="sxs-lookup"><span data-stu-id="71c4f-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="71c4f-123">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="71c4f-123">Issues fixed in this release</span></span>

<span data-ttu-id="71c4f-124">**Błędy:**</span><span class="sxs-lookup"><span data-stu-id="71c4f-124">**Bugs:**</span></span>

* <span data-ttu-id="71c4f-125">VS firmy 16.0 NuGet interfejsu użytkownika ma nie można go odczytać karty z powodu problemów z kolorem - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="71c4f-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="71c4f-126">NuGet.Core & wyjaśnienie NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="71c4f-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="71c4f-127">Przywracanie niepotrzebnie uwzględnia folderu pakietu globalne próbę określenia typu — [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="71c4f-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="71c4f-128">Błędy z wymuszania pliku blokady powinny być teraz widoczne w oknie Lista błędów - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="71c4f-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="71c4f-129">Rozwiązywanie problemów z NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="71c4f-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="71c4f-130">Dostosowanie do aktualizowania MSBuild go w lokalizacji instalacji.</span><span class="sxs-lookup"><span data-stu-id="71c4f-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="71c4f-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="71c4f-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="71c4f-132">NuGet.Build.Tasks.Pack powinny być zależnością programistyczną - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="71c4f-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="71c4f-133">Dodaj pakiet rozszerzenia punktu, w tym debugowania symbole - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="71c4f-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="71c4f-134">pakietu DotNet powinno zachować zależności zakres wersji w nupkg utworzony.</span><span class="sxs-lookup"><span data-stu-id="71c4f-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="71c4f-135">(nawet jeśli jest używana wersja zmiennoprzecinkowego) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="71c4f-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="71c4f-136">DotNet restore kończy się niepowodzeniem w źródle uwierzytelnionego podczas konfiguracji na poziomie użytkownika ma również źródłem — [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="71c4f-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="71c4f-137">Pakiet, nie należy ograniczyć zestaw BuildActions dla plików zawartości — [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="71c4f-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="71c4f-138">Za pomocą elementu projectreference, co wymaga AssetTargetFallback została wykonana pomyślnie, należy ostrzec.</span><span class="sxs-lookup"><span data-stu-id="71c4f-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="71c4f-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="71c4f-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="71c4f-140">Zakleszczenie spowodowane wątkowości problemy podczas wywoływania w systemie CPS (CommonProjectSystem) — [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="71c4f-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="71c4f-141">polecenia DotNet Dodaj pakiet nie używać poświadczeń z globalnej konfiguracji dla źródła, określony w konfiguracji lokalnej — [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="71c4f-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="71c4f-142">Wątkowość problemy związane z MEF jest wywoływana dla ścieżek codepath async - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="71c4f-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="71c4f-143">Podpisywania: zgłoszony dwa razy i bez stosu wywołań — błąd [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="71c4f-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="71c4f-144">Instalowanie pakietu podpisane za pomocą niezaufanego certyfikatu podpisywania powinien zostać wyświetlony błąd - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="71c4f-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="71c4f-145">Przywracanie NuGet nieprawidłowo NoOps podczas udostępniania katalogu - 2 projektów [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="71c4f-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="71c4f-146">Nie można używać osobisty token dostępu z przywracania dotnet w systemie Linux przy użyciu pakietów uwierzytelnionego - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="71c4f-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="71c4f-147">DotNet restore kończy się niepowodzeniem z powodu wyłączenia maszyny szerokiego źródła danych — [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="71c4f-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="71c4f-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="71c4f-148">**DCRs**</span></span>

* <span data-ttu-id="71c4f-149">Zestawy NuGet w wersji 5.0, będą musieli .NET 4.7.2 (za pośrednictwem elementu TFM zmiana) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="71c4f-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="71c4f-150">NuGetLicenseData z NuGet.Packaging powinien być typem publicznym.</span><span class="sxs-lookup"><span data-stu-id="71c4f-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="71c4f-151">Zaktualizuj metadane licencji pozyskanych z spdx.</span><span class="sxs-lookup"><span data-stu-id="71c4f-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="71c4f-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="71c4f-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="71c4f-153">Usuń przestarzałe ustawienia interfejsy API — [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="71c4f-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="71c4f-154">Obejście problemu Przywróć przekroczeń limitu czasu w systemach z 1 procesor cpu — [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="71c4f-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="71c4f-155">NuGet preferuje uwierzytelniania NTLM, nawet jeśli występują poświadczenia w pliku NuGet.config — dodaj opcję konfiguracji do filtrowania typów uwierzytelniania, aby uzyskać poświadczenia — [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="71c4f-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="71c4f-156">Włącz EmbedInteropTypes dla funkcji PackageReference (pasującego pliku Packages.Config możliwość) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="71c4f-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="71c4f-157">Lista wszystkie problemy rozwiązane w tej wersji 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="71c4f-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="71c4f-158">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="71c4f-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="71c4f-159">DotNet nuget push--interaktywne powoduje błąd na komputerze Mac.</span><span class="sxs-lookup"><span data-stu-id="71c4f-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="71c4f-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="71c4f-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="71c4f-161">**Problem** `--interactive` argument nie są przekazywane przez interfejs wiersza polecenia platformy dotnet i powoduje błąd `error: Missing value for option 'interactive'` 
 **obejście** uruchamiania dowolnego polecenia dotnet z opcją interaktywnych, takich jak `dotnet restore --interactive` i uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="71c4f-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="71c4f-162">Uwierzytelnianie, program może być buforowane przez dostawcę poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="71c4f-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="71c4f-163">Następnie uruchom `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="71c4f-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="71c4f-164">Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="71c4f-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="71c4f-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="71c4f-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="71c4f-166">**Problem** przy użyciu dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych.</span><span class="sxs-lookup"><span data-stu-id="71c4f-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="71c4f-167">Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="71c4f-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="71c4f-168">**Obejście** wyłączyć użycie folderu rezerwowego przez ustawienie `RestoreAdditionalProjectSources` na wartość nothing.</span><span class="sxs-lookup"><span data-stu-id="71c4f-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="71c4f-169">`<RestoreAdditionalProjectSources/>` Korzystanie z rozwagą, ponieważ spowoduje to wiele pakietów, które mają być pobrane z repozytorium NuGet.org, które w przeciwnym razie byłoby zostały przywrócone z folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="71c4f-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
