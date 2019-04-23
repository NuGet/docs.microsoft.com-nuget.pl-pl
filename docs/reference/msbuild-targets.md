---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą działać bezpośrednio jako elementów docelowych MSBuild nuget 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 1e89aeb46f2538d46c013561a51a41702b2472d8
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932102"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="07708-103">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="07708-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="07708-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="07708-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="07708-105">Przy użyciu formatu PackageReference NuGet 4.0 + mogą przechowywać metadanych wszystkie manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="07708-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="07708-106">Za pomocą narzędzia MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` jest przeznaczony dla zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="07708-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="07708-107">Te obiekty docelowe umożliwiają pracę z NuGet, tak jak przy użyciu innych zadań programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="07708-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="07708-108">(Dla NuGet 3.x i starszym użyj [pakiet](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="07708-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="07708-109">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="07708-109">Target build order</span></span>

<span data-ttu-id="07708-110">Ponieważ `pack` i `restore` są elementy docelowe programu MSBuild, można wywołać, aby zwiększyć przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="07708-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="07708-111">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu jej.</span><span class="sxs-lookup"><span data-stu-id="07708-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="07708-112">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="07708-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="07708-113">Podobnie można zapisać zadania programu MSBuild, napisać własne docelowe i korzystać z właściwości NuGet w zadaniu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="07708-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="07708-114">Pakiet docelowy</span><span class="sxs-lookup"><span data-stu-id="07708-114">pack target</span></span>

