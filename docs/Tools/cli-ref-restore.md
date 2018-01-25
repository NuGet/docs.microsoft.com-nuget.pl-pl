---
title: Polecenie restore interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia restore nuget.exe"
keywords: "nuget przywrócić odwołania, przywrócić pakiety, polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93d7b6967d9297ee822df1583351385210775173
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="4940f-104">polecenie Restore (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4940f-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="4940f-105">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="4940f-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="4940f-106">Pobiera i instaluje wszystkie pakiety brakuje `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="4940f-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="4940f-107">W przypadku użycia z NuGet 4.0 + i PackageReference format, generuje `<project>.nuget.props` pliku, w razie potrzeby w `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="4940f-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="4940f-108">(Plik można pominąć z kontroli źródła).</span><span class="sxs-lookup"><span data-stu-id="4940f-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="4940f-109">Mac OS x i Linux z poziomu interfejsu wiersza polecenia na Mono Przywracanie pakietów nie jest obsługiwany z PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4940f-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="4940f-110">Użycie</span><span class="sxs-lookup"><span data-stu-id="4940f-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="4940f-111">gdzie `<projectPath>` Określa lokalizację rozwiązania lub `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="4940f-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="4940f-112">Zobacz [uwagi](#remarks) poniżej behawioralnej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="4940f-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="4940f-113">Opcje</span><span class="sxs-lookup"><span data-stu-id="4940f-113">Options</span></span>

| <span data-ttu-id="4940f-114">Opcja</span><span class="sxs-lookup"><span data-stu-id="4940f-114">Option</span></span> | <span data-ttu-id="4940f-115">Opis</span><span class="sxs-lookup"><span data-stu-id="4940f-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4940f-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4940f-116">ConfigFile</span></span> | <span data-ttu-id="4940f-117">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="4940f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4940f-118">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="4940f-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="4940f-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="4940f-119">DirectDownload</span></span> | <span data-ttu-id="4940f-120">*(4.0 +)*  Pobiera pakiety bezpośrednio, bez wypełnianie pamięci podręczne z plików binarnych lub metadanych.</span><span class="sxs-lookup"><span data-stu-id="4940f-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="4940f-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="4940f-121">DisableParallelProcessing</span></span> | <span data-ttu-id="4940f-122">Wyłącza Przywracanie wielu pakietów równolegle.</span><span class="sxs-lookup"><span data-stu-id="4940f-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="4940f-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="4940f-123">FallbackSource</span></span> | <span data-ttu-id="4940f-124">*(3.2 +)*  Lista źródła pakietów do użycia jako przejścia, w przypadku, gdy nie można znaleźć pakietu w podstawowej lub źródło domyślne.</span><span class="sxs-lookup"><span data-stu-id="4940f-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="4940f-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4940f-125">ForceEnglishOutput</span></span> | <span data-ttu-id="4940f-126">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="4940f-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4940f-127">Pomoc</span><span class="sxs-lookup"><span data-stu-id="4940f-127">Help</span></span> | <span data-ttu-id="4940f-128">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="4940f-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="4940f-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="4940f-129">MSBuildPath</span></span> | <span data-ttu-id="4940f-130">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="4940f-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="4940f-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="4940f-131">MSBuildVersion</span></span> | <span data-ttu-id="4940f-132">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4940f-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="4940f-133">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="4940f-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="4940f-134">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4940f-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="4940f-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="4940f-135">NoCache</span></span> | <span data-ttu-id="4940f-136">Zapobiega z pamięci podręcznej komputera lokalnego za pomocą pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="4940f-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="4940f-137">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="4940f-137">NonInteractive</span></span> | <span data-ttu-id="4940f-138">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="4940f-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4940f-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="4940f-139">OutputDirectory</span></span> | <span data-ttu-id="4940f-140">Określa folder, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="4940f-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="4940f-141">Jeśli folder nie jest określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="4940f-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="4940f-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="4940f-142">PackageSaveMode</span></span> | <span data-ttu-id="4940f-143">Określa typy plików, aby zapisać po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4940f-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="4940f-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="4940f-144">PackagesDirectory</span></span> | <span data-ttu-id="4940f-145">Taki sam jak `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="4940f-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="4940f-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="4940f-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="4940f-147">Limit czasu w sekundach dla rozpoznawania odwołań projektu do projektu.</span><span class="sxs-lookup"><span data-stu-id="4940f-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="4940f-148">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="4940f-148">Recursive</span></span> | <span data-ttu-id="4940f-149">*(4.0 +)*  Przywraca wszystkie projekty odwołań dla projektów uniwersalnych systemu Windows i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4940f-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="4940f-150">Nie ma zastosowania do projektów przy użyciu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4940f-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="4940f-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="4940f-151">RequireConsent</span></span> | <span data-ttu-id="4940f-152">Sprawdza, czy Przywracanie pakietów jest włączona przed pobierania i instalowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="4940f-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="4940f-153">Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="4940f-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="4940f-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="4940f-154">SolutionDirectory</span></span> | <span data-ttu-id="4940f-155">Określa folder rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4940f-155">Specifies the solution folder.</span></span> <span data-ttu-id="4940f-156">Nieprawidłowy gdy trwa przywracanie pakietów dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4940f-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="4940f-157">Źródło</span><span class="sxs-lookup"><span data-stu-id="4940f-157">Source</span></span> | <span data-ttu-id="4940f-158">Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby przywracania.</span><span class="sxs-lookup"><span data-stu-id="4940f-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="4940f-159">W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="4940f-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="4940f-160">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="4940f-160">Verbosity</span></span> |<span data-ttu-id="4940f-161">> określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="4940f-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4940f-162">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4940f-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="4940f-163">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4940f-163">Remarks</span></span>

<span data-ttu-id="4940f-164">Polecenie restore wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4940f-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="4940f-165">Określ tryb działania polecenia restore.</span><span class="sxs-lookup"><span data-stu-id="4940f-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="4940f-166">Typ pliku projectPath</span><span class="sxs-lookup"><span data-stu-id="4940f-166">projectPath file type</span></span> | <span data-ttu-id="4940f-167">Zachowanie</span><span class="sxs-lookup"><span data-stu-id="4940f-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="4940f-168">Rozwiązania (folder)</span><span class="sxs-lookup"><span data-stu-id="4940f-168">Solution (folder)</span></span> | <span data-ttu-id="4940f-169">Wyszukuje NuGet `.sln` pliku i korzysta z jeśli je znaleziono; w przeciwnym razie zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="4940f-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="4940f-170">`(SolutionDir)\.nuget`jest używana jako folder początkowy.</span><span class="sxs-lookup"><span data-stu-id="4940f-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="4940f-171">`.sln`plik</span><span class="sxs-lookup"><span data-stu-id="4940f-171">`.sln` file</span></span> | <span data-ttu-id="4940f-172">Przywracanie pakietów zidentyfikowane przez rozwiązanie; Zwraca błąd, jeśli `-SolutionDirectory` jest używany.</span><span class="sxs-lookup"><span data-stu-id="4940f-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="4940f-173">`$(SolutionDir)\.nuget`jest używana jako folder początkowy.</span><span class="sxs-lookup"><span data-stu-id="4940f-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="4940f-174">`packages.config`lub pliku projektu</span><span class="sxs-lookup"><span data-stu-id="4940f-174">`packages.config` or project file</span></span> | <span data-ttu-id="4940f-175">Przywróć pakiety wymienione w pliku rozwiązania i instalowanie zależności.</span><span class="sxs-lookup"><span data-stu-id="4940f-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="4940f-176">Innego typu pliku</span><span class="sxs-lookup"><span data-stu-id="4940f-176">Other file type</span></span> | <span data-ttu-id="4940f-177">Plik zakłada się, że `.sln` plik jako powyżej; Jeśli nie jest to rozwiązanie zapewnia NuGet błąd.</span><span class="sxs-lookup"><span data-stu-id="4940f-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="4940f-178">(nie określono projectPath)</span><span class="sxs-lookup"><span data-stu-id="4940f-178">(projectPath not specified)</span></span> | <span data-ttu-id="4940f-179">-NuGet wyszukuje pliki rozwiązania w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="4940f-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="4940f-180">Jeśli zostanie znaleziony jeden plik, że jeden służy do przywracania pakietów; w przypadku znalezienia wielu rozwiązań NuGet zawiera błąd.</span><span class="sxs-lookup"><span data-stu-id="4940f-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="4940f-181">— Jeśli nie ma żadnych plików rozwiązania, NuGet szuka `packages.config` i użyty pod kątem przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="4940f-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="4940f-182">— Jeśli żadne rozwiązanie lub `packages.config` plik zostanie znaleziony, NuGet zawiera błąd.</span><span class="sxs-lookup"><span data-stu-id="4940f-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="4940f-183">Określ folder pakietów przy użyciu następującej kolejności priorytet (NuGet zwraca błąd, jeśli żadnego z tych folderów nie są znaleziono):</span><span class="sxs-lookup"><span data-stu-id="4940f-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="4940f-184">Folder określony za pomocą `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="4940f-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="4940f-185">`repositoryPath` Vale w`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="4940f-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="4940f-186">Folder określony za pomocą`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="4940f-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="4940f-187">Trwa przywracanie pakietów dla rozwiązania, NuGet wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4940f-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="4940f-188">Ładuje plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4940f-188">Loads the solution file.</span></span>
    - <span data-ttu-id="4940f-189">Przywraca poziomu pakietów rozwiązania na liście `$(SolutionDir)\.nuget\packages.config` do `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="4940f-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="4940f-190">Przywracanie pakietów na liście `$(ProjectDir)\packages.config` do `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="4940f-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="4940f-191">Dla każdego pakietu określony Przywracanie pakietu równolegle, chyba że `-DisableParallelProcessing` jest określona.</span><span class="sxs-lookup"><span data-stu-id="4940f-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="4940f-192">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4940f-192">Examples</span></span>

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
