---
title: "NuGet pakietu i ich przywracania docelowych elementów MSBuild | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Pakiet NuGet i przywracania może współpracować bezpośrednio jako docelowych elementów MSBuild nuget 4.0 +."
keywords: NuGet i MSBuild, docelowy pakietu NuGet, docelowy przywracania NuGet
ms.reviewer:
- karann-msft
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="7eba9-104">Pakiet NuGet i przywracania jako docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="7eba9-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="7eba9-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="7eba9-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="7eba9-106">W formacie PackageReference NuGet 4.0 + mogą przechowywać wszystkie manifestu metadanych bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="7eba9-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="7eba9-107">Przy użyciu programu MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` celem zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="7eba9-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="7eba9-108">Następujących elementów docelowych umożliwiają pracę z programem NuGet, tak jak inne zadanie programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="7eba9-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="7eba9-109">(Programu NuGet 3.x i wcześniej, użyj [pakietu](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast tego polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="7eba9-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="7eba9-110">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="7eba9-110">Target build order</span></span>

<span data-ttu-id="7eba9-111">Ponieważ `pack` i `restore` MSBuild elementów docelowych, można wywołać w celu zwiększenia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="7eba9-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="7eba9-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu go.</span><span class="sxs-lookup"><span data-stu-id="7eba9-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="7eba9-113">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="7eba9-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="7eba9-114">Podobnie można zapisać zadania programu MSBuild, napisać własny docelowych i korzystać z właściwości NuGet w zadanie programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="7eba9-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="7eba9-115">docelowy pakiet</span><span class="sxs-lookup"><span data-stu-id="7eba9-115">pack target</span></span>

<span data-ttu-id="7eba9-116">Korzystając z docelowym pakietu, oznacza to, `msbuild /t:pack`, MSBuild rysuje wejścia z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="7eba9-117">W poniższej tabeli opisano właściwości programu MSBuild, które mogą zostać dodane do pliku projektu w pierwszym `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="7eba9-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="7eba9-118">Wprowadź te zmiany łatwe w Visual Studio 2017 i później przez kliknięcie prawym przyciskiem myszy projekt i wybierając **edytować {nazwa_projektu}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="7eba9-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="7eba9-119">Dla wygody tabeli jest zorganizowana według równoważne właściwości w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="7eba9-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="7eba9-120">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane przy użyciu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="7eba9-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="7eba9-121">Wartość atrybutu/NuSpec.</span><span class="sxs-lookup"><span data-stu-id="7eba9-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="7eba9-122">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="7eba9-122">MSBuild Property</span></span> | <span data-ttu-id="7eba9-123">Domyślny</span><span class="sxs-lookup"><span data-stu-id="7eba9-123">Default</span></span> | <span data-ttu-id="7eba9-124">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7eba9-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="7eba9-125">Id</span><span class="sxs-lookup"><span data-stu-id="7eba9-125">Id</span></span> | <span data-ttu-id="7eba9-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="7eba9-126">PackageId</span></span> | <span data-ttu-id="7eba9-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="7eba9-127">AssemblyName</span></span> | <span data-ttu-id="7eba9-128">$(AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="7eba9-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="7eba9-129">Wersja</span><span class="sxs-lookup"><span data-stu-id="7eba9-129">Version</span></span> | <span data-ttu-id="7eba9-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="7eba9-130">PackageVersion</span></span> | <span data-ttu-id="7eba9-131">Wersja</span><span class="sxs-lookup"><span data-stu-id="7eba9-131">Version</span></span> | <span data-ttu-id="7eba9-132">Jest to zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" programu semver</span><span class="sxs-lookup"><span data-stu-id="7eba9-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="7eba9-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="7eba9-133">VersionPrefix</span></span> | <span data-ttu-id="7eba9-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="7eba9-134">PackageVersionPrefix</span></span> | <span data-ttu-id="7eba9-135">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-135">empty</span></span> | <span data-ttu-id="7eba9-136">Ustawienie PackageVersion zastępuje PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="7eba9-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="7eba9-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="7eba9-137">VersionSuffix</span></span> | <span data-ttu-id="7eba9-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="7eba9-138">PackageVersionSuffix</span></span> | <span data-ttu-id="7eba9-139">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-139">empty</span></span> | <span data-ttu-id="7eba9-140">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="7eba9-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="7eba9-141">Ustawienie PackageVersion zastępuje PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="7eba9-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="7eba9-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="7eba9-142">Authors</span></span> | <span data-ttu-id="7eba9-143">Autorzy</span><span class="sxs-lookup"><span data-stu-id="7eba9-143">Authors</span></span> | <span data-ttu-id="7eba9-144">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="7eba9-144">Username of the current user</span></span> | |
| <span data-ttu-id="7eba9-145">Właściciele</span><span class="sxs-lookup"><span data-stu-id="7eba9-145">Owners</span></span> | <span data-ttu-id="7eba9-146">Brak</span><span class="sxs-lookup"><span data-stu-id="7eba9-146">N/A</span></span> | <span data-ttu-id="7eba9-147">Nie istnieje w pliku NuSpec</span><span class="sxs-lookup"><span data-stu-id="7eba9-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="7eba9-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="7eba9-148">Title</span></span> | <span data-ttu-id="7eba9-149">Tytuł</span><span class="sxs-lookup"><span data-stu-id="7eba9-149">Title</span></span> | <span data-ttu-id="7eba9-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="7eba9-150">The PackageId</span></span>| |
| <span data-ttu-id="7eba9-151">Opis</span><span class="sxs-lookup"><span data-stu-id="7eba9-151">Description</span></span> | <span data-ttu-id="7eba9-152">Opis</span><span class="sxs-lookup"><span data-stu-id="7eba9-152">Description</span></span> | <span data-ttu-id="7eba9-153">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="7eba9-153">"Package Description"</span></span> | |
| <span data-ttu-id="7eba9-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="7eba9-154">Copyright</span></span> | <span data-ttu-id="7eba9-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="7eba9-155">Copyright</span></span> | <span data-ttu-id="7eba9-156">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-156">empty</span></span> | |
| <span data-ttu-id="7eba9-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="7eba9-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="7eba9-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="7eba9-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="7eba9-159">false</span><span class="sxs-lookup"><span data-stu-id="7eba9-159">false</span></span> | |
| <span data-ttu-id="7eba9-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-160">LicenseUrl</span></span> | <span data-ttu-id="7eba9-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-161">PackageLicenseUrl</span></span> | <span data-ttu-id="7eba9-162">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-162">empty</span></span> | |
| <span data-ttu-id="7eba9-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-163">ProjectUrl</span></span> | <span data-ttu-id="7eba9-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-164">PackageProjectUrl</span></span> | <span data-ttu-id="7eba9-165">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-165">empty</span></span> | |
| <span data-ttu-id="7eba9-166">iconUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-166">IconUrl</span></span> | <span data-ttu-id="7eba9-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-167">PackageIconUrl</span></span> | <span data-ttu-id="7eba9-168">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-168">empty</span></span> | |
| <span data-ttu-id="7eba9-169">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="7eba9-169">Tags</span></span> | <span data-ttu-id="7eba9-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="7eba9-170">PackageTags</span></span> | <span data-ttu-id="7eba9-171">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-171">empty</span></span> | <span data-ttu-id="7eba9-172">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="7eba9-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="7eba9-173">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="7eba9-173">ReleaseNotes</span></span> | <span data-ttu-id="7eba9-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="7eba9-174">PackageReleaseNotes</span></span> | <span data-ttu-id="7eba9-175">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-175">empty</span></span> | |
| <span data-ttu-id="7eba9-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-176">RepositoryUrl</span></span> | <span data-ttu-id="7eba9-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-177">RepositoryUrl</span></span> | <span data-ttu-id="7eba9-178">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-178">empty</span></span> | |
| <span data-ttu-id="7eba9-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="7eba9-179">RepositoryType</span></span> | <span data-ttu-id="7eba9-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="7eba9-180">RepositoryType</span></span> | <span data-ttu-id="7eba9-181">empty</span><span class="sxs-lookup"><span data-stu-id="7eba9-181">empty</span></span> | |
| <span data-ttu-id="7eba9-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="7eba9-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="7eba9-183">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="7eba9-183">Summary</span></span> | <span data-ttu-id="7eba9-184">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="7eba9-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="7eba9-185">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="7eba9-185">pack target inputs</span></span>

