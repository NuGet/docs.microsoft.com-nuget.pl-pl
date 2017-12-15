---
title: Przywracanie pakietu NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Opis sposobu NuGet przywraca pakietów, od których jest zależna projektu, w tym jak wyłączyć przywracania i ograniczyć wersji."
keywords: "Przywracanie pakietu NuGet, instalacja pakietu NuGet, instalowanie pakietu Przywracanie pakietów, wersje zależności, wyłączenie automatycznego przywracania ograniczający wersji pakietu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a><span data-ttu-id="77c51-104">Przywracanie pakietu</span><span class="sxs-lookup"><span data-stu-id="77c51-104">Package Restore</span></span>

<span data-ttu-id="77c51-105">Aby promować czyszczący Środowisko deweloperskie i zmniejszyć rozmiar repozytorium NuGet **przywracania pakietów** instaluje pakiety wszystkich przywoływanych przed projektu jest wbudowana.</span><span class="sxs-lookup"><span data-stu-id="77c51-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="77c51-106">Ta funkcja powszechnie używane gwarantuje, że wszystkie zależności są dostępne w projekcie bez konieczności pakiety mają być przechowywane w kontroli źródła (zobacz [pakietów i kontroli źródła](../consume-packages/packages-and-source-control.md) na temat konfigurowania repozytorium, aby wykluczyć pliki binarne pakietu).</span><span class="sxs-lookup"><span data-stu-id="77c51-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="77c51-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="77c51-107">In this topic:</span></span>
- [<span data-ttu-id="77c51-108">Przywróć krótki przewodnik do pakietu</span><span class="sxs-lookup"><span data-stu-id="77c51-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="77c51-109">Omówienie przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="77c51-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="77c51-110">Włączanie i wyłączanie przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="77c51-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="77c51-111">Ograniczający wersje pakietu z przywracania</span><span class="sxs-lookup"><span data-stu-id="77c51-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="77c51-112">[Przywracanie wiersza polecenia](#command-line-restore), wszystkie wersje programu NuGet</span><span class="sxs-lookup"><span data-stu-id="77c51-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="77c51-113">[Automatyczne przywracania w programie Visual Studio](#automatic-restore-in-visual-studio)dla NuGet 2.7 i później.</span><span class="sxs-lookup"><span data-stu-id="77c51-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="77c51-114">[Zintegrowane MSBuild przywracania w programie Visual Studio](#msbuild-integrated-restore)dla NuGet 2.6 i starszych.</span><span class="sxs-lookup"><span data-stu-id="77c51-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="77c51-115">Przywracanie pakietu z Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="77c51-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="77c51-116">Przywróć zachowanie zależy od wersji; Aby sprawdzić wersję programu NuGet, wystarczy uruchomić `nuget.exe` na wiersz polecenia i znajduje się w pierwszym wierszu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="77c51-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="77c51-117">Aby uzyskać dodatkowe szczegóły dotyczące przywracania pakietu na serwerach kompilacji, zobacz [Przywracanie pakietu z TFBuild](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="77c51-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="77c51-118">Projekty skonfigurowane dla pakietu przywrócić również współpracują z xbuild na Mono.</span><span class="sxs-lookup"><span data-stu-id="77c51-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="77c51-119">Przywróć krótki przewodnik do pakietu</span><span class="sxs-lookup"><span data-stu-id="77c51-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="77c51-120">Jeśli zostanie wyświetlony błąd "ten projekt zawiera odwołania do pakietów NuGet, na tym komputerze brakuje" lub "co najmniej jednego pakietu NuGet konieczne jest przywrócenie, ale nie może być, ponieważ nie udzielono zgody", należy włączyć automatyczne przywracanie zgodnie z instrukcjami w obszarze [Włączanie i wyłączanie Przywracanie pakietu](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="77c51-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="77c51-121">Omówienie przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="77c51-121">Package restore overview</span></span>

<span data-ttu-id="77c51-122">Po pierwsze odwołania do pakietu są obsługiwane w jednym z następujących formatów zarządzania pakiet, w zależności od typu projektu i wersja narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="77c51-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="77c51-123">(Uwaga NuGet 4 i MSBuild 15.1 są instalowane z programu Visual Studio 2017 r.)</span><span class="sxs-lookup"><span data-stu-id="77c51-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="77c51-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="77c51-124">Method</span></span> | <span data-ttu-id="77c51-125">Wersja narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="77c51-125">NuGet Version</span></span> | <span data-ttu-id="77c51-126">Opis</span><span class="sxs-lookup"><span data-stu-id="77c51-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="77c51-127">2.x +</span><span class="sxs-lookup"><span data-stu-id="77c51-127">2.x+</span></span> | <span data-ttu-id="77c51-128">Wyświetla listę pełny zestaw głębokie zależności.</span><span class="sxs-lookup"><span data-stu-id="77c51-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="77c51-129">Dodane do pakietów `packages.config` również musi zostać dodany do pliku projektu i cele i właściwości, również muszą zostać dodane do pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="77c51-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="77c51-130">Jest to metoda linii bazowej dla wszystkich wersji programu NuGet, ale działa wolniej w porównaniu z innymi opcjami.</span><span class="sxs-lookup"><span data-stu-id="77c51-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="77c51-131">(Zobacz [schematu pliku packages.config](../schema/packages-config.md).)</span><span class="sxs-lookup"><span data-stu-id="77c51-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="77c51-132">3.x +</span><span class="sxs-lookup"><span data-stu-id="77c51-132">3.x+</span></span> | <span data-ttu-id="77c51-133">Używany domyślnie tylko z projektami platformy uniwersalnej systemu Windows, ale można przekonwertować projektów z `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="77c51-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="77c51-134">`project.json`zawiera tylko zależności najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="77c51-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="77c51-135">Odwołania do obiektów docelowych i właściwości są dodawane dynamicznie do projektu podczas kompilacji, co zapewnia lepszą wydajność w porównaniu z `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="77c51-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="77c51-136">(Zobacz [schematu project.json](../schema/project-json.md).)</span><span class="sxs-lookup"><span data-stu-id="77c51-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="77c51-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="77c51-137">PackageReference</span></span> | <span data-ttu-id="77c51-138">4.x +</span><span class="sxs-lookup"><span data-stu-id="77c51-138">4.x+</span></span> | <span data-ttu-id="77c51-139">Zawiera listę zależności bezpośrednio w pliku projektu w `<PackageReference>` węzła, alongside `<Reference>` i `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="77c51-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="77c51-140">Działa podobnie do `project.json`; zobacz [pakietu odwołań w plikach projektu](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="77c51-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="77c51-141">Po drugie rozpoczęciem przywracania przy użyciu listy odwołania na różne sposoby:</span><span class="sxs-lookup"><span data-stu-id="77c51-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="77c51-142">W wierszu polecenia lub [Konsola Menedżera pakietów](../tools/Package-Manager-Console.md):</span><span class="sxs-lookup"><span data-stu-id="77c51-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="77c51-143">Polecenie</span><span class="sxs-lookup"><span data-stu-id="77c51-143">Command</span></span> | <span data-ttu-id="77c51-144">Scenariusze zastosowania</span><span class="sxs-lookup"><span data-stu-id="77c51-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="77c51-145">Wszystkie wersje programu NuGet i wszystkie typy referencyjne.</span><span class="sxs-lookup"><span data-stu-id="77c51-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="77c51-146">Zobacz [wiersza polecenia przywracania](#command-line-restore) poniżej.</span><span class="sxs-lookup"><span data-stu-id="77c51-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="77c51-147">Taki sam jak `nuget restore` dla projektów .NET Core.</span><span class="sxs-lookup"><span data-stu-id="77c51-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="77c51-148">Zobacz [przywracania dotnet](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="77c51-148">See [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="77c51-149">Nuget 4.x+ i MSBuild 15.1 + z [pakietu odwołań w plikach projektu](../Consume-Packages/Package-References-in-Project-Files.md) tylko.</span><span class="sxs-lookup"><span data-stu-id="77c51-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="77c51-150">`nuget restore`i `dotnet restore` dla projektów dotyczy zarówno Użyj tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="77c51-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="77c51-151">Zobacz [pakiet NuGet i przywracania jako MSBuild elementy docelowe przywracaniem docelowej](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="77c51-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="77c51-152">Visual Studio, sama przywraca również pakiety w różnym czasie:</span><span class="sxs-lookup"><span data-stu-id="77c51-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="77c51-153">Typ</span><span class="sxs-lookup"><span data-stu-id="77c51-153">Type</span></span> | <span data-ttu-id="77c51-154">Podczas przywracania sytuacji</span><span class="sxs-lookup"><span data-stu-id="77c51-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="77c51-155">Przywracanie szablonu</span><span class="sxs-lookup"><span data-stu-id="77c51-155">Template restore</span></span> | <span data-ttu-id="77c51-156">Podczas tworzenia nowego projektu jako niektóre szablony są zależne od pakietów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="77c51-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="77c51-157">Tworzenie przywracania</span><span class="sxs-lookup"><span data-stu-id="77c51-157">Build restore</span></span> | <span data-ttu-id="77c51-158">W pierwszym kroku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="77c51-158">As the first step of a build.</span></span> |
| <span data-ttu-id="77c51-159">Przywrócenie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="77c51-159">Solution restore</span></span> | <span data-ttu-id="77c51-160">Gdy użytkownik kliknie prawym przyciskiem myszy rozwiązanie i wybiera **przywracania pakietów NuGet**.</span><span class="sxs-lookup"><span data-stu-id="77c51-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="77c51-161">Przywracanie w przypadku zmiany projektu</span><span class="sxs-lookup"><span data-stu-id="77c51-161">Restore on project change</span></span> | <span data-ttu-id="77c51-162">*(NuGet tylko 4.x)*  Projektu podczas .NET Core SDK jest używany, łącznie z projektu zmiany stanu.</span><span class="sxs-lookup"><span data-stu-id="77c51-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="77c51-163">Włączanie i wyłączanie przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="77c51-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="77c51-164">Przywracanie pakietu głównie jest włączany za pomocą **Narzędzia > Opcje > Menedżera pakietów NuGet** w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="77c51-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Kontrolowanie zachowania przywracania pakietu za pomocą opcji Menedżera pakietów NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="77c51-166">**Zezwalaj narzędziu NuGet na pobieranie brakujących pakietów**: Określa wszystkich formularzy Przywracanie pakietu, zmieniając `packageRestore/enabled` w `%AppData%\NuGet\NuGet.Config` plików, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="77c51-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="77c51-167">`packageRestore/enabled` Ustawienie można zastąpić globalny, ustawiając zmienną środowiskową o nazwie **EnableNuGetPackageRestore** o wartości TRUE lub FALSE przed uruchomieniem programu Visual Studio lub uruchamianie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="77c51-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="77c51-168">**Automatyczne sprawdzenie dostępności dla brakujących pakietów podczas kompilacji w programie Visual Studio**: Określa przywracania automatycznie NuGet 2.7 i później, zmieniając `packageRestore/automatic` w `%AppData%\NuGet\NuGet.Config` plików, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="77c51-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="77c51-169">Aby informacje, zobacz [NuGet pliku konfiguracji - sekcji packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="77c51-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="77c51-170">W niektórych przypadkach włączyć lub wyłączyć Przywracanie pakietu na komputerze, domyślnie dla wszystkich użytkowników może być deweloperem lub firmy.</span><span class="sxs-lookup"><span data-stu-id="77c51-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="77c51-171">Można to zrobić przez dodanie tych samych ustawień powyżej do globalnych znajduje się w pliku konfiguracji w NuGet `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="77c51-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="77c51-172">Poszczególnym użytkownikom można selektywnie włączysz przywracania na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="77c51-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="77c51-173">Zobacz [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) dokładne szczegółowe informacje na temat sposobu NuGet priorytetem wiele plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="77c51-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="77c51-174">Ograniczający wersje pakietu z przywracania</span><span class="sxs-lookup"><span data-stu-id="77c51-174">Constraining package versions with restore</span></span>

<span data-ttu-id="77c51-175">Gdy NuGet przywraca pakietów przy użyciu dowolnej metody, podlegają wszystkie ograniczenia określone w `packages.config`, `project.json`, lub plik projektu:</span><span class="sxs-lookup"><span data-stu-id="77c51-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="77c51-176">`packages.config`: Określ zakres wersji w `allowedVersion` właściwości zależności.</span><span class="sxs-lookup"><span data-stu-id="77c51-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="77c51-177">Zobacz [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="77c51-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="77c51-178">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="77c51-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="77c51-179">`project.json`: Określ zakres wersji bezpośrednio z numerem wersji tych zależności.</span><span class="sxs-lookup"><span data-stu-id="77c51-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="77c51-180">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="77c51-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="77c51-181">Pakiet odwołań w plikach projektu: Określ zakres wersji bezpośrednio z numerem wersji tych zależności.</span><span class="sxs-lookup"><span data-stu-id="77c51-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="77c51-182">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="77c51-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="77c51-183">We wszystkich przypadkach Notacja opisanego w [wersji pakietu](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="77c51-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="77c51-184">Przywracanie wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="77c51-184">Command-line restore</span></span>

<span data-ttu-id="77c51-185">NuGet 2.7 i nowszych, użyj [przywrócić](../tools/cli-ref-restore.md) polecenia, aby przywrócić wszystkie pakiety w rozwiązaniu (czy używa `packages.config`, `project.json`, lub pakietu odwołań w plikach projektu).</span><span class="sxs-lookup"><span data-stu-id="77c51-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="77c51-186">W przypadku folderu danego projektu, takie jak `c:\proj\app`, typowe przykłady poniżej każdego przywrócenia pakietów:</span><span class="sxs-lookup"><span data-stu-id="77c51-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="77c51-187">NuGet 4.0 + i MSBuild 15.1 + umożliwia także `MSBuild /t:restore` zgodnie z opisem na [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="77c51-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="77c51-188">Przywracanie czas kompilacji w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77c51-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="77c51-189">Visual Studio automatycznie przywraca brakujących pakietów domyślnie na początku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="77c51-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="77c51-190">To zachowanie można zmienić po usunięciu zaznaczenia **Narzędzia > Opcje > Menedżera pakietów NuGet > Ogólne > automatyczne sprawdzenie dostępności dla brakujących pakietów podczas kompilacji w programie Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="77c51-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="77c51-191">Po włączeniu automatycznej przywracania działa w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="77c51-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="77c51-192">Po rozpoczęciu kompilacji programu Visual Studio nakazuje NuGet pod kątem przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="77c51-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="77c51-193">NuGet rekursywnie wyszukuje wszystkie `packages.config` wyszukuje pliki w rozwiązaniu, `project.json`, lub jest wyszukiwany w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="77c51-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="77c51-194">Dla każdego pakietów na liście plików źródłowych, NuGet kontroli Jeśli już istnieje w rozwiązaniu ( `packages` folderu, `project.lock.json`, lub `project.assets.json` w zależności od tego, czy projekt jest przy użyciu `packages.config`, `project.json`, lub pakietu odwołań w pliki projektu).</span><span class="sxs-lookup"><span data-stu-id="77c51-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="77c51-195">Jeśli pakiet nie zostanie znaleziony, NuGet podejmuje próbę pobrania pakietu z pamięci podręcznej najpierw (zobacz [Zarządzanie pamięci podręcznej NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="77c51-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="77c51-196">Jeśli pakiet nie jest w pamięci podręcznej, NuGet podejmuje próbę pobrania pakietu z włączonych źródeł wymienionych w **Narzędzia > Opcje > Menedżera pakietów NuGet > źródła pakietów w**, w kolejności źródeł.</span><span class="sxs-lookup"><span data-stu-id="77c51-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="77c51-197">W takim przypadku NuGet nie wskazuje niepowodzenie, można znaleźć pakietu, dopóki wszystkie źródła zostały sprawdzone, po tym czasie zgłasza błąd tylko dla ostatniego źródła na liście.</span><span class="sxs-lookup"><span data-stu-id="77c51-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="77c51-198">Co za tym idzie takiego błędu oznacza także, że pakiet nie był dostępny na żadnym z innych źródeł albo, nawet jeśli błędy zostały nie wyświetlane dla tych źródeł pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="77c51-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="77c51-199">Jeśli pobieranie się pomyślnie, NuGet buforuje pakietu i instaluje je do rozwiązania (ponownie, albo do `packages` folderu, `project.lock.json`, lub `project.assets.json`); w przeciwnym razie NuGet kończy się niepowodzeniem i kompilacja zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="77c51-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="77c51-200">W trakcie tego procesu zostanie wyświetlony postęp okno dialogowe z opcji, aby anulować przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="77c51-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="77c51-201">Przywracanie pakietu z programu Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="77c51-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="77c51-202">Przywracanie pakietu jest często stosowany podczas tworzenia projektów na serwerach kompilacji, tak jak w przypadku Team Foundation Server (TFS) i Visual Studio Team Services (a także innych systemów kompilacji, które nie zostały omówione w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="77c51-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="77c51-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="77c51-203">Visual Studio Team Services</span></span>

<span data-ttu-id="77c51-204">Podczas tworzenia definicji kompilacji na Team Services, wystarczy dołączyć zadań przywracania pakietów NuGet w definicji przed dowolnego zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="77c51-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="77c51-205">To zadanie jest domyślnie włączone w szablony kompilacji.</span><span class="sxs-lookup"><span data-stu-id="77c51-205">This task is included by default in a number of build templates.</span></span>

![Zadanie przywracania pakietów NuGet w definicji kompilacji programu Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="77c51-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="77c51-207">Team Foundation Server</span></span>

<span data-ttu-id="77c51-208">Z programem TFS 2013 i nowsze są automatycznie przywrócić pakiety domyślnie podczas kompilacji, pod warunkiem, że używasz zespołu tworzenie szablonu dla Team Foundation Server 2013 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="77c51-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="77c51-209">Jeśli używasz poprzednią wersję szablonów kompilacji (takich jak klastry projektu, które zostały poddane migracji z wcześniejszych wersji programu TFS), musisz również migrację kompilacji tych szablonów do TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="77c51-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="77c51-210">Oznacza to, zasadniczo odtworzenie części niestandardowe szablony kompilacji dla kontroli źródła (TFVC lub Git) przy użyciu odpowiedniego szablonu.</span><span class="sxs-lookup"><span data-stu-id="77c51-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="77c51-211">Dla wcześniejszych wersji programu TFS, należy po prostu zawierają kroku kompilacji do wywołania [wiersza polecenia przywracania](#command-line-restore) zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="77c51-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="77c51-212">Aby uzyskać więcej informacji, zobacz następnie [wskazówki z przywracania pakietów z Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="77c51-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
