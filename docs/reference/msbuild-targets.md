---
title: Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild
description: Pakiet NuGet i przywracanie mogą współpracować bezpośrednio z obiektami docelowymi programu MSBuild z pakietem NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 16b8ff532b87a3e3f96029e77dd166eb39294c0b
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815344"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="fa257-103">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa257-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="fa257-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="fa257-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="fa257-105">W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) program NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="fa257-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="fa257-106">Dzięki programowi MSBuild 15.1 + pakiet NuGet jest również pierwszym klasą obywatela programu `pack` MSBuild `restore` z obiektami docelowymi, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="fa257-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="fa257-107">Te elementy docelowe umożliwiają współdziałanie z pakietem NuGet, podobnie jak w przypadku każdego innego zadania lub celu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa257-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="fa257-108">Aby uzyskać instrukcje tworzenia pakietu NuGet przy użyciu programu MSBuild, zobacz [Tworzenie pakietu NuGet przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="fa257-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="fa257-109">(W przypadku programu NuGet 3. x i starszych należy użyć poleceń [pakiet](../reference/cli-reference/cli-ref-pack.md) i [Przywróć](../reference/cli-reference/cli-ref-restore.md) zamiast tego w interfejsie wiersza polecenia NuGet).</span><span class="sxs-lookup"><span data-stu-id="fa257-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="fa257-110">Docelowy porządek kompilacji</span><span class="sxs-lookup"><span data-stu-id="fa257-110">Target build order</span></span>

<span data-ttu-id="fa257-111">Ponieważ `pack` i`restore` są obiektami docelowymi programu MSBuild, możesz uzyskać do nich dostęp, aby usprawnić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="fa257-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="fa257-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu.</span><span class="sxs-lookup"><span data-stu-id="fa257-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="fa257-113">Można to zrobić, dodając następujący plik w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="fa257-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="fa257-114">Podobnie można napisać zadanie programu MSBuild, napisać własne miejsce docelowe i korzystać z właściwości NuGet w zadaniu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa257-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="fa257-115">`$(OutputPath)`jest względna i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="fa257-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="fa257-116">cel pakietu</span><span class="sxs-lookup"><span data-stu-id="fa257-116">pack target</span></span>

