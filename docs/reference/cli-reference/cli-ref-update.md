---
title: Polecenie aktualizacji interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe Update — polecenie
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236792"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="6da6a-103">Update — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="6da6a-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="6da6a-104">**Dotyczy:** &bullet; **obsługiwane wersje** pakietów: wszystkie</span><span class="sxs-lookup"><span data-stu-id="6da6a-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6da6a-105">Aktualizuje wszystkie pakiety w projekcie (przy użyciu programu `packages.config` ) do ich najnowszych dostępnych wersji.</span><span class="sxs-lookup"><span data-stu-id="6da6a-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="6da6a-106">Zaleca się uruchomienie funkcji ["Restore"](cli-ref-restore.md) przed uruchomieniem narzędzia `update` .</span><span class="sxs-lookup"><span data-stu-id="6da6a-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="6da6a-107">(Aby zaktualizować pojedynczy pakiet, użyj [`nuget install`](cli-ref-install.md) bez określenia numeru wersji, w którym przypadku pakiet NuGet instaluje najnowszą wersję).</span><span class="sxs-lookup"><span data-stu-id="6da6a-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="6da6a-108">Uwaga: `update` program nie współpracuje z interfejsem wiersza polecenia w systemie mono (Mac OSX lub Linux) lub w przypadku korzystania z formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6da6a-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="6da6a-109">`update`Polecenie aktualizuje również odwołania do zestawu w pliku projektu, pod warunkiem, że te odwołania już istnieją.</span><span class="sxs-lookup"><span data-stu-id="6da6a-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="6da6a-110">Jeśli zaktualizowany pakiet ma dodany zestaw, nowe odwołanie *nie* zostanie dodane.</span><span class="sxs-lookup"><span data-stu-id="6da6a-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="6da6a-111">Nowe zależności pakietu nie mają również dodanych odwołań do zestawów.</span><span class="sxs-lookup"><span data-stu-id="6da6a-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="6da6a-112">Aby uwzględnić te operacje w ramach aktualizacji, zaktualizuj pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="6da6a-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="6da6a-113">To polecenie służy również do aktualizowania nuget.exe samego siebie przy użyciu flagi *-Auto* .</span><span class="sxs-lookup"><span data-stu-id="6da6a-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="6da6a-114">Użycie</span><span class="sxs-lookup"><span data-stu-id="6da6a-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="6da6a-115">gdzie `<configPath>` identyfikuje `packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="6da6a-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="6da6a-116">Opcje</span><span class="sxs-lookup"><span data-stu-id="6da6a-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6da6a-117">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="6da6a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6da6a-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="6da6a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="6da6a-119">Określa wersję pakietów zależności do użycia, która może być jedną z następujących:</span><span class="sxs-lookup"><span data-stu-id="6da6a-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="6da6a-120">*Najniższy* (domyślny): najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="6da6a-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="6da6a-121">*HighestPatch* : wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="6da6a-121">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="6da6a-122">*HighestMinor* : wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="6da6a-122">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="6da6a-123">*Najwyższa* : najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="6da6a-123">*Highest* : the highest version</span></span></li><li><span data-ttu-id="6da6a-124">*Ignoruj* : nie będą używane żadne pakiety zależności</span><span class="sxs-lookup"><span data-stu-id="6da6a-124">*Ignore* : No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="6da6a-125">Określa domyślną akcję, gdy plik z pakietu już istnieje w projekcie docelowym.</span><span class="sxs-lookup"><span data-stu-id="6da6a-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="6da6a-126">Ustaw, aby `Overwrite` zawsze zastępowały pliki.</span><span class="sxs-lookup"><span data-stu-id="6da6a-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="6da6a-127">Ustaw, aby `Ignore` pominąć pliki.</span><span class="sxs-lookup"><span data-stu-id="6da6a-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="6da6a-128">Akcja domyślnie wyświetli monit o podanie `PromptUser` każdego pliku powodującego konflikt, chyba że `OverwriteAll` lub `IgnoreAll` nie zostanie podany, który zostanie zastosowany do wszystkich pozostałych plików.</span><span class="sxs-lookup"><span data-stu-id="6da6a-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6da6a-129">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="6da6a-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6da6a-130">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="6da6a-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="6da6a-131">Określa listę identyfikatorów pakietów do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="6da6a-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="6da6a-132">*(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo przed `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="6da6a-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="6da6a-133">*(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem.</span><span class="sxs-lookup"><span data-stu-id="6da6a-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="6da6a-134">Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="6da6a-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="6da6a-135">Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6da6a-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6da6a-136">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6da6a-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="6da6a-137">Umożliwia aktualizację wersji wstępnych.</span><span class="sxs-lookup"><span data-stu-id="6da6a-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="6da6a-138">Ta flaga nie jest wymagana podczas aktualizacji pakietów wersji wstępnej, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="6da6a-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="6da6a-139">Określa folder lokalny, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="6da6a-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="6da6a-140">Określa, że zostaną zainstalowane tylko aktualizacje o najwyższej wersji dostępnej w ramach tej samej wersji głównej i pomocniczej co zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="6da6a-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="6da6a-141">Aktualizuje nuget.exe do najnowszej wersji; wszystkie pozostałe argumenty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="6da6a-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="6da6a-142">Określa listę źródeł pakietów (jako adresy URL), które mają być używane na potrzeby aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6da6a-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="6da6a-143">W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6da6a-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6da6a-144">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6da6a-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="6da6a-145">W przypadku użycia z jednym IDENTYFIKATORem pakietu określa wersję pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="6da6a-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="6da6a-146">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6da6a-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6da6a-147">Przykłady</span><span class="sxs-lookup"><span data-stu-id="6da6a-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
