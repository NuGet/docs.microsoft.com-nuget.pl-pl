---
title: Informacje o wersji nuGet 4.0 RC
description: Informacje o wersji dla NuGet 4.0 RTM, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496607"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="32fe5-103">Informacje o wydaniu programu NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="32fe5-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="32fe5-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest wyposażony w NuGet 4.0, który dodaje obsługę .NET Core, ma kilka poprawek jakości i zwiększa wydajność.</span><span class="sxs-lookup"><span data-stu-id="32fe5-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="32fe5-105">Ta wersja zawiera również kilka ulepszeń, takich jak obsługa PackageReference, Polecenia NuGet jako obiekty docelowe MSBuild, przywraca pakiet w tle i inne.</span><span class="sxs-lookup"><span data-stu-id="32fe5-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="32fe5-106">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="32fe5-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="32fe5-107">Przywracanie pakietów NuGet może się nie powieść, jeśli masz wiele projektów odwołujących się do innego projektu w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="32fe5-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-108">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-108">Issue</span></span>

<span data-ttu-id="32fe5-109">Przywracanie pakietów NuGet może nie działać, jeśli w rozwiązaniu istnieją odwołania do projektu do tego samego projektu z inną wielkością liter lub innymi ścieżkami względnymi.</span><span class="sxs-lookup"><span data-stu-id="32fe5-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="32fe5-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="32fe5-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="32fe5-111">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-111">Workaround</span></span>

<span data-ttu-id="32fe5-112">Napraw wielkość liter lub ścieżki względne w taki sposób, aby były takie same dla wszystkich odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="32fe5-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="32fe5-113">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="32fe5-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-114">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-114">Issue</span></span>

<span data-ttu-id="32fe5-115">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="32fe5-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="32fe5-116">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="32fe5-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="32fe5-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="32fe5-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="32fe5-118">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-118">Workaround</span></span>

<span data-ttu-id="32fe5-119">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="32fe5-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="32fe5-120">Alternatywnie spróbuj usunąć `project.lock.json` i przywrócić ponownie.</span><span class="sxs-lookup"><span data-stu-id="32fe5-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="32fe5-121">W projektach .NET Core użytkownik może pozostać w pętli nieskończonej przywracania w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem</span><span class="sxs-lookup"><span data-stu-id="32fe5-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-122">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-122">Issue</span></span>

<span data-ttu-id="32fe5-123">Czasami, w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie uruchamiane w pętli nieskończonej.</span><span class="sxs-lookup"><span data-stu-id="32fe5-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="32fe5-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="32fe5-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="32fe5-125">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-125">Workaround</span></span>

<span data-ttu-id="32fe5-126">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="32fe5-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="32fe5-127">Nie można wyświetlać, dodawać ani aktualizować dotNetCLITools przy użyciu Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="32fe5-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-128">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-128">Issue</span></span>

<span data-ttu-id="32fe5-129">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="32fe5-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="32fe5-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="32fe5-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="32fe5-131">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-131">Workaround</span></span>

<span data-ttu-id="32fe5-132">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="32fe5-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="32fe5-133">Przywracanie NuGet zakończy się niepowodzeniem po ustawieniu właściwości PackageId dla projektów</span><span class="sxs-lookup"><span data-stu-id="32fe5-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-134">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-134">Issue</span></span>

<span data-ttu-id="32fe5-135">Dla projektów .NET Core funkcja przywracania NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów.</span><span class="sxs-lookup"><span data-stu-id="32fe5-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="32fe5-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="32fe5-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="32fe5-137">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-137">Workaround</span></span>

<span data-ttu-id="32fe5-138">Uruchom przywracanie przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="32fe5-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="32fe5-139">Gdy projekt nie ma folderu „obj”, przywracanie pakietu może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="32fe5-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-140">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-140">Issue</span></span>

<span data-ttu-id="32fe5-141">Program Visual Studio nie może przywrócić składnika PackageReferences, jeśli folder „obj” został usunięty.</span><span class="sxs-lookup"><span data-stu-id="32fe5-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="32fe5-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="32fe5-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="32fe5-143">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-143">Workaround</span></span>

<span data-ttu-id="32fe5-144">Gdy utworzysz folder „obj” ręcznie, funkcja przywracania powinna zadziałać.</span><span class="sxs-lookup"><span data-stu-id="32fe5-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="32fe5-145">Ręczna aktualizacja pakietów przy użyciu pakietu aktualizacji w konsoli może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="32fe5-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-146">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-146">Issue</span></span>

