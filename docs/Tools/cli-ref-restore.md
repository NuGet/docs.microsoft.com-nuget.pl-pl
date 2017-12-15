---
title: Polecenie restore interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Informacje dotyczące polecenia restore nuget.exe"
keywords: "nuget przywrócić odwołania, przywrócić pakiety, polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="7d856-104">polecenie Restore (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7d856-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="7d856-105">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="7d856-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="7d856-106">NuGet 2.7 +: Pobiera i instaluje wszystkie pakiety brakuje `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="7d856-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="7d856-107">NuGet 3.3 + z projektami za pomocą `project.json`: generuje `project.lock.json` pliku i `<project>.nuget.props` plików, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7d856-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="7d856-108">(Oba pliki można pominąć z kontroli źródła).</span><span class="sxs-lookup"><span data-stu-id="7d856-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="7d856-109">NuGet 4.0 + z projektem, w którym pakiecie odwołania znajdują się w pliku projektu bezpośrednio: generuje `<project>.nuget.props` pliku, w razie potrzeby w `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="7d856-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="7d856-110">(Plik można pominąć z kontroli źródła).</span><span class="sxs-lookup"><span data-stu-id="7d856-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="7d856-111">Mac OS x i Linux z poziomu interfejsu wiersza polecenia na Mono Przywracanie pakietów nie jest obsługiwane w formacie PackageReference.</span><span class="sxs-lookup"><span data-stu-id="7d856-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="7d856-112">Użycie</span><span class="sxs-lookup"><span data-stu-id="7d856-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="7d856-113">gdzie `<projectPath>` Określa lokalizację rozwiązania, `packages.config` pliku, lub `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="7d856-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="7d856-114">Zobacz [uwagi](#remarks) poniżej behawioralnej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="7d856-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="7d856-115">Opcje</span><span class="sxs-lookup"><span data-stu-id="7d856-115">Options</span></span>

| <span data-ttu-id="7d856-116">Opcja</span><span class="sxs-lookup"><span data-stu-id="7d856-116">Option</span></span> | <span data-ttu-id="7d856-117">Opis</span><span class="sxs-lookup"><span data-stu-id="7d856-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7d856-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7d856-118">ConfigFile</span></span> | <span data-ttu-id="7d856-119">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="7d856-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7d856-120">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="7d856-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="7d856-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="7d856-121">DirectDownload</span></span> | <span data-ttu-id="7d856-122">*(4.0 +)*  Pobiera pakiety bezpośrednio, bez wypełnianie pamięci podręczne z plików binarnych lub metadanych.</span><span class="sxs-lookup"><span data-stu-id="7d856-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="7d856-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="7d856-123">DisableParallelProcessing</span></span> | <span data-ttu-id="7d856-124">Wyłącza Przywracanie wielu pakietów równolegle.</span><span class="sxs-lookup"><span data-stu-id="7d856-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="7d856-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="7d856-125">FallbackSource</span></span> | <span data-ttu-id="7d856-126">*(3.2 +)*  Lista źródła pakietów do użycia jako przejścia, w przypadku, gdy nie można znaleźć pakietu w podstawowej lub źródło domyślne.</span><span class="sxs-lookup"><span data-stu-id="7d856-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="7d856-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7d856-127">ForceEnglishOutput</span></span> | <span data-ttu-id="7d856-128">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="7d856-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7d856-129">Pomoc</span><span class="sxs-lookup"><span data-stu-id="7d856-129">Help</span></span> | <span data-ttu-id="7d856-130">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="7d856-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="7d856-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="7d856-131">MSBuildPath</span></span> | <span data-ttu-id="7d856-132">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="7d856-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="7d856-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="7d856-133">MSBuildVersion</span></span> | <span data-ttu-id="7d856-134">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7d856-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="7d856-135">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="7d856-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="7d856-136">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="7d856-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="7d856-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="7d856-137">NoCache</span></span> | <span data-ttu-id="7d856-138">Zapobiega z pamięci podręcznej komputera lokalnego za pomocą pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d856-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="7d856-139">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="7d856-139">NonInteractive</span></span> | <span data-ttu-id="7d856-140">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="7d856-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7d856-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="7d856-141">OutputDirectory</span></span> | <span data-ttu-id="7d856-142">Określa folder, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="7d856-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="7d856-143">Jeśli folder nie jest określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="7d856-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="7d856-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="7d856-144">PackageSaveMode</span></span> | <span data-ttu-id="7d856-145">Określa typy plików, aby zapisać po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="7d856-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="7d856-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="7d856-146">PackagesDirectory</span></span> | <span data-ttu-id="7d856-147">Taki sam jak `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="7d856-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="7d856-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="7d856-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="7d856-149">Limit czasu w sekundach dla rozpoznawania odwołań projektu do projektu.</span><span class="sxs-lookup"><span data-stu-id="7d856-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="7d856-150">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="7d856-150">Recursive</span></span> | <span data-ttu-id="7d856-151">*(4.0 +)*  Przywraca wszystkie projekty odwołań dla projektów uniwersalnych systemu Windows i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7d856-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="7d856-152">Nie ma zastosowania do projektów przy użyciu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="7d856-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="7d856-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="7d856-153">RequireConsent</span></span> | <span data-ttu-id="7d856-154">Sprawdza, czy Przywracanie pakietów jest włączona przed pobierania i instalowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="7d856-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="7d856-155">Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7d856-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="7d856-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="7d856-156">SolutionDirectory</span></span> | <span data-ttu-id="7d856-157">Określa folder rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7d856-157">Specifies the solution folder.</span></span> <span data-ttu-id="7d856-158">Nieprawidłowy gdy trwa przywracanie pakietów dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7d856-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="7d856-159">Źródło</span><span class="sxs-lookup"><span data-stu-id="7d856-159">Source</span></span> | <span data-ttu-id="7d856-160">Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby przywracania.</span><span class="sxs-lookup"><span data-stu-id="7d856-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="7d856-161">W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7d856-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="7d856-162">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="7d856-162">Verbosity</span></span> |<span data-ttu-id="7d856-163">> określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="7d856-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="7d856-164">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7d856-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="7d856-165">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7d856-165">Remarks</span></span>

