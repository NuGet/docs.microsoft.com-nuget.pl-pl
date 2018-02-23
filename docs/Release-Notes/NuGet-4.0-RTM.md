---
title: Informacje o wersji RC NuGet 4.0 | Dokumentacja firmy Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o tym znanych problemów, poprawki, dodatkowe funkcje i dcr RTM 4.0 NuGet."
keywords: NuGet 4.0 RTM informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d1ab89f0decb64a64d04dc293e5273b577e8398b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="a7097-104">Informacje o wersji 4.0 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="a7097-104">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="a7097-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z 4.0 NuGet, który dodaje obsługę platformy .NET Core, licznych poprawki jakości i zwiększa wydajność.</span><span class="sxs-lookup"><span data-stu-id="a7097-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="a7097-106">Tej wersji wprowadzono również kilka ulepszeń, takich jak obsługa PackageReference polecenia NuGet jako MSBuild elementy docelowe, przywraca pakietu tła i inne.</span><span class="sxs-lookup"><span data-stu-id="a7097-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a7097-107">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="a7097-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="a7097-108">Przywracanie pakietów NuGet może się nie powieść, jeśli masz wiele projektów odwołujących się do innego projektu w rozwiązaniu</span><span class="sxs-lookup"><span data-stu-id="a7097-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-109">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-109">Issue</span></span>

<span data-ttu-id="a7097-110">Przywracanie pakietów NuGet może nie działać, jeśli w rozwiązaniu istnieją odwołania do projektu do tego samego projektu z inną wielkością liter lub innymi ścieżkami względnymi.</span><span class="sxs-lookup"><span data-stu-id="a7097-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="a7097-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="a7097-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="a7097-112">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-112">Workaround</span></span>

<span data-ttu-id="a7097-113">Napraw wielkość liter lub ścieżki względne w taki sposób, aby były takie same dla wszystkich odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="a7097-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="a7097-114">Podczas korzystania z konsoli Menedżera pakietów może nie działać klawisz „Enter”</span><span class="sxs-lookup"><span data-stu-id="a7097-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-115">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-115">Issue</span></span>

<span data-ttu-id="a7097-116">Czasami klawisz Enter nie działa w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a7097-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="a7097-117">Jeśli tak się dzieje, sprawdź postęp poprawki i podaj wszystkie przydatne informacje dodatkowe dotyczące kroków odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="a7097-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="a7097-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="a7097-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="a7097-119">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-119">Workaround</span></span>

<span data-ttu-id="a7097-120">Uruchom ponownie program Visual Studio, a następnie otwórz konsolę zarządzania pakietami przed otwarciem rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a7097-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="a7097-121">Alternatywnie, spróbuj usunąć `project.lock.json` i przywracanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="a7097-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="a7097-122">W projektach .NET Core użytkownik może pozostać w pętli nieskończonej przywracania w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem</span><span class="sxs-lookup"><span data-stu-id="a7097-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-123">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-123">Issue</span></span>

<span data-ttu-id="a7097-124">Czasami, w przypadku użycia pakietu zawierającego zestaw z nieprawidłowym podpisem lub gdy wersja pakietu została ustawiona za pomocą znacznika „DateTime”, automatyczne przywracanie pakietu będzie uruchamiane w pętli nieskończonej.</span><span class="sxs-lookup"><span data-stu-id="a7097-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="a7097-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="a7097-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="a7097-126">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-126">Workaround</span></span>

<span data-ttu-id="a7097-127">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="a7097-127">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="a7097-128">Nie można wyświetlić, dodać lub zaktualizować DotNetCLITools, za pomocą Menedżera pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="a7097-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-129">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-129">Issue</span></span>

<span data-ttu-id="a7097-130">Menedżer pakietów NuGet nie wyświetla składnika DotNetCLITools ani nie zezwala na jego dodawanie/aktualizowanie.</span><span class="sxs-lookup"><span data-stu-id="a7097-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="a7097-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="a7097-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="a7097-132">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-132">Workaround</span></span>

