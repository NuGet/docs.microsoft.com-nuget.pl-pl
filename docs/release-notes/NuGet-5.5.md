---
title: Informacje o wersji narzędzia NuGet 5,5
description: Informacje o wersji programu NuGet 5,5, w tym nowe funkcje, poprawki błędów i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780111"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="bb61a-103">Informacje o wersji narzędzia NuGet 5,5</span><span class="sxs-lookup"><span data-stu-id="bb61a-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="bb61a-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="bb61a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="bb61a-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="bb61a-105">NuGet version</span></span> | <span data-ttu-id="bb61a-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb61a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="bb61a-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="bb61a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="bb61a-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="bb61a-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="bb61a-109">Visual Studio 2019 w wersji 16,5</span><span class="sxs-lookup"><span data-stu-id="bb61a-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="bb61a-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="bb61a-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="bb61a-111"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="bb61a-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="bb61a-112">Podsumowanie: co nowego w 5,5</span><span class="sxs-lookup"><span data-stu-id="bb61a-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="bb61a-113">Ulepszona obsługa ułatwień dostępu i czytnika ekranu dla interfejsu użytkownika Menedżera pakietów NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb61a-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="bb61a-114">Problemy z ułatwieniami dostępu w środowiskach odczytywania zawartości ekranu, brak altText i dostępnej nazwy dla zainstalowanego pola tekstowego itd.,- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="bb61a-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="bb61a-115">Problemy z ułatwieniami dostępu w programie odczytywanie zawartości ekranu na liście pakietów — [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="bb61a-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="bb61a-116">Problemy z ułatwieniami dostępu w programie czytnika ekranu związane z kartami "Przeglądaj", "Zainstaluj" i "Aktualizuj" — [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="bb61a-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="bb61a-117">Narrator nie ogłasza "puste", "No Dependencies", "NuGet. org", "MIT" etykiety łącza [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="bb61a-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="bb61a-118">Obsługa wbudowanych ikon samodzielnego umieszczania w interfejsie użytkownika Menedżera pakietów programu Visual Studio dla pakietów hostowanych w lokalnych źródłach danych — [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="bb61a-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="bb61a-119">Znacznie ulepszona wydajność przywracania No-op przy użyciu `RestoreUseStaticGraphEvaluation` przyspieszania obliczeń przez wywoływanie statycznych interfejsów API programu MSBuild — [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="bb61a-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="bb61a-120">Ulepszona dotnet.exe niezawodność przy użyciu wtyczek do uwierzytelniania dla wielu platform</span><span class="sxs-lookup"><span data-stu-id="bb61a-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="bb61a-121">dotnet restore niepowodzenie z TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="bb61a-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="bb61a-122">Wtyczka: "zadanie zostało anulowane" — problem z uwierzytelnianiem ADO z powodu tego elementu.</span><span class="sxs-lookup"><span data-stu-id="bb61a-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="bb61a-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="bb61a-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="bb61a-124">Dodaj `dotnet nuget <add|remove|update|disable|enable|list> source` polecenie [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="bb61a-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="bb61a-125">Obsługę do `--skip-duplicate`  użycia wypychania NuGet programu dotnet- [#8778](https://github.com/NuGet/Home/issues/8778)</span><span class="sxs-lookup"><span data-stu-id="bb61a-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="bb61a-126">Obsługa `packages.config` przy użyciu programu MSBuild/Restore — [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="bb61a-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="bb61a-127">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="bb61a-127">Issues fixed in this release</span></span>

<span data-ttu-id="bb61a-128">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="bb61a-128">**Bugs**</span></span>

* <span data-ttu-id="bb61a-129">Self-Updater współpracujące z interfejsami API v3 — [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="bb61a-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="bb61a-130">Nieprawidłowa wersja zależności pakietu, jeśli w wersji zależności pakietu ustawiono wartość "\*"- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="bb61a-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="bb61a-131">ErrorUnsafePackageEntry komunikat o błędzie nie wskazuje źródła problemu — [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="bb61a-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="bb61a-132">Plik blokady nie jest uznawany za scenariusze "\*" — [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="bb61a-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="bb61a-133">NuGet.exe nie jest rozpoznawana jako Najnowsza wersja pakietu przy użyciu funkcji \* w PackageReference (MSBuild/dotnet/program VS Restore) — [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="bb61a-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="bb61a-134">pakiet listy dotnet z projektem WPF o wiele elementów docelowych — [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="bb61a-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="bb61a-135">Ulepsz ConcurrencyUtilities (Zmniejsz użycie procesora) — [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="bb61a-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="bb61a-136">Specyfikacja DG dla scenariuszy niezaładowanych projektów nie powinna być zapisywana w wersji zapoznawczej — [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="bb61a-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="bb61a-137">Pakiety NuGet programu Visual Studio (RestoreManagerPackage) muszą zostać automatyczne załadowane w zdarzeniach kompilacji rozwiązania — [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="bb61a-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="bb61a-138">Zakleszczenie w VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="bb61a-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="bb61a-139">Przybornik VisualStudio nie jest wypełniany w pakiecie NuGet, jeśli projekt jest umieszczony w folderze rozwiązania — [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="bb61a-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="bb61a-140">VS: Przywracanie rozwiązania bezproblemowo nie powiodło się z powodu warunku wyścigu — [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="bb61a-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="bb61a-141">Stała "ładowanie.." na zainstalowanej karcie i "wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="bb61a-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="bb61a-142">.. "na karcie Aktualizacje — [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="bb61a-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="bb61a-143">Brak ikon osadzonych w interfejsie użytkownika programu VS PM po wygaśnięciu pamięci podręcznej — [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="bb61a-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="bb61a-144">Uruchamianie interfejsu użytkownika FireAndForget PM — [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="bb61a-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="bb61a-145">Instrukcja RESTORE: IncludeExcludeFiles. Equals (...) jest niepoprawna — [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="bb61a-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="bb61a-146">Restore: PackageSpec. Clone () tworzy nierówny klon- [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="bb61a-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="bb61a-147">Pokazana Lista błędów mimo błędu "Zawsze pokazuj Lista błędów, jeśli kompilacja zakończy się z błędami" nie jest zaznaczona — [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="bb61a-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="bb61a-148">Statyczne przywracanie wykresu nie powinno przekazywać pustej SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="bb61a-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="bb61a-149">Przywróć: zamknięcie obliczone dla każdego projektu 4 razy — [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="bb61a-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="bb61a-150">Instrukcja RESTORE: DependencyGraphSpec. Load (...) nie wymaga JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="bb61a-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="bb61a-151">Przywracanie: duże ciągi utworzone na stercie dużego obiektu (LOH) — [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="bb61a-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="bb61a-152">Niestandardowe nuget.exe w nowszych mono mogą zostać przerwane ze względu na program rozpoznawania SDK MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="bb61a-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="bb61a-153">Przywracanie kończy się niepowodzeniem, gdy nuget.dgspec.json jest używany przez inny proces "- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="bb61a-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="bb61a-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="bb61a-154">**DCRs**</span></span>

* <span data-ttu-id="bb61a-155">Logika w _GetRestoreProjectStyle powinna znajdować się w [#8804](https://github.com/NuGet/Home/issues/8804) zadania</span><span class="sxs-lookup"><span data-stu-id="bb61a-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="bb61a-156">Domyślnie Dodaj informacje o zaniechaniu na zainstalowanej karcie — [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="bb61a-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="bb61a-157">**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="bb61a-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