<span data-ttu-id="fa257-117">W przypadku projektów .NET standard przy użyciu formatu PackageReference użycie `msbuild -t:pack` narzędzi pobiera dane wejściowe z pliku projektu do użycia podczas tworzenia pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa257-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="fa257-118">W poniższej tabeli opisano właściwości programu MSBuild, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle.</span><span class="sxs-lookup"><span data-stu-id="fa257-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="fa257-119">Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="fa257-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="fa257-120">Dla wygody tabela jest zorganizowana przez równoważną właściwość w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="fa257-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="fa257-121">Należy zauważyć, `Owners` że `Summary` właściwości i `.nuspec` z nie są obsługiwane w programie MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa257-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="fa257-122">Wartość atrybutu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="fa257-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="fa257-123">Właściwość programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa257-123">MSBuild Property</span></span> | <span data-ttu-id="fa257-124">Domyślny</span><span class="sxs-lookup"><span data-stu-id="fa257-124">Default</span></span> | <span data-ttu-id="fa257-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fa257-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="fa257-126">Id</span><span class="sxs-lookup"><span data-stu-id="fa257-126">Id</span></span> | <span data-ttu-id="fa257-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="fa257-127">PackageId</span></span> | <span data-ttu-id="fa257-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="fa257-128">AssemblyName</span></span> | <span data-ttu-id="fa257-129">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa257-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="fa257-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="fa257-130">Version</span></span> | <span data-ttu-id="fa257-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fa257-131">PackageVersion</span></span> | <span data-ttu-id="fa257-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="fa257-132">Version</span></span> | <span data-ttu-id="fa257-133">Jest to zgodne z semver, na przykład "1.0.0", "1.0.0-beta" lub "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="fa257-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="fa257-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fa257-134">VersionPrefix</span></span> | <span data-ttu-id="fa257-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fa257-135">PackageVersionPrefix</span></span> | <span data-ttu-id="fa257-136">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-136">empty</span></span> | <span data-ttu-id="fa257-137">Ustawienie PackageVersion zastępowanie PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fa257-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="fa257-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fa257-138">VersionSuffix</span></span> | <span data-ttu-id="fa257-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fa257-139">PackageVersionSuffix</span></span> | <span data-ttu-id="fa257-140">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-140">empty</span></span> | <span data-ttu-id="fa257-141">$ (VersionSuffix) z programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fa257-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="fa257-142">Ustawienie PackageVersion zastępowanie PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fa257-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="fa257-143">Autorzy</span><span class="sxs-lookup"><span data-stu-id="fa257-143">Authors</span></span> | <span data-ttu-id="fa257-144">Autorzy</span><span class="sxs-lookup"><span data-stu-id="fa257-144">Authors</span></span> | <span data-ttu-id="fa257-145">Nazwa_użytkownika bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="fa257-145">Username of the current user</span></span> | |
| <span data-ttu-id="fa257-146">Rzecz</span><span class="sxs-lookup"><span data-stu-id="fa257-146">Owners</span></span> | <span data-ttu-id="fa257-147">Brak</span><span class="sxs-lookup"><span data-stu-id="fa257-147">N/A</span></span> | <span data-ttu-id="fa257-148">Nieobecny w NuSpec</span><span class="sxs-lookup"><span data-stu-id="fa257-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="fa257-149">Tytuł</span><span class="sxs-lookup"><span data-stu-id="fa257-149">Title</span></span> | <span data-ttu-id="fa257-150">Tytuł</span><span class="sxs-lookup"><span data-stu-id="fa257-150">Title</span></span> | <span data-ttu-id="fa257-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="fa257-151">The PackageId</span></span>| |
| <span data-ttu-id="fa257-152">Opis</span><span class="sxs-lookup"><span data-stu-id="fa257-152">Description</span></span> | <span data-ttu-id="fa257-153">Opis</span><span class="sxs-lookup"><span data-stu-id="fa257-153">Description</span></span> | <span data-ttu-id="fa257-154">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="fa257-154">"Package Description"</span></span> | |
| <span data-ttu-id="fa257-155">Prawo</span><span class="sxs-lookup"><span data-stu-id="fa257-155">Copyright</span></span> | <span data-ttu-id="fa257-156">Prawo</span><span class="sxs-lookup"><span data-stu-id="fa257-156">Copyright</span></span> | <span data-ttu-id="fa257-157">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-157">empty</span></span> | |
| <span data-ttu-id="fa257-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fa257-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="fa257-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fa257-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="fa257-160">false</span><span class="sxs-lookup"><span data-stu-id="fa257-160">false</span></span> | |
| <span data-ttu-id="fa257-161">licencjonowan</span><span class="sxs-lookup"><span data-stu-id="fa257-161">license</span></span> | <span data-ttu-id="fa257-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="fa257-162">PackageLicenseExpression</span></span> | <span data-ttu-id="fa257-163">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-163">empty</span></span> | <span data-ttu-id="fa257-164">Odnosi się do`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="fa257-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="fa257-165">licencjonowan</span><span class="sxs-lookup"><span data-stu-id="fa257-165">license</span></span> | <span data-ttu-id="fa257-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="fa257-166">PackageLicenseFile</span></span> | <span data-ttu-id="fa257-167">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-167">empty</span></span> | <span data-ttu-id="fa257-168">Odnosi się `<license type="file">`do.</span><span class="sxs-lookup"><span data-stu-id="fa257-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="fa257-169">Może być konieczne jawne spakowanie pliku licencji, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="fa257-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="fa257-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-170">LicenseUrl</span></span> | <span data-ttu-id="fa257-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-171">PackageLicenseUrl</span></span> | <span data-ttu-id="fa257-172">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-172">empty</span></span> | <span data-ttu-id="fa257-173">`PackageLicenseUrl`jest przestarzałe, użyj właściwości PackageLicenseExpression lub PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="fa257-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="fa257-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-174">ProjectUrl</span></span> | <span data-ttu-id="fa257-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-175">PackageProjectUrl</span></span> | <span data-ttu-id="fa257-176">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-176">empty</span></span> | |
| <span data-ttu-id="fa257-177">Ikona</span><span class="sxs-lookup"><span data-stu-id="fa257-177">Icon</span></span> | <span data-ttu-id="fa257-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="fa257-178">PackageIcon</span></span> | <span data-ttu-id="fa257-179">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-179">empty</span></span> | <span data-ttu-id="fa257-180">Może być konieczne jawne spakowanie pliku obrazu ikony, do którego się odwołuje.</span><span class="sxs-lookup"><span data-stu-id="fa257-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="fa257-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-181">IconUrl</span></span> | <span data-ttu-id="fa257-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-182">PackageIconUrl</span></span> | <span data-ttu-id="fa257-183">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-183">empty</span></span> | <span data-ttu-id="fa257-184">`PackageIconUrl`jest przestarzałe, użyj właściwości PackageIcon</span><span class="sxs-lookup"><span data-stu-id="fa257-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="fa257-185">Znaczniki</span><span class="sxs-lookup"><span data-stu-id="fa257-185">Tags</span></span> | <span data-ttu-id="fa257-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fa257-186">PackageTags</span></span> | <span data-ttu-id="fa257-187">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-187">empty</span></span> | <span data-ttu-id="fa257-188">Tagi są rozdzielane średnikami.</span><span class="sxs-lookup"><span data-stu-id="fa257-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="fa257-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fa257-189">ReleaseNotes</span></span> | <span data-ttu-id="fa257-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fa257-190">PackageReleaseNotes</span></span> | <span data-ttu-id="fa257-191">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-191">empty</span></span> | |
| <span data-ttu-id="fa257-192">Repozytorium/adres URL</span><span class="sxs-lookup"><span data-stu-id="fa257-192">Repository/Url</span></span> | <span data-ttu-id="fa257-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-193">RepositoryUrl</span></span> | <span data-ttu-id="fa257-194">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-194">empty</span></span> | <span data-ttu-id="fa257-195">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="fa257-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="fa257-196">Przyklad *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="fa257-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="fa257-197">Repozytorium/typ</span><span class="sxs-lookup"><span data-stu-id="fa257-197">Repository/Type</span></span> | <span data-ttu-id="fa257-198">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="fa257-198">RepositoryType</span></span> | <span data-ttu-id="fa257-199">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-199">empty</span></span> | <span data-ttu-id="fa257-200">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fa257-200">Repository type.</span></span> <span data-ttu-id="fa257-201">Przykłady: *git*i *TFS*.</span><span class="sxs-lookup"><span data-stu-id="fa257-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="fa257-202">Repozytorium/gałąź</span><span class="sxs-lookup"><span data-stu-id="fa257-202">Repository/Branch</span></span> | <span data-ttu-id="fa257-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="fa257-203">RepositoryBranch</span></span> | <span data-ttu-id="fa257-204">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-204">empty</span></span> | <span data-ttu-id="fa257-205">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fa257-205">Optional repository branch information.</span></span> <span data-ttu-id="fa257-206">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="fa257-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fa257-207">Przykład: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="fa257-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fa257-208">Repozytorium/zatwierdzenie</span><span class="sxs-lookup"><span data-stu-id="fa257-208">Repository/Commit</span></span> | <span data-ttu-id="fa257-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="fa257-209">RepositoryCommit</span></span> | <span data-ttu-id="fa257-210">empty</span><span class="sxs-lookup"><span data-stu-id="fa257-210">empty</span></span> | <span data-ttu-id="fa257-211">Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="fa257-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="fa257-212">Aby można było uwzględnić tę właściwość, należy również określić *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="fa257-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fa257-213">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="fa257-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fa257-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="fa257-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="fa257-215">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fa257-215">Summary</span></span> | <span data-ttu-id="fa257-216">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="fa257-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="fa257-217">docelowe dane wejściowe pakietu</span><span class="sxs-lookup"><span data-stu-id="fa257-217">pack target inputs</span></span>

- <span data-ttu-id="fa257-218">Ispacking</span><span class="sxs-lookup"><span data-stu-id="fa257-218">IsPackable</span></span>
- <span data-ttu-id="fa257-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="fa257-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="fa257-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fa257-220">PackageVersion</span></span>
- <span data-ttu-id="fa257-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="fa257-221">PackageId</span></span>
- <span data-ttu-id="fa257-222">Autorzy</span><span class="sxs-lookup"><span data-stu-id="fa257-222">Authors</span></span>
- <span data-ttu-id="fa257-223">Opis</span><span class="sxs-lookup"><span data-stu-id="fa257-223">Description</span></span>
- <span data-ttu-id="fa257-224">Prawo</span><span class="sxs-lookup"><span data-stu-id="fa257-224">Copyright</span></span>
- <span data-ttu-id="fa257-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="fa257-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="fa257-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="fa257-226">DevelopmentDependency</span></span>
- <span data-ttu-id="fa257-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="fa257-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="fa257-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="fa257-228">PackageLicenseFile</span></span>
- <span data-ttu-id="fa257-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="fa257-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-230">PackageProjectUrl</span></span>
- <span data-ttu-id="fa257-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-231">PackageIconUrl</span></span>
- <span data-ttu-id="fa257-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fa257-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="fa257-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fa257-233">PackageTags</span></span>
- <span data-ttu-id="fa257-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="fa257-234">PackageOutputPath</span></span>
- <span data-ttu-id="fa257-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="fa257-235">IncludeSymbols</span></span>
- <span data-ttu-id="fa257-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="fa257-236">IncludeSource</span></span>
- <span data-ttu-id="fa257-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="fa257-237">PackageTypes</span></span>
- <span data-ttu-id="fa257-238">Istool</span><span class="sxs-lookup"><span data-stu-id="fa257-238">IsTool</span></span>
- <span data-ttu-id="fa257-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-239">RepositoryUrl</span></span>
- <span data-ttu-id="fa257-240">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="fa257-240">RepositoryType</span></span>
- <span data-ttu-id="fa257-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="fa257-241">RepositoryBranch</span></span>
- <span data-ttu-id="fa257-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="fa257-242">RepositoryCommit</span></span>
- <span data-ttu-id="fa257-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="fa257-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="fa257-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="fa257-244">MinClientVersion</span></span>
- <span data-ttu-id="fa257-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fa257-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="fa257-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="fa257-246">IncludeContentInPack</span></span>
- <span data-ttu-id="fa257-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="fa257-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="fa257-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="fa257-248">ContentTargetFolders</span></span>
- <span data-ttu-id="fa257-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="fa257-249">NuspecFile</span></span>
- <span data-ttu-id="fa257-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="fa257-250">NuspecBasePath</span></span>
- <span data-ttu-id="fa257-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="fa257-251">NuspecProperties</span></span>
- <span data-ttu-id="fa257-252">Deterministyczne</span><span class="sxs-lookup"><span data-stu-id="fa257-252">Deterministic</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="fa257-253">scenariusze dotyczące pakietów</span><span class="sxs-lookup"><span data-stu-id="fa257-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="fa257-254">Pomiń zależności</span><span class="sxs-lookup"><span data-stu-id="fa257-254">Suppress dependencies</span></span>

<span data-ttu-id="fa257-255">Aby pominąć zależności pakietów z wygenerowanego pakietu NuGet `SuppressDependenciesWhenPacking` , `true` ustaw opcję na, która będzie zezwalać na pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.</span><span class="sxs-lookup"><span data-stu-id="fa257-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="fa257-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="fa257-256">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="fa257-257">PackageIconUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="fa257-257">PackageIconUrl is deprecated.</span></span> <span data-ttu-id="fa257-258">Zamiast tego użyj [PackageIcon](#packing-an-icon-image-file) .</span><span class="sxs-lookup"><span data-stu-id="fa257-258">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="fa257-259">Pakowanie pliku obrazu ikony</span><span class="sxs-lookup"><span data-stu-id="fa257-259">Packing an icon image file</span></span>

<span data-ttu-id="fa257-260">Podczas pakowania pliku obrazu ikony należy użyć właściwości PackageIcon, aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-260">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="fa257-261">Ponadto należy się upewnić, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-261">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="fa257-262">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="fa257-262">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="fa257-263">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="fa257-263">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="fa257-264">Zalecamy rozdzielczość obrazu 64x64.</span><span class="sxs-lookup"><span data-stu-id="fa257-264">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="fa257-265">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="fa257-265">For example:</span></span>

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

<span data-ttu-id="fa257-266">[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="fa257-266">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="fa257-267">Aby uzyskać odpowiedniki nuspec, zapoznaj się z tematem [nuspec Reference dla ikony](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="fa257-267">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="fa257-268">Zestawy wyjściowe</span><span class="sxs-lookup"><span data-stu-id="fa257-268">Output assemblies</span></span>

<span data-ttu-id="fa257-269">`nuget pack`Kopiuje pliki `.exe`wyjściowe z rozszerzeniami `.dll` `.xml`, `.winmd` `.pri`,,, i. `.json`</span><span class="sxs-lookup"><span data-stu-id="fa257-269">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="fa257-270">Pliki wyjściowe, które są kopiowane, zależą od tego, co `BuiltOutputProjectGroup` program MSBuild dostarcza z elementu docelowego.</span><span class="sxs-lookup"><span data-stu-id="fa257-270">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="fa257-271">Istnieją dwie właściwości programu MSBuild, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie znajdują się zestawy wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="fa257-271">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="fa257-272">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="fa257-272">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="fa257-273">`BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="fa257-273">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="fa257-274">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="fa257-274">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="fa257-275">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="fa257-275">Package references</span></span>

