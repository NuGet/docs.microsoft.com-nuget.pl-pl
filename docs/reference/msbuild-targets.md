---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą współpracować bezpośrednio z obiektami docelowymi programu MSBuild z pakietem NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8403ae38b5d2e907c6f06b162a18cdcd5425565b
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817521"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="bec81-103">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="bec81-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="bec81-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="bec81-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="bec81-105">W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) program NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="bec81-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="bec81-106">Dzięki programowi MSBuild 15.1 + pakiet NuGet jest również pierwszym klasą obywatela programu `pack` MSBuild `restore` z obiektami docelowymi, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="bec81-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="bec81-107">Te elementy docelowe umożliwiają współdziałanie z pakietem NuGet, podobnie jak w przypadku każdego innego zadania lub celu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bec81-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="bec81-108">Aby uzyskać instrukcje tworzenia pakietu NuGet przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="bec81-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="bec81-109">(W przypadku programu NuGet 3. x i starszych należy użyć poleceń [pakiet](../reference/cli-reference/cli-ref-pack.md) i [Przywróć](../reference/cli-reference/cli-ref-restore.md) zamiast tego w interfejsie wiersza polecenia NuGet).</span><span class="sxs-lookup"><span data-stu-id="bec81-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="bec81-110">Docelowy porządek kompilacji</span><span class="sxs-lookup"><span data-stu-id="bec81-110">Target build order</span></span>

<span data-ttu-id="bec81-111">Ponieważ `pack` i`restore` są obiektami docelowymi programu MSBuild, możesz uzyskać do nich dostęp, aby usprawnić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="bec81-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="bec81-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu.</span><span class="sxs-lookup"><span data-stu-id="bec81-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="bec81-113">Można to zrobić, dodając następujący plik w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="bec81-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="bec81-114">Podobnie można napisać zadanie programu MSBuild, napisać własne miejsce docelowe i korzystać z właściwości NuGet w zadaniu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bec81-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="bec81-115">cel pakietu</span><span class="sxs-lookup"><span data-stu-id="bec81-115">pack target</span></span>

