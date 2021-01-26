---
title: Informacje o wersji narzędzia NuGet 4,0 RTM
description: Informacje o wersji dla programu NuGet 4,0 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c3ec5c20e5175edd315de20ca98c7a106c51809e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776277"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="2eb47-103">Informacje o wersji narzędzia NuGet 4,0 RTM</span><span class="sxs-lookup"><span data-stu-id="2eb47-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="2eb47-104">[Program Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z pakietem NuGet 4,0, który dodaje obsługę platformy .NET Core, ma wiele poprawek dotyczących jakości i poprawia wydajność.</span><span class="sxs-lookup"><span data-stu-id="2eb47-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="2eb47-105">W tej wersji wprowadzono również kilka ulepszeń, takich jak obsługa PackageReference, poleceń NuGet jako obiektów docelowych programu MSBuild, przywrócenie pakietu w tle i nie tylko.</span><span class="sxs-lookup"><span data-stu-id="2eb47-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="2eb47-106">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="2eb47-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="2eb47-107">Przywracanie pakietów NuGet może się nie powieść, jeśli masz wiele projektów odwołujących się do innego projektu w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="2eb47-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-108">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-108">Issue</span></span>

<span data-ttu-id="2eb47-109">Przywracanie pakietów NuGet może nie działać, jeśli w rozwiązaniu istnieją odwołania do projektu do tego samego projektu z inną wielkością liter lub innymi ścieżkami względnymi.</span><span class="sxs-lookup"><span data-stu-id="2eb47-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="2eb47-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="2eb47-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="2eb47-111">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-111">Workaround</span></span>

<span data-ttu-id="2eb47-112">Napraw wielkość liter lub ścieżki względne w taki sposób, aby były takie same dla wszystkich odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="2eb47-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="2eb47-113">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="2eb47-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-114">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-114">Issue</span></span>

<span data-ttu-id="2eb47-115">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2eb47-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="2eb47-116">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="2eb47-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="2eb47-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="2eb47-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="2eb47-118">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-118">Workaround</span></span>

<span data-ttu-id="2eb47-119">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2eb47-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="2eb47-120">Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.</span><span class="sxs-lookup"><span data-stu-id="2eb47-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="2eb47-121">W projektach .NET Core użytkownik może pozostać w pętli nieskończonej przywracania w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem</span><span class="sxs-lookup"><span data-stu-id="2eb47-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-122">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-122">Issue</span></span>

<span data-ttu-id="2eb47-123">Czasami, w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie uruchamiane w pętli nieskończonej.</span><span class="sxs-lookup"><span data-stu-id="2eb47-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="2eb47-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="2eb47-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="2eb47-125">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-125">Workaround</span></span>

<span data-ttu-id="2eb47-126">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="2eb47-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="2eb47-127">Nie można wyświetlać, dodawać ani aktualizować składnika dotnetclitools przy użyciu Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="2eb47-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-128">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-128">Issue</span></span>

<span data-ttu-id="2eb47-129">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="2eb47-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="2eb47-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="2eb47-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="2eb47-131">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-131">Workaround</span></span>

<span data-ttu-id="2eb47-132">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="2eb47-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="2eb47-133">Przywracanie NuGet zakończy się niepowodzeniem po ustawieniu właściwości PackageId dla projektów</span><span class="sxs-lookup"><span data-stu-id="2eb47-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-134">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-134">Issue</span></span>

<span data-ttu-id="2eb47-135">Dla projektów .NET Core funkcja przywracania NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów.</span><span class="sxs-lookup"><span data-stu-id="2eb47-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="2eb47-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="2eb47-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="2eb47-137">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-137">Workaround</span></span>

<span data-ttu-id="2eb47-138">Uruchom przywracanie przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2eb47-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="2eb47-139">Gdy projekt nie ma folderu „obj”, przywracanie pakietu może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="2eb47-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-140">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-140">Issue</span></span>

<span data-ttu-id="2eb47-141">Program Visual Studio nie może przywrócić składnika PackageReferences, jeśli folder „obj” został usunięty.</span><span class="sxs-lookup"><span data-stu-id="2eb47-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="2eb47-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="2eb47-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="2eb47-143">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-143">Workaround</span></span>

<span data-ttu-id="2eb47-144">Gdy utworzysz folder „obj” ręcznie, funkcja przywracania powinna zadziałać.</span><span class="sxs-lookup"><span data-stu-id="2eb47-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="2eb47-145">Ręczna aktualizacja pakietów przy użyciu pakietu aktualizacji w konsoli może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="2eb47-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-146">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-146">Issue</span></span>

<span data-ttu-id="2eb47-147">Ręczne użycie pakietu aktualizacji w konsoli działa tylko jeden raz dla projektów PackageReferences, które zostały właśnie przekonwertowane.</span><span class="sxs-lookup"><span data-stu-id="2eb47-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="2eb47-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="2eb47-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="2eb47-149">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-149">Workaround</span></span>

<span data-ttu-id="2eb47-150">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="2eb47-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="2eb47-151">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="2eb47-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-152">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-152">Issue</span></span>

<span data-ttu-id="2eb47-153">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2eb47-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="2eb47-154">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2eb47-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="2eb47-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="2eb47-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="2eb47-156">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-156">Workaround</span></span>

<span data-ttu-id="2eb47-157">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="2eb47-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="2eb47-158">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt przeznaczony dla platformy .NET461 odwołuje się do innego projektu przeznaczonego dla platformy .NETStandard</span><span class="sxs-lookup"><span data-stu-id="2eb47-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="2eb47-159">Problem</span><span class="sxs-lookup"><span data-stu-id="2eb47-159">Issue</span></span>

<span data-ttu-id="2eb47-160">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt oparty na składniku PackageReferenece przeznaczony dla platformy .NET461 odwołuje się do innego projektu opartego na składniku PackageReference przeznaczonego dla platformy .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="2eb47-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="2eb47-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="2eb47-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="2eb47-162">Obejście</span><span class="sxs-lookup"><span data-stu-id="2eb47-162">Workaround</span></span>

<span data-ttu-id="2eb47-163">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="2eb47-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="2eb47-164">Problemy rozwiązane w przedziale czasu NuGet 4,0 RTM</span><span class="sxs-lookup"><span data-stu-id="2eb47-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="2eb47-165">[Informacje o wersji programu nuget 4,0 RC](../release-notes/nuget-4.0-RC.md) — zawiera listę wszystkich problemów rozwiązanych dla programu NuGet 4,0 RC</span><span class="sxs-lookup"><span data-stu-id="2eb47-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="2eb47-166">Funkcje</span><span class="sxs-lookup"><span data-stu-id="2eb47-166">Features</span></span>

- <span data-ttu-id="2eb47-167">Lokalizowanie ciągów w NuGet. Core. sln- [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="2eb47-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="2eb47-168">Siły NuGet do ładowania projektów aplikacji sieci Web w trybie SKRÓCONO — [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="2eb47-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="2eb47-169">Obsługa PackageReference, która blokuje zmiany wersji w interfejsie użytkownika dla pakietów "zainstalowane w zestawie SDK" — [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="2eb47-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="2eb47-170">Poprawnie komunikuj PackageSpec. Version dla dowolnych zależności projektu (PackageRef) — [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="2eb47-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="2eb47-171">obsługa usuwania odwołań do `.csproj` z wierszy polecenia — [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="2eb47-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="2eb47-172">Obsługa przywracania projektów PackageReference (normalne i Xplat) i uproszczonego ładowania rozwiązań — [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="2eb47-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="2eb47-173">Obsługa dodawania odwołań do `.csproj` z wiersza polecenia — [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="2eb47-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="2eb47-174">Obsługa przywracania NuGet na potrzeby uproszczonego ładowania rozwiązań dla programu `packages.config` lub `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="2eb47-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="2eb47-175">Obsługa contentFiles w pliku docelowych wygenerowanych przez narzędzie NuGet — [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="2eb47-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="2eb47-176">Ustanawianie elementu konfiguracji mono dla nuget.exe weryfikacji na komputerze Mac przy użyciu programu MSBuild — [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="2eb47-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="2eb47-177">Przenoszenie narzędzia NuGet z wersji 2 programu NuGet. zależności podstawowe — [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="2eb47-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="2eb47-178">Usterki</span><span class="sxs-lookup"><span data-stu-id="2eb47-178">Bugs</span></span>

- <span data-ttu-id="2eb47-179">Przywracanie NuGet w programie Visual Studio nie uwzględnia właściwości PackageId projektów — [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="2eb47-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="2eb47-180">Błąd narzędzia NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie VSIX — [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="2eb47-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="2eb47-181">Pakiet zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wieloma TFMs- [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="2eb47-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="2eb47-182">VS 2017 RC3 awarie przy użyciu aktualizacji z zarządzania pakietami w całym rozwiązaniu — [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="2eb47-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="2eb47-183">Nie można odinstalować nowo zainstalowanego pakietu — [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="2eb47-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="2eb47-184">W przypadku migrowania do PackageRef rozwiązania hybrydowe mają nietypowe zachowanie przywracania — [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="2eb47-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="2eb47-185">Kompilowanie wkrótce po uruchomieniu operacji NuGet (Install, Update, Restore), może spowodować zawieszenie [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="2eb47-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="2eb47-186">Zawieszanie zawieszenia interfejsu użytkownika podczas inicjowania NuGet. SolutionRestoreManager. RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="2eb47-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="2eb47-187">polecenie Dodaj pakiet powinno dodać wersję jako atrybut zamiast elementu [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="2eb47-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="2eb47-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-188">dotnet</span></span>
  - <span data-ttu-id="2eb47-189">dotnetcore Restore foo. sln--kończy się niepowodzeniem, jeśli konfiguracje w SLN powodują zduplikowane projekty (ale różnice konfiguracji) w programie Restore Graph- [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="2eb47-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="2eb47-190">Pakiety tylko zawartości — [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="2eb47-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="2eb47-191">Domyślnie zrezygnuj z opcji selektora formatu pakietu — [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="2eb47-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="2eb47-192">Wydajność: CreateUAP_CSharp_VS. 01.1. Create Project uległa pogorszeniu Duration_TotalElapsedTime o 3 153,570 MS (149,1%).</span><span class="sxs-lookup"><span data-stu-id="2eb47-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="2eb47-193">Linia bazowa 26129,02- [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="2eb47-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="2eb47-194">Wydajność: ManagedLangs_CS_DDRIT .0300. Rebuild rozwiązanie uległa pogorszeniu Duration_TotalElapsedTime o 1,5 sek.</span><span class="sxs-lookup"><span data-stu-id="2eb47-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="2eb47-195">Linia bazowa 26105- [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="2eb47-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="2eb47-196">Nominacja nie powiedzie się w projektach wieloTFMowych — [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="2eb47-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="2eb47-197">Wydajność: WebForms_DDRIT .1200. Zamknij rozwiązanie uległa pogorszeniu VM_ImagesInMemory_Total_devenv według liczby 3,000 (0,5%).</span><span class="sxs-lookup"><span data-stu-id="2eb47-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="2eb47-198">Linia bazowa 26123,04- [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="2eb47-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="2eb47-199">vsfeedback — ostrzeżenia dotyczące pakietów podczas określania wartości docelowej netcoreapp [#4397](https://github.com/NuGet/Home/issues/4397) 1.1</span><span class="sxs-lookup"><span data-stu-id="2eb47-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="2eb47-200">PathTooLongException podczas próby dodania pakietu NuGet do pustej ASP.NET Core aplikacji sieci Web — [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="2eb47-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="2eb47-201">Pakiet jest uruchamiany zbyt często — dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="2eb47-202">Pakiet dotnetcore kończy się niepowodzeniem, gdy istnieje zależność cykliczna w docelowym grafie zależności obejmująca element docelowy "Pack" — [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="2eb47-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="2eb47-203">Pakiet jest uruchamiany zbyt często — Generowanie pakietu NuGet nie obejmuje wszystkich konfiguracji — [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="2eb47-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="2eb47-204">NullReferenceException Dodawanie NuGet z packageref w projekcie C++ — [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="2eb47-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="2eb47-205">Ułatwienia dostępu: program Narrator nie narratoruje tego pola wyboru, aby wybrać projekty, do których ma zostać zainstalowany pakiet- [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="2eb47-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="2eb47-206">VS17 NuGet sporadycznie nie może nawiązać połączenia ze źródłami VSO/VSTS — Usterka programu VS 365798 — [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="2eb47-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="2eb47-207">contentFiles uzyskać dane wyjściowe do nieprawidłowej lokalizacji, jeśli PackagePath określa ścieżkę jako "contentFiles"- [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="2eb47-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="2eb47-208">Element docelowy Pack dołącza Właściwość PackageVersion z VersionSuffix- [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="2eb47-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="2eb47-209">Określanie ścieżki pakietu nie działa z pakietem dotnet Pack — [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="2eb47-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="2eb47-210">Pakiet NuGet wyprowadza wiele ostrzeżeń dotyczących zduplikowanych importów podczas przywracania [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="2eb47-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="2eb47-211">Wybierz opcję "format Menedżera pakietów NuGet" jest nieprawidłowy w przypadku motywu ciemny — [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="2eb47-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="2eb47-212">VS Crash podczas przywracania kompilacji — [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="2eb47-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="2eb47-213">Zakleszczenie programu Visual Studio w przypadku dodania TFM w targetframeworks, Zapisz, a następnie Skompiluj.</span><span class="sxs-lookup"><span data-stu-id="2eb47-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="2eb47-214">10% czasu [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="2eb47-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="2eb47-215">Pakiet NuGet nie wyprowadza komunikatu o powodzeniu w przypadku pomyślnego pakowania projektu — [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="2eb47-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="2eb47-216">PackTask nie powiodła się z powodu nieznalezienia metody System. IO. Compression 4,1- [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="2eb47-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="2eb47-217">Pakiet jest uruchamiany zbyt często — PackTask często kończy się niepowodzeniem z powodu konfliktu dostępu do plików — [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="2eb47-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="2eb47-218">Pakiet NuGet otwiera okno dane wyjściowe podczas przywracania w tle — [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="2eb47-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="2eb47-219">Eliminowanie jako wzorca kodowania niebezpiecznego (co może spowodować zawieszenie) — [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="2eb47-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="2eb47-220">Perf/UIHang — ulepszanie operacji odczytu DownloadTimeoutStream- [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="2eb47-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="2eb47-221">Zakleszczenie programu Visual Studio w przypadku próby zamknięcia projektu przed zakończeniem przywracania NuGet [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="2eb47-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="2eb47-222">Problemy z PackTask i pakowanie `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="2eb47-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="2eb47-223">[vsfeedback] Nie można rozpoznać pakietów NuGet w nowym projekcie (wymaga ponownego uruchomienia programu Visual Studio) — [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="2eb47-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="2eb47-224">[vsfeedback] Zostanie wyświetlona lista rozwijana "wersja", która zawiera dostępne wersje pakietów, co może pozostawać w synchronizacji z wybranym pakietem nuGet...- [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="2eb47-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="2eb47-225">Pakiet NuGet. Klient powinien używać JoinableTaskFactory CPS podczas współpracy z serwerem CPS, aby zapobiec zakleszczeniom — [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="2eb47-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="2eb47-226">Pakiet NuGet 3.5.0 nie rozpakować `.targets` z pakietu — [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="2eb47-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="2eb47-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-227">dotnet</span></span>
  - <span data-ttu-id="2eb47-228">Pakiet dotnetcore nie obsługuje tytułu w `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="2eb47-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="2eb47-229">Install-Package wyniki w oknie dialogowym błędów w program VS2017 RC — [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="2eb47-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="2eb47-230">Aktualizacja pakietu dla projektu .NET Core prawdopodobnie nie działa, ponieważ interfejs użytkownika nie pobiera aktualizacji CPS z nominacji.</span><span class="sxs-lookup"><span data-stu-id="2eb47-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="2eb47-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="2eb47-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="2eb47-232">Popraw nierozwiązane ostrzeżenie dotyczące odwołań — [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="2eb47-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="2eb47-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-233">dotnet</span></span>
  - <span data-ttu-id="2eb47-234">dotnetcore Pack — elementu ProjectReference utraci informacje o wersji — [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="2eb47-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="2eb47-235">Utwórz aplikację platformy UWP Utwórz projekt & ponownie skompilować łączny czas, który upłynął, [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="2eb47-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="2eb47-236">Komunikat o powodzeniu przywracania jest wyświetlany nawet po wystąpieniu błędu podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="2eb47-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="2eb47-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="2eb47-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="2eb47-238">ponownie Opublikuj pakiet NuGet. CommandLine 3.4.4 do Nuget.org- [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="2eb47-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="2eb47-239">Po migracji projekty zmieniają się z `project.json` na `.csproj` ---przywracanie nie powiedzie się [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="2eb47-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="2eb47-240">Przywracanie nie powiodło się w przypadku nowo utworzonego projektu testowego xUnit — [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="2eb47-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="2eb47-241">Projekty podstawowe mogą zawieszać się, blokować interfejs użytkownika przy otwartym [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="2eb47-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="2eb47-242">Napraw plik elementów docelowych dla zadań kompilacji — [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="2eb47-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="2eb47-243">Lista błędów zawiera błąd po rozwiązaniu kompilacji, które zwalnia przywoływany projekt [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="2eb47-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="2eb47-244">MSB4057: element docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="2eb47-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="2eb47-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="2eb47-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="2eb47-246">vsfeedback: interfejs użytkownika Menedżera NuGet dla awarii rozwiązań po wybraniu opcji wszystkie projekty — [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="2eb47-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="2eb47-247">nuget.exe msbuildpath kończy się niepowodzeniem, gdy występuje końcowy ukośnik — [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="2eb47-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="2eb47-248">vsfeedback: Przywracanie NuGet daje kilka ostrzeżeń odwołania projektu dla projektu LinqToTwitter — [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="2eb47-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="2eb47-249">Pakiet od `.csproj` nie zawiera atrybutu minClientVersion — [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="2eb47-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="2eb47-250">NuGet.Build.Tasks.Pack.dll wysłane opóźnienie z podpisem program VS2017 (d15rel 26014,00) — [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="2eb47-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="2eb47-251">VSFeedback: Przywracanie nie powiodło się dla projektu VS 2015 wygenerowanego z CMake 3.7.1- [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="2eb47-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="2eb47-252">VSFeedback: Błędy przywracania mogą zasłaniać bardziej kompletne komunikaty o błędach, które kompilacja może dać [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="2eb47-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="2eb47-253">[VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny sieci Web: wartość nie może być równa null.</span><span class="sxs-lookup"><span data-stu-id="2eb47-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="2eb47-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="2eb47-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="2eb47-255">Migracja zgłasza "wyjątek odwołania do obiektu" w NuGet. PackageManagement. VisualStudio. SolutionRestoreWorker- [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="2eb47-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="2eb47-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-256">dotnet</span></span>
  - <span data-ttu-id="2eb47-257">Pakiet dotnetcore Pack powinien mieć pakiet narzędzi z wersjami, dla których został skompilowany pakiet — [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="2eb47-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="2eb47-258">Nowe przywracanie w tle powoduje zapis milisekund na pasku stanu, gdy trwa sekund, aby przywrócić [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="2eb47-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="2eb47-259">Literówka w przypadku niepowodzenia rozpoznania wszystkich odwołań do projektu — [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="2eb47-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="2eb47-260">Włącz przepływy pracy PCM w scenariuszach odwołań do pakietów — [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="2eb47-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="2eb47-261">Nie można znaleźć zainstalowanych pakietów w interfejsie użytkownika Menedżera pakietów — [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="2eb47-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="2eb47-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-262">dotnet</span></span>
  - <span data-ttu-id="2eb47-263">Pakiet dotnetcore kończy się niepowodzeniem, gdy PackagePath jest pusty- [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="2eb47-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="2eb47-264">Zadanie przywracania kończy się niepowodzeniem w scenariuszu obejmującym wiele użytkowników — [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="2eb47-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="2eb47-265">Nie można zmienić typu zawartości podczas pakowania przy użyciu zadania pakietu NuGet — [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="2eb47-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="2eb47-266">Domyślna kopia ContentFiles jest niepoprawna dla programu MsBuild/t: Pack- [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="2eb47-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="2eb47-267">Pakiet instalacyjny programu instalacyjnego podwójnego rejestrowania komunikat przywracania pakietów — [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="2eb47-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="2eb47-268">Usuń Guardrails — przywracanie sekcji "środowiska uruchomieniowe" powinno być stosowane tylko do bieżącego projektu — [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="2eb47-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="2eb47-269">Pakiet Task umieszcza pliki zawartości w "Content/" i "contentFiles/"- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="2eb47-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="2eb47-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-270">dotnet</span></span>
  - <span data-ttu-id="2eb47-271">dotnetcore Pack3 wykonuje dodatkowe dzielenie tagów — [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="2eb47-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="2eb47-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-272">dotnet</span></span>
  - <span data-ttu-id="2eb47-273">Pakiet dotnetcore: projekty pakowania z odwołaniami do pakietu są wynikiem ostrzeżenia o zduplikowanym imporcie — [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="2eb47-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="2eb47-274">Przywracanie dzienników w programie VS nie jest zawsze wyświetlane- [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="2eb47-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="2eb47-275">tekst pomocy dla ustawień regionalnych NuGet nadal omawiany w pamięci podręcznej pakietów — [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="2eb47-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="2eb47-276">Restore3 Couples składnika packagereferences z TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="2eb47-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="2eb47-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="2eb47-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="2eb47-278">Pakiet NuGet wybiera nieoczekiwaną wersję programu MSBuild w programie VS "15" (wersja zapoznawcza 4).</span><span class="sxs-lookup"><span data-stu-id="2eb47-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="2eb47-279">wiersz polecenia — [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="2eb47-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="2eb47-280">Zapisuj pliki docelowe/elementy props w przypadku niepowodzenia przywracania — [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="2eb47-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="2eb47-281">Pakiet NuGet podczas przywracania nie uwzględnia tych samych podkładek zgodności jak MSBuild w przypadku uruchamiania w wierszu polecenia programu VS 15 — [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="2eb47-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="2eb47-282">Ponowne włączanie PackFromProjectWithDevelopmentDependencySet dla VS15- [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="2eb47-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="2eb47-283">Mieszanie problemów z pakietem NuGet — [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="2eb47-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="2eb47-284">Integruj 4.0.0.2067 w interfejsie wiersza polecenia i repozytoria zestawu SDK, aby dostarczyć z użyciem RC2- [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="2eb47-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="2eb47-285">VS zawiesza się podczas tworzenia nowej aplikacji z konsolą podstawową, zamykaj rozwiązanie, otwieraj rozwiązanie i zamykaj rozwiązanie — [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="2eb47-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="2eb47-286">Wysunięcie otwierające projekt względem d15prerel. 25916.01- [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="2eb47-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="2eb47-287">Naprawianie dokumentu/pomocy dotyczącej ustawień regionalnych dotnet/nuget.exe — [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="2eb47-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="2eb47-288">Sprawdź PackTask pod kątem problemów z końcowym lub wiodącym odstępem — [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="2eb47-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="2eb47-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-289">dotnet</span></span>
  - <span data-ttu-id="2eb47-290">Pakiet dotnetcore Pack jest pakowany z opakowania nie bin- [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="2eb47-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="2eb47-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-291">dotnet</span></span>
  - <span data-ttu-id="2eb47-292">Pakiet dotnetcore zawsze wygląda na ustawienie wersji elementu ProjectReference na 1.0.0- [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="2eb47-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="2eb47-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="2eb47-293">dotnet</span></span>
  - <span data-ttu-id="2eb47-294">Pakiet dotnetcore kończy się niepowodzeniem z odwołaniami projektu i <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="2eb47-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="2eb47-295">LockRecursionException w ProjectSystemCache. TryGetProjectNameByShortName- [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="2eb47-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="2eb47-296">Przytnij odstępy od właściwości programu MSBuild — [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="2eb47-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="2eb47-297">Konsoliduj dwa zdarzenia projektu zgłoszone podczas ładowania projektu — [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="2eb47-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="2eb47-298">Biblioteki P2P w `project.assets.json` pliku mają niepoprawną wersję [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="2eb47-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="2eb47-299">Przywracanie awarii z powodu braku odpowiedzi i niedostępnego pakietu — [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="2eb47-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="2eb47-300">nuget.exe może zawiesić się dużą ilość danych wyjściowych błędu MSBuild — [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="2eb47-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="2eb47-301">Przywracanie po kompilacji dla programu Blend kończy się niepowodzeniem po raz pierwszy [#2121](https://github.com/NuGet/Home/issues/2121) .</span><span class="sxs-lookup"><span data-stu-id="2eb47-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="2eb47-302">DCR</span><span class="sxs-lookup"><span data-stu-id="2eb47-302">DCRs</span></span>

- <span data-ttu-id="2eb47-303">Migrowanie VSIX z wersji 2 VSIX do V3 VSIX- [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="2eb47-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="2eb47-304">Pakiet NuGet powinien mieć mechanizm pobierania ścieżki do pliku blokady w programie MSBuild — [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="2eb47-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="2eb47-305">Dodaj zasoby kompilacji do TFM kontroli zgodności i plików zasobów — [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="2eb47-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="2eb47-306">Zdefiniuj nowy ProjectCapability "Pack" w celu włączenia funkcji związanych z pakietem — [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="2eb47-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="2eb47-307">Uruchom pakiet jako element docelowy po kompilacji dla właściwości "GeneratePackageOnBuild" programu MSBuild — [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="2eb47-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="2eb47-308">Użyj właściwości NuGet RestoreProjectStyle, aby utworzyć określony projekt NuGet — [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="2eb47-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="2eb47-309">Dostosuj przywracanie dla przechodnich odwołań do projektu- [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="2eb47-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="2eb47-310">Dodaj właściwości NuGet w pliku docelowym dla projektów innych niż platformy UWP — [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="2eb47-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="2eb47-311">Obsługa TargetPlatformVersion platformy UWP — [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="2eb47-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="2eb47-312">Przekaż metadane odwołania projektu do systemu projektu NuGet — [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="2eb47-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="2eb47-313">Dodaj interfejs użytkownika dla trybu pakowania — [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="2eb47-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="2eb47-314">Starsze `.csproj` potrzeby NugetTargetMoniker i RuntimeIdentifiers są ustawiane w elemencie proj/targets- [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="2eb47-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="2eb47-315">Pakiet instalacyjny może się pokrywać z funkcją automatycznej przywracania [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="2eb47-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="2eb47-316">QueryStatus menu kontekstowego nie nastąpi, gdy pakietu VSPackage nie jest załadowany- [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="2eb47-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="2eb47-317">Przywracanie rozwiązań i przywracanie kompilacji nadal wyświetla okna dialogowe — [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="2eb47-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="2eb47-318">Izolowanie wersji VSSDK w programie NuGet. klienci — kompilacja rozwiązań — [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="2eb47-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="2eb47-319">Linki do problemów z usługą GitHub rozwiązane w wersji RTM</span><span class="sxs-lookup"><span data-stu-id="2eb47-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="2eb47-320">Lista problemów 1</span><span class="sxs-lookup"><span data-stu-id="2eb47-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="2eb47-321">Lista problemów 2</span><span class="sxs-lookup"><span data-stu-id="2eb47-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="2eb47-322">Lista problemów 3</span><span class="sxs-lookup"><span data-stu-id="2eb47-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="2eb47-323">Lista problemów 4</span><span class="sxs-lookup"><span data-stu-id="2eb47-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="2eb47-324">Lista problemów 5</span><span class="sxs-lookup"><span data-stu-id="2eb47-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
