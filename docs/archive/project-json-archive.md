---
title: Zawartość archiwum Project. JSON elementu NuGet
description: Różne bity zawartości pliku Project. JSON usunięte z innych obszarów dokumentacji programu NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 87116669c1e685ffd0dbe4142c2f7e357c413497
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488245"
---
# <a name="projectjson-archive"></a><span data-ttu-id="f1b1c-103">Archiwum Project. JSON</span><span class="sxs-lookup"><span data-stu-id="f1b1c-103">project.json archive</span></span>

<span data-ttu-id="f1b1c-104">Format `project.json` zarządzania został wprowadzony z pakietem NuGet 3. x i używany dla niektórych typów projektów.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="f1b1c-105">Była przestarzała z wprowadzeniem formatu PackageReference, w którym zależności są wyświetlane bezpośrednio w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="f1b1c-106">Zobacz również:</span><span class="sxs-lookup"><span data-stu-id="f1b1c-106">Also see:</span></span>

- [<span data-ttu-id="f1b1c-107">project.json schema</span><span class="sxs-lookup"><span data-stu-id="f1b1c-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="f1b1c-108">wpływ pliku Project. JSON na autorów pakietów</span><span class="sxs-lookup"><span data-stu-id="f1b1c-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="f1b1c-109">Plik project.json i platforma UWP</span><span class="sxs-lookup"><span data-stu-id="f1b1c-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="f1b1c-110">Format zarządzania project.json</span><span class="sxs-lookup"><span data-stu-id="f1b1c-110">project.json management format</span></span>

<span data-ttu-id="f1b1c-111">*Pierwotnie w ramach [przywracania pakietu](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="f1b1c-112">Na liście formatów zarządzania:</span><span class="sxs-lookup"><span data-stu-id="f1b1c-112">In the list of management formats:</span></span>

- <span data-ttu-id="f1b1c-113">[`project.json`](project-json.md): *(przestarzałe)* plik JSON, który przechowuje listę zależności projektu z ogólnym grafem pakietu w skojarzonym pliku `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="f1b1c-114">Ten format jest przestarzały na korzyść PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="f1b1c-115">Przywracanie NuGet przy mono</span><span class="sxs-lookup"><span data-stu-id="f1b1c-115">nuget restore on Mono</span></span>

<span data-ttu-id="f1b1c-116">*Pierwotnie [zainstalowane narzędzia klienta NuGet](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="f1b1c-117">Współpracuje z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="f1b1c-118">Ograniczanie wersji pakietów przy użyciu funkcji przywracania</span><span class="sxs-lookup"><span data-stu-id="f1b1c-118">Constraining package versions with restore</span></span>

<span data-ttu-id="f1b1c-119">*Pierwotnie w ramach [przywracania pakietu](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-119">*Originally in [Package restore](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span></span>

- <span data-ttu-id="f1b1c-120">`project.json`: Określ zakres wersji bezpośrednio z numerem wersji zależności.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="f1b1c-121">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f1b1c-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="f1b1c-122">Poleceń interfejsu wiersza polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="f1b1c-122">NuGet CLI commands</span></span>

- <span data-ttu-id="f1b1c-123">`nuget install`nie działa z `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="f1b1c-124">`nuget restore`: w przypadku projektów `project.json`korzystających z `project.lock.json` programu Program generuje `<project>.nuget.props` plik i plik, w razie konieczności.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="f1b1c-125">(Oba pliki można pominąć z kontroli źródła). Argument może wskazywać plik i ma takie samo `packages.config` zachowanie jak wskazanie pliku projektu lub. `project.json` `<projectPath>`</span><span class="sxs-lookup"><span data-stu-id="f1b1c-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="f1b1c-126">W kolejności według priorytetu dla folderów pakietów `%userprofile%\.nuget\packages` program jest wyszukiwany `project.json`jako pierwszy podczas korzystania z programu.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="f1b1c-127">`nuget update`: W przypadku mono to polecenie nie działa z projektami przy użyciu `project.json`programu.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="f1b1c-128">Rozpoznawanie zależności z PackageReference</span><span class="sxs-lookup"><span data-stu-id="f1b1c-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="f1b1c-129">*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-129">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="f1b1c-130">Zachowanie PackageReference ma zastosowanie również do `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="f1b1c-131">Funkcja przywracania NuGet zapisuje wykres zależności w pliku o nazwie `project.lock.json` obok `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="f1b1c-132">Zarządzanie zasobami zależności</span><span class="sxs-lookup"><span data-stu-id="f1b1c-132">Managing dependency assets</span></span>

<span data-ttu-id="f1b1c-133">*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-133">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="f1b1c-134">W przypadku korzystania `project.json` z formatu można kontrolować, które zasoby z zależności są przepływem do projektu najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="f1b1c-135">Aby uzyskać szczegółowe informacje, zobacz plik [Project. JSON](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="f1b1c-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="f1b1c-136">Wykluczanie odwołań</span><span class="sxs-lookup"><span data-stu-id="f1b1c-136">Excluding references</span></span>

<span data-ttu-id="f1b1c-137">*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-137">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="f1b1c-138">`project.json`: Dodaj `"exclude" : "all"` w zależności od PackageC:</span><span class="sxs-lookup"><span data-stu-id="f1b1c-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="f1b1c-139">Rozwiązywanie niezgodnych błędów pakietów</span><span class="sxs-lookup"><span data-stu-id="f1b1c-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="f1b1c-140">*Pierwotnie w ramach [rozpoznawania zależności](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-140">*Originally in [Dependency resolution](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="f1b1c-141">Dodano metodę rozwiązywania błędów:</span><span class="sxs-lookup"><span data-stu-id="f1b1c-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="f1b1c-142">**Niezalecane**: jako rozwiązanie tymczasowe podczas pracy z autorem pakietu, projekty `netcore`mające znaczenie, `netstandard`i `netcoreapp` mogą wskazywać inne struktury jako zgodne, umożliwiając tym samym stosowanie pakietów docelowych platformy, które mają być używane.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="f1b1c-143">Zobacz plik [Project. JSON Imports](project-json.md#imports) i [element docelowy przywracania MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="f1b1c-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="f1b1c-144">Może to spowodować nieoczekiwane zachowanie, dlatego najlepiej rozwiązać niezgodności pakietów, pracując z autorem pakietu w ramach aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="f1b1c-145">Platformy docelowe</span><span class="sxs-lookup"><span data-stu-id="f1b1c-145">Target frameworks</span></span>

<span data-ttu-id="f1b1c-146">*Początkowo w [strukturach docelowych](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="f1b1c-147">[project.json](project-json.md): `frameworks` Węzeł określa wersje architektury, względem których można skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="f1b1c-148">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="f1b1c-148">Creating a package</span></span>

<span data-ttu-id="f1b1c-149">*Pierwotnie podczas [tworzenia pakietu](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="f1b1c-150">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="f1b1c-150">Setting a package type</span></span>

<span data-ttu-id="f1b1c-151">W przypadku programu .NET Core 1. x po zainstalowaniu pakietu DotnetCliTool program Visual Studio umieszcza pakiet w `project.json` `tools` węźle, a nie `dependencies` w węźle.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="f1b1c-152">Typy pakietów są ustawione w `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="f1b1c-153">`project.json`: Wskaż typ pakietu w pliku `packOptions.packageType` json właściwości:</span><span class="sxs-lookup"><span data-stu-id="f1b1c-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="f1b1c-154">Dodawanie elementów docelowych i właściwości dla programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="f1b1c-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="f1b1c-155">*Pierwotnie [twórz .NET standard pakiety NuGet przy użyciu programu Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="f1b1c-156">W przypadku `project.json`korzystania z obiektów docelowych nie są dodawane do projektu, ale są udostępniane `project.lock.json`za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="f1b1c-157">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="f1b1c-157">Package versioning</span></span>

<span data-ttu-id="f1b1c-158">*Początkowo w [wersji pakietu](../concepts/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-158">*Originally in [Package versioning](../concepts/package-versioning.md).*</span></span>

<span data-ttu-id="f1b1c-159">W przypadku korzystania `project.json` z formatu, pakiet NuGet obsługuje również używanie \*notacji wieloznacznej, w przypadku elementów głównych, pomocniczych, poprawek i prefiksu w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="f1b1c-160">Dokumentacja NuGet. config</span><span class="sxs-lookup"><span data-stu-id="f1b1c-160">NuGet.Config reference</span></span>

<span data-ttu-id="f1b1c-161">*Pierwotnie w [dokumentacji NuGet. config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="f1b1c-162">`globalPackagesFolder`ma zastosowanie tylko `project.json`do.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="f1b1c-163">(Dodana Uwaga: dotyczy także PackageReference).</span><span class="sxs-lookup"><span data-stu-id="f1b1c-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="f1b1c-164">odwołanie do pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="f1b1c-164">nuspec file reference</span></span>

<span data-ttu-id="f1b1c-165">*Pierwotnie w [nuspec Reference](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="f1b1c-166">Element jest używany `<files>` zamiast `project.json`. `<contentFiles>`</span><span class="sxs-lookup"><span data-stu-id="f1b1c-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="f1b1c-167">Kontrola opcji Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="f1b1c-167">Package manager options control</span></span>

<span data-ttu-id="f1b1c-168">*Pierwotnie w [dokumentacji interfejsu użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-168">*Originally in [Package Manager UI reference](../consume-packages/install-use-packages-visual-studio.md).*</span></span>

<span data-ttu-id="f1b1c-169">Projekty używające `project.json` formatu zarządzania pokazują tylko opcję **Pokaż podgląd okna** .</span><span class="sxs-lookup"><span data-stu-id="f1b1c-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="f1b1c-170">Szablony Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1b1c-170">Visual Studio Templates</span></span>

<span data-ttu-id="f1b1c-171">*Początkowo w [pakietach NuGet w szablonach programu Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="f1b1c-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="f1b1c-172">Najlepsze rozwiązania: szablony nie zawierają `project.json` plików i nie zawierają odwołań ani zawartości, które zostałyby dodane po zainstalowaniu pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1b1c-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>