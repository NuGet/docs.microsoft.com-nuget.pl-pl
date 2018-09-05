---
title: Interfejs wiersza polecenia NuGet polecenia update
description: Dokumentacja dotycząca polecenia update nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc34550b3669d83466318645987cfd3078bc3c18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545103"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="12f18-103">update command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="12f18-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="12f18-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="12f18-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="12f18-105">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do jego najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="12f18-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="12f18-106">Zaleca się uruchomienie ["restore"](cli-ref-restore.md) przed uruchomieniem `update`.</span><span class="sxs-lookup"><span data-stu-id="12f18-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="12f18-107">(Aby zaktualizować poszczególnych pakietów, użyj [ `nuget install` ](cli-ref-install.md) bez określania numeru wersji, w którym wielkość NuGet instaluje najnowszą wersję.)</span><span class="sxs-lookup"><span data-stu-id="12f18-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="12f18-108">Uwaga: `update` nie działa z interfejsem wiersza polecenia, uruchomione w Mono (Mac OS x lub Linux) lub przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="12f18-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="12f18-109">`update` Polecenie aktualizuje również odwołania do zestawu w pliku projektu, pod warunkiem tych odwołuje się już istnieje.</span><span class="sxs-lookup"><span data-stu-id="12f18-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="12f18-110">Jeśli dodano zestaw zaktualizowany pakiet, nowe odwołanie jest *nie* dodane.</span><span class="sxs-lookup"><span data-stu-id="12f18-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="12f18-111">Nowe zależności pakietu nie ma również ich dodać odwołania do zestawu.</span><span class="sxs-lookup"><span data-stu-id="12f18-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="12f18-112">Aby uwzględnić te operacje w ramach aktualizacji, należy zaktualizować pakiet w programie Visual Studio za pomocą interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="12f18-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="12f18-113">To polecenie można również zaktualizować nuget.exe się przy użyciu *-self* flagi.</span><span class="sxs-lookup"><span data-stu-id="12f18-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="12f18-114">Użycie</span><span class="sxs-lookup"><span data-stu-id="12f18-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="12f18-115">gdzie `<configPath>` identyfikuje albo `packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="12f18-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="12f18-116">Opcje</span><span class="sxs-lookup"><span data-stu-id="12f18-116">Options</span></span>

| <span data-ttu-id="12f18-117">Opcja</span><span class="sxs-lookup"><span data-stu-id="12f18-117">Option</span></span> | <span data-ttu-id="12f18-118">Opis</span><span class="sxs-lookup"><span data-stu-id="12f18-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12f18-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="12f18-119">ConfigFile</span></span> | <span data-ttu-id="12f18-120">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="12f18-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="12f18-121">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="12f18-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="12f18-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="12f18-122">FileConflictAction</span></span> | <span data-ttu-id="12f18-123">Określa akcję wykonywaną po wyświetleniu monitu o zastąpienie lub zignorować istniejące pliki przywoływanego przez projekt.</span><span class="sxs-lookup"><span data-stu-id="12f18-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="12f18-124">Wartości są *zastąpić, Ignoruj Brak*.</span><span class="sxs-lookup"><span data-stu-id="12f18-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="12f18-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="12f18-125">ForceEnglishOutput</span></span> | <span data-ttu-id="12f18-126">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="12f18-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="12f18-127">Pomoc</span><span class="sxs-lookup"><span data-stu-id="12f18-127">Help</span></span> | <span data-ttu-id="12f18-128">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="12f18-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="12f18-129">Id</span><span class="sxs-lookup"><span data-stu-id="12f18-129">Id</span></span> | <span data-ttu-id="12f18-130">Określa listę identyfikatorów, aby zaktualizować pakiet.</span><span class="sxs-lookup"><span data-stu-id="12f18-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="12f18-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="12f18-131">MSBuildPath</span></span> | <span data-ttu-id="12f18-132">*(4.0 +)*  Określa ścieżkę program MSBuild będzie używać za pomocą polecenia pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="12f18-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="12f18-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="12f18-133">MSBuildVersion</span></span> | <span data-ttu-id="12f18-134">*(3.2 +)*  Określa numer wersji MSBuild ma być używany za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="12f18-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="12f18-135">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="12f18-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="12f18-136">Domyślnie program MSBuild w ścieżce jest pobierana w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="12f18-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="12f18-137">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="12f18-137">NonInteractive</span></span> | <span data-ttu-id="12f18-138">Wyłącza monity dotyczące danych wejściowych użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="12f18-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="12f18-139">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="12f18-139">PreRelease</span></span> | <span data-ttu-id="12f18-140">Zezwala na aktualizację do wersji wstępnych.</span><span class="sxs-lookup"><span data-stu-id="12f18-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="12f18-141">Ta flaga nie jest wymagana podczas aktualizowania pakietów wydań wstępnych, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="12f18-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="12f18-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="12f18-142">RepositoryPath</span></span> | <span data-ttu-id="12f18-143">Określa folder lokalny, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="12f18-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="12f18-144">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="12f18-144">Safe</span></span> | <span data-ttu-id="12f18-145">Określa, która aktualizuje tylko z najwyższą wersją dostępne w ramach tej samej wersji głównych i pomocniczych zgodnie z zainstalowanym pakietem zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="12f18-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="12f18-146">Samodzielna</span><span class="sxs-lookup"><span data-stu-id="12f18-146">Self</span></span> | <span data-ttu-id="12f18-147">Nuget.exe aktualizacji do najnowszej wersji; wszystkie inne argumenty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="12f18-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="12f18-148">Źródło</span><span class="sxs-lookup"><span data-stu-id="12f18-148">Source</span></span> | <span data-ttu-id="12f18-149">Określa listę źródeł pakietów (jako adresy URL) na potrzeby aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="12f18-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="12f18-150">Jeśli argument jest pominięty, polecenie używa źródeł dostarczane w plikach konfiguracyjnych, zobacz [zachowania programu NuGet Konfigurowanie](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="12f18-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="12f18-151">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="12f18-151">Verbosity</span></span> | <span data-ttu-id="12f18-152">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="12f18-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="12f18-153">Wersja</span><span class="sxs-lookup"><span data-stu-id="12f18-153">Version</span></span> | <span data-ttu-id="12f18-154">W przypadku użycia z jednym Identyfikatorem pakietu, określa wersję pakiet do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="12f18-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="12f18-155">Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="12f18-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="12f18-156">Przykłady</span><span class="sxs-lookup"><span data-stu-id="12f18-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
