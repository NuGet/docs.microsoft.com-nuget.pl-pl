---
title: Dokumentacja pliku. nuspec dla narzędzia NuGet
description: Plik. nuspec zawiera metadane pakietu używane podczas kompilowania pakietu i dostarczania informacji użytkownikom pakietu.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6bd730db16d8e8783f0d949bb04cf3b52c642cd0
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380553"
---
# <a name="nuspec-reference"></a><span data-ttu-id="5c0db-103">nuspec — odwołanie</span><span class="sxs-lookup"><span data-stu-id="5c0db-103">.nuspec reference</span></span>

<span data-ttu-id="5c0db-104">Plik `.nuspec` jest manifestem XML zawierającym metadane pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="5c0db-105">Ten manifest jest używany zarówno do kompilowania pakietu, jak i dostarczania informacji klientom.</span><span class="sxs-lookup"><span data-stu-id="5c0db-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="5c0db-106">Manifest jest zawsze zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="5c0db-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="5c0db-107">In this topic:</span></span>

- [<span data-ttu-id="5c0db-108">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="5c0db-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="5c0db-109">[Tokeny zastępcze](#replacement-tokens) (gdy są używane z projektem programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5c0db-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="5c0db-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="5c0db-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="5c0db-111">Jawne odwołania do zestawów</span><span class="sxs-lookup"><span data-stu-id="5c0db-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="5c0db-112">Odwołania do zestawów struktury</span><span class="sxs-lookup"><span data-stu-id="5c0db-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="5c0db-113">Dołączanie plików zestawów</span><span class="sxs-lookup"><span data-stu-id="5c0db-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="5c0db-114">Dołączanie plików zawartości</span><span class="sxs-lookup"><span data-stu-id="5c0db-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="5c0db-115">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="5c0db-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="5c0db-116">Zgodność typu projektu</span><span class="sxs-lookup"><span data-stu-id="5c0db-116">Project type compatibility</span></span>

- <span data-ttu-id="5c0db-117">Użyj `.nuspec` z `nuget.exe pack` dla projektów typu non-SDK, które używają `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="5c0db-118">Plik `.nuspec` nie jest wymagany do tworzenia pakietów dla [projektów w stylu zestawu SDK](../resources/check-project-format.md) (zazwyczaj projekty .NET Core i .NET Standard, które używają [atrybutu SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="5c0db-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="5c0db-119">(Należy pamiętać, że podczas tworzenia pakietu jest generowane `.nuspec`).</span><span class="sxs-lookup"><span data-stu-id="5c0db-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="5c0db-120">Jeśli tworzysz pakiet przy użyciu `dotnet.exe pack` lub `msbuild pack target`, zalecamy [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w pliku `.nuspec` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="5c0db-121">Można jednak [użyć pliku `.nuspec` do spakowania przy użyciu `dotnet.exe` lub `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="5c0db-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="5c0db-122">W przypadku projektów migrowanych z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md)plik `.nuspec` nie jest wymagany do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="5c0db-123">Zamiast tego należy użyć [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="5c0db-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="5c0db-124">Ogólny formularz i schemat</span><span class="sxs-lookup"><span data-stu-id="5c0db-124">General form and schema</span></span>

<span data-ttu-id="5c0db-125">Bieżący plik schematu `nuspec.xsd` znajduje się w [repozytorium GitHub usługi NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="5c0db-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="5c0db-126">W tym schemacie plik `.nuspec` ma następującą formę ogólną:</span><span class="sxs-lookup"><span data-stu-id="5c0db-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="5c0db-127">Aby wyczyścić wizualną reprezentację schematu, Otwórz plik schematu w programie Visual Studio w trybie projektowania i kliknij link **Eksplorator schematu XML** .</span><span class="sxs-lookup"><span data-stu-id="5c0db-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="5c0db-128">Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze, a następnie wybierz polecenie **Pokaż Eksplorator schematu XML**.</span><span class="sxs-lookup"><span data-stu-id="5c0db-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="5c0db-129">W dowolnym momencie możesz wyświetlić widok podobny do przedstawionego poniżej (w większości rozwiniętych):</span><span class="sxs-lookup"><span data-stu-id="5c0db-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Eksplorator schematu programu Visual Studio z otwartym nuspec. xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="5c0db-131">Wymagane elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="5c0db-131">Required metadata elements</span></span>

<span data-ttu-id="5c0db-132">Mimo że następujące elementy są minimalnymi wymaganiami dotyczącymi pakietu, należy rozważyć dodanie [opcjonalnych elementów metadanych](#optional-metadata-elements) w celu poprawienia ogólnych doświadczeń deweloperów korzystających z Twojego pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="5c0db-133">Te elementy muszą występować w elemencie `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="5c0db-134">identyfikator</span><span class="sxs-lookup"><span data-stu-id="5c0db-134">id</span></span> 
<span data-ttu-id="5c0db-135">Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowy w obrębie nuget.org lub dowolnej galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="5c0db-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="5c0db-136">Identyfikatory nie mogą zawierać spacji ani znaków, które są nieprawidłowe dla adresu URL, i ogólnie przestrzegają reguł przestrzeni nazw platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="5c0db-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="5c0db-137">Aby uzyskać wskazówki [, zobacz Wybieranie unikatowego identyfikatora pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="5c0db-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="5c0db-138">version</span><span class="sxs-lookup"><span data-stu-id="5c0db-138">version</span></span>
<span data-ttu-id="5c0db-139">Wersja pakietu, po wzorcu *główna. pomocnicza. poprawka* .</span><span class="sxs-lookup"><span data-stu-id="5c0db-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="5c0db-140">Numery wersji mogą zawierać sufiks wstępnej wersji, zgodnie z opisem w temacie [wersja pakietu](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="5c0db-140">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="5c0db-141">opis</span><span class="sxs-lookup"><span data-stu-id="5c0db-141">description</span></span>
<span data-ttu-id="5c0db-142">Opis pakietu na potrzeby wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c0db-142">A description of the package for UI display.</span></span>
#### <a name="authors"></a><span data-ttu-id="5c0db-143">Autorów</span><span class="sxs-lookup"><span data-stu-id="5c0db-143">authors</span></span>
<span data-ttu-id="5c0db-144">Rozdzielana przecinkami lista autorów pakietów, które pasują do nazw profilów w nuget.org. Są one wyświetlane w galerii NuGet w witrynie nuget.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="5c0db-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="5c0db-145">Opcjonalne elementy metadanych</span><span class="sxs-lookup"><span data-stu-id="5c0db-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="5c0db-146">rzecz</span><span class="sxs-lookup"><span data-stu-id="5c0db-146">owners</span></span>
<span data-ttu-id="5c0db-147">Rozdzielana przecinkami lista twórców pakietów korzystających z nazw profilów w nuget.org. Jest to często taka sama lista jak w `authors` i jest ignorowana podczas przekazywania pakietu do nuget.org. Zobacz [Zarządzanie właścicielami pakietów w witrynie NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="5c0db-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="5c0db-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="5c0db-148">projectUrl</span></span>
<span data-ttu-id="5c0db-149">Adres URL strony głównej pakietu, często wyświetlany w interfejsie użytkownika, a także nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5c0db-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="5c0db-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="5c0db-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="5c0db-151">licenseUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="5c0db-151">licenseUrl is deprecated.</span></span> <span data-ttu-id="5c0db-152">Zamiast tego użyj licencji.</span><span class="sxs-lookup"><span data-stu-id="5c0db-152">Use license instead.</span></span>

<span data-ttu-id="5c0db-153">Adres URL licencji pakietu, często przedstawiony w interfejsów użytkownika, na przykład nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5c0db-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="5c0db-154">licencjonowan</span><span class="sxs-lookup"><span data-stu-id="5c0db-154">license</span></span>
<span data-ttu-id="5c0db-155">Wyrażenie licencji SPDX lub ścieżka do pliku licencji w pakiecie, często pokazywane w interfejsów użytkownika, jak nuget.org. Jeśli pakiet jest licencjonowany w ramach wspólnej licencji, takiej jak MIT lub BSD-2-klauzule, należy użyć skojarzonego [identyfikatora licencji SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="5c0db-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="5c0db-156">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c0db-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="5c0db-157">NuGet.org akceptuje tylko wyrażenia licencyjne zatwierdzone przez inicjatywę Open Source lub bezpłatną program Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="5c0db-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="5c0db-158">Jeśli pakiet jest licencjonowany w ramach wielu popularnych licencji, możesz określić licencję złożoną przy użyciu [składni wyrażenia SPDX w wersji 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="5c0db-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="5c0db-159">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c0db-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="5c0db-160">Jeśli używasz niestandardowej licencji, która nie jest obsługiwana przez wyrażenia licencji, możesz spakować plik `.txt` lub `.md` z tekstem licencji.</span><span class="sxs-lookup"><span data-stu-id="5c0db-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="5c0db-161">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c0db-161">For example:</span></span>

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

<span data-ttu-id="5c0db-162">Aby uzyskać odpowiedniki programu MSBuild, zapoznaj się z tematem [pakowanie wyrażenia licencji lub pliku licencji](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="5c0db-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="5c0db-163">Dokładna składnia wyrażeń licencji narzędzia NuGet została opisana poniżej w [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="5c0db-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="5c0db-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="5c0db-164">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="5c0db-165">iconUrl jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="5c0db-165">iconUrl is deprecated.</span></span> <span data-ttu-id="5c0db-166">Zamiast tego użyj ikony.</span><span class="sxs-lookup"><span data-stu-id="5c0db-166">Use icon instead.</span></span>

<span data-ttu-id="5c0db-167">Adres URL obrazu 64x64 z przezroczystym tłem, który będzie używany jako ikona pakietu w wyświetlanym interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c0db-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="5c0db-168">Upewnij się, że ten element zawiera *adres URL obrazu bezpośredniego* , a nie adres URL strony sieci Web zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="5c0db-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="5c0db-169">Na przykład, aby użyć obrazu z usługi GitHub, użyj adresu URL nieprzetworzonego pliku, takiego jak <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="5c0db-169">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
#### <a name="icon"></a><span data-ttu-id="5c0db-170">Ikona</span><span class="sxs-lookup"><span data-stu-id="5c0db-170">icon</span></span>

<span data-ttu-id="5c0db-171">Jest to ścieżka do pliku obrazu w pakiecie, często pokazana w interfejsów użytkownika, jak nuget.org jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-171">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="5c0db-172">Rozmiar pliku obrazu jest ograniczony do 1 MB.</span><span class="sxs-lookup"><span data-stu-id="5c0db-172">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="5c0db-173">Obsługiwane formaty plików to JPEG i PNG.</span><span class="sxs-lookup"><span data-stu-id="5c0db-173">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="5c0db-174">Zalecamy resoulution obrazu 64x64.</span><span class="sxs-lookup"><span data-stu-id="5c0db-174">We recommend an image resoulution of 64x64.</span></span>

<span data-ttu-id="5c0db-175">Na przykład podczas tworzenia pakietu przy użyciu programu NuGet. exe należy dodać następujący element do nuspecu:</span><span class="sxs-lookup"><span data-stu-id="5c0db-175">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="5c0db-176">Przykład nuspec ikony pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-176">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="5c0db-177">W przypadku odpowiedników programu MSBuild zapoznaj się z [opakowaniem pliku obrazu ikony](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="5c0db-177">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="5c0db-178">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5c0db-178">requireLicenseAcceptance</span></span>
<span data-ttu-id="5c0db-179">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-179">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="5c0db-180">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="5c0db-180">developmentDependency</span></span>
<span data-ttu-id="5c0db-181">*(2.8 +)* Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do programowania, który uniemożliwia dołączenie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="5c0db-181">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="5c0db-182">W przypadku PackageReference (NuGet 4.8 +) Ta flaga oznacza również, że wykluczają się zasoby czasu kompilacji z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5c0db-182">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="5c0db-183">Zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="5c0db-183">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="5c0db-184">podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5c0db-184">summary</span></span>
> [!Important]
> <span data-ttu-id="5c0db-185">`summary` jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="5c0db-185">`summary` is being deprecated.</span></span> <span data-ttu-id="5c0db-186">Zamiast nich należy używać słów kluczowych `description`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-186">Use `description` instead.</span></span>

<span data-ttu-id="5c0db-187">Krótki opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c0db-187">A short description of the package for UI display.</span></span> <span data-ttu-id="5c0db-188">W przypadku pominięcia zostanie użyta obcięta wersja `description`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-188">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="5c0db-189">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="5c0db-189">releaseNotes</span></span>
<span data-ttu-id="5c0db-190">*(1,5 +)* Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak karta **aktualizacje** w Menedżerze pakietów programu Visual Studio zamiast opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-190">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="5c0db-191">informacji o prawach autorskich,</span><span class="sxs-lookup"><span data-stu-id="5c0db-191">copyright</span></span>
<span data-ttu-id="5c0db-192">*(1,5 +)* Szczegóły dotyczące praw autorskich pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-192">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="5c0db-193">język</span><span class="sxs-lookup"><span data-stu-id="5c0db-193">language</span></span>
<span data-ttu-id="5c0db-194">Identyfikator ustawień regionalnych dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-194">The locale ID for the package.</span></span> <span data-ttu-id="5c0db-195">Zobacz [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="5c0db-195">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="5c0db-196">tagi</span><span class="sxs-lookup"><span data-stu-id="5c0db-196">tags</span></span>
<span data-ttu-id="5c0db-197">Rozdzielana spacjami Lista tagów i słów kluczowych, które opisują pakiet i ułatwiają odnajdywanie pakietów przez wyszukiwanie i filtrowanie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-197">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="5c0db-198">Obsługa</span><span class="sxs-lookup"><span data-stu-id="5c0db-198">serviceable</span></span> 
<span data-ttu-id="5c0db-199">*(3.3 +)* Tylko do użytku wewnętrznego narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c0db-199">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="5c0db-200">repozytorium</span><span class="sxs-lookup"><span data-stu-id="5c0db-200">repository</span></span>
<span data-ttu-id="5c0db-201">Metadane repozytorium zawierające cztery opcjonalne atrybuty: `type` i `url` *(4.0 +)* i `branch` i `commit` *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="5c0db-201">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="5c0db-202">Te atrybuty umożliwiają mapowanie `.nupkg` do repozytorium, które zostało przez siebie skompilowane, z możliwością uzyskania tak szczegółowej nazwy gałęzi i/lub zatwierdzenia skrótu SHA-1, który skompilowano pakiet.</span><span class="sxs-lookup"><span data-stu-id="5c0db-202">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="5c0db-203">Powinien to być publicznie dostępny adres URL, który może być wywoływany bezpośrednio przez oprogramowanie kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="5c0db-203">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="5c0db-204">Nie powinna być stroną HTML, ponieważ jest ona przeznaczona dla komputera.</span><span class="sxs-lookup"><span data-stu-id="5c0db-204">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="5c0db-205">W przypadku łączenia ze stroną projektu zamiast tego użyj pola `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-205">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="5c0db-206">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c0db-206">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="5c0db-207">tytuły</span><span class="sxs-lookup"><span data-stu-id="5c0db-207">title</span></span>
<span data-ttu-id="5c0db-208">Przyjazny dla człowieka tytuł pakietu, który może być używany w niektórych interfejsach użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c0db-208">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="5c0db-209">(nuget.org i Menedżer pakietów w programie Visual Studio nie wyświetla tytułu)</span><span class="sxs-lookup"><span data-stu-id="5c0db-209">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="5c0db-210">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="5c0db-210">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="5c0db-211">packageTypes</span><span class="sxs-lookup"><span data-stu-id="5c0db-211">packageTypes</span></span>
<span data-ttu-id="5c0db-212">*(3.5 +)* Kolekcja elementów `<packageType>`, które określają typ pakietu, jeśli jest inny niż tradycyjny pakiet zależności.</span><span class="sxs-lookup"><span data-stu-id="5c0db-212">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="5c0db-213">Każdy pakiet PackageType ma atrybuty *nazwy* i *wersji*.</span><span class="sxs-lookup"><span data-stu-id="5c0db-213">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="5c0db-214">Zobacz [Ustawianie typu pakietu](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="5c0db-214">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="5c0db-215">zależności</span><span class="sxs-lookup"><span data-stu-id="5c0db-215">dependencies</span></span>
<span data-ttu-id="5c0db-216">Kolekcja zero lub więcej elementów `<dependency>` określających zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-216">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="5c0db-217">Każda zależność ma atrybuty *identyfikatora*, *wersji*, *include* (3. x +) i *exclude* (3. x +).</span><span class="sxs-lookup"><span data-stu-id="5c0db-217">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="5c0db-218">Zobacz [zależności](#dependencies-element) poniżej.</span><span class="sxs-lookup"><span data-stu-id="5c0db-218">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="5c0db-219">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="5c0db-219">frameworkAssemblies</span></span>
<span data-ttu-id="5c0db-220">*(1.2 +)* Kolekcja elementów `<frameworkAssembly>`, które identyfikują .NET Framework odwołania do zestawów, które są wymagane przez ten pakiet, co zapewnia, że odwołania są dodawane do projektów zużywających pakiet.</span><span class="sxs-lookup"><span data-stu-id="5c0db-220">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="5c0db-221">Każdy frameworkAssembly ma atrybuty *AssemblyName* i *TargetFramework* .</span><span class="sxs-lookup"><span data-stu-id="5c0db-221">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="5c0db-222">Zobacz [Określanie zestawu Framework odwołuje się do poniższej pamięci podręcznej](#specifying-framework-assembly-references-gac) .</span><span class="sxs-lookup"><span data-stu-id="5c0db-222">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="5c0db-223">odwołania</span><span class="sxs-lookup"><span data-stu-id="5c0db-223">references</span></span>
<span data-ttu-id="5c0db-224">*(1,5 +)* Kolekcja elementów w folderze `lib` `<reference>`, które są dodawane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-224">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="5c0db-225">Każde odwołanie ma atrybut *pliku* .</span><span class="sxs-lookup"><span data-stu-id="5c0db-225">Each reference has a *file* attribute.</span></span> <span data-ttu-id="5c0db-226">`<references>` może również zawierać element `<group>` z atrybutem *TargetFramework* , który następnie zawiera elementy `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-226">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="5c0db-227">W przypadku pominięcia są uwzględniane wszystkie odwołania w `lib`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-227">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="5c0db-228">Zobacz [Określanie jawnych odwołań do zestawów](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="5c0db-228">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="5c0db-229">contentFiles</span><span class="sxs-lookup"><span data-stu-id="5c0db-229">contentFiles</span></span>
<span data-ttu-id="5c0db-230">*(3.3 +)* Kolekcja elementów `<files>`, które identyfikują pliki zawartości do uwzględnienia w projekcie konsumowanym.</span><span class="sxs-lookup"><span data-stu-id="5c0db-230">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="5c0db-231">Te pliki są określone za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-231">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="5c0db-232">Zobacz sekcję [określanie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej.</span><span class="sxs-lookup"><span data-stu-id="5c0db-232">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="5c0db-233">— pliki</span><span class="sxs-lookup"><span data-stu-id="5c0db-233">files</span></span> 
<span data-ttu-id="5c0db-234">Węzeł `<package>` może zawierać węzeł `<files>` jako element równorzędny do `<metadata>` i element podrzędny `<contentFiles>` w obszarze `<metadata>`, aby określić, które pliki zestawu i zawartości mają zostać uwzględnione w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-234">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="5c0db-235">Szczegółowe informacje znajdują się w temacie [zawierającym pliki zestawu](#including-assembly-files) i [pliki zawartości](#including-content-files) w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-235">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="5c0db-236">atrybuty metadanych</span><span class="sxs-lookup"><span data-stu-id="5c0db-236">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="5c0db-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5c0db-237">minClientVersion</span></span>
<span data-ttu-id="5c0db-238">Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszony przez NuGet. exe i Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c0db-238">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="5c0db-239">Jest on używany zawsze, gdy pakiet jest zależny od określonych funkcji pliku `.nuspec`, które zostały dodane w określonej wersji klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c0db-239">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="5c0db-240">Na przykład pakiet z atrybutem `developmentDependency` powinien określać wartość "2,8" dla `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-240">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="5c0db-241">Podobnie pakiet używający elementu `contentFiles` (zobacz następną sekcję) powinien ustawić `minClientVersion` na "3,3".</span><span class="sxs-lookup"><span data-stu-id="5c0db-241">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="5c0db-242">Należy zauważyć, że ponieważ klienci NuGet przed 2,5 nie rozpoznają tej flagi, *zawsze* odmówią instalacji pakietu niezależnie od tego, co `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="5c0db-242">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
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

## <a name="replacement-tokens"></a><span data-ttu-id="5c0db-243">Tokeny zastępcze</span><span class="sxs-lookup"><span data-stu-id="5c0db-243">Replacement tokens</span></span>

<span data-ttu-id="5c0db-244">Podczas tworzenia pakietu [polecenie `nuget pack`](../reference/cli-reference/cli-ref-pack.md) zastępuje tokeny $-Unlimited w węźle `<metadata>` pliku `.nuspec` wartościami, które pochodzą z pliku projektu lub z `pack` polecenia `-properties`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-244">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="5c0db-245">W wierszu polecenia należy określić wartości tokenów z `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-245">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="5c0db-246">Na przykład można użyć tokenu, takiego jak `$owners$` i `$desc$` w `.nuspec` i podać wartości w czasie pakowania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5c0db-246">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="5c0db-247">Aby użyć wartości z projektu, należy określić tokeny opisane w poniższej tabeli (AssemblyInfo odnosi się do pliku w `Properties`, na przykład `AssemblyInfo.cs` lub `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="5c0db-247">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="5c0db-248">Aby użyć tych tokenów, uruchom `nuget pack` z plikiem projektu, a nie tylko `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-248">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="5c0db-249">Na przykład w przypadku korzystania z następującego polecenia tokeny `$id$` i `$version$` w pliku `.nuspec` są zastępowane wartościami `AssemblyName` i `AssemblyVersion` projektu:</span><span class="sxs-lookup"><span data-stu-id="5c0db-249">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="5c0db-250">Zwykle, gdy masz projekt, tworzysz `.nuspec` początkowo przy użyciu `nuget spec MyProject.csproj`, który automatycznie zawiera niektóre z tych standardowych tokenów.</span><span class="sxs-lookup"><span data-stu-id="5c0db-250">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="5c0db-251">Jeśli jednak projekt nie zawiera wartości dla wymaganych elementów `.nuspec`, wówczas `nuget pack` kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5c0db-251">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="5c0db-252">Ponadto jeśli zmienisz wartości projektu, pamiętaj, aby ponownie skompilować przed utworzeniem pakietu; można to zrobić wygodnie za pomocą przełącznika `build` polecenia pakiet.</span><span class="sxs-lookup"><span data-stu-id="5c0db-252">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="5c0db-253">Z wyjątkiem `$configuration$` wartości w projekcie są używane w preferencjach do wszystkich przypisanych do tego samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c0db-253">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="5c0db-254">Klucza</span><span class="sxs-lookup"><span data-stu-id="5c0db-254">Token</span></span> | <span data-ttu-id="5c0db-255">Źródło wartości</span><span class="sxs-lookup"><span data-stu-id="5c0db-255">Value source</span></span> | <span data-ttu-id="5c0db-256">Wartość</span><span class="sxs-lookup"><span data-stu-id="5c0db-256">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="5c0db-257">**$id $**</span><span class="sxs-lookup"><span data-stu-id="5c0db-257">**$id$**</span></span> | <span data-ttu-id="5c0db-258">Plik projektu</span><span class="sxs-lookup"><span data-stu-id="5c0db-258">Project file</span></span> | <span data-ttu-id="5c0db-259">AssemblyName (title) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="5c0db-259">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="5c0db-260">**$version $**</span><span class="sxs-lookup"><span data-stu-id="5c0db-260">**$version$**</span></span> | <span data-ttu-id="5c0db-261">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="5c0db-261">AssemblyInfo</span></span> | <span data-ttu-id="5c0db-262">AssemblyInformationalVersion, jeśli jest obecny, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="5c0db-262">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="5c0db-263">**$author $**</span><span class="sxs-lookup"><span data-stu-id="5c0db-263">**$author$**</span></span> | <span data-ttu-id="5c0db-264">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="5c0db-264">AssemblyInfo</span></span> | <span data-ttu-id="5c0db-265">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="5c0db-265">AssemblyCompany</span></span> |
| <span data-ttu-id="5c0db-266">**$title $**</span><span class="sxs-lookup"><span data-stu-id="5c0db-266">**$title$**</span></span> | <span data-ttu-id="5c0db-267">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="5c0db-267">AssemblyInfo</span></span> | <span data-ttu-id="5c0db-268">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="5c0db-268">AssemblyTitle</span></span> |
| <span data-ttu-id="5c0db-269">**$description $**</span><span class="sxs-lookup"><span data-stu-id="5c0db-269">**$description$**</span></span> | <span data-ttu-id="5c0db-270">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="5c0db-270">AssemblyInfo</span></span> | <span data-ttu-id="5c0db-271">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="5c0db-271">AssemblyDescription</span></span> |
| <span data-ttu-id="5c0db-272">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="5c0db-272">**$copyright$**</span></span> | <span data-ttu-id="5c0db-273">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="5c0db-273">AssemblyInfo</span></span> | <span data-ttu-id="5c0db-274">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="5c0db-274">AssemblyCopyright</span></span> |
| <span data-ttu-id="5c0db-275">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="5c0db-275">**$configuration$**</span></span> | <span data-ttu-id="5c0db-276">Biblioteka DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="5c0db-276">Assembly DLL</span></span> | <span data-ttu-id="5c0db-277">Konfiguracja użyta do skompilowania zestawu, czyli domyślnego debugowania.</span><span class="sxs-lookup"><span data-stu-id="5c0db-277">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="5c0db-278">Należy pamiętać, że aby utworzyć pakiet przy użyciu konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c0db-278">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="5c0db-279">Tokeny mogą być również używane do rozpoznawania ścieżek podczas dołączania [plików zestawu](#including-assembly-files) i [plików zawartości](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="5c0db-279">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="5c0db-280">Tokeny mają takie same nazwy jak właściwości programu MSBuild, dzięki czemu można wybrać pliki do uwzględnienia w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5c0db-280">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="5c0db-281">Jeśli na przykład w pliku `.nuspec` są używane następujące tokeny:</span><span class="sxs-lookup"><span data-stu-id="5c0db-281">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="5c0db-282">I kompilowanie zestawu, którego `AssemblyName` to `LoggingLibrary` z konfiguracją `Release` w programie MSBuild, wyniki wierszy w pliku `.nuspec` w pakiecie są następujące:</span><span class="sxs-lookup"><span data-stu-id="5c0db-282">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="5c0db-283">Element zależności</span><span class="sxs-lookup"><span data-stu-id="5c0db-283">Dependencies element</span></span>

<span data-ttu-id="5c0db-284">Element `<dependencies>` w `<metadata>` zawiera dowolną liczbę elementów `<dependency>`, które identyfikują inne pakiety, od których zależy pakiet najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-284">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="5c0db-285">Atrybuty dla każdego `<dependency>` są następujące:</span><span class="sxs-lookup"><span data-stu-id="5c0db-285">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="5c0db-286">Atrybut</span><span class="sxs-lookup"><span data-stu-id="5c0db-286">Attribute</span></span> | <span data-ttu-id="5c0db-287">Opis</span><span class="sxs-lookup"><span data-stu-id="5c0db-287">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="5c0db-288">Potrzeb Identyfikator pakietu zależności, taki jak "EntityFramework" i "NUnit", czyli nazwa pakietu nuget.org wyświetlana na stronie pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-288">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="5c0db-289">Potrzeb Zakres wersji akceptowalnych jako zależność.</span><span class="sxs-lookup"><span data-stu-id="5c0db-289">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="5c0db-290">Aby uzyskać dokładną składnię, zobacz [wersja pakietu](../concepts/package-versioning.md#version-ranges-and-wildcards) .</span><span class="sxs-lookup"><span data-stu-id="5c0db-290">See [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> <span data-ttu-id="5c0db-291">Wersje wieloznaczne (przestawne) nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5c0db-291">Wildcard (floating) versions are not supported.</span></span> |
| <span data-ttu-id="5c0db-292">include</span><span class="sxs-lookup"><span data-stu-id="5c0db-292">include</span></span> | <span data-ttu-id="5c0db-293">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazujących zależność do uwzględnienia w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="5c0db-293">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="5c0db-294">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-294">The default value is `all`.</span></span> |
| <span data-ttu-id="5c0db-295">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="5c0db-295">exclude</span></span> | <span data-ttu-id="5c0db-296">Rozdzielana przecinkami lista tagów dołączania/wykluczania (patrz poniżej) wskazujących zależność do wykluczenia w końcowym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-296">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="5c0db-297">Wartość domyślna to `build,analyzers`, która może być nadpisywana.</span><span class="sxs-lookup"><span data-stu-id="5c0db-297">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="5c0db-298">Ale `content/ ContentFiles` również jest niejawnie wykluczony w pakiecie końcowym, który nie może być nadpisany.</span><span class="sxs-lookup"><span data-stu-id="5c0db-298">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="5c0db-299">Tagi określone za pomocą `exclude` mają pierwszeństwo przed tymi określonymi przy użyciu `include`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-299">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="5c0db-300">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-300">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="5c0db-301">Include/Exclude — tag</span><span class="sxs-lookup"><span data-stu-id="5c0db-301">Include/Exclude tag</span></span> | <span data-ttu-id="5c0db-302">Zmodyfikowane foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="5c0db-302">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="5c0db-303">contentFiles</span><span class="sxs-lookup"><span data-stu-id="5c0db-303">contentFiles</span></span> | <span data-ttu-id="5c0db-304">Zawartość</span><span class="sxs-lookup"><span data-stu-id="5c0db-304">Content</span></span> |
| <span data-ttu-id="5c0db-305">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="5c0db-305">runtime</span></span> | <span data-ttu-id="5c0db-306">Środowisko uruchomieniowe, zasoby i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="5c0db-306">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="5c0db-307">Opracowania</span><span class="sxs-lookup"><span data-stu-id="5c0db-307">compile</span></span> | <span data-ttu-id="5c0db-308">lib</span><span class="sxs-lookup"><span data-stu-id="5c0db-308">lib</span></span> |
| <span data-ttu-id="5c0db-309">kompilacja</span><span class="sxs-lookup"><span data-stu-id="5c0db-309">build</span></span> | <span data-ttu-id="5c0db-310">Kompilacja (właściwości i elementy docelowe programu MSBuild)</span><span class="sxs-lookup"><span data-stu-id="5c0db-310">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="5c0db-311">natywne</span><span class="sxs-lookup"><span data-stu-id="5c0db-311">native</span></span> | <span data-ttu-id="5c0db-312">natywne</span><span class="sxs-lookup"><span data-stu-id="5c0db-312">native</span></span> |
| <span data-ttu-id="5c0db-313">brak</span><span class="sxs-lookup"><span data-stu-id="5c0db-313">none</span></span> | <span data-ttu-id="5c0db-314">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="5c0db-314">No folders</span></span> |
| <span data-ttu-id="5c0db-315">wszystkie</span><span class="sxs-lookup"><span data-stu-id="5c0db-315">all</span></span> | <span data-ttu-id="5c0db-316">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="5c0db-316">All folders</span></span> |

<span data-ttu-id="5c0db-317">Na przykład następujące wiersze wskazują zależności od `PackageA` w wersji 1.1.0 lub nowszej oraz `PackageB` wersji 1. x.</span><span class="sxs-lookup"><span data-stu-id="5c0db-317">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="5c0db-318">Poniższe wiersze wskazują zależności dotyczące tych samych pakietów, ale określają, że mają być dostępne foldery `contentFiles` i `build` `PackageA` i wszystko, ale `native` i `compile` folderów `PackageB` "</span><span class="sxs-lookup"><span data-stu-id="5c0db-318">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="5c0db-319">Podczas tworzenia `.nuspec` z projektu przy użyciu `nuget spec` zależności, które istnieją w tym projekcie, nie są automatycznie uwzględniane w wytworzonym pliku `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-319">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="5c0db-320">Zamiast tego należy użyć `nuget pack myproject.csproj` i pobrać plik *. nuspec* z wygenerowanego pliku *NUPKG* .</span><span class="sxs-lookup"><span data-stu-id="5c0db-320">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="5c0db-321">This *. nuspec* zawiera zależności.</span><span class="sxs-lookup"><span data-stu-id="5c0db-321">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="5c0db-322">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="5c0db-322">Dependency groups</span></span>

<span data-ttu-id="5c0db-323">*Wersja 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="5c0db-323">*Version 2.0+*</span></span>

<span data-ttu-id="5c0db-324">Jako alternatywę dla pojedynczej płaskiej listy, zależności można określić zgodnie z profilem struktury projektu docelowego za pomocą elementów `<group>` w `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-324">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="5c0db-325">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej elementów `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-325">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="5c0db-326">Te zależności są instalowane razem, gdy struktura docelowa jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-326">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="5c0db-327">Element `<group>` bez atrybutu `targetFramework` jest używany jako domyślna lub rezerwowa lista zależności.</span><span class="sxs-lookup"><span data-stu-id="5c0db-327">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="5c0db-328">Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.</span><span class="sxs-lookup"><span data-stu-id="5c0db-328">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="5c0db-329">Format grupy nie może być mieszany z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="5c0db-329">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="5c0db-330">W poniższym przykładzie przedstawiono różne odmiany elementu `<group>`:</span><span class="sxs-lookup"><span data-stu-id="5c0db-330">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="5c0db-331">Jawne odwołania do zestawów</span><span class="sxs-lookup"><span data-stu-id="5c0db-331">Explicit assembly references</span></span>

<span data-ttu-id="5c0db-332">Element `<references>` jest używany przez projekty używające `packages.config` do jawnego określania zestawów, do których projekt docelowy powinien odwoływać się podczas korzystania z pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-332">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="5c0db-333">Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="5c0db-333">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="5c0db-334">Aby uzyskać więcej informacji, zobacz stronę [wybierania zestawów, do których odwołują się projekty](../create-packages/select-assemblies-referenced-by-projects.md) , aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5c0db-334">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="5c0db-335">Na przykład następujący element `<references>` nakazuje pakietowi NuGet dodanie odwołań do `xunit.dll` i `xunit.extensions.dll`, nawet jeśli w pakiecie istnieją dodatkowe zestawy:</span><span class="sxs-lookup"><span data-stu-id="5c0db-335">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="5c0db-336">Grupy odwołań</span><span class="sxs-lookup"><span data-stu-id="5c0db-336">Reference groups</span></span>

<span data-ttu-id="5c0db-337">Jako alternatywę dla pojedynczej płaskiej listy, odwołania można określić zgodnie z profilem struktury projektu docelowego za pomocą elementów `<group>` w `<references>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-337">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="5c0db-338">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej elementów `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-338">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="5c0db-339">Te odwołania są dodawane do projektu, gdy struktura docelowa jest zgodna z profilem struktury projektu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-339">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="5c0db-340">Element `<group>` bez atrybutu `targetFramework` jest używany jako domyślna lub rezerwowa lista odwołań.</span><span class="sxs-lookup"><span data-stu-id="5c0db-340">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="5c0db-341">Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.</span><span class="sxs-lookup"><span data-stu-id="5c0db-341">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="5c0db-342">Format grupy nie może być mieszany z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="5c0db-342">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="5c0db-343">W poniższym przykładzie przedstawiono różne odmiany elementu `<group>`:</span><span class="sxs-lookup"><span data-stu-id="5c0db-343">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="5c0db-344">Odwołania do zestawów struktury</span><span class="sxs-lookup"><span data-stu-id="5c0db-344">Framework assembly references</span></span>

<span data-ttu-id="5c0db-345">Zestawy struktur są tymi, które są częścią programu .NET Framework i powinny już znajdować się w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej maszyny.</span><span class="sxs-lookup"><span data-stu-id="5c0db-345">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="5c0db-346">Identyfikując te zestawy w ramach elementu `<frameworkAssemblies>`, pakiet może zapewnić, że wymagane odwołania są dodawane do projektu w przypadku, gdy projekt nie ma już odwołań.</span><span class="sxs-lookup"><span data-stu-id="5c0db-346">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="5c0db-347">Takie zespoły nie są bezpośrednio zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-347">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="5c0db-348">Element `<frameworkAssemblies>` zawiera zero lub więcej elementów `<frameworkAssembly>`, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="5c0db-348">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="5c0db-349">Atrybut</span><span class="sxs-lookup"><span data-stu-id="5c0db-349">Attribute</span></span> | <span data-ttu-id="5c0db-350">Opis</span><span class="sxs-lookup"><span data-stu-id="5c0db-350">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c0db-351">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="5c0db-351">**assemblyName**</span></span> | <span data-ttu-id="5c0db-352">Potrzeb W pełni kwalifikowana nazwa zestawu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-352">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="5c0db-353">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="5c0db-353">**targetFramework**</span></span> | <span data-ttu-id="5c0db-354">Obowiązkowe Określa platformę docelową, do której stosuje się to odwołanie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-354">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="5c0db-355">W przypadku pominięcia wskazuje, że odwołanie dotyczy wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="5c0db-355">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="5c0db-356">Zobacz [Platformy docelowe](../reference/target-frameworks.md) dla dokładnych identyfikatorów platformy.</span><span class="sxs-lookup"><span data-stu-id="5c0db-356">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="5c0db-357">W poniższym przykładzie przedstawiono odwołanie do `System.Net` dla wszystkich platform docelowych i odwołania do `System.ServiceModel` tylko dla .NET Framework 4,0:</span><span class="sxs-lookup"><span data-stu-id="5c0db-357">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="5c0db-358">Dołączanie plików zestawów</span><span class="sxs-lookup"><span data-stu-id="5c0db-358">Including assembly files</span></span>

<span data-ttu-id="5c0db-359">Jeśli przestrzegasz Konwencji opisanych w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md), nie musisz jawnie określać listy plików w pliku `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-359">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="5c0db-360">Polecenie `nuget pack` automatycznie pobiera niezbędne pliki.</span><span class="sxs-lookup"><span data-stu-id="5c0db-360">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="5c0db-361">Gdy pakiet jest instalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu do bibliotek DLL pakietu, *z wyłączeniem* tych, które mają nazwę `.resources.dll`, ponieważ zakłada się, że są to zlokalizowane zestawy satelickie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-361">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="5c0db-362">Z tego powodu należy unikać używania `.resources.dll` w przypadku plików, które w przeciwnym razie zawierają istotny kod pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-362">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="5c0db-363">Aby ominąć to automatyczne zachowanie i jawnie kontrolować, które pliki są zawarte w pakiecie, umieść `<files>` elementu jako element podrzędny `<package>` (i element równorzędny `<metadata>`), identyfikujący każdy plik z oddzielnym elementem `<file>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-363">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="5c0db-364">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c0db-364">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="5c0db-365">W przypadku pakietów NuGet 2. x i starszych oraz projektów używających `packages.config` element `<files>` jest również używany do uwzględniania niezmiennych plików zawartości podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-365">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="5c0db-366">W przypadku pakietów NuGet 3.3 + i projektów PackageReference, zamiast tego jest używany element `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-366">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="5c0db-367">Aby uzyskać szczegółowe informacje, zobacz temat [uwzględnianie plików zawartości](#including-content-files) poniżej.</span><span class="sxs-lookup"><span data-stu-id="5c0db-367">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="5c0db-368">Atrybuty elementu pliku</span><span class="sxs-lookup"><span data-stu-id="5c0db-368">File element attributes</span></span>

<span data-ttu-id="5c0db-369">Każdy element `<file>` określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="5c0db-369">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="5c0db-370">Atrybut</span><span class="sxs-lookup"><span data-stu-id="5c0db-370">Attribute</span></span> | <span data-ttu-id="5c0db-371">Opis</span><span class="sxs-lookup"><span data-stu-id="5c0db-371">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c0db-372">**SRC**</span><span class="sxs-lookup"><span data-stu-id="5c0db-372">**src**</span></span> | <span data-ttu-id="5c0db-373">Lokalizacja pliku lub plików do dołączenia, z uwzględnieniem wyjątków określonych przez atrybut `exclude`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-373">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="5c0db-374">Ścieżka jest określana względem pliku `.nuspec`, chyba że zostanie określona ścieżka bezwzględna.</span><span class="sxs-lookup"><span data-stu-id="5c0db-374">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="5c0db-375">Symbol wieloznaczny `*` jest dozwolony, a podwójny symbol wieloznaczny `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="5c0db-375">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="5c0db-376">**obiektów**</span><span class="sxs-lookup"><span data-stu-id="5c0db-376">**target**</span></span> | <span data-ttu-id="5c0db-377">Ścieżka względna do folderu w pakiecie, w którym znajdują się pliki źródłowe, co musi rozpoczynać się od `lib`, `content`, `build` lub `tools`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-377">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="5c0db-378">Zobacz [Tworzenie nuspec z katalogu roboczego opartego na Konwencji](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="5c0db-378">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="5c0db-379">**klucza**</span><span class="sxs-lookup"><span data-stu-id="5c0db-379">**exclude**</span></span> | <span data-ttu-id="5c0db-380">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z lokalizacji `src`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-380">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="5c0db-381">Symbol wieloznaczny `*` jest dozwolony, a podwójny symbol wieloznaczny `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="5c0db-381">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="5c0db-382">Przykłady</span><span class="sxs-lookup"><span data-stu-id="5c0db-382">Examples</span></span>

<span data-ttu-id="5c0db-383">**Pojedynczy zestaw**</span><span class="sxs-lookup"><span data-stu-id="5c0db-383">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="5c0db-384">**Pojedynczy zestaw specyficzny dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="5c0db-384">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="5c0db-385">**Zestaw bibliotek DLL przy użyciu symbolu wieloznacznego**</span><span class="sxs-lookup"><span data-stu-id="5c0db-385">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="5c0db-386">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="5c0db-386">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="5c0db-387">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="5c0db-387">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="5c0db-388">Dołączanie plików zawartości</span><span class="sxs-lookup"><span data-stu-id="5c0db-388">Including content files</span></span>

<span data-ttu-id="5c0db-389">Pliki zawartości to niezmienne pliki, których pakiet musi zawierać w projekcie.</span><span class="sxs-lookup"><span data-stu-id="5c0db-389">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="5c0db-390">Są niezmienne, nie są przeznaczone do modyfikacji przez projekt zużywający.</span><span class="sxs-lookup"><span data-stu-id="5c0db-390">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="5c0db-391">Przykładowe pliki zawartości obejmują:</span><span class="sxs-lookup"><span data-stu-id="5c0db-391">Example content files include:</span></span>

- <span data-ttu-id="5c0db-392">Obrazy osadzone jako zasoby</span><span class="sxs-lookup"><span data-stu-id="5c0db-392">Images that are embedded as resources</span></span>
- <span data-ttu-id="5c0db-393">Pliki źródłowe, które zostały już skompilowane</span><span class="sxs-lookup"><span data-stu-id="5c0db-393">Source files that are already compiled</span></span>
- <span data-ttu-id="5c0db-394">Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="5c0db-394">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="5c0db-395">Pliki konfiguracji pakietu, które muszą być zawarte w projekcie, ale nie muszą mieć żadnych zmian specyficznych dla projektu</span><span class="sxs-lookup"><span data-stu-id="5c0db-395">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="5c0db-396">Pliki zawartości są zawarte w pakiecie przy użyciu elementu `<files>`, określając folder `content` w atrybucie `target`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-396">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="5c0db-397">Jednak takie pliki są ignorowane, gdy pakiet zostanie zainstalowany w projekcie przy użyciu PackageReference, który zamiast tego używa elementu `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-397">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="5c0db-398">Aby zapewnić maksymalną zgodność z zużywanymi projektami, pakiet najlepiej określa pliki zawartości w obu elementach.</span><span class="sxs-lookup"><span data-stu-id="5c0db-398">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="5c0db-399">Używanie elementu Files dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="5c0db-399">Using the files element for content files</span></span>

<span data-ttu-id="5c0db-400">W przypadku plików zawartości po prostu Użyj tego samego formatu co dla plików zestawu, ale Określ `content` jako folder podstawowy w atrybucie `target`, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="5c0db-400">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="5c0db-401">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="5c0db-401">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="5c0db-402">**Pliki zawartości z strukturą katalogów**</span><span class="sxs-lookup"><span data-stu-id="5c0db-402">**Content files with directory structure**</span></span>

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

<span data-ttu-id="5c0db-403">**Plik zawartości specyficzny dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="5c0db-403">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="5c0db-404">**Plik zawartości skopiowany do folderu z kropką w nazwie**</span><span class="sxs-lookup"><span data-stu-id="5c0db-404">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="5c0db-405">W takim przypadku pakiet NuGet uważa, że rozszerzenie w `target` nie pasuje do rozszerzenia w `src` i w ten sposób traktuje tę część nazwy w `target` jako folder:</span><span class="sxs-lookup"><span data-stu-id="5c0db-405">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="5c0db-406">**Pliki zawartości bez rozszerzeń**</span><span class="sxs-lookup"><span data-stu-id="5c0db-406">**Content files without extensions**</span></span>

<span data-ttu-id="5c0db-407">Aby dołączyć pliki bez rozszerzenia, Użyj symboli wieloznacznych `*` lub `**`:</span><span class="sxs-lookup"><span data-stu-id="5c0db-407">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="5c0db-408">**Pliki zawartości ze szczegółową ścieżką i głębokiego celu**</span><span class="sxs-lookup"><span data-stu-id="5c0db-408">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="5c0db-409">W tym przypadku, ponieważ rozszerzenia plików dla dopasowania źródłowego i docelowego, pakiet NuGet zakłada, że obiektem docelowym jest nazwa pliku, a nie folder:</span><span class="sxs-lookup"><span data-stu-id="5c0db-409">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="5c0db-410">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="5c0db-410">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="5c0db-411">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="5c0db-411">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="5c0db-412">Używanie elementu contentFiles dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="5c0db-412">Using the contentFiles element for content files</span></span>

<span data-ttu-id="5c0db-413">*Pakiet NuGet 4.0 + z PackageReference*</span><span class="sxs-lookup"><span data-stu-id="5c0db-413">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="5c0db-414">Domyślnie pakiet umieszcza zawartość w folderze `contentFiles` (patrz poniżej) i `nuget pack` dołączył wszystkie pliki w tym folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="5c0db-414">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="5c0db-415">W takim przypadku nie trzeba uwzględniać węzła `contentFiles` w `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-415">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="5c0db-416">Aby kontrolować, które pliki są uwzględniane, element `<contentFiles>` Określa kolekcję elementów `<files>`, które identyfikują dokładne pliki include.</span><span class="sxs-lookup"><span data-stu-id="5c0db-416">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="5c0db-417">Te pliki są określone za pomocą zestawu atrybutów, które opisują, jak powinny być używane w systemie projektu:</span><span class="sxs-lookup"><span data-stu-id="5c0db-417">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="5c0db-418">Atrybut</span><span class="sxs-lookup"><span data-stu-id="5c0db-418">Attribute</span></span> | <span data-ttu-id="5c0db-419">Opis</span><span class="sxs-lookup"><span data-stu-id="5c0db-419">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c0db-420">**include**</span><span class="sxs-lookup"><span data-stu-id="5c0db-420">**include**</span></span> | <span data-ttu-id="5c0db-421">Potrzeb Lokalizacja pliku lub plików do dołączenia, z uwzględnieniem wyjątków określonych przez atrybut `exclude`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-421">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="5c0db-422">Ścieżka jest określana względem folderu `contentFiles`, chyba że zostanie określona ścieżka bezwzględna.</span><span class="sxs-lookup"><span data-stu-id="5c0db-422">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="5c0db-423">Symbol wieloznaczny `*` jest dozwolony, a podwójny symbol wieloznaczny `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="5c0db-423">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="5c0db-424">**klucza**</span><span class="sxs-lookup"><span data-stu-id="5c0db-424">**exclude**</span></span> | <span data-ttu-id="5c0db-425">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z lokalizacji `src`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-425">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="5c0db-426">Symbol wieloznaczny `*` jest dozwolony, a podwójny symbol wieloznaczny `**` oznacza cykliczne wyszukiwanie folderów.</span><span class="sxs-lookup"><span data-stu-id="5c0db-426">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="5c0db-427">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="5c0db-427">**buildAction**</span></span> | <span data-ttu-id="5c0db-428">Akcja kompilacji, która ma zostać przypisana do elementu zawartości dla programu MSBuild, taka jak `Content`, `None`, `Embedded Resource`, `Compile` itd. Wartość domyślna to `Compile`.</span><span class="sxs-lookup"><span data-stu-id="5c0db-428">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="5c0db-429">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="5c0db-429">**copyToOutput**</span></span> | <span data-ttu-id="5c0db-430">Wartość logiczna wskazująca, czy elementy zawartości mają być kopiowane do folderu wyjściowego kompilacja (lub publikacja).</span><span class="sxs-lookup"><span data-stu-id="5c0db-430">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="5c0db-431">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="5c0db-431">The default is false.</span></span> |
| <span data-ttu-id="5c0db-432">**Flatten**</span><span class="sxs-lookup"><span data-stu-id="5c0db-432">**flatten**</span></span> | <span data-ttu-id="5c0db-433">Wartość logiczna wskazująca, czy kopiować elementy zawartości do pojedynczego folderu w danych wyjściowych kompilacji (true), czy też zachować strukturę folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="5c0db-433">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="5c0db-434">Ta flaga działa tylko wtedy, gdy flaga copyToOutput jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="5c0db-434">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="5c0db-435">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="5c0db-435">The default is false.</span></span> |

<span data-ttu-id="5c0db-436">Podczas instalowania pakietu NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-436">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="5c0db-437">Jeśli wiele wpisów pasuje do tego samego pliku, zostaną zastosowane wszystkie wpisy.</span><span class="sxs-lookup"><span data-stu-id="5c0db-437">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="5c0db-438">Wpis najwyższego poziomu zastępuje niższe wpisy w przypadku konfliktu dla tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="5c0db-438">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="5c0db-439">Struktura folderu pakietu</span><span class="sxs-lookup"><span data-stu-id="5c0db-439">Package folder structure</span></span>

<span data-ttu-id="5c0db-440">Projekt pakietu powinien mieć strukturę zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="5c0db-440">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="5c0db-441">`codeLanguages` może być `cs`, `vb`, `fs`, `any` lub małymi literami odpowiadającymi `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="5c0db-441">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="5c0db-442">`TxM` to dowolna moniker platformy docelowej, który obsługuje pakiet NuGet (patrz [Platformy docelowe](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="5c0db-442">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="5c0db-443">Wszystkie struktury folderów mogą być dołączane na końcu tej składni.</span><span class="sxs-lookup"><span data-stu-id="5c0db-443">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="5c0db-444">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c0db-444">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="5c0db-445">Puste foldery mogą używać `.`, aby zrezygnować z udostępniania zawartości dla niektórych kombinacji języka i TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c0db-445">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="5c0db-446">Przykładowa sekcja contentFiles</span><span class="sxs-lookup"><span data-stu-id="5c0db-446">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="5c0db-447">Przykładowe pliki nuspec</span><span class="sxs-lookup"><span data-stu-id="5c0db-447">Example nuspec files</span></span>

<span data-ttu-id="5c0db-448">**Prosta `.nuspec`, która nie określa zależności ani plików**</span><span class="sxs-lookup"><span data-stu-id="5c0db-448">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="5c0db-449">**@No__t-1 z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="5c0db-449">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="5c0db-450">**@No__t-1 z plikami**</span><span class="sxs-lookup"><span data-stu-id="5c0db-450">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="5c0db-451">**@No__t-1 z zestawami struktury**</span><span class="sxs-lookup"><span data-stu-id="5c0db-451">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="5c0db-452">W tym przykładzie są zainstalowane następujące elementy docelowe dla konkretnych projektów:</span><span class="sxs-lookup"><span data-stu-id="5c0db-452">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="5c0db-453">. NET4-> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="5c0db-453">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="5c0db-454">. Profil klienta NET4 — > `System.Net`</span><span class="sxs-lookup"><span data-stu-id="5c0db-454">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="5c0db-455">Silverlight 3 — > `System.Json`</span><span class="sxs-lookup"><span data-stu-id="5c0db-455">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="5c0db-456">WindowsPhone — @no__t >-0</span><span class="sxs-lookup"><span data-stu-id="5c0db-456">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
