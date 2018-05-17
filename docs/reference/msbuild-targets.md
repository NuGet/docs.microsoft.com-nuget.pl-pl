---
title: Pakiet NuGet i przywracania jako docelowych elementów MSBuild
description: Pakiet NuGet i przywracania może współpracować bezpośrednio jako docelowych elementów MSBuild nuget 4.0 +.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 00d763bcfdd2f3db50378a1e7774eae7a2e1fcd1
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="8fb54-103">Pakiet NuGet i przywracania jako docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="8fb54-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="8fb54-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="8fb54-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="8fb54-105">W formacie PackageReference NuGet 4.0 + mogą przechowywać wszystkie manifestu metadanych bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="8fb54-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="8fb54-106">Przy użyciu programu MSBuild 15.1 +, NuGet jest również najwyższej jakości obywateli MSBuild z `pack` i `restore` celem zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="8fb54-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="8fb54-107">Następujących elementów docelowych umożliwiają pracę z programem NuGet, tak jak inne zadanie programu MSBuild lub docelowego.</span><span class="sxs-lookup"><span data-stu-id="8fb54-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="8fb54-108">(Programu NuGet 3.x i wcześniej, użyj [pakietu](../tools/cli-ref-pack.md) i [przywrócić](../tools/cli-ref-restore.md) zamiast tego polecenia za pomocą interfejsu wiersza polecenia NuGet.)</span><span class="sxs-lookup"><span data-stu-id="8fb54-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="8fb54-109">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="8fb54-109">Target build order</span></span>

<span data-ttu-id="8fb54-110">Ponieważ `pack` i `restore` MSBuild elementów docelowych, można wywołać w celu zwiększenia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="8fb54-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="8fb54-111">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po spakowaniu go.</span><span class="sxs-lookup"><span data-stu-id="8fb54-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="8fb54-112">Możesz to zrobić przez dodanie poniższego w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="8fb54-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="8fb54-113">Podobnie można zapisać zadania programu MSBuild, napisać własny docelowych i korzystać z właściwości NuGet w zadanie programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8fb54-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="8fb54-114">docelowy pakiet</span><span class="sxs-lookup"><span data-stu-id="8fb54-114">pack target</span></span>