<span data-ttu-id="7d856-166">Polecenie restore wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7d856-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="7d856-167">Określ tryb działania polecenia restore.</span><span class="sxs-lookup"><span data-stu-id="7d856-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="7d856-168">Typ pliku projectPath</span><span class="sxs-lookup"><span data-stu-id="7d856-168">projectPath file type</span></span> | <span data-ttu-id="7d856-169">Zachowanie</span><span class="sxs-lookup"><span data-stu-id="7d856-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="7d856-170">Rozwiązania (folder)</span><span class="sxs-lookup"><span data-stu-id="7d856-170">Solution (folder)</span></span> | <span data-ttu-id="7d856-171">Wyszukuje NuGet `.sln` pliku i korzysta z jeśli je znaleziono; w przeciwnym razie zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="7d856-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="7d856-172">`(SolutionDir)\.nuget`jest używana jako folder początkowy.</span><span class="sxs-lookup"><span data-stu-id="7d856-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="7d856-173">`.sln`plik</span><span class="sxs-lookup"><span data-stu-id="7d856-173">`.sln` file</span></span> | <span data-ttu-id="7d856-174">Przywracanie pakietów zidentyfikowane przez rozwiązanie; Zwraca błąd, jeśli `-SolutionDirectory` jest używany.</span><span class="sxs-lookup"><span data-stu-id="7d856-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="7d856-175">`$(SolutionDir)\.nuget`jest używana jako folder początkowy.</span><span class="sxs-lookup"><span data-stu-id="7d856-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="7d856-176">`packages.config`, `project.json`, lub plik projektu</span><span class="sxs-lookup"><span data-stu-id="7d856-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="7d856-177">Przywróć pakiety wymienione w pliku rozwiązania i instalowanie zależności.</span><span class="sxs-lookup"><span data-stu-id="7d856-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="7d856-178">Innego typu pliku</span><span class="sxs-lookup"><span data-stu-id="7d856-178">Other file type</span></span> | <span data-ttu-id="7d856-179">Plik zakłada się, że `.sln` plik jako powyżej; Jeśli nie jest to rozwiązanie zapewnia NuGet błąd.</span><span class="sxs-lookup"><span data-stu-id="7d856-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="7d856-180">(nie określono projectPath)</span><span class="sxs-lookup"><span data-stu-id="7d856-180">(projectPath not specified)</span></span> | <span data-ttu-id="7d856-181">-NuGet wyszukuje pliki rozwiązania w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="7d856-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="7d856-182">Jeśli zostanie znaleziony jeden plik, że jeden służy do przywracania pakietów; w przypadku znalezienia wielu rozwiązań NuGet zawiera błąd.</span><span class="sxs-lookup"><span data-stu-id="7d856-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="7d856-183">— Jeśli nie ma żadnych plików rozwiązania, NuGet szuka `packages.config` lub `project.json` i użyty pod kątem przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="7d856-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="7d856-184">— Jeśli plik rozwiązania nie `packages.config`, lub `project.json` zostanie znaleziony, NuGet zawiera błąd.</span><span class="sxs-lookup"><span data-stu-id="7d856-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="7d856-185">Określ folder pakietów przy użyciu następującej kolejności priorytet (NuGet zwraca błąd, jeśli żadnego z tych folderów nie są znaleziono):</span><span class="sxs-lookup"><span data-stu-id="7d856-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="7d856-186">`%userprofile%\.nuget\packages` Wartość w `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7d856-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="7d856-187">Folder określony za pomocą `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="7d856-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="7d856-188">`repositoryPath` Vale w`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="7d856-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="7d856-189">Folder określony za pomocą`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="7d856-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="7d856-190">Trwa przywracanie pakietów dla rozwiązania, NuGet wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7d856-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="7d856-191">Ładuje plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7d856-191">Loads the solution file.</span></span>
    - <span data-ttu-id="7d856-192">Przywraca poziomu pakietów rozwiązania na liście `$(SolutionDir)\.nuget\packages.config` do `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="7d856-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="7d856-193">Przywracanie pakietów na liście `$(ProjectDir)\packages.config` do `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="7d856-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="7d856-194">Dla każdego pakietu określony Przywracanie pakietu równolegle, chyba że `-DisableParallelProcessing` jest określona.</span><span class="sxs-lookup"><span data-stu-id="7d856-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="7d856-195">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7d856-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
