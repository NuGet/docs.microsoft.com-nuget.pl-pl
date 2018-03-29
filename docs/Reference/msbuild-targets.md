---
title: NuGet pakietu i ich przywracania docelowych elementów MSBuild | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Pakiet NuGet i przywracania może współpracować bezpośrednio jako docelowych elementów MSBuild nuget 4.0 +.
keywords: NuGet i MSBuild, docelowy pakietu NuGet, docelowy przywracania NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a9c2c2229d717dff8472dce0ba568e4a21900b19
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="35799-104">Pakiet NuGet i przywracania jako docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="35799-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="35799-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="35799-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="35799-106">W formacie PackageReference NuGet 4.0 + mogą przechowywać wszystkie manifestu metadanych bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="35799-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="35799-107">Przy użyciu programu MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` celem zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="35799-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="35799-108">Następujących elementów docelowych umożliwiają pracę z programem NuGet, tak jak inne zadanie programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="35799-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="35799-109">(Programu NuGet 3.x i wcześniej, użyj [pakietu](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast tego polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="35799-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="35799-110">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="35799-110">Target build order</span></span>

<span data-ttu-id="35799-111">Ponieważ `pack` i `restore` MSBuild elementów docelowych, można wywołać w celu zwiększenia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="35799-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="35799-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu go.</span><span class="sxs-lookup"><span data-stu-id="35799-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="35799-113">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="35799-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="35799-114">Podobnie można zapisać zadania programu MSBuild, napisać własny docelowych i korzystać z właściwości NuGet w zadanie programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="35799-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="35799-115">docelowy pakiet</span><span class="sxs-lookup"><span data-stu-id="35799-115">pack target</span></span>

<span data-ttu-id="35799-116">Dla platformy .NET Standard projektów przy użyciu formatu PackageReference, używając `msbuild /t:pack` pobiera dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="35799-116">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="35799-117">W poniższej tabeli opisano właściwości programu MSBuild, które mogą zostać dodane do pliku projektu w pierwszym `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="35799-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="35799-118">Wprowadź te zmiany łatwe w Visual Studio 2017 i później przez kliknięcie prawym przyciskiem myszy projekt i wybierając **edytować {nazwa_projektu}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="35799-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="35799-119">Dla wygody tabeli jest zorganizowana według równoważne właściwości w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="35799-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="35799-120">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane przy użyciu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="35799-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="35799-121">Wartość atrybutu/NuSpec.</span><span class="sxs-lookup"><span data-stu-id="35799-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="35799-122">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="35799-122">MSBuild Property</span></span> | <span data-ttu-id="35799-123">Domyślny</span><span class="sxs-lookup"><span data-stu-id="35799-123">Default</span></span> | <span data-ttu-id="35799-124">Uwagi</span><span class="sxs-lookup"><span data-stu-id="35799-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="35799-125">Id</span><span class="sxs-lookup"><span data-stu-id="35799-125">Id</span></span> | <span data-ttu-id="35799-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="35799-126">PackageId</span></span> | <span data-ttu-id="35799-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="35799-127">AssemblyName</span></span> | <span data-ttu-id="35799-128">$(AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="35799-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="35799-129">Wersja</span><span class="sxs-lookup"><span data-stu-id="35799-129">Version</span></span> | <span data-ttu-id="35799-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="35799-130">PackageVersion</span></span> | <span data-ttu-id="35799-131">Wersja</span><span class="sxs-lookup"><span data-stu-id="35799-131">Version</span></span> | <span data-ttu-id="35799-132">Jest to zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" programu semver</span><span class="sxs-lookup"><span data-stu-id="35799-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="35799-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="35799-133">VersionPrefix</span></span> | <span data-ttu-id="35799-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="35799-134">PackageVersionPrefix</span></span> | <span data-ttu-id="35799-135">empty</span><span class="sxs-lookup"><span data-stu-id="35799-135">empty</span></span> | <span data-ttu-id="35799-136">Ustawienie PackageVersion zastępuje PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="35799-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="35799-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="35799-137">VersionSuffix</span></span> | <span data-ttu-id="35799-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="35799-138">PackageVersionSuffix</span></span> | <span data-ttu-id="35799-139">empty</span><span class="sxs-lookup"><span data-stu-id="35799-139">empty</span></span> | <span data-ttu-id="35799-140">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="35799-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="35799-141">Ustawienie PackageVersion zastępuje PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="35799-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="35799-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="35799-142">Authors</span></span> | <span data-ttu-id="35799-143">Autorzy</span><span class="sxs-lookup"><span data-stu-id="35799-143">Authors</span></span> | <span data-ttu-id="35799-144">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="35799-144">Username of the current user</span></span> | |
| <span data-ttu-id="35799-145">Właściciele</span><span class="sxs-lookup"><span data-stu-id="35799-145">Owners</span></span> | <span data-ttu-id="35799-146">Brak</span><span class="sxs-lookup"><span data-stu-id="35799-146">N/A</span></span> | <span data-ttu-id="35799-147">Nie istnieje w pliku NuSpec</span><span class="sxs-lookup"><span data-stu-id="35799-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="35799-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="35799-148">Title</span></span> | <span data-ttu-id="35799-149">Tytuł</span><span class="sxs-lookup"><span data-stu-id="35799-149">Title</span></span> | <span data-ttu-id="35799-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="35799-150">The PackageId</span></span>| |
| <span data-ttu-id="35799-151">Opis</span><span class="sxs-lookup"><span data-stu-id="35799-151">Description</span></span> | <span data-ttu-id="35799-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="35799-152">PackageDescription</span></span> | <span data-ttu-id="35799-153">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="35799-153">"Package Description"</span></span> | |
| <span data-ttu-id="35799-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="35799-154">Copyright</span></span> | <span data-ttu-id="35799-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="35799-155">Copyright</span></span> | <span data-ttu-id="35799-156">empty</span><span class="sxs-lookup"><span data-stu-id="35799-156">empty</span></span> | |
| <span data-ttu-id="35799-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="35799-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="35799-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="35799-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="35799-159">false</span><span class="sxs-lookup"><span data-stu-id="35799-159">false</span></span> | |
| <span data-ttu-id="35799-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="35799-160">LicenseUrl</span></span> | <span data-ttu-id="35799-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="35799-161">PackageLicenseUrl</span></span> | <span data-ttu-id="35799-162">empty</span><span class="sxs-lookup"><span data-stu-id="35799-162">empty</span></span> | |
| <span data-ttu-id="35799-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="35799-163">ProjectUrl</span></span> | <span data-ttu-id="35799-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="35799-164">PackageProjectUrl</span></span> | <span data-ttu-id="35799-165">empty</span><span class="sxs-lookup"><span data-stu-id="35799-165">empty</span></span> | |
| <span data-ttu-id="35799-166">iconUrl</span><span class="sxs-lookup"><span data-stu-id="35799-166">IconUrl</span></span> | <span data-ttu-id="35799-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="35799-167">PackageIconUrl</span></span> | <span data-ttu-id="35799-168">empty</span><span class="sxs-lookup"><span data-stu-id="35799-168">empty</span></span> | |
| <span data-ttu-id="35799-169">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="35799-169">Tags</span></span> | <span data-ttu-id="35799-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="35799-170">PackageTags</span></span> | <span data-ttu-id="35799-171">empty</span><span class="sxs-lookup"><span data-stu-id="35799-171">empty</span></span> | <span data-ttu-id="35799-172">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="35799-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="35799-173">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="35799-173">ReleaseNotes</span></span> | <span data-ttu-id="35799-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="35799-174">PackageReleaseNotes</span></span> | <span data-ttu-id="35799-175">empty</span><span class="sxs-lookup"><span data-stu-id="35799-175">empty</span></span> | |
| <span data-ttu-id="35799-176">Adres Url i repozytorium</span><span class="sxs-lookup"><span data-stu-id="35799-176">Repository/Url</span></span> | <span data-ttu-id="35799-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="35799-177">RepositoryUrl</span></span> | <span data-ttu-id="35799-178">empty</span><span class="sxs-lookup"><span data-stu-id="35799-178">empty</span></span> | <span data-ttu-id="35799-179">Adres URL repozytorium jest używany do klonowania lub pobrać kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="35799-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="35799-180">Przykład: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="35799-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="35799-181">Repozytorium/typ</span><span class="sxs-lookup"><span data-stu-id="35799-181">Repository/Type</span></span> | <span data-ttu-id="35799-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="35799-182">RepositoryType</span></span> | <span data-ttu-id="35799-183">empty</span><span class="sxs-lookup"><span data-stu-id="35799-183">empty</span></span> | <span data-ttu-id="35799-184">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="35799-184">Repository type.</span></span> <span data-ttu-id="35799-185">Przykłady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="35799-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="35799-186">Repozytorium/gałęzi</span><span class="sxs-lookup"><span data-stu-id="35799-186">Repository/Branch</span></span> | <span data-ttu-id="35799-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="35799-187">RepositoryBranch</span></span> | <span data-ttu-id="35799-188">empty</span><span class="sxs-lookup"><span data-stu-id="35799-188">empty</span></span> | <span data-ttu-id="35799-189">Informacje o gałęzi repozytorium opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="35799-189">Optional repository branch information.</span></span> <span data-ttu-id="35799-190">*RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="35799-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="35799-191">Przykład: *wzorca* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="35799-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="35799-192">Repozytorium/zatwierdzeniu</span><span class="sxs-lookup"><span data-stu-id="35799-192">Repository/Commit</span></span> | <span data-ttu-id="35799-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="35799-193">RepositoryCommit</span></span> | <span data-ttu-id="35799-194">empty</span><span class="sxs-lookup"><span data-stu-id="35799-194">empty</span></span> | <span data-ttu-id="35799-195">Opcjonalne repozytorium zatwierdzania lub zestaw zmian, aby wskazać, który źródła pakietu został skompilowany przy.</span><span class="sxs-lookup"><span data-stu-id="35799-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="35799-196">*RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="35799-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="35799-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="35799-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="35799-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="35799-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="35799-199">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="35799-199">Summary</span></span> | <span data-ttu-id="35799-200">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="35799-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="35799-201">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="35799-201">pack target inputs</span></span>

- <span data-ttu-id="35799-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="35799-202">IsPackable</span></span>
- <span data-ttu-id="35799-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="35799-203">PackageVersion</span></span>
- <span data-ttu-id="35799-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="35799-204">PackageId</span></span>
- <span data-ttu-id="35799-205">Autorzy</span><span class="sxs-lookup"><span data-stu-id="35799-205">Authors</span></span>
- <span data-ttu-id="35799-206">Opis</span><span class="sxs-lookup"><span data-stu-id="35799-206">Description</span></span>
- <span data-ttu-id="35799-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="35799-207">Copyright</span></span>
- <span data-ttu-id="35799-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="35799-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="35799-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="35799-209">DevelopmentDependency</span></span>
- <span data-ttu-id="35799-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="35799-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="35799-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="35799-211">PackageProjectUrl</span></span>
- <span data-ttu-id="35799-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="35799-212">PackageIconUrl</span></span>
- <span data-ttu-id="35799-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="35799-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="35799-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="35799-214">PackageTags</span></span>
- <span data-ttu-id="35799-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="35799-215">PackageOutputPath</span></span>
- <span data-ttu-id="35799-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="35799-216">IncludeSymbols</span></span>
- <span data-ttu-id="35799-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="35799-217">IncludeSource</span></span>
- <span data-ttu-id="35799-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="35799-218">PackageTypes</span></span>
- <span data-ttu-id="35799-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="35799-219">IsTool</span></span>
- <span data-ttu-id="35799-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="35799-220">RepositoryUrl</span></span>
- <span data-ttu-id="35799-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="35799-221">RepositoryType</span></span>
- <span data-ttu-id="35799-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="35799-222">RepositoryBranch</span></span>
- <span data-ttu-id="35799-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="35799-223">RepositoryCommit</span></span>
- <span data-ttu-id="35799-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="35799-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="35799-225">Element MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="35799-225">MinClientVersion</span></span>
- <span data-ttu-id="35799-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="35799-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="35799-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="35799-227">IncludeContentInPack</span></span>
- <span data-ttu-id="35799-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="35799-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="35799-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="35799-229">ContentTargetFolders</span></span>
- <span data-ttu-id="35799-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="35799-230">NuspecFile</span></span>
- <span data-ttu-id="35799-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="35799-231">NuspecBasePath</span></span>
- <span data-ttu-id="35799-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="35799-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="35799-233">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="35799-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="35799-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="35799-234">PackageIconUrl</span></span>

<span data-ttu-id="35799-235">Zmiana w ramach [352 problem NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` po pewnym czasie zostaną zmienione na `PackageIconUri` i może być względna ścieżka do pliku ikony, które zostaną uwzględnione w katalogu głównym wynikowy pakiet.</span><span class="sxs-lookup"><span data-stu-id="35799-235">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="35799-236">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="35799-236">Output assemblies</span></span>

<span data-ttu-id="35799-237">`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="35799-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="35799-238">Pliki wyjściowe, które są kopiowane są zależne od MSBuild zapewnia z `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="35799-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="35799-239">Istnieją dwie właściwości programu MSBuild, które są dostępne w pliku projektu lub wiersza polecenia w celu sterowania gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="35799-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="35799-240">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="35799-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="35799-241">`BuildOutputTargetFolder`: Określa folder, w którym ma zostać umieszczony zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="35799-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="35799-242">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich framework folderów.</span><span class="sxs-lookup"><span data-stu-id="35799-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="35799-243">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="35799-243">Package references</span></span>

<span data-ttu-id="35799-244">Zobacz [pakietu odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="35799-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="35799-245">Projekt do odwołań projektu</span><span class="sxs-lookup"><span data-stu-id="35799-245">Project to project references</span></span>

<span data-ttu-id="35799-246">Projekt do odwołań projektu są traktowane jako domyślnie jako odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="35799-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="35799-247">Można również dodać następujące metadane odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="35799-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="35799-248">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="35799-248">Including content in a package</span></span>

<span data-ttu-id="35799-249">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="35799-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="35799-250">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że nadpiszesz zapisami jak następujące:</span><span class="sxs-lookup"><span data-stu-id="35799-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="35799-251">Domyślnie pobiera wszystkie elementy dodane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje struktury folder względny, o ile nie zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="35799-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="35799-252">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` oba), można użyć właściwości programu MSBuild `ContentTargetFolders`, jakie nie "zawartość; pliki", ale może być ustawiony na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="35799-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="35799-253">Należy pamiętać, że po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="35799-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="35799-254">`PackagePath` może być rozdzielone średnikami zbiór ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="35799-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="35799-255">Określenie ścieżki pusty pakietu dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="35799-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="35799-256">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="35799-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="35799-257">Istnieje również właściwość MSBuild `$(IncludeContentInPack)`, jakie nie `true`.</span><span class="sxs-lookup"><span data-stu-id="35799-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="35799-258">Jeśli ta wartość jest równa `false` w żadnym projekcie następnie zawartość z tego projektu nie znajdują się w pakiecie nuget.</span><span class="sxs-lookup"><span data-stu-id="35799-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="35799-259">Zawiera inne metadane określonego pakietu, które można ustawić na żadnym z powyższych elementów ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który określa ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpisu w pliku nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="35799-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="35799-260">Oprócz elementy zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić na pliki z akcją kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="35799-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="35799-261">Pakiet można dołączyć nazwę pliku do ścieżki pakietu przy użyciu globbing wzorców ścieżka do pakietu musi być zakończona z folderu znak separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełna ścieżka, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="35799-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="35799-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="35799-262">IncludeSymbols</span></span>

<span data-ttu-id="35799-263">Korzystając z `MSBuild /t:pack /p:IncludeSymbols=true`, odpowiadającego `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="35799-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="35799-264">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="35799-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="35799-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="35799-265">IncludeSource</span></span>

<span data-ttu-id="35799-266">To jest taka sama jak `IncludeSymbols`, ale kopiuje pliki źródłowe wraz z programem `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="35799-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="35799-267">Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną w pakiecie wynikowy.</span><span class="sxs-lookup"><span data-stu-id="35799-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="35799-268">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` ustawioną `false`.</span><span class="sxs-lookup"><span data-stu-id="35799-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="35799-269">Jeśli plik typu skompilować, znajduje się poza folderu projektu, a następnie wystarczy dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="35799-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="35799-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="35799-270">IsTool</span></span>

<span data-ttu-id="35799-271">Korzystając z `MSBuild /t:pack /p:IsTool=true`, wszystkie dane wyjściowe pliki, jak określono w [zestawy danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folder zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="35799-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="35799-272">Należy pamiętać, że jest inny niż `DotNetCliTool` który jest określany przez ustawienie `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="35799-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="35799-273">Przy użyciu .nuspec pakowania</span><span class="sxs-lookup"><span data-stu-id="35799-273">Packing using a .nuspec</span></span>

<span data-ttu-id="35799-274">Można użyć `.nuspec` plik można spakować projektu, pod warunkiem, że masz SDK plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` , dzięki czemu mogą być wykonywane zadanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="35799-274">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="35799-275">Nadal potrzebujesz przywrócić projekt przed można pliku nuspec.</span><span class="sxs-lookup"><span data-stu-id="35799-275">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="35799-276">Platforma docelowa pliku projektu nie ma znaczenia, a nie używany podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="35799-276">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="35799-277">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="35799-277">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="35799-278">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` pliku używany na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="35799-278">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="35799-279">`NuspecProperties`: Rozdzielana średnikami lista klucz = pary wartości.</span><span class="sxs-lookup"><span data-stu-id="35799-279">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="35799-280">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild, wiele właściwości musi być następujący: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="35799-280">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="35799-281">`NuspecBasePath`: Ścieżki podstawowa dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="35799-281">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="35799-282">Jeśli przy użyciu `dotnet.exe` pakowania projektu, użyj polecenia podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="35799-282">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="35799-283">Jeśli pakiet projektu za pomocą programu MSBuild, należy użyć polecenia podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="35799-283">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="35799-284">Należy pamiętać, pakowanie nuspec przy użyciu dotnet.exe lub msbuild również prowadzi do tworzenia projektu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="35799-284">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="35799-285">Można tego uniknąć przez przekazanie ```--no-build``` dotnet.exe, który jest odpowiednikiem ustawienie dla właściwości ```<NoBuild>true</NoBuild> ``` w pliku projektu oraz ustawienie ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="35799-285">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="35799-286">Przykładowy plik csproj, można spakować plik nuspec to:</span><span class="sxs-lookup"><span data-stu-id="35799-286">An example of a csproj file to pack a nuspec file is:</span></span>

```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="35799-287">Zaawansowane punktów rozszerzenia, aby utworzyć dostosowany pakiet</span><span class="sxs-lookup"><span data-stu-id="35799-287">Advanced extension points to create customized package</span></span>

<span data-ttu-id="35799-288">`pack` Docelowy zawiera dwa punkty rozszerzeń uruchamianych w wewnętrznej, określonej kompilacji framework docelowej.</span><span class="sxs-lookup"><span data-stu-id="35799-288">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="35799-289">Punkty rozszerzenia pomocy technicznej oraz docelowego framework określone zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="35799-289">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="35799-290">`TargetsForTfmSpecificBuildOutput` docelowy: pliki znajdujące się na użytek `lib` folder lub folder, określić przy użyciu `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="35799-290">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="35799-291">`TargetsForTfmSpecificContentInPackage` docelowy: Użyj dla plików znajdujących się poza `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="35799-291">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="35799-292">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="35799-292">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="35799-293">Zapisz niestandardowe docelowych i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="35799-293">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="35799-294">Pliki, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), element docelowy należy zapisać te pliki do ItemGroup `BuildOutputInPackage` i ustaw następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="35799-294">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="35799-295">`FinalOutputPath`: Ścieżka bezwzględna plików; Jeśli nie podano tożsamości jest używane do analizowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="35799-295">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="35799-296">`TargetPath`: (Opcjonalnie) ustawić, gdy trzeba przejdź do podfolderu w pliku `lib\<TargetFramework>` , takie jak towarzyszącej zestawy tego Przejdź w folderach ich odpowiednich kultury.</span><span class="sxs-lookup"><span data-stu-id="35799-296">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="35799-297">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="35799-297">Defaults to the name of the file.</span></span>

<span data-ttu-id="35799-298">Przykład:</span><span class="sxs-lookup"><span data-stu-id="35799-298">Example:</span></span>

```
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="35799-299">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="35799-299">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="35799-300">Zapisz niestandardowe docelowych i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="35799-300">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="35799-301">W przypadku plików do uwzględnienia w pakiecie docelowy należy zapisać te pliki do ItemGroup `TfmSpecificPackageFile` i ustaw następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="35799-301">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="35799-302">`PackagePath`: Ścieżka, gdy ten plik powinien być dane wyjściowe w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="35799-302">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="35799-303">NuGet wygeneruje ostrzeżenie, jeśli więcej niż jeden plik został dodany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="35799-303">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="35799-304">`BuildAction`: Akcja kompilacji do przypisania do plików, jest wymagany tylko wtedy, jeśli ścieżka pakietu znajduje się w `contentFiles` folderu.</span><span class="sxs-lookup"><span data-stu-id="35799-304">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="35799-305">Wartość domyślna to "None".</span><span class="sxs-lookup"><span data-stu-id="35799-305">Defaults to "None".</span></span>

<span data-ttu-id="35799-306">Przykład:</span><span class="sxs-lookup"><span data-stu-id="35799-306">An example:</span></span>
```
<PropertyGroup>
    <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
    <ItemGroup>
      <TfmSpecificPackageFile Include=""abc.txt"">
        <PackagePath>mycontent/$(TargetFramework)</PackagePath>
      </TfmSpecificPackageFile>
      <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
        <PackagePath>net46content</PackagePath>
      </TfmSpecificPackageFile>  
    </ItemGroup>
  </Target>  
```

## <a name="restore-target"></a><span data-ttu-id="35799-307">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="35799-307">restore target</span></span>

<span data-ttu-id="35799-308">`MSBuild /t:restore` (który `nuget restore` i `dotnet restore` za pomocą platformy .NET Core projektów), przywraca pakietów, do których odwołuje się w pliku projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="35799-308">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="35799-309">Przeczytaj wszystkich odwołań do projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="35799-309">Read all project to project references</span></span>
1. <span data-ttu-id="35799-310">Właściwości projektu, aby znaleźć pośredniego struktury folderów i obiekt docelowy do odczytu</span><span class="sxs-lookup"><span data-stu-id="35799-310">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="35799-311">Przekazywanie danych msbuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="35799-311">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="35799-312">Uruchamianie przywracania</span><span class="sxs-lookup"><span data-stu-id="35799-312">Run restore</span></span>
1. <span data-ttu-id="35799-313">Pobieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="35799-313">Download packages</span></span>
1. <span data-ttu-id="35799-314">Zapis plików zasobów, cele i właściwości</span><span class="sxs-lookup"><span data-stu-id="35799-314">Write assets file, targets, and props</span></span>

<span data-ttu-id="35799-315">`restore` Docelowy działa **tylko** dla projektów w formacie PackageReference.</span><span class="sxs-lookup"><span data-stu-id="35799-315">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="35799-316">Robi **nie** pracy dla projektów przy użyciu `packages.config` sformatować; użyj [Przywracanie nuget](../tools/cli-ref-restore.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="35799-316">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="35799-317">Przywróć właściwości</span><span class="sxs-lookup"><span data-stu-id="35799-317">Restore properties</span></span>

<span data-ttu-id="35799-318">Przywróć dodatkowe ustawienia mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="35799-318">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="35799-319">Można również ustawić wartości z wiersza polecenia przy użyciu `/p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="35799-319">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="35799-320">Właściwość</span><span class="sxs-lookup"><span data-stu-id="35799-320">Property</span></span> | <span data-ttu-id="35799-321">Opis</span><span class="sxs-lookup"><span data-stu-id="35799-321">Description</span></span> |
|--------|--------|
| <span data-ttu-id="35799-322">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="35799-322">RestoreSources</span></span> | <span data-ttu-id="35799-323">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="35799-323">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="35799-324">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="35799-324">RestorePackagesPath</span></span> | <span data-ttu-id="35799-325">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="35799-325">User packages folder path.</span></span> |
| <span data-ttu-id="35799-326">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="35799-326">RestoreDisableParallel</span></span> | <span data-ttu-id="35799-327">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="35799-327">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="35799-328">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="35799-328">RestoreConfigFile</span></span> | <span data-ttu-id="35799-329">Ścieżka do `Nuget.Config` pliku w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="35799-329">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="35799-330">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="35799-330">RestoreNoCache</span></span> | <span data-ttu-id="35799-331">Jeśli PRAWDA, pozwala uniknąć za pomocą pakietów pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="35799-331">If true, avoids using cached packages.</span></span> <span data-ttu-id="35799-332">Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="35799-332">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="35799-333">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="35799-333">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="35799-334">Jeśli PRAWDA, ignoruje wystąpił błąd lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="35799-334">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="35799-335">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="35799-335">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="35799-336">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="35799-336">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="35799-337">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="35799-337">RestoreGraphProjectInput</span></span> | <span data-ttu-id="35799-338">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="35799-338">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="35799-339">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="35799-339">RestoreOutputPath</span></span> | <span data-ttu-id="35799-340">Folder wyjściowy, przyjęty `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="35799-340">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="35799-341">Przykłady</span><span class="sxs-lookup"><span data-stu-id="35799-341">Examples</span></span>

<span data-ttu-id="35799-342">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="35799-342">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="35799-343">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="35799-343">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="35799-344">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="35799-344">Restore outputs</span></span>

<span data-ttu-id="35799-345">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="35799-345">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="35799-346">Plik</span><span class="sxs-lookup"><span data-stu-id="35799-346">File</span></span> | <span data-ttu-id="35799-347">Opis</span><span class="sxs-lookup"><span data-stu-id="35799-347">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="35799-348">Zawiera wykres zależności wszystkie odwołania do pakietu.</span><span class="sxs-lookup"><span data-stu-id="35799-348">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="35799-349">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="35799-349">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="35799-350">Odwołania do zawartych w pakietach docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="35799-350">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="35799-351">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="35799-351">PackageTargetFallback</span></span>

<span data-ttu-id="35799-352">`PackageTargetFallback` Element służy do określenia zestawu zgodne cele, które mają być użyte podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="35799-352">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="35799-353">Został zaprojektowany tak, aby umożliwić pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklaruje dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="35799-353">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="35799-354">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkie pakiety zależy on od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do projektu, aby umożliwić platformy dotnet z systemem innym niż był zgodny z dotnet.</span><span class="sxs-lookup"><span data-stu-id="35799-354">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="35799-355">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależny pakiet zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projekt zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="35799-355">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="35799-356">Jeśli chcesz przenieść jest ostatnim biblioteki DLL, a następnie można dodać `PackageTargetFallback` w następujący sposób, aby oznacza, że `portable-net45+win81` zgodnego biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="35799-356">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="35799-357">Aby zadeklarować używane dla wszystkich elementów docelowych w projekcie, pozostaw `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="35799-357">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="35799-358">Można również rozszerzyć zasięg wszelkie istniejące `PackageTargetFallback` przez dołączenie `$(PackageTargetFallback)` w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="35799-358">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="35799-359">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="35799-359">Replacing one library from a restore graph</span></span>

<span data-ttu-id="35799-360">Jeśli przywracania jest Przywracanie nieprawidłowy zestaw, jest możliwe do wykluczenia z pakietów domyślny wybór i zamień ją na dowolny inny.</span><span class="sxs-lookup"><span data-stu-id="35799-360">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="35799-361">Pierwszy z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="35799-361">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="35799-362">Następnie dodaj własne odwołanie do odpowiedniego lokalną kopię pliku DLL:</span><span class="sxs-lookup"><span data-stu-id="35799-362">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
