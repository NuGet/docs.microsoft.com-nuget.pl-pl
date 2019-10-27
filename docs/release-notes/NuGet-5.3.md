---
title: Informacje o wersji narzędzia NuGet 5,3
description: Informacje o wersji programu NuGet 5,3, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 994a0da3728e05a09b5537d150f2203477922efc
ms.sourcegitcommit: 904cbee57770af04efcae0b3709301685475bf64
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/26/2019
ms.locfileid: "72962293"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="f6cd0-103">Informacje o wersji narzędzia NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="f6cd0-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="f6cd0-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="f6cd0-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f6cd0-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="f6cd0-105">NuGet version</span></span> | <span data-ttu-id="f6cd0-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6cd0-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f6cd0-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="f6cd0-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f6cd0-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="f6cd0-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f6cd0-109">Visual Studio 2019 w wersji 16,3</span><span class="sxs-lookup"><span data-stu-id="f6cd0-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f6cd0-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f6cd0-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="f6cd0-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="f6cd0-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f6cd0-112">Visual Studio 2019 w wersji 16.3.6</span><span class="sxs-lookup"><span data-stu-id="f6cd0-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="f6cd0-113">Przyszła wersja: 3.0.101</span><span class="sxs-lookup"><span data-stu-id="f6cd0-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="f6cd0-114"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="f6cd0-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="f6cd0-115">Podsumowanie: co nowego w 5,3</span><span class="sxs-lookup"><span data-stu-id="f6cd0-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="f6cd0-116">[Ikonę pakietu można osadzić w pakiecie](../reference/msbuild-targets.md#packing-an-icon-image-file), zamiast korzystać z zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="f6cd0-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="f6cd0-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="f6cd0-118">Ulepszone zabezpieczenia dzięki śledzeniu i wymuszaniu algorytmu SHA dla pakietów Packages. config — [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="f6cd0-119">Włącz wycofanie przestarzałych/starszych pakietów NuGet [#2867](https://github.com/NuGet/Home/issues/2867) | [wpis w blogu](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f6cd0-120">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="f6cd0-120">Issues fixed in this release</span></span>

<span data-ttu-id="f6cd0-121">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="f6cd0-121">**Bugs**</span></span>

* <span data-ttu-id="f6cd0-122">Pakiety NuGet utworzone za pomocą zestawu SDK 3.0.100-preview9 nie mogą być używane przez użytkowników SDK 2,2... w zależności od [#8603](https://github.com/NuGet/Home/issues/8603) strefy czasowej</span><span class="sxs-lookup"><span data-stu-id="f6cd0-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="f6cd0-123">"Znaki cudzysłowu" w ścieżce powodują awarię "niedozwolone znaki w ścieżce" w `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="f6cd0-124">VS: zestawy są w pełni NGen-Ed nie częściowo NGen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="f6cd0-125">Zmniejsz użycie pamięci (anulowanie subskrypcji zdarzeń) — [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="f6cd0-126">Komunikat "Error_UnableToFindProjectInfo" nie jest poprawny gramatycznie — [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="f6cd0-127">Udoskonalenia NU1403 — sprawdzaj poprawność wszystkich pakietów, Uwzględnij oczekiwane/rzeczywiste wartości SHA- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="f6cd0-128">Wielokrotne Wyliczenie w `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="f6cd0-129">Przywróć zmianę "Public-> Internal" w PluginProcess — [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="f6cd0-130">IVsPackageSourceProvider. getsources (...) ma źle zdefiniowane zachowanie wyjątków — [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="f6cd0-131">Utwórz ponownie Konstruktor wtyczki — [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="f6cd0-132">Metryki do śledzenia częstotliwości odświeżania interfejsu użytkownika PM — [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="f6cd0-133">Zmniejsz liczbę odświeżanych interfejsów użytkownika podczas instalacji za pomocą interfejsu użytkownika Menedżera pakietów — [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="f6cd0-134">Telemetrię: wartości DateTime używają formatów specyficznych dla kultury — [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="f6cd0-135">Zmniejsz liczbę odświeżanych interfejsów użytkownika na karcie Przeglądaj w interfejsie użytkownika Menedżera pakietów #6570 — [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="f6cd0-136">[Niepowodzenie testu] "Nie można przeanalizować pliku konfiguracji" zostanie wyświetlony monit dwa razy — [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="f6cd0-137">Zgłoś błąd NU5037 z dobrą stroną dokumentu, która objaśnia poprawki klientów (w pakiecie brakuje wymaganego pliku nuspec) — [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="f6cd0-138">Przywracanie w trybie zablokowanym kończy się niepowodzeniem, gdy RuntimeIdentifier projektu zostanie zmieniony — [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="f6cd0-139">Ustaw odczytywanie ustawień w programie VS z opóźnieniem [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="f6cd0-140">Regresja w `Nuget sources add` powoduje, że "znak": ", wartość szesnastkowa 0x3A, nie może zostać uwzględniony w nazwie" Błędy — [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="f6cd0-141">Dostawcy poświadczeń wtyczki NuGet — ukrywanie okna procesu — [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="f6cd0-142">Wymuś PackagePathResolver jest ścieżką bezwzględną- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="f6cd0-143">Zmniejsz odświeżanie interfejsu użytkownika na kartach Instalowanie i aktualizowanie interfejsu użytkownika Menedżera pakietów — [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="f6cd0-144">**DCR**</span><span class="sxs-lookup"><span data-stu-id="f6cd0-144">**DCR:**</span></span>

* <span data-ttu-id="f6cd0-145">Aktualizowanie platform platformy Xamarin do mapowania na Standard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="f6cd0-146">Włącz kopiowanie zawartości Menedżera pakietów "okno podglądu" dla instalacji/aktualizacji- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="f6cd0-147">Włącz przywracanie na plikach. proj — [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="f6cd0-148">Wprowadź `NUGET_NETFX_PLUGIN_PATHS` i `NUGET_NETCORE_PLUGIN_PATHS` do obsługi konfiguracji obu jednocześnie [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="f6cd0-149">Włącz wiele wersji dla PackageDownload za pomocą atrybutu Version- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="f6cd0-150">Opcje Add-SolutionDirectory i-PackageDirectory do programu NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="f6cd0-151">**[Lista wszystkich problemów rozwiązanych w tej wersji — 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="f6cd0-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="f6cd0-152">Podsumowanie: co nowego w programie 5.3.1</span><span class="sxs-lookup"><span data-stu-id="f6cd0-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="f6cd0-153">Wtyczka: zadanie zostało anulowane — nie Zezwalaj na anulowanie dla tworzenia wystąpienia wtyczki — [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="f6cd0-154">Nie można bezpiecznie uruchomić zadania przywracania dwa razy w jednym procesie (gdy są używane dostawcy poświadczeń) — [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="f6cd0-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
