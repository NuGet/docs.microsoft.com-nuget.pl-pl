---
title: 3.5 informacje o wersji RC
description: Informacje o wersji programu NuGet 3.5 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d620a8b8d97f9a52cb2bc93a91eb393130a42898
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="e53c1-103">Informacje o wersji RC NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="e53c1-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="e53c1-104">[Informacje o wersji 3.5 Beta2 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 — informacje o wersji RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="e53c1-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="e53c1-105">3.5 wydanie koncentruje się na poprawie jakości i wydajności klientów NuGet.</span><span class="sxs-lookup"><span data-stu-id="e53c1-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="e53c1-106">Ponadto zostały dostarczone kilka funkcji, takich jak obsługa [rezerwowy folderów](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) obsługuje w `.nuspec` itd.</span><span class="sxs-lookup"><span data-stu-id="e53c1-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="e53c1-107">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="e53c1-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="e53c1-108">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="e53c1-108">Bug Fixes</span></span>

* <span data-ttu-id="e53c1-109">Instalacja/przywracania pakietu nie powiodło się "pakiet zawiera wiele `.nuspec` pliki."</span><span class="sxs-lookup"><span data-stu-id="e53c1-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="e53c1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="e53c1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="e53c1-111">Pakiet nuget wymuszone dodaje `.tt` plików do folderu zawartości bez względu na okoliczności - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="e53c1-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="e53c1-112">csproj pakiet nuget (z `project.json`) ulega awarii, jeśli istnieją nie packOptions i właściciel w pliku JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="e53c1-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="e53c1-113">Pakiet nuget `project.json` ignoruje tagi packOptions podsumowanie, autorzy, właściciele itp - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="e53c1-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="e53c1-114">Pakiet nuget ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="e53c1-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="e53c1-115">Aktualizowania wielu pakietów z wycofywania pozostawia projektu w stan przerwane — [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="e53c1-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="e53c1-116">Nie dodano pliki we wszystkich projektów krótkich nazw netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="e53c1-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="e53c1-117">Nie można spakować biblioteki przeznaczonych dla platformy .net Standard poprawnie - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="e53c1-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="e53c1-118">Plik -> Nowy Projekt -> projektu biblioteki klas (przenośna) kończy się niepowodzeniem w programie VS2015 i Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="e53c1-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="e53c1-119">Błąd NuGet — 1.0.0-\* nie jest prawidłowym ciągiem wersji - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="e53c1-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="e53c1-120">Znajdź pakietu nie powiedzie się do wyświetlania, ale działa Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="e53c1-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="e53c1-121">Błąd podczas "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="e53c1-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="e53c1-122">Gdy zainstalowanej wersji programu VS 2015 Aktualizacja 3 w wersji programu VS używane NuGet występuje błąd wersji 3.5.0 — [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="e53c1-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="e53c1-123">Pakiet interfejsu użytkownika Menedżera: nie są wyświetlane po zaktualizowaniu pakietu nowej wersji — [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="e53c1-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="e53c1-124">-ApiKey w wierszu polecenia delete nie odczytu/wysyłane 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="e53c1-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="e53c1-125">Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć na zależność wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="e53c1-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="e53c1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="e53c1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="e53c1-127">Tworzenie PCL (net46 i windows 10) projektu get NullRef wyjątku.</span><span class="sxs-lookup"><span data-stu-id="e53c1-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="e53c1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="e53c1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="e53c1-129">Aktualizacja Nuget należy podać komunikat informacyjny w przypadku nowszej wersji jest ograniczony przez ograniczenie allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="e53c1-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="e53c1-130">Dodatek poświadczeń został zakończony z powodu błędu -1 / błąd podczas pobierania pakietu podczas używania dostawcy poświadczeń z wielu źródeł - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="e53c1-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="e53c1-131">Pakiet nuget - Brak Newtonsoft.Json zależność pakietu - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="e53c1-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="e53c1-132">Błąd w ExecuteSynchronizedCore w systemie Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="e53c1-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="e53c1-133">VS nie obsługuje zmiennych środowiskowych w repositoryPath (nie nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="e53c1-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="e53c1-134">Rozwiąż problemy dotyczące ułatwień dostępu — [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="e53c1-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="e53c1-135">Przenośne platformy przy użyciu profilów podzielonym są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="e53c1-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="e53c1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="e53c1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="e53c1-137">Menedżer pakietów NuGet powinien stał się wyczyścić tej listy opcji w pakietach szczegółów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="e53c1-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="e53c1-138">Aktualizacja NuGet 3.3.0 "... dodatkowe ograniczenie zdefiniowane w pliku packages.config uniemożliwia wykonanie tej operacji."</span><span class="sxs-lookup"><span data-stu-id="e53c1-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="e53c1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="e53c1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="e53c1-140">Instalowanie pakietu z lokalnego źródła, które nie istnieje zgłasza sfałszowany komunikat - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="e53c1-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="e53c1-141">Filtr "Dostępne uaktualnienia" pokazuje uaktualnień, które narusza ograniczenie wersji - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="e53c1-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="e53c1-142">Usprawnienia wydajności</span><span class="sxs-lookup"><span data-stu-id="e53c1-142">Performance Improvements</span></span>

* <span data-ttu-id="e53c1-143">Wydajność: Zwiększyć ContentModel docelowej framework analizowania - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="e53c1-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="e53c1-144">Wydajność: Unikaj odczytu `runtime.json` plików dla operacji przywracania, które nie mają identyfikatorów RID [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="e53c1-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="e53c1-145">Na maszynach CI przywrócić przykładowej aplikacji sieci Web ASP.NET zmniejszone ponad 15 sekund do 3 w sekundach.</span><span class="sxs-lookup"><span data-stu-id="e53c1-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="e53c1-146">Wydajność: Czas ładowania init.ps1 w konsoli Menedżera pakietów [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="e53c1-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="e53c1-147">Czas, aby otworzyć PackageManagerConsole zwiększona w niektórych przypadkach z 132s 10s.</span><span class="sxs-lookup"><span data-stu-id="e53c1-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="e53c1-148">Rozwiązać problemy z wydajnością ReSharper w aktualizacji NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): na przykładowy projekt, czas trwania, aby zainstalować pakiety zredukować z 140s 68s.</span><span class="sxs-lookup"><span data-stu-id="e53c1-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="e53c1-149">Dcr</span><span class="sxs-lookup"><span data-stu-id="e53c1-149">DCRs</span></span>

* <span data-ttu-id="e53c1-150">Należy powiadomić użytkowników, że uaktualnienie/instalowanie tfm dotnet, na podstawie PCL może to spowodować problemy — NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="e53c1-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="e53c1-151">Ostrzegaj zły instalacja/aktualizacja dla projektu z tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="e53c1-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="e53c1-152">Dodawanie obsługi netcoreapp11 i netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="e53c1-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="e53c1-153">Drukuj zawartość nagłówka ostrzeżenie NuGet do konsoli w nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="e53c1-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="e53c1-154">Wykorzystywanie assemblymetadata — atrybut `.nuspec` token zamiany - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="e53c1-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="e53c1-155">Usuń właściwość locked z pliku blokady - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="e53c1-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="e53c1-156">Pakiety symboli nigdy nie należy używać w instalacji lub aktualizacji #2807</span><span class="sxs-lookup"><span data-stu-id="e53c1-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="e53c1-157">Funkcje</span><span class="sxs-lookup"><span data-stu-id="e53c1-157">Features</span></span>

* <span data-ttu-id="e53c1-158">Obsługi rezerwowego pakietu folderów - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="e53c1-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="e53c1-159">Projektowania i implementacji pojęcie typu pakietu do obsługi pakietów narzędzie - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="e53c1-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="e53c1-160">Interfejsu API można pobrać ścieżki do folderu pakietów globalne - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="e53c1-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="e53c1-161">Oryginalne pakiety aktualizacji support — [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="e53c1-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
