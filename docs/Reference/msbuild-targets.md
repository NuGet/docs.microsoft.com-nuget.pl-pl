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
ms.openlocfilehash: 798b3550718294072d86b6e4827ec5017178d2cc
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5a5df-104">Pakiet NuGet i przywracania jako docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="5a5df-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5a5df-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="5a5df-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="5a5df-106">W formacie PackageReference NuGet 4.0 + mogą przechowywać wszystkie manifestu metadanych bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="5a5df-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="5a5df-107">Przy użyciu programu MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` celem zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="5a5df-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5a5df-108">Następujących elementów docelowych umożliwiają pracę z programem NuGet, tak jak inne zadanie programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="5a5df-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5a5df-109">(Programu NuGet 3.x i wcześniej, użyj [pakietu](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast tego polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="5a5df-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="5a5df-110">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="5a5df-110">Target build order</span></span>

<span data-ttu-id="5a5df-111">Ponieważ `pack` i `restore` MSBuild elementów docelowych, można wywołać w celu zwiększenia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5a5df-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5a5df-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu go.</span><span class="sxs-lookup"><span data-stu-id="5a5df-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5a5df-113">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="5a5df-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="5a5df-114">Podobnie można zapisać zadania programu MSBuild, napisać własny docelowych i korzystać z właściwości NuGet w zadanie programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5a5df-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5a5df-115">docelowy pakiet</span><span class="sxs-lookup"><span data-stu-id="5a5df-115">pack target</span></span>

<span data-ttu-id="5a5df-116">Korzystając z docelowym pakietu, oznacza to, `msbuild /t:pack`, MSBuild rysuje wejścia z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="5a5df-117">W poniższej tabeli opisano właściwości programu MSBuild, które mogą zostać dodane do pliku projektu w pierwszym `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="5a5df-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5a5df-118">Wprowadź te zmiany łatwe w Visual Studio 2017 i później przez kliknięcie prawym przyciskiem myszy projekt i wybierając **edytować {nazwa_projektu}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="5a5df-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5a5df-119">Dla wygody tabeli jest zorganizowana według równoważne właściwości w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="5a5df-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="5a5df-120">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane przy użyciu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5a5df-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="5a5df-121">Wartość atrybutu/NuSpec.</span><span class="sxs-lookup"><span data-stu-id="5a5df-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5a5df-122">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="5a5df-122">MSBuild Property</span></span> | <span data-ttu-id="5a5df-123">Domyślny</span><span class="sxs-lookup"><span data-stu-id="5a5df-123">Default</span></span> | <span data-ttu-id="5a5df-124">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5a5df-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5a5df-125">Id</span><span class="sxs-lookup"><span data-stu-id="5a5df-125">Id</span></span> | <span data-ttu-id="5a5df-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="5a5df-126">PackageId</span></span> | <span data-ttu-id="5a5df-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5a5df-127">AssemblyName</span></span> | <span data-ttu-id="5a5df-128">$(AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="5a5df-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5a5df-129">Wersja</span><span class="sxs-lookup"><span data-stu-id="5a5df-129">Version</span></span> | <span data-ttu-id="5a5df-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5a5df-130">PackageVersion</span></span> | <span data-ttu-id="5a5df-131">Wersja</span><span class="sxs-lookup"><span data-stu-id="5a5df-131">Version</span></span> | <span data-ttu-id="5a5df-132">Jest to zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" programu semver</span><span class="sxs-lookup"><span data-stu-id="5a5df-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5a5df-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5a5df-133">VersionPrefix</span></span> | <span data-ttu-id="5a5df-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5a5df-134">PackageVersionPrefix</span></span> | <span data-ttu-id="5a5df-135">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-135">empty</span></span> | <span data-ttu-id="5a5df-136">Ustawienie PackageVersion zastępuje PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5a5df-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="5a5df-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5a5df-137">VersionSuffix</span></span> | <span data-ttu-id="5a5df-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5a5df-138">PackageVersionSuffix</span></span> | <span data-ttu-id="5a5df-139">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-139">empty</span></span> | <span data-ttu-id="5a5df-140">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5a5df-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5a5df-141">Ustawienie PackageVersion zastępuje PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5a5df-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="5a5df-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="5a5df-142">Authors</span></span> | <span data-ttu-id="5a5df-143">Autorzy</span><span class="sxs-lookup"><span data-stu-id="5a5df-143">Authors</span></span> | <span data-ttu-id="5a5df-144">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="5a5df-144">Username of the current user</span></span> | |
| <span data-ttu-id="5a5df-145">Właściciele</span><span class="sxs-lookup"><span data-stu-id="5a5df-145">Owners</span></span> | <span data-ttu-id="5a5df-146">Brak</span><span class="sxs-lookup"><span data-stu-id="5a5df-146">N/A</span></span> | <span data-ttu-id="5a5df-147">Nie istnieje w pliku NuSpec</span><span class="sxs-lookup"><span data-stu-id="5a5df-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5a5df-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="5a5df-148">Title</span></span> | <span data-ttu-id="5a5df-149">Tytuł</span><span class="sxs-lookup"><span data-stu-id="5a5df-149">Title</span></span> | <span data-ttu-id="5a5df-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="5a5df-150">The PackageId</span></span>| |
| <span data-ttu-id="5a5df-151">Opis</span><span class="sxs-lookup"><span data-stu-id="5a5df-151">Description</span></span> | <span data-ttu-id="5a5df-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="5a5df-152">PackageDescription</span></span> | <span data-ttu-id="5a5df-153">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="5a5df-153">"Package Description"</span></span> | |
| <span data-ttu-id="5a5df-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="5a5df-154">Copyright</span></span> | <span data-ttu-id="5a5df-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="5a5df-155">Copyright</span></span> | <span data-ttu-id="5a5df-156">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-156">empty</span></span> | |
| <span data-ttu-id="5a5df-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5a5df-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5a5df-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5a5df-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5a5df-159">false</span><span class="sxs-lookup"><span data-stu-id="5a5df-159">false</span></span> | |
| <span data-ttu-id="5a5df-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-160">LicenseUrl</span></span> | <span data-ttu-id="5a5df-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-161">PackageLicenseUrl</span></span> | <span data-ttu-id="5a5df-162">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-162">empty</span></span> | |
| <span data-ttu-id="5a5df-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-163">ProjectUrl</span></span> | <span data-ttu-id="5a5df-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-164">PackageProjectUrl</span></span> | <span data-ttu-id="5a5df-165">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-165">empty</span></span> | |
| <span data-ttu-id="5a5df-166">iconUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-166">IconUrl</span></span> | <span data-ttu-id="5a5df-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-167">PackageIconUrl</span></span> | <span data-ttu-id="5a5df-168">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-168">empty</span></span> | |
| <span data-ttu-id="5a5df-169">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="5a5df-169">Tags</span></span> | <span data-ttu-id="5a5df-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5a5df-170">PackageTags</span></span> | <span data-ttu-id="5a5df-171">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-171">empty</span></span> | <span data-ttu-id="5a5df-172">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="5a5df-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5a5df-173">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="5a5df-173">ReleaseNotes</span></span> | <span data-ttu-id="5a5df-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5a5df-174">PackageReleaseNotes</span></span> | <span data-ttu-id="5a5df-175">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-175">empty</span></span> | |
| <span data-ttu-id="5a5df-176">Adres Url i repozytorium</span><span class="sxs-lookup"><span data-stu-id="5a5df-176">Repository/Url</span></span> | <span data-ttu-id="5a5df-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-177">RepositoryUrl</span></span> | <span data-ttu-id="5a5df-178">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-178">empty</span></span> | <span data-ttu-id="5a5df-179">Adres URL repozytorium jest używany do klonowania lub pobrać kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="5a5df-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="5a5df-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="5a5df-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="5a5df-181">Repozytorium/typ</span><span class="sxs-lookup"><span data-stu-id="5a5df-181">Repository/Type</span></span> | <span data-ttu-id="5a5df-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5a5df-182">RepositoryType</span></span> | <span data-ttu-id="5a5df-183">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-183">empty</span></span> | <span data-ttu-id="5a5df-184">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="5a5df-184">Repository type.</span></span> <span data-ttu-id="5a5df-185">Przykłady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="5a5df-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="5a5df-186">Repozytorium/gałęzi</span><span class="sxs-lookup"><span data-stu-id="5a5df-186">Repository/Branch</span></span> | <span data-ttu-id="5a5df-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5a5df-187">RepositoryBranch</span></span> | <span data-ttu-id="5a5df-188">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-188">empty</span></span> | <span data-ttu-id="5a5df-189">Informacje o gałęzi repozytorium opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="5a5df-189">Optional repository branch information.</span></span> <span data-ttu-id="5a5df-190">*RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="5a5df-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5a5df-191">Przykład: *wzorca* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="5a5df-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5a5df-192">Repozytorium/zatwierdzeniu</span><span class="sxs-lookup"><span data-stu-id="5a5df-192">Repository/Commit</span></span> | <span data-ttu-id="5a5df-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5a5df-193">RepositoryCommit</span></span> | <span data-ttu-id="5a5df-194">empty</span><span class="sxs-lookup"><span data-stu-id="5a5df-194">empty</span></span> | <span data-ttu-id="5a5df-195">Opcjonalne repozytorium zatwierdzania lub zestaw zmian, aby wskazać, który źródła pakietu został skompilowany przy.</span><span class="sxs-lookup"><span data-stu-id="5a5df-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="5a5df-196">*RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="5a5df-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5a5df-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="5a5df-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5a5df-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="5a5df-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5a5df-199">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5a5df-199">Summary</span></span> | <span data-ttu-id="5a5df-200">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="5a5df-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="5a5df-201">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="5a5df-201">pack target inputs</span></span>

