---
title: Informacje o wersji 4.9 RTM NuGet
description: Informacje o wersji programu NuGet 4.9 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 99578c5ed7e88b7269872bf88c465bbda462870a
ms.sourcegitcommit: 585394f063e95dcbc24d7ac0ce07de643eaf6f4d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045111"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="25a82-103">4.9 wersji NuGet</span><span class="sxs-lookup"><span data-stu-id="25a82-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="25a82-104">NuGet pojazdów dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="25a82-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="25a82-105">NuGet w wersji</span><span class="sxs-lookup"><span data-stu-id="25a82-105">NuGet version</span></span> | <span data-ttu-id="25a82-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="25a82-106">Available in Visual Studio version</span></span>| <span data-ttu-id="25a82-107">Dostępne w zestawów SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="25a82-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="25a82-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="25a82-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="25a82-109">Visual Studio 2017 w wersji 15.9.0</span><span class="sxs-lookup"><span data-stu-id="25a82-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="25a82-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="25a82-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="25a82-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="25a82-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="25a82-112">n/d</span><span class="sxs-lookup"><span data-stu-id="25a82-112">n/a</span></span> | <span data-ttu-id="25a82-113">n/d</span><span class="sxs-lookup"><span data-stu-id="25a82-113">n/a</span></span> |
| [<span data-ttu-id="25a82-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="25a82-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="25a82-115">Visual Studio 2017 w wersji 15.9.4</span><span class="sxs-lookup"><span data-stu-id="25a82-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="25a82-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="25a82-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="25a82-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="25a82-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="25a82-118">Visual Studio 2017 w wersji 15.9.6</span><span class="sxs-lookup"><span data-stu-id="25a82-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="25a82-119">n/d</span><span class="sxs-lookup"><span data-stu-id="25a82-119">n/a</span></span> |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="25a82-120">Podsumowanie: What's New in 4.9.0</span><span class="sxs-lookup"><span data-stu-id="25a82-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="25a82-121">Signing: Włącz ClientPolicies wymagać korzystanie z zestawu zaufanych autorzy i repozytoriów, wymienione w pliku NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [wpis w blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="25a82-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="25a82-122">Tworzenie plików ".snupkg" zawierają symbole w pakiecie — Zwiększ wypchnięcie, aby zrozumieć nuget protokołu do akceptowania plików snupkg do serwera symboli - [#6878](https://github.com/NuGet/Home/issues/6878), [wpis w blogu](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="25a82-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="25a82-123">Wtyczka poświadczeń NuGet w wersji 2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="25a82-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="25a82-124">Pakiety NuGet niezależna - License - [#4628](https://github.com/NuGet/Home/issues/4628), [anonsu](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="25a82-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="25a82-125">Włącz zoptymalizowany pod kątem w metadanych "GeneratePathProperty" na PackageReference do wygenerowania dla właściwości MSBuild pakietu na "Foo.Bar\1.0\" katalogu — [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="25a82-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="25a82-126">Zwiększyć sukces klientów przy użyciu operacji NuGet — [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="25a82-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="25a82-127">Włącz Przywracanie pakietów powtarzalne przy użyciu blokady pliku — [#5602](https://github.com/NuGet/Home/issues/5602), [ogłoszenie](https://github.com/NuGet/Announcements/issues/28), [wpis w blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="25a82-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="25a82-128">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="25a82-128">Issues fixed in this release</span></span>

* <span data-ttu-id="25a82-129">Ostrzeżenia z podwyższonym poziomem uprawnień na błędy (za pośrednictwem WarnAsErrors), które zostały wygenerowane przez PackageExtraction nigdy nie należy pozostawić wyodrębniony pakiet wokół - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="25a82-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="25a82-130">Nieprawidłowo podpisanych pakietów nie powinna kończyć w folderze globalnymi pakietami - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="25a82-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="25a82-131">Powiązanie generowania przekierowania nie należy pomijać zestawy fasady - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="25a82-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="25a82-132">Jest równe VersionRange nie porównania zmiennoprzecinkowy zakresów — [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="25a82-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="25a82-133">Przywracanie: stos regresji wydajności przy użyciu protokołu HTTP nowej platformy .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="25a82-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="25a82-134">Aktualizacja pakietu nie należy modyfikować PrivateAssets PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="25a82-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="25a82-135">Podpisywanie: podpisywanie powinna zakończyć się niepowodzeniem Jeżeli pakiet zawiera zbyt wiele wpisów pakietu (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="25a82-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="25a82-136">prefiksu "dotnet nuget wypychania" powinien obsługiwać nowego dostawcę poświadczeń - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="25a82-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="25a82-137">Obsługuje wykonywanie wtyczek przy użyciu niezmiennej kultury (tak jak wykonywane na platformie docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="25a82-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="25a82-138">Dodaj źródła nuget, nie należy usuwać poświadczenia w pliku NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="25a82-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="25a82-139">Instalowanie devDependency PackageReference powinny domyślnie excludeassets = kompilacji - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="25a82-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="25a82-140">Usuń opcję migrator ma być wyświetlany dla wszystkich projektów i Pokaż błąd, jeśli projekt jest niezgodny - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="25a82-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="25a82-141">"dotnet Dodaj pakiet" powinien zużywać przywracania sprawdzi się w pliku zasobów - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="25a82-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="25a82-142">Podpisywanie: poprawa podpisywania pokrewne komunikaty o błędach - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="25a82-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="25a82-143">[Niepowodzenie testu] [zh-TW] Ciąg "Konsola Menedżera pakietów" nie zlokalizować w konsoli Menedżera pakietów - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="25a82-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="25a82-144">Komunikat o błędzie wokół "Nie można odnaleźć informacji o projekcie" powinna być nieco bardziej szczegółowe wewnątrz VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="25a82-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="25a82-145">Komunikat o błędzie zbędny, korzystając z niepoprawnie nuspec tag wersji pakietu nuget — [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="25a82-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="25a82-146">DCR - podpisywania: obsługują protokół NuGet: Zasób RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="25a82-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="25a82-147">DCR —. zostanie teraz utworzony plik nupkg.metadata podczas wyodrębniania pakietu - zawiera "zawartość hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="25a82-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="25a82-148">DCR - pomijania weryfikacji authenticode dla wtyczek podczas wykonywania w Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="25a82-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="25a82-149">Lista wszystkie problemy rozwiązane w tej wersji 4.9.0</span><span class="sxs-lookup"><span data-stu-id="25a82-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="25a82-150">Podsumowanie: What's New in 4.9.1</span><span class="sxs-lookup"><span data-stu-id="25a82-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="25a82-151">Dodano obsługę odczytu zapisu do pliku nuget.config, za pomocą nowego polecenia zaufanych — które podpisały - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="25a82-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="25a82-152">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="25a82-152">Issues fixed in this release</span></span>

* <span data-ttu-id="25a82-153">Napraw Generowanie konsolidacji licencji - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="25a82-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="25a82-154">Kody błędów regresji do weryfikowania podpisów- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="25a82-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="25a82-155">Pakiet NuGet.Build.Tasks.Pack nie ma informacji o licencjach - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="25a82-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="25a82-156">Lista wszystkie problemy rozwiązane w tej wersji 4.9.1</span><span class="sxs-lookup"><span data-stu-id="25a82-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="25a82-157">Podsumowanie: What's New in 4.9.2</span><span class="sxs-lookup"><span data-stu-id="25a82-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="25a82-158">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="25a82-158">Issues fixed in this release</span></span>

* <span data-ttu-id="25a82-159">VS/dotnet.exe/nuget.exe/msbuild.exe przywracania nie używa poświadczeń, gdy nazwa źródła zawiera odstępem - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="25a82-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="25a82-160">Problemy dotyczące LicenseAcceptanceWindow i dostępności LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="25a82-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="25a82-161">Usuń formatexception — na przykład DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="25a82-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="25a82-162">Lista wszystkie problemy rozwiązane w tej wersji 4.9.2</span><span class="sxs-lookup"><span data-stu-id="25a82-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="25a82-163">Podsumowanie: What's New in 4.9.3</span><span class="sxs-lookup"><span data-stu-id="25a82-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="25a82-164">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="25a82-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="25a82-165">Problemy z "Pozycji powtarzalne pakietu za pomocą pliku blokady"</span><span class="sxs-lookup"><span data-stu-id="25a82-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="25a82-166">Zablokowany tryb nie działa zgodnie z wyznaczania wartości skrótu jest obliczana niepoprawnie dla wcześniej pamięci podręcznej pakietów - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="25a82-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="25a82-167">Przywracanie jest rozpoznawana jako do innej wersji niż zdefiniowana w `packages.lock.json` pliku — [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="25a82-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="25a82-168">"--Tryb zablokowany / RestoreLockedMode" powoduje, że fałszywe błędy przywracania w przypadku odwołania do projektu - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="25a82-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="25a82-169">Mechanizm rozpoznawania zestawu SDK programu MSBuild próbuje zweryfikować SHA dla pakietu SDK, który zakończy się niepowodzeniem przywracania przy użyciu packages.lock.json — [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="25a82-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="25a82-170">"Zablokować zależności za pomocą zasad można skonfigurować zaufanie" problemów</span><span class="sxs-lookup"><span data-stu-id="25a82-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="25a82-171">DotNet.exe nie należy ocenić zaufane osoby podpisujące podpisanych pakietów nie są obsługiwane - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="25a82-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="25a82-172">Kolejność trustedSigners w pliku konfiguracji ma wpływ na ocenę zaufania - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="25a82-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="25a82-173">Nie można zaimplementować ISettings [spowodowany refaktoryzacją ustawienia interfejsów API do obsługi funkcji zasady zaufania]- [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="25a82-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="25a82-174">"Improved środowisko debugowania" problemów</span><span class="sxs-lookup"><span data-stu-id="25a82-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="25a82-175">Nie można opublikować pakietu symboli dla platformy .NET Core globalnego narzędzia - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="25a82-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="25a82-176">Problemy z "Pakiety NuGet niezależna - licencji"</span><span class="sxs-lookup"><span data-stu-id="25a82-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="25a82-177">Wystąpił błąd podczas tworzenia pakietu .snupkg symboli, korzystając z osadzonych pliku licencji - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="25a82-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="25a82-178">Lista wszystkie problemy rozwiązane w tej wersji 4.9.3</span><span class="sxs-lookup"><span data-stu-id="25a82-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a><span data-ttu-id="25a82-179">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="25a82-179">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="25a82-180">DotNet nuget push--interaktywne powoduje błąd na komputerze Mac.</span><span class="sxs-lookup"><span data-stu-id="25a82-180">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="25a82-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="25a82-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="25a82-182">Problem</span><span class="sxs-lookup"><span data-stu-id="25a82-182">Issue</span></span>
<span data-ttu-id="25a82-183">`--interactive` Argument nie są przekazywane przez interfejs wiersza polecenia platformy dotnet i powoduje błąd `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="25a82-183">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="25a82-184">Obejście</span><span class="sxs-lookup"><span data-stu-id="25a82-184">Workaround</span></span>
<span data-ttu-id="25a82-185">Aby możliwe było uruchamianie dowolnego polecenia dotnet z opcją interaktywnych, takich jak `dotnet restore --interactive` i uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="25a82-185">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="25a82-186">Uwierzytelnianie, program może być buforowane przez dostawcę poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="25a82-186">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="25a82-187">Następnie uruchom `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="25a82-187">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="25a82-188">Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="25a82-188">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="25a82-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="25a82-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="25a82-190">Problem</span><span class="sxs-lookup"><span data-stu-id="25a82-190">Issue</span></span>
<span data-ttu-id="25a82-191">Korzystając z dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych.</span><span class="sxs-lookup"><span data-stu-id="25a82-191">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="25a82-192">Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="25a82-192">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="25a82-193">Obejście</span><span class="sxs-lookup"><span data-stu-id="25a82-193">Workaround</span></span>
<span data-ttu-id="25a82-194">Wyłącz użycie folderu rezerwowy, ustawiając `RestoreAdditionalProjectSources` na wartość nothing.</span><span class="sxs-lookup"><span data-stu-id="25a82-194">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="25a82-195">`<RestoreAdditionalProjectSources/>` Korzystanie z rozwagą, ponieważ spowoduje to wiele pakietów, które mają być pobrane z repozytorium NuGet.org, które w przeciwnym razie byłoby zostały przywrócone z folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="25a82-195">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
