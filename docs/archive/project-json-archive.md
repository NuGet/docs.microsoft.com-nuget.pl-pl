---
title: Zawartość archiwum project.json NuGet
description: Różne bity usunięte z innych części dokumentacji NuGet zawartość pliku project.json.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: cd0f4bc44c1acaeed3b3ed0241c501ddd281628d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="56977-103">archiwum Project.JSON</span><span class="sxs-lookup"><span data-stu-id="56977-103">project.json archive</span></span>

<span data-ttu-id="56977-104">`project.json` Format zarządzania wprowadzono w systemie NuGet 3.x i używana do pewnych typów projektów.</span><span class="sxs-lookup"><span data-stu-id="56977-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="56977-105">Go została uznana za przestarzałą wraz z wprowadzeniem PackageReference format, w którym zależności są wymienione bezpośrednio w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="56977-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="56977-106">Zobacz też:</span><span class="sxs-lookup"><span data-stu-id="56977-106">Also see:</span></span>

- [<span data-ttu-id="56977-107">project.json schema</span><span class="sxs-lookup"><span data-stu-id="56977-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="56977-108">Project.JSON wpływ na autora pakietu</span><span class="sxs-lookup"><span data-stu-id="56977-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="56977-109">Plik project.json i platforma UWP</span><span class="sxs-lookup"><span data-stu-id="56977-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="56977-110">format zarządzania Project.JSON</span><span class="sxs-lookup"><span data-stu-id="56977-110">project.json management format</span></span>

<span data-ttu-id="56977-111">*Pierwotnie w [Przywracanie pakietu](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="56977-112">Na liście formatów zarządzania:</span><span class="sxs-lookup"><span data-stu-id="56977-112">In the list of management formats:</span></span>

- <span data-ttu-id="56977-113">[`project.json`](project-json.md): *(przestarzałe)* pliku A JSON, który przechowuje listę zależności projektu z ogólną wykres pakietu w skojarzony plik `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="56977-114">Ten format jest zastąpiona PackageReference.</span><span class="sxs-lookup"><span data-stu-id="56977-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="56977-115">Przywracanie nuget dla Mono</span><span class="sxs-lookup"><span data-stu-id="56977-115">nuget restore on Mono</span></span>

<span data-ttu-id="56977-116">*Pierwotnie w [NuGet zainstalować narzędzia klienta](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="56977-117">Współpracuje z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="56977-118">Ograniczający wersje pakietu z przywracania</span><span class="sxs-lookup"><span data-stu-id="56977-118">Constraining package versions with restore</span></span>

<span data-ttu-id="56977-119">*Pierwotnie w [Przywracanie pakietu](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="56977-119">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="56977-120">`project.json`: Określ zakres wersji bezpośrednio z numerem wersji tych zależności.</span><span class="sxs-lookup"><span data-stu-id="56977-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="56977-121">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="56977-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="56977-122">Polecenia interfejsu wiersza polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="56977-122">NuGet CLI commands</span></span>

- <span data-ttu-id="56977-123">`nuget install` nie działa z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="56977-124">`nuget restore`: z projektami za pomocą `project.json`, generuje `project.lock.json` pliku i `<project>.nuget.props` plików, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="56977-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="56977-125">(Oba pliki można pominąć z kontroli źródła). `<projectPath>` Argument może wskazywać `project.json` plików i zachowanie jest takie samo jak wskazujący `packages.config` lub pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="56977-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="56977-126">W kolejności priorytetu do folderów pakietów `%userprofile%\.nuget\packages` przeszukiwane są najpierw przy użyciu `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="56977-127">`nuget update`: Na Mono, to polecenie nie działa z projektami za pomocą `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="56977-128">Rozpoznawanie zależności z PackageReference</span><span class="sxs-lookup"><span data-stu-id="56977-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="56977-129">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="56977-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="56977-130">Zachowanie PackageReference dotyczą również `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="56977-131">Przywracanie NuGet zapisuje wykresu zależności w pliku o nazwie `project.lock.json` obok `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="56977-132">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="56977-132">Managing dependency assets</span></span>

<span data-ttu-id="56977-133">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="56977-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="56977-134">Korzystając z `project.json` format, można kontrolować, które zasoby z przepływu zależności w projekcie najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="56977-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="56977-135">Aby uzyskać więcej informacji, zobacz [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="56977-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="56977-136">Z wyjątkiem odwołania</span><span class="sxs-lookup"><span data-stu-id="56977-136">Excluding references</span></span>

<span data-ttu-id="56977-137">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="56977-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="56977-138">`project.json`: Dodaj `"exclude" : "all"` w zależność PackageC:</span><span class="sxs-lookup"><span data-stu-id="56977-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="56977-139">Rozwiązywanie błędów niezgodne pakietu</span><span class="sxs-lookup"><span data-stu-id="56977-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="56977-140">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="56977-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="56977-141">Dodano sposób rozwiązywaniu problemów z błędami:</span><span class="sxs-lookup"><span data-stu-id="56977-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="56977-142">**Nie zaleca się**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projektów przeznaczonych dla `netcore`, `netstandard`, i `netcoreapp` są oznaczane innych platform, jako niezgodna, umożliwiając pakietów przeznaczonych dla tych innych platform, które mają być używane.</span><span class="sxs-lookup"><span data-stu-id="56977-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="56977-143">Zobacz [importuje project.json](project-json.md#imports) i [docelowy programu MSBuild przywracania PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="56977-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="56977-144">Może to spowodować nieoczekiwane wyniki, więc ponownie najlepiej rozwiązać niezgodności pakietu przy pracy z autorem pakietu podczas aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="56977-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="56977-145">Docelowych platform</span><span class="sxs-lookup"><span data-stu-id="56977-145">Target frameworks</span></span>

<span data-ttu-id="56977-146">*Pierwotnie w [platform docelowych](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="56977-147">[Project.JSON](project-json.md): `frameworks` wersji framework, które mogą być kompilowane projektu przed określa węzła.</span><span class="sxs-lookup"><span data-stu-id="56977-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="56977-148">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="56977-148">Creating a package</span></span>

<span data-ttu-id="56977-149">*Pierwotnie w [tworzenia pakietu](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="56977-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="56977-150">Ustawienie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="56977-150">Setting a package type</span></span>

<span data-ttu-id="56977-151">Z platformą .NET Core 1.x, gdy DotnetCliTool pakiet jest zainstalowany, program Visual Studio umieszcza pakietu w `project.json` `tools` węzła zamiast `dependencies` węzła.</span><span class="sxs-lookup"><span data-stu-id="56977-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="56977-152">Typy pakietów są ustawiane w `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="56977-153">`project.json`: Określ typ pakietu w `packOptions.packageType` właściwości json:</span><span class="sxs-lookup"><span data-stu-id="56977-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="56977-154">Dodawanie elementów docelowych i właściwości dla programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="56977-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="56977-155">*Pierwotnie w [tworzenia pakietów NuGet standardowe .NET z programem Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="56977-156">Korzystając z `project.json`, elementy docelowe nie zostaną dodane do projektu, ale są udostępniane za pośrednictwem `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="56977-157">Przechowywanie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="56977-157">Package versioning</span></span>

<span data-ttu-id="56977-158">*Pierwotnie w [wersji pakietu](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="56977-159">Korzystając z `project.json` formacie NuGet również obsługuje za pomocą notacji symboli wieloznacznych, \*, główna, pomocnicze, poprawki i sufiks wersji wstępnej części numeru.</span><span class="sxs-lookup"><span data-stu-id="56977-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="56977-160">Odwołanie do pliku NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="56977-160">NuGet.Config reference</span></span>

<span data-ttu-id="56977-161">*Pierwotnie w [odwołanie do pliku NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="56977-162">`globalPackagesFolder` dotyczy tylko `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="56977-163">(Dodanie uwagi: odnosi się także do PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="56977-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="56977-164">Odwołanie do pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="56977-164">nuspec file reference</span></span>

<span data-ttu-id="56977-165">*Pierwotnie w [odwołania nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="56977-166">`<contentFiles>` Element jest używany zamiast `<files>` z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="56977-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="56977-167">Kontrolki opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="56977-167">Package manager options control</span></span>

<span data-ttu-id="56977-168">*Pierwotnie w [informacje o interfejsie użytkownika Menedżera pakietów](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="56977-169">Projektów przy użyciu `project.json` zarządzania format Pokaż tylko **Pokaż okno podglądu** opcji.</span><span class="sxs-lookup"><span data-stu-id="56977-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="56977-170">Szablony Visual Studio</span><span class="sxs-lookup"><span data-stu-id="56977-170">Visual Studio Templates</span></span>

<span data-ttu-id="56977-171">*Pierwotnie w [pakietów NuGet w szablony Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="56977-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="56977-172">Najlepsze rozwiązania: szablony nie zawierają `project.json` pliku, a nie dołączaj lub żadnych odwołań do zawartości lub zostanie dodany podczas instalowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="56977-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>