- <span data-ttu-id="5a5df-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="5a5df-202">IsPackable</span></span>
- <span data-ttu-id="5a5df-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5a5df-203">PackageVersion</span></span>
- <span data-ttu-id="5a5df-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="5a5df-204">PackageId</span></span>
- <span data-ttu-id="5a5df-205">Autorzy</span><span class="sxs-lookup"><span data-stu-id="5a5df-205">Authors</span></span>
- <span data-ttu-id="5a5df-206">Opis</span><span class="sxs-lookup"><span data-stu-id="5a5df-206">Description</span></span>
- <span data-ttu-id="5a5df-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="5a5df-207">Copyright</span></span>
- <span data-ttu-id="5a5df-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5a5df-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5a5df-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5a5df-209">DevelopmentDependency</span></span>
- <span data-ttu-id="5a5df-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="5a5df-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-211">PackageProjectUrl</span></span>
- <span data-ttu-id="5a5df-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-212">PackageIconUrl</span></span>
- <span data-ttu-id="5a5df-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5a5df-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="5a5df-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5a5df-214">PackageTags</span></span>
- <span data-ttu-id="5a5df-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5a5df-215">PackageOutputPath</span></span>
- <span data-ttu-id="5a5df-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5a5df-216">IncludeSymbols</span></span>
- <span data-ttu-id="5a5df-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5a5df-217">IncludeSource</span></span>
- <span data-ttu-id="5a5df-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5a5df-218">PackageTypes</span></span>
- <span data-ttu-id="5a5df-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="5a5df-219">IsTool</span></span>
- <span data-ttu-id="5a5df-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-220">RepositoryUrl</span></span>
- <span data-ttu-id="5a5df-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5a5df-221">RepositoryType</span></span>
- <span data-ttu-id="5a5df-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="5a5df-222">RepositoryBranch</span></span>
- <span data-ttu-id="5a5df-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="5a5df-223">RepositoryCommit</span></span>
- <span data-ttu-id="5a5df-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5a5df-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="5a5df-225">Element MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5a5df-225">MinClientVersion</span></span>
- <span data-ttu-id="5a5df-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5a5df-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="5a5df-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5a5df-227">IncludeContentInPack</span></span>
- <span data-ttu-id="5a5df-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5a5df-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5a5df-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5a5df-229">ContentTargetFolders</span></span>
- <span data-ttu-id="5a5df-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="5a5df-230">NuspecFile</span></span>
- <span data-ttu-id="5a5df-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="5a5df-231">NuspecBasePath</span></span>
- <span data-ttu-id="5a5df-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="5a5df-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5a5df-233">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="5a5df-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5a5df-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5a5df-234">PackageIconUrl</span></span>

