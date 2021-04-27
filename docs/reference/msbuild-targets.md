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
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067313"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="1e6bc-103">NuGet spakuj i przywróć jako MSBuild obiekty docelowe</span><span class="sxs-lookup"><span data-stu-id="1e6bc-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="1e6bc-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="1e6bc-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="1e6bc-105">W [formacie PackageReference](../consume-packages/package-references-in-project-files.md) program 4.0+ może przechowywać wszystkie metadane manifestu bezpośrednio w pliku projektu, NuGet zamiast używać oddzielnego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="1e6bc-106">W przypadku programu 15.1+ jest również pierwszoklasowym obywatelem z celami i , MSBuild NuGet jak MSBuild `pack` `restore` opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="1e6bc-107">Te obiekty docelowe umożliwiają pracę z usługą tak NuGet jak z innymi zadaniami lub MSBuild obiektami docelowymi.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="1e6bc-108">Aby uzyskać instrukcje NuGet dotyczące tworzenia pakietu przy użyciu polecenia , zobacz Tworzenie pakietu przy użyciu MSBuild [ NuGet polecenia MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="1e6bc-109">(W przypadku NuGet W wersji 3.x lub starszej zamiast tego należy użyć poleceń [pakowania](../reference/cli-reference/cli-ref-pack.md) [i](../reference/cli-reference/cli-ref-restore.md) przywracania za pośrednictwem interfejsu NuGet wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="1e6bc-110">Kolejność kompilowania obiektów docelowych</span><span class="sxs-lookup"><span data-stu-id="1e6bc-110">Target build order</span></span>

<span data-ttu-id="1e6bc-111">Ponieważ `pack` i `restore` są  MSBuild celami, możesz uzyskać do nich dostęp, aby ulepszyć przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="1e6bc-112">Załóżmy na przykład, że chcesz skopiować pakiet do udziału sieciowego po jego spakowaniu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="1e6bc-113">Możesz to zrobić, dodając następujące elementy w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="1e6bc-114">Podobnie można napisać MSBuild zadanie, napisać własny element docelowy i korzystać z właściwości w NuGet MSBuild zadaniu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="1e6bc-115">`$(OutputPath)` jest względny i oczekuje, że uruchamiasz polecenie z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="1e6bc-116">element docelowy pakietu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-116">pack target</span></span>

<span data-ttu-id="1e6bc-117">W przypadku projektów .NET, które używają formatu , przy użyciu rysuje dane wejściowe z pliku projektu do `PackageReference` `msbuild -t:pack` użycia podczas tworzenia NuGet pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="1e6bc-118">W poniższej tabeli MSBuild opisano właściwości, które można dodać do pliku projektu w pierwszym `<PropertyGroup>` węźle.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="1e6bc-119">Te zmiany można łatwo wprowadzić w programie Visual Studio 2017 lub nowszym, klikając prawym przyciskiem myszy projekt i wybierając pozycję Edytuj **{project_name}** w menu kontekstowym.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="1e6bc-120">Dla wygody tabela jest zorganizowana według równoważnej właściwości w [ `.nuspec` pliku](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1e6bc-121">`Owners` Właściwości `Summary` i z nie są obsługiwane w `.nuspec` programie MSBuild .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="1e6bc-122">nuspecAtrybut/wartość</span><span class="sxs-lookup"><span data-stu-id="1e6bc-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="1e6bc-123">MSBuild Właściwość</span><span class="sxs-lookup"><span data-stu-id="1e6bc-123">MSBuild Property</span></span> | <span data-ttu-id="1e6bc-124">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1e6bc-124">Default</span></span> | <span data-ttu-id="1e6bc-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1e6bc-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="1e6bc-126">`$(AssemblyName)` Z MSBuild</span><span class="sxs-lookup"><span data-stu-id="1e6bc-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="1e6bc-127">Wersja</span><span class="sxs-lookup"><span data-stu-id="1e6bc-127">Version</span></span> | <span data-ttu-id="1e6bc-128">Jest to zgodne z semver, na przykład `1.0.0` `1.0.0-beta` , lub `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="1e6bc-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="1e6bc-129">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-129">empty</span></span> | <span data-ttu-id="1e6bc-130">Zastępowanie `PackageVersion` ustawień `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="1e6bc-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="1e6bc-131">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-131">empty</span></span> | <span data-ttu-id="1e6bc-132">`$(VersionSuffix)` z MSBuild .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="1e6bc-133">Zastępowanie `PackageVersion` ustawień `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="1e6bc-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="1e6bc-134">Nazwa użytkownika bieżącego użytkownika</span><span class="sxs-lookup"><span data-stu-id="1e6bc-134">Username of the current user</span></span> | <span data-ttu-id="1e6bc-135">Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów na nuget.org. Są one wyświetlane w galerii na nuget.org i są używane do odsyłania pakietów NuGet przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="1e6bc-136">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1e6bc-136">N/A</span></span> | <span data-ttu-id="1e6bc-137">Nie ma w nuspec</span><span class="sxs-lookup"><span data-stu-id="1e6bc-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="1e6bc-138">Element `PackageId`.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-138">The `PackageId`</span></span> | <span data-ttu-id="1e6bc-139">Przyjazny dla człowieka tytuł pakietu, zwykle używany w interfejsie użytkownika, jest wyświetlany jako nuget.org i Menedżer pakietów w Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="1e6bc-140">"Opis pakietu"</span><span class="sxs-lookup"><span data-stu-id="1e6bc-140">"Package Description"</span></span> | <span data-ttu-id="1e6bc-141">Długi opis zestawu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-141">A long description for the assembly.</span></span> <span data-ttu-id="1e6bc-142">Jeśli nie zostanie określony, ta właściwość jest również używana `PackageDescription` jako opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="1e6bc-143">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-143">empty</span></span> | <span data-ttu-id="1e6bc-144">Szczegóły praw autorskich dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="1e6bc-145">Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="1e6bc-146">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-146">empty</span></span> | <span data-ttu-id="1e6bc-147">Odpowiada `<license type="expression">` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="1e6bc-148">Zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="1e6bc-149">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-149">empty</span></span> | <span data-ttu-id="1e6bc-150">Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji niestandardowej lub licencji, do których nie przypisano identyfikatora SPDX.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="1e6bc-151">Musisz jawnie spakować plik licencji, do których się odwołujesz.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="1e6bc-152">Odpowiada `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="1e6bc-153">Zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="1e6bc-154">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-154">empty</span></span> | <span data-ttu-id="1e6bc-155">`PackageLicenseUrl` jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="1e6bc-156">Zamiast `PackageLicenseExpression` tego użyj lub `PackageLicenseFile` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="1e6bc-157">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="1e6bc-158">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-158">empty</span></span> | <span data-ttu-id="1e6bc-159">Ścieżka do obrazu w pakiecie do użycia jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="1e6bc-160">Musisz jawnie spakować plik obrazu ikony, do których się odwołujesz.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="1e6bc-161">Aby uzyskać więcej informacji, zobacz [Pakowanie pliku obrazu ikony i](#packing-an-icon-image-file) [ `icon` metadanych](./nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="1e6bc-162">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-162">empty</span></span> | <span data-ttu-id="1e6bc-163">`PackageIconUrl` jest przestarzała na rzecz `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="1e6bc-164">Jednak aby uzyskać najlepsze środowisko na 1. łydce, oprócz wartości należy `PackageIconUrl` określić wartość `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="1e6bc-165">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-165">empty</span></span> | <span data-ttu-id="1e6bc-166">Należy jawnie spakować przywołyowany plik readme.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="1e6bc-167">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-167">empty</span></span> | <span data-ttu-id="1e6bc-168">Rozdzielana średnikami lista tagów, która wyznacza pakiet.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="1e6bc-169">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-169">empty</span></span> | <span data-ttu-id="1e6bc-170">Informacje o wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="1e6bc-171">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-171">empty</span></span> | <span data-ttu-id="1e6bc-172">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="1e6bc-173">Przykład: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="1e6bc-174">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-174">empty</span></span> | <span data-ttu-id="1e6bc-175">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-175">Repository type.</span></span> <span data-ttu-id="1e6bc-176">Przykłady: `git` (ustawienie domyślne), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="1e6bc-177">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-177">empty</span></span> | <span data-ttu-id="1e6bc-178">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-178">Optional repository branch information.</span></span> <span data-ttu-id="1e6bc-179">`RepositoryUrl` Należy również określić dla tej właściwości, która ma zostać uwzględniona.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1e6bc-180">Przykład: *master* NuGet (4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="1e6bc-181">puste</span><span class="sxs-lookup"><span data-stu-id="1e6bc-181">empty</span></span> | <span data-ttu-id="1e6bc-182">Opcjonalne zatwierdzenie repozytorium lub zestaw zmian w celu wskazania źródła, z którego został s zbudowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="1e6bc-183">`RepositoryUrl` Należy również określić dla tej właściwości do dołączona.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1e6bc-184">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | <span data-ttu-id="1e6bc-185">Wskazuje przeznaczenie pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-185">Indicates the package's intended use.</span></span> <span data-ttu-id="1e6bc-186">Typy pakietów używają tego samego formatu co identyfikatory pakietów i są rozdzielane znakiem `;` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-186">Package types use the same format as package IDs and are delimited by `;`.</span></span> <span data-ttu-id="1e6bc-187">Typy pakietów mogą być wersjonarowane przez dołączenie `,` ciągu [`Version`](/dotnet/api/system.version) i .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-187">Package types may be versioned by appending a `,` and a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="1e6bc-188">Zobacz [Ustawianie NuGet typu pakietu](../create-packages/set-package-type.md) ( NuGet 3.5.0+).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-188">See [Set a NuGet package type](../create-packages/set-package-type.md) (NuGet 3.5.0+).</span></span> |
| `Summary` | <span data-ttu-id="1e6bc-189">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="1e6bc-189">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="1e6bc-190">docelowe dane wejściowe pakietu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-190">pack target inputs</span></span>

| <span data-ttu-id="1e6bc-191">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1e6bc-191">Property</span></span> | <span data-ttu-id="1e6bc-192">Opis</span><span class="sxs-lookup"><span data-stu-id="1e6bc-192">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="1e6bc-193">Wartość logiczna określająca, czy można spakować projekt.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-193">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="1e6bc-194">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-194">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="1e6bc-195">Ustaw na `true` , aby pominąć zależności pakietu z wygenerowanego NuGet pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-195">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="1e6bc-196">Określa wersję pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-196">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="1e6bc-197">Akceptuje wszystkie formy ciągu NuGet wersji.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-197">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="1e6bc-198">Wartość domyślna to wartość , czyli właściwości `$(Version)` `Version` w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-198">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="1e6bc-199">Określa nazwę pakietu wynikowego.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-199">Specifies the name for the resulting package.</span></span> <span data-ttu-id="1e6bc-200">Jeśli nie zostanie określony, `pack` operacja domyślnie będzie używać nazwy katalogu lub jako nazwy `AssemblyName` pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-200">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="1e6bc-201">Długi opis pakietu dla wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-201">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="1e6bc-202">Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów na nuget.org. Są one wyświetlane w galerii na nuget.org i są używane do odsyłania pakietów NuGet przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-202">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="1e6bc-203">Długi opis zestawu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-203">A long description for the assembly.</span></span> <span data-ttu-id="1e6bc-204">Jeśli nie zostanie określony, ta właściwość jest również używana `PackageDescription` jako opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-204">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="1e6bc-205">Szczegóły praw autorskich dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-205">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="1e6bc-206">Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-206">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="1e6bc-207">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-207">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="1e6bc-208">Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-208">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="1e6bc-209">W `PackageReference` przypadku programu (4.8+) ta flaga oznacza również, że zasoby w czasie kompilacji NuGet są wykluczone z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-209">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="1e6bc-210">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference (Obsługa](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)zależności development dla packageReference).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-210">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="1e6bc-211">Identyfikator [licencji SPDX](https://spdx.org/licenses/) lub wyrażenie, na przykład `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-211">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="1e6bc-212">Aby uzyskać więcej informacji, zobacz [Pakowanie wyrażenia licencji lub pliku licencji](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-212">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="1e6bc-213">Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji niestandardowej lub licencji, która nie ma przypisanego identyfikatora SPDX.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-213">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="1e6bc-214">`PackageLicenseUrl` jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-214">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="1e6bc-215">Zamiast `PackageLicenseExpression` tego użyj lub `PackageLicenseFile` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-215">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="1e6bc-216">Określa ścieżkę ikony pakietu względem katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-216">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="1e6bc-217">Aby uzyskać więcej informacji, zobacz [Pakowanie pliku obrazu ikony](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-217">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="1e6bc-218">Informacje o wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-218">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="1e6bc-219">Readme dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-219">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="1e6bc-220">Rozdzielana średnikami lista tagów, która wyznacza pakiet.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-220">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="1e6bc-221">Określa ścieżkę wyjściową, w której spakowany pakiet zostanie porzucony.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-221">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="1e6bc-222">Wartość domyślna to `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-222">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="1e6bc-223">Ta wartość logiczna wskazuje, czy pakiet powinien utworzyć dodatkowy pakiet symboli podczas pakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-223">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="1e6bc-224">Format pakietu symboli jest kontrolowany przez `SymbolPackageFormat` właściwość .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-224">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="1e6bc-225">Aby uzyskać więcej informacji, zobacz [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-225">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="1e6bc-226">Ta wartość logiczna wskazuje, czy proces pakietu powinien utworzyć pakiet źródłowy.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-226">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="1e6bc-227">Pakiet źródłowy zawiera kod źródłowy biblioteki, a także pliki PDB.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-227">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="1e6bc-228">Pliki źródłowe są umieszczane `src/ProjectName` w katalogu w wynikowym pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-228">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="1e6bc-229">Aby uzyskać więcej informacji, zobacz [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-229">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="1e6bc-230">Określa, czy wszystkie pliki wyjściowe są kopiowane do folderu *tools,* a nie do *folderu lib.*</span><span class="sxs-lookup"><span data-stu-id="1e6bc-230">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="1e6bc-231">Aby uzyskać więcej informacji, zobacz [IsTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-231">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="1e6bc-232">Adres URL repozytorium używany do klonowania lub pobierania kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-232">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="1e6bc-233">Przykład: *https://github.com/ NuGet / NuGet . Client.git*.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-233">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="1e6bc-234">Typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-234">Repository type.</span></span> <span data-ttu-id="1e6bc-235">Przykłady: `git` (ustawienie domyślne), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-235">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="1e6bc-236">Opcjonalne informacje o gałęzi repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-236">Optional repository branch information.</span></span> <span data-ttu-id="1e6bc-237">`RepositoryUrl` Należy również określić dla tej właściwości do dołączona.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-237">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1e6bc-238">Przykład: *master* NuGet (4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-238">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="1e6bc-239">Opcjonalne zatwierdzenie repozytorium lub zestaw zmian w celu wskazania źródła, z którego został s zbudowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-239">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="1e6bc-240">`RepositoryUrl` Należy również określić dla tej właściwości do dołączona.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-240">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="1e6bc-241">Przykład: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-241">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="1e6bc-242">Określa format pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-242">Specifies the format of the symbols package.</span></span> <span data-ttu-id="1e6bc-243">W przypadku pliku "symbols.nupkg" starszy pakiet symboli jest tworzony z rozszerzeniem *.symbols.nupkg* zawierającym pliki PDB, DLL i inne pliki wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-243">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="1e6bc-244">W przypadku polecenia "snupkg" tworzony jest pakiet symboli snupkg zawierający przenośne pliki PDB.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-244">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="1e6bc-245">Wartość domyślna to "symbols.nupkg".</span><span class="sxs-lookup"><span data-stu-id="1e6bc-245">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="1e6bc-246">Określa, `pack` że nie należy uruchamiać analizy pakietu po sbudowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-246">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="1e6bc-247">Określa minimalną wersję klienta, który może zainstalować ten pakiet, wymuszaną przez nuget.exe NuGet i Visual Studio Menedżer pakietów.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-247">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="1e6bc-248">Ta wartość logiczna określa, czy zestawy wyjściowe kompilacji powinny być spakowane w pliku *nupkg,* czy nie.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-248">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="1e6bc-249">Ta wartość logiczna określa, czy jakiekolwiek elementy, które mają typ , są automatycznie uwzględniane `Content` w wynikowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-249">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="1e6bc-250">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-250">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="1e6bc-251">Określa folder, w którym mają być umieszczane zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-251">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="1e6bc-252">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-252">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="1e6bc-253">Aby uzyskać więcej informacji, zobacz [Output assemblies (Zestawy wyjściowe).](#output-assemblies)</span><span class="sxs-lookup"><span data-stu-id="1e6bc-253">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="1e6bc-254">Określa domyślną lokalizację, w której powinny przejść wszystkie pliki zawartości, jeśli `PackagePath` nie zostanie określona dla nich.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-254">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="1e6bc-255">Wartość domyślna to "content;contentFiles".</span><span class="sxs-lookup"><span data-stu-id="1e6bc-255">The default value is "content;contentFiles".</span></span> <span data-ttu-id="1e6bc-256">Aby uzyskać więcej informacji, zobacz [Including content in a package](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-256">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="1e6bc-257">Względna lub bezwzględna ścieżka *.nuspec* do pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-257">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="1e6bc-258">Jeśli to określono, są używane **wyłącznie do pakowania** informacji, a żadne informacje w projektach nie są używane.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-258">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="1e6bc-259">Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file)</span><span class="sxs-lookup"><span data-stu-id="1e6bc-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="1e6bc-260">Ścieżka podstawowa *.nuspec* pliku.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-260">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="1e6bc-261">Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file)</span><span class="sxs-lookup"><span data-stu-id="1e6bc-261">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="1e6bc-262">Rozdzielana średnikami lista par klucz=wartość.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-262">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="1e6bc-263">Aby uzyskać więcej informacji, zobacz [Pakowanie przy użyciu . .nuspec ](#packing-using-a-nuspec-file)</span><span class="sxs-lookup"><span data-stu-id="1e6bc-263">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="1e6bc-264">scenariusze pakietu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-264">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="1e6bc-265">Pomijanie zależności</span><span class="sxs-lookup"><span data-stu-id="1e6bc-265">Suppressing dependencies</span></span>

<span data-ttu-id="1e6bc-266">Aby pominąć zależności pakietu z wygenerowanego pakietu, ustaw wartość , aby umożliwić pominięcie wszystkich zależności z wygenerowanego NuGet `SuppressDependenciesWhenPacking` pliku `true` nupkg.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-266">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="1e6bc-267">`PackageIconUrl` jest przestarzała na rzecz [`PackageIcon`](#packageicon) właściwości .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-267">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="1e6bc-268">Począwszy od NuGet wersji 5.3 i Visual Studio 2019 w wersji 16.3, program zgłasza ostrzeżenie `pack` [NU5048,](./errors-and-warnings/nu5048.md) jeśli metadane pakietu określają tylko wartość `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-268">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="1e6bc-269">Aby zachować zgodność z poprzednimi wersjami z klientami i źródłami, które nie obsługują jeszcze `PackageIcon` usługi , określ wartości i `PackageIcon` `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-269">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="1e6bc-270">Visual Studio obsługuje `PackageIcon` pakiety pochodzące ze źródła opartego na folderach.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-270">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="1e6bc-271">Pakowanie pliku obrazu ikony</span><span class="sxs-lookup"><span data-stu-id="1e6bc-271">Packing an icon image file</span></span>

<span data-ttu-id="1e6bc-272">Podczas pakowania pliku obrazu ikony użyj właściwości , aby określić ścieżkę pliku ikony względem katalogu `PackageIcon` głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-272">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="1e6bc-273">Ponadto upewnij się, że plik znajduje się w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-273">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="1e6bc-274">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-274">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="1e6bc-275">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-275">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="1e6bc-276">Zalecamy rozdzielczość obrazu 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-276">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="1e6bc-277">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-277">For example:</span></span>

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

<span data-ttu-id="1e6bc-278">[Przykład ikony pakietu](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-278">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="1e6bc-279">Aby uzyskać odpowiednik, zobacz odwołanie do nuspec [ nuspec ikony](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-279">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="1e6bc-280">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="1e6bc-280">PackageReadmeFile</span></span>

<span data-ttu-id="1e6bc-281">*Obsługiwane w **NuGet wersji 5.10.0 (wersja zapoznawcza 2)**  /  **zestawu .NET SDK 5.0.300** i jego wersjach*</span><span class="sxs-lookup"><span data-stu-id="1e6bc-281">*Supported with **NuGet 5.10.0 preview 2** / **.NET SDK 5.0.300** and above*</span></span>

<span data-ttu-id="1e6bc-282">Podczas pakowania pliku readme należy użyć właściwości , aby określić ścieżkę pakietu względem katalogu `PackageReadmeFile` głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-282">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="1e6bc-283">Oprócz tego należy się upewnić, że plik znajduje się w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-283">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="1e6bc-284">Obsługiwane formaty plików obejmują tylko markdown *(md).*</span><span class="sxs-lookup"><span data-stu-id="1e6bc-284">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="1e6bc-285">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-285">For example:</span></span>

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

<span data-ttu-id="1e6bc-286">Aby uzyskać nuspec odpowiednik, zapoznaj się z odwołaniem [ nuspec do readme](nuspec.md#readme).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-286">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="1e6bc-287">Zestawy wyjściowe</span><span class="sxs-lookup"><span data-stu-id="1e6bc-287">Output assemblies</span></span>

<span data-ttu-id="1e6bc-288">`nuget pack` Kopiuje pliki wyjściowe z `.exe` rozszerzeniami `.dll` , , , , i `.xml` `.winmd` `.json` `.pri` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-288">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="1e6bc-289">Kopiowane pliki wyjściowe zależą od tego, MSBuild co zapewnia obiekt `BuiltOutputProjectGroup` docelowy.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-289">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="1e6bc-290">Istnieją dwie właściwości, których można użyć w pliku projektu lub wierszu polecenia, aby kontrolować, MSBuild  gdzie trafiają zestawy wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-290">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="1e6bc-291">`IncludeBuildOutput`: wartość logiczna, która określa, czy zestawy wyjściowe kompilacji powinny być zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-291">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="1e6bc-292">`BuildOutputTargetFolder`: określa folder, w którym powinny zostać umieszczone zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-292">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="1e6bc-293">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-293">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="1e6bc-294">Odwołania do pakietu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-294">Package references</span></span>

<span data-ttu-id="1e6bc-295">Zobacz [Odwołania do pakietu w plikach projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-295">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="1e6bc-296">Odwołania projektu do projektu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-296">Project to project references</span></span>

<span data-ttu-id="1e6bc-297">Odwołania projektu do projektu są domyślnie traktowane jako odwołania NuGet do pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-297">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="1e6bc-298">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-298">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="1e6bc-299">Możesz również dodać następujące metadane do odwołania do projektu:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-299">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="1e6bc-300">Łącznie z zawartością w pakiecie</span><span class="sxs-lookup"><span data-stu-id="1e6bc-300">Including content in a package</span></span>

<span data-ttu-id="1e6bc-301">Aby dołączyć zawartość, dodaj dodatkowe metadane do istniejącego `<Content>` elementu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-301">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="1e6bc-302">Domyślnie wszystko typu "Zawartość" jest uwzględniane w pakiecie, chyba że zastąpisz wpisami podobnymi do następujących:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-302">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="1e6bc-303">Domyślnie wszystko jest dodawane do katalogu głównego folderu i w pakiecie i zachowuje względną strukturę folderów, chyba że określisz `content` `contentFiles\any\<target_framework>` ścieżkę pakietu:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-303">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="1e6bc-304">Jeśli chcesz skopiować całą zawartość tylko do określonych folderów głównych (zamiast i obu), możesz użyć właściwości , która domyślnie ma wartość `content` `contentFiles` MSBuild "content;contentFiles", ale może być ustawiona na inne `ContentTargetFolders` nazwy folderów.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-304">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="1e6bc-305">Należy pamiętać, że po prostu określenie "contentFiles" w `ContentTargetFolders` pliku umieszcza pliki w obszarze lub na podstawie `contentFiles\any\<target_framework>` `contentFiles\<language>\<target_framework>` `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-305">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="1e6bc-306">`PackagePath` może być rozdzielany średnikami zestaw ścieżek docelowych.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-306">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="1e6bc-307">Określenie pustej ścieżki pakietu doda plik do katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-307">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="1e6bc-308">Na przykład następujący kod dodaje `libuv.txt` do , i główny `content\myfiles` `content\samples` pakiet:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-308">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="1e6bc-309">Istnieje również właściwość MSBuild , która domyślnie ma wartość `$(IncludeContentInPack)` `true` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-309">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="1e6bc-310">Jeśli jest ona ustawiona na wartość w dowolnym projekcie, zawartość z tego projektu nie zostanie `false` uwzględniona w pakiecie nuget.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-310">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="1e6bc-311">Inne metadane specyficzne dla pakietu, które można ustawić dla dowolnego z powyższych elementów, obejmują zestawy i wartości we wpisie ```<PackageCopyToOutput>``` ```<PackageFlatten>``` w danych ```CopyToOutput``` ```Flatten``` ```contentFiles``` wyjściowych nuspec .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-311">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="1e6bc-312">Oprócz elementów zawartości metadane i można również ustawić dla plików z akcją kompilacji `<Pack>` `<PackagePath>` Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource lub None.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-312">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="1e6bc-313">Aby pakiet dołączał nazwę pliku do ścieżki pakietu w przypadku używania wzorców wieloznaków, ścieżka pakietu musi kończyć się znakiem separatora folderu. W przeciwnym razie ścieżka pakietu jest traktowana jako pełna ścieżka wraz z nazwą pliku.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-313">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="1e6bc-314">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="1e6bc-314">IncludeSymbols</span></span>

<span data-ttu-id="1e6bc-315">W przypadku `MSBuild -t:pack -p:IncludeSymbols=true` korzystania z programu odpowiednie pliki są `.pdb` kopiowane wraz z innymi plikami wyjściowych ( `.dll` , , , , , `.exe` `.winmd` `.xml` `.json` `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-315">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="1e6bc-316">Należy pamiętać, `IncludeSymbols=true` że ustawienie tworzy zwykły pakiet *i* pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-316">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="1e6bc-317">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="1e6bc-317">IncludeSource</span></span>

<span data-ttu-id="1e6bc-318">Jest to taka sama jak , z tą różnicą, że kopiuje również pliki źródłowe `IncludeSymbols` `.pdb` wraz z plikami.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-318">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="1e6bc-319">Wszystkie pliki typu są kopiowane do zachowywania struktury folderów ścieżki `Compile` `src\<ProjectName>\` względnej w wynikowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-319">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="1e6bc-320">To samo dzieje się również w przypadku plików źródłowych dowolnego `ProjectReference` z nich, dla `TreatAsPackageReference` którego ustawiono wartość `false` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-320">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="1e6bc-321">Jeśli plik typu Compile znajduje się poza folderem projektu, jest po prostu dodawany do `src\<ProjectName>\` pliku .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-321">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="1e6bc-322">Pakowanie wyrażenia licencji lub pliku licencji</span><span class="sxs-lookup"><span data-stu-id="1e6bc-322">Packing a license expression or a license file</span></span>

<span data-ttu-id="1e6bc-323">W przypadku korzystania z wyrażenia licencji użyj `PackageLicenseExpression` właściwości .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-323">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="1e6bc-324">Aby uzyskać przykład, zobacz [Przykład wyrażenia licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-324">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="1e6bc-325">Aby dowiedzieć się więcej o wyrażeniach licencji i licencjach akceptowanych przez NuGet .org, zobacz [metadane licencji](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-325">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="1e6bc-326">Podczas pakowania pliku licencji użyj właściwości , aby określić ścieżkę pakietu względem katalogu `PackageLicenseFile` głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-326">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="1e6bc-327">Ponadto upewnij się, że plik znajduje się w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-327">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="1e6bc-328">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-328">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="1e6bc-329">Aby uzyskać przykład, zobacz [Przykładowy plik licencji](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-329">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="1e6bc-330">Jednocześnie można określić tylko jeden z , i `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-330">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="1e6bc-331">Pakowanie pliku bez rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="1e6bc-331">Packing a file without an extension</span></span>

<span data-ttu-id="1e6bc-332">W niektórych scenariuszach, takich jak pakowanie pliku licencji, warto dołączyć plik bez rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-332">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="1e6bc-333">Ze względów NuGet  &  MSBuild historycznych ścieżki bez rozszerzenia należy traktować jako katalogi.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-333">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="1e6bc-334">[Plik bez przykładowego rozszerzenia](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-334">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="1e6bc-335">IsTool</span><span class="sxs-lookup"><span data-stu-id="1e6bc-335">IsTool</span></span>

<span data-ttu-id="1e6bc-336">W przypadku korzystania z programu wszystkie pliki wyjściowe określone w scenariuszu Zestawów wyjściowych są kopiowane do folderu , `MSBuild -t:pack -p:IsTool=true` a nie do folderu [](#output-assemblies) `tools` `lib` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-336">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="1e6bc-337">Należy zauważyć, że różni się to od `DotNetCliTool` obiektu , który jest określony przez ustawienie w pliku `PackageType` `.csproj` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-337">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="1e6bc-338">Pakowanie przy użyciu `.nuspec` pliku</span><span class="sxs-lookup"><span data-stu-id="1e6bc-338">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="1e6bc-339">Mimo że zaleca się, [aby](../reference/msbuild-targets.md#pack-target) zamiast tego uwzględnić wszystkie właściwości, które zwykle znajdują się w pliku projektu, można użyć pliku do `.nuspec` `.nuspec` pakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-339">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="1e6bc-340">W przypadku projektu bez zestawu SDK, który używa narzędzia , należy zaimportować plik , aby `PackageReference` można było wykonać zadanie `NuGet.Build.Tasks.Pack.targets` pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-340">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="1e6bc-341">Aby można było spakować plik, należy przywrócić nuspec projekt.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-341">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="1e6bc-342">(Projekt w stylu zestawu SDK domyślnie zawiera elementy docelowe pakietu).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-342">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="1e6bc-343">Docelowa framework pliku projektu nie ma znaczenia i nie jest używana podczas pakowania obiektu nuspec .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-343">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="1e6bc-344">Następujące trzy właściwości MSBuild są istotne w przypadku pakowania przy użyciu obiektu `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="1e6bc-344">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="1e6bc-345">`NuspecFile`: względna lub bezwzględna ścieżka `.nuspec` do pliku używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-345">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="1e6bc-346">`NuspecProperties`: rozdzielana średnikami lista par klucz=wartość.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-346">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="1e6bc-347">Ze względu na sposób działania analizowania wiersza polecenia należy określić wiele właściwości MSBuild w następujący sposób: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-347">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="1e6bc-348">`NuspecBasePath`: ścieżka podstawowa `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-348">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="1e6bc-349">Jeśli używasz `dotnet.exe` polecenia do pakowania projektu, użyj polecenia podobnego do następującego:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-349">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1e6bc-350">Jeśli używasz MSBuild polecenia do pakowania projektu, użyj polecenia podobnego do następującego:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-350">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1e6bc-351">Należy pamiętać, że pakowanie przy użyciu dotnet.exe lub msbuild domyślnie prowadzi również nuspec do budowania projektu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-351">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="1e6bc-352">Można tego uniknąć, przekazując właściwość do dotnet.exe, co jest odpowiednikiem ustawienia w pliku projektu wraz z ustawieniem ```--no-build``` ```<NoBuild>true</NoBuild> ``` w pliku ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` projektu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-352">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="1e6bc-353">Przykładem pliku *csproj do* pakowania nuspec pliku jest:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-353">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="1e6bc-354">Zaawansowane punkty rozszerzenia do tworzenia dostosowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-354">Advanced extension points to create customized package</span></span>

<span data-ttu-id="1e6bc-355">Obiekt `pack` docelowy udostępnia dwa punkty rozszerzenia, które są uruchamiane w kompilacji specyficznej dla wewnętrznej, docelowej struktury.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-355">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="1e6bc-356">Punkty rozszerzenia obsługują m.in. zawartość i zestawy specyficzne dla struktury docelowej w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-356">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="1e6bc-357">`TargetsForTfmSpecificBuildOutput`target: użyj dla plików w `lib` folderze lub folderze określonym za pomocą . `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="1e6bc-357">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="1e6bc-358">`TargetsForTfmSpecificContentInPackage` target: użyj dla plików spoza `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-358">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="1e6bc-359">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificBuildOutput)` właściwości .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-359">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="1e6bc-360">Dla wszystkich plików, które muszą przejść do pliku (domyślnie lib), obiekt docelowy powinien zapisać te pliki w grupie ItemGroup i ustawić `BuildOutputTargetFolder` `BuildOutputInPackage` następujące dwie wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-360">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="1e6bc-361">`FinalOutputPath`: ścieżka bezwzględna pliku; Jeśli nie zostanie podany, tożsamość jest używana do oceny ścieżki źródłowej.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-361">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="1e6bc-362">`TargetPath`: (Opcjonalnie) Ustaw, gdy plik musi przejść do podfolderu w programie , na przykład zestawów satelicie, które są dostępne w `lib\<TargetFramework>` odpowiednich folderach kulturowych.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-362">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="1e6bc-363">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-363">Defaults to the name of the file.</span></span>

<span data-ttu-id="1e6bc-364">Przykład:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-364">Example:</span></span>

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

<span data-ttu-id="1e6bc-365">Napisz niestandardowy element docelowy i określ go jako wartość `$(TargetsForTfmSpecificContentInPackage)` właściwości .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-365">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="1e6bc-366">W przypadku plików do uwzględnienia w pakiecie element docelowy powinien zapisać te pliki w grupie ItemGroup i ustawić `TfmSpecificPackageFile` następujące opcjonalne metadane:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-366">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="1e6bc-367">`PackagePath`: ścieżka, w której plik powinien być wyjściowy w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-367">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="1e6bc-368">NuGet program wydaje ostrzeżenie, jeśli do tej samej ścieżki pakietu zostanie dodany więcej niż jeden plik.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-368">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="1e6bc-369">`BuildAction`: akcja kompilacji do przypisania do pliku, wymagana tylko wtedy, gdy ścieżka pakietu znajduje się w `contentFiles` folderze .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-369">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="1e6bc-370">Wartość domyślna to "Brak".</span><span class="sxs-lookup"><span data-stu-id="1e6bc-370">Defaults to "None".</span></span>

<span data-ttu-id="1e6bc-371">Przykład:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-371">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="1e6bc-372">przywracanie obiektu docelowego</span><span class="sxs-lookup"><span data-stu-id="1e6bc-372">restore target</span></span>

<span data-ttu-id="1e6bc-373">`MSBuild -t:restore` (którego `nuget restore` i których można używać z projektami .NET Core), przywraca pakiety przywołyne `dotnet restore` w pliku projektu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-373">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="1e6bc-374">Odczytywanie wszystkich odwołań do projektu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-374">Read all project to project references</span></span>
1. <span data-ttu-id="1e6bc-375">Odczytywanie właściwości projektu w celu znalezienia folderów pośrednich i platform docelowych</span><span class="sxs-lookup"><span data-stu-id="1e6bc-375">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="1e6bc-376">Przekaż MSBuild dane do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="1e6bc-376">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="1e6bc-377">Uruchamianie przywracania</span><span class="sxs-lookup"><span data-stu-id="1e6bc-377">Run restore</span></span>
1. <span data-ttu-id="1e6bc-378">Pobieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="1e6bc-378">Download packages</span></span>
1. <span data-ttu-id="1e6bc-379">Zapis pliku zasobów, obiektów docelowych i propeduł</span><span class="sxs-lookup"><span data-stu-id="1e6bc-379">Write assets file, targets, and props</span></span>

<span data-ttu-id="1e6bc-380">Element `restore` docelowy działa w przypadku projektów w formacie PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-380">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="1e6bc-381">`MSBuild 16.5+` Program [obsługuje również](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) format `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-381">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="1e6bc-382">Obiektu `restore` [docelowego nie należy uruchamiać](#restoring-and-building-with-one-msbuild-command) w połączeniu z obiektem `build` docelowym.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-382">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="1e6bc-383">Przywróć właściwości</span><span class="sxs-lookup"><span data-stu-id="1e6bc-383">Restore properties</span></span>

<span data-ttu-id="1e6bc-384">Dodatkowe ustawienia przywracania mogą pochodzić MSBuild z właściwości w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-384">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="1e6bc-385">Wartości można również ustawiać z poziomu wiersza polecenia przy użyciu `-p:` przełącznika (zobacz przykłady poniżej).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-385">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="1e6bc-386">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1e6bc-386">Property</span></span> | <span data-ttu-id="1e6bc-387">Opis</span><span class="sxs-lookup"><span data-stu-id="1e6bc-387">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="1e6bc-388">Rozdzielana średnikami lista źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-388">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="1e6bc-389">Ścieżka folderu pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-389">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="1e6bc-390">Ogranicz pobieranie do jednego na raz.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-390">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="1e6bc-391">Ścieżka do `Nuget.Config` pliku do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-391">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="1e6bc-392">W przypadku wartości true unika używania buforowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-392">If true, avoids using cached packages.</span></span> <span data-ttu-id="1e6bc-393">Zobacz [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej.](../consume-packages/managing-the-global-packages-and-cache-folders.md)</span><span class="sxs-lookup"><span data-stu-id="1e6bc-393">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="1e6bc-394">W przypadku wartości true ignoruje brakujące źródła pakietów lub je ignoruje.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-394">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="1e6bc-395">Foldery rezerwowe używane w taki sam sposób jak folder pakietów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-395">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="1e6bc-396">Dodatkowe źródła do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-396">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="1e6bc-397">Dodatkowe foldery rezerwowe do użycia podczas przywracania.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-397">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="1e6bc-398">Wyklucza foldery rezerwowe określone w `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="1e6bc-398">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="1e6bc-399">Ścieżka do `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-399">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="1e6bc-400">Rozdzielana średnikami lista projektów do przywrócenia, która powinna zawierać ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-400">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="1e6bc-401">Gdy projekty są zbierane za pośrednictwem programu , określa, czy są one MSBuild zbierane przy użyciu `SkipNonexistentTargets` optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-401">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="1e6bc-402">Jeśli nie zostanie ustawiona, wartość domyślna to `true` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-402">When not set, defaults to `true`.</span></span> <span data-ttu-id="1e6bc-403">Konsekwencją jest szybkie działanie w przypadku, gdy nie można zaimportować obiektów docelowych projektu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-403">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="1e6bc-404">Folder wyjściowy z wartością domyślną `BaseIntermediateOutputPath` i `obj` folderem .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-404">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="1e6bc-405">W projektach opartych na packageReference program wymusza rozwiązanie wszystkich zależności, nawet jeśli ostatnie przywracanie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-405">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="1e6bc-406">Określenie tej flagi jest podobne do usuwania `project.assets.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-406">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="1e6bc-407">Nie pomija to pamięci podręcznej http.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-407">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="1e6bc-408">Decyduje się na użycie pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-408">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="1e6bc-409">Uruchom przywracanie w trybie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-409">Run restore in locked mode.</span></span> <span data-ttu-id="1e6bc-410">Oznacza to, że przywracanie nie spowoduje ponownej wyceny zależności.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-410">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="1e6bc-411">Niestandardowa lokalizacja pliku blokady.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-411">A custom location for the lock file.</span></span> <span data-ttu-id="1e6bc-412">Domyślna lokalizacja znajduje się obok projektu i nosi nazwę `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-412">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="1e6bc-413">Wymusza przywracanie, aby ponownie skompilować zależności i zaktualizować plik blokady bez żadnego ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-413">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="1e6bc-414">Przełącznik zgody, który przywraca projekty za pomocą packages.config. Obsługa tylko `MSBuild -t:restore` za pomocą.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-414">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="1e6bc-415">Przełączenie do korzystania z oceny statycznego MSBuild grafu zamiast standardowej oceny.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-415">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="1e6bc-416">Statyczna ocena grafu to funkcja eksperymentalna, która jest znacznie szybsza w przypadku dużych repos i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-416">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="1e6bc-417">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1e6bc-417">Examples</span></span>

<span data-ttu-id="1e6bc-418">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-418">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="1e6bc-419">Plik projektu:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-419">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="1e6bc-420">Przywracanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="1e6bc-420">Restore outputs</span></span>

<span data-ttu-id="1e6bc-421">Przywracanie tworzy następujące pliki w `obj` folderze kompilacji:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-421">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="1e6bc-422">Plik</span><span class="sxs-lookup"><span data-stu-id="1e6bc-422">File</span></span> | <span data-ttu-id="1e6bc-423">Opis</span><span class="sxs-lookup"><span data-stu-id="1e6bc-423">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="1e6bc-424">Zawiera wykres zależności wszystkich odwołań do pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-424">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="1e6bc-425">Odwołania do MSBuild propeduł zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="1e6bc-425">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="1e6bc-426">Odwołania do MSBuild obiektów docelowych zawartych w pakietach</span><span class="sxs-lookup"><span data-stu-id="1e6bc-426">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="1e6bc-427">Przywracanie i budowania za pomocą jednego MSBuild polecenia</span><span class="sxs-lookup"><span data-stu-id="1e6bc-427">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="1e6bc-428">Ze względu na fakt, że można przywrócić pakiety, które wprowadzają obiekty docelowe i propeduły, oceny przywracania i kompilacji są NuGet MSBuild uruchamiane z różnymi właściwościami globalnymi.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-428">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="1e6bc-429">Oznacza to, że poniższe elementy będą mieć nieprzewidywalne i często nieprawidłowe zachowanie.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-429">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="1e6bc-430">Zamiast tego zalecane jest:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-430">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="1e6bc-431">Ta sama logika ma zastosowanie do innych obiektów docelowych podobnych do `build` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-431">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="1e6bc-432">Przywracanie packageReference i packages.config projektów za pomocą MSBuild</span><span class="sxs-lookup"><span data-stu-id="1e6bc-432">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="1e6bc-433">W MSBuild przypadku programu 16.5 packages.config są również obsługiwane dla programu `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-433">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="1e6bc-434">`packages.config` Przywracanie jest dostępne tylko z `MSBuild 16.5+` , a nie z `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="1e6bc-434">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="1e6bc-435">Przywracanie za pomocą MSBuild statycznej oceny grafu</span><span class="sxs-lookup"><span data-stu-id="1e6bc-435">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="1e6bc-436">W MSBuild programie 16.6+ dodano eksperymentalną funkcję do korzystania z oceny statycznego grafu z wiersza polecenia, która znacznie poprawia czas przywracania w NuGet dużych repozytoriach.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-436">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="1e6bc-437">Alternatywnie można ją włączyć, ustawiając właściwość w Directory.Build.Props.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-437">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="1e6bc-438">Od Visual Studio 2019.x i 5.x ta funkcja jest uznawana za eksperymentalną i NuGet zrezygnuje z jej otrzymywania.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-438">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="1e6bc-439">Postępuj [ NuGet zgodnie z tematem /Home#9803,](https://github.com/NuGet/Home/issues/9803) aby uzyskać szczegółowe informacje o tym, kiedy ta funkcja będzie domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-439">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="1e6bc-440">Statyczne przywracanie grafu zmienia część msbuild przywracania, odczytywanie i ocenianie projektu, ale nie algorytm przywracania!</span><span class="sxs-lookup"><span data-stu-id="1e6bc-440">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="1e6bc-441">Algorytm przywracania jest taki sam we wszystkich narzędziach NuGet NuGet (exe, MSBuild exe, dotnet.exe i Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1e6bc-441">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="1e6bc-442">W bardzo nielicznych scenariuszach przywracanie statycznego grafu może zachowywać się inaczej niż bieżące przywracanie, a niektóre zadeklarowane elementy PackageReferences lub ProjectReferences mogą być brakujące.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-442">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="1e6bc-443">Aby ułatwić sobie rozum, podczas migracji do statycznego przywracania grafu rozważ uruchomienie:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-443">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="1e6bc-444">NuGet Nie *należy zgłaszać* żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-444">NuGet should *not* report any changes.</span></span> <span data-ttu-id="1e6bc-445">Jeśli widzisz niezgodność, napisz na stronie [ NuGet /Home](https://github.com/nuget/home/issues/new)problem .</span><span class="sxs-lookup"><span data-stu-id="1e6bc-445">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="1e6bc-446">Zastępowanie jednej biblioteki z wykresu przywracania</span><span class="sxs-lookup"><span data-stu-id="1e6bc-446">Replacing one library from a restore graph</span></span>

<span data-ttu-id="1e6bc-447">Jeśli przywracanie przywraca niewłaściwy zestaw, można wykluczyć ten domyślny wybór pakietów i zastąpić go własnym wyborem.</span><span class="sxs-lookup"><span data-stu-id="1e6bc-447">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="1e6bc-448">Najpierw przy użyciu najwyższego poziomu `PackageReference` wyklucz wszystkie zasoby:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-448">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="1e6bc-449">Następnie dodaj własne odwołanie do odpowiedniej lokalnej kopii biblioteki DLL:</span><span class="sxs-lookup"><span data-stu-id="1e6bc-449">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
