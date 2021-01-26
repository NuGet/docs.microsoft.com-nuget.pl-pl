---
title: Informacje o wersji 3,5 RC
description: Informacje o wersji programu NuGet 3,5 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780198"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="b664f-103">Informacje o wersji narzędzia NuGet 3,5 RC</span><span class="sxs-lookup"><span data-stu-id="b664f-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="b664f-104">[NuGet 3,5 — informacje](../release-notes/nuget-3.5-Beta2.md)  |  o wersji beta2 Pakiet [NuGet 3,5 — informacje o wersji RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="b664f-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="b664f-105">Wersja 3,5 jest ukierunkowana na poprawę jakości i wydajności klientów programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="b664f-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="b664f-106">Ponadto firma Microsoft dostarczyła kilka funkcji, takich jak obsługa [folderów rezerwowych](https://github.com/NuGet/Home/issues/2899), obsługa elementów [PackageType](https://github.com/NuGet/Home/issues/2476) w `.nuspec` i innych.</span><span class="sxs-lookup"><span data-stu-id="b664f-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="b664f-107">Lista problemów</span><span class="sxs-lookup"><span data-stu-id="b664f-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="b664f-108">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="b664f-108">Bug Fixes</span></span>

* <span data-ttu-id="b664f-109">Instalowanie/przywracanie pakietu kończy się niepowodzeniem z "pakiet zawiera wiele `.nuspec` plików".</span><span class="sxs-lookup"><span data-stu-id="b664f-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="b664f-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="b664f-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="b664f-111">Pakiet NuGet wymusza dodanie `.tt` plików do folderu Content niezależnie od tego, co [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="b664f-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="b664f-112">Pakiet NuGet csproj (z `project.json` ) ulega awarii, jeśli nie ma packOptions i właściciela w pliku JSON — [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="b664f-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="b664f-113">Pakiet NuGet dla `project.json` ignorowania tagów packOptions, takich jak podsumowanie, autorzy, właściciele itp., [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="b664f-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="b664f-114">Pakiet NuGet ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="b664f-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="b664f-115">Aktualizacja wielu pakietów z wycofywaniem pozostawia projekt w stanie przerwania — [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="b664f-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="b664f-116">ContentFiles w obszarze any nie są dodawane do projektów standardowych, [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="b664f-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="b664f-117">Nie można prawidłowo spakować biblioteki dla platformy .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="b664f-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="b664f-118">Plik > nowy projekt — > Biblioteka klas (przenośna) kończy się niepowodzeniem w programu VS2015 i Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="b664f-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="b664f-119">Błąd NuGet-1.0.0-\* nie jest prawidłowym ciągiem wersji- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="b664f-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="b664f-120">Nie można wyświetlić Find-Package, ale Install-Package działa [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="b664f-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="b664f-121">Błąd podczas "Install-Package jQuery. Validation" w dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="b664f-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="b664f-122">Po zainstalowaniu programu VS 2015 Update 3 w programie VS, który korzysta z 3.5.0 w wersji NuGet, występuje błąd- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="b664f-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="b664f-123">Interfejs użytkownika Menedżera pakietów: nie wyświetla nowej wersji po zaktualizowaniu pakietu — [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="b664f-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="b664f-124">-ApiKey w wierszu polecenia usuwania nie jest odczytywany/wysyłany w 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="b664f-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="b664f-125">Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć w zależności od wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="b664f-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="b664f-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="b664f-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="b664f-127">Tworzenie wyjątku NullRef w projekcie PCL (net46 i Windows 10).</span><span class="sxs-lookup"><span data-stu-id="b664f-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="b664f-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="b664f-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="b664f-129">Aktualizacja NuGet powinna podawać komunikat informacyjny, gdy wyższa wersja jest ograniczona przez ograniczenie allowedVersions — [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="b664f-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="b664f-130">Wtyczka poświadczeń została zakończona z błędem-1/Pobieranie pakietu podczas korzystania z dostawców poświadczeń z wieloma źródłami — [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="b664f-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="b664f-131">Pakiet NuGet — brak Newtonsoft.Jsw zależności od pakietu — [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="b664f-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="b664f-132">Usterka w ExecuteSynchronizedCore w systemie Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="b664f-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="b664f-133">Program VS nie obsługuje zmiennych środowiskowych w programie repositoryPath (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="b664f-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="b664f-134">Rozwiązywanie problemów z ułatwieniami dostępu — [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="b664f-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="b664f-135">Platformy przenośne z zadzielonymi profilami są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="b664f-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="b664f-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="b664f-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="b664f-137">Menedżer pakietów NuGet powinien wyczyścić, że lista opcji w szczegółach pakietów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="b664f-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="b664f-138">Aktualizacja NuGet 3.3.0 kończy się niepowodzeniem z "dodatkowym ograniczeniem... zdefiniowane w packages.config uniemożliwia wykonanie tej operacji ".</span><span class="sxs-lookup"><span data-stu-id="b664f-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="b664f-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="b664f-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="b664f-140">Instalowanie pakietu z lokalnego źródła, które nie istnieje, zgłasza fałszywe wiadomości [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="b664f-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="b664f-141">Filtr "dostępne uaktualnienie" zawiera uaktualnienia, które naruszają ograniczenie wersji — [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="b664f-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="b664f-142">Usprawnienia wydajności</span><span class="sxs-lookup"><span data-stu-id="b664f-142">Performance Improvements</span></span>

* <span data-ttu-id="b664f-143">Wydajność: ulepszanie analizy struktury docelowej ContentModel — [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="b664f-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="b664f-144">Wydajność: należy unikać odczytywania `runtime.json` plików do przywracania, które nie mają identyfikatorów rid [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="b664f-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="b664f-145">Na komputerach CI można przywrócić przykładową aplikację sieci Web ASP.NET ograniczoną od ponad 15 sekund do 3 s.</span><span class="sxs-lookup"><span data-stu-id="b664f-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="b664f-146">Wydajność: Konsola Menedżera pakietów init.ps1 czas ładowania [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="b664f-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="b664f-147">Czas, aby otworzyć PackageManagerConsole udoskonalony w niektórych przypadkach z 132S na dziesiątkach.</span><span class="sxs-lookup"><span data-stu-id="b664f-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="b664f-148">Rozwiązywanie problemów z wydajnością w pakiecie NuGet Update- [#3044](https://github.com/NuGet/Home/issues/3044): w przykładowym projekcie czas potrzebny na zainstalowanie pakietów zredukowanych z 140S do 68s.</span><span class="sxs-lookup"><span data-stu-id="b664f-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="b664f-149">DCR</span><span class="sxs-lookup"><span data-stu-id="b664f-149">DCRs</span></span>

* <span data-ttu-id="b664f-150">Pakiet NuGet musi poinformować użytkowników, że uaktualnianie/Instalowanie w formacie PCL opartym na platformie dotnet TFM może powodować problemy — [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="b664f-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="b664f-151">Ostrzegaj o złej instalacji/uaktualnieniu dla projektu w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="b664f-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="b664f-152">Dodawanie obsługi netcoreapp11 i netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="b664f-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="b664f-153">Drukuj zawartość nagłówka NuGet-Warning w konsoli programu nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="b664f-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="b664f-154">Wykorzystanie atrybutu AssemblyMetadata dla `.nuspec` zamiany tokenów — [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="b664f-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="b664f-155">Usuń zablokowaną właściwość z pliku blokady — [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="b664f-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="b664f-156">Pakiety symboli nie powinny być używane w instalacji ani aktualizacji #2807</span><span class="sxs-lookup"><span data-stu-id="b664f-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="b664f-157">Funkcje</span><span class="sxs-lookup"><span data-stu-id="b664f-157">Features</span></span>

* <span data-ttu-id="b664f-158">Obsługa folderów pakietów powrotu — [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="b664f-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="b664f-159">Projektuj i Implementuj pojęcie typu pakietu do obsługi pakietów narzędzi — [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="b664f-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="b664f-160">Interfejs API umożliwiający uzyskanie ścieżki do folderu pakietów globalnych — [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="b664f-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="b664f-161">Obsługa aktualizacji pakietów natywnych — [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="b664f-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
