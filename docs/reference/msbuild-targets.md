---
title: NuGet spakuj i przywróć jako MSBuild obiekty docelowe
description: NuGet Pakiet i przywracanie mogą działać bezpośrednio jako MSBuild obiekty docelowe w ponad NuGet 4.0.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 0a10a6f1e4c71903232281c25a6c4b6bbc65fb34
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901488"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="eb244-103">NuGet spakuj i przywróć jako MSBuild obiekty docelowe</span><span class="sxs-lookup"><span data-stu-id="eb244-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="eb244-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="eb244-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="eb244-105">W [formacie PackageReference](../consume-packages/package-references-in-project-files.md) program 4.0+ może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, NuGet zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="eb244-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="eb244-106">W przypadku programu 15.1+ jest również pierwszoklasowym obywatelem z celami i , MSBuild NuGet jak MSBuild `pack` `restore` opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="eb244-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="eb244-107">Te obiekty docelowe umożliwiają pracę z usługą tak NuGet jak z innymi zadaniami lub MSBuild obiektami docelowymi.</span><span class="sxs-lookup"><span data-stu-id="eb244-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="eb244-108">Aby uzyskać instrukcje NuGet dotyczące tworzenia pakietu przy użyciu polecenia , zobacz Tworzenie pakietu przy użyciu MSBuild [ NuGet polecenia MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="eb244-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="eb244-109">(W przypadku NuGet W wersji 3.x lub starszej zamiast tego należy użyć poleceń [pakowania](../reference/cli-reference/cli-ref-pack.md) [i](../reference/cli-reference/cli-ref-restore.md) przywracania za pośrednictwem interfejsu NuGet wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="eb244-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="eb244-110">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="eb244-110">Target build order</span></span>

<span data-ttu-id="eb244-111">Ponieważ `pack` i `restore` są  MSBuild celami, możesz uzyskać do nich dostęp, aby ulepszyć przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="eb244-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="eb244-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu.</span><span class="sxs-lookup"><span data-stu-id="eb244-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="eb244-113">Możesz to zrobić, dodając następujące elementy w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="eb244-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="eb244-114">Podobnie można napisać MSBuild zadanie, napisać własny element docelowy i korzystać z właściwości w NuGet MSBuild zadaniu.</span><span class="sxs-lookup"><span data-stu-id="eb244-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="eb244-115">`$(OutputPath)` jest względny i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="eb244-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="eb244-116">element docelowy pakietu</span><span class="sxs-lookup"><span data-stu-id="eb244-116">pack target</span></span>

<span data-ttu-id="eb244-117">W przypadku projektów .NET, które używają formatu , przy użyciu rysuje dane wejściowe z pliku projektu do `PackageReference` `msbuild -t:pack` użycia podczas tworzenia NuGet pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="eb244-118">W poniższej tabeli MSBuild opisano właściwości, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle.</span><span class="sxs-lookup"><span data-stu-id="eb244-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="eb244-119">Te zmiany można łatwo wprowadzić w programie Visual Studio 2017 lub nowszym, klikając prawym przyciskiem myszy projekt i wybierając pozycję Edytuj **{project_name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="eb244-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="eb244-120">Dla wygody tabela jest zorganizowana według równoważnej właściwości w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="eb244-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="eb244-121">`Owners` Właściwości `Summary` i z nie są obsługiwane w `.nuspec` programie MSBuild .</span><span class="sxs-lookup"><span data-stu-id="eb244-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="eb244-122">nuspecAtrybut/wartość</span><span class="sxs-lookup"><span data-stu-id="eb244-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="eb244-123">MSBuild Właściwość</span><span class="sxs-lookup"><span data-stu-id="eb244-123">MSBuild Property</span></span> | <span data-ttu-id="eb244-124">Domyślne</span><span class="sxs-lookup"><span data-stu-id="eb244-124">Default</span></span> | <span data-ttu-id="eb244-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="eb244-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="eb244-126">`$(AssemblyName)` Z MSBuild</span><span class="sxs-lookup"><span data-stu-id="eb244-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="eb244-127">Wersja</span><span class="sxs-lookup"><span data-stu-id="eb244-127">Version</span></span> | <span data-ttu-id="eb244-128">Jest to zgodne ze semver, na przykład `1.0.0` `1.0.0-beta` , lub `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="eb244-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="eb244-129">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-129">empty</span></span> | <span data-ttu-id="eb244-130">Zastępowanie `PackageVersion` ustawień `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="eb244-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="eb244-131">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-131">empty</span></span> | <span data-ttu-id="eb244-132">`$(VersionSuffix)` z MSBuild .</span><span class="sxs-lookup"><span data-stu-id="eb244-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="eb244-133">Zastępowanie `PackageVersion` ustawień `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="eb244-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="eb244-134">Nazwa użytkownika bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="eb244-134">Username of the current user</span></span> | <span data-ttu-id="eb244-135">Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów na nuget.org. Są one wyświetlane w galerii na nuget.org i są używane do odsyłania pakietów NuGet przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="eb244-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="eb244-136">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="eb244-136">N/A</span></span> | <span data-ttu-id="eb244-137">Nie ma w nuspec</span><span class="sxs-lookup"><span data-stu-id="eb244-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="eb244-138">Element `PackageId`.</span><span class="sxs-lookup"><span data-stu-id="eb244-138">The `PackageId`</span></span> | <span data-ttu-id="eb244-139">Przyjazny dla człowieka tytuł pakietu, zwykle używany w interfejsie użytkownika, jest wyświetlany jako nuget.org i Menedżer pakietów w Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb244-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="eb244-140">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="eb244-140">"Package Description"</span></span> | <span data-ttu-id="eb244-141">Długi opis zestawu.</span><span class="sxs-lookup"><span data-stu-id="eb244-141">A long description for the assembly.</span></span> <span data-ttu-id="eb244-142">Jeśli nie zostanie określony, ta właściwość jest również używana `PackageDescription` jako opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="eb244-143">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-143">empty</span></span> | <span data-ttu-id="eb244-144">Szczegóły praw autorskich dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="eb244-145">Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="eb244-146">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-146">empty</span></span> | <span data-ttu-id="eb244-147">Odpowiada `<license type="expression">` .</span><span class="sxs-lookup"><span data-stu-id="eb244-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="eb244-148">Zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="eb244-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="eb244-149">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-149">empty</span></span> | <span data-ttu-id="eb244-150">Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji niestandardowej lub licencji, do których nie przypisano identyfikatora SPDX.</span><span class="sxs-lookup"><span data-stu-id="eb244-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="eb244-151">Musisz jawnie spakować plik licencji, do których się odwołujesz.</span><span class="sxs-lookup"><span data-stu-id="eb244-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="eb244-152">Odpowiada `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="eb244-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="eb244-153">Zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="eb244-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="eb244-154">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-154">empty</span></span> | <span data-ttu-id="eb244-155">`PackageLicenseUrl` jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="eb244-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="eb244-156">Zamiast `PackageLicenseExpression` tego użyj lub `PackageLicenseFile` .</span><span class="sxs-lookup"><span data-stu-id="eb244-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="eb244-157">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="eb244-158">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-158">empty</span></span> | <span data-ttu-id="eb244-159">Ścieżka do obrazu w pakiecie do użycia jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="eb244-160">Musisz jawnie spakować plik obrazu ikony, do których się odwołujesz.</span><span class="sxs-lookup"><span data-stu-id="eb244-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="eb244-161">Aby uzyskać więcej informacji, zobacz [Pakowanie pliku obrazu ikony i](#packing-an-icon-image-file) [ `icon` metadanych](./nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="eb244-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="eb244-162">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-162">empty</span></span> | <span data-ttu-id="eb244-163">`PackageIconUrl` jest przestarzała na rzecz `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="eb244-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="eb244-164">Jednak aby uzyskać najlepsze środowisko na 1. łydce, oprócz wartości należy `PackageIconUrl` określić wartość `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="eb244-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="eb244-165">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-165">empty</span></span> | <span data-ttu-id="eb244-166">Należy jawnie spakować przywołyowany plik readme.</span><span class="sxs-lookup"><span data-stu-id="eb244-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="eb244-167">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-167">empty</span></span> | <span data-ttu-id="eb244-168">Rozdzielana średnikami lista tagów, która wyznacza pakiet.</span><span class="sxs-lookup"><span data-stu-id="eb244-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="eb244-169">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-169">empty</span></span> | <span data-ttu-id="eb244-170">Informacje o wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="eb244-171">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-171">empty</span></span> | <span data-ttu-id="eb244-172">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="eb244-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="eb244-173">Przykład: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="eb244-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="eb244-174">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-174">empty</span></span> | <span data-ttu-id="eb244-175">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="eb244-175">Repository type.</span></span> <span data-ttu-id="eb244-176">Przykłady: `git` (ustawienie domyślne), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="eb244-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="eb244-177">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-177">empty</span></span> | <span data-ttu-id="eb244-178">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="eb244-178">Optional repository branch information.</span></span> <span data-ttu-id="eb244-179">`RepositoryUrl` Należy również określić dla tej właściwości, która ma zostać uwzględniona.</span><span class="sxs-lookup"><span data-stu-id="eb244-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eb244-180">Przykład: *master* NuGet (4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eb244-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="eb244-181">puste</span><span class="sxs-lookup"><span data-stu-id="eb244-181">empty</span></span> | <span data-ttu-id="eb244-182">Opcjonalne zatwierdzenie repozytorium lub zestaw zmian w celu wskazania źródła, z którego został s zbudowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="eb244-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="eb244-183">`RepositoryUrl` Należy również określić dla tej właściwości, aby można było do nich do nich dołączona.</span><span class="sxs-lookup"><span data-stu-id="eb244-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eb244-184">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eb244-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="eb244-185">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="eb244-185">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="eb244-186">docelowe dane wejściowe pakietu</span><span class="sxs-lookup"><span data-stu-id="eb244-186">pack target inputs</span></span>

| <span data-ttu-id="eb244-187">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eb244-187">Property</span></span> | <span data-ttu-id="eb244-188">Opis</span><span class="sxs-lookup"><span data-stu-id="eb244-188">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="eb244-189">Wartość logiczna określająca, czy można spakować projekt.</span><span class="sxs-lookup"><span data-stu-id="eb244-189">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="eb244-190">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="eb244-190">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="eb244-191">Ustaw na `true` , aby pominąć zależności pakietu z wygenerowanego NuGet pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-191">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="eb244-192">Określa wersję pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="eb244-192">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="eb244-193">Akceptuje wszystkie formy ciągu NuGet wersji.</span><span class="sxs-lookup"><span data-stu-id="eb244-193">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="eb244-194">Wartość domyślna to `$(Version)` wartość , czyli właściwości w `Version` projekcie.</span><span class="sxs-lookup"><span data-stu-id="eb244-194">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="eb244-195">Określa nazwę pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="eb244-195">Specifies the name for the resulting package.</span></span> <span data-ttu-id="eb244-196">Jeśli nie zostanie określony, operacja domyślnie będzie używać nazwy katalogu lub jako `pack` `AssemblyName` nazwy pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-196">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="eb244-197">Długi opis pakietu dla wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eb244-197">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="eb244-198">Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów na nuget.org. Są one wyświetlane w galerii na nuget.org i są używane do odsyłania pakietów NuGet przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="eb244-198">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="eb244-199">Długi opis zestawu.</span><span class="sxs-lookup"><span data-stu-id="eb244-199">A long description for the assembly.</span></span> <span data-ttu-id="eb244-200">Jeśli nie zostanie określony, ta właściwość jest również używana `PackageDescription` jako opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-200">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="eb244-201">Szczegóły praw autorskich dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-201">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="eb244-202">Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-202">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="eb244-203">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="eb244-203">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="eb244-204">Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="eb244-204">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="eb244-205">W `PackageReference` przypadku programu (4.8+) ta flaga oznacza również, że zasoby w czasie kompilacji NuGet są wykluczone z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="eb244-205">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="eb244-206">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference (Obsługa zależności dla packageReference).](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="eb244-206">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="eb244-207">Identyfikator [licencji SPDX](https://spdx.org/licenses/) lub wyrażenie, na przykład `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="eb244-207">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="eb244-208">Aby uzyskać więcej informacji, zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="eb244-208">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="eb244-209">Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji niestandardowej lub licencji, która nie ma przypisanego identyfikatora SPDX.</span><span class="sxs-lookup"><span data-stu-id="eb244-209">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="eb244-210">`PackageLicenseUrl` jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="eb244-210">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="eb244-211">Zamiast `PackageLicenseExpression` tego użyj lub `PackageLicenseFile` .</span><span class="sxs-lookup"><span data-stu-id="eb244-211">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="eb244-212">Określa ścieżkę ikony pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-212">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="eb244-213">Aby uzyskać więcej informacji, zobacz [Pakowanie pliku obrazu ikony](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="eb244-213">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="eb244-214">Informacje o wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-214">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="eb244-215">Readme dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-215">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="eb244-216">Rozdzielana średnikami lista tagów, która wyznacza pakiet.</span><span class="sxs-lookup"><span data-stu-id="eb244-216">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="eb244-217">Określa ścieżkę wyjściową, w której spakowany pakiet zostanie porzucony.</span><span class="sxs-lookup"><span data-stu-id="eb244-217">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="eb244-218">Wartość domyślna to `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="eb244-218">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="eb244-219">Ta wartość logiczna wskazuje, czy pakiet powinien utworzyć dodatkowy pakiet symboli podczas pakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="eb244-219">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="eb244-220">Format pakietu symboli jest kontrolowany przez `SymbolPackageFormat` właściwość .</span><span class="sxs-lookup"><span data-stu-id="eb244-220">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="eb244-221">Aby uzyskać więcej informacji, zobacz [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="eb244-221">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="eb244-222">Ta wartość logiczna wskazuje, czy proces pakietu powinien utworzyć pakiet źródłowy.</span><span class="sxs-lookup"><span data-stu-id="eb244-222">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="eb244-223">Pakiet źródłowy zawiera kod źródłowy biblioteki, a także pliki PDB.</span><span class="sxs-lookup"><span data-stu-id="eb244-223">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="eb244-224">Pliki źródłowe są umieszczane `src/ProjectName` w katalogu w wynikowym pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-224">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="eb244-225">Aby uzyskać więcej informacji, zobacz [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="eb244-225">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="eb244-226">Określa, czy wszystkie pliki wyjściowe są kopiowane do folderu *tools* zamiast do *folderu lib.*</span><span class="sxs-lookup"><span data-stu-id="eb244-226">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="eb244-227">Aby uzyskać więcej informacji, zobacz [IsTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="eb244-227">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="eb244-228">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="eb244-228">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="eb244-229">Przykład: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="eb244-229">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="eb244-230">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="eb244-230">Repository type.</span></span> <span data-ttu-id="eb244-231">Przykłady: `git` (ustawienie domyślne), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="eb244-231">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="eb244-232">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="eb244-232">Optional repository branch information.</span></span> <span data-ttu-id="eb244-233">`RepositoryUrl` Należy również określić dla tej właściwości, aby można było do nich do nich dołączona.</span><span class="sxs-lookup"><span data-stu-id="eb244-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eb244-234">Przykład: *master* NuGet (4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eb244-234">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="eb244-235">Opcjonalne zatwierdzenie repozytorium lub zestaw zmian, aby wskazać źródło, z którego został s zbudowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="eb244-235">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="eb244-236">`RepositoryUrl` Należy również określić dla tej właściwości, aby można było do nich do nich dołączona.</span><span class="sxs-lookup"><span data-stu-id="eb244-236">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="eb244-237">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="eb244-237">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="eb244-238">Określa format pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="eb244-238">Specifies the format of the symbols package.</span></span> <span data-ttu-id="eb244-239">W przypadku pliku "symbols.nupkg" starszy pakiet symboli jest tworzony z rozszerzeniem *.symbols.nupkg* zawierającym pliki PDB, DLL i inne pliki wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="eb244-239">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="eb244-240">W przypadku polecenia "snupkg" tworzony jest pakiet symboli tabupkg zawierający przenośne pliki PDB.</span><span class="sxs-lookup"><span data-stu-id="eb244-240">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="eb244-241">Wartość domyślna to "symbols.nupkg".</span><span class="sxs-lookup"><span data-stu-id="eb244-241">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="eb244-242">Określa, `pack` że nie należy uruchamiać analizy pakietu po sbudowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-242">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="eb244-243">Określa minimalną wersję klienta, który może zainstalować ten pakiet, wymuszaną przez nuget.exe NuGet i Visual Studio Menedżer pakietów.</span><span class="sxs-lookup"><span data-stu-id="eb244-243">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="eb244-244">Ta wartość logiczna określa, czy zestawy wyjściowe kompilacji powinny być spakowane w pliku *nupkg,* czy nie.</span><span class="sxs-lookup"><span data-stu-id="eb244-244">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="eb244-245">Ta wartość logiczna określa, czy jakiekolwiek elementy, które mają typ , są automatycznie uwzględniane `Content` w wynikowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="eb244-245">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="eb244-246">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="eb244-246">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="eb244-247">Określa folder, w którym mają być umieszczane zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="eb244-247">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="eb244-248">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="eb244-248">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="eb244-249">Aby uzyskać więcej informacji, zobacz [Output assemblies (Zestawy wyjściowe).](#output-assemblies)</span><span class="sxs-lookup"><span data-stu-id="eb244-249">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="eb244-250">Określa domyślną lokalizację, w której powinny przejść wszystkie pliki zawartości, jeśli `PackagePath` nie zostanie określona dla nich.</span><span class="sxs-lookup"><span data-stu-id="eb244-250">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="eb244-251">Wartość domyślna to "content;contentFiles".</span><span class="sxs-lookup"><span data-stu-id="eb244-251">The default value is "content;contentFiles".</span></span> <span data-ttu-id="eb244-252">Aby uzyskać więcej informacji, zobacz [Including content in a package](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="eb244-252">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="eb244-253">Względna lub bezwzględna ścieżka *.nuspec* do pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="eb244-253">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="eb244-254">Jeśli to określono, są używane **wyłącznie do pakowania** informacji, a żadne informacje w projektach nie są używane.</span><span class="sxs-lookup"><span data-stu-id="eb244-254">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="eb244-255">Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file)</span><span class="sxs-lookup"><span data-stu-id="eb244-255">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="eb244-256">Ścieżka podstawowa *.nuspec* pliku.</span><span class="sxs-lookup"><span data-stu-id="eb244-256">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="eb244-257">Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file)</span><span class="sxs-lookup"><span data-stu-id="eb244-257">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="eb244-258">Rozdzielana średnikami lista par klucz=wartość.</span><span class="sxs-lookup"><span data-stu-id="eb244-258">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="eb244-259">Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file)</span><span class="sxs-lookup"><span data-stu-id="eb244-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="eb244-260">scenariusze pakietu</span><span class="sxs-lookup"><span data-stu-id="eb244-260">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="eb244-261">Pomijanie zależności</span><span class="sxs-lookup"><span data-stu-id="eb244-261">Suppressing dependencies</span></span>

<span data-ttu-id="eb244-262">Aby pominąć zależności pakietu z wygenerowanego pakietu, ustaw wartość , aby umożliwić pominięcie wszystkich zależności z wygenerowanego NuGet `SuppressDependenciesWhenPacking` pliku `true` nupkg.</span><span class="sxs-lookup"><span data-stu-id="eb244-262">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="eb244-263">`PackageIconUrl` jest przestarzała na rzecz [`PackageIcon`](#packageicon) właściwości .</span><span class="sxs-lookup"><span data-stu-id="eb244-263">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="eb244-264">Począwszy od NuGet wersji 5.3 i Visual Studio 2019 w wersji 16.3, program zgłasza ostrzeżenie `pack` [NU5048,](./errors-and-warnings/nu5048.md) jeśli metadane pakietu określają tylko wartość `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="eb244-264">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="eb244-265">Aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które nie obsługują jeszcze `PackageIcon` usługi , określ wartości i `PackageIcon` `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="eb244-265">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="eb244-266">Visual Studio obsługuje `PackageIcon` pakiety pochodzące ze źródła opartego na folderach.</span><span class="sxs-lookup"><span data-stu-id="eb244-266">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="eb244-267">Pakowanie pliku obrazu ikony</span><span class="sxs-lookup"><span data-stu-id="eb244-267">Packing an icon image file</span></span>

<span data-ttu-id="eb244-268">Podczas pakowania pliku obrazu ikony użyj właściwości , aby określić ścieżkę pliku ikony względem katalogu `PackageIcon` głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-268">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="eb244-269">Ponadto upewnij się, że plik znajduje się w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="eb244-269">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="eb244-270">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eb244-270">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="eb244-271">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="eb244-271">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="eb244-272">Zalecamy rozdzielczość obrazu 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="eb244-272">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="eb244-273">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eb244-273">For example:</span></span>

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

<span data-ttu-id="eb244-274">[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="eb244-274">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="eb244-275">Aby uzyskać nuspec odpowiednik, zobacz odwołanie do [ nuspec ikony](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="eb244-275">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="eb244-276">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="eb244-276">PackageReadmeFile</span></span>

<span data-ttu-id="eb244-277">*Obsługiwane w **NuGet wersji 5.10.0 (wersja zapoznawcza 2)**  /  **.NET 5.0.3** i wersjach powyżej*</span><span class="sxs-lookup"><span data-stu-id="eb244-277">*Supported with **NuGet 5.10.0 preview 2** / **.NET 5.0.3** and above*</span></span>

<span data-ttu-id="eb244-278">Podczas pakowania pliku readme należy użyć właściwości , aby określić ścieżkę pakietu względem katalogu `PackageReadmeFile` głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-278">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eb244-279">Oprócz tego należy się upewnić, że plik znajduje się w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="eb244-279">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="eb244-280">Obsługiwane formaty plików obejmują tylko markdown *(md).*</span><span class="sxs-lookup"><span data-stu-id="eb244-280">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="eb244-281">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eb244-281">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="eb244-282">Aby uzyskać nuspec odpowiednik, zapoznaj się z odwołaniem [ nuspec do readme](nuspec.md#readme).</span><span class="sxs-lookup"><span data-stu-id="eb244-282">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="eb244-283">Zestawy wyjściowe</span><span class="sxs-lookup"><span data-stu-id="eb244-283">Output assemblies</span></span>

<span data-ttu-id="eb244-284">`nuget pack` Kopiuje pliki wyjściowe z `.exe` rozszerzeniami `.dll` , , , , i `.xml` `.winmd` `.json` `.pri` .</span><span class="sxs-lookup"><span data-stu-id="eb244-284">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="eb244-285">Kopiowane pliki wyjściowe zależą od tego, MSBuild co zapewnia obiekt `BuiltOutputProjectGroup` docelowy.</span><span class="sxs-lookup"><span data-stu-id="eb244-285">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="eb244-286">Istnieją dwie właściwości, których można użyć w pliku projektu lub wierszu polecenia, aby kontrolować, MSBuild  gdzie trafiają zestawy wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="eb244-286">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="eb244-287">`IncludeBuildOutput`: wartość logiczna, która określa, czy zestawy wyjściowe kompilacji powinny być zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="eb244-287">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="eb244-288">`BuildOutputTargetFolder`: określa folder, w którym mają zostać umieszczone zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="eb244-288">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="eb244-289">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="eb244-289">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="eb244-290">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="eb244-290">Package references</span></span>

<span data-ttu-id="eb244-291">Zobacz [Odwołania do pakietów w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="eb244-291">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="eb244-292">Odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="eb244-292">Project to project references</span></span>

<span data-ttu-id="eb244-293">Odwołania projektu do projektu są domyślnie traktowane jako odwołania NuGet do pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-293">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="eb244-294">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eb244-294">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="eb244-295">Możesz również dodać następujące metadane do odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="eb244-295">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="eb244-296">Łącznie z zawartością w pakiecie</span><span class="sxs-lookup"><span data-stu-id="eb244-296">Including content in a package</span></span>

<span data-ttu-id="eb244-297">Aby dołączyć zawartość, dodaj dodatkowe metadane do istniejącego `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="eb244-297">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="eb244-298">Domyślnie wszystko typu "Zawartość" jest uwzględniane w pakiecie, chyba że zastąpisz wpisami podobnymi do następujących:</span><span class="sxs-lookup"><span data-stu-id="eb244-298">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="eb244-299">Domyślnie wszystko jest dodawane do katalogu głównego folderu i w pakiecie i zachowuje względną strukturę folderów, chyba że określisz `content` `contentFiles\any\<target_framework>` ścieżkę pakietu:</span><span class="sxs-lookup"><span data-stu-id="eb244-299">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="eb244-300">Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (zamiast i obu), możesz użyć właściwości , która domyślnie ma wartość `content` `contentFiles` MSBuild "content;contentFiles", ale może być ustawiona na inne `ContentTargetFolders` nazwy folderów.</span><span class="sxs-lookup"><span data-stu-id="eb244-300">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="eb244-301">Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` pliku umieszcza pliki w obszarze lub na podstawie `contentFiles\any\<target_framework>` `contentFiles\<language>\<target_framework>` `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="eb244-301">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="eb244-302">`PackagePath` może być rozdzielany średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="eb244-302">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="eb244-303">Określenie pustej ścieżki pakietu doda plik do katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-303">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="eb244-304">Na przykład następujący kod dodaje `libuv.txt` do , i główny `content\myfiles` `content\samples` pakiet:</span><span class="sxs-lookup"><span data-stu-id="eb244-304">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="eb244-305">Istnieje również właściwość MSBuild , która domyślnie ma wartość `$(IncludeContentInPack)` `true` .</span><span class="sxs-lookup"><span data-stu-id="eb244-305">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="eb244-306">Jeśli jest ona ustawiona na wartość w dowolnym projekcie, zawartość z tego projektu nie zostanie `false` uwzględniona w pakiecie nuget.</span><span class="sxs-lookup"><span data-stu-id="eb244-306">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="eb244-307">Inne metadane specyficzne dla pakietu, które można ustawić dla dowolnego z powyższych elementów, obejmują zestawy i wartości we wpisie ```<PackageCopyToOutput>``` ```<PackageFlatten>``` w danych ```CopyToOutput``` ```Flatten``` ```contentFiles``` wyjściowych nuspec .</span><span class="sxs-lookup"><span data-stu-id="eb244-307">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="eb244-308">Oprócz elementów Zawartości metadane i można również ustawić dla plików za pomocą akcji kompilacji `<Pack>` `<PackagePath>` Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="eb244-308">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="eb244-309">Aby pakiet dołączał nazwę pliku do ścieżki pakietu w przypadku używania wzorców wieloznaków, ścieżka pakietu musi kończyć się znakiem separatora folderu. W przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka wraz z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="eb244-309">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="eb244-310">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eb244-310">IncludeSymbols</span></span>

<span data-ttu-id="eb244-311">W przypadku `MSBuild -t:pack -p:IncludeSymbols=true` korzystania z programu odpowiednie pliki są `.pdb` kopiowane wraz z innymi plikami wyjściowych ( `.dll` , , , , , `.exe` `.winmd` `.xml` `.json` `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="eb244-311">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="eb244-312">Należy pamiętać, `IncludeSymbols=true` że ustawienie tworzy zwykły pakiet *i* pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="eb244-312">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="eb244-313">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eb244-313">IncludeSource</span></span>

<span data-ttu-id="eb244-314">Jest to taka sama jak `IncludeSymbols` , z tą różnicą, że kopiuje pliki źródłowe wraz `.pdb` z plikami.</span><span class="sxs-lookup"><span data-stu-id="eb244-314">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="eb244-315">Wszystkie pliki typu są kopiowane do zachowywania struktury folderów ścieżki `Compile` `src\<ProjectName>\` względnej w wynikowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="eb244-315">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="eb244-316">To samo dzieje się również w przypadku plików źródłowych `ProjectReference` dowolnego, dla którego `TreatAsPackageReference` ustawiono wartość `false` .</span><span class="sxs-lookup"><span data-stu-id="eb244-316">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="eb244-317">Jeśli plik typu Compile znajduje się poza folderem projektu, jest po prostu dodawany do `src\<ProjectName>\` pliku .</span><span class="sxs-lookup"><span data-stu-id="eb244-317">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="eb244-318">Pakowanie wyrażenia licencji lub pliku licencji</span><span class="sxs-lookup"><span data-stu-id="eb244-318">Packing a license expression or a license file</span></span>

<span data-ttu-id="eb244-319">W przypadku korzystania z wyrażenia licencji użyj `PackageLicenseExpression` właściwości .</span><span class="sxs-lookup"><span data-stu-id="eb244-319">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="eb244-320">Aby uzyskać przykład, zobacz [Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="eb244-320">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="eb244-321">Aby dowiedzieć się więcej o wyrażeniach licencji i licencjach akceptowanych przez NuGet .org, zobacz [metadane licencji](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="eb244-321">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="eb244-322">Podczas pakowania pliku licencji użyj właściwości , aby określić ścieżkę pakietu względem katalogu `PackageLicenseFile` głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-322">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eb244-323">Ponadto upewnij się, że plik znajduje się w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="eb244-323">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="eb244-324">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eb244-324">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="eb244-325">Aby uzyskać przykład, zobacz [Przykładowy plik licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="eb244-325">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="eb244-326">Jednocześnie można określić tylko jeden z , i `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` .</span><span class="sxs-lookup"><span data-stu-id="eb244-326">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="eb244-327">Pakowanie pliku bez rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="eb244-327">Packing a file without an extension</span></span>

<span data-ttu-id="eb244-328">W niektórych scenariuszach, takich jak pakowanie pliku licencji, warto dołączyć plik bez rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="eb244-328">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="eb244-329">Ze względów historycznych ścieżki bez rozszerzenia należy traktować NuGet  &  MSBuild jako katalogi.</span><span class="sxs-lookup"><span data-stu-id="eb244-329">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="eb244-330">[Plik bez przykładowego rozszerzenia](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="eb244-330">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="eb244-331">IsTool</span><span class="sxs-lookup"><span data-stu-id="eb244-331">IsTool</span></span>

<span data-ttu-id="eb244-332">W przypadku korzystania z programu wszystkie pliki wyjściowe określone w scenariuszu Zestawów wyjściowych są kopiowane do folderu , `MSBuild -t:pack -p:IsTool=true` a nie do folderu [](#output-assemblies) `tools` `lib` .</span><span class="sxs-lookup"><span data-stu-id="eb244-332">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="eb244-333">Należy zauważyć, że różni się to od `DotNetCliTool` obiektu , który jest określony przez ustawienie w pliku `PackageType` `.csproj` .</span><span class="sxs-lookup"><span data-stu-id="eb244-333">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="eb244-334">Pakowanie przy użyciu `.nuspec` pliku</span><span class="sxs-lookup"><span data-stu-id="eb244-334">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="eb244-335">Mimo że zaleca się, [aby](../reference/msbuild-targets.md#pack-target) zamiast tego uwzględnić wszystkie właściwości, które zwykle znajdują się w pliku projektu, można użyć pliku do `.nuspec` `.nuspec` pakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="eb244-335">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="eb244-336">W przypadku projektu bez zestawu SDK, który używa narzędzia , należy zaimportować plik , aby `PackageReference` można było wykonać zadanie `NuGet.Build.Tasks.Pack.targets` pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-336">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="eb244-337">Aby można było spakować plik, należy przywrócić nuspec projekt.</span><span class="sxs-lookup"><span data-stu-id="eb244-337">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="eb244-338">(Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).</span><span class="sxs-lookup"><span data-stu-id="eb244-338">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="eb244-339">Docelowa framework pliku projektu nie ma znaczenia i nie jest używana podczas pakowania obiektu nuspec .</span><span class="sxs-lookup"><span data-stu-id="eb244-339">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="eb244-340">Następujące trzy właściwości MSBuild są istotne w przypadku pakowania przy użyciu obiektu `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="eb244-340">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="eb244-341">`NuspecFile`: względna lub bezwzględna ścieżka `.nuspec` do pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="eb244-341">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="eb244-342">`NuspecProperties`: rozdzielana średnikami lista par klucz=wartość.</span><span class="sxs-lookup"><span data-stu-id="eb244-342">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="eb244-343">Ze względu na sposób działania analizowania wiersza polecenia należy określić wiele właściwości MSBuild w następujący sposób: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="eb244-343">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="eb244-344">`NuspecBasePath`: ścieżka podstawowa `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="eb244-344">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="eb244-345">Jeśli używasz `dotnet.exe` polecenia do pakowania projektu, użyj polecenia podobnego do następującego:</span><span class="sxs-lookup"><span data-stu-id="eb244-345">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eb244-346">Jeśli używasz MSBuild polecenia do pakowania projektu, użyj polecenia podobnego do następującego:</span><span class="sxs-lookup"><span data-stu-id="eb244-346">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eb244-347">Należy pamiętać, że pakowanie przy użyciu dotnet.exe lub msbuild domyślnie prowadzi również nuspec do budowania projektu.</span><span class="sxs-lookup"><span data-stu-id="eb244-347">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="eb244-348">Można tego uniknąć, przekazując właściwość do dotnet.exe, co jest odpowiednikiem ustawienia w pliku projektu wraz z ustawieniem ```--no-build``` ```<NoBuild>true</NoBuild> ``` w pliku ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` projektu.</span><span class="sxs-lookup"><span data-stu-id="eb244-348">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="eb244-349">Przykład pliku *csproj służącego* do pakowania nuspec pliku to:</span><span class="sxs-lookup"><span data-stu-id="eb244-349">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="eb244-350">Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="eb244-350">Advanced extension points to create customized package</span></span>

<span data-ttu-id="eb244-351">Obiekt `pack` docelowy udostępnia dwa punkty rozszerzenia, które są uruchamiane w kompilacji specyficznej dla wewnętrznej, docelowej struktury.</span><span class="sxs-lookup"><span data-stu-id="eb244-351">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="eb244-352">Punkty rozszerzenia obsługują m.in. zawartość i zestawy specyficzne dla docelowej struktury w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="eb244-352">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="eb244-353">`TargetsForTfmSpecificBuildOutput` target: użyj dla plików w `lib` folderze lub folderze określonym za pomocą `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="eb244-353">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="eb244-354">`TargetsForTfmSpecificContentInPackage` target: użyj dla plików spoza `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="eb244-354">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="eb244-355">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości .</span><span class="sxs-lookup"><span data-stu-id="eb244-355">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="eb244-356">W przypadku plików, które muszą przejść do pliku (domyślnie lib), obiekt docelowy powinien zapisać te pliki w grupie ItemGroup i ustawić `BuildOutputTargetFolder` `BuildOutputInPackage` następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="eb244-356">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="eb244-357">`FinalOutputPath`: ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość jest używana do oceny ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="eb244-357">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="eb244-358">`TargetPath`: (Opcjonalnie) Ustaw, gdy plik musi przejść do podfolderu w programie , na przykład zestawów satelicie, które trafiają do `lib\<TargetFramework>` odpowiednich folderów kulturowych.</span><span class="sxs-lookup"><span data-stu-id="eb244-358">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="eb244-359">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="eb244-359">Defaults to the name of the file.</span></span>

<span data-ttu-id="eb244-360">Przykład:</span><span class="sxs-lookup"><span data-stu-id="eb244-360">Example:</span></span>

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

<span data-ttu-id="eb244-361">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości .</span><span class="sxs-lookup"><span data-stu-id="eb244-361">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="eb244-362">W przypadku plików do uwzględnienia w pakiecie element docelowy powinien zapisać te pliki w grupie ItemGroup i ustawić `TfmSpecificPackageFile` następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="eb244-362">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="eb244-363">`PackagePath`: ścieżka, w której plik powinien być wyjściowy w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="eb244-363">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="eb244-364">NuGet program wydaje ostrzeżenie, jeśli do tej samej ścieżki pakietu zostanie dodany więcej niż jeden plik.</span><span class="sxs-lookup"><span data-stu-id="eb244-364">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="eb244-365">`BuildAction`: akcja kompilacji do przypisania do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w `contentFiles` folderze .</span><span class="sxs-lookup"><span data-stu-id="eb244-365">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="eb244-366">Wartość domyślna to "None".</span><span class="sxs-lookup"><span data-stu-id="eb244-366">Defaults to "None".</span></span>

<span data-ttu-id="eb244-367">Przykład:</span><span class="sxs-lookup"><span data-stu-id="eb244-367">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="eb244-368">przywracanie obiektu docelowego</span><span class="sxs-lookup"><span data-stu-id="eb244-368">restore target</span></span>

<span data-ttu-id="eb244-369">`MSBuild -t:restore` (które `nuget restore` i są dostępne w projektach .NET Core), przywraca pakiety przywołyne `dotnet restore` w pliku projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eb244-369">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="eb244-370">Odczytywanie wszystkich odwołań do projektu</span><span class="sxs-lookup"><span data-stu-id="eb244-370">Read all project to project references</span></span>
1. <span data-ttu-id="eb244-371">Odczytaj właściwości projektu, aby znaleźć pośrednie struktury folderów i obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="eb244-371">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="eb244-372">Przekaż MSBuild dane do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="eb244-372">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="eb244-373">Uruchamianie przywracania</span><span class="sxs-lookup"><span data-stu-id="eb244-373">Run restore</span></span>
1. <span data-ttu-id="eb244-374">Pobieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="eb244-374">Download packages</span></span>
1. <span data-ttu-id="eb244-375">Zapis pliku zasobów, obiektów docelowych i propeduł</span><span class="sxs-lookup"><span data-stu-id="eb244-375">Write assets file, targets, and props</span></span>

<span data-ttu-id="eb244-376">Element `restore` docelowy działa w przypadku projektów w formacie PackageReference.</span><span class="sxs-lookup"><span data-stu-id="eb244-376">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="eb244-377">`MSBuild 16.5+` Program [obsługuje również](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) format `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="eb244-377">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="eb244-378">Obiektu `restore` [docelowego nie należy uruchamiać](#restoring-and-building-with-one-msbuild-command) w połączeniu z obiektem `build` docelowym.</span><span class="sxs-lookup"><span data-stu-id="eb244-378">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="eb244-379">Przywróć właściwości</span><span class="sxs-lookup"><span data-stu-id="eb244-379">Restore properties</span></span>

<span data-ttu-id="eb244-380">Dodatkowe ustawienia przywracania mogą pochodzić MSBuild z właściwości w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="eb244-380">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="eb244-381">Wartości można również ustawiać z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="eb244-381">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="eb244-382">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eb244-382">Property</span></span> | <span data-ttu-id="eb244-383">Opis</span><span class="sxs-lookup"><span data-stu-id="eb244-383">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="eb244-384">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="eb244-384">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="eb244-385">Ścieżka folderu pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eb244-385">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="eb244-386">Ogranicz pobieranie do jednego na raz.</span><span class="sxs-lookup"><span data-stu-id="eb244-386">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="eb244-387">Ścieżka do `Nuget.Config` pliku do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="eb244-387">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="eb244-388">W przypadku wartości true unika używania buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="eb244-388">If true, avoids using cached packages.</span></span> <span data-ttu-id="eb244-389">Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej.](../consume-packages/managing-the-global-packages-and-cache-folders.md)</span><span class="sxs-lookup"><span data-stu-id="eb244-389">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="eb244-390">W przypadku wartości true ignoruje brakujące źródła pakietów lub je ignoruje.</span><span class="sxs-lookup"><span data-stu-id="eb244-390">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="eb244-391">Foldery rezerwowe używane w taki sam sposób jak folder pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eb244-391">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="eb244-392">Dodatkowe źródła do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="eb244-392">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="eb244-393">Dodatkowe foldery rezerwowe do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="eb244-393">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="eb244-394">Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="eb244-394">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="eb244-395">Ścieżka do `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="eb244-395">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="eb244-396">Rozdzielana średnikami lista projektów do przywrócenia, która powinna zawierać ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="eb244-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="eb244-397">Gdy projekty są zbierane za pośrednictwem programu , określa, czy są one MSBuild zbierane przy użyciu `SkipNonexistentTargets` optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="eb244-397">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="eb244-398">Jeśli wartość nie zostanie ustawiona, wartość domyślna to `true` .</span><span class="sxs-lookup"><span data-stu-id="eb244-398">When not set, defaults to `true`.</span></span> <span data-ttu-id="eb244-399">Konsekwencją jest szybkie działanie w przypadku, gdy nie można zaimportować obiektów docelowych projektu.</span><span class="sxs-lookup"><span data-stu-id="eb244-399">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="eb244-400">Folder wyjściowy z wartością domyślną `BaseIntermediateOutputPath` i `obj` folderem .</span><span class="sxs-lookup"><span data-stu-id="eb244-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="eb244-401">W projektach opartych na packageReference program wymusza rozwiązanie wszystkich zależności, nawet jeśli ostatnie przywracanie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="eb244-401">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="eb244-402">Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="eb244-402">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="eb244-403">Nie pomija to pamięci podręcznej http.</span><span class="sxs-lookup"><span data-stu-id="eb244-403">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="eb244-404">Decyduje się na użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="eb244-404">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="eb244-405">Uruchom przywracanie w trybie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="eb244-405">Run restore in locked mode.</span></span> <span data-ttu-id="eb244-406">Oznacza to, że przywracanie nie spowoduje ponownej wyceny zależności.</span><span class="sxs-lookup"><span data-stu-id="eb244-406">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="eb244-407">Niestandardowa lokalizacja pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="eb244-407">A custom location for the lock file.</span></span> <span data-ttu-id="eb244-408">Domyślna lokalizacja znajduje się obok projektu i nosi nazwę `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="eb244-408">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="eb244-409">Wymusza przywracanie, aby ponownie skompilować zależności i zaktualizować plik blokady bez żadnego ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="eb244-409">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="eb244-410">Przełącznik zgody, który przywraca projekty za pomocą packages.config. Obsługa tylko `MSBuild -t:restore` za pomocą.</span><span class="sxs-lookup"><span data-stu-id="eb244-410">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="eb244-411">Przełączenie do korzystania z oceny statycznego MSBuild grafu zamiast standardowej oceny.</span><span class="sxs-lookup"><span data-stu-id="eb244-411">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="eb244-412">Ocena statycznego grafu to funkcja eksperymentalna, która jest znacznie szybsza w przypadku dużych repo i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="eb244-412">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="eb244-413">Przykłady</span><span class="sxs-lookup"><span data-stu-id="eb244-413">Examples</span></span>

<span data-ttu-id="eb244-414">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="eb244-414">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="eb244-415">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="eb244-415">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="eb244-416">Przywracanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="eb244-416">Restore outputs</span></span>

<span data-ttu-id="eb244-417">Przywracanie tworzy następujące pliki w `obj` folderze kompilacji:</span><span class="sxs-lookup"><span data-stu-id="eb244-417">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="eb244-418">Plik</span><span class="sxs-lookup"><span data-stu-id="eb244-418">File</span></span> | <span data-ttu-id="eb244-419">Opis</span><span class="sxs-lookup"><span data-stu-id="eb244-419">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="eb244-420">Zawiera wykres zależności wszystkich odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb244-420">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="eb244-421">Odwołania do MSBuild propeduł zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="eb244-421">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="eb244-422">Odwołania do MSBuild obiektów docelowych zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="eb244-422">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="eb244-423">Przywracanie i budowania za pomocą jednego MSBuild polecenia</span><span class="sxs-lookup"><span data-stu-id="eb244-423">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="eb244-424">Ze względu na fakt, że można przywrócić pakiety, które wprowadzają obiekty docelowe i propeduły, oceny przywracania i kompilacji są NuGet MSBuild uruchamiane z różnymi właściwościami globalnymi.</span><span class="sxs-lookup"><span data-stu-id="eb244-424">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="eb244-425">Oznacza to, że poniższe elementy będą mieć nieprzewidywalne i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="eb244-425">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="eb244-426">Zamiast tego zalecane jest:</span><span class="sxs-lookup"><span data-stu-id="eb244-426">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="eb244-427">Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build` .</span><span class="sxs-lookup"><span data-stu-id="eb244-427">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="eb244-428">Przywracanie packageReference i packages.config projektów za pomocą MSBuild</span><span class="sxs-lookup"><span data-stu-id="eb244-428">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="eb244-429">W MSBuild przypadku programu 16.5 packages.config są również obsługiwane dla programu `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="eb244-429">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="eb244-430">`packages.config` Przywracanie jest dostępne tylko z `MSBuild 16.5+` , a nie z `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="eb244-430">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="eb244-431">Przywracanie za pomocą MSBuild statycznej oceny grafu</span><span class="sxs-lookup"><span data-stu-id="eb244-431">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="eb244-432">W MSBuild programie 16.6+ dodano eksperymentalną funkcję do korzystania z oceny statycznego grafu z wiersza polecenia, która znacznie poprawia czas przywracania w NuGet dużych repozytoriach.</span><span class="sxs-lookup"><span data-stu-id="eb244-432">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="eb244-433">Alternatywnie można ją włączyć, ustawiając właściwość w Directory.Build.Props.</span><span class="sxs-lookup"><span data-stu-id="eb244-433">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="eb244-434">Od Visual Studio 2019.x i 5.x ta funkcja jest uznawana za eksperymentalną i NuGet zrezygnuje z jej otrzymywania.</span><span class="sxs-lookup"><span data-stu-id="eb244-434">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="eb244-435">Postępuj [ NuGet zgodnie z /Home#9803,](https://github.com/NuGet/Home/issues/9803) aby uzyskać szczegółowe informacje na temat tego, kiedy ta funkcja będzie domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="eb244-435">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="eb244-436">Statyczne przywracanie grafu zmienia część msbuild przywracania, odczytywanie i ocenianie projektu, ale nie algorytm przywracania!</span><span class="sxs-lookup"><span data-stu-id="eb244-436">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="eb244-437">Algorytm przywracania jest taki sam we wszystkich narzędziach NuGet NuGet (exe, MSBuild exe, dotnet.exe i Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="eb244-437">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="eb244-438">W bardzo nielicznych scenariuszach przywracanie statycznego grafu może zachowywać się inaczej niż bieżące przywracanie, a niektóre zadeklarowane elementy PackageReferences lub ProjectReferences mogą być brakujące.</span><span class="sxs-lookup"><span data-stu-id="eb244-438">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="eb244-439">Aby ułatwić sobie rozum, podczas migracji do statycznego przywracania grafu rozważ uruchomienie:</span><span class="sxs-lookup"><span data-stu-id="eb244-439">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="eb244-440">NuGet Nie *należy zgłaszać* żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="eb244-440">NuGet should *not* report any changes.</span></span> <span data-ttu-id="eb244-441">Jeśli widzisz niezgodność, prosimy o nadsyłanie problemu na [ NuGet stronie /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="eb244-441">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="eb244-442">Zastępowanie jednej biblioteki z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="eb244-442">Replacing one library from a restore graph</span></span>

<span data-ttu-id="eb244-443">Jeśli przywracanie przywraca niewłaściwy zestaw, można wykluczyć ten domyślny wybór pakietów i zastąpić go własnym wyborem.</span><span class="sxs-lookup"><span data-stu-id="eb244-443">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="eb244-444">Najpierw przy użyciu najwyższego poziomu `PackageReference` wyklucz wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="eb244-444">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="eb244-445">Następnie dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="eb244-445">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```