<span data-ttu-id="fa257-276">Zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="fa257-276">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="fa257-277">Odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="fa257-277">Project to project references</span></span>

<span data-ttu-id="fa257-278">Odwołania projektu do projektu są traktowane domyślnie jako odwołania do pakietów NuGet, na przykład:</span><span class="sxs-lookup"><span data-stu-id="fa257-278">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="fa257-279">Możesz również dodać następujące metadane do odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="fa257-279">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="deterministic"></a><span data-ttu-id="fa257-280">Deterministyczne</span><span class="sxs-lookup"><span data-stu-id="fa257-280">Deterministic</span></span>

<span data-ttu-id="fa257-281">W przypadku `MSBuild -t:pack -p:Deterministic=true`użycia, wielokrotne wywołania obiektu docelowego pakietu wygenerują dokładnie ten sam pakiet.</span><span class="sxs-lookup"><span data-stu-id="fa257-281">When using `MSBuild -t:pack -p:Deterministic=true`, multiple invocations of the the pack target will generate the exact same package.</span></span>
<span data-ttu-id="fa257-282">W danych wyjściowych polecenia pakowania nie ma wpływ stan otoczenia maszyny.</span><span class="sxs-lookup"><span data-stu-id="fa257-282">The output of the pack command is not affected by the ambient state of the machine.</span></span> <span data-ttu-id="fa257-283">W przypadku wpisów zip zostaną wpisane sygnatury czasowe jako 1980-01-01.</span><span class="sxs-lookup"><span data-stu-id="fa257-283">Specifically zip entries will be timestamped as 1980-01-01.</span></span> <span data-ttu-id="fa257-284">Aby osiągnąć pełną, należy skompilować zestawy z odpowiednią opcją kompilatora [-deterministyczną](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="fa257-284">To achieve full determinism, the assemblies should be built with the respective compiler option [-deterministic](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span></span>
<span data-ttu-id="fa257-285">Zaleca się, aby określić właściwość deterministyczną, taką jak następująca, więc zarówno kompilator, jak i NuGet porespektują ten element.</span><span class="sxs-lookup"><span data-stu-id="fa257-285">It is recommended that you specify the deterministic property like following, so both the compiler and NuGet will respect it.</span></span>

```xml
<PropertyGroup>
  <Deterministic>true</Deterministic>
</PropertyGroup>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="fa257-286">Dołączanie zawartości do pakietu</span><span class="sxs-lookup"><span data-stu-id="fa257-286">Including content in a package</span></span>

<span data-ttu-id="fa257-287">Aby dołączyć zawartość, Dodaj dodatkowe metadane do istniejącego `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="fa257-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="fa257-288">Domyślnie wszystkie elementy typu "Content" są uwzględniane w pakiecie, chyba że przestąpisz do wpisów, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="fa257-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="fa257-289">Domyślnie wszystko jest dodawane do katalogu głównego `content` folderu i `contentFiles\any\<target_framework>` w pakiecie i zachowuje względną strukturę folderów, chyba że zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="fa257-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="fa257-290">Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (a nie `content` `contentFiles` obu), możesz użyć właściwości `ContentTargetFolders`programu MSBuild, która jest wartością domyślną "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="fa257-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="fa257-291">Należy pamiętać, że po prostu określenie " `ContentTargetFolders` contentFiles" w `contentFiles\any\<target_framework>` umieszcza plików w `buildAction`obszarze lub `contentFiles\<language>\<target_framework>` na podstawie.</span><span class="sxs-lookup"><span data-stu-id="fa257-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="fa257-292">`PackagePath`może to być rozdzielany średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="fa257-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="fa257-293">Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="fa257-294">Na przykład następujące polecenie dodaje `libuv.txt` do `content\myfiles`, `content\samples`i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="fa257-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="fa257-295">Istnieje również właściwość `$(IncludeContentInPack)`programu MSBuild, której `true`wartością domyślną jest.</span><span class="sxs-lookup"><span data-stu-id="fa257-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="fa257-296">Jeśli ta wartość jest ustawiona `false` na dla każdego projektu, zawartość z tego projektu nie jest dołączana do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa257-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="fa257-297">Inne metadane specyficzne dla pakietu, które można ustawić dla każdego z powyższych elementów, ```<PackageCopyToOutput>``` obejmują ```<PackageFlatten>``` i które ```CopyToOutput``` ```contentFiles``` zestawy ```Flatten``` i wartości wpisu w danych wyjściowych nuspec.</span><span class="sxs-lookup"><span data-stu-id="fa257-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="fa257-298">Oprócz elementów `<Pack>` zawartości można również ustawić metadane `<PackagePath>` i dla plików z akcją kompilacji kompilowania, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="fa257-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="fa257-299">Aby pakiet mógł dołączyć nazwę pliku do ścieżki pakietu przy użyciu wzorców obsługi symboli wieloznacznych, ścieżka pakietu musi kończyć się znakiem separatora folderów. w przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka, w tym nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="fa257-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="fa257-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="fa257-300">IncludeSymbols</span></span>

<span data-ttu-id="fa257-301">W przypadku `MSBuild -t:pack -p:IncludeSymbols=true`korzystania z programu `.pdb` odpowiednie pliki są kopiowane wraz z innymi `.xml`plikami wyjściowymi `.exe` `.json`( `.winmd``.dll`,,, `.pri`,,).</span><span class="sxs-lookup"><span data-stu-id="fa257-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="fa257-302">Należy pamiętać, `IncludeSymbols=true` że ustawienie powoduje utworzenie regularnego pakietu *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="fa257-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="fa257-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="fa257-303">IncludeSource</span></span>

<span data-ttu-id="fa257-304">Jest to takie samo, `IncludeSymbols`jak, z tą różnicą, że kopiuje `.pdb` również pliki źródłowe wraz z plikami.</span><span class="sxs-lookup"><span data-stu-id="fa257-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="fa257-305">Wszystkie pliki typu `Compile` są kopiowane za pośrednictwem `src\<ProjectName>\` , aby zachować strukturę folderu ścieżki względnej w pakietie będącym wynikiem.</span><span class="sxs-lookup"><span data-stu-id="fa257-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="fa257-306">To samo występuje również dla plików `ProjectReference` źródłowych, które mają `TreatAsPackageReference` ustawioną wartość `false`.</span><span class="sxs-lookup"><span data-stu-id="fa257-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="fa257-307">Jeśli plik typu Kompiluj znajduje się poza folderem projektu, to właśnie został dodany do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="fa257-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="fa257-308">Pakowanie wyrażenia licencji lub pliku licencji</span><span class="sxs-lookup"><span data-stu-id="fa257-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="fa257-309">W przypadku korzystania z wyrażenia licencji Właściwość PackageLicenseExpression powinna zostać użyta.</span><span class="sxs-lookup"><span data-stu-id="fa257-309">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="fa257-310">[Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="fa257-310">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="fa257-311">[Dowiedz się więcej na temat wyrażeń licencji i licencji akceptowanych przez NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="fa257-311">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="fa257-312">Podczas pakowania pliku licencji należy użyć właściwości PackageLicenseFile, aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-312">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="fa257-313">Ponadto należy się upewnić, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-313">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="fa257-314">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="fa257-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="fa257-315">[Przykład pliku licencji](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="fa257-315">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="fa257-316">Istool</span><span class="sxs-lookup"><span data-stu-id="fa257-316">IsTool</span></span>

<span data-ttu-id="fa257-317">W przypadku `MSBuild -t:pack -p:IsTool=true`korzystania z programu wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , `tools` są kopiowane do folderu `lib` , a nie do folderu.</span><span class="sxs-lookup"><span data-stu-id="fa257-317">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="fa257-318">Należy zauważyć, że różni się to `DotNetCliTool` od elementu, który jest określony `PackageType` przez `.csproj` ustawienie w pliku.</span><span class="sxs-lookup"><span data-stu-id="fa257-318">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="fa257-319">Pakowanie przy użyciu elementu. nuspec</span><span class="sxs-lookup"><span data-stu-id="fa257-319">Packing using a .nuspec</span></span>

<span data-ttu-id="fa257-320">Mimo że zaleca się [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu, można użyć `.nuspec` pliku do spakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="fa257-320">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="fa257-321">W przypadku projektu typu innego niż zestaw SDK, który `PackageReference`używa programu, należy `NuGet.Build.Tasks.Pack.targets` go zaimportować, aby można było wykonać zadanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-321">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="fa257-322">Nadal trzeba przywrócić projekt, aby można było spakować plik NUSPEC.</span><span class="sxs-lookup"><span data-stu-id="fa257-322">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="fa257-323">(Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).</span><span class="sxs-lookup"><span data-stu-id="fa257-323">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="fa257-324">Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania nuspec.</span><span class="sxs-lookup"><span data-stu-id="fa257-324">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="fa257-325">Następujące trzy właściwości programu MSBuild dotyczą pakowania przy użyciu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="fa257-325">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="fa257-326">`NuspecFile`: względna lub bezwzględna `.nuspec` ścieżka do pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="fa257-326">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="fa257-327">`NuspecProperties`: rozdzielana średnikami lista par klucz = wartość.</span><span class="sxs-lookup"><span data-stu-id="fa257-327">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="fa257-328">Ze względu na sposób działania analizy wiersza polecenia programu MSBuild należy określić wiele właściwości w następujący sposób: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="fa257-328">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="fa257-329">`NuspecBasePath`: Podstawowa ścieżka do `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="fa257-329">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="fa257-330">Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fa257-330">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fa257-331">Jeśli używasz programu MSBuild do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fa257-331">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fa257-332">Należy pamiętać, że pakowanie nuspec przy użyciu programu dotnet. exe lub MSBuild również prowadzi do domyślnego kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="fa257-332">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="fa257-333">Można to uniknąć przez przekazanie ```--no-build``` właściwości do programu dotnet. exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="fa257-333">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="fa257-334">Przykład pliku *. csproj* do spakowania pliku nuspec jest:</span><span class="sxs-lookup"><span data-stu-id="fa257-334">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="fa257-335">Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="fa257-335">Advanced extension points to create customized package</span></span>

<span data-ttu-id="fa257-336">`pack` Element docelowy zawiera dwa punkty rozszerzenia, które są uruchamiane w wewnętrznej, docelowej kompilacji specyficznej dla platformy.</span><span class="sxs-lookup"><span data-stu-id="fa257-336">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="fa257-337">Obsługa punktów rozszerzenia umożliwia uwzględnienie zawartości i zestawów określonych dla platformy docelowej w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="fa257-337">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="fa257-338">`TargetsForTfmSpecificBuildOutput`obiektów Używane dla plików wewnątrz `lib` folderu lub folderu określonego przy użyciu. `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="fa257-338">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="fa257-339">`TargetsForTfmSpecificContentInPackage`obiektów Używane dla plików poza programem `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="fa257-339">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="fa257-340">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fa257-340">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="fa257-341">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa257-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="fa257-342">Dla wszystkich plików, które muszą przejść `BuildOutputTargetFolder` do (domyślnie lib), obiekt docelowy powinien zapisać te pliki do obiektu `BuildOutputInPackage` Items i ustawić następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="fa257-342">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="fa257-343">`FinalOutputPath`: Ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość służy do oszacowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="fa257-343">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="fa257-344">`TargetPath`:  Obowiązkowe Ustaw, gdy plik musi przejść do podfolderu w `lib\<TargetFramework>` , podobnie jak zestawy satelickie, które przechodzą w odpowiednie foldery kultury.</span><span class="sxs-lookup"><span data-stu-id="fa257-344">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="fa257-345">Wartością domyślną jest nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="fa257-345">Defaults to the name of the file.</span></span>

<span data-ttu-id="fa257-346">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fa257-346">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="fa257-347">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="fa257-347">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="fa257-348">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa257-348">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="fa257-349">Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki `TfmSpecificPackageFile` w obiekcie Items i ustawić następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="fa257-349">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="fa257-350">`PackagePath`: Ścieżka, w której plik powinien być wyprowadzany w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="fa257-350">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="fa257-351">Pakiet NuGet wystawia ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-351">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="fa257-352">`BuildAction`: Akcja kompilacji, która ma zostać przypisana do pliku, wymagana tylko wtedy, gdy ścieżka pakietu `contentFiles` znajduje się w folderze.</span><span class="sxs-lookup"><span data-stu-id="fa257-352">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="fa257-353">Wartość domyślna to "none".</span><span class="sxs-lookup"><span data-stu-id="fa257-353">Defaults to "None".</span></span>

<span data-ttu-id="fa257-354">Przykład:</span><span class="sxs-lookup"><span data-stu-id="fa257-354">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="fa257-355">Przywróć miejsce docelowe</span><span class="sxs-lookup"><span data-stu-id="fa257-355">restore target</span></span>

<span data-ttu-id="fa257-356">`MSBuild -t:restore`(które `nuget restore` `dotnet restore` są używane z projektami .NET Core), przywraca pakiety, do których odwołuje się plik projektu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa257-356">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="fa257-357">Odczytuj wszystkie odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="fa257-357">Read all project to project references</span></span>
1. <span data-ttu-id="fa257-358">Odczytywanie właściwości projektu w celu znalezienia pośredniego folderu i platform docelowych</span><span class="sxs-lookup"><span data-stu-id="fa257-358">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="fa257-359">Przekaż dane programu MSBuild do pliku NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="fa257-359">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="fa257-360">Uruchom przywracanie</span><span class="sxs-lookup"><span data-stu-id="fa257-360">Run restore</span></span>
1. <span data-ttu-id="fa257-361">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="fa257-361">Download packages</span></span>
1. <span data-ttu-id="fa257-362">Zapisz plik zasobów, cele i właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa257-362">Write assets file, targets, and props</span></span>

<span data-ttu-id="fa257-363">Obiekt docelowy działa tylko w przypadku projektów korzystających z formatu PackageReference. `restore`</span><span class="sxs-lookup"><span data-stu-id="fa257-363">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="fa257-364">**Nie działa w** przypadku projektów przy użyciu `packages.config` formatu; zamiast tego należy użyć [przywracania NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="fa257-364">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="fa257-365">Właściwości przywracania</span><span class="sxs-lookup"><span data-stu-id="fa257-365">Restore properties</span></span>

<span data-ttu-id="fa257-366">Dodatkowe ustawienia przywracania mogą pochodzić z właściwości programu MSBuild w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="fa257-366">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="fa257-367">Wartości można również ustawić z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="fa257-367">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="fa257-368">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fa257-368">Property</span></span> | <span data-ttu-id="fa257-369">Opis</span><span class="sxs-lookup"><span data-stu-id="fa257-369">Description</span></span> |
|--------|--------|
| <span data-ttu-id="fa257-370">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="fa257-370">RestoreSources</span></span> | <span data-ttu-id="fa257-371">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="fa257-371">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="fa257-372">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="fa257-372">RestorePackagesPath</span></span> | <span data-ttu-id="fa257-373">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa257-373">User packages folder path.</span></span> |
| <span data-ttu-id="fa257-374">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="fa257-374">RestoreDisableParallel</span></span> | <span data-ttu-id="fa257-375">Ogranicz pobieranie do jednej naraz.</span><span class="sxs-lookup"><span data-stu-id="fa257-375">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="fa257-376">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="fa257-376">RestoreConfigFile</span></span> | <span data-ttu-id="fa257-377">Ścieżka do `Nuget.Config` pliku, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="fa257-377">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="fa257-378">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="fa257-378">RestoreNoCache</span></span> | <span data-ttu-id="fa257-379">Jeśli ma wartość true, unika używania buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="fa257-379">If true, avoids using cached packages.</span></span> <span data-ttu-id="fa257-380">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa257-380">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="fa257-381">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="fa257-381">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="fa257-382">W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="fa257-382">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="fa257-383">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="fa257-383">RestoreFallbackFolders</span></span> | <span data-ttu-id="fa257-384">Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fa257-384">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="fa257-385">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="fa257-385">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="fa257-386">Dodatkowe źródła do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="fa257-386">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="fa257-387">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="fa257-387">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="fa257-388">Dodatkowe foldery rezerwowe do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="fa257-388">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="fa257-389">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="fa257-389">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="fa257-390">Wyklucza foldery rezerwowe określone w`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="fa257-390">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="fa257-391">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="fa257-391">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="fa257-392">Ścieżka do `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="fa257-392">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="fa257-393">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="fa257-393">RestoreGraphProjectInput</span></span> | <span data-ttu-id="fa257-394">Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="fa257-394">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="fa257-395">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="fa257-395">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="fa257-396">Gdy projekty są zbierane za pośrednictwem programu `SkipNonexistentTargets` MSBuild, określa, czy są zbierane przy użyciu optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="fa257-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="fa257-397">Gdy wartość nie jest ustawiona, `true`wartością domyślną jest.</span><span class="sxs-lookup"><span data-stu-id="fa257-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="fa257-398">Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu.</span><span class="sxs-lookup"><span data-stu-id="fa257-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="fa257-399">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="fa257-399">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="fa257-400">Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` `obj` i folder.</span><span class="sxs-lookup"><span data-stu-id="fa257-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="fa257-401">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fa257-401">Examples</span></span>

<span data-ttu-id="fa257-402">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="fa257-402">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="fa257-403">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="fa257-403">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="fa257-404">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="fa257-404">Restore outputs</span></span>

<span data-ttu-id="fa257-405">Instrukcja RESTORE tworzy następujące pliki w folderze Build `obj` :</span><span class="sxs-lookup"><span data-stu-id="fa257-405">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="fa257-406">Plik</span><span class="sxs-lookup"><span data-stu-id="fa257-406">File</span></span> | <span data-ttu-id="fa257-407">Opis</span><span class="sxs-lookup"><span data-stu-id="fa257-407">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="fa257-408">Zawiera wykres zależności wszystkich odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="fa257-408">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="fa257-409">Odwołania do właściwości programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="fa257-409">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="fa257-410">Odwołania do elementów docelowych programu MSBuild zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="fa257-410">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="fa257-411">Przywracanie i kompilowanie za pomocą jednego polecenia MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa257-411">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="fa257-412">Ze względu na fakt, że pakiet NuGet może przywrócić pakiety, które wyłączają elementy docelowe i właściwości programu MSBuild, a oceny przywracania i kompilacji są uruchamiane z różnymi właściwośćmi globalnymi.</span><span class="sxs-lookup"><span data-stu-id="fa257-412">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="fa257-413">Oznacza to, że następujące elementy będą miały nieprzewidywalne i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="fa257-413">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="fa257-414">Zamiast tego zalecane podejście to:</span><span class="sxs-lookup"><span data-stu-id="fa257-414">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="fa257-415">Ta sama logika ma zastosowanie do innych obiektów `build`docelowych podobnych do.</span><span class="sxs-lookup"><span data-stu-id="fa257-415">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="fa257-416">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="fa257-416">PackageTargetFallback</span></span>

<span data-ttu-id="fa257-417">`PackageTargetFallback` Element umożliwia określenie zestawu zgodnych elementów docelowych, które mają być używane podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="fa257-417">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="fa257-418">Została zaprojektowana tak, aby zezwalać na pakiety, które używają [TxM](../reference/target-frameworks.md) dotnet, do pracy z zgodnymi pakietami, które nie deklarują TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="fa257-418">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="fa257-419">Oznacza to, że jeśli w projekcie jest używany TxM dotnet, wszystkie pakiety, od których zależy, muszą także mieć TxM dotnet, chyba że zostanie dodany `<PackageTargetFallback>` do projektu w celu umożliwienia zgodności z platformą dotnet.</span><span class="sxs-lookup"><span data-stu-id="fa257-419">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="fa257-420">Na przykład jeśli projekt używa `netstandard1.6` TxM, a pakiet zależny zawiera tylko `lib/net45/a.dll` i `lib/portable-net45+win81/a.dll`, to projekt nie zostanie skompilowany.</span><span class="sxs-lookup"><span data-stu-id="fa257-420">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="fa257-421">Jeśli co chcesz zrobić, jest to Ostatnia Biblioteka DLL, a następnie możesz dodać `PackageTargetFallback` polecenie w następujący sposób, aby powiedzieć, `portable-net45+win81` że biblioteka DLL jest zgodna:</span><span class="sxs-lookup"><span data-stu-id="fa257-421">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="fa257-422">Aby zadeklarować rezerwę dla wszystkich obiektów docelowych w projekcie, pozostaw ten `Condition` atrybut.</span><span class="sxs-lookup"><span data-stu-id="fa257-422">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="fa257-423">Możesz również rozłożyć wszystkie istniejące `PackageTargetFallback` , w `$(PackageTargetFallback)` tym tutaj, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="fa257-423">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="fa257-424">Zastępowanie jednej biblioteki na podstawie grafu przywracania</span><span class="sxs-lookup"><span data-stu-id="fa257-424">Replacing one library from a restore graph</span></span>

<span data-ttu-id="fa257-425">Jeśli przywracanie powoduje przełączenie niewłaściwego zestawu, możliwe jest wykluczenie domyślnego wyboru pakietów i zamienienie go na własny wybór.</span><span class="sxs-lookup"><span data-stu-id="fa257-425">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="fa257-426">Najpierw należy wykluczyć wszystkie elementy `PackageReference`zawartości z najwyższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="fa257-426">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="fa257-427">Następnie Dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="fa257-427">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
