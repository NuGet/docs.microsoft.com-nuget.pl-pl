---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą współpracować bezpośrednio z obiektami docelowymi programu MSBuild z pakietem NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 1c2af0b42e88623fa7a1216c17aa269e9b0a58cf
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096907"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="ca4b7-103">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="ca4b7-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="ca4b7-104">*Pakiet NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="ca4b7-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="ca4b7-105">W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) program NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego pliku `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="ca4b7-106">W programie MSBuild 15.1 + pakiet NuGet jest również pierwszą klasą obywatela programu MSBuild z `pack` i `restore`, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="ca4b7-107">Te elementy docelowe umożliwiają współdziałanie z pakietem NuGet, podobnie jak w przypadku każdego innego zadania lub celu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="ca4b7-108">Aby uzyskać instrukcje tworzenia pakietu NuGet przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="ca4b7-109">(W przypadku programu NuGet 3. x i starszych należy użyć poleceń [pakiet](../reference/cli-reference/cli-ref-pack.md) i [Przywróć](../reference/cli-reference/cli-ref-restore.md) zamiast tego w interfejsie wiersza polecenia NuGet).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="ca4b7-110">Docelowy porządek kompilacji</span><span class="sxs-lookup"><span data-stu-id="ca4b7-110">Target build order</span></span>

<span data-ttu-id="ca4b7-111">Ponieważ `pack` i `restore` są obiektami docelowymi programu MSBuild, można uzyskać do nich dostęp, aby usprawnić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="ca4b7-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="ca4b7-113">Można to zrobić, dodając następujący plik w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="ca4b7-114">Podobnie można napisać zadanie programu MSBuild, napisać własne miejsce docelowe i korzystać z właściwości NuGet w zadaniu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="ca4b7-115">`$(OutputPath)` jest względna i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="ca4b7-116">cel pakietu</span><span class="sxs-lookup"><span data-stu-id="ca4b7-116">pack target</span></span>