<span data-ttu-id="32fe5-147">Ręczne użycie pakietu aktualizacji w konsoli działa tylko jeden raz dla projektów PackageReferences, które zostały właśnie przekonwertowane.</span><span class="sxs-lookup"><span data-stu-id="32fe5-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="32fe5-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="32fe5-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="32fe5-149">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-149">Workaround</span></span>

<span data-ttu-id="32fe5-150">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="32fe5-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="32fe5-151">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="32fe5-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-152">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-152">Issue</span></span>

<span data-ttu-id="32fe5-153">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32fe5-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="32fe5-154">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="32fe5-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="32fe5-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="32fe5-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="32fe5-156">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-156">Workaround</span></span>

<span data-ttu-id="32fe5-157">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="32fe5-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="32fe5-158">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt przeznaczony dla platformy .NET461 odwołuje się do innego projektu przeznaczonego dla platformy .NETStandard</span><span class="sxs-lookup"><span data-stu-id="32fe5-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="32fe5-159">Problem</span><span class="sxs-lookup"><span data-stu-id="32fe5-159">Issue</span></span>

<span data-ttu-id="32fe5-160">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt oparty na składniku PackageReferenece przeznaczony dla platformy .NET461 odwołuje się do innego projektu opartego na składniku PackageReference przeznaczonego dla platformy .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="32fe5-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="32fe5-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="32fe5-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="32fe5-162">Obejście</span><span class="sxs-lookup"><span data-stu-id="32fe5-162">Workaround</span></span>

<span data-ttu-id="32fe5-163">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="32fe5-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="32fe5-164">Naprawiono problemy w ramach czasowych NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="32fe5-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="32fe5-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Wyświetla listę wszystkich problemów rozwiązanych dla NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="32fe5-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="32fe5-166">Funkcje</span><span class="sxs-lookup"><span data-stu-id="32fe5-166">Features</span></span>

