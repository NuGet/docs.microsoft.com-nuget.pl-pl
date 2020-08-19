---
title: Dokumentacja pliku. nuspec dla narzędzia NuGet
description: Plik. nuspec zawiera metadane pakietu używane podczas kompilowania pakietu i dostarczania informacji użytkownikom pakietu.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: f91d47bdf9b957b512d3d83434693ee93de07afb
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623139"
---
# <a name="nuspec-reference"></a><span data-ttu-id="80ff4-103">nuspec — odwołanie</span><span class="sxs-lookup"><span data-stu-id="80ff4-103">.nuspec reference</span></span>

<span data-ttu-id="80ff4-104">`.nuspec`Plik jest manifestem XML zawierającym metadane pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="80ff4-105">Ten manifest jest używany zarówno do kompilowania pakietu, jak i dostarczania informacji klientom.</span><span class="sxs-lookup"><span data-stu-id="80ff4-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="80ff4-106">Manifest jest zawsze zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="80ff4-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="80ff4-107">In this topic:</span></span>

- [<span data-ttu-id="80ff4-108">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="80ff4-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="80ff4-109">[Tokeny zastępcze](#replacement-tokens) (gdy są używane z projektem programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="80ff4-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="80ff4-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="80ff4-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="80ff4-111">Jawne odwołania do zestawów</span><span class="sxs-lookup"><span data-stu-id="80ff4-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="80ff4-112">Odwołania do zestawów struktury</span><span class="sxs-lookup"><span data-stu-id="80ff4-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="80ff4-113">Dołączanie plików zestawów</span><span class="sxs-lookup"><span data-stu-id="80ff4-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="80ff4-114">Dołączanie plików zawartości</span><span class="sxs-lookup"><span data-stu-id="80ff4-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="80ff4-115">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="80ff4-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="80ff4-116">Zgodność typu projektu</span><span class="sxs-lookup"><span data-stu-id="80ff4-116">Project type compatibility</span></span>

- <span data-ttu-id="80ff4-117">Używany `.nuspec` z programem `nuget.exe pack` dla projektów typu non-SDK, które używają `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="80ff4-118">`.nuspec`Plik nie jest wymagany do tworzenia pakietów dla [projektów w stylu zestawu SDK](../resources/check-project-format.md) (zazwyczaj platformy .net core i .NET Standard projektów, które używają [atrybutu SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="80ff4-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="80ff4-119">(Należy pamiętać, że `.nuspec` jest generowany podczas tworzenia pakietu).</span><span class="sxs-lookup"><span data-stu-id="80ff4-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="80ff4-120">Jeśli tworzysz pakiet przy użyciu programu `dotnet.exe pack` lub `msbuild pack target` , zalecamy [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="80ff4-121">Można jednak wybrać opcję [użycia `.nuspec` pliku do spakowania przy użyciu `dotnet.exe` lub `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="80ff4-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="80ff4-122">W przypadku projektów migrowanych z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md) `.nuspec` plik nie jest wymagany do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="80ff4-123">Zamiast tego należy użyć [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="80ff4-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="80ff4-124">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="80ff4-124">General form and schema</span></span>

<span data-ttu-id="80ff4-125">Bieżący `nuspec.xsd` plik schematu znajduje się w [repozytorium GitHub usługi NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="80ff4-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="80ff4-126">W tym schemacie `.nuspec` plik ma następującą formę ogólną:</span><span class="sxs-lookup"><span data-stu-id="80ff4-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="80ff4-127">Aby wyczyścić wizualną reprezentację schematu, Otwórz plik schematu w programie Visual Studio w trybie projektowania i kliknij link **Eksplorator schematu XML** .</span><span class="sxs-lookup"><span data-stu-id="80ff4-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="80ff4-128">Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze, a następnie wybierz polecenie **Pokaż Eksplorator schematu XML**.</span><span class="sxs-lookup"><span data-stu-id="80ff4-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="80ff4-129">W dowolnym momencie możesz wyświetlić widok podobny do przedstawionego poniżej (w większości rozwiniętych):</span><span class="sxs-lookup"><span data-stu-id="80ff4-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Eksplorator schematu programu Visual Studio z otwartym nuspec. xsd](media/SchemaExplorer.png)

<span data-ttu-id="80ff4-131">Wszystkie nazwy elementów XML w pliku nuspec są rozróżniane wielkości liter, podobnie jak w przypadku XML.</span><span class="sxs-lookup"><span data-stu-id="80ff4-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="80ff4-132">Na przykład użycie elementu Metadata `<description>` jest poprawne i `<Description>` nie jest poprawne.</span><span class="sxs-lookup"><span data-stu-id="80ff4-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="80ff4-133">Poniższa Nazwa każdego elementu jest opisana poniżej.</span><span class="sxs-lookup"><span data-stu-id="80ff4-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="80ff4-134">Wymagane elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="80ff4-134">Required metadata elements</span></span>

<span data-ttu-id="80ff4-135">Mimo że następujące elementy są minimalnymi wymaganiami dotyczącymi pakietu, należy rozważyć dodanie [opcjonalnych elementów metadanych](#optional-metadata-elements) w celu poprawienia ogólnych doświadczeń deweloperów korzystających z Twojego pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="80ff4-136">Te elementy muszą znajdować się w obrębie `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="80ff4-137">identyfikator</span><span class="sxs-lookup"><span data-stu-id="80ff4-137">id</span></span> 
<span data-ttu-id="80ff4-138">Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowy w obrębie nuget.org lub dowolnej galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="80ff4-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="80ff4-139">Identyfikatory nie mogą zawierać spacji ani znaków, które są nieprawidłowe dla adresu URL, i ogólnie przestrzegają reguł przestrzeni nazw platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="80ff4-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="80ff4-140">Aby uzyskać wskazówki [, zobacz Wybieranie unikatowego identyfikatora pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="80ff4-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="80ff4-141">Podczas przekazywania pakietu do nuget.org, `id` pole jest ograniczone do 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="80ff4-142">version</span><span class="sxs-lookup"><span data-stu-id="80ff4-142">version</span></span>
<span data-ttu-id="80ff4-143">Wersja pakietu, po wzorcu *główna. pomocnicza. poprawka* .</span><span class="sxs-lookup"><span data-stu-id="80ff4-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="80ff4-144">Numery wersji mogą zawierać sufiks wstępnej wersji, zgodnie z opisem w temacie [wersja pakietu](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="80ff4-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="80ff4-145">Podczas przekazywania pakietu do nuget.org, `version` pole jest ograniczone do 64 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="80ff4-146">description (opis)</span><span class="sxs-lookup"><span data-stu-id="80ff4-146">description</span></span>
<span data-ttu-id="80ff4-147">Opis pakietu na potrzeby wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80ff4-147">A description of the package for UI display.</span></span>

<span data-ttu-id="80ff4-148">Podczas przekazywania pakietu do nuget.org, `description` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="80ff4-149">autorów</span><span class="sxs-lookup"><span data-stu-id="80ff4-149">authors</span></span>
<span data-ttu-id="80ff4-150">Rozdzielana przecinkami lista autorów pakietów, które pasują do nazw profilów w nuget.org. Są one wyświetlane w galerii NuGet w witrynie nuget.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="80ff4-151">Podczas przekazywania pakietu do nuget.org, `authors` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="80ff4-152">Opcjonalne elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="80ff4-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="80ff4-153">rzecz</span><span class="sxs-lookup"><span data-stu-id="80ff4-153">owners</span></span>
<span data-ttu-id="80ff4-154">Rozdzielana przecinkami lista twórców pakietów korzystających z nazw profilów w nuget.org. Jest to często taka sama lista jak w programie `authors` i jest ignorowana podczas przekazywania pakietu do NuGet.org. Zobacz [Zarządzanie właścicielami pakietów w witrynie NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="80ff4-154">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="80ff4-155">projectUrl</span><span class="sxs-lookup"><span data-stu-id="80ff4-155">projectUrl</span></span>
<span data-ttu-id="80ff4-156">Adres URL strony głównej pakietu, często wyświetlany w interfejsie użytkownika, a także nuget.org.</span><span class="sxs-lookup"><span data-stu-id="80ff4-156">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="80ff4-157">Podczas przekazywania pakietu do nuget.org, `projectUrl` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-157">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="80ff4-158">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="80ff4-158">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="80ff4-159">licenseUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="80ff4-159">licenseUrl is deprecated.</span></span> <span data-ttu-id="80ff4-160">Zamiast tego użyj licencji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-160">Use license instead.</span></span>

<span data-ttu-id="80ff4-161">Adres URL licencji pakietu, często przedstawiony w interfejsów użytkownika, na przykład nuget.org.</span><span class="sxs-lookup"><span data-stu-id="80ff4-161">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="80ff4-162">Podczas przekazywania pakietu do nuget.org, `licenseUrl` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-162">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="80ff4-163">license (licencja)</span><span class="sxs-lookup"><span data-stu-id="80ff4-163">license</span></span>

<span data-ttu-id="80ff4-164">*Obsługiwane przez **4.9.0 NuGet** i nowsze*</span><span class="sxs-lookup"><span data-stu-id="80ff4-164">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="80ff4-165">Wyrażenie licencji SPDX lub ścieżka do pliku licencji w pakiecie, często pokazywane w interfejsów użytkownika, jak nuget.org. Jeśli pakiet jest licencjonowany w ramach wspólnej licencji, takiej jak MIT lub BSD-2-klauzule, należy użyć skojarzonego [identyfikatora licencji SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="80ff4-165">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="80ff4-166">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="80ff4-166">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="80ff4-167">NuGet.org akceptuje tylko wyrażenia licencyjne zatwierdzone przez inicjatywę Open Source lub bezpłatną program Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="80ff4-167">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="80ff4-168">Jeśli pakiet jest licencjonowany w ramach wielu popularnych licencji, możesz określić licencję złożoną przy użyciu [składni wyrażenia SPDX w wersji 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="80ff4-168">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="80ff4-169">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="80ff4-169">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="80ff4-170">Jeśli używasz niestandardowej licencji, która nie jest obsługiwana przez wyrażenia licencji, możesz spakować `.txt` `.md` plik lub z tekstem licencji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-170">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="80ff4-171">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="80ff4-171">For example:</span></span>

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

<span data-ttu-id="80ff4-172">Aby uzyskać odpowiedniki programu MSBuild, zapoznaj się z tematem [pakowanie wyrażenia licencji lub pliku licencji](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="80ff4-172">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="80ff4-173">Dokładna składnia wyrażeń licencji narzędzia NuGet została opisana poniżej w [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="80ff4-173">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="80ff4-174">iconUrl</span><span class="sxs-lookup"><span data-stu-id="80ff4-174">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="80ff4-175">iconUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="80ff4-175">iconUrl is deprecated.</span></span> <span data-ttu-id="80ff4-176">Zamiast tego użyj ikony.</span><span class="sxs-lookup"><span data-stu-id="80ff4-176">Use icon instead.</span></span>

<span data-ttu-id="80ff4-177">Adres URL obrazu 128 x 128 z przezroczystym tłem, który będzie używany jako ikona pakietu w wyświetlanym interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80ff4-177">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="80ff4-178">Upewnij się, że ten element zawiera *adres URL obrazu bezpośredniego* , a nie adres URL strony sieci Web zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="80ff4-178">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="80ff4-179">Na przykład, aby użyć obrazu z usługi GitHub, użyj adresu URL nieprzetworzonego pliku, takiego jak <em> https://github.com/ \<username\> / \<repository\> /RAW/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="80ff4-179">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
<span data-ttu-id="80ff4-180">Podczas przekazywania pakietu do nuget.org, `iconUrl` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-180">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="80ff4-181">ikona</span><span class="sxs-lookup"><span data-stu-id="80ff4-181">icon</span></span>

<span data-ttu-id="80ff4-182">*Obsługiwane przez **5.3.0 NuGet** i nowsze*</span><span class="sxs-lookup"><span data-stu-id="80ff4-182">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="80ff4-183">Jest to ścieżka do pliku obrazu w pakiecie, często pokazana w interfejsów użytkownika, jak nuget.org jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-183">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="80ff4-184">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="80ff4-184">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="80ff4-185">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="80ff4-185">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="80ff4-186">Zalecamy rozdzielczość obrazu 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="80ff4-186">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="80ff4-187">Można na przykład dodać następujący element do nuspec podczas tworzenia pakietu przy użyciu nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="80ff4-187">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="80ff4-188">Przykład nuspec ikony pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-188">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="80ff4-189">W przypadku odpowiedników programu MSBuild zapoznaj się z [opakowaniem pliku obrazu ikony](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="80ff4-189">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="80ff4-190">Można określić zarówno `icon` , jak i `iconUrl` zachować zgodność z poprzednimi wersjami ze źródłami, które nie są obsługiwane `icon` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-190">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="80ff4-191">Program Visual Studio będzie obsługiwał `icon` pakiety pochodzące ze źródła opartego na folderach w przyszłej wersji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-191">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="80ff4-192">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="80ff4-192">requireLicenseAcceptance</span></span>
<span data-ttu-id="80ff4-193">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-193">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="80ff4-194">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="80ff4-194">developmentDependency</span></span>
<span data-ttu-id="80ff4-195">*(2.8 +)* Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do programowania, który uniemożliwia dołączenie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="80ff4-195">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="80ff4-196">W przypadku PackageReference (NuGet 4.8 +) Ta flaga oznacza również, że wykluczają się zasoby czasu kompilacji z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-196">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="80ff4-197">Zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="80ff4-197">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="80ff4-198">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="80ff4-198">summary</span></span>
> [!Important]
> <span data-ttu-id="80ff4-199">`summary` jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="80ff4-199">`summary` is being deprecated.</span></span> <span data-ttu-id="80ff4-200">Zamiast tego użyj polecenia cmdlet `description`.</span><span class="sxs-lookup"><span data-stu-id="80ff4-200">Use `description` instead.</span></span>

<span data-ttu-id="80ff4-201">Krótki opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80ff4-201">A short description of the package for UI display.</span></span> <span data-ttu-id="80ff4-202">W przypadku pominięcia `description` zostanie użyta obcięta wersja.</span><span class="sxs-lookup"><span data-stu-id="80ff4-202">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="80ff4-203">Podczas przekazywania pakietu do nuget.org, `summary` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-203">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="80ff4-204">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="80ff4-204">releaseNotes</span></span>
<span data-ttu-id="80ff4-205">*(1,5 +)* Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak karta **aktualizacje** w Menedżerze pakietów programu Visual Studio zamiast opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-205">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="80ff4-206">Podczas przekazywania pakietu do nuget.org, `releaseNotes` pole jest ograniczone do 35 000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-206">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="80ff4-207">informacji o prawach autorskich,</span><span class="sxs-lookup"><span data-stu-id="80ff4-207">copyright</span></span>
<span data-ttu-id="80ff4-208">*(1,5 +)* Szczegóły dotyczące praw autorskich pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-208">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="80ff4-209">Podczas przekazywania pakietu do nuget.org, `copyright` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-209">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="80ff4-210">language</span><span class="sxs-lookup"><span data-stu-id="80ff4-210">language</span></span>
<span data-ttu-id="80ff4-211">Identyfikator ustawień regionalnych dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-211">The locale ID for the package.</span></span> <span data-ttu-id="80ff4-212">Zobacz [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="80ff4-212">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="80ff4-213">tags</span><span class="sxs-lookup"><span data-stu-id="80ff4-213">tags</span></span>
<span data-ttu-id="80ff4-214">Rozdzielana spacjami Lista tagów i słów kluczowych, które opisują pakiet i ułatwiają odnajdywanie pakietów przez wyszukiwanie i filtrowanie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-214">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="80ff4-215">Podczas przekazywania pakietu do nuget.org, `tags` pole jest ograniczone do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-215">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="80ff4-216">Obsługa</span><span class="sxs-lookup"><span data-stu-id="80ff4-216">serviceable</span></span> 
<span data-ttu-id="80ff4-217">*(3.3 +)* Tylko do użytku wewnętrznego narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="80ff4-217">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="80ff4-218">repozytorium</span><span class="sxs-lookup"><span data-stu-id="80ff4-218">repository</span></span>
<span data-ttu-id="80ff4-219">Metadane repozytorium zawierające cztery opcjonalne atrybuty: `type` i `url` *(4.0 +)* i `branch` i `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="80ff4-219">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="80ff4-220">Te atrybuty umożliwiają mapowanie `.nupkg` do repozytorium, które zostało przez niego skompilowane, z możliwością uzyskania tak szczegółowej nazwy gałęzi i/lub zatwierdzenia skrótu SHA-1, który skompilowano pakiet.</span><span class="sxs-lookup"><span data-stu-id="80ff4-220">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="80ff4-221">Powinien to być publicznie dostępny adres URL, który może być wywoływany bezpośrednio przez oprogramowanie kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-221">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="80ff4-222">Nie powinna być stroną HTML, ponieważ jest ona przeznaczona dla komputera.</span><span class="sxs-lookup"><span data-stu-id="80ff4-222">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="80ff4-223">W przypadku łączenia ze stroną projektu `projectUrl` zamiast tego użyj pola.</span><span class="sxs-lookup"><span data-stu-id="80ff4-223">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="80ff4-224">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="80ff4-224">For example:</span></span>
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

<span data-ttu-id="80ff4-225">Podczas przekazywania pakietu do nuget.org, `type` atrybut jest ograniczony do 100 znaków, a `url` atrybut jest ograniczony do 4000 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-225">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="80ff4-226">tytuł</span><span class="sxs-lookup"><span data-stu-id="80ff4-226">title</span></span>
<span data-ttu-id="80ff4-227">Przyjazny dla człowieka tytuł pakietu, który może być używany w niektórych interfejsach użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80ff4-227">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="80ff4-228">(nuget.org i Menedżer pakietów w programie Visual Studio nie wyświetla tytułu)</span><span class="sxs-lookup"><span data-stu-id="80ff4-228">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="80ff4-229">Podczas przekazywania pakietu do nuget.org, `title` pole jest ograniczone do 256 znaków, ale nie jest używane do żadnych celów wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="80ff4-229">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="80ff4-230">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="80ff4-230">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="80ff4-231">packageTypes</span><span class="sxs-lookup"><span data-stu-id="80ff4-231">packageTypes</span></span>
<span data-ttu-id="80ff4-232">*(3.5 +)* Kolekcja elementów o zerowym lub większej liczbie `<packageType>` określająca typ pakietu, jeśli jest inny niż tradycyjny pakiet zależności.</span><span class="sxs-lookup"><span data-stu-id="80ff4-232">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="80ff4-233">Każdy pakiet PackageType ma atrybuty *nazwy* i *wersji*.</span><span class="sxs-lookup"><span data-stu-id="80ff4-233">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="80ff4-234">Zobacz [Ustawianie typu pakietu](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="80ff4-234">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="80ff4-235">zależności</span><span class="sxs-lookup"><span data-stu-id="80ff4-235">dependencies</span></span>
<span data-ttu-id="80ff4-236">Kolekcja elementów co najmniej zero `<dependency>` określających zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-236">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="80ff4-237">Każda zależność ma atrybuty *identyfikatora*, *wersji*, *include* (3. x +) i *exclude* (3. x +).</span><span class="sxs-lookup"><span data-stu-id="80ff4-237">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="80ff4-238">Zobacz [zależności](#dependencies-element) poniżej.</span><span class="sxs-lookup"><span data-stu-id="80ff4-238">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="80ff4-239">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="80ff4-239">frameworkAssemblies</span></span>
<span data-ttu-id="80ff4-240">*(1.2 +)* Kolekcja zawierająca zero lub więcej `<frameworkAssembly>` elementów .NET Framework identyfikujących odwołania do zestawów, które są wymagane przez ten pakiet, co zapewnia, że odwołania są dodawane do projektów zużywających pakiet.</span><span class="sxs-lookup"><span data-stu-id="80ff4-240">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="80ff4-241">Każdy frameworkAssembly ma atrybuty *AssemblyName* i *TargetFramework* .</span><span class="sxs-lookup"><span data-stu-id="80ff4-241">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="80ff4-242">Zobacz [Określanie zestawu Framework odwołuje się do poniższej pamięci podręcznej](#specifying-framework-assembly-references-gac) .</span><span class="sxs-lookup"><span data-stu-id="80ff4-242">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="80ff4-243">odwołania</span><span class="sxs-lookup"><span data-stu-id="80ff4-243">references</span></span>
<span data-ttu-id="80ff4-244">*(1,5 +)* Kolekcja `<reference>` elementów w `lib` folderze pakietu, które są dodawane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-244">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="80ff4-245">Każde odwołanie ma atrybut *pliku* .</span><span class="sxs-lookup"><span data-stu-id="80ff4-245">Each reference has a *file* attribute.</span></span> <span data-ttu-id="80ff4-246">`<references>` może również zawierać `<group>` element z atrybutem *TargetFramework* , który zawiera `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="80ff4-246">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="80ff4-247">W przypadku pominięcia `lib` zostaną uwzględnione wszystkie odwołania.</span><span class="sxs-lookup"><span data-stu-id="80ff4-247">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="80ff4-248">Zobacz [Określanie jawnych odwołań do zestawów](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="80ff4-248">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="80ff4-249">contentFiles</span><span class="sxs-lookup"><span data-stu-id="80ff4-249">contentFiles</span></span>
<span data-ttu-id="80ff4-250">*(3.3 +)* Kolekcja `<files>` elementów, które identyfikują pliki zawartości do uwzględnienia w projekcie zużywanym.</span><span class="sxs-lookup"><span data-stu-id="80ff4-250">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="80ff4-251">Te pliki są określone za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-251">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="80ff4-252">Zobacz sekcję [określanie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej.</span><span class="sxs-lookup"><span data-stu-id="80ff4-252">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="80ff4-253">files</span><span class="sxs-lookup"><span data-stu-id="80ff4-253">files</span></span> 
<span data-ttu-id="80ff4-254">`<package>`Węzeł może zawierać `<files>` węzeł jako element równorzędny i element `<metadata>` `<contentFiles>` podrzędny w programie `<metadata>` , aby określić, które pliki zestawu i zawartości mają być zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-254">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="80ff4-255">Szczegółowe informacje znajdują się w temacie [zawierającym pliki zestawu](#including-assembly-files) i [pliki zawartości](#including-content-files) w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-255">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="80ff4-256">atrybuty metadanych</span><span class="sxs-lookup"><span data-stu-id="80ff4-256">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="80ff4-257">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="80ff4-257">minClientVersion</span></span>
<span data-ttu-id="80ff4-258">Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszony przez nuget.exe i Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80ff4-258">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="80ff4-259">Jest on używany zawsze, gdy pakiet jest zależny od określonych funkcji `.nuspec` pliku, które zostały dodane w określonej wersji klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="80ff4-259">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="80ff4-260">Na przykład pakiet używający `developmentDependency` atrybutu powinien określać wartość "2,8" dla `minClientVersion` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-260">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="80ff4-261">Podobnie pakiet używający `contentFiles` elementu (patrz następna sekcja) powinien mieć ustawioną wartość `minClientVersion` "3,3".</span><span class="sxs-lookup"><span data-stu-id="80ff4-261">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="80ff4-262">Należy zauważyć, że ponieważ klienci NuGet przed 2,5 nie rozpoznają tej flagi, *zawsze* odmówią instalacji pakietu bez względu na to, co `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="80ff4-262">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="80ff4-263">Tokeny zastępcze</span><span class="sxs-lookup"><span data-stu-id="80ff4-263">Replacement tokens</span></span>

<span data-ttu-id="80ff4-264">Podczas tworzenia pakietu [ `nuget pack` polecenie](../reference/cli-reference/cli-ref-pack.md) zastępuje tokeny $-Limited w `.nuspec` `<metadata>` węźle pliku wartościami, które pochodzą z pliku projektu lub `pack` `-properties` przełącznika polecenia.</span><span class="sxs-lookup"><span data-stu-id="80ff4-264">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="80ff4-265">W wierszu polecenia należy określić wartości tokenu przy użyciu `nuget pack -properties <name>=<value>;<name>=<value>` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-265">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="80ff4-266">Na przykład można użyć tokenu, takiego jak `$owners$` i `$desc$` w `.nuspec` i podać wartości w czasie pakowania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="80ff4-266">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="80ff4-267">Aby użyć wartości z projektu, należy określić tokeny opisane w poniższej tabeli (AssemblyInfo odnosi się do pliku, na przykład `Properties` `AssemblyInfo.cs` lub `AssemblyInfo.vb` ).</span><span class="sxs-lookup"><span data-stu-id="80ff4-267">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="80ff4-268">Aby użyć tych tokenów, uruchom polecenie `nuget pack` z plikiem projektu, a nie tylko `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-268">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="80ff4-269">Na przykład podczas korzystania z następującego polecenia `$id$` `$version$` tokeny i w `.nuspec` pliku są zastępowane `AssemblyName` i `AssemblyVersion` wartościami projektu:</span><span class="sxs-lookup"><span data-stu-id="80ff4-269">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="80ff4-270">Zazwyczaj w przypadku projektu można utworzyć `.nuspec` początkowo przy użyciu, `nuget spec MyProject.csproj` który automatycznie zawiera niektóre z tych standardowych tokenów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-270">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="80ff4-271">Jeśli jednak projekt nie zawiera wartości wymaganych `.nuspec` elementów, `nuget pack` kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="80ff4-271">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="80ff4-272">Ponadto jeśli zmienisz wartości projektu, pamiętaj, aby ponownie skompilować przed utworzeniem pakietu; można to zrobić przy użyciu przełącznika polecenia pakietu `build` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-272">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="80ff4-273">Z wyjątkiem `$configuration$` wartości w projekcie są używane w preferencjach do wszystkich przypisanych do tego samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="80ff4-273">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="80ff4-274">Token</span><span class="sxs-lookup"><span data-stu-id="80ff4-274">Token</span></span> | <span data-ttu-id="80ff4-275">Źródło wartości</span><span class="sxs-lookup"><span data-stu-id="80ff4-275">Value source</span></span> | <span data-ttu-id="80ff4-276">Wartość</span><span class="sxs-lookup"><span data-stu-id="80ff4-276">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="80ff4-277">**$id $**</span><span class="sxs-lookup"><span data-stu-id="80ff4-277">**$id$**</span></span> | <span data-ttu-id="80ff4-278">Plik projektu</span><span class="sxs-lookup"><span data-stu-id="80ff4-278">Project file</span></span> | <span data-ttu-id="80ff4-279">AssemblyName (title) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="80ff4-279">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="80ff4-280">**$version $**</span><span class="sxs-lookup"><span data-stu-id="80ff4-280">**$version$**</span></span> | <span data-ttu-id="80ff4-281">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="80ff4-281">AssemblyInfo</span></span> | <span data-ttu-id="80ff4-282">AssemblyInformationalVersion, jeśli jest obecny, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="80ff4-282">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="80ff4-283">**$author $**</span><span class="sxs-lookup"><span data-stu-id="80ff4-283">**$author$**</span></span> | <span data-ttu-id="80ff4-284">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="80ff4-284">AssemblyInfo</span></span> | <span data-ttu-id="80ff4-285">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="80ff4-285">AssemblyCompany</span></span> |
| <span data-ttu-id="80ff4-286">**$title $**</span><span class="sxs-lookup"><span data-stu-id="80ff4-286">**$title$**</span></span> | <span data-ttu-id="80ff4-287">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="80ff4-287">AssemblyInfo</span></span> | <span data-ttu-id="80ff4-288">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="80ff4-288">AssemblyTitle</span></span> |
| <span data-ttu-id="80ff4-289">**$description $**</span><span class="sxs-lookup"><span data-stu-id="80ff4-289">**$description$**</span></span> | <span data-ttu-id="80ff4-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="80ff4-290">AssemblyInfo</span></span> | <span data-ttu-id="80ff4-291">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="80ff4-291">AssemblyDescription</span></span> |
| <span data-ttu-id="80ff4-292">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="80ff4-292">**$copyright$**</span></span> | <span data-ttu-id="80ff4-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="80ff4-293">AssemblyInfo</span></span> | <span data-ttu-id="80ff4-294">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="80ff4-294">AssemblyCopyright</span></span> |
| <span data-ttu-id="80ff4-295">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="80ff4-295">**$configuration$**</span></span> | <span data-ttu-id="80ff4-296">Biblioteka DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="80ff4-296">Assembly DLL</span></span> | <span data-ttu-id="80ff4-297">Konfiguracja użyta do skompilowania zestawu, czyli domyślnego debugowania.</span><span class="sxs-lookup"><span data-stu-id="80ff4-297">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="80ff4-298">Należy pamiętać, że aby utworzyć pakiet przy użyciu konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="80ff4-298">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="80ff4-299">Tokeny mogą być również używane do rozpoznawania ścieżek podczas dołączania [plików zestawu](#including-assembly-files) i [plików zawartości](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="80ff4-299">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="80ff4-300">Tokeny mają takie same nazwy jak właściwości programu MSBuild, dzięki czemu można wybrać pliki do uwzględnienia w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-300">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="80ff4-301">Jeśli na przykład w pliku są używane następujące tokeny `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="80ff4-301">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="80ff4-302">Po utworzeniu zestawu `AssemblyName` , którego konfiguracja jest `LoggingLibrary` `Release` w programie MSBuild, wyniki wierszy w `.nuspec` pliku w pakiecie są następujące:</span><span class="sxs-lookup"><span data-stu-id="80ff4-302">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="80ff4-303">Element zależności</span><span class="sxs-lookup"><span data-stu-id="80ff4-303">Dependencies element</span></span>

<span data-ttu-id="80ff4-304">`<dependencies>`Element w obrębie `<metadata>` zawiera dowolną liczbę `<dependency>` elementów, które identyfikują inne pakiety, od których zależy pakiet najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-304">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="80ff4-305">Atrybuty dla każdej z nich `<dependency>` są następujące:</span><span class="sxs-lookup"><span data-stu-id="80ff4-305">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="80ff4-306">Atrybut</span><span class="sxs-lookup"><span data-stu-id="80ff4-306">Attribute</span></span> | <span data-ttu-id="80ff4-307">Opis</span><span class="sxs-lookup"><span data-stu-id="80ff4-307">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="80ff4-308">Potrzeb Identyfikator pakietu zależności, taki jak "EntityFramework" i "NUnit", czyli nazwa pakietu nuget.org wyświetlana na stronie pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-308">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="80ff4-309">Potrzeb Zakres wersji akceptowalnych jako zależność.</span><span class="sxs-lookup"><span data-stu-id="80ff4-309">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="80ff4-310">Aby uzyskać dokładną składnię, zobacz [wersja pakietu](../concepts/package-versioning.md#version-ranges) .</span><span class="sxs-lookup"><span data-stu-id="80ff4-310">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="80ff4-311">Wersje zmiennoprzecinkowe nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="80ff4-311">Floating versions are not supported.</span></span> |
| <span data-ttu-id="80ff4-312">include</span><span class="sxs-lookup"><span data-stu-id="80ff4-312">include</span></span> | <span data-ttu-id="80ff4-313">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazujących zależność do uwzględnienia w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="80ff4-313">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="80ff4-314">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="80ff4-314">The default value is `all`.</span></span> |
| <span data-ttu-id="80ff4-315">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="80ff4-315">exclude</span></span> | <span data-ttu-id="80ff4-316">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazujących zależność do wykluczenia w końcowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-316">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="80ff4-317">Wartość domyślna to `build,analyzers` , że można ją wypisać.</span><span class="sxs-lookup"><span data-stu-id="80ff4-317">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="80ff4-318">Ale `content/ ContentFiles` są również niejawnie wykluczone w pakiecie końcowym, który nie może być nadpisany.</span><span class="sxs-lookup"><span data-stu-id="80ff4-318">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="80ff4-319">Tagi określone za pomocą `exclude` mają pierwszeństwo przed tymi określonymi przy użyciu `include` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-319">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="80ff4-320">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-320">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="80ff4-321">Podczas przekazywania pakietu do nuget.org, każdy `id` atrybut zależności jest ograniczony do 128 znaków, a `version` atrybut jest ograniczony do 256 znaków.</span><span class="sxs-lookup"><span data-stu-id="80ff4-321">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="80ff4-322">Include/Exclude — tag</span><span class="sxs-lookup"><span data-stu-id="80ff4-322">Include/Exclude tag</span></span> | <span data-ttu-id="80ff4-323">Zmodyfikowane foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="80ff4-323">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="80ff4-324">contentFiles</span><span class="sxs-lookup"><span data-stu-id="80ff4-324">contentFiles</span></span> | <span data-ttu-id="80ff4-325">Zawartość</span><span class="sxs-lookup"><span data-stu-id="80ff4-325">Content</span></span> |
| <span data-ttu-id="80ff4-326">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="80ff4-326">runtime</span></span> | <span data-ttu-id="80ff4-327">Środowisko uruchomieniowe, zasoby i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="80ff4-327">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="80ff4-328">kompilowanie</span><span class="sxs-lookup"><span data-stu-id="80ff4-328">compile</span></span> | <span data-ttu-id="80ff4-329">lib</span><span class="sxs-lookup"><span data-stu-id="80ff4-329">lib</span></span> |
| <span data-ttu-id="80ff4-330">kompilacja</span><span class="sxs-lookup"><span data-stu-id="80ff4-330">build</span></span> | <span data-ttu-id="80ff4-331">Kompilacja (właściwości i elementy docelowe programu MSBuild)</span><span class="sxs-lookup"><span data-stu-id="80ff4-331">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="80ff4-332">natywne</span><span class="sxs-lookup"><span data-stu-id="80ff4-332">native</span></span> | <span data-ttu-id="80ff4-333">natywne</span><span class="sxs-lookup"><span data-stu-id="80ff4-333">native</span></span> |
| <span data-ttu-id="80ff4-334">brak</span><span class="sxs-lookup"><span data-stu-id="80ff4-334">none</span></span> | <span data-ttu-id="80ff4-335">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="80ff4-335">No folders</span></span> |
| <span data-ttu-id="80ff4-336">all</span><span class="sxs-lookup"><span data-stu-id="80ff4-336">all</span></span> | <span data-ttu-id="80ff4-337">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="80ff4-337">All folders</span></span> |

<span data-ttu-id="80ff4-338">Na przykład następujące wiersze wskazują zależności w `PackageA` wersji 1.1.0 lub nowszej, a `PackageB` wersja 1. x.</span><span class="sxs-lookup"><span data-stu-id="80ff4-338">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="80ff4-339">Poniższe wiersze wskazują zależności dotyczące tych samych pakietów, ale określają, że mają być dostępne foldery i i `contentFiles` `build` wszystkie z nich, `PackageA` ale `native` `compile` Foldery `PackageB` "</span><span class="sxs-lookup"><span data-stu-id="80ff4-339">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="80ff4-340">Podczas tworzenia `.nuspec` z projektu przy użyciu `nuget spec` , zależności, które istnieją w tym projekcie, nie są automatycznie dołączane do `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="80ff4-340">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="80ff4-341">Zamiast tego należy użyć `nuget pack myproject.csproj` i pobrać plik *. nuspec* z wygenerowanego pliku *NUPKG* .</span><span class="sxs-lookup"><span data-stu-id="80ff4-341">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="80ff4-342">This *. nuspec* zawiera zależności.</span><span class="sxs-lookup"><span data-stu-id="80ff4-342">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="80ff4-343">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="80ff4-343">Dependency groups</span></span>

<span data-ttu-id="80ff4-344">*Wersja 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="80ff4-344">*Version 2.0+*</span></span>

<span data-ttu-id="80ff4-345">Jako alternatywę dla pojedynczej płaskiej listy, zależności można określić zgodnie z profilem struktury projektu docelowego za pomocą `<group>` elementów w `<dependencies>` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-345">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="80ff4-346">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-346">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="80ff4-347">Te zależności są instalowane razem, gdy struktura docelowa jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-347">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="80ff4-348">`<group>`Element bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista zależności.</span><span class="sxs-lookup"><span data-stu-id="80ff4-348">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="80ff4-349">Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.</span><span class="sxs-lookup"><span data-stu-id="80ff4-349">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="80ff4-350">Format grupy nie może być mieszany z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="80ff4-350">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="80ff4-351">Format [monikera platformy docelowej (TFM)](../reference/target-frameworks.md) używany w `lib/ref` folderze jest inny w porównaniu z TFM używanym w `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-351">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="80ff4-352">Jeśli Platformy docelowe zadeklarowane w `dependencies group` `lib/ref` folderze i `.nuspec` pliku nie mają dokładnych odpowiedników, `pack` polecenie spowoduje [wygenerowanie ostrzeżenia NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="80ff4-352">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="80ff4-353">W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="80ff4-353">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="80ff4-354">Jawne odwołania do zestawów</span><span class="sxs-lookup"><span data-stu-id="80ff4-354">Explicit assembly references</span></span>

<span data-ttu-id="80ff4-355">`<references>`Element jest używany przez projekty `packages.config` , aby jawnie określić zestawy, do których projekt docelowy powinien odwoływać się przy użyciu pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-355">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="80ff4-356">Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="80ff4-356">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="80ff4-357">Aby uzyskać więcej informacji, zobacz stronę [wybierania zestawów, do których odwołują się projekty](../create-packages/select-assemblies-referenced-by-projects.md) , aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-357">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="80ff4-358">Na przykład poniższy `<references>` element instruuje pakiet NuGet, aby dodać odwołania do tylko `xunit.dll` , a `xunit.extensions.dll` nawet wtedy, gdy w pakiecie istnieją dodatkowe zestawy:</span><span class="sxs-lookup"><span data-stu-id="80ff4-358">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="80ff4-359">Grupy odwołań</span><span class="sxs-lookup"><span data-stu-id="80ff4-359">Reference groups</span></span>

<span data-ttu-id="80ff4-360">Jako alternatywę dla pojedynczej płaskiej listy, odwołania można określić zgodnie z profilem struktury projektu docelowego za pomocą `<group>` elementów w `<references>` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-360">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="80ff4-361">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-361">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="80ff4-362">Te odwołania są dodawane do projektu, gdy struktura docelowa jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-362">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="80ff4-363">`<group>`Element bez `targetFramework` atrybutu jest używany jako domyślna lub rezerwowa lista odwołań.</span><span class="sxs-lookup"><span data-stu-id="80ff4-363">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="80ff4-364">Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.</span><span class="sxs-lookup"><span data-stu-id="80ff4-364">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="80ff4-365">Format grupy nie może być mieszany z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="80ff4-365">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="80ff4-366">W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="80ff4-366">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="80ff4-367">Odwołania do zestawów struktury</span><span class="sxs-lookup"><span data-stu-id="80ff4-367">Framework assembly references</span></span>

<span data-ttu-id="80ff4-368">Zestawy struktur są tymi, które są częścią programu .NET Framework i powinny już znajdować się w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej maszyny.</span><span class="sxs-lookup"><span data-stu-id="80ff4-368">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="80ff4-369">Identyfikując te zestawy w obrębie `<frameworkAssemblies>` elementu, pakiet może zapewnić, że wymagane odwołania są dodawane do projektu w przypadku, gdy projekt nie ma już odwołań.</span><span class="sxs-lookup"><span data-stu-id="80ff4-369">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="80ff4-370">Takie zespoły nie są bezpośrednio zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-370">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="80ff4-371">`<frameworkAssemblies>`Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="80ff4-371">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="80ff4-372">Atrybut</span><span class="sxs-lookup"><span data-stu-id="80ff4-372">Attribute</span></span> | <span data-ttu-id="80ff4-373">Opis</span><span class="sxs-lookup"><span data-stu-id="80ff4-373">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80ff4-374">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="80ff4-374">**assemblyName**</span></span> | <span data-ttu-id="80ff4-375">Potrzeb W pełni kwalifikowana nazwa zestawu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-375">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="80ff4-376">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="80ff4-376">**targetFramework**</span></span> | <span data-ttu-id="80ff4-377">Obowiązkowe Określa platformę docelową, do której stosuje się to odwołanie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-377">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="80ff4-378">W przypadku pominięcia wskazuje, że odwołanie dotyczy wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="80ff4-378">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="80ff4-379">Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.</span><span class="sxs-lookup"><span data-stu-id="80ff4-379">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="80ff4-380">W poniższym przykładzie przedstawiono odwołanie do `System.Net` dla wszystkich platform docelowych i odwołania do `System.ServiceModel` tylko dla .NET Framework 4,0:</span><span class="sxs-lookup"><span data-stu-id="80ff4-380">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="80ff4-381">Dołączanie plików zestawów</span><span class="sxs-lookup"><span data-stu-id="80ff4-381">Including assembly files</span></span>

<span data-ttu-id="80ff4-382">Jeśli przestrzegasz Konwencji opisanych w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md), nie musisz jawnie określać listy plików w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="80ff4-382">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="80ff4-383">`nuget pack`Polecenie automatycznie pobiera niezbędne pliki.</span><span class="sxs-lookup"><span data-stu-id="80ff4-383">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="80ff4-384">Gdy pakiet jest instalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu do bibliotek DLL pakietu, *z wyjątkiem* tych, które są nazwane, `.resources.dll` ponieważ zakłada się, że są to zlokalizowane zespoły satelickie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-384">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="80ff4-385">Z tego powodu należy unikać używania `.resources.dll` dla plików, które w przeciwnym razie zawierają istotny kod pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-385">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="80ff4-386">Aby ominąć to automatyczne zachowanie i jawnie kontrolować, które pliki są zawarte w pakiecie, umieść `<files>` element jako obiekt podrzędny `<package>` (i element równorzędny `<metadata>` ), identyfikując każdy plik z oddzielnym `<file>` elementem.</span><span class="sxs-lookup"><span data-stu-id="80ff4-386">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="80ff4-387">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="80ff4-387">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="80ff4-388">W przypadku pakietów NuGet 2. x i starszych oraz projektów korzystających z programu `packages.config` `<files>` element jest również używany do uwzględniania niezmiennych plików zawartości podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-388">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="80ff4-389">W przypadku pakietów NuGet 3.3 + i projektów PackageReference, `<contentFiles>` element jest używany.</span><span class="sxs-lookup"><span data-stu-id="80ff4-389">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="80ff4-390">Aby uzyskać szczegółowe informacje, zobacz temat [uwzględnianie plików zawartości](#including-content-files) poniżej.</span><span class="sxs-lookup"><span data-stu-id="80ff4-390">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="80ff4-391">Atrybuty elementu pliku</span><span class="sxs-lookup"><span data-stu-id="80ff4-391">File element attributes</span></span>

<span data-ttu-id="80ff4-392">Każdy `<file>` element określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="80ff4-392">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="80ff4-393">Atrybut</span><span class="sxs-lookup"><span data-stu-id="80ff4-393">Attribute</span></span> | <span data-ttu-id="80ff4-394">Opis</span><span class="sxs-lookup"><span data-stu-id="80ff4-394">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80ff4-395">**src**</span><span class="sxs-lookup"><span data-stu-id="80ff4-395">**src**</span></span> | <span data-ttu-id="80ff4-396">Lokalizacja pliku lub plików do dołączenia, z uwzględnieniem wyjątków określonych przez `exclude` atrybut.</span><span class="sxs-lookup"><span data-stu-id="80ff4-396">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="80ff4-397">Ścieżka jest względna do `.nuspec` pliku, chyba że zostanie określona ścieżka bezwzględna.</span><span class="sxs-lookup"><span data-stu-id="80ff4-397">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="80ff4-398">Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-398">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="80ff4-399">**obiektów**</span><span class="sxs-lookup"><span data-stu-id="80ff4-399">**target**</span></span> | <span data-ttu-id="80ff4-400">Ścieżka względna do folderu w pakiecie, w którym znajdują się pliki źródłowe, które muszą zaczynać się od `lib` , `content` , `build` , lub `tools` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-400">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="80ff4-401">Zobacz [Tworzenie nuspec z katalogu roboczego opartego na Konwencji](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="80ff4-401">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="80ff4-402">**wykluczanie**</span><span class="sxs-lookup"><span data-stu-id="80ff4-402">**exclude**</span></span> | <span data-ttu-id="80ff4-403">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-403">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="80ff4-404">Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-404">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="80ff4-405">Przykłady</span><span class="sxs-lookup"><span data-stu-id="80ff4-405">Examples</span></span>

<span data-ttu-id="80ff4-406">**Pojedynczy zestaw**</span><span class="sxs-lookup"><span data-stu-id="80ff4-406">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="80ff4-407">**Pojedynczy zestaw specyficzny dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="80ff4-407">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="80ff4-408">**Zestaw bibliotek DLL przy użyciu symbolu wieloznacznego**</span><span class="sxs-lookup"><span data-stu-id="80ff4-408">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="80ff4-409">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="80ff4-409">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="80ff4-410">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="80ff4-410">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="80ff4-411">Dołączanie plików zawartości</span><span class="sxs-lookup"><span data-stu-id="80ff4-411">Including content files</span></span>

<span data-ttu-id="80ff4-412">Pliki zawartości to niezmienne pliki, których pakiet musi zawierać w projekcie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-412">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="80ff4-413">Są niezmienne, nie są przeznaczone do modyfikacji przez projekt zużywający.</span><span class="sxs-lookup"><span data-stu-id="80ff4-413">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="80ff4-414">Przykładowe pliki zawartości obejmują:</span><span class="sxs-lookup"><span data-stu-id="80ff4-414">Example content files include:</span></span>

- <span data-ttu-id="80ff4-415">Obrazy osadzone jako zasoby</span><span class="sxs-lookup"><span data-stu-id="80ff4-415">Images that are embedded as resources</span></span>
- <span data-ttu-id="80ff4-416">Pliki źródłowe, które zostały już skompilowane</span><span class="sxs-lookup"><span data-stu-id="80ff4-416">Source files that are already compiled</span></span>
- <span data-ttu-id="80ff4-417">Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="80ff4-417">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="80ff4-418">Pliki konfiguracji pakietu, które muszą być zawarte w projekcie, ale nie muszą mieć żadnych zmian specyficznych dla projektu</span><span class="sxs-lookup"><span data-stu-id="80ff4-418">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="80ff4-419">Pliki zawartości są zawarte w pakiecie przy użyciu `<files>` elementu, określając `content` folder w `target` atrybucie.</span><span class="sxs-lookup"><span data-stu-id="80ff4-419">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="80ff4-420">Jednak takie pliki są ignorowane, gdy pakiet zostanie zainstalowany w projekcie przy użyciu PackageReference, który zamiast tego używa `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-420">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="80ff4-421">Aby zapewnić maksymalną zgodność z zużywanymi projektami, pakiet najlepiej określa pliki zawartości w obu elementach.</span><span class="sxs-lookup"><span data-stu-id="80ff4-421">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="80ff4-422">Używanie elementu Files dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="80ff4-422">Using the files element for content files</span></span>

<span data-ttu-id="80ff4-423">W przypadku plików zawartości wystarczy użyć tego samego formatu co w przypadku plików zestawu, ale określić `content` jako folder podstawowy w `target` atrybucie, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="80ff4-423">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="80ff4-424">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="80ff4-424">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="80ff4-425">**Pliki zawartości z strukturą katalogów**</span><span class="sxs-lookup"><span data-stu-id="80ff4-425">**Content files with directory structure**</span></span>

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

<span data-ttu-id="80ff4-426">**Plik zawartości specyficzny dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="80ff4-426">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="80ff4-427">**Plik zawartości skopiowany do folderu z kropką w nazwie**</span><span class="sxs-lookup"><span data-stu-id="80ff4-427">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="80ff4-428">W takim przypadku pakiet NuGet uważa, że rozszerzenie w programie nie jest `target` zgodne z rozszerzeniem w `src` i w ten sposób traktuje tę część nazwy w `target` postaci folderu:</span><span class="sxs-lookup"><span data-stu-id="80ff4-428">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="80ff4-429">**Pliki zawartości bez rozszerzeń**</span><span class="sxs-lookup"><span data-stu-id="80ff4-429">**Content files without extensions**</span></span>

<span data-ttu-id="80ff4-430">Aby dołączyć pliki bez rozszerzenia, użyj `*` `**` symboli wieloznacznych lub:</span><span class="sxs-lookup"><span data-stu-id="80ff4-430">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="80ff4-431">**Pliki zawartości ze szczegółową ścieżką i głębokiego celu**</span><span class="sxs-lookup"><span data-stu-id="80ff4-431">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="80ff4-432">W tym przypadku, ponieważ rozszerzenia plików dla dopasowania źródłowego i docelowego, pakiet NuGet zakłada, że obiektem docelowym jest nazwa pliku, a nie folder:</span><span class="sxs-lookup"><span data-stu-id="80ff4-432">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="80ff4-433">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="80ff4-433">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="80ff4-434">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="80ff4-434">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="80ff4-435">Używanie elementu contentFiles dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="80ff4-435">Using the contentFiles element for content files</span></span>

<span data-ttu-id="80ff4-436">*Pakiet NuGet 4.0 + z PackageReference*</span><span class="sxs-lookup"><span data-stu-id="80ff4-436">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="80ff4-437">Domyślnie pakiet umieszcza zawartość w `contentFiles` folderze (patrz poniżej) i `nuget pack` uwzględnia wszystkie pliki w tym folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="80ff4-437">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="80ff4-438">W takim przypadku nie trzeba umieszczać `contentFiles` węzła w ogóle `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-438">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="80ff4-439">Aby kontrolować, które pliki są uwzględniane, `<contentFiles>` element Określa kolekcję `<files>` elementów, które identyfikują dokładne pliki include.</span><span class="sxs-lookup"><span data-stu-id="80ff4-439">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="80ff4-440">Te pliki są określone za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu:</span><span class="sxs-lookup"><span data-stu-id="80ff4-440">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="80ff4-441">Atrybut</span><span class="sxs-lookup"><span data-stu-id="80ff4-441">Attribute</span></span> | <span data-ttu-id="80ff4-442">Opis</span><span class="sxs-lookup"><span data-stu-id="80ff4-442">Description</span></span> |
| --- | --- |
| <span data-ttu-id="80ff4-443">**być**</span><span class="sxs-lookup"><span data-stu-id="80ff4-443">**include**</span></span> | <span data-ttu-id="80ff4-444">Potrzeb Lokalizacja pliku lub plików do dołączenia, z uwzględnieniem wyjątków określonych przez `exclude` atrybut.</span><span class="sxs-lookup"><span data-stu-id="80ff4-444">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="80ff4-445">Ścieżka jest `contentFiles` określana względem folderu, chyba że określona jest ścieżka bezwzględna.</span><span class="sxs-lookup"><span data-stu-id="80ff4-445">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="80ff4-446">Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-446">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="80ff4-447">**wykluczanie**</span><span class="sxs-lookup"><span data-stu-id="80ff4-447">**exclude**</span></span> | <span data-ttu-id="80ff4-448">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="80ff4-448">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="80ff4-449">Symbol wieloznaczny `*` jest dozwolony, a podwójne symbole wieloznaczne `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-449">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="80ff4-450">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="80ff4-450">**buildAction**</span></span> | <span data-ttu-id="80ff4-451">Akcja kompilacji, która ma zostać przypisana do elementu zawartości dla programu MSBuild, takich jak,,, `Content` `None` `Embedded Resource` `Compile` itd. Wartość domyślna to `Compile` .</span><span class="sxs-lookup"><span data-stu-id="80ff4-451">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="80ff4-452">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="80ff4-452">**copyToOutput**</span></span> | <span data-ttu-id="80ff4-453">Wartość logiczna wskazująca, czy elementy zawartości mają być kopiowane do folderu wyjściowego kompilacja (lub publikacja).</span><span class="sxs-lookup"><span data-stu-id="80ff4-453">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="80ff4-454">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="80ff4-454">The default is false.</span></span> |
| <span data-ttu-id="80ff4-455">**Flatten**</span><span class="sxs-lookup"><span data-stu-id="80ff4-455">**flatten**</span></span> | <span data-ttu-id="80ff4-456">Wartość logiczna wskazująca, czy kopiować elementy zawartości do pojedynczego folderu w danych wyjściowych kompilacji (true), czy też zachować strukturę folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="80ff4-456">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="80ff4-457">Ta flaga działa tylko wtedy, gdy flaga copyToOutput jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="80ff4-457">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="80ff4-458">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="80ff4-458">The default is false.</span></span> |

<span data-ttu-id="80ff4-459">Podczas instalacji pakietu NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-459">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="80ff4-460">Jeśli wiele wpisów pasuje do tego samego pliku, zostaną zastosowane wszystkie wpisy.</span><span class="sxs-lookup"><span data-stu-id="80ff4-460">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="80ff4-461">Wpis najwyższego poziomu zastępuje niższe wpisy w przypadku konfliktu dla tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-461">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="80ff4-462">Struktura folderu pakietu</span><span class="sxs-lookup"><span data-stu-id="80ff4-462">Package folder structure</span></span>

<span data-ttu-id="80ff4-463">Projekt pakietu powinien mieć strukturę zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="80ff4-463">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="80ff4-464">`codeLanguages` może być `cs` ,,, `vb` `fs` `any` lub małymi literami odpowiadającymi danej `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="80ff4-464">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="80ff4-465">`TxM` to dowolna docelowa moniker platformy docelowej, który obsługuje pakiet NuGet (patrz [Platformy docelowe](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="80ff4-465">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="80ff4-466">Wszystkie struktury folderów mogą być dołączane na końcu tej składni.</span><span class="sxs-lookup"><span data-stu-id="80ff4-466">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="80ff4-467">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="80ff4-467">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="80ff4-468">Za pomocą pustych folderów można `.` zrezygnować z udostępniania zawartości dla niektórych kombinacji języka i TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="80ff4-468">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="80ff4-469">Przykładowa sekcja contentFiles</span><span class="sxs-lookup"><span data-stu-id="80ff4-469">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="80ff4-470">Grupy odwołań platformy</span><span class="sxs-lookup"><span data-stu-id="80ff4-470">Framework reference groups</span></span>

<span data-ttu-id="80ff4-471">*Tylko wersja 5.1 + wih PackageReference*</span><span class="sxs-lookup"><span data-stu-id="80ff4-471">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="80ff4-472">Odwołania do platformy są koncepcjami platformy .NET Core reprezentującymi współdzielone platformy, takie jak WPF lub Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="80ff4-472">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="80ff4-473">Określając strukturę udostępnioną, pakiet gwarantuje, że wszystkie jej zależności struktury są zawarte w projekcie odwołującym.</span><span class="sxs-lookup"><span data-stu-id="80ff4-473">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="80ff4-474">Każdy `<group>` element wymaga `targetFramework` atrybutu i zero lub więcej `<frameworkReference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="80ff4-474">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="80ff4-475">W poniższym przykładzie przedstawiono nuspec wygenerowane dla projektu WPF platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="80ff4-475">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="80ff4-476">Należy zauważyć, że nie zaleca się tworzenia ręcznie nuspecs, które zawierają odwołania do struktury.</span><span class="sxs-lookup"><span data-stu-id="80ff4-476">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="80ff4-477">Rozważ użycie pakietu [Target](msbuild-targets.md) Pack, co spowoduje automatyczne wywnioskowanie ich z projektu.</span><span class="sxs-lookup"><span data-stu-id="80ff4-477">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="80ff4-478">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="80ff4-478">Example nuspec files</span></span>

<span data-ttu-id="80ff4-479">**Prosta `.nuspec` , która nie określa zależności ani plików**</span><span class="sxs-lookup"><span data-stu-id="80ff4-479">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="80ff4-480">**A `.nuspec` z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="80ff4-480">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="80ff4-481">**A `.nuspec` z plikami**</span><span class="sxs-lookup"><span data-stu-id="80ff4-481">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="80ff4-482">**`.nuspec`Z zestawami Framework**</span><span class="sxs-lookup"><span data-stu-id="80ff4-482">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="80ff4-483">W tym przykładzie są zainstalowane następujące elementy docelowe dla konkretnych projektów:</span><span class="sxs-lookup"><span data-stu-id="80ff4-483">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="80ff4-484">. NET4 > `System.Web` , `System.Net`</span><span class="sxs-lookup"><span data-stu-id="80ff4-484">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="80ff4-485">. Profil klienta NET4 — > `System.Net`</span><span class="sxs-lookup"><span data-stu-id="80ff4-485">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="80ff4-486">Silverlight 3 — > `System.Json`</span><span class="sxs-lookup"><span data-stu-id="80ff4-486">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="80ff4-487">WindowsPhone — > `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="80ff4-487">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
