---
title: Informacje o wydaniu programu NuGet 4.9 RTM
description: Informacje o wersji dla NuGet 4.9, w tym znane problemy, poprawki błędów, nowe funkcje i dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496462"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="acdf5-103">Informacje o wersji nuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="acdf5-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="acdf5-104">Pojazdy dystrybucyjne NuGet:</span><span class="sxs-lookup"><span data-stu-id="acdf5-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="acdf5-105">Wersja NuGet</span><span class="sxs-lookup"><span data-stu-id="acdf5-105">NuGet version</span></span> | <span data-ttu-id="acdf5-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="acdf5-106">Available in Visual Studio version</span></span>| <span data-ttu-id="acdf5-107">Dostępne w plikach .NET SDK</span><span class="sxs-lookup"><span data-stu-id="acdf5-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="acdf5-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="acdf5-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="acdf5-109">Visual Studio 2017 w wersji 15.9.0</span><span class="sxs-lookup"><span data-stu-id="acdf5-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="acdf5-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="acdf5-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="acdf5-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="acdf5-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="acdf5-112">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="acdf5-112">n/a</span></span> | <span data-ttu-id="acdf5-113">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="acdf5-113">n/a</span></span> |
| [<span data-ttu-id="acdf5-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="acdf5-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="acdf5-115">Visual Studio 2017 w wersji 15.9.4</span><span class="sxs-lookup"><span data-stu-id="acdf5-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="acdf5-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="acdf5-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="acdf5-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="acdf5-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="acdf5-118">Visual Studio 2017 w wersji 15.9.6</span><span class="sxs-lookup"><span data-stu-id="acdf5-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="acdf5-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="acdf5-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="acdf5-120">Krótki opis: Co nowego w 4.9.0</span><span class="sxs-lookup"><span data-stu-id="acdf5-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="acdf5-121">Podpisywanie: Włącz ClientPolicies wymagać użycia zestawu zaufanych autorów i repozytoriów wymienionych w NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="acdf5-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="acdf5-122">tworzenie plików ".snupkg" zawierają symbole w opakowaniu - poprawić push do zrozumienia protokołu nuget do akceptowania plików snupkg dla serwera symboli - [#6878](https://github.com/NuGet/Home/issues/6878), [blogu](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="acdf5-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="acdf5-123">Wtyczka poświadczeń NuGet V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="acdf5-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="acdf5-124">Samodzielne pakiety NuGet - Licencja - [#4628](https://github.com/NuGet/Home/issues/4628), [ogłoszenie](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="acdf5-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="acdf5-125">Włącz metadane opt-in "GeneratePathProperty" na PackageReference, aby wygenerować właściwość na pakiet MSBuild do katalogu "Foo.Bar\1.0\" katalogu — [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="acdf5-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="acdf5-126">Zwiększ sukces klienta dzięki operacjom NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="acdf5-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="acdf5-127">Włącz powtarzalne przywracanie pakietu za pomocą pliku blokady - [#5602](https://github.com/NuGet/Home/issues/5602), [ogłoszenie](https://github.com/NuGet/Announcements/issues/28), wpis [w blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="acdf5-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="acdf5-128">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="acdf5-128">Issues fixed in this release</span></span>

* <span data-ttu-id="acdf5-129">Ostrzeżenia podwyższone do błędów (za pośrednictwem WarnAsErrors) wywoływane przez PackageExtraction nigdy nie powinny pozostawiać wyodrębnionych pakietów wokół - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="acdf5-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="acdf5-130">Źle podpisane pakiety nie powinny trafić do folderu pakietów globalnych - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="acdf5-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="acdf5-131">generowanie przekierowania wiązania nie powinno pomijać zespołów elewacyjnych - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="acdf5-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="acdf5-132">VersionRange Equals nie porównuje zakresów przestawnych — [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="acdf5-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="acdf5-133">Przywracanie: regresja wydajności przy użyciu nowego stosu HTTP .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="acdf5-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="acdf5-134">Aktualizacja pakietu nie należy modyfikować PrivateAssets packageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="acdf5-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="acdf5-135">Podpisywanie: podpisywanie powinno zakończyć się niepowodzeniem, jeśli pakiet ma zbyt wiele wpisów pakietu (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="acdf5-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="acdf5-136">Ścieżka kodu "dotnet nuget push" powinna obsługiwać nowego dostawcę poświadczeń — [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="acdf5-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="acdf5-137">Obsługa wykonywania wtyczek z niezmienną kulturą (jak to się dzieje w docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="acdf5-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="acdf5-138">nuget sources add nie należy usuwać poświadczeń z pliku NuGet.config — [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="acdf5-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="acdf5-139">instalowanie devDependency PackageReference powinien domyślnie excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="acdf5-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="acdf5-140">fix migrator opcja, która ma być wyświetlana dla wszystkich projektów i pokazać błąd, jeśli projekt jest niezgodny - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="acdf5-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="acdf5-141">"dotnet add package" powinien zatwierdzić przywracanie, które wykonuje w pliku zasobów - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="acdf5-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="acdf5-142">Podpisywanie: ulepszanie komunikatów o błędach związanych z podpisywaniem — [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="acdf5-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="acdf5-143">[Błąd testu] [zh-TW] Ciąg "Konsola menedżera pakietów" nie lokalizuje się na konsoli Menedżera pakietów — [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="acdf5-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="acdf5-144">Komunikat o błędzie wokół "Nie można znaleźć informacji o projekcie" powinien być nieco bardziej szczegółowy wewnątrz VS — [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="acdf5-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="acdf5-145">Niepomocny komunikat o błędzie, gdy niepoprawnie przy użyciu nuspec tag wersji nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="acdf5-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="acdf5-146">DCR - Podpisywanie: obsługa protokołu NuGet: RepozytoriumSignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="acdf5-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="acdf5-147">DCR - plik .nupkg.metadata zostanie utworzony podczas wyodrębniania pakietu - zawiera "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="acdf5-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="acdf5-148">DCR - Pomiń weryfikację authenticode dla wtyczek podczas wykonywania na Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="acdf5-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="acdf5-149">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.0</span><span class="sxs-lookup"><span data-stu-id="acdf5-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="acdf5-150">Krótki opis: Co nowego w 4.9.1</span><span class="sxs-lookup"><span data-stu-id="acdf5-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="acdf5-151">Dodaj obsługę czytania zapisu do nuget.config za pomocą nowego polecenia zaufanych sygnatariuszy - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="acdf5-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="acdf5-152">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="acdf5-152">Issues fixed in this release</span></span>

* <span data-ttu-id="acdf5-153">Napraw generowanie łączy licencji - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="acdf5-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="acdf5-154">Regresja kodów błędów do sprawdzania poprawności podpisów - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="acdf5-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="acdf5-155">Pakiet NuGet.Build.Tasks.Pack nie zawiera informacji o licencji — [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="acdf5-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="acdf5-156">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.1</span><span class="sxs-lookup"><span data-stu-id="acdf5-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="acdf5-157">Krótki opis: Co nowego w 4.9.2</span><span class="sxs-lookup"><span data-stu-id="acdf5-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="acdf5-158">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="acdf5-158">Issues fixed in this release</span></span>

* <span data-ttu-id="acdf5-159">Narzędzie VS/dotnet.exe/nuget.exe/msbuild.exe przywracanie nie używa poświadczeń, gdy nazwa źródła zawiera odstęp - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="acdf5-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="acdf5-160">LicenseAcceptanceWindow i LicenseFileWindow Problemy z dostępnością - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="acdf5-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="acdf5-161">Fix FormatException w DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="acdf5-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="acdf5-162">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.2</span><span class="sxs-lookup"><span data-stu-id="acdf5-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="acdf5-163">Krótki opis: Co nowego w 4.9.3</span><span class="sxs-lookup"><span data-stu-id="acdf5-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="acdf5-164">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="acdf5-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="acdf5-165">Problemy z "powtarzalnym pakietem przy użyciu pliku blokady"</span><span class="sxs-lookup"><span data-stu-id="acdf5-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="acdf5-166">Tryb zablokowany nie działa jako skrót jest obliczany niepoprawnie dla wcześniej buforowanych pakietów - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="acdf5-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="acdf5-167">Przywracanie rozwiązuje do innej wersji `packages.lock.json` niż zdefiniowane w pliku - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="acdf5-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="acdf5-168">'--locked-mode / RestoreLockedMode' powoduje fałszywe błędy przywracania, gdy zaangażowane są wnioskowania projectreferences - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="acdf5-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="acdf5-169">Program rozpoznawania nazw zestawu SDK msbuild próbuje zweryfikować sha dla pakietu zestawu SDK, który nie powiedzie się przywrócenie podczas korzystania z packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="acdf5-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="acdf5-170">Problemy "Blokowanie zależności przy użyciu konfigurowalnych zasad zaufania"</span><span class="sxs-lookup"><span data-stu-id="acdf5-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="acdf5-171">dotnet.exe nie powinien oceniać zaufanych sygnatariuszy, gdy podpisane pakiety nie są obsługiwane - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="acdf5-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="acdf5-172">Kolejność zaufanych podpisywzorów w pliku konfiguracyjnym wpływa na ocenę zaufania - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="acdf5-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="acdf5-173">Nie można zaimplementować ustawień ISettings [Spowodowane przez refaktoryzowanie ustawień interfejsów API do obsługi funkcji zasad zaufania] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="acdf5-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="acdf5-174">Problemy z "ulepszonym debugowaniem"</span><span class="sxs-lookup"><span data-stu-id="acdf5-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="acdf5-175">Nie można opublikować pakietu symboli dla narzędzia globalnego .NET Core — [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="acdf5-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="acdf5-176">Problemy z "samodzielnymi pakietami NuGet — licencja"</span><span class="sxs-lookup"><span data-stu-id="acdf5-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="acdf5-177">Błąd podczas tworzenia symbolu .snupkg podczas korzystania z osadzonego pliku licencji - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="acdf5-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="acdf5-178">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.3</span><span class="sxs-lookup"><span data-stu-id="acdf5-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="acdf5-179">Krótki opis: Co nowego w 4.9.4</span><span class="sxs-lookup"><span data-stu-id="acdf5-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="acdf5-180">Poprawka zabezpieczeń: Uprawnienia do plików utworzonych wewnątrz ~/.nuget są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="acdf5-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="acdf5-181">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="acdf5-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="acdf5-182">dotnet nuget push --interactive daje błąd na komputerze Mac.</span><span class="sxs-lookup"><span data-stu-id="acdf5-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="acdf5-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="acdf5-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="acdf5-184">Problem</span><span class="sxs-lookup"><span data-stu-id="acdf5-184">Issue</span></span>
<span data-ttu-id="acdf5-185">Argument `--interactive` nie jest przekazywany przez dotnet cli i powoduje błąd`error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="acdf5-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="acdf5-186">Obejście</span><span class="sxs-lookup"><span data-stu-id="acdf5-186">Workaround</span></span>
<span data-ttu-id="acdf5-187">Uruchom inne polecenie dotnet z opcją `dotnet restore --interactive` interaktywną, taką jak i uwierzytelnij.</span><span class="sxs-lookup"><span data-stu-id="acdf5-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="acdf5-188">Uwierzytelnianie może być buforowane przez dostawcę poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="acdf5-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="acdf5-189">Następnie należy uruchomić polecenie `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="acdf5-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="acdf5-190">Pakiety w składach rezerwowych zainstalowanych przez pakiet .NET Core SDK są instalowane na zamówienie i nie można ich sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="acdf5-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="acdf5-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="acdf5-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="acdf5-192">Problem</span><span class="sxs-lookup"><span data-stu-id="acdf5-192">Issue</span></span>
<span data-ttu-id="acdf5-193">W przypadku korzystania z pliku dotnet.exe 2.x w celu przywrócenia projektu, który zawiera wiele celów netcoreapp 1.x i netcoreapp 2.x, folder rezerwowy jest traktowany jako plik danych.</span><span class="sxs-lookup"><span data-stu-id="acdf5-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="acdf5-194">Oznacza to, że podczas przywracania NuGet wybierze pakiet z folderu rezerwowego i spróbuje zainstalować go w folderze pakietów globalnych i wykonaj zwykłe sprawdzanie poprawności podpisywania, które zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="acdf5-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="acdf5-195">Obejście</span><span class="sxs-lookup"><span data-stu-id="acdf5-195">Workaround</span></span>
<span data-ttu-id="acdf5-196">Wyłącz użycie folderu rezerwowego, `RestoreAdditionalProjectSources` ustawiając na nic.</span><span class="sxs-lookup"><span data-stu-id="acdf5-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="acdf5-197">`<RestoreAdditionalProjectSources/>`Użyj tego ostrożnie, ponieważ spowoduje to wiele pakietów do pobrania z NuGet.org które w przeciwnym razie zostałyby przywrócone z folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="acdf5-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