<span data-ttu-id="07708-115">W przypadku projektów .NET Standard przy użyciu formatu PackageReference, przy użyciu `msbuild -t:pack` pobiera dane wejściowe z pliku projektu w celu utworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="07708-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="07708-116">W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w obrębie pierwszych `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="07708-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="07708-117">Zmiany możesz wprowadzić te łatwe w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając polecenie **Edytuj {project_name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="07708-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="07708-118">Dla wygody tabeli jest zorganizowana według równoważne właściwość [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="07708-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="07708-119">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane za pomocą narzędzia MSBuild.</span><span class="sxs-lookup"><span data-stu-id="07708-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="07708-120">Wartość atrybutu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="07708-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="07708-121">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="07708-121">MSBuild Property</span></span> | <span data-ttu-id="07708-122">Domyślny</span><span class="sxs-lookup"><span data-stu-id="07708-122">Default</span></span> | <span data-ttu-id="07708-123">Uwagi</span><span class="sxs-lookup"><span data-stu-id="07708-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="07708-124">Id</span><span class="sxs-lookup"><span data-stu-id="07708-124">Id</span></span> | <span data-ttu-id="07708-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="07708-125">PackageId</span></span> | <span data-ttu-id="07708-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="07708-126">AssemblyName</span></span> | <span data-ttu-id="07708-127">$(AssemblyName) z programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="07708-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="07708-128">Wersja</span><span class="sxs-lookup"><span data-stu-id="07708-128">Version</span></span> | <span data-ttu-id="07708-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="07708-129">PackageVersion</span></span> | <span data-ttu-id="07708-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="07708-130">Version</span></span> | <span data-ttu-id="07708-131">Jest to semver zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="07708-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="07708-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="07708-132">VersionPrefix</span></span> | <span data-ttu-id="07708-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="07708-133">PackageVersionPrefix</span></span> | <span data-ttu-id="07708-134">empty</span><span class="sxs-lookup"><span data-stu-id="07708-134">empty</span></span> | <span data-ttu-id="07708-135">Ustawienie PackageVersion zastępuje PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="07708-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="07708-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="07708-136">VersionSuffix</span></span> | <span data-ttu-id="07708-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="07708-137">PackageVersionSuffix</span></span> | <span data-ttu-id="07708-138">empty</span><span class="sxs-lookup"><span data-stu-id="07708-138">empty</span></span> | <span data-ttu-id="07708-139">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="07708-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="07708-140">Ustawienie PackageVersion zastępuje PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="07708-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="07708-141">Autorzy</span><span class="sxs-lookup"><span data-stu-id="07708-141">Authors</span></span> | <span data-ttu-id="07708-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="07708-142">Authors</span></span> | <span data-ttu-id="07708-143">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="07708-143">Username of the current user</span></span> | |
| <span data-ttu-id="07708-144">Właściciele</span><span class="sxs-lookup"><span data-stu-id="07708-144">Owners</span></span> | <span data-ttu-id="07708-145">Brak</span><span class="sxs-lookup"><span data-stu-id="07708-145">N/A</span></span> | <span data-ttu-id="07708-146">Nie są obecne w NuSpec</span><span class="sxs-lookup"><span data-stu-id="07708-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="07708-147">Tytuł</span><span class="sxs-lookup"><span data-stu-id="07708-147">Title</span></span> | <span data-ttu-id="07708-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="07708-148">Title</span></span> | <span data-ttu-id="07708-149">Jako PackageId</span><span class="sxs-lookup"><span data-stu-id="07708-149">The PackageId</span></span>| |
| <span data-ttu-id="07708-150">Opis</span><span class="sxs-lookup"><span data-stu-id="07708-150">Description</span></span> | <span data-ttu-id="07708-151">Opis</span><span class="sxs-lookup"><span data-stu-id="07708-151">Description</span></span> | <span data-ttu-id="07708-152">"Pakiet opis"</span><span class="sxs-lookup"><span data-stu-id="07708-152">"Package Description"</span></span> | |
| <span data-ttu-id="07708-153">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="07708-153">Copyright</span></span> | <span data-ttu-id="07708-154">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="07708-154">Copyright</span></span> | <span data-ttu-id="07708-155">empty</span><span class="sxs-lookup"><span data-stu-id="07708-155">empty</span></span> | |
| <span data-ttu-id="07708-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="07708-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="07708-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="07708-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="07708-158">false</span><span class="sxs-lookup"><span data-stu-id="07708-158">false</span></span> | |
| <span data-ttu-id="07708-159">Licencja</span><span class="sxs-lookup"><span data-stu-id="07708-159">license</span></span> | <span data-ttu-id="07708-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="07708-160">PackageLicenseExpression</span></span> | <span data-ttu-id="07708-161">empty</span><span class="sxs-lookup"><span data-stu-id="07708-161">empty</span></span> | <span data-ttu-id="07708-162">Odnosi się do `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="07708-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="07708-163">Licencja</span><span class="sxs-lookup"><span data-stu-id="07708-163">license</span></span> | <span data-ttu-id="07708-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="07708-164">PackageLicenseFile</span></span> | <span data-ttu-id="07708-165">empty</span><span class="sxs-lookup"><span data-stu-id="07708-165">empty</span></span> | <span data-ttu-id="07708-166">Odnosi się do `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="07708-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="07708-167">Konieczne może być jawnie pakietu pliku odwołania licencji.</span><span class="sxs-lookup"><span data-stu-id="07708-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="07708-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="07708-168">LicenseUrl</span></span> | <span data-ttu-id="07708-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="07708-169">PackageLicenseUrl</span></span> | <span data-ttu-id="07708-170">empty</span><span class="sxs-lookup"><span data-stu-id="07708-170">empty</span></span> | <span data-ttu-id="07708-171">`licenseUrl` jest on przestarzały, użyj właściwości PackageLicenseExpression lub PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="07708-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="07708-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="07708-172">ProjectUrl</span></span> | <span data-ttu-id="07708-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="07708-173">PackageProjectUrl</span></span> | <span data-ttu-id="07708-174">empty</span><span class="sxs-lookup"><span data-stu-id="07708-174">empty</span></span> | |
| <span data-ttu-id="07708-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="07708-175">IconUrl</span></span> | <span data-ttu-id="07708-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="07708-176">PackageIconUrl</span></span> | <span data-ttu-id="07708-177">empty</span><span class="sxs-lookup"><span data-stu-id="07708-177">empty</span></span> | |
| <span data-ttu-id="07708-178">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="07708-178">Tags</span></span> | <span data-ttu-id="07708-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="07708-179">PackageTags</span></span> | <span data-ttu-id="07708-180">empty</span><span class="sxs-lookup"><span data-stu-id="07708-180">empty</span></span> | <span data-ttu-id="07708-181">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="07708-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="07708-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="07708-182">ReleaseNotes</span></span> | <span data-ttu-id="07708-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="07708-183">PackageReleaseNotes</span></span> | <span data-ttu-id="07708-184">empty</span><span class="sxs-lookup"><span data-stu-id="07708-184">empty</span></span> | |
| <span data-ttu-id="07708-185">Adres Url i repozytorium</span><span class="sxs-lookup"><span data-stu-id="07708-185">Repository/Url</span></span> | <span data-ttu-id="07708-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="07708-186">RepositoryUrl</span></span> | <span data-ttu-id="07708-187">empty</span><span class="sxs-lookup"><span data-stu-id="07708-187">empty</span></span> | <span data-ttu-id="07708-188">Adres URL repozytorium jest używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="07708-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="07708-189">Przykład: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="07708-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="07708-190">Repozytorium/typu</span><span class="sxs-lookup"><span data-stu-id="07708-190">Repository/Type</span></span> | <span data-ttu-id="07708-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="07708-191">RepositoryType</span></span> | <span data-ttu-id="07708-192">empty</span><span class="sxs-lookup"><span data-stu-id="07708-192">empty</span></span> | <span data-ttu-id="07708-193">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="07708-193">Repository type.</span></span> <span data-ttu-id="07708-194">Przykłady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="07708-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="07708-195">Repozytorium/gałąź</span><span class="sxs-lookup"><span data-stu-id="07708-195">Repository/Branch</span></span> | <span data-ttu-id="07708-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="07708-196">RepositoryBranch</span></span> | <span data-ttu-id="07708-197">empty</span><span class="sxs-lookup"><span data-stu-id="07708-197">empty</span></span> | <span data-ttu-id="07708-198">Informacje o gałęzi repozytorium opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="07708-198">Optional repository branch information.</span></span> <span data-ttu-id="07708-199">*RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="07708-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="07708-200">Przykład: *wzorca* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="07708-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="07708-201">Repozytorium na zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="07708-201">Repository/Commit</span></span> | <span data-ttu-id="07708-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="07708-202">RepositoryCommit</span></span> | <span data-ttu-id="07708-203">empty</span><span class="sxs-lookup"><span data-stu-id="07708-203">empty</span></span> | <span data-ttu-id="07708-204">Opcjonalne repozytorium zatwierdzenia lub zestaw zmian, aby wskazać, które źródła pakietu została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="07708-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="07708-205">*RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="07708-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="07708-206">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="07708-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="07708-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="07708-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="07708-208">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="07708-208">Summary</span></span> | <span data-ttu-id="07708-209">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="07708-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="07708-210">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="07708-210">pack target inputs</span></span>

- <span data-ttu-id="07708-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="07708-211">IsPackable</span></span>
- <span data-ttu-id="07708-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="07708-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="07708-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="07708-213">PackageVersion</span></span>
- <span data-ttu-id="07708-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="07708-214">PackageId</span></span>
- <span data-ttu-id="07708-215">Autorzy</span><span class="sxs-lookup"><span data-stu-id="07708-215">Authors</span></span>
- <span data-ttu-id="07708-216">Opis</span><span class="sxs-lookup"><span data-stu-id="07708-216">Description</span></span>
- <span data-ttu-id="07708-217">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="07708-217">Copyright</span></span>
- <span data-ttu-id="07708-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="07708-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="07708-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="07708-219">DevelopmentDependency</span></span>
- <span data-ttu-id="07708-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="07708-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="07708-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="07708-221">PackageLicenseFile</span></span>
- <span data-ttu-id="07708-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="07708-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="07708-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="07708-223">PackageProjectUrl</span></span>
- <span data-ttu-id="07708-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="07708-224">PackageIconUrl</span></span>
- <span data-ttu-id="07708-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="07708-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="07708-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="07708-226">PackageTags</span></span>
- <span data-ttu-id="07708-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="07708-227">PackageOutputPath</span></span>
- <span data-ttu-id="07708-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="07708-228">IncludeSymbols</span></span>
- <span data-ttu-id="07708-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="07708-229">IncludeSource</span></span>
- <span data-ttu-id="07708-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="07708-230">PackageTypes</span></span>
- <span data-ttu-id="07708-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="07708-231">IsTool</span></span>
- <span data-ttu-id="07708-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="07708-232">RepositoryUrl</span></span>
- <span data-ttu-id="07708-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="07708-233">RepositoryType</span></span>
- <span data-ttu-id="07708-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="07708-234">RepositoryBranch</span></span>
- <span data-ttu-id="07708-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="07708-235">RepositoryCommit</span></span>
- <span data-ttu-id="07708-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="07708-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="07708-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="07708-237">MinClientVersion</span></span>
- <span data-ttu-id="07708-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="07708-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="07708-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="07708-239">IncludeContentInPack</span></span>
- <span data-ttu-id="07708-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="07708-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="07708-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="07708-241">ContentTargetFolders</span></span>
- <span data-ttu-id="07708-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="07708-242">NuspecFile</span></span>
- <span data-ttu-id="07708-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="07708-243">NuspecBasePath</span></span>
- <span data-ttu-id="07708-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="07708-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="07708-245">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="07708-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="07708-246">Pomiń zależności</span><span class="sxs-lookup"><span data-stu-id="07708-246">Suppress dependencies</span></span>

<span data-ttu-id="07708-247">Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet, należy ustawić `SuppressDependenciesWhenPacking` do `true` co pozwoli pomija wszystkie zależności z nupkg wygenerowany plik.</span><span class="sxs-lookup"><span data-stu-id="07708-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="07708-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="07708-248">PackageIconUrl</span></span>

<span data-ttu-id="07708-249">Zmiana w ramach [352 problem NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` ostatecznie zostanie zmieniony na `PackageIconUri` i może być ścieżką względną do pliku ikony, który zostanie uwzględniony w katalogu głównym pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="07708-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="07708-250">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="07708-250">Output assemblies</span></span>

<span data-ttu-id="07708-251">`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="07708-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="07708-252">Pliki wyjściowe, które są kopiowane zależą od tego, co MSBuild zapewnia klientom — od `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="07708-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="07708-253">Istnieją dwie właściwości programu MSBuild, które można w pliku projektu lub wiersza polecenia do kontrolki gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="07708-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="07708-254">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="07708-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="07708-255">`BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="07708-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="07708-256">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich ramach folderów.</span><span class="sxs-lookup"><span data-stu-id="07708-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="07708-257">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="07708-257">Package references</span></span>

<span data-ttu-id="07708-258">Zobacz [pakietu odwołania w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="07708-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="07708-259">Projekt do odwołania do projektu</span><span class="sxs-lookup"><span data-stu-id="07708-259">Project to project references</span></span>

<span data-ttu-id="07708-260">Projekt do odwołania do projektu są uznawane za domyślnie odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="07708-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="07708-261">Można również dodać następujące metadane, do której można się odwołać projektu:</span><span class="sxs-lookup"><span data-stu-id="07708-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="07708-262">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="07708-262">Including content in a package</span></span>

<span data-ttu-id="07708-263">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="07708-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="07708-264">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że przesłonisz z wpisy jak następujące:</span><span class="sxs-lookup"><span data-stu-id="07708-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="07708-265">Domyślnie dodawane pobiera wszystkie elementy w folderze głównym `content` i `contentFiles\any\<target_framework>` folder, w ramach pakietu i zachowuje strukturę folderu względnego, chyba że określisz Ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="07708-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="07708-266">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` zarówno), można użyć właściwości programu MSBuild `ContentTargetFolders`, którego wartość domyślna to "zawartość; pliki", ale może być ustawiona na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="07708-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="07708-267">Należy pamiętać, który po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="07708-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="07708-268">`PackagePath` może być rozdzielone średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="07708-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="07708-269">Określenie ścieżki pusty pakiet dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="07708-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="07708-270">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="07708-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="07708-271">Istnieje również właściwość narzędzia MSBuild `$(IncludeContentInPack)`, które domyślnie używa `true`.</span><span class="sxs-lookup"><span data-stu-id="07708-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="07708-272">Jeśli jest ono ustawione na `false` w żadnym projekcie następnie zawartość z tego projektu nie są uwzględnione w pakiet nuget.</span><span class="sxs-lookup"><span data-stu-id="07708-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="07708-273">Obejmuje inne określonych metadanych pakietu, który dla każdego z powyższych elementów można ustawić ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który konfiguruje ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpis nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="07708-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="07708-274">Oprócz elementów zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić w plikach za pomocą akcji kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource lub Brak.</span><span class="sxs-lookup"><span data-stu-id="07708-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="07708-275">Pakiet można dołączyć nazwę pliku do ścieżki pakietu, korzystając z wzorców obsługi symboli wieloznacznych ścieżka do pakietu musi kończyć folderu znaku separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełną ścieżkę, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="07708-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="07708-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="07708-276">IncludeSymbols</span></span>

<span data-ttu-id="07708-277">Korzystając z `MSBuild -t:pack -p:IncludeSymbols=true`, odpowiedni `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="07708-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="07708-278">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="07708-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="07708-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="07708-279">IncludeSource</span></span>

<span data-ttu-id="07708-280">To jest taka sama jak `IncludeSymbols`, chyba że kopiuje pliki źródłowe, wraz z `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="07708-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="07708-281">Pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną do pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="07708-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="07708-282">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` równa `false`.</span><span class="sxs-lookup"><span data-stu-id="07708-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="07708-283">Plik typu kompilacji, czy poza folderem projektu, a następnie po prostu dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="07708-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="07708-284">Pakowanie wyrażenie licencji lub też pliku licencji</span><span class="sxs-lookup"><span data-stu-id="07708-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="07708-285">Korzystając z wyrażenia licencji, właściwość PackageLicenseExpression powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="07708-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="07708-286">[Przykładowe wyrażenie licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="07708-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="07708-287">[Dowiedz się więcej na temat wyrażeń licencji i licencji, które są akceptowane przez NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="07708-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="07708-288">Podczas pakowania pliku licencji, należy użyć właściwości PackageLicenseFile do określenia ścieżki pakietu, względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="07708-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="07708-289">Ponadto należy się upewnić, że plik znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="07708-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="07708-290">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="07708-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="07708-291">[Przykładowy plik licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="07708-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="07708-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="07708-292">IsTool</span></span>

<span data-ttu-id="07708-293">Korzystając z `MSBuild -t:pack -p:IsTool=true`, wszystkie dane wyjściowe pliki, jak to określono w [zestawów danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folderu zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="07708-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="07708-294">Należy pamiętać, że to różni się od `DotNetCliTool` określić, ustawiając `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="07708-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="07708-295">Pakowanie przy użyciu .nuspec</span><span class="sxs-lookup"><span data-stu-id="07708-295">Packing using a .nuspec</span></span>

<span data-ttu-id="07708-296">Możesz użyć `.nuspec` pliku do pakietu projektu, pod warunkiem, że masz zestaw SDK plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` tak, aby zadanie pakietów, które mogą być wykonywane.</span><span class="sxs-lookup"><span data-stu-id="07708-296">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="07708-297">Nadal trzeba przywrócić projektu, zanim można spakować soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="07708-297">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="07708-298">Platforma docelowa pliku projektu nie ma znaczenia, a nie używany podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="07708-298">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="07708-299">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania, za pomocą `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="07708-299">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="07708-300">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` plików używanych na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="07708-300">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="07708-301">`NuspecProperties`: rozdzieloną średnikami listę klucz = wartość pary.</span><span class="sxs-lookup"><span data-stu-id="07708-301">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="07708-302">Ze względu na sposób MSBuild wiersza polecenia analizy działa wiele właściwości należy określić w następujący sposób: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="07708-302">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="07708-303">`NuspecBasePath`: Podstawową ścieżkę dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="07708-303">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="07708-304">Jeśli przy użyciu `dotnet.exe` umieszczenie projektu, użyj polecenia podobnego do poniższego:</span><span class="sxs-lookup"><span data-stu-id="07708-304">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="07708-305">Jeśli korzystanie z MSBuild do pakietu projektu, należy użyć polecenie podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="07708-305">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="07708-306">Należy pamiętać, pakowanie nuspec przy użyciu dotnet.exe lub msbuild również prowadzi do kompilowania projektu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="07708-306">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="07708-307">Można tego uniknąć, przekazując ```--no-build``` właściwości dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu oraz ustawienie ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="07708-307">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="07708-308">Przykładowy plik csproj, umieszczenie soubor nuspec jest:</span><span class="sxs-lookup"><span data-stu-id="07708-308">An example of a csproj file to pack a nuspec file is:</span></span>

```xml
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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="07708-309">Zaawansowane punktów rozszerzenia, aby utworzyć dostosowany pakiet</span><span class="sxs-lookup"><span data-stu-id="07708-309">Advanced extension points to create customized package</span></span>

<span data-ttu-id="07708-310">`pack` Docelowy zawiera dwa punkty rozszerzenia, które działają w wewnętrznej, target framework kompilacji.</span><span class="sxs-lookup"><span data-stu-id="07708-310">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="07708-311">Punkty rozszerzenia obsługi w tym target framework określoną zawartość i zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="07708-311">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="07708-312">`TargetsForTfmSpecificBuildOutput` Element docelowy: Pliki znajdujące się na użytek `lib` folder lub folder określony za pomocą `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="07708-312">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="07708-313">`TargetsForTfmSpecificContentInPackage` Element docelowy: Na użytek plików poza `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="07708-313">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="07708-314">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="07708-314">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="07708-315">Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="07708-315">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="07708-316">Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), element docelowy powinien zapisać te pliki do element ItemGroup `BuildOutputInPackage` i ustaw poniższe dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="07708-316">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="07708-317">`FinalOutputPath`: Ścieżka bezwzględna pliku. Jeśli nie zostanie podana, tożsamość jest używane do analizowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="07708-317">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="07708-318">`TargetPath`:  (Opcjonalnie) Ustawiana, jeśli plik musi przejść do podfolderu w `lib\<TargetFramework>` , takich jak zestawy satelickie tego go w ramach ich odpowiednich kultury folderów.</span><span class="sxs-lookup"><span data-stu-id="07708-318">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="07708-319">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="07708-319">Defaults to the name of the file.</span></span>

