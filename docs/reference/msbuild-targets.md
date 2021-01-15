---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą współpracować bezpośrednio z obiektami docelowymi programu MSBuild z pakietem NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235701"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="29963-103">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="29963-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="29963-104">*Pakiet NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="29963-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="29963-105">W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) program NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="29963-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="29963-106">Dzięki programowi MSBuild 15.1 + pakiet NuGet jest również pierwszym klasą obywatela programu MSBuild z `pack` `restore` obiektami docelowymi, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="29963-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="29963-107">Te elementy docelowe umożliwiają współdziałanie z pakietem NuGet, podobnie jak w przypadku każdego innego zadania lub celu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="29963-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="29963-108">Aby uzyskać instrukcje tworzenia pakietu NuGet przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="29963-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="29963-109">(W przypadku programu NuGet 3. x i starszych należy użyć poleceń [pakiet](../reference/cli-reference/cli-ref-pack.md) i [Przywróć](../reference/cli-reference/cli-ref-restore.md) zamiast tego w interfejsie wiersza polecenia NuGet).</span><span class="sxs-lookup"><span data-stu-id="29963-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="29963-110">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="29963-110">Target build order</span></span>

<span data-ttu-id="29963-111">Ponieważ `pack` i `restore` są obiektami docelowymi programu MSBuild, możesz uzyskać do nich dostęp, aby usprawnić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="29963-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="29963-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu.</span><span class="sxs-lookup"><span data-stu-id="29963-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="29963-113">Można to zrobić, dodając następujący plik w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="29963-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="29963-114">Podobnie można napisać zadanie programu MSBuild, napisać własne miejsce docelowe i korzystać z właściwości NuGet w zadaniu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="29963-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="29963-115">`$(OutputPath)` jest względna i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="29963-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="29963-116">cel pakietu</span><span class="sxs-lookup"><span data-stu-id="29963-116">pack target</span></span>

