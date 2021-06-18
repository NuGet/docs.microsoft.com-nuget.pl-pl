---
title: Informacje o wersji nuGet 5.10
description: Informacje o wersji dla programu NuGet 5.10, w tym nowe funkcje, poprawki błędów i dcrs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356540"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="bcaeb-103">Informacje o wersji nuGet 5.10</span><span class="sxs-lookup"><span data-stu-id="bcaeb-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="bcaeb-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="bcaeb-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="bcaeb-105">Wersja nuGet</span><span class="sxs-lookup"><span data-stu-id="bcaeb-105">NuGet version</span></span> | <span data-ttu-id="bcaeb-106">Dostępne w Visual Studio wersji</span><span class="sxs-lookup"><span data-stu-id="bcaeb-106">Available in Visual Studio version</span></span> | <span data-ttu-id="bcaeb-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="bcaeb-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="bcaeb-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="bcaeb-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="bcaeb-109">Visual Studio 2019 w wersji 16.10</span><span class="sxs-lookup"><span data-stu-id="bcaeb-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="bcaeb-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="bcaeb-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="bcaeb-111"><sup>1 Zainstalowane</sup> z programem Visual Studio 2019 z obciążeniem .NET Core</span><span class="sxs-lookup"><span data-stu-id="bcaeb-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="bcaeb-112">Visual Studio 16.10, MSBuild 16.10 i .NET 5.0.300+ wymagają programu NuGet.exe 5.10 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="bcaeb-113">Podsumowanie: Co nowego w programie 5.10</span><span class="sxs-lookup"><span data-stu-id="bcaeb-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="bcaeb-114">Podpisywanie: implementowanie polecenia dotnet trusted-signers — [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="bcaeb-115">Wyłącz domyślną weryfikację w systemie Linux, ale włącz ją domyślnie w systemie Windows — [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="bcaeb-116">Dodawanie zmiennej ENV do weryfikacji podpisywania pakietów na platformie .NET 5+ Linux/MAC [— #10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="bcaeb-117">Poprawianie wydajności instalacji nowych pakietów dla dużych rozwiązań [— #10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="bcaeb-118">Dodaj typ projektu `nfproj` do listy supportedProjectExtensions dla interfejsu wiersza polecenia nuget.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="bcaeb-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="bcaeb-120">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="bcaeb-120">Issues fixed in this release</span></span>

