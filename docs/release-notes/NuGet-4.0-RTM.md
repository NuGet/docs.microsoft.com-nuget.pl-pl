---
title: Informacje o wersji programu NuGet 4.0 RC
description: Informacje o wersji NuGet 4.0 RTM, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547764"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="bcacd-103">Informacje o wersji NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="bcacd-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="bcacd-104">[Program Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.0, który dodaje obsługę platformy .NET Core i ma wiele poprawek jakości oraz zwiększa wydajność.</span><span class="sxs-lookup"><span data-stu-id="bcacd-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="bcacd-105">Ta wersja oferuje również kilka udoskonaleń, takich jak obsługa PackageReference, polecenia NuGet MSBuild elementów docelowych, Przywracanie pakietu tło i inne.</span><span class="sxs-lookup"><span data-stu-id="bcacd-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="bcacd-106">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="bcacd-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="bcacd-107">Przywracanie pakietów NuGet może się nie powieść, jeśli masz wiele projektów odwołujących się do innego projektu w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="bcacd-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-108">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-108">Issue</span></span>

<span data-ttu-id="bcacd-109">Przywracanie pakietów NuGet może nie działać, jeśli w rozwiązaniu istnieją odwołania do projektu do tego samego projektu z inną wielkością liter lub innymi ścieżkami względnymi.</span><span class="sxs-lookup"><span data-stu-id="bcacd-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="bcacd-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="bcacd-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="bcacd-111">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-111">Workaround</span></span>

<span data-ttu-id="bcacd-112">Napraw wielkość liter lub ścieżki względne w taki sposób, aby były takie same dla wszystkich odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="bcacd-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="bcacd-113">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="bcacd-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-114">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-114">Issue</span></span>

<span data-ttu-id="bcacd-115">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="bcacd-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="bcacd-116">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="bcacd-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="bcacd-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="bcacd-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="bcacd-118">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-118">Workaround</span></span>

<span data-ttu-id="bcacd-119">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bcacd-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="bcacd-120">Alternatywnie, spróbuj usunąć `project.lock.json` i przywrócić go ponownie.</span><span class="sxs-lookup"><span data-stu-id="bcacd-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="bcacd-121">W projektach .NET Core użytkownik może pozostać w pętli nieskończonej przywracania w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem</span><span class="sxs-lookup"><span data-stu-id="bcacd-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-122">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-122">Issue</span></span>

<span data-ttu-id="bcacd-123">Czasami, w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie uruchamiane w pętli nieskończonej.</span><span class="sxs-lookup"><span data-stu-id="bcacd-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="bcacd-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="bcacd-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="bcacd-125">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-125">Workaround</span></span>

<span data-ttu-id="bcacd-126">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="bcacd-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="bcacd-127">Nie można wyświetlić, dodać ani zaktualizować składnika DotNetCLITools przy użyciu Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="bcacd-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-128">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-128">Issue</span></span>

<span data-ttu-id="bcacd-129">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="bcacd-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="bcacd-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="bcacd-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="bcacd-131">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-131">Workaround</span></span>

<span data-ttu-id="bcacd-132">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="bcacd-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="bcacd-133">Przywracanie NuGet zakończy się niepowodzeniem po ustawieniu właściwości PackageId dla projektów</span><span class="sxs-lookup"><span data-stu-id="bcacd-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-134">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-134">Issue</span></span>

<span data-ttu-id="bcacd-135">Dla projektów .NET Core funkcja przywracania NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów.</span><span class="sxs-lookup"><span data-stu-id="bcacd-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="bcacd-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="bcacd-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="bcacd-137">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-137">Workaround</span></span>

<span data-ttu-id="bcacd-138">Uruchom przywracanie przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="bcacd-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="bcacd-139">Gdy projekt nie ma folderu „obj”, przywracanie pakietu może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="bcacd-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-140">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-140">Issue</span></span>

<span data-ttu-id="bcacd-141">Program Visual Studio nie może przywrócić składnika PackageReferences, jeśli folder „obj” został usunięty.</span><span class="sxs-lookup"><span data-stu-id="bcacd-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="bcacd-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="bcacd-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="bcacd-143">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-143">Workaround</span></span>

<span data-ttu-id="bcacd-144">Gdy utworzysz folder „obj” ręcznie, funkcja przywracania powinna zadziałać.</span><span class="sxs-lookup"><span data-stu-id="bcacd-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="bcacd-145">Ręczna aktualizacja pakietów przy użyciu pakietu aktualizacji w konsoli może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="bcacd-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-146">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-146">Issue</span></span>

<span data-ttu-id="bcacd-147">Ręczne użycie pakietu aktualizacji w konsoli działa tylko jeden raz dla projektów PackageReferences, które zostały właśnie przekonwertowane.</span><span class="sxs-lookup"><span data-stu-id="bcacd-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="bcacd-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="bcacd-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="bcacd-149">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-149">Workaround</span></span>

<span data-ttu-id="bcacd-150">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="bcacd-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="bcacd-151">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="bcacd-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-152">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-152">Issue</span></span>

<span data-ttu-id="bcacd-153">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bcacd-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="bcacd-154">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="bcacd-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="bcacd-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="bcacd-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="bcacd-156">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-156">Workaround</span></span>

<span data-ttu-id="bcacd-157">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="bcacd-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="bcacd-158">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt przeznaczony dla platformy .NET461 odwołuje się do innego projektu przeznaczonego dla platformy .NETStandard</span><span class="sxs-lookup"><span data-stu-id="bcacd-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="bcacd-159">Problem</span><span class="sxs-lookup"><span data-stu-id="bcacd-159">Issue</span></span>

<span data-ttu-id="bcacd-160">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt oparty na składniku PackageReferenece przeznaczony dla platformy .NET461 odwołuje się do innego projektu opartego na składniku PackageReference przeznaczonego dla platformy .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="bcacd-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="bcacd-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="bcacd-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="bcacd-162">Obejście</span><span class="sxs-lookup"><span data-stu-id="bcacd-162">Workaround</span></span>

<span data-ttu-id="bcacd-163">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="bcacd-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="bcacd-164">Problemy rozwiązane w wersji RTM 4.0 NuGet przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="bcacd-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="bcacd-165">[Informacje o wersji NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) — Wyświetla listę wszystkich problemów naprawione w wersji NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="bcacd-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="bcacd-166">Funkcje</span><span class="sxs-lookup"><span data-stu-id="bcacd-166">Features</span></span>

- <span data-ttu-id="bcacd-167">Localize — ciągi w NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="bcacd-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="bcacd-168">Nuget wymusza załadować projektów aplikacji sieci web w trybie LSL - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="bcacd-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="bcacd-169">Obsługę AutoReferenced PackageReference wersja bloku zmiany w interfejsie użytkownika dla pakietów "zainstalowany zestaw sdk" - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="bcacd-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="bcacd-170">Skomunikował się PackageSpec.Version dla wszelkich zależności projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="bcacd-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="bcacd-171">Obsługa Usuwanie odwołań do `.csproj` z commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="bcacd-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="bcacd-172">Obsługa przywracania projektów PackageReference (normalne i interfejs xplat) i uproszczonego ładowania rozwiązań — [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="bcacd-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="bcacd-173">Obsługa dodawania odwołań do `.csproj` z commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="bcacd-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="bcacd-174">Obsługa przywracania NuGet dla uproszczonego ładowania rozwiązań dla `packages.config` lub `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="bcacd-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="bcacd-175">Pliki obsługi w pliku cele nuget generowane — [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="bcacd-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="bcacd-176">Ustanowić ciągła Integracja platformy Mono Walidacja nuget.exe na komputerze Mac przy użyciu platformy MSBuild — [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="bcacd-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="bcacd-177">Przenieś NuGet poza zależności NuGet.Core v2 - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="bcacd-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="bcacd-178">Usterki</span><span class="sxs-lookup"><span data-stu-id="bcacd-178">Bugs</span></span>

- <span data-ttu-id="bcacd-179">Przywracanie pakietów NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów — [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="bcacd-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="bcacd-180">Błąd NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie vsix — [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="bcacd-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="bcacd-181">Pakiet zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wielu krótkich nazw platform — [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="bcacd-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="bcacd-182">Program VS 2017 RC3 awarie na temat korzystania z aktualizacji z całego rozwiązania pakietów zarządzania — [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="bcacd-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="bcacd-183">Nie można odinstalować nowo zainstalowany pakiet — [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="bcacd-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="bcacd-184">Podczas migracji do PackageRef, rozwiązania hybrydowego mają przywracania dziwne zachowania - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="bcacd-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="bcacd-185">Tworzenie wkrótce po uruchamianie NuGet działanie (instalacja, aktualizacja, przywracanie), może spowodować VS do zawieszenia - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="bcacd-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="bcacd-186">Zawieszanie interfejsu użytkownika — inicjowanie NuGet.SolutionRestoreManager.RestoreManagerPackage zakleszczenia [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="bcacd-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="bcacd-187">Dodaj polecenie pakietu należy dodać wersję jako atrybut zamiast elementu - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="bcacd-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="bcacd-188">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-188">dotnet</span></span>
  - <span data-ttu-id="bcacd-189">foo.sln przywracania dotnetcore — kończy się niepowodzeniem, podczas konfiguracji w SLN spowodować przywracania graph — projekty zduplikowane (ale config różnic) [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="bcacd-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="bcacd-190">Zawartość tylko pakiety - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="bcacd-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="bcacd-191">Domyślnie zrezygnować z pakietu format selektor, opcja - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="bcacd-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="bcacd-192">Danych o wydajności: Projekt CreateUAP_CSharp_VS.01.1.Create uwzględniona Duration_TotalElapsedTime przez 3,153.570 ms (149.1%).</span><span class="sxs-lookup"><span data-stu-id="bcacd-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="bcacd-193">Plan bazowy 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="bcacd-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="bcacd-194">Danych o wydajności: Rozwiązanie ManagedLangs_CS_DDRIT.0300.Rebuild uwzględniona Duration_TotalElapsedTime przez 1,5 s.</span><span class="sxs-lookup"><span data-stu-id="bcacd-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="bcacd-195">Plan bazowy 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="bcacd-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="bcacd-196">Nominacji zakończy się niepowodzeniem w projektach multi TFM - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="bcacd-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="bcacd-197">Danych o wydajności: Rozwiązanie WebForms_DDRIT.1200.Close uwzględniona VM_ImagesInMemory_Total_devenv według liczby 3.000 (0,5%).</span><span class="sxs-lookup"><span data-stu-id="bcacd-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="bcacd-198">Plan bazowy 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="bcacd-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="bcacd-199">vsfeedback - pakietu ostrzeżenia podczas określania wartości netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="bcacd-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="bcacd-200">Pathtoolongexception — podczas próby dodania pakiet NuGet do aplikacji sieci web platformy ASP.NET Core puste - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="bcacd-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="bcacd-201">Pakiet jest uruchamiany zbyt często — dotnet</span><span class="sxs-lookup"><span data-stu-id="bcacd-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="bcacd-202">dotnetcore pakietu zakończy się niepowodzeniem z miejsca to zależność cykliczną w zależności programu graph obejmujące docelowe "Pakiet" - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="bcacd-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="bcacd-203">Pakiet jest uruchamiany zbyt często — pakiet NuGet Generowanie nie obejmuje wszystkie konfiguracje — [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="bcacd-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="bcacd-204">Nuget Dodawanie obiektu NullReferenceException z packageref w projekcie C++ - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="bcacd-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="bcacd-205">Ułatwienia dostępu: Narrator nie narracji pole wyboru, aby wybrać projekty, aby zainstalować pakiet: [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="bcacd-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="bcacd-206">NuGet VS17 sporadycznie nie powiedzie się nawiązywania połączenia z kanałów informacyjnych VSO/VSTS - 365798 usterki programu VS - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="bcacd-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="bcacd-207">Pliki pobierać dane wyjściowe do niewłaściwej lokalizacji, jeśli PackagePath Określa ścieżkę jako "pliki" - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="bcacd-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="bcacd-208">Pakiet docelowy dołącza właściwość VersionSuffix - PackageVersion [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="bcacd-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="bcacd-209">Określanie ścieżki pakietu nie działa w przypadku pakietu dotnet - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="bcacd-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="bcacd-210">NuGet generuje wiele ostrzeżeń o zduplikowane Importy, podczas przywracania - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="bcacd-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="bcacd-211">Wybierz okno dialogowe "Menedżer pakietów NuGet Format" wygląda niewłaściwie w obszarze motyw ciemny - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="bcacd-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="bcacd-212">VS awarii po Przywracanie kompilacji — [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="bcacd-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="bcacd-213">Visual Studio zakleszczenie w przypadku dodania elementu TFM w targetframeworks, Zapisz, a następnie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bcacd-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="bcacd-214">10% czasu - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="bcacd-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="bcacd-215">Pakiet nuget nie wyświetla komunikat informujący o pomyślnym - pakowania projektu [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="bcacd-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="bcacd-216">PackTask zakończy się niepowodzeniem z powodu 4.1 System.IO.Compression nie można odnaleźć - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="bcacd-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="bcacd-217">Pakiet jest uruchamiany zbyt często — PackTask często zakończy się niepowodzeniem z konfliktem dostępu do pliku - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="bcacd-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="bcacd-218">NuGet spowoduje otwarcie okna dane wyjściowe podczas przywracania tła - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="bcacd-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="bcacd-219">Wyeliminuj element ServiceProvider jako niebezpieczne wzorzec pisania kodu, (które mogą powodować zawiesza się) — [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="bcacd-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="bcacd-220">Perf/UIHang - poprawić odczyty DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="bcacd-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="bcacd-221">Zakleszczenia programu Visual Studio, jeśli użytkownik podejmie próbę zamykanie projektu, zanim zakończy przywracanie pakietów NuGet — [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="bcacd-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="bcacd-222">Problemy związane z PackTask i pakowanie `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="bcacd-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="bcacd-223">[vsfeedback] Nie można rozpoznać pakietów nuget dla nowego projektu (wymaga ponownego uruchomienia programu visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="bcacd-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="bcacd-224">[vsfeedback] "Wersja" Lista rozwijana, które pokazuje wersje pakiet niezbyt dobrze radzi sobie, aby pozostać w synchronizacji z pakietu nuGet wybrane... — [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="bcacd-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="bcacd-225">Nuget.Client skorzystaj z CPS JoinableTaskFactory podczas interakcji z CPS zapobiegające zakleszczenia - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="bcacd-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="bcacd-226">NuGet 3.5.0 nie rozpakowywania `.targets` z pakietu - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="bcacd-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="bcacd-227">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-227">dotnet</span></span>
  - <span data-ttu-id="bcacd-228">dotnetcore nie obsługuje tytuł w `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="bcacd-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="bcacd-229">Install-Package skutkuje okna dialogowego błędu w programie VS2017 RC — [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="bcacd-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="bcacd-230">Aktualizowanie pakietu dla projektu programu .net core nie działa prawidłowo, zgodnie z interfejsu użytkownika nie pobranie aktualizacji CPS z nominate.</span><span class="sxs-lookup"><span data-stu-id="bcacd-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="bcacd-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="bcacd-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="bcacd-232">Poprawa ostrzeżenie nierozpoznane odwołanie - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="bcacd-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="bcacd-233">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-233">dotnet</span></span>
  - <span data-ttu-id="bcacd-234">Pakiet dotnetcore — elementu ProjectReference utraci informacje o wersji — [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="bcacd-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="bcacd-235">Tworzenie aplikacji platformy uniwersalnej systemu Windows tworzenie projektu i Odbuduj regresji całkowity upływ czasu — [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="bcacd-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="bcacd-236">Nawet po błędzie jest wyświetlany komunikat pomyślnie przeprowadzić przywrócenie podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="bcacd-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="bcacd-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="bcacd-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="bcacd-238">Ponowne publikowanie Nuget.CommandLine 3.4.4 na stronie Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="bcacd-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="bcacd-239">Na migracji, projekty zmienić z `project.json` do `.csproj` ---Przywracanie nie powiodło się — [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="bcacd-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="bcacd-240">Niepowodzenie przywracania na projekt testu xunit nowo utworzony - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="bcacd-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="bcacd-241">Projekty Core zawieszanie znajduje się w zablokowanie interfejsu użytkownika podczas otwierania - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="bcacd-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="bcacd-242">Napraw plik elementów docelowych dla zadania kompilacji - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="bcacd-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="bcacd-243">Lista błędów zawiera błąd, po rozwiązania kompilacji, które zwolnić odwołania projekt - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="bcacd-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="bcacd-244">MSB4057: Element docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="bcacd-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="bcacd-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="bcacd-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="bcacd-246">vsfeedback: interfejsu użytkownika Menedżera nuget dla rozwiązania ulega awarii podczas wybierz wszystkie projekty - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="bcacd-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="bcacd-247">nuget.exe msbuildpath nie powiedzie się po znaku ukośnika na końcu - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="bcacd-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="bcacd-248">vsfeedback: Przywracanie pakietów NuGet zapewniają kilka ostrzeżeń odwołania projektu dla projektu LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="bcacd-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="bcacd-249">Pakietu z `.csproj` nie zawiera atrybutu atrybutu minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="bcacd-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="bcacd-250">NuGet.Build.Tasks.Pack.dll dostarczane podpisany w programie VS2017 z opóźnieniem (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="bcacd-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="bcacd-251">VSFeedback: Restore kończy się niepowodzeniem dla projektu programu VS 2015, wygenerowane za pomocą narzędzia CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="bcacd-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="bcacd-252">VSFeedback: Błędy odtwarzania może zasłaniać pełniejsze komunikaty o błędach kompilacji może przyznać - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="bcacd-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="bcacd-253">[VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny sieci Web: wartość nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="bcacd-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="bcacd-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="bcacd-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="bcacd-255">Migracja zgłasza "Odwołanie do obiektu wyjątku" w NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="bcacd-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="bcacd-256">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-256">dotnet</span></span>
  - <span data-ttu-id="bcacd-257">Pakiet dotnetcore powinien pakietu narzędzi z wersjami, które pakietu została skompilowana - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="bcacd-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="bcacd-258">Nowe tle przywracania zapisuje milisekund pasek po zajmuje sekund, aby przywrócić - stanu [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="bcacd-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="bcacd-259">Błąd pisowni w udało się rozpoznać wszystkie projektu odwołania — [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="bcacd-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="bcacd-260">Włącz PCM przepływy pracy, w scenariuszach odwołanie do pakietu - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="bcacd-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="bcacd-261">Nie można odnaleźć zainstalowanych pakietów w pakiecie Menedżer interfejsu użytkownika — [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="bcacd-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="bcacd-262">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-262">dotnet</span></span>
  - <span data-ttu-id="bcacd-263">Pakiet dotnetcore zakończy się niepowodzeniem, gdy PackagePath jest pusta — [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="bcacd-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="bcacd-264">Przywracanie nie powiodło się zadań, w scenariuszu użytkownik multi - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="bcacd-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="bcacd-265">Nie można zmienić typu zawartości, gdy pakowanie przy użyciu zadania pakietu NuGet — [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="bcacd-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="bcacd-266">Domyślna kopia pliki są nieprawidłowe dla MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="bcacd-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="bcacd-267">Przywracanie pakietu instalacji double rejestruje przywracania pakietów komunikat - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="bcacd-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="bcacd-268">Usuń Guardrails - przywracania w sekcji "runtimes" stosuje się tylko do bieżącego projektu - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="bcacd-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="bcacd-269">Zadanie pakietów umieszcza pliki zawartości w obu "zawartość /" i "pliki /"- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="bcacd-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="bcacd-270">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-270">dotnet</span></span>
  - <span data-ttu-id="bcacd-271">dotnetcore dodatkiem Service Pack 3 dodatkowych tagu podziału - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="bcacd-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="bcacd-272">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-272">dotnet</span></span>
  - <span data-ttu-id="bcacd-273">Pakiet dotnetcore: pakowanie projektów za pomocą pakietu odwołuje się do powoduje zduplikowanie ostrzeżenia dotyczącego importowania - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="bcacd-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="bcacd-274">Przywróć rejestrowania w programie VS nie zawsze pokazuj - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="bcacd-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="bcacd-275">tekst pomocy dla zmiennych lokalnych nuget nadal wymienionych pakietów pamięci podręcznej — [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="bcacd-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="bcacd-276">Pozamałżeńskie Restore3 PackageReferences z TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="bcacd-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="bcacd-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="bcacd-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="bcacd-278">Nuget wybiera nieoczekiwaną wersją programu MSBuild w programie VS "15" dev. 4 (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="bcacd-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="bcacd-279">Wiersz polecenia — [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="bcacd-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="bcacd-280">Zapisać pliki celów/arkuszy właściwości na przywracanie nie powiodło się — [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="bcacd-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="bcacd-281">NuGet podczas przywracania nie jest zgodny ten sam podkładki compat jako MSBuild uruchamianego w wierszu polecenia programu VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="bcacd-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="bcacd-282">Ponownie włącz PackFromProjectWithDevelopmentDependencySet dla VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="bcacd-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="bcacd-283">Problemy z NuGet — Blend [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="bcacd-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="bcacd-284">Integrowanie 4.0.0.2067 repozytoriów interfejsu wiersza polecenia i zestawu SDK do wysłania z RC2 — [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="bcacd-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="bcacd-285">Zawiesza się programu VS, podczas tworzenia nowej aplikacji Konsolowej Core, Zamknij rozwiązanie, otwórz rozwiązanie i Zamknij rozwiązanie - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="bcacd-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="bcacd-286">Osiągnięcia zawieszenie otwierania projektu przed d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="bcacd-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="bcacd-287">Usuń lokalne dotnet/nuget.exe komunikatu pomocy doc — [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="bcacd-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="bcacd-288">Sprawdzanie PackTask problemów za pomocą spacji końcowych lub początkowych — [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="bcacd-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="bcacd-289">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-289">dotnet</span></span>
  - <span data-ttu-id="bcacd-290">Pakiet dotnetcore jest pakowanie z obj nie bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="bcacd-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="bcacd-291">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-291">dotnet</span></span>
  - <span data-ttu-id="bcacd-292">Pakiet dotnetcore zawsze wydaje się równa elementu ProjectReference w wersji 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="bcacd-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="bcacd-293">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="bcacd-293">dotnet</span></span>
  - <span data-ttu-id="bcacd-294">Pakiet dotnetcore kończy się niepowodzeniem z odwołaniami do projektów i <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="bcacd-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="bcacd-295">LockRecursionException w ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="bcacd-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="bcacd-296">Przycina odstępu z właściwości programu MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="bcacd-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="bcacd-297">Konsoliduj zdarzenia projektu dwóch wywoływane po załadowaniu projektu - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="bcacd-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="bcacd-298">Biblioteki p2p w `project.assets.json` plik ma nieprawidłową wersję - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="bcacd-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="bcacd-299">Przywróć awarii ze względu na źródło danych nie odpowiada i pakiet niedostępny — [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="bcacd-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="bcacd-300">nuget.exe mogą powodować zawieszanie na dużą ilość danych wyjściowych błąd MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="bcacd-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="bcacd-301">Przywracanie w kompilacji dla programu Blend nie powiedzie się po raz pierwszy, zakończy się pomyślnie po raz drugi (VS scenariusz rozwiązany) - [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="bcacd-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="bcacd-302">DCRs</span><span class="sxs-lookup"><span data-stu-id="bcacd-302">DCRs</span></span>

- <span data-ttu-id="bcacd-303">Przeprowadź migrację vsix z v2 vsix do v3 vsix — [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="bcacd-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="bcacd-304">NuGet powinny mieć mechanizm do pobierania ścieżki do pliku blokady w programie MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="bcacd-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="bcacd-305">Dodaj zasoby kompilacji do elementu TFM zgodności wyboru i zasoby pliku - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="bcacd-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="bcacd-306">Definiowanie nowych ProjectCapability "Pakiet" w pakiecie cele dotyczące włączania pakietu powiązane możliwości — [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="bcacd-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="bcacd-307">Uruchom pakiet jako wpis kompilacji można korzystać we właściwości programu MSBuild "GeneratePackageOnBuild" - target [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="bcacd-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="bcacd-308">Użyj właściwości NuGet RestoreProjectStyle do utworzenia określonego projektu NuGet — [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="bcacd-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="bcacd-309">Dostosowania przywracania dla zmienić przechodnie odwołania do projektu - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="bcacd-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="bcacd-310">Dodaj właściwości NuGet w pliku docelowym dla projektów UWP nie - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="bcacd-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="bcacd-311">Pomoc techniczna dla platformy uniwersalnej systemu Windows TargetPlatformVersion — [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="bcacd-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="bcacd-312">Metadane odwołania projektu do systemu projektu NuGet — komunikacji [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="bcacd-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="bcacd-313">Dodawanie interfejsu użytkownika dla trybu pakowania - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="bcacd-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="bcacd-314">Starsza wersja `.csproj` potrzebuje NugetTargetMoniker i RuntimeIdentifiers w proj/cele — [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="bcacd-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="bcacd-315">Pakiet instalacyjny nakładają się przy użyciu automatycznego przywracania - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="bcacd-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="bcacd-316">Menu kontekstowe QueryStatus nie się zdarzyć, gdy nie został załadowany pakietu VSPackage - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="bcacd-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="bcacd-317">Przywracanie rozwiązań i kompilacji przywracania w dalszym ciągu wyświetlać okien dialogowych - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="bcacd-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="bcacd-318">Izoluj wersji VSSDK NuGet.Clients kompilacji rozwiązań — [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="bcacd-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="bcacd-319">Linki do serwisu GitHub problemy rozwiązane w wersji RTM</span><span class="sxs-lookup"><span data-stu-id="bcacd-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="bcacd-320">Lista problemów 1</span><span class="sxs-lookup"><span data-stu-id="bcacd-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="bcacd-321">Lista problemów 2</span><span class="sxs-lookup"><span data-stu-id="bcacd-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="bcacd-322">Lista problemów 3</span><span class="sxs-lookup"><span data-stu-id="bcacd-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="bcacd-323">Lista problemów z 4</span><span class="sxs-lookup"><span data-stu-id="bcacd-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="bcacd-324">Lista problemów z 5</span><span class="sxs-lookup"><span data-stu-id="bcacd-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