<span data-ttu-id="ca4b7-117">W przypadku projektów .NET Standard przy użyciu formatu PackageReference użycie `msbuild -t:pack` rysuje dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="ca4b7-118">W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w pierwszym węźle `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="ca4b7-119">Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="ca4b7-120">Dla wygody tabela jest zorganizowana przez równoważną właściwość w [pliku `.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="ca4b7-121">Należy zauważyć, że właściwości `Owners` i `Summary` z `.nuspec` nie są obsługiwane w programie MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="ca4b7-122">Wartość atrybutu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="ca4b7-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="ca4b7-123">Właściwość programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="ca4b7-123">MSBuild Property</span></span> | <span data-ttu-id="ca4b7-124">Domyślny</span><span class="sxs-lookup"><span data-stu-id="ca4b7-124">Default</span></span> | <span data-ttu-id="ca4b7-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ca4b7-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="ca4b7-126">#C1</span><span class="sxs-lookup"><span data-stu-id="ca4b7-126">Id</span></span> | <span data-ttu-id="ca4b7-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="ca4b7-127">PackageId</span></span> | <span data-ttu-id="ca4b7-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="ca4b7-128">AssemblyName</span></span> | <span data-ttu-id="ca4b7-129">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="ca4b7-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="ca4b7-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="ca4b7-130">Version</span></span> | <span data-ttu-id="ca4b7-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="ca4b7-131">PackageVersion</span></span> | <span data-ttu-id="ca4b7-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="ca4b7-132">Version</span></span> | <span data-ttu-id="ca4b7-133">Jest to zgodne z semver, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="ca4b7-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="ca4b7-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ca4b7-134">VersionPrefix</span></span> | <span data-ttu-id="ca4b7-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ca4b7-135">PackageVersionPrefix</span></span> | <span data-ttu-id="ca4b7-136">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-136">empty</span></span> | <span data-ttu-id="ca4b7-137">Ustawienie PackageVersion zastępowanie PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ca4b7-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="ca4b7-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ca4b7-138">VersionSuffix</span></span> | <span data-ttu-id="ca4b7-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ca4b7-139">PackageVersionSuffix</span></span> | <span data-ttu-id="ca4b7-140">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-140">empty</span></span> | <span data-ttu-id="ca4b7-141">$ (VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="ca4b7-142">Ustawienie PackageVersion zastępowanie PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ca4b7-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="ca4b7-143">Autorów</span><span class="sxs-lookup"><span data-stu-id="ca4b7-143">Authors</span></span> | <span data-ttu-id="ca4b7-144">Autorów</span><span class="sxs-lookup"><span data-stu-id="ca4b7-144">Authors</span></span> | <span data-ttu-id="ca4b7-145">Nazwa_użytkownika bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="ca4b7-145">Username of the current user</span></span> | |
| <span data-ttu-id="ca4b7-146">rzecz</span><span class="sxs-lookup"><span data-stu-id="ca4b7-146">Owners</span></span> | <span data-ttu-id="ca4b7-147">Brak</span><span class="sxs-lookup"><span data-stu-id="ca4b7-147">N/A</span></span> | <span data-ttu-id="ca4b7-148">Nieobecny w NuSpec</span><span class="sxs-lookup"><span data-stu-id="ca4b7-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="ca4b7-149">Tytuł</span><span class="sxs-lookup"><span data-stu-id="ca4b7-149">Title</span></span> | <span data-ttu-id="ca4b7-150">Tytuł</span><span class="sxs-lookup"><span data-stu-id="ca4b7-150">Title</span></span> | <span data-ttu-id="ca4b7-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="ca4b7-151">The PackageId</span></span>| |
| <span data-ttu-id="ca4b7-152">Opis</span><span class="sxs-lookup"><span data-stu-id="ca4b7-152">Description</span></span> | <span data-ttu-id="ca4b7-153">Opis</span><span class="sxs-lookup"><span data-stu-id="ca4b7-153">Description</span></span> | <span data-ttu-id="ca4b7-154">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="ca4b7-154">"Package Description"</span></span> | |
| <span data-ttu-id="ca4b7-155">Prawo</span><span class="sxs-lookup"><span data-stu-id="ca4b7-155">Copyright</span></span> | <span data-ttu-id="ca4b7-156">Prawo</span><span class="sxs-lookup"><span data-stu-id="ca4b7-156">Copyright</span></span> | <span data-ttu-id="ca4b7-157">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-157">empty</span></span> | |
| <span data-ttu-id="ca4b7-158">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="ca4b7-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="ca4b7-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="ca4b7-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="ca4b7-160">false</span><span class="sxs-lookup"><span data-stu-id="ca4b7-160">false</span></span> | |
| <span data-ttu-id="ca4b7-161">licencjonowan</span><span class="sxs-lookup"><span data-stu-id="ca4b7-161">license</span></span> | <span data-ttu-id="ca4b7-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="ca4b7-162">PackageLicenseExpression</span></span> | <span data-ttu-id="ca4b7-163">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-163">empty</span></span> | <span data-ttu-id="ca4b7-164">Odnosi się do `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="ca4b7-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="ca4b7-165">licencjonowan</span><span class="sxs-lookup"><span data-stu-id="ca4b7-165">license</span></span> | <span data-ttu-id="ca4b7-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ca4b7-166">PackageLicenseFile</span></span> | <span data-ttu-id="ca4b7-167">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-167">empty</span></span> | <span data-ttu-id="ca4b7-168">Odnosi się do `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="ca4b7-169">Należy jawnie spakować plik licencji, do której istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="ca4b7-170">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-170">LicenseUrl</span></span> | <span data-ttu-id="ca4b7-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-171">PackageLicenseUrl</span></span> | <span data-ttu-id="ca4b7-172">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-172">empty</span></span> | <span data-ttu-id="ca4b7-173">`PackageLicenseUrl` jest przestarzałe, użyj właściwości PackageLicenseExpression lub PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ca4b7-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="ca4b7-174">projectUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-174">ProjectUrl</span></span> | <span data-ttu-id="ca4b7-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-175">PackageProjectUrl</span></span> | <span data-ttu-id="ca4b7-176">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-176">empty</span></span> | |
| <span data-ttu-id="ca4b7-177">Ikona</span><span class="sxs-lookup"><span data-stu-id="ca4b7-177">Icon</span></span> | <span data-ttu-id="ca4b7-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="ca4b7-178">PackageIcon</span></span> | <span data-ttu-id="ca4b7-179">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-179">empty</span></span> | <span data-ttu-id="ca4b7-180">Należy jawnie spakować plik obrazu ikony, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="ca4b7-181">iconUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-181">IconUrl</span></span> | <span data-ttu-id="ca4b7-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-182">PackageIconUrl</span></span> | <span data-ttu-id="ca4b7-183">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-183">empty</span></span> | <span data-ttu-id="ca4b7-184">Aby zapewnić najlepsze środowisko niskiego poziomu, `PackageIconUrl` należy określić oprócz `PackageIcon`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="ca4b7-185">Dłuższy termin, `PackageIconUrl` będzie przestarzały.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="ca4b7-186">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="ca4b7-186">Tags</span></span> | <span data-ttu-id="ca4b7-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="ca4b7-187">PackageTags</span></span> | <span data-ttu-id="ca4b7-188">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-188">empty</span></span> | <span data-ttu-id="ca4b7-189">Tagi są rozdzielane średnikami.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="ca4b7-190">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="ca4b7-190">ReleaseNotes</span></span> | <span data-ttu-id="ca4b7-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="ca4b7-191">PackageReleaseNotes</span></span> | <span data-ttu-id="ca4b7-192">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-192">empty</span></span> | |
| <span data-ttu-id="ca4b7-193">Repozytorium/adres URL</span><span class="sxs-lookup"><span data-stu-id="ca4b7-193">Repository/Url</span></span> | <span data-ttu-id="ca4b7-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-194">RepositoryUrl</span></span> | <span data-ttu-id="ca4b7-195">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-195">empty</span></span> | <span data-ttu-id="ca4b7-196">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="ca4b7-197">Przykład: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="ca4b7-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="ca4b7-198">Repozytorium/typ</span><span class="sxs-lookup"><span data-stu-id="ca4b7-198">Repository/Type</span></span> | <span data-ttu-id="ca4b7-199">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="ca4b7-199">RepositoryType</span></span> | <span data-ttu-id="ca4b7-200">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-200">empty</span></span> | <span data-ttu-id="ca4b7-201">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-201">Repository type.</span></span> <span data-ttu-id="ca4b7-202">Przykłady: *git*i *TFS*.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="ca4b7-203">Repozytorium/gałąź</span><span class="sxs-lookup"><span data-stu-id="ca4b7-203">Repository/Branch</span></span> | <span data-ttu-id="ca4b7-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="ca4b7-204">RepositoryBranch</span></span> | <span data-ttu-id="ca4b7-205">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-205">empty</span></span> | <span data-ttu-id="ca4b7-206">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-206">Optional repository branch information.</span></span> <span data-ttu-id="ca4b7-207">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="ca4b7-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="ca4b7-208">Przykład: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="ca4b7-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="ca4b7-209">Repozytorium/zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="ca4b7-209">Repository/Commit</span></span> | <span data-ttu-id="ca4b7-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="ca4b7-210">RepositoryCommit</span></span> | <span data-ttu-id="ca4b7-211">empty</span><span class="sxs-lookup"><span data-stu-id="ca4b7-211">empty</span></span> | <span data-ttu-id="ca4b7-212">Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="ca4b7-213">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="ca4b7-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="ca4b7-214">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="ca4b7-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="ca4b7-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="ca4b7-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="ca4b7-216">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ca4b7-216">Summary</span></span> | <span data-ttu-id="ca4b7-217">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="ca4b7-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="ca4b7-218">docelowe dane wejściowe pakietu</span><span class="sxs-lookup"><span data-stu-id="ca4b7-218">pack target inputs</span></span>

