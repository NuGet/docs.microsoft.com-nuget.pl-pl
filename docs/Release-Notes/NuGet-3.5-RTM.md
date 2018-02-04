---
title: Informacje o wersji Beta NuGet 3.5 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.5 tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.5 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ee78ceb2ff032c05c0f8ef9a6623b94cc56ee0a9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="952b2-104">Informacje o wersji 3.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="952b2-104">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="952b2-105">[Informacje o wersji 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [— informacje o wersji RC NuGet 4.0](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="952b2-105">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="952b2-106">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="952b2-106">Bug Fixes</span></span>

* <span data-ttu-id="952b2-107">Pakiet nie używa MSBuild 14.1 na mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="952b2-107">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="952b2-108">Aktualizacja nie wybierz pozycję najnowszej dostępnej wersji aktualizacji zamiast tego zaznacz bieżące zainstalowanej wersji — [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="952b2-108">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="952b2-109">Usuń awarii po prywatnej v2, MyGet źródła danych uwierzytelniania i kliknięcie przycisku "Pokaż x więcej wyników"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="952b2-109">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="952b2-110">Komunikaty dziennika wydają się być w kolejności odwrotnej do interfejsu użytkownika — [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="952b2-110">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="952b2-111">Przywracanie Nuget v3.4.4 - zgłasza "format podanej ścieżki nie jest obsługiwany" - [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="952b2-111">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="952b2-112">CmdLine 3,6 NuGet w wersji beta nie honoruje - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="952b2-112">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="952b2-113">Powolne IKVM Nuget zainstalować na dużych projekt — [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="952b2-113">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="952b2-114">nuget.exe Update - Self przechowuje na aktualizowanie sam — [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="952b2-114">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="952b2-115">3.5 instalacji/przywracania z udziału UNC ma wydajności regresji z 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="952b2-115">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="952b2-116">Błąd podczas instalowania Moq z interfejs zarządzania pakietami dla projektu net451 - [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="952b2-116">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="952b2-117">Karta instalacji na poziomie rozwiązania nie wyświetla wersję pakietu - [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="952b2-117">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="952b2-118">xproj `project.json` aktualizacji z karty zainstalowana utraci stan — [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="952b2-118">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="952b2-119">Pakiet NuGet w `.csproj` ignoruje element pustych plików w `.nuspec` pliku - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="952b2-119">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="952b2-120">Projektów witryny sieci Web hostowanych w usługach IIS nie powinno powodować niepowodzenie — po ukończeniu przywracania [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="952b2-120">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="952b2-121">Poświadczenia nie są pobierane z pliku Nuget.Config, gdy punkt końcowy v3 przekierowuje do v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="952b2-121">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="952b2-122">Pakiet NuGet nie może rozpoznać zestawu podczas pobierania metadanych zestawu przenośnych - [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="952b2-122">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="952b2-123">Nie można odnaleźć Nuget `msbuild.exe` na Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="952b2-123">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="952b2-124">Pakiet nuget.exe nie zezwala na tagu wersji wstępnej, który rozpoczyna się od cyfry - [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="952b2-124">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="952b2-125">Instalacja pakietu nuget nie powiodło się na VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="952b2-125">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="952b2-126">allowedVersions filtru nie pracy na poziomie rozwiązania - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="952b2-126">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="952b2-127">Przywracanie losowo kończy się niepowodzeniem z element o takim samym kluczem został już dodany.</span><span class="sxs-lookup"><span data-stu-id="952b2-127">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="952b2-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="952b2-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="952b2-129">Nie można zainstalować Nuget.Common w `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="952b2-129">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="952b2-130">Wyszukaj źródło V2 za pomocą interfejsu użytkownika, FindPackagesById jest wywoływana dwukrotnie dla każdego Identyfikatora - [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="952b2-130">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="952b2-131">Pakiety nie może zależeć od projektów - [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="952b2-131">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="952b2-132">Pakiet nuget.exe — Wyklucz jest udokumentowany, ale nie jest obsługiwana — [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="952b2-132">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="952b2-133">Problemy z powodu błędu wiadomości, gdy sekcję "pliki" `.nuspec` jest nieprawidłowy — [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="952b2-133">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="952b2-134">Wypychania zawsze wysyła cały pakiet dwa razy z uwierzytelniony źródła pakietów - [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="952b2-134">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="952b2-135">Żadne informacje nie podano, gdy wywoływanie nuget.exe \*.csproj aktualizacji podczas projektu nie ma `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="952b2-135">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="952b2-136">`packages.config`Przywracanie nie ponów 5xx kodów stanu ze źródeł V2 - [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="952b2-136">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="952b2-137">Dwie kropki w pliku src w `.nuspec` nie działa — [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="952b2-137">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="952b2-138">Przywracanie środowisko CoreCLR musi Ignoruj źródła danych za pomocą szyfrowania - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="952b2-138">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="952b2-139">nuget.exe push Obsługa 403 - niepoprawnie monit o podanie poświadczeń — [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="952b2-139">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="952b2-140">Aktualizacja NuGet za pomocą Menedżera pakietów usuwa właściwości z `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="952b2-140">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="952b2-141">NuGet.PackageManagement.VisualStudio spróbuj załadować "NuGet.TeamFoundationServer14", ale zmiana nazwy biblioteki DLL "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="952b2-141">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="952b2-142">Menedżer pakietów interfejsu użytkownika nie wyświetla nowo zaktualizowanej wersji - [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="952b2-142">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="952b2-143">pakiet aktualizacji próby użycia pakietu, wersji, zamiast package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="952b2-143">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="952b2-144">nuget Przywracanie csproj powinien błąd Jeśli projekt nie jest przy użyciu narzędzia nuget (`packages.config` lub `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="952b2-144">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="952b2-145">Błąd TFS "[plik] nie można znaleźć w obszarze roboczym lub nie masz uprawnień dostępu do niego" podczas uaktualniania lub odinstalowywania, gdy rozwiązanie lub projekt jest powiązany z kontrolą źródła TFS - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="952b2-145">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="952b2-146">pakiet aktualizacji nie uzyskać zależności pakietów niebędące - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="952b2-146">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="952b2-147">Nie istnieje sposób ustawić poziom szczegółowości dzienniki dla akcji interfejsu użytkownika Menedżera pakietów Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="952b2-147">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="952b2-148">Konfiguracja nuget projektu jest nieprawidłowy — VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="952b2-148">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="952b2-149">DefaultPushSource w `NuGetDefaults.Config` (`ProgramData\NuGet`) nie działa — [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="952b2-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="952b2-150">Wersja nuget 3.4.3 - pobieranie wartości nie może być pusty podczas kompilacji pakietu — [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="952b2-150">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="952b2-151">Przywracanie nie używa przechowywanych poświadczeń z pliku Nuget.Config dla źródła danych programu VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="952b2-151">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="952b2-152">[dotnet przywracania] — configfile jest względem katalogu projektu zamiast cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="952b2-152">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="952b2-153">Nadmierne alokacji w kodzie porównania wersji — [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="952b2-153">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="952b2-154">Wiele wystąpień nuget.exe spróbujesz zainstalować takie same pakietu w równoległych przyczyny zapisu podwójny - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="952b2-154">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="952b2-155">Informacje o zależnościach nie są buforowane dla wielu projektów operacji - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="952b2-155">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="952b2-156">Instalowanie i pobierania pakietów aktualizacji bez sprawdzania folderu pakietów najpierw - [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="952b2-156">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="952b2-157">Jeśli lista źródła pakietu jest pusta, nie można dodać źródła pakietu za pośrednictwem interfejsu użytkownika (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="952b2-157">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="952b2-158">Błąd błąd podczas próby zainstalowania pakietu, który jest zależny od czasu projektowania fasad - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="952b2-158">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="952b2-159">Instalowanie pakietu z konsoli PackageManager, ustawienie "All" próbuje tylko pierwsze źródło - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="952b2-159">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="952b2-160">Najnowszej wersji beta nie rozpakować ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="952b2-160">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="952b2-161">VS2015 awarii podczas uruchamiania komputera z własnym wbudowanych NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="952b2-161">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="952b2-162">Polecenie aktualizacji może być bardziej pełne i poproś go jako operacji.. - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="952b2-162">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="952b2-163">Utworzony lokalnie VSIX powinny mieć te same biblioteki dll i plików jako elementu konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="952b2-163">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="952b2-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="952b2-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="952b2-165">Usuń NuGet obniżenia poziomu ostrzeżenia w kompilacji - [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="952b2-165">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="952b2-166">Nieudanych uwierzytelnień źródła pakietu (3 razy) jest zablokowana w nieskończoność - [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="952b2-166">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="952b2-167">Zawartość pakietu jest nie została poprawnie przywrócona podczas instalowania pakietu z v3.3 nuget + źródła danych z argumentem - NoCache, jeśli pakiet zawiera `.nupkg` pliki - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="952b2-167">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="952b2-168">Nuget Install wszystkie źródła pakietów, ale brakuje 1 źródła pakietu nie powiodło się — [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="952b2-168">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="952b2-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="952b2-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="952b2-170">Zainstaluj bloków, jeśli pojedyncze źródło odmawia autoryzacji - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="952b2-170">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="952b2-171">`.nuspec`Wersja zakresu powinny zastępować wersja - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="952b2-171">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="952b2-172">Pakiet aktualizacji super powolna — "Próba zebrania informacji zależności" - [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="952b2-172">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="952b2-173">Zmiany na NuGet ukrywana starszą wersję pakietu, gdy partii aktualizowanie zależnościami - [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="952b2-173">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="952b2-174">Aktualizacja nuget.exe porzuca silna nazwa zestawu i atrybut Private.</span><span class="sxs-lookup"><span data-stu-id="952b2-174">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="952b2-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="952b2-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="952b2-176">Względna ścieżka do pliku dla "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="952b2-176">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="952b2-177">Poprawa komunikaty o błędach rozpoznawania — [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="952b2-177">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="952b2-178">pakiet aktualizacji w wersji 3 nie powiedzie się z pakietami nie znajduje się w określonym źródle - [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="952b2-178">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="952b2-179">Używanie ścieżek względnych dla źródła pakietu jest pozwala używać - [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="952b2-179">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="952b2-180">Brak zależności w pliku NUPKG generowane z projektu, jeśli istnieje już pośrednią zależność związaną z niższe wymagania dotyczące wersji - [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="952b2-180">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="952b2-181">Usuwanie projektu zamyka odpowiedniego okna interfejsu użytkownika, ale zmiana nazwy projektu nie powoduje zmiany nazwy okna interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="952b2-181">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="952b2-182">Należy pamiętać, że PMC nasłuchuje do zmiany nazwy projektu i projektu zdarzenia remove - [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="952b2-182">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="952b2-183">[Willow obciążenia sieci Web] Tworzenie Razor v3 WSP zawiesza się - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="952b2-183">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="952b2-184">Instalacja/przywracania określonego pakietu nie powiodło się "Pakiet zawiera wiele plików nuspec."</span><span class="sxs-lookup"><span data-stu-id="952b2-184">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="952b2-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="952b2-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="952b2-186">Małe litery identyfikatory & `packages.config` scenariusze - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="952b2-186">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="952b2-187">[3.5 beta2] Przywracanie pakietu nie powiedzie się pod kątem przywracania pakietów "starszych" - [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="952b2-187">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="952b2-188">Pakiet nuget dodaje wymuszone .TT — pliki do folderu zawartości bez względu na okoliczności - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="952b2-188">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="952b2-189">pakiet aktualizacji aplikacji sieci web ASP.NET generuje ostrzeżenie związane z pliku: źródło - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="952b2-189">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="952b2-190">csproj pakiet nuget (z `project.json`) ulega awarii, jeśli istnieją nie packOptions i właściciel w pliku JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="952b2-190">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="952b2-191">Pakiet nuget `project.json` ignoruje tagi packOptions podsumowanie, autorzy, właściciele itp - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="952b2-191">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="952b2-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="952b2-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="952b2-193">Pakiet NuGet ignoruje zależności w danych wyjściowych `.nuspec` dla `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="952b2-193">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="952b2-194">Aktualizowania wielu pakietów z wycofywania pozostawia projektu w stan przerwane — [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="952b2-194">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="952b2-195">Nie dodano pliki we wszystkich projektów krótkich nazw netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="952b2-195">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="952b2-196">Nie można spakować biblioteki przeznaczonych dla platformy .net Standard poprawnie - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="952b2-196">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="952b2-197">Plik -> Nowy Projekt -> projektu biblioteki klas (przenośna) kończy się niepowodzeniem w programie VS2015 i Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="952b2-197">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="952b2-198">Błąd nuGet — 1.0.0-\* nie jest prawidłowym ciągiem wersji - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="952b2-198">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="952b2-199">Znajdź pakietu nie powiedzie się do wyświetlania, ale działa Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="952b2-199">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="952b2-200">Błąd podczas "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="952b2-200">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="952b2-201">Domyślnie pakiet nuget xproj ścieżkę docelową nieprawidłowy - [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="952b2-201">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="952b2-202">Gdy zainstalowanej wersji programu VS 2015 Aktualizacja 3 w wersji programu VS używane NuGet występuje błąd wersji 3.5.0 — [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="952b2-202">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="952b2-203">"Zablokowany w pliku packages.config" `project.json` (platformy uniwersalnej systemu Windows, nazywane również kompilacji zintegrowany) projektu - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="952b2-203">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="952b2-204">Zaktualizuj dotnet zainstalowane za pomocą skryptu kompilacji do preview2-003121, czyli kompilacji oficjalnego preview2 interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="952b2-204">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="952b2-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="952b2-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="952b2-206">Pakiet interfejsu użytkownika Menedżera: nie są wyświetlane po zaktualizowaniu pakietu nowej wersji — [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="952b2-206">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="952b2-207">-ApiKey w wierszu polecenia delete nie odczytu/wysyłane 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="952b2-207">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="952b2-208">Niepoprawny ciąg: stabilna wersja pakietu nie powinna mieć na zależność wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="952b2-208">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="952b2-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="952b2-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="952b2-210">Pamięć podręczna OptimizedZipPackage pozostawia puste foldery - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="952b2-210">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="952b2-211">Tworzenie PCL (net46 i windows 10) projektu get NullRef wyjątku.</span><span class="sxs-lookup"><span data-stu-id="952b2-211">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="952b2-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="952b2-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="952b2-213">Aktualizacja Nuget należy podać komunikat informacyjny w przypadku nowszej wersji jest ograniczony przez ograniczenie allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="952b2-213">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="952b2-214">Problemy dotyczące przywracania v3 Nuget — [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="952b2-214">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="952b2-215">Dodatek poświadczeń został zakończony z powodu błędu -1 / błąd podczas pobierania pakietu podczas używania dostawcy poświadczeń z wielu źródeł - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="952b2-215">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="952b2-216">`project.json`Przywracanie nuget powoduje ponowną kompilację, gdy nie zmienić - [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="952b2-216">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="952b2-217">Symbole pakietów nie należy nigdy używać w instalacji lub aktualizacji - [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="952b2-217">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="952b2-218">VS nie obsługuje zmiennych środowiskowych w repositoryPath (nie nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="952b2-218">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="952b2-219">Etykieta bez etykiety elementy interfejsu użytkownika w interfejsie użytkownika Menedżera pakietów ułatwień dostępu - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="952b2-219">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="952b2-220">Przenośne platformy przy użyciu profilów podzielonym są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="952b2-220">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="952b2-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="952b2-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="952b2-222">Menedżer pakietów NuGet powinien stał się wyczyścić tej listy opcji w pakietach szczegółów nie ma zastosowania do `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="952b2-222">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="952b2-223">nuget.exe wypychania lub usuń używać klucza API - [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="952b2-223">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="952b2-224">Usuń właściwość locked z pliku blokady - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="952b2-224">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="952b2-225">Aktualizacja NuGet 3.3.0 "... dodatkowe ograniczenie zdefiniowane w pliku packages.config uniemożliwia wykonanie tej operacji."</span><span class="sxs-lookup"><span data-stu-id="952b2-225">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="952b2-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="952b2-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="952b2-227">Instalowanie pakietu z lokalnego źródła, które nie istnieje zgłasza sfałszowany komunikat - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="952b2-227">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="952b2-228">Filtr "Dostępne uaktualnienie" pokazuje uaktualnień, które narusza ograniczenie wersji - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="952b2-228">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="952b2-229">Nie można zaktualizować oryginalne pakiety - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="952b2-229">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="952b2-230">Funkcje</span><span class="sxs-lookup"><span data-stu-id="952b2-230">Features</span></span>

* <span data-ttu-id="952b2-231">Obsługuje ustawienie CopyLocal FALSE na odwołania dodane przez narzędzie NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="952b2-231">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="952b2-232">Obsługa nuget.exe MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="952b2-232">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="952b2-233">Obsługa pakietu.`csproj`</span><span class="sxs-lookup"><span data-stu-id="952b2-233">Pack support for .`csproj`</span></span><span data-ttu-id="952b2-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="952b2-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="952b2-235">Wyłączania akcja ze strony użytkownika, gdy jest wykonywana akcji użytkownika- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="952b2-235">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="952b2-236">NuGet należy dodać obsługę `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="952b2-236">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="952b2-237">Dodaj brakujące w NuGet możliwości framework 2.x (które są już 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="952b2-237">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="952b2-238">Obsługi rezerwowego pakietu folderów - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="952b2-238">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="952b2-239">Projektowania i implementacji pojęcie typu pakietu do obsługi pakietów narzędzie - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="952b2-239">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="952b2-240">Dodawanie interfejsu API można pobrać ścieżki do folderu pakietów globalne - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="952b2-240">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="952b2-241">Włączanie programu SemVer 2.0.0 w pakiecie - [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="952b2-241">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="952b2-242">Dcr</span><span class="sxs-lookup"><span data-stu-id="952b2-242">DCRs</span></span>

* <span data-ttu-id="952b2-243">nuget.exe push - parametr limitu czasu nie działa — [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="952b2-243">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="952b2-244">Tekst opisu pakiet powinien być możliwy - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="952b2-244">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="952b2-245">Włącz nuget.exe do produkcji `.props` i `.targets` pliki `.nuproj` projekty [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="952b2-245">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="952b2-246">Dodawanie rozszerzeń interfejsu API można porównać struktury z importów - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="952b2-246">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="952b2-247">Ukryj opcje zależności, korzystając z `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="952b2-247">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="952b2-248">Wydrukować nagłówka wersji nuget.exe w szczegółowych danych wyjściowych - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="952b2-248">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="952b2-249">Należy powiadomić użytkowników, że uaktualnienie/instalowanie tfm dotnet, na podstawie PCL może to spowodować problemy — NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="952b2-249">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="952b2-250">Ostrzegaj zły instalacja/aktualizacja dla projektu z tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="952b2-250">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="952b2-251">Rozwiązywanie problemów z wydajnością z ReShaper i NuGet aktualizacji — [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="952b2-251">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="952b2-252">Dodawanie obsługi netcoreapp11 i netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="952b2-252">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="952b2-253">Wykorzystywanie assemblymetadata — atrybut `.nuspec` token zamiany - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="952b2-253">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