<span data-ttu-id="8fb54-115">Dla platformy .NET Standard projektów przy użyciu formatu PackageReference, używając `msbuild /t:pack` pobiera dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="8fb54-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="8fb54-116">W poniższej tabeli opisano właściwości programu MSBuild, które mogą zostać dodane do pliku projektu w pierwszym `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="8fb54-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="8fb54-117">Wprowadź te zmiany łatwe w Visual Studio 2017 i później przez kliknięcie prawym przyciskiem myszy projekt i wybierając **edytować {nazwa_projektu}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="8fb54-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="8fb54-118">Dla wygody tabeli jest zorganizowana według równoważne właściwości w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="8fb54-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="8fb54-119">Należy pamiętać, że `Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane przy użyciu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8fb54-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="8fb54-120">Wartość atrybutu/NuSpec.</span><span class="sxs-lookup"><span data-stu-id="8fb54-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="8fb54-121">Właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="8fb54-121">MSBuild Property</span></span> | <span data-ttu-id="8fb54-122">Domyślny</span><span class="sxs-lookup"><span data-stu-id="8fb54-122">Default</span></span> | <span data-ttu-id="8fb54-123">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8fb54-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="8fb54-124">Id</span><span class="sxs-lookup"><span data-stu-id="8fb54-124">Id</span></span> | <span data-ttu-id="8fb54-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="8fb54-125">PackageId</span></span> | <span data-ttu-id="8fb54-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="8fb54-126">AssemblyName</span></span> | <span data-ttu-id="8fb54-127">$(AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="8fb54-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="8fb54-128">Wersja</span><span class="sxs-lookup"><span data-stu-id="8fb54-128">Version</span></span> | <span data-ttu-id="8fb54-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="8fb54-129">PackageVersion</span></span> | <span data-ttu-id="8fb54-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="8fb54-130">Version</span></span> | <span data-ttu-id="8fb54-131">Jest to zgodne, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345" programu semver</span><span class="sxs-lookup"><span data-stu-id="8fb54-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="8fb54-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="8fb54-132">VersionPrefix</span></span> | <span data-ttu-id="8fb54-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="8fb54-133">PackageVersionPrefix</span></span> | <span data-ttu-id="8fb54-134">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-134">empty</span></span> | <span data-ttu-id="8fb54-135">Ustawienie PackageVersion zastępuje PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="8fb54-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="8fb54-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="8fb54-136">VersionSuffix</span></span> | <span data-ttu-id="8fb54-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="8fb54-137">PackageVersionSuffix</span></span> | <span data-ttu-id="8fb54-138">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-138">empty</span></span> | <span data-ttu-id="8fb54-139">$(VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8fb54-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="8fb54-140">Ustawienie PackageVersion zastępuje PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="8fb54-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="8fb54-141">Autorzy</span><span class="sxs-lookup"><span data-stu-id="8fb54-141">Authors</span></span> | <span data-ttu-id="8fb54-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="8fb54-142">Authors</span></span> | <span data-ttu-id="8fb54-143">Nazwa bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="8fb54-143">Username of the current user</span></span> | |
| <span data-ttu-id="8fb54-144">Właściciele</span><span class="sxs-lookup"><span data-stu-id="8fb54-144">Owners</span></span> | <span data-ttu-id="8fb54-145">Brak</span><span class="sxs-lookup"><span data-stu-id="8fb54-145">N/A</span></span> | <span data-ttu-id="8fb54-146">Nie istnieje w pliku NuSpec</span><span class="sxs-lookup"><span data-stu-id="8fb54-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="8fb54-147">Tytuł</span><span class="sxs-lookup"><span data-stu-id="8fb54-147">Title</span></span> | <span data-ttu-id="8fb54-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="8fb54-148">Title</span></span> | <span data-ttu-id="8fb54-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="8fb54-149">The PackageId</span></span>| |
| <span data-ttu-id="8fb54-150">Opis</span><span class="sxs-lookup"><span data-stu-id="8fb54-150">Description</span></span> | <span data-ttu-id="8fb54-151">Opis</span><span class="sxs-lookup"><span data-stu-id="8fb54-151">Description</span></span> | <span data-ttu-id="8fb54-152">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="8fb54-152">"Package Description"</span></span> | |
| <span data-ttu-id="8fb54-153">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="8fb54-153">Copyright</span></span> | <span data-ttu-id="8fb54-154">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="8fb54-154">Copyright</span></span> | <span data-ttu-id="8fb54-155">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-155">empty</span></span> | |
| <span data-ttu-id="8fb54-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="8fb54-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="8fb54-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="8fb54-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="8fb54-158">false</span><span class="sxs-lookup"><span data-stu-id="8fb54-158">false</span></span> | |
| <span data-ttu-id="8fb54-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-159">LicenseUrl</span></span> | <span data-ttu-id="8fb54-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-160">PackageLicenseUrl</span></span> | <span data-ttu-id="8fb54-161">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-161">empty</span></span> | |
| <span data-ttu-id="8fb54-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-162">ProjectUrl</span></span> | <span data-ttu-id="8fb54-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-163">PackageProjectUrl</span></span> | <span data-ttu-id="8fb54-164">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-164">empty</span></span> | |
| <span data-ttu-id="8fb54-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-165">IconUrl</span></span> | <span data-ttu-id="8fb54-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-166">PackageIconUrl</span></span> | <span data-ttu-id="8fb54-167">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-167">empty</span></span> | |
| <span data-ttu-id="8fb54-168">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="8fb54-168">Tags</span></span> | <span data-ttu-id="8fb54-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="8fb54-169">PackageTags</span></span> | <span data-ttu-id="8fb54-170">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-170">empty</span></span> | <span data-ttu-id="8fb54-171">Tagi są rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="8fb54-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="8fb54-172">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="8fb54-172">ReleaseNotes</span></span> | <span data-ttu-id="8fb54-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="8fb54-173">PackageReleaseNotes</span></span> | <span data-ttu-id="8fb54-174">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-174">empty</span></span> | |
| <span data-ttu-id="8fb54-175">Adres Url i repozytorium</span><span class="sxs-lookup"><span data-stu-id="8fb54-175">Repository/Url</span></span> | <span data-ttu-id="8fb54-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-176">RepositoryUrl</span></span> | <span data-ttu-id="8fb54-177">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-177">empty</span></span> | <span data-ttu-id="8fb54-178">Adres URL repozytorium jest używany do klonowania lub pobrać kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="8fb54-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="8fb54-179">Przykład: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="8fb54-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="8fb54-180">Repozytorium/typ</span><span class="sxs-lookup"><span data-stu-id="8fb54-180">Repository/Type</span></span> | <span data-ttu-id="8fb54-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="8fb54-181">RepositoryType</span></span> | <span data-ttu-id="8fb54-182">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-182">empty</span></span> | <span data-ttu-id="8fb54-183">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="8fb54-183">Repository type.</span></span> <span data-ttu-id="8fb54-184">Przykłady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="8fb54-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="8fb54-185">Repozytorium/gałęzi</span><span class="sxs-lookup"><span data-stu-id="8fb54-185">Repository/Branch</span></span> | <span data-ttu-id="8fb54-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="8fb54-186">RepositoryBranch</span></span> | <span data-ttu-id="8fb54-187">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-187">empty</span></span> | <span data-ttu-id="8fb54-188">Informacje o gałęzi repozytorium opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="8fb54-188">Optional repository branch information.</span></span> <span data-ttu-id="8fb54-189">*RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="8fb54-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="8fb54-190">Przykład: *wzorca* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="8fb54-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="8fb54-191">Repozytorium/zatwierdzeniu</span><span class="sxs-lookup"><span data-stu-id="8fb54-191">Repository/Commit</span></span> | <span data-ttu-id="8fb54-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="8fb54-192">RepositoryCommit</span></span> | <span data-ttu-id="8fb54-193">empty</span><span class="sxs-lookup"><span data-stu-id="8fb54-193">empty</span></span> | <span data-ttu-id="8fb54-194">Opcjonalne repozytorium zatwierdzania lub zestaw zmian, aby wskazać, który źródła pakietu został skompilowany przy.</span><span class="sxs-lookup"><span data-stu-id="8fb54-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="8fb54-195">*RepositoryUrl* musi być także określona dla tej właściwości, które zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="8fb54-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="8fb54-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="8fb54-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="8fb54-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="8fb54-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="8fb54-198">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="8fb54-198">Summary</span></span> | <span data-ttu-id="8fb54-199">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="8fb54-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="8fb54-200">dane wejściowe docelowego pakietu</span><span class="sxs-lookup"><span data-stu-id="8fb54-200">pack target inputs</span></span>

- <span data-ttu-id="8fb54-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="8fb54-201">IsPackable</span></span>
- <span data-ttu-id="8fb54-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="8fb54-202">PackageVersion</span></span>
- <span data-ttu-id="8fb54-203">PackageId</span><span class="sxs-lookup"><span data-stu-id="8fb54-203">PackageId</span></span>
- <span data-ttu-id="8fb54-204">Autorzy</span><span class="sxs-lookup"><span data-stu-id="8fb54-204">Authors</span></span>
- <span data-ttu-id="8fb54-205">Opis</span><span class="sxs-lookup"><span data-stu-id="8fb54-205">Description</span></span>
- <span data-ttu-id="8fb54-206">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="8fb54-206">Copyright</span></span>
- <span data-ttu-id="8fb54-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="8fb54-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="8fb54-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="8fb54-208">DevelopmentDependency</span></span>
- <span data-ttu-id="8fb54-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="8fb54-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-210">PackageProjectUrl</span></span>
- <span data-ttu-id="8fb54-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-211">PackageIconUrl</span></span>
- <span data-ttu-id="8fb54-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="8fb54-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="8fb54-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="8fb54-213">PackageTags</span></span>
- <span data-ttu-id="8fb54-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="8fb54-214">PackageOutputPath</span></span>
- <span data-ttu-id="8fb54-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="8fb54-215">IncludeSymbols</span></span>
- <span data-ttu-id="8fb54-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="8fb54-216">IncludeSource</span></span>
- <span data-ttu-id="8fb54-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="8fb54-217">PackageTypes</span></span>
- <span data-ttu-id="8fb54-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="8fb54-218">IsTool</span></span>
- <span data-ttu-id="8fb54-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-219">RepositoryUrl</span></span>
- <span data-ttu-id="8fb54-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="8fb54-220">RepositoryType</span></span>
- <span data-ttu-id="8fb54-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="8fb54-221">RepositoryBranch</span></span>
- <span data-ttu-id="8fb54-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="8fb54-222">RepositoryCommit</span></span>
- <span data-ttu-id="8fb54-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="8fb54-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="8fb54-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="8fb54-224">MinClientVersion</span></span>
- <span data-ttu-id="8fb54-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="8fb54-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="8fb54-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="8fb54-226">IncludeContentInPack</span></span>
- <span data-ttu-id="8fb54-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="8fb54-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="8fb54-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="8fb54-228">ContentTargetFolders</span></span>
- <span data-ttu-id="8fb54-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="8fb54-229">NuspecFile</span></span>
- <span data-ttu-id="8fb54-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="8fb54-230">NuspecBasePath</span></span>
- <span data-ttu-id="8fb54-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="8fb54-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="8fb54-232">scenariusze z dodatkiem Service Pack</span><span class="sxs-lookup"><span data-stu-id="8fb54-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="8fb54-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="8fb54-233">PackageIconUrl</span></span>

<span data-ttu-id="8fb54-234">Zmiana w ramach [352 problem NuGet](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` po pewnym czasie zostaną zmienione na `PackageIconUri` i może być względna ścieżka do pliku ikony, które zostaną uwzględnione w katalogu głównym wynikowy pakiet.</span><span class="sxs-lookup"><span data-stu-id="8fb54-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="8fb54-235">Zestawy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="8fb54-235">Output assemblies</span></span>

