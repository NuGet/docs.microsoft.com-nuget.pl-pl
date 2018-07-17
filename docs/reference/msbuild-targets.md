---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą działać bezpośrednio jako elementów docelowych MSBuild nuget 4.0 +.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0e7e0952519afdcb4b50f31d33cce2a92e3579b4
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/17/2018
ms.locfileid: "39069703"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="fbbc1-103">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="fbbc1-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="fbbc1-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="fbbc1-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="fbbc1-105">Przy użyciu formatu PackageReference NuGet 4.0 + mogą przechowywać metadanych wszystkie manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="fbbc1-106">Za pomocą narzędzia MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` jest przeznaczony dla zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="fbbc1-107">Te obiekty docelowe umożliwiają pracę z NuGet, tak jak przy użyciu innych zadań programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="fbbc1-108">(Dla NuGet 3.x i starszym użyj [pakiet](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="fbbc1-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="fbbc1-109">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="fbbc1-109">Target build order</span></span>

<span data-ttu-id="fbbc1-110">Ponieważ `pack` i `restore` są elementy docelowe programu MSBuild, można wywołać, aby zwiększyć przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="fbbc1-111">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu jej.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="fbbc1-112">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="fbbc1-113">Podobnie można zapisać zadania programu MSBuild, napisać własne docelowe i korzystać z właściwości NuGet w zadaniu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="fbbc1-114">Pakiet docelowy</span><span class="sxs-lookup"><span data-stu-id="fbbc1-114">pack target</span></span>

