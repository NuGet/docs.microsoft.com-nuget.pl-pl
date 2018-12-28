---
title: Informacje o wersji 4.9 RTM NuGet
description: Informacje o wersji programu NuGet 4.9 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735139"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="cf594-103">4.9 wersji NuGet</span><span class="sxs-lookup"><span data-stu-id="cf594-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="cf594-104">NuGet pojazdów dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="cf594-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="cf594-105">NuGet w wersji</span><span class="sxs-lookup"><span data-stu-id="cf594-105">NuGet version</span></span> | <span data-ttu-id="cf594-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf594-106">Available in Visual Studio version</span></span>| <span data-ttu-id="cf594-107">Dostępne w zestawów SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="cf594-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="cf594-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="cf594-108">**4.9.0**</span></span> | <span data-ttu-id="cf594-109">Visual Studio 2017 w wersji 15.9.0</span><span class="sxs-lookup"><span data-stu-id="cf594-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="cf594-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="cf594-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="cf594-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="cf594-111">**4.9.1**</span></span> | <span data-ttu-id="cf594-112">n/d</span><span class="sxs-lookup"><span data-stu-id="cf594-112">n/a</span></span> | <span data-ttu-id="cf594-113">n/d</span><span class="sxs-lookup"><span data-stu-id="cf594-113">n/a</span></span> |
| [<span data-ttu-id="cf594-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="cf594-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="cf594-115">Visual Studio 2017 w wersji 15.9.4</span><span class="sxs-lookup"><span data-stu-id="cf594-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="cf594-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="cf594-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="cf594-117">Podsumowanie: What's New in 4.9.0</span><span class="sxs-lookup"><span data-stu-id="cf594-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="cf594-118">Podpisywania: Włącz ClientPolicies wymagać korzystanie z zestawu zaufanych autorzy i repozytoriów, wymienione w pliku NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [wpis w blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="cf594-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="cf594-119">Tworzenie plików ".snupkg" zawierają symbole w pakiecie — Zwiększ wypchnięcie, aby zrozumieć nuget protokołu do akceptowania plików snupkg do serwera symboli - [#6878](https://github.com/NuGet/Home/issues/6878), [wpis w blogu](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="cf594-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="cf594-120">Wtyczka poświadczeń NuGet w wersji 2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="cf594-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="cf594-121">Pakiety NuGet niezależna - License - [#4628](https://github.com/NuGet/Home/issues/4628), [anonsu](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="cf594-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="cf594-122">Włącz zoptymalizowany pod kątem w metadanych "GeneratePathProperty" na PackageReference do wygenerowania dla właściwości MSBuild pakietu na "Foo.Bar\1.0\" katalogu — [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="cf594-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="cf594-123">Zwiększyć sukces klientów przy użyciu operacji NuGet — [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="cf594-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cf594-124">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="cf594-124">Issues fixed in this release</span></span>

* <span data-ttu-id="cf594-125">Ostrzeżenia z podwyższonym poziomem uprawnień na błędy (za pośrednictwem WarnAsErrors), które zostały wygenerowane przez PackageExtraction nigdy nie należy pozostawić wyodrębniony pakiet wokół - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="cf594-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="cf594-126">Nieprawidłowo podpisanych pakietów nie powinna kończyć w folderze globalnymi pakietami - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="cf594-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="cf594-127">Powiązanie generowania przekierowania nie należy pomijać zestawy fasady - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="cf594-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="cf594-128">Jest równe VersionRange nie porównania zmiennoprzecinkowy zakresów — [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="cf594-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="cf594-129">Przywracanie: stos regresji wydajności przy użyciu protokołu HTTP nowej platformy .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="cf594-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="cf594-130">Aktualizacja pakietu nie należy modyfikować PrivateAssets PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="cf594-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="cf594-131">Podpisywanie: podpisywanie powinna zakończyć się niepowodzeniem Jeżeli pakiet zawiera zbyt wiele wpisów pakietu (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="cf594-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="cf594-132">prefiksu "dotnet nuget wypychania" powinien obsługiwać nowego dostawcę poświadczeń - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="cf594-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="cf594-133">Obsługuje wykonywanie wtyczek przy użyciu niezmiennej kultury (tak jak wykonywane na platformie docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="cf594-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="cf594-134">Dodaj źródła nuget, nie należy usuwać poświadczenia w pliku NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="cf594-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="cf594-135">Instalowanie devDependency PackageReference powinny domyślnie excludeassets = kompilacji - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="cf594-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="cf594-136">Usuń opcję migrator ma być wyświetlany dla wszystkich projektów i Pokaż błąd, jeśli projekt jest niezgodny - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="cf594-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="cf594-137">"dotnet Dodaj pakiet" powinien zużywać przywracania sprawdzi się w pliku zasobów - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="cf594-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="cf594-138">Podpisywanie: poprawa podpisywania pokrewne komunikaty o błędach - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="cf594-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="cf594-139">[Niepowodzenie testu] [zh-TW] Ciąg "Konsola Menedżera pakietów" nie zlokalizować w konsoli Menedżera pakietów - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="cf594-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="cf594-140">Komunikat o błędzie wokół "Nie można odnaleźć informacji o projekcie" powinna być nieco bardziej szczegółowe wewnątrz VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="cf594-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="cf594-141">Komunikat o błędzie zbędny, korzystając z niepoprawnie nuspec tag wersji pakietu nuget — [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="cf594-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="cf594-142">DCR - podpisywania: obsługują protokół NuGet: Zasób RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="cf594-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="cf594-143">DCR —. zostanie teraz utworzony plik nupkg.metadata podczas wyodrębniania pakietu - zawiera "zawartość hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="cf594-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="cf594-144">DCR - pomijania weryfikacji authenticode dla wtyczek podczas wykonywania w Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="cf594-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="cf594-145">Lista wszystkie problemy rozwiązane w tej wersji 4.9.0</span><span class="sxs-lookup"><span data-stu-id="cf594-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="cf594-146">Podsumowanie: What's New in 4.9.1</span><span class="sxs-lookup"><span data-stu-id="cf594-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="cf594-147">Dodano obsługę odczytu zapisu do pliku nuget.config, za pomocą nowego polecenia zaufanych — które podpisały - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="cf594-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cf594-148">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="cf594-148">Issues fixed in this release</span></span>

* <span data-ttu-id="cf594-149">Napraw Generowanie konsolidacji licencji - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="cf594-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="cf594-150">Kody błędów regresji do weryfikowania podpisów- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="cf594-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="cf594-151">Pakiet NuGet.Build.Tasks.Pack nie ma informacji o licencjach - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="cf594-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="cf594-152">Lista wszystkie problemy rozwiązane w tej wersji 4.9.1</span><span class="sxs-lookup"><span data-stu-id="cf594-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="cf594-153">Podsumowanie: What's New in 4.9.2</span><span class="sxs-lookup"><span data-stu-id="cf594-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cf594-154">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="cf594-154">Issues fixed in this release</span></span>

* <span data-ttu-id="cf594-155">VS/dotnet.exe/nuget.exe/msbuild.exe przywracania nie używa poświadczeń, gdy nazwa źródła zawiera odstępem - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="cf594-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="cf594-156">Problemy dotyczące LicenseAcceptanceWindow i dostępności LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="cf594-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="cf594-157">Usuń formatexception — na przykład DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="cf594-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="cf594-158">Lista wszystkie problemy rozwiązane w tej wersji 4.9.2</span><span class="sxs-lookup"><span data-stu-id="cf594-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="cf594-159">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="cf594-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="cf594-160">DotNet nuget push--interaktywne powoduje błąd na komputerze Mac.</span><span class="sxs-lookup"><span data-stu-id="cf594-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="cf594-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="cf594-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="cf594-162">Problem</span><span class="sxs-lookup"><span data-stu-id="cf594-162">Issue</span></span>
<span data-ttu-id="cf594-163">`--interactive` Argument nie są przekazywane przez interfejs wiersza polecenia platformy dotnet i powoduje błąd `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="cf594-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="cf594-164">Obejście</span><span class="sxs-lookup"><span data-stu-id="cf594-164">Workaround</span></span>
<span data-ttu-id="cf594-165">Aby możliwe było uruchamianie dowolnego polecenia dotnet z opcją interaktywnych, takich jak `dotnet restore --interactive` i uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="cf594-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="cf594-166">Uwierzytelnianie, program może być buforowane przez dostawcę poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="cf594-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="cf594-167">Następnie uruchom `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="cf594-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="cf594-168">Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="cf594-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="cf594-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="cf594-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="cf594-170">Problem</span><span class="sxs-lookup"><span data-stu-id="cf594-170">Issue</span></span>
<span data-ttu-id="cf594-171">Korzystając z dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych.</span><span class="sxs-lookup"><span data-stu-id="cf594-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="cf594-172">Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="cf594-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="cf594-173">Obejście</span><span class="sxs-lookup"><span data-stu-id="cf594-173">Workaround</span></span>
<span data-ttu-id="cf594-174">Wyłącz użycie folderu rezerwowy, ustawiając `RestoreAdditionalProjectSources` na wartość nothing.</span><span class="sxs-lookup"><span data-stu-id="cf594-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="cf594-175">`<RestoreAdditionalProjectSources/>` Korzystanie z rozwagą, ponieważ spowoduje to wiele pakietów, które mają być pobrane z repozytorium NuGet.org, które w przeciwnym razie byłoby zostały przywrócone z folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="cf594-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
