---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą działać bezpośrednio jako elementów docelowych MSBuild nuget 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8132595cbfaf553736fbcc81aada283a44d6cdbf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324854"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="aaee8-103">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="aaee8-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="aaee8-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="aaee8-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="aaee8-105">Przy użyciu formatu PackageReference NuGet 4.0 + mogą przechowywać metadanych wszystkie manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="aaee8-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="aaee8-106">Za pomocą narzędzia MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` jest przeznaczony dla zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="aaee8-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="aaee8-107">Te obiekty docelowe umożliwiają pracę z NuGet, tak jak przy użyciu innych zadań programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="aaee8-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="aaee8-108">(Dla NuGet 3.x i starszym użyj [pakiet](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="aaee8-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="aaee8-109">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="aaee8-109">Target build order</span></span>

<span data-ttu-id="aaee8-110">Ponieważ `pack` i `restore` są elementy docelowe programu MSBuild, można wywołać, aby zwiększyć przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="aaee8-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="aaee8-111">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu jej.</span><span class="sxs-lookup"><span data-stu-id="aaee8-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="aaee8-112">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="aaee8-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="aaee8-113">Podobnie można zapisać zadania programu MSBuild, napisać własne docelowe i korzystać z właściwości NuGet w zadaniu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="aaee8-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="aaee8-114">Pakiet docelowy</span><span class="sxs-lookup"><span data-stu-id="aaee8-114">pack target</span></span>

