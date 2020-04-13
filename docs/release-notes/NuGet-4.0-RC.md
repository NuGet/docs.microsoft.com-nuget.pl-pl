---
title: Informacje o wersji nuGet 4.0 RC
description: Informacje o wersji dla NuGet 4.0 RC, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496646"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="83f92-103">Informacje o wersji nuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="83f92-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="83f92-104">Informacje o wydaniu programu NuGet 3.5 RTM</span><span class="sxs-lookup"><span data-stu-id="83f92-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="83f92-105">[NuGet 4.0 RC dla programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na dodawaniu obsługi scenariuszy .NET Core, adresowaniu kluczowych opinii klientów i zwiększaniu wydajności w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="83f92-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="83f92-106">Ta wersja zawiera kilka ulepszeń, takich jak obsługa PackageReference, Polecenia NuGet jako obiekty docelowe MSBuild, przywracanie pakietu w tle i inne.</span><span class="sxs-lookup"><span data-stu-id="83f92-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="83f92-107">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="83f92-107">Bug Fixes</span></span>

- <span data-ttu-id="83f92-108">Zmiany zachowań `dotnet pack --version-suffix foo`  - w [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="83f92-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="83f92-109">nuget.exe przywracanie na vs "15" komputer tylko nie powiedzie się - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="83f92-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="83f92-110">. NetCore plik nowy projekt powinien blokować kompilacji podczas przywracania - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="83f92-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="83f92-111">ASP.NET podstawowej aplikacji sieci web, migracji z VS2015 do VS "15", nie można przywrócić.</span><span class="sxs-lookup"><span data-stu-id="83f92-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="83f92-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="83f92-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="83f92-113">[Błąd testu] Pakietu "jQuery Validation" nie można odinstalować przez interfejs użytkownika PM - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="83f92-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="83f92-114">Gdy pakiet jest zainstalowany `project.json`na platformie UNIWERSALNEJ systemu Windows, projekty nadrzędne powinny również zostać przywrócone - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="83f92-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="83f92-115">Zmodyfikuj obiekty docelowe NuGet, aby rejestrować źródła pakietu jako wysoka szczegółowość zamiast normalnych [— #3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="83f92-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="83f92-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="83f92-116">dotnet</span></span>
  - <span data-ttu-id="83f92-117">dotnetcore pack3 powinien domyślnie zawierać dokumentację XML - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="83f92-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="83f92-118">Aktualizacja wsadowa kończy się niepowodzeniem z interfejsu użytkownika, gdy źródło bez pakietu jest pierwsze i wybrano wszystkie źródło - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="83f92-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="83f92-119">Polecenie Nuget pack nie zawiera wszystkich plików - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="83f92-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="83f92-120">Problem OOM - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="83f92-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="83f92-121">ProjectFileDependencyGroups sekcji pliku zasobów należy użyć nazw bibliotek dla projektów - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="83f92-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="83f92-122">"dotnet restore" i powtarzające się katalogi - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="83f92-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="83f92-123">Błędy przywracania3 są rejestrowane jako ostrzeżenia zamiast błędów - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="83f92-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="83f92-124">Problem z TFS: "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego" - [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="83f92-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="83f92-125">Wpisując "nuget <packagename>" w polu wyszukiwania vs quicklaunch zachowuje prefiks "nuget " - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="83f92-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="83f92-126">System.Xml.XmlException: Nierozpoznany element główny w części Właściwości rdzenia.</span><span class="sxs-lookup"><span data-stu-id="83f92-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="83f92-127">Linia 2, pozycja 2.</span><span class="sxs-lookup"><span data-stu-id="83f92-127">Line 2, position 2.</span></span><span data-ttu-id="83f92-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="83f92-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="83f92-129">`.nuspec`z &lt; przestawną lub &gt; w polach tekstowych nie buduje - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="83f92-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="83f92-130">nuget.exe delete nie monituje o poświadczenia (jest w trybie nieinterakcyjnym) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="83f92-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="83f92-131">nuget.exe delete ostrzega o kluczu INTERFEJSU API dla źródeł lokalnych, mimo że nie ma sensu - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="83f92-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="83f92-132">Podczas instalowania pakietu EF -pre package — [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="83f92-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="83f92-133">Visual Studio uległ awarii po zmianie wyboru w Menedżerze pakietów - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="83f92-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="83f92-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="83f92-134">dotnet</span></span>
  - <span data-ttu-id="83f92-135">przywracanie dotnetcore wykonuje wyszukiwania identyfikatorów z uwzględnieniem wielkości liter w repozytoriach lokalnych z płaską listą, gdy używane są wersje przestawne — [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="83f92-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="83f92-136">nuget.exe delete jest uszkodzony dla kanału V2 - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="83f92-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="83f92-137">limit czasu wypychania nuget.exe wymaga lepszego komunikatu o błędzie - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="83f92-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="83f92-138">Przywracanie narzędzia bez prawidłowego importu po cichu kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="83f92-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="83f92-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="83f92-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="83f92-140">NuGet monituje o wprowadzenie poświadczeń, gdy istnieje prywatny kanał informacyjny, nawet podczas instalacji z nuget.org — [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="83f92-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="83f92-141">Pakiet ApplicationInsights 2.0 jest wymieniony, ale jeszcze nie istnieje — [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="83f92-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="83f92-142">UIDelay w VS "15" podgląd 5 oddział - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="83f92-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="83f92-143">Pierwsze zdarzenie OnBuild jest pomijane dla przywracania podczas kompilacji dla platformy uniwersalnej systemu i platformy uniwersalnej — [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="83f92-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="83f92-144">Program PowerShell5 przerywa instalację programu EntityFramework?</span><span class="sxs-lookup"><span data-stu-id="83f92-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="83f92-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="83f92-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="83f92-146">Dodaj źródło do szczegółowego rejestrowania (należy wziąć pod uwagę dla 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="83f92-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="83f92-147">Parametr NoCache nie jest honorowany w wersji klienta nuget 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="83f92-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="83f92-148">Gdy dostawca poświadczeń nie można załadować w programie VS, nie przerywaj nuget - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="83f92-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="83f92-149">Funkcje</span><span class="sxs-lookup"><span data-stu-id="83f92-149">Features</span></span>

- <span data-ttu-id="83f92-150">Konfigurowanie ciągłego uruchamiania w celu uruchomienia x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="83f92-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="83f92-151">Automatyczne przywracanie 3/3: nieblokowanie interfejsu użytkownika - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="83f92-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="83f92-152">Auto Restore 2/3: przywracanie tła przy nominacji - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="83f92-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="83f92-153">Przywróć refs projektu, aby dopasować zachowanie kompilacji (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="83f92-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="83f92-154">Obsługa DPL w VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="83f92-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="83f92-155">Przenieś plik ustawień do plików programu - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="83f92-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="83f92-156">Wygenerowane rekwizyty i cele przywracania wymagają wsparcia uczestnictwa w przekroju - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="83f92-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="83f92-157">Obsługa nuget restore dla PackageTargetFallback (f.k.a Imports) — [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="83f92-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="83f92-158">Implementacja ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="83f92-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="83f92-159">Restore3 dla rid - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="83f92-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="83f92-160">NuGet UI do obsługi dodaj/usuń/aktualizuj y packagerefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="83f92-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="83f92-161">Auto Restore 1/3: Implemenation nominacji API za pośrednictwem buforowania project restore info - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="83f92-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="83f92-162">[0] Cele & zadań przywracania nuget - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="83f92-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="83f92-163">[1] Włącz przywracanie poziomu rozwiązania w MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="83f92-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="83f92-164">Publiczne rozszerzalność dostawcy poświadczeń pomocy technicznej w programie Visual Studio [— #2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="83f92-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="83f92-165">Rekursywne przywracanie nuget - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="83f92-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="83f92-166">Nie można załadować microsoft.TeamFoundation.Client na dev15, trzeba zaktualizować wersję Microsoft.TeamFoundation.Client do 15.0 dla VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="83f92-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="83f92-167">Nie można zainstalować pakietu C++ w projekcie platformy uniwersalnej systemu Windows w programie VS "15" Preview — [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="83f92-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="83f92-168">Nupkg musi obsługiwać folder \buildCrossTargeting\ i importować `.targets`  /  `.props` dla "crosstargeting" zakres MSBuild.</span><span class="sxs-lookup"><span data-stu-id="83f92-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="83f92-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="83f92-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="83f92-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="83f92-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="83f92-171">Napraw interfejs użytkownika NuGet do obsługi przywracania `.csproj`  - w/ PackageReferences w [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="83f92-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="83f92-172">Dodawanie przycisku wyczyść pamięć podręczną do ustawień menedżera pakietów VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="83f92-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="83f92-173">DDR</span><span class="sxs-lookup"><span data-stu-id="83f92-173">DCRs</span></span>

- <span data-ttu-id="83f92-174">Przywracanie rozwiązania powinno być blokowane podczas automatycznego przywracania.</span><span class="sxs-lookup"><span data-stu-id="83f92-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="83f92-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="83f92-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="83f92-176">NetCore zainstalować z NuGet Package Manager UI instaluje się do każdego TFM , zamiast tych, które obsługuje pakiet - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="83f92-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="83f92-177">Przywróć nominator API musi obsługiwać DotNetCliToolsReferences zbyt.</span><span class="sxs-lookup"><span data-stu-id="83f92-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="83f92-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="83f92-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="83f92-179">Oznacz vs "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="83f92-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="83f92-180">Migrowanie z odwoływania się do MS. Vs. Services.Client do MS. Vs. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="83f92-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="83f92-181">$(RestoreLegacyPackagesDirectory) powinny być przestrzegane na poziomie projektu przez restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="83f92-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="83f92-182">Przywracanie do projektu za pomocą pojedynczego targetframework nie może kondycjonować rekwizytów - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="83f92-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="83f92-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="83f92-183">dotnet</span></span>
  - <span data-ttu-id="83f92-184">dotnetcore restore3 foo.csproj powinien podążać za zależnościami projectref i przywracać te również.</span><span class="sxs-lookup"><span data-stu-id="83f92-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="83f92-185">Jak budować.</span><span class="sxs-lookup"><span data-stu-id="83f92-185">Like build.</span></span><span data-ttu-id="83f92-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="83f92-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="83f92-187">"type": zależności "platformy" reprezentowane jako "typ":"pakiet" w pliku blokady - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="83f92-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="83f92-188">nuget.exe Tryb verbose powinien pokazać adres URL pobierania - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="83f92-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="83f92-189">Przenieś nuget xplat do microsoft.NetCore.App i netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="83f92-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="83f92-190">Push - Powinno być możliwe zastąpienie serwera symboli podczas wypychania z wiersza polecenia - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="83f92-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="83f92-191">Skonsoliduj kod do znajdowania ścieżki pakietów globalnych — [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="83f92-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="83f92-192">Potrzebujesz lepszej nazwy niż suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="83f92-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="83f92-193">Określanie `project.json` nazwy zależności do użycia dla projektów MSBuild — [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="83f92-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="83f92-194">Dodaj obsługę SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="83f92-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="83f92-195">Zezwalaj na przechodnie zależności `.targets` NuPkgs z być dostępne w MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="83f92-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="83f92-196">Przywracanie NuGet z wiersza polecenia jest znacznie wolniejsze niż VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="83f92-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="83f92-197">Spraw, aby identyfikator pakietu i przypadek porównania wersji były niewrażliwe - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="83f92-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="83f92-198">Opcja NoCache nie `packages.config` działa w przypadku przywracania/instalowania na podstawie (GlobalPackagesFolder) — [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="83f92-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="83f92-199">FindPackageByIdResource zasobów potrzebuje domyślnego kontekstu pamięci podręcznej i rejestratora - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="83f92-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
