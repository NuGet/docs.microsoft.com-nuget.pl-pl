---
title: Informacje o wersji narzędzia NuGet 4,0 RC
description: Informacje o wersji programu NuGet 4,0 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780192"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="e7854-103">Informacje o wersji narzędzia NuGet 4,0 RC</span><span class="sxs-lookup"><span data-stu-id="e7854-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="e7854-104">Informacje o wersji narzędzia NuGet 3,5 RTM</span><span class="sxs-lookup"><span data-stu-id="e7854-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="e7854-105">Pakiet [NuGet 4,0 RC dla programu Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) koncentruje się na dodawaniu obsługi scenariuszy platformy .NET Core, rozwiązywaniu kluczowych opinii klientów i ulepszaniu wydajności w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="e7854-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="e7854-106">W tej wersji wprowadzono kilka ulepszeń, takich jak obsługa PackageReference, poleceń NuGet jako obiektów docelowych programu MSBuild, przywracania pakietów w tle i innych.</span><span class="sxs-lookup"><span data-stu-id="e7854-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e7854-107">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="e7854-107">Bug Fixes</span></span>

- <span data-ttu-id="e7854-108">Zmiany zachowania w `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="e7854-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="e7854-109">nuget.exe przywracania na komputerze vs "15" kończy się niepowodzeniem — [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="e7854-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="e7854-110">. Nowy projekt pliku podstawowego powinien blokować kompilację podczas przywracania [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="e7854-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="e7854-111">Nie można przywrócić ASP.NET Core aplikacji sieci Web migrowanej z programu VS2015 do programu VS "15".</span><span class="sxs-lookup"><span data-stu-id="e7854-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="e7854-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="e7854-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="e7854-113">[Niepowodzenie testu] Nie można odinstalować pakietu "jQuery Validation" przy użyciu interfejsu użytkownika PM — [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="e7854-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="e7854-114">Gdy pakiet jest zainstalowany w platformy UWP `project.json` , należy również przywrócić projekty nadrzędne — [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="e7854-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="e7854-115">Zmodyfikuj cele NuGet, aby rejestrować źródła pakietów jako wysoki poziom szczegółowości zamiast normalnej [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="e7854-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="e7854-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="e7854-116">dotnet</span></span>
  - <span data-ttu-id="e7854-117">dotnetcore Pack3 powinien domyślnie zawierać dokumentację XML — [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="e7854-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="e7854-118">Aktualizacja usługi Batch kończy się niepowodzeniem z poziomu interfejsu użytkownika, gdy źródło bez pakietu jest wybrane — [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="e7854-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="e7854-119">Polecenie pakietu NuGet nie obejmuje wszystkich plików — [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="e7854-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="e7854-120">Problem z OOM — [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="e7854-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="e7854-121">Sekcja ProjectFileDependencyGroups pliku Assets powinna używać nazw bibliotek dla projektów — [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="e7854-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="e7854-122">"dotnet restore" i powtarzanie katalogów — [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="e7854-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="e7854-123">Błędy Restore3 są rejestrowane jako ostrzeżenia zamiast błędów — [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="e7854-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="e7854-124">Problem z TFS: "[plik] nie został znaleziony w Twoim obszarze roboczym lub nie masz uprawnień dostępu do niego"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="e7854-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="e7854-125">Wpisanie słowa "NuGet <packagename> " w polu wyszukiwania programu vs — umożliwia zachowanie prefiksu "NuGet" — [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="e7854-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="e7854-126">Wyjątek System.Xml.Xml: nierozpoznany element główny w części Core Properties.</span><span class="sxs-lookup"><span data-stu-id="e7854-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="e7854-127">Wiersz 2, pozycja 2.</span><span class="sxs-lookup"><span data-stu-id="e7854-127">Line 2, position 2.</span></span><span data-ttu-id="e7854-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="e7854-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="e7854-129">`.nuspec` w przypadku &lt; , gdy &gt; w polach tekstowych nie są już kompilacje — [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="e7854-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="e7854-130">nuget.exe usuwania nie będzie monitować o poświadczenia (jest w trybie nieinteraktywnym) — [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="e7854-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="e7854-131">nuget.exe Delete ostrzega o kluczu interfejsu API dla źródeł lokalnych, nawet jeśli nie ma sensu [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="e7854-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="e7854-132">Wystąpił błąd podczas instalowania pakietu EF-pre- [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="e7854-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="e7854-133">Program Visual Studio uległ awarii po zmianie zaznaczenia w Menedżerze pakietów — [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="e7854-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="e7854-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="e7854-134">dotnet</span></span>
  - <span data-ttu-id="e7854-135">Funkcja przywracania dotnetcore wykonuje wyszukiwania identyfikatorów z uwzględnieniem wielkości liter w lokalnych repozytoriach na płaskich listach, gdy są używane wersje zmiennoprzecinkowe — [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="e7854-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="e7854-136">nuget.exe usunięcie jest zerwane dla źródła danych w wersji 2 [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="e7854-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="e7854-137">nuget.exe przekroczenie limitu czasu wypychania wymaga lepszego komunikatu o błędzie — [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="e7854-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="e7854-138">Przywracanie narzędzia bez odpowiednich importów w trybie dyskretnym nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="e7854-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="e7854-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="e7854-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="e7854-140">Pakiet NuGet monituje o wprowadzenie poświadczeń, gdy istnieje prywatne źródło danych nawet podczas instalacji z nuget.org- [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="e7854-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="e7854-141">Pakiet ApplicationInsights 2,0 jest wymieniony, ale jeszcze nie istnieje — [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="e7854-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="e7854-142">UIDelay w programie VS "15" (wersja zapoznawcza 5) — [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="e7854-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="e7854-143">Nie pominięto pierwszego zdarzenia onbuild dla przywracania podczas kompilacji dla platformy UWP- [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="e7854-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="e7854-144">PowerShell5 przerwań instalacji EntityFramework?</span><span class="sxs-lookup"><span data-stu-id="e7854-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="e7854-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="e7854-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="e7854-146">Dodaj źródło do szczegółowego rejestrowania (Rozważ 3,5) — [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="e7854-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="e7854-147">Parametr nocache nie został uznany w kliencie NuGet w wersji 3.4 +- [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="e7854-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="e7854-148">W przypadku niepowodzenia ładowania dostawcy poświadczeń w programie VS nie należy dzielić narzędzia NuGet- [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="e7854-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="e7854-149">Funkcje</span><span class="sxs-lookup"><span data-stu-id="e7854-149">Features</span></span>

- <span data-ttu-id="e7854-150">Skonfiguruj CI do uruchamiania architektury x86 [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="e7854-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="e7854-151">Autoprzywracanie 3/3: nie blokuje interfejsu użytkownika [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="e7854-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="e7854-152">Autoprzywracanie 2/3: przywracanie w tle w wyznaczonym [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="e7854-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="e7854-153">Przywróć odwołania projektu w celu dopasowania do zachowania kompilacji (rekursywnie) — [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="e7854-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="e7854-154">Obsługa DPL w programie VS "15"-minbar- [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="e7854-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="e7854-155">Przenoszenie pliku ustawień do plików programu — [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="e7854-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="e7854-156">Wygenerowane właściwości przywracania i elementy docelowe wymagają obsługi partycypacji obejmującej wiele elementów docelowych — [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="e7854-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="e7854-157">Obsługa przywracania NuGet dla PackageTargetFallback (f. k. a Imports) — [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="e7854-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="e7854-158">Implementacja ToolsRef — [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="e7854-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="e7854-159">Restore3 identyfikatorów RID [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="e7854-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="e7854-160">Interfejs użytkownika narzędzia NuGet do obsługi dodawania/usuwania/aktualizowania PackageRefs- [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="e7854-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="e7854-161">Automatyczne przywracanie 1/3: implementacji interfejsu API wyznaczania przez buforowanie informacji o przywracaniu projektu — [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="e7854-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="e7854-162">[0] zadanie przywracania NuGet & cele — [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="e7854-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="e7854-163">[1] Włącz przywracanie na poziomie rozwiązania w programie MSBuild — [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="e7854-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="e7854-164">Obsługa publicznej rozszerzalności dostawcy poświadczeń w programie Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="e7854-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="e7854-165">Rekursywne przywracanie NuGet — [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="e7854-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="e7854-166">Nie można załadować Microsoft. TeamFoundation. Client on dev15, należy zaktualizować wersję Microsoft. TeamFoundation. Client do 15,0 dla programu VS "15" (wersja zapoznawcza) [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="e7854-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="e7854-167">Nie można zainstalować pakietu C++ do projektu C++ platformy UWP w programie VS "15" (wersja zapoznawcza) — [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="e7854-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="e7854-168">NUPKG musi obsługiwać folder \buildCrossTargeting\ i importować `.targets`  /  `.props` dla zakresu programu MSBuild "crosstargeting".</span><span class="sxs-lookup"><span data-stu-id="e7854-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="e7854-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="e7854-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="e7854-170">Projekt ToolsReference — [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="e7854-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="e7854-171">Napraw interfejs użytkownika NuGet, aby obsługiwał przywracanie z/składnika packagereferences w `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="e7854-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="e7854-172">Dodawanie przycisku Wyczyść pamięć podręczną do ustawień Menedżera pakietów programu VS — [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="e7854-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="e7854-173">DCR</span><span class="sxs-lookup"><span data-stu-id="e7854-173">DCRs</span></span>