- <span data-ttu-id="7eba9-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="7eba9-186">IsPackable</span></span>
- <span data-ttu-id="7eba9-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="7eba9-187">PackageVersion</span></span>
- <span data-ttu-id="7eba9-188">PackageId</span><span class="sxs-lookup"><span data-stu-id="7eba9-188">PackageId</span></span>
- <span data-ttu-id="7eba9-189">Autorzy</span><span class="sxs-lookup"><span data-stu-id="7eba9-189">Authors</span></span>
- <span data-ttu-id="7eba9-190">Opis</span><span class="sxs-lookup"><span data-stu-id="7eba9-190">Description</span></span>
- <span data-ttu-id="7eba9-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="7eba9-191">Copyright</span></span>
- <span data-ttu-id="7eba9-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="7eba9-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="7eba9-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="7eba9-193">DevelopmentDependency</span></span>
- <span data-ttu-id="7eba9-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="7eba9-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-195">PackageProjectUrl</span></span>
- <span data-ttu-id="7eba9-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-196">PackageIconUrl</span></span>
- <span data-ttu-id="7eba9-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="7eba9-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="7eba9-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="7eba9-198">PackageTags</span></span>
- <span data-ttu-id="7eba9-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="7eba9-199">PackageOutputPath</span></span>
- <span data-ttu-id="7eba9-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="7eba9-200">IncludeSymbols</span></span>
- <span data-ttu-id="7eba9-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="7eba9-201">IncludeSource</span></span>
- <span data-ttu-id="7eba9-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="7eba9-202">PackageTypes</span></span>
- <span data-ttu-id="7eba9-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="7eba9-203">IsTool</span></span>
- <span data-ttu-id="7eba9-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-204">RepositoryUrl</span></span>
- <span data-ttu-id="7eba9-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="7eba9-205">RepositoryType</span></span>
- <span data-ttu-id="7eba9-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="7eba9-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="7eba9-207">Element MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="7eba9-207">MinClientVersion</span></span>
- <span data-ttu-id="7eba9-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="7eba9-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="7eba9-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="7eba9-209">IncludeContentInPack</span></span>
- <span data-ttu-id="7eba9-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="7eba9-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="7eba9-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="7eba9-211">ContentTargetFolders</span></span>
- <span data-ttu-id="7eba9-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="7eba9-212">NuspecFile</span></span>
- <span data-ttu-id="7eba9-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="7eba9-213">NuspecBasePath</span></span>
- <span data-ttu-id="7eba9-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="7eba9-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="7eba9-215">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="7eba9-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="7eba9-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="7eba9-216">PackageIconUrl</span></span>

