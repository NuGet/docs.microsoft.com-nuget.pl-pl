---
title: Informacje o wersji 4.9 RTM NuGet
description: Informacje o wersji programu NuGet 4.9 łącznie znane problemy, poprawki, nowe funkcje i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453807"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="f4c03-103">4.9 wersji NuGet</span><span class="sxs-lookup"><span data-stu-id="f4c03-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="f4c03-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) jest dostarczany z NuGet 4.9.0 funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4c03-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="f4c03-105">Dostępne są wersje wiersza polecenia funkcji:</span><span class="sxs-lookup"><span data-stu-id="f4c03-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="f4c03-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="f4c03-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="f4c03-107">DotNet.exe - [platformy .NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="f4c03-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="f4c03-108">Podsumowanie: What's New in 4.9.0</span><span class="sxs-lookup"><span data-stu-id="f4c03-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="f4c03-109">Podpisywanie: Włącz ClientPolicies wymagać korzystanie z zestawu zaufanych autorzy i repozytoriów, wymienione w pliku NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="f4c03-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="f4c03-110">Tworzenie plików ".snupkg" zawierają symbole w pakiecie — Zwiększ wypchnięcie, aby zrozumieć nuget protokołu do akceptowania plików snupkg do serwera symboli - [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="f4c03-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="f4c03-111">Wtyczka poświadczeń NuGet w wersji 2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="f4c03-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="f4c03-112">-License - pakietów programu NuGet niezależna [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="f4c03-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="f4c03-113">Włącz zoptymalizowany pod kątem w metadanych "GeneratePathProperty" na PackageReference do wygenerowania dla właściwości MSBuild pakietu na "Foo.Bar\1.0\" katalogu — [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="f4c03-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="f4c03-114">Zwiększyć sukces klientów przy użyciu operacji NuGet — [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="f4c03-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f4c03-115">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="f4c03-115">Issues fixed in this release</span></span>

* <span data-ttu-id="f4c03-116">Ostrzeżenia z podwyższonym poziomem uprawnień na błędy (za pośrednictwem WarnAsErrors), które zostały wygenerowane przez PackageExtraction nigdy nie należy pozostawić wyodrębniony pakiet wokół - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="f4c03-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="f4c03-117">Nieprawidłowo podpisanych pakietów nie powinna kończyć w folderze globalnymi pakietami - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="f4c03-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="f4c03-118">Powiązanie generowania przekierowania nie należy pomijać zestawy fasady - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="f4c03-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="f4c03-119">Jest równe VersionRange nie porównania zmiennoprzecinkowy zakresów — [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="f4c03-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="f4c03-120">Przywracanie: stos regresji wydajności przy użyciu protokołu HTTP nowej platformy .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="f4c03-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="f4c03-121">Aktualizacja pakietu nie należy modyfikować PrivateAssets PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="f4c03-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="f4c03-122">Podpisywanie: podpisywanie powinna zakończyć się niepowodzeniem Jeżeli pakiet zawiera zbyt wiele wpisów pakietu (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="f4c03-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="f4c03-123">prefiksu "dotnet nuget wypychania" powinien obsługiwać nowego dostawcę poświadczeń - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="f4c03-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="f4c03-124">Obsługuje wykonywanie wtyczek przy użyciu niezmiennej kultury (tak jak wykonywane na platformie docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="f4c03-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="f4c03-125">Dodaj źródła nuget, nie należy usuwać poświadczenia w pliku NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="f4c03-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="f4c03-126">Instalowanie devDependency PackageReference powinny domyślnie excludeassets = kompilacji - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="f4c03-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="f4c03-127">Usuń opcję migrator ma być wyświetlany dla wszystkich projektów i Pokaż błąd, jeśli projekt jest niezgodny - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="f4c03-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="f4c03-128">"dotnet Dodaj pakiet" powinien zużywać przywracania sprawdzi się w pliku zasobów - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="f4c03-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="f4c03-129">Podpisywanie: poprawa podpisywania pokrewne komunikaty o błędach - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="f4c03-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="f4c03-130">[Niepowodzenie testu] [zh-TW] Ciąg "Konsola Menedżera pakietów" nie zlokalizować w konsoli Menedżera pakietów - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="f4c03-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="f4c03-131">Komunikat o błędzie wokół "Nie można odnaleźć informacji o projekcie" powinna być nieco bardziej szczegółowe wewnątrz VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="f4c03-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="f4c03-132">Komunikat o błędzie zbędny, korzystając z niepoprawnie nuspec tag wersji pakietu nuget — [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="f4c03-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="f4c03-133">DCR - podpisywania: obsługują protokół NuGet: zasób RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="f4c03-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="f4c03-134">DCR —. zostanie teraz utworzony plik nupkg.metadata podczas wyodrębniania pakietu - zawiera "zawartość hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="f4c03-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="f4c03-135">DCR - pomijania weryfikacji authenticode dla wtyczek podczas wykonywania w Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="f4c03-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="f4c03-136">Lista wszystkie problemy rozwiązane w tej wersji 4.9.0</span><span class="sxs-lookup"><span data-stu-id="f4c03-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="f4c03-137">Podsumowanie: What's New in 4.9.1</span><span class="sxs-lookup"><span data-stu-id="f4c03-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="f4c03-138">Dodano obsługę odczytu zapisu do pliku nuget.config, za pomocą nowego polecenia zaufanych — które podpisały - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="f4c03-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f4c03-139">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="f4c03-139">Issues fixed in this release</span></span>

* <span data-ttu-id="f4c03-140">Napraw Generowanie konsolidacji licencji - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="f4c03-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="f4c03-141">Kody błędów regresji do weryfikowania podpisów- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="f4c03-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="f4c03-142">Pakiet NuGet.Build.Tasks.Pack nie ma informacji o licencjach - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="f4c03-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="f4c03-143">Lista wszystkie problemy rozwiązane w tej wersji 4.9.1</span><span class="sxs-lookup"><span data-stu-id="f4c03-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="f4c03-144">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="f4c03-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="f4c03-145">DotNet.exe/nuget.exe nie używa poświadczeń, gdy nazwa źródła zawiera odstępem - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="f4c03-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="f4c03-146">Problem</span><span class="sxs-lookup"><span data-stu-id="f4c03-146">Issue</span></span>
<span data-ttu-id="f4c03-147">Jeśli nazwa źródła jest odstępem, nuget.exe zgłasza błąd, taki jak `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span><span class="sxs-lookup"><span data-stu-id="f4c03-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="f4c03-148">Obejście</span><span class="sxs-lookup"><span data-stu-id="f4c03-148">Workaround</span></span>
<span data-ttu-id="f4c03-149">Zmień nazwę źródła, które ma nie zawierać białych znaków.</span><span class="sxs-lookup"><span data-stu-id="f4c03-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="f4c03-150">DotNet nuget push--interaktywne powoduje błąd na komputerze Mac.</span><span class="sxs-lookup"><span data-stu-id="f4c03-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="f4c03-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="f4c03-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="f4c03-152">Problem</span><span class="sxs-lookup"><span data-stu-id="f4c03-152">Issue</span></span>
<span data-ttu-id="f4c03-153">`--interactive` Argument nie są przekazywane przez interfejs wiersza polecenia platformy dotnet i powoduje błąd `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="f4c03-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="f4c03-154">Obejście</span><span class="sxs-lookup"><span data-stu-id="f4c03-154">Workaround</span></span>
<span data-ttu-id="f4c03-155">Aby możliwe było uruchamianie dowolnego polecenia dotnet z opcją interaktywnych, takich jak `dotnet restore --interactive` i uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f4c03-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="f4c03-156">Uwierzytelnianie, program może być buforowane przez dostawcę poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="f4c03-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="f4c03-157">Następnie uruchom `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f4c03-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="f4c03-158">Problemy dotyczące LicenseAcceptanceWindow i dostępności LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="f4c03-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="f4c03-159">Problem</span><span class="sxs-lookup"><span data-stu-id="f4c03-159">Issue</span></span>
<span data-ttu-id="f4c03-160">Okno akceptacja licencji i okno pliku licencji ma problemy ułatwień dostępu za pomocą klawiatury i narracji przy użyciu czytnika zawartości ekranu i JAWS.</span><span class="sxs-lookup"><span data-stu-id="f4c03-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="f4c03-161">Obejście</span><span class="sxs-lookup"><span data-stu-id="f4c03-161">Workaround</span></span>
<span data-ttu-id="f4c03-162">Brak obejścia.</span><span class="sxs-lookup"><span data-stu-id="f4c03-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="f4c03-163">Pakiety w FallbackFolders instalowane przez zestaw .NET Core SDK są zainstalowane niestandardowe i wystąpi niepowodzenie weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="f4c03-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="f4c03-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="f4c03-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="f4c03-165">Problem</span><span class="sxs-lookup"><span data-stu-id="f4c03-165">Issue</span></span>
<span data-ttu-id="f4c03-166">Korzystając z dotnet.exe 2.x można przywrócić tego netcoreapp wiele elementów docelowych projektu 1.x i netcoreapp 2.x, rezerwowy folderu jest traktowany jako plik źródła danych.</span><span class="sxs-lookup"><span data-stu-id="f4c03-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="f4c03-167">Oznacza to, podczas przywracania, NuGet spowoduje pobranie pakietu z rezerwowego folderu i spróbuj zainstalować go w folderze globalnymi pakietami i są zwykle podpisywania sprawdzania poprawności, który kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="f4c03-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="f4c03-168">Obejście</span><span class="sxs-lookup"><span data-stu-id="f4c03-168">Workaround</span></span>
<span data-ttu-id="f4c03-169">Wyłącz użycie folderu rezerwowy, ustawiając `RestoreAdditionalProjectSources` na wartość nothing.</span><span class="sxs-lookup"><span data-stu-id="f4c03-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="f4c03-170">`<RestoreAdditionalProjectSources/>` Korzystanie z rozwagą, ponieważ spowoduje to wiele pakietów, które mają być pobrane z repozytorium NuGet.org, które w przeciwnym razie byłoby zostały przywrócone z folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="f4c03-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