<span data-ttu-id="a7097-133">Należy ręcznie edytować składnik DotNetCLIToolReferences w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="a7097-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="a7097-134">Przywracanie NuGet zakończy się niepowodzeniem po ustawieniu właściwości PackageId dla projektów</span><span class="sxs-lookup"><span data-stu-id="a7097-134">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-135">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-135">Issue</span></span>

<span data-ttu-id="a7097-136">Dla projektów .NET Core funkcja przywracania NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów.</span><span class="sxs-lookup"><span data-stu-id="a7097-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="a7097-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="a7097-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="a7097-138">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-138">Workaround</span></span>

<span data-ttu-id="a7097-139">Uruchom przywracanie przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7097-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="a7097-140">Gdy projekt nie ma folderu „obj”, przywracanie pakietu może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="a7097-140">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-141">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-141">Issue</span></span>

<span data-ttu-id="a7097-142">Program Visual Studio nie może przywrócić składnika PackageReferences, jeśli folder „obj” został usunięty.</span><span class="sxs-lookup"><span data-stu-id="a7097-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="a7097-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="a7097-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="a7097-144">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-144">Workaround</span></span>

<span data-ttu-id="a7097-145">Gdy utworzysz folder „obj” ręcznie, funkcja przywracania powinna zadziałać.</span><span class="sxs-lookup"><span data-stu-id="a7097-145">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="a7097-146">Ręczna aktualizacja pakietów przy użyciu pakietu aktualizacji w konsoli może zakończyć się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="a7097-146">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-147">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-147">Issue</span></span>

<span data-ttu-id="a7097-148">Ręczne użycie pakietu aktualizacji w konsoli działa tylko jeden raz dla projektów PackageReferences, które zostały właśnie przekonwertowane.</span><span class="sxs-lookup"><span data-stu-id="a7097-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="a7097-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="a7097-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="a7097-150">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-150">Workaround</span></span>

<span data-ttu-id="a7097-151">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="a7097-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="a7097-152">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense</span><span class="sxs-lookup"><span data-stu-id="a7097-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-153">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-153">Issue</span></span>

<span data-ttu-id="a7097-154">Przekierowanie wersji platformy docelowej może prowadzić do niekompletnej funkcji IntelliSense w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7097-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="a7097-155">Dzieje się tak w przypadku używania składnika PackageReferences jako formatu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a7097-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="a7097-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="a7097-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="a7097-157">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-157">Workaround</span></span>

<span data-ttu-id="a7097-158">Wykonaj przywracanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="a7097-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="a7097-159">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt przeznaczony dla platformy .NET461 odwołuje się do innego projektu przeznaczonego dla platformy .NETStandard</span><span class="sxs-lookup"><span data-stu-id="a7097-159">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="a7097-160">Problem</span><span class="sxs-lookup"><span data-stu-id="a7097-160">Issue</span></span>

<span data-ttu-id="a7097-161">Działanie polecenia msbuild /t:restore kończy się niepowodzeniem, gdy projekt oparty na składniku PackageReferenece przeznaczony dla platformy .NET461 odwołuje się do innego projektu opartego na składniku PackageReference przeznaczonego dla platformy .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="a7097-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="a7097-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="a7097-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="a7097-163">Obejście</span><span class="sxs-lookup"><span data-stu-id="a7097-163">Workaround</span></span>

<span data-ttu-id="a7097-164">Obecnie nie istnieje obejście tego problemu.</span><span class="sxs-lookup"><span data-stu-id="a7097-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="a7097-165">Problemy, które usunięto w wersji RTM programu NuGet 4.0 przedziale czasu</span><span class="sxs-lookup"><span data-stu-id="a7097-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="a7097-166">[Informacje o wersji RC 4.0 NuGet](../release-notes/nuget-4.0-RC.md) -Wyświetla wszystkie problemy u NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="a7097-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="a7097-167">Funkcje</span><span class="sxs-lookup"><span data-stu-id="a7097-167">Features</span></span>

