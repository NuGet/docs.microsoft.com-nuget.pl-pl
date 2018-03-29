---
title: Zawartość archiwum project.json NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Różne bity usunięte z innych części dokumentacji NuGet zawartość pliku project.json.
keywords: Plik project.json NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="ac79e-104">archiwum Project.JSON</span><span class="sxs-lookup"><span data-stu-id="ac79e-104">project.json archive</span></span>

<span data-ttu-id="ac79e-105">`project.json` Format zarządzania wprowadzono w systemie NuGet 3.x i używana do pewnych typów projektów.</span><span class="sxs-lookup"><span data-stu-id="ac79e-105">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="ac79e-106">Go została uznana za przestarzałą wraz z wprowadzeniem PackageReference format, w którym zależności są wymienione bezpośrednio w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="ac79e-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="ac79e-107">Zobacz też:</span><span class="sxs-lookup"><span data-stu-id="ac79e-107">Also see:</span></span>

- [<span data-ttu-id="ac79e-108">project.json schema</span><span class="sxs-lookup"><span data-stu-id="ac79e-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="ac79e-109">Project.JSON wpływ na autora pakietu</span><span class="sxs-lookup"><span data-stu-id="ac79e-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="ac79e-110">Plik project.json i platforma UWP</span><span class="sxs-lookup"><span data-stu-id="ac79e-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="ac79e-111">format zarządzania Project.JSON</span><span class="sxs-lookup"><span data-stu-id="ac79e-111">project.json management format</span></span>

<span data-ttu-id="ac79e-112">*Pierwotnie w [Przywracanie pakietu](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="ac79e-113">Na liście formatów zarządzania:</span><span class="sxs-lookup"><span data-stu-id="ac79e-113">In the list of management formats:</span></span>

- <span data-ttu-id="ac79e-114">[`project.json`](project-json.md): *(przestarzałe)* pliku A JSON, który przechowuje listę zależności projektu z ogólną wykres pakietu w skojarzony plik `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="ac79e-115">Ten format jest zastąpiona PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ac79e-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="ac79e-116">Przywracanie nuget dla Mono</span><span class="sxs-lookup"><span data-stu-id="ac79e-116">nuget restore on Mono</span></span>

<span data-ttu-id="ac79e-117">*Pierwotnie w [NuGet zainstalować narzędzia klienta](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="ac79e-118">Współpracuje z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="ac79e-119">Ograniczający wersje pakietu z przywracania</span><span class="sxs-lookup"><span data-stu-id="ac79e-119">Constraining package versions with restore</span></span>

<span data-ttu-id="ac79e-120">*Pierwotnie w [Przywracanie pakietu](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="ac79e-121">`project.json`: Określ zakres wersji bezpośrednio z numerem wersji tych zależności.</span><span class="sxs-lookup"><span data-stu-id="ac79e-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="ac79e-122">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ac79e-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="ac79e-123">Polecenia interfejsu wiersza polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="ac79e-123">NuGet CLI commands</span></span>

- <span data-ttu-id="ac79e-124">`nuget install` nie działa z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="ac79e-125">`nuget restore`: z projektami za pomocą `project.json`, generuje `project.lock.json` pliku i `<project>.nuget.props` plików, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ac79e-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="ac79e-126">(Oba pliki można pominąć z kontroli źródła). `<projectPath>` Argument może wskazywać `project.json` plików i zachowanie jest takie samo jak wskazujący `packages.config` lub pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="ac79e-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="ac79e-127">W kolejności priorytetu do folderów pakietów `%userprofile%\.nuget\packages` przeszukiwane są najpierw przy użyciu `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="ac79e-128">`nuget update`: Na Mono, to polecenie nie działa z projektami za pomocą `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="ac79e-129">Rozpoznawanie zależności z PackageReference</span><span class="sxs-lookup"><span data-stu-id="ac79e-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="ac79e-130">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="ac79e-131">Zachowanie PackageReference dotyczą również `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="ac79e-132">Przywracanie NuGet zapisuje wykresu zależności w pliku o nazwie `project.lock.json` obok `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="ac79e-133">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="ac79e-133">Managing dependency assets</span></span>

<span data-ttu-id="ac79e-134">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="ac79e-135">Korzystając z `project.json` format, można kontrolować, które zasoby z przepływu zależności w projekcie najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="ac79e-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="ac79e-136">Aby uzyskać więcej informacji, zobacz [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="ac79e-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="ac79e-137">Z wyjątkiem odwołania</span><span class="sxs-lookup"><span data-stu-id="ac79e-137">Excluding references</span></span>

<span data-ttu-id="ac79e-138">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="ac79e-139">`project.json`: Dodaj `"exclude" : "all"` w zależność PackageC:</span><span class="sxs-lookup"><span data-stu-id="ac79e-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="ac79e-140">Rozwiązywanie błędów niezgodne pakietu</span><span class="sxs-lookup"><span data-stu-id="ac79e-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="ac79e-141">*Pierwotnie w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="ac79e-142">Dodano sposób rozwiązywaniu problemów z błędami:</span><span class="sxs-lookup"><span data-stu-id="ac79e-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="ac79e-143">**Nie zaleca się**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projektów przeznaczonych dla `netcore`, `netstandard`, i `netcoreapp` są oznaczane innych platform, jako niezgodna, umożliwiając pakietów przeznaczonych dla tych innych platform, które mają być używane.</span><span class="sxs-lookup"><span data-stu-id="ac79e-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="ac79e-144">Zobacz [importuje project.json](project-json.md#imports) i [docelowy programu MSBuild przywracania PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="ac79e-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="ac79e-145">Może to spowodować nieoczekiwane wyniki, więc ponownie najlepiej rozwiązać niezgodności pakietu przy pracy z autorem pakietu podczas aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ac79e-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="ac79e-146">Docelowych platform</span><span class="sxs-lookup"><span data-stu-id="ac79e-146">Target frameworks</span></span>

<span data-ttu-id="ac79e-147">*Pierwotnie w [platform docelowych](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="ac79e-148">[Project.JSON](project-json.md): `frameworks` wersji framework, które mogą być kompilowane projektu przed określa węzła.</span><span class="sxs-lookup"><span data-stu-id="ac79e-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="ac79e-149">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="ac79e-149">Creating a package</span></span>

<span data-ttu-id="ac79e-150">*Pierwotnie w [tworzenia pakietu](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="ac79e-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="ac79e-151">Ustawienie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="ac79e-151">Setting a package type</span></span>

<span data-ttu-id="ac79e-152">Z platformą .NET Core 1.x, gdy DotnetCliTool pakiet jest zainstalowany, program Visual Studio umieszcza pakietu w `project.json` `tools` węzła zamiast `dependencies` węzła.</span><span class="sxs-lookup"><span data-stu-id="ac79e-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="ac79e-153">Typy pakietów są ustawiane w `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="ac79e-154">`project.json`: Określ typ pakietu w `packOptions.packageType` właściwości json:</span><span class="sxs-lookup"><span data-stu-id="ac79e-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="ac79e-155">Dodawanie elementów docelowych i właściwości dla programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="ac79e-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="ac79e-156">*Pierwotnie w [tworzenia pakietów NuGet standardowe .NET z programem Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="ac79e-157">Korzystając z `project.json`, elementy docelowe nie zostaną dodane do projektu, ale są udostępniane za pośrednictwem `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="ac79e-158">Przechowywanie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="ac79e-158">Package versioning</span></span>

<span data-ttu-id="ac79e-159">*Pierwotnie w [wersji pakietu](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="ac79e-160">Korzystając z `project.json` formacie NuGet również obsługuje za pomocą notacji symboli wieloznacznych, \*, główna, pomocnicze, poprawki i sufiks wersji wstępnej części numeru.</span><span class="sxs-lookup"><span data-stu-id="ac79e-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="ac79e-161">Odwołanie do pliku NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="ac79e-161">NuGet.Config reference</span></span>

<span data-ttu-id="ac79e-162">*Pierwotnie w [odwołanie do pliku NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="ac79e-163">`globalPackagesFolder` dotyczy tylko `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-163">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="ac79e-164">(Dodanie uwagi: odnosi się także do PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="ac79e-164">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="ac79e-165">Odwołanie do pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="ac79e-165">nuspec file reference</span></span>

<span data-ttu-id="ac79e-166">*Pierwotnie w [odwołania nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-166">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="ac79e-167">`<contentFiles>` Element jest używany zamiast `<files>` z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ac79e-167">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="ac79e-168">Kontrolki opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="ac79e-168">Package manager options control</span></span>

<span data-ttu-id="ac79e-169">*Pierwotnie w [informacje o interfejsie użytkownika Menedżera pakietów](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-169">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="ac79e-170">Projektów przy użyciu `project.json` zarządzania format Pokaż tylko **Pokaż okno podglądu** opcji.</span><span class="sxs-lookup"><span data-stu-id="ac79e-170">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="ac79e-171">Szablony Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac79e-171">Visual Studio Templates</span></span>

<span data-ttu-id="ac79e-172">*Pierwotnie w [pakietów NuGet w szablony Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="ac79e-172">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="ac79e-173">Najlepsze rozwiązania: szablony nie zawierają `project.json` pliku, a nie dołączaj lub żadnych odwołań do zawartości lub zostanie dodany podczas instalowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac79e-173">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>