- <span data-ttu-id="32fe5-167">Lokalizuj ciągi w pliku NuGet.Core.sln — [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="32fe5-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="32fe5-168">Nuget wymusza ładowanie projektów aplikacji internetowych w trybie LSL - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="32fe5-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="32fe5-169">Obsługa funkcji AutoReferenced PackageReference w celu zablokowania zmian wersji w interfejsie użytkownika dla pakietów "zainstalowany sdk" — [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="32fe5-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="32fe5-170">Poprawnie komunikować PackageSpec.Version dla wszystkich zależności projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="32fe5-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="32fe5-171">obsługa usuwania odwołań `.csproj` z wierszy poleceń - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="32fe5-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="32fe5-172">Obsługa przywracania dla projektów PackageReference (normalny i xplat) i lekkie obciążenie rozwiązania - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="32fe5-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="32fe5-173">obsługa dodawania odwołań do `.csproj` wierszy poleceń — [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="32fe5-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="32fe5-174">Obsługa przywracania NuGet dla `packages.config` `project.json`  - lekkiego ładowania rozwiązania dla lub [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="32fe5-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="32fe5-175">contentFiles wsparcie w pliku docelowym generowanym przez nuget - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="32fe5-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="32fe5-176">Ustanawianie mono ci dla sprawdzania poprawności nuget.exe na komputerze Mac przy użyciu MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="32fe5-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="32fe5-177">Przenieś NuGet off z v2 NuGet.Core zależności - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="32fe5-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="32fe5-178">Usterki</span><span class="sxs-lookup"><span data-stu-id="32fe5-178">Bugs</span></span>

- <span data-ttu-id="32fe5-179">NuGet restore w programie Visual Studio nie respektuje właściwości PackageId projektów — [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="32fe5-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="32fe5-180">Błąd NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie vsix - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="32fe5-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="32fe5-181">Pack zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wieloma TFM - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="32fe5-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="32fe5-182">Vs 2017 RC3 zawiesza się przy użyciu aktualizacji z zarządzania pakietami w całej rozwiązania - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="32fe5-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="32fe5-183">Nie można odinstalować nowo zainstalowanego pakietu - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="32fe5-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="32fe5-184">Podczas migracji do PackageRef rozwiązania hybrydowe mają dziwne zachowanie przywracania — [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="32fe5-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="32fe5-185">Tworzenie wkrótce po uruchomieniu operacji NuGet (instalacja, aktualizacja, przywracanie), może spowodować VS hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="32fe5-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="32fe5-186">Zawieszanie interfejsu użytkownika — zakleszczenie inicjowania nuget.solutionrestoremanager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="32fe5-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="32fe5-187">polecenie dodaj pakiet należy dodać wersję jako atrybut zamiast elementu - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="32fe5-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="32fe5-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-188">dotnet</span></span>
  - <span data-ttu-id="32fe5-189">dotnetcore Restore foo.sln -- kończy się niepowodzeniem, gdy konfiguracje w SLN powodują duplikaty (ale diff config) projekty na wykresie przywracania - [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="32fe5-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="32fe5-190">Pakiety tylko do zawartości - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="32fe5-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="32fe5-191">Domyślnie opcja wyboru formatu pakietu - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="32fe5-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="32fe5-192">Perf: CreateUAP_CSharp_VS.01.1.Tworzenie projektu regressed Duration_TotalElapsedTime o 3.153.570 ms (149.1%).</span><span class="sxs-lookup"><span data-stu-id="32fe5-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="32fe5-193">Wartość bazowa 26129,02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="32fe5-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="32fe5-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Rozwiązanie cofło Duration_TotalElapsedTime o 1,5 s.</span><span class="sxs-lookup"><span data-stu-id="32fe5-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="32fe5-195">Wartość bazowa 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="32fe5-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="32fe5-196">Nominacja nie powiedzie się w wielu projektach TFM - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="32fe5-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="32fe5-197">Perf: WebForms_DDRIT.1200.Close Rozwiązanie cofło VM_ImagesInMemory_Total_devenv o 3.000 Count (0.5%).</span><span class="sxs-lookup"><span data-stu-id="32fe5-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="32fe5-198">Wartość bazowa 26123,04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="32fe5-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="32fe5-199">vsfeedback - Ostrzeżenia o pakowaniu podczas kierowania netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="32fe5-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="32fe5-200">PathTooLongException podczas próby dodania pakietu NuGet do pustej aplikacji sieci web ASP.NET Core — [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="32fe5-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="32fe5-201">Pakiet działa zbyt często - dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="32fe5-202">pakiet dotnetcore kończy się niepowodzeniem z istnieje cykliczna zależność na wykresie zależności docelowej obejmującej docelowy "Pack" — [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="32fe5-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="32fe5-203">Pakiet działa zbyt często — generowanie pakietu NuGet nie zawiera wszystkich konfiguracji — [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="32fe5-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="32fe5-204">NullReferenceException dodawanie nuget z packageref w projekcie C++ - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="32fe5-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="32fe5-205">Dostępność : Narrator nie opowiada pola wyboru, aby wybrać projekty, aby zainstalować pakiet do - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="32fe5-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="32fe5-206">NuGet VS17 sporadycznie nie łączy się z kanałami informacyjnymi VSO/VSTS — błąd 365798 — [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="32fe5-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="32fe5-207">contentFiles uzyskać dane wyjściowe do niewłaściwej lokalizacji, jeśli PackagePath określa ścieżkę jako "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="32fe5-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="32fe5-208">Pack target dołącza packageversion właściwości z VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="32fe5-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="32fe5-209">Określanie ścieżki pakietu nie działa z pakietem dotnet - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="32fe5-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="32fe5-210">NuGet wyprowadza kilka ostrzeżeń o zduplikowanych importach podczas przywracania — [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="32fe5-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="32fe5-211">Wybierz okno dialogowe "NuGet Package Manager Format" wygląda źle pod ciemnym motywem - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="32fe5-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="32fe5-212">Awaria vs na przywracanie kompilacji - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="32fe5-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="32fe5-213">Zakleszczenia programu Visual Studio, jeśli dodasz TFM w targetframeworks, zapisz, a następnie skompilować.</span><span class="sxs-lookup"><span data-stu-id="32fe5-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="32fe5-214">10% czasu - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="32fe5-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="32fe5-215">nuget pack nie wyprowadza komunikatu o sukcesie podczas pomyślnego pakowania projektu - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="32fe5-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="32fe5-216">PackTask nie powiedzie się z powodu nieuleczeniu systemu.IO.Compression 4.1 - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="32fe5-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="32fe5-217">Pack działa zbyt często — PackTask często kończy się niepowodzeniem z konfliktem dostępu do plików - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="32fe5-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="32fe5-218">NuGet otwiera okno wyjściowe podczas przywracania tła - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="32fe5-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="32fe5-219">Wyeliminuj ServiceProvider jako niebezpieczny wzorzec kodowania (który może powodować zawiesza się) - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="32fe5-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="32fe5-220">Perf/UIHang - Poprawa odczytów DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="32fe5-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="32fe5-221">Zakleszczenia programu Visual Studio, jeśli spróbujesz zamknąć projekt przed zakończeniem przywracania NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="32fe5-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="32fe5-222">Problemy z PackTask `.nuspec`  - i pakowania [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="32fe5-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="32fe5-223">[vsfeedback] Nie można rozwiązać pakietów nuget w nowym projekcie (musi ponownie uruchomić visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="32fe5-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="32fe5-224">[vsfeedback] Rozwijana "Wersja", która pokazuje dostępne wersje pakietów, stara się pozostać w synchronizacji z wybranym pakietem nuGet... - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="32fe5-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="32fe5-225">Nuget.Client powinien używać CPS JoinableTaskFactory podczas interakcji z CPS, aby zapobiec zakleszczenia - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="32fe5-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="32fe5-226">NuGet 3.5.0 nie `.targets` rozpakowywanie z opakowania - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="32fe5-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="32fe5-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-227">dotnet</span></span>
  - <span data-ttu-id="32fe5-228">dotnetcore pack nie obsługuje `.csproj`  - tytułu w [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="32fe5-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="32fe5-229">Install-Package powoduje błąd w vs2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="32fe5-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="32fe5-230">Aktualizowanie pakietu dla projektu .net core wydaje się nie działać, ponieważ interfejs użytkownika nie pobiera aktualizacji CPS z nominuj.</span><span class="sxs-lookup"><span data-stu-id="32fe5-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="32fe5-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="32fe5-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="32fe5-232">Poprawa ostrzeżenia o nierozwiązanym odwołaniu - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="32fe5-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="32fe5-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-233">dotnet</span></span>
  - <span data-ttu-id="32fe5-234">dotnetcore pack - ProjectReference traci informacje o wersji - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="32fe5-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="32fe5-235">Tworzenie aplikacji platformy uniwersalnej systemu ZWP tworzenie projektu & odbudowy całkowitych regresji czasu, które upłynął - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="32fe5-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="32fe5-236">Komunikat pomyślnego przywracania jest wyświetlany nawet po błędzie podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="32fe5-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="32fe5-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="32fe5-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="32fe5-238">ponownie opublikować Nuget.CommandLine 3.4.4 do Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="32fe5-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="32fe5-239">Podczas migracji projekty zmieniają `project.json` `.csproj` się z --- przywracania --- nie powiedzie się — [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="32fe5-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="32fe5-240">Przywracanie w przypadku niepowodzenia nowo utworzonego projektu testu xunit — [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="32fe5-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="32fe5-241">Podstawowe projekty mogą zawieszać się, blokować interfejs użytkownika na otwartym - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="32fe5-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="32fe5-242">naprawić plik docelowy dla zadań kompilacji - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="32fe5-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="32fe5-243">Lista błędów zawiera błąd po rozwiązaniu kompilacji, które zwalnia projekt, do którego istnieje odwołanie - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="32fe5-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="32fe5-244">MSB4057: Docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="32fe5-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="32fe5-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="32fe5-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="32fe5-246">vsfeedback: nuget manager ui dla rozwiązania ulega awarii po wybraniu wszystkich projektów - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="32fe5-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="32fe5-247">nuget.exe msbuildpath nie powiedzie się, gdy istnieje cięcie końcowe - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="32fe5-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="32fe5-248">vsfeedback: Przywracanie NuGet daje kilka ostrzeżeń odwołania do projektu LinqToTwitter — [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="32fe5-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="32fe5-249">Pakiet `.csproj` z nie zawiera atrybutu minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="32fe5-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="32fe5-250">NuGet.Build.Tasks.Pack.dll wysłane opóźnienie podpisane w programie VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="32fe5-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="32fe5-251">VSFeedback: Przywracanie kończy się niepowodzeniem dla projektu VS 2015 wygenerowanego za pomocą CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="32fe5-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="32fe5-252">VSFeedback: Przywracanie błędów może przesłaniać bardziej kompletne komunikaty o błędach, które kompilacji może dać - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="32fe5-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="32fe5-253">[VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny: Wartość nie może być null.</span><span class="sxs-lookup"><span data-stu-id="32fe5-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="32fe5-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="32fe5-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="32fe5-255">Migracja zgłasza "Wyjątek odwołania do obiektu" w NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="32fe5-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="32fe5-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-256">dotnet</span></span>
  - <span data-ttu-id="32fe5-257">dotnetcore pack powinien pakować narzędzia z wersjami, przeciwko których pakiet został zbudowany - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="32fe5-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="32fe5-258">Nowe przywracanie tła zapisuje milisekundy na pasku stanu, gdy trwa kilka sekund, aby przywrócić - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="32fe5-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="32fe5-259">Literówka na nie może rozwiązać wszystkich odwołań do projektu - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="32fe5-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="32fe5-260">Włączanie przepływów pracy PCM w scenariuszach referencyjnych pakietów — [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="32fe5-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="32fe5-261">Nie można znaleźć zainstalowanych pakietów w interfejsie menedżera pakietów - [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="32fe5-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="32fe5-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-262">dotnet</span></span>
  - <span data-ttu-id="32fe5-263">pakiet dotnetcore kończy się niepowodzeniem, gdy PackagePath jest pusty - [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="32fe5-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="32fe5-264">Przywracanie zadania kończy się niepowodzeniem w scenariuszu dla wielu użytkowników — [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="32fe5-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="32fe5-265">Nie można zmienić typu zawartości podczas pakowania przy użyciu zadania Pakietu NuGet Pack — [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="32fe5-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="32fe5-266">Domyślna kopia contentfiles są niepoprawne dla MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="32fe5-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="32fe5-267">Zainstaluj pakiet przywracanie dwukrotnie rejestruje komunikat przywracania pakietów - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="32fe5-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="32fe5-268">Usuń barierki — przywracanie sekcji "środowiska wykonawcze" powinno dotyczyć tylko bieżącego projektu — [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="32fe5-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="32fe5-269">Zadanie pack umieszcza pliki zawartości zarówno w "zawartość / " i "contentFiles/" - [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="32fe5-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="32fe5-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-270">dotnet</span></span>
  - <span data-ttu-id="32fe5-271">dotnetcore pack3 robi dodatkowe dzielenie tagów - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="32fe5-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="32fe5-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-272">dotnet</span></span>
  - <span data-ttu-id="32fe5-273">dotnetcore pack: projekty pakowania z odniesieniami do pakietów skutkują zduplikowanym ostrzeżeniem importu - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="32fe5-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="32fe5-274">Przywróć rejestrowanie w vs nie zawsze pokazuje - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="32fe5-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="32fe5-275">nuget mieszkańcy pomagają tekst nadal wymienione pakiety cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="32fe5-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="32fe5-276">Restore3 pary PackageReferences z TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="32fe5-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="32fe5-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="32fe5-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="32fe5-278">Nuget wybiera nieoczekiwaną wersję MSBuild w vs "15" Preview 4 dev.</span><span class="sxs-lookup"><span data-stu-id="32fe5-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="32fe5-279">wiersz polecenia - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="32fe5-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="32fe5-280">Zapisz pliki obiektów docelowych/rekwizytów podczas nie powiodło się przywracanie - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="32fe5-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="32fe5-281">NuGet podczas przywracania nie respektuje tych samych podkładek compat co MSBuild podczas uruchamiania w wierszu polecenia programu VS 15 — [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="32fe5-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="32fe5-282">Ponownie włącz PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="32fe5-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="32fe5-283">Problemy z mieszaniem z NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="32fe5-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="32fe5-284">Integracja 4.0.0.2067 z repo CLI i SDK do wysyłki z RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="32fe5-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="32fe5-285">VS zawiesza się podczas tworzenia nowej aplikacji Core Console, zamknij rozwiązanie, otwarte rozwiązanie i zamknij rozwiązanie - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="32fe5-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="32fe5-286">Uderzenie w projekt otwarcia zawieszenia przeciwko d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="32fe5-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="32fe5-287">Napraw komunikat dotnet/nuget.exe locals doc/help - [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="32fe5-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="32fe5-288">Sprawdź PackTask pod kątem problemów z spływu lub wiodących odstępów - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="32fe5-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="32fe5-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-289">dotnet</span></span>
  - <span data-ttu-id="32fe5-290">dotnetcore pack jest pakowanie z obj nie bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="32fe5-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="32fe5-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-291">dotnet</span></span>
  - <span data-ttu-id="32fe5-292">dotnetcore pack zawsze wydaje się ustawić wersję ProjectReference na 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="32fe5-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="32fe5-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="32fe5-293">dotnet</span></span>
  - <span data-ttu-id="32fe5-294">pakiet dotnetcore kończy się <TargetFramework>  - niepowodzeniem z odwołaniami do projektu i [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="32fe5-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="32fe5-295">LockRecursionException w programie ProjectSystemCache.TryGetProjectNameByShortName — [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="32fe5-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="32fe5-296">Przycinanie odstępu z właściwości MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="32fe5-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="32fe5-297">Konsolidacja dwóch zdarzeń projektu podniesionych przy obciążeniu projektu - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="32fe5-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="32fe5-298">Biblioteki P2P `project.assets.json` w pliku mają niepoprawną wersję - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="32fe5-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="32fe5-299">Przywracanie awarii z powodu braku odpowiedzi i niedostępnego pakietu - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="32fe5-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="32fe5-300">nuget.exe może zawiesić się na dużej ilości danych wyjściowych błędu MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="32fe5-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="32fe5-301">Przywracanie na kompilacji dla blendu kończy się niepowodzeniem po raz pierwszy, kończy się po raz drugi (poprawiony scenariusz VS) — [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="32fe5-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="32fe5-302">DDR</span><span class="sxs-lookup"><span data-stu-id="32fe5-302">DCRs</span></span>

- <span data-ttu-id="32fe5-303">migrować vsix z v2 vsix do v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="32fe5-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="32fe5-304">NuGet powinien mieć mechanizm uzyskiwania ścieżki do pliku blokady w MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="32fe5-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="32fe5-305">Dodawanie zasobów kompilacji do pliku sprawdzania zgodności tfm i zasobów — [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="32fe5-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="32fe5-306">Zdefiniuj nowy pakiet "Pack" w pakiecie docelowym umożliwiający włączenie możliwości związanych z pakietem — [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="32fe5-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="32fe5-307">Uruchom pakiet jako miejsce docelowe kompilacji postu uwarunkowane właściwością MSBuild "GeneratePackageOnBuild" — [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="32fe5-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="32fe5-308">Użyj Właściwości NuGet RestoreProjectStyle do utworzenia określonego projektu NuGet - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="32fe5-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="32fe5-309">Adaptuj przywracanie dla przechodnich odwołań do projektu — [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="32fe5-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="32fe5-310">Dodaj właściwości NuGet w pliku docelowym dla projektów innych niż platformy uniwersalne — [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="32fe5-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="32fe5-311">Obsługa platformy docelowej platformy uniwersalnej platformy uniwersalnej — [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="32fe5-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="32fe5-312">Komunikuj metadane odwołania do projektu do systemu projektu NuGet — [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="32fe5-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="32fe5-313">Dodaj interfejs użytkownika dla trybu pakowania - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="32fe5-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="32fe5-314">Starsze `.csproj` potrzeby NugetTargetMoniker i RuntimeIdentifiers określone w proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="32fe5-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="32fe5-315">Pakiet instalacyjny może pokrywać się z automatycznym przywracaniem - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="32fe5-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="32fe5-316">Menu kontekstowe QueryStatus nie dzieje się, gdy VSPackage nie jest załadowany - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="32fe5-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="32fe5-317">Przywracanie i przywracanie kompilacji rozwiązania nadal wyświetla okna dialogowe - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="32fe5-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="32fe5-318">Izoluj wersję VSSDK w kompilacji rozwiązania NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="32fe5-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="32fe5-319">Naprawiono łącza do githubu</span><span class="sxs-lookup"><span data-stu-id="32fe5-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="32fe5-320">Lista problemów 1</span><span class="sxs-lookup"><span data-stu-id="32fe5-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="32fe5-321">Lista problemów 2</span><span class="sxs-lookup"><span data-stu-id="32fe5-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="32fe5-322">Lista problemów 3</span><span class="sxs-lookup"><span data-stu-id="32fe5-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="32fe5-323">Lista problemów 4</span><span class="sxs-lookup"><span data-stu-id="32fe5-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="32fe5-324">Lista problemów 5</span><span class="sxs-lookup"><span data-stu-id="32fe5-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