* <span data-ttu-id="bcaeb-121">Pomijanie <requireLicenseAcceptance> elementu podczas pakowania projektu — [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="bcaeb-122">Ostrzeżenie o wersji zapoznawczej [CPVM] powinno być wyświetlane w interfejsie wiersza polecenia dotnet [— #10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="bcaeb-123">Zaktualizuj tokeny koloru tła i pierwszego planu dla uwierzytelniania PMUI na CommonDocumentColors — [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="bcaeb-124">[Bug Bash] Błąd "Operacja anulowana przez użytkownika" jest pokazywana w oknie Lista błędów podczas szybkiego przełączania między kartami w interfejsie użytkownika PM — [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="bcaeb-125">Interfejs użytkownika PM: Poprawianie wydajności instalacji pakietu na poziomie rozwiązania — [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="bcaeb-126">Zastąp getservice z GetServiceAsync wszędzie w NuGet.Clients — [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="bcaeb-127">NuGet.exe wydajności pakietu z `..` ścieżką względną [— #5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="bcaeb-128">Wydajność "pakietu nuget" spada wraz ze wzrostem poziomów w ścieżkach źródłowych — [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="bcaeb-129">NuGet doesn't error when packaging nuspec with duplicate files (NuGet nie zwraca błędu podczas pakowania nuspec ze zduplikowanymi plikami).</span><span class="sxs-lookup"><span data-stu-id="bcaeb-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="bcaeb-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="bcaeb-131">Pakiet NuGet "Określonego zestawu DateTimeOffset nie można przekonwertować na znacznik czasu pliku zip" — [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="bcaeb-132">Znaczniki czasu pliku spakowanego pakietu są przesunięte o strefę czasową [— #7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="bcaeb-133">Nu1004 powinien zawierać więcej informacji z akcjami [— #7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="bcaeb-134">[Bug Bash] [Test Failure] Pusty/źle sformułowany plik blokady nie powinien być aktualizowany w przypadku uruchamiania pliku "dotnet restore --use-lock-file --locked-mode" — [#8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="bcaeb-135">NuGetVersionRange umożliwia analizowanie logicznie nieprawidłowych zakresów — [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="bcaeb-136">Interfejs użytkownika PM nie może wyświetlać wyróżniających się kolorów tła między wybranymi i najechanym kursorem źródeł pakietów [—](https://github.com/NuGet/Home/issues/9538) #9538</span><span class="sxs-lookup"><span data-stu-id="bcaeb-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="bcaeb-137">Pole wyboru wyboru wyboru wyboru projektów do zainstalowania nie jest odczytywane przez czytnik zawartości ekranu — [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="bcaeb-138">Domyślną domyślną wartością listy rozwijanej Wersje okienka szczegółów powinna być Zainstalowana/NajnowszaStable na kartach Zainstalowane/Aktualizacje — [#9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="bcaeb-139">Usuń konto obejścia dla niektórych zestawów SDK .NET 5, które zgłaszają element TargetPlatformMoniker ` ,Version= ` #9913  -  [](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="bcaeb-140">dotnet nuget verify is too quiet - #10316 (Sprawdzanie dotnet nuget jest [zbyt #10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="bcaeb-141">VersionRange nie może analizowania zakresów jednocyfrowych [— #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="bcaeb-142">Menedżer rozwiązań programu VS zgłasza wyjątek o wartości null podczas debugowania [— #10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="bcaeb-143">Przenoszenie komunikatów o wyjątkach interfejsu wiersza polecenia do plików zasobów ciągu [— #10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="bcaeb-144">Usuwanie niechybnego kodu (TabItemButtonAutomationPeer) — [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="bcaeb-145">Menu kontekstowe aktualizacji powinno zostać przewinąć do pierwszego wybranego [elementu — #10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="bcaeb-146">Szczegóły PMUI rozwiązania mają nakładający się pasek poziomy [— #10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="bcaeb-147">Podpisywanie: szczegóły podpisu podstawowego nie są wyświetlane, gdy certyfikat wygasł i sygnatura czasowa jest niezaufana — [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="bcaeb-148">Brak włączonych źródeł uniemożliwia wyświetlanie interfejsu użytkownika PM — [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="bcaeb-149">Metadane pakietu (szczegóły, wycofana) czasami nie są ściągane z nuget.org CodeSpaces [—](https://github.com/NuGet/Home/issues/10549) #10549</span><span class="sxs-lookup"><span data-stu-id="bcaeb-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="bcaeb-150">Inicjowanie PMUI kończy się niepowodzeniem z wyjątkiem podczas sesji debugowania [— #10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="bcaeb-151">Przywracanie nuget powoduje niepowodzenie sprawdzania integralności pakietu w big endian systemu — [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="bcaeb-152">Zamiast wyjątek PackagingException jest zgłaszany wyjątek FormatException [— #10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="bcaeb-153">CPVM — problemy ze współbieżnością w algorytmie chybienia grafu — [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="bcaeb-154">Dodawanie telemetrii wersji programu PowerShell dla pmc [— #10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="bcaeb-155">Poprawianie wydajności sortowania w wersji NuGetVersion [— #10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="bcaeb-156">Dodanie zaufanych podpisujących ma niespójne argumenty [— #10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="bcaeb-157">Vs2019 w wersji 16.9.0: przełączanie kart w programie NuGet Menedżer pakietów z "Aktualizacje" na "Zainstalowane" nie aktualizuje ramki.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="bcaeb-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="bcaeb-159">Usuń "v" z numeru wersji w pmui — [#10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="bcaeb-160">INuGetProjectService.GetInstalledPackagesAsync zgłasza wyjątek przed otrzymaniem nominacji systemu projektu CPS — [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="bcaeb-161">Osadzone ikony powodują odmowę dostępu ze źródła "pakiety Microsoft Visual Studio offline" na karcie Przeglądaj [—](https://github.com/NuGet/Home/issues/10687) #10687</span><span class="sxs-lookup"><span data-stu-id="bcaeb-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="bcaeb-162">INuGetProjectService.GetInstalledPackagesAsync zgłasza wyjątek, gdy ścieżka MSBuildProjectExtensionsPath nie jest ustawiona [— #10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="bcaeb-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="bcaeb-164">Nuget blokuje wątek threadpool w metodzie asynchronicznej, wywołując synchroniczne wywołanie wątku interfejsu użytkownika — [#10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="bcaeb-165">Narzędzia -> Opcje -> NuGet Menedżer pakietów ciąg jest obcięty — [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="bcaeb-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` jest niechybny kod i wydajność jest [zaniona — #10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="bcaeb-167">Używanie osadzonej ikony w pakietach zestawu NuGet SDK [— #10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="bcaeb-168">Aktualizowanie listy licencji SPDX [— #10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="bcaeb-169">**[Lista wszystkich problemów rozwiązanych w tej wersji — 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="bcaeb-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="bcaeb-170">**[Lista zatwierdzeń w tej wersji — 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="bcaeb-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="bcaeb-171">Materiały przekazywane przez społeczność</span><span class="sxs-lookup"><span data-stu-id="bcaeb-171">Community contributions</span></span>

<span data-ttu-id="bcaeb-172">Dziękujemy wszystkim współautorom, którzy pomogli w wytwórzeniu tej wersji NuGet!</span><span class="sxs-lookup"><span data-stu-id="bcaeb-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="bcaeb-173">Który</span><span class="sxs-lookup"><span data-stu-id="bcaeb-173">Who</span></span>|<span data-ttu-id="bcaeb-174">Prs</span><span class="sxs-lookup"><span data-stu-id="bcaeb-174">PRs</span></span>|<span data-ttu-id="bcaeb-175">Problemy</span><span class="sxs-lookup"><span data-stu-id="bcaeb-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="bcaeb-176">luizja z</span><span class="sxs-lookup"><span data-stu-id="bcaeb-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="bcaeb-177">3991</span><span class="sxs-lookup"><span data-stu-id="bcaeb-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="bcaeb-178">VersionRange nie może analizowania zakresów jednocyfrowych [— #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="bcaeb-179">omajid</span><span class="sxs-lookup"><span data-stu-id="bcaeb-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="bcaeb-180">3860</span><span class="sxs-lookup"><span data-stu-id="bcaeb-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="bcaeb-181">Niedziała build.sh NuGet.Client — [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="bcaeb-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="bcaeb-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="bcaeb-183">3623</span><span class="sxs-lookup"><span data-stu-id="bcaeb-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="bcaeb-184">Niedziała build.sh NuGet.Client — [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="bcaeb-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="bcaeb-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="bcaeb-186">3953</span><span class="sxs-lookup"><span data-stu-id="bcaeb-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="bcaeb-187">Wydajność "pakietu nuget" spada wraz ze wzrostem poziomów w ścieżkach źródłowych — [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="bcaeb-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="bcaeb-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="bcaeb-189">3953</span><span class="sxs-lookup"><span data-stu-id="bcaeb-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="bcaeb-190">NuGet.exe z wydajnością pakietu.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="bcaeb-191">ścieżka względna [— #5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="bcaeb-192">dojdą do 2017 r.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="bcaeb-193">3940</span><span class="sxs-lookup"><span data-stu-id="bcaeb-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="bcaeb-194">CPVM — problemy ze współbieżnością w algorytmie chybienia grafu — [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="bcaeb-195">josesimoes</span><span class="sxs-lookup"><span data-stu-id="bcaeb-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="bcaeb-196">3943</span><span class="sxs-lookup"><span data-stu-id="bcaeb-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="bcaeb-197">Dodaj typ projektu nfproj do listy supportedProjectExtensions dla interfejsu wiersza polecenia nuget.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="bcaeb-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="bcaeb-199">Opinie powitane</span><span class="sxs-lookup"><span data-stu-id="bcaeb-199">Feedback welcome</span></span>

<span data-ttu-id="bcaeb-200">Twoja opinia jest dla nas ważna.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-200">Your feedback is important to us.</span></span>  <span data-ttu-id="bcaeb-201">Jeśli w tej wersji występują jakiekolwiek problemy, zapoznaj się z naszymi problemami usługi [GitHub](https://github.com/NuGet/Home/issues) [i Visual Studio Developer Community](https://developercommunity.visualstudio.com/) istniejących problemów.</span><span class="sxs-lookup"><span data-stu-id="bcaeb-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="bcaeb-202">W przypadku nowych problemów w ramach narzędzia NuGet zgłoś problem [w usłudze GitHub.](https://github.com/NuGet/Home/issues/new)</span><span class="sxs-lookup"><span data-stu-id="bcaeb-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="bcaeb-203">W przypadku ogólnych problemów ze środowiskami NuGet daj nam znać za pośrednictwem opcji Zgłoś [problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) w ulubionym idee w obszarze Pomoc **> Zgłoś problem.**</span><span class="sxs-lookup"><span data-stu-id="bcaeb-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
