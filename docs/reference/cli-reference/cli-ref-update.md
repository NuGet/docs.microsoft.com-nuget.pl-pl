---
title: Polecenie aktualizacji interfejsu wiersza polecenia nuGet
description: Odwołanie do polecenia nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323651"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="131af-103">Polecenie update (interfejs wiersza polecenia nuGet)</span><span class="sxs-lookup"><span data-stu-id="131af-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="131af-104">**Dotyczy: zużycie** pakietu &bullet; **Obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="131af-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="131af-105">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config` ) do ich najnowszych dostępnych wersji.</span><span class="sxs-lookup"><span data-stu-id="131af-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="131af-106">Zaleca się uruchomienie ["przywracania"](cli-ref-restore.md) przed uruchomieniem . `update`</span><span class="sxs-lookup"><span data-stu-id="131af-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="131af-107">(Aby zaktualizować pojedynczy pakiet, użyj bez określania numeru wersji, w takim przypadku [`nuget install`](cli-ref-install.md) nuGet instaluje najnowszą wersję).</span><span class="sxs-lookup"><span data-stu-id="131af-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="131af-108">Uwaga: `update` nie działa z interfejsem wiersza polecenia uruchomionym w programie Mono (Mac OSX lub Linux) ani w przypadku korzystania z formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="131af-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="131af-109">Polecenie `update` aktualizuje również odwołania do zestawu w pliku projektu, o ile te odwołania już istnieją.</span><span class="sxs-lookup"><span data-stu-id="131af-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="131af-110">Jeśli zaktualizowany pakiet ma dodany zestaw, nowe odwołanie nie *jest dodawane.*</span><span class="sxs-lookup"><span data-stu-id="131af-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="131af-111">Nowe zależności pakietów również nie mają dodanych odwołań do zestawu.</span><span class="sxs-lookup"><span data-stu-id="131af-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="131af-112">Aby uwzględnić te operacje w ramach aktualizacji, zaktualizuj pakiet w programie Visual Studio użyciu interfejsu Menedżer pakietów użytkownika lub Menedżer pakietów konsoli programu .</span><span class="sxs-lookup"><span data-stu-id="131af-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="131af-113">To polecenie może również służyć do aktualizowania nuget.exe za pomocą *-self* flag.</span><span class="sxs-lookup"><span data-stu-id="131af-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="131af-114">Użycie</span><span class="sxs-lookup"><span data-stu-id="131af-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="131af-115">gdzie `<configPath>` identyfikuje plik rozwiązania lub , który wyświetla listę zależności `packages.config` projektu.</span><span class="sxs-lookup"><span data-stu-id="131af-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="131af-116">Opcje</span><span class="sxs-lookup"><span data-stu-id="131af-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="131af-117">Plik konfiguracji NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="131af-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="131af-118">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="131af-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="131af-119">Określa wersję pakietów zależności do użycia, która może być jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="131af-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="131af-120">*Najniższa* (domyślna): najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="131af-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="131af-121">*HighestPatch:* wersja z najniższą wersją główną, najmniejszą poprawką pomocniczą, najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="131af-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="131af-122">*HighestMinor:* wersja z najniższą wersją główną, najwyższą poprawką pomocniczą i najwyższą</span><span class="sxs-lookup"><span data-stu-id="131af-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="131af-123">*Najwyższa:* najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="131af-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="131af-124">*Ignoruj:* nie będą używane żadne pakiety zależności</span><span class="sxs-lookup"><span data-stu-id="131af-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="131af-125">Określa domyślną akcję, gdy plik z pakietu już istnieje w projekcie docelowym.</span><span class="sxs-lookup"><span data-stu-id="131af-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="131af-126">Ustawienie na wartość `Overwrite` powoduje, że pliki są zawsze zastępowane.</span><span class="sxs-lookup"><span data-stu-id="131af-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="131af-127">Ustaw na , `Ignore` aby pominąć pliki.</span><span class="sxs-lookup"><span data-stu-id="131af-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="131af-128">Akcja, domyślna, będzie monitować o każdy plik powodujące konflikt, chyba że zostanie podany lub, co będzie `PromptUser` stosowane do wszystkich pozostałych `OverwriteAll` `IgnoreAll` plików.</span><span class="sxs-lookup"><span data-stu-id="131af-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="131af-129">*(3.5+)* Wymusza nuget.exe uruchamiania przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="131af-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="131af-130">Wyświetla informacje pomocy dotyczące polecenia.</span><span class="sxs-lookup"><span data-stu-id="131af-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="131af-131">Określa listę identyfikatorów pakietów do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="131af-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="131af-132">*(4.0+)* Określa ścieżkę msBuild do użycia z poleceniem, pierwszeństwo przed `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="131af-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="131af-133">*(3.2+)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem.</span><span class="sxs-lookup"><span data-stu-id="131af-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="131af-134">Obsługiwane wartości to 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="131af-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="131af-135">Domyślnie jest wybierany program MSBuild w ścieżce. W przeciwnym razie domyślnie jest wybierana najwyższa zainstalowana wersja programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="131af-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="131af-136">Pomija monity o wprowadzenie danych przez użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="131af-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="131af-137">Umożliwia aktualizowanie do wersji wstępnych.</span><span class="sxs-lookup"><span data-stu-id="131af-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="131af-138">Ta flaga nie jest wymagana w przypadku aktualizowania pakietów wstępnych, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="131af-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="131af-139">Określa folder lokalny, w którym są instalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="131af-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="131af-140">Określa, że zostaną zainstalowane tylko aktualizacje z najwyższą wersją dostępną w tej samej wersji główna i pomocnicza, co zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="131af-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="131af-141">Aktualizacje `nuget.exe` do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="131af-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="131af-142">`-Source` można użyć, jednak wszystkie inne argumenty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="131af-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="131af-143">Jeśli nie podano źródła, sprawdza aktualizacje `nuget.org` niezależnie od `NuGet.Config` ustawień.</span><span class="sxs-lookup"><span data-stu-id="131af-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="131af-144">Określa listę źródeł pakietów (jako adresy URL) do użycia na użytek aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="131af-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="131af-145">Jeśli polecenie zostanie pominięte, użyje źródeł podanych w plikach konfiguracji. Zobacz [Typowe konfiguracje NuGet.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="131af-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="131af-146">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (ustawienie domyślne), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="131af-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="131af-147">Gdy jest używany z jednym identyfikatorem pakietu, określa wersję pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="131af-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="131af-148">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="131af-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="131af-149">Przykłady</span><span class="sxs-lookup"><span data-stu-id="131af-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
