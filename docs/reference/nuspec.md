---
title: Odwołanie do pliku nuspec dla nuGet
description: Plik nuspec zawiera metadane pakietu używane podczas tworzenia pakietu i w celu zapewnienia informacji klientom pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: a8a8058032b0b6c6ddcd5eed1cf22e75f0e3af72
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387416"
---
# <a name="nuspec-reference"></a><span data-ttu-id="64bd0-103">Odwołanie do nuspec</span><span class="sxs-lookup"><span data-stu-id="64bd0-103">.nuspec reference</span></span>

<span data-ttu-id="64bd0-104">Plik `.nuspec` jest manifestem XML, który zawiera metadane pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="64bd0-105">Ten manifest jest używany zarówno do kompilowania pakietu, jak i do zapewnienia informacji klientom.</span><span class="sxs-lookup"><span data-stu-id="64bd0-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="64bd0-106">Manifest jest zawsze zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="64bd0-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="64bd0-107">In this topic:</span></span>

- [<span data-ttu-id="64bd0-108">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="64bd0-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="64bd0-109">[Tokeny zastępcze](#replacement-tokens) (w przypadku korzystania z Visual Studio projektu)</span><span class="sxs-lookup"><span data-stu-id="64bd0-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="64bd0-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="64bd0-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="64bd0-111">Jawne odwołania do zestawu</span><span class="sxs-lookup"><span data-stu-id="64bd0-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="64bd0-112">Odwołania do zestawu struktury</span><span class="sxs-lookup"><span data-stu-id="64bd0-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="64bd0-113">Łącznie z plikami zestawu</span><span class="sxs-lookup"><span data-stu-id="64bd0-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="64bd0-114">Łącznie z plikami zawartości</span><span class="sxs-lookup"><span data-stu-id="64bd0-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="64bd0-115">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="64bd0-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="64bd0-116">Zgodność typu projektu</span><span class="sxs-lookup"><span data-stu-id="64bd0-116">Project type compatibility</span></span>

- <span data-ttu-id="64bd0-117">Użyj `.nuspec` z dla projektów innych niż w stylu `nuget.exe pack` zestawu SDK, które używają `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="64bd0-118">Plik nie jest wymagany do tworzenia pakietów dla projektów w stylu zestawu `.nuspec` [SDK](../resources/check-project-format.md) (zazwyczaj platformy .NET Core i projektów .NET Standard, które używają [atrybutu SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="64bd0-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="64bd0-119">(Zwróć uwagę, że podczas `.nuspec` tworzenia pakietu jest generowany obiekt .</span><span class="sxs-lookup"><span data-stu-id="64bd0-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="64bd0-120">Jeśli tworzysz pakiet przy użyciu polecenia lub , zalecamy dołącz zamiast tego wszystkie właściwości, które zwykle znajdują się w `dotnet.exe pack` `msbuild pack target` pliku [](../reference/msbuild-targets.md#pack-target) `.nuspec` projektu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="64bd0-121">Zamiast tego można jednak użyć pliku do [ `.nuspec` pakowania przy użyciu lub `dotnet.exe` `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="64bd0-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="64bd0-122">W przypadku projektów migrowanych z programu do `packages.config` [packageReference](../consume-packages/package-references-in-project-files.md) `.nuspec` plik nie jest wymagany do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="64bd0-123">Zamiast tego użyj [msbuild -t:pack.](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)</span><span class="sxs-lookup"><span data-stu-id="64bd0-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="64bd0-124">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="64bd0-124">General form and schema</span></span>

<span data-ttu-id="64bd0-125">Bieżący plik `nuspec.xsd` schematu można znaleźć w [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="64bd0-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="64bd0-126">W ramach tego schematu `.nuspec` plik ma następującą ogólną postać:</span><span class="sxs-lookup"><span data-stu-id="64bd0-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="64bd0-127">Aby uzyskać czytelną wizualną reprezentację schematu, otwórz plik schematu w oknie Visual Studio trybie projektowania i kliknij link **Eksplorator schematu XML.**</span><span class="sxs-lookup"><span data-stu-id="64bd0-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="64bd0-128">Alternatywnie otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz polecenie **Pokaż Eksplorator schematu XML.**</span><span class="sxs-lookup"><span data-stu-id="64bd0-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="64bd0-129">W obu tych sposób możesz uzyskać widok podobny do poniższego (w przypadku większości rozwiniętego):</span><span class="sxs-lookup"><span data-stu-id="64bd0-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Eksplorator schematu z otwartym programem nuspec.xsd](media/SchemaExplorer.png)

<span data-ttu-id="64bd0-131">We wszystkich nazwach elementów XML w pliku nuspec jest wielkość liter, podobnie jak w przypadku XML ogólnie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="64bd0-132">Na przykład użycie elementu metadanych `<description>` jest poprawne i nie jest `<Description>` poprawne.</span><span class="sxs-lookup"><span data-stu-id="64bd0-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="64bd0-133">Prawidłowa nazwa każdego elementu zawiera prawidłową wielkością wielkości.</span><span class="sxs-lookup"><span data-stu-id="64bd0-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="64bd0-134">Wymagane elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="64bd0-134">Required metadata elements</span></span>

<span data-ttu-id="64bd0-135">Mimo że następujące elementy są minimalnymi wymaganiami pakietu, [](#optional-metadata-elements) należy rozważyć dodanie opcjonalnych elementów metadanych w celu poprawienia ogólnego środowiska pracy deweloperów z pakietem.</span><span class="sxs-lookup"><span data-stu-id="64bd0-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="64bd0-136">Te elementy muszą znajdować się w `<metadata>` elemencie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="64bd0-137">identyfikator</span><span class="sxs-lookup"><span data-stu-id="64bd0-137">id</span></span> 
<span data-ttu-id="64bd0-138">Identyfikator pakietu bez uwzględniania liter, który musi być unikatowy w nuget.org galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="64bd0-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="64bd0-139">Identyfikatory mogą nie zawierać spacji ani znaków, które nie są prawidłowe dla adresu URL, i zazwyczaj są zgodne z regułami przestrzeni nazw .NET.</span><span class="sxs-lookup"><span data-stu-id="64bd0-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="64bd0-140">Aby [uzyskać wskazówki, zobacz Choosing a unique package identifier (Wybieranie unikatowego identyfikatora](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) pakietu).</span><span class="sxs-lookup"><span data-stu-id="64bd0-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="64bd0-141">Podczas przekazywania pakietu do nuget.org pole `id` jest ograniczone do 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="64bd0-142">Wersja</span><span class="sxs-lookup"><span data-stu-id="64bd0-142">version</span></span>
<span data-ttu-id="64bd0-143">Wersja pakietu, zgodnie ze wzorcem *główna.pomocnicza.poprawka.*</span><span class="sxs-lookup"><span data-stu-id="64bd0-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="64bd0-144">Numery wersji mogą zawierać sufiks wersji wstępnej, zgodnie z opisem [w te stronie Package versioning (Wersja pakietu).](../concepts/package-versioning.md#pre-release-versions)</span><span class="sxs-lookup"><span data-stu-id="64bd0-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="64bd0-145">Podczas przekazywania pakietu do nuget.org pole `version` jest ograniczone do 64 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="64bd0-146">description (opis)</span><span class="sxs-lookup"><span data-stu-id="64bd0-146">description</span></span>
<span data-ttu-id="64bd0-147">Opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="64bd0-147">A description of the package for UI display.</span></span>

<span data-ttu-id="64bd0-148">Podczas przekazywania pakietu do nuget.org pole `description` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="64bd0-149">Autorów</span><span class="sxs-lookup"><span data-stu-id="64bd0-149">authors</span></span>
<span data-ttu-id="64bd0-150">Rozdzielana przecinkami lista autorów pakietów pasujących do nazw profilów nuget.org. Są one wyświetlane w galerii NuGet na nuget.org i są używane do odsyłania pakietów przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="64bd0-151">Podczas przekazywania pakietu do nuget.org pole `authors` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="64bd0-152">Opcjonalne elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="64bd0-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="64bd0-153">Właścicieli</span><span class="sxs-lookup"><span data-stu-id="64bd0-153">owners</span></span>
> [!Important]
> <span data-ttu-id="64bd0-154">właściciele są przestarzali.</span><span class="sxs-lookup"><span data-stu-id="64bd0-154">owners is deprecated.</span></span> <span data-ttu-id="64bd0-155">Zamiast tego należy używać autorów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-155">Use authors instead.</span></span>

<span data-ttu-id="64bd0-156">Rozdzielana przecinkami lista twórców pakietów używających nazw profilów na nuget.org. Jest to często ta sama lista co w pliku i jest ignorowana podczas przekazywania `authors` pakietu do nuget.org. Zobacz [Zarządzanie właścicielami pakietów na nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="64bd0-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="64bd0-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="64bd0-157">projectUrl</span></span>
<span data-ttu-id="64bd0-158">Adres URL strony głównej pakietu, często wyświetlany w interfejsie użytkownika, a także nuget.org.</span><span class="sxs-lookup"><span data-stu-id="64bd0-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="64bd0-159">Podczas przekazywania pakietu do nuget.org pole `projectUrl` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="64bd0-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="64bd0-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="64bd0-161">LicenseUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="64bd0-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="64bd0-162">Zamiast tego użyj licencji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-162">Use license instead.</span></span>

<span data-ttu-id="64bd0-163">Adres URL licencji pakietu, często wyświetlany w interfejsach użytkownika, takich jak nuget.org.</span><span class="sxs-lookup"><span data-stu-id="64bd0-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="64bd0-164">Podczas przekazywania pakietu do nuget.org pole `licenseUrl` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="64bd0-165">license (licencja)</span><span class="sxs-lookup"><span data-stu-id="64bd0-165">license</span></span>

<span data-ttu-id="64bd0-166">*Obsługiwane z **programem NuGet 4.9.0** i jego produktami*</span><span class="sxs-lookup"><span data-stu-id="64bd0-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="64bd0-167">Wyrażenie licencji SPDX lub ścieżka do pliku licencji w pakiecie, często wyświetlane w interfejsach użytkownika, takich jak nuget.org. Jeśli licencjonowanie pakietu jest na podstawie wspólnej licencji, na przykład MIT lub BSD-2-Clause, użyj skojarzonego identyfikatora licencji [SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="64bd0-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="64bd0-168">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="64bd0-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="64bd0-169">NuGet.org akceptuje tylko wyrażenia licencji zatwierdzone przez inicjatywę Open Source Initiative lub Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="64bd0-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="64bd0-170">Jeśli pakiet jest licencjonowany w ramach wielu typowych licencji, możesz określić licencję złożoną przy użyciu składni wyrażeń [SPDX w wersji 2.0.](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)</span><span class="sxs-lookup"><span data-stu-id="64bd0-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="64bd0-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="64bd0-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="64bd0-172">Jeśli używasz licencji niestandardowej, która nie jest obsługiwana przez wyrażenia licencji, możesz spakć plik lub `.txt` `.md` z tekstem licencji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="64bd0-173">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="64bd0-173">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="64bd0-174">Aby uzyskać odpowiednik msBuild, zobacz Pakowanie [wyrażenia licencji lub plik licencji](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="64bd0-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="64bd0-175">Dokładna składnia wyrażeń licencji NuGet jest opisana poniżej w [abnf](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="64bd0-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="64bd0-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="64bd0-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="64bd0-177">IconUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="64bd0-177">iconUrl is deprecated.</span></span> <span data-ttu-id="64bd0-178">Zamiast tego użyj ikony .</span><span class="sxs-lookup"><span data-stu-id="64bd0-178">Use icon instead.</span></span>

<span data-ttu-id="64bd0-179">Adres URL obrazu o rozdzielczości 128 x 128 z przezroczystym tłem do użycia jako ikona pakietu na ekranie interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="64bd0-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="64bd0-180">Upewnij się, że ten element zawiera *bezpośredni adres URL obrazu,* a nie adres URL strony internetowej zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="64bd0-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="64bd0-181">Aby na przykład użyć obrazu z usługi GitHub, użyj nieprzetworzowego adresu URL pliku, takiego <em> https://github.com/ \<username\> / \<repository\> jak \<branch\> / \<logo.png\> /raw/</em>.</span><span class="sxs-lookup"><span data-stu-id="64bd0-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="64bd0-182">Podczas przekazywania pakietu do nuget.org pole `iconUrl` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="64bd0-183">Ikonę</span><span class="sxs-lookup"><span data-stu-id="64bd0-183">icon</span></span>

<span data-ttu-id="64bd0-184">*Obsługiwane w **programie NuGet 5.3.0** i jego produktach*</span><span class="sxs-lookup"><span data-stu-id="64bd0-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="64bd0-185">Jest to ścieżka do pliku obrazu w pakiecie, często wyświetlana w interfejsach nuget.org jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="64bd0-186">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="64bd0-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="64bd0-187">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="64bd0-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="64bd0-188">Zalecamy rozdzielczość obrazu 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="64bd0-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="64bd0-189">Na przykład podczas tworzenia pakietu przy użyciu narzędzia nuspec należy dodać następujące nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="64bd0-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="64bd0-190">Przykład ikony pakietu nuspec.</span><span class="sxs-lookup"><span data-stu-id="64bd0-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="64bd0-191">W przypadku odpowiednika msBuild zobacz Pakowanie [pliku obrazu ikony](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="64bd0-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="64bd0-192">Można określić zarówno , `icon` jak i , aby zachować zgodność z `iconUrl` poprzednimi wersjami ze źródłami, które nie obsługują systemu `icon` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="64bd0-193">Visual Studio będzie obsługiwać pakiety pochodzące ze źródła opartego na `icon` folderach w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="readme"></a><span data-ttu-id="64bd0-194">Plik readme</span><span class="sxs-lookup"><span data-stu-id="64bd0-194">readme</span></span>

<span data-ttu-id="64bd0-195">Podczas pakowania pliku readme należy użyć elementu , aby określić ścieżkę pakietu względem katalogu `readme` głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-195">When packing a readme file, you need to use the `readme` element to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="64bd0-196">Oprócz tego należy się upewnić, że plik znajduje się w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="64bd0-196">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="64bd0-197">Obsługiwane formaty plików obejmują tylko markdown *(md).*</span><span class="sxs-lookup"><span data-stu-id="64bd0-197">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="64bd0-198">Na przykład należy dodać następujący kod do swojego nuspec, aby spakować plik readme z projektem:</span><span class="sxs-lookup"><span data-stu-id="64bd0-198">For example, you would add the following to your nuspec in order to pack a readme file with your project:</span></span>

```xml
<package>
  <metadata>
    ...
    <readme>docs\readme.md</readme>
    ...
  </metadata>
  <files>
    ...
    <file src="..\readme.md" target="docs\" />
    ...
  </files>
</package>
```

<span data-ttu-id="64bd0-199">W przypadku odpowiednika msBuild zapoznaj się z tematem [Pakowanie pliku readme.](msbuild-targets.md#packagereadmefile)</span><span class="sxs-lookup"><span data-stu-id="64bd0-199">For the MSBuild equivalent, take a look at [Packing a readme file](msbuild-targets.md#packagereadmefile).</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="64bd0-200">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="64bd0-200">requireLicenseAcceptance</span></span>
<span data-ttu-id="64bd0-201">Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-201">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="64bd0-202">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="64bd0-202">developmentDependency</span></span>
<span data-ttu-id="64bd0-203">*(2.8+)* Wartość logiczna określająca, czy pakiet ma być oznaczony jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="64bd0-203">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="64bd0-204">W przypadku packageReference (NuGet 4.8+) ta flaga oznacza również, że wyklucza ona z kompilacji zasoby czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-204">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="64bd0-205">Zobacz [DevelopmentDependency support for PackageReference (Obsługa zależności dla packageReference)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="64bd0-205">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="64bd0-206">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="64bd0-206">summary</span></span>
> [!Important]
> <span data-ttu-id="64bd0-207">`summary` jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="64bd0-207">`summary` is being deprecated.</span></span> <span data-ttu-id="64bd0-208">Zamiast tego użyj polecenia cmdlet `description`.</span><span class="sxs-lookup"><span data-stu-id="64bd0-208">Use `description` instead.</span></span>

<span data-ttu-id="64bd0-209">Krótki opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="64bd0-209">A short description of the package for UI display.</span></span> <span data-ttu-id="64bd0-210">W przypadku pominięcia używana jest obcinana `description` wersja programu .</span><span class="sxs-lookup"><span data-stu-id="64bd0-210">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="64bd0-211">Podczas przekazywania pakietu do nuget.org pole `summary` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-211">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="64bd0-212">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="64bd0-212">releaseNotes</span></span>
<span data-ttu-id="64bd0-213">*(1,5+)* Opis zmian wprowadzonych w tej wersji pakietu, często używany  w interfejsie użytkownika, taki jak karta Aktualizacje Visual Studio Menedżer pakietów w miejsce opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-213">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="64bd0-214">Podczas przekazywania pakietu do nuget.org pole `releaseNotes` jest ograniczone do 35 000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-214">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="64bd0-215">informacji o prawach autorskich,</span><span class="sxs-lookup"><span data-stu-id="64bd0-215">copyright</span></span>
<span data-ttu-id="64bd0-216">*(1,5+)* Szczegóły praw autorskich dotyczących pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-216">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="64bd0-217">Podczas przekazywania pakietu do nuget.org pole `copyright` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-217">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="64bd0-218">language</span><span class="sxs-lookup"><span data-stu-id="64bd0-218">language</span></span>
<span data-ttu-id="64bd0-219">Identyfikator regionalny pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-219">The locale ID for the package.</span></span> <span data-ttu-id="64bd0-220">Zobacz [Creating localized packages (Tworzenie zlokalizowanych pakietów).](../create-packages/creating-localized-packages.md)</span><span class="sxs-lookup"><span data-stu-id="64bd0-220">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="64bd0-221">tags</span><span class="sxs-lookup"><span data-stu-id="64bd0-221">tags</span></span>
<span data-ttu-id="64bd0-222">Rozdzielana spacjami lista tagów i słów kluczowych, które opisują pakiet i wspomagają odnajdywanie pakietów za pomocą wyszukiwania i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="64bd0-222">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="64bd0-223">Podczas przekazywania pakietu do nuget.org pole `tags` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-223">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="64bd0-224">Sprawne</span><span class="sxs-lookup"><span data-stu-id="64bd0-224">serviceable</span></span> 
<span data-ttu-id="64bd0-225">*(3.3+)* Wewnętrznego nuGet należy używać tylko.</span><span class="sxs-lookup"><span data-stu-id="64bd0-225">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="64bd0-226">repozytorium</span><span class="sxs-lookup"><span data-stu-id="64bd0-226">repository</span></span>
<span data-ttu-id="64bd0-227">Metadane repozytorium składające się z czterech atrybutów opcjonalnych: `type` i `url` *(4.0+)*, `branch` i `commit` *(4.6+)*.</span><span class="sxs-lookup"><span data-stu-id="64bd0-227">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="64bd0-228">Te atrybuty umożliwiają mapowanie pliku do repozytorium, które go sbudowały, z możliwością uzyskania tak szczegółowej informacji jak nazwa poszczególnych gałęzi i/lub zatwierdzenie skrótu SHA-1, który sbudowali `.nupkg` pakiet.</span><span class="sxs-lookup"><span data-stu-id="64bd0-228">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="64bd0-229">Powinien to być publicznie dostępny adres URL, który może być wywoływany bezpośrednio przez oprogramowanie do kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-229">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="64bd0-230">Nie powinna to być strona HTML, ponieważ jest przeznaczona dla komputera.</span><span class="sxs-lookup"><span data-stu-id="64bd0-230">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="64bd0-231">W przypadku łączenia ze stroną projektu zamiast `projectUrl` tego użyj pola .</span><span class="sxs-lookup"><span data-stu-id="64bd0-231">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="64bd0-232">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="64bd0-232">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="64bd0-233">Podczas przekazywania pakietu do nuget.org atrybut jest ograniczony do 100 znaków, a atrybut jest ograniczony do `type` `url` 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-233">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="64bd0-234">tytuł</span><span class="sxs-lookup"><span data-stu-id="64bd0-234">title</span></span>
<span data-ttu-id="64bd0-235">Zostanie wyświetlony przyjazny dla człowieka tytuł pakietu, który może być używany w niektórych interfejsach użytkownika.</span><span class="sxs-lookup"><span data-stu-id="64bd0-235">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="64bd0-236">(nuget.org i Menedżer pakietów w Visual Studio nie są wyświetlane tytuł)</span><span class="sxs-lookup"><span data-stu-id="64bd0-236">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="64bd0-237">Podczas przekazywania pakietu do nuget.org pole jest ograniczone do 256 znaków, ale nie jest używane `title` do żadnych celów wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="64bd0-237">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="64bd0-238">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="64bd0-238">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="64bd0-239">packageTypes</span><span class="sxs-lookup"><span data-stu-id="64bd0-239">packageTypes</span></span>
<span data-ttu-id="64bd0-240">*(3.5+)* Kolekcja zerową lub większą liczbę elementów określającą typ pakietu, jeśli jest inny niż `<packageType>` tradycyjny pakiet zależności.</span><span class="sxs-lookup"><span data-stu-id="64bd0-240">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="64bd0-241">Każdy typ packageType ma atrybuty *nazwy i* *wersji*.</span><span class="sxs-lookup"><span data-stu-id="64bd0-241">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="64bd0-242">Zobacz [Setting a package type (Ustawianie typu pakietu).](../create-packages/set-package-type.md)</span><span class="sxs-lookup"><span data-stu-id="64bd0-242">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="64bd0-243">zależności</span><span class="sxs-lookup"><span data-stu-id="64bd0-243">dependencies</span></span>
<span data-ttu-id="64bd0-244">Kolekcja zerowych lub większej `<dependency>` liczby elementów określających zależności dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-244">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="64bd0-245">Każda zależność ma atrybuty *identyfikatora,* *wersji,* *dołączania* (3.x+) i *wykluczania* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="64bd0-245">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="64bd0-246">Zobacz [zależności](#dependencies-element) poniżej.</span><span class="sxs-lookup"><span data-stu-id="64bd0-246">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="64bd0-247">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="64bd0-247">frameworkAssemblies</span></span>
<span data-ttu-id="64bd0-248">*(1.2+)* Kolekcja zerowych lub większej liczby elementów identyfikujące odwołania .NET Framework zestawu, których wymaga ten pakiet, co zapewnia, że odwołania są dodawane do projektów, które `<frameworkAssembly>` zużywają pakiet.</span><span class="sxs-lookup"><span data-stu-id="64bd0-248">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="64bd0-249">Każdy element frameworkAssembly ma *atrybuty assemblyName* i *targetFramework.*</span><span class="sxs-lookup"><span data-stu-id="64bd0-249">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="64bd0-250">Zobacz [Temat Specifying framework assembly references (Określanie odwołań do zestawu struktury) PONIŻEJ.](#specifying-framework-assembly-references-gac)</span><span class="sxs-lookup"><span data-stu-id="64bd0-250">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="64bd0-251">odwołania</span><span class="sxs-lookup"><span data-stu-id="64bd0-251">references</span></span>
<span data-ttu-id="64bd0-252">*(1.5+)* Kolekcja zero lub więcej elementów nazewnictwa zestawów w folderze pakietu, które `<reference>` są dodawane jako odwołania do `lib` projektu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-252">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="64bd0-253">Każde odwołanie ma *atrybut* pliku.</span><span class="sxs-lookup"><span data-stu-id="64bd0-253">Each reference has a *file* attribute.</span></span> <span data-ttu-id="64bd0-254">`<references>` Może również zawierać `<group>` element z *atrybutem targetFramework,* który następnie zawiera `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="64bd0-254">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="64bd0-255">W przypadku pominięcia wszystkie odwołania w `lib` są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="64bd0-255">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="64bd0-256">Zobacz [Temat Specifying explicit assembly references (Określanie jawnych odwołań do zestawu)](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="64bd0-256">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="64bd0-257">contentFiles</span><span class="sxs-lookup"><span data-stu-id="64bd0-257">contentFiles</span></span>
<span data-ttu-id="64bd0-258">*(3.3+)* Kolekcja `<files>` elementów, które identyfikują pliki zawartości, które mają być dołączane do projektu zużywającego zasoby.</span><span class="sxs-lookup"><span data-stu-id="64bd0-258">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="64bd0-259">Te pliki są określane za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-259">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="64bd0-260">Zobacz Temat Specifying files to include in the package below (Określanie plików [do dołączyć do poniższego](#specifying-files-to-include-in-the-package) pakietu).</span><span class="sxs-lookup"><span data-stu-id="64bd0-260">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="64bd0-261">files</span><span class="sxs-lookup"><span data-stu-id="64bd0-261">files</span></span> 
<span data-ttu-id="64bd0-262">Węzeł może zawierać węzeł jako element równorzędny do elementu i element podrzędny w obszarze , aby określić, które pliki zestawu i zawartości mają zostać `<package>` `<files>` zawarte w `<metadata>` `<contentFiles>` `<metadata>` pakiecie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-262">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="64bd0-263">Aby uzyskać [szczegółowe informacje, zobacz](#including-assembly-files) Tematy Including assembly files (Łącznie z [plikami](#including-content-files) zestawu) i Including content files (W tym pliki zawartości) w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-263">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="64bd0-264">atrybuty metadanych</span><span class="sxs-lookup"><span data-stu-id="64bd0-264">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="64bd0-265">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="64bd0-265">minClientVersion</span></span>
<span data-ttu-id="64bd0-266">Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszaną przez nuget.exe i Visual Studio Menedżer pakietów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-266">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="64bd0-267">Jest to używane za każdym razem, gdy pakiet zależy od określonych funkcji pliku, które zostały dodane w `.nuspec` określonej wersji klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="64bd0-267">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="64bd0-268">Na przykład pakiet używający `developmentDependency` atrybutu powinien określać wartość "2.8" dla `minClientVersion` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-268">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="64bd0-269">Podobnie pakiet używający `contentFiles` elementu (zobacz następną sekcję) powinien mieć `minClientVersion` wartość "3.3".</span><span class="sxs-lookup"><span data-stu-id="64bd0-269">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="64bd0-270">Należy również zauważyć, że klienci NuGet wcześniejszym niż 2.5 nie rozpoznają tej flagi, dlatego zawsze odmawiają zainstalowania pakietu niezależnie od tego, co  `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="64bd0-270">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="64bd0-271">Tokeny zastępcze</span><span class="sxs-lookup"><span data-stu-id="64bd0-271">Replacement tokens</span></span>

<span data-ttu-id="64bd0-272">Podczas tworzenia pakietu [ `nuget pack` ](../reference/cli-reference/cli-ref-pack.md) polecenie zastępuje tokeny rozdzielane $w węźle pliku wartościami, które pochodzą z pliku projektu lub `.nuspec` `<metadata>` `pack` przełącznika `-properties` polecenia.</span><span class="sxs-lookup"><span data-stu-id="64bd0-272">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="64bd0-273">W wierszu polecenia należy określić wartości tokenu za pomocą polecenia `nuget pack -properties <name>=<value>;<name>=<value>` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-273">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="64bd0-274">Na przykład można użyć tokenu, takiego jak i , i podać wartości w czasie `$owners$` `$desc$` `.nuspec` pakowania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="64bd0-274">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="64bd0-275">Aby użyć wartości z projektu, określ tokeny opisane w poniższej tabeli (AssemblyInfo odnosi się do pliku w `Properties` pliku, takim `AssemblyInfo.cs` jak lub `AssemblyInfo.vb` ).</span><span class="sxs-lookup"><span data-stu-id="64bd0-275">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="64bd0-276">Aby użyć tych tokenów, uruchom plik `nuget pack` projektu, a nie tylko plik `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-276">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="64bd0-277">Na przykład w przypadku użycia następującego polecenia tokeny i w pliku są zastępowane wartościami `$id$` `$version$` i `.nuspec` `AssemblyName` `AssemblyVersion` projektu:</span><span class="sxs-lookup"><span data-stu-id="64bd0-277">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="64bd0-278">Zazwyczaj, gdy masz projekt, początkowo tworzysz przy użyciu , `.nuspec` który automatycznie zawiera niektóre z tych `nuget spec MyProject.csproj` standardowych tokenów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-278">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="64bd0-279">Jeśli jednak projekt nie ma wartości dla wymaganych elementów, to `.nuspec` kończy się `nuget pack` niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="64bd0-279">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="64bd0-280">Ponadto w przypadku zmiany wartości projektu pamiętaj, aby ponownie skompilować przed utworzeniem pakietu; Można to zrobić wygodnie za pomocą przełącznika polecenia `build` pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-280">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="64bd0-281">Z wyjątkiem , wartości w projekcie są używane w preferencji do wszystkich przypisanych do tego `$configuration$` samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="64bd0-281">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="64bd0-282">Token</span><span class="sxs-lookup"><span data-stu-id="64bd0-282">Token</span></span> | <span data-ttu-id="64bd0-283">Źródło wartości</span><span class="sxs-lookup"><span data-stu-id="64bd0-283">Value source</span></span> | <span data-ttu-id="64bd0-284">Wartość</span><span class="sxs-lookup"><span data-stu-id="64bd0-284">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="64bd0-285">**$id$**</span><span class="sxs-lookup"><span data-stu-id="64bd0-285">**$id$**</span></span> | <span data-ttu-id="64bd0-286">Plik projektu</span><span class="sxs-lookup"><span data-stu-id="64bd0-286">Project file</span></span> | <span data-ttu-id="64bd0-287">Nazwa_zestawu (tytuł) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="64bd0-287">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="64bd0-288">**$version$**</span><span class="sxs-lookup"><span data-stu-id="64bd0-288">**$version$**</span></span> | <span data-ttu-id="64bd0-289">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="64bd0-289">AssemblyInfo</span></span> | <span data-ttu-id="64bd0-290">AssemblyInformationalVersion, jeśli jest obecny, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="64bd0-290">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="64bd0-291">**$author$**</span><span class="sxs-lookup"><span data-stu-id="64bd0-291">**$author$**</span></span> | <span data-ttu-id="64bd0-292">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="64bd0-292">AssemblyInfo</span></span> | <span data-ttu-id="64bd0-293">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="64bd0-293">AssemblyCompany</span></span> |
| <span data-ttu-id="64bd0-294">**$title$**</span><span class="sxs-lookup"><span data-stu-id="64bd0-294">**$title$**</span></span> | <span data-ttu-id="64bd0-295">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="64bd0-295">AssemblyInfo</span></span> | <span data-ttu-id="64bd0-296">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="64bd0-296">AssemblyTitle</span></span> |
| <span data-ttu-id="64bd0-297">**$description$**</span><span class="sxs-lookup"><span data-stu-id="64bd0-297">**$description$**</span></span> | <span data-ttu-id="64bd0-298">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="64bd0-298">AssemblyInfo</span></span> | <span data-ttu-id="64bd0-299">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="64bd0-299">AssemblyDescription</span></span> |
| <span data-ttu-id="64bd0-300">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="64bd0-300">**$copyright$**</span></span> | <span data-ttu-id="64bd0-301">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="64bd0-301">AssemblyInfo</span></span> | <span data-ttu-id="64bd0-302">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="64bd0-302">AssemblyCopyright</span></span> |
| <span data-ttu-id="64bd0-303">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="64bd0-303">**$configuration$**</span></span> | <span data-ttu-id="64bd0-304">Biblioteka DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="64bd0-304">Assembly DLL</span></span> | <span data-ttu-id="64bd0-305">Konfiguracja używana do kompilowania zestawu z wartością domyślną Debugowanie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-305">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="64bd0-306">Należy pamiętać, że aby utworzyć pakiet przy użyciu konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` polecenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="64bd0-306">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="64bd0-307">Tokeny mogą być również używane do rozpoznawania ścieżek w przypadku dołączania plików [zestawu i](#including-assembly-files) [plików zawartości](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="64bd0-307">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="64bd0-308">Tokeny mają takie same nazwy jak właściwości programu MSBuild, dzięki czemu można wybierać pliki do dołączona w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-308">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="64bd0-309">Jeśli na przykład użyjemy w pliku następujących `.nuspec` tokenów:</span><span class="sxs-lookup"><span data-stu-id="64bd0-309">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="64bd0-310">I tworzysz zestaw, którego jest z konfiguracją w `AssemblyName` `LoggingLibrary` `Release` PROGRAMIE MSBuild, wynikowe wiersze w pliku w `.nuspec` pakiecie są następujące:</span><span class="sxs-lookup"><span data-stu-id="64bd0-310">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="64bd0-311">Element zależności</span><span class="sxs-lookup"><span data-stu-id="64bd0-311">Dependencies element</span></span>

<span data-ttu-id="64bd0-312">Element `<dependencies>` w `<metadata>` elemencie zawiera dowolną liczbę elementów, które identyfikują inne pakiety, od których zależy pakiet `<dependency>` najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-312">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="64bd0-313">Atrybuty dla każdego z `<dependency>` nich są następujące:</span><span class="sxs-lookup"><span data-stu-id="64bd0-313">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="64bd0-314">Atrybut</span><span class="sxs-lookup"><span data-stu-id="64bd0-314">Attribute</span></span> | <span data-ttu-id="64bd0-315">Opis</span><span class="sxs-lookup"><span data-stu-id="64bd0-315">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="64bd0-316">(Wymagane) Identyfikator pakietu zależności, taki jak "EntityFramework" i "NUnit", który jest nazwą pakietu nuget.org na stronie pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-316">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="64bd0-317">(Wymagane) Zakres wersji akceptowalnych jako zależność.</span><span class="sxs-lookup"><span data-stu-id="64bd0-317">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="64bd0-318">Aby [uzyskać dokładną składnię,](../concepts/package-versioning.md#version-ranges) zobacz Package versioning (Wersja pakietu).</span><span class="sxs-lookup"><span data-stu-id="64bd0-318">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="64bd0-319">Wersje zmiennoprzecinowe nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="64bd0-319">Floating versions are not supported.</span></span> |
| <span data-ttu-id="64bd0-320">include</span><span class="sxs-lookup"><span data-stu-id="64bd0-320">include</span></span> | <span data-ttu-id="64bd0-321">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazująca zależność do dołączyć do pakietu końcowego.</span><span class="sxs-lookup"><span data-stu-id="64bd0-321">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="64bd0-322">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="64bd0-322">The default value is `all`.</span></span> |
| <span data-ttu-id="64bd0-323">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="64bd0-323">exclude</span></span> | <span data-ttu-id="64bd0-324">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazująca zależność do wykluczenia w końcowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-324">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="64bd0-325">Wartość domyślna to `build,analyzers` , która może być zbyt zapisywana.</span><span class="sxs-lookup"><span data-stu-id="64bd0-325">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="64bd0-326">Są `content/ ContentFiles` jednak również niejawnie wykluczane w końcowym pakiecie, którego nie można zbytniego napisano.</span><span class="sxs-lookup"><span data-stu-id="64bd0-326">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="64bd0-327">Tagi określone za `exclude` pomocą mają pierwszeństwo przed tagami określonymi za pomocą . `include`</span><span class="sxs-lookup"><span data-stu-id="64bd0-327">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="64bd0-328">Na przykład jest `include="runtime, compile" exclude="compile"` taka sama jak `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-328">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="64bd0-329">Podczas przekazywania pakietu do nuget.org atrybut każdej zależności jest ograniczony do 128 znaków, a atrybut jest ograniczony do `id` `version` 256 znaków.</span><span class="sxs-lookup"><span data-stu-id="64bd0-329">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="64bd0-330">Tag Dołączanie/wykluczanie</span><span class="sxs-lookup"><span data-stu-id="64bd0-330">Include/Exclude tag</span></span> | <span data-ttu-id="64bd0-331">Foldery docelowe, których dotyczy problem</span><span class="sxs-lookup"><span data-stu-id="64bd0-331">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="64bd0-332">contentFiles</span><span class="sxs-lookup"><span data-stu-id="64bd0-332">contentFiles</span></span> | <span data-ttu-id="64bd0-333">Zawartość</span><span class="sxs-lookup"><span data-stu-id="64bd0-333">Content</span></span> |
| <span data-ttu-id="64bd0-334">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="64bd0-334">runtime</span></span> | <span data-ttu-id="64bd0-335">Środowisko uruchomieniowe, zasoby i frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="64bd0-335">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="64bd0-336">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="64bd0-336">compile</span></span> | <span data-ttu-id="64bd0-337">Lib</span><span class="sxs-lookup"><span data-stu-id="64bd0-337">lib</span></span> |
| <span data-ttu-id="64bd0-338">kompilacja</span><span class="sxs-lookup"><span data-stu-id="64bd0-338">build</span></span> | <span data-ttu-id="64bd0-339">build (obiekty prop i obiekty docelowe MSBuild)</span><span class="sxs-lookup"><span data-stu-id="64bd0-339">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="64bd0-340">natywne</span><span class="sxs-lookup"><span data-stu-id="64bd0-340">native</span></span> | <span data-ttu-id="64bd0-341">natywne</span><span class="sxs-lookup"><span data-stu-id="64bd0-341">native</span></span> |
| <span data-ttu-id="64bd0-342">brak</span><span class="sxs-lookup"><span data-stu-id="64bd0-342">none</span></span> | <span data-ttu-id="64bd0-343">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="64bd0-343">No folders</span></span> |
| <span data-ttu-id="64bd0-344">all</span><span class="sxs-lookup"><span data-stu-id="64bd0-344">all</span></span> | <span data-ttu-id="64bd0-345">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="64bd0-345">All folders</span></span> |

<span data-ttu-id="64bd0-346">Na przykład następujące wiersze wskazują zależności od wersji `PackageA` 1.1.0 lub wyższej oraz `PackageB` wersji 1.x.</span><span class="sxs-lookup"><span data-stu-id="64bd0-346">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="64bd0-347">Następujące wiersze wskazują zależności od tych samych pakietów, ale określ, aby uwzględnić foldery i i wszystkie elementy oprócz folderów `contentFiles` `build` i `PackageA` `native` `compile` `PackageB` "</span><span class="sxs-lookup"><span data-stu-id="64bd0-347">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="64bd0-348">Podczas tworzenia pliku z projektu przy użyciu funkcji zależności, które istnieją w tym projekcie, nie są automatycznie uwzględniane `.nuspec` `nuget spec` w wynikowym `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="64bd0-348">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="64bd0-349">Zamiast tego użyj `nuget pack myproject.csproj` funkcji i pobierz plik *nuspec* z wygenerowanego pliku *nupkg.*</span><span class="sxs-lookup"><span data-stu-id="64bd0-349">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="64bd0-350">Ten *plik .nuspec* zawiera zależności.</span><span class="sxs-lookup"><span data-stu-id="64bd0-350">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="64bd0-351">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="64bd0-351">Dependency groups</span></span>

<span data-ttu-id="64bd0-352">*Wersja 2.0 lub nowsza*</span><span class="sxs-lookup"><span data-stu-id="64bd0-352">*Version 2.0+*</span></span>

<span data-ttu-id="64bd0-353">Alternatywą dla pojedynczej listy płaskiej jest możliwość określonej zależności zgodnie z profilem struktury projektu docelowego przy użyciu `<group>` elementów w ramach . `<dependencies>`</span><span class="sxs-lookup"><span data-stu-id="64bd0-353">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="64bd0-354">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-354">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="64bd0-355">Te zależności są instalowane razem, gdy docelowa framework jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-355">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="64bd0-356">Element `<group>` bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista zależności.</span><span class="sxs-lookup"><span data-stu-id="64bd0-356">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="64bd0-357">Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).</span><span class="sxs-lookup"><span data-stu-id="64bd0-357">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="64bd0-358">Format grupy nie może być połączony z listą płaską.</span><span class="sxs-lookup"><span data-stu-id="64bd0-358">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="64bd0-359">Format [monikera docelowej struktury (TFM)](../reference/target-frameworks.md) używanej w folderze różni się w porównaniu z `lib/ref` programem TFM używanym w programie `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-359">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="64bd0-360">Jeśli struktury docelowe zadeklarowane w pliku i folderze nie mają dokładnych dopasowania, polecenie zwniesie ostrzeżenie `dependencies group` `lib/ref` `.nuspec` `pack` [NuGet NU5128.](../reference/errors-and-warnings/nu5128.md)</span><span class="sxs-lookup"><span data-stu-id="64bd0-360">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="64bd0-361">W poniższym przykładzie pokazano różne odmiany `<group>` elementu :</span><span class="sxs-lookup"><span data-stu-id="64bd0-361">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="64bd0-362">Jawne odwołania do zestawu</span><span class="sxs-lookup"><span data-stu-id="64bd0-362">Explicit assembly references</span></span>

<span data-ttu-id="64bd0-363">Element jest używany przez projekty przy użyciu elementu , aby jawnie określić zestawy, do których powinien odwoływać się projekt docelowy `<references>` `packages.config` podczas korzystania z pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-363">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="64bd0-364">Odwołania jawne są zwykle używane w przypadku zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="64bd0-364">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="64bd0-365">Aby uzyskać więcej informacji, zobacz stronę [wybierania zestawów,](../create-packages/select-assemblies-referenced-by-projects.md) do których odwołują się projekty.</span><span class="sxs-lookup"><span data-stu-id="64bd0-365">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="64bd0-366">Na przykład następujący element instruuje program NuGet, aby dodał odwołania tylko do elementu i nawet jeśli w pakiecie znajdują się `<references>` `xunit.dll` dodatkowe `xunit.extensions.dll` zestawy:</span><span class="sxs-lookup"><span data-stu-id="64bd0-366">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="64bd0-367">Grupy odwoły</span><span class="sxs-lookup"><span data-stu-id="64bd0-367">Reference groups</span></span>

<span data-ttu-id="64bd0-368">Alternatywą dla pojedynczej listy płaskiej jest możliwość określonej odwołań zgodnie z profilem struktury projektu docelowego przy użyciu `<group>` elementów w pliku `<references>` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-368">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="64bd0-369">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-369">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="64bd0-370">Te odwołania są dodawane do projektu, gdy docelowa framework jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-370">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="64bd0-371">Element `<group>` bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista odwołań.</span><span class="sxs-lookup"><span data-stu-id="64bd0-371">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="64bd0-372">Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).</span><span class="sxs-lookup"><span data-stu-id="64bd0-372">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="64bd0-373">Format grupy nie może być połączony z listą płaską.</span><span class="sxs-lookup"><span data-stu-id="64bd0-373">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="64bd0-374">W poniższym przykładzie pokazano różne odmiany `<group>` elementu :</span><span class="sxs-lookup"><span data-stu-id="64bd0-374">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="64bd0-375">Odwołania do zestawu struktury</span><span class="sxs-lookup"><span data-stu-id="64bd0-375">Framework assembly references</span></span>

<span data-ttu-id="64bd0-376">Zestawy struktury to te, które są częścią programu .NET Framework i powinny już być w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej maszyny.</span><span class="sxs-lookup"><span data-stu-id="64bd0-376">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="64bd0-377">Identyfikując te zestawy w elemencie, pakiet może zapewnić, że wymagane odwołania zostaną dodane do projektu w przypadku, gdy projekt nie ma jeszcze `<frameworkAssemblies>` takich odwołań.</span><span class="sxs-lookup"><span data-stu-id="64bd0-377">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="64bd0-378">Takie zestawy oczywiście nie są bezpośrednio zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-378">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="64bd0-379">Element `<frameworkAssemblies>` zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="64bd0-379">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="64bd0-380">Atrybut</span><span class="sxs-lookup"><span data-stu-id="64bd0-380">Attribute</span></span> | <span data-ttu-id="64bd0-381">Opis</span><span class="sxs-lookup"><span data-stu-id="64bd0-381">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64bd0-382">**Assemblyname**</span><span class="sxs-lookup"><span data-stu-id="64bd0-382">**assemblyName**</span></span> | <span data-ttu-id="64bd0-383">(Wymagane) W pełni kwalifikowana nazwa zestawu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-383">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="64bd0-384">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="64bd0-384">**targetFramework**</span></span> | <span data-ttu-id="64bd0-385">(Opcjonalnie) Określa platformę docelową, do której odnosi się to odwołanie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-385">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="64bd0-386">W przypadku pominięcia wskazuje, że odwołanie ma zastosowanie do wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="64bd0-386">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="64bd0-387">Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).</span><span class="sxs-lookup"><span data-stu-id="64bd0-387">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="64bd0-388">W poniższym przykładzie pokazano odwołanie do dla wszystkich platform docelowych i odwołanie do dla .NET Framework `System.Net` `System.ServiceModel` 4.0:</span><span class="sxs-lookup"><span data-stu-id="64bd0-388">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="64bd0-389">Łącznie z plikami zestawu</span><span class="sxs-lookup"><span data-stu-id="64bd0-389">Including assembly files</span></span>

<span data-ttu-id="64bd0-390">Jeśli są zgodne z konwencjami opisanymi w [tworzenie](../create-packages/creating-a-package.md)pakietu , nie trzeba jawnie określić listę plików w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="64bd0-390">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="64bd0-391">Polecenie `nuget pack` automatycznie pobiera niezbędne pliki.</span><span class="sxs-lookup"><span data-stu-id="64bd0-391">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="64bd0-392">Po zainstalowaniu pakietu w projekcie pakiet NuGet automatycznie dodaje odwołania do zestawów do bibliotek DLL *pakietu,* z wyłączeniem tych, które są nazwane, ponieważ zakłada się, że są zlokalizowane zestawy `.resources.dll` satelicki.</span><span class="sxs-lookup"><span data-stu-id="64bd0-392">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="64bd0-393">Z tego powodu należy unikać używania dla `.resources.dll` plików, które w przeciwnym razie zawierają podstawowy kod pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-393">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="64bd0-394">Aby pominąć to automatyczne zachowanie i jawnie kontrolować, które pliki znajdują się w pakiecie, umieść element jako element podrzędny (i element równorzędny ), identyfikując każdy plik z `<files>` `<package>` `<metadata>` oddzielnym `<file>` elementem.</span><span class="sxs-lookup"><span data-stu-id="64bd0-394">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="64bd0-395">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="64bd0-395">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="64bd0-396">W programie NuGet 2.x i starszych wersjach oraz projektach korzystających z programu element jest również używany do dołączania niezmiennych plików zawartości podczas `packages.config` `<files>` instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-396">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="64bd0-397">W przypadku pakietów NuGet 3.3+ i projektów PackageReference zamiast tego `<contentFiles>` jest używany element .</span><span class="sxs-lookup"><span data-stu-id="64bd0-397">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="64bd0-398">Aby uzyskać [szczegółowe informacje, zobacz](#including-content-files) temat Including content files below (Zawieranie plików zawartości poniżej).</span><span class="sxs-lookup"><span data-stu-id="64bd0-398">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="64bd0-399">Atrybuty elementu pliku</span><span class="sxs-lookup"><span data-stu-id="64bd0-399">File element attributes</span></span>

<span data-ttu-id="64bd0-400">Każdy `<file>` element określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="64bd0-400">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="64bd0-401">Atrybut</span><span class="sxs-lookup"><span data-stu-id="64bd0-401">Attribute</span></span> | <span data-ttu-id="64bd0-402">Opis</span><span class="sxs-lookup"><span data-stu-id="64bd0-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64bd0-403">**src**</span><span class="sxs-lookup"><span data-stu-id="64bd0-403">**src**</span></span> | <span data-ttu-id="64bd0-404">Lokalizacja pliku lub plików dołączyć, z zastrzeżeniem wykluczeń określonych przez `exclude` atrybut.</span><span class="sxs-lookup"><span data-stu-id="64bd0-404">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="64bd0-405">Ścieżka jest względna do `.nuspec` pliku, chyba że określono ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="64bd0-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="64bd0-406">Symbol wieloznaczny `*` jest dozwolony, a podwójny symbol wieloznaczny `**` oznacza cykliczne wyszukiwanie w folderze.</span><span class="sxs-lookup"><span data-stu-id="64bd0-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="64bd0-407">**Docelowego**</span><span class="sxs-lookup"><span data-stu-id="64bd0-407">**target**</span></span> | <span data-ttu-id="64bd0-408">Ścieżka względna do folderu w pakiecie, w którym znajdują się pliki źródłowe, która musi zaczynać się `lib` od , , lub `content` `build` `tools` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-408">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="64bd0-409">Zobacz [Creating a .nuspec from a convention-based working directory (Tworzenie .nuspec z katalogu roboczego opartego na konwencji).](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)</span><span class="sxs-lookup"><span data-stu-id="64bd0-409">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="64bd0-410">**wykluczanie**</span><span class="sxs-lookup"><span data-stu-id="64bd0-410">**exclude**</span></span> | <span data-ttu-id="64bd0-411">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-411">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="64bd0-412">Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie w folderze.</span><span class="sxs-lookup"><span data-stu-id="64bd0-412">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="64bd0-413">Przykłady</span><span class="sxs-lookup"><span data-stu-id="64bd0-413">Examples</span></span>

<span data-ttu-id="64bd0-414">**Pojedynczy zestaw**</span><span class="sxs-lookup"><span data-stu-id="64bd0-414">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="64bd0-415">**Pojedynczy zestaw specyficzny dla struktury docelowej**</span><span class="sxs-lookup"><span data-stu-id="64bd0-415">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="64bd0-416">**Zestaw bibliotek DLL używających symboli wieloznacznych**</span><span class="sxs-lookup"><span data-stu-id="64bd0-416">**Set of DLLs using a wildcard**</span></span>

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

<span data-ttu-id="64bd0-417">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="64bd0-417">**DLLs for different frameworks**</span></span>

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

<span data-ttu-id="64bd0-418">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="64bd0-418">**Excluding files**</span></span>

```
Source files:
    \tools\fileA.bak
    \tools\fileB.bak
    \tools\fileA.log
    \tools\build\fileB.log

.nuspec entries:
    <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
    <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

Package result:
    (no files)
```

## <a name="including-content-files"></a><span data-ttu-id="64bd0-419">Łącznie z plikami zawartości</span><span class="sxs-lookup"><span data-stu-id="64bd0-419">Including content files</span></span>

<span data-ttu-id="64bd0-420">Pliki zawartości to pliki niezmienne, które pakiet musi uwzględnić w projekcie.</span><span class="sxs-lookup"><span data-stu-id="64bd0-420">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="64bd0-421">Będąc niezmiennym, nie są one przeznaczone do modyfikacji przez projekt konsumowania.</span><span class="sxs-lookup"><span data-stu-id="64bd0-421">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="64bd0-422">Przykładowe pliki zawartości:</span><span class="sxs-lookup"><span data-stu-id="64bd0-422">Example content files include:</span></span>

- <span data-ttu-id="64bd0-423">Obrazy osadzone jako zasoby</span><span class="sxs-lookup"><span data-stu-id="64bd0-423">Images that are embedded as resources</span></span>
- <span data-ttu-id="64bd0-424">Pliki źródłowe, które zostały już skompilowane</span><span class="sxs-lookup"><span data-stu-id="64bd0-424">Source files that are already compiled</span></span>
- <span data-ttu-id="64bd0-425">Skrypty, które muszą zostać dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="64bd0-425">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="64bd0-426">Pliki konfiguracji pakietu, które muszą zostać uwzględnione w projekcie, ale nie wymagają żadnych zmian specyficznych dla projektu</span><span class="sxs-lookup"><span data-stu-id="64bd0-426">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="64bd0-427">Pliki zawartości są zawarte w pakiecie przy użyciu `<files>` elementu , określając folder w `content` `target` atrybutze .</span><span class="sxs-lookup"><span data-stu-id="64bd0-427">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="64bd0-428">Jednak takie pliki są ignorowane, gdy pakiet jest instalowany w projekcie przy użyciu packageReference, który zamiast tego używa `<contentFiles>` elementu .</span><span class="sxs-lookup"><span data-stu-id="64bd0-428">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="64bd0-429">W celu zapewnienia maksymalnej zgodności z projektami konsumowymi pakiet w idealnym przypadku określa pliki zawartości w obu elementach.</span><span class="sxs-lookup"><span data-stu-id="64bd0-429">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="64bd0-430">Używanie elementu files dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="64bd0-430">Using the files element for content files</span></span>

<span data-ttu-id="64bd0-431">W przypadku plików zawartości po prostu użyj tego samego formatu, co w przypadku plików zestawu, ale określ jako folder podstawowy w atrybutze , jak pokazano `content` `target` w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="64bd0-431">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="64bd0-432">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="64bd0-432">**Basic content files**</span></span>

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

<span data-ttu-id="64bd0-433">**Pliki zawartości ze strukturą katalogów**</span><span class="sxs-lookup"><span data-stu-id="64bd0-433">**Content files with directory structure**</span></span>

```
Source files:
    css\mobile\style.css
    css\mobile\wp7\style.css
    css\browser\style.css

.nuspec entry:
    <file src="css\**\*.css" target="content\css" />

Packaged result:
    content\css\mobile\style.css
    content\css\mobile\wp7\style.css
    content\css\browser\style.css
```

<span data-ttu-id="64bd0-434">**Plik zawartości specyficzny dla struktury docelowej**</span><span class="sxs-lookup"><span data-stu-id="64bd0-434">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="64bd0-435">**Plik zawartości skopiowany do folderu z kropką w nazwie**</span><span class="sxs-lookup"><span data-stu-id="64bd0-435">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="64bd0-436">W takim przypadku nuGet widzi, że rozszerzenie w pliku nie jest zgodne z rozszerzeniem w pliku i w związku z tym traktuje tę część nazwy `target` `src` w `target` folderze:</span><span class="sxs-lookup"><span data-stu-id="64bd0-436">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="64bd0-437">**Pliki zawartości bez rozszerzeń**</span><span class="sxs-lookup"><span data-stu-id="64bd0-437">**Content files without extensions**</span></span>

<span data-ttu-id="64bd0-438">Aby dołączyć pliki bez rozszerzenia, użyj `*` symboli wieloznacznych `**` lub :</span><span class="sxs-lookup"><span data-stu-id="64bd0-438">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="64bd0-439">**Pliki zawartości ze ścieżką głęboką i głębokim elementem docelowym**</span><span class="sxs-lookup"><span data-stu-id="64bd0-439">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="64bd0-440">W tym przypadku, ponieważ rozszerzenia pliku źródłowego i docelowego są zgodne, nuGet zakłada, że element docelowy jest nazwą pliku, a nie folderem:</span><span class="sxs-lookup"><span data-stu-id="64bd0-440">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

<span data-ttu-id="64bd0-441">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="64bd0-441">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="64bd0-442">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="64bd0-442">**Excluding files**</span></span>

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="64bd0-443">Używanie elementu contentFiles dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="64bd0-443">Using the contentFiles element for content files</span></span>

<span data-ttu-id="64bd0-444">*NuGet 4.0+ z packageReference*</span><span class="sxs-lookup"><span data-stu-id="64bd0-444">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="64bd0-445">Domyślnie pakiet umieszcza zawartość w folderze (patrz poniżej) i uwzględnia wszystkie pliki w `contentFiles` `nuget pack` tym folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="64bd0-445">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="64bd0-446">W takim przypadku nie trzeba w ogóle uwzględniać węzła w `contentFiles` `.nuspec` węźle .</span><span class="sxs-lookup"><span data-stu-id="64bd0-446">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="64bd0-447">Aby kontrolować, które pliki są dołączone, element określa kolekcję elementów, które `<contentFiles>` identyfikują dokładne pliki `<files>` obejmują.</span><span class="sxs-lookup"><span data-stu-id="64bd0-447">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="64bd0-448">Te pliki są określane za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu:</span><span class="sxs-lookup"><span data-stu-id="64bd0-448">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="64bd0-449">Atrybut</span><span class="sxs-lookup"><span data-stu-id="64bd0-449">Attribute</span></span> | <span data-ttu-id="64bd0-450">Opis</span><span class="sxs-lookup"><span data-stu-id="64bd0-450">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64bd0-451">**Obejmują**</span><span class="sxs-lookup"><span data-stu-id="64bd0-451">**include**</span></span> | <span data-ttu-id="64bd0-452">(Wymagane) Lokalizacja pliku lub plików dołączyć, z zastrzeżeniem wykluczeń określonych przez `exclude` atrybut.</span><span class="sxs-lookup"><span data-stu-id="64bd0-452">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="64bd0-453">Ścieżka jest względna względem `contentFiles` folderu, chyba że określono ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="64bd0-453">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="64bd0-454">Symbol wieloznaczny `*` jest dozwolony, a podwójny symbol wieloznaczny `**` oznacza cykliczne wyszukiwanie w folderze.</span><span class="sxs-lookup"><span data-stu-id="64bd0-454">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="64bd0-455">**wykluczanie**</span><span class="sxs-lookup"><span data-stu-id="64bd0-455">**exclude**</span></span> | <span data-ttu-id="64bd0-456">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="64bd0-456">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="64bd0-457">Symbol wieloznaczny `*` jest dozwolony, a podwójny symbol wieloznaczny `**` oznacza cykliczne wyszukiwanie w folderze.</span><span class="sxs-lookup"><span data-stu-id="64bd0-457">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="64bd0-458">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="64bd0-458">**buildAction**</span></span> | <span data-ttu-id="64bd0-459">Akcja kompilacji do przypisania do elementu zawartości dla programu MSBuild, takiego jak `Content` , `None` , , `Embedded Resource` `Compile` itp. Wartość domyślna to `Compile` .</span><span class="sxs-lookup"><span data-stu-id="64bd0-459">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="64bd0-460">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="64bd0-460">**copyToOutput**</span></span> | <span data-ttu-id="64bd0-461">Wartość logiczna wskazująca, czy kopiować elementy zawartości do folderu wyjściowego kompilacji (lub publikowania).</span><span class="sxs-lookup"><span data-stu-id="64bd0-461">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="64bd0-462">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="64bd0-462">The default is false.</span></span> |
| <span data-ttu-id="64bd0-463">**Spłaszczyć**</span><span class="sxs-lookup"><span data-stu-id="64bd0-463">**flatten**</span></span> | <span data-ttu-id="64bd0-464">Wartość logiczna wskazująca, czy kopiować elementy zawartości do jednego folderu w danych wyjściowych kompilacji (true), czy zachować strukturę folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="64bd0-464">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="64bd0-465">Ta flaga działa tylko wtedy, gdy flaga copyToOutput jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="64bd0-465">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="64bd0-466">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="64bd0-466">The default is false.</span></span> |

<span data-ttu-id="64bd0-467">Podczas instalowania pakietu pakiet NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-467">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="64bd0-468">Jeśli wiele wpisów pasuje do tego samego pliku, wszystkie wpisy są stosowane.</span><span class="sxs-lookup"><span data-stu-id="64bd0-468">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="64bd0-469">Wpis o najwyższej wartości zastępuje niższe wpisy, jeśli występuje konflikt dla tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-469">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="64bd0-470">Struktura folderów pakietów</span><span class="sxs-lookup"><span data-stu-id="64bd0-470">Package folder structure</span></span>

<span data-ttu-id="64bd0-471">Projekt pakietu powinien mieć strukturę zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="64bd0-471">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="64bd0-472">`codeLanguages` może być `cs` , , , , lub `vb` `fs` `any` małymi literami równoważnymi danej `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="64bd0-472">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="64bd0-473">`TxM` to dowolna prawna docelowa moniker struktury, która obsługuje program NuGet (zobacz [Platforme docelowe](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="64bd0-473">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="64bd0-474">Na końcu tej składni można dołączyć dowolną strukturę folderów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-474">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="64bd0-475">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="64bd0-475">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="64bd0-476">Puste foldery mogą zrezygnować z dostarczania zawartości dla niektórych kombinacji języka i `.` TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="64bd0-476">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="64bd0-477">Przykładowa sekcja contentFiles</span><span class="sxs-lookup"><span data-stu-id="64bd0-477">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="64bd0-478">Grupy odwoływać się do struktury</span><span class="sxs-lookup"><span data-stu-id="64bd0-478">Framework reference groups</span></span>

<span data-ttu-id="64bd0-479">*Tylko wersja 5.1 lub nowsza PackageReference*</span><span class="sxs-lookup"><span data-stu-id="64bd0-479">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="64bd0-480">Odwołania do platformy to pojęcie platformy .NET Core reprezentujące platformy udostępnione, takie jak WPF lub Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="64bd0-480">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="64bd0-481">Określając udostępnioną platformę, pakiet zapewnia, że wszystkie jego zależności struktury zostaną uwzględnione w projekcie odwołującym się.</span><span class="sxs-lookup"><span data-stu-id="64bd0-481">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="64bd0-482">Każdy `<group>` element wymaga `targetFramework` atrybutu i zero lub więcej `<frameworkReference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="64bd0-482">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="64bd0-483">W poniższym przykładzie pokazano nuspec wygenerowany dla projektu WPF platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="64bd0-483">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="64bd0-484">Należy pamiętać, że ręczne tworzenie nuspecs, które zawierają odwołania do struktury nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="64bd0-484">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="64bd0-485">Zamiast tego rozważ użycie [pakietu targets,](msbuild-targets.md) który automatycznie wywnioskuje je z projektu.</span><span class="sxs-lookup"><span data-stu-id="64bd0-485">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="64bd0-486">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="64bd0-486">Example nuspec files</span></span>

<span data-ttu-id="64bd0-487">**Prosta, `.nuspec` która nie określa zależności ani plików**</span><span class="sxs-lookup"><span data-stu-id="64bd0-487">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="64bd0-488">**A `.nuspec` z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="64bd0-488">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="64bd0-489">**A `.nuspec` z plikami**</span><span class="sxs-lookup"><span data-stu-id="64bd0-489">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="64bd0-490">**A `.nuspec` z zestawami platform**</span><span class="sxs-lookup"><span data-stu-id="64bd0-490">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="64bd0-491">W tym przykładzie dla określonych celów projektu są instalowane następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="64bd0-491">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="64bd0-492">. NET4 — > `System.Web` , `System.Net`</span><span class="sxs-lookup"><span data-stu-id="64bd0-492">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="64bd0-493">. Profil klienta NET4 — > `System.Net`</span><span class="sxs-lookup"><span data-stu-id="64bd0-493">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="64bd0-494">Silverlight 3 —> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="64bd0-494">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="64bd0-495">WindowsPhone — > `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="64bd0-495">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