<span data-ttu-id="5a5df-235">Zmiana w ramach [2582 problem NuGet](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` po pewnym czasie zostaną zmienione na `PackageIconUri` i może być względna ścieżka do pliku ikony, które zostaną uwzględnione w katalogu głównym wynikowy pakiet.</span><span class="sxs-lookup"><span data-stu-id="5a5df-235">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5a5df-236">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="5a5df-236">Output assemblies</span></span>

<span data-ttu-id="5a5df-237">`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="5a5df-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5a5df-238">Pliki wyjściowe, które są kopiowane są zależne od MSBuild zapewnia z `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="5a5df-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5a5df-239">Istnieją dwie właściwości programu MSBuild, które są dostępne w pliku projektu lub wiersza polecenia w celu sterowania gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="5a5df-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5a5df-240">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="5a5df-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5a5df-241">`BuildOutputTargetFolder`: Określa folder, w którym ma zostać umieszczony zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5a5df-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5a5df-242">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich framework folderów.</span><span class="sxs-lookup"><span data-stu-id="5a5df-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5a5df-243">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="5a5df-243">Package references</span></span>

<span data-ttu-id="5a5df-244">Zobacz [pakietu odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="5a5df-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5a5df-245">Projekt do odwołań projektu</span><span class="sxs-lookup"><span data-stu-id="5a5df-245">Project to project references</span></span>

<span data-ttu-id="5a5df-246">Projekt do odwołań projektu są traktowane jako domyślnie jako odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="5a5df-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5a5df-247">Można również dodać następujące metadane odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="5a5df-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5a5df-248">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="5a5df-248">Including content in a package</span></span>

<span data-ttu-id="5a5df-249">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5a5df-250">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że nadpiszesz zapisami jak następujące:</span><span class="sxs-lookup"><span data-stu-id="5a5df-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="5a5df-251">Domyślnie pobiera wszystkie elementy dodane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje struktury folder względny, o ile nie zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="5a5df-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5a5df-252">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` oba), można użyć właściwości programu MSBuild `ContentTargetFolders`, jakie nie "zawartość; pliki", ale może być ustawiony na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5a5df-253">Należy pamiętać, że po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="5a5df-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5a5df-254">`PackagePath` może być rozdzielone średnikami zbiór ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="5a5df-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5a5df-255">Określenie ścieżki pusty pakietu dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5a5df-256">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="5a5df-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5a5df-257">Istnieje również właściwość MSBuild `$(IncludeContentInPack)`, jakie nie `true`.</span><span class="sxs-lookup"><span data-stu-id="5a5df-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5a5df-258">Jeśli ta wartość jest równa `false` w żadnym projekcie następnie zawartość z tego projektu nie znajdują się w pakiecie nuget.</span><span class="sxs-lookup"><span data-stu-id="5a5df-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5a5df-259">Zawiera inne metadane określonego pakietu, które można ustawić na żadnym z powyższych elementów ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który określa ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpisu w pliku nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5a5df-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="5a5df-260">Oprócz elementy zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić na pliki z akcją kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="5a5df-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5a5df-261">Pakiet można dołączyć nazwę pliku do ścieżki pakietu przy użyciu globbing wzorców ścieżka do pakietu musi być zakończona z folderu znak separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełna ścieżka, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="5a5df-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5a5df-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5a5df-262">IncludeSymbols</span></span>

