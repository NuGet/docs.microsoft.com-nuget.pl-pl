---
title: Informacje o wersji programu NuGet 4.0 RC
description: Informacje o wersji NuGet 4.0 RC obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549249"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="13ada-103">Informacje o wersji programu NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="13ada-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="13ada-104">Informacje o wersji programu NuGet 3.5 RTM</span><span class="sxs-lookup"><span data-stu-id="13ada-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="13ada-105">[Program NuGet 4.0 RC programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na dodano obsługę scenariuszy .NET Core, odnoszący się opinie klientów i zwiększanie wydajności w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="13ada-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="13ada-106">Ta wersja oferuje kilka udoskonaleń, takich jak obsługa PackageReference, NuGet polecenia jako elementy docelowe programu MSBuild, przywracania pakietów w tle i nie tylko.</span><span class="sxs-lookup"><span data-stu-id="13ada-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="13ada-107">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="13ada-107">Bug Fixes</span></span>

- <span data-ttu-id="13ada-108">Zmiany zachowania w `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="13ada-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="13ada-109">Przywracanie nuget.exe dla programu vs "15" tylko komputera nie powiodło się — [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="13ada-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="13ada-110">. Nowy projekt pliku NETCore powinna blokować kompilacji podczas przywracania - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="13ada-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="13ada-111">Aplikacja sieci web platformy ASP.NET Core, poddane migracji z programu VS2015 VS "15", nie można przywrócić.</span><span class="sxs-lookup"><span data-stu-id="13ada-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="13ada-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="13ada-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="13ada-113">[Niepowodzenie testu] Nie można odinstalować pakietu "jQuery weryfikacji" przez interfejs użytkownika PM - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="13ada-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="13ada-114">Po zainstalowaniu pakietu do platformy uniwersalnej systemu Windows `project.json`, projekty nadrzędnego powinny również zostanie przywrócony - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="13ada-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="13ada-115">Modyfikowanie cele NuGet logowania źródła pakietów jako wysoki poziom szczegółowości zamiast normalny - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="13ada-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="13ada-116">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="13ada-116">dotnet</span></span>
  - <span data-ttu-id="13ada-117">dotnetcore dodatkiem Service Pack 3 powinna zawierać dokumentację XML domyślnie - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="13ada-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="13ada-118">Batch aktualizacja nie powiodła się z poziomu interfejsu użytkownika po wybraniu wszystkich źródła - i źródła bez pakietu jest pierwszy [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="13ada-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="13ada-119">Polecenie pakietu Nuget nie zawiera wszystkie pliki - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="13ada-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="13ada-120">Za mało pamięci problemu — [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="13ada-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="13ada-121">Sekcja ProjectFileDependencyGroups pliku zasobów, należy użyć nazwy bibliotek dla projekty — [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="13ada-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="13ada-122">"dotnet restore" i recursing katalogów - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="13ada-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="13ada-123">Restore3 błędy są rejestrowane jako ostrzeżenia zamiast błędów — [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="13ada-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="13ada-124">Problem z TFS: "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="13ada-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="13ada-125">Wpisywanie "nuget <packagename>" w programie vs pole wyszukiwania szybkiego uruchamiania utrzymuje prefiksu "nuget" - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="13ada-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="13ada-126">System.Xml.XmlException: Element główny nierozpoznaną część podstawowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="13ada-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="13ada-127">Wiersz 2, pozycji 2.</span><span class="sxs-lookup"><span data-stu-id="13ada-127">Line 2, position 2.</span></span><span data-ttu-id="13ada-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="13ada-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="13ada-129">`.nuspec` za pomocą ucieczki &lt; lub &gt; pól w tekście nie umożliwia już skompilowania - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="13ada-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="13ada-130">Usuń nuget.exe nie Monituj o poświadczenia, (jest w trybie nieinterakcyjnym) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="13ada-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="13ada-131">Usuń nuget.exe ostrzega o klucz interfejsu API dla źródeł lokalnych, nawet jeśli nie ma sensu — [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="13ada-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="13ada-132">Niska środowisko błąd podczas instalowania programu EF - pre package — [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="13ada-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="13ada-133">Program Visual Studio uległ awarii, próby po zmianie wyboru w Menedżerze pakietów - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="13ada-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="13ada-134">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="13ada-134">dotnet</span></span>
  - <span data-ttu-id="13ada-135">Przywracanie dotnetcore wykonuje z uwzględnieniem wielkości liter wyszukiwania identyfikatora kwerendy płaskiej listy repozytoriów lokalnych podczas korzystania z wersji zmiennoprzecinkowy — [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="13ada-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="13ada-136">Usuń nuget.exe nie działa dla źródła danych w wersji 2 - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="13ada-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="13ada-137">limit czasu wypychania nuget.exe musi udoskonalony komunikat o błędzie - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="13ada-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="13ada-138">Narzędzie przywracania bez odpowiedniego dyskretnie importuje kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="13ada-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="13ada-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="13ada-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="13ada-140">NuGet wyświetla monit o podanie poświadczeń, gdy istnieje prywatne źródło danych nawet wtedy, gdy instalowanie z repozytorium nuget.org — [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="13ada-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="13ada-141">Pakiet dotycząca usługi Application Insights w wersji 2.0, znajduje się na liście, ale nie istnieje jeszcze - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="13ada-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="13ada-142">UIDelay w programie VS "15" w wersji zapoznawczej 5 gałąź — [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="13ada-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="13ada-143">Pierwsze zdarzenie OnBuild brakuje przywracane podczas kompilacji dla platformy uniwersalnej systemu Windows — [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="13ada-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="13ada-144">Podziały PowerShell5 EntityFramework instalacji?</span><span class="sxs-lookup"><span data-stu-id="13ada-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="13ada-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="13ada-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="13ada-146">Dodawanie źródła danych do szczegółowe rejestrowanie (należy wziąć pod uwagę 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="13ada-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="13ada-147">Parametr Właściwość NoCache nie honorowane w wersji klienta nuget 3.4. + - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="13ada-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="13ada-148">Gdy dostawca poświadczeń nie można załadować w programie VS, nie DZIEL NuGet — [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="13ada-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="13ada-149">Funkcje</span><span class="sxs-lookup"><span data-stu-id="13ada-149">Features</span></span>

- <span data-ttu-id="13ada-150">Konfigurowanie ciągłej integracji na potrzeby uruchamiania x86- [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="13ada-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="13ada-151">Automatycznego przywracania 3/3: bez blokujące elementy interfejsu użytkownika — [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="13ada-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="13ada-152">Automatycznego przywracania 2/3: przywracanie dla nominacji — w tle [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="13ada-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="13ada-153">Przywracanie projektu systemu plików refs, aby dopasować zachowanie kompilacji (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="13ada-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="13ada-154">DPL obsługi w programie VS "15" — minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="13ada-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="13ada-155">Przenieś plik ustawień Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="13ada-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="13ada-156">Cele i właściwości wygenerowanej przywracania potrzebujesz przeznaczonych dla wielu współdziałania ze strony pomocy technicznej — [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="13ada-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="13ada-157">Przywracanie NuGet obsługę PackageTargetFallback (f.k.a Importy) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="13ada-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="13ada-158">Implementacja ToolsRef — [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="13ada-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="13ada-159">Restore3 dla identyfikatora RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="13ada-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="13ada-160">NuGet interfejsu użytkownika w celu obsługi Dodaj/Usuń/zaktualizuj PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="13ada-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="13ada-161">Automatycznego przywracania 1/3: Implementacji nominacji interfejsu API za pośrednictwem buforowanie projektu przywracanie informacji - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="13ada-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="13ada-162">[0] NuGet Restore, zadania i elementy docelowe — [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="13ada-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="13ada-163">[1] Włącz Przywracanie na poziomie rozwiązania w programie MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="13ada-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="13ada-164">Obsługuje rozszerzalność publicznego dostawcy poświadczeń w programie Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="13ada-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="13ada-165">Przywracanie pakietów nuget cykliczne - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="13ada-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="13ada-166">Nie można załadować Microsoft.TeamFoundation.Client dev15, trzeba zaktualizować Microsoft.TeamFoundation.Client w wersji 15.0 dla programu VS "15" (wersja zapoznawcza) — [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="13ada-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="13ada-167">Nie można zainstalować pakiet języka C++ platformy uniwersalnej systemu Windows w języku C++ projektu w programie VS "15" (wersja zapoznawcza) — [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="13ada-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="13ada-168">Nupkg musi obsługiwać folder \buildCrossTargeting\ — i zaimportować `.targets`  /  `.props` dla "crosstargeting" zakresu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="13ada-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="13ada-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="13ada-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="13ada-170">Projekt ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="13ada-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="13ada-171">Napraw NuGet interfejsu użytkownika, która obsługuje Przywracanie z PackageReferences w `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="13ada-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="13ada-172">Dodawanie przycisk Wyczyść pamięć podręczną, aby ustawienia Menedżera pakietów programu VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="13ada-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="13ada-173">DCRs</span><span class="sxs-lookup"><span data-stu-id="13ada-173">DCRs</span></span>

