---
title: Zawartość archiwum pliku project.json NuGet
description: Różne bity zawartość pliku project.json usunięcie z innych obszarów dokumentacja programu NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: d43f002b740b669de13f5872844ac0df97fc8fdc
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467786"
---
# <a name="projectjson-archive"></a><span data-ttu-id="8bb34-103">archiwum pliku Project.JSON</span><span class="sxs-lookup"><span data-stu-id="8bb34-103">project.json archive</span></span>

<span data-ttu-id="8bb34-104">`project.json` Format zarządzania wprowadzono nuget 3.x i używane w przypadku niektórych typów projektów.</span><span class="sxs-lookup"><span data-stu-id="8bb34-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="8bb34-105">Została ona zakończona wraz z wprowadzeniem PackageReference format, w którym zależności są wymienione bezpośrednio w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8bb34-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="8bb34-106">Zobacz też:</span><span class="sxs-lookup"><span data-stu-id="8bb34-106">Also see:</span></span>

- [<span data-ttu-id="8bb34-107">project.json schema</span><span class="sxs-lookup"><span data-stu-id="8bb34-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="8bb34-108">wpływ pliku Project.JSON na autorom pakietów</span><span class="sxs-lookup"><span data-stu-id="8bb34-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="8bb34-109">Plik project.json i platforma UWP</span><span class="sxs-lookup"><span data-stu-id="8bb34-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="8bb34-110">Format zarządzania project.json</span><span class="sxs-lookup"><span data-stu-id="8bb34-110">project.json management format</span></span>

<span data-ttu-id="8bb34-111">*Początkowo w [Przywracanie pakietu](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="8bb34-112">Na liście formatów zarządzania:</span><span class="sxs-lookup"><span data-stu-id="8bb34-112">In the list of management formats:</span></span>

- <span data-ttu-id="8bb34-113">[`project.json`](project-json.md): *(przestarzałe)* pliku JSON, który utrzymuje listę zależności projektu za pomocą ogólny wykres pakietu skojarzony plik `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="8bb34-114">Ten format jest zastąpiona PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8bb34-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="8bb34-115">Przywracanie nuget dla platformy Mono</span><span class="sxs-lookup"><span data-stu-id="8bb34-115">nuget restore on Mono</span></span>

<span data-ttu-id="8bb34-116">*Początkowo w [narzędzia klienta programu NuGet zainstalować](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="8bb34-117">W programach `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="8bb34-118">Ograniczający wersji pakietu, dzięki funkcji przywracania</span><span class="sxs-lookup"><span data-stu-id="8bb34-118">Constraining package versions with restore</span></span>

<span data-ttu-id="8bb34-119">*Początkowo w [Przywracanie pakietu](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-119">*Originally in [Package restore](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span></span>

- <span data-ttu-id="8bb34-120">`project.json`: Określ zakres wersji bezpośrednio z numerem wersji zależności.</span><span class="sxs-lookup"><span data-stu-id="8bb34-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="8bb34-121">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8bb34-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="8bb34-122">Polecenia interfejsu wiersza polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="8bb34-122">NuGet CLI commands</span></span>

- <span data-ttu-id="8bb34-123">`nuget install` nie działa z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="8bb34-124">`nuget restore`: z projektami za pomocą `project.json`, generuje `project.lock.json` pliku i `<project>.nuget.props` pliku, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8bb34-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="8bb34-125">(Oba pliki można pominąć z kontroli źródła.) `<projectPath>` Argument może wskazywać `project.json` plików i ma takie samo zachowanie, co wskazuje `packages.config` lub pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8bb34-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="8bb34-126">W kolejności priorytetu do folderów pakietów `%userprofile%\.nuget\packages` jest przeszukiwany w pierwszej kolejności przy użyciu `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="8bb34-127">`nuget update`: W rozwiązaniu Mono to polecenie nie działa z projektami za pomocą `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="8bb34-128">Rozpoznawanie zależności za pomocą funkcji PackageReference</span><span class="sxs-lookup"><span data-stu-id="8bb34-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="8bb34-129">*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="8bb34-130">Zachowanie funkcji PackageReference ma również zastosowanie do `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="8bb34-131">Przywracanie pakietów NuGet zapisuje wykres zależności w pliku o nazwie `project.lock.json` obok `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="8bb34-132">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="8bb34-132">Managing dependency assets</span></span>

<span data-ttu-id="8bb34-133">*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="8bb34-134">Korzystając z `project.json` formatu, można kontrolować, które zasoby z przepływem zależności do najwyższego poziomu projektu.</span><span class="sxs-lookup"><span data-stu-id="8bb34-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="8bb34-135">Aby uzyskać więcej informacji, zobacz [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="8bb34-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="8bb34-136">Z wyjątkiem odwołania</span><span class="sxs-lookup"><span data-stu-id="8bb34-136">Excluding references</span></span>

<span data-ttu-id="8bb34-137">*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="8bb34-138">`project.json`: Dodaj `"exclude" : "all"` powstanie zależności dla PackageC:</span><span class="sxs-lookup"><span data-stu-id="8bb34-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="8bb34-139">Rozwiązywanie błędów pakietu niezgodne</span><span class="sxs-lookup"><span data-stu-id="8bb34-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="8bb34-140">*Początkowo w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="8bb34-141">Dodano sposób Rozwiązywanie błędów:</span><span class="sxs-lookup"><span data-stu-id="8bb34-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="8bb34-142">**Nie zaleca się**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projekty przeznaczone dla `netcore`, `netstandard`, i `netcoreapp` można oznaczają inne struktury jako zgodne, umożliwiając w ten sposób pakiety przeznaczone dla tych inne struktury do użycia.</span><span class="sxs-lookup"><span data-stu-id="8bb34-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="8bb34-143">Zobacz [importuje plik project.json](project-json.md#imports) i [docelowej przywracania MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="8bb34-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="8bb34-144">Może to powodować nieoczekiwane zachowania, więc ponownie jest najlepsze rozwiązanie niezgodności pakietu poprzez współdziałanie z autorem pakietu podczas aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="8bb34-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="8bb34-145">Platformy docelowe</span><span class="sxs-lookup"><span data-stu-id="8bb34-145">Target frameworks</span></span>

<span data-ttu-id="8bb34-146">*Początkowo w [ustalać platformy docelowe](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="8bb34-147">[project.json](project-json.md): `frameworks` Węzła określa wersje framework skompilowany projekt.</span><span class="sxs-lookup"><span data-stu-id="8bb34-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="8bb34-148">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="8bb34-148">Creating a package</span></span>

<span data-ttu-id="8bb34-149">*Początkowo w [Tworzenie pakietu](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="8bb34-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="8bb34-150">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="8bb34-150">Setting a package type</span></span>

<span data-ttu-id="8bb34-151">Za pomocą programu .NET Core 1.x, gdy DotnetCliTool pakiet jest zainstalowany, program Visual Studio umieszcza pakiet w `project.json` `tools` węzła zamiast `dependencies` węzła.</span><span class="sxs-lookup"><span data-stu-id="8bb34-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="8bb34-152">Typy pakietów są ustawiane w `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="8bb34-153">`project.json`: Wskazuje typ pakietu we `packOptions.packageType` właściwości json:</span><span class="sxs-lookup"><span data-stu-id="8bb34-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="8bb34-154">Dodawanie obiektów docelowych i właściwości dla programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="8bb34-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="8bb34-155">*Początkowo w [utworzyć pakiety NuGet standardowy .NET przy użyciu programu Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="8bb34-156">Korzystając z `project.json`, elementy docelowe nie są dodawane do projektu, ale są udostępniane za pośrednictwem `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="8bb34-157">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="8bb34-157">Package versioning</span></span>

<span data-ttu-id="8bb34-158">*Początkowo w [przechowywanie wersji pakietów](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="8bb34-159">Korzystając z `project.json` formatowania, NuGet również obsługuje używanie notacji symbolu wieloznacznego, \*, główne, pomocnicze, poprawki i sufiks wersji wstępnej części numeru.</span><span class="sxs-lookup"><span data-stu-id="8bb34-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="8bb34-160">Odwołanie do pliku NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="8bb34-160">NuGet.Config reference</span></span>

<span data-ttu-id="8bb34-161">*Początkowo w [odwołanie do pliku NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="8bb34-162">`globalPackagesFolder` ma zastosowanie tylko do `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="8bb34-163">(Dodanie uwagi: ma zastosowanie również do odwołania PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="8bb34-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="8bb34-164">Odwołanie do pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="8bb34-164">nuspec file reference</span></span>

<span data-ttu-id="8bb34-165">*Początkowo w [odwołania nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="8bb34-166">`<contentFiles>` Element jest używany zamiast `<files>` z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8bb34-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="8bb34-167">Kontrolka opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="8bb34-167">Package manager options control</span></span>

<span data-ttu-id="8bb34-168">*Początkowo w [informacje o interfejsie użytkownika Menedżera pakietów](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="8bb34-169">Projekty, za pomocą `project.json` zarządzania format zobrazit pouze **Pokaż okno podglądu** opcji.</span><span class="sxs-lookup"><span data-stu-id="8bb34-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="8bb34-170">Szablony Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8bb34-170">Visual Studio Templates</span></span>

<span data-ttu-id="8bb34-171">*Początkowo w [pakietów NuGet w programie Visual Studio szablonach](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="8bb34-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="8bb34-172">Najlepsze rozwiązania: szablony nie obejmują `project.json` pliku i nie obejmują lub odwołania do dowolnej zawartości, która zostanie dodany po zainstalowaniu pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="8bb34-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>