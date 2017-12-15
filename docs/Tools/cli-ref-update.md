---
title: Polecenie Uaktualnij interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Informacje dotyczące polecenia update nuget.exe"
keywords: "Odwołanie do aktualizacji nuget, polecenie pakietu aktualizacji"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="31592-104">polecenie aktualizacji (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="31592-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="31592-105">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="31592-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="31592-106">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do ich najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="31592-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="31592-107">Zalecane jest uruchomienie ["Przywracanie"](#restore) przed uruchomieniem `update`.</span><span class="sxs-lookup"><span data-stu-id="31592-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="31592-108">(Aby poszczególnych pakiet aktualizacji, należy użyć [ `nuget install` ](cli-ref-install.md) bez określania numeru wersji, w których wielkość NuGet instaluje najnowszą wersję.)</span><span class="sxs-lookup"><span data-stu-id="31592-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="31592-109">Uwaga: `update` nie działa z poziomu interfejsu wiersza polecenia do uruchamiania Mono (Mac OS x lub Linux).</span><span class="sxs-lookup"><span data-stu-id="31592-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="31592-110">Polecenie również nie działa z projektami za pomocą `project.json` lub PackageReference zarządzania formatów.</span><span class="sxs-lookup"><span data-stu-id="31592-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="31592-111">`update` Polecenie aktualizuje również odwołania do zestawów w pliku projektu, pod warunkiem tych odwołuje się do już istnieje.</span><span class="sxs-lookup"><span data-stu-id="31592-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="31592-112">Jeśli zaktualizowany pakiet został dodany zestaw, jest nowe odwołanie *nie* dodane.</span><span class="sxs-lookup"><span data-stu-id="31592-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="31592-113">Nowe zależności pakietów również nie ma ich dodać odwołania do zestawów.</span><span class="sxs-lookup"><span data-stu-id="31592-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="31592-114">Aby uwzględnić te operacje w ramach aktualizacji, należy zaktualizować pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="31592-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="31592-115">To polecenie można także zaktualizować nuget.exe się przy użyciu *-self* flagi.</span><span class="sxs-lookup"><span data-stu-id="31592-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="31592-116">Użycie</span><span class="sxs-lookup"><span data-stu-id="31592-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="31592-117">gdzie `<configPath>` identyfikuje albo `packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="31592-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="31592-118">Opcje</span><span class="sxs-lookup"><span data-stu-id="31592-118">Options</span></span>

| <span data-ttu-id="31592-119">Opcja</span><span class="sxs-lookup"><span data-stu-id="31592-119">Option</span></span> | <span data-ttu-id="31592-120">Opis</span><span class="sxs-lookup"><span data-stu-id="31592-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31592-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="31592-121">ConfigFile</span></span> | <span data-ttu-id="31592-122">*(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="31592-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="31592-123">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="31592-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="31592-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="31592-124">FileConflictAction</span></span> | <span data-ttu-id="31592-125">*(2.5 +)*  Określa akcję wykonywaną po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="31592-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="31592-126">Wartości są *zastępowania, zignorować, Brak*.</span><span class="sxs-lookup"><span data-stu-id="31592-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="31592-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="31592-127">ForceEnglishOutput</span></span> | <span data-ttu-id="31592-128">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="31592-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="31592-129">Pomoc</span><span class="sxs-lookup"><span data-stu-id="31592-129">Help</span></span> | <span data-ttu-id="31592-130">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="31592-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="31592-131">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="31592-131">Id</span></span> | <span data-ttu-id="31592-132">Określa listę identyfikatorów do zaktualizowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="31592-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="31592-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="31592-133">MSBuildPath</span></span> | <span data-ttu-id="31592-134">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="31592-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="31592-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="31592-135">MSBuildVersion</span></span> | <span data-ttu-id="31592-136">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="31592-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="31592-137">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="31592-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="31592-138">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="31592-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="31592-139">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="31592-139">NonInteractive</span></span> | <span data-ttu-id="31592-140">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="31592-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="31592-141">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="31592-141">PreRelease</span></span> | <span data-ttu-id="31592-142">Umożliwia aktualizacji do wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="31592-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="31592-143">Ta flaga nie jest wymagana podczas aktualizowania pakiety wersji wstępnej, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="31592-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="31592-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="31592-144">RepositoryPath</span></span> | <span data-ttu-id="31592-145">Określa folder lokalny, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="31592-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="31592-146">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="31592-146">Safe</span></span> | <span data-ttu-id="31592-147">Określa, że tylko aktualizacje o najwyższej dostępne w ramach tej samej wersji głównej i pomocniczej wersji zgodnie z zainstalowanym pakietem zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="31592-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="31592-148">Samodzielnie</span><span class="sxs-lookup"><span data-stu-id="31592-148">Self</span></span> | <span data-ttu-id="31592-149">*(1.4 +)*  Aktualizacji do najnowszej wersji; nuget.exe inne argumenty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="31592-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="31592-150">Źródło</span><span class="sxs-lookup"><span data-stu-id="31592-150">Source</span></span> | <span data-ttu-id="31592-151">Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="31592-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="31592-152">W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="31592-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="31592-153">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="31592-153">Verbosity</span></span> | <span data-ttu-id="31592-154">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="31592-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="31592-155">Wersja</span><span class="sxs-lookup"><span data-stu-id="31592-155">Version</span></span> | <span data-ttu-id="31592-156">W przypadku użycia z jeden identyfikator pakietu, określa wersję pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="31592-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="31592-157">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="31592-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="31592-158">Przykłady</span><span class="sxs-lookup"><span data-stu-id="31592-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
