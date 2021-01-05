---
title: Informacje o wersji narzędzia NuGet 5,1 RTM
description: Informacje o wersji programu NuGet 5,1, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699862"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="32c29-103">Informacje o wersji narzędzia NuGet 5,1</span><span class="sxs-lookup"><span data-stu-id="32c29-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="32c29-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="32c29-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="32c29-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="32c29-105">NuGet version</span></span> | <span data-ttu-id="32c29-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32c29-106">Available in Visual Studio version</span></span>| <span data-ttu-id="32c29-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="32c29-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="32c29-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="32c29-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="32c29-109">Visual Studio 2019 w wersji 16,1</span><span class="sxs-lookup"><span data-stu-id="32c29-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="32c29-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="32c29-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="32c29-111"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="32c29-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="32c29-112"><sup>2</sup> Dostępne jako opcjonalna instalacja z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="32c29-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="32c29-113">Podsumowanie: co nowego w 5,1</span><span class="sxs-lookup"><span data-stu-id="32c29-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="32c29-114">Obsługa pominięcia wypychania pakietu, jeśli już istnieje, aby umożliwić lepszą integrację z przepływami pracy ciągłej integracji/ciągłego wdrażania — [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="32c29-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="32c29-115">Program Visual Studio udostępnia teraz wygodny link do strony galerii nuget.org pakietu — [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="32c29-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="32c29-116">Obsługa nowych zasobów platformy .NET Core 3,0, takich jak [pakiety docelowe](https://github.com/dotnet/cli/issues/10006) i [pakiety środowiska uruchomieniowego](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="32c29-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="32c29-117">Pakiet NuGet i obsługa przywracania dla FrameworkReferences w celu włączenia elementów docelowych i odwołań do pakietów środowiska uruchomieniowego — [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="32c29-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="32c29-118">Obsługa scenariusza pakietu "tylko pobieranie" z PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="32c29-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="32c29-119">Wyklucz środowisko uruchomieniowe i pakiety docelowe z wyników wyszukiwania & przywracanie wykresu przy użyciu elementu PackageType — [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="32c29-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="32c29-120">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="32c29-120">Issues fixed in this release</span></span>

<span data-ttu-id="32c29-121">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="32c29-121">**Bugs**</span></span>

* <span data-ttu-id="32c29-122">Wtyczki: Szczegóły wyjątku utracone podczas tworzenia wtyczki — [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="32c29-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="32c29-123">Zakres PackageReference z wyłącznym dolnym ograniczeniem nie działa, jeśli Dolna granica jest obecna w jednym ze źródeł.</span><span class="sxs-lookup"><span data-stu-id="32c29-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="32c29-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="32c29-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="32c29-125">Ulepszanie komunikatu IsPackableFalseError — [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="32c29-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="32c29-126">Zablokuj plik — Wygeneruj ponownie plik blokady podczas zmiany grafu projektu — [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="32c29-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="32c29-127">Usterka współdzielone: pakiety NuGet do pobrania są usuwane [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="32c29-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="32c29-128">Dodaj obiekt docelowy do zwrócenia FrameworkReference podobnego do CollectPackageDownloads i CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="32c29-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="32c29-129">Pamięć podręczna HTTP: zasób RepositoryResources nie jest buforowany w sposób [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="32c29-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="32c29-130">Rejestrowanie: wyjątek stosy wywołań nie jest raportowany ze szczegółowym szczegółowośćem — [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="32c29-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="32c29-131">Zmień adresy URL wszystkich dokumentów NuGet, aby używały protokołu HTTPS [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="32c29-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="32c29-132">Ulepsz komunikat ostrzegawczy NU3024 — [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="32c29-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="32c29-133">Zablokuj plik nie jest aktualizowany po usunięciu packagereference — [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="32c29-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="32c29-134">Popraw obsługę wielkości liter podczas sprawdzania poprawności elementu licenseurl i licencji w nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="32c29-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="32c29-135">Interfejs użytkownika PM — kliknij prawym przyciskiem myszy nagłówek karty i kliknięcie pozycji "Otwórz lokalizację pliku" spowoduje błąd — [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="32c29-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="32c29-136">Wtyczki: log po zakończeniu procesu wtyczki — [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="32c29-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="32c29-137">Wtyczki: współczynnik dużej kolizji w wartościach DateTime rejestrowania — [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="32c29-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="32c29-138">Manifest. ReadFrom kończy się niepowodzeniem na żadnym nuspec z LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="32c29-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="32c29-139">RestoreLockedMode: nieoczekiwany NU1004, gdy elementu ProjectReference odwołuje się do projektu z niestandardowym elementem AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="32c29-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="32c29-140">Lepszy komunikat o błędzie podczas uruchamiania wtyczki kończy się niepowodzeniem z wyjątkiem [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="32c29-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="32c29-141">Podczas wykonywania operacji przywracania aktualizujący nie działa należy unikać \* .dgspec.jsprzy zapisie w katalogu obj- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="32c29-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="32c29-142">GeneratePathProperty = true nie można wygenerować właściwości w przypadku niezgodności przypadków — [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="32c29-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="32c29-143">Ustawienia: niedozwolony znak w ścieżce źródłowej pakietu może ulec awarii i [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="32c29-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="32c29-144">Jeśli plik blokady zostanie usunięty, instrukcja RESTORE nie generuje pliku blokady na aktualizujący nie działa- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="32c29-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="32c29-145">Adres URL i licencja licencji powodują błąd odczytu w metadanych — [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="32c29-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="32c29-146">Nieobsłużone wyjątki w V2FeedParser — [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="32c29-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="32c29-147">nuget.exe zwraca kod zakończenia zero dla nieprawidłowych argumentów — [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="32c29-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="32c29-148">Aktualizowanie błędów i dokumentów ostrzeżeń w celu odzwierciedlenia scenariuszy związanych z podpisywaniem — [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="32c29-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="32c29-149">Plik zasobów powinien używać ścieżek względnych, aby łatwiej przenosić projekty [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="32c29-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="32c29-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="32c29-150">**DCRs**</span></span>

* <span data-ttu-id="32c29-151">Wtyczki: Włączanie rejestrowania diagnostycznego — [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="32c29-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="32c29-152">Utwórz mapę Tizen 6 do standardu 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="32c29-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="32c29-153">**[Lista wszystkich problemów rozwiązanych w tym wydaniu — 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="32c29-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