- <span data-ttu-id="13ada-174">Rozwiązanie Przywróć powinien być blokowany podczas automatycznego przywracania.</span><span class="sxs-lookup"><span data-stu-id="13ada-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="13ada-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="13ada-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="13ada-176">NetCore instalacji z poziomu interfejsu użytkownika Menedżera pakietów NuGet instaluje co TFM, a nie te, które obsługuje pakiet - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="13ada-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="13ada-177">Przywróć nominator interfejsu API musi obsługiwać DotNetCliToolsReferences zbyt.</span><span class="sxs-lookup"><span data-stu-id="13ada-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="13ada-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="13ada-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="13ada-179">Oznacz naszych VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="13ada-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="13ada-180">Przeprowadź migrację z odwołujące się do MS. VS. Services.Client MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="13ada-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="13ada-181">$(RestoreLegacyPackagesDirectory) powinny być przestrzegane na poziomie projektu przez Przywracanie — [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="13ada-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="13ada-182">Przywracanie projektu za pomocą pojedynczego TargetFramework nie musi warunku właściwości - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="13ada-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="13ada-183">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="13ada-183">dotnet</span></span>
  - <span data-ttu-id="13ada-184">dotnetcore restore3 foo.csproj powinny wykonaj projectref zależności, a także przywrócić te zbyt.</span><span class="sxs-lookup"><span data-stu-id="13ada-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="13ada-185">Podobnie jak kompilacji.</span><span class="sxs-lookup"><span data-stu-id="13ada-185">Like build.</span></span><span data-ttu-id="13ada-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="13ada-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="13ada-187">"type": "platforma" zależności reprezentowane jako "type": "pakiet" w pliku blokady - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="13ada-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="13ada-188">Tryb informacji pełnej nuget.exe powinien być wyświetlony pobierania adresa url – [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="13ada-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="13ada-189">Przenieś NuGet xplat pakietów Microsoft.NetCore.App i netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="13ada-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="13ada-190">Push — powinno być możliwe do przesłonięcia serwera symboli, podczas wypychania z wiersza polecenia — [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="13ada-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="13ada-191">Skonsolidować kodu do znajdowania globalnego pakietów ścieżka - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="13ada-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="13ada-192">Potrzebujesz nazwę lepsze niż suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="13ada-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="13ada-193">Określić `project.json` Nazwa zależności dla projektów programu MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="13ada-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="13ada-194">Dodano obsługę SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="13ada-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="13ada-195">Zezwalaj na przechodnie zależności NuPkgs z `.targets` mają być dostępne w programie MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="13ada-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="13ada-196">Przywracanie pakietów NuGet z wiersza polecenia jest znacznie wolniejsze niż VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="13ada-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="13ada-197">Wprowadź bez uwzględniania wielkości liter — porównanie identyfikator i wersja pakietu [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="13ada-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="13ada-198">Właściwość NoCache opcji nie działa w przypadku `packages.config` przywracania/instalacja (GlobalPackagesFolder) — oparta na [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="13ada-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="13ada-199">Wymagane przez zasoby FindPackageByIdResource domyślny kontekst pamięci podręcznej i rejestratora - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="13ada-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