<span data-ttu-id="29963-117">W przypadku projektów .NET Standard przy użyciu formatu PackageReference użycie narzędzi `msbuild -t:pack` Pobiera dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="29963-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="29963-118">W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle.</span><span class="sxs-lookup"><span data-stu-id="29963-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="29963-119">Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="29963-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="29963-120">Dla wygody tabela jest zorganizowana przez równoważną właściwość w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="29963-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="29963-121">Należy zauważyć, `Owners` że `Summary` właściwości i z `.nuspec` nie są obsługiwane w programie MSBuild.</span><span class="sxs-lookup"><span data-stu-id="29963-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="29963-122">Wartość atrybutu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="29963-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="29963-123">Właściwość programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="29963-123">MSBuild Property</span></span> | <span data-ttu-id="29963-124">Domyślne</span><span class="sxs-lookup"><span data-stu-id="29963-124">Default</span></span> | <span data-ttu-id="29963-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="29963-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="29963-126">Id</span><span class="sxs-lookup"><span data-stu-id="29963-126">Id</span></span> | <span data-ttu-id="29963-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="29963-127">PackageId</span></span> | <span data-ttu-id="29963-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="29963-128">AssemblyName</span></span> | <span data-ttu-id="29963-129">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="29963-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="29963-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="29963-130">Version</span></span> | <span data-ttu-id="29963-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="29963-131">PackageVersion</span></span> | <span data-ttu-id="29963-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="29963-132">Version</span></span> | <span data-ttu-id="29963-133">Jest to zgodne z semver, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="29963-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="29963-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="29963-134">VersionPrefix</span></span> | <span data-ttu-id="29963-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="29963-135">PackageVersionPrefix</span></span> | <span data-ttu-id="29963-136">puste</span><span class="sxs-lookup"><span data-stu-id="29963-136">empty</span></span> | <span data-ttu-id="29963-137">Ustawienie PackageVersion zastępowanie PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="29963-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="29963-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="29963-138">VersionSuffix</span></span> | <span data-ttu-id="29963-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="29963-139">PackageVersionSuffix</span></span> | <span data-ttu-id="29963-140">puste</span><span class="sxs-lookup"><span data-stu-id="29963-140">empty</span></span> | <span data-ttu-id="29963-141">$ (VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="29963-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="29963-142">Ustawienie PackageVersion zastępowanie PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="29963-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="29963-143">Autorzy</span><span class="sxs-lookup"><span data-stu-id="29963-143">Authors</span></span> | <span data-ttu-id="29963-144">Autorzy</span><span class="sxs-lookup"><span data-stu-id="29963-144">Authors</span></span> | <span data-ttu-id="29963-145">Nazwa_użytkownika bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="29963-145">Username of the current user</span></span> | |
| <span data-ttu-id="29963-146">Właściciele</span><span class="sxs-lookup"><span data-stu-id="29963-146">Owners</span></span> | <span data-ttu-id="29963-147">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="29963-147">N/A</span></span> | <span data-ttu-id="29963-148">Nieobecny w NuSpec</span><span class="sxs-lookup"><span data-stu-id="29963-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="29963-149">Tytuł</span><span class="sxs-lookup"><span data-stu-id="29963-149">Title</span></span> | <span data-ttu-id="29963-150">Tytuł</span><span class="sxs-lookup"><span data-stu-id="29963-150">Title</span></span> | <span data-ttu-id="29963-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="29963-151">The PackageId</span></span>| |
| <span data-ttu-id="29963-152">Opis</span><span class="sxs-lookup"><span data-stu-id="29963-152">Description</span></span> | <span data-ttu-id="29963-153">Opis</span><span class="sxs-lookup"><span data-stu-id="29963-153">Description</span></span> | <span data-ttu-id="29963-154">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="29963-154">"Package Description"</span></span> | |
| <span data-ttu-id="29963-155">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="29963-155">Copyright</span></span> | <span data-ttu-id="29963-156">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="29963-156">Copyright</span></span> | <span data-ttu-id="29963-157">puste</span><span class="sxs-lookup"><span data-stu-id="29963-157">empty</span></span> | |
| <span data-ttu-id="29963-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="29963-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="29963-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="29963-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="29963-160">fałsz</span><span class="sxs-lookup"><span data-stu-id="29963-160">false</span></span> | |
| <span data-ttu-id="29963-161">license (licencja)</span><span class="sxs-lookup"><span data-stu-id="29963-161">license</span></span> | <span data-ttu-id="29963-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="29963-162">PackageLicenseExpression</span></span> | <span data-ttu-id="29963-163">puste</span><span class="sxs-lookup"><span data-stu-id="29963-163">empty</span></span> | <span data-ttu-id="29963-164">Odnosi się do `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="29963-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="29963-165">license (licencja)</span><span class="sxs-lookup"><span data-stu-id="29963-165">license</span></span> | <span data-ttu-id="29963-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="29963-166">PackageLicenseFile</span></span> | <span data-ttu-id="29963-167">puste</span><span class="sxs-lookup"><span data-stu-id="29963-167">empty</span></span> | <span data-ttu-id="29963-168">Odnosi się do `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="29963-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="29963-169">Należy jawnie spakować plik licencji, do której istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="29963-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="29963-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="29963-170">LicenseUrl</span></span> | <span data-ttu-id="29963-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="29963-171">PackageLicenseUrl</span></span> | <span data-ttu-id="29963-172">puste</span><span class="sxs-lookup"><span data-stu-id="29963-172">empty</span></span> | <span data-ttu-id="29963-173">`PackageLicenseUrl` jest przestarzałe, użyj właściwości PackageLicenseExpression lub PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="29963-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="29963-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="29963-174">ProjectUrl</span></span> | <span data-ttu-id="29963-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="29963-175">PackageProjectUrl</span></span> | <span data-ttu-id="29963-176">puste</span><span class="sxs-lookup"><span data-stu-id="29963-176">empty</span></span> | |
| <span data-ttu-id="29963-177">Ikona</span><span class="sxs-lookup"><span data-stu-id="29963-177">Icon</span></span> | <span data-ttu-id="29963-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="29963-178">PackageIcon</span></span> | <span data-ttu-id="29963-179">puste</span><span class="sxs-lookup"><span data-stu-id="29963-179">empty</span></span> | <span data-ttu-id="29963-180">Należy jawnie spakować plik obrazu ikony, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="29963-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="29963-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="29963-181">IconUrl</span></span> | <span data-ttu-id="29963-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="29963-182">PackageIconUrl</span></span> | <span data-ttu-id="29963-183">puste</span><span class="sxs-lookup"><span data-stu-id="29963-183">empty</span></span> | <span data-ttu-id="29963-184">W przypadku najlepszego środowiska niskiego poziomu `PackageIconUrl` należy określić oprócz programu `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="29963-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="29963-185">Dłuższy termin, `PackageIconUrl` będzie przestarzały.</span><span class="sxs-lookup"><span data-stu-id="29963-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="29963-186">Tagi</span><span class="sxs-lookup"><span data-stu-id="29963-186">Tags</span></span> | <span data-ttu-id="29963-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="29963-187">PackageTags</span></span> | <span data-ttu-id="29963-188">puste</span><span class="sxs-lookup"><span data-stu-id="29963-188">empty</span></span> | <span data-ttu-id="29963-189">Tagi są rozdzielane średnikami.</span><span class="sxs-lookup"><span data-stu-id="29963-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="29963-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="29963-190">ReleaseNotes</span></span> | <span data-ttu-id="29963-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="29963-191">PackageReleaseNotes</span></span> | <span data-ttu-id="29963-192">puste</span><span class="sxs-lookup"><span data-stu-id="29963-192">empty</span></span> | |
| <span data-ttu-id="29963-193">Repozytorium/adres URL</span><span class="sxs-lookup"><span data-stu-id="29963-193">Repository/Url</span></span> | <span data-ttu-id="29963-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="29963-194">RepositoryUrl</span></span> | <span data-ttu-id="29963-195">puste</span><span class="sxs-lookup"><span data-stu-id="29963-195">empty</span></span> | <span data-ttu-id="29963-196">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="29963-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="29963-197">Przyklad *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="29963-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="29963-198">Repozytorium/typ</span><span class="sxs-lookup"><span data-stu-id="29963-198">Repository/Type</span></span> | <span data-ttu-id="29963-199">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="29963-199">RepositoryType</span></span> | <span data-ttu-id="29963-200">puste</span><span class="sxs-lookup"><span data-stu-id="29963-200">empty</span></span> | <span data-ttu-id="29963-201">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="29963-201">Repository type.</span></span> <span data-ttu-id="29963-202">Przykłady: *git* i *TFS*.</span><span class="sxs-lookup"><span data-stu-id="29963-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="29963-203">Repozytorium/gałąź</span><span class="sxs-lookup"><span data-stu-id="29963-203">Repository/Branch</span></span> | <span data-ttu-id="29963-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="29963-204">RepositoryBranch</span></span> | <span data-ttu-id="29963-205">puste</span><span class="sxs-lookup"><span data-stu-id="29963-205">empty</span></span> | <span data-ttu-id="29963-206">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="29963-206">Optional repository branch information.</span></span> <span data-ttu-id="29963-207">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="29963-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="29963-208">Przykład: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="29963-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="29963-209">Repozytorium/zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="29963-209">Repository/Commit</span></span> | <span data-ttu-id="29963-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="29963-210">RepositoryCommit</span></span> | <span data-ttu-id="29963-211">puste</span><span class="sxs-lookup"><span data-stu-id="29963-211">empty</span></span> | <span data-ttu-id="29963-212">Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="29963-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="29963-213">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="29963-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="29963-214">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="29963-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="29963-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="29963-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="29963-216">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="29963-216">Summary</span></span> | <span data-ttu-id="29963-217">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="29963-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="29963-218">docelowe dane wejściowe pakietu</span><span class="sxs-lookup"><span data-stu-id="29963-218">pack target inputs</span></span>

- <span data-ttu-id="29963-219">Ispacking</span><span class="sxs-lookup"><span data-stu-id="29963-219">IsPackable</span></span>
- <span data-ttu-id="29963-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="29963-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="29963-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="29963-221">PackageVersion</span></span>
- <span data-ttu-id="29963-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="29963-222">PackageId</span></span>
- <span data-ttu-id="29963-223">Autorzy</span><span class="sxs-lookup"><span data-stu-id="29963-223">Authors</span></span>
- <span data-ttu-id="29963-224">Opis</span><span class="sxs-lookup"><span data-stu-id="29963-224">Description</span></span>
- <span data-ttu-id="29963-225">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="29963-225">Copyright</span></span>
- <span data-ttu-id="29963-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="29963-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="29963-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="29963-227">DevelopmentDependency</span></span>
- <span data-ttu-id="29963-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="29963-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="29963-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="29963-229">PackageLicenseFile</span></span>
- <span data-ttu-id="29963-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="29963-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="29963-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="29963-231">PackageProjectUrl</span></span>
- <span data-ttu-id="29963-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="29963-232">PackageIconUrl</span></span>
- <span data-ttu-id="29963-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="29963-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="29963-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="29963-234">PackageTags</span></span>
- <span data-ttu-id="29963-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="29963-235">PackageOutputPath</span></span>
- <span data-ttu-id="29963-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="29963-236">IncludeSymbols</span></span>
- <span data-ttu-id="29963-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="29963-237">IncludeSource</span></span>
- <span data-ttu-id="29963-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="29963-238">PackageTypes</span></span>
- <span data-ttu-id="29963-239">Istool</span><span class="sxs-lookup"><span data-stu-id="29963-239">IsTool</span></span>
- <span data-ttu-id="29963-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="29963-240">RepositoryUrl</span></span>
- <span data-ttu-id="29963-241">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="29963-241">RepositoryType</span></span>
- <span data-ttu-id="29963-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="29963-242">RepositoryBranch</span></span>
- <span data-ttu-id="29963-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="29963-243">RepositoryCommit</span></span>
- <span data-ttu-id="29963-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="29963-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="29963-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="29963-245">MinClientVersion</span></span>
- <span data-ttu-id="29963-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="29963-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="29963-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="29963-247">IncludeContentInPack</span></span>
- <span data-ttu-id="29963-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="29963-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="29963-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="29963-249">ContentTargetFolders</span></span>
- <span data-ttu-id="29963-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="29963-250">NuspecFile</span></span>
- <span data-ttu-id="29963-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="29963-251">NuspecBasePath</span></span>
- <span data-ttu-id="29963-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="29963-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="29963-253">scenariusze dotyczące pakietów</span><span class="sxs-lookup"><span data-stu-id="29963-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="29963-254">Pomiń zależności</span><span class="sxs-lookup"><span data-stu-id="29963-254">Suppress dependencies</span></span>

<span data-ttu-id="29963-255">Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet, ustaw opcję `SuppressDependenciesWhenPacking` na `true` , która będzie zezwalać na pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.</span><span class="sxs-lookup"><span data-stu-id="29963-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="29963-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="29963-256">PackageIconUrl</span></span>

<span data-ttu-id="29963-257">`PackageIconUrl` zostanie zaniechane na korzyść nowej [`PackageIcon`](#packageicon) właściwości.</span><span class="sxs-lookup"><span data-stu-id="29963-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="29963-258">Począwszy od programu NuGet 5,3 & programu Visual Studio 2019 w wersji 16,3, `pack` program zwróci ostrzeżenie [NU5048](./errors-and-warnings/nu5048.md) , jeśli określi on tylko metadane pakietu `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="29963-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="29963-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="29963-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="29963-260">Należy określić zarówno `PackageIcon` i, `PackageIconUrl` Aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które nie są jeszcze obsługiwane `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="29963-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="29963-261">Program Visual Studio będzie obsługiwał `PackageIcon` pakiety pochodzące ze źródła opartego na folderach w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="29963-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="29963-262">Pakowanie pliku obrazu ikony</span><span class="sxs-lookup"><span data-stu-id="29963-262">Packing an icon image file</span></span>

<span data-ttu-id="29963-263">Podczas pakowania pliku obrazu ikony należy użyć `PackageIcon` właściwości, aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="29963-264">Ponadto należy się upewnić, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="29963-265">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="29963-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="29963-266">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="29963-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="29963-267">Zalecamy rozdzielczość obrazu 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="29963-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="29963-268">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="29963-268">For example:</span></span>

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

<span data-ttu-id="29963-269">[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="29963-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="29963-270">Aby uzyskać odpowiedniki nuspec, zapoznaj się z tematem [nuspec Reference dla ikony](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="29963-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="29963-271">Zestawy wyjściowe</span><span class="sxs-lookup"><span data-stu-id="29963-271">Output assemblies</span></span>

<span data-ttu-id="29963-272">`nuget pack` Kopiuje pliki wyjściowe z rozszerzeniami,,,, `.exe` `.dll` `.xml` `.winmd` `.json` i `.pri` .</span><span class="sxs-lookup"><span data-stu-id="29963-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="29963-273">Pliki wyjściowe, które są kopiowane, zależą od tego, co program MSBuild dostarcza z `BuiltOutputProjectGroup` elementu docelowego.</span><span class="sxs-lookup"><span data-stu-id="29963-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="29963-274">Istnieją dwie właściwości programu MSBuild, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie znajdują się zestawy wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="29963-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="29963-275">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="29963-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="29963-276">`BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="29963-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="29963-277">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="29963-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="29963-278">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="29963-278">Package references</span></span>

<span data-ttu-id="29963-279">Zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="29963-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="29963-280">Odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="29963-280">Project to project references</span></span>

<span data-ttu-id="29963-281">Odwołania projektu do projektu są traktowane domyślnie jako odwołania do pakietów NuGet, na przykład:</span><span class="sxs-lookup"><span data-stu-id="29963-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="29963-282">Możesz również dodać następujące metadane do odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="29963-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="29963-283">Dołączanie zawartości do pakietu</span><span class="sxs-lookup"><span data-stu-id="29963-283">Including content in a package</span></span>

<span data-ttu-id="29963-284">Aby dołączyć zawartość, Dodaj dodatkowe metadane do istniejącego `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="29963-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="29963-285">Domyślnie wszystkie elementy typu "Content" są uwzględniane w pakiecie, chyba że przestąpisz do wpisów, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="29963-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="29963-286">Domyślnie wszystko jest dodawane do katalogu głównego `content` `contentFiles\any\<target_framework>` folderu i w pakiecie i zachowuje względną strukturę folderów, chyba że zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="29963-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="29963-287">Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (a nie `content` `contentFiles` obu), możesz użyć właściwości programu MSBuild `ContentTargetFolders` , która jest wartością domyślną "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="29963-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="29963-288">Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` umieszcza plików w obszarze `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="29963-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="29963-289">`PackagePath` może to być rozdzielany średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="29963-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="29963-290">Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="29963-291">Na przykład następujące polecenie dodaje `libuv.txt` do `content\myfiles` , `content\samples` i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="29963-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="29963-292">Istnieje również właściwość programu MSBuild `$(IncludeContentInPack)` , której wartością domyślną jest `true` .</span><span class="sxs-lookup"><span data-stu-id="29963-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="29963-293">Jeśli ta wartość jest ustawiona na `false` dla każdego projektu, zawartość z tego projektu nie jest dołączana do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="29963-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="29963-294">Inne metadane specyficzne dla pakietu, które można ustawić dla każdego z powyższych elementów, obejmują ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` które zestawy ```CopyToOutput``` i ```Flatten``` wartości ```contentFiles``` wpisu w danych wyjściowych nuspec.</span><span class="sxs-lookup"><span data-stu-id="29963-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="29963-295">Oprócz elementów zawartości `<Pack>` `<PackagePath>` można również ustawić metadane i dla plików z akcją kompilacji kompilowania, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="29963-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="29963-296">Aby pakiet mógł dołączyć nazwę pliku do ścieżki pakietu przy użyciu wzorców obsługi symboli wieloznacznych, ścieżka pakietu musi kończyć się znakiem separatora folderów. w przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka, w tym nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="29963-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="29963-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="29963-297">IncludeSymbols</span></span>

<span data-ttu-id="29963-298">W przypadku korzystania z programu `MSBuild -t:pack -p:IncludeSymbols=true` odpowiednie `.pdb` pliki są kopiowane wraz z innymi plikami wyjściowymi ( `.dll` ,,,, `.exe` `.winmd` `.xml` `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="29963-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="29963-299">Należy pamiętać, że ustawienie `IncludeSymbols=true` powoduje utworzenie regularnego pakietu *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="29963-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="29963-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="29963-300">IncludeSource</span></span>

<span data-ttu-id="29963-301">Jest to takie samo `IncludeSymbols` , jak, z tą różnicą, że kopiuje również pliki źródłowe wraz z `.pdb` plikami.</span><span class="sxs-lookup"><span data-stu-id="29963-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="29963-302">Wszystkie pliki typu `Compile` są kopiowane za pośrednictwem `src\<ProjectName>\` , aby zachować strukturę folderu ścieżki względnej w pakietie będącym wynikiem.</span><span class="sxs-lookup"><span data-stu-id="29963-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="29963-303">To samo występuje również dla plików źródłowych, `ProjectReference` które mają `TreatAsPackageReference` ustawioną wartość `false` .</span><span class="sxs-lookup"><span data-stu-id="29963-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="29963-304">Jeśli plik typu Kompiluj znajduje się poza folderem projektu, to właśnie został dodany do `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="29963-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="29963-305">Pakowanie wyrażenia licencji lub pliku licencji</span><span class="sxs-lookup"><span data-stu-id="29963-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="29963-306">W przypadku korzystania z wyrażenia licencji Właściwość PackageLicenseExpression powinna zostać użyta.</span><span class="sxs-lookup"><span data-stu-id="29963-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="29963-307">[Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="29963-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="29963-308">[Dowiedz się więcej na temat wyrażeń licencji i licencji akceptowanych przez NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="29963-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="29963-309">Podczas pakowania pliku licencji należy użyć właściwości PackageLicenseFile, aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="29963-310">Ponadto należy się upewnić, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="29963-311">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="29963-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="29963-312">[Przykład pliku licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="29963-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="29963-313">Pakowanie pliku bez rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="29963-313">Packing a file without an extension</span></span>

<span data-ttu-id="29963-314">W niektórych scenariuszach, takich jak podczas pakowania pliku licencji, może być konieczne dołączenie pliku bez rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="29963-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="29963-315">Ze względów historycznych pakiet NuGet & MSBuild traktuje ścieżki bez rozszerzenia jako katalogów.</span><span class="sxs-lookup"><span data-stu-id="29963-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="29963-316">[Plik bez rozszerzenia](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="29963-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="29963-317">Istool</span><span class="sxs-lookup"><span data-stu-id="29963-317">IsTool</span></span>

<span data-ttu-id="29963-318">W przypadku korzystania z programu `MSBuild -t:pack -p:IsTool=true` wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , są kopiowane do `tools` folderu, a nie do `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="29963-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="29963-319">Należy zauważyć, że różni się to od elementu, `DotNetCliTool` który jest określony przez ustawienie `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="29963-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="29963-320">Pakowanie przy użyciu elementu. nuspec</span><span class="sxs-lookup"><span data-stu-id="29963-320">Packing using a .nuspec</span></span>

<span data-ttu-id="29963-321">Mimo że zaleca się [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu, można użyć `.nuspec` pliku do spakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="29963-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="29963-322">W przypadku projektu typu innego niż zestaw SDK, który używa programu `PackageReference` , należy go zaimportować, `NuGet.Build.Tasks.Pack.targets` Aby można było wykonać zadanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="29963-323">Nadal trzeba przywrócić projekt, aby można było spakować plik NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="29963-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="29963-324">(Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).</span><span class="sxs-lookup"><span data-stu-id="29963-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="29963-325">Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="29963-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="29963-326">Następujące trzy właściwości programu MSBuild dotyczą pakowania przy użyciu `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="29963-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="29963-327">`NuspecFile`: względna lub bezwzględna ścieżka do `.nuspec` pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="29963-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="29963-328">`NuspecProperties`: rozdzielana średnikami lista par klucz = wartość.</span><span class="sxs-lookup"><span data-stu-id="29963-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="29963-329">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild należy określić wiele właściwości w następujący sposób: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="29963-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="29963-330">`NuspecBasePath`: Ścieżka podstawowa dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="29963-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="29963-331">Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29963-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="29963-332">Jeśli używasz programu MSBuild do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29963-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="29963-333">Należy pamiętać, że pakowanie nuspec przy użyciu dotnet.exe lub MSBuild również prowadzi do domyślnego kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="29963-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="29963-334">Można to uniknąć przez przekazanie ```--no-build``` właściwości do dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="29963-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="29963-335">Przykład pliku *. csproj* do spakowania pliku nuspec jest:</span><span class="sxs-lookup"><span data-stu-id="29963-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="29963-336">Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="29963-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="29963-337">`pack`Element docelowy zawiera dwa punkty rozszerzenia, które są uruchamiane w wewnętrznej, docelowej kompilacji specyficznej dla platformy.</span><span class="sxs-lookup"><span data-stu-id="29963-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="29963-338">Obsługa punktów rozszerzenia umożliwia uwzględnienie zawartości i zestawów określonych dla platformy docelowej w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="29963-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="29963-339">`TargetsForTfmSpecificBuildOutput` target: Użyj dla plików znajdujących się w `lib` folderze lub folderu określonego przy użyciu `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="29963-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="29963-340">`TargetsForTfmSpecificContentInPackage` target: Użyj dla plików poza `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="29963-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="29963-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="29963-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="29963-342">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="29963-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="29963-343">Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), obiekt docelowy powinien zapisać te pliki do obiektu Items `BuildOutputInPackage` i ustawić następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="29963-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="29963-344">`FinalOutputPath`: Ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość służy do oszacowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="29963-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="29963-345">`TargetPath`: (Opcjonalnie) ustawia się, gdy plik musi przejść do podfolderu w `lib\<TargetFramework>` , podobnie jak zestawy satelickie, które przechodzą w odpowiednie foldery kultury.</span><span class="sxs-lookup"><span data-stu-id="29963-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="29963-346">Wartością domyślną jest nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="29963-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="29963-347">Przykład:</span><span class="sxs-lookup"><span data-stu-id="29963-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="29963-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="29963-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="29963-349">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="29963-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="29963-350">Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki w obiekcie Items `TfmSpecificPackageFile` i ustawić następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="29963-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="29963-351">`PackagePath`: Ścieżka, w której plik powinien być wyprowadzany w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="29963-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="29963-352">Pakiet NuGet wystawia ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="29963-353">`BuildAction`: Akcja kompilacji, która ma zostać przypisana do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w `contentFiles` folderze.</span><span class="sxs-lookup"><span data-stu-id="29963-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="29963-354">Wartość domyślna to "none".</span><span class="sxs-lookup"><span data-stu-id="29963-354">Defaults to "None".</span></span>

<span data-ttu-id="29963-355">Przykład:</span><span class="sxs-lookup"><span data-stu-id="29963-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="29963-356">Przywróć miejsce docelowe</span><span class="sxs-lookup"><span data-stu-id="29963-356">restore target</span></span>

<span data-ttu-id="29963-357">`MSBuild -t:restore` (które `nuget restore` `dotnet restore` są używane z projektami .NET Core), przywraca pakiety, do których odwołuje się plik projektu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29963-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="29963-358">Odczytuj wszystkie odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="29963-358">Read all project to project references</span></span>
1. <span data-ttu-id="29963-359">Odczytywanie właściwości projektu w celu znalezienia pośredniego folderu i platform docelowych</span><span class="sxs-lookup"><span data-stu-id="29963-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="29963-360">Przekaż dane programu MSBuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="29963-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="29963-361">Uruchom przywracanie</span><span class="sxs-lookup"><span data-stu-id="29963-361">Run restore</span></span>
1. <span data-ttu-id="29963-362">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="29963-362">Download packages</span></span>
1. <span data-ttu-id="29963-363">Zapisz plik zasobów, cele i właściwości.</span><span class="sxs-lookup"><span data-stu-id="29963-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="29963-364">`restore`Obiekt docelowy działa dla projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="29963-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="29963-365">`MSBuild 16.5+` Ponadto zapewnia [obsługę](#restoring-packagereference-and-packagesconfig-with-msbuild) tego `packages.config` formatu.</span><span class="sxs-lookup"><span data-stu-id="29963-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="29963-366">`restore`Element docelowy [nie powinien być uruchamiany](#restoring-and-building-with-one-msbuild-command) w połączeniu z `build` elementem docelowym.</span><span class="sxs-lookup"><span data-stu-id="29963-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="29963-367">Właściwości przywracania</span><span class="sxs-lookup"><span data-stu-id="29963-367">Restore properties</span></span>

<span data-ttu-id="29963-368">Dodatkowe ustawienia przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="29963-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="29963-369">Wartości można również ustawić z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="29963-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="29963-370">Właściwość</span><span class="sxs-lookup"><span data-stu-id="29963-370">Property</span></span> | <span data-ttu-id="29963-371">Opis</span><span class="sxs-lookup"><span data-stu-id="29963-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="29963-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="29963-372">RestoreSources</span></span> | <span data-ttu-id="29963-373">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="29963-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="29963-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="29963-374">RestorePackagesPath</span></span> | <span data-ttu-id="29963-375">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29963-375">User packages folder path.</span></span> |
| <span data-ttu-id="29963-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="29963-376">RestoreDisableParallel</span></span> | <span data-ttu-id="29963-377">Ogranicz pobieranie do jednej naraz.</span><span class="sxs-lookup"><span data-stu-id="29963-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="29963-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="29963-378">RestoreConfigFile</span></span> | <span data-ttu-id="29963-379">Ścieżka do `Nuget.Config` pliku, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="29963-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="29963-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="29963-380">RestoreNoCache</span></span> | <span data-ttu-id="29963-381">Jeśli ma wartość true, unika używania buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="29963-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="29963-382">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="29963-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="29963-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="29963-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="29963-384">W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="29963-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="29963-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="29963-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="29963-386">Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29963-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="29963-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="29963-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="29963-388">Dodatkowe źródła do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="29963-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="29963-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="29963-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="29963-390">Dodatkowe foldery rezerwowe do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="29963-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="29963-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="29963-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="29963-392">Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="29963-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="29963-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="29963-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="29963-394">Ścieżka do `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="29963-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="29963-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="29963-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="29963-396">Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="29963-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="29963-397">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="29963-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="29963-398">Gdy projekty są zbierane za pośrednictwem programu MSBuild, określa, czy są zbierane przy użyciu `SkipNonexistentTargets` optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="29963-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="29963-399">Gdy wartość nie jest ustawiona, wartością domyślną jest `true` .</span><span class="sxs-lookup"><span data-stu-id="29963-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="29963-400">Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu.</span><span class="sxs-lookup"><span data-stu-id="29963-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="29963-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="29963-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="29963-402">Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` i `obj` folder.</span><span class="sxs-lookup"><span data-stu-id="29963-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="29963-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="29963-403">RestoreForce</span></span> | <span data-ttu-id="29963-404">W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="29963-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="29963-405">Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="29963-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="29963-406">Nie powoduje to obejścia pamięci podręcznej protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="29963-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="29963-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="29963-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="29963-408">Umożliwia użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="29963-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="29963-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="29963-409">RestoreLockedMode</span></span> | <span data-ttu-id="29963-410">Uruchom przywracanie w trybie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="29963-410">Run restore in locked mode.</span></span> <span data-ttu-id="29963-411">Oznacza to, że przywracanie nie będzie obliczać zależności.</span><span class="sxs-lookup"><span data-stu-id="29963-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="29963-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="29963-412">NuGetLockFilePath</span></span> | <span data-ttu-id="29963-413">Niestandardowa lokalizacja pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="29963-413">A custom location for the lock file.</span></span> <span data-ttu-id="29963-414">Domyślna lokalizacja jest obok projektu i ma nazwę `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="29963-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="29963-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="29963-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="29963-416">Wymusza ponowne obliczenie zależności przez Przywracanie i zaktualizowanie pliku blokady bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="29963-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="29963-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="29963-417">RestorePackagesConfig</span></span> | <span data-ttu-id="29963-418">Opcjonalny przełącznik, który przywraca projekty z packages.config. Obsługa `MSBuild -t:restore` wyłącznie.</span><span class="sxs-lookup"><span data-stu-id="29963-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="29963-419">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="29963-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="29963-420">Opcjonalny przełącznik do korzystania z oceny MSBuild wykresu statycznego zamiast standardowej oceny.</span><span class="sxs-lookup"><span data-stu-id="29963-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="29963-421">Obliczanie wykresu statycznego to eksperymentalna funkcja, która jest znacznie szybsza w przypadku dużych repozytoriów i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="29963-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="29963-422">Przykłady</span><span class="sxs-lookup"><span data-stu-id="29963-422">Examples</span></span>

<span data-ttu-id="29963-423">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="29963-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="29963-424">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="29963-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="29963-425">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="29963-425">Restore outputs</span></span>

<span data-ttu-id="29963-426">Instrukcja RESTORE tworzy następujące pliki w folderze Build `obj` :</span><span class="sxs-lookup"><span data-stu-id="29963-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="29963-427">Plik</span><span class="sxs-lookup"><span data-stu-id="29963-427">File</span></span> | <span data-ttu-id="29963-428">Opis</span><span class="sxs-lookup"><span data-stu-id="29963-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="29963-429">Zawiera wykres zależności wszystkich odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="29963-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="29963-430">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="29963-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="29963-431">Odwołania do elementów docelowych programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="29963-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="29963-432">Przywracanie i kompilowanie za pomocą jednego polecenia MSBuild</span><span class="sxs-lookup"><span data-stu-id="29963-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="29963-433">Ze względu na fakt, że pakiet NuGet może przywrócić pakiety, które wyłączają elementy docelowe i właściwości programu MSBuild, a oceny przywracania i kompilacji są uruchamiane z różnymi właściwośćmi globalnymi.</span><span class="sxs-lookup"><span data-stu-id="29963-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="29963-434">Oznacza to, że następujące elementy będą miały nieprzewidywalne i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="29963-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="29963-435">Zamiast tego zalecane podejście to:</span><span class="sxs-lookup"><span data-stu-id="29963-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="29963-436">Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build` .</span><span class="sxs-lookup"><span data-stu-id="29963-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="29963-437">Przywracanie PackageReference i packages.config przy użyciu programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="29963-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="29963-438">W programie MSBuild 16.5 + packages.config są również obsługiwane w programie `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="29963-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="29963-439">`packages.config` Przywracanie jest dostępne `MSBuild 16.5+` tylko z `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="29963-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="29963-440">Przywracanie za pomocą obliczenia wykresu statycznego MSBuild</span><span class="sxs-lookup"><span data-stu-id="29963-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="29963-441">Przy użyciu programu MSBuild 16.6 + pakiet NuGet dodał funkcję eksperymentalną do użycia obliczeń wykresu statycznego z wiersza polecenia, która znacznie skraca czas przywracania dla dużych repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="29963-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="29963-442">Alternatywnie możesz ją włączyć, ustawiając właściwość w katalogu. Build. props.</span><span class="sxs-lookup"><span data-stu-id="29963-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="29963-443">Począwszy od programu Visual Studio 2019. x i NuGet 5. x, ta funkcja jest uznawana za eksperymentalną i niezależną.</span><span class="sxs-lookup"><span data-stu-id="29963-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="29963-444">Aby uzyskać szczegółowe informacje o tym, kiedy ta funkcja zostanie włączona domyślnie, należy przestrzegać [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) .</span><span class="sxs-lookup"><span data-stu-id="29963-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="29963-445">Statyczne przywracanie wykresu zmienia część programu MSBuild przywracania, odczytywanie i ocenianie projektu, ale nie algorytmem przywracania.</span><span class="sxs-lookup"><span data-stu-id="29963-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="29963-446">Algorytm przywracania jest taki sam dla wszystkich narzędzi NuGet (NuGet.exe, MSBuild.exe, dotnet.exe i Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="29963-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="29963-447">W bardzo kilku scenariuszach statyczne przywracanie wykresu może zachowywać się inaczej niż bieżące przywracanie, a niektóre zadeklarowane składnika packagereferences lub zawierających mogą być niedostępne.</span><span class="sxs-lookup"><span data-stu-id="29963-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="29963-448">Aby ułatwić sobie zdanie, podczas migracji do przywracania wykresu statycznego należy wziąć pod uwagę następujące działania:</span><span class="sxs-lookup"><span data-stu-id="29963-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="29963-449">Pakiet NuGet *nie* powinien zgłaszać żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="29963-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="29963-450">Jeśli widzisz Niezgodność, zrób problem w pliku [NuGet/Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="29963-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="29963-451">Zastępowanie jednej biblioteki na podstawie grafu przywracania</span><span class="sxs-lookup"><span data-stu-id="29963-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="29963-452">Jeśli przywracanie powoduje przełączenie niewłaściwego zestawu, możliwe jest wykluczenie domyślnego wyboru pakietów i zamienienie go na własny wybór.</span><span class="sxs-lookup"><span data-stu-id="29963-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="29963-453">Najpierw `PackageReference` należy wykluczyć wszystkie elementy zawartości z najwyższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="29963-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="29963-454">Następnie Dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="29963-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