<span data-ttu-id="5a5df-263">Korzystając z `MSBuild /t:pack /p:IncludeSymbols=true`, odpowiadającego `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="5a5df-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5a5df-264">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="5a5df-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5a5df-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5a5df-265">IncludeSource</span></span>

<span data-ttu-id="5a5df-266">To jest taka sama jak `IncludeSymbols`, ale kopiuje pliki źródłowe wraz z programem `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="5a5df-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5a5df-267">Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną w pakiecie wynikowy.</span><span class="sxs-lookup"><span data-stu-id="5a5df-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5a5df-268">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` ustawioną `false`.</span><span class="sxs-lookup"><span data-stu-id="5a5df-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5a5df-269">Jeśli plik typu skompilować, znajduje się poza folderu projektu, a następnie wystarczy dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="5a5df-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="5a5df-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="5a5df-270">IsTool</span></span>

<span data-ttu-id="5a5df-271">Korzystając z `MSBuild /t:pack /p:IsTool=true`, wszystkie dane wyjściowe pliki, jak określono w [zestawy danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folder zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5a5df-272">Należy pamiętać, że jest inny niż `DotNetCliTool` który jest określany przez ustawienie `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="5a5df-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5a5df-273">Przy użyciu .nuspec pakowania</span><span class="sxs-lookup"><span data-stu-id="5a5df-273">Packing using a .nuspec</span></span>