- <span data-ttu-id="ca4b7-219">Ispacking</span><span class="sxs-lookup"><span data-stu-id="ca4b7-219">IsPackable</span></span>
- <span data-ttu-id="ca4b7-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="ca4b7-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="ca4b7-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="ca4b7-221">PackageVersion</span></span>
- <span data-ttu-id="ca4b7-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="ca4b7-222">PackageId</span></span>
- <span data-ttu-id="ca4b7-223">Autorów</span><span class="sxs-lookup"><span data-stu-id="ca4b7-223">Authors</span></span>
- <span data-ttu-id="ca4b7-224">Opis</span><span class="sxs-lookup"><span data-stu-id="ca4b7-224">Description</span></span>
- <span data-ttu-id="ca4b7-225">Prawo</span><span class="sxs-lookup"><span data-stu-id="ca4b7-225">Copyright</span></span>
- <span data-ttu-id="ca4b7-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="ca4b7-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="ca4b7-227">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="ca4b7-227">DevelopmentDependency</span></span>
- <span data-ttu-id="ca4b7-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="ca4b7-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="ca4b7-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ca4b7-229">PackageLicenseFile</span></span>
- <span data-ttu-id="ca4b7-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="ca4b7-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-231">PackageProjectUrl</span></span>
- <span data-ttu-id="ca4b7-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-232">PackageIconUrl</span></span>
- <span data-ttu-id="ca4b7-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="ca4b7-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="ca4b7-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="ca4b7-234">PackageTags</span></span>
- <span data-ttu-id="ca4b7-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="ca4b7-235">PackageOutputPath</span></span>
- <span data-ttu-id="ca4b7-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="ca4b7-236">IncludeSymbols</span></span>
- <span data-ttu-id="ca4b7-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="ca4b7-237">IncludeSource</span></span>
- <span data-ttu-id="ca4b7-238">packageTypes</span><span class="sxs-lookup"><span data-stu-id="ca4b7-238">PackageTypes</span></span>
- <span data-ttu-id="ca4b7-239">Istool</span><span class="sxs-lookup"><span data-stu-id="ca4b7-239">IsTool</span></span>
- <span data-ttu-id="ca4b7-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-240">RepositoryUrl</span></span>
- <span data-ttu-id="ca4b7-241">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="ca4b7-241">RepositoryType</span></span>
- <span data-ttu-id="ca4b7-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="ca4b7-242">RepositoryBranch</span></span>
- <span data-ttu-id="ca4b7-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="ca4b7-243">RepositoryCommit</span></span>
- <span data-ttu-id="ca4b7-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="ca4b7-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="ca4b7-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="ca4b7-245">MinClientVersion</span></span>
- <span data-ttu-id="ca4b7-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="ca4b7-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="ca4b7-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="ca4b7-247">IncludeContentInPack</span></span>
- <span data-ttu-id="ca4b7-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="ca4b7-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="ca4b7-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="ca4b7-249">ContentTargetFolders</span></span>
- <span data-ttu-id="ca4b7-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="ca4b7-250">NuspecFile</span></span>
- <span data-ttu-id="ca4b7-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="ca4b7-251">NuspecBasePath</span></span>
- <span data-ttu-id="ca4b7-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="ca4b7-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="ca4b7-253">scenariusze dotyczące pakietów</span><span class="sxs-lookup"><span data-stu-id="ca4b7-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="ca4b7-254">Pomiń zależności</span><span class="sxs-lookup"><span data-stu-id="ca4b7-254">Suppress dependencies</span></span>