<span data-ttu-id="aaee8-115">W przypadku projektów .NET Standard przy użyciu formatu PackageReference, przy użyciu `msbuild -t:pack` pobiera dane wejściowe z pliku projektu w celu utworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="aaee8-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="aaee8-116">W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w obrębie pierwszych `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="aaee8-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="aaee8-117">Zmiany możesz wprowadzić te łatwe w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając polecenie **Edytuj {project_name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="aaee8-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="aaee8-118">Dla wygody tabeli jest zorganizowana według równoważne właściwość [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="aaee8-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="aaee8-119">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane za pomocą narzędzia MSBuild.</span><span class="sxs-lookup"><span data-stu-id="aaee8-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="aaee8-120">Wartość atrybutu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="aaee8-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="aaee8-121">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="aaee8-121">MSBuild Property</span></span> | <span data-ttu-id="aaee8-122">Domyślny</span><span class="sxs-lookup"><span data-stu-id="aaee8-122">Default</span></span> | <span data-ttu-id="aaee8-123">Uwagi</span><span class="sxs-lookup"><span data-stu-id="aaee8-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="aaee8-124">Id</span><span class="sxs-lookup"><span data-stu-id="aaee8-124">Id</span></span> | <span data-ttu-id="aaee8-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="aaee8-125">PackageId</span></span> | <span data-ttu-id="aaee8-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="aaee8-126">AssemblyName</span></span> | <span data-ttu-id="aaee8-127">$(AssemblyName) z programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="aaee8-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="aaee8-128">Wersja</span><span class="sxs-lookup"><span data-stu-id="aaee8-128">Version</span></span> | <span data-ttu-id="aaee8-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="aaee8-129">PackageVersion</span></span> | <span data-ttu-id="aaee8-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="aaee8-130">Version</span></span> | <span data-ttu-id="aaee8-131">Jest to semver zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="aaee8-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="aaee8-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="aaee8-132">VersionPrefix</span></span> | <span data-ttu-id="aaee8-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="aaee8-133">PackageVersionPrefix</span></span> | <span data-ttu-id="aaee8-134">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-134">empty</span></span> | <span data-ttu-id="aaee8-135">Ustawienie PackageVersion zastępuje PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="aaee8-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="aaee8-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="aaee8-136">VersionSuffix</span></span> | <span data-ttu-id="aaee8-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="aaee8-137">PackageVersionSuffix</span></span> | <span data-ttu-id="aaee8-138">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-138">empty</span></span> | <span data-ttu-id="aaee8-139">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="aaee8-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="aaee8-140">Ustawienie PackageVersion zastępuje PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="aaee8-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="aaee8-141">Autorzy</span><span class="sxs-lookup"><span data-stu-id="aaee8-141">Authors</span></span> | <span data-ttu-id="aaee8-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="aaee8-142">Authors</span></span> | <span data-ttu-id="aaee8-143">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="aaee8-143">Username of the current user</span></span> | |
| <span data-ttu-id="aaee8-144">Właściciele</span><span class="sxs-lookup"><span data-stu-id="aaee8-144">Owners</span></span> | <span data-ttu-id="aaee8-145">Brak</span><span class="sxs-lookup"><span data-stu-id="aaee8-145">N/A</span></span> | <span data-ttu-id="aaee8-146">Nie są obecne w NuSpec</span><span class="sxs-lookup"><span data-stu-id="aaee8-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="aaee8-147">Tytuł</span><span class="sxs-lookup"><span data-stu-id="aaee8-147">Title</span></span> | <span data-ttu-id="aaee8-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="aaee8-148">Title</span></span> | <span data-ttu-id="aaee8-149">Jako PackageId</span><span class="sxs-lookup"><span data-stu-id="aaee8-149">The PackageId</span></span>| |
| <span data-ttu-id="aaee8-150">Opis</span><span class="sxs-lookup"><span data-stu-id="aaee8-150">Description</span></span> | <span data-ttu-id="aaee8-151">Opis</span><span class="sxs-lookup"><span data-stu-id="aaee8-151">Description</span></span> | <span data-ttu-id="aaee8-152">"Pakiet opis"</span><span class="sxs-lookup"><span data-stu-id="aaee8-152">"Package Description"</span></span> | |
| <span data-ttu-id="aaee8-153">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="aaee8-153">Copyright</span></span> | <span data-ttu-id="aaee8-154">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="aaee8-154">Copyright</span></span> | <span data-ttu-id="aaee8-155">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-155">empty</span></span> | |
| <span data-ttu-id="aaee8-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="aaee8-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="aaee8-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="aaee8-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="aaee8-158">false</span><span class="sxs-lookup"><span data-stu-id="aaee8-158">false</span></span> | |
| <span data-ttu-id="aaee8-159">Licencja</span><span class="sxs-lookup"><span data-stu-id="aaee8-159">license</span></span> | <span data-ttu-id="aaee8-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="aaee8-160">PackageLicenseExpression</span></span> | <span data-ttu-id="aaee8-161">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-161">empty</span></span> | <span data-ttu-id="aaee8-162">Odnosi się do `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="aaee8-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="aaee8-163">Licencja</span><span class="sxs-lookup"><span data-stu-id="aaee8-163">license</span></span> | <span data-ttu-id="aaee8-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="aaee8-164">PackageLicenseFile</span></span> | <span data-ttu-id="aaee8-165">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-165">empty</span></span> | <span data-ttu-id="aaee8-166">Odnosi się do `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="aaee8-167">Konieczne może być jawnie pakietu pliku odwołania licencji.</span><span class="sxs-lookup"><span data-stu-id="aaee8-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="aaee8-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-168">LicenseUrl</span></span> | <span data-ttu-id="aaee8-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-169">PackageLicenseUrl</span></span> | <span data-ttu-id="aaee8-170">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-170">empty</span></span> | <span data-ttu-id="aaee8-171">`licenseUrl` jest on przestarzały, użyj właściwości PackageLicenseExpression lub PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="aaee8-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="aaee8-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-172">ProjectUrl</span></span> | <span data-ttu-id="aaee8-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-173">PackageProjectUrl</span></span> | <span data-ttu-id="aaee8-174">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-174">empty</span></span> | |
| <span data-ttu-id="aaee8-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-175">IconUrl</span></span> | <span data-ttu-id="aaee8-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-176">PackageIconUrl</span></span> | <span data-ttu-id="aaee8-177">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-177">empty</span></span> | |
| <span data-ttu-id="aaee8-178">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="aaee8-178">Tags</span></span> | <span data-ttu-id="aaee8-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="aaee8-179">PackageTags</span></span> | <span data-ttu-id="aaee8-180">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-180">empty</span></span> | <span data-ttu-id="aaee8-181">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="aaee8-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="aaee8-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="aaee8-182">ReleaseNotes</span></span> | <span data-ttu-id="aaee8-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="aaee8-183">PackageReleaseNotes</span></span> | <span data-ttu-id="aaee8-184">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-184">empty</span></span> | |
| <span data-ttu-id="aaee8-185">Adres Url i repozytorium</span><span class="sxs-lookup"><span data-stu-id="aaee8-185">Repository/Url</span></span> | <span data-ttu-id="aaee8-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-186">RepositoryUrl</span></span> | <span data-ttu-id="aaee8-187">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-187">empty</span></span> | <span data-ttu-id="aaee8-188">Adres URL repozytorium jest używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="aaee8-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="aaee8-189">Przykład: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="aaee8-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="aaee8-190">Repozytorium/typu</span><span class="sxs-lookup"><span data-stu-id="aaee8-190">Repository/Type</span></span> | <span data-ttu-id="aaee8-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="aaee8-191">RepositoryType</span></span> | <span data-ttu-id="aaee8-192">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-192">empty</span></span> | <span data-ttu-id="aaee8-193">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="aaee8-193">Repository type.</span></span> <span data-ttu-id="aaee8-194">Przykłady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="aaee8-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="aaee8-195">Repozytorium/gałąź</span><span class="sxs-lookup"><span data-stu-id="aaee8-195">Repository/Branch</span></span> | <span data-ttu-id="aaee8-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="aaee8-196">RepositoryBranch</span></span> | <span data-ttu-id="aaee8-197">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-197">empty</span></span> | <span data-ttu-id="aaee8-198">Informacje o gałęzi repozytorium opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="aaee8-198">Optional repository branch information.</span></span> <span data-ttu-id="aaee8-199">*RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="aaee8-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="aaee8-200">Przykład: *wzorca* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="aaee8-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="aaee8-201">Repozytorium na zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="aaee8-201">Repository/Commit</span></span> | <span data-ttu-id="aaee8-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="aaee8-202">RepositoryCommit</span></span> | <span data-ttu-id="aaee8-203">empty</span><span class="sxs-lookup"><span data-stu-id="aaee8-203">empty</span></span> | <span data-ttu-id="aaee8-204">Opcjonalne repozytorium zatwierdzenia lub zestaw zmian, aby wskazać, które źródła pakietu została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="aaee8-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="aaee8-205">*RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="aaee8-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="aaee8-206">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="aaee8-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="aaee8-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="aaee8-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="aaee8-208">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="aaee8-208">Summary</span></span> | <span data-ttu-id="aaee8-209">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="aaee8-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="aaee8-210">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="aaee8-210">pack target inputs</span></span>

- <span data-ttu-id="aaee8-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="aaee8-211">IsPackable</span></span>
- <span data-ttu-id="aaee8-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="aaee8-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="aaee8-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="aaee8-213">PackageVersion</span></span>
- <span data-ttu-id="aaee8-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="aaee8-214">PackageId</span></span>
- <span data-ttu-id="aaee8-215">Autorzy</span><span class="sxs-lookup"><span data-stu-id="aaee8-215">Authors</span></span>
- <span data-ttu-id="aaee8-216">Opis</span><span class="sxs-lookup"><span data-stu-id="aaee8-216">Description</span></span>
- <span data-ttu-id="aaee8-217">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="aaee8-217">Copyright</span></span>
- <span data-ttu-id="aaee8-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="aaee8-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="aaee8-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="aaee8-219">DevelopmentDependency</span></span>
- <span data-ttu-id="aaee8-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="aaee8-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="aaee8-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="aaee8-221">PackageLicenseFile</span></span>
- <span data-ttu-id="aaee8-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="aaee8-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-223">PackageProjectUrl</span></span>
- <span data-ttu-id="aaee8-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-224">PackageIconUrl</span></span>
- <span data-ttu-id="aaee8-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="aaee8-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="aaee8-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="aaee8-226">PackageTags</span></span>
- <span data-ttu-id="aaee8-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="aaee8-227">PackageOutputPath</span></span>
- <span data-ttu-id="aaee8-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="aaee8-228">IncludeSymbols</span></span>
- <span data-ttu-id="aaee8-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="aaee8-229">IncludeSource</span></span>
- <span data-ttu-id="aaee8-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="aaee8-230">PackageTypes</span></span>
- <span data-ttu-id="aaee8-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="aaee8-231">IsTool</span></span>
- <span data-ttu-id="aaee8-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-232">RepositoryUrl</span></span>
- <span data-ttu-id="aaee8-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="aaee8-233">RepositoryType</span></span>
- <span data-ttu-id="aaee8-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="aaee8-234">RepositoryBranch</span></span>
- <span data-ttu-id="aaee8-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="aaee8-235">RepositoryCommit</span></span>
- <span data-ttu-id="aaee8-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="aaee8-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="aaee8-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="aaee8-237">MinClientVersion</span></span>
- <span data-ttu-id="aaee8-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="aaee8-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="aaee8-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="aaee8-239">IncludeContentInPack</span></span>
- <span data-ttu-id="aaee8-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="aaee8-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="aaee8-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="aaee8-241">ContentTargetFolders</span></span>
- <span data-ttu-id="aaee8-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="aaee8-242">NuspecFile</span></span>
- <span data-ttu-id="aaee8-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="aaee8-243">NuspecBasePath</span></span>
- <span data-ttu-id="aaee8-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="aaee8-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="aaee8-245">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="aaee8-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="aaee8-246">Pomiń zależności</span><span class="sxs-lookup"><span data-stu-id="aaee8-246">Suppress dependencies</span></span>

<span data-ttu-id="aaee8-247">Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet, należy ustawić `SuppressDependenciesWhenPacking` do `true` co pozwoli pomija wszystkie zależności z nupkg wygenerowany plik.</span><span class="sxs-lookup"><span data-stu-id="aaee8-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="aaee8-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="aaee8-248">PackageIconUrl</span></span>

<span data-ttu-id="aaee8-249">Zmiana w ramach [352 problem NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` ostatecznie zostanie zmieniony na `PackageIconUri` i może być ścieżką względną do pliku ikony, który zostanie uwzględniony w katalogu głównym pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="aaee8-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="aaee8-250">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="aaee8-250">Output assemblies</span></span>

<span data-ttu-id="aaee8-251">`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="aaee8-252">Pliki wyjściowe, które są kopiowane zależą od tego, co MSBuild zapewnia klientom — od `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="aaee8-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="aaee8-253">Istnieją dwie właściwości programu MSBuild, które można w pliku projektu lub wiersza polecenia do kontrolki gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="aaee8-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="aaee8-254">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="aaee8-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="aaee8-255">`BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="aaee8-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="aaee8-256">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich ramach folderów.</span><span class="sxs-lookup"><span data-stu-id="aaee8-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="aaee8-257">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="aaee8-257">Package references</span></span>

<span data-ttu-id="aaee8-258">Zobacz [pakietu odwołania w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="aaee8-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="aaee8-259">Projekt do odwołania do projektu</span><span class="sxs-lookup"><span data-stu-id="aaee8-259">Project to project references</span></span>

<span data-ttu-id="aaee8-260">Projekt do odwołania do projektu są uznawane za domyślnie odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="aaee8-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="aaee8-261">Można również dodać następujące metadane, do której można się odwołać projektu:</span><span class="sxs-lookup"><span data-stu-id="aaee8-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="aaee8-262">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="aaee8-262">Including content in a package</span></span>

<span data-ttu-id="aaee8-263">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="aaee8-264">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że przesłonisz z wpisy jak następujące:</span><span class="sxs-lookup"><span data-stu-id="aaee8-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="aaee8-265">Domyślnie dodawane pobiera wszystkie elementy w folderze głównym `content` i `contentFiles\any\<target_framework>` folder, w ramach pakietu i zachowuje strukturę folderu względnego, chyba że określisz Ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="aaee8-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="aaee8-266">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` zarówno), można użyć właściwości programu MSBuild `ContentTargetFolders`, którego wartość domyślna to "zawartość; pliki", ale może być ustawiona na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="aaee8-267">Należy pamiętać, który po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="aaee8-268">`PackagePath` może być rozdzielone średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="aaee8-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="aaee8-269">Określenie ścieżki pusty pakiet dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="aaee8-270">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="aaee8-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="aaee8-271">Istnieje również właściwość narzędzia MSBuild `$(IncludeContentInPack)`, które domyślnie używa `true`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="aaee8-272">Jeśli jest ono ustawione na `false` w żadnym projekcie następnie zawartość z tego projektu nie są uwzględnione w pakiet nuget.</span><span class="sxs-lookup"><span data-stu-id="aaee8-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="aaee8-273">Obejmuje inne określonych metadanych pakietu, który dla każdego z powyższych elementów można ustawić ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który konfiguruje ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpis nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="aaee8-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="aaee8-274">Oprócz elementów zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić w plikach za pomocą akcji kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource lub Brak.</span><span class="sxs-lookup"><span data-stu-id="aaee8-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="aaee8-275">Pakiet można dołączyć nazwę pliku do ścieżki pakietu, korzystając z wzorców obsługi symboli wieloznacznych ścieżka do pakietu musi kończyć folderu znaku separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełną ścieżkę, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="aaee8-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="aaee8-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="aaee8-276">IncludeSymbols</span></span>

<span data-ttu-id="aaee8-277">Korzystając z `MSBuild -t:pack -p:IncludeSymbols=true`, odpowiedni `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="aaee8-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="aaee8-278">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="aaee8-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="aaee8-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="aaee8-279">IncludeSource</span></span>

<span data-ttu-id="aaee8-280">To jest taka sama jak `IncludeSymbols`, chyba że kopiuje pliki źródłowe, wraz z `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="aaee8-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="aaee8-281">Pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną do pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="aaee8-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="aaee8-282">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` równa `false`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="aaee8-283">Plik typu kompilacji, czy poza folderem projektu, a następnie po prostu dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="aaee8-284">Pakowanie wyrażenie licencji lub też pliku licencji</span><span class="sxs-lookup"><span data-stu-id="aaee8-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="aaee8-285">Korzystając z wyrażenia licencji, właściwość PackageLicenseExpression powinna być używana.</span><span class="sxs-lookup"><span data-stu-id="aaee8-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="aaee8-286">[Przykładowe wyrażenie licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="aaee8-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="aaee8-287">[Dowiedz się więcej na temat wyrażeń licencji i licencji, które są akceptowane przez NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="aaee8-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="aaee8-288">Podczas pakowania pliku licencji, należy użyć właściwości PackageLicenseFile do określenia ścieżki pakietu, względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="aaee8-289">Ponadto należy się upewnić, że plik znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="aaee8-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="aaee8-290">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="aaee8-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="aaee8-291">[Przykładowy plik licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="aaee8-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="aaee8-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="aaee8-292">IsTool</span></span>

<span data-ttu-id="aaee8-293">Korzystając z `MSBuild -t:pack -p:IsTool=true`, wszystkie dane wyjściowe pliki, jak to określono w [zestawów danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folderu zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="aaee8-294">Należy pamiętać, że to różni się od `DotNetCliTool` określić, ustawiając `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="aaee8-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="aaee8-295">Pakowanie przy użyciu .nuspec</span><span class="sxs-lookup"><span data-stu-id="aaee8-295">Packing using a .nuspec</span></span>

<span data-ttu-id="aaee8-296">Możesz użyć `.nuspec` pliku do pakietu projektu, pod warunkiem, że masz zestaw SDK plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` tak, aby zadanie pakietów, które mogą być wykonywane.</span><span class="sxs-lookup"><span data-stu-id="aaee8-296">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="aaee8-297">Nadal trzeba przywrócić projektu, zanim można spakować soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="aaee8-297">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="aaee8-298">Platforma docelowa pliku projektu nie ma znaczenia, a nie używany podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="aaee8-298">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="aaee8-299">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania, za pomocą `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="aaee8-299">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="aaee8-300">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` plików używanych na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="aaee8-300">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="aaee8-301">`NuspecProperties`: rozdzieloną średnikami listę klucz = wartość pary.</span><span class="sxs-lookup"><span data-stu-id="aaee8-301">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="aaee8-302">Ze względu na sposób MSBuild wiersza polecenia analizy działa wiele właściwości należy określić w następujący sposób: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-302">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="aaee8-303">`NuspecBasePath`: Podstawową ścieżkę dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="aaee8-303">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="aaee8-304">Jeśli przy użyciu `dotnet.exe` umieszczenie projektu, użyj polecenia podobnego do poniższego:</span><span class="sxs-lookup"><span data-stu-id="aaee8-304">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="aaee8-305">Jeśli korzystanie z MSBuild do pakietu projektu, należy użyć polecenie podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="aaee8-305">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="aaee8-306">Należy pamiętać, pakowanie nuspec przy użyciu dotnet.exe lub msbuild również prowadzi do kompilowania projektu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="aaee8-306">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="aaee8-307">Można tego uniknąć, przekazując ```--no-build``` właściwości dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu oraz ustawienie ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="aaee8-307">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="aaee8-308">Przykładowy plik csproj, umieszczenie soubor nuspec jest:</span><span class="sxs-lookup"><span data-stu-id="aaee8-308">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="aaee8-309">Zaawansowane punktów rozszerzenia, aby utworzyć dostosowany pakiet</span><span class="sxs-lookup"><span data-stu-id="aaee8-309">Advanced extension points to create customized package</span></span>

<span data-ttu-id="aaee8-310">`pack` Docelowy zawiera dwa punkty rozszerzenia, które działają w wewnętrznej, target framework kompilacji.</span><span class="sxs-lookup"><span data-stu-id="aaee8-310">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="aaee8-311">Punkty rozszerzenia obsługi w tym target framework określoną zawartość i zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="aaee8-311">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="aaee8-312">`TargetsForTfmSpecificBuildOutput` Element docelowy: Pliki znajdujące się na użytek `lib` folder lub folder określony za pomocą `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-312">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="aaee8-313">`TargetsForTfmSpecificContentInPackage` Element docelowy: Na użytek plików poza `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-313">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="aaee8-314">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="aaee8-314">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="aaee8-315">Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="aaee8-315">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="aaee8-316">Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), element docelowy powinien zapisać te pliki do element ItemGroup `BuildOutputInPackage` i ustaw poniższe dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="aaee8-316">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="aaee8-317">`FinalOutputPath`: Ścieżka bezwzględna pliku. Jeśli nie zostanie podana, tożsamość jest używane do analizowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="aaee8-317">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="aaee8-318">`TargetPath`:  (Opcjonalnie) Ustawiana, jeśli plik musi przejść do podfolderu w `lib\<TargetFramework>` , takich jak zestawy satelickie tego go w ramach ich odpowiednich kultury folderów.</span><span class="sxs-lookup"><span data-stu-id="aaee8-318">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="aaee8-319">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="aaee8-319">Defaults to the name of the file.</span></span>

<span data-ttu-id="aaee8-320">Przykład:</span><span class="sxs-lookup"><span data-stu-id="aaee8-320">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="aaee8-321">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="aaee8-321">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="aaee8-322">Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="aaee8-322">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="aaee8-323">Dla wszystkich plików do uwzględnienia w pakiecie docelowym powinien zapisać te pliki do element ItemGroup `TfmSpecificPackageFile` i ustaw następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="aaee8-323">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="aaee8-324">`PackagePath`: Ścieżka, w którym plik powinien znajdować się w danych wyjściowych w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="aaee8-324">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="aaee8-325">NuGet generuje ostrzeżenie, jeśli więcej niż jeden plik jest dodawany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-325">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="aaee8-326">`BuildAction`: Akcja kompilacji, aby przypisać do pliku, jest wymagany tylko, jeśli ścieżka pakietu jest w `contentFiles` folderu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-326">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="aaee8-327">Wartość domyślna to "None".</span><span class="sxs-lookup"><span data-stu-id="aaee8-327">Defaults to "None".</span></span>

<span data-ttu-id="aaee8-328">Przykład:</span><span class="sxs-lookup"><span data-stu-id="aaee8-328">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="aaee8-329">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="aaee8-329">restore target</span></span>

<span data-ttu-id="aaee8-330">`MSBuild -t:restore` (który `nuget restore` i `dotnet restore` za pomocą projektów .NET Core), pakiety, do którego odwołuje się plik projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="aaee8-330">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="aaee8-331">Odczyt wszystkich odwołań między projektami</span><span class="sxs-lookup"><span data-stu-id="aaee8-331">Read all project to project references</span></span>
1. <span data-ttu-id="aaee8-332">Odczyt właściwości projektu, aby znaleźć pośrednich struktur dla folderu docelowego</span><span class="sxs-lookup"><span data-stu-id="aaee8-332">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="aaee8-333">Pass msbuild data to NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="aaee8-333">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="aaee8-334">Uruchom Przywracanie</span><span class="sxs-lookup"><span data-stu-id="aaee8-334">Run restore</span></span>
1. <span data-ttu-id="aaee8-335">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="aaee8-335">Download packages</span></span>
1. <span data-ttu-id="aaee8-336">Zapisu pliku zasobów, obiektów docelowych i właściwości</span><span class="sxs-lookup"><span data-stu-id="aaee8-336">Write assets file, targets, and props</span></span>

<span data-ttu-id="aaee8-337">`restore` Docelowy działa **tylko** dla projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="aaee8-337">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="aaee8-338">Robi **nie** nadają się do projektów przy użyciu `packages.config` formatowania; użyj [Przywracanie pakietów nuget](../tools/cli-ref-restore.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="aaee8-338">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="aaee8-339">Przywracanie właściwości</span><span class="sxs-lookup"><span data-stu-id="aaee8-339">Restore properties</span></span>

<span data-ttu-id="aaee8-340">Ustawienia dodatkowe przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-340">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="aaee8-341">Ponadto można ustawić wartości z wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="aaee8-341">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="aaee8-342">Właściwość</span><span class="sxs-lookup"><span data-stu-id="aaee8-342">Property</span></span> | <span data-ttu-id="aaee8-343">Opis</span><span class="sxs-lookup"><span data-stu-id="aaee8-343">Description</span></span> |
|--------|--------|
| <span data-ttu-id="aaee8-344">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="aaee8-344">RestoreSources</span></span> | <span data-ttu-id="aaee8-345">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="aaee8-345">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="aaee8-346">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="aaee8-346">RestorePackagesPath</span></span> | <span data-ttu-id="aaee8-347">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aaee8-347">User packages folder path.</span></span> |
| <span data-ttu-id="aaee8-348">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="aaee8-348">RestoreDisableParallel</span></span> | <span data-ttu-id="aaee8-349">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="aaee8-349">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="aaee8-350">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="aaee8-350">RestoreConfigFile</span></span> | <span data-ttu-id="aaee8-351">Ścieżka do `Nuget.Config` pliku, aby zastosować.</span><span class="sxs-lookup"><span data-stu-id="aaee8-351">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="aaee8-352">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="aaee8-352">RestoreNoCache</span></span> | <span data-ttu-id="aaee8-353">W przypadku wartości true umożliwia uniknięcie korzystania z pamięci podręcznej pakietów.</span><span class="sxs-lookup"><span data-stu-id="aaee8-353">If true, avoids using cached packages.</span></span> <span data-ttu-id="aaee8-354">Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="aaee8-354">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="aaee8-355">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="aaee8-355">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="aaee8-356">W przypadku opcji true ignoruje awarie lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="aaee8-356">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="aaee8-357">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="aaee8-357">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="aaee8-358">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="aaee8-358">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="aaee8-359">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="aaee8-359">RestoreGraphProjectInput</span></span> | <span data-ttu-id="aaee8-360">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="aaee8-360">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="aaee8-361">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="aaee8-361">RestoreOutputPath</span></span> | <span data-ttu-id="aaee8-362">Folder wyjściowy, przyjęty `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-362">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="aaee8-363">Przykłady</span><span class="sxs-lookup"><span data-stu-id="aaee8-363">Examples</span></span>

<span data-ttu-id="aaee8-364">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="aaee8-364">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="aaee8-365">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="aaee8-365">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="aaee8-366">Przywracanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="aaee8-366">Restore outputs</span></span>

<span data-ttu-id="aaee8-367">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="aaee8-367">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="aaee8-368">Plik</span><span class="sxs-lookup"><span data-stu-id="aaee8-368">File</span></span> | <span data-ttu-id="aaee8-369">Opis</span><span class="sxs-lookup"><span data-stu-id="aaee8-369">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="aaee8-370">Zawiera wykres zależności dla wszystkich odwołań do pakietów.</span><span class="sxs-lookup"><span data-stu-id="aaee8-370">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="aaee8-371">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="aaee8-371">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="aaee8-372">Odwołania do elementów docelowych MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="aaee8-372">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="aaee8-373">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="aaee8-373">PackageTargetFallback</span></span>

<span data-ttu-id="aaee8-374">`PackageTargetFallback` Element umożliwia określenie zestawu zgodnych elementów docelowych do użycia podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="aaee8-374">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="aaee8-375">Został zaprojektowany tak, aby zezwolić na pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklarują dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="aaee8-375">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="aaee8-376">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkich pakietów to zależy od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do swojego projektu, aby umożliwić-dotnet platform zapewnić ich zgodność za pomocą polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="aaee8-376">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="aaee8-377">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależnego pakietu zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projektu zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="aaee8-377">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="aaee8-378">Jeśli chcesz w ostatnim biblioteki DLL, wówczas można dodać `PackageTargetFallback` następujący powiedzieć, `portable-net45+win81` Biblioteka DLL jest niezgodny:</span><span class="sxs-lookup"><span data-stu-id="aaee8-378">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="aaee8-379">Aby zadeklarować rezerwowe dla wszystkich obiektów docelowych w projekcie, należy pozostawić wyłączone `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="aaee8-379">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="aaee8-380">Można także rozszerzyć istniejące `PackageTargetFallback` umieszczając `$(PackageTargetFallback)` jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="aaee8-380">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="aaee8-381">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="aaee8-381">Replacing one library from a restore graph</span></span>

<span data-ttu-id="aaee8-382">Jeśli chodzi o przeniesienie zły zestaw przywracania, istnieje możliwość wykluczenia pakietów wybór domyślny i zamień ją na własną nazwę.</span><span class="sxs-lookup"><span data-stu-id="aaee8-382">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="aaee8-383">Najpierw z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="aaee8-383">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="aaee8-384">Następnie dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="aaee8-384">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
