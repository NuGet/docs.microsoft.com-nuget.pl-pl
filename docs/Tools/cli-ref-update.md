---
title: Polecenie Uaktualnij interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Informacje dotyczące polecenia update nuget.exe"
keywords: "Odwołanie do aktualizacji nuget, polecenie pakietu aktualizacji"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a788244d23354b980e8fa86fa170740c18f17b2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="5eb69-104">polecenie aktualizacji (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5eb69-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="5eb69-105">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="5eb69-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5eb69-106">Aktualizuje wszystkie pakiety w projekcie (przy użyciu `packages.config`) do ich najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="5eb69-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="5eb69-107">Zalecane jest uruchomienie ["Przywracanie"](cli-ref-restore.md) przed uruchomieniem `update`.</span><span class="sxs-lookup"><span data-stu-id="5eb69-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="5eb69-108">(Aby poszczególnych pakiet aktualizacji, należy użyć [ `nuget install` ](cli-ref-install.md) bez określania numeru wersji, w których wielkość NuGet instaluje najnowszą wersję.)</span><span class="sxs-lookup"><span data-stu-id="5eb69-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="5eb69-109">Uwaga: `update` nie działa z systemem w obszarze Mono (Mac OS x lub Linux) lub gdy w formacie PackageReference interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5eb69-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="5eb69-110">`update` Polecenie aktualizuje również odwołania do zestawów w pliku projektu, pod warunkiem tych odwołuje się do już istnieje.</span><span class="sxs-lookup"><span data-stu-id="5eb69-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="5eb69-111">Jeśli zaktualizowany pakiet został dodany zestaw, jest nowe odwołanie *nie* dodane.</span><span class="sxs-lookup"><span data-stu-id="5eb69-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="5eb69-112">Nowe zależności pakietów również nie ma ich dodać odwołania do zestawów.</span><span class="sxs-lookup"><span data-stu-id="5eb69-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="5eb69-113">Aby uwzględnić te operacje w ramach aktualizacji, należy zaktualizować pakiet w programie Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5eb69-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="5eb69-114">To polecenie można także zaktualizować nuget.exe się przy użyciu *-self* flagi.</span><span class="sxs-lookup"><span data-stu-id="5eb69-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="5eb69-115">Użycie</span><span class="sxs-lookup"><span data-stu-id="5eb69-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="5eb69-116">gdzie `<configPath>` identyfikuje albo `packages.config` lub plik rozwiązania, który zawiera listę zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="5eb69-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="5eb69-117">Opcje</span><span class="sxs-lookup"><span data-stu-id="5eb69-117">Options</span></span>

| <span data-ttu-id="5eb69-118">Opcja</span><span class="sxs-lookup"><span data-stu-id="5eb69-118">Option</span></span> | <span data-ttu-id="5eb69-119">Opis</span><span class="sxs-lookup"><span data-stu-id="5eb69-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5eb69-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5eb69-120">ConfigFile</span></span> | <span data-ttu-id="5eb69-121">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="5eb69-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5eb69-122">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="5eb69-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="5eb69-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5eb69-123">FileConflictAction</span></span> | <span data-ttu-id="5eb69-124">Określa akcję wykonywaną po otrzymaniu monitu, aby zastąpić, lub przycisk Ignoruj istniejące pliki odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="5eb69-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5eb69-125">Wartości są *zastępowania, zignorować, Brak*.</span><span class="sxs-lookup"><span data-stu-id="5eb69-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="5eb69-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5eb69-126">ForceEnglishOutput</span></span> | <span data-ttu-id="5eb69-127">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="5eb69-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5eb69-128">Pomoc</span><span class="sxs-lookup"><span data-stu-id="5eb69-128">Help</span></span> | <span data-ttu-id="5eb69-129">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="5eb69-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="5eb69-130">Id</span><span class="sxs-lookup"><span data-stu-id="5eb69-130">Id</span></span> | <span data-ttu-id="5eb69-131">Określa listę identyfikatorów do zaktualizowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="5eb69-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="5eb69-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="5eb69-132">MSBuildPath</span></span> | <span data-ttu-id="5eb69-133">*(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="5eb69-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="5eb69-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="5eb69-134">MSBuildVersion</span></span> | <span data-ttu-id="5eb69-135">*(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="5eb69-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="5eb69-136">Obsługiwane wartości to 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="5eb69-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="5eb69-137">Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5eb69-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="5eb69-138">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="5eb69-138">NonInteractive</span></span> | <span data-ttu-id="5eb69-139">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="5eb69-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5eb69-140">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="5eb69-140">PreRelease</span></span> | <span data-ttu-id="5eb69-141">Umożliwia aktualizacji do wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="5eb69-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="5eb69-142">Ta flaga nie jest wymagana podczas aktualizowania pakiety wersji wstępnej, które są już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="5eb69-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="5eb69-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="5eb69-143">RepositoryPath</span></span> | <span data-ttu-id="5eb69-144">Określa folder lokalny, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="5eb69-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="5eb69-145">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="5eb69-145">Safe</span></span> | <span data-ttu-id="5eb69-146">Określa, że tylko aktualizacje o najwyższej dostępne w ramach tej samej wersji głównej i pomocniczej wersji zgodnie z zainstalowanym pakietem zostanie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="5eb69-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="5eb69-147">Samodzielnie</span><span class="sxs-lookup"><span data-stu-id="5eb69-147">Self</span></span> | <span data-ttu-id="5eb69-148">Nuget.exe aktualizacji do najnowszej wersji; wszystkie inne argumenty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="5eb69-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="5eb69-149">Źródło</span><span class="sxs-lookup"><span data-stu-id="5eb69-149">Source</span></span> | <span data-ttu-id="5eb69-150">Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5eb69-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="5eb69-151">W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5eb69-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="5eb69-152">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="5eb69-152">Verbosity</span></span> | <span data-ttu-id="5eb69-153">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="5eb69-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="5eb69-154">Wersja</span><span class="sxs-lookup"><span data-stu-id="5eb69-154">Version</span></span> | <span data-ttu-id="5eb69-155">W przypadku użycia z jeden identyfikator pakietu, określa wersję pakietu do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="5eb69-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="5eb69-156">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5eb69-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5eb69-157">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5eb69-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
