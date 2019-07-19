---
title: Polecenie aktualizacji interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328256"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="5f3d7-103">update command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="5f3d7-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="5f3d7-104">**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : wszystkie</span><span class="sxs-lookup"><span data-stu-id="5f3d7-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5f3d7-105">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`programu) do ich najnowszych dostępnych wersji.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="5f3d7-106">Zaleca się uruchomienie funkcji ["Restore"](cli-ref-restore.md) przed uruchomieniem `update`narzędzia.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="5f3d7-107">(Aby zaktualizować pojedynczy pakiet, użyj [`nuget install`](cli-ref-install.md) bez określenia numeru wersji, w którym przypadku pakiet NuGet instaluje najnowszą wersję).</span><span class="sxs-lookup"><span data-stu-id="5f3d7-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="5f3d7-108">Uwaga: `update` program nie współpracuje z interfejsem wiersza polecenia w systemie mono (Mac OSX lub Linux) lub w przypadku korzystania z formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="5f3d7-109">`update` Polecenie aktualizuje również odwołania do zestawu w pliku projektu, pod warunkiem, że te odwołania już istnieją.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="5f3d7-110">Jeśli zaktualizowany pakiet ma dodany zestaw, nowe odwołanie *nie* zostanie dodane.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="5f3d7-111">Nowe zależności pakietu nie mają również dodanych odwołań do zestawów.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="5f3d7-112">Aby uwzględnić te operacje w ramach aktualizacji, zaktualizuj pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="5f3d7-113">Tego polecenia można także użyć do zaktualizowania pliku NuGet. exe przy użyciu flagi *-Auto* .</span><span class="sxs-lookup"><span data-stu-id="5f3d7-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="5f3d7-114">Użycie</span><span class="sxs-lookup"><span data-stu-id="5f3d7-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="5f3d7-115">gdzie `<configPath>` identyfikuje`packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="5f3d7-116">Opcje</span><span class="sxs-lookup"><span data-stu-id="5f3d7-116">Options</span></span>

| <span data-ttu-id="5f3d7-117">Opcja</span><span class="sxs-lookup"><span data-stu-id="5f3d7-117">Option</span></span> | <span data-ttu-id="5f3d7-118">Opis</span><span class="sxs-lookup"><span data-stu-id="5f3d7-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f3d7-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5f3d7-119">ConfigFile</span></span> | <span data-ttu-id="5f3d7-120">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5f3d7-121">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5f3d7-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5f3d7-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5f3d7-122">FileConflictAction</span></span> | <span data-ttu-id="5f3d7-123">Określa akcję, która ma zostać podjęta po wyświetleniu monitu o zastąpienie lub zignorowanie istniejących plików, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5f3d7-124">Wartości są *zastępowane, ignorowanie, brak*.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="5f3d7-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5f3d7-125">ForceEnglishOutput</span></span> | <span data-ttu-id="5f3d7-126">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5f3d7-127">Help</span><span class="sxs-lookup"><span data-stu-id="5f3d7-127">Help</span></span> | <span data-ttu-id="5f3d7-128">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="5f3d7-129">Id</span><span class="sxs-lookup"><span data-stu-id="5f3d7-129">Id</span></span> | <span data-ttu-id="5f3d7-130">Określa listę identyfikatorów pakietów do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="5f3d7-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="5f3d7-131">MSBuildPath</span></span> | <span data-ttu-id="5f3d7-132">*(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo `-MSBuildVersion`przed.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="5f3d7-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="5f3d7-133">MSBuildVersion</span></span> | <span data-ttu-id="5f3d7-134">*(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="5f3d7-135">Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="5f3d7-136">Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="5f3d7-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5f3d7-137">NonInteractive</span></span> | <span data-ttu-id="5f3d7-138">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5f3d7-139">Wersja wstępna</span><span class="sxs-lookup"><span data-stu-id="5f3d7-139">PreRelease</span></span> | <span data-ttu-id="5f3d7-140">Umożliwia aktualizację wersji wstępnych.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="5f3d7-141">Ta flaga nie jest wymagana podczas aktualizacji pakietów wersji wstępnej, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="5f3d7-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="5f3d7-142">RepositoryPath</span></span> | <span data-ttu-id="5f3d7-143">Określa folder lokalny, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="5f3d7-144">Sejf</span><span class="sxs-lookup"><span data-stu-id="5f3d7-144">Safe</span></span> | <span data-ttu-id="5f3d7-145">Określa, że zostaną zainstalowane tylko aktualizacje o najwyższej wersji dostępnej w ramach tej samej wersji głównej i pomocniczej co zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="5f3d7-146">Automatycznej</span><span class="sxs-lookup"><span data-stu-id="5f3d7-146">Self</span></span> | <span data-ttu-id="5f3d7-147">Aktualizuje plik NuGet. exe do najnowszej wersji; wszystkie pozostałe argumenty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="5f3d7-148">Source</span><span class="sxs-lookup"><span data-stu-id="5f3d7-148">Source</span></span> | <span data-ttu-id="5f3d7-149">Określa listę źródeł pakietów (jako adresy URL), które mają być używane na potrzeby aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="5f3d7-150">W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5f3d7-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="5f3d7-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5f3d7-151">Verbosity</span></span> | <span data-ttu-id="5f3d7-152">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="5f3d7-153">Wersja</span><span class="sxs-lookup"><span data-stu-id="5f3d7-153">Version</span></span> | <span data-ttu-id="5f3d7-154">W przypadku użycia z jednym IDENTYFIKATORem pakietu określa wersję pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="5f3d7-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="5f3d7-155">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5f3d7-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5f3d7-156">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5f3d7-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