<span data-ttu-id="fbbc1-115">W przypadku projektów .NET Standard przy użyciu formatu PackageReference, przy użyciu `msbuild /t:pack` pobiera dane wejściowe z pliku projektu w celu utworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="fbbc1-116">W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w obrębie pierwszych `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="fbbc1-117">Zmiany możesz wprowadzić te łatwe w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając polecenie **Edytuj {project_name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="fbbc1-118">Dla wygody tabeli jest zorganizowana według równoważne właściwość [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="fbbc1-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="fbbc1-119">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane za pomocą narzędzia MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="fbbc1-120">Wartość atrybutu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="fbbc1-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="fbbc1-121">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="fbbc1-121">MSBuild Property</span></span> | <span data-ttu-id="fbbc1-122">Domyślny</span><span class="sxs-lookup"><span data-stu-id="fbbc1-122">Default</span></span> | <span data-ttu-id="fbbc1-123">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fbbc1-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="fbbc1-124">Id</span><span class="sxs-lookup"><span data-stu-id="fbbc1-124">Id</span></span> | <span data-ttu-id="fbbc1-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="fbbc1-125">PackageId</span></span> | <span data-ttu-id="fbbc1-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="fbbc1-126">AssemblyName</span></span> | <span data-ttu-id="fbbc1-127">$(AssemblyName) z programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="fbbc1-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="fbbc1-128">Wersja</span><span class="sxs-lookup"><span data-stu-id="fbbc1-128">Version</span></span> | <span data-ttu-id="fbbc1-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fbbc1-129">PackageVersion</span></span> | <span data-ttu-id="fbbc1-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="fbbc1-130">Version</span></span> | <span data-ttu-id="fbbc1-131">Jest to semver zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="fbbc1-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="fbbc1-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fbbc1-132">VersionPrefix</span></span> | <span data-ttu-id="fbbc1-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fbbc1-133">PackageVersionPrefix</span></span> | <span data-ttu-id="fbbc1-134">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-134">empty</span></span> | <span data-ttu-id="fbbc1-135">Ustawienie PackageVersion zastępuje PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fbbc1-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="fbbc1-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fbbc1-136">VersionSuffix</span></span> | <span data-ttu-id="fbbc1-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fbbc1-137">PackageVersionSuffix</span></span> | <span data-ttu-id="fbbc1-138">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-138">empty</span></span> | <span data-ttu-id="fbbc1-139">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="fbbc1-140">Ustawienie PackageVersion zastępuje PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fbbc1-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="fbbc1-141">Autorzy</span><span class="sxs-lookup"><span data-stu-id="fbbc1-141">Authors</span></span> | <span data-ttu-id="fbbc1-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="fbbc1-142">Authors</span></span> | <span data-ttu-id="fbbc1-143">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="fbbc1-143">Username of the current user</span></span> | |
| <span data-ttu-id="fbbc1-144">Właściciele</span><span class="sxs-lookup"><span data-stu-id="fbbc1-144">Owners</span></span> | <span data-ttu-id="fbbc1-145">Brak</span><span class="sxs-lookup"><span data-stu-id="fbbc1-145">N/A</span></span> | <span data-ttu-id="fbbc1-146">Nie są obecne w NuSpec</span><span class="sxs-lookup"><span data-stu-id="fbbc1-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="fbbc1-147">Tytuł</span><span class="sxs-lookup"><span data-stu-id="fbbc1-147">Title</span></span> | <span data-ttu-id="fbbc1-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="fbbc1-148">Title</span></span> | <span data-ttu-id="fbbc1-149">Jako PackageId</span><span class="sxs-lookup"><span data-stu-id="fbbc1-149">The PackageId</span></span>| |
| <span data-ttu-id="fbbc1-150">Opis</span><span class="sxs-lookup"><span data-stu-id="fbbc1-150">Description</span></span> | <span data-ttu-id="fbbc1-151">Opis</span><span class="sxs-lookup"><span data-stu-id="fbbc1-151">Description</span></span> | <span data-ttu-id="fbbc1-152">"Pakiet opis"</span><span class="sxs-lookup"><span data-stu-id="fbbc1-152">"Package Description"</span></span> | |
| <span data-ttu-id="fbbc1-153">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="fbbc1-153">Copyright</span></span> | <span data-ttu-id="fbbc1-154">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="fbbc1-154">Copyright</span></span> | <span data-ttu-id="fbbc1-155">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-155">empty</span></span> | |
| <span data-ttu-id="fbbc1-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fbbc1-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="fbbc1-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fbbc1-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="fbbc1-158">false</span><span class="sxs-lookup"><span data-stu-id="fbbc1-158">false</span></span> | |
| <span data-ttu-id="fbbc1-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-159">LicenseUrl</span></span> | <span data-ttu-id="fbbc1-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-160">PackageLicenseUrl</span></span> | <span data-ttu-id="fbbc1-161">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-161">empty</span></span> | |
| <span data-ttu-id="fbbc1-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-162">ProjectUrl</span></span> | <span data-ttu-id="fbbc1-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-163">PackageProjectUrl</span></span> | <span data-ttu-id="fbbc1-164">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-164">empty</span></span> | |
| <span data-ttu-id="fbbc1-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-165">IconUrl</span></span> | <span data-ttu-id="fbbc1-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-166">PackageIconUrl</span></span> | <span data-ttu-id="fbbc1-167">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-167">empty</span></span> | |
| <span data-ttu-id="fbbc1-168">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="fbbc1-168">Tags</span></span> | <span data-ttu-id="fbbc1-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fbbc1-169">PackageTags</span></span> | <span data-ttu-id="fbbc1-170">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-170">empty</span></span> | <span data-ttu-id="fbbc1-171">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="fbbc1-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fbbc1-172">ReleaseNotes</span></span> | <span data-ttu-id="fbbc1-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fbbc1-173">PackageReleaseNotes</span></span> | <span data-ttu-id="fbbc1-174">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-174">empty</span></span> | |
| <span data-ttu-id="fbbc1-175">Adres Url i repozytorium</span><span class="sxs-lookup"><span data-stu-id="fbbc1-175">Repository/Url</span></span> | <span data-ttu-id="fbbc1-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-176">RepositoryUrl</span></span> | <span data-ttu-id="fbbc1-177">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-177">empty</span></span> | <span data-ttu-id="fbbc1-178">Adres URL repozytorium jest używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="fbbc1-179">Przykład: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="fbbc1-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="fbbc1-180">Repozytorium/typu</span><span class="sxs-lookup"><span data-stu-id="fbbc1-180">Repository/Type</span></span> | <span data-ttu-id="fbbc1-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="fbbc1-181">RepositoryType</span></span> | <span data-ttu-id="fbbc1-182">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-182">empty</span></span> | <span data-ttu-id="fbbc1-183">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-183">Repository type.</span></span> <span data-ttu-id="fbbc1-184">Przykłady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="fbbc1-185">Repozytorium/gałąź</span><span class="sxs-lookup"><span data-stu-id="fbbc1-185">Repository/Branch</span></span> | <span data-ttu-id="fbbc1-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="fbbc1-186">RepositoryBranch</span></span> | <span data-ttu-id="fbbc1-187">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-187">empty</span></span> | <span data-ttu-id="fbbc1-188">Informacje o gałęzi repozytorium opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-188">Optional repository branch information.</span></span> <span data-ttu-id="fbbc1-189">*RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fbbc1-190">Przykład: *wzorca* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="fbbc1-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fbbc1-191">Repozytorium na zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="fbbc1-191">Repository/Commit</span></span> | <span data-ttu-id="fbbc1-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="fbbc1-192">RepositoryCommit</span></span> | <span data-ttu-id="fbbc1-193">empty</span><span class="sxs-lookup"><span data-stu-id="fbbc1-193">empty</span></span> | <span data-ttu-id="fbbc1-194">Opcjonalne repozytorium zatwierdzenia lub zestaw zmian, aby wskazać, które źródła pakietu została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="fbbc1-195">*RepositoryUrl* musi być także określona dla tej właściwości do uwzględnienia.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fbbc1-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="fbbc1-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fbbc1-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="fbbc1-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="fbbc1-198">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fbbc1-198">Summary</span></span> | <span data-ttu-id="fbbc1-199">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="fbbc1-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="fbbc1-200">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="fbbc1-200">pack target inputs</span></span>

- <span data-ttu-id="fbbc1-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="fbbc1-201">IsPackable</span></span>
- <span data-ttu-id="fbbc1-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fbbc1-202">PackageVersion</span></span>
- <span data-ttu-id="fbbc1-203">PackageId</span><span class="sxs-lookup"><span data-stu-id="fbbc1-203">PackageId</span></span>
- <span data-ttu-id="fbbc1-204">Autorzy</span><span class="sxs-lookup"><span data-stu-id="fbbc1-204">Authors</span></span>
- <span data-ttu-id="fbbc1-205">Opis</span><span class="sxs-lookup"><span data-stu-id="fbbc1-205">Description</span></span>
- <span data-ttu-id="fbbc1-206">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="fbbc1-206">Copyright</span></span>
- <span data-ttu-id="fbbc1-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fbbc1-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="fbbc1-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="fbbc1-208">DevelopmentDependency</span></span>
- <span data-ttu-id="fbbc1-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="fbbc1-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-210">PackageProjectUrl</span></span>
- <span data-ttu-id="fbbc1-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-211">PackageIconUrl</span></span>
- <span data-ttu-id="fbbc1-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fbbc1-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="fbbc1-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fbbc1-213">PackageTags</span></span>
- <span data-ttu-id="fbbc1-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="fbbc1-214">PackageOutputPath</span></span>
- <span data-ttu-id="fbbc1-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="fbbc1-215">IncludeSymbols</span></span>
- <span data-ttu-id="fbbc1-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="fbbc1-216">IncludeSource</span></span>
- <span data-ttu-id="fbbc1-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="fbbc1-217">PackageTypes</span></span>
- <span data-ttu-id="fbbc1-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="fbbc1-218">IsTool</span></span>
- <span data-ttu-id="fbbc1-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-219">RepositoryUrl</span></span>
- <span data-ttu-id="fbbc1-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="fbbc1-220">RepositoryType</span></span>
- <span data-ttu-id="fbbc1-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="fbbc1-221">RepositoryBranch</span></span>
- <span data-ttu-id="fbbc1-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="fbbc1-222">RepositoryCommit</span></span>
- <span data-ttu-id="fbbc1-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="fbbc1-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="fbbc1-224">Atrybut MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="fbbc1-224">MinClientVersion</span></span>
- <span data-ttu-id="fbbc1-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fbbc1-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="fbbc1-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="fbbc1-226">IncludeContentInPack</span></span>
- <span data-ttu-id="fbbc1-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="fbbc1-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="fbbc1-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="fbbc1-228">ContentTargetFolders</span></span>
- <span data-ttu-id="fbbc1-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="fbbc1-229">NuspecFile</span></span>
- <span data-ttu-id="fbbc1-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="fbbc1-230">NuspecBasePath</span></span>
- <span data-ttu-id="fbbc1-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="fbbc1-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="fbbc1-232">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="fbbc1-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="fbbc1-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fbbc1-233">PackageIconUrl</span></span>

<span data-ttu-id="fbbc1-234">Zmiana w ramach [352 problem NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` ostatecznie zostanie zmieniony na `PackageIconUri` i może być ścieżką względną do pliku ikony, który zostanie uwzględniony w katalogu głównym pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="fbbc1-235">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="fbbc1-235">Output assemblies</span></span>

