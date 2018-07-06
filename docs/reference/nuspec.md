---
title: Odwołanie do pliku .nuspec dla NuGet
description: Plik .nuspec zawiera metadane pakietów używane podczas tworzenia pakietu i do dostarczania informacji klientów pakietu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 142f82386395b8ab2ed1d57218db9bc1d2e98638
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843449"
---
# <a name="nuspec-reference"></a><span data-ttu-id="a6395-103">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="a6395-103">.nuspec reference</span></span>

<span data-ttu-id="a6395-104">A `.nuspec` plik jest manifestu XML, który zawiera metadane pakietów.</span><span class="sxs-lookup"><span data-stu-id="a6395-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="a6395-105">Ten manifest służy do tworzenia pakietu i podaj informacje dla klientów.</span><span class="sxs-lookup"><span data-stu-id="a6395-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="a6395-106">Manifest zawsze znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="a6395-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="a6395-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="a6395-107">In this topic:</span></span>

- [<span data-ttu-id="a6395-108">Ogólna postać i schematu</span><span class="sxs-lookup"><span data-stu-id="a6395-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="a6395-109">[Zastąpienia tokenów](#replacement-tokens) (jeśli jest używana w projekcie programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a6395-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="a6395-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="a6395-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="a6395-111">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="a6395-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="a6395-112">Odwołania zestawu</span><span class="sxs-lookup"><span data-stu-id="a6395-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="a6395-113">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="a6395-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="a6395-114">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="a6395-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="a6395-115">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a6395-115">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="a6395-116">Ogólna postać i schematu</span><span class="sxs-lookup"><span data-stu-id="a6395-116">General form and schema</span></span>

<span data-ttu-id="a6395-117">Bieżący `nuspec.xsd` można znaleźć w pliku schematu [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="a6395-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="a6395-118">W tym schemacie `.nuspec` plik ma następującą postać ogólne:</span><span class="sxs-lookup"><span data-stu-id="a6395-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="a6395-119">Wizualnych reprezentacji schematu, otwórz plik schematu w programie Visual Studio w trybie projektowania, a następnie kliknij przycisk na **Eksploratora schematu XML** łącza.</span><span class="sxs-lookup"><span data-stu-id="a6395-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="a6395-120">Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz **Pokaż Eksploratora schematu XML**.</span><span class="sxs-lookup"><span data-stu-id="a6395-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="a6395-121">W obu przypadkach, uzyskasz widoku podobne do pokazanego poniżej (w przypadku większości rozwinięte):</span><span class="sxs-lookup"><span data-stu-id="a6395-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Explorer schematu z nuspec.xsd Otwórz](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="a6395-123">Atrybuty metadanych</span><span class="sxs-lookup"><span data-stu-id="a6395-123">Metadata attributes</span></span>

<span data-ttu-id="a6395-124">`<metadata>` Obsługuje element atrybutów opisanych w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="a6395-124">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="a6395-125">Atrybut</span><span class="sxs-lookup"><span data-stu-id="a6395-125">Attribute</span></span> | <span data-ttu-id="a6395-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a6395-126">Required</span></span> | <span data-ttu-id="a6395-127">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-127">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="a6395-128">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="a6395-128">**minClientVersion**</span></span> | <span data-ttu-id="a6395-129">Nie</span><span class="sxs-lookup"><span data-stu-id="a6395-129">No</span></span> | <span data-ttu-id="a6395-130">Określa minimalną wersję klienta NuGet, który można zainstalować ten pakiet, wymuszane przez nuget.exe oraz Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6395-130">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="a6395-131">Jest on używany zawsze wtedy, gdy pakiet jest zależny od określonych funkcji `.nuspec` plików, które zostały dodane w konkretnej wersji klienta programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6395-131">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="a6395-132">Na przykład pakiet przy użyciu `developmentDependency` atrybut należy określić "2.8" dla `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="a6395-132">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="a6395-133">Podobnie, pakiet przy użyciu `contentFiles` (zobacz następną sekcję) należy ustawić element `minClientVersion` do "3.3".</span><span class="sxs-lookup"><span data-stu-id="a6395-133">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="a6395-134">Należy zauważyć, że ponieważ klienci programu NuGet przed 2.5 nie rozpoznają tej flagi należy ich *zawsze* odmówić można zainstalować pakietu, niezależnie od tego, co `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="a6395-134">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="a6395-135">Elementy wymagane metadane</span><span class="sxs-lookup"><span data-stu-id="a6395-135">Required metadata elements</span></span>

<span data-ttu-id="a6395-136">Mimo że następujące elementy są minimalne wymagania dotyczące pakietu, należy rozważyć dodanie [elementy opcjonalne metadane](#optional-metadata-elements) usprawniających atrakcyjniejsze środowisko pracy deweloperzy muszą z pakietem.</span><span class="sxs-lookup"><span data-stu-id="a6395-136">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="a6395-137">Te elementy muszą znajdować się w `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="a6395-137">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="a6395-138">Element</span><span class="sxs-lookup"><span data-stu-id="a6395-138">Element</span></span> | <span data-ttu-id="a6395-139">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6395-140">**id**</span><span class="sxs-lookup"><span data-stu-id="a6395-140">**id**</span></span> | <span data-ttu-id="a6395-141">Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowa w witrynie nuget.org lub cokolwiek innego pakietu, który znajduje się w galerii.</span><span class="sxs-lookup"><span data-stu-id="a6395-141">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="a6395-142">Identyfikatory nie mogą zawierać spacji ani znaków, które nie są prawidłowe dla danego adresu URL i zazwyczaj korzystają z reguły w przestrzeni nazw .NET.</span><span class="sxs-lookup"><span data-stu-id="a6395-142">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="a6395-143">Zobacz [wybierając identyfikator unikatowy pakiet](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) wskazówki.</span><span class="sxs-lookup"><span data-stu-id="a6395-143">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="a6395-144">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="a6395-144">**version**</span></span> | <span data-ttu-id="a6395-145">Wersja pakietu, następujące *Wersja_główna.WERSJA_POMOCNICZA.poprawka* wzorca.</span><span class="sxs-lookup"><span data-stu-id="a6395-145">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="a6395-146">Numery wersji mogą zawierać sufiks wersji wstępnej, zgodnie z opisem w [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="a6395-146">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="a6395-147">**Opis elementu**</span><span class="sxs-lookup"><span data-stu-id="a6395-147">**description**</span></span> | <span data-ttu-id="a6395-148">Długi opis pakietu do wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a6395-148">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="a6395-149">**Autorzy**</span><span class="sxs-lookup"><span data-stu-id="a6395-149">**authors**</span></span> | <span data-ttu-id="a6395-150">Rozdzielana przecinkami lista autorów pakietów, pasujące nazwy profilu w witrynie nuget.org. Te są wyświetlane w galerii pakietów NuGet w witrynie nuget.org i są odwoływania się do pakietów przez ten sam autorów.</span><span class="sxs-lookup"><span data-stu-id="a6395-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="a6395-151">Elementy opcjonalne metadane</span><span class="sxs-lookup"><span data-stu-id="a6395-151">Optional metadata elements</span></span>

<span data-ttu-id="a6395-152">Te elementy mogą być widoczne w `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="a6395-152">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="a6395-153">Pojedyncze elementy</span><span class="sxs-lookup"><span data-stu-id="a6395-153">Single elements</span></span>

| <span data-ttu-id="a6395-154">Element</span><span class="sxs-lookup"><span data-stu-id="a6395-154">Element</span></span> | <span data-ttu-id="a6395-155">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-155">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6395-156">**Tytuł**</span><span class="sxs-lookup"><span data-stu-id="a6395-156">**title**</span></span> | <span data-ttu-id="a6395-157">Tytuł przyjaznego dla człowieka pakietu, zwykle używanych w interfejsie użytkownika wyświetla w witrynach nuget.org i Menedżera pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6395-157">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="a6395-158">Jeśli nie zostanie określony, identyfikator pakietu jest używany.</span><span class="sxs-lookup"><span data-stu-id="a6395-158">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="a6395-159">**Właściciele**</span><span class="sxs-lookup"><span data-stu-id="a6395-159">**owners**</span></span> | <span data-ttu-id="a6395-160">Rozdzielana przecinkami lista twórców pakietów przy użyciu nazwy profilu w witrynie nuget.org. Jest to często tej samej listy podobnie jak w `authors`i jest ignorowana podczas przekazywania pakietu na stronie nuget.org. Zobacz [właścicieli pakietu zarządzania w witrynie nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="a6395-160">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="a6395-161">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="a6395-161">**projectUrl**</span></span> | <span data-ttu-id="a6395-162">Adres URL strony głównej pakietu, często wyświetlany w użytkownika, jak również adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a6395-162">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="a6395-163">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="a6395-163">**licenseUrl**</span></span> | <span data-ttu-id="a6395-164">Adres URL licencji pakietu, często wyświetlany w użytkownika, jak również adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a6395-164">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="a6395-165">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="a6395-165">**iconUrl**</span></span> | <span data-ttu-id="a6395-166">Adres URL obrazu 64 x 64 z przezroczystość tła do użycia jako ikona dla pakietu wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a6395-166">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="a6395-167">Pamiętaj, że ten element zawiera *bezpośredni adres URL obrazu* a nie jej adres URL strony sieci web zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="a6395-167">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="a6395-168">Na przykład, aby użyć obrazu z witryny GitHub, należy użyć plik raw, takie jak adres URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="a6395-168">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> |
| <span data-ttu-id="a6395-169">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="a6395-169">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="a6395-170">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-170">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="a6395-171">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="a6395-171">**developmentDependency**</span></span> | <span data-ttu-id="a6395-172">*(2.8 +)*  Wartość logiczna określająca, czy pakiet jest oznaczone jako — tylko zależnością programistyczną, co zapobiega uwzględniane jako zależności w innych pakietach pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-172">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="a6395-173">**Podsumowanie**</span><span class="sxs-lookup"><span data-stu-id="a6395-173">**summary**</span></span> | <span data-ttu-id="a6395-174">Krótki opis pakietu do wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a6395-174">A short description of the package for UI display.</span></span> <span data-ttu-id="a6395-175">Jeśli argument jest pominięty, skróconą wersję `description` jest używany.</span><span class="sxs-lookup"><span data-stu-id="a6395-175">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="a6395-176">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="a6395-176">**releaseNotes**</span></span> | <span data-ttu-id="a6395-177">*(w wersji 1.5 +)*  Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak **aktualizacje** kartę z Menedżera pakietów Visual Studio zamiast opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-177">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="a6395-178">**copyright**</span><span class="sxs-lookup"><span data-stu-id="a6395-178">**copyright**</span></span> | <span data-ttu-id="a6395-179">*(w wersji 1.5 +)*  Copyright szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-179">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="a6395-180">**Język**</span><span class="sxs-lookup"><span data-stu-id="a6395-180">**language**</span></span> | <span data-ttu-id="a6395-181">Identyfikator ustawień regionalnych dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-181">The locale ID for the package.</span></span> <span data-ttu-id="a6395-182">Zobacz [tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a6395-182">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="a6395-183">**tagi**</span><span class="sxs-lookup"><span data-stu-id="a6395-183">**tags**</span></span>  | <span data-ttu-id="a6395-184">Rozdzielany spacjami lista tagów i słów kluczowych, które opisują możliwości pakietu i pomocy pakietów za pomocą wyszukiwania i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="a6395-184">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="a6395-185">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="a6395-185">**serviceable**</span></span> | <span data-ttu-id="a6395-186">*(3.3 +)*  NuGet wewnętrznego użytku tylko.</span><span class="sxs-lookup"><span data-stu-id="a6395-186">*(3.3+)* For internal NuGet use only.</span></span> |
| <span data-ttu-id="a6395-187">**repozytorium**</span><span class="sxs-lookup"><span data-stu-id="a6395-187">**repository**</span></span> | <span data-ttu-id="a6395-188">Metadane repozytorium, składający się z czterech atrybuty opcjonalne: *typu* i *adresu url* *(4.0 i nowsze)*, i *gałęzi* i  *zatwierdzenie* *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="a6395-188">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="a6395-189">Te atrybuty zezwalać na mapowanie .nupkg do repozytorium, którego kompilacja, z których można pobrać jak wyjaśniono, jak poszczególne gałęzi lub zatwierdzania, który skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="a6395-189">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="a6395-190">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="a6395-190">Collection elements</span></span>

| <span data-ttu-id="a6395-191">Element</span><span class="sxs-lookup"><span data-stu-id="a6395-191">Element</span></span> | <span data-ttu-id="a6395-192">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-192">Description</span></span> |
| --- | --- |
<span data-ttu-id="a6395-193">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="a6395-193">**packageTypes**</span></span> | <span data-ttu-id="a6395-194">*(3.5 +)*  Zbiór zero lub więcej `<packageType>` elementów, określając typ pakietu, jeśli inne niż tradycyjne zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-194">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="a6395-195">Każdy packageType ma atrybuty *nazwa* i *wersji*.</span><span class="sxs-lookup"><span data-stu-id="a6395-195">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="a6395-196">Zobacz [ustawienie typu pakietu](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="a6395-196">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="a6395-197">**zależności**</span><span class="sxs-lookup"><span data-stu-id="a6395-197">**dependencies**</span></span> | <span data-ttu-id="a6395-198">Kolekcja zero lub więcej `<dependency>` elementy określenie zależności dotyczących pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-198">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="a6395-199">Poszczególne zależności ma atrybuty *identyfikator*, *wersji*, *obejmują* (3.x+) i *wykluczyć* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="a6395-199">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="a6395-200">Zobacz [zależności](#dependencies) poniżej.</span><span class="sxs-lookup"><span data-stu-id="a6395-200">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="a6395-201">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="a6395-201">**frameworkAssemblies**</span></span> | <span data-ttu-id="a6395-202">*(1.2 +)*  Zbiór zero lub więcej `<frameworkAssembly>` elementów identyfikowanie odwołania do zestawów .NET Framework, które wymaga tego pakietu, dzięki któremu czy odwołania są dodawane do projektów, korzystanie z pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-202">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="a6395-203">Została każda frameworkAssembly *assemblyName* i *targetFramework* atrybutów.</span><span class="sxs-lookup"><span data-stu-id="a6395-203">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="a6395-204">Zobacz [określenie zestawu struktury odwołuje się do globalnej pamięci podręcznej zestawów](#specifying-framework-assembly-references-gac) poniżej.</span><span class="sxs-lookup"><span data-stu-id="a6395-204">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="a6395-205">**odwołania**</span><span class="sxs-lookup"><span data-stu-id="a6395-205">**references**</span></span> | <span data-ttu-id="a6395-206">*(w wersji 1.5 +)*  Zbiór zero lub więcej `<reference>` elementy nazewnictwa zestawów, w tym pakiecie `lib` folderu, które są dodawane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="a6395-206">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="a6395-207">Każde odwołanie zawiera *pliku* atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a6395-207">Each reference has a *file* attribute.</span></span> <span data-ttu-id="a6395-208">`<references>` może również zawierać `<group>` element z *targetFramework* atrybut, który następnie zawiera `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="a6395-208">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="a6395-209">Jeśli argument jest pominięty, wszystkie odwołania w `lib` są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="a6395-209">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="a6395-210">Zobacz [odwołania do zestawów jawne określenie](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="a6395-210">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="a6395-211">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="a6395-211">**contentFiles**</span></span> | <span data-ttu-id="a6395-212">*(3.3 +)*  Zbiór `<files>` elementy, które identyfikują plików zawartości do uwzględnienia w projekcie odbierająca komunikaty.</span><span class="sxs-lookup"><span data-stu-id="a6395-212">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="a6395-213">Te pliki są określane przy użyciu zestawu atrybutów, które opisują, jak powinna być używana w ramach systemu projektu.</span><span class="sxs-lookup"><span data-stu-id="a6395-213">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="a6395-214">Zobacz [określenie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej.</span><span class="sxs-lookup"><span data-stu-id="a6395-214">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="a6395-215">Element Pliki</span><span class="sxs-lookup"><span data-stu-id="a6395-215">Files element</span></span>

<span data-ttu-id="a6395-216">`<package>` Węzeł może zawierać `<files>` węzeł jako element równorzędny do `<metadata>`, a lub `<contentFiles>` podrzędne w ramach `<metadata>`, aby określić, które pliki zestawu i zawartości do uwzględnienia w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="a6395-216">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="a6395-217">Zobacz [w tym pliki zestawu](#including-assembly-files) i [pliki zawartości w tym](#including-content-files) później w tym temacie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a6395-217">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="a6395-218">Zastąpienia tokenów</span><span class="sxs-lookup"><span data-stu-id="a6395-218">Replacement tokens</span></span>

<span data-ttu-id="a6395-219">Podczas tworzenia pakietu [ `nuget pack` polecenia](../tools/cli-ref-pack.md) zastępuje rozdzielonych $ tokenów w `.nuspec` pliku `<metadata>` węzła z wartości, które pochodzą z poziomu pliku projektu lub `pack` polecenia `-properties`przełącznika.</span><span class="sxs-lookup"><span data-stu-id="a6395-219">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="a6395-220">W wierszu polecenia określ wartości tokenu `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="a6395-220">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="a6395-221">Na przykład takie jak możesz użyć tokenu `$owners$` i `$desc$` w `.nuspec` i podaj wartości w pakowania czasu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a6395-221">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="a6395-222">Aby użyć wartości z projektem, określ tokenów opisane w poniższej tabeli (AssemblyInfo odwołuje się do pliku w `Properties` takich jak `AssemblyInfo.cs` lub `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="a6395-222">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="a6395-223">Aby korzystać z tych tokenów, należy uruchomić `nuget pack` przy użyciu pliku projektu, a nie po prostu `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a6395-223">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="a6395-224">Na przykład przy użyciu następującego polecenia `$id$` i `$version$` tokenów w `.nuspec` pliku są zastępowane projektu `AssemblyName` i `AssemblyVersion` wartości:</span><span class="sxs-lookup"><span data-stu-id="a6395-224">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="a6395-225">Zazwyczaj w przypadku projektu tworzony `.nuspec` początkowo przy użyciu `nuget spec MyProject.csproj` automatycznie zawierający niektóre z tych tokenów standardowych.</span><span class="sxs-lookup"><span data-stu-id="a6395-225">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="a6395-226">Jednakże jeśli projekt nie ma wartości dla wymaganych `.nuspec` elementów, a następnie `nuget pack` zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a6395-226">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="a6395-227">Ponadto w przypadku zmiany wartości projektu, upewnij się odbudować przed utworzeniem pakietu; Można to zrobić wygodna przy użyciu polecenia pakietu `build` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="a6395-227">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="a6395-228">Z wyjątkiem produktów `$configuration$`, wartości w projekcie są używane zamiast dowolne przypisane do tego samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6395-228">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="a6395-229">Token</span><span class="sxs-lookup"><span data-stu-id="a6395-229">Token</span></span> | <span data-ttu-id="a6395-230">Wartość źródła</span><span class="sxs-lookup"><span data-stu-id="a6395-230">Value source</span></span> | <span data-ttu-id="a6395-231">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6395-231">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="a6395-232">**$id$**</span><span class="sxs-lookup"><span data-stu-id="a6395-232">**$id$**</span></span> | <span data-ttu-id="a6395-233">Plik projektu</span><span class="sxs-lookup"><span data-stu-id="a6395-233">Project file</span></span> | <span data-ttu-id="a6395-234">AssemblyName (tytuł) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="a6395-234">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="a6395-235">**$version$**</span><span class="sxs-lookup"><span data-stu-id="a6395-235">**$version$**</span></span> | <span data-ttu-id="a6395-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a6395-236">AssemblyInfo</span></span> | <span data-ttu-id="a6395-237">AssemblyInformationalVersion, jeśli jest obecna, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="a6395-237">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="a6395-238">**$author$**</span><span class="sxs-lookup"><span data-stu-id="a6395-238">**$author$**</span></span> | <span data-ttu-id="a6395-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a6395-239">AssemblyInfo</span></span> | <span data-ttu-id="a6395-240">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="a6395-240">AssemblyCompany</span></span> |
| <span data-ttu-id="a6395-241">**$title$**</span><span class="sxs-lookup"><span data-stu-id="a6395-241">**$title$**</span></span> | <span data-ttu-id="a6395-242">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a6395-242">AssemblyInfo</span></span> | <span data-ttu-id="a6395-243">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="a6395-243">AssemblyTitle</span></span> |
| <span data-ttu-id="a6395-244">**$description$**</span><span class="sxs-lookup"><span data-stu-id="a6395-244">**$description$**</span></span> | <span data-ttu-id="a6395-245">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a6395-245">AssemblyInfo</span></span> | <span data-ttu-id="a6395-246">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="a6395-246">AssemblyDescription</span></span> |
| <span data-ttu-id="a6395-247">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="a6395-247">**$copyright$**</span></span> | <span data-ttu-id="a6395-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a6395-248">AssemblyInfo</span></span> | <span data-ttu-id="a6395-249">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="a6395-249">AssemblyCopyright</span></span> |
| <span data-ttu-id="a6395-250">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="a6395-250">**$configuration$**</span></span> | <span data-ttu-id="a6395-251">Zestaw bibliotek DLL</span><span class="sxs-lookup"><span data-stu-id="a6395-251">Assembly DLL</span></span> | <span data-ttu-id="a6395-252">Konfiguracja używana do tworzenia zestawu, domyślnie używany do debugowania.</span><span class="sxs-lookup"><span data-stu-id="a6395-252">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="a6395-253">Należy pamiętać, że aby utworzyć pakiet za pomocą konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6395-253">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="a6395-254">Tokeny, również może służyć do rozpoznawania ścieżek, po włączeniu [plików zestawu](#including-assembly-files) i [zawartości plików](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="a6395-254">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="a6395-255">Tokeny mają takie same nazwy właściwości programu MSBuild, dzięki czemu można wybrać pliki do uwzględnienia w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a6395-255">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="a6395-256">Na przykład, jeśli używasz następujące generatory kodów w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="a6395-256">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="a6395-257">I kompilowania zestawu którego `AssemblyName` jest `LoggingLibrary` z `Release` konfiguracji w programie MSBuild, a wiersze wynikowe `.nuspec` plik w pakiecie znajduje się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a6395-257">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="a6395-258">Zależności</span><span class="sxs-lookup"><span data-stu-id="a6395-258">Dependencies</span></span>

<span data-ttu-id="a6395-259">`<dependencies>` Elemencie `<metadata>` zawiera dowolną liczbę `<dependency>` elementy, które identyfikują innych pakietów, od których zależy Pakiet najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="a6395-259">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="a6395-260">Atrybuty dla każdego `<dependency>` są następujące:</span><span class="sxs-lookup"><span data-stu-id="a6395-260">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="a6395-261">Atrybut</span><span class="sxs-lookup"><span data-stu-id="a6395-261">Attribute</span></span> | <span data-ttu-id="a6395-262">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-262">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="a6395-263">(Wymagane) Identyfikator pakietu zależności, takie jak "EntityFramework" i "NUnit", czyli nazwy nuget.org pakietu zawiera strona pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-263">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="a6395-264">(Wymagane) Zakres wersji dopuszczalne jako zależność.</span><span class="sxs-lookup"><span data-stu-id="a6395-264">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="a6395-265">Zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards) dla określonej składni.</span><span class="sxs-lookup"><span data-stu-id="a6395-265">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="a6395-266">include</span><span class="sxs-lookup"><span data-stu-id="a6395-266">include</span></span> | <span data-ttu-id="a6395-267">Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności do uwzględnienia w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="a6395-267">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="a6395-268">Wartość domyślna to `none`.</span><span class="sxs-lookup"><span data-stu-id="a6395-268">The default value is `none`.</span></span> |
| <span data-ttu-id="a6395-269">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="a6395-269">exclude</span></span> | <span data-ttu-id="a6395-270">Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności, które mają zostać wykluczone w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="a6395-270">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="a6395-271">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="a6395-271">The  default value is `all`.</span></span> <span data-ttu-id="a6395-272">Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`.</span><span class="sxs-lookup"><span data-stu-id="a6395-272">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="a6395-273">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="a6395-273">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="a6395-274">Uwzględnianie/wykluczanie znaczników</span><span class="sxs-lookup"><span data-stu-id="a6395-274">Include/Exclude tag</span></span> | <span data-ttu-id="a6395-275">Odpowiednie foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="a6395-275">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="a6395-276">Pliki</span><span class="sxs-lookup"><span data-stu-id="a6395-276">contentFiles</span></span> | <span data-ttu-id="a6395-277">Zawartość</span><span class="sxs-lookup"><span data-stu-id="a6395-277">Content</span></span> |
| <span data-ttu-id="a6395-278">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="a6395-278">runtime</span></span> | <span data-ttu-id="a6395-279">Środowisko uruchomieniowe, zasobów i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a6395-279">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="a6395-280">kompilacji</span><span class="sxs-lookup"><span data-stu-id="a6395-280">compile</span></span> | <span data-ttu-id="a6395-281">lib</span><span class="sxs-lookup"><span data-stu-id="a6395-281">lib</span></span> |
| <span data-ttu-id="a6395-282">kompilacja</span><span class="sxs-lookup"><span data-stu-id="a6395-282">build</span></span> | <span data-ttu-id="a6395-283">Kompilacja (cele i właściwości programu MSBuild)</span><span class="sxs-lookup"><span data-stu-id="a6395-283">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="a6395-284">natywne</span><span class="sxs-lookup"><span data-stu-id="a6395-284">native</span></span> | <span data-ttu-id="a6395-285">natywne</span><span class="sxs-lookup"><span data-stu-id="a6395-285">native</span></span> |
| <span data-ttu-id="a6395-286">brak</span><span class="sxs-lookup"><span data-stu-id="a6395-286">none</span></span> | <span data-ttu-id="a6395-287">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="a6395-287">No folders</span></span> |
| <span data-ttu-id="a6395-288">wszystkie</span><span class="sxs-lookup"><span data-stu-id="a6395-288">all</span></span> | <span data-ttu-id="a6395-289">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="a6395-289">All folders</span></span> |

<span data-ttu-id="a6395-290">Na przykład następujące wiersze wskazywać zależności na `PackageA` wersji 1.1.0 lub nowszej, a `PackageB` wersji 1.x.</span><span class="sxs-lookup"><span data-stu-id="a6395-290">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="a6395-291">Następujące wiersze wskazują zależności na te same pakiety, ale określono jako uwzględniane `contentFiles` i `build` folderów `PackageA` i wszystko, ale `native` i `compile` folderów `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="a6395-291">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="a6395-292">Uwaga: Podczas tworzenia `.nuspec` projektu używającego `nuget spec`, zależności, które istnieją w tym projekcie są automatycznie uwzględniane w wynikowym `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="a6395-292">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="a6395-293">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="a6395-293">Dependency groups</span></span>

<span data-ttu-id="a6395-294">*W wersji 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="a6395-294">*Version 2.0+*</span></span>

<span data-ttu-id="a6395-295">Jako alternatywy dla pojedynczego płaskiej listy, można określić zależności zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="a6395-295">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="a6395-296">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów.</span><span class="sxs-lookup"><span data-stu-id="a6395-296">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="a6395-297">Te zależności są instalowane razem, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="a6395-297">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a6395-298">`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listę zależności.</span><span class="sxs-lookup"><span data-stu-id="a6395-298">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="a6395-299">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="a6395-299">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a6395-300">Nie można się zmieszać format grupy z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="a6395-300">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="a6395-301">W poniższym przykładzie pokazano różnych odmian `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="a6395-301">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="a6395-302">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="a6395-302">Explicit assembly references</span></span>

<span data-ttu-id="a6395-303">`<references>` Element jawnie określa zestawy, które projekt docelowy powinny odwoływać się przy użyciu pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-303">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="a6395-304">Gdy ten element jest obecny, NuGet dodać odwołania do tylko zestawy wymienionych; nie powoduje dodania odwołania do innych zestawów, w tym pakiecie `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="a6395-304">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="a6395-305">Na przykład następująca `<references>` elementu powoduje, że rozszerzenie NuGet, aby dodać odwołania do tylko `xunit.dll` i `xunit.extensions.dll` nawet, jeśli istnieją dodatkowe zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="a6395-305">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="a6395-306">Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="a6395-306">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="a6395-307">Korzystając z [kontrakty kodu](/dotnet/framework/debug-trace-profile/code-contracts), na przykład zestawy umowy muszą być obok zestawów środowiska uruchomieniowego, które mogą rozszerzyć, aby je znaleźć programu Visual Studio, ale zestawy kontraktu nie musi być przywoływanego przez projekt lub skopiowany w projekcie `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="a6395-307">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="a6395-308">Podobnie jawnych odwołań może służyć do struktur testów jednostek, takich jak XUnit, którą jej narzędzi, zestawy znajdujące się obok zestawów środowiska uruchomieniowego, ale nie wymaga dołączeni ich jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="a6395-308">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="a6395-309">Grupy odwołań</span><span class="sxs-lookup"><span data-stu-id="a6395-309">Reference groups</span></span>

<span data-ttu-id="a6395-310">Alternatywą dla pojedynczego płaskiej listy odwołania można określić zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<references>`.</span><span class="sxs-lookup"><span data-stu-id="a6395-310">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="a6395-311">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="a6395-311">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="a6395-312">Te odwołania są dodawane do projektu, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="a6395-312">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a6395-313">`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listy odwołań.</span><span class="sxs-lookup"><span data-stu-id="a6395-313">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="a6395-314">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="a6395-314">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a6395-315">Nie można się zmieszać format grupy z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="a6395-315">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="a6395-316">W poniższym przykładzie pokazano różnych odmian `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="a6395-316">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="a6395-317">Odwołania zestawu</span><span class="sxs-lookup"><span data-stu-id="a6395-317">Framework assembly references</span></span>

<span data-ttu-id="a6395-318">Zestawy struktury są te, które są częścią programu .NET framework i powinien już znajdować się w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej podanej maszyny.</span><span class="sxs-lookup"><span data-stu-id="a6395-318">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="a6395-319">Identyfikując te zestawy w ramach `<frameworkAssemblies>` elementu pakietu można upewnij się, że wymagane odwołania są dodawane do projektu, w przypadku, gdy projekt nie ma już odwołania te.</span><span class="sxs-lookup"><span data-stu-id="a6395-319">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="a6395-320">Takie zestawy oczywiście nie są uwzględnione w pakiecie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="a6395-320">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="a6395-321">`<frameworkAssemblies>` Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="a6395-321">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="a6395-322">Atrybut</span><span class="sxs-lookup"><span data-stu-id="a6395-322">Attribute</span></span> | <span data-ttu-id="a6395-323">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-323">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6395-324">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="a6395-324">**assemblyName**</span></span> | <span data-ttu-id="a6395-325">(Wymagane) W pełni kwalifikowanej nazwy zestawu.</span><span class="sxs-lookup"><span data-stu-id="a6395-325">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="a6395-326">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="a6395-326">**targetFramework**</span></span> | <span data-ttu-id="a6395-327">(Opcjonalnie) Określa platformę docelową, której dotyczy odwołanie.</span><span class="sxs-lookup"><span data-stu-id="a6395-327">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="a6395-328">Jeśli argument jest pominięty, wskazuje, że odwołanie ma zastosowanie do wszystkich środowisk.</span><span class="sxs-lookup"><span data-stu-id="a6395-328">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="a6395-329">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="a6395-329">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="a6395-330">W poniższym przykładzie pokazano odwołanie do `System.Net` dla wszystkich docelowych struktur i odwołania do `System.ServiceModel` dla programu .NET Framework 4.0 tylko:</span><span class="sxs-lookup"><span data-stu-id="a6395-330">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="a6395-331">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="a6395-331">Including assembly files</span></span>

<span data-ttu-id="a6395-332">Jeśli stosujesz konwencje opisanego w [Tworzenie pakietu](../create-packages/creating-a-package.md), nie trzeba jawnie określić listę plików w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="a6395-332">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="a6395-333">`nuget pack` Polecenia automatycznie przejmuje on niezbędne pliki.</span><span class="sxs-lookup"><span data-stu-id="a6395-333">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="a6395-334">Po zainstalowaniu do projektu pakiet NuGet automatycznie dodaje odwołania do zestawów do pakietu biblioteki dll, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie.</span><span class="sxs-lookup"><span data-stu-id="a6395-334">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="a6395-335">Z tego powodu należy unikać `.resources.dll` dla plików, w przeciwnym razie zawierające kod essential pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6395-335">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="a6395-336">Aby pominąć to zachowanie automatyczne i jawnie kontrolować pliki, które są umieszczone w pakiecie, umieść `<files>` element jako element podrzędny elementu `<package>` (i element równorzędny `<metadata>`), identyfikowanie poszczególnych plików za pomocą oddzielnego `<file>` elementu.</span><span class="sxs-lookup"><span data-stu-id="a6395-336">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="a6395-337">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a6395-337">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="a6395-338">Nuget 2.x i starszych i projektów za pomocą `packages.config`, `<files>` element umożliwia również dołączać niezmienne pliki zawartości, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="a6395-338">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="a6395-339">Za pomocą narzędzi NuGet 3.3 + i projekty PackageReference `<contentFiles>` element jest używany zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="a6395-339">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="a6395-340">Zobacz [pliki zawartości w tym](#including-content-files) poniżej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a6395-340">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="a6395-341">Atrybuty elementu pliku</span><span class="sxs-lookup"><span data-stu-id="a6395-341">File element attributes</span></span>

<span data-ttu-id="a6395-342">Każdy `<file>` element określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="a6395-342">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="a6395-343">Atrybut</span><span class="sxs-lookup"><span data-stu-id="a6395-343">Attribute</span></span> | <span data-ttu-id="a6395-344">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-344">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6395-345">**src**</span><span class="sxs-lookup"><span data-stu-id="a6395-345">**src**</span></span> | <span data-ttu-id="a6395-346">Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a6395-346">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a6395-347">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="a6395-347">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="a6395-348">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="a6395-348">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a6395-349">**docelowy**</span><span class="sxs-lookup"><span data-stu-id="a6395-349">**target**</span></span> | <span data-ttu-id="a6395-350">Względna ścieżka do folderu, w pakiecie, gdzie są umieszczone pliki źródłowe, musi zaczynać się od `lib`, `content`, `build`, lub `tools`.</span><span class="sxs-lookup"><span data-stu-id="a6395-350">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="a6395-351">Zobacz [tworzenie .nuspec z katalogu roboczego oparty na Konwencji](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="a6395-351">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="a6395-352">**exclude**</span><span class="sxs-lookup"><span data-stu-id="a6395-352">**exclude**</span></span> | <span data-ttu-id="a6395-353">Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a6395-353">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a6395-354">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="a6395-354">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="a6395-355">Przykłady</span><span class="sxs-lookup"><span data-stu-id="a6395-355">Examples</span></span>

<span data-ttu-id="a6395-356">**Pojedynczy zestaw**</span><span class="sxs-lookup"><span data-stu-id="a6395-356">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="a6395-357">**Pojedynczy zestaw specyficzne dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="a6395-357">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="a6395-358">**Zbiór bibliotek DLL, przy użyciu symboli wieloznacznych**</span><span class="sxs-lookup"><span data-stu-id="a6395-358">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="a6395-359">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="a6395-359">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="a6395-360">**Wykluczenie plików**</span><span class="sxs-lookup"><span data-stu-id="a6395-360">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="a6395-361">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="a6395-361">Including content files</span></span>

<span data-ttu-id="a6395-362">Pliki zawartości są niezmienne pliki, które pakietu musi zawierać się w projekcie.</span><span class="sxs-lookup"><span data-stu-id="a6395-362">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="a6395-363">Trwa niezmienne, nie mają one zostać zmodyfikowane przez konsumencki projektu.</span><span class="sxs-lookup"><span data-stu-id="a6395-363">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="a6395-364">Pliki zawartości przykład obejmują:</span><span class="sxs-lookup"><span data-stu-id="a6395-364">Example content files include:</span></span>

- <span data-ttu-id="a6395-365">Obrazy, które są osadzane jako zasoby</span><span class="sxs-lookup"><span data-stu-id="a6395-365">Images that are embedded as resources</span></span>
- <span data-ttu-id="a6395-366">Pliki źródłowe, które już są kompilowane</span><span class="sxs-lookup"><span data-stu-id="a6395-366">Source files that are already compiled</span></span>
- <span data-ttu-id="a6395-367">Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="a6395-367">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="a6395-368">Pliki konfiguracji dla pakietów, które należy uwzględnić w projekcie, ale nie ma potrzeby zmiany specyficzne dla projektu</span><span class="sxs-lookup"><span data-stu-id="a6395-368">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="a6395-369">Zawartość, pliki są zawarte w pakiecie przy użyciu `<files>` elementu, określając `content` folderu w `target` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a6395-369">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="a6395-370">Jednak takie pliki są ignorowane, gdy pakiet jest zainstalowany w projekcie przy użyciu funkcji PackageReference, który zamiast tego używa `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="a6395-370">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="a6395-371">Maksymalna zgodność z wykorzystywanie projektów pakietu najlepiej określa pliki zawartości w oba te elementy.</span><span class="sxs-lookup"><span data-stu-id="a6395-371">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="a6395-372">Za pomocą elementu plików dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="a6395-372">Using the files element for content files</span></span>

<span data-ttu-id="a6395-373">W przypadku plików zawartości, po prostu użyć tego samego formatu jak w przypadku plików zestawu jednak określić `content` jako podstawowy folder w `target` atrybutu, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="a6395-373">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="a6395-374">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="a6395-374">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="a6395-375">**Pliki zawartości przy użyciu struktury katalogów**</span><span class="sxs-lookup"><span data-stu-id="a6395-375">**Content files with directory structure**</span></span>

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

<span data-ttu-id="a6395-376">**Plik zawartości, które są specyficzne dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="a6395-376">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="a6395-377">**Skopiowany do folderu z dot w nazwie pliku zawartości**</span><span class="sxs-lookup"><span data-stu-id="a6395-377">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="a6395-378">W tym przypadku NuGet widzi, że rozszerzenie w `target` nie pasuje do rozszerzenia w `src` i w związku z tym traktuje tę część nazwy w `target` jako folder:</span><span class="sxs-lookup"><span data-stu-id="a6395-378">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="a6395-379">**Pliki zawartości, bez rozszerzenia**</span><span class="sxs-lookup"><span data-stu-id="a6395-379">**Content files without extensions**</span></span>

<span data-ttu-id="a6395-380">Aby dołączyć pliki bez rozszerzenia, należy użyć `*` lub `**` symboli wieloznacznych:</span><span class="sxs-lookup"><span data-stu-id="a6395-380">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="a6395-381">**Pliki zawartości głębokości ścieżki i głębokiego obiektem docelowym**</span><span class="sxs-lookup"><span data-stu-id="a6395-381">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="a6395-382">W tym przypadku ponieważ pasuje do rozszerzenia pliku źródłowego i docelowego, NuGet zakłada, że obiekt docelowy jest nazwa pliku, a nie folder:</span><span class="sxs-lookup"><span data-stu-id="a6395-382">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="a6395-383">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="a6395-383">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="a6395-384">**Wykluczenie plików**</span><span class="sxs-lookup"><span data-stu-id="a6395-384">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="a6395-385">Za pomocą elementu contentFiles dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="a6395-385">Using the contentFiles element for content files</span></span>

<span data-ttu-id="a6395-386">*NuGet 4.0 + przy użyciu funkcji PackageReference*</span><span class="sxs-lookup"><span data-stu-id="a6395-386">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="a6395-387">Domyślnie pakiet umieszcza zawartość `contentFiles` folder (patrz poniżej) i `nuget pack` uwzględnione wszystkie pliki w folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="a6395-387">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="a6395-388">W takim przypadku nie jest konieczne uwzględnienie `contentFiles` w węźle `.nuspec` wcale.</span><span class="sxs-lookup"><span data-stu-id="a6395-388">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="a6395-389">Do kontroli, które pliki są uwzględnione `<contentFiles>` element określa to zbiór `<files>` obejmują elementy, które identyfikują konkretne pliki.</span><span class="sxs-lookup"><span data-stu-id="a6395-389">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="a6395-390">Te pliki są określane za pomocą zestaw atrybutów, które opisują, jak powinna być używana w ramach systemu projektu:</span><span class="sxs-lookup"><span data-stu-id="a6395-390">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="a6395-391">Atrybut</span><span class="sxs-lookup"><span data-stu-id="a6395-391">Attribute</span></span> | <span data-ttu-id="a6395-392">Opis</span><span class="sxs-lookup"><span data-stu-id="a6395-392">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a6395-393">**include**</span><span class="sxs-lookup"><span data-stu-id="a6395-393">**include**</span></span> | <span data-ttu-id="a6395-394">(Wymagane) Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a6395-394">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a6395-395">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="a6395-395">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="a6395-396">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="a6395-396">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a6395-397">**exclude**</span><span class="sxs-lookup"><span data-stu-id="a6395-397">**exclude**</span></span> | <span data-ttu-id="a6395-398">Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a6395-398">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a6395-399">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="a6395-399">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a6395-400">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="a6395-400">**buildAction**</span></span> | <span data-ttu-id="a6395-401">Akcja kompilacji, aby przypisać do elementu zawartości dla platformy MSBuild, takich jak `Content`, `None`, `Embedded Resource`, `Compile`itp. Wartość domyślna to `Compile`.</span><span class="sxs-lookup"><span data-stu-id="a6395-401">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="a6395-402">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="a6395-402">**copyToOutput**</span></span> | <span data-ttu-id="a6395-403">Wartość Boolean wskazującą, czy chcesz skopiować elementy zawartości do kompilacji (lub opublikować) folder wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="a6395-403">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="a6395-404">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="a6395-404">The default is false.</span></span> |
| <span data-ttu-id="a6395-405">**spłaszczanie**</span><span class="sxs-lookup"><span data-stu-id="a6395-405">**flatten**</span></span> | <span data-ttu-id="a6395-406">Wartość logiczna wskazująca, czy skopiować elementy zawartości na pojedynczy folder w danych wyjściowych kompilacji (true) czy zachować strukturę folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="a6395-406">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="a6395-407">Ta flaga działa tylko, gdy copyToOutput flaga jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="a6395-407">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="a6395-408">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="a6395-408">The default is false.</span></span> |

<span data-ttu-id="a6395-409">Instalując pakiet NuGet dotyczy elementów podrzędnych `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="a6395-409">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="a6395-410">Jeśli wiele wpisów pasuje do tego samego pliku wszystkie wpisy są stosowane.</span><span class="sxs-lookup"><span data-stu-id="a6395-410">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="a6395-411">Wpis umieszczony najwyżej zastępuje wpisy niżej, jeśli występuje konflikt z tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a6395-411">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="a6395-412">Struktura folderów pakietu</span><span class="sxs-lookup"><span data-stu-id="a6395-412">Package folder structure</span></span>

<span data-ttu-id="a6395-413">Projekt pakietu powinien struktury zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="a6395-413">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="a6395-414">`codeLanguages` może być `cs`, `vb`, `fs`, `any`, lub litery odpowiednikiem danego `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="a6395-414">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="a6395-415">`TxM` jest dowolnym prawne krótka nazwa docelowej platformy obsługującej NuGet (zobacz [ustalać platformy docelowe](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="a6395-415">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="a6395-416">Dowolnej struktury folderów może być dołączany na końcu tej składni.</span><span class="sxs-lookup"><span data-stu-id="a6395-416">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="a6395-417">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a6395-417">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="a6395-418">Puste foldery można użyć `.` zrezygnować z dostarczanie zawartości dla niektórych kombinacji języka i TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="a6395-418">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="a6395-419">Sekcji z przykładowym pliki</span><span class="sxs-lookup"><span data-stu-id="a6395-419">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="a6395-420">Przykład .nuspec plików</span><span class="sxs-lookup"><span data-stu-id="a6395-420">Example .nuspec files</span></span>

<span data-ttu-id="a6395-421">**Prosty `.nuspec` nie określające zależności lub plików**</span><span class="sxs-lookup"><span data-stu-id="a6395-421">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="a6395-422">**A `.nuspec` z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="a6395-422">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="a6395-423">**A `.nuspec` z plikami**</span><span class="sxs-lookup"><span data-stu-id="a6395-423">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="a6395-424">**A `.nuspec` za pomocą zestawów framework**</span><span class="sxs-lookup"><span data-stu-id="a6395-424">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="a6395-425">W tym przykładzie poniżej są zainstalowane dla określonego projektu celów:</span><span class="sxs-lookup"><span data-stu-id="a6395-425">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="a6395-426">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="a6395-426">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="a6395-427">. NET4 -> Profil klienta `System.Net`</span><span class="sxs-lookup"><span data-stu-id="a6395-427">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="a6395-428">Program Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="a6395-428">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="a6395-429">Program Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="a6395-429">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="a6395-430">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="a6395-430">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
