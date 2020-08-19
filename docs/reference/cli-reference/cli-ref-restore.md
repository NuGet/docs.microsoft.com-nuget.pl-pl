---
title: Polecenie przywracania interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe polecenia Restore
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622833"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="79ad6-103">Restore — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="79ad6-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="79ad6-104">**Dotyczy:** &bullet; **obsługiwane wersje** pakietów: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="79ad6-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="79ad6-105">Pobiera i instaluje wszystkie brakujące pakiety w `packages` folderze.</span><span class="sxs-lookup"><span data-stu-id="79ad6-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="79ad6-106">W przypadku użycia z pakietem NuGet 4.0 + i formatem PackageReference program generuje `<project>.nuget.props` plik, w razie konieczności, w `obj` folderze.</span><span class="sxs-lookup"><span data-stu-id="79ad6-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="79ad6-107">(Plik można pominąć z kontroli źródła).</span><span class="sxs-lookup"><span data-stu-id="79ad6-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="79ad6-108">W systemach Mac OSX i Linux przy użyciu interfejsu wiersza polecenia w systemie mono przywracanie pakietów nie jest obsługiwane z PackageReference.</span><span class="sxs-lookup"><span data-stu-id="79ad6-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="79ad6-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="79ad6-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="79ad6-110">gdzie `<projectPath>` określa lokalizację rozwiązania lub `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="79ad6-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="79ad6-111">Aby uzyskać szczegółowe informacje o zachowaniu, zobacz [uwagi](#remarks) poniżej.</span><span class="sxs-lookup"><span data-stu-id="79ad6-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="79ad6-112">Opcje</span><span class="sxs-lookup"><span data-stu-id="79ad6-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="79ad6-113">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="79ad6-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="79ad6-114">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="79ad6-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="79ad6-115">*(4.0 +)* Pobiera pakiety bezpośrednio bez wypełniania pamięci podręcznych za pomocą jakichkolwiek plików binarnych lub metadanych.</span><span class="sxs-lookup"><span data-stu-id="79ad6-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="79ad6-116">Wyłącza przywracanie równolegle wielu pakietów.</span><span class="sxs-lookup"><span data-stu-id="79ad6-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="79ad6-117">*(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle.</span><span class="sxs-lookup"><span data-stu-id="79ad6-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="79ad6-118">Użyj średnika, aby oddzielić pozycje listy.</span><span class="sxs-lookup"><span data-stu-id="79ad6-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="79ad6-119">W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="79ad6-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="79ad6-120">Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="79ad6-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="79ad6-121">Nie powoduje to obejścia pamięci podręcznej protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="79ad6-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="79ad6-122">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="79ad6-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="79ad6-123">Wymusza przywrócenie przez Przywracanie wszystkich zależności, nawet jeśli plik blokady już istnieje.</span><span class="sxs-lookup"><span data-stu-id="79ad6-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="79ad6-124">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="79ad6-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="79ad6-125">Lokalizacja wyjściowa, w której jest zapisywana plik blokady projektu.</span><span class="sxs-lookup"><span data-stu-id="79ad6-125">Output location where project lock file is written.</span></span> <span data-ttu-id="79ad6-126">Domyślnie jest to `PROJECT_ROOT\packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="79ad6-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="79ad6-127">Nie Zezwalaj na aktualizowanie pliku blokady projektu.</span><span class="sxs-lookup"><span data-stu-id="79ad6-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="79ad6-128">*(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo przed `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="79ad6-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="79ad6-129">*(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem.</span><span class="sxs-lookup"><span data-stu-id="79ad6-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="79ad6-130">Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="79ad6-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="79ad6-131">Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="79ad6-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="79ad6-132">Uniemożliwia narzędziu NuGet używanie buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="79ad6-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="79ad6-133">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="79ad6-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="79ad6-134">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="79ad6-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="79ad6-135">Określa folder, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="79ad6-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="79ad6-136">Jeśli folder nie zostanie określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="79ad6-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="79ad6-137">Wymagane w przypadku przywracania z `packages.config` plikiem, chyba że `PackagesDirectory` lub `SolutionDirectory` jest używany.</span><span class="sxs-lookup"><span data-stu-id="79ad6-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="79ad6-138">Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec` , `nupkg` lub `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="79ad6-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="79ad6-139">Analogicznie jak `OutputDirectory` .</span><span class="sxs-lookup"><span data-stu-id="79ad6-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="79ad6-140">Wymagane w przypadku przywracania z `packages.config` plikiem, chyba że `OutputDirectory` lub `SolutionDirectory` jest używany.</span><span class="sxs-lookup"><span data-stu-id="79ad6-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="79ad6-141">Limit czasu w sekundach dla rozpoznawania odwołań między projektami.</span><span class="sxs-lookup"><span data-stu-id="79ad6-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="79ad6-142">*(4.0 +)* Przywraca wszystkie projekty odwołań dla projektów platformy UWP i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="79ad6-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="79ad6-143">Nie dotyczy projektów korzystających z programu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="79ad6-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="79ad6-144">Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów.</span><span class="sxs-lookup"><span data-stu-id="79ad6-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="79ad6-145">Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="79ad6-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="79ad6-146">Określa folder rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="79ad6-146">Specifies the solution folder.</span></span> <span data-ttu-id="79ad6-147">Nieprawidłowy podczas przywracania pakietów dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="79ad6-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="79ad6-148">Wymagane w przypadku przywracania z `packages.config` plikiem, chyba że `PackagesDirectory` lub `OutputDirectory` jest używany.</span><span class="sxs-lookup"><span data-stu-id="79ad6-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="79ad6-149">Określa listę źródeł pakietów (jako adresy URL) do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="79ad6-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="79ad6-150">W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [Konfigurowanie zachowania NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="79ad6-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="79ad6-151">Użyj średnika, aby oddzielić pozycje listy.</span><span class="sxs-lookup"><span data-stu-id="79ad6-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="79ad6-152">Umożliwia generowanie i używanie pliku blokady projektu z przywracaniem.</span><span class="sxs-lookup"><span data-stu-id="79ad6-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="79ad6-153">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="79ad6-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="79ad6-154">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="79ad6-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="79ad6-155">Uwagi</span><span class="sxs-lookup"><span data-stu-id="79ad6-155">Remarks</span></span>

<span data-ttu-id="79ad6-156">Polecenie Restore wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="79ad6-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="79ad6-157">Określ tryb operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="79ad6-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="79ad6-158">Typ pliku projectPath</span><span class="sxs-lookup"><span data-stu-id="79ad6-158">projectPath file type</span></span> | <span data-ttu-id="79ad6-159">Zachowanie</span><span class="sxs-lookup"><span data-stu-id="79ad6-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="79ad6-160">Rozwiązanie (folder)</span><span class="sxs-lookup"><span data-stu-id="79ad6-160">Solution (folder)</span></span> | <span data-ttu-id="79ad6-161">Pakiet NuGet szuka `.sln` pliku i używa go, jeśli został znaleziony; w przeciwnym razie wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="79ad6-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="79ad6-162">`(SolutionDir)\.nuget` jest używany jako folder początkowy.</span><span class="sxs-lookup"><span data-stu-id="79ad6-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="79ad6-163">`.sln` rozszerzeniem</span><span class="sxs-lookup"><span data-stu-id="79ad6-163">`.sln` file</span></span> | <span data-ttu-id="79ad6-164">Przywróć pakiety zidentyfikowane przez rozwiązanie; występuje błąd, jeśli `-SolutionDirectory` jest używany.</span><span class="sxs-lookup"><span data-stu-id="79ad6-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="79ad6-165">`$(SolutionDir)\.nuget` jest używany jako folder początkowy.</span><span class="sxs-lookup"><span data-stu-id="79ad6-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="79ad6-166">`packages.config` lub plik projektu</span><span class="sxs-lookup"><span data-stu-id="79ad6-166">`packages.config` or project file</span></span> | <span data-ttu-id="79ad6-167">Przywróć pakiety wymienione w pliku, Rozwiązuj i instalując zależności.</span><span class="sxs-lookup"><span data-stu-id="79ad6-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="79ad6-168">Inny typ pliku</span><span class="sxs-lookup"><span data-stu-id="79ad6-168">Other file type</span></span> | <span data-ttu-id="79ad6-169">Przyjęto, że plik jest `.sln` plikiem, tak jak powyżej; Jeśli nie jest to rozwiązanie, wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="79ad6-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="79ad6-170">(nie określono projectPath)</span><span class="sxs-lookup"><span data-stu-id="79ad6-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="79ad6-171">Pakiet NuGet szuka plików rozwiązania w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="79ad6-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="79ad6-172">Jeśli zostanie znaleziony pojedynczy plik, jest on używany do przywracania pakietów; Jeśli zostanie znalezionych wiele rozwiązań, wystąpi błąd programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="79ad6-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="79ad6-173">Jeśli nie ma plików rozwiązania, pakiet NuGet szuka `packages.config` i używa do przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="79ad6-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="79ad6-174">Jeśli nie zostanie znalezione żadne rozwiązanie lub `packages.config` plik, wystąpi błąd programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="79ad6-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="79ad6-175">Określ folder Packages przy użyciu następującej kolejności priorytetów (NuGet powoduje błąd, jeśli nie odnaleziono żadnego z tych folderów):</span><span class="sxs-lookup"><span data-stu-id="79ad6-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="79ad6-176">Folder określony za pomocą `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="79ad6-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="79ad6-177">`repositoryPath`Wartość w`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="79ad6-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="79ad6-178">Folder określony za pomocą `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="79ad6-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="79ad6-179">Podczas przywracania pakietów dla rozwiązania NuGet wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="79ad6-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="79ad6-180">Ładuje plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="79ad6-180">Loads the solution file.</span></span>
    - <span data-ttu-id="79ad6-181">Przywraca pakiety na poziomie rozwiązania wymienione w `$(SolutionDir)\.nuget\packages.config` `packages` folderze.</span><span class="sxs-lookup"><span data-stu-id="79ad6-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="79ad6-182">Przywróć pakiety wymienione w `$(ProjectDir)\packages.config` folderze do `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="79ad6-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="79ad6-183">Dla każdego określonego pakietu Przywróć pakiet równolegle, chyba że `-DisableParallelProcessing` zostanie określony.</span><span class="sxs-lookup"><span data-stu-id="79ad6-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="79ad6-184">Przykłady</span><span class="sxs-lookup"><span data-stu-id="79ad6-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
