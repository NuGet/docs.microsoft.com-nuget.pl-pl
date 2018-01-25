---
title: Polecenie instalowania NuGet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Dokumentacja dla polecenia install nuget.exe
keywords: "nuget zainstalować odwołania, należy zainstalować pakiet polecenia"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b77e0e6ce045d1a1e59b29f770b5aca13fc4e7e3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="c6e98-104">Zainstaluj polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c6e98-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="c6e98-105">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="c6e98-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c6e98-106">Pobiera i instaluje pakiet w projekcie, domyślnie używany do bieżącego folderu przy użyciu określonego pakietu źródeł.</span><span class="sxs-lookup"><span data-stu-id="c6e98-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="c6e98-107">Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu na [nuget.org](https://www.nuget.org) i wybierz **Pobierz** łącza.</span><span class="sxs-lookup"><span data-stu-id="c6e98-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="c6e98-108">Jeśli nie określono żadnych źródeł, wymienione w pliku konfigurację globalną `%APPDATA%\NuGet\NuGet.Config`, są używane.</span><span class="sxs-lookup"><span data-stu-id="c6e98-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="c6e98-109">Zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md) dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="c6e98-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="c6e98-110">Jeśli nie określono żadnych określonych pakietów, `install` instaluje wszystkie pakiety wymienione w projekcie `packages.config` plików, dzięki czemu podobny do [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="c6e98-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="c6e98-111">`install` Polecenia nie modyfikuje plik projektu lub `packages.config`; w ten sposób jest podobna do `restore` w tym go tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="c6e98-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="c6e98-112">Aby dodać zależność, Dodaj projekt za pomocą Menedżera pakietów interfejsu użytkownika lub konsoli w programie Visual Studio lub zmodyfikować `packages.config` , a następnie uruchom albo `install` lub `restore`.</span><span class="sxs-lookup"><span data-stu-id="c6e98-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="c6e98-113">Użycie</span><span class="sxs-lookup"><span data-stu-id="c6e98-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="c6e98-114">gdzie `<packageID>` nazwy pakietu do zainstalowania (przy użyciu najnowszej wersji,) lub `<configFilePath>` identyfikuje `packages.config` plik zawierający listę pakietów do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="c6e98-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="c6e98-115">Można wskazać określoną wersję z `-Version` opcji.</span><span class="sxs-lookup"><span data-stu-id="c6e98-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="c6e98-116">Opcje</span><span class="sxs-lookup"><span data-stu-id="c6e98-116">Options</span></span>

| <span data-ttu-id="c6e98-117">Opcja</span><span class="sxs-lookup"><span data-stu-id="c6e98-117">Option</span></span> | <span data-ttu-id="c6e98-118">Opis</span><span class="sxs-lookup"><span data-stu-id="c6e98-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6e98-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c6e98-119">ConfigFile</span></span> | <span data-ttu-id="c6e98-120">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="c6e98-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c6e98-121">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="c6e98-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="c6e98-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="c6e98-122">DependencyVersion</span></span> | <span data-ttu-id="c6e98-123">*(4.4 +)*  Określa określonej wersji, Zastępowanie domyślnego zachowania rozpoznawania zależności.</span><span class="sxs-lookup"><span data-stu-id="c6e98-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="c6e98-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="c6e98-124">DisableParallelProcessing</span></span> | <span data-ttu-id="c6e98-125">Wyłącza równolegle wielu pakietów.</span><span class="sxs-lookup"><span data-stu-id="c6e98-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="c6e98-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="c6e98-126">ExcludeVersion</span></span> | <span data-ttu-id="c6e98-127">Instaluje pakiet do folderu o nazwie z tylko nazwę pakietu i nie numer wersji.</span><span class="sxs-lookup"><span data-stu-id="c6e98-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="c6e98-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="c6e98-128">FallbackSource</span></span> | <span data-ttu-id="c6e98-129">*(3.2 +)*  Lista źródła pakietów do użycia jako przejścia, w przypadku, gdy nie można znaleźć pakietu w podstawowej lub źródło domyślne.</span><span class="sxs-lookup"><span data-stu-id="c6e98-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="c6e98-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c6e98-130">ForceEnglishOutput</span></span> | <span data-ttu-id="c6e98-131">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="c6e98-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c6e98-132">Framework</span><span class="sxs-lookup"><span data-stu-id="c6e98-132">Framework</span></span> | <span data-ttu-id="c6e98-133">*(4.4 +)*  Platformy docelowej służy do wybierania zależności.</span><span class="sxs-lookup"><span data-stu-id="c6e98-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="c6e98-134">Wartość domyślna to "Any" Jeśli nie zostanie określony.</span><span class="sxs-lookup"><span data-stu-id="c6e98-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="c6e98-135">Pomoc</span><span class="sxs-lookup"><span data-stu-id="c6e98-135">Help</span></span> | <span data-ttu-id="c6e98-136">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6e98-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="c6e98-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="c6e98-137">NoCache</span></span> | <span data-ttu-id="c6e98-138">Zapobiega z pamięci podręcznej komputera lokalnego za pomocą pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="c6e98-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="c6e98-139">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="c6e98-139">NonInteractive</span></span> | <span data-ttu-id="c6e98-140">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="c6e98-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c6e98-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="c6e98-141">OutputDirectory</span></span> | <span data-ttu-id="c6e98-142">Określa folder, w którym są zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="c6e98-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="c6e98-143">Jeśli folder nie jest określony, używany jest bieżący folder.</span><span class="sxs-lookup"><span data-stu-id="c6e98-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="c6e98-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="c6e98-144">PackageSaveMode</span></span> | <span data-ttu-id="c6e98-145">Określa typy plików, aby zapisać po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="c6e98-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="c6e98-146">Wydanie wstępne</span><span class="sxs-lookup"><span data-stu-id="c6e98-146">PreRelease</span></span> | <span data-ttu-id="c6e98-147">Zezwala na pakiety wersji wstępnej do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="c6e98-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="c6e98-148">Ta flaga nie jest wymagana, gdy trwa przywracanie pakietów z `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c6e98-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="c6e98-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="c6e98-149">RequireConsent</span></span> | <span data-ttu-id="c6e98-150">Sprawdza, czy Przywracanie pakietów jest włączona przed pobierania i instalowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c6e98-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="c6e98-151">Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="c6e98-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="c6e98-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="c6e98-152">SolutionDirectory</span></span> | <span data-ttu-id="c6e98-153">Określa folder główny rozwiązaniu, dla których pod kątem przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c6e98-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="c6e98-154">Źródło</span><span class="sxs-lookup"><span data-stu-id="c6e98-154">Source</span></span> | <span data-ttu-id="c6e98-155">Określa listę źródła pakietu (jako adresy URL).</span><span class="sxs-lookup"><span data-stu-id="c6e98-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="c6e98-156">W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c6e98-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="c6e98-157">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="c6e98-157">Verbosity</span></span> | <span data-ttu-id="c6e98-158">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="c6e98-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="c6e98-159">Wersja</span><span class="sxs-lookup"><span data-stu-id="c6e98-159">Version</span></span> | <span data-ttu-id="c6e98-160">Określa wersję pakietu do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="c6e98-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="c6e98-161">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c6e98-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c6e98-162">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c6e98-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
