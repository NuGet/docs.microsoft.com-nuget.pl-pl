---
title: Informacje o wersji 5.1 RTM NuGet
description: Informacje o wersji programu NuGet 5.1 obejmuje nowe funkcje, poprawki błędów i DCRs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842582"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="b52df-103">Informacje o wersji 5.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="b52df-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="b52df-104">NuGet pojazdów dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="b52df-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="b52df-105">NuGet w wersji</span><span class="sxs-lookup"><span data-stu-id="b52df-105">NuGet version</span></span> | <span data-ttu-id="b52df-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b52df-106">Available in Visual Studio version</span></span>| <span data-ttu-id="b52df-107">Dostępne w zestawów SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="b52df-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="b52df-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="b52df-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="b52df-109">Visual Studio 2019 version 16.1</span><span class="sxs-lookup"><span data-stu-id="b52df-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="b52df-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b52df-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="b52df-111"><sup>1</sup>instalowane z Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="b52df-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="b52df-112"><sup>2</sup>jest dostępna jako opcjonalna instalacja przy użyciu programu Visual Studio 2019 r przy użyciu obciążenia platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="b52df-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="b52df-113">Podsumowanie: What's New in 5.1</span><span class="sxs-lookup"><span data-stu-id="b52df-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="b52df-114">Pomocy technicznej, aby pominąć powiadomienie wypychane pakietu, jeśli już istnieje, aby umożliwić lepszą integrację z przepływami pracy ciągłej integracji/ciągłego wdrażania — [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="b52df-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="b52df-115">Program Visual Studio teraz oferuje wygodny link do strony galerii nuget.org pakietu - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="b52df-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="b52df-116">Obsługa nowe zasoby platformy .NET Core 3.0, takie jak [pakietów przeznaczonych dla](https://github.com/dotnet/cli/issues/10006) i [pakiety środowiska uruchomieniowego](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="b52df-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="b52df-117">Pakiet NuGet i przywracanie Obsługa FrameworkReferences umożliwia określanie wartości docelowej i środowisko uruchomieniowe odwołania do pakietu - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="b52df-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="b52df-118">Obsługa "Pobierz tylko" pakiet scenariusz PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="b52df-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="b52df-119">Środowisko uruchomieniowe Exlcude i kierowania pakietów z wyników wyszukiwania i ich przywracanie grafu przy użyciu PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="b52df-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="b52df-120">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="b52df-120">Issues fixed in this release</span></span>

<span data-ttu-id="b52df-121">**Błędy**</span><span class="sxs-lookup"><span data-stu-id="b52df-121">**Bugs**</span></span>

* <span data-ttu-id="b52df-122">Wtyczki: Szczegóły wyjątku utracone podczas tworzenia wtyczki - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="b52df-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="b52df-123">Zakres PackageReference się wyłączności dolna granica nie działa, jeśli dolna granica jest obecny w jedno ze źródeł.</span><span class="sxs-lookup"><span data-stu-id="b52df-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="b52df-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="b52df-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="b52df-125">Poprawić komunikatu IsPackableFalseError — [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="b52df-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="b52df-126">Pakiety blokady pliku — ponowne generowanie blokady po zmianie projektów programu graph — [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="b52df-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="b52df-127">Współdzielone usterka: Pakiety Nuget wprowadzenie automatycznie usunięte - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="b52df-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="b52df-128">Dodanie elementu docelowego w celu zwrócenia FrameworkReference przypominające CollectPackageDownloads i CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="b52df-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="b52df-129">Pamięć podręczna HTTP:  RepositoryResources zasobu nie jest buforowana w sposób wersjonowany - [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="b52df-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="b52df-130">Rejestrowanie: stosy wywołań wyjątków nie są zgłaszane wraz z szczegółowy poziom szczegółowości - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="b52df-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="b52df-131">Zmień wszystkie adresy URL Docs NuGet do używania protokołu HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="b52df-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="b52df-132">Poprawa komunikat ostrzegawczy NU3024 - [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="b52df-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="b52df-133">plik blokady nie aktualizuje, gdy packagereference usunięte - [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="b52df-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="b52df-134">Poprawa obsługi przypadków błędów podczas weryfikowania elementu licenseurl i licencji w nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="b52df-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="b52df-135">Kliknij prawym przyciskiem myszy w nagłówku kartę i kliknięcie przycisku "Otwórz lokalizację pliku" powoduje błąd — PM interfejsu użytkownika — [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="b52df-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="b52df-136">Wtyczki: dziennika podczas procesu wtyczki zamyka - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="b52df-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="b52df-137">Wtyczki: współczynnik kolizji wysokiej rejestrowanie wartości daty/godziny — [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="b52df-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="b52df-138">Manifest.ReadFrom zakończy się niepowodzeniem w dowolnym nuspec z LicenseExpression — [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="b52df-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="b52df-139">RestoreLockedMode: Nieoczekiwany NU1004 elementu ProjectReference odwołuje się do projektu przy użyciu niestandardowych AssemblyName — [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="b52df-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="b52df-140">Udoskonalony komunikat o błędzie podczas uruchamiania wtyczki zakończy się niepowodzeniem z powodu wyjątku - [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="b52df-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="b52df-141">W trakcie przywracania aktualizujący nie działa, należy unikać \*. dgspec.json zapisu w katalogu obj — [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="b52df-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="b52df-142">GeneratePathProperty = true kończy się niepowodzeniem, można wygenerować właściwości w przypadku niezgodność - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="b52df-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="b52df-143">Ustawienia: niedozwolony znak w ścieżce źródła pakietu może ulec awarii VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="b52df-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="b52df-144">Usunięcie pliku blokady przywracania nie generuje pliku blokady na aktualizujący nie działa — [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="b52df-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="b52df-145">Adres URL licencji i licencji powoduje błąd z metadanymi - odczytu [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="b52df-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="b52df-146">Nieobsługiwane wyjątki w V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="b52df-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="b52df-147">nuget.exe zwróci kod zakończenia zero w przypadku podania nieprawidłowych argumentów - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="b52df-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="b52df-148">Zaktualizuj błędy i ostrzeżenia docs, aby odzwierciedlały podpisywania scenariusze pokrewne - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="b52df-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="b52df-149">Plik zasobów należy użyć ścieżek względnych umożliwiające łatwiejsze — przenoszenie projektów [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="b52df-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="b52df-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="b52df-150">**DCRs**</span></span>

* <span data-ttu-id="b52df-151">Wtyczki: Włączanie rejestrowania diagnostycznego - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="b52df-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="b52df-152">Utwórz Tizen 6 mapę, aby NetStandard 2.1 — [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="b52df-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="b52df-153">**[Lista wszystkie problemy rozwiązane w tej wersji — 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="b52df-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
