---
title: Informacje o wersji RC NuGet 4.0
description: Informacje o wersji programu NuGet 4.0 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="3eddd-103">Informacje o wersji RC NuGet 4.0</span><span class="sxs-lookup"><span data-stu-id="3eddd-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="3eddd-104">Informacje o wersji 3.5 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="3eddd-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="3eddd-105">[RC 4.0 NuGet dla programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na obsługę scenariuszy .NET Core, odpowiedzi na opinie klientów klucza i poprawia wydajność w wielu scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="3eddd-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="3eddd-106">Tej wersji wprowadzono kilka ulepszeń, takich jak obsługa PackageReference, polecenia, jako docelowych elementów MSBuild i tła przywracania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="3eddd-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="3eddd-107">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="3eddd-107">Bug Fixes</span></span>

- <span data-ttu-id="3eddd-108">Zmiany zachowania `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="3eddd-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="3eddd-109">Przywracanie nuget.exe dla vs "15" tylko komputera nie powiodło się — [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="3eddd-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="3eddd-110">. NETCore pliku nowego projektu należy zablokować kompilacji podczas przywracania - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="3eddd-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="3eddd-111">Aplikacja sieci web platformy ASP.NET Core, migracja z programu VS2015 do wersji programu VS "15", nie można przywrócić.</span><span class="sxs-lookup"><span data-stu-id="3eddd-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="3eddd-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="3eddd-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="3eddd-113">[Błąd podczas badania] Nie można odinstalować pakietu "jQuery weryfikacji" przez interfejs użytkownika PM - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="3eddd-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="3eddd-114">Po zainstalowaniu pakietu do platformy uniwersalnej systemu Windows `project.json`, również powinny zostać przywrócone projektów nadrzędny - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="3eddd-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="3eddd-115">Zmodyfikuj elementy docelowe NuGet do rejestrowania źródeł pakietów jako wysoki poziom szczegółowości zamiast normalny - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="3eddd-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="3eddd-116">DotNet</span><span class="sxs-lookup"><span data-stu-id="3eddd-116">dotnet</span></span>
  - <span data-ttu-id="3eddd-117">dotnetcore dodatkiem Service Pack 3 powinna zawierać dokumentację XML domyślnie - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="3eddd-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="3eddd-118">Wsadowe aktualizacji nie powiedzie się z poziomu interfejsu użytkownika po wybraniu wszystkich źródła - i źródła bez pakietu zostanie najpierw [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="3eddd-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="3eddd-119">Polecenie pakietu Nuget nie zawiera wszystkie pliki - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="3eddd-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="3eddd-120">Za mało pamięci problem - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="3eddd-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="3eddd-121">ProjectFileDependencyGroups sekcji pliku zasobów należy używać nazwy biblioteki dla projektów - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="3eddd-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="3eddd-122">"Przywracanie dotnet" i recursing katalogów - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="3eddd-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="3eddd-123">Restore3 błędy są rejestrowane jako ostrzeżenia zamiast błędy - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="3eddd-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="3eddd-124">Problem TFS: "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="3eddd-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="3eddd-125">Wpisz "nuget <packagename>" w programie vs pole wyszukiwania szybkiego uruchamiania śledzi prefiksu "nuget" - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="3eddd-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="3eddd-126">System.Xml.XmlException: Nierozpoznany element główny w części Core Properties.</span><span class="sxs-lookup"><span data-stu-id="3eddd-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="3eddd-127">Wiersz 2, pozycji 2.</span><span class="sxs-lookup"><span data-stu-id="3eddd-127">Line 2, position 2.</span></span><span data-ttu-id="3eddd-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="3eddd-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="3eddd-129">`.nuspec` o znaczeniu zmienionym &lt; lub &gt; pól w tekście już kompilacje - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="3eddd-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="3eddd-130">Usuń nuget.exe nie monit o podanie poświadczeń (jest w trybie nieinterakcyjnym) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="3eddd-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="3eddd-131">Usuń nuget.exe ostrzeganie o klucz interfejsu API dla lokalnych źródeł, nawet jeśli nie ma sensu - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="3eddd-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="3eddd-132">Słaby środowisko błąd podczas instalowania pakietu wersji pre - EF - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="3eddd-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="3eddd-133">Visual Studio awarii próby po zmianie zaznaczenia w Menedżerze pakietów - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="3eddd-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="3eddd-134">DotNet</span><span class="sxs-lookup"><span data-stu-id="3eddd-134">dotnet</span></span>
  - <span data-ttu-id="3eddd-135">Przywracanie dotnetcore wykonuje wyszukiwań identyfikator z uwzględnieniem wielkości liter na płaski listy repozytoriów lokalnych stosowania przestawne wersji — [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="3eddd-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="3eddd-136">Usuń nuget.exe został przerwany dla źródła danych w wersji 2 - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="3eddd-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="3eddd-137">limit wypychania nuget.exe musi komunikat o błędzie lepsze - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="3eddd-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="3eddd-138">Narzędzie przywracania bez odpowiedniego dyskretnie importuje kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3eddd-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="3eddd-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="3eddd-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="3eddd-140">NuGet wyświetla monit o podanie poświadczeń, gdy jest prywatny źródła strumieniowego nawet w przypadku instalowania z nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="3eddd-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="3eddd-141">Pakiet ApplicationInsights 2.0 jest wyświetlane, ale nie istnieje jeszcze — [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="3eddd-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="3eddd-142">UIDelay w programie VS "15" preview gałęzi 5 - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="3eddd-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="3eddd-143">Pierwsze zdarzenie OnBuild zostało pominięte przywracane podczas kompilacji dla platformy uniwersalnej systemu Windows - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="3eddd-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="3eddd-144">Podziały PowerShell5 EntityFramework zainstalować?</span><span class="sxs-lookup"><span data-stu-id="3eddd-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="3eddd-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="3eddd-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="3eddd-146">Dodawanie źródła danych do szczegółowe rejestrowanie (należy wziąć pod uwagę 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="3eddd-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="3eddd-147">Parametr NoCache nie honorowane w wersji klienta nuget 3.4 + - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="3eddd-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="3eddd-148">W przypadku awarii Dostawca poświadczeń do załadowania w programie VS Nie dziel NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="3eddd-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="3eddd-149">Funkcje</span><span class="sxs-lookup"><span data-stu-id="3eddd-149">Features</span></span>

- <span data-ttu-id="3eddd-150">Konfigurowanie elementu konfiguracji do uruchamiania x86- [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="3eddd-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="3eddd-151">Automatyczne przywracanie 3/3: z systemem innym niż blokujące elementy interfejsu użytkownika — [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="3eddd-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="3eddd-152">Automatyczne przywracanie 2/3: w tle przywracania na wyznaczenie - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="3eddd-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="3eddd-153">Przywróć system plików refs projektu do dopasowania zachowanie kompilacji (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="3eddd-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="3eddd-154">DPL obsługi w programie VS "15" — minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="3eddd-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="3eddd-155">Przenieś plik ustawień do plików programu - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="3eddd-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="3eddd-156">Właściwości wygenerowanego przywracania i obiektów docelowych niezbędna jest obsługa udział przeznaczonych dla różnych - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="3eddd-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="3eddd-157">Przywracanie NuGet obsługę PackageTargetFallback (f.k.a importów) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="3eddd-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="3eddd-158">Implementacja ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="3eddd-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="3eddd-159">Restore3 dla identyfikatora RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="3eddd-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="3eddd-160">NuGet interfejsu użytkownika Służącego do obsługi Dodaj/Usuń/aktualizacja PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="3eddd-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="3eddd-161">Automatyczne przywracanie 1/3: Implementacji wyznaczenie interfejsu API za pomocą buforowanie projektu przywrócić informacje - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="3eddd-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="3eddd-162">[0] NuGet przywracanie zadań & cele — [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="3eddd-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="3eddd-163">[1] Włącz rozwiązania poziomu przywracania w programie MSBuild — [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="3eddd-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="3eddd-164">Obsługuje rozszerzalności publicznego dostawcy poświadczeń w programie Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="3eddd-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="3eddd-165">Przywracanie nuget cykliczne - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="3eddd-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="3eddd-166">Nie można załadować Microsoft.TeamFoundation.Client na dev15, należy zaktualizować wersję Microsoft.TeamFoundation.Client do 15.0 dla wersji programu VS "15" wersja zapoznawcza — [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="3eddd-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="3eddd-167">Nie można zainstalować pakietu C++ do platformy uniwersalnej systemu Windows w języku C++ projektu w programie VS "15" wersja zapoznawcza — [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="3eddd-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="3eddd-168">Nupkg musi obsługiwać folderu \buildCrossTargeting\ - i zaimportować `.targets`  /  `.props` dla "crosstargeting" MSBuild zakresu.</span><span class="sxs-lookup"><span data-stu-id="3eddd-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="3eddd-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="3eddd-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="3eddd-170">Projekt ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="3eddd-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="3eddd-171">Usuń NuGet interfejsu użytkownika Służącego do obsługi przywracania z PackageReferences w `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="3eddd-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="3eddd-172">Dodawanie przycisk Wyczyść pamięć podręczną, aby ustawienia Menedżera pakietów programu VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="3eddd-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="3eddd-173">Dcr</span><span class="sxs-lookup"><span data-stu-id="3eddd-173">DCRs</span></span>

- <span data-ttu-id="3eddd-174">Przywracanie rozwiązanie powinno zostać zablokowane podczas przywracania automatycznie wykonywane.</span><span class="sxs-lookup"><span data-stu-id="3eddd-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="3eddd-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="3eddd-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="3eddd-176">NetCore instalacji z interfejsu użytkownika Menedżera pakietów NuGet instaluje co TFM, zamiast tych, które obsługuje pakiet - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="3eddd-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="3eddd-177">Przywróć nominator interfejsu API musi obsługiwać DotNetCliToolsReferences zbyt.</span><span class="sxs-lookup"><span data-stu-id="3eddd-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="3eddd-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="3eddd-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="3eddd-179">Oznacz naszych VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="3eddd-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="3eddd-180">Migracja z odwołujące się do MS. VS. Services.Client MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="3eddd-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="3eddd-181">$(RestoreLegacyPackagesDirectory) powinny być przestrzegane na poziomie projektu przez przywrócenie - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="3eddd-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="3eddd-182">Przywracanie do projektu z jednym TargetFramework musi nie warunku właściwości — [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="3eddd-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="3eddd-183">DotNet</span><span class="sxs-lookup"><span data-stu-id="3eddd-183">dotnet</span></span>
  - <span data-ttu-id="3eddd-184">dotnetcore restore3 foo.csproj należy wykonaj projectref zależności i przywrócić te zbyt.</span><span class="sxs-lookup"><span data-stu-id="3eddd-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="3eddd-185">Podobnie jak kompilacji.</span><span class="sxs-lookup"><span data-stu-id="3eddd-185">Like build.</span></span><span data-ttu-id="3eddd-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="3eddd-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="3eddd-187">"type": "platformy" zależności reprezentowane jako "type": "pakietu" w pliku blokady - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="3eddd-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="3eddd-188">Tryb informacji pełnej nuget.exe powinny być widoczne pobierania adresu url - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="3eddd-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="3eddd-189">Przenieś NuGet xplat Microsoft.NetCore.App i netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="3eddd-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="3eddd-190">Push - powinno być możliwe do przesłonięcia serwera symboli w przypadku wypychania w wierszu polecenia - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="3eddd-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="3eddd-191">Konsolidacja kodu do znajdowania globalnej pakietów ścieżka - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="3eddd-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="3eddd-192">Należy nazwę lepszą niż suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="3eddd-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="3eddd-193">Określić `project.json` Nazwa zależności dla projektów MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="3eddd-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="3eddd-194">Dodaj obsługę programu SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="3eddd-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="3eddd-195">Zezwalaj na przechodnie zależności NuPkgs z `.targets` mają być dostępne w programie MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="3eddd-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="3eddd-196">Przywracanie NuGet w wierszu polecenia jest znacznie mniejsza niż VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="3eddd-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="3eddd-197">Wprowadź bez uwzględniania wielkości liter - porównania identyfikator i wersję pakietu [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="3eddd-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="3eddd-198">Opcja NoCache nie działa w przypadku `packages.config` (wartość GlobalPackagesFolder) - restore/Instalacja oparta na [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="3eddd-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="3eddd-199">Zasoby FindPackageByIdResource wymaga domyślny kontekst pamięci podręcznej i rejestratora — [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="3eddd-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