<span data-ttu-id="fbbc1-236">`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="fbbc1-237">Pliki wyjściowe, które są kopiowane zależą od tego, co MSBuild zapewnia klientom — od `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="fbbc1-238">Istnieją dwie właściwości programu MSBuild, które można w pliku projektu lub wiersza polecenia do kontrolki gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="fbbc1-239">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="fbbc1-240">`BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="fbbc1-241">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich ramach folderów.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="fbbc1-242">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="fbbc1-242">Package references</span></span>

<span data-ttu-id="fbbc1-243">Zobacz [pakietu odwołania w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="fbbc1-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="fbbc1-244">Projekt do odwołania do projektu</span><span class="sxs-lookup"><span data-stu-id="fbbc1-244">Project to project references</span></span>

<span data-ttu-id="fbbc1-245">Projekt do odwołania do projektu są uznawane za domyślnie odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="fbbc1-246">Można również dodać następujące metadane, do której można się odwołać projektu:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="fbbc1-247">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="fbbc1-247">Including content in a package</span></span>

<span data-ttu-id="fbbc1-248">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="fbbc1-249">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że przesłonisz z wpisy jak następujące:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="fbbc1-250">Domyślnie dodawane pobiera wszystkie elementy w folderze głównym `content` i `contentFiles\any\<target_framework>` folder, w ramach pakietu i zachowuje strukturę folderu względnego, chyba że określisz Ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="fbbc1-251">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` zarówno), można użyć właściwości programu MSBuild `ContentTargetFolders`, którego wartość domyślna to "zawartość; pliki", ale może być ustawiona na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="fbbc1-252">Należy pamiętać, który po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="fbbc1-253">`PackagePath` może być rozdzielone średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="fbbc1-254">Określenie ścieżki pusty pakiet dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="fbbc1-255">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="fbbc1-256">Istnieje również właściwość narzędzia MSBuild `$(IncludeContentInPack)`, które domyślnie używa `true`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="fbbc1-257">Jeśli jest ono ustawione na `false` w żadnym projekcie następnie zawartość z tego projektu nie są uwzględnione w pakiet nuget.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="fbbc1-258">Obejmuje inne określonych metadanych pakietu, który dla każdego z powyższych elementów można ustawić ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który konfiguruje ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpis nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="fbbc1-259">Oprócz elementów zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić w plikach za pomocą akcji kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource lub Brak.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="fbbc1-260">Pakiet można dołączyć nazwę pliku do ścieżki pakietu, korzystając z wzorców obsługi symboli wieloznacznych ścieżka do pakietu musi kończyć folderu znaku separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełną ścieżkę, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="fbbc1-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="fbbc1-261">IncludeSymbols</span></span>

