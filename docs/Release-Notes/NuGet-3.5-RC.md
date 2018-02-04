---
title: 3.5 informacje o wersji RC | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.5 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.5 informacje o wersji RC, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fdb84da5f1648ce4508afe6ddcf04bddd41284d3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="75257-104">Informacje o wersji RC NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="75257-104">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="75257-105">[Informacje o wersji 3.5 Beta2 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 — informacje o wersji RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="75257-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="75257-106">3.5 wydanie koncentruje się na poprawie jakości i wydajności klientów NuGet.</span><span class="sxs-lookup"><span data-stu-id="75257-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="75257-107">Ponadto zostały dostarczone kilka funkcji, takich jak obsługa [rezerwowy folderów](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) obsługuje w `.nuspec` itd.</span><span class="sxs-lookup"><span data-stu-id="75257-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="75257-108">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="75257-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="75257-109">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="75257-109">Bug Fixes</span></span>

* <span data-ttu-id="75257-110">Instalacja/przywracania pakietu nie powiodło się "pakiet zawiera wiele `.nuspec` pliki."</span><span class="sxs-lookup"><span data-stu-id="75257-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="75257-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="75257-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="75257-112">Pakiet nuget wymuszone dodaje `.tt` plików do folderu zawartości bez względu na okoliczności - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="75257-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="75257-113">csproj pakiet nuget (z `project.json`) ulega awarii, jeśli istnieją nie packOptions i właściciel w pliku JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="75257-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="75257-114">Pakiet nuget `project.json` ignoruje tagi packOptions podsumowanie, autorzy, właściciele itp - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="75257-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="75257-115">Pakiet nuget ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="75257-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="75257-116">Aktualizowania wielu pakietów z wycofywania pozostawia projektu w stan przerwane — [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="75257-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="75257-117">Nie dodano pliki we wszystkich projektów krótkich nazw netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="75257-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="75257-118">Nie można spakować biblioteki przeznaczonych dla platformy .net Standard poprawnie - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="75257-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="75257-119">Plik -> Nowy Projekt -> projektu biblioteki klas (przenośna) kończy się niepowodzeniem w programie VS2015 i Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="75257-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="75257-120">Błąd nuGet — 1.0.0-\* nie jest prawidłowym ciągiem wersji - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="75257-120">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="75257-121">Znajdź pakietu nie powiedzie się do wyświetlania, ale działa Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="75257-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="75257-122">Błąd podczas "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="75257-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="75257-123">Gdy zainstalowanej wersji programu VS 2015 Aktualizacja 3 w wersji programu VS używane NuGet występuje błąd wersji 3.5.0 — [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="75257-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="75257-124">Pakiet interfejsu użytkownika Menedżera: nie są wyświetlane po zaktualizowaniu pakietu nowej wersji — [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="75257-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="75257-125">-ApiKey w wierszu polecenia delete nie odczytu/wysyłane 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="75257-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="75257-126">Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć na zależność wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="75257-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="75257-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="75257-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="75257-128">Tworzenie PCL (net46 i windows 10) projektu get NullRef wyjątku.</span><span class="sxs-lookup"><span data-stu-id="75257-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="75257-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="75257-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="75257-130">Aktualizacja Nuget należy podać komunikat informacyjny w przypadku nowszej wersji jest ograniczony przez ograniczenie allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="75257-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="75257-131">Dodatek poświadczeń został zakończony z powodu błędu -1 / błąd podczas pobierania pakietu podczas używania dostawcy poświadczeń z wielu źródeł - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="75257-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="75257-132">Pakiet nuget - Brak Newtonsoft.Json zależność pakietu - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="75257-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="75257-133">Błąd w ExecuteSynchronizedCore w systemie Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="75257-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="75257-134">VS nie obsługuje zmiennych środowiskowych w repositoryPath (nie nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="75257-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="75257-135">Rozwiąż problemy dotyczące ułatwień dostępu — [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="75257-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="75257-136">Przenośne platformy przy użyciu profilów podzielonym są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="75257-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="75257-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="75257-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="75257-138">Menedżer pakietów NuGet powinien stał się wyczyścić tej listy opcji w pakietach szczegółów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="75257-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="75257-139">Aktualizacja NuGet 3.3.0 "... dodatkowe ograniczenie zdefiniowane w pliku packages.config uniemożliwia wykonanie tej operacji."</span><span class="sxs-lookup"><span data-stu-id="75257-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="75257-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="75257-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="75257-141">Instalowanie pakietu z lokalnego źródła, które nie istnieje zgłasza sfałszowany komunikat - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="75257-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="75257-142">Filtr "Dostępne uaktualnienia" pokazuje uaktualnień, które narusza ograniczenie wersji - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="75257-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="75257-143">Usprawnienia wydajności</span><span class="sxs-lookup"><span data-stu-id="75257-143">Performance Improvements</span></span>

* <span data-ttu-id="75257-144">Wydajność: Zwiększyć ContentModel docelowej framework analizowania - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="75257-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="75257-145">Wydajność: Unikaj odczytu `runtime.json` plików dla operacji przywracania, które nie mają identyfikatorów RID [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="75257-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="75257-146">Na maszynach CI przywrócić przykładowej aplikacji sieci Web ASP.NET zmniejszone ponad 15 sekund do 3 w sekundach.</span><span class="sxs-lookup"><span data-stu-id="75257-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="75257-147">Wydajność: Czas ładowania init.ps1 w konsoli Menedżera pakietów [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="75257-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="75257-148">Czas, aby otworzyć PackageManagerConsole zwiększona w niektórych przypadkach z 132s 10s.</span><span class="sxs-lookup"><span data-stu-id="75257-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="75257-149">Rozwiązać problemy z wydajnością ReSharper w aktualizacji NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): na przykładowy projekt, czas trwania, aby zainstalować pakiety zredukować z 140s 68s.</span><span class="sxs-lookup"><span data-stu-id="75257-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="75257-150">Dcr</span><span class="sxs-lookup"><span data-stu-id="75257-150">DCRs</span></span>

* <span data-ttu-id="75257-151">Należy powiadomić użytkowników, że uaktualnienie/instalowanie tfm dotnet, na podstawie PCL może to spowodować problemy — NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="75257-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="75257-152">Ostrzegaj zły instalacja/aktualizacja dla projektu z tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="75257-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="75257-153">Dodawanie obsługi netcoreapp11 i netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="75257-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="75257-154">Drukuj zawartość nagłówka ostrzeżenie NuGet do konsoli w nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="75257-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="75257-155">Wykorzystywanie assemblymetadata — atrybut `.nuspec` token zamiany - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="75257-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="75257-156">Usuń właściwość locked z pliku blokady - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="75257-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="75257-157">Pakiety symboli nigdy nie należy używać w instalacji lub aktualizacji #2807</span><span class="sxs-lookup"><span data-stu-id="75257-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="75257-158">Funkcje</span><span class="sxs-lookup"><span data-stu-id="75257-158">Features</span></span>

* <span data-ttu-id="75257-159">Obsługi rezerwowego pakietu folderów - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="75257-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="75257-160">Projektowania i implementacji pojęcie typu pakietu do obsługi pakietów narzędzie - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="75257-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="75257-161">Interfejsu API można pobrać ścieżki do folderu pakietów globalne - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="75257-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="75257-162">Oryginalne pakiety aktualizacji support — [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="75257-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
