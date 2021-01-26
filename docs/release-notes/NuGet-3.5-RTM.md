---
title: Informacje o wersji narzędzia NuGet 3,5 RTM
description: Informacje o wersji programu NuGet 3,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776353"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="2eb3b-103">Informacje o wersji narzędzia NuGet 3,5</span><span class="sxs-lookup"><span data-stu-id="2eb3b-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="2eb3b-104">Pakiet [NuGet 3,5 — informacje](../release-notes/nuget-3.5-RC.md)  |  o wersji RC [Informacje o wersji narzędzia NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="2eb3b-105">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="2eb3b-105">Bug Fixes</span></span>

* <span data-ttu-id="2eb3b-106">Pakiet nie używa programu MSBuild 14,1 w programie mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="2eb3b-107">Na karcie aktualizacja nie jest wybrana najnowsza dostępna wersja, która ma zostać zaktualizowana, a zamiast tego wybierana jest bieżąca zainstalowana wersja — [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="2eb3b-108">Napraw awarię po uwierzytelnieniu prywatnego źródła danych w wersji 2 MyGet i kliknięciu pozycji "Pokaż x więcej wyników" — [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="2eb3b-109">Komunikaty dziennika pozornie są uporządkowane w kolejności odwrotnej dla interfejsu użytkownika [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="2eb3b-110">v 3.4.4 — Przywracanie NuGet zgłasza "format danego ścieżki nie jest obsługiwany"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="2eb3b-111">Pakiet NuGet Cmdlines 3,6 beta nie jest zgodny z konfiguracją = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="2eb3b-112">Powolna instalacja narzędzia NuGet IKVM na dużym projekcie — [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="2eb3b-113">nuget.exe Update — umożliwia samodzielną aktualizację [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="2eb3b-114">3,5 Zainstaluj/Przywróć z udziału UNC ma regresję wydajności z 3.4.4 — [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="2eb3b-115">Wystąpił błąd podczas instalowania MOQ z interfejsu użytkownika zarządzania pakietami dla projektu net451 — [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="2eb3b-116">Karta Instalacja na poziomie rozwiązania nie wyświetla wersji [#3339](https://github.com/NuGet/Home/issues/3339) pakietu</span><span class="sxs-lookup"><span data-stu-id="2eb3b-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="2eb3b-117">`project.json`Aktualizacja xproj z zainstalowanej karty traci stan- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="2eb3b-118">Pakiet NuGet w przypadku `.csproj` ignorowania pustego elementu Files w `.nuspec` pliku- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="2eb3b-119">Projekty witryn sieci Web hostowane w usługach IIS nie powinny spowodować niepowodzenia przywracania [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="2eb3b-120">Nie pobrano poświadczeń z Nuget.Config po przekierowaniu punktu końcowego v3 do wersji 2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="2eb3b-121">Pakiet NuGet nie może rozpoznać zestawu podczas pobierania metadanych zestawu przenośnego — [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="2eb3b-122">Pakiet NuGet nie może znaleźć `msbuild.exe` na mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="2eb3b-123">Pakiet nuget.exe nie zezwala na tag w wersji wstępnej zaczynający się od cyfr- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="2eb3b-124">Instalacja pakietu NuGet kończy się niepowodzeniem na VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="2eb3b-125">Filtr allowedVersions nie działa na poziomie rozwiązania — [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="2eb3b-126">Operacja przywracania losowo kończy się niepowodzeniem z elementem z tym samym kluczem, który został już dodany.</span><span class="sxs-lookup"><span data-stu-id="2eb3b-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="2eb3b-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="2eb3b-128">Nie można zainstalować NuGet. Common w `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="2eb3b-129">W przypadku używania interfejsu użytkownika do wyszukiwania źródła w wersji 2 FindPackagesById jest wywoływana dwa razy dla każdego identyfikatora — [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="2eb3b-130">Pakiety nie mogą zależeć od projektów — [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="2eb3b-131">Pakiet nuget.exe — wykluczenie jest udokumentowane, ale nie jest obsługiwane — [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="2eb3b-132">Problemy z komunikatami o błędach, gdy sekcja "contentFiles" `.nuspec` jest nieprawidłowa — [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="2eb3b-133">Wypychanie zawsze wysyła cały pakiet z uwierzytelnionymi źródłami pakietów — [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="2eb3b-134">Nie podano informacji podczas wywoływania nuget.exe Update \*. csproj, gdy projekt nie ma `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="2eb3b-135">`packages.config` instrukcja RESTORE nie ponawia próby dla kodów stanu 5xx ze źródeł v2 — [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="2eb3b-136">Podwójna kropka w pliku SRC `.nuspec` nie działa — [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="2eb3b-137">Przywracanie CoreCLR musi ignorować kanały informacyjne z szyfrowaniem [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="2eb3b-138">nuget.exe obsługi wypychania 403 — nieprawidłowo Monituj o poświadczenia — [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="2eb3b-139">Aktualizacja NuGet za pomocą Menedżera pakietów usuwa właściwości z `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="2eb3b-140">NuGet. PackageManagement. VisualStudio spróbuj załadować "NuGet. TeamFoundationServer14", ale nazwa biblioteki DLL została zmieniona na "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="2eb3b-141">Interfejs użytkownika Menedżera pakietów nie wyświetla nowo zaktualizowanej wersji — [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="2eb3b-142">Update-pakiet próbuje użyć PackageID, Version zamiast Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="2eb3b-143">CSPROJ przywracania NuGet powinien błąd, jeśli projekt nie korzysta z NuGet ( `packages.config` lub `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="2eb3b-144">Błąd TFS "[plik] nie został znaleziony w Twoim obszarze roboczym lub nie masz uprawnień dostępu do niego" podczas uaktualniania lub odinstalowywania, gdy rozwiązanie/projekt jest powiązane z kontrolą źródła TFS- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="2eb3b-145">pakiet aktualizacji nie pobiera zależności dla pakietów innych niż docelowe — [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="2eb3b-146">Nie ma możliwości ustawienia poziomu szczegółowości dzienników dla akcji interfejsu użytkownika Menedżera pakietów NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="2eb3b-147">Konfiguracja NuGet jest nieprawidłowa — VS 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="2eb3b-148">DefaultPushSource w `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="2eb3b-149">wydanie NuGet 3.4.3 — pobieranie wartości nie może mieć wartości null w kompilacji pakietu- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="2eb3b-150">Przywracanie nie używa przechowywanych poświadczeń z Nuget.Config dla źródeł danych VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="2eb3b-151">[dotnet restore] — ConfigFile jest względem projektu dir zamiast cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="2eb3b-152">Nadmierne alokacje w wersji comparsion Code- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="2eb3b-153">Wiele wystąpień nuget.exe próbuje zainstalować ten sam pakiet równolegle powoduje podwójny zapis [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="2eb3b-154">Informacje o zależnościach nie są buforowane dla operacji wieloprojektowych — [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="2eb3b-155">Zainstaluj i zaktualizuj pakiety pobierania bez sprawdzania folderu Packages First- [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="2eb3b-156">Jeśli lista źródeł pakietów jest pusta, nie można dodać źródła pakietu za pośrednictwem interfejsu użytkownika (NuGet 3.4. x) — [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="2eb3b-157">Błąd mylący podczas próby zainstalowania pakietu, który zależy od [#2594](https://github.com/NuGet/Home/issues/2594) fasad czasu projektowania</span><span class="sxs-lookup"><span data-stu-id="2eb3b-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="2eb3b-158">Instalowanie pakietu z konsoli pakietu Packagemanager z ustawieniem "All" powoduje tylko próbę pierwszego źródła — [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="2eb3b-159">Najnowsza wersja beta nie rozpakować ModernHttpClient — [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="2eb3b-160">PROGRAMU VS2015 awarię przy uruchamianiu przy użyciu wbudowanego narzędzia NuGetobject- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="2eb3b-161">Polecenie Update może być nieco bardziej pełne, jeśli poprosił o to...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="2eb3b-162">Program VSIX utworzony lokalnie powinien mieć te same biblioteki DLL i pliki co kompilacja elementu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2eb3b-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="2eb3b-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="2eb3b-164">Napraw ostrzeżenia o obniżeniu poziomu NuGet w [#2396](https://github.com/NuGet/Home/issues/2396) kompilacji</span><span class="sxs-lookup"><span data-stu-id="2eb3b-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="2eb3b-165">Niepowodzenie uwierzytelniania źródła pakietów (3 razy) jest blokowane w nieskończoność — [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="2eb3b-166">Zawartość pakietu nie jest przywracana poprawnie podczas instalowania pakietu z programu NuGet v 3.3 + ze źródła danych argument-nocache, gdy pakiet zawiera `.nupkg` pliki- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="2eb3b-167">Instalacja narzędzia NuGet ze wszystkimi źródłami pakietów, ale brakuje pakietu z 1 źródła, kończy się niepowodzeniem — [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="2eb3b-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + \* lt; &gt; c__DisplayClass_0 i &lt; &lt; addreference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="2eb3b-169">Zainstaluj bloki w przypadku niepowodzenia autoryzacji pojedynczego źródła — [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="2eb3b-170">`.nuspec` zakres wersji powinien przesłonić IncludeReferencedProjects wersji [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="2eb3b-171">Update-Package bardzo wolno — "próba zebrania informacji o zależnościach" — [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="2eb3b-172">Pakiet NuGet niewidzialnego obniżenia poziomu przy aktualizacji wsadowej — [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="2eb3b-173">nuget.exe Update odrzuca silną nazwę i atrybut prywatny zestawu.</span><span class="sxs-lookup"><span data-stu-id="2eb3b-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="2eb3b-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="2eb3b-175">Względna ścieżka pliku dla "DefaultPushSource" — [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="2eb3b-176">Optymalizowanie komunikatów o błędach programu rozpoznawania nazw — [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="2eb3b-177">pakiet aktualizacji w wersji v3 kończy się niepowodzeniem z pakietami spoza określonego źródła — [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="2eb3b-178">Używanie ścieżek względnych dla źródeł pakietów jest problematyczne do użycia- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="2eb3b-179">Brakująca zależność w NUPKG — plik wygenerowany z projektu, jeśli zależność pośrednia już istnieje o niższej wersji — [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="2eb3b-180">Usunięcie projektu powoduje zamknięcie odpowiedniego okna interfejsu użytkownika, ale zmiana nazwy projektu nie powoduje zmiany nazwy okna interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2eb3b-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="2eb3b-181">Należy zauważyć, że PMC nasłuchuje w celu zmiany nazwy projektu i zdarzeń usunięcia projektu — [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="2eb3b-182">[Willow obciążenia sieci Web] Tworzenie zawieszeń z aparatu Razor v3 — [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="2eb3b-183">Instalacja/przywracanie określonego pakietu kończy się niepowodzeniem z "pakiet zawiera wiele plików nuspec".</span><span class="sxs-lookup"><span data-stu-id="2eb3b-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="2eb3b-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="2eb3b-185">Małe identyfikatory & `packages.config` scenariusze — [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="2eb3b-186">[3,5-beta2] Przywracanie pakietu nie może przywrócić "starszych" pakietów — [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="2eb3b-187">Pakiet NuGet wymusza dodanie plików TT do folderu Content niezależnie od tego, co [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="2eb3b-188">Funkcja Update-Package programu ASP.NET Web App generuje ostrzeżenie związane z plikiem: Source- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="2eb3b-189">Pakiet NuGet csproj (z `project.json` ) ulega awarii, jeśli nie ma packOptions i właściciela w pliku JSON — [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="2eb3b-190">Pakiet NuGet dla `project.json` ignorowania tagów packOptions, takich jak podsumowanie, autorzy, właściciele itp., [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="2eb3b-191">NullReferenceException za pośrednictwem NuGet. pakowanie. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="2eb3b-192">Pakiet NuGet ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="2eb3b-193">Aktualizacja wielu pakietów z wycofywaniem pozostawia projekt w stanie przerwania — [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="2eb3b-194">ContentFiles w obszarze any nie są dodawane do projektów standardowych, [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="2eb3b-195">Nie można prawidłowo spakować biblioteki dla platformy .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="2eb3b-196">Plik > nowy projekt — > Biblioteka klas (przenośna) kończy się niepowodzeniem w programu VS2015 i Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="2eb3b-197">błąd nuGet-1.0.0-\* nie jest prawidłowym ciągiem wersji- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="2eb3b-198">Nie można wyświetlić Find-Package, ale Install-Package działa [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="2eb3b-199">Błąd podczas "Install-Package jQuery. Validation" w dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="2eb3b-200">Pakiet NuGet xproj ma domyślnie wartość nieprawidłowa ścieżka docelowa — [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="2eb3b-201">Po zainstalowaniu programu VS 2015 Update 3 w programie VS, który korzysta z 3.5.0 w wersji NuGet, występuje błąd- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="2eb3b-202">"Zablokowane przez packages.config" w `project.json` (platformy UWP, a. k. a kompilacja zintegrowana) projekt — [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="2eb3b-203">Zaktualizuj interfejs wiersza polecenia dotnet instalowany przez skrypt kompilacji do preview2-003121, który jest oficjalną kompilacją preview2.</span><span class="sxs-lookup"><span data-stu-id="2eb3b-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="2eb3b-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="2eb3b-205">Interfejs użytkownika Menedżera pakietów: nie wyświetla nowej wersji po zaktualizowaniu pakietu — [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="2eb3b-206">-ApiKey w wierszu polecenia usuwania nie jest odczytywany/wysyłany w 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="2eb3b-207">Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć w zależności od wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="2eb3b-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="2eb3b-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="2eb3b-209">Pamięć podręczna OptimizedZipPackage pozostawia puste foldery — [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="2eb3b-210">Tworzenie wyjątku NullRef w projekcie PCL (net46 i Windows 10).</span><span class="sxs-lookup"><span data-stu-id="2eb3b-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="2eb3b-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="2eb3b-212">Aktualizacja NuGet powinna podawać komunikat informacyjny, gdy wyższa wersja jest ograniczona przez ograniczenie allowedVersions — [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="2eb3b-213">Problemy z przywracaniem NuGet v3 — [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="2eb3b-214">Wtyczka poświadczeń została zakończona z błędem-1/Pobieranie pakietu podczas korzystania z dostawców poświadczeń z wieloma źródłami — [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="2eb3b-215">`project.json` Przywracanie NuGet powoduje ponowną kompilację, gdy nic się nie zmieniło — [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="2eb3b-216">Pakiety symboli nie powinny być używane w instalacji ani aktualizacji- [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="2eb3b-217">Program VS nie obsługuje zmiennych środowiskowych w programie repositoryPath (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="2eb3b-218">Oznacz nieoznaczone elementy UIElement w interfejsie użytkownika Menedżera pakietów na potrzeby ułatwień dostępu [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="2eb3b-219">Platformy przenośne z zadzielonymi profilami są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="2eb3b-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="2eb3b-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="2eb3b-221">Menedżer pakietów NuGet powinien wyczyścić, że lista opcji w szczegółach pakietów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="2eb3b-222">nuget.exe push/Delete nie będzie używać klucza interfejsu API [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="2eb3b-223">Usuń zablokowaną właściwość z pliku blokady — [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="2eb3b-224">Aktualizacja NuGet 3.3.0 kończy się niepowodzeniem z "dodatkowym ograniczeniem... zdefiniowane w packages.config uniemożliwia wykonanie tej operacji ".</span><span class="sxs-lookup"><span data-stu-id="2eb3b-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="2eb3b-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="2eb3b-226">Instalowanie pakietu z lokalnego źródła, które nie istnieje, zgłasza fałszywe wiadomości [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="2eb3b-227">Filtr "dostępne uaktualnienie" zawiera uaktualnienia, które naruszają ograniczenie wersji — [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="2eb3b-228">Nie można zaktualizować pakietów natywnych — [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="2eb3b-229">Funkcje</span><span class="sxs-lookup"><span data-stu-id="2eb3b-229">Features</span></span>

* <span data-ttu-id="2eb3b-230">Obsługa ustawienia CopyLocal na wartość false w odwołaniach dodanych przez NuGet- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="2eb3b-231">nuget.exe obsługa programu MSBuild 15 — [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="2eb3b-232">Obsługa pakietu dla programu.`csproj`</span><span class="sxs-lookup"><span data-stu-id="2eb3b-232">Pack support for .`csproj`</span></span><span data-ttu-id="2eb3b-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="2eb3b-234">Wyłącz akcję użytkownika, gdy są wykonywane akcje użytkownika — [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="2eb3b-235">Pakiet NuGet powinien dodać obsługę `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="2eb3b-236">W programie NuGet 2. x brakuje niezgodności struktur, które znajdują się już w 3. x) — [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="2eb3b-237">Obsługa folderów pakietów powrotu — [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="2eb3b-238">Projektuj i Implementuj pojęcie typu pakietu do obsługi pakietów narzędzi — [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="2eb3b-239">Dodaj interfejs API, aby uzyskać ścieżkę do folderu pakietów globalnych — [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="2eb3b-240">Włączanie SemVer 2.0.0 w pakiecie Pack- [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="2eb3b-241">DCR</span><span class="sxs-lookup"><span data-stu-id="2eb3b-241">DCRs</span></span>

* <span data-ttu-id="2eb3b-242">nuget.exe parametr limitu czasu wypychania nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="2eb3b-243">Tekst opisu pakietu powinien być wybrany- [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="2eb3b-244">Włącz nuget.exe do produkcji `.props` i `.targets` plików dla `.nuproj` projektów [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="2eb3b-245">Dodawanie interfejsu API rozszerzalności do porównywania platform z importami — [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="2eb3b-246">Ukryj Opcje zależności przy użyciu `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="2eb3b-247">Drukuj nagłówek nuget.exe wersji w szczegółowych danych wyjściowych — [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="2eb3b-248">Pakiet NuGet musi poinformować użytkowników, że uaktualnianie/Instalowanie w formacie PCL opartym na platformie dotnet TFM może powodować problemy — [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="2eb3b-249">Ostrzegaj o złej instalacji/uaktualnieniu dla projektu w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="2eb3b-250">Rozwiązywanie problemów z wydajnością za pomocą Przekształć i narzędzia NuGet na potrzeby aktualizacji [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="2eb3b-251">Dodawanie obsługi netcoreapp11 i netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="2eb3b-252">Wykorzystanie atrybutu AssemblyMetadata dla `.nuspec` zamiany tokenów — [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="2eb3b-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
