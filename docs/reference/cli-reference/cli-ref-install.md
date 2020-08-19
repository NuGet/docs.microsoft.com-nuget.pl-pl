---
title: Polecenie instalacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia instalacji nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623100"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="cc762-103">Install — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="cc762-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="cc762-104">**Dotyczy:** &bullet; **obsługiwane wersje** pakietów: wszystkie</span><span class="sxs-lookup"><span data-stu-id="cc762-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cc762-105">Pobiera i instaluje pakiet w projekcie, domyślnie do bieżącego folderu przy użyciu określonych źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc762-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="cc762-106">Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu w witrynie [NuGet.org](https://www.nuget.org) i wybierz link **pobierania** .</span><span class="sxs-lookup"><span data-stu-id="cc762-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="cc762-107">Jeśli nie określono żadnych źródeł, są używane wymienione w pliku konfiguracji globalnej `%appdata%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="cc762-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="cc762-108">Zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md) , aby uzyskać dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="cc762-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="cc762-109">Jeśli nie określono żadnych określonych pakietów, program `install` zainstaluje wszystkie pakiety wymienione w `packages.config` pliku projektu, co przypomina [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="cc762-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="cc762-110">`install`Polecenie nie modyfikuje pliku projektu lub `packages.config` ; w ten sposób jest podobne do `restore` programu, że tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="cc762-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="cc762-111">Aby dodać zależność, Dodaj pakiet za pomocą interfejsu użytkownika lub konsoli Menedżera pakietów w programie Visual Studio lub zmodyfikuj, `packages.config` a następnie uruchom albo `install` `restore` .</span><span class="sxs-lookup"><span data-stu-id="cc762-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="cc762-112">Użycie</span><span class="sxs-lookup"><span data-stu-id="cc762-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="cc762-113">gdzie `<packageID>` nazywa pakiet, który ma zostać zainstalowany (przy użyciu najnowszej wersji), lub `<configFilePath>` identyfikuje `packages.config` plik, który zawiera listę pakietów do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="cc762-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="cc762-114">Można wskazać określoną wersję z `-Version` opcją.</span><span class="sxs-lookup"><span data-stu-id="cc762-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="cc762-115">Opcje</span><span class="sxs-lookup"><span data-stu-id="cc762-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="cc762-116">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="cc762-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cc762-117">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="cc762-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="cc762-118">*(4.4 +)* Wersja pakietów zależności do użycia, która może być jedną z następujących:</span><span class="sxs-lookup"><span data-stu-id="cc762-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="cc762-119">*Najniższy* (domyślny): najniższa wersja</span><span class="sxs-lookup"><span data-stu-id="cc762-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="cc762-120">*HighestPatch*: wersja z najniższą główną, najmniejszą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="cc762-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="cc762-121">*HighestMinor*: wersja z najmniejszą główną, najwyższą niewielką lub najwyższą poprawką</span><span class="sxs-lookup"><span data-stu-id="cc762-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="cc762-122">*Najwyższa*: najwyższa wersja</span><span class="sxs-lookup"><span data-stu-id="cc762-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="cc762-123">*Ignoruj*: nie będą używane żadne pakiety zależności</span><span class="sxs-lookup"><span data-stu-id="cc762-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="cc762-124">Pobierz bezpośrednio bez wypełniania pamięci podręcznych za pomocą metadanych lub plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="cc762-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="cc762-125">Wyłącza równoczesne Instalowanie wielu pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc762-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="cc762-126">Instaluje pakiet w folderze o nazwie tylko w nazwie pakietu, a nie w numerze wersji.</span><span class="sxs-lookup"><span data-stu-id="cc762-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="cc762-127">*(3.2 +)* Lista źródeł pakietów do użycia jako rezerwy w przypadku, gdy pakiet nie znajduje się w głównym lub domyślnym źródle.</span><span class="sxs-lookup"><span data-stu-id="cc762-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="cc762-128">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="cc762-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="cc762-129">*(4.4 +)* Platforma docelowa używana do wybierania zależności.</span><span class="sxs-lookup"><span data-stu-id="cc762-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="cc762-130">Jeśli nie zostanie określony, wartością domyślną będzie "any".</span><span class="sxs-lookup"><span data-stu-id="cc762-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cc762-131">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="cc762-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="cc762-132">Uniemożliwia narzędziu NuGet używanie buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc762-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="cc762-133">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cc762-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cc762-134">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc762-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="cc762-135">Określa folder, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="cc762-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="cc762-136">Jeśli folder nie zostanie określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="cc762-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="cc762-137">Określa typy plików do zapisania po zainstalowaniu pakietu: jeden z `nuspec` , `nupkg` lub `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="cc762-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="cc762-138">Zezwala na zainstalowanie pakietów wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="cc762-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="cc762-139">Ta flaga nie jest wymagana podczas przywracania pakietów przy użyciu programu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="cc762-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="cc762-140">Sprawdza, czy przywracanie pakietów jest włączone przed pobraniem i zainstalowaniem pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc762-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="cc762-141">Aby uzyskać szczegółowe informacje, zobacz [przywracanie pakietu](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="cc762-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="cc762-142">Określa folder główny rozwiązania, dla którego mają zostać przywrócone pakiety.</span><span class="sxs-lookup"><span data-stu-id="cc762-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="cc762-143">Określa listę źródeł pakietów (jako adresy URL) do użycia.</span><span class="sxs-lookup"><span data-stu-id="cc762-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="cc762-144">W przypadku pominięcia polecenie używa źródeł dostarczonych w plikach konfiguracyjnych, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cc762-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cc762-145">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="cc762-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="cc762-146">Określa wersję pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="cc762-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="cc762-147">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cc762-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cc762-148">Przykłady</span><span class="sxs-lookup"><span data-stu-id="cc762-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