<span data-ttu-id="07708-320">Przykład:</span><span class="sxs-lookup"><span data-stu-id="07708-320">Example:</span></span>

```xml
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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="07708-321">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="07708-321">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="07708-322">Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="07708-322">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="07708-323">Dla wszystkich plików do uwzględnienia w pakiecie docelowym powinien zapisać te pliki do element ItemGroup `TfmSpecificPackageFile` i ustaw następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="07708-323">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="07708-324">`PackagePath`: Ścieżka, w którym plik powinien znajdować się w danych wyjściowych w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="07708-324">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="07708-325">NuGet generuje ostrzeżenie, jeśli więcej niż jeden plik jest dodawany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="07708-325">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="07708-326">`BuildAction`: Akcja kompilacji, aby przypisać do pliku, jest wymagany tylko, jeśli ścieżka pakietu jest w `contentFiles` folderu.</span><span class="sxs-lookup"><span data-stu-id="07708-326">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="07708-327">Wartość domyślna to "None".</span><span class="sxs-lookup"><span data-stu-id="07708-327">Defaults to "None".</span></span>

<span data-ttu-id="07708-328">Przykład:</span><span class="sxs-lookup"><span data-stu-id="07708-328">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="07708-329">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="07708-329">restore target</span></span>

<span data-ttu-id="07708-330">`MSBuild -t:restore` (który `nuget restore` i `dotnet restore` za pomocą projektów .NET Core), pakiety, do którego odwołuje się plik projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="07708-330">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="07708-331">Odczyt wszystkich odwołań między projektami</span><span class="sxs-lookup"><span data-stu-id="07708-331">Read all project to project references</span></span>
1. <span data-ttu-id="07708-332">Odczyt właściwości projektu, aby znaleźć pośrednich struktur dla folderu docelowego</span><span class="sxs-lookup"><span data-stu-id="07708-332">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="07708-333">Przekazywanie danych programu MSBuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="07708-333">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="07708-334">Uruchom Przywracanie</span><span class="sxs-lookup"><span data-stu-id="07708-334">Run restore</span></span>
1. <span data-ttu-id="07708-335">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="07708-335">Download packages</span></span>
1. <span data-ttu-id="07708-336">Zapisu pliku zasobów, obiektów docelowych i właściwości</span><span class="sxs-lookup"><span data-stu-id="07708-336">Write assets file, targets, and props</span></span>

<span data-ttu-id="07708-337">`restore` Docelowy działa **tylko** dla projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="07708-337">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="07708-338">Robi **nie** nadają się do projektów przy użyciu `packages.config` formatowania; użyj [Przywracanie pakietów nuget](../tools/cli-ref-restore.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="07708-338">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="07708-339">Przywracanie właściwości</span><span class="sxs-lookup"><span data-stu-id="07708-339">Restore properties</span></span>

<span data-ttu-id="07708-340">Ustawienia dodatkowe przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="07708-340">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="07708-341">Ponadto można ustawić wartości z wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="07708-341">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="07708-342">Właściwość</span><span class="sxs-lookup"><span data-stu-id="07708-342">Property</span></span> | <span data-ttu-id="07708-343">Opis</span><span class="sxs-lookup"><span data-stu-id="07708-343">Description</span></span> |
|--------|--------|
| <span data-ttu-id="07708-344">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="07708-344">RestoreSources</span></span> | <span data-ttu-id="07708-345">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="07708-345">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="07708-346">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="07708-346">RestorePackagesPath</span></span> | <span data-ttu-id="07708-347">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07708-347">User packages folder path.</span></span> |
| <span data-ttu-id="07708-348">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="07708-348">RestoreDisableParallel</span></span> | <span data-ttu-id="07708-349">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="07708-349">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="07708-350">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="07708-350">RestoreConfigFile</span></span> | <span data-ttu-id="07708-351">Ścieżka do `Nuget.Config` pliku, aby zastosować.</span><span class="sxs-lookup"><span data-stu-id="07708-351">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="07708-352">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="07708-352">RestoreNoCache</span></span> | <span data-ttu-id="07708-353">W przypadku wartości true umożliwia uniknięcie korzystania z pamięci podręcznej pakietów.</span><span class="sxs-lookup"><span data-stu-id="07708-353">If true, avoids using cached packages.</span></span> <span data-ttu-id="07708-354">Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="07708-354">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="07708-355">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="07708-355">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="07708-356">W przypadku opcji true ignoruje awarie lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="07708-356">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="07708-357">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="07708-357">RestoreFallbackFolders</span></span> | <span data-ttu-id="07708-358">Rezerwowy foldery, używane w taki sam sposób pakiety użytkownika, który jest używany folder.</span><span class="sxs-lookup"><span data-stu-id="07708-358">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="07708-359">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="07708-359">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="07708-360">Dodatkowe zasoby do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="07708-360">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="07708-361">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="07708-361">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="07708-362">Dodatkowe rezerwowego foldery do wykorzystania podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="07708-362">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="07708-363">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="07708-363">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="07708-364">Wyklucza rezerwowego foldery określone w `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="07708-364">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="07708-365">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="07708-365">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="07708-366">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="07708-366">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="07708-367">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="07708-367">RestoreGraphProjectInput</span></span> | <span data-ttu-id="07708-368">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="07708-368">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="07708-369">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="07708-369">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="07708-370">Gdy projekty są zbierane za pomocą programu MSBuild Określa, czy ich są zbierane przy użyciu `SkipNonexistentTargets` optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="07708-370">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="07708-371">Gdy nie są ustawione, wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="07708-371">When not set, defaults to `true`.</span></span> <span data-ttu-id="07708-372">Jego konsekwencję jest zachowanie bezawaryjną, gdy obiekt docelowy projektu nie może zostać zaimportowany.</span><span class="sxs-lookup"><span data-stu-id="07708-372">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="07708-373">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="07708-373">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="07708-374">Folder wyjściowy, przyjęty `BaseIntermediateOutputPath` i `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="07708-374">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="07708-375">Przykłady</span><span class="sxs-lookup"><span data-stu-id="07708-375">Examples</span></span>

<span data-ttu-id="07708-376">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="07708-376">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="07708-377">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="07708-377">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="07708-378">Przywracanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="07708-378">Restore outputs</span></span>

<span data-ttu-id="07708-379">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="07708-379">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="07708-380">Plik</span><span class="sxs-lookup"><span data-stu-id="07708-380">File</span></span> | <span data-ttu-id="07708-381">Opis</span><span class="sxs-lookup"><span data-stu-id="07708-381">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="07708-382">Zawiera wykres zależności dla wszystkich odwołań do pakietów.</span><span class="sxs-lookup"><span data-stu-id="07708-382">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="07708-383">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="07708-383">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="07708-384">Odwołania do elementów docelowych MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="07708-384">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="07708-385">Przywracanie i tworzenie za pomocą jednego polecenia programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="07708-385">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="07708-386">Fakt, że NuGet można przywrócić pakietów, które obniżyć elementów docelowych MSBuild oraz właściwości, przywracania i ocen kompilacji są uruchamiane przy użyciu różnych właściwości globalne.</span><span class="sxs-lookup"><span data-stu-id="07708-386">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="07708-387">To oznacza, że następujące będzie mieć nieprzewidywalnością i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="07708-387">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="07708-388">Zamiast tego zaleca:</span><span class="sxs-lookup"><span data-stu-id="07708-388">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="07708-389">Ta sama logika dotyczy do innych celów, które są podobne do `build`.</span><span class="sxs-lookup"><span data-stu-id="07708-389">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="07708-390">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="07708-390">PackageTargetFallback</span></span>

<span data-ttu-id="07708-391">`PackageTargetFallback` Element umożliwia określenie zestawu zgodnych elementów docelowych do użycia podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="07708-391">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="07708-392">Został zaprojektowany tak, aby zezwolić na pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklarują dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="07708-392">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="07708-393">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkich pakietów to zależy od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do swojego projektu, aby umożliwić-dotnet platform zapewnić ich zgodność za pomocą polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="07708-393">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="07708-394">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależnego pakietu zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projektu zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="07708-394">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="07708-395">Jeśli chcesz w ostatnim biblioteki DLL, wówczas można dodać `PackageTargetFallback` następujący powiedzieć, `portable-net45+win81` Biblioteka DLL jest niezgodny:</span><span class="sxs-lookup"><span data-stu-id="07708-395">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="07708-396">Aby zadeklarować rezerwowe dla wszystkich obiektów docelowych w projekcie, należy pozostawić wyłączone `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="07708-396">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="07708-397">Można także rozszerzyć istniejące `PackageTargetFallback` umieszczając `$(PackageTargetFallback)` jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="07708-397">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="07708-398">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="07708-398">Replacing one library from a restore graph</span></span>

<span data-ttu-id="07708-399">Jeśli chodzi o przeniesienie zły zestaw przywracania, istnieje możliwość wykluczenia pakietów wybór domyślny i zamień ją na własną nazwę.</span><span class="sxs-lookup"><span data-stu-id="07708-399">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="07708-400">Najpierw z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="07708-400">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="07708-401">Następnie dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="07708-401">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