<span data-ttu-id="7eba9-217">Zmiana w ramach [2582 problem NuGet](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` po pewnym czasie zostaną zmienione na `PackageIconUri` i może być względna ścieżka do pliku ikony, które zostaną uwzględnione w katalogu głównym wynikowy pakiet.</span><span class="sxs-lookup"><span data-stu-id="7eba9-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="7eba9-218">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="7eba9-218">Output assemblies</span></span>

<span data-ttu-id="7eba9-219">`nuget pack`kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="7eba9-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="7eba9-220">Pliki wyjściowe, które są kopiowane są zależne od MSBuild zapewnia z `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="7eba9-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="7eba9-221">Istnieją dwie właściwości programu MSBuild, które są dostępne w pliku projektu lub wiersza polecenia w celu sterowania gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="7eba9-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="7eba9-222">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="7eba9-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="7eba9-223">`BuildOutputTargetFolder`: Określa folder, w którym ma zostać umieszczony zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7eba9-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="7eba9-224">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich framework folderów.</span><span class="sxs-lookup"><span data-stu-id="7eba9-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="7eba9-225">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="7eba9-225">Package references</span></span>

<span data-ttu-id="7eba9-226">Zobacz [pakietu odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="7eba9-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="7eba9-227">Projekt do odwołań projektu</span><span class="sxs-lookup"><span data-stu-id="7eba9-227">Project to project references</span></span>

<span data-ttu-id="7eba9-228">Projekt do odwołań projektu są traktowane jako domyślnie jako odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="7eba9-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="7eba9-229">Można również dodać następujące metadane odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="7eba9-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="7eba9-230">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="7eba9-230">Including content in a package</span></span>

<span data-ttu-id="7eba9-231">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="7eba9-232">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że nadpiszesz zapisami jak następujące:</span><span class="sxs-lookup"><span data-stu-id="7eba9-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="7eba9-233">Domyślnie pobiera wszystkie elementy dodane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje struktury folder względny, o ile nie zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="7eba9-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="7eba9-234">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` oba), można użyć właściwości programu MSBuild `ContentTargetFolders`, jakie nie "zawartość; pliki", ale może być ustawiony na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="7eba9-235">Należy pamiętać, że po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="7eba9-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="7eba9-236">`PackagePath`może być rozdzielone średnikami zbiór ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="7eba9-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="7eba9-237">Określenie ścieżki pusty pakietu dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="7eba9-238">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="7eba9-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="7eba9-239">Istnieje również właściwość MSBuild `$(IncludeContentInPack)`, jakie nie `true`.</span><span class="sxs-lookup"><span data-stu-id="7eba9-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="7eba9-240">Jeśli ta wartość jest równa `false` w żadnym projekcie następnie zawartość z tego projektu nie znajdują się w pakiecie nuget.</span><span class="sxs-lookup"><span data-stu-id="7eba9-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="7eba9-241">Zawiera inne metadane określonego pakietu, które można ustawić na żadnym z powyższych elementów ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który określa ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpisu w pliku nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7eba9-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="7eba9-242">Oprócz elementy zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić na pliki z akcją kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="7eba9-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="7eba9-243">Pakiet można dołączyć nazwę pliku do ścieżki pakietu przy użyciu globbing wzorców ścieżka do pakietu musi być zakończona z folderu znak separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełna ścieżka, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="7eba9-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="7eba9-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="7eba9-244">IncludeSymbols</span></span>

<span data-ttu-id="7eba9-245">Korzystając z `MSBuild /t:pack /p:IncludeSymbols=true`, odpowiadającego `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="7eba9-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="7eba9-246">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="7eba9-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="7eba9-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="7eba9-247">IncludeSource</span></span>

<span data-ttu-id="7eba9-248">To jest taka sama jak `IncludeSymbols`, ale kopiuje pliki źródłowe wraz z programem `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="7eba9-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="7eba9-249">Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną w pakiecie wynikowy.</span><span class="sxs-lookup"><span data-stu-id="7eba9-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="7eba9-250">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` ustawioną `false`.</span><span class="sxs-lookup"><span data-stu-id="7eba9-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="7eba9-251">Jeśli plik typu skompilować, znajduje się poza folderu projektu, a następnie wystarczy dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="7eba9-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="7eba9-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="7eba9-252">IsTool</span></span>

<span data-ttu-id="7eba9-253">Korzystając z `MSBuild /t:pack /p:IsTool=true`, wszystkie dane wyjściowe pliki, jak określono w [zestawy danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folder zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="7eba9-254">Należy pamiętać, że jest inny niż `DotNetCliTool` który jest określany przez ustawienie `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="7eba9-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="7eba9-255">Przy użyciu .nuspec pakowania</span><span class="sxs-lookup"><span data-stu-id="7eba9-255">Packing using a .nuspec</span></span>

<span data-ttu-id="7eba9-256">Można użyć `.nuspec` plik można spakować projektu, pod warunkiem, że masz plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` , dzięki czemu mogą być wykonywane zadanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="7eba9-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="7eba9-257">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="7eba9-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="7eba9-258">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` pliku używany na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="7eba9-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="7eba9-259">`NuspecProperties`: Rozdzielana średnikami lista klucz = pary wartości.</span><span class="sxs-lookup"><span data-stu-id="7eba9-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="7eba9-260">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild, wiele właściwości musi być następujący: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="7eba9-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="7eba9-261">`NuspecBasePath`: Ścieżki podstawowa dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="7eba9-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="7eba9-262">Jeśli przy użyciu `dotnet.exe` pakowania projektu, użyj polecenia podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="7eba9-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="7eba9-263">Jeśli pakiet projektu za pomocą programu MSBuild, należy użyć polecenia podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="7eba9-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="7eba9-264">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="7eba9-264">restore target</span></span>

<span data-ttu-id="7eba9-265">`MSBuild /t:restore`(który `nuget restore` i `dotnet restore` za pomocą platformy .NET Core projektów), przywraca pakietów, do których odwołuje się w pliku projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7eba9-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="7eba9-266">Przeczytaj wszystkich odwołań do projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="7eba9-266">Read all project to project references</span></span>
1. <span data-ttu-id="7eba9-267">Właściwości projektu, aby znaleźć pośredniego struktury folderów i obiekt docelowy do odczytu</span><span class="sxs-lookup"><span data-stu-id="7eba9-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="7eba9-268">Przekazywanie danych msbuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="7eba9-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="7eba9-269">Uruchamianie przywracania</span><span class="sxs-lookup"><span data-stu-id="7eba9-269">Run restore</span></span>
1. <span data-ttu-id="7eba9-270">Pobieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="7eba9-270">Download packages</span></span>
1. <span data-ttu-id="7eba9-271">Zapis plików zasobów, cele i właściwości</span><span class="sxs-lookup"><span data-stu-id="7eba9-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="7eba9-272">Przywróć właściwości</span><span class="sxs-lookup"><span data-stu-id="7eba9-272">Restore properties</span></span>

<span data-ttu-id="7eba9-273">Przywróć dodatkowe ustawienia mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="7eba9-274">Można również ustawić wartości z wiersza polecenia przy użyciu `/p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="7eba9-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="7eba9-275">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7eba9-275">Property</span></span> | <span data-ttu-id="7eba9-276">Opis</span><span class="sxs-lookup"><span data-stu-id="7eba9-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="7eba9-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="7eba9-277">RestoreSources</span></span> | <span data-ttu-id="7eba9-278">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="7eba9-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="7eba9-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="7eba9-279">RestorePackagesPath</span></span> | <span data-ttu-id="7eba9-280">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7eba9-280">User packages folder path.</span></span> |
| <span data-ttu-id="7eba9-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="7eba9-281">RestoreDisableParallel</span></span> | <span data-ttu-id="7eba9-282">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="7eba9-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="7eba9-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="7eba9-283">RestoreConfigFile</span></span> | <span data-ttu-id="7eba9-284">Ścieżka do `Nuget.Config` pliku w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="7eba9-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="7eba9-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="7eba9-285">RestoreNoCache</span></span> | <span data-ttu-id="7eba9-286">Jeśli PRAWDA, pozwala uniknąć przy użyciu pamięci podręcznej sieci web.</span><span class="sxs-lookup"><span data-stu-id="7eba9-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="7eba9-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="7eba9-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="7eba9-288">Jeśli PRAWDA, ignoruje wystąpił błąd lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="7eba9-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="7eba9-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="7eba9-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="7eba9-290">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="7eba9-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="7eba9-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="7eba9-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="7eba9-292">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="7eba9-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="7eba9-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="7eba9-293">RestoreOutputPath</span></span> | <span data-ttu-id="7eba9-294">Folder wyjściowy, przyjęty `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="7eba9-295">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7eba9-295">Examples</span></span>

<span data-ttu-id="7eba9-296">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="7eba9-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="7eba9-297">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="7eba9-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="7eba9-298">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="7eba9-298">Restore outputs</span></span>

<span data-ttu-id="7eba9-299">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="7eba9-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="7eba9-300">Plik</span><span class="sxs-lookup"><span data-stu-id="7eba9-300">File</span></span> | <span data-ttu-id="7eba9-301">Opis</span><span class="sxs-lookup"><span data-stu-id="7eba9-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="7eba9-302">Wcześniej`project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="7eba9-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="7eba9-303">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="7eba9-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="7eba9-304">Odwołania do zawartych w pakietach docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="7eba9-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="7eba9-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="7eba9-305">PackageTargetFallback</span></span>

<span data-ttu-id="7eba9-306">`PackageTargetFallback` Element służy do określenia zestawu zgodne cele, które mają być użyte podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="7eba9-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="7eba9-307">Został zaprojektowany tak, aby umożliwić pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklaruje dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="7eba9-307">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="7eba9-308">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkie pakiety zależy on od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do projektu, aby umożliwić platformy dotnet z systemem innym niż był zgodny z dotnet.</span><span class="sxs-lookup"><span data-stu-id="7eba9-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="7eba9-309">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależny pakiet zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projekt zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="7eba9-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="7eba9-310">Jeśli chcesz przenieść jest ostatnim biblioteki DLL, a następnie można dodać `PackageTargetFallback` w następujący sposób, aby oznacza, że `portable-net45+win81` zgodnego biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="7eba9-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="7eba9-311">Aby zadeklarować używane dla wszystkich elementów docelowych w projekcie, pozostaw `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7eba9-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="7eba9-312">Można również rozszerzyć zasięg wszelkie istniejące `PackageTargetFallback` przez dołączenie `$(PackageTargetFallback)` w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="7eba9-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="7eba9-313">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="7eba9-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="7eba9-314">Jeśli przywracania jest Przywracanie nieprawidłowy zestaw, jest możliwe do wykluczenia z pakietów domyślny wybór i zamień ją na dowolny inny.</span><span class="sxs-lookup"><span data-stu-id="7eba9-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="7eba9-315">Pierwszy z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="7eba9-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="7eba9-316">Następnie dodaj własne odwołanie do odpowiedniego lokalną kopię pliku DLL:</span><span class="sxs-lookup"><span data-stu-id="7eba9-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
