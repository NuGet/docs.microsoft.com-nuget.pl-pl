---
title: Polecenie aktualizacji interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia update nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="2246d-103">update command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="2246d-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="2246d-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="2246d-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2246d-105">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do ich najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="2246d-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="2246d-106">Zalecane jest uruchomienie ["Przywracanie"](cli-ref-restore.md) przed uruchomieniem `update`.</span><span class="sxs-lookup"><span data-stu-id="2246d-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="2246d-107">(Aby poszczególnych pakiet aktualizacji, należy użyć [ `nuget install` ](cli-ref-install.md) bez określania numeru wersji, w których wielkość NuGet instaluje najnowszą wersję.)</span><span class="sxs-lookup"><span data-stu-id="2246d-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="2246d-108">Uwaga: `update` nie działa z systemem w obszarze Mono (Mac OS x lub Linux) lub gdy w formacie PackageReference interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2246d-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="2246d-109">`update` Polecenie aktualizuje również odwołania do zestawów w pliku projektu, pod warunkiem tych odwołuje się do już istnieje.</span><span class="sxs-lookup"><span data-stu-id="2246d-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="2246d-110">Jeśli zaktualizowany pakiet został dodany zestaw, jest nowe odwołanie *nie* dodane.</span><span class="sxs-lookup"><span data-stu-id="2246d-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="2246d-111">Nowe zależności pakietów również nie ma ich dodać odwołania do zestawów.</span><span class="sxs-lookup"><span data-stu-id="2246d-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="2246d-112">Aby uwzględnić te operacje w ramach aktualizacji, należy zaktualizować pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2246d-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="2246d-113">To polecenie można także zaktualizować nuget.exe się przy użyciu *-self* flagi.</span><span class="sxs-lookup"><span data-stu-id="2246d-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="2246d-114">Użycie</span><span class="sxs-lookup"><span data-stu-id="2246d-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="2246d-115">gdzie `<configPath>` identyfikuje albo `packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="2246d-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="2246d-116">Opcje</span><span class="sxs-lookup"><span data-stu-id="2246d-116">Options</span></span>

| <span data-ttu-id="2246d-117">Opcja</span><span class="sxs-lookup"><span data-stu-id="2246d-117">Option</span></span> | <span data-ttu-id="2246d-118">Opis</span><span class="sxs-lookup"><span data-stu-id="2246d-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2246d-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2246d-119">ConfigFile</span></span> | <span data-ttu-id="2246d-120">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="2246d-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2246d-121">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="2246d-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2246d-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="2246d-122">FileConflictAction</span></span> | <span data-ttu-id="2246d-123">Określa akcję wykonywaną po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="2246d-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="2246d-124">Wartości są *zastępowania, zignorować, Brak*.</span><span class="sxs-lookup"><span data-stu-id="2246d-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="2246d-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2246d-125">ForceEnglishOutput</span></span> | <span data-ttu-id="2246d-126">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="2246d-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2246d-127">Pomoc</span><span class="sxs-lookup"><span data-stu-id="2246d-127">Help</span></span> | <span data-ttu-id="2246d-128">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="2246d-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="2246d-129">Id</span><span class="sxs-lookup"><span data-stu-id="2246d-129">Id</span></span> | <span data-ttu-id="2246d-130">Określa listę identyfikatorów do zaktualizowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="2246d-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="2246d-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="2246d-131">MSBuildPath</span></span> | <span data-ttu-id="2246d-132">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="2246d-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="2246d-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="2246d-133">MSBuildVersion</span></span> | <span data-ttu-id="2246d-134">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="2246d-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="2246d-135">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="2246d-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="2246d-136">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="2246d-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="2246d-137">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="2246d-137">NonInteractive</span></span> | <span data-ttu-id="2246d-138">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="2246d-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2246d-139">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="2246d-139">PreRelease</span></span> | <span data-ttu-id="2246d-140">Umożliwia aktualizacji do wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="2246d-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="2246d-141">Ta flaga nie jest wymagana podczas aktualizowania pakiety wersji wstępnej, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="2246d-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="2246d-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="2246d-142">RepositoryPath</span></span> | <span data-ttu-id="2246d-143">Określa folder lokalny, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="2246d-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="2246d-144">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="2246d-144">Safe</span></span> | <span data-ttu-id="2246d-145">Określa, że tylko aktualizacje o najwyższej dostępne w ramach tej samej wersji głównej i pomocniczej wersji zgodnie z zainstalowanym pakietem zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="2246d-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="2246d-146">Samodzielnie</span><span class="sxs-lookup"><span data-stu-id="2246d-146">Self</span></span> | <span data-ttu-id="2246d-147">Nuget.exe aktualizacji do najnowszej wersji; wszystkie inne argumenty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="2246d-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="2246d-148">Źródło</span><span class="sxs-lookup"><span data-stu-id="2246d-148">Source</span></span> | <span data-ttu-id="2246d-149">Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="2246d-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="2246d-150">W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2246d-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="2246d-151">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="2246d-151">Verbosity</span></span> | <span data-ttu-id="2246d-152">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="2246d-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="2246d-153">Wersja</span><span class="sxs-lookup"><span data-stu-id="2246d-153">Version</span></span> | <span data-ttu-id="2246d-154">W przypadku użycia z jeden identyfikator pakietu, określa wersję pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="2246d-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="2246d-155">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2246d-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2246d-156">Przykłady</span><span class="sxs-lookup"><span data-stu-id="2246d-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
