---
title: NuGet Pakowanie i przywracanie jako MSBuild elementy docelowe
description: NuGet Pakowanie i przywracanie może współdziałać bezpośrednio jako MSBuild elementy docelowe z NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858969"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="4e1be-103">NuGet Pakowanie i przywracanie jako MSBuild elementy docelowe</span><span class="sxs-lookup"><span data-stu-id="4e1be-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="4e1be-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="4e1be-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="4e1be-105">W formacie [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, a nie przy użyciu osobnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="4e1be-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="4e1be-106">MSBuild15.1 +, NuGet jest również MSBuild obywatelem pierwszej klasy z `pack` i celami, zgodnie z `restore` poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="4e1be-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="4e1be-107">Te elementy docelowe umożliwiają współdziałanie z NuGet innymi MSBuild zadaniami lub obiektami docelowymi.</span><span class="sxs-lookup"><span data-stu-id="4e1be-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="4e1be-108">Aby uzyskać instrukcje tworzenia NuGet pakietu przy użyciu programu MSBuild , zobacz [Tworzenie NuGet pakietu MSBuild przy użyciu ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="4e1be-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="4e1be-109">(W przypadku NuGet 3. x i starszych, zamiast tego należy użyć poleceń [pakowanie](../reference/cli-reference/cli-ref-pack.md) i [przywracanie](../reference/cli-reference/cli-ref-restore.md) za pomocą NuGet interfejsu wiersza polecenia.)</span><span class="sxs-lookup"><span data-stu-id="4e1be-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="4e1be-110">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="4e1be-110">Target build order</span></span>

<span data-ttu-id="4e1be-111">Ponieważ `pack` i `restore` są  MSBuild obiektami docelowymi, można uzyskać do nich dostęp, aby usprawnić przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="4e1be-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="4e1be-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="4e1be-113">Można to zrobić, dodając następujący plik w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="4e1be-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="4e1be-114">Podobnie można napisać MSBuild zadanie, napisać własne miejsce docelowe i użyć NuGet właściwości w MSBuild zadaniu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="4e1be-115">`$(OutputPath)` jest względna i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="4e1be-116">cel pakietu</span><span class="sxs-lookup"><span data-stu-id="4e1be-116">pack target</span></span>

<span data-ttu-id="4e1be-117">W przypadku projektów platformy .NET korzystających z tego `PackageReference` formatu użycie `msbuild -t:pack` rysuje dane wejściowe z pliku projektu do użycia podczas tworzenia NuGet pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="4e1be-118">W poniższej tabeli opisano MSBuild właściwości, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle.</span><span class="sxs-lookup"><span data-stu-id="4e1be-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="4e1be-119">Można je łatwo edytować w programie Visual Studio 2017 i później, klikając prawym przyciskiem myszy projekt i wybierając pozycję **Edytuj {Project_Name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="4e1be-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="4e1be-120">Dla wygody tabela jest zorganizowana według równoważnej właściwości w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="4e1be-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4e1be-121">`Owners` i `Summary` właściwości z `.nuspec` nie są obsługiwane w programie MSBuild .</span><span class="sxs-lookup"><span data-stu-id="4e1be-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="4e1be-122">Atrybut/ nuspec wartość</span><span class="sxs-lookup"><span data-stu-id="4e1be-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="4e1be-123">MSBuild Wartość</span><span class="sxs-lookup"><span data-stu-id="4e1be-123">MSBuild Property</span></span> | <span data-ttu-id="4e1be-124">Domyślne</span><span class="sxs-lookup"><span data-stu-id="4e1be-124">Default</span></span> | <span data-ttu-id="4e1be-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4e1be-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="4e1be-126">`$(AssemblyName)` wniosek MSBuild</span><span class="sxs-lookup"><span data-stu-id="4e1be-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="4e1be-127">Wersja</span><span class="sxs-lookup"><span data-stu-id="4e1be-127">Version</span></span> | <span data-ttu-id="4e1be-128">Jest to zgodne z semver, na przykład, `1.0.0` `1.0.0-beta` lub `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="4e1be-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="4e1be-129">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-129">empty</span></span> | <span data-ttu-id="4e1be-130">Ustawianie `PackageVersion` zastępowanie `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="4e1be-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="4e1be-131">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-131">empty</span></span> | <span data-ttu-id="4e1be-132">`$(VersionSuffix)` z programu MSBuild .</span><span class="sxs-lookup"><span data-stu-id="4e1be-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="4e1be-133">Ustawianie `PackageVersion` zastępowanie `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="4e1be-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="4e1be-134">Nazwa_użytkownika bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="4e1be-134">Username of the current user</span></span> | <span data-ttu-id="4e1be-135">Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów w nuget.org. Są one wyświetlane w NuGet galerii w witrynie NuGet.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="4e1be-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="4e1be-136">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="4e1be-136">N/A</span></span> | <span data-ttu-id="4e1be-137">Nieobecne w nuspec</span><span class="sxs-lookup"><span data-stu-id="4e1be-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="4e1be-138">Element `PackageId`.</span><span class="sxs-lookup"><span data-stu-id="4e1be-138">The `PackageId`</span></span> | <span data-ttu-id="4e1be-139">Przyjazny dla człowieka tytuł pakietu, zazwyczaj używany w interfejsie użytkownika jako nuget.org i Menedżer pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e1be-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="4e1be-140">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="4e1be-140">"Package Description"</span></span> | <span data-ttu-id="4e1be-141">Długi opis zestawu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-141">A long description for the assembly.</span></span> <span data-ttu-id="4e1be-142">Jeśli `PackageDescription` nie jest określony, ta właściwość jest również używana jako Opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="4e1be-143">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-143">empty</span></span> | <span data-ttu-id="4e1be-144">Szczegóły dotyczące praw autorskich pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="4e1be-145">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="4e1be-146">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-146">empty</span></span> | <span data-ttu-id="4e1be-147">Odnosi się do `<license type="expression">` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="4e1be-148">Zobacz [pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="4e1be-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="4e1be-149">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-149">empty</span></span> | <span data-ttu-id="4e1be-150">Ścieżka do pliku licencji w pakiecie w przypadku korzystania z licencji niestandardowej lub licencji, która nie ma przypisanego identyfikatora SPDX.</span><span class="sxs-lookup"><span data-stu-id="4e1be-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="4e1be-151">Należy jawnie spakować plik licencji, do której istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="4e1be-152">Odnosi się do `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="4e1be-153">Zobacz [pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="4e1be-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="4e1be-154">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-154">empty</span></span> | <span data-ttu-id="4e1be-155">`PackageLicenseUrl` jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="4e1be-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4e1be-156">Użyj polecenia `PackageLicenseExpression` or `PackageLicenseFile` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="4e1be-157">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="4e1be-158">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-158">empty</span></span> | <span data-ttu-id="4e1be-159">Ścieżka do obrazu w pakiecie do użycia jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="4e1be-160">Należy jawnie spakować plik obrazu ikony, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="4e1be-161">Aby uzyskać więcej informacji, zobacz [pakowanie pliku obrazu ikony](#packing-an-icon-image-file) i [ `icon` metadanych](/nuget/reference/nuspec#icon).</span><span class="sxs-lookup"><span data-stu-id="4e1be-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="4e1be-162">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-162">empty</span></span> | <span data-ttu-id="4e1be-163">`PackageIconUrl` jest przestarzały `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="4e1be-164">Jednak w przypadku najlepszego środowiska niskiego poziomu należy określić `PackageIconUrl` oprócz `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Tags` | `PackageTags` | <span data-ttu-id="4e1be-165">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-165">empty</span></span> | <span data-ttu-id="4e1be-166">Rozdzielana średnikami lista znaczników, które wyznaczają pakiet.</span><span class="sxs-lookup"><span data-stu-id="4e1be-166">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="4e1be-167">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-167">empty</span></span> | <span data-ttu-id="4e1be-168">Informacje o wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-168">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="4e1be-169">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-169">empty</span></span> | <span data-ttu-id="4e1be-170">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="4e1be-170">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4e1be-171">Przykład: *https://github.com/ NuGet / NuGet . Klient. git*.</span><span class="sxs-lookup"><span data-stu-id="4e1be-171">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="4e1be-172">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-172">empty</span></span> | <span data-ttu-id="4e1be-173">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="4e1be-173">Repository type.</span></span> <span data-ttu-id="4e1be-174">Przykłady: `git` (domyślnie), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-174">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="4e1be-175">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-175">empty</span></span> | <span data-ttu-id="4e1be-176">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="4e1be-176">Optional repository branch information.</span></span> <span data-ttu-id="4e1be-177">`RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona.</span><span class="sxs-lookup"><span data-stu-id="4e1be-177">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e1be-178">Przykład: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4e1be-178">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="4e1be-179">puste</span><span class="sxs-lookup"><span data-stu-id="4e1be-179">empty</span></span> | <span data-ttu-id="4e1be-180">Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="4e1be-180">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4e1be-181">`RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona.</span><span class="sxs-lookup"><span data-stu-id="4e1be-181">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e1be-182">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4e1be-182">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="4e1be-183">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="4e1be-183">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="4e1be-184">docelowe dane wejściowe pakietu</span><span class="sxs-lookup"><span data-stu-id="4e1be-184">pack target inputs</span></span>

| <span data-ttu-id="4e1be-185">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e1be-185">Property</span></span> | <span data-ttu-id="4e1be-186">Opis</span><span class="sxs-lookup"><span data-stu-id="4e1be-186">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="4e1be-187">Wartość logiczna określająca, czy projekt może być spakowany.</span><span class="sxs-lookup"><span data-stu-id="4e1be-187">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="4e1be-188">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="4e1be-188">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="4e1be-189">Ustaw, aby `true` pominąć zależności pakietów z wygenerowanego NuGet pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-189">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="4e1be-190">Określa wersję, która będzie miała pakiet otrzymany.</span><span class="sxs-lookup"><span data-stu-id="4e1be-190">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="4e1be-191">Akceptuje wszystkie formy NuGet ciągu wersji.</span><span class="sxs-lookup"><span data-stu-id="4e1be-191">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="4e1be-192">Wartość domyślna to `$(Version)` , czyli Właściwość `Version` w projekcie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-192">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="4e1be-193">Określa nazwę pakietu, który ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="4e1be-193">Specifies the name for the resulting package.</span></span> <span data-ttu-id="4e1be-194">Jeśli nie zostanie określony, `pack` operacja będzie domyślnie używać `AssemblyName` nazwy katalogu jako nazwy pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-194">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="4e1be-195">Długi opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4e1be-195">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="4e1be-196">Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów w nuget.org. Są one wyświetlane w NuGet galerii w witrynie NuGet.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="4e1be-196">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="4e1be-197">Długi opis zestawu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-197">A long description for the assembly.</span></span> <span data-ttu-id="4e1be-198">Jeśli `PackageDescription` nie jest określony, ta właściwość jest również używana jako Opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-198">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="4e1be-199">Szczegóły dotyczące praw autorskich pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-199">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="4e1be-200">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-200">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="4e1be-201">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="4e1be-201">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="4e1be-202">Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do programowania, który uniemożliwia dołączenie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="4e1be-202">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="4e1be-203">W przypadku `PackageReference` ( NuGet 4.8 +) Ta flaga oznacza również, że zasoby czasu kompilacji są wyłączone z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="4e1be-203">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="4e1be-204">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="4e1be-204">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="4e1be-205">Identyfikator lub wyrażenie [licencji SPDX](https://spdx.org/licenses/) , na przykład `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-205">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="4e1be-206">Aby uzyskać więcej informacji, zobacz [pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="4e1be-206">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="4e1be-207">Ścieżka do pliku licencji w pakiecie w przypadku korzystania z licencji niestandardowej lub licencji, która nie ma przypisanego identyfikatora SPDX.</span><span class="sxs-lookup"><span data-stu-id="4e1be-207">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="4e1be-208">`PackageLicenseUrl` jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="4e1be-208">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="4e1be-209">Użyj polecenia `PackageLicenseExpression` or `PackageLicenseFile` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-209">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="4e1be-210">Określa ścieżkę ikony pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-210">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="4e1be-211">Aby uzyskać więcej informacji, zobacz [pakowanie pliku obrazu ikony](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="4e1be-211">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="4e1be-212">Informacje o wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-212">Release notes for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="4e1be-213">Rozdzielana średnikami lista znaczników, które wyznaczają pakiet.</span><span class="sxs-lookup"><span data-stu-id="4e1be-213">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="4e1be-214">Określa ścieżkę wyjściową, w której zostanie usunięty spakowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="4e1be-214">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="4e1be-215">Wartość domyślna to `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="4e1be-215">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="4e1be-216">Ta wartość logiczna wskazuje, czy pakiet powinien utworzyć dodatkowy pakiet symboli podczas pakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-216">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="4e1be-217">Format pakietu symboli jest kontrolowany przez `SymbolPackageFormat` Właściwość.</span><span class="sxs-lookup"><span data-stu-id="4e1be-217">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="4e1be-218">Aby uzyskać więcej informacji, zobacz [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="4e1be-218">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="4e1be-219">Ta wartość logiczna wskazuje, czy proces pakietu powinien utworzyć pakiet źródłowy.</span><span class="sxs-lookup"><span data-stu-id="4e1be-219">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="4e1be-220">Pakiet źródłowy zawiera kod źródłowy biblioteki, a także pliki PDB.</span><span class="sxs-lookup"><span data-stu-id="4e1be-220">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="4e1be-221">Pliki źródłowe są umieszczane w `src/ProjectName` katalogu w pliku pakietu, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4e1be-221">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="4e1be-222">Aby uzyskać więcej informacji, zobacz [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="4e1be-222">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="4e1be-223">Określa, czy wszystkie pliki wyjściowe są kopiowane do folderu *Tools* zamiast folderu *lib* .</span><span class="sxs-lookup"><span data-stu-id="4e1be-223">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="4e1be-224">Aby uzyskać więcej informacji, zobacz [istool](#istool).</span><span class="sxs-lookup"><span data-stu-id="4e1be-224">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="4e1be-225">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="4e1be-225">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="4e1be-226">Przykład: *https://github.com/ NuGet / NuGet . Klient. git*.</span><span class="sxs-lookup"><span data-stu-id="4e1be-226">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="4e1be-227">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="4e1be-227">Repository type.</span></span> <span data-ttu-id="4e1be-228">Przykłady: `git` (domyślnie), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-228">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="4e1be-229">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="4e1be-229">Optional repository branch information.</span></span> <span data-ttu-id="4e1be-230">`RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona.</span><span class="sxs-lookup"><span data-stu-id="4e1be-230">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e1be-231">Przykład: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4e1be-231">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="4e1be-232">Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="4e1be-232">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="4e1be-233">`RepositoryUrl` należy również określić, aby ta właściwość została uwzględniona.</span><span class="sxs-lookup"><span data-stu-id="4e1be-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="4e1be-234">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="4e1be-234">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="4e1be-235">Określa format pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="4e1be-235">Specifies the format of the symbols package.</span></span> <span data-ttu-id="4e1be-236">W przypadku wystąpienia "Symbols. nupkg" jest tworzony pakiet starszych symboli z rozszerzeniem *. Symbols. nupkg* zawierającym plików PDB, DLL i inne pliki wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4e1be-236">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="4e1be-237">W przypadku "snupkg" tworzony jest pakiet symboli snupkg zawierający przenośne plików PDB.</span><span class="sxs-lookup"><span data-stu-id="4e1be-237">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="4e1be-238">Wartość domyślna to "Symbols. nupkg".</span><span class="sxs-lookup"><span data-stu-id="4e1be-238">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="4e1be-239">Określa, że `pack` nie należy uruchamiać analizy pakietu po skompilowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-239">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="4e1be-240">Określa minimalną wersję klienta, NuGet który może zainstalować ten pakiet, wymuszony przez nuget.exe i Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e1be-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="4e1be-241">Ta wartość logiczna określa, czy zestawy danych wyjściowych kompilacji powinny być pakowane do pliku *. nupkg* , czy nie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-241">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="4e1be-242">Ta wartość logiczna określa, czy wszystkie elementy, które mają typ `Content` są zawarte w pakiecie, są automatycznie uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="4e1be-242">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="4e1be-243">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="4e1be-243">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="4e1be-244">Określa folder, w którym mają zostać umieszczone zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4e1be-244">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="4e1be-245">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="4e1be-245">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="4e1be-246">Aby uzyskać więcej informacji, zobacz [zestawy danych wyjściowych](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="4e1be-246">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="4e1be-247">Określa domyślną lokalizację, w której należy wykonać wszystkie pliki zawartości, jeśli `PackagePath` nie została określona dla nich.</span><span class="sxs-lookup"><span data-stu-id="4e1be-247">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="4e1be-248">Wartość domyślna to "Content; contentFiles".</span><span class="sxs-lookup"><span data-stu-id="4e1be-248">The default value is "content;contentFiles".</span></span> <span data-ttu-id="4e1be-249">Aby uzyskać więcej informacji, zobacz temat [uwzględnianie zawartości w pakiecie](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="4e1be-249">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="4e1be-250">Względna lub bezwzględna ścieżka do *.nuspec* pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="4e1be-250">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="4e1be-251">Jeśli ta wartość jest określona, jest używana **wyłącznie** na potrzeby informacji o pakowaniu, a wszelkie informacje w projektach nie są używane.</span><span class="sxs-lookup"><span data-stu-id="4e1be-251">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="4e1be-252">Aby uzyskać więcej informacji, zobacz [pakowanie przy .nuspec użyciu a ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4e1be-252">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="4e1be-253">Podstawowa ścieżka do *.nuspec* pliku.</span><span class="sxs-lookup"><span data-stu-id="4e1be-253">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="4e1be-254">Aby uzyskać więcej informacji, zobacz [pakowanie przy .nuspec użyciu a ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4e1be-254">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="4e1be-255">Rozdzielana średnikami lista par klucz = wartość.</span><span class="sxs-lookup"><span data-stu-id="4e1be-255">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="4e1be-256">Aby uzyskać więcej informacji, zobacz [pakowanie przy .nuspec użyciu a ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="4e1be-256">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="4e1be-257">scenariusze dotyczące pakietów</span><span class="sxs-lookup"><span data-stu-id="4e1be-257">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="4e1be-258">Pomijanie zależności</span><span class="sxs-lookup"><span data-stu-id="4e1be-258">Suppressing dependencies</span></span>

<span data-ttu-id="4e1be-259">Aby pominąć zależności pakietów z wygenerowanego NuGet pakietu, ustaw opcję `SuppressDependenciesWhenPacking` na `true` , która zezwoli na pomijanie wszystkich zależności od wygenerowanego pliku NUPKG.</span><span class="sxs-lookup"><span data-stu-id="4e1be-259">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="4e1be-260">`PackageIconUrl` jest przestarzałe na rzecz [`PackageIcon`](#packageicon) właściwości.</span><span class="sxs-lookup"><span data-stu-id="4e1be-260">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="4e1be-261">Począwszy od NuGet 5,3 i programu Visual Studio 2019 w wersji 16,3, program `pack` wywołuje ostrzeżenie [NU5048](./errors-and-warnings/nu5048.md) , jeśli tylko metadane pakietu są określone `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-261">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="4e1be-262">Aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które jeszcze nie obsługują `PackageIcon` , określ zarówno, `PackageIcon` jak i `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-262">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="4e1be-263">Program Visual Studio obsługuje `PackageIcon` pakiety pochodzące ze źródła opartego na folderach.</span><span class="sxs-lookup"><span data-stu-id="4e1be-263">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="4e1be-264">Pakowanie pliku obrazu ikony</span><span class="sxs-lookup"><span data-stu-id="4e1be-264">Packing an icon image file</span></span>

<span data-ttu-id="4e1be-265">Podczas pakowania pliku obrazu ikony Użyj właściwości, `PackageIcon` Aby określić ścieżkę pliku ikony względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-265">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="4e1be-266">Ponadto upewnij się, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-266">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4e1be-267">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="4e1be-267">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="4e1be-268">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="4e1be-268">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="4e1be-269">Zalecamy rozdzielczość obrazu 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="4e1be-269">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="4e1be-270">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4e1be-270">For example:</span></span>

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

<span data-ttu-id="4e1be-271">[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="4e1be-271">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="4e1be-272">Aby uzyskać nuspec odpowiedni odpowiednik, zapoznaj się z [ nuspec odwołaniem do ikony](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="4e1be-272">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="4e1be-273">Zestawy wyjściowe</span><span class="sxs-lookup"><span data-stu-id="4e1be-273">Output assemblies</span></span>

<span data-ttu-id="4e1be-274">`nuget pack` Kopiuje pliki wyjściowe z rozszerzeniami,,,, `.exe` `.dll` `.xml` `.winmd` `.json` i `.pri` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-274">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="4e1be-275">Kopiowane pliki wyjściowe zależą od tego, co jest MSBuild dostępne w `BuiltOutputProjectGroup` miejscu docelowym.</span><span class="sxs-lookup"><span data-stu-id="4e1be-275">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="4e1be-276">Istnieją dwie MSBuild  właściwości, których można użyć w pliku projektu lub wierszu polecenia do kontrolowania, gdzie są dostępne zestawy wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="4e1be-276">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="4e1be-277">`IncludeBuildOutput`: Wartość logiczna określająca, czy zestawy danych wyjściowych kompilacji powinny być zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-277">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="4e1be-278">`BuildOutputTargetFolder`: Określa folder, w którym należy umieścić zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4e1be-278">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="4e1be-279">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="4e1be-279">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="4e1be-280">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="4e1be-280">Package references</span></span>

<span data-ttu-id="4e1be-281">Zobacz [odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="4e1be-281">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="4e1be-282">Odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="4e1be-282">Project to project references</span></span>

<span data-ttu-id="4e1be-283">Odwołania do projektu są uwzględniane domyślnie jako NuGet odwołania do pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-283">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="4e1be-284">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4e1be-284">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="4e1be-285">Możesz również dodać następujące metadane do odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="4e1be-285">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="4e1be-286">Dołączanie zawartości do pakietu</span><span class="sxs-lookup"><span data-stu-id="4e1be-286">Including content in a package</span></span>

<span data-ttu-id="4e1be-287">Aby dołączyć zawartość, Dodaj dodatkowe metadane do istniejącego `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="4e1be-288">Domyślnie wszystkie elementy typu "Content" są uwzględniane w pakiecie, chyba że przestąpisz do wpisów, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="4e1be-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="4e1be-289">Domyślnie wszystko jest dodawane do katalogu głównego `content` `contentFiles\any\<target_framework>` folderu i w pakiecie i zachowuje względną strukturę folderów, chyba że zostanie określona ścieżka pakietu:</span><span class="sxs-lookup"><span data-stu-id="4e1be-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="4e1be-290">Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (a nie `content` `contentFiles` obu), możesz użyć MSBuild właściwości `ContentTargetFolders` , która domyślnie przyjmuje wartość "Content; contentFiles", ale można ją ustawić na dowolną inną nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="4e1be-291">Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` umieszcza plików w obszarze `contentFiles\any\<target_framework>` lub `contentFiles\<language>\<target_framework>` na podstawie `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="4e1be-292">`PackagePath` może to być rozdzielany średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="4e1be-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="4e1be-293">Określenie pustej ścieżki pakietu spowoduje dodanie pliku do katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="4e1be-294">Na przykład następujące polecenie dodaje `libuv.txt` do `content\myfiles` , `content\samples` i katalog główny pakietu:</span><span class="sxs-lookup"><span data-stu-id="4e1be-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="4e1be-295">Istnieje również MSBuild Właściwość `$(IncludeContentInPack)` , której wartością domyślną jest `true` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="4e1be-296">Jeśli ta wartość jest ustawiona na `false` dla każdego projektu, zawartość z tego projektu nie jest dołączana do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e1be-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="4e1be-297">Inne metadane specyficzne dla pakietu, które można ustawić dla każdego z powyższych elementów, obejmują ```<PackageCopyToOutput>``` i ```<PackageFlatten>``` które zestawy ```CopyToOutput``` i ```Flatten``` wartości ```contentFiles``` wpisu w danych wyjściowych nuspec .</span><span class="sxs-lookup"><span data-stu-id="4e1be-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="4e1be-298">Oprócz elementów zawartości `<Pack>` `<PackagePath>` można również ustawić metadane i dla plików z akcją kompilacji kompilowania, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="4e1be-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="4e1be-299">Aby pakiet mógł dołączyć nazwę pliku do ścieżki pakietu przy użyciu wzorców obsługi symboli wieloznacznych, ścieżka pakietu musi kończyć się znakiem separatora folderów. w przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka, w tym nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="4e1be-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="4e1be-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="4e1be-300">IncludeSymbols</span></span>

<span data-ttu-id="4e1be-301">W przypadku korzystania z programu `MSBuild -t:pack -p:IncludeSymbols=true` odpowiednie `.pdb` pliki są kopiowane wraz z innymi plikami wyjściowymi ( `.dll` ,,,, `.exe` `.winmd` `.xml` `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="4e1be-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="4e1be-302">Należy pamiętać, że ustawienie `IncludeSymbols=true` powoduje utworzenie regularnego pakietu *i* pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="4e1be-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="4e1be-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="4e1be-303">IncludeSource</span></span>

<span data-ttu-id="4e1be-304">Jest to takie samo `IncludeSymbols` , jak, z tą różnicą, że kopiuje również pliki źródłowe wraz z `.pdb` plikami.</span><span class="sxs-lookup"><span data-stu-id="4e1be-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="4e1be-305">Wszystkie pliki typu `Compile` są kopiowane za pośrednictwem `src\<ProjectName>\` , aby zachować strukturę folderu ścieżki względnej w pakietie będącym wynikiem.</span><span class="sxs-lookup"><span data-stu-id="4e1be-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="4e1be-306">To samo występuje również dla plików źródłowych, `ProjectReference` które mają `TreatAsPackageReference` ustawioną wartość `false` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="4e1be-307">Jeśli plik typu Kompiluj znajduje się poza folderem projektu, to właśnie został dodany do `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="4e1be-308">Pakowanie wyrażenia licencji lub pliku licencji</span><span class="sxs-lookup"><span data-stu-id="4e1be-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="4e1be-309">W przypadku korzystania z wyrażenia licencji Użyj `PackageLicenseExpression` właściwości.</span><span class="sxs-lookup"><span data-stu-id="4e1be-309">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="4e1be-310">Aby uzyskać przykład, zobacz [przykładowe wyrażenie licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="4e1be-310">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="4e1be-311">Aby dowiedzieć się więcej na temat wyrażeń licencji i licencji akceptowanych przez NuGet program. org, zobacz [metadane licencji](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="4e1be-311">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="4e1be-312">Podczas pakowania pliku licencji Użyj właściwości, `PackageLicenseFile` Aby określić ścieżkę pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-312">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="4e1be-313">Ponadto upewnij się, że plik jest dołączony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-313">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="4e1be-314">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4e1be-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="4e1be-315">Aby uzyskać przykład, zobacz [przykład pliku licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="4e1be-315">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="4e1be-316">Tylko jeden z `PackageLicenseExpression` , `PackageLicenseFile` i `PackageLicenseUrl` można określić w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-316">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="4e1be-317">Pakowanie pliku bez rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="4e1be-317">Packing a file without an extension</span></span>

<span data-ttu-id="4e1be-318">W niektórych scenariuszach, takich jak podczas pakowania pliku licencji, może być konieczne dołączenie pliku bez rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="4e1be-318">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="4e1be-319">Z przyczyn historycznych NuGet  &  MSBuild Traktuj ścieżki bez rozszerzenia jako katalogów.</span><span class="sxs-lookup"><span data-stu-id="4e1be-319">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="4e1be-320">[Plik bez rozszerzenia](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="4e1be-320">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="4e1be-321">Istool</span><span class="sxs-lookup"><span data-stu-id="4e1be-321">IsTool</span></span>

<span data-ttu-id="4e1be-322">W przypadku korzystania z programu `MSBuild -t:pack -p:IsTool=true` wszystkie pliki wyjściowe, zgodnie z opisem w scenariuszu [zestawów wyjściowych](#output-assemblies) , są kopiowane do `tools` folderu, a nie do `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-322">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="4e1be-323">Należy zauważyć, że różni się to od elementu, `DotNetCliTool` który jest określony przez ustawienie `PackageType` w `.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="4e1be-323">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="4e1be-324">Pakowanie przy użyciu `.nuspec` pliku</span><span class="sxs-lookup"><span data-stu-id="4e1be-324">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="4e1be-325">Mimo że zaleca się [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu, można użyć `.nuspec` pliku do spakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-325">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="4e1be-326">W przypadku projektu typu innego niż zestaw SDK, który używa programu `PackageReference` , należy go zaimportować, `NuGet.Build.Tasks.Pack.targets` Aby można było wykonać zadanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-326">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="4e1be-327">Nadal trzeba przywrócić projekt, aby można było spakować nuspec plik.</span><span class="sxs-lookup"><span data-stu-id="4e1be-327">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="4e1be-328">(Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).</span><span class="sxs-lookup"><span data-stu-id="4e1be-328">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="4e1be-329">Struktura docelowa pliku projektu jest nieistotna i nie jest używana podczas pakowania a nuspec .</span><span class="sxs-lookup"><span data-stu-id="4e1be-329">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="4e1be-330">Następujące trzy MSBuild właściwości są istotne dla pakowania przy użyciu `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="4e1be-330">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="4e1be-331">`NuspecFile`: względna lub bezwzględna ścieżka do `.nuspec` pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="4e1be-331">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="4e1be-332">`NuspecProperties`: rozdzielana średnikami lista par klucz = wartość.</span><span class="sxs-lookup"><span data-stu-id="4e1be-332">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="4e1be-333">Ze względu na sposób MSBuild działania analizy wiersza polecenia należy określić wiele właściwości w następujący sposób: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-333">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="4e1be-334">`NuspecBasePath`: Ścieżka podstawowa dla `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="4e1be-334">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="4e1be-335">Jeśli używasz `dotnet.exe` do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4e1be-335">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4e1be-336">Jeśli używasz MSBuild do pakowania projektu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4e1be-336">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="4e1be-337">Należy pamiętać, że pakowanie a nuspec using dotnet.exe lub MSBuild również prowadzi do domyślnego kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-337">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="4e1be-338">Można to uniknąć przez przekazanie ```--no-build``` właściwości do dotnet.exe, który jest odpowiednikiem ustawienia ```<NoBuild>true</NoBuild> ``` w pliku projektu, wraz z ustawieniem ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-338">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="4e1be-339">Przykład pliku *. csproj* do spakowania nuspec pliku:</span><span class="sxs-lookup"><span data-stu-id="4e1be-339">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="4e1be-340">Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="4e1be-340">Advanced extension points to create customized package</span></span>

<span data-ttu-id="4e1be-341">`pack`Element docelowy zawiera dwa punkty rozszerzenia, które są uruchamiane w wewnętrznej, docelowej kompilacji specyficznej dla platformy.</span><span class="sxs-lookup"><span data-stu-id="4e1be-341">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="4e1be-342">Obsługa punktów rozszerzenia umożliwia uwzględnienie zawartości i zestawów określonych dla platformy docelowej w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="4e1be-342">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="4e1be-343">`TargetsForTfmSpecificBuildOutput` target: Użyj dla plików znajdujących się w `lib` folderze lub folderu określonego przy użyciu `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-343">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="4e1be-344">`TargetsForTfmSpecificContentInPackage` target: Użyj dla plików poza `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-344">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="4e1be-345">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="4e1be-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="4e1be-346">Dla wszystkich plików, które muszą przejść do `BuildOutputTargetFolder` (domyślnie lib), obiekt docelowy powinien zapisać te pliki do obiektu Items `BuildOutputInPackage` i ustawić następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="4e1be-346">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="4e1be-347">`FinalOutputPath`: Ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość służy do oszacowania ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="4e1be-347">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="4e1be-348">`TargetPath`: (Opcjonalnie) ustawia się, gdy plik musi przejść do podfolderu w `lib\<TargetFramework>` , podobnie jak zestawy satelickie, które przechodzą w odpowiednie foldery kultury.</span><span class="sxs-lookup"><span data-stu-id="4e1be-348">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="4e1be-349">Wartością domyślną jest nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="4e1be-349">Defaults to the name of the file.</span></span>

<span data-ttu-id="4e1be-350">Przykład:</span><span class="sxs-lookup"><span data-stu-id="4e1be-350">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="4e1be-351">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości.</span><span class="sxs-lookup"><span data-stu-id="4e1be-351">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="4e1be-352">Dla dowolnych plików, które mają zostać dołączone do pakietu, obiekt docelowy powinien zapisać te pliki w obiekcie Items `TfmSpecificPackageFile` i ustawić następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="4e1be-352">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="4e1be-353">`PackagePath`: Ścieżka, w której plik powinien być wyprowadzany w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-353">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="4e1be-354">NuGet wyświetla ostrzeżenie, jeśli więcej niż jeden plik zostanie dodany do tej samej ścieżki pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-354">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="4e1be-355">`BuildAction`: Akcja kompilacji, która ma zostać przypisana do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w `contentFiles` folderze.</span><span class="sxs-lookup"><span data-stu-id="4e1be-355">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="4e1be-356">Wartość domyślna to "none".</span><span class="sxs-lookup"><span data-stu-id="4e1be-356">Defaults to "None".</span></span>

<span data-ttu-id="4e1be-357">Przykład:</span><span class="sxs-lookup"><span data-stu-id="4e1be-357">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="4e1be-358">Przywróć miejsce docelowe</span><span class="sxs-lookup"><span data-stu-id="4e1be-358">restore target</span></span>

<span data-ttu-id="4e1be-359">`MSBuild -t:restore` (które `nuget restore` `dotnet restore` są używane z projektami .NET Core), przywraca pakiety, do których odwołuje się plik projektu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4e1be-359">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="4e1be-360">Odczytuj wszystkie odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="4e1be-360">Read all project to project references</span></span>
1. <span data-ttu-id="4e1be-361">Odczytywanie właściwości projektu w celu znalezienia pośredniego folderu i platform docelowych</span><span class="sxs-lookup"><span data-stu-id="4e1be-361">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="4e1be-362">Przekaż MSBuild dane do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="4e1be-362">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="4e1be-363">Uruchom przywracanie</span><span class="sxs-lookup"><span data-stu-id="4e1be-363">Run restore</span></span>
1. <span data-ttu-id="4e1be-364">Pobierz pakiety</span><span class="sxs-lookup"><span data-stu-id="4e1be-364">Download packages</span></span>
1. <span data-ttu-id="4e1be-365">Zapisz plik zasobów, cele i właściwości.</span><span class="sxs-lookup"><span data-stu-id="4e1be-365">Write assets file, targets, and props</span></span>

<span data-ttu-id="4e1be-366">`restore`Obiekt docelowy działa dla projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="4e1be-366">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="4e1be-367">`MSBuild 16.5+` Ponadto zapewnia [obsługę](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) tego `packages.config` formatu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-367">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="4e1be-368">`restore`Element docelowy [nie powinien być uruchamiany](#restoring-and-building-with-one-msbuild-command) w połączeniu z `build` elementem docelowym.</span><span class="sxs-lookup"><span data-stu-id="4e1be-368">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="4e1be-369">Właściwości przywracania</span><span class="sxs-lookup"><span data-stu-id="4e1be-369">Restore properties</span></span>

<span data-ttu-id="4e1be-370">Dodatkowe ustawienia przywracania mogą pochodzić z MSBuild właściwości w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-370">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="4e1be-371">Wartości można również ustawić z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (Zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="4e1be-371">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="4e1be-372">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e1be-372">Property</span></span> | <span data-ttu-id="4e1be-373">Opis</span><span class="sxs-lookup"><span data-stu-id="4e1be-373">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="4e1be-374">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="4e1be-374">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="4e1be-375">Ścieżka folderu pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4e1be-375">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="4e1be-376">Ogranicz pobieranie do jednej naraz.</span><span class="sxs-lookup"><span data-stu-id="4e1be-376">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="4e1be-377">Ścieżka do `Nuget.Config` pliku, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="4e1be-377">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="4e1be-378">Jeśli ma wartość true, unika używania buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="4e1be-378">If true, avoids using cached packages.</span></span> <span data-ttu-id="4e1be-379">Zobacz [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="4e1be-379">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="4e1be-380">W przypadku wartości true program ignoruje Niepowodzenie lub brak źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="4e1be-380">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="4e1be-381">Foldery rezerwowe używane w taki sam sposób, w jaki jest używany folder pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4e1be-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="4e1be-382">Dodatkowe źródła do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="4e1be-382">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="4e1be-383">Dodatkowe foldery rezerwowe do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="4e1be-383">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="4e1be-384">Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="4e1be-384">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="4e1be-385">Ścieżka do `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="4e1be-386">Rozdzielana średnikami lista projektów do przywrócenia, które powinny zawierać ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="4e1be-386">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="4e1be-387">Gdy projekty są zbierane za pośrednictwem, MSBuild określają, czy są zbierane przy użyciu `SkipNonexistentTargets` optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="4e1be-387">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="4e1be-388">Gdy wartość nie jest ustawiona, wartością domyślną jest `true` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-388">When not set, defaults to `true`.</span></span> <span data-ttu-id="4e1be-389">Sekwencja jest zachowaniem nieprawidłowej awarii, gdy nie można zaimportować elementów docelowych projektu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-389">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="4e1be-390">Folder wyjściowy, domyślny dla `BaseIntermediateOutputPath` i `obj` folder.</span><span class="sxs-lookup"><span data-stu-id="4e1be-390">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="4e1be-391">W projektach opartych na PackageReference wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-391">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="4e1be-392">Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="4e1be-392">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="4e1be-393">Nie powoduje to obejścia pamięci podręcznej protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="4e1be-393">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="4e1be-394">Umożliwia użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="4e1be-394">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="4e1be-395">Uruchom przywracanie w trybie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="4e1be-395">Run restore in locked mode.</span></span> <span data-ttu-id="4e1be-396">Oznacza to, że przywracanie nie będzie obliczać zależności.</span><span class="sxs-lookup"><span data-stu-id="4e1be-396">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="4e1be-397">Niestandardowa lokalizacja pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="4e1be-397">A custom location for the lock file.</span></span> <span data-ttu-id="4e1be-398">Domyślna lokalizacja jest obok projektu i ma nazwę `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-398">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="4e1be-399">Wymusza ponowne obliczenie zależności przez Przywracanie i zaktualizowanie pliku blokady bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="4e1be-399">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="4e1be-400">Opcjonalny przełącznik, który przywraca projekty z packages.config. Obsługa `MSBuild -t:restore` wyłącznie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-400">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="4e1be-401">Opcjonalny przełącznik służący do użycia oceny wykresu statycznego MSBuild zamiast standardowej oceny.</span><span class="sxs-lookup"><span data-stu-id="4e1be-401">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="4e1be-402">Obliczanie wykresu statycznego to eksperymentalna funkcja, która jest znacznie szybsza w przypadku dużych repozytoriów i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="4e1be-402">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="4e1be-403">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4e1be-403">Examples</span></span>

<span data-ttu-id="4e1be-404">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="4e1be-404">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="4e1be-405">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="4e1be-405">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="4e1be-406">Przywróć dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="4e1be-406">Restore outputs</span></span>

<span data-ttu-id="4e1be-407">Instrukcja RESTORE tworzy następujące pliki w folderze Build `obj` :</span><span class="sxs-lookup"><span data-stu-id="4e1be-407">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="4e1be-408">Plik</span><span class="sxs-lookup"><span data-stu-id="4e1be-408">File</span></span> | <span data-ttu-id="4e1be-409">Opis</span><span class="sxs-lookup"><span data-stu-id="4e1be-409">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="4e1be-410">Zawiera wykres zależności wszystkich odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="4e1be-410">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="4e1be-411">Odwołania do MSBuild Właściwości props zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="4e1be-411">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="4e1be-412">Odwołania do MSBuild elementów docelowych zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="4e1be-412">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="4e1be-413">Przywracanie i kompilowanie za pomocą jednego MSBuild polecenia</span><span class="sxs-lookup"><span data-stu-id="4e1be-413">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="4e1be-414">Ze względu na fakt, że NuGet można przywrócić pakiety, które wyłączają MSBuild elementy docelowe i wartościowe, oceny przywracania i kompilacji są uruchamiane z różnymi właściwościami globalnymi.</span><span class="sxs-lookup"><span data-stu-id="4e1be-414">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="4e1be-415">Oznacza to, że następujące elementy będą miały nieprzewidywalne i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="4e1be-415">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="4e1be-416">Zamiast tego zalecane podejście to:</span><span class="sxs-lookup"><span data-stu-id="4e1be-416">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="4e1be-417">Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-417">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="4e1be-418">Przywracanie projektów PackageReference i packages.config za pomocą MSBuild</span><span class="sxs-lookup"><span data-stu-id="4e1be-418">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="4e1be-419">W przypadku programu MSBuild 16.5 + packages.config są również obsługiwane w programie `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="4e1be-419">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="4e1be-420">`packages.config` Przywracanie jest dostępne `MSBuild 16.5+` tylko z `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="4e1be-420">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="4e1be-421">Przywracanie za pomocą MSBuild obliczenia wykresu statycznego</span><span class="sxs-lookup"><span data-stu-id="4e1be-421">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="4e1be-422">Program MSBuild 16.6 +, NuGet dodał funkcję eksperymentalną do użycia obliczeń wykresu statycznego z wiersza polecenia, który znacznie skraca czas przywracania dla dużych repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="4e1be-422">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="4e1be-423">Alternatywnie możesz ją włączyć, ustawiając właściwość w katalogu. Build. props.</span><span class="sxs-lookup"><span data-stu-id="4e1be-423">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="4e1be-424">Począwszy od programu Visual Studio 2019. x i NuGet 5. x, ta funkcja jest uznawana za eksperymentalną i niezależną.</span><span class="sxs-lookup"><span data-stu-id="4e1be-424">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="4e1be-425">Aby uzyskać szczegółowe informacje o tym, kiedy ta funkcja zostanie włączona domyślnie, obserwuj [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) .</span><span class="sxs-lookup"><span data-stu-id="4e1be-425">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="4e1be-426">Statyczne przywracanie wykresu zmienia część programu MSBuild przywracania, odczytywanie i ocenianie projektu, ale nie algorytmem przywracania.</span><span class="sxs-lookup"><span data-stu-id="4e1be-426">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="4e1be-427">Algorytm przywracania jest taki sam dla wszystkich NuGet narzędzi ( NuGet exe, MSBuild exe, dotnet.exe i Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="4e1be-427">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="4e1be-428">W bardzo kilku scenariuszach statyczne przywracanie wykresu może zachowywać się inaczej niż bieżące przywracanie, a niektóre zadeklarowane składnika packagereferences lub zawierających mogą być niedostępne.</span><span class="sxs-lookup"><span data-stu-id="4e1be-428">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="4e1be-429">Aby ułatwić sobie zdanie, podczas migracji do przywracania wykresu statycznego należy wziąć pod uwagę następujące działania:</span><span class="sxs-lookup"><span data-stu-id="4e1be-429">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="4e1be-430">NuGet*nie* należy zgłaszać żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="4e1be-430">NuGet should *not* report any changes.</span></span> <span data-ttu-id="4e1be-431">Jeśli widzisz Niezgodność, zrób problem pod adresem [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="4e1be-431">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="4e1be-432">Zastępowanie jednej biblioteki na podstawie grafu przywracania</span><span class="sxs-lookup"><span data-stu-id="4e1be-432">Replacing one library from a restore graph</span></span>

<span data-ttu-id="4e1be-433">Jeśli przywracanie powoduje przełączenie niewłaściwego zestawu, możliwe jest wykluczenie domyślnego wyboru pakietów i zamienienie go na własny wybór.</span><span class="sxs-lookup"><span data-stu-id="4e1be-433">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="4e1be-434">Najpierw `PackageReference` należy wykluczyć wszystkie elementy zawartości z najwyższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="4e1be-434">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="4e1be-435">Następnie Dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="4e1be-435">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