<span data-ttu-id="5a5df-274">Można użyć `.nuspec` plik można spakować projektu, pod warunkiem, że masz plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` , dzięki czemu mogą być wykonywane zadanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="5a5df-274">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5a5df-275">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="5a5df-275">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5a5df-276">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` pliku używany na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="5a5df-276">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5a5df-277">`NuspecProperties`: Rozdzielana średnikami lista klucz = pary wartości.</span><span class="sxs-lookup"><span data-stu-id="5a5df-277">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5a5df-278">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild, wiele właściwości musi być następujący: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="5a5df-278">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5a5df-279">`NuspecBasePath`: Ścieżki podstawowa dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="5a5df-279">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5a5df-280">Jeśli przy użyciu `dotnet.exe` pakowania projektu, użyj polecenia podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="5a5df-280">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5a5df-281">Jeśli pakiet projektu za pomocą programu MSBuild, należy użyć polecenia podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="5a5df-281">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="5a5df-282">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="5a5df-282">restore target</span></span>

<span data-ttu-id="5a5df-283">`MSBuild /t:restore` (który `nuget restore` i `dotnet restore` za pomocą platformy .NET Core projektów), przywraca pakietów, do których odwołuje się w pliku projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5a5df-283">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5a5df-284">Przeczytaj wszystkich odwołań do projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="5a5df-284">Read all project to project references</span></span>
1. <span data-ttu-id="5a5df-285">Właściwości projektu, aby znaleźć pośredniego struktury folderów i obiekt docelowy do odczytu</span><span class="sxs-lookup"><span data-stu-id="5a5df-285">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5a5df-286">Przekazywanie danych msbuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="5a5df-286">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5a5df-287">Uruchamianie przywracania</span><span class="sxs-lookup"><span data-stu-id="5a5df-287">Run restore</span></span>
1. <span data-ttu-id="5a5df-288">Pobieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="5a5df-288">Download packages</span></span>
1. <span data-ttu-id="5a5df-289">Zapis plików zasobów, cele i właściwości</span><span class="sxs-lookup"><span data-stu-id="5a5df-289">Write assets file, targets, and props</span></span>