- <span data-ttu-id="e7854-174">Przywracanie rozwiązania powinno być blokowane, gdy jest wykonywane Autoprzywracanie.</span><span class="sxs-lookup"><span data-stu-id="e7854-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="e7854-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="e7854-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="e7854-176">Instalacja programu servicecore z poziomu interfejsu użytkownika Menedżera pakietów NuGet jest instalowana do każdego TFMu, a nie do tych, które są obsługiwane przez pakiet — [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="e7854-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="e7854-177">Interfejs API przywracania nominowania musi również obsługiwać DotNetCliToolsReferences.</span><span class="sxs-lookup"><span data-stu-id="e7854-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="e7854-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="e7854-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="e7854-179">Oznacz nasz plik VSIX programu VS "15" jako SystemComponent [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="e7854-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="e7854-180">Migruj z odwołującego się do MS. Lokalne. Services. Client do MS. Lokalne. Services. Client. Interactive — [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="e7854-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="e7854-181">Wartość $ (RestoreLegacyPackagesDirectory) powinna być przestrzegana na poziomie projektu przez przywrócenie [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="e7854-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="e7854-182">Przywracanie do projektu z pojedynczym TargetFrameworkem nie może mieć warunku- [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="e7854-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="e7854-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="e7854-183">dotnet</span></span>
  - <span data-ttu-id="e7854-184">dotnetcore restore3 foo. csproj powinna być zgodna z zależnościami projectref i przywrócić te.</span><span class="sxs-lookup"><span data-stu-id="e7854-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="e7854-185">Podobnie jak kompilacja.</span><span class="sxs-lookup"><span data-stu-id="e7854-185">Like build.</span></span><span data-ttu-id="e7854-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="e7854-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="e7854-187">"Type": zależności "platform" reprezentowane jako "Type": "Package" w pliku blokady — [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="e7854-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="e7854-188">W trybie pełny nuget.exe powinien zostać wyświetlony adres URL pobierania — [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="e7854-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="e7854-189">Przenoszenie NuGet Xplat do Microsoft. WebCore. app i netcoreapp 1.0- [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="e7854-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="e7854-190">Wypychanie — powinno być możliwe przesłonięcie serwera symboli podczas wypychania z wiersza polecenia — [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="e7854-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="e7854-191">Konsolidowanie kodu do znajdowania ścieżki pakietów globalnych — [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="e7854-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="e7854-192">Potrzebna lepsza nazwa niż suppressParent — [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="e7854-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="e7854-193">Określanie `project.json` nazwy zależności, która ma być używana dla projektów MSBuild — [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="e7854-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="e7854-194">Dodawanie obsługi SemVer 2.0.0 do narzędzia NuGet. Core — [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="e7854-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="e7854-195">Zezwalaj na użycie przechodniej NuPkgs zależności `.targets` w programie MSBuild — [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="e7854-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="e7854-196">Przywracanie NuGet z wiersza polecenia jest znacznie wolniejsze niż VS- [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="e7854-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="e7854-197">Ustaw identyfikator pakietu i wersję z uwzględnieniem wielkości liter — [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="e7854-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="e7854-198">Opcja NoCache nie działa na `packages.config` podstawie przywracania/instalacji (GlobalPackagesFolder) — [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="e7854-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="e7854-199">Zasoby FindPackageByIdResource potrzebują domyślnego kontekstu pamięci podręcznej i rejestratora [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="e7854-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