- <span data-ttu-id="a7097-168">Localize — ciągi w NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="a7097-168">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="a7097-169">Nuget wymusza załadować projekty aplikacji sieci web w trybie LSL - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="a7097-169">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="a7097-170">Wsparcie AutoReferenced PackageReference wersja bloku zmiany w interfejsie użytkownika dla pakietów "zainstalowany zestaw sdk" - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="a7097-170">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="a7097-171">Poprawnie komunikacji PackageSpec.Version wszelkie zależności projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="a7097-171">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="a7097-172">obsługuje usuwania odwołań w `.csproj` z commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="a7097-172">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="a7097-173">Obsługuje przywracania dla projektów PackageReference (normalny i xplat) i ładowania rozwiązania Lightweight - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="a7097-173">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="a7097-174">obsługę dodawania odwołania do `.csproj` z commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="a7097-174">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="a7097-175">Obsługa Przywracanie NuGet Lightweight ładowania rozwiązania dla `packages.config` lub `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="a7097-175">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="a7097-176">Pliki obsługi w nuget wygenerowany plik elementów docelowych - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="a7097-176">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="a7097-177">Ustanowić CI Mono do weryfikacji nuget.exe dla komputerów Mac przy użyciu programu MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="a7097-177">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="a7097-178">Przenieś NuGet wylogowuje zależności NuGet.Core v2 - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="a7097-178">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="a7097-179">Usterki</span><span class="sxs-lookup"><span data-stu-id="a7097-179">Bugs</span></span>

- <span data-ttu-id="a7097-180">Przywracanie NuGet w programie Visual Studio nie przestrzega właściwości PackageId projektów - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="a7097-180">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="a7097-181">Błąd NuGet ProjectSystemCache podczas dodawania pakietu w pakiecie vsix - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="a7097-181">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="a7097-182">Pakiet zgłasza wyjątek, jeśli IncludeSource jest używany w projekcie z wielu TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="a7097-182">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="a7097-183">Awarie 2017 RC3 VS przy użyciu aktualizacji całym rozwiązaniu pakietów zarządzania — [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="a7097-183">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="a7097-184">Nie można odinstalować nowo zainstalowanego pakietu - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="a7097-184">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="a7097-185">Podczas migracji do PackageRef, hybrydowych rozwiązań zachowują się dziwne przywracania - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="a7097-185">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="a7097-186">Tworzenie wkrótce po uruchamianie NuGet działanie (instalację aktualizacji, przywracania), może spowodować VS do zawieszenia - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="a7097-186">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="a7097-187">Zawieszenie interfejsu użytkownika — Zakleszczenie podczas inicjowania NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="a7097-187">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="a7097-188">Dodaj polecenie pakietu należy dodać wersji jako atrybut zamiast elementu - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="a7097-188">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="a7097-189">Przywróć DotNet foo.sln — kończy się niepowodzeniem, podczas konfiguracji w SLN spowodować wykresu przywracania — projekty zduplikowaną (ale różnicowego config) [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="a7097-189">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="a7097-190">Zawartości tylko pakiety - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="a7097-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="a7097-191">Domyślnie opcja rezygnacji z pakietu format selektor, opcja - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="a7097-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="a7097-192">Danych o wydajności: Projekt CreateUAP_CSharp_VS.01.1.Create uwzględniona Duration_TotalElapsedTime przez 3,153.570 ms (149.1%).</span><span class="sxs-lookup"><span data-stu-id="a7097-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="a7097-193">Plan bazowy 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="a7097-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="a7097-194">Danych o wydajności: Rozwiązanie ManagedLangs_CS_DDRIT.0300.Rebuild uwzględniona Duration_TotalElapsedTime przez 1,5 s.</span><span class="sxs-lookup"><span data-stu-id="a7097-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="a7097-195">Plan bazowy 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="a7097-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="a7097-196">Wyznaczenie zakończy się niepowodzeniem w projektach multi TFM - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="a7097-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="a7097-197">Danych o wydajności: Rozwiązanie WebForms_DDRIT.1200.Close uwzględniona VM_ImagesInMemory_Total_devenv według liczby 3.000 (0,5%).</span><span class="sxs-lookup"><span data-stu-id="a7097-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="a7097-198">Plan bazowy 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="a7097-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="a7097-199">vsfeedback — pakiet ostrzeżenia, gdy netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="a7097-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="a7097-200">Pathtoolongexception — podczas próby dodania pakiet NuGet do pustych aplikacji sieci web platformy ASP.NET Core - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="a7097-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="a7097-201">Pakiet jest uruchamiany zbyt często — dotnet pakietu zakończy się niepowodzeniem z nim to zależność cykliczną w docelowym zależności wykres obejmujące docelowej "Pakiet" - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="a7097-201">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="a7097-202">Pakiet jest uruchamiany zbyt często — pakiet NuGet Generowanie nie zawiera wszystkie konfiguracje - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="a7097-202">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="a7097-203">Dodawanie nuget NullReferenceException z packageref w projektach C++ - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="a7097-203">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="a7097-204">Ułatwienia dostępu: Narrator nie komentować pole wyboru, aby Wybierz projekty, do zainstalowania pakietu do - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="a7097-204">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="a7097-205">NuGet VS17 sporadycznie niepowodzenia nawiązywania połączenia źródła danych usługi VSO/VSTS — 365798 usterki VS - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="a7097-205">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="a7097-206">Pliki pobierać dane wyjściowe do niewłaściwej lokalizacji, jeżeli PackagePath Określa ścieżkę jako "pliki" - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="a7097-206">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="a7097-207">Docelowy pakiet dołącza właściwość PackageVersion o VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="a7097-207">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="a7097-208">Określanie ścieżki pakietu nie działa z dodatkiem Service pack dotnet — [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="a7097-208">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="a7097-209">NuGet dane wyjściowe licznych ostrzeżenia o zduplikowane Importy podczas przywracania - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="a7097-209">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="a7097-210">Wybierz wygląd okna dialogowego "Menedżer pakietów NuGet Format" w obszarze ciemny motyw — [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="a7097-210">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="a7097-211">VS awarii przy przywracaniu kompilacji - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="a7097-211">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="a7097-212">Visual Studio zakleszczenie po dodaniu TFM w targetframeworks, Zapisz, a następnie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a7097-212">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="a7097-213">10% czasu - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="a7097-213">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="a7097-214">Pakiet nuget nie wyprowadza komunikat z potwierdzeniem na pakowania projektu- [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="a7097-214">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="a7097-215">PackTask zakończy się niepowodzeniem z powodu 4.1 System.IO.Compression nie można odnaleźć - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="a7097-215">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="a7097-216">Pakiet jest uruchamiany zbyt często — PackTask często kończy się niepowodzeniem z konflikt dostępu do pliku - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="a7097-216">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="a7097-217">NuGet zostanie otwarte okno danych wyjściowych podczas przywracania tła - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="a7097-217">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="a7097-218">Wyeliminować element ServiceProvider jako niebezpieczne wzorzec kodowania, (co może spowodować zawieszeń) - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="a7097-218">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="a7097-219">Wydajności/UIHang - poprawy odczyty DownloadTimeoutStream - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="a7097-219">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="a7097-220">Zakleszczenie programu Visual Studio przy próbie Zamknij projekt zanim zakończy przywracanie NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="a7097-220">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="a7097-221">Problemy z PackTask i pakowania `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="a7097-221">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="a7097-222">[vsfeedback] Nie można rozpoznać pakietów nuget dla nowego projektu (wymaga ponownego uruchomienia programu visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="a7097-222">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="a7097-223">[vsfeedback] "Wersja" listy rozwijanej, które zawiera wersje dostępnych pakietów, zmagania pozostanie zsynchronizowana z pakietu nuGet wybranego... - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="a7097-223">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="a7097-224">Nuget.Client powinna być używana klasa JoinableTaskFactory CPS podczas interakcji z CPS do zapobiec zakleszczenie - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="a7097-224">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="a7097-225">NuGet 3.5.0 nie rozpakowywania `.targets` z pakietu - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="a7097-225">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="a7097-226">Pakiet DotNet nie obsługuje tytuł w `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="a7097-226">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="a7097-227">Pakiet instalacyjny powoduje okna dialogowego błędu w wersji VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="a7097-227">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="a7097-228">Aktualizowanie pakietu dla platformy .net core projektu wydaje się nie działać zgodnie z interfejsu użytkownika nie Pobierz aktualizację CPS z nominate.</span><span class="sxs-lookup"><span data-stu-id="a7097-228">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="a7097-229"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="a7097-229"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="a7097-230">Poprawa ostrzeżenie nierozpoznane odwołanie - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="a7097-230">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="a7097-231">Pakiet DotNet — informacje o wersji — utraci ProjectReference [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="a7097-231">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="a7097-232">Tworzenie aplikacji platformy uniwersalnej systemu Windows tworzenia projektu i Odbuduj regresji całkowity czas — [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="a7097-232">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="a7097-233">Nawet po błędzie podczas przywracania zostanie wyświetlony komunikat przywrócone.</span><span class="sxs-lookup"><span data-stu-id="a7097-233">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="a7097-234"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="a7097-234"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="a7097-235">ponownie opublikować Nuget.CommandLine 3.4.4 do Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="a7097-235">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="a7097-236">Na migracji, projekty zmienić z `project.json` do `.csproj` ---przywracania kończy się niepowodzeniem - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="a7097-236">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="a7097-237">Niepowodzenie przywracania na xunit nowo utworzonego projektu testowego - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="a7097-237">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="a7097-238">Projekty Core mogą wykraczać, blokowanie interfejsu użytkownika na open - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="a7097-238">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="a7097-239">Napraw plik elementów docelowych dla zadania kompilacji — [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="a7097-239">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="a7097-240">Lista błędów zawiera błąd po kompilacji rozwiązania, które zwolnić przywoływanego projektu - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="a7097-240">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="a7097-241">MSB4057: Element docelowy "_GenerateRestoreGraphProjectEntry" nie istnieje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="a7097-241">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="a7097-242"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="a7097-242"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="a7097-243">vsfeedback: interfejsu użytkownika Menedżera nuget dla rozwiązania ulegnie awarii po wybraniu wszystkich projektów - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="a7097-243">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="a7097-244">nuget.exe msbuildpath zakończy się niepowodzeniem, jeśli znajduje się znakiem ukośnika — [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="a7097-244">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="a7097-245">vsfeedback: Przywracanie NuGet podać kilka ostrzeżeń odwołania projektu dla projektu LinqToTwitter - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="a7097-245">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="a7097-246">Pakiet z `.csproj` nie ma atrybutu minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="a7097-246">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="a7097-247">NuGet.Build.Tasks.Pack.dll dostarczanego delay zalogowany VS2017 (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="a7097-247">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="a7097-248">VSFeedback: Przywracanie nie powiodło się dla projektu programu VS 2015 wygenerowane z CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="a7097-248">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="a7097-249">VSFeedback: Błędy odtwarzania mogą przesłaniać bardziej szczegółowy komunikaty o błędach, które zapewniają można kompilacji — [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="a7097-249">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="a7097-250">[VSFeedback] Wystąpił błąd podczas przywracania pakietów NuGet dla projektu witryny sieci Web: wartość nie może mieć wartości null.</span><span class="sxs-lookup"><span data-stu-id="a7097-250">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="a7097-251"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="a7097-251"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="a7097-252">Migracja zgłasza "Obiektu odwołania wyjątek" w NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="a7097-252">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="a7097-253">Pakiet DotNet powinien pakietu narzędzi z wersjami, które pakiet został utworzony przed - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="a7097-253">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="a7097-254">Nowe przywracania tła zapisuje milisekund pasek gdy trwa sekund, aby przywrócić - stanu [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="a7097-254">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="a7097-255">Literówka w nie udało się rozwiązać, wszystkie projektu odwołań - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="a7097-255">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="a7097-256">Włącz przepływy pracy PCM w scenariuszach odwołanie do pakietu - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="a7097-256">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="a7097-257">Nie można odnaleźć zainstalowanych pakietów w pakiecie menedżera interfejsu użytkownika — [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="a7097-257">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="a7097-258">DotNet pakietu nie powiedzie się, gdy PackagePath jest pusty — [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="a7097-258">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="a7097-259">Przywróć zadań kończy się niepowodzeniem w scenariuszu użytkownik multi - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="a7097-259">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="a7097-260">Nie można zmienić typu zawartości, podczas pakowania, za pomocą zadania pakiet NuGet- [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="a7097-260">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="a7097-261">Kopiuj pliki domyślne są nieprawidłowe dla MsBuild /t:pack — [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="a7097-261">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="a7097-262">Przywracanie pakietu instalacji podwójne rejestruje przywracania komunikat pakiety - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="a7097-262">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="a7097-263">Usuń Guardrails - przywracania sekcji "środowisk uruchomieniowych" stosuje się tylko do bieżącego projektu - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="a7097-263">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="a7097-264">Zadanie pakietów umieszcza pliki zawartości zarówno w "zawartości /" i "pliki /"- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="a7097-264">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="a7097-265">DotNet dodatkiem Service Pack 3 bardzo tagu dzielenia - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="a7097-265">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="a7097-266">Pakiet DotNet: pakowania projektów z pakietem odwołuje się do wyników w ostrzeżenie zduplikowane import - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="a7097-266">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="a7097-267">Przywróć rejestrowania w programie VS nie zawsze pokazuj - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="a7097-267">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="a7097-268">tekst pomocy zmiennych lokalnych nuget wymienionych nadal pamięci podręcznej pakiety - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="a7097-268">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="a7097-269">Pozamałżeńskie Restore3 PackageReferences z TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="a7097-269">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="a7097-270"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="a7097-270"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="a7097-271">Nuget wybiera nieoczekiwany wersji programu MSBuild w programie VS "15" Preview 4 odchyleń</span><span class="sxs-lookup"><span data-stu-id="a7097-271">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="a7097-272">Wiersz polecenia - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="a7097-272">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="a7097-273">Zapis plików celów/arkuszy właściwości podczas przywracania nie powiodło się - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="a7097-273">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="a7097-274">NuGet podczas przywracania nie jest zgodny tego samego podkładek compat jako MSBuild podczas uruchamiania w wierszu polecenia VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="a7097-274">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="a7097-275">Ponownie włącz PackFromProjectWithDevelopmentDependencySet dla VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="a7097-275">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="a7097-276">Blend problemów z programem NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="a7097-276">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="a7097-277">Integrowanie 4.0.0.2067 interfejsu wiersza polecenia i zestawu SDK repozytoriów dostarczany z RC2 — [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="a7097-277">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="a7097-278">VS zawieszeń podczas tworzenia nowej aplikacji konsoli Core, Zamknij rozwiązanie, otwórz rozwiązanie i Zamknij rozwiązanie - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="a7097-278">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="a7097-279">Naciśnięcie zawieszenie otwierania projektu przed d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="a7097-279">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="a7097-280">Usuń elementy lokalne dotnet/nuget.exe komunikat pomocy doc — [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="a7097-280">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="a7097-281">Sprawdzenia pod kątem problemów z spacji końcowych lub początkowych - PackTask [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="a7097-281">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="a7097-282">Pakiet DotNet jest pakowania z obj nie bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="a7097-282">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="a7097-283">Pakiet DotNet zawsze wydaje się, że wartość elementu ProjectReference w wersji 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="a7097-283">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="a7097-284">Pakiet DotNet kończy się niepowodzeniem z odwołań do projektu i <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="a7097-284">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="a7097-285">LockRecursionException w ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="a7097-285">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="a7097-286">TRIM z wartości właściwości programu MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="a7097-286">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="a7097-287">Konsoliduj zdarzenia dwóch projektu zgłoszony podczas ładowania projektu — [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="a7097-287">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="a7097-288">Bibliotek p2p `project.assets.json` plik ma nieprawidłową wersję - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="a7097-288">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="a7097-289">Przywróć awarii z powodu źródło danych nie odpowiada, a pakiet niedostępny — [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="a7097-289">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="a7097-290">nuget.exe mogą powodować zawieszanie na dużą ilość danych wyjściowych błąd MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="a7097-290">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="a7097-291">Przywracanie w kompilacji dla programu Blend nie powiedzie się po raz pierwszy, powiedzie się po raz drugi (VS scenariusz rozwiązany) — [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="a7097-291">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="a7097-292">Dcr</span><span class="sxs-lookup"><span data-stu-id="a7097-292">DCRs</span></span>

- <span data-ttu-id="a7097-293">migracji vsix z Instalatora vsix w wersji 2 do vsix w wersji 3 - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="a7097-293">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="a7097-294">NuGet powinien mieć mechanizmu uzyskiwania ścieżki do pliku blokady w programie MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="a7097-294">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="a7097-295">Dodaj zasoby kompilacji do TFM zgodności wyboru i zasoby pliku - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="a7097-295">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="a7097-296">Zdefiniuj nowy ProjectCapability "Pakiet" w pakiecie cele dotyczące włączania pakietu dotyczące możliwości — [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="a7097-296">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="a7097-297">Uruchom pakiet jako post kompilacji docelowy przygotować we właściwości "GeneratePackageOnBuild" MSBuild - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="a7097-297">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="a7097-298">Użyj właściwości NuGet RestoreProjectStyle do utworzenia danego projektu NuGet - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="a7097-298">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="a7097-299">Dostosowania przywracania przechodnie odwołania do projektu zmian - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="a7097-299">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="a7097-300">Dodaj właściwości NuGet w pliku docelowym dla projektów aplikacje platformy UWP - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="a7097-300">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="a7097-301">Obsługa platformy uniwersalnej systemu Windows TargetPlatformVersion - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="a7097-301">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="a7097-302">Komunikacji metadanych odwołania projektu do systemu projektu NuGet - [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="a7097-302">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="a7097-303">Dodawanie interfejsu użytkownika dla trybu tworzenia pakietów - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="a7097-303">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="a7097-304">Starsza wersja `.csproj` potrzebuje NugetTargetMoniker i RuntimeIdentifiers w proj/cele — [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="a7097-304">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="a7097-305">Pakiet instalacyjny nakładają się z przywracaniem auto - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="a7097-305">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="a7097-306">Menu kontekstowe QueryStatus nie jest realizowane podczas VSPackage nie został załadowany - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="a7097-306">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="a7097-307">Przywróć rozwiązania i przywrócić kompilacji w dalszym ciągu wyświetlać okien dialogowych - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="a7097-307">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="a7097-308">Odizolowanego wersji VSSDK w kompilacji rozwiązania NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="a7097-308">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="a7097-309">Łącza do GitHub problemy rozwiązane w wersji RTM</span><span class="sxs-lookup"><span data-stu-id="a7097-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="a7097-310">Lista problemów 1</span><span class="sxs-lookup"><span data-stu-id="a7097-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="a7097-311">Lista problemów 2</span><span class="sxs-lookup"><span data-stu-id="a7097-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="a7097-312">Lista problemów 3</span><span class="sxs-lookup"><span data-stu-id="a7097-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="a7097-313">Lista problemów 4</span><span class="sxs-lookup"><span data-stu-id="a7097-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="a7097-314">Lista problemów 5</span><span class="sxs-lookup"><span data-stu-id="a7097-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