<span data-ttu-id="fbbc1-262">Korzystając z `MSBuild /t:pack /p:IncludeSymbols=true`, odpowiedni `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="fbbc1-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="fbbc1-263">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="fbbc1-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="fbbc1-264">IncludeSource</span></span>

<span data-ttu-id="fbbc1-265">To jest taka sama jak `IncludeSymbols`, chyba że kopiuje pliki źródłowe, wraz z `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="fbbc1-266">Pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną do pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="fbbc1-267">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` równa `false`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="fbbc1-268">Plik typu kompilacji, czy poza folderem projektu, a następnie po prostu dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="fbbc1-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="fbbc1-269">IsTool</span></span>

<span data-ttu-id="fbbc1-270">Korzystając z `MSBuild /t:pack /p:IsTool=true`, wszystkie dane wyjściowe pliki, jak to określono w [zestawów danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folderu zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="fbbc1-271">Należy pamiętać, że to różni się od `DotNetCliTool` określić, ustawiając `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="fbbc1-272">Pakowanie przy użyciu .nuspec</span><span class="sxs-lookup"><span data-stu-id="fbbc1-272">Packing using a .nuspec</span></span>

<span data-ttu-id="fbbc1-273">Możesz użyć `.nuspec` pliku do pakietu projektu, pod warunkiem, że masz zestaw SDK plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` tak, aby zadanie pakietów, które mogą być wykonywane.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="fbbc1-274">Nadal trzeba przywrócić projektu, zanim można spakować soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="fbbc1-275">Platforma docelowa pliku projektu nie ma znaczenia, a nie używany podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="fbbc1-276">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania, za pomocą `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="fbbc1-277">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` plików używanych na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="fbbc1-278">`NuspecProperties`: rozdzieloną średnikami listę klucz = wartość pary.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="fbbc1-279">Ze względu na sposób MSBuild wiersza polecenia analizy działa wiele właściwości należy określić w następujący sposób: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="fbbc1-280">`NuspecBasePath`: Podstawową ścieżkę dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="fbbc1-281">Jeśli przy użyciu `dotnet.exe` umieszczenie projektu, użyj polecenia podobnego do poniższego:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fbbc1-282">Jeśli korzystanie z MSBuild do pakietu projektu, należy użyć polecenie podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fbbc1-283">Należy pamiętać, pakowanie nuspec przy użyciu dotnet.exe lub msbuild również prowadzi do kompilowania projektu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="fbbc1-284">Można tego uniknąć, przekazując ```--no-build``` właściwości dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu oraz ustawienie ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="fbbc1-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="fbbc1-285">Przykładowy plik csproj, umieszczenie soubor nuspec jest:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-285">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="fbbc1-286">Zaawansowane punktów rozszerzenia, aby utworzyć dostosowany pakiet</span><span class="sxs-lookup"><span data-stu-id="fbbc1-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="fbbc1-287">`pack` Docelowy zawiera dwa punkty rozszerzenia, które działają w wewnętrznej, target framework kompilacji.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="fbbc1-288">Punkty rozszerzenia obsługi w tym target framework określoną zawartość i zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="fbbc1-289">`TargetsForTfmSpecificBuildOutput` docelowy: pliki znajdujące się na użytek `lib` folder lub folder określony za pomocą `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="fbbc1-290">`TargetsForTfmSpecificContentInPackage` docelowy: używany do plików znajdujących się poza `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="fbbc1-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fbbc1-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="fbbc1-292">Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="fbbc1-293">Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), element docelowy powinien zapisać te pliki do element ItemGroup `BuildOutputInPackage` i ustaw poniższe dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="fbbc1-294">`FinalOutputPath`: Ścieżka bezwzględna pliku. Jeśli nie zostanie podana, tożsamość jest używane do analizowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="fbbc1-295">`TargetPath`: (Opcjonalnie) ustawiana, jeśli plik musi przejść do podfolderu w `lib\<TargetFramework>` , takich jak zestawy satelickie tego go w ramach ich odpowiednich kultury folderów.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="fbbc1-296">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="fbbc1-297">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-297">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="fbbc1-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="fbbc1-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="fbbc1-299">Zapisz niestandardowe obiekty docelowe i określ ją jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="fbbc1-300">Dla wszystkich plików do uwzględnienia w pakiecie docelowym powinien zapisać te pliki do element ItemGroup `TfmSpecificPackageFile` i ustaw następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="fbbc1-301">`PackagePath`: Ścieżka, gdzie plik powinien znajdować się w danych wyjściowych w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="fbbc1-302">NuGet generuje ostrzeżenie, jeśli więcej niż jeden plik jest dodawany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="fbbc1-303">`BuildAction`: Akcja kompilacji do przypisania do plików, jest wymagany tylko, jeśli ścieżka pakietu jest w `contentFiles` folderu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="fbbc1-304">Wartość domyślna to "None".</span><span class="sxs-lookup"><span data-stu-id="fbbc1-304">Defaults to "None".</span></span>

<span data-ttu-id="fbbc1-305">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-305">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="fbbc1-306">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="fbbc1-306">restore target</span></span>

<span data-ttu-id="fbbc1-307">`MSBuild /t:restore` (który `nuget restore` i `dotnet restore` za pomocą projektów .NET Core), pakiety, do którego odwołuje się plik projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="fbbc1-308">Odczyt wszystkich odwołań między projektami</span><span class="sxs-lookup"><span data-stu-id="fbbc1-308">Read all project to project references</span></span>
1. <span data-ttu-id="fbbc1-309">Odczyt właściwości projektu, aby znaleźć pośrednich struktur dla folderu docelowego</span><span class="sxs-lookup"><span data-stu-id="fbbc1-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="fbbc1-310">Przekazywanie danych programu msbuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="fbbc1-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="fbbc1-311">Uruchom Przywracanie</span><span class="sxs-lookup"><span data-stu-id="fbbc1-311">Run restore</span></span>
1. <span data-ttu-id="fbbc1-312">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="fbbc1-312">Download packages</span></span>
1. <span data-ttu-id="fbbc1-313">Zapisu pliku zasobów, obiektów docelowych i właściwości</span><span class="sxs-lookup"><span data-stu-id="fbbc1-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="fbbc1-314">`restore` Docelowy działa **tylko** dla projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="fbbc1-315">Robi **nie** nadają się do projektów przy użyciu `packages.config` formatowania; użyj [Przywracanie pakietów nuget](../tools/cli-ref-restore.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="fbbc1-316">Przywracanie właściwości</span><span class="sxs-lookup"><span data-stu-id="fbbc1-316">Restore properties</span></span>

<span data-ttu-id="fbbc1-317">Ustawienia dodatkowe przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="fbbc1-318">Ponadto można ustawić wartości z wiersza polecenia przy użyciu `/p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="fbbc1-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="fbbc1-319">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fbbc1-319">Property</span></span> | <span data-ttu-id="fbbc1-320">Opis</span><span class="sxs-lookup"><span data-stu-id="fbbc1-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="fbbc1-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="fbbc1-321">RestoreSources</span></span> | <span data-ttu-id="fbbc1-322">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="fbbc1-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="fbbc1-323">RestorePackagesPath</span></span> | <span data-ttu-id="fbbc1-324">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-324">User packages folder path.</span></span> |
| <span data-ttu-id="fbbc1-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="fbbc1-325">RestoreDisableParallel</span></span> | <span data-ttu-id="fbbc1-326">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="fbbc1-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="fbbc1-327">RestoreConfigFile</span></span> | <span data-ttu-id="fbbc1-328">Ścieżka do `Nuget.Config` pliku, aby zastosować.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="fbbc1-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="fbbc1-329">RestoreNoCache</span></span> | <span data-ttu-id="fbbc1-330">W przypadku wartości true umożliwia uniknięcie korzystania z pamięci podręcznej pakietów.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="fbbc1-331">Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fbbc1-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="fbbc1-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="fbbc1-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="fbbc1-333">W przypadku opcji true ignoruje awarie lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="fbbc1-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="fbbc1-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="fbbc1-335">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="fbbc1-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="fbbc1-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="fbbc1-337">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="fbbc1-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="fbbc1-338">RestoreOutputPath</span></span> | <span data-ttu-id="fbbc1-339">Folder wyjściowy, przyjęty `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="fbbc1-340">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fbbc1-340">Examples</span></span>

<span data-ttu-id="fbbc1-341">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="fbbc1-342">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="fbbc1-343">Przywracanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="fbbc1-343">Restore outputs</span></span>

<span data-ttu-id="fbbc1-344">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="fbbc1-345">Plik</span><span class="sxs-lookup"><span data-stu-id="fbbc1-345">File</span></span> | <span data-ttu-id="fbbc1-346">Opis</span><span class="sxs-lookup"><span data-stu-id="fbbc1-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="fbbc1-347">Zawiera wykres zależności dla wszystkich odwołań do pakietów.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="fbbc1-348">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="fbbc1-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="fbbc1-349">Odwołania do elementów docelowych MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="fbbc1-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="fbbc1-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="fbbc1-350">PackageTargetFallback</span></span>

<span data-ttu-id="fbbc1-351">`PackageTargetFallback` Element umożliwia określenie zestawu zgodnych elementów docelowych do użycia podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="fbbc1-352">Został zaprojektowany tak, aby zezwolić na pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklarują dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="fbbc1-353">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkich pakietów to zależy od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do swojego projektu, aby umożliwić-dotnet platform zapewnić ich zgodność za pomocą polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="fbbc1-354">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależnego pakietu zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projektu zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="fbbc1-355">Jeśli chcesz w ostatnim biblioteki DLL, wówczas można dodać `PackageTargetFallback` następujący powiedzieć, `portable-net45+win81` Biblioteka DLL jest niezgodny:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="fbbc1-356">Aby zadeklarować rezerwowe dla wszystkich obiektów docelowych w projekcie, należy pozostawić wyłączone `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="fbbc1-357">Można także rozszerzyć istniejące `PackageTargetFallback` umieszczając `$(PackageTargetFallback)` jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="fbbc1-358">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="fbbc1-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="fbbc1-359">Jeśli chodzi o przeniesienie zły zestaw przywracania, istnieje możliwość wykluczenia pakietów wybór domyślny i zamień ją na własną nazwę.</span><span class="sxs-lookup"><span data-stu-id="fbbc1-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="fbbc1-360">Najpierw z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="fbbc1-361">Następnie dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="fbbc1-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
