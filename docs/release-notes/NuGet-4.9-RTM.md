---
title: Informacje o wersji narzędzia NuGet 4,9 RTM
description: Informacje o wersji programu NuGet 4,9, w tym znane problemy, poprawki błędów, nowe funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780148"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="79279-103">Informacje o wersji narzędzia NuGet 4,9</span><span class="sxs-lookup"><span data-stu-id="79279-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="79279-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="79279-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="79279-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="79279-105">NuGet version</span></span> | <span data-ttu-id="79279-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79279-106">Available in Visual Studio version</span></span>| <span data-ttu-id="79279-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="79279-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="79279-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="79279-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="79279-109">Visual Studio 2017 w wersji 15.9.0</span><span class="sxs-lookup"><span data-stu-id="79279-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="79279-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="79279-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="79279-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="79279-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="79279-112">nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="79279-112">n/a</span></span> | <span data-ttu-id="79279-113">nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="79279-113">n/a</span></span> |
| [<span data-ttu-id="79279-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="79279-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="79279-115">Visual Studio 2017 w wersji 15.9.4</span><span class="sxs-lookup"><span data-stu-id="79279-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="79279-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="79279-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="79279-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="79279-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="79279-118">Visual Studio 2017 w wersji 15.9.6</span><span class="sxs-lookup"><span data-stu-id="79279-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="79279-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="79279-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="79279-120">Podsumowanie: co nowego w programie 4.9.0</span><span class="sxs-lookup"><span data-stu-id="79279-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="79279-121">Podpisywanie: Włącz ClientPolicies, aby wymagać użycia zestawu zaufanych autorów i repozytoriów wymienionych w NuGet.Config- [#6961](https://github.com/NuGet/Home/issues/6961), [wpis w blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="79279-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="79279-122">Utwórz pliki ". snupkg", aby zawierały symbole w pakiecie — ulepszanie wypychania, aby zrozumieć protokół NuGet, aby akceptować pliki snupkg dla serwera symboli — [#6878](https://github.com/NuGet/Home/issues/6878), [wpis w blogu](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="79279-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="79279-123">Wtyczka poświadczeń NuGet v2- [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="79279-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="79279-124">Self-Contained pakietów NuGet — licencja [#4628](https://github.com/NuGet/Home/issues/4628), [ogłoszenie](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="79279-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="79279-125">Włącz opcję "GeneratePathProperty" metadanych na PackageReference, aby wygenerować Właściwość programu MSBuild dla pakietu na "foo. Bar\1.0 \" Directory- [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="79279-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="79279-126">Popraw sukces klientów dzięki operacjom NuGet — [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="79279-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="79279-127">Włącz przywracanie Powtórzonego pakietu przy użyciu pliku blokady — [#5602](https://github.com/NuGet/Home/issues/5602), [ogłoszenie](https://github.com/NuGet/Announcements/issues/28), [wpis w blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="79279-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="79279-128">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="79279-128">Issues fixed in this release</span></span>

* <span data-ttu-id="79279-129">Ostrzeżenia z błędami (przez WarnAsErrors) wywoływane przez PackageExtraction nigdy nie powinny opuszczać wyodrębnionego pakietu [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="79279-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="79279-130">Nieprawidłowo podpisane pakiety nie powinny kończyć się w folderze pakietów globalnych — [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="79279-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="79279-131">Generowanie powiązania powiązań nie powinno pomijać zestawów elewacji — [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="79279-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="79279-132">VersionRange Equals nie porównują zakresów zmiennoprzecinkowych — [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="79279-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="79279-133">Przywracanie: regresja wydajności przy użyciu nowego stosu HTTP programu .NET Core 2,1 — [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="79279-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="79279-134">Aktualizacja pakietu nie powinna modyfikować PrivateAssets PackageReference- [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="79279-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="79279-135">Podpisywanie: podpisywanie powinno zakończyć się niepowodzeniem, jeśli pakiet ma zbyt wiele wpisów pakietów (>65534) — [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="79279-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="79279-136">"wypychanie NuGet" dotnet "prefiksu powinien obsługiwać nowego dostawcę poświadczeń — [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="79279-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="79279-137">Obsługa wykonywania wtyczek z niezmienną kulturą (w przypadku platformy Docker) — [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="79279-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="79279-138">Dodawanie źródeł NuGet nie powinno usuwać poświadczeń z NuGet.config- [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="79279-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="79279-139">Instalowanie devDependency PackageReference powinno domyślnie mieć wartość excludeassets = Kompiluj- [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="79279-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="79279-140">Napraw opcję Migrator, która ma być wyświetlana dla wszystkich projektów i Pokaż błąd, jeśli projekt jest niezgodny — [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="79279-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="79279-141">"do dodania pakietu dotnet" należy zatwierdzić przywracanie wykonywane do pliku zasobów — [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="79279-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="79279-142">Podpisywanie: ulepszanie podpisywania komunikatów o błędach — [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="79279-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="79279-143">[Niepowodzenie testu] [zh-TW] Ciąg "Konsola Menedżera pakietów" nie jest zlokalizowany w konsoli Menedżera pakietów — [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="79279-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="79279-144">Komunikat o błędzie "nie można znaleźć informacji o projekcie" powinien być nieco bardziej szczegółowy w programie VS- [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="79279-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="79279-145">Niepomocny komunikat o błędzie podczas nieprawidłowego używania tagu Version nuspec pakietu NuGet Pack — [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="79279-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="79279-146">Podpisywanie DCR: obsługa protokołu NuGet: RepositorySignatures/4.9.0 Resource- [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="79279-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="79279-147">Plik DCR-. nupkg. Metadata zostanie teraz utworzony podczas wyodrębniania pakietu — zawiera ciąg "Content-hash"- [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="79279-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="79279-148">DCR — Pomiń weryfikację Authenticode dla wtyczek podczas wykonywania na mono- [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="79279-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="79279-149">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.0</span><span class="sxs-lookup"><span data-stu-id="79279-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="79279-150">Podsumowanie: co nowego w programie 4.9.1</span><span class="sxs-lookup"><span data-stu-id="79279-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="79279-151">Dodaj obsługę odczytywania zapisu do nuget.config za pośrednictwem nowego polecenia zaufane osoby podpisujące — [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="79279-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="79279-152">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="79279-152">Issues fixed in this release</span></span>

* <span data-ttu-id="79279-153">Napraw Generowanie łącza licencji — [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="79279-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="79279-154">Regresja kodów błędów dla walidacji sygnatur — [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="79279-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="79279-155">Pakiet NuGet. Build. Tasks. Pack nie ma informacji o licencji — [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="79279-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="79279-156">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.1</span><span class="sxs-lookup"><span data-stu-id="79279-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="79279-157">Podsumowanie: co nowego w programie 4.9.2</span><span class="sxs-lookup"><span data-stu-id="79279-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="79279-158">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="79279-158">Issues fixed in this release</span></span>

* <span data-ttu-id="79279-159">Program VS/dotnet.exe/nuget.exe/msbuild.exe Restore nie używa poświadczeń, gdy nazwa źródła zawiera spację — [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="79279-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="79279-160">Problemy z ułatwieniami dostępu LicenseAcceptanceWindow i LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="79279-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="79279-161">Naprawianie FormatException w elemencie DateTime. Przeanalizuj z DateTimeConverter- [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="79279-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="79279-162">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.2</span><span class="sxs-lookup"><span data-stu-id="79279-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="79279-163">Podsumowanie: co nowego w programie 4.9.3</span><span class="sxs-lookup"><span data-stu-id="79279-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="79279-164">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="79279-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="79279-165">"Powtarzające się pakiety są przywracane przy użyciu pliku blokady"</span><span class="sxs-lookup"><span data-stu-id="79279-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="79279-166">Tryb zablokowany nie działa, ponieważ wartość skrótu jest obliczana niepoprawnie dla wcześniej buforowanych pakietów — [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="79279-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="79279-167">Przywracanie jest rozpoznawane jako inna wersja niż zdefiniowana w `packages.lock.json` [#7667](https://github.com/NuGet/Home/issues/7667) pliku</span><span class="sxs-lookup"><span data-stu-id="79279-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="79279-168">Tryb "--locked-Mode/RestoreLockedMode" powoduje błędy przywracania fałszywe, gdy [#7646](https://github.com/NuGet/Home/issues/7646) zawierających</span><span class="sxs-lookup"><span data-stu-id="79279-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="79279-169">Program rozpoznawania SDK programu MSBuild próbuje sprawdzić poprawność agenta SHA dla pakietu zestawu SDK, którego przywracanie nie powiodło się podczas korzystania z packages.lock.js[#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="79279-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="79279-170">Problemy "Zablokuj zależności przy użyciu konfigurowalnych zasad zaufania"</span><span class="sxs-lookup"><span data-stu-id="79279-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="79279-171">dotnet.exe nie należy szacować nadawców zaufanych, gdy podpisane pakiety nie są obsługiwane — [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="79279-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="79279-172">Kolejność trustedSigners w pliku konfiguracji ma wpływ na ocenę zaufania — [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="79279-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="79279-173">Nie można zaimplementować ISettings [spowodowane przez refaktoryzację ustawień interfejsów API do obsługi zasad zaufania]- [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="79279-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="79279-174">Problemy "Ulepszone środowisko debugowania"</span><span class="sxs-lookup"><span data-stu-id="79279-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="79279-175">Nie można opublikować pakietu symboli dla narzędzia globalnego platformy .NET Core — [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="79279-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="79279-176">"Problemy związane z własnymi pakietami NuGet — licencje"</span><span class="sxs-lookup"><span data-stu-id="79279-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="79279-177">Wystąpił błąd podczas kompilowania pakietu symboli. snupkg podczas korzystania z pliku licencji osadzonej — [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="79279-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="79279-178">Lista wszystkich problemów rozwiązanych w tej wersji 4.9.3</span><span class="sxs-lookup"><span data-stu-id="79279-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="79279-179">Podsumowanie: co nowego w programie 4.9.4</span><span class="sxs-lookup"><span data-stu-id="79279-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="79279-180">Poprawka zabezpieczeń: uprawnienia dla plików utworzonych wewnątrz ~/.NuGet są zbyt otwarte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="79279-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="79279-181">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="79279-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="79279-182">wypychanie NuGet programu dotnet — interaktywny błąd na komputerze Mac.</span><span class="sxs-lookup"><span data-stu-id="79279-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="79279-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="79279-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="79279-184">Problem</span><span class="sxs-lookup"><span data-stu-id="79279-184">Issue</span></span>
<span data-ttu-id="79279-185">`--interactive`Argument nie jest przesyłany dalej przez interfejs wiersza polecenia dotnet i powoduje błąd`error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="79279-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="79279-186">Obejście</span><span class="sxs-lookup"><span data-stu-id="79279-186">Workaround</span></span>
<span data-ttu-id="79279-187">Uruchom dowolne inne polecenie dotnet przy użyciu opcji Interactive, takiej jak `dotnet restore --interactive` i uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="79279-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="79279-188">Uwierzytelnianie może zostać zapisane w pamięci podręcznej przez dostawcę poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="79279-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="79279-189">Następnie należy uruchomić polecenie `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="79279-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="79279-190">Pakiety w FallbackFolders zainstalowane przez zestaw .NET Core SDK są zainstalowane niestandardowo i nie można zweryfikować podpisu.</span><span class="sxs-lookup"><span data-stu-id="79279-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="79279-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="79279-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="79279-192">Problem</span><span class="sxs-lookup"><span data-stu-id="79279-192">Issue</span></span>
<span data-ttu-id="79279-193">W przypadku korzystania z dotnet.exe 2. x w celu przywrócenia projektu, który ma wiele obiektów docelowych netcoreapp 1. x i netcoreapp 2. x, folder rezerwowy jest traktowany jako źródło plików.</span><span class="sxs-lookup"><span data-stu-id="79279-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="79279-194">Oznacza to, że podczas przywracania program NuGet wybierze pakiet z folderu rezerwowego i spróbuje go zainstalować w folderze pakiety globalne i wykonać zwykłą weryfikację podpisywania, która kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="79279-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="79279-195">Obejście</span><span class="sxs-lookup"><span data-stu-id="79279-195">Workaround</span></span>
<span data-ttu-id="79279-196">Wyłącz użycie folderu rezerwowego, ustawiając wartość `RestoreAdditionalProjectSources` Nothing.</span><span class="sxs-lookup"><span data-stu-id="79279-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="79279-197">`<RestoreAdditionalProjectSources/>` Należy to zrobić z ostrożnością, ponieważ spowoduje to pobranie wielu pakietów z NuGet.org, które w przeciwnym razie zostałyby przywrócone z folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="79279-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