> [!Note]
> <span data-ttu-id="5a5df-290">`restore` Działa tylko dla projektów przy użyciu programu MSBuild `PackageReference` elementów i nie powoduje przywrócenia pakietów odwoływać się przy użyciu `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="5a5df-290">The `restore` MSBuild target only works for projects using `PackageReference` items and does not restore packages referenced using a `packages.config` file.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="5a5df-291">Przywróć właściwości</span><span class="sxs-lookup"><span data-stu-id="5a5df-291">Restore properties</span></span>

<span data-ttu-id="5a5df-292">Przywróć dodatkowe ustawienia mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-292">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5a5df-293">Można również ustawić wartości z wiersza polecenia przy użyciu `/p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="5a5df-293">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5a5df-294">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5a5df-294">Property</span></span> | <span data-ttu-id="5a5df-295">Opis</span><span class="sxs-lookup"><span data-stu-id="5a5df-295">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5a5df-296">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5a5df-296">RestoreSources</span></span> | <span data-ttu-id="5a5df-297">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="5a5df-297">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5a5df-298">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5a5df-298">RestorePackagesPath</span></span> | <span data-ttu-id="5a5df-299">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5a5df-299">User packages folder path.</span></span> |
| <span data-ttu-id="5a5df-300">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5a5df-300">RestoreDisableParallel</span></span> | <span data-ttu-id="5a5df-301">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="5a5df-301">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5a5df-302">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5a5df-302">RestoreConfigFile</span></span> | <span data-ttu-id="5a5df-303">Ścieżka do `Nuget.Config` pliku w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="5a5df-303">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5a5df-304">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5a5df-304">RestoreNoCache</span></span> | <span data-ttu-id="5a5df-305">Jeśli PRAWDA, pozwala uniknąć przy użyciu pamięci podręcznej sieci web.</span><span class="sxs-lookup"><span data-stu-id="5a5df-305">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="5a5df-306">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5a5df-306">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5a5df-307">Jeśli PRAWDA, ignoruje wystąpił błąd lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="5a5df-307">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5a5df-308">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5a5df-308">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5a5df-309">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="5a5df-309">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5a5df-310">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5a5df-310">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5a5df-311">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="5a5df-311">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5a5df-312">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="5a5df-312">RestoreOutputPath</span></span> | <span data-ttu-id="5a5df-313">Folder wyjściowy, przyjęty `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-313">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="5a5df-314">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5a5df-314">Examples</span></span>

<span data-ttu-id="5a5df-315">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="5a5df-315">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="5a5df-316">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="5a5df-316">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5a5df-317">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="5a5df-317">Restore outputs</span></span>

<span data-ttu-id="5a5df-318">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="5a5df-318">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5a5df-319">Plik</span><span class="sxs-lookup"><span data-stu-id="5a5df-319">File</span></span> | <span data-ttu-id="5a5df-320">Opis</span><span class="sxs-lookup"><span data-stu-id="5a5df-320">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5a5df-321">Wcześniej `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="5a5df-321">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5a5df-322">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="5a5df-322">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5a5df-323">Odwołania do zawartych w pakietach docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="5a5df-323">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="5a5df-324">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5a5df-324">PackageTargetFallback</span></span>

<span data-ttu-id="5a5df-325">`PackageTargetFallback` Element służy do określenia zestawu zgodne cele, które mają być użyte podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="5a5df-325">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="5a5df-326">Został zaprojektowany tak, aby umożliwić pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklaruje dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="5a5df-326">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5a5df-327">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkie pakiety zależy on od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do projektu, aby umożliwić platformy dotnet z systemem innym niż był zgodny z dotnet.</span><span class="sxs-lookup"><span data-stu-id="5a5df-327">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="5a5df-328">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależny pakiet zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projekt zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5a5df-328">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5a5df-329">Jeśli chcesz przenieść jest ostatnim biblioteki DLL, a następnie można dodać `PackageTargetFallback` w następujący sposób, aby oznacza, że `portable-net45+win81` zgodnego biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="5a5df-329">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5a5df-330">Aby zadeklarować używane dla wszystkich elementów docelowych w projekcie, pozostaw `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="5a5df-330">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5a5df-331">Można również rozszerzyć zasięg wszelkie istniejące `PackageTargetFallback` przez dołączenie `$(PackageTargetFallback)` w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="5a5df-331">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5a5df-332">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="5a5df-332">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5a5df-333">Jeśli przywracania jest Przywracanie nieprawidłowy zestaw, jest możliwe do wykluczenia z pakietów domyślny wybór i zamień ją na dowolny inny.</span><span class="sxs-lookup"><span data-stu-id="5a5df-333">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5a5df-334">Pierwszy z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="5a5df-334">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5a5df-335">Następnie dodaj własne odwołanie do odpowiedniego lokalną kopię pliku DLL:</span><span class="sxs-lookup"><span data-stu-id="5a5df-335">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