<span data-ttu-id="bec81-116">W przypadku projektów .NET standard przy użyciu formatu PackageReference użycie `msbuild -t:pack` narzędzi pobiera dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="bec81-116">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="bec81-117">W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle.</span><span class="sxs-lookup"><span data-stu-id="bec81-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="bec81-118">Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="bec81-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="bec81-119">Dla wygody tabela jest zorganizowana przez równoważną właściwość w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="bec81-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="bec81-120">Należy zauważyć, `Owners` że `Summary` właściwości i `.nuspec` z nie są obsługiwane w programie MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bec81-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="bec81-121">Wartość atrybutu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="bec81-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="bec81-122">Właściwość programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="bec81-122">MSBuild Property</span></span> | <span data-ttu-id="bec81-123">Domyślny</span><span class="sxs-lookup"><span data-stu-id="bec81-123">Default</span></span> | <span data-ttu-id="bec81-124">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bec81-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="bec81-125">Id</span><span class="sxs-lookup"><span data-stu-id="bec81-125">Id</span></span> | <span data-ttu-id="bec81-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="bec81-126">PackageId</span></span> | <span data-ttu-id="bec81-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="bec81-127">AssemblyName</span></span> | <span data-ttu-id="bec81-128">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="bec81-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="bec81-129">Wersja</span><span class="sxs-lookup"><span data-stu-id="bec81-129">Version</span></span> | <span data-ttu-id="bec81-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="bec81-130">PackageVersion</span></span> | <span data-ttu-id="bec81-131">Wersja</span><span class="sxs-lookup"><span data-stu-id="bec81-131">Version</span></span> | <span data-ttu-id="bec81-132">Jest to zgodne z semver, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="bec81-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="bec81-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="bec81-133">VersionPrefix</span></span> | <span data-ttu-id="bec81-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="bec81-134">PackageVersionPrefix</span></span> | <span data-ttu-id="bec81-135">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-135">empty</span></span> | <span data-ttu-id="bec81-136">Ustawienie PackageVersion zastępowanie PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="bec81-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="bec81-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="bec81-137">VersionSuffix</span></span> | <span data-ttu-id="bec81-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="bec81-138">PackageVersionSuffix</span></span> | <span data-ttu-id="bec81-139">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-139">empty</span></span> | <span data-ttu-id="bec81-140">$ (VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bec81-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="bec81-141">Ustawienie PackageVersion zastępowanie PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="bec81-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="bec81-142">Autorzy</span><span class="sxs-lookup"><span data-stu-id="bec81-142">Authors</span></span> | <span data-ttu-id="bec81-143">Autorzy</span><span class="sxs-lookup"><span data-stu-id="bec81-143">Authors</span></span> | <span data-ttu-id="bec81-144">Nazwa_użytkownika bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="bec81-144">Username of the current user</span></span> | |
| <span data-ttu-id="bec81-145">Rzecz</span><span class="sxs-lookup"><span data-stu-id="bec81-145">Owners</span></span> | <span data-ttu-id="bec81-146">Brak</span><span class="sxs-lookup"><span data-stu-id="bec81-146">N/A</span></span> | <span data-ttu-id="bec81-147">Nieobecny w NuSpec</span><span class="sxs-lookup"><span data-stu-id="bec81-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="bec81-148">Tytuł</span><span class="sxs-lookup"><span data-stu-id="bec81-148">Title</span></span> | <span data-ttu-id="bec81-149">Tytuł</span><span class="sxs-lookup"><span data-stu-id="bec81-149">Title</span></span> | <span data-ttu-id="bec81-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="bec81-150">The PackageId</span></span>| |
| <span data-ttu-id="bec81-151">Opis</span><span class="sxs-lookup"><span data-stu-id="bec81-151">Description</span></span> | <span data-ttu-id="bec81-152">Opis</span><span class="sxs-lookup"><span data-stu-id="bec81-152">Description</span></span> | <span data-ttu-id="bec81-153">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="bec81-153">"Package Description"</span></span> | |
| <span data-ttu-id="bec81-154">Prawo</span><span class="sxs-lookup"><span data-stu-id="bec81-154">Copyright</span></span> | <span data-ttu-id="bec81-155">Prawo</span><span class="sxs-lookup"><span data-stu-id="bec81-155">Copyright</span></span> | <span data-ttu-id="bec81-156">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-156">empty</span></span> | |
| <span data-ttu-id="bec81-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="bec81-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="bec81-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="bec81-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="bec81-159">false</span><span class="sxs-lookup"><span data-stu-id="bec81-159">false</span></span> | |
| <span data-ttu-id="bec81-160">licencjonowan</span><span class="sxs-lookup"><span data-stu-id="bec81-160">license</span></span> | <span data-ttu-id="bec81-161">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="bec81-161">PackageLicenseExpression</span></span> | <span data-ttu-id="bec81-162">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-162">empty</span></span> | <span data-ttu-id="bec81-163">Odnosi się do`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="bec81-163">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="bec81-164">licencjonowan</span><span class="sxs-lookup"><span data-stu-id="bec81-164">license</span></span> | <span data-ttu-id="bec81-165">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="bec81-165">PackageLicenseFile</span></span> | <span data-ttu-id="bec81-166">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-166">empty</span></span> | <span data-ttu-id="bec81-167">Odnosi się `<license type="file">`do.</span><span class="sxs-lookup"><span data-stu-id="bec81-167">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="bec81-168">Może być konieczne jawne spakowanie pliku licencji, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="bec81-168">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="bec81-169">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-169">LicenseUrl</span></span> | <span data-ttu-id="bec81-170">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-170">PackageLicenseUrl</span></span> | <span data-ttu-id="bec81-171">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-171">empty</span></span> | <span data-ttu-id="bec81-172">`licenseUrl`jest przestarzały, użyj właściwości PackageLicenseExpression lub PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="bec81-172">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="bec81-173">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-173">ProjectUrl</span></span> | <span data-ttu-id="bec81-174">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-174">PackageProjectUrl</span></span> | <span data-ttu-id="bec81-175">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-175">empty</span></span> | |
| <span data-ttu-id="bec81-176">IconUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-176">IconUrl</span></span> | <span data-ttu-id="bec81-177">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-177">PackageIconUrl</span></span> | <span data-ttu-id="bec81-178">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-178">empty</span></span> | |
| <span data-ttu-id="bec81-179">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="bec81-179">Tags</span></span> | <span data-ttu-id="bec81-180">PackageTags</span><span class="sxs-lookup"><span data-stu-id="bec81-180">PackageTags</span></span> | <span data-ttu-id="bec81-181">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-181">empty</span></span> | <span data-ttu-id="bec81-182">Tagi są rozdzielane średnikami.</span><span class="sxs-lookup"><span data-stu-id="bec81-182">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="bec81-183">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="bec81-183">ReleaseNotes</span></span> | <span data-ttu-id="bec81-184">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="bec81-184">PackageReleaseNotes</span></span> | <span data-ttu-id="bec81-185">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-185">empty</span></span> | |
| <span data-ttu-id="bec81-186">Repozytorium/adres URL</span><span class="sxs-lookup"><span data-stu-id="bec81-186">Repository/Url</span></span> | <span data-ttu-id="bec81-187">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-187">RepositoryUrl</span></span> | <span data-ttu-id="bec81-188">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-188">empty</span></span> | <span data-ttu-id="bec81-189">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="bec81-189">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="bec81-190">Przyklad *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="bec81-190">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="bec81-191">Repozytorium/typ</span><span class="sxs-lookup"><span data-stu-id="bec81-191">Repository/Type</span></span> | <span data-ttu-id="bec81-192">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="bec81-192">RepositoryType</span></span> | <span data-ttu-id="bec81-193">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-193">empty</span></span> | <span data-ttu-id="bec81-194">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="bec81-194">Repository type.</span></span> <span data-ttu-id="bec81-195">Przykłady: *git*i *TFS*.</span><span class="sxs-lookup"><span data-stu-id="bec81-195">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="bec81-196">Repozytorium/gałąź</span><span class="sxs-lookup"><span data-stu-id="bec81-196">Repository/Branch</span></span> | <span data-ttu-id="bec81-197">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="bec81-197">RepositoryBranch</span></span> | <span data-ttu-id="bec81-198">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-198">empty</span></span> | <span data-ttu-id="bec81-199">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="bec81-199">Optional repository branch information.</span></span> <span data-ttu-id="bec81-200">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="bec81-200">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="bec81-201">Przykład: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="bec81-201">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="bec81-202">Repozytorium/zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="bec81-202">Repository/Commit</span></span> | <span data-ttu-id="bec81-203">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="bec81-203">RepositoryCommit</span></span> | <span data-ttu-id="bec81-204">empty</span><span class="sxs-lookup"><span data-stu-id="bec81-204">empty</span></span> | <span data-ttu-id="bec81-205">Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="bec81-205">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="bec81-206">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="bec81-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="bec81-207">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="bec81-207">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="bec81-208">PackageType</span><span class="sxs-lookup"><span data-stu-id="bec81-208">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="bec81-209">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="bec81-209">Summary</span></span> | <span data-ttu-id="bec81-210">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="bec81-210">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="bec81-211">docelowe dane wejściowe pakietu</span><span class="sxs-lookup"><span data-stu-id="bec81-211">pack target inputs</span></span>

- <span data-ttu-id="bec81-212">Ispacking</span><span class="sxs-lookup"><span data-stu-id="bec81-212">IsPackable</span></span>
- <span data-ttu-id="bec81-213">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="bec81-213">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="bec81-214">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="bec81-214">PackageVersion</span></span>
- <span data-ttu-id="bec81-215">PackageId</span><span class="sxs-lookup"><span data-stu-id="bec81-215">PackageId</span></span>
- <span data-ttu-id="bec81-216">Autorzy</span><span class="sxs-lookup"><span data-stu-id="bec81-216">Authors</span></span>
- <span data-ttu-id="bec81-217">Opis</span><span class="sxs-lookup"><span data-stu-id="bec81-217">Description</span></span>
- <span data-ttu-id="bec81-218">Prawo</span><span class="sxs-lookup"><span data-stu-id="bec81-218">Copyright</span></span>
- <span data-ttu-id="bec81-219">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="bec81-219">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="bec81-220">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="bec81-220">DevelopmentDependency</span></span>
- <span data-ttu-id="bec81-221">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="bec81-221">PackageLicenseExpression</span></span>
- <span data-ttu-id="bec81-222">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="bec81-222">PackageLicenseFile</span></span>
- <span data-ttu-id="bec81-223">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-223">PackageLicenseUrl</span></span>
- <span data-ttu-id="bec81-224">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-224">PackageProjectUrl</span></span>
- <span data-ttu-id="bec81-225">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-225">PackageIconUrl</span></span>
- <span data-ttu-id="bec81-226">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="bec81-226">PackageReleaseNotes</span></span>
- <span data-ttu-id="bec81-227">PackageTags</span><span class="sxs-lookup"><span data-stu-id="bec81-227">PackageTags</span></span>
- <span data-ttu-id="bec81-228">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="bec81-228">PackageOutputPath</span></span>
- <span data-ttu-id="bec81-229">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="bec81-229">IncludeSymbols</span></span>
- <span data-ttu-id="bec81-230">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="bec81-230">IncludeSource</span></span>
- <span data-ttu-id="bec81-231">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="bec81-231">PackageTypes</span></span>
- <span data-ttu-id="bec81-232">Istool</span><span class="sxs-lookup"><span data-stu-id="bec81-232">IsTool</span></span>
- <span data-ttu-id="bec81-233">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-233">RepositoryUrl</span></span>
- <span data-ttu-id="bec81-234">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="bec81-234">RepositoryType</span></span>
- <span data-ttu-id="bec81-235">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="bec81-235">RepositoryBranch</span></span>
- <span data-ttu-id="bec81-236">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="bec81-236">RepositoryCommit</span></span>
- <span data-ttu-id="bec81-237">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="bec81-237">NoPackageAnalysis</span></span>
- <span data-ttu-id="bec81-238">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="bec81-238">MinClientVersion</span></span>
- <span data-ttu-id="bec81-239">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="bec81-239">IncludeBuildOutput</span></span>
- <span data-ttu-id="bec81-240">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="bec81-240">IncludeContentInPack</span></span>
- <span data-ttu-id="bec81-241">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="bec81-241">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="bec81-242">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="bec81-242">ContentTargetFolders</span></span>
- <span data-ttu-id="bec81-243">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="bec81-243">NuspecFile</span></span>
- <span data-ttu-id="bec81-244">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="bec81-244">NuspecBasePath</span></span>
- <span data-ttu-id="bec81-245">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="bec81-245">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="bec81-246">scenariusze dotyczące pakietów</span><span class="sxs-lookup"><span data-stu-id="bec81-246">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="bec81-247">Pomiń zależności</span><span class="sxs-lookup"><span data-stu-id="bec81-247">Suppress dependencies</span></span>

<span data-ttu-id="bec81-248">Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet `SuppressDependenciesWhenPacking` , `true` ustaw opcję na, która będzie zezwalać na pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.</span><span class="sxs-lookup"><span data-stu-id="bec81-248">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="bec81-249">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="bec81-249">PackageIconUrl</span></span>

<span data-ttu-id="bec81-250">W ramach zmiany problemu z pakietem [NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` ostatecznie zmieni się na `PackageIconUri` i będzie to ścieżka względna do pliku ikony, który będzie zawarty w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="bec81-250">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="bec81-251">Zestawy wyjściowe</span><span class="sxs-lookup"><span data-stu-id="bec81-251">Output assemblies</span></span>

<span data-ttu-id="bec81-252">`nuget pack`Kopiuje pliki `.exe`wyjściowe z rozszerzeniami `.dll` `.xml`, `.winmd` `.pri`,,, i. `.json`</span><span class="sxs-lookup"><span data-stu-id="bec81-252">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="bec81-253">Pliki wyjściowe, które są kopiowane, zależą od tego, co `BuiltOutputProjectGroup` program MSBuild dostarcza z elementu docelowego.</span><span class="sxs-lookup"><span data-stu-id="bec81-253">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="bec81-254">Istnieją dwie właściwości programu MSBuild, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie znajdują się zestawy wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bec81-254">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="bec81-255">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="bec81-255">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="bec81-256">`BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="bec81-256">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="bec81-257">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="bec81-257">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="bec81-258">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="bec81-258">Package references</span></span>

<span data-ttu-id="bec81-259">Zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="bec81-259">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="bec81-260">Odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="bec81-260">Project to project references</span></span>

<span data-ttu-id="bec81-261">Odwołania projektu do projektu są traktowane domyślnie jako odwołania do pakietów NuGet, na przykład:</span><span class="sxs-lookup"><span data-stu-id="bec81-261">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="bec81-262">Możesz również dodać następujące metadane do odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="bec81-262">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="bec81-263">Dołączanie zawartości do pakietu</span><span class="sxs-lookup"><span data-stu-id="bec81-263">Including content in a package</span></span>

<span data-ttu-id="bec81-264">Aby dołączyć zawartość, Dodaj dodatkowe metadane do istniejącego `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="bec81-264">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="bec81-265">Domyślnie wszystkie elementy typu "Content" są uwzględniane w pakiecie, chyba że przestąpisz do wpisów, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="bec81-265">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="bec81-266">Domyślnie wszystko jest dodawane do katalogu głównego `content` folderu i `contentFiles\any\<target_framework>` w pakiecie i zachowuje względną strukturę folderów, chyba że zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="bec81-266">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="bec81-267">Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (a nie `content` `contentFiles` obu), możesz użyć właściwości `ContentTargetFolders`programu MSBuild, która jest wartością domyślną "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="bec81-267">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="bec81-268">Należy pamiętać, że po prostu określenie " `ContentTargetFolders` contentFiles" w `contentFiles\any\<target_framework>` umieszcza plików w `buildAction`obszarze lub `contentFiles\<language>\<target_framework>` na podstawie.</span><span class="sxs-lookup"><span data-stu-id="bec81-268">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="bec81-269">`PackagePath`może to być rozdzielany średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="bec81-269">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="bec81-270">Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="bec81-270">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="bec81-271">Na przykład następujące polecenie dodaje `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="bec81-271">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="bec81-272">Istnieje również właściwość `$(IncludeContentInPack)`programu MSBuild, której `true`wartością domyślną jest.</span><span class="sxs-lookup"><span data-stu-id="bec81-272">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="bec81-273">Jeśli ta wartość jest ustawiona `false` na dla każdego projektu, zawartość z tego projektu nie jest dołączana do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="bec81-273">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="bec81-274">Inne metadane specyficzne dla pakietu, które można ustawić dla każdego z powyższych elementów, ```<PackageCopyToOutput>``` obejmują ```<PackageFlatten>``` i które ```CopyToOutput``` ```contentFiles``` zestawy ```Flatten``` i wartości wpisu w danych wyjściowych nuspec.</span><span class="sxs-lookup"><span data-stu-id="bec81-274">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="bec81-275">Oprócz elementów `<Pack>` zawartości można również ustawić metadane `<PackagePath>` i dla plików z akcją kompilacji kompilowania, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="bec81-275">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="bec81-276">Aby pakiet mógł dołączyć nazwę pliku do ścieżki pakietu przy użyciu wzorców obsługi symboli wieloznacznych, ścieżka pakietu musi kończyć się znakiem separatora folderów. w przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka, w tym nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="bec81-276">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="bec81-277">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="bec81-277">IncludeSymbols</span></span>

<span data-ttu-id="bec81-278">W przypadku `MSBuild -t:pack -p:IncludeSymbols=true`korzystania z programu `.pdb` odpowiednie pliki są kopiowane wraz z innymi `.xml`plikami wyjściowymi `.exe` `.json`( `.winmd``.dll`,,, `.pri`,,).</span><span class="sxs-lookup"><span data-stu-id="bec81-278">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="bec81-279">Należy pamiętać, `IncludeSymbols=true` że ustawienie powoduje utworzenie regularnego pakietu *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="bec81-279">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="bec81-280">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="bec81-280">IncludeSource</span></span>

<span data-ttu-id="bec81-281">Jest to takie samo, `IncludeSymbols`jak, z tą różnicą, że kopiuje `.pdb` również pliki źródłowe wraz z plikami.</span><span class="sxs-lookup"><span data-stu-id="bec81-281">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="bec81-282">Wszystkie pliki typu `Compile` są kopiowane za pośrednictwem `src\<ProjectName>\` , aby zachować strukturę folderu ścieżki względnej w pakietie będącym wynikiem.</span><span class="sxs-lookup"><span data-stu-id="bec81-282">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="bec81-283">To samo występuje również dla plików `ProjectReference` źródłowych, które mają `TreatAsPackageReference` ustawioną wartość `false`.</span><span class="sxs-lookup"><span data-stu-id="bec81-283">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="bec81-284">Jeśli plik typu Kompiluj znajduje się poza folderem projektu, to właśnie został dodany do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="bec81-284">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="bec81-285">Pakowanie wyrażenia licencji lub pliku licencji</span><span class="sxs-lookup"><span data-stu-id="bec81-285">Packing a license expression or a license file</span></span>

<span data-ttu-id="bec81-286">W przypadku korzystania z wyrażenia licencji Właściwość PackageLicenseExpression powinna zostać użyta.</span><span class="sxs-lookup"><span data-stu-id="bec81-286">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="bec81-287">[Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="bec81-287">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="bec81-288">[Dowiedz się więcej na temat wyrażeń licencji i licencji akceptowanych przez NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="bec81-288">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="bec81-289">Podczas pakowania pliku licencji należy użyć właściwości PackageLicenseFile, aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="bec81-289">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="bec81-290">Ponadto należy się upewnić, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="bec81-290">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="bec81-291">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bec81-291">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="bec81-292">[Przykład pliku licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="bec81-292">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="bec81-293">Istool</span><span class="sxs-lookup"><span data-stu-id="bec81-293">IsTool</span></span>

<span data-ttu-id="bec81-294">W przypadku `MSBuild -t:pack -p:IsTool=true`korzystania z programu wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , `tools` są kopiowane do folderu `lib` , a nie do folderu.</span><span class="sxs-lookup"><span data-stu-id="bec81-294">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="bec81-295">Należy zauważyć, że różni się to `DotNetCliTool` od elementu, który jest określony `PackageType` przez `.csproj` ustawienie w pliku.</span><span class="sxs-lookup"><span data-stu-id="bec81-295">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="bec81-296">Pakowanie przy użyciu elementu. nuspec</span><span class="sxs-lookup"><span data-stu-id="bec81-296">Packing using a .nuspec</span></span>

<span data-ttu-id="bec81-297">Mimo że zaleca się uwzględnienie [wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu, można użyć `.nuspec` pliku do spakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="bec81-297">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="bec81-298">W przypadku projektu typu innego niż zestaw SDK, który `PackageReference`używa programu, należy `NuGet.Build.Tasks.Pack.targets` go zaimportować, aby można było wykonać zadanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="bec81-298">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="bec81-299">Nadal trzeba przywrócić projekt, aby można było spakować plik NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="bec81-299">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="bec81-300">(Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).</span><span class="sxs-lookup"><span data-stu-id="bec81-300">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="bec81-301">Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="bec81-301">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="bec81-302">Następujące trzy właściwości programu MSBuild dotyczą pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="bec81-302">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="bec81-303">`NuspecFile`: względna lub bezwzględna `.nuspec` ścieżka do pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="bec81-303">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="bec81-304">`NuspecProperties`: rozdzielana średnikami lista par klucz = wartość.</span><span class="sxs-lookup"><span data-stu-id="bec81-304">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="bec81-305">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild należy określić wiele właściwości w następujący sposób: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="bec81-305">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="bec81-306">`NuspecBasePath`: Podstawowa ścieżka do `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="bec81-306">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="bec81-307">Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bec81-307">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="bec81-308">Jeśli używasz programu MSBuild do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bec81-308">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="bec81-309">Należy pamiętać, że pakowanie nuspec przy użyciu programu dotnet. exe lub MSBuild również prowadzi do domyślnego kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="bec81-309">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="bec81-310">Można to uniknąć przez przekazanie ```--no-build``` właściwości do programu dotnet. exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="bec81-310">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="bec81-311">Przykład pliku *. csproj* do spakowania pliku nuspec jest:</span><span class="sxs-lookup"><span data-stu-id="bec81-311">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="bec81-312">Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="bec81-312">Advanced extension points to create customized package</span></span>

<span data-ttu-id="bec81-313">`pack` Element docelowy zawiera dwa punkty rozszerzenia, które są uruchamiane w wewnętrznej, docelowej kompilacji specyficznej dla platformy.</span><span class="sxs-lookup"><span data-stu-id="bec81-313">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="bec81-314">Obsługa punktów rozszerzenia umożliwia uwzględnienie zawartości i zestawów określonych dla platformy docelowej w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="bec81-314">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="bec81-315">`TargetsForTfmSpecificBuildOutput`obiektów Używane dla plików wewnątrz `lib` folderu lub folderu określonego przy użyciu. `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="bec81-315">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="bec81-316">`TargetsForTfmSpecificContentInPackage`obiektów Używane dla plików poza programem `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="bec81-316">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="bec81-317">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="bec81-317">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="bec81-318">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="bec81-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="bec81-319">Dla wszystkich plików, które muszą przejść `BuildOutputTargetFolder` do (domyślnie lib), obiekt docelowy powinien zapisać te pliki do obiektu `BuildOutputInPackage` Items i ustawić następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="bec81-319">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="bec81-320">`FinalOutputPath`: Ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość służy do oszacowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="bec81-320">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="bec81-321">`TargetPath`:  Obowiązkowe Ustaw, gdy plik musi przejść do podfolderu w `lib\<TargetFramework>` , podobnie jak zestawy satelickie, które przechodzą w odpowiednie foldery kultury.</span><span class="sxs-lookup"><span data-stu-id="bec81-321">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="bec81-322">Wartością domyślną jest nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="bec81-322">Defaults to the name of the file.</span></span>

<span data-ttu-id="bec81-323">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bec81-323">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="bec81-324">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="bec81-324">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="bec81-325">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="bec81-325">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="bec81-326">Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki `TfmSpecificPackageFile` w obiekcie Items i ustawić następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="bec81-326">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="bec81-327">`PackagePath`: Ścieżka, w której plik powinien być wyprowadzany w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="bec81-327">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="bec81-328">Pakiet NuGet wystawia ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="bec81-328">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="bec81-329">`BuildAction`: Akcja kompilacji, która ma zostać przypisana do pliku, wymagana tylko wtedy, gdy ścieżka pakietu `contentFiles` znajduje się w folderze.</span><span class="sxs-lookup"><span data-stu-id="bec81-329">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="bec81-330">Wartość domyślna to "none".</span><span class="sxs-lookup"><span data-stu-id="bec81-330">Defaults to "None".</span></span>

<span data-ttu-id="bec81-331">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bec81-331">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="bec81-332">Przywróć miejsce docelowe</span><span class="sxs-lookup"><span data-stu-id="bec81-332">restore target</span></span>

<span data-ttu-id="bec81-333">`MSBuild -t:restore`(które `nuget restore` `dotnet restore` są używane z projektami .NET Core), przywraca pakiety, do których odwołuje się plik projektu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bec81-333">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="bec81-334">Odczytuj wszystkie odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="bec81-334">Read all project to project references</span></span>
1. <span data-ttu-id="bec81-335">Odczytywanie właściwości projektu w celu znalezienia pośredniego folderu i platform docelowych</span><span class="sxs-lookup"><span data-stu-id="bec81-335">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="bec81-336">Przekaż dane programu MSBuild do pliku NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="bec81-336">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="bec81-337">Uruchom przywracanie</span><span class="sxs-lookup"><span data-stu-id="bec81-337">Run restore</span></span>
1. <span data-ttu-id="bec81-338">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="bec81-338">Download packages</span></span>
1. <span data-ttu-id="bec81-339">Zapisz plik zasobów, cele i właściwości.</span><span class="sxs-lookup"><span data-stu-id="bec81-339">Write assets file, targets, and props</span></span>

<span data-ttu-id="bec81-340">Obiekt docelowy działa tylko w przypadku projektów korzystających z formatu PackageReference. `restore`</span><span class="sxs-lookup"><span data-stu-id="bec81-340">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="bec81-341">Nie działa w przypadku projektów przy użyciu `packages.config` formatu; zamiast tego należy użyć [przywracania NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="bec81-341">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="bec81-342">Właściwości przywracania</span><span class="sxs-lookup"><span data-stu-id="bec81-342">Restore properties</span></span>

<span data-ttu-id="bec81-343">Dodatkowe ustawienia przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="bec81-343">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="bec81-344">Wartości można również ustawić z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="bec81-344">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="bec81-345">Właściwość</span><span class="sxs-lookup"><span data-stu-id="bec81-345">Property</span></span> | <span data-ttu-id="bec81-346">Opis</span><span class="sxs-lookup"><span data-stu-id="bec81-346">Description</span></span> |
|--------|--------|
| <span data-ttu-id="bec81-347">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="bec81-347">RestoreSources</span></span> | <span data-ttu-id="bec81-348">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="bec81-348">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="bec81-349">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="bec81-349">RestorePackagesPath</span></span> | <span data-ttu-id="bec81-350">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bec81-350">User packages folder path.</span></span> |
| <span data-ttu-id="bec81-351">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="bec81-351">RestoreDisableParallel</span></span> | <span data-ttu-id="bec81-352">Ogranicz pobieranie do jednej naraz.</span><span class="sxs-lookup"><span data-stu-id="bec81-352">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="bec81-353">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="bec81-353">RestoreConfigFile</span></span> | <span data-ttu-id="bec81-354">Ścieżka do `Nuget.Config` pliku, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="bec81-354">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="bec81-355">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="bec81-355">RestoreNoCache</span></span> | <span data-ttu-id="bec81-356">Jeśli ma wartość true, unika używania buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="bec81-356">If true, avoids using cached packages.</span></span> <span data-ttu-id="bec81-357">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci](../consume-packages/managing-the-global-packages-and-cache-folders.md)podręcznej.</span><span class="sxs-lookup"><span data-stu-id="bec81-357">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="bec81-358">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="bec81-358">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="bec81-359">W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="bec81-359">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="bec81-360">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="bec81-360">RestoreFallbackFolders</span></span> | <span data-ttu-id="bec81-361">Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bec81-361">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="bec81-362">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="bec81-362">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="bec81-363">Dodatkowe źródła do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="bec81-363">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="bec81-364">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="bec81-364">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="bec81-365">Dodatkowe foldery rezerwowe do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="bec81-365">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="bec81-366">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="bec81-366">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="bec81-367">Wyklucza foldery rezerwowe określone w`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="bec81-367">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="bec81-368">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="bec81-368">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="bec81-369">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="bec81-369">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="bec81-370">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="bec81-370">RestoreGraphProjectInput</span></span> | <span data-ttu-id="bec81-371">Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="bec81-371">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="bec81-372">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="bec81-372">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="bec81-373">Gdy projekty są zbierane za pośrednictwem programu `SkipNonexistentTargets` MSBuild, określa, czy są zbierane przy użyciu optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="bec81-373">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="bec81-374">Gdy wartość nie jest ustawiona, `true`wartością domyślną jest.</span><span class="sxs-lookup"><span data-stu-id="bec81-374">When not set, defaults to `true`.</span></span> <span data-ttu-id="bec81-375">Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu.</span><span class="sxs-lookup"><span data-stu-id="bec81-375">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="bec81-376">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="bec81-376">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="bec81-377">Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` `obj` i folder.</span><span class="sxs-lookup"><span data-stu-id="bec81-377">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="bec81-378">Przykłady</span><span class="sxs-lookup"><span data-stu-id="bec81-378">Examples</span></span>

<span data-ttu-id="bec81-379">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="bec81-379">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="bec81-380">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="bec81-380">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="bec81-381">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="bec81-381">Restore outputs</span></span>

<span data-ttu-id="bec81-382">Instrukcja RESTORE tworzy następujące pliki w folderze Build `obj` :</span><span class="sxs-lookup"><span data-stu-id="bec81-382">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="bec81-383">Plik</span><span class="sxs-lookup"><span data-stu-id="bec81-383">File</span></span> | <span data-ttu-id="bec81-384">Opis</span><span class="sxs-lookup"><span data-stu-id="bec81-384">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="bec81-385">Zawiera wykres zależności wszystkich odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="bec81-385">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="bec81-386">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="bec81-386">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="bec81-387">Odwołania do elementów docelowych programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="bec81-387">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="bec81-388">Przywracanie i kompilowanie za pomocą jednego polecenia MSBuild</span><span class="sxs-lookup"><span data-stu-id="bec81-388">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="bec81-389">Ze względu na fakt, że pakiet NuGet może przywrócić pakiety, które wyłączają elementy docelowe i właściwości programu MSBuild, a oceny przywracania i kompilacji są uruchamiane z różnymi właściwośćmi globalnymi.</span><span class="sxs-lookup"><span data-stu-id="bec81-389">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="bec81-390">Oznacza to, że następujące elementy będą miały nieprzewidywalne i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="bec81-390">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="bec81-391">Zamiast tego zalecane podejście to:</span><span class="sxs-lookup"><span data-stu-id="bec81-391">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="bec81-392">Ta sama logika ma zastosowanie do innych obiektów `build`docelowych podobnych do.</span><span class="sxs-lookup"><span data-stu-id="bec81-392">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="bec81-393">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="bec81-393">PackageTargetFallback</span></span>

<span data-ttu-id="bec81-394">`PackageTargetFallback` Element umożliwia określenie zestawu zgodnych elementów docelowych, które mają być używane podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="bec81-394">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="bec81-395">Została zaprojektowana tak, aby zezwalać na pakiety, które używają [TxM](../reference/target-frameworks.md) dotnet, do pracy z zgodnymi pakietami, które nie deklarują TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="bec81-395">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="bec81-396">Oznacza to, że jeśli w projekcie jest używany TxM dotnet, wszystkie pakiety, od których zależy, muszą także mieć TxM dotnet, chyba że zostanie dodany `<PackageTargetFallback>` do projektu w celu umożliwienia zgodności z platformą dotnet.</span><span class="sxs-lookup"><span data-stu-id="bec81-396">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="bec81-397">Na przykład jeśli projekt używa `netstandard1.6` TxM, a pakiet zależny zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, to projekt nie zostanie skompilowany.</span><span class="sxs-lookup"><span data-stu-id="bec81-397">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="bec81-398">Jeśli co chcesz zrobić, jest to Ostatnia Biblioteka DLL, a następnie możesz dodać `PackageTargetFallback` polecenie w następujący sposób, aby powiedzieć, `portable-net45+win81` że biblioteka DLL jest zgodna:</span><span class="sxs-lookup"><span data-stu-id="bec81-398">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="bec81-399">Aby zadeklarować rezerwę dla wszystkich obiektów docelowych w projekcie, pozostaw ten `Condition` atrybut.</span><span class="sxs-lookup"><span data-stu-id="bec81-399">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="bec81-400">Możesz również rozłożyć wszystkie istniejące `PackageTargetFallback` , w `$(PackageTargetFallback)` tym tutaj, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="bec81-400">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="bec81-401">Zastępowanie jednej biblioteki na podstawie grafu przywracania</span><span class="sxs-lookup"><span data-stu-id="bec81-401">Replacing one library from a restore graph</span></span>

<span data-ttu-id="bec81-402">Jeśli przywracanie powoduje przełączenie niewłaściwego zestawu, możliwe jest wykluczenie domyślnego wyboru pakietów i zamienienie go na własny wybór.</span><span class="sxs-lookup"><span data-stu-id="bec81-402">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="bec81-403">Najpierw należy wykluczyć wszystkie elementy `PackageReference`zawartości z najwyższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="bec81-403">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="bec81-404">Następnie Dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="bec81-404">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