<span data-ttu-id="ca4b7-255">Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet, ustaw wartość `SuppressDependenciesWhenPacking` na `true`, co umożliwi pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="ca4b7-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="ca4b7-256">PackageIconUrl</span></span>

<span data-ttu-id="ca4b7-257">`PackageIconUrl` będą przestarzałe na korzyść nowej właściwości [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="ca4b7-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="ca4b7-258">Począwszy od programu NuGet 5,3 & Visual Studio 2019 w wersji 16,3, `pack` zwróci ostrzeżenie [NU5048](errors-and-warnings/nu5048) , jeśli metadane pakietu określają tylko `PackageIconUrl`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](errors-and-warnings/nu5048) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="ca4b7-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="ca4b7-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="ca4b7-260">Należy określić zarówno `PackageIcon`, jak i `PackageIconUrl`, aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które jeszcze nie obsługują `PackageIcon`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="ca4b7-261">Program Visual Studio będzie obsługiwał `PackageIcon` pakietów pochodzących ze źródła opartego na folderach w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="ca4b7-262">Pakowanie pliku obrazu ikony</span><span class="sxs-lookup"><span data-stu-id="ca4b7-262">Packing an icon image file</span></span>

<span data-ttu-id="ca4b7-263">Podczas pakowania pliku obrazu ikony należy użyć właściwości `PackageIcon`, aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ca4b7-264">Ponadto należy się upewnić, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="ca4b7-265">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="ca4b7-266">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="ca4b7-267">Zalecamy rozdzielczość obrazu 64x64.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-267">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="ca4b7-268">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-268">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="ca4b7-269">[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="ca4b7-270">Aby uzyskać odpowiedniki nuspec, zapoznaj się z tematem [nuspec Reference dla ikony](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="ca4b7-271">Zestawy wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ca4b7-271">Output assemblies</span></span>

<span data-ttu-id="ca4b7-272">`nuget pack` kopiuje pliki wyjściowe z rozszerzeniami `.exe`, `.dll`, `.xml`, `.winmd`, `.json` i `.pri`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="ca4b7-273">Pliki wyjściowe, które są kopiowane, zależą od tego, co dziedziczy program MSBuild z elementu docelowego `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="ca4b7-274">Istnieją dwie właściwości programu MSBuild, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie znajdują się zestawy wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="ca4b7-275">`IncludeBuildOutput`: wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być dołączone do pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="ca4b7-276">`BuildOutputTargetFolder`: określa folder, w którym należy umieścić zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="ca4b7-277">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="ca4b7-278">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="ca4b7-278">Package references</span></span>

<span data-ttu-id="ca4b7-279">Zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="ca4b7-280">Odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="ca4b7-280">Project to project references</span></span>

<span data-ttu-id="ca4b7-281">Odwołania projektu do projektu są traktowane domyślnie jako odwołania do pakietów NuGet, na przykład:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="ca4b7-282">Możesz również dodać następujące metadane do odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="ca4b7-283">Dołączanie zawartości do pakietu</span><span class="sxs-lookup"><span data-stu-id="ca4b7-283">Including content in a package</span></span>

<span data-ttu-id="ca4b7-284">Aby dołączyć zawartość, Dodaj dodatkowe metadane do istniejącego elementu `<Content>`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="ca4b7-285">Domyślnie wszystkie elementy typu "Content" są uwzględniane w pakiecie, chyba że przestąpisz do wpisów, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="ca4b7-286">Domyślnie wszystko jest dodawane do katalogu głównego `content` i `contentFiles\any\<target_framework>` folderu w ramach pakietu i zachowuje względną strukturę folderów, chyba że zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="ca4b7-287">Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (zamiast `content` i `contentFiles`), możesz użyć właściwości programu MSBuild `ContentTargetFolders`, która domyślnie przyjmuje wartość "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="ca4b7-288">Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` umieszcza pliki w `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="ca4b7-289">`PackagePath` może być zestawem z rozdzielonymi średnikami ścieżkami docelowymi.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="ca4b7-290">Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="ca4b7-291">Na przykład następujące dodaje `libuv.txt` do `content\myfiles`, `content\samples` i katalogu głównego pakietu:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="ca4b7-292">Istnieje również właściwość programu MSBuild `$(IncludeContentInPack)`, która ma wartość domyślną `true`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="ca4b7-293">Jeśli jest ustawiona na `false` w każdym projekcie, zawartość z tego projektu nie jest dołączana do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="ca4b7-294">Inne metadane specyficzne dla pakietu, które można ustawić dla dowolnego z powyższych elementów, obejmują ```<PackageCopyToOutput>``` i ```<PackageFlatten>```, które ustawiają wartości ```CopyToOutput``` i ```Flatten``` w pozycji ```contentFiles``` w danych wyjściowych nuspec.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="ca4b7-295">Oprócz elementów zawartości można również ustawić metadane `<Pack>` i `<PackagePath>` dla plików z akcją kompilacji kompilowania, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="ca4b7-296">Aby pakiet mógł dołączyć nazwę pliku do ścieżki pakietu przy użyciu wzorców obsługi symboli wieloznacznych, ścieżka pakietu musi kończyć się znakiem separatora folderów. w przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka, w tym nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="ca4b7-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="ca4b7-297">IncludeSymbols</span></span>

<span data-ttu-id="ca4b7-298">W przypadku używania `MSBuild -t:pack -p:IncludeSymbols=true` odpowiednie pliki `.pdb` są kopiowane wraz z innymi plikami wyjściowymi (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="ca4b7-299">Należy pamiętać, że ustawienie `IncludeSymbols=true` tworzy zwykły pakiet *i* pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="ca4b7-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="ca4b7-300">IncludeSource</span></span>

<span data-ttu-id="ca4b7-301">Jest to taka sama jak `IncludeSymbols`, z tą różnicą, że kopiuje pliki źródłowe wraz z również plikami `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="ca4b7-302">Wszystkie pliki typu `Compile` są kopiowane do `src\<ProjectName>\` zachowując strukturę folderu ścieżki względnej w pakietie będącym wynikiem.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="ca4b7-303">Dzieje się tak samo w przypadku plików źródłowych dowolnego `ProjectReference` z ustawieniem `TreatAsPackageReference` ustawionym na `false`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="ca4b7-304">Jeśli plik typu Kompiluj znajduje się poza folderem projektu, to właśnie został dodany do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="ca4b7-305">Pakowanie wyrażenia licencji lub pliku licencji</span><span class="sxs-lookup"><span data-stu-id="ca4b7-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="ca4b7-306">W przypadku korzystania z wyrażenia licencji Właściwość PackageLicenseExpression powinna zostać użyta.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="ca4b7-307">[Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="ca4b7-308">[Dowiedz się więcej na temat wyrażeń licencji i licencji akceptowanych przez NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="ca4b7-309">Podczas pakowania pliku licencji należy użyć właściwości PackageLicenseFile, aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ca4b7-310">Ponadto należy się upewnić, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="ca4b7-311">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="ca4b7-312">[Przykład pliku licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="ca4b7-313">Istool</span><span class="sxs-lookup"><span data-stu-id="ca4b7-313">IsTool</span></span>

<span data-ttu-id="ca4b7-314">W przypadku używania `MSBuild -t:pack -p:IsTool=true` wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , są kopiowane do folderu `tools` zamiast folderu `lib`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-314">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="ca4b7-315">Należy zauważyć, że różni się od `DotNetCliTool`, który jest określony przez ustawienie `PackageType` w pliku `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-315">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="ca4b7-316">Pakowanie przy użyciu elementu. nuspec</span><span class="sxs-lookup"><span data-stu-id="ca4b7-316">Packing using a .nuspec</span></span>

<span data-ttu-id="ca4b7-317">Mimo że zaleca się [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w pliku z `.nuspec` w pliku projektu, można użyć pliku `.nuspec` do spakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-317">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="ca4b7-318">W przypadku projektu typu innego niż zestaw SDK, który używa `PackageReference`, należy zaimportować `NuGet.Build.Tasks.Pack.targets`, aby można było wykonać zadanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-318">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="ca4b7-319">Nadal trzeba przywrócić projekt, aby można było spakować plik NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-319">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="ca4b7-320">(Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-320">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="ca4b7-321">Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-321">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="ca4b7-322">Następujące trzy właściwości programu MSBuild dotyczą pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-322">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="ca4b7-323">`NuspecFile`: ścieżka względna lub bezwzględna do pliku `.nuspec` używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-323">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="ca4b7-324">`NuspecProperties`: rozdzielana średnikami lista par klucz = wartość.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-324">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="ca4b7-325">Ze względu na sposób działania analizy wiersza polecenia MSBuild należy określić wiele właściwości: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-325">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="ca4b7-326">`NuspecBasePath`: Ścieżka bazowa dla pliku `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-326">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="ca4b7-327">Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-327">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ca4b7-328">Jeśli używasz programu MSBuild do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-328">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ca4b7-329">Należy pamiętać, że pakowanie nuspec przy użyciu programu dotnet. exe lub MSBuild również prowadzi do domyślnego kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-329">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="ca4b7-330">Można to uniknąć przez przekazanie właściwości ```--no-build``` do programu dotnet. exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-330">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="ca4b7-331">Przykład pliku *. csproj* do spakowania pliku nuspec jest:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-331">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="ca4b7-332">Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="ca4b7-332">Advanced extension points to create customized package</span></span>

<span data-ttu-id="ca4b7-333">Element docelowy `pack` zawiera dwa punkty rozszerzenia, które są uruchamiane w wewnętrznej kompilacji specyficznej dla platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-333">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="ca4b7-334">Obsługa punktów rozszerzenia umożliwia uwzględnienie zawartości i zestawów określonych dla platformy docelowej w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-334">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="ca4b7-335">element docelowy `TargetsForTfmSpecificBuildOutput`: Użyj dla plików znajdujących się w folderze `lib` lub folderze określonym przy użyciu `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-335">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="ca4b7-336">`TargetsForTfmSpecificContentInPackage` target: Użyj dla plików poza `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-336">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="ca4b7-337">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="ca4b7-337">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="ca4b7-338">Napisz niestandardowy element docelowy i określ go jako wartość właściwości `$(TargetsForTfmSpecificBuildOutput)`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-338">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="ca4b7-339">Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), obiekt docelowy powinien zapisać te pliki w obiekcie Items `BuildOutputInPackage` i ustawić następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-339">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="ca4b7-340">`FinalOutputPath`: ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość służy do oszacowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-340">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="ca4b7-341">`TargetPath`: (opcjonalnie) ustawia się, gdy plik musi przejść do podfolderu w `lib\<TargetFramework>`, podobnie jak zestawy satelickie, które przechodzą w odpowiednie foldery kultury.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-341">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="ca4b7-342">Wartością domyślną jest nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-342">Defaults to the name of the file.</span></span>

<span data-ttu-id="ca4b7-343">Przykład:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-343">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="ca4b7-344">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="ca4b7-344">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="ca4b7-345">Napisz niestandardowy element docelowy i określ go jako wartość właściwości `$(TargetsForTfmSpecificContentInPackage)`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="ca4b7-346">Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki do `TfmSpecificPackageFile` i ustawić następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-346">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="ca4b7-347">`PackagePath`: ścieżka, w której plik powinien być wyprowadzany w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-347">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="ca4b7-348">Pakiet NuGet wystawia ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-348">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="ca4b7-349">`BuildAction`: Akcja kompilacji, która ma zostać przypisana do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w folderze `contentFiles`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-349">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="ca4b7-350">Wartość domyślna to "none".</span><span class="sxs-lookup"><span data-stu-id="ca4b7-350">Defaults to "None".</span></span>

<span data-ttu-id="ca4b7-351">Przykład:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-351">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="ca4b7-352">Przywróć miejsce docelowe</span><span class="sxs-lookup"><span data-stu-id="ca4b7-352">restore target</span></span>

<span data-ttu-id="ca4b7-353">`MSBuild -t:restore` (które `nuget restore` i `dotnet restore` są używane z projektami .NET Core), przywraca pakiety, do których odwołuje się plik projektu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-353">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="ca4b7-354">Odczytuj wszystkie odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="ca4b7-354">Read all project to project references</span></span>
1. <span data-ttu-id="ca4b7-355">Odczytywanie właściwości projektu w celu znalezienia pośredniego folderu i platform docelowych</span><span class="sxs-lookup"><span data-stu-id="ca4b7-355">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="ca4b7-356">Przekaż dane programu MSBuild do pliku NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="ca4b7-356">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="ca4b7-357">Uruchom przywracanie</span><span class="sxs-lookup"><span data-stu-id="ca4b7-357">Run restore</span></span>
1. <span data-ttu-id="ca4b7-358">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="ca4b7-358">Download packages</span></span>
1. <span data-ttu-id="ca4b7-359">Zapisz plik zasobów, cele i właściwości.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-359">Write assets file, targets, and props</span></span>

<span data-ttu-id="ca4b7-360">Element docelowy `restore` działa **tylko** w przypadku projektów korzystających z formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-360">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="ca4b7-361">**Nie działa w** przypadku projektów przy użyciu formatu `packages.config`; Zamiast tego użyj [przywracania NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="ca4b7-361">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="ca4b7-362">Właściwości przywracania</span><span class="sxs-lookup"><span data-stu-id="ca4b7-362">Restore properties</span></span>

<span data-ttu-id="ca4b7-363">Dodatkowe ustawienia przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-363">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="ca4b7-364">Wartości można również ustawić z poziomu wiersza polecenia przy użyciu przełącznika `-p:` (Zobacz poniższe przykłady).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-364">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="ca4b7-365">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ca4b7-365">Property</span></span> | <span data-ttu-id="ca4b7-366">Opis</span><span class="sxs-lookup"><span data-stu-id="ca4b7-366">Description</span></span> |
|--------|--------|
| <span data-ttu-id="ca4b7-367">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="ca4b7-367">RestoreSources</span></span> | <span data-ttu-id="ca4b7-368">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-368">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="ca4b7-369">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="ca4b7-369">RestorePackagesPath</span></span> | <span data-ttu-id="ca4b7-370">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-370">User packages folder path.</span></span> |
| <span data-ttu-id="ca4b7-371">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="ca4b7-371">RestoreDisableParallel</span></span> | <span data-ttu-id="ca4b7-372">Ogranicz pobieranie do jednej naraz.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-372">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="ca4b7-373">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="ca4b7-373">RestoreConfigFile</span></span> | <span data-ttu-id="ca4b7-374">Ścieżka do pliku `Nuget.Config`, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-374">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="ca4b7-375">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="ca4b7-375">RestoreNoCache</span></span> | <span data-ttu-id="ca4b7-376">Jeśli ma wartość true, unika używania buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-376">If true, avoids using cached packages.</span></span> <span data-ttu-id="ca4b7-377">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ca4b7-377">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="ca4b7-378">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="ca4b7-378">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="ca4b7-379">W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-379">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="ca4b7-380">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="ca4b7-380">RestoreFallbackFolders</span></span> | <span data-ttu-id="ca4b7-381">Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="ca4b7-382">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="ca4b7-382">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="ca4b7-383">Dodatkowe źródła do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-383">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="ca4b7-384">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="ca4b7-384">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="ca4b7-385">Dodatkowe foldery rezerwowe do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-385">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="ca4b7-386">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="ca4b7-386">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="ca4b7-387">Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="ca4b7-387">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="ca4b7-388">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="ca4b7-388">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="ca4b7-389">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-389">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="ca4b7-390">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="ca4b7-390">RestoreGraphProjectInput</span></span> | <span data-ttu-id="ca4b7-391">Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-391">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="ca4b7-392">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="ca4b7-392">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="ca4b7-393">Gdy projekty są zbierane za pośrednictwem programu MSBuild, określa, czy są zbierane przy użyciu optymalizacji `SkipNonexistentTargets`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-393">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="ca4b7-394">Gdy nie jest ustawiona, wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-394">When not set, defaults to `true`.</span></span> <span data-ttu-id="ca4b7-395">Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-395">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="ca4b7-396">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="ca4b7-396">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="ca4b7-397">Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` i folder `obj`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-397">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="ca4b7-398">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="ca4b7-398">RestoreForce</span></span> | <span data-ttu-id="ca4b7-399">W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-399">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="ca4b7-400">Określenie tej flagi jest podobne do usuwania pliku `project.assets.json`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-400">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="ca4b7-401">Nie powoduje to obejścia pamięci podręcznej protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-401">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="ca4b7-402">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="ca4b7-402">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="ca4b7-403">Umożliwia użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-403">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="ca4b7-404">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="ca4b7-404">RestoreLockedMode</span></span> | <span data-ttu-id="ca4b7-405">Uruchom przywracanie w trybie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-405">Run restore in locked mode.</span></span> <span data-ttu-id="ca4b7-406">Oznacza to, że przywracanie nie będzie obliczać zależności.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-406">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="ca4b7-407">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="ca4b7-407">NuGetLockFilePath</span></span> | <span data-ttu-id="ca4b7-408">Niestandardowa lokalizacja pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-408">A custom location for the lock file.</span></span> <span data-ttu-id="ca4b7-409">Domyślna lokalizacja jest obok projektu i nosi nazwę `packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-409">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="ca4b7-410">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="ca4b7-410">RestoreForceEvaluate</span></span> | <span data-ttu-id="ca4b7-411">Wymusza ponowne obliczenie zależności przez Przywracanie i zaktualizowanie pliku blokady bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-411">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="ca4b7-412">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ca4b7-412">Examples</span></span>

<span data-ttu-id="ca4b7-413">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-413">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="ca4b7-414">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-414">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="ca4b7-415">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="ca4b7-415">Restore outputs</span></span>

<span data-ttu-id="ca4b7-416">Instrukcja RESTORE tworzy następujące pliki w folderze Build `obj`:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-416">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="ca4b7-417">Plik</span><span class="sxs-lookup"><span data-stu-id="ca4b7-417">File</span></span> | <span data-ttu-id="ca4b7-418">Opis</span><span class="sxs-lookup"><span data-stu-id="ca4b7-418">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="ca4b7-419">Zawiera wykres zależności wszystkich odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-419">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="ca4b7-420">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="ca4b7-420">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="ca4b7-421">Odwołania do elementów docelowych programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="ca4b7-421">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="ca4b7-422">Przywracanie i kompilowanie za pomocą jednego polecenia MSBuild</span><span class="sxs-lookup"><span data-stu-id="ca4b7-422">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="ca4b7-423">Ze względu na fakt, że pakiet NuGet może przywrócić pakiety, które wyłączają elementy docelowe i właściwości programu MSBuild, a oceny przywracania i kompilacji są uruchamiane z różnymi właściwośćmi globalnymi.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-423">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="ca4b7-424">Oznacza to, że następujące elementy będą miały nieprzewidywalne i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-424">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="ca4b7-425">Zamiast tego zalecane podejście to:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-425">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="ca4b7-426">Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-426">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="ca4b7-427">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="ca4b7-427">PackageTargetFallback</span></span>

<span data-ttu-id="ca4b7-428">Element `PackageTargetFallback` umożliwia określenie zestawu zgodnych elementów docelowych, które mają być używane podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-428">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="ca4b7-429">Została zaprojektowana tak, aby zezwalać na pakiety, które używają [TxM](../reference/target-frameworks.md) dotnet, do pracy z zgodnymi pakietami, które nie deklarują TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-429">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="ca4b7-430">Oznacza to, że jeśli projekt używa TxM dotnet, wszystkie pakiety, od których zależy, muszą także mieć TxM dotnet, chyba że dodasz `<PackageTargetFallback>` do projektu w celu umożliwienia zgodności z platformą dotnet.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-430">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="ca4b7-431">Na przykład jeśli projekt używa `netstandard1.6` TxM, a pakiet zależny zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, to projekt nie zostanie skompilowany.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-431">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="ca4b7-432">Jeśli to, co chcesz zrobić, jest tą samą biblioteką DLL, można dodać `PackageTargetFallback` w następujący sposób, aby wyznaczyć, że biblioteka `portable-net45+win81` jest zgodna:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-432">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="ca4b7-433">Aby zadeklarować rezerwę dla wszystkich obiektów docelowych w projekcie, pozostaw atrybut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-433">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="ca4b7-434">Możesz również rozłożyć wszystkie istniejące `PackageTargetFallback` przez uwzględnienie `$(PackageTargetFallback)`, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-434">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="ca4b7-435">Zastępowanie jednej biblioteki na podstawie grafu przywracania</span><span class="sxs-lookup"><span data-stu-id="ca4b7-435">Replacing one library from a restore graph</span></span>

<span data-ttu-id="ca4b7-436">Jeśli przywracanie powoduje przełączenie niewłaściwego zestawu, możliwe jest wykluczenie domyślnego wyboru pakietów i zamienienie go na własny wybór.</span><span class="sxs-lookup"><span data-stu-id="ca4b7-436">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="ca4b7-437">Po pierwsze `PackageReference` Wyklucz wszystkie elementy zawartości:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-437">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="ca4b7-438">Następnie Dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="ca4b7-438">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
