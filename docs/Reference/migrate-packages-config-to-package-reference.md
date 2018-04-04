---
title: Migrowanie z package.config do formatów PackageReference | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Więcej informacji na temat migracji projektu z formatu zarządzania package.config do PackageReference obsługiwana przez NuGet 4.0 + i VS2017 i .NET Core 2.0
keywords: NuGet migrator migracji, odwołania do pakietu, projektu packages.config pliki, PackageReference, VS2017, Visual Studio 2017 r, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="9a0a3-104">Migracja z pliku packages.config do PackageReference</span><span class="sxs-lookup"><span data-stu-id="9a0a3-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="9a0a3-105">Visual Studio 2017 wersji 15.7 Preview 3 i nowsze wersje obsługują migracji projektu z [packages.config](./packages-config.md) format zarządzania [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="9a0a3-106">Korzyści wynikające ze stosowania PackageReference</span><span class="sxs-lookup"><span data-stu-id="9a0a3-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="9a0a3-107">**Zarządzanie wszystkie zależności projektu w jednym miejscu**: Podobnie jak odwołań projektów i odwołania do zestawów odwołuje się do pakietu NuGet (przy użyciu `PackageReference` węzła) są zarządzane bezpośrednio w ramach plików projektu, zamiast używać oddzielnego pliku Packages.config.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="9a0a3-108">**Widok ikonami najwyższego poziomu zależności**: w przeciwieństwie do pliku packages.config, PackageReference wyświetla tylko te pakiety NuGet, które są bezpośrednio zainstalowanych w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="9a0a3-109">W związku z tym interfejsu użytkownika Menedżera pakietów NuGet i plik projektu nie ma elementów z zależnościami niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="9a0a3-110">**Ulepszenia wydajności**: używając PackageReference pakiety są obsługiwane w *globalne pakietów* folder (zgodnie z opisem na [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md) zamiast w `packages` folderu w ramach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="9a0a3-111">W związku z tym PackageReference wykonuje szybciej i zajmuje mniej miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="9a0a3-112">**Drobne kontrolę nad zależności i zawartości przepływu**: istniejące funkcje programu MSBuild umożliwia [warunkowo odwołują się do pakietu NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) i wybierz polecenie odwołania do pakietu dla platformy docelowej, konfiguracji, Platforma lub innych przestawień.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="9a0a3-113">**PackageReference jest w fazie projektowania active**: zobacz [PackageReference problemów w serwisie GitHub](https://aka.ms/nuget-pr-improvements).</span><span class="sxs-lookup"><span data-stu-id="9a0a3-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="9a0a3-114">Packages.config nie jest już opracowywane aktywne.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="9a0a3-115">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="9a0a3-115">Limitations</span></span>

* <span data-ttu-id="9a0a3-116">NuGet PackageReference nie jest dostępne w programie Visual Studio 2015 lub starszym.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="9a0a3-117">Zmigrowane projekty można otwierać tylko w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="9a0a3-118">Migracja nie jest obecnie dostępne dla projektów C++ i platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="9a0a3-119">Niektóre pakiety nie może być całkowicie zgodne z PackageReference.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="9a0a3-120">Aby uzyskać więcej informacji, zobacz [pakietu problemy ze zgodnością](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="9a0a3-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="9a0a3-121">Kroki migracji</span><span class="sxs-lookup"><span data-stu-id="9a0a3-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="9a0a3-122">Przed rozpoczęciem migracji programu Visual Studio tworzona jest kopia zapasowa projektu, co pozwala na [: Przywracanie pliku packages.config](#how-to-roll-back-to-packagesconfig) w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="9a0a3-123">Otwórz rozwiązanie zawierające projekt za pomocą `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="9a0a3-124">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **odwołania** węzła lub `packages.config` plik i wybierz **migracji pliku packages.config do PackageReference...** .</span><span class="sxs-lookup"><span data-stu-id="9a0a3-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="9a0a3-125">Migrator analizuje odwołania do pakietu NuGet projektu i próbuje przeprowadzić ich do skategoryzowania **najwyższego poziomu zależności** (ten katalog można zainstalować pakietów NuGet) i **przechodnie zależności**(pakiety, które zostały zainstalowane jako zależności pakietów najwyższego poziomu).</span><span class="sxs-lookup"><span data-stu-id="9a0a3-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="9a0a3-126">PackageReference obsługuje Przywracanie pakietu przechodnie i jest rozpoznawany jako zależności dynamicznie, co oznacza przechodnie zależności muszą nie zainstalowania jawnie.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="9a0a3-127">(Opcjonalnie) Możesz traktować pakietu NuGet sklasyfikowane jako zależność przechodnie jako zależność najwyższego poziomu, wybierając **najwyższego poziomu** opcją dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="9a0a3-128">Ta opcja jest automatycznie ustawiana pakiety zawierające zasoby, które nie wpływają przechodnie (w `build`, `buildCrossTargeting`, `contentFiles`, lub `analyzers` folderów) i tymi oznaczony jako zależność Programowanie (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="9a0a3-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="9a0a3-129">Przejrzyj wszelkie [pakietu problemy ze zgodnością](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="9a0a3-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="9a0a3-130">Wybierz **OK** do rozpoczęcia migracji.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="9a0a3-131">Po zakończeniu migracji programu Visual Studio udostępnia raport ze ścieżką do kopii zapasowej, listy pakietów zainstalowanych (najwyższego poziomu zależności), listę pakietów, określany jako zależności przechodnie i listę problemów ze zgodnością identyfikowane na początku Migracja.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="9a0a3-132">Raport jest zapisywany w folderze kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="9a0a3-133">Sprawdź, czy rozwiązanie tworzenia i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="9a0a3-134">Jeśli wystąpią problemy, [pliku problemu w serwisie GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="9a0a3-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="9a0a3-135">Jak przywrócić pliku packages.config</span><span class="sxs-lookup"><span data-stu-id="9a0a3-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="9a0a3-136">Zamknij projekt zmigrowane.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-136">Close the migrated project.</span></span>

1. <span data-ttu-id="9a0a3-137">Skopiuj plik projektu i `packages.config` z kopii zapasowej (zazwyczaj `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) do folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="9a0a3-138">Otwórz projekt.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-138">Open the project.</span></span>

1. <span data-ttu-id="9a0a3-139">Otwórz konsolę Menedżera pakietów przy użyciu **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="9a0a3-140">W konsoli, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9a0a3-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="9a0a3-141">Problemy ze zgodnością pakietu</span><span class="sxs-lookup"><span data-stu-id="9a0a3-141">Package compatibility issues</span></span>

<span data-ttu-id="9a0a3-142">Niektóre aspekty, które są obsługiwane w pliku packages.config nie są obsługiwane w PackageReference.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="9a0a3-143">Migrator analizuje i wykrywa takich problemów.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="9a0a3-144">Dowolnego pakietu, który ma co najmniej jeden z następujących problemów może nie działać zgodnie z oczekiwaniami po migracji.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="9a0a3-145">skrypty "install.ps1" są ignorowane, gdy pakiet jest zainstalowany po migracji</span><span class="sxs-lookup"><span data-stu-id="9a0a3-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9a0a3-146">**Opis**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-146">**Description**</span></span> | <span data-ttu-id="9a0a3-147">Z PackageReference install.ps1 i uninstall.ps1 skryptów programu PowerShell nie są wykonywane podczas instalowania lub odinstalowywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="9a0a3-148">**Potencjalny wpływ**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-148">**Potential impact**</span></span> | <span data-ttu-id="9a0a3-149">Pakiety, które są zależne od tych skryptów, aby skonfigurować niektóre zachowania w projekcie docelowym może nie działać zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="9a0a3-150">"zawartość" zasoby są niedostępne, gdy pakiet jest zainstalowany po migracji</span><span class="sxs-lookup"><span data-stu-id="9a0a3-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9a0a3-151">**Opis**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-151">**Description**</span></span> | <span data-ttu-id="9a0a3-152">Zasoby w pakiecie `content` folderu nie są obsługiwane z PackageReference i zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="9a0a3-153">PackageReference dodaje obsługę `contentFiles` mają lepszą obsługę przechodnie i zawartości udostępnionej.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="9a0a3-154">**Potencjalny wpływ**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-154">**Potential impact**</span></span> | <span data-ttu-id="9a0a3-155">Zasoby w `content` nie są kopiowane do projektu i projektu wymaga refaktoryzacji kodu, która zależy od obecności tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="9a0a3-156">Transformacje XDT nie są stosowane, gdy pakiet jest zainstalowany po uaktualnieniu</span><span class="sxs-lookup"><span data-stu-id="9a0a3-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9a0a3-157">**Opis**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-157">**Description**</span></span> | <span data-ttu-id="9a0a3-158">Transformacje XDT nie są obsługiwane przez PackageReference i `.xdt` pliki są ignorowane, podczas instalowania lub odinstalowywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="9a0a3-159">**Potencjalny wpływ**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-159">**Potential impact**</span></span> | <span data-ttu-id="9a0a3-160">Transformacje XDT nie są stosowane do projektu pliki XML, najczęściej `web.config.install.xdt` i `web.config.uninstall.xdt`, co oznacza, że projekt` web.config` pliku nie jest aktualizowany po zainstalowaniu lub odinstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="9a0a3-161">Zestawy w katalogu lib są ignorowane, gdy pakiet jest zainstalowany po migracji</span><span class="sxs-lookup"><span data-stu-id="9a0a3-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="9a0a3-162">**Opis**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-162">**Description**</span></span> | <span data-ttu-id="9a0a3-163">Z PackageReference, zestawów występujących w katalogu głównym `lib` folderu bez docelowego framework określonych podfolderów są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="9a0a3-164">NuGet szuka podfolderu dopasowania moniker platformy docelowej (TFM) odpowiadający platformy docelowej projektu i instaluje zestawy pasującego do projektu.</span><span class="sxs-lookup"><span data-stu-id="9a0a3-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="9a0a3-165">**Potencjalny wpływ**</span><span class="sxs-lookup"><span data-stu-id="9a0a3-165">**Potential impact**</span></span> | <span data-ttu-id="9a0a3-166">Pakiety, które nie mają podfolderu dopasowania moniker platformy docelowej (TFM) odpowiadający platformy docelowej projektu może nie działać zgodnie z oczekiwaniami po przejściu lub niepowodzenie instalacji podczas migracji</span><span class="sxs-lookup"><span data-stu-id="9a0a3-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="9a0a3-167">Wystąpił problem związany?</span><span class="sxs-lookup"><span data-stu-id="9a0a3-167">Found an issue?</span></span> <span data-ttu-id="9a0a3-168">Zgłoś to!</span><span class="sxs-lookup"><span data-stu-id="9a0a3-168">Report it!</span></span>

<span data-ttu-id="9a0a3-169">Jeśli napotkasz problem z obsługi migracji [pliku problemu w repozytorium NuGet GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="9a0a3-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
