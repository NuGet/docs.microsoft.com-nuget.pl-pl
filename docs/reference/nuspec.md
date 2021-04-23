---
title: Odwołanie do pliku nuspec dla nuGet
description: Plik nuspec zawiera metadane pakietu używane podczas budowania pakietu i w celu zapewnienia informacji klientom pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ed865aad6f72752adcf3e3921287a20b961c4a8a
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901814"
---
# <a name="nuspec-reference"></a><span data-ttu-id="7631d-103">Odwołanie do nuspec</span><span class="sxs-lookup"><span data-stu-id="7631d-103">.nuspec reference</span></span>

<span data-ttu-id="7631d-104">Plik `.nuspec` jest manifestem XML, który zawiera metadane pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="7631d-105">Ten manifest jest używany zarówno do kompilowania pakietu, jak i do zapewnienia informacji klientom.</span><span class="sxs-lookup"><span data-stu-id="7631d-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="7631d-106">Manifest jest zawsze zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="7631d-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="7631d-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="7631d-107">In this topic:</span></span>

- [<span data-ttu-id="7631d-108">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="7631d-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="7631d-109">[Tokeny zastępcze](#replacement-tokens) (w przypadku korzystania z Visual Studio projektu)</span><span class="sxs-lookup"><span data-stu-id="7631d-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="7631d-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="7631d-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="7631d-111">Jawne odwołania do zestawu</span><span class="sxs-lookup"><span data-stu-id="7631d-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="7631d-112">Odwołania do zestawu struktury</span><span class="sxs-lookup"><span data-stu-id="7631d-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="7631d-113">Łącznie z plikami zestawu</span><span class="sxs-lookup"><span data-stu-id="7631d-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="7631d-114">Łącznie z plikami zawartości</span><span class="sxs-lookup"><span data-stu-id="7631d-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="7631d-115">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="7631d-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="7631d-116">Zgodność typu projektu</span><span class="sxs-lookup"><span data-stu-id="7631d-116">Project type compatibility</span></span>

- <span data-ttu-id="7631d-117">Użyj `.nuspec` z dla projektów innych niż zestaw `nuget.exe pack` SDK, które używają `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="7631d-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="7631d-118">Plik nie jest wymagany do tworzenia pakietów dla projektów w stylu zestawu SDK (zazwyczaj platformy .NET Core i projektów .NET Standard, które `.nuspec` używają [atrybutu SDK](/dotnet/core/tools/csproj#additions)). [](../resources/check-project-format.md)</span><span class="sxs-lookup"><span data-stu-id="7631d-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="7631d-119">(Zwróć uwagę, że podczas tworzenia pakietu `.nuspec` jest generowany obiekt .</span><span class="sxs-lookup"><span data-stu-id="7631d-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="7631d-120">Jeśli tworzysz pakiet przy użyciu polecenia lub , zalecamy dołącz zamiast tego wszystkie właściwości, które zwykle znajdują się `dotnet.exe pack` `msbuild pack target` w pliku [](../reference/msbuild-targets.md#pack-target) `.nuspec` projektu.</span><span class="sxs-lookup"><span data-stu-id="7631d-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="7631d-121">Zamiast tego można jednak użyć pliku do pakowania przy użyciu [ `.nuspec` programu `dotnet.exe` lub `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="7631d-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="7631d-122">W przypadku projektów migrowanych z do `packages.config` [packageReference](../consume-packages/package-references-in-project-files.md) `.nuspec` plik nie jest wymagany do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="7631d-123">Zamiast tego użyj [msbuild -t:pack.](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)</span><span class="sxs-lookup"><span data-stu-id="7631d-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="7631d-124">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="7631d-124">General form and schema</span></span>

<span data-ttu-id="7631d-125">Bieżący plik `nuspec.xsd` schematu można znaleźć w [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="7631d-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="7631d-126">W ramach tego schematu `.nuspec` plik ma następującą ogólną postać:</span><span class="sxs-lookup"><span data-stu-id="7631d-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="7631d-127">Aby uzyskać czytelną wizualną reprezentację schematu, otwórz plik schematu w Visual Studio w trybie projektowania i kliknij link **Eksplorator schematu XML.**</span><span class="sxs-lookup"><span data-stu-id="7631d-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="7631d-128">Alternatywnie otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz polecenie **Pokaż Eksplorator schematu XML.**</span><span class="sxs-lookup"><span data-stu-id="7631d-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="7631d-129">W obu sposób możesz uzyskać widok podobny do poniższego (w przypadku większości rozwiniętego):</span><span class="sxs-lookup"><span data-stu-id="7631d-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Schema Explorer z otwartym programem nuspec.xsd](media/SchemaExplorer.png)

<span data-ttu-id="7631d-131">W nazwach wszystkich elementów XML w pliku nuspec jest wielkość liter, podobnie jak w przypadku XML.</span><span class="sxs-lookup"><span data-stu-id="7631d-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="7631d-132">Na przykład użycie elementu metadanych `<description>` jest poprawne i nie jest `<Description>` poprawne.</span><span class="sxs-lookup"><span data-stu-id="7631d-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="7631d-133">Prawidłowa nazwa każdego elementu zawiera prawidłową wielkością wielkości.</span><span class="sxs-lookup"><span data-stu-id="7631d-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="7631d-134">Wymagane elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="7631d-134">Required metadata elements</span></span>

<span data-ttu-id="7631d-135">Chociaż poniższe elementy są minimalnymi wymaganiami pakietu, należy [](#optional-metadata-elements) rozważyć dodanie opcjonalnych elementów metadanych w celu poprawienia ogólnego środowiska pracy deweloperów z pakietem.</span><span class="sxs-lookup"><span data-stu-id="7631d-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="7631d-136">Te elementy muszą znajdować się w `<metadata>` elemencie.</span><span class="sxs-lookup"><span data-stu-id="7631d-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="7631d-137">identyfikator</span><span class="sxs-lookup"><span data-stu-id="7631d-137">id</span></span> 
<span data-ttu-id="7631d-138">Identyfikator pakietu bez uwzględniania liter, który musi być unikatowy w nuget.org galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="7631d-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="7631d-139">Identyfikatory mogą nie zawierać spacji lub znaków, które nie są prawidłowe dla adresu URL, i zazwyczaj są zgodne z regułami przestrzeni nazw .NET.</span><span class="sxs-lookup"><span data-stu-id="7631d-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="7631d-140">Aby [uzyskać wskazówki, zobacz Choosing a unique package identifier (Wybieranie unikatowego identyfikatora](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) pakietu).</span><span class="sxs-lookup"><span data-stu-id="7631d-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="7631d-141">Podczas przekazywania pakietu do nuget.org pole `id` jest ograniczone do 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="7631d-142">Wersja</span><span class="sxs-lookup"><span data-stu-id="7631d-142">version</span></span>
<span data-ttu-id="7631d-143">Wersja pakietu, zgodnie ze wzorcem *główna.pomocnicza.poprawka.*</span><span class="sxs-lookup"><span data-stu-id="7631d-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="7631d-144">Numery wersji mogą zawierać sufiks wersji wstępnej zgodnie z opisem [w tece Wersje pakietu](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="7631d-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="7631d-145">Podczas przekazywania pakietu do nuget.org pole `version` jest ograniczone do 64 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="7631d-146">description (opis)</span><span class="sxs-lookup"><span data-stu-id="7631d-146">description</span></span>
<span data-ttu-id="7631d-147">Opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7631d-147">A description of the package for UI display.</span></span>

<span data-ttu-id="7631d-148">Podczas przekazywania pakietu do nuget.org pole `description` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="7631d-149">Autorów</span><span class="sxs-lookup"><span data-stu-id="7631d-149">authors</span></span>
<span data-ttu-id="7631d-150">Rozdzielana przecinkami lista autorów pakietów, pasująca do nazw profilów nuget.org. Są one wyświetlane w galerii NuGet na nuget.org i są używane do odsyłania pakietów przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="7631d-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="7631d-151">Podczas przekazywania pakietu do nuget.org pole `authors` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="7631d-152">Opcjonalne elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="7631d-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="7631d-153">Właścicieli</span><span class="sxs-lookup"><span data-stu-id="7631d-153">owners</span></span>
> [!Important]
> <span data-ttu-id="7631d-154">Właściciele są przestarzali.</span><span class="sxs-lookup"><span data-stu-id="7631d-154">owners is deprecated.</span></span> <span data-ttu-id="7631d-155">Zamiast tego należy używać autorów.</span><span class="sxs-lookup"><span data-stu-id="7631d-155">Use authors instead.</span></span>

<span data-ttu-id="7631d-156">Rozdzielana przecinkami lista twórców pakietów używających nazw profilów w nuget.org. Jest to często ta sama lista co w pliku i jest ignorowana podczas przekazywania pakietu do `authors` nuget.org. Zobacz Managing package owners on nuget.org (Zarządzanie [właścicielami pakietów na nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)).</span><span class="sxs-lookup"><span data-stu-id="7631d-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="7631d-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="7631d-157">projectUrl</span></span>
<span data-ttu-id="7631d-158">Adres URL strony głównej pakietu, często wyświetlany w interfejsie użytkownika, a także adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7631d-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="7631d-159">Podczas przekazywania pakietu do nuget.org pole `projectUrl` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="7631d-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="7631d-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="7631d-161">LicenseUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="7631d-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="7631d-162">Zamiast tego użyj licencji.</span><span class="sxs-lookup"><span data-stu-id="7631d-162">Use license instead.</span></span>

<span data-ttu-id="7631d-163">Adres URL licencji pakietu, często wyświetlany w interfejsach użytkownika, takich jak nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7631d-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="7631d-164">Podczas przekazywania pakietu do nuget.org pole `licenseUrl` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="7631d-165">license (licencja)</span><span class="sxs-lookup"><span data-stu-id="7631d-165">license</span></span>

<span data-ttu-id="7631d-166">*Obsługiwane w **programie NuGet 4.9.0** i jego produktach*</span><span class="sxs-lookup"><span data-stu-id="7631d-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="7631d-167">Wyrażenie licencji SPDX lub ścieżka do pliku licencji w pakiecie, często wyświetlane w interfejsach użytkownika, takich jak nuget.org. Jeśli licencjonowanie pakietu jest na podstawie wspólnej licencji, na przykład MIT lub BSD-2-Clause, użyj skojarzonego identyfikatora licencji [SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="7631d-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="7631d-168">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7631d-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="7631d-169">NuGet.org akceptuje tylko wyrażenia licencji zatwierdzone przez inicjatywę Open Source Initiative lub Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="7631d-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="7631d-170">Jeśli pakiet jest licencjonowany w ramach wielu typowych licencji, możesz określić licencję złożoną przy użyciu składni wyrażeń [SPDX w wersji 2.0.](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)</span><span class="sxs-lookup"><span data-stu-id="7631d-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="7631d-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7631d-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="7631d-172">Jeśli używasz licencji niestandardowej, która nie jest obsługiwana przez wyrażenia licencji, możesz spakć plik lub `.txt` `.md` z tekstem licencji.</span><span class="sxs-lookup"><span data-stu-id="7631d-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="7631d-173">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7631d-173">For example:</span></span>

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

<span data-ttu-id="7631d-174">Aby uzyskać odpowiednik msBuild, zobacz [Pakowanie wyrażenia licencji lub plik licencji](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="7631d-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="7631d-175">Dokładna składnia wyrażeń licencji nuGet jest opisana poniżej w [abnf](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="7631d-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

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

#### <a name="iconurl"></a><span data-ttu-id="7631d-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="7631d-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="7631d-177">IconUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="7631d-177">iconUrl is deprecated.</span></span> <span data-ttu-id="7631d-178">Zamiast tego użyj ikony .</span><span class="sxs-lookup"><span data-stu-id="7631d-178">Use icon instead.</span></span>

<span data-ttu-id="7631d-179">Adres URL obrazu o rozdzielczości 128 x 128 z przezroczystym tłem do użycia jako ikona pakietu na ekranie interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7631d-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="7631d-180">Upewnij się, że ten element zawiera *bezpośredni adres URL obrazu,* a nie adres URL strony internetowej zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="7631d-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="7631d-181">Aby na przykład użyć obrazu z usługi GitHub, użyj adresu URL pliku nieprzetworzowego, takiego <em> https://github.com/ \<username\> / \<repository\> jak \<branch\> / \<logo.png\> /raw/</em>.</span><span class="sxs-lookup"><span data-stu-id="7631d-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="7631d-182">Podczas przekazywania pakietu do nuget.org pole `iconUrl` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="7631d-183">Ikonę</span><span class="sxs-lookup"><span data-stu-id="7631d-183">icon</span></span>

<span data-ttu-id="7631d-184">*Obsługiwane z **programem NuGet 5.3.0** i jego produktami*</span><span class="sxs-lookup"><span data-stu-id="7631d-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="7631d-185">Jest to ścieżka do pliku obrazu w pakiecie, często wyświetlana w interfejsach nuget.org jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="7631d-186">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7631d-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="7631d-187">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="7631d-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="7631d-188">Zalecamy rozdzielczość obrazu 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="7631d-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="7631d-189">Na przykład podczas tworzenia pakietu przy użyciu narzędzia do tworzenia pakietu należy dodać następujące nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="7631d-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="7631d-190">Ikona pakietu przykład nuspec.</span><span class="sxs-lookup"><span data-stu-id="7631d-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="7631d-191">Aby uzyskać odpowiednik msBuild, zobacz Pakowanie [pliku obrazu ikony](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="7631d-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="7631d-192">Można określić zarówno , `icon` jak i , aby zachować zgodność z `iconUrl` poprzednimi wersjami ze źródłami, które nie obsługują systemu `icon` .</span><span class="sxs-lookup"><span data-stu-id="7631d-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="7631d-193">Visual Studio będzie obsługiwać pakiety pochodzące ze źródła opartego `icon` na folderach w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="7631d-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="readme"></a><span data-ttu-id="7631d-194">Plik readme</span><span class="sxs-lookup"><span data-stu-id="7631d-194">readme</span></span>

<span data-ttu-id="7631d-195">*Obsługiwane w **przypadku programu NuGet 5.10.0 (wersja zapoznawcza 2 lub 2)***</span><span class="sxs-lookup"><span data-stu-id="7631d-195">*Supported with **NuGet 5.10.0 preview 2** and above*</span></span>

<span data-ttu-id="7631d-196">Podczas pakowania pliku readme należy użyć elementu , aby określić ścieżkę pakietu względem `readme` katalogu głównego pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-196">When packing a readme file, you need to use the `readme` element to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="7631d-197">Oprócz tego należy się upewnić, że plik znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="7631d-197">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="7631d-198">Obsługiwane formaty plików obejmują tylko markdown *(md).*</span><span class="sxs-lookup"><span data-stu-id="7631d-198">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="7631d-199">Na przykład należy dodać następujący kod do swojego nuspec, aby spakować plik readme do projektu:</span><span class="sxs-lookup"><span data-stu-id="7631d-199">For example, you would add the following to your nuspec in order to pack a readme file with your project:</span></span>

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

<span data-ttu-id="7631d-200">Aby uzyskać odpowiednik msBuild, zapoznaj się z tematem [Pakowanie pliku readme.](msbuild-targets.md#packagereadmefile)</span><span class="sxs-lookup"><span data-stu-id="7631d-200">For the MSBuild equivalent, take a look at [Packing a readme file](msbuild-targets.md#packagereadmefile).</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="7631d-201">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="7631d-201">requireLicenseAcceptance</span></span>
<span data-ttu-id="7631d-202">Wartość logiczna określająca, czy klient musi monitować użytkownika o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-202">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="7631d-203">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="7631d-203">developmentDependency</span></span>
<span data-ttu-id="7631d-204">*(2.8+)* Wartość logiczna określająca, czy pakiet ma być oznaczony jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="7631d-204">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="7631d-205">W przypadku pakietu PackageReference (NuGet 4.8+) ta flaga oznacza również, że wyklucza zasoby czasu kompilacji z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="7631d-205">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="7631d-206">Zobacz [DevelopmentDependency support for PackageReference (Obsługa zależności dla packageReference)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="7631d-206">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="7631d-207">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="7631d-207">summary</span></span>
> [!Important]
> <span data-ttu-id="7631d-208">`summary` jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="7631d-208">`summary` is being deprecated.</span></span> <span data-ttu-id="7631d-209">Zamiast tego użyj polecenia cmdlet `description`.</span><span class="sxs-lookup"><span data-stu-id="7631d-209">Use `description` instead.</span></span>

<span data-ttu-id="7631d-210">Krótki opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7631d-210">A short description of the package for UI display.</span></span> <span data-ttu-id="7631d-211">W przypadku pominięcia używana jest obcinana `description` wersja systemu .</span><span class="sxs-lookup"><span data-stu-id="7631d-211">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="7631d-212">Podczas przekazywania pakietu do nuget.org pole `summary` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-212">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="7631d-213">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="7631d-213">releaseNotes</span></span>
<span data-ttu-id="7631d-214">*(1.5+)* Opis zmian wprowadzonych w tej wersji pakietu, często używany  w interfejsie użytkownika, taki jak karta Aktualizacje Visual Studio Menedżer pakietów w miejsce opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-214">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="7631d-215">Podczas przekazywania pakietu do nuget.org pole `releaseNotes` jest ograniczone do 35 000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-215">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="7631d-216">informacji o prawach autorskich,</span><span class="sxs-lookup"><span data-stu-id="7631d-216">copyright</span></span>
<span data-ttu-id="7631d-217">*(1.5+)* Szczegóły praw autorskich dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-217">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="7631d-218">Podczas przekazywania pakietu do nuget.org pole `copyright` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-218">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="7631d-219">language</span><span class="sxs-lookup"><span data-stu-id="7631d-219">language</span></span>
<span data-ttu-id="7631d-220">Identyfikator regionalny pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-220">The locale ID for the package.</span></span> <span data-ttu-id="7631d-221">Zobacz [Creating localized packages (Tworzenie zlokalizowanych pakietów).](../create-packages/creating-localized-packages.md)</span><span class="sxs-lookup"><span data-stu-id="7631d-221">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="7631d-222">tags</span><span class="sxs-lookup"><span data-stu-id="7631d-222">tags</span></span>
<span data-ttu-id="7631d-223">Rozdzielana spacjami lista tagów i słów kluczowych, które opisują pakiet i wspomagają odnajdywanie pakietów za pomocą wyszukiwania i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="7631d-223">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="7631d-224">Podczas przekazywania pakietu do nuget.org pole `tags` jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-224">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="7631d-225">Sprawne</span><span class="sxs-lookup"><span data-stu-id="7631d-225">serviceable</span></span> 
<span data-ttu-id="7631d-226">*(3.3+)* Wewnętrznego nuGet należy używać tylko.</span><span class="sxs-lookup"><span data-stu-id="7631d-226">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="7631d-227">repozytorium</span><span class="sxs-lookup"><span data-stu-id="7631d-227">repository</span></span>
<span data-ttu-id="7631d-228">Metadane repozytorium składające się z czterech atrybutów opcjonalnych: `type` i `url` *(4.0+)*, `branch` i `commit` *(4.6+)*.</span><span class="sxs-lookup"><span data-stu-id="7631d-228">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="7631d-229">Te atrybuty umożliwiają mapowanie pliku do repozytorium, które go sbudowały, z możliwością uzyskania tak szczegółowych informacji jak nazwa poszczególnych gałęzi i/lub zatwierdzenie skrótu SHA-1, który sbudowali `.nupkg` pakiet.</span><span class="sxs-lookup"><span data-stu-id="7631d-229">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="7631d-230">Powinien to być publicznie dostępny adres URL, który może być wywoływany bezpośrednio przez oprogramowanie do kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="7631d-230">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="7631d-231">Nie powinna to być strona HTML, ponieważ jest przeznaczona dla komputera.</span><span class="sxs-lookup"><span data-stu-id="7631d-231">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="7631d-232">W przypadku łączenia ze stroną projektu zamiast `projectUrl` tego użyj pola .</span><span class="sxs-lookup"><span data-stu-id="7631d-232">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="7631d-233">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7631d-233">For example:</span></span>
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

<span data-ttu-id="7631d-234">Podczas przekazywania pakietu do nuget.org atrybut jest ograniczony do 100 znaków, a atrybut jest ograniczony do `type` `url` 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-234">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="7631d-235">tytuł</span><span class="sxs-lookup"><span data-stu-id="7631d-235">title</span></span>
<span data-ttu-id="7631d-236">Zostanie wyświetlony przyjazny dla człowieka tytuł pakietu, który może być używany w niektórych interfejsach użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7631d-236">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="7631d-237">(nuget.org i Menedżer pakietów w Visual Studio nie są wyświetlane tytuły)</span><span class="sxs-lookup"><span data-stu-id="7631d-237">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="7631d-238">Podczas przekazywania pakietu do nuget.org pole jest ograniczone do 256 znaków, ale nie jest używane `title` do żadnych celów wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="7631d-238">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="7631d-239">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="7631d-239">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="7631d-240">packageTypes</span><span class="sxs-lookup"><span data-stu-id="7631d-240">packageTypes</span></span>
<span data-ttu-id="7631d-241">*(3,5+)* Kolekcja zerową lub większą liczbę elementów określającą typ pakietu, jeśli jest inny niż `<packageType>` tradycyjny pakiet zależności.</span><span class="sxs-lookup"><span data-stu-id="7631d-241">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="7631d-242">Każdy typ packageType ma atrybuty *nazwy i* *wersji*.</span><span class="sxs-lookup"><span data-stu-id="7631d-242">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="7631d-243">Zobacz [Setting a package type (Ustawianie typu pakietu).](../create-packages/set-package-type.md)</span><span class="sxs-lookup"><span data-stu-id="7631d-243">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="7631d-244">zależności</span><span class="sxs-lookup"><span data-stu-id="7631d-244">dependencies</span></span>
<span data-ttu-id="7631d-245">Kolekcja zerowych lub większej `<dependency>` liczby elementów określających zależności dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-245">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="7631d-246">Każda zależność ma atrybuty *identyfikatora*, *wersji*, *dołączania* (3.x+) i *wykluczania* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="7631d-246">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="7631d-247">Zobacz [zależności](#dependencies-element) poniżej.</span><span class="sxs-lookup"><span data-stu-id="7631d-247">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="7631d-248">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7631d-248">frameworkAssemblies</span></span>
<span data-ttu-id="7631d-249">*(1.2+)* Kolekcja zerową lub większą liczby elementów identyfikującą odwołania do .NET Framework, których wymaga ten pakiet, co gwarantuje, że odwołania są dodawane do projektów `<frameworkAssembly>` zydujące pakiet.</span><span class="sxs-lookup"><span data-stu-id="7631d-249">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="7631d-250">Każdy element frameworkAssembly ma *atrybuty assemblyName* i *targetFramework.*</span><span class="sxs-lookup"><span data-stu-id="7631d-250">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="7631d-251">Zobacz [Temat Specifying framework assembly references (Określanie odwołań do zestawu struktury) poniżej.](#specifying-framework-assembly-references-gac)</span><span class="sxs-lookup"><span data-stu-id="7631d-251">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="7631d-252">odwołania</span><span class="sxs-lookup"><span data-stu-id="7631d-252">references</span></span>
<span data-ttu-id="7631d-253">*(1,5+)* Kolekcja zerową lub większą liczby elementów nazewnictwa zestawów w `<reference>` `lib` folderze pakietu, które są dodawane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="7631d-253">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="7631d-254">Każde odwołanie ma *atrybut* pliku.</span><span class="sxs-lookup"><span data-stu-id="7631d-254">Each reference has a *file* attribute.</span></span> <span data-ttu-id="7631d-255">`<references>` Może również zawierać `<group>` element z *atrybutem targetFramework,* który następnie zawiera `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="7631d-255">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="7631d-256">W przypadku pominięcia wszystkie odwołania w `lib` są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="7631d-256">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="7631d-257">Zobacz [Temat Specifying explicit assembly references (Określanie jawnych odwołań do zestawu)](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="7631d-257">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="7631d-258">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7631d-258">contentFiles</span></span>
<span data-ttu-id="7631d-259">*(3.3+)* Kolekcja `<files>` elementów, które identyfikują pliki zawartości, które mają być dołączane do projektu zużywającego zasoby.</span><span class="sxs-lookup"><span data-stu-id="7631d-259">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="7631d-260">Te pliki są określane za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu.</span><span class="sxs-lookup"><span data-stu-id="7631d-260">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="7631d-261">Zobacz Specifying files to include in the package below (Określanie [plików do dołączyć do poniższego](#specifying-files-to-include-in-the-package) pakietu).</span><span class="sxs-lookup"><span data-stu-id="7631d-261">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="7631d-262">files</span><span class="sxs-lookup"><span data-stu-id="7631d-262">files</span></span> 
<span data-ttu-id="7631d-263">Węzeł może zawierać węzeł jako element równorzędny dla elementu i element podrzędny w programie , aby określić, które pliki zestawu i zawartości mają zostać `<package>` `<files>` zawarte w `<metadata>` `<contentFiles>` `<metadata>` pakiecie.</span><span class="sxs-lookup"><span data-stu-id="7631d-263">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="7631d-264">Aby uzyskać [szczegółowe informacje, zobacz](#including-assembly-files) Tematy Including assembly files [(W tym pliki zestawu)](#including-content-files) i Including content files (W tym pliki zawartości) w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="7631d-264">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="7631d-265">atrybuty metadanych</span><span class="sxs-lookup"><span data-stu-id="7631d-265">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="7631d-266">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="7631d-266">minClientVersion</span></span>
<span data-ttu-id="7631d-267">Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszaną przez nuget.exe i Visual Studio Menedżer pakietów.</span><span class="sxs-lookup"><span data-stu-id="7631d-267">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="7631d-268">Jest to używane za każdym razem, gdy pakiet zależy od określonych funkcji pliku, które zostały dodane w określonej wersji `.nuspec` klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="7631d-268">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="7631d-269">Na przykład pakiet używający `developmentDependency` atrybutu powinien określać wartość "2.8" dla . `minClientVersion`</span><span class="sxs-lookup"><span data-stu-id="7631d-269">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="7631d-270">Podobnie pakiet używający `contentFiles` elementu (zobacz następną sekcję) powinien mieć `minClientVersion` wartość "3.3".</span><span class="sxs-lookup"><span data-stu-id="7631d-270">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="7631d-271">Należy również zauważyć, że ponieważ klienci NuGet wcześniejszych niż 2.5 nie rozpoznają tej flagi, zawsze odrzucają zainstalowanie pakietu niezależnie od tego, co  `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="7631d-271">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="7631d-272">Tokeny zastępcze</span><span class="sxs-lookup"><span data-stu-id="7631d-272">Replacement tokens</span></span>

<span data-ttu-id="7631d-273">Podczas tworzenia pakietu [ `nuget pack` ](../reference/cli-reference/cli-ref-pack.md) polecenie zastępuje tokeny rozdzielane $w węźle pliku wartościami, które pochodzą z pliku projektu lub `.nuspec` `<metadata>` `pack` przełącznika `-properties` polecenia.</span><span class="sxs-lookup"><span data-stu-id="7631d-273">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="7631d-274">W wierszu polecenia należy określić wartości tokenu za pomocą `nuget pack -properties <name>=<value>;<name>=<value>` polecenia .</span><span class="sxs-lookup"><span data-stu-id="7631d-274">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="7631d-275">Na przykład można użyć tokenu, takiego jak i , i podać wartości `$owners$` `$desc$` w czasie `.nuspec` pakowania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7631d-275">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="7631d-276">Aby użyć wartości z projektu, określ tokeny opisane w poniższej tabeli (AssemblyInfo odnosi się do pliku w `Properties` pliku, takim `AssemblyInfo.cs` jak lub `AssemblyInfo.vb` ).</span><span class="sxs-lookup"><span data-stu-id="7631d-276">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="7631d-277">Aby użyć tych tokenów, uruchom plik `nuget pack` projektu, a nie tylko plik `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="7631d-277">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="7631d-278">Na przykład w przypadku użycia następującego polecenia tokeny i w pliku są zastępowane `$id$` `$version$` `.nuspec` wartościami `AssemblyName` i `AssemblyVersion` projektu:</span><span class="sxs-lookup"><span data-stu-id="7631d-278">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="7631d-279">Zwykle, gdy masz projekt, tworzysz początkowo przy użyciu , `.nuspec` który automatycznie zawiera niektóre z tych `nuget spec MyProject.csproj` standardowych tokenów.</span><span class="sxs-lookup"><span data-stu-id="7631d-279">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="7631d-280">Jeśli jednak projekt nie ma wartości dla wymaganych elementów, to `.nuspec` nie `nuget pack` powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="7631d-280">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="7631d-281">Ponadto w przypadku zmiany wartości projektu należy ponownie skompilować pakiet przed utworzeniem pakietu; Można to zrobić wygodnie za pomocą przełącznika polecenia `build` pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-281">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="7631d-282">Z wyjątkiem , wartości w projekcie są używane w preferencji do wszystkich przypisanych do tego `$configuration$` samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="7631d-282">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="7631d-283">Token</span><span class="sxs-lookup"><span data-stu-id="7631d-283">Token</span></span> | <span data-ttu-id="7631d-284">Źródło wartości</span><span class="sxs-lookup"><span data-stu-id="7631d-284">Value source</span></span> | <span data-ttu-id="7631d-285">Wartość</span><span class="sxs-lookup"><span data-stu-id="7631d-285">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="7631d-286">**$id$**</span><span class="sxs-lookup"><span data-stu-id="7631d-286">**$id$**</span></span> | <span data-ttu-id="7631d-287">Plik projektu</span><span class="sxs-lookup"><span data-stu-id="7631d-287">Project file</span></span> | <span data-ttu-id="7631d-288">Nazwa_zestawu (tytuł) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="7631d-288">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="7631d-289">**$version$**</span><span class="sxs-lookup"><span data-stu-id="7631d-289">**$version$**</span></span> | <span data-ttu-id="7631d-290">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="7631d-290">AssemblyInfo</span></span> | <span data-ttu-id="7631d-291">AssemblyInformationalVersion, jeśli jest obecny, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="7631d-291">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="7631d-292">**$author$**</span><span class="sxs-lookup"><span data-stu-id="7631d-292">**$author$**</span></span> | <span data-ttu-id="7631d-293">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="7631d-293">AssemblyInfo</span></span> | <span data-ttu-id="7631d-294">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="7631d-294">AssemblyCompany</span></span> |
| <span data-ttu-id="7631d-295">**$title$**</span><span class="sxs-lookup"><span data-stu-id="7631d-295">**$title$**</span></span> | <span data-ttu-id="7631d-296">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="7631d-296">AssemblyInfo</span></span> | <span data-ttu-id="7631d-297">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="7631d-297">AssemblyTitle</span></span> |
| <span data-ttu-id="7631d-298">**$description$**</span><span class="sxs-lookup"><span data-stu-id="7631d-298">**$description$**</span></span> | <span data-ttu-id="7631d-299">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="7631d-299">AssemblyInfo</span></span> | <span data-ttu-id="7631d-300">AssemblyDescription (Deskryptor zestawu)</span><span class="sxs-lookup"><span data-stu-id="7631d-300">AssemblyDescription</span></span> |
| <span data-ttu-id="7631d-301">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="7631d-301">**$copyright$**</span></span> | <span data-ttu-id="7631d-302">Assemblyinfo</span><span class="sxs-lookup"><span data-stu-id="7631d-302">AssemblyInfo</span></span> | <span data-ttu-id="7631d-303">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="7631d-303">AssemblyCopyright</span></span> |
| <span data-ttu-id="7631d-304">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="7631d-304">**$configuration$**</span></span> | <span data-ttu-id="7631d-305">Biblioteka DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="7631d-305">Assembly DLL</span></span> | <span data-ttu-id="7631d-306">Konfiguracja używana do kompilowania zestawu, domyślnie debugowania.</span><span class="sxs-lookup"><span data-stu-id="7631d-306">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="7631d-307">Pamiętaj, że aby utworzyć pakiet przy użyciu konfiguracji wydania, zawsze używasz `-properties Configuration=Release` polecenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="7631d-307">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="7631d-308">Tokeny mogą być również używane do rozpoznawania ścieżek w przypadku dołączania [plików zestawu i](#including-assembly-files) [plików zawartości](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="7631d-308">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="7631d-309">Tokeny mają takie same nazwy jak właściwości programu MSBuild, dzięki czemu można wybierać pliki do dołączona w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="7631d-309">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="7631d-310">Jeśli na przykład użyjemy w pliku następujących `.nuspec` tokenów:</span><span class="sxs-lookup"><span data-stu-id="7631d-310">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="7631d-311">Podczas kompilowania zestawu, którego konfiguracja jest zgodna z konfiguracją w `AssemblyName` `LoggingLibrary` `Release` programie MSBuild, wynikowe wiersze w pliku w pakiecie `.nuspec` są następujące:</span><span class="sxs-lookup"><span data-stu-id="7631d-311">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="7631d-312">Element zależności</span><span class="sxs-lookup"><span data-stu-id="7631d-312">Dependencies element</span></span>

<span data-ttu-id="7631d-313">Element `<dependencies>` w `<metadata>` elemencie zawiera dowolną liczbę elementów, które identyfikują inne pakiety, od których zależy pakiet `<dependency>` najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="7631d-313">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="7631d-314">Atrybuty dla każdego z `<dependency>` nich są następujące:</span><span class="sxs-lookup"><span data-stu-id="7631d-314">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="7631d-315">Atrybut</span><span class="sxs-lookup"><span data-stu-id="7631d-315">Attribute</span></span> | <span data-ttu-id="7631d-316">Opis</span><span class="sxs-lookup"><span data-stu-id="7631d-316">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="7631d-317">(Wymagane) Identyfikator pakietu zależności, taki jak "EntityFramework" i "NUnit", który jest nazwą pakietu nuget.org na stronie pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-317">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="7631d-318">(Wymagane) Zakres wersji akceptowalnych jako zależność.</span><span class="sxs-lookup"><span data-stu-id="7631d-318">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="7631d-319">Aby [uzyskać dokładną składnię,](../concepts/package-versioning.md#version-ranges) zobacz Package versioning (Wersjonarowanie pakietów).</span><span class="sxs-lookup"><span data-stu-id="7631d-319">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="7631d-320">Wersje zmiennoprzecinowe nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="7631d-320">Floating versions are not supported.</span></span> |
| <span data-ttu-id="7631d-321">include</span><span class="sxs-lookup"><span data-stu-id="7631d-321">include</span></span> | <span data-ttu-id="7631d-322">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazująca zależność do dołączyć do końcowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-322">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="7631d-323">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="7631d-323">The default value is `all`.</span></span> |
| <span data-ttu-id="7631d-324">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="7631d-324">exclude</span></span> | <span data-ttu-id="7631d-325">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazująca zależność do wykluczenia w końcowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="7631d-325">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="7631d-326">Wartość domyślna to `build,analyzers` , która może być zbyt zapisywana.</span><span class="sxs-lookup"><span data-stu-id="7631d-326">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="7631d-327">Są `content/ ContentFiles` jednak również niejawnie wykluczane w końcowym pakiecie, którego nie można zbytniego napisano.</span><span class="sxs-lookup"><span data-stu-id="7631d-327">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="7631d-328">Tagi określone za `exclude` pomocą mają pierwszeństwo przed tagami określonymi za pomocą . `include`</span><span class="sxs-lookup"><span data-stu-id="7631d-328">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="7631d-329">Na przykład jest `include="runtime, compile" exclude="compile"` taka sama jak `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="7631d-329">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="7631d-330">Podczas przekazywania pakietu do nuget.org atrybut każdej zależności jest ograniczony do 128 znaków, a atrybut jest ograniczony do `id` `version` 256 znaków.</span><span class="sxs-lookup"><span data-stu-id="7631d-330">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="7631d-331">Dołącz/Wyklucz tag</span><span class="sxs-lookup"><span data-stu-id="7631d-331">Include/Exclude tag</span></span> | <span data-ttu-id="7631d-332">Foldery docelowe, których dotyczy problem</span><span class="sxs-lookup"><span data-stu-id="7631d-332">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="7631d-333">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7631d-333">contentFiles</span></span> | <span data-ttu-id="7631d-334">Zawartość</span><span class="sxs-lookup"><span data-stu-id="7631d-334">Content</span></span> |
| <span data-ttu-id="7631d-335">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="7631d-335">runtime</span></span> | <span data-ttu-id="7631d-336">Środowisko uruchomieniowe, zasoby i frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="7631d-336">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="7631d-337">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="7631d-337">compile</span></span> | <span data-ttu-id="7631d-338">Lib</span><span class="sxs-lookup"><span data-stu-id="7631d-338">lib</span></span> |
| <span data-ttu-id="7631d-339">kompilacja</span><span class="sxs-lookup"><span data-stu-id="7631d-339">build</span></span> | <span data-ttu-id="7631d-340">build (obiekty prop i obiekty docelowe PROGRAMU MSBuild)</span><span class="sxs-lookup"><span data-stu-id="7631d-340">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="7631d-341">natywne</span><span class="sxs-lookup"><span data-stu-id="7631d-341">native</span></span> | <span data-ttu-id="7631d-342">natywne</span><span class="sxs-lookup"><span data-stu-id="7631d-342">native</span></span> |
| <span data-ttu-id="7631d-343">brak</span><span class="sxs-lookup"><span data-stu-id="7631d-343">none</span></span> | <span data-ttu-id="7631d-344">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="7631d-344">No folders</span></span> |
| <span data-ttu-id="7631d-345">all</span><span class="sxs-lookup"><span data-stu-id="7631d-345">all</span></span> | <span data-ttu-id="7631d-346">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="7631d-346">All folders</span></span> |

<span data-ttu-id="7631d-347">Na przykład następujące wiersze wskazują zależności od wersji `PackageA` 1.1.0 lub wyższej oraz `PackageB` wersji 1.x.</span><span class="sxs-lookup"><span data-stu-id="7631d-347">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="7631d-348">Poniższe wiersze wskazują zależności od tych samych pakietów, ale określają, aby uwzględnić foldery i i wszystkie elementy oprócz folderów i `contentFiles` `build` `PackageA` `native` `compile` `PackageB` "</span><span class="sxs-lookup"><span data-stu-id="7631d-348">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="7631d-349">Podczas tworzenia pliku z projektu przy użyciu funkcji zależności, które istnieją w tym projekcie, nie są automatycznie uwzględniane `.nuspec` `nuget spec` w wynikowym `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="7631d-349">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="7631d-350">Zamiast tego należy `nuget pack myproject.csproj` użyć funkcji i pobrać plik *nuspec* z wygenerowanego pliku *nupkg.*</span><span class="sxs-lookup"><span data-stu-id="7631d-350">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="7631d-351">Ten *plik nuspec* zawiera zależności.</span><span class="sxs-lookup"><span data-stu-id="7631d-351">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="7631d-352">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="7631d-352">Dependency groups</span></span>

<span data-ttu-id="7631d-353">*Wersja 2.0 lub nowsza*</span><span class="sxs-lookup"><span data-stu-id="7631d-353">*Version 2.0+*</span></span>

<span data-ttu-id="7631d-354">Alternatywą dla pojedynczej listy płaskiej jest możliwość określonej zależności zgodnie z profilem struktury projektu docelowego przy użyciu `<group>` elementów w ramach . `<dependencies>`</span><span class="sxs-lookup"><span data-stu-id="7631d-354">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="7631d-355">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów.</span><span class="sxs-lookup"><span data-stu-id="7631d-355">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="7631d-356">Te zależności są instalowane razem, gdy docelowa framework jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="7631d-356">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="7631d-357">Element `<group>` bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista zależności.</span><span class="sxs-lookup"><span data-stu-id="7631d-357">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="7631d-358">Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).</span><span class="sxs-lookup"><span data-stu-id="7631d-358">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="7631d-359">Format grupy nie może być połączony z listą płaską.</span><span class="sxs-lookup"><span data-stu-id="7631d-359">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="7631d-360">Format monikera struktury docelowej [(TFM)](../reference/target-frameworks.md) używanej w folderze różni się w porównaniu z `lib/ref` programem TFM używanym w programie `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="7631d-360">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="7631d-361">Jeśli struktury docelowe zadeklarowane w folderze i pliku nie mają dokładnych dopasowania, polecenie zwniesie ostrzeżenie `dependencies group` `lib/ref` `.nuspec` `pack` [NuGet NU5128.](../reference/errors-and-warnings/nu5128.md)</span><span class="sxs-lookup"><span data-stu-id="7631d-361">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="7631d-362">W poniższym przykładzie pokazano różne odmiany `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="7631d-362">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="7631d-363">Jawne odwołania do zestawu</span><span class="sxs-lookup"><span data-stu-id="7631d-363">Explicit assembly references</span></span>

<span data-ttu-id="7631d-364">Element jest używany przez projekty przy użyciu , aby jawnie określić zestawy, do których powinien odwoływać się projekt docelowy `<references>` `packages.config` podczas korzystania z pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-364">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="7631d-365">Odwołania jawne są zwykle używane dla zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="7631d-365">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="7631d-366">Aby uzyskać więcej informacji, zobacz stronę [wybierania zestawów,](../create-packages/select-assemblies-referenced-by-projects.md) do których odwołują się projekty.</span><span class="sxs-lookup"><span data-stu-id="7631d-366">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="7631d-367">Na przykład następujący element instruuje program NuGet, aby dodał odwołania tylko do elementu i nawet jeśli w pakiecie znajdują się `<references>` `xunit.dll` dodatkowe `xunit.extensions.dll` zestawy:</span><span class="sxs-lookup"><span data-stu-id="7631d-367">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="7631d-368">Grupy odwoływek</span><span class="sxs-lookup"><span data-stu-id="7631d-368">Reference groups</span></span>

<span data-ttu-id="7631d-369">Alternatywą dla pojedynczej listy płaskiej można określić odwołania zgodnie z profilem struktury projektu docelowego przy użyciu `<group>` elementów w ramach `<references>` .</span><span class="sxs-lookup"><span data-stu-id="7631d-369">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="7631d-370">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="7631d-370">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="7631d-371">Te odwołania są dodawane do projektu, gdy docelowa framework jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="7631d-371">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="7631d-372">Element `<group>` bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista odwołań.</span><span class="sxs-lookup"><span data-stu-id="7631d-372">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="7631d-373">Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).</span><span class="sxs-lookup"><span data-stu-id="7631d-373">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="7631d-374">Format grupy nie może być połączony z listą płaską.</span><span class="sxs-lookup"><span data-stu-id="7631d-374">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="7631d-375">W poniższym przykładzie pokazano różne odmiany `<group>` elementu :</span><span class="sxs-lookup"><span data-stu-id="7631d-375">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="7631d-376">Odwołania do zestawu struktury</span><span class="sxs-lookup"><span data-stu-id="7631d-376">Framework assembly references</span></span>

<span data-ttu-id="7631d-377">Zestawy struktury to te, które są częścią programu .NET Framework i powinny już być w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej maszyny.</span><span class="sxs-lookup"><span data-stu-id="7631d-377">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="7631d-378">Identyfikując te zestawy w elemencie, pakiet może zapewnić, że wymagane odwołania zostaną dodane do projektu w przypadku, gdy projekt nie ma jeszcze `<frameworkAssemblies>` takich odwołań.</span><span class="sxs-lookup"><span data-stu-id="7631d-378">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="7631d-379">Oczywiście takie zestawy nie są bezpośrednio zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="7631d-379">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="7631d-380">Element `<frameworkAssemblies>` zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="7631d-380">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="7631d-381">Atrybut</span><span class="sxs-lookup"><span data-stu-id="7631d-381">Attribute</span></span> | <span data-ttu-id="7631d-382">Opis</span><span class="sxs-lookup"><span data-stu-id="7631d-382">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7631d-383">**Assemblyname**</span><span class="sxs-lookup"><span data-stu-id="7631d-383">**assemblyName**</span></span> | <span data-ttu-id="7631d-384">(Wymagane) W pełni kwalifikowana nazwa zestawu.</span><span class="sxs-lookup"><span data-stu-id="7631d-384">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="7631d-385">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="7631d-385">**targetFramework**</span></span> | <span data-ttu-id="7631d-386">(Opcjonalnie) Określa platformę docelową, do której ma zastosowanie to odwołanie.</span><span class="sxs-lookup"><span data-stu-id="7631d-386">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="7631d-387">W przypadku pominięcia wskazuje, że odwołanie ma zastosowanie do wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="7631d-387">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="7631d-388">Aby [uzyskać dokładne identyfikatory](../reference/target-frameworks.md) platform, zobacz Target frameworks (Struktury docelowe).</span><span class="sxs-lookup"><span data-stu-id="7631d-388">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="7631d-389">W poniższym przykładzie pokazano odwołanie do dla wszystkich platform docelowych i odwołanie do dla .NET Framework `System.Net` `System.ServiceModel` 4.0:</span><span class="sxs-lookup"><span data-stu-id="7631d-389">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="7631d-390">Łącznie z plikami zestawu</span><span class="sxs-lookup"><span data-stu-id="7631d-390">Including assembly files</span></span>

<span data-ttu-id="7631d-391">W przypadku śledzenia zgodnie z konwencjami opisanymi w tece [Tworzenie](../create-packages/creating-a-package.md)pakietu nie trzeba jawnie określać listy plików w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="7631d-391">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="7631d-392">Polecenie `nuget pack` automatycznie pobiera niezbędne pliki.</span><span class="sxs-lookup"><span data-stu-id="7631d-392">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="7631d-393">Po zainstalowaniu pakietu w projekcie pakiet NuGet automatycznie dodaje odwołania do zestawów do bibliotek DLL *pakietu,* z wyłączeniem tych, które są nazwane, ponieważ zakłada się, że są zlokalizowanymi zestawami `.resources.dll` satelickimi.</span><span class="sxs-lookup"><span data-stu-id="7631d-393">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="7631d-394">Z tego powodu należy unikać używania `.resources.dll` dla plików, które w przeciwnym razie zawierają podstawowy kod pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-394">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="7631d-395">Aby pominąć to automatyczne zachowanie i jawnie kontrolować, które pliki znajdują się w pakiecie, umieść element jako element podrzędny (i element równorzędny ), identyfikując każdy plik z `<files>` `<package>` `<metadata>` oddzielnym `<file>` elementem.</span><span class="sxs-lookup"><span data-stu-id="7631d-395">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="7631d-396">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7631d-396">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="7631d-397">W programie NuGet 2.x i starszych wersjach oraz projektach korzystających z programu element jest również używany do dołączania niezmiennych plików zawartości podczas `packages.config` `<files>` instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="7631d-397">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="7631d-398">W przypadku pakietów NuGet 3.3+ i projektów PackageReference zamiast tego `<contentFiles>` jest używany element .</span><span class="sxs-lookup"><span data-stu-id="7631d-398">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="7631d-399">Aby uzyskać [szczegółowe informacje, zobacz Temat Including content files](#including-content-files) below (W tym pliki zawartości poniżej).</span><span class="sxs-lookup"><span data-stu-id="7631d-399">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="7631d-400">Atrybuty elementu pliku</span><span class="sxs-lookup"><span data-stu-id="7631d-400">File element attributes</span></span>

<span data-ttu-id="7631d-401">Każdy `<file>` element określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="7631d-401">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="7631d-402">Atrybut</span><span class="sxs-lookup"><span data-stu-id="7631d-402">Attribute</span></span> | <span data-ttu-id="7631d-403">Opis</span><span class="sxs-lookup"><span data-stu-id="7631d-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7631d-404">**src**</span><span class="sxs-lookup"><span data-stu-id="7631d-404">**src**</span></span> | <span data-ttu-id="7631d-405">Lokalizacja pliku lub plików dołączyć, z zastrzeżeniem wykluczeń określonych przez `exclude` atrybut.</span><span class="sxs-lookup"><span data-stu-id="7631d-405">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="7631d-406">Ścieżka jest względna do `.nuspec` pliku, chyba że określono ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="7631d-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="7631d-407">Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="7631d-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7631d-408">**Docelowego**</span><span class="sxs-lookup"><span data-stu-id="7631d-408">**target**</span></span> | <span data-ttu-id="7631d-409">Ścieżka względna do folderu w pakiecie, w którym znajdują się pliki źródłowe, która musi zaczynać się `lib` od , , , lub `content` `build` `tools` .</span><span class="sxs-lookup"><span data-stu-id="7631d-409">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="7631d-410">Zobacz [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)(Tworzenie nuspec z katalogu roboczego opartego na konwencji).</span><span class="sxs-lookup"><span data-stu-id="7631d-410">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="7631d-411">**wykluczanie**</span><span class="sxs-lookup"><span data-stu-id="7631d-411">**exclude**</span></span> | <span data-ttu-id="7631d-412">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7631d-412">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="7631d-413">Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="7631d-413">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="7631d-414">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7631d-414">Examples</span></span>

<span data-ttu-id="7631d-415">**Pojedynczy zestaw**</span><span class="sxs-lookup"><span data-stu-id="7631d-415">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="7631d-416">**Pojedynczy zestaw specyficzny dla struktury docelowej**</span><span class="sxs-lookup"><span data-stu-id="7631d-416">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="7631d-417">**Zestaw bibliotek DLL korzystających z symbolu wieloznacznego**</span><span class="sxs-lookup"><span data-stu-id="7631d-417">**Set of DLLs using a wildcard**</span></span>

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

<span data-ttu-id="7631d-418">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="7631d-418">**DLLs for different frameworks**</span></span>

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

<span data-ttu-id="7631d-419">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="7631d-419">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="7631d-420">Łącznie z plikami zawartości</span><span class="sxs-lookup"><span data-stu-id="7631d-420">Including content files</span></span>

<span data-ttu-id="7631d-421">Pliki zawartości to pliki niezmienne, które pakiet musi uwzględnić w projekcie.</span><span class="sxs-lookup"><span data-stu-id="7631d-421">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="7631d-422">Będąc niezmienne, nie są one przeznaczone do modyfikacji przez projekt konsumowania.</span><span class="sxs-lookup"><span data-stu-id="7631d-422">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="7631d-423">Przykładowe pliki zawartości:</span><span class="sxs-lookup"><span data-stu-id="7631d-423">Example content files include:</span></span>

- <span data-ttu-id="7631d-424">Obrazy osadzone jako zasoby</span><span class="sxs-lookup"><span data-stu-id="7631d-424">Images that are embedded as resources</span></span>
- <span data-ttu-id="7631d-425">Pliki źródłowe, które zostały już skompilowane</span><span class="sxs-lookup"><span data-stu-id="7631d-425">Source files that are already compiled</span></span>
- <span data-ttu-id="7631d-426">Skrypty, które muszą zostać dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="7631d-426">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="7631d-427">Pliki konfiguracji pakietu, które muszą zostać uwzględnione w projekcie, ale nie wymagają żadnych zmian specyficznych dla projektu</span><span class="sxs-lookup"><span data-stu-id="7631d-427">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="7631d-428">Pliki zawartości są zawarte w pakiecie przy użyciu `<files>` elementu , określając folder w `content` `target` atrybutze .</span><span class="sxs-lookup"><span data-stu-id="7631d-428">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="7631d-429">Jednak takie pliki są ignorowane, gdy pakiet jest instalowany w projekcie przy użyciu funkcji PackageReference, która zamiast tego używa `<contentFiles>` elementu .</span><span class="sxs-lookup"><span data-stu-id="7631d-429">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="7631d-430">Aby uzyskać maksymalną zgodność z konsumowanie projektów, pakiet w idealnym przypadku określa pliki zawartości w obu elementach.</span><span class="sxs-lookup"><span data-stu-id="7631d-430">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="7631d-431">Używanie elementu files dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="7631d-431">Using the files element for content files</span></span>

<span data-ttu-id="7631d-432">W przypadku plików zawartości należy po prostu użyć tego samego formatu co dla plików zestawu, ale określić jako folder podstawowy w atrybutze , jak pokazano w `content` `target` poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="7631d-432">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="7631d-433">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="7631d-433">**Basic content files**</span></span>

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

<span data-ttu-id="7631d-434">**Pliki zawartości ze strukturą katalogów**</span><span class="sxs-lookup"><span data-stu-id="7631d-434">**Content files with directory structure**</span></span>

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

<span data-ttu-id="7631d-435">**Plik zawartości specyficzny dla struktury docelowej**</span><span class="sxs-lookup"><span data-stu-id="7631d-435">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="7631d-436">**Plik zawartości skopiowany do folderu z kropką w nazwie**</span><span class="sxs-lookup"><span data-stu-id="7631d-436">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="7631d-437">W takim przypadku program NuGet widzi, że rozszerzenie w pliku nie jest zgodne z rozszerzeniem w pliku i w związku z tym traktuje tę część nazwy `target` `src` w pliku jako `target` folder:</span><span class="sxs-lookup"><span data-stu-id="7631d-437">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="7631d-438">**Pliki zawartości bez rozszerzeń**</span><span class="sxs-lookup"><span data-stu-id="7631d-438">**Content files without extensions**</span></span>

<span data-ttu-id="7631d-439">Aby dołączyć pliki bez rozszerzenia, użyj `*` symboli `**` wieloznacznych lub :</span><span class="sxs-lookup"><span data-stu-id="7631d-439">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="7631d-440">**Pliki zawartości ze ścieżką głęboką i głębokim elementem docelowym**</span><span class="sxs-lookup"><span data-stu-id="7631d-440">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="7631d-441">W tym przypadku, ponieważ rozszerzenia pliku źródłowego i docelowego są zgodne, nuGet zakłada, że element docelowy jest nazwą pliku, a nie folderem:</span><span class="sxs-lookup"><span data-stu-id="7631d-441">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

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

<span data-ttu-id="7631d-442">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="7631d-442">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="7631d-443">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="7631d-443">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="7631d-444">Używanie elementu contentFiles dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="7631d-444">Using the contentFiles element for content files</span></span>

<span data-ttu-id="7631d-445">*NuGet 4.0+ z packageReference*</span><span class="sxs-lookup"><span data-stu-id="7631d-445">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="7631d-446">Domyślnie pakiet umieszcza zawartość w folderze (patrz poniżej) i uwzględnia wszystkie pliki w `contentFiles` `nuget pack` tym folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="7631d-446">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="7631d-447">W takim przypadku nie trzeba w ogóle uwzględniać `contentFiles` węzła `.nuspec` w węźle .</span><span class="sxs-lookup"><span data-stu-id="7631d-447">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="7631d-448">Aby kontrolować, które pliki są dołączone, `<contentFiles>` element określa kolekcję `<files>` elementów, które identyfikują dokładne pliki obejmują.</span><span class="sxs-lookup"><span data-stu-id="7631d-448">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="7631d-449">Te pliki są określane za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu:</span><span class="sxs-lookup"><span data-stu-id="7631d-449">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="7631d-450">Atrybut</span><span class="sxs-lookup"><span data-stu-id="7631d-450">Attribute</span></span> | <span data-ttu-id="7631d-451">Opis</span><span class="sxs-lookup"><span data-stu-id="7631d-451">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7631d-452">**Obejmują**</span><span class="sxs-lookup"><span data-stu-id="7631d-452">**include**</span></span> | <span data-ttu-id="7631d-453">(Wymagane) Lokalizacja pliku lub plików dołączyć, z zastrzeżeniem wykluczeń określonych przez `exclude` atrybut.</span><span class="sxs-lookup"><span data-stu-id="7631d-453">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="7631d-454">Ścieżka jest względna do `contentFiles` folderu, chyba że określono ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="7631d-454">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="7631d-455">Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="7631d-455">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7631d-456">**wykluczanie**</span><span class="sxs-lookup"><span data-stu-id="7631d-456">**exclude**</span></span> | <span data-ttu-id="7631d-457">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7631d-457">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="7631d-458">Symbol wieloznaczny jest dozwolony, a podwójny symbol `*` wieloznaczny `**` implikuje cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="7631d-458">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="7631d-459">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="7631d-459">**buildAction**</span></span> | <span data-ttu-id="7631d-460">Akcja kompilacji do przypisania do elementu zawartości dla programu MSBuild, na przykład `Content` , `None` , , `Embedded Resource` `Compile` itp. Wartość domyślna to `Compile` .</span><span class="sxs-lookup"><span data-stu-id="7631d-460">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="7631d-461">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="7631d-461">**copyToOutput**</span></span> | <span data-ttu-id="7631d-462">Wartość logiczna wskazująca, czy kopiować elementy zawartości do folderu wyjściowego kompilacji (lub publikowania).</span><span class="sxs-lookup"><span data-stu-id="7631d-462">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="7631d-463">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="7631d-463">The default is false.</span></span> |
| <span data-ttu-id="7631d-464">**Spłaszczyć**</span><span class="sxs-lookup"><span data-stu-id="7631d-464">**flatten**</span></span> | <span data-ttu-id="7631d-465">Wartość logiczna wskazująca, czy kopiować elementy zawartości do jednego folderu w danych wyjściowych kompilacji (true), czy zachować strukturę folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="7631d-465">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="7631d-466">Ta flaga działa tylko wtedy, gdy flaga copyToOutput jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="7631d-466">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="7631d-467">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="7631d-467">The default is false.</span></span> |

<span data-ttu-id="7631d-468">Podczas instalowania pakietu pakiet NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="7631d-468">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="7631d-469">Jeśli wiele wpisów pasuje do tego samego pliku, zostaną zastosowane wszystkie wpisy.</span><span class="sxs-lookup"><span data-stu-id="7631d-469">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="7631d-470">Wpis o najwyższej wartości zastępuje niższe wpisy, jeśli występuje konflikt dla tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7631d-470">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="7631d-471">Struktura folderów pakietów</span><span class="sxs-lookup"><span data-stu-id="7631d-471">Package folder structure</span></span>

<span data-ttu-id="7631d-472">Projekt pakietu powinien mieć strukturę zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="7631d-472">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="7631d-473">`codeLanguages` może być `cs` , , , , lub `vb` `fs` `any` małymi literami równoważnymi danej `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="7631d-473">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="7631d-474">`TxM`to dowolna prawna docelowa podsieć struktury, która jest wspierana przez program NuGet [(zobacz Platforme docelowe).](../reference/target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="7631d-474">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="7631d-475">Na końcu tej składni można dołączyć dowolną strukturę folderów.</span><span class="sxs-lookup"><span data-stu-id="7631d-475">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="7631d-476">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7631d-476">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="7631d-477">Puste foldery mogą być używany do rezygnacji z dostarczania zawartości dla niektórych kombinacji języka i `.` TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="7631d-477">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="7631d-478">Przykładowa sekcja contentFiles</span><span class="sxs-lookup"><span data-stu-id="7631d-478">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="7631d-479">Grupy odwoływać się do struktury</span><span class="sxs-lookup"><span data-stu-id="7631d-479">Framework reference groups</span></span>

<span data-ttu-id="7631d-480">*Tylko packageReference w wersji 5.1+*</span><span class="sxs-lookup"><span data-stu-id="7631d-480">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="7631d-481">Odwołania do platformy to pojęcie platformy .NET Core reprezentujące platformy udostępnione, takie jak WPF lub Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="7631d-481">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="7631d-482">Określając platformę udostępnioną, pakiet zapewnia, że wszystkie jego zależności struktury zostaną uwzględnione w projekcie odwołującym się.</span><span class="sxs-lookup"><span data-stu-id="7631d-482">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="7631d-483">Każdy `<group>` element wymaga `targetFramework` atrybutu i zero lub więcej `<frameworkReference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="7631d-483">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="7631d-484">W poniższym przykładzie pokazano nuspec wygenerowany dla projektu WPF platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7631d-484">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="7631d-485">Należy pamiętać, że ręczne tworzenie nuspecs, które zawierają odwołania do struktury, nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="7631d-485">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="7631d-486">Zamiast tego rozważ [użycie pakietu targets,](msbuild-targets.md) który automatycznie wywnioskuje je z projektu.</span><span class="sxs-lookup"><span data-stu-id="7631d-486">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="7631d-487">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="7631d-487">Example nuspec files</span></span>

<span data-ttu-id="7631d-488">**Prosta, `.nuspec` która nie określa zależności ani plików**</span><span class="sxs-lookup"><span data-stu-id="7631d-488">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="7631d-489">**A `.nuspec` z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="7631d-489">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="7631d-490">**A `.nuspec` z plikami**</span><span class="sxs-lookup"><span data-stu-id="7631d-490">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="7631d-491">**A `.nuspec` z zestawami struktury**</span><span class="sxs-lookup"><span data-stu-id="7631d-491">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="7631d-492">W tym przykładzie dla określonych celów projektu są instalowane następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7631d-492">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="7631d-493">. NET4 — > `System.Web` , `System.Net`</span><span class="sxs-lookup"><span data-stu-id="7631d-493">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="7631d-494">. Profil klienta NET4 — > `System.Net`</span><span class="sxs-lookup"><span data-stu-id="7631d-494">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="7631d-495">Silverlight 3 —> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="7631d-495">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="7631d-496">WindowsPhone — > `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="7631d-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
