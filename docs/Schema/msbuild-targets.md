---
title: "NuGet pakietu i ich przywracania docelowych elementów MSBuild | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "Pakiet NuGet i przywracania może współpracować bezpośrednio jako docelowych elementów MSBuild nuget 4.0 +."
keywords: NuGet i MSBuild, docelowy pakietu NuGet, docelowy przywracania NuGet
ms.reviewer: karann-msft
ms.openlocfilehash: d4778a21a96de6d76d7a20ff9a305960dd6c2bf1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="da72c-104">Pakiet NuGet i przywracania jako docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="da72c-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="da72c-105">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="da72c-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="da72c-106">NuGet 4.0 + może współpracować bezpośrednio z informacji w `.csproj` pliku bez konieczności oddzielnego `.nuspec` lub `project.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="da72c-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="da72c-107">Metadane, które wcześniej były przechowywane w tych plikach konfiguracji, które mogą być zamiast tego przechowywane w `.csproj` pliku bezpośrednio, zgodnie z opisem w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="da72c-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="da72c-108">Przy użyciu programu MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` celem zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="da72c-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="da72c-109">Następujących elementów docelowych umożliwiają pracę z programem NuGet, tak jak inne zadanie programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="da72c-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="da72c-110">(Programu NuGet 3.x i wcześniej, użyj [pakietu](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast tego polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="da72c-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="da72c-111">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="da72c-111">In this topic:</span></span>

- [<span data-ttu-id="da72c-112">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="da72c-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="da72c-113">docelowy pakiet</span><span class="sxs-lookup"><span data-stu-id="da72c-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="da72c-114">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="da72c-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="da72c-115">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="da72c-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="da72c-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="da72c-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="da72c-117">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="da72c-117">Target build order</span></span>

<span data-ttu-id="da72c-118">Ponieważ `pack` i `restore` MSBuild elementów docelowych, można wywołać w celu zwiększenia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="da72c-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="da72c-119">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu go.</span><span class="sxs-lookup"><span data-stu-id="da72c-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="da72c-120">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="da72c-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="da72c-121">Podobnie można zapisać zadania programu MSBuild, napisać własny docelowych i korzystać z właściwości NuGet w zadanie programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="da72c-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="da72c-122">docelowy pakiet</span><span class="sxs-lookup"><span data-stu-id="da72c-122">pack target</span></span>

<span data-ttu-id="da72c-123">Korzystając z docelowym pakietu, oznacza to, `msbuild /t:pack`, MSBuild rysuje wejścia z `.csproj` pliku zamiast `project.json` lub `.nuspec` plików.</span><span class="sxs-lookup"><span data-stu-id="da72c-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="da72c-124">W poniższej tabeli opisano właściwości programu MSBuild, które mogą zostać dodane do `.csproj` pliku w pierwszym `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="da72c-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="da72c-125">Wprowadź te zmiany łatwe w Visual Studio 2017 i później przez kliknięcie prawym przyciskiem myszy projekt i wybierając **edytować {nazwa_projektu}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="da72c-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="da72c-126">Dla wygody tabeli jest zorganizowana według równoważne właściwości w [ `.nuspec` pliku](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="da72c-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="da72c-127">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane przy użyciu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="da72c-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="da72c-128">Wartość atrybutu/NuSpec.</span><span class="sxs-lookup"><span data-stu-id="da72c-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="da72c-129">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="da72c-129">MSBuild Property</span></span> | <span data-ttu-id="da72c-130">Domyślny</span><span class="sxs-lookup"><span data-stu-id="da72c-130">Default</span></span> | <span data-ttu-id="da72c-131">Uwagi</span><span class="sxs-lookup"><span data-stu-id="da72c-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="da72c-132">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="da72c-132">Id</span></span> | <span data-ttu-id="da72c-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="da72c-133">PackageId</span></span> | <span data-ttu-id="da72c-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="da72c-134">AssemblyName</span></span> | <span data-ttu-id="da72c-135">$(AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="da72c-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="da72c-136">Wersja</span><span class="sxs-lookup"><span data-stu-id="da72c-136">Version</span></span> | <span data-ttu-id="da72c-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="da72c-137">PackageVersion</span></span> | <span data-ttu-id="da72c-138">Wersja</span><span class="sxs-lookup"><span data-stu-id="da72c-138">Version</span></span> | <span data-ttu-id="da72c-139">Jest to zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" programu semver</span><span class="sxs-lookup"><span data-stu-id="da72c-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="da72c-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="da72c-140">VersionPrefix</span></span> | <span data-ttu-id="da72c-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="da72c-141">PackageVersionPrefix</span></span> | <span data-ttu-id="da72c-142">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-142">empty</span></span> | <span data-ttu-id="da72c-143">Ustawienie PackageVersion spowoduje zastąpienie PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="da72c-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="da72c-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="da72c-144">VersionSuffix</span></span> | <span data-ttu-id="da72c-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="da72c-145">PackageVersionSuffix</span></span> | <span data-ttu-id="da72c-146">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-146">empty</span></span> | <span data-ttu-id="da72c-147">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="da72c-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="da72c-148">Ustawienie PackageVersion spowoduje zastąpienie PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="da72c-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="da72c-149">Autorzy</span><span class="sxs-lookup"><span data-stu-id="da72c-149">Authors</span></span> | <span data-ttu-id="da72c-150">Autorzy</span><span class="sxs-lookup"><span data-stu-id="da72c-150">Authors</span></span> | <span data-ttu-id="da72c-151">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="da72c-151">Username of the current user</span></span> | |
| <span data-ttu-id="da72c-152">Właściciele</span><span class="sxs-lookup"><span data-stu-id="da72c-152">Owners</span></span> | <span data-ttu-id="da72c-153">Brak</span><span class="sxs-lookup"><span data-stu-id="da72c-153">N/A</span></span> | <span data-ttu-id="da72c-154">Nie istnieje w pliku NuSpec</span><span class="sxs-lookup"><span data-stu-id="da72c-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="da72c-155">Tytuł</span><span class="sxs-lookup"><span data-stu-id="da72c-155">Title</span></span> | <span data-ttu-id="da72c-156">Tytuł</span><span class="sxs-lookup"><span data-stu-id="da72c-156">Title</span></span> | <span data-ttu-id="da72c-157">PackageId</span><span class="sxs-lookup"><span data-stu-id="da72c-157">The PackageId</span></span>| |
| <span data-ttu-id="da72c-158">Opis</span><span class="sxs-lookup"><span data-stu-id="da72c-158">Description</span></span> | <span data-ttu-id="da72c-159">Opis</span><span class="sxs-lookup"><span data-stu-id="da72c-159">Description</span></span> | <span data-ttu-id="da72c-160">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="da72c-160">"Package Description"</span></span> | |
| <span data-ttu-id="da72c-161">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="da72c-161">Copyright</span></span> | <span data-ttu-id="da72c-162">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="da72c-162">Copyright</span></span> | <span data-ttu-id="da72c-163">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-163">empty</span></span> | |
| <span data-ttu-id="da72c-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="da72c-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="da72c-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="da72c-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="da72c-166">false</span><span class="sxs-lookup"><span data-stu-id="da72c-166">false</span></span> | |
| <span data-ttu-id="da72c-167">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-167">LicenseUrl</span></span> | <span data-ttu-id="da72c-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-168">PackageLicenseUrl</span></span> | <span data-ttu-id="da72c-169">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-169">empty</span></span> | |
| <span data-ttu-id="da72c-170">adresem projectUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-170">ProjectUrl</span></span> | <span data-ttu-id="da72c-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-171">PackageProjectUrl</span></span> | <span data-ttu-id="da72c-172">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-172">empty</span></span> | |
| <span data-ttu-id="da72c-173">iconUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-173">IconUrl</span></span> | <span data-ttu-id="da72c-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-174">PackageIconUrl</span></span> | <span data-ttu-id="da72c-175">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-175">empty</span></span> | |
| <span data-ttu-id="da72c-176">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="da72c-176">Tags</span></span> | <span data-ttu-id="da72c-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="da72c-177">PackageTags</span></span> | <span data-ttu-id="da72c-178">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-178">empty</span></span> | <span data-ttu-id="da72c-179">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="da72c-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="da72c-180">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="da72c-180">ReleaseNotes</span></span> | <span data-ttu-id="da72c-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="da72c-181">PackageReleaseNotes</span></span> | <span data-ttu-id="da72c-182">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-182">empty</span></span> | |
| <span data-ttu-id="da72c-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-183">RepositoryUrl</span></span> | <span data-ttu-id="da72c-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-184">RepositoryUrl</span></span> | <span data-ttu-id="da72c-185">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-185">empty</span></span> | |
| <span data-ttu-id="da72c-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="da72c-186">RepositoryType</span></span> | <span data-ttu-id="da72c-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="da72c-187">RepositoryType</span></span> | <span data-ttu-id="da72c-188">empty</span><span class="sxs-lookup"><span data-stu-id="da72c-188">empty</span></span> | |
| <span data-ttu-id="da72c-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="da72c-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="da72c-190">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="da72c-190">Summary</span></span> | <span data-ttu-id="da72c-191">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="da72c-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="da72c-192">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="da72c-192">pack target inputs</span></span>

- <span data-ttu-id="da72c-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="da72c-193">IsPackable</span></span>
- <span data-ttu-id="da72c-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="da72c-194">PackageVersion</span></span>
- <span data-ttu-id="da72c-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="da72c-195">PackageId</span></span>
- <span data-ttu-id="da72c-196">Autorzy</span><span class="sxs-lookup"><span data-stu-id="da72c-196">Authors</span></span>
- <span data-ttu-id="da72c-197">Opis</span><span class="sxs-lookup"><span data-stu-id="da72c-197">Description</span></span>
- <span data-ttu-id="da72c-198">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="da72c-198">Copyright</span></span>
- <span data-ttu-id="da72c-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="da72c-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="da72c-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="da72c-200">DevelopmentDependency</span></span>
- <span data-ttu-id="da72c-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="da72c-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-202">PackageProjectUrl</span></span>
- <span data-ttu-id="da72c-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-203">PackageIconUrl</span></span>
- <span data-ttu-id="da72c-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="da72c-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="da72c-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="da72c-205">PackageTags</span></span>
- <span data-ttu-id="da72c-206">Ścieżki PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="da72c-206">PackageOutputPath</span></span>
- <span data-ttu-id="da72c-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="da72c-207">IncludeSymbols</span></span>
- <span data-ttu-id="da72c-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="da72c-208">IncludeSource</span></span>
- <span data-ttu-id="da72c-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="da72c-209">PackageTypes</span></span>
- <span data-ttu-id="da72c-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="da72c-210">IsTool</span></span>
- <span data-ttu-id="da72c-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-211">RepositoryUrl</span></span>
- <span data-ttu-id="da72c-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="da72c-212">RepositoryType</span></span>
- <span data-ttu-id="da72c-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="da72c-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="da72c-214">Element MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="da72c-214">MinClientVersion</span></span>
- <span data-ttu-id="da72c-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="da72c-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="da72c-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="da72c-216">IncludeContentInPack</span></span>
- <span data-ttu-id="da72c-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="da72c-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="da72c-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="da72c-218">ContentTargetFolders</span></span>
- <span data-ttu-id="da72c-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="da72c-219">NuspecFile</span></span>
- <span data-ttu-id="da72c-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="da72c-220">NuspecBasePath</span></span>
- <span data-ttu-id="da72c-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="da72c-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="da72c-222">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="da72c-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="da72c-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="da72c-223">PackageIconUrl</span></span>

<span data-ttu-id="da72c-224">Zmiana w ramach [2582 problem NuGet](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` po pewnym czasie zostaną zmienione na `PackageIconUri` i może być względna ścieżka do pliku ikony, które zostaną uwzględnione w katalogu głównym wynikowy pakiet.</span><span class="sxs-lookup"><span data-stu-id="da72c-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="da72c-225">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="da72c-225">Output assemblies</span></span>

<span data-ttu-id="da72c-226">`nuget pack`kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="da72c-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="da72c-227">Pliki wyjściowe, które są kopiowane są zależne od MSBuild zapewnia z `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="da72c-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="da72c-228">Istnieją dwie właściwości programu MSBuild, które są dostępne w pliku projektu lub wiersza polecenia w celu sterowania gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="da72c-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="da72c-229">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="da72c-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="da72c-230">`BuildOutputTargetFolder`: Określa folder, w którym ma zostać umieszczony zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="da72c-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="da72c-231">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich framework folderów.</span><span class="sxs-lookup"><span data-stu-id="da72c-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="da72c-232">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="da72c-232">Package references</span></span>

<span data-ttu-id="da72c-233">Zobacz [pakietu odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="da72c-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="da72c-234">Projekt do odwołań projektu</span><span class="sxs-lookup"><span data-stu-id="da72c-234">Project to project references</span></span>

<span data-ttu-id="da72c-235">Projekt do odwołań projektu są traktowane jako domyślnie jako odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="da72c-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="da72c-236">Można również dodać następujące metadane odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="da72c-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="da72c-237">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="da72c-237">Including content in a package</span></span>

<span data-ttu-id="da72c-238">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="da72c-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="da72c-239">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że nadpiszesz zapisami jak następujące:</span><span class="sxs-lookup"><span data-stu-id="da72c-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="da72c-240">Domyślnie pobiera wszystkie elementy dodane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje struktury folder względny, o ile nie zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="da72c-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="da72c-241">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` oba), można użyć właściwości programu MSBuild `ContentTargetFolders`, jakie nie "zawartość; pliki", ale może być ustawiony na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="da72c-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="da72c-242">Należy pamiętać, że po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="da72c-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="da72c-243">`PackagePath`może być rozdzielone średnikami zbiór ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="da72c-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="da72c-244">Określenie ścieżki pusty pakietu dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="da72c-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="da72c-245">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="da72c-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="da72c-246">Istnieje również właściwość MSBuild `$(IncludeContentInPack)`, jakie nie `true`.</span><span class="sxs-lookup"><span data-stu-id="da72c-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="da72c-247">Jeśli ta wartość jest równa `false` w żadnym projekcie następnie zawartość z tego projektu nie znajdują się w pakiecie nuget.</span><span class="sxs-lookup"><span data-stu-id="da72c-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="da72c-248">Zawiera inne metadane określonego pakietu, które można ustawić na żadnym z powyższych elementów ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który określa ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpisu w pliku nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="da72c-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="da72c-249">Oprócz elementy zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić na pliki z akcją kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="da72c-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="da72c-250">Pakiet można dołączyć nazwę pliku do ścieżki pakietu przy użyciu globbing wzorców ścieżka do pakietu musi być zakończona z folderu znak separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełna ścieżka, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="da72c-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="da72c-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="da72c-251">IncludeSymbols</span></span>

<span data-ttu-id="da72c-252">Korzystając z `MSBuild /t:pack /p:IncludeSymbols=true`, odpowiadającego `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="da72c-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="da72c-253">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="da72c-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="da72c-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="da72c-254">IncludeSource</span></span>

<span data-ttu-id="da72c-255">To jest taka sama jak `IncludeSymbols`, ale kopiuje pliki źródłowe wraz z programem `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="da72c-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="da72c-256">Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną w pakiecie wynikowy.</span><span class="sxs-lookup"><span data-stu-id="da72c-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="da72c-257">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` ustawioną `false`.</span><span class="sxs-lookup"><span data-stu-id="da72c-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="da72c-258">Jeśli plik typu skompilować, znajduje się poza folderu projektu, a następnie wystarczy dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="da72c-258">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="da72c-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="da72c-259">IsTool</span></span>

<span data-ttu-id="da72c-260">Korzystając z `MSBuild /t:pack /p:IsTool=true`, wszystkie dane wyjściowe pliki, jak określono w [zestawy danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folder zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="da72c-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="da72c-261">Należy pamiętać, że jest inny niż `DotNetCliTool` który jest określany przez ustawienie `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="da72c-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="da72c-262">Przy użyciu .nuspec pakowania</span><span class="sxs-lookup"><span data-stu-id="da72c-262">Packing using a .nuspec</span></span>

<span data-ttu-id="da72c-263">Można użyć `.nuspec` plik można spakować projektu, pod warunkiem, że masz plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` , dzięki czemu mogą być wykonywane zadanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="da72c-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="da72c-264">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="da72c-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="da72c-265">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` pliku używany na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="da72c-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="da72c-266">`NuspecProperties`: Rozdzielana średnikami lista klucz = pary wartości.</span><span class="sxs-lookup"><span data-stu-id="da72c-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="da72c-267">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild, wiele właściwości musi być następujący: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="da72c-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="da72c-268">`NuspecBasePath`: Ścieżki podstawowa dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="da72c-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="da72c-269">Jeśli przy użyciu `dotnet.exe` pakowania projektu, użyj polecenia podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="da72c-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="da72c-270">Jeśli pakiet projektu za pomocą programu MSBuild, należy użyć polecenia podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="da72c-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="da72c-271">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="da72c-271">restore target</span></span>

<span data-ttu-id="da72c-272">`MSBuild /t:restore`(który `nuget restore` i `dotnet restore` za pomocą platformy .NET Core projektów), przywraca pakietów, do których odwołuje się w pliku projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="da72c-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="da72c-273">Przeczytaj wszystkich odwołań do projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="da72c-273">Read all project to project references</span></span>
1. <span data-ttu-id="da72c-274">Właściwości projektu, aby znaleźć pośredniego struktury folderów i obiekt docelowy do odczytu</span><span class="sxs-lookup"><span data-stu-id="da72c-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="da72c-275">Przekazywanie danych msbuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="da72c-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="da72c-276">Uruchamianie przywracania</span><span class="sxs-lookup"><span data-stu-id="da72c-276">Run restore</span></span>
1. <span data-ttu-id="da72c-277">Pobieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="da72c-277">Download packages</span></span>
1. <span data-ttu-id="da72c-278">Zapis plików zasobów, cele i właściwości</span><span class="sxs-lookup"><span data-stu-id="da72c-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="da72c-279">Przywróć właściwości</span><span class="sxs-lookup"><span data-stu-id="da72c-279">Restore properties</span></span>

<span data-ttu-id="da72c-280">Przywróć dodatkowe ustawienia mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="da72c-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="da72c-281">Można również ustawić wartości z wiersza polecenia przy użyciu `/p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="da72c-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="da72c-282">Właściwość</span><span class="sxs-lookup"><span data-stu-id="da72c-282">Property</span></span> | <span data-ttu-id="da72c-283">Opis</span><span class="sxs-lookup"><span data-stu-id="da72c-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="da72c-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="da72c-284">RestoreSources</span></span> | <span data-ttu-id="da72c-285">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="da72c-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="da72c-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="da72c-286">RestorePackagesPath</span></span> | <span data-ttu-id="da72c-287">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="da72c-287">User packages folder path.</span></span> |
| <span data-ttu-id="da72c-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="da72c-288">RestoreDisableParallel</span></span> | <span data-ttu-id="da72c-289">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="da72c-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="da72c-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="da72c-290">RestoreConfigFile</span></span> | <span data-ttu-id="da72c-291">Ścieżka do `Nuget.Config` pliku w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="da72c-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="da72c-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="da72c-292">RestoreNoCache</span></span> | <span data-ttu-id="da72c-293">Jeśli PRAWDA, pozwala uniknąć przy użyciu pamięci podręcznej sieci web.</span><span class="sxs-lookup"><span data-stu-id="da72c-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="da72c-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="da72c-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="da72c-295">Jeśli PRAWDA, ignoruje wystąpił błąd lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="da72c-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="da72c-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="da72c-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="da72c-297">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="da72c-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="da72c-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="da72c-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="da72c-299">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="da72c-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="da72c-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="da72c-300">RestoreOutputPath</span></span> | <span data-ttu-id="da72c-301">Folder wyjściowy, przyjęty `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="da72c-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="da72c-302">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="da72c-302">**Examples**</span></span>

<span data-ttu-id="da72c-303">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="da72c-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="da72c-304">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="da72c-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="da72c-305">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="da72c-305">Restore outputs</span></span>

<span data-ttu-id="da72c-306">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="da72c-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="da72c-307">Plik</span><span class="sxs-lookup"><span data-stu-id="da72c-307">File</span></span> | <span data-ttu-id="da72c-308">Opis</span><span class="sxs-lookup"><span data-stu-id="da72c-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="da72c-309">Wcześniej`project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="da72c-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="da72c-310">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="da72c-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="da72c-311">Odwołania do zawartych w pakietach docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="da72c-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="da72c-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="da72c-312">PackageTargetFallback</span></span> 

<span data-ttu-id="da72c-313">`PackageTargetFallback` Element służy do określenia zestawu zgodne cele, które mają być użyte podczas przywracania pakietów (odpowiednik [ `imports` w `project.json` ](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="da72c-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="da72c-314">Został zaprojektowany tak, aby umożliwić pakiety, które używają dotnet [TxM](../schema/target-frameworks.md) do pracy z pakietami zgodne, które nie deklaruje dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="da72c-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="da72c-315">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkie pakiety zależy on od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do projektu, aby umożliwić platformy dotnet z systemem innym niż był zgodny z dotnet.</span><span class="sxs-lookup"><span data-stu-id="da72c-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="da72c-316">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależny pakiet zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projekt zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="da72c-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="da72c-317">Jeśli chcesz przenieść jest ostatnim biblioteki DLL, a następnie można dodać `PackageTargetFallback` w następujący sposób, aby oznacza, że `portable-net45+win81` zgodnego biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="da72c-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="da72c-318">Aby zadeklarować używane dla wszystkich elementów docelowych w projekcie, pozostaw `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="da72c-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="da72c-319">Można również rozszerzyć zasięg wszelkie istniejące `PackageTargetFallback` przez dołączenie `$(PackageTargetFallback)` w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="da72c-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="da72c-320">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="da72c-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="da72c-321">Jeśli przywracania jest Przywracanie nieprawidłowy zestaw, jest możliwe do wykluczenia z pakietów domyślny wybór i zamień ją na dowolny inny.</span><span class="sxs-lookup"><span data-stu-id="da72c-321">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="da72c-322">Pierwszy z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="da72c-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="da72c-323">Następnie dodaj własne odwołanie do odpowiedniego lokalną kopię pliku DLL:</span><span class="sxs-lookup"><span data-stu-id="da72c-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