<span data-ttu-id="8fb54-236">`nuget pack` kopiuje dane wyjściowe pliki z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="8fb54-237">Pliki wyjściowe, które są kopiowane są zależne od MSBuild zapewnia z `BuiltOutputProjectGroup` docelowej.</span><span class="sxs-lookup"><span data-stu-id="8fb54-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="8fb54-238">Istnieją dwie właściwości programu MSBuild, które są dostępne w pliku projektu lub wiersza polecenia w celu sterowania gdzie zestawy danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="8fb54-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="8fb54-239">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji mają być uwzględniane w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="8fb54-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="8fb54-240">`BuildOutputTargetFolder`: Określa folder, w którym ma zostać umieszczony zestawy danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8fb54-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="8fb54-241">Zestawy danych wyjściowych (i inne pliki wyjściowe) są kopiowane do ich odpowiednich framework folderów.</span><span class="sxs-lookup"><span data-stu-id="8fb54-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="8fb54-242">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="8fb54-242">Package references</span></span>

<span data-ttu-id="8fb54-243">Zobacz [pakietu odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="8fb54-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="8fb54-244">Projekt do odwołań projektu</span><span class="sxs-lookup"><span data-stu-id="8fb54-244">Project to project references</span></span>

<span data-ttu-id="8fb54-245">Projekt do odwołań projektu są traktowane jako domyślnie jako odwołania do pakietu nuget, na przykład:</span><span class="sxs-lookup"><span data-stu-id="8fb54-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="8fb54-246">Można również dodać następujące metadane odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="8fb54-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="8fb54-247">W tym zawartości w pakiecie</span><span class="sxs-lookup"><span data-stu-id="8fb54-247">Including content in a package</span></span>

<span data-ttu-id="8fb54-248">Aby uwzględnić zawartość, należy dodać dodatkowe metadane do istniejącej `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="8fb54-249">Domyślnie wszystkie elementy typu "Zawartość" pobiera uwzględniony w pakiecie chyba że nadpiszesz zapisami jak następujące:</span><span class="sxs-lookup"><span data-stu-id="8fb54-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="8fb54-250">Domyślnie pobiera wszystkie elementy dodane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje struktury folder względny, o ile nie zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="8fb54-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="8fb54-251">Jeśli chcesz skopiować wszystkie zawartość tylko z określonym główny folderów (zamiast `content` i `contentFiles` oba), można użyć właściwości programu MSBuild `ContentTargetFolders`, jakie nie "zawartość; pliki", ale może być ustawiony na inne nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="8fb54-252">Należy pamiętać, że po prostu określenie "pliki" w `ContentTargetFolders` umieszcza pliki objęte `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="8fb54-253">`PackagePath` może być rozdzielone średnikami zbiór ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="8fb54-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="8fb54-254">Określenie ścieżki pusty pakietu dodać plik w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="8fb54-255">Na przykład dodaje następujące `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="8fb54-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="8fb54-256">Istnieje również właściwość MSBuild `$(IncludeContentInPack)`, jakie nie `true`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="8fb54-257">Jeśli ta wartość jest równa `false` w żadnym projekcie następnie zawartość z tego projektu nie znajdują się w pakiecie nuget.</span><span class="sxs-lookup"><span data-stu-id="8fb54-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="8fb54-258">Zawiera inne metadane określonego pakietu, które można ustawić na żadnym z powyższych elementów ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` który określa ```CopyToOutput``` i ```Flatten``` wartości na ```contentFiles``` wpisu w pliku nuspec danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8fb54-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="8fb54-259">Oprócz elementy zawartości `<Pack>` i `<PackagePath>` metadanych można również ustawić na pliki z akcją kompilacji w kompilacji, EmbeddedResource, ApplicationDefinition, strony, zasobów, ekranu powitalnego, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="8fb54-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="8fb54-260">Pakiet można dołączyć nazwę pliku do ścieżki pakietu przy użyciu globbing wzorców ścieżka do pakietu musi być zakończona z folderu znak separatora, w przeciwnym razie Ścieżka pakietu jest traktowana jako pełna ścieżka, łącznie z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="8fb54-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="8fb54-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="8fb54-261">IncludeSymbols</span></span>

<span data-ttu-id="8fb54-262">Korzystając z `MSBuild /t:pack /p:IncludeSymbols=true`, odpowiadającego `.pdb` pliki są kopiowane oraz inne pliki wyjściowe (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="8fb54-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="8fb54-263">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy pakiet regularne *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="8fb54-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="8fb54-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="8fb54-264">IncludeSource</span></span>

<span data-ttu-id="8fb54-265">To jest taka sama jak `IncludeSymbols`, ale kopiuje pliki źródłowe wraz z programem `.pdb` również pliki.</span><span class="sxs-lookup"><span data-stu-id="8fb54-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="8fb54-266">Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowaniem struktury folderów ścieżkę względną w pakiecie wynikowy.</span><span class="sxs-lookup"><span data-stu-id="8fb54-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="8fb54-267">W tym celu również dla plików źródłowych dowolnego `ProjectReference` mającego `TreatAsPackageReference` ustawioną `false`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="8fb54-268">Jeśli plik typu skompilować, znajduje się poza folderu projektu, a następnie wystarczy dodać go do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="8fb54-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="8fb54-269">IsTool</span></span>

<span data-ttu-id="8fb54-270">Korzystając z `MSBuild /t:pack /p:IsTool=true`, wszystkie dane wyjściowe pliki, jak określono w [zestawy danych wyjściowych](#output-assemblies) scenariusza, są kopiowane do `tools` folder zamiast `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="8fb54-271">Należy pamiętać, że jest inny niż `DotNetCliTool` który jest określany przez ustawienie `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="8fb54-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="8fb54-272">Przy użyciu .nuspec pakowania</span><span class="sxs-lookup"><span data-stu-id="8fb54-272">Packing using a .nuspec</span></span>

<span data-ttu-id="8fb54-273">Można użyć `.nuspec` plik można spakować projektu, pod warunkiem, że masz SDK plik projektu do zaimportowania `NuGet.Build.Tasks.Pack.targets` , dzięki czemu mogą być wykonywane zadanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="8fb54-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="8fb54-274">Nadal potrzebujesz przywrócić projekt przed można pliku nuspec.</span><span class="sxs-lookup"><span data-stu-id="8fb54-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="8fb54-275">Platforma docelowa pliku projektu nie ma znaczenia, a nie używany podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="8fb54-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="8fb54-276">Następujące trzy właściwości programu MSBuild mają zastosowanie do pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="8fb54-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="8fb54-277">`NuspecFile`: ścieżka względna lub bezwzględna do `.nuspec` pliku używany na potrzeby pakowania.</span><span class="sxs-lookup"><span data-stu-id="8fb54-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="8fb54-278">`NuspecProperties`: Rozdzielana średnikami lista klucz = pary wartości.</span><span class="sxs-lookup"><span data-stu-id="8fb54-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="8fb54-279">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild, wiele właściwości musi być następujący: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="8fb54-280">`NuspecBasePath`: Ścieżki podstawowa dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="8fb54-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="8fb54-281">Jeśli przy użyciu `dotnet.exe` pakowania projektu, użyj polecenia podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="8fb54-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="8fb54-282">Jeśli pakiet projektu za pomocą programu MSBuild, należy użyć polecenia podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="8fb54-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="8fb54-283">Należy pamiętać, pakowanie nuspec przy użyciu dotnet.exe lub msbuild również prowadzi do tworzenia projektu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="8fb54-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="8fb54-284">Można tego uniknąć przez przekazanie ```--no-build``` dotnet.exe, który jest odpowiednikiem ustawienie dla właściwości ```<NoBuild>true</NoBuild> ``` w pliku projektu oraz ustawienie ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="8fb54-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="8fb54-285">Przykładowy plik csproj, można spakować plik nuspec to:</span><span class="sxs-lookup"><span data-stu-id="8fb54-285">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="8fb54-286">Zaawansowane punktów rozszerzenia, aby utworzyć dostosowany pakiet</span><span class="sxs-lookup"><span data-stu-id="8fb54-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="8fb54-287">`pack` Docelowy zawiera dwa punkty rozszerzeń uruchamianych w wewnętrznej, określonej kompilacji framework docelowej.</span><span class="sxs-lookup"><span data-stu-id="8fb54-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="8fb54-288">Punkty rozszerzenia pomocy technicznej oraz docelowego framework określone zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="8fb54-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="8fb54-289">`TargetsForTfmSpecificBuildOutput` docelowy: pliki znajdujące się na użytek `lib` folder lub folder, określić przy użyciu `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="8fb54-290">`TargetsForTfmSpecificContentInPackage` docelowy: Użyj dla plików znajdujących się poza `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="8fb54-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="8fb54-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="8fb54-292">Zapisz niestandardowe docelowych i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="8fb54-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="8fb54-293">Pliki, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), element docelowy należy zapisać te pliki do ItemGroup `BuildOutputInPackage` i ustaw następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="8fb54-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="8fb54-294">`FinalOutputPath`: Ścieżka bezwzględna plików; Jeśli nie podano tożsamości jest używane do analizowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="8fb54-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="8fb54-295">`TargetPath`: (Opcjonalnie) ustawić, gdy trzeba przejdź do podfolderu w pliku `lib\<TargetFramework>` , takie jak towarzyszącej zestawy tego Przejdź w folderach ich odpowiednich kultury.</span><span class="sxs-lookup"><span data-stu-id="8fb54-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="8fb54-296">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="8fb54-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="8fb54-297">Przykład:</span><span class="sxs-lookup"><span data-stu-id="8fb54-297">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="8fb54-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="8fb54-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="8fb54-299">Zapisz niestandardowe docelowych i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="8fb54-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="8fb54-300">W przypadku plików do uwzględnienia w pakiecie docelowy należy zapisać te pliki do ItemGroup `TfmSpecificPackageFile` i ustaw następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="8fb54-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="8fb54-301">`PackagePath`: Ścieżka, gdy ten plik powinien być dane wyjściowe w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="8fb54-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="8fb54-302">NuGet wygeneruje ostrzeżenie, jeśli więcej niż jeden plik został dodany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="8fb54-303">`BuildAction`: Akcja kompilacji do przypisania do plików, jest wymagany tylko wtedy, jeśli ścieżka pakietu znajduje się w `contentFiles` folderu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="8fb54-304">Wartość domyślna to "None".</span><span class="sxs-lookup"><span data-stu-id="8fb54-304">Defaults to "None".</span></span>

<span data-ttu-id="8fb54-305">Przykład:</span><span class="sxs-lookup"><span data-stu-id="8fb54-305">An example:</span></span>
```xml
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

## <a name="restore-target"></a><span data-ttu-id="8fb54-306">Lokalizacja docelowa przywracania</span><span class="sxs-lookup"><span data-stu-id="8fb54-306">restore target</span></span>

<span data-ttu-id="8fb54-307">`MSBuild /t:restore` (który `nuget restore` i `dotnet restore` za pomocą platformy .NET Core projektów), przywraca pakietów, do których odwołuje się w pliku projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8fb54-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="8fb54-308">Przeczytaj wszystkich odwołań do projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="8fb54-308">Read all project to project references</span></span>
1. <span data-ttu-id="8fb54-309">Właściwości projektu, aby znaleźć pośredniego struktury folderów i obiekt docelowy do odczytu</span><span class="sxs-lookup"><span data-stu-id="8fb54-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="8fb54-310">Przekazywanie danych msbuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="8fb54-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="8fb54-311">Uruchamianie przywracania</span><span class="sxs-lookup"><span data-stu-id="8fb54-311">Run restore</span></span>
1. <span data-ttu-id="8fb54-312">Pobieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="8fb54-312">Download packages</span></span>
1. <span data-ttu-id="8fb54-313">Zapis plików zasobów, cele i właściwości</span><span class="sxs-lookup"><span data-stu-id="8fb54-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="8fb54-314">`restore` Docelowy działa **tylko** dla projektów w formacie PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8fb54-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="8fb54-315">Robi **nie** pracy dla projektów przy użyciu `packages.config` sformatować; użyj [Przywracanie nuget](../tools/cli-ref-restore.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="8fb54-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="8fb54-316">Przywróć właściwości</span><span class="sxs-lookup"><span data-stu-id="8fb54-316">Restore properties</span></span>

<span data-ttu-id="8fb54-317">Przywróć dodatkowe ustawienia mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="8fb54-318">Można również ustawić wartości z wiersza polecenia przy użyciu `/p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="8fb54-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="8fb54-319">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8fb54-319">Property</span></span> | <span data-ttu-id="8fb54-320">Opis</span><span class="sxs-lookup"><span data-stu-id="8fb54-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="8fb54-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="8fb54-321">RestoreSources</span></span> | <span data-ttu-id="8fb54-322">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="8fb54-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="8fb54-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="8fb54-323">RestorePackagesPath</span></span> | <span data-ttu-id="8fb54-324">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8fb54-324">User packages folder path.</span></span> |
| <span data-ttu-id="8fb54-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="8fb54-325">RestoreDisableParallel</span></span> | <span data-ttu-id="8fb54-326">Limit pobiera pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="8fb54-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="8fb54-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="8fb54-327">RestoreConfigFile</span></span> | <span data-ttu-id="8fb54-328">Ścieżka do `Nuget.Config` pliku w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="8fb54-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="8fb54-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="8fb54-329">RestoreNoCache</span></span> | <span data-ttu-id="8fb54-330">Jeśli PRAWDA, pozwala uniknąć za pomocą pakietów pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="8fb54-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="8fb54-331">Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="8fb54-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="8fb54-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="8fb54-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="8fb54-333">Jeśli PRAWDA, ignoruje wystąpił błąd lub Brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="8fb54-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="8fb54-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="8fb54-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="8fb54-335">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="8fb54-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="8fb54-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="8fb54-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="8fb54-337">Rozdzielana średnikami lista projektów do przywrócenia, powinna ona zawierać ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="8fb54-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="8fb54-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="8fb54-338">RestoreOutputPath</span></span> | <span data-ttu-id="8fb54-339">Folder wyjściowy, przyjęty `obj` folderu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="8fb54-340">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8fb54-340">Examples</span></span>

<span data-ttu-id="8fb54-341">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="8fb54-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="8fb54-342">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="8fb54-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="8fb54-343">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="8fb54-343">Restore outputs</span></span>

<span data-ttu-id="8fb54-344">Przywracanie tworzy następujące pliki w kompilacji `obj` folderu:</span><span class="sxs-lookup"><span data-stu-id="8fb54-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="8fb54-345">Plik</span><span class="sxs-lookup"><span data-stu-id="8fb54-345">File</span></span> | <span data-ttu-id="8fb54-346">Opis</span><span class="sxs-lookup"><span data-stu-id="8fb54-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="8fb54-347">Zawiera wykres zależności wszystkie odwołania do pakietu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="8fb54-348">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="8fb54-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="8fb54-349">Odwołania do zawartych w pakietach docelowych elementów MSBuild</span><span class="sxs-lookup"><span data-stu-id="8fb54-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="8fb54-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="8fb54-350">PackageTargetFallback</span></span>

<span data-ttu-id="8fb54-351">`PackageTargetFallback` Element służy do określenia zestawu zgodne cele, które mają być użyte podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="8fb54-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="8fb54-352">Został zaprojektowany tak, aby umożliwić pakiety, które używają dotnet [TxM](../reference/target-frameworks.md) do pracy z pakietami zgodne, które nie deklaruje dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="8fb54-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="8fb54-353">Oznacza to, jeśli projekt używa dotnet TxM, następnie wszystkie pakiety zależy on od musi również mieć dotnet TxM, chyba że dodasz `<PackageTargetFallback>` do projektu, aby umożliwić platformy dotnet z systemem innym niż był zgodny z dotnet.</span><span class="sxs-lookup"><span data-stu-id="8fb54-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="8fb54-354">Na przykład, jeśli projekt używa `netstandard1.6` TxM i zależny pakiet zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, projekt zakończy się niepowodzeniem do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8fb54-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="8fb54-355">Jeśli chcesz przenieść jest ostatnim biblioteki DLL, a następnie można dodać `PackageTargetFallback` w następujący sposób, aby oznacza, że `portable-net45+win81` zgodnego biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="8fb54-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="8fb54-356">Aby zadeklarować używane dla wszystkich elementów docelowych w projekcie, pozostaw `Condition` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="8fb54-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="8fb54-357">Można również rozszerzyć zasięg wszelkie istniejące `PackageTargetFallback` przez dołączenie `$(PackageTargetFallback)` w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="8fb54-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="8fb54-358">Zastępowanie jedną bibliotekę z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="8fb54-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="8fb54-359">Jeśli przywracania jest Przywracanie nieprawidłowy zestaw, jest możliwe do wykluczenia z pakietów domyślny wybór i zamień ją na dowolny inny.</span><span class="sxs-lookup"><span data-stu-id="8fb54-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="8fb54-360">Pierwszy z najwyższym poziomie `PackageReference`, wykluczyć wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="8fb54-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="8fb54-361">Następnie dodaj własne odwołanie do odpowiedniego lokalną kopię pliku DLL:</span><span class="sxs-lookup"><span data-stu-id="8fb54-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
