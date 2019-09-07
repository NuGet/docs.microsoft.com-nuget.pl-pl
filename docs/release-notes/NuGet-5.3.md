---
title: Informacje o wersji narzędzia NuGet 5,3
description: Informacje o wersji programu NuGet 5,3, w tym nowe funkcje, poprawki błędów i DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774102"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="ab76a-103">Informacje o wersji narzędzia NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="ab76a-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="ab76a-104">Pojazdy dystrybucji NuGet:</span><span class="sxs-lookup"><span data-stu-id="ab76a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ab76a-105">Wersja programu NuGet</span><span class="sxs-lookup"><span data-stu-id="ab76a-105">NuGet version</span></span> | <span data-ttu-id="ab76a-106">Dostępne w wersji programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ab76a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="ab76a-107">Dostępne w zestawach SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="ab76a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="ab76a-108">**5.3.0 — preview3**</span><span class="sxs-lookup"><span data-stu-id="ab76a-108">**5.3.0-preview3**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ab76a-109">Visual Studio 2019 w wersji 16,3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="ab76a-109">Visual Studio 2019 version 16.3 Preview 3</span></span>](https://visualstudio.microsoft.com/vs/preview/) | <span data-ttu-id="ab76a-110">[3.0.100 — preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ab76a-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="ab76a-111"><sup>1</sup> Zainstalowane z programem Visual Studio 2019 przy użyciu obciążenia .NET Core</span><span class="sxs-lookup"><span data-stu-id="ab76a-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53-preview-3"></a><span data-ttu-id="ab76a-112">Podsumowanie Co nowego w wersji zapoznawczej 5,3 3</span><span class="sxs-lookup"><span data-stu-id="ab76a-112">Summary: What's New in 5.3 preview 3</span></span>

* <span data-ttu-id="ab76a-113">[Ikonę pakietu można osadzić w pakiecie](../reference/msbuild-targets.md#packing-an-icon-image-file), zamiast korzystać z zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="ab76a-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="ab76a-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="ab76a-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="ab76a-115">Ulepszone zabezpieczenia dzięki śledzeniu i wymuszaniu algorytmu SHA dla pakietów Packages. config — [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="ab76a-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ab76a-116">Problemy rozwiązane w tej wersji</span><span class="sxs-lookup"><span data-stu-id="ab76a-116">Issues fixed in this release</span></span>

<span data-ttu-id="ab76a-117">**Usterek**</span><span class="sxs-lookup"><span data-stu-id="ab76a-117">**Bugs**</span></span>

* <span data-ttu-id="ab76a-118">VS: zestawy są w pełni NGen-Ed nie częściowo NGen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="ab76a-118">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="ab76a-119">Zmniejsz użycie pamięci (anulowanie subskrypcji zdarzeń) — [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="ab76a-119">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="ab76a-120">Komunikat "Error_UnableToFindProjectInfo" nie jest poprawny gramatycznie — [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="ab76a-120">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="ab76a-121">Udoskonalenia NU1403 — sprawdzaj poprawność wszystkich pakietów, Uwzględnij oczekiwane/rzeczywiste wartości SHA- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="ab76a-121">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="ab76a-122">Wielokrotne Wyliczenie w NuGetPackageManager. PreviewUpdatePackagesAsync- [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="ab76a-122">Multiple enumeration in NuGetPackageManager.PreviewUpdatePackagesAsync - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="ab76a-123">Przywróć zmianę "Public-> Internal" w PluginProcess — [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="ab76a-123">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="ab76a-124">IVsPackageSourceProvider. getsources (...) ma źle zdefiniowane zachowanie wyjątków — [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="ab76a-124">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="ab76a-125">Utwórz ponownie Konstruktor wtyczki — [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="ab76a-125">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="ab76a-126">Metryki do śledzenia częstotliwości odświeżania interfejsu użytkownika PM — [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="ab76a-126">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="ab76a-127">Zmniejsz liczbę odświeżanych interfejsów użytkownika podczas instalacji za pomocą interfejsu użytkownika Menedżera pakietów — [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="ab76a-127">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="ab76a-128">Telemetrię: wartości DateTime używają formatów specyficznych dla kultury — [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="ab76a-128">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="ab76a-129">Zmniejsz liczbę odświeżanych interfejsów użytkownika na karcie Przeglądaj w interfejsie użytkownika Menedżera pakietów #6570 — [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="ab76a-129">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="ab76a-130">[Niepowodzenie testu] "Nie można przeanalizować pliku konfiguracji" zostanie wyświetlony monit dwa razy — [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="ab76a-130">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="ab76a-131">Zgłoś błąd NU5037 z dobrą stroną dokumentu, która objaśnia poprawki klientów (w pakiecie brakuje wymaganego pliku nuspec) — [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="ab76a-131">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="ab76a-132">Przywracanie w trybie zablokowanym kończy się niepowodzeniem, gdy RuntimeIdentifier projektu zostanie zmieniony — [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="ab76a-132">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="ab76a-133">Ustaw odczytywanie ustawień w programie VS z opóźnieniem [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="ab76a-133">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="ab76a-134">Regresja w "Dodawanie źródeł NuGet" powoduje, że "znak": ", wartość szesnastkowa 0x3A, nie może zostać uwzględniony w nazwie" Błędy- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="ab76a-134">Regression in 'Nuget sources add' causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="ab76a-135">Dostawcy poświadczeń wtyczki NuGet — ukrywanie okna procesu — [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="ab76a-135">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="ab76a-136">Wymuś PackagePathResolver jest ścieżką bezwzględną- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="ab76a-136">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="ab76a-137">Zmniejsz odświeżanie interfejsu użytkownika na kartach Instalowanie i aktualizowanie interfejsu użytkownika Menedżera pakietów — [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="ab76a-137">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="ab76a-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="ab76a-138">**DCR:**</span></span>

* <span data-ttu-id="ab76a-139">Aktualizowanie platform platformy Xamarin do mapowania na Standard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="ab76a-139">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="ab76a-140">Włącz kopiowanie zawartości Menedżera pakietów "okno podglądu" dla instalacji/aktualizacji- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="ab76a-140">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="ab76a-141">Włącz przywracanie na plikach. proj — [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="ab76a-141">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="ab76a-142">Wprowadź `NUGET_NETFX_PLUGIN_PATHS` i`NUGET_NETCORE_PLUGIN_PATHS` aby obsługiwać konfigurację obu jednocześnie — [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="ab76a-142">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="ab76a-143">Włącz wiele wersji dla PackageDownload za pomocą atrybutu Version- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="ab76a-143">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="ab76a-144">Opcje Add-SolutionDirectory i-PackageDirectory do programu NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="ab76a-144">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

* <span data-ttu-id="ab76a-145">Włącz deterministyczne pakiet NuGet- [#6229](https://github.com/NuGet/Home/issues/6229)</span><span class="sxs-lookup"><span data-stu-id="ab76a-145">Enable NuGet Pack to be deterministic - [#6229](https://github.com/NuGet/Home/issues/6229)</span></span>

<span data-ttu-id="ab76a-146">**[Lista wszystkich problemów rozwiązanych w tej wersji (wersja zapoznawcza 3) 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="ab76a-146">**[List of all issues fixed in this release - 5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
