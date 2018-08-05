---
title: Odwołanie do pliku .nuspec dla NuGet
description: Plik .nuspec zawiera metadane pakietów używane podczas tworzenia pakietu i do dostarczania informacji klientów pakietu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6d190d9fdb26d76fa8e46b7d283c1857cfab26e9
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508039"
---
# <a name="nuspec-reference"></a><span data-ttu-id="f2a33-103">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="f2a33-103">.nuspec reference</span></span>

<span data-ttu-id="f2a33-104">A `.nuspec` plik jest manifestu XML, który zawiera metadane pakietów.</span><span class="sxs-lookup"><span data-stu-id="f2a33-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="f2a33-105">Ten manifest służy do tworzenia pakietu i podaj informacje dla klientów.</span><span class="sxs-lookup"><span data-stu-id="f2a33-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="f2a33-106">Manifest zawsze znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="f2a33-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="f2a33-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="f2a33-107">In this topic:</span></span>

- [<span data-ttu-id="f2a33-108">Ogólna postać i schematu</span><span class="sxs-lookup"><span data-stu-id="f2a33-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="f2a33-109">[Zastąpienia tokenów](#replacement-tokens) (jeśli jest używana w projekcie programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f2a33-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="f2a33-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="f2a33-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="f2a33-111">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="f2a33-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="f2a33-112">Odwołania zestawu</span><span class="sxs-lookup"><span data-stu-id="f2a33-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="f2a33-113">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="f2a33-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="f2a33-114">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="f2a33-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="f2a33-115">Przykład nuspec plików</span><span class="sxs-lookup"><span data-stu-id="f2a33-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="f2a33-116">Ogólna postać i schematu</span><span class="sxs-lookup"><span data-stu-id="f2a33-116">General form and schema</span></span>

<span data-ttu-id="f2a33-117">Bieżący `nuspec.xsd` można znaleźć w pliku schematu [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="f2a33-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="f2a33-118">W tym schemacie `.nuspec` plik ma następującą postać ogólne:</span><span class="sxs-lookup"><span data-stu-id="f2a33-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="f2a33-119">Wizualnych reprezentacji schematu, otwórz plik schematu w programie Visual Studio w trybie projektowania, a następnie kliknij przycisk na **Eksploratora schematu XML** łącza.</span><span class="sxs-lookup"><span data-stu-id="f2a33-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="f2a33-120">Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz **Pokaż Eksploratora schematu XML**.</span><span class="sxs-lookup"><span data-stu-id="f2a33-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="f2a33-121">W obu przypadkach, uzyskasz widoku podobne do pokazanego poniżej (w przypadku większości rozwinięte):</span><span class="sxs-lookup"><span data-stu-id="f2a33-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Explorer schematu z nuspec.xsd Otwórz](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="f2a33-123">Atrybuty metadanych</span><span class="sxs-lookup"><span data-stu-id="f2a33-123">Metadata attributes</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="f2a33-124">Elementy wymagane metadane</span><span class="sxs-lookup"><span data-stu-id="f2a33-124">Required metadata elements</span></span>

<span data-ttu-id="f2a33-125">Mimo że następujące elementy są minimalne wymagania dotyczące pakietu, należy rozważyć dodanie [elementy opcjonalne metadane](#optional-metadata-elements) usprawniających atrakcyjniejsze środowisko pracy deweloperzy muszą z pakietem.</span><span class="sxs-lookup"><span data-stu-id="f2a33-125">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="f2a33-126">Te elementy muszą znajdować się w `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-126">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="f2a33-127">Element</span><span class="sxs-lookup"><span data-stu-id="f2a33-127">Element</span></span> | <span data-ttu-id="f2a33-128">Opis</span><span class="sxs-lookup"><span data-stu-id="f2a33-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2a33-129">**id**</span><span class="sxs-lookup"><span data-stu-id="f2a33-129">**id**</span></span> | <span data-ttu-id="f2a33-130">Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowa w witrynie nuget.org lub cokolwiek innego pakietu, który znajduje się w galerii.</span><span class="sxs-lookup"><span data-stu-id="f2a33-130">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="f2a33-131">Identyfikatory nie mogą zawierać spacji ani znaków, które nie są prawidłowe dla danego adresu URL i zazwyczaj korzystają z reguły w przestrzeni nazw .NET.</span><span class="sxs-lookup"><span data-stu-id="f2a33-131">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="f2a33-132">Zobacz [wybierając identyfikator unikatowy pakiet](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) wskazówki.</span><span class="sxs-lookup"><span data-stu-id="f2a33-132">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="f2a33-133">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="f2a33-133">**version**</span></span> | <span data-ttu-id="f2a33-134">Wersja pakietu, następujące *Wersja_główna.WERSJA_POMOCNICZA.poprawka* wzorca.</span><span class="sxs-lookup"><span data-stu-id="f2a33-134">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="f2a33-135">Numery wersji mogą zawierać sufiks wersji wstępnej, zgodnie z opisem w [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="f2a33-135">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="f2a33-136">**Opis elementu**</span><span class="sxs-lookup"><span data-stu-id="f2a33-136">**description**</span></span> | <span data-ttu-id="f2a33-137">Długi opis pakietu do wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2a33-137">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="f2a33-138">**Autorzy**</span><span class="sxs-lookup"><span data-stu-id="f2a33-138">**authors**</span></span> | <span data-ttu-id="f2a33-139">Rozdzielana przecinkami lista autorów pakietów, pasujące nazwy profilu w witrynie nuget.org. Te są wyświetlane w galerii pakietów NuGet w witrynie nuget.org i są odwoływania się do pakietów przez ten sam autorów.</span><span class="sxs-lookup"><span data-stu-id="f2a33-139">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="f2a33-140">Elementy opcjonalne metadane</span><span class="sxs-lookup"><span data-stu-id="f2a33-140">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="f2a33-141">Tytuł</span><span class="sxs-lookup"><span data-stu-id="f2a33-141">title</span></span>
<span data-ttu-id="f2a33-142">Tytuł przyjaznego dla człowieka pakietu, zwykle używanych w interfejsie użytkownika wyświetla w witrynach nuget.org i Menedżera pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2a33-142">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="f2a33-143">Jeśli nie zostanie określony, identyfikator pakietu jest używany.</span><span class="sxs-lookup"><span data-stu-id="f2a33-143">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="f2a33-144">Właściciele</span><span class="sxs-lookup"><span data-stu-id="f2a33-144">owners</span></span>
<span data-ttu-id="f2a33-145">Rozdzielana przecinkami lista twórców pakietów przy użyciu nazwy profilu w witrynie nuget.org. Jest to często tej samej listy podobnie jak w `authors`i jest ignorowana podczas przekazywania pakietu na stronie nuget.org. Zobacz [właścicieli pakietu zarządzania w witrynie nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="f2a33-145">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="f2a33-146">projectUrl</span><span class="sxs-lookup"><span data-stu-id="f2a33-146">projectUrl</span></span>
<span data-ttu-id="f2a33-147">Adres URL strony głównej pakietu, często wyświetlany w użytkownika, jak również adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f2a33-147">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="f2a33-148">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="f2a33-148">licenseUrl</span></span>
<span data-ttu-id="f2a33-149">Adres URL licencji pakietu, często wyświetlany w użytkownika, jak również adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f2a33-149">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="f2a33-150">IconUrl</span><span class="sxs-lookup"><span data-stu-id="f2a33-150">iconUrl</span></span>
<span data-ttu-id="f2a33-151">Adres URL obrazu 64 x 64 z przezroczystość tła do użycia jako ikona dla pakietu wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2a33-151">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="f2a33-152">Pamiętaj, że ten element zawiera *bezpośredni adres URL obrazu* a nie jej adres URL strony sieci web zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="f2a33-152">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="f2a33-153">Na przykład, aby użyć obrazu z witryny GitHub, należy użyć plik raw, takie jak adres URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="f2a33-153">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="f2a33-154">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f2a33-154">requireLicenseAcceptance</span></span>
<span data-ttu-id="f2a33-155">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-155">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="f2a33-156">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="f2a33-156">developmentDependency</span></span>
<span data-ttu-id="f2a33-157">*(2.8 +)*  Wartość logiczna określająca, czy pakiet jest oznaczone jako — tylko zależnością programistyczną, co zapobiega uwzględniane jako zależności w innych pakietach pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-157">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span>
#### <a name="summary"></a><span data-ttu-id="f2a33-158">podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f2a33-158">summary</span></span>
<span data-ttu-id="f2a33-159">Krótki opis pakietu do wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2a33-159">A short description of the package for UI display.</span></span> <span data-ttu-id="f2a33-160">Jeśli argument jest pominięty, skróconą wersję `description` jest używany.</span><span class="sxs-lookup"><span data-stu-id="f2a33-160">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="f2a33-161">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f2a33-161">releaseNotes</span></span>
<span data-ttu-id="f2a33-162">*(w wersji 1.5 +)*  Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak **aktualizacje** kartę z Menedżera pakietów Visual Studio zamiast opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-162">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="f2a33-163">informacji o prawach autorskich,</span><span class="sxs-lookup"><span data-stu-id="f2a33-163">copyright</span></span>
<span data-ttu-id="f2a33-164">*(w wersji 1.5 +)*  Copyright szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-164">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="f2a33-165">język</span><span class="sxs-lookup"><span data-stu-id="f2a33-165">language</span></span>
<span data-ttu-id="f2a33-166">Identyfikator ustawień regionalnych dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-166">The locale ID for the package.</span></span> <span data-ttu-id="f2a33-167">Zobacz [tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f2a33-167">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="f2a33-168">tagi</span><span class="sxs-lookup"><span data-stu-id="f2a33-168">tags</span></span>
<span data-ttu-id="f2a33-169">Rozdzielany spacjami lista tagów i słów kluczowych, które opisują możliwości pakietu i pomocy pakietów za pomocą wyszukiwania i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="f2a33-169">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="f2a33-170">zdatne do użytku</span><span class="sxs-lookup"><span data-stu-id="f2a33-170">serviceable</span></span> 
<span data-ttu-id="f2a33-171">*(3.3 +)*  NuGet wewnętrznego użytku tylko.</span><span class="sxs-lookup"><span data-stu-id="f2a33-171">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="f2a33-172">repozytorium</span><span class="sxs-lookup"><span data-stu-id="f2a33-172">repository</span></span>
<span data-ttu-id="f2a33-173">Metadane repozytorium, składający się z czterech atrybuty opcjonalne: *typu* i *adresu url* *(4.0 i nowsze)*, i *gałęzi* i  *zatwierdzenie* *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="f2a33-173">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="f2a33-174">Te atrybuty zezwalać na mapowanie .nupkg do repozytorium, którego kompilacja, z których można pobrać jak wyjaśniono, jak poszczególne gałęzi lub zatwierdzania, który skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="f2a33-174">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="f2a33-175">Powinna to być publicznie dostępnego adresu url, który może być wywoływany bezpośrednio przez oprogramowania do kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="f2a33-175">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="f2a33-176">Ponieważ jest on przeznaczony dla komputera nie powinna być strony html.</span><span class="sxs-lookup"><span data-stu-id="f2a33-176">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="f2a33-177">Łącze do strony projektu, użyj `projectUrl` pola zamiast. |</span><span class="sxs-lookup"><span data-stu-id="f2a33-177">For linking to project page, use the `projectUrl` field, instead.|</span></span>
#### <a name="minclientversion"></a><span data-ttu-id="f2a33-178">Atrybut MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="f2a33-178">minClientVersion</span></span>
<span data-ttu-id="f2a33-179">Określa minimalną wersję klienta NuGet, który można zainstalować ten pakiet, wymuszane przez nuget.exe oraz Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2a33-179">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="f2a33-180">Jest on używany zawsze wtedy, gdy pakiet jest zależny od określonych funkcji `.nuspec` plików, które zostały dodane w konkretnej wersji klienta programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="f2a33-180">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="f2a33-181">Na przykład pakiet przy użyciu `developmentDependency` atrybut należy określić "2.8" dla `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-181">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="f2a33-182">Podobnie, pakiet przy użyciu `contentFiles` (zobacz następną sekcję) należy ustawić element `minClientVersion` do "3.3".</span><span class="sxs-lookup"><span data-stu-id="f2a33-182">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="f2a33-183">Należy zauważyć, że ponieważ klienci programu NuGet przed 2.5 nie rozpoznają tej flagi należy ich *zawsze* odmówić można zainstalować pakietu, niezależnie od tego, co `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="f2a33-183">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="f2a33-184">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="f2a33-184">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="f2a33-185">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="f2a33-185">packageTypes</span></span>
<span data-ttu-id="f2a33-186">*(3.5 +)*  Zbiór zero lub więcej `<packageType>` elementów, określając typ pakietu, jeśli inne niż tradycyjne zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-186">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="f2a33-187">Każdy packageType ma atrybuty *nazwa* i *wersji*.</span><span class="sxs-lookup"><span data-stu-id="f2a33-187">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="f2a33-188">Zobacz [ustawienie typu pakietu](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="f2a33-188">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="f2a33-189">zależności</span><span class="sxs-lookup"><span data-stu-id="f2a33-189">dependencies</span></span>
<span data-ttu-id="f2a33-190">Kolekcja zero lub więcej `<dependency>` elementy określenie zależności dotyczących pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-190">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="f2a33-191">Poszczególne zależności ma atrybuty *identyfikator*, *wersji*, *obejmują* (3.x+) i *wykluczyć* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="f2a33-191">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="f2a33-192">Zobacz [zależności](#dependencies-element) poniżej.</span><span class="sxs-lookup"><span data-stu-id="f2a33-192">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="f2a33-193">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f2a33-193">frameworkAssemblies</span></span>
<span data-ttu-id="f2a33-194">*(1.2 +)*  Zbiór zero lub więcej `<frameworkAssembly>` elementów identyfikowanie odwołania do zestawów .NET Framework, które wymaga tego pakietu, dzięki któremu czy odwołania są dodawane do projektów, korzystanie z pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-194">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="f2a33-195">Została każda frameworkAssembly *assemblyName* i *targetFramework* atrybutów.</span><span class="sxs-lookup"><span data-stu-id="f2a33-195">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="f2a33-196">Zobacz [określenie zestawu struktury odwołuje się do globalnej pamięci podręcznej zestawów](#specifying-framework-assembly-references-gac) poniżej.</span><span class="sxs-lookup"><span data-stu-id="f2a33-196">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="f2a33-197">odwołania</span><span class="sxs-lookup"><span data-stu-id="f2a33-197">references</span></span>
<span data-ttu-id="f2a33-198">*(w wersji 1.5 +)*  Zbiór zero lub więcej `<reference>` elementy nazewnictwa zestawów, w tym pakiecie `lib` folderu, które są dodawane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-198">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="f2a33-199">Każde odwołanie zawiera *pliku* atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-199">Each reference has a *file* attribute.</span></span> <span data-ttu-id="f2a33-200">`<references>` może również zawierać `<group>` element z *targetFramework* atrybut, który następnie zawiera `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="f2a33-200">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="f2a33-201">Jeśli argument jest pominięty, wszystkie odwołania w `lib` są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="f2a33-201">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="f2a33-202">Zobacz [odwołania do zestawów jawne określenie](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="f2a33-202">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="f2a33-203">Pliki</span><span class="sxs-lookup"><span data-stu-id="f2a33-203">contentFiles</span></span>
<span data-ttu-id="f2a33-204">*(3.3 +)*  Zbiór `<files>` elementy, które identyfikują plików zawartości do uwzględnienia w projekcie odbierająca komunikaty.</span><span class="sxs-lookup"><span data-stu-id="f2a33-204">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="f2a33-205">Te pliki są określane przy użyciu zestawu atrybutów, które opisują, jak powinna być używana w ramach systemu projektu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-205">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="f2a33-206">Zobacz [określenie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej.</span><span class="sxs-lookup"><span data-stu-id="f2a33-206">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="f2a33-207">— pliki</span><span class="sxs-lookup"><span data-stu-id="f2a33-207">files</span></span> 
<span data-ttu-id="f2a33-208">`<package>` Węzeł może zawierać `<files>` węzeł jako element równorzędny do `<metadata>`, a lub `<contentFiles>` podrzędne w ramach `<metadata>`, aby określić, które pliki zestawu i zawartości do uwzględnienia w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="f2a33-208">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="f2a33-209">Zobacz [w tym pliki zestawu](#including-assembly-files) i [pliki zawartości w tym](#including-content-files) później w tym temacie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f2a33-209">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="f2a33-210">Zastąpienia tokenów</span><span class="sxs-lookup"><span data-stu-id="f2a33-210">Replacement tokens</span></span>

<span data-ttu-id="f2a33-211">Podczas tworzenia pakietu [ `nuget pack` polecenia](../tools/cli-ref-pack.md) zastępuje rozdzielonych $ tokenów w `.nuspec` pliku `<metadata>` węzła z wartości, które pochodzą z poziomu pliku projektu lub `pack` polecenia `-properties`przełącznika.</span><span class="sxs-lookup"><span data-stu-id="f2a33-211">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="f2a33-212">W wierszu polecenia określ wartości tokenu `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-212">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="f2a33-213">Na przykład takie jak możesz użyć tokenu `$owners$` i `$desc$` w `.nuspec` i podaj wartości w pakowania czasu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f2a33-213">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="f2a33-214">Aby użyć wartości z projektem, określ tokenów opisane w poniższej tabeli (AssemblyInfo odwołuje się do pliku w `Properties` takich jak `AssemblyInfo.cs` lub `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="f2a33-214">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="f2a33-215">Aby korzystać z tych tokenów, należy uruchomić `nuget pack` przy użyciu pliku projektu, a nie po prostu `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-215">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="f2a33-216">Na przykład przy użyciu następującego polecenia `$id$` i `$version$` tokenów w `.nuspec` pliku są zastępowane projektu `AssemblyName` i `AssemblyVersion` wartości:</span><span class="sxs-lookup"><span data-stu-id="f2a33-216">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="f2a33-217">Zazwyczaj w przypadku projektu tworzony `.nuspec` początkowo przy użyciu `nuget spec MyProject.csproj` automatycznie zawierający niektóre z tych tokenów standardowych.</span><span class="sxs-lookup"><span data-stu-id="f2a33-217">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="f2a33-218">Jednakże jeśli projekt nie ma wartości dla wymaganych `.nuspec` elementów, a następnie `nuget pack` zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="f2a33-218">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="f2a33-219">Ponadto w przypadku zmiany wartości projektu, upewnij się odbudować przed utworzeniem pakietu; Można to zrobić wygodna przy użyciu polecenia pakietu `build` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="f2a33-219">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="f2a33-220">Z wyjątkiem produktów `$configuration$`, wartości w projekcie są używane zamiast dowolne przypisane do tego samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f2a33-220">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="f2a33-221">Token</span><span class="sxs-lookup"><span data-stu-id="f2a33-221">Token</span></span> | <span data-ttu-id="f2a33-222">Wartość źródła</span><span class="sxs-lookup"><span data-stu-id="f2a33-222">Value source</span></span> | <span data-ttu-id="f2a33-223">Wartość</span><span class="sxs-lookup"><span data-stu-id="f2a33-223">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="f2a33-224">**$id$**</span><span class="sxs-lookup"><span data-stu-id="f2a33-224">**$id$**</span></span> | <span data-ttu-id="f2a33-225">plik projektu</span><span class="sxs-lookup"><span data-stu-id="f2a33-225">Project file</span></span> | <span data-ttu-id="f2a33-226">AssemblyName (tytuł) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="f2a33-226">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="f2a33-227">**$version$**</span><span class="sxs-lookup"><span data-stu-id="f2a33-227">**$version$**</span></span> | <span data-ttu-id="f2a33-228">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f2a33-228">AssemblyInfo</span></span> | <span data-ttu-id="f2a33-229">AssemblyInformationalVersion, jeśli jest obecna, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="f2a33-229">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="f2a33-230">**$author$**</span><span class="sxs-lookup"><span data-stu-id="f2a33-230">**$author$**</span></span> | <span data-ttu-id="f2a33-231">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f2a33-231">AssemblyInfo</span></span> | <span data-ttu-id="f2a33-232">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="f2a33-232">AssemblyCompany</span></span> |
| <span data-ttu-id="f2a33-233">**$title$**</span><span class="sxs-lookup"><span data-stu-id="f2a33-233">**$title$**</span></span> | <span data-ttu-id="f2a33-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f2a33-234">AssemblyInfo</span></span> | <span data-ttu-id="f2a33-235">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="f2a33-235">AssemblyTitle</span></span> |
| <span data-ttu-id="f2a33-236">**$description$**</span><span class="sxs-lookup"><span data-stu-id="f2a33-236">**$description$**</span></span> | <span data-ttu-id="f2a33-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f2a33-237">AssemblyInfo</span></span> | <span data-ttu-id="f2a33-238">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="f2a33-238">AssemblyDescription</span></span> |
| <span data-ttu-id="f2a33-239">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="f2a33-239">**$copyright$**</span></span> | <span data-ttu-id="f2a33-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="f2a33-240">AssemblyInfo</span></span> | <span data-ttu-id="f2a33-241">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="f2a33-241">AssemblyCopyright</span></span> |
| <span data-ttu-id="f2a33-242">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="f2a33-242">**$configuration$**</span></span> | <span data-ttu-id="f2a33-243">Zestaw bibliotek DLL</span><span class="sxs-lookup"><span data-stu-id="f2a33-243">Assembly DLL</span></span> | <span data-ttu-id="f2a33-244">Konfiguracja używana do tworzenia zestawu, domyślnie używany do debugowania.</span><span class="sxs-lookup"><span data-stu-id="f2a33-244">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="f2a33-245">Należy pamiętać, że aby utworzyć pakiet za pomocą konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f2a33-245">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="f2a33-246">Tokeny, również może służyć do rozpoznawania ścieżek, po włączeniu [plików zestawu](#including-assembly-files) i [zawartości plików](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="f2a33-246">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="f2a33-247">Tokeny mają takie same nazwy właściwości programu MSBuild, dzięki czemu można wybrać pliki do uwzględnienia w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f2a33-247">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="f2a33-248">Na przykład, jeśli używasz następujące generatory kodów w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="f2a33-248">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="f2a33-249">I kompilowania zestawu którego `AssemblyName` jest `LoggingLibrary` z `Release` konfiguracji w programie MSBuild, a wiersze wynikowe `.nuspec` plik w pakiecie znajduje się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f2a33-249">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="f2a33-250">Element zależności</span><span class="sxs-lookup"><span data-stu-id="f2a33-250">Dependencies element</span></span>

<span data-ttu-id="f2a33-251">`<dependencies>` Elemencie `<metadata>` zawiera dowolną liczbę `<dependency>` elementy, które identyfikują innych pakietów, od których zależy Pakiet najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-251">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="f2a33-252">Atrybuty dla każdego `<dependency>` są następujące:</span><span class="sxs-lookup"><span data-stu-id="f2a33-252">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="f2a33-253">Atrybut</span><span class="sxs-lookup"><span data-stu-id="f2a33-253">Attribute</span></span> | <span data-ttu-id="f2a33-254">Opis</span><span class="sxs-lookup"><span data-stu-id="f2a33-254">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="f2a33-255">(Wymagane) Identyfikator pakietu zależności, takie jak "EntityFramework" i "NUnit", czyli nazwy nuget.org pakietu zawiera strona pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-255">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="f2a33-256">(Wymagane) Zakres wersji dopuszczalne jako zależność.</span><span class="sxs-lookup"><span data-stu-id="f2a33-256">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="f2a33-257">Zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards) dla określonej składni.</span><span class="sxs-lookup"><span data-stu-id="f2a33-257">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="f2a33-258">include</span><span class="sxs-lookup"><span data-stu-id="f2a33-258">include</span></span> | <span data-ttu-id="f2a33-259">Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności do uwzględnienia w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="f2a33-259">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="f2a33-260">Wartość domyślna to `none`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-260">The default value is `none`.</span></span> |
| <span data-ttu-id="f2a33-261">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="f2a33-261">exclude</span></span> | <span data-ttu-id="f2a33-262">Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności, które mają zostać wykluczone w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="f2a33-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="f2a33-263">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-263">The  default value is `all`.</span></span> <span data-ttu-id="f2a33-264">Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-264">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="f2a33-265">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-265">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="f2a33-266">Uwzględnianie/wykluczanie znaczników</span><span class="sxs-lookup"><span data-stu-id="f2a33-266">Include/Exclude tag</span></span> | <span data-ttu-id="f2a33-267">Odpowiednie foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="f2a33-267">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="f2a33-268">Pliki</span><span class="sxs-lookup"><span data-stu-id="f2a33-268">contentFiles</span></span> | <span data-ttu-id="f2a33-269">Zawartość</span><span class="sxs-lookup"><span data-stu-id="f2a33-269">Content</span></span> |
| <span data-ttu-id="f2a33-270">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="f2a33-270">runtime</span></span> | <span data-ttu-id="f2a33-271">Środowisko uruchomieniowe, zasobów i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f2a33-271">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="f2a33-272">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="f2a33-272">compile</span></span> | <span data-ttu-id="f2a33-273">lib</span><span class="sxs-lookup"><span data-stu-id="f2a33-273">lib</span></span> |
| <span data-ttu-id="f2a33-274">kompilacja</span><span class="sxs-lookup"><span data-stu-id="f2a33-274">build</span></span> | <span data-ttu-id="f2a33-275">Kompilacja (cele i właściwości programu MSBuild)</span><span class="sxs-lookup"><span data-stu-id="f2a33-275">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="f2a33-276">natywne</span><span class="sxs-lookup"><span data-stu-id="f2a33-276">native</span></span> | <span data-ttu-id="f2a33-277">natywne</span><span class="sxs-lookup"><span data-stu-id="f2a33-277">native</span></span> |
| <span data-ttu-id="f2a33-278">brak</span><span class="sxs-lookup"><span data-stu-id="f2a33-278">none</span></span> | <span data-ttu-id="f2a33-279">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="f2a33-279">No folders</span></span> |
| <span data-ttu-id="f2a33-280">wszystkie</span><span class="sxs-lookup"><span data-stu-id="f2a33-280">all</span></span> | <span data-ttu-id="f2a33-281">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="f2a33-281">All folders</span></span> |

<span data-ttu-id="f2a33-282">Na przykład następujące wiersze wskazywać zależności na `PackageA` wersji 1.1.0 lub nowszej, a `PackageB` wersji 1.x.</span><span class="sxs-lookup"><span data-stu-id="f2a33-282">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="f2a33-283">Następujące wiersze wskazują zależności na te same pakiety, ale określono jako uwzględniane `contentFiles` i `build` folderów `PackageA` i wszystko, ale `native` i `compile` folderów `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="f2a33-283">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="f2a33-284">Uwaga: Podczas tworzenia `.nuspec` projektu używającego `nuget spec`, zależności, które istnieją w tym projekcie są automatycznie uwzględniane w wynikowym `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="f2a33-284">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="f2a33-285">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="f2a33-285">Dependency groups</span></span>

<span data-ttu-id="f2a33-286">*W wersji 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="f2a33-286">*Version 2.0+*</span></span>

<span data-ttu-id="f2a33-287">Jako alternatywy dla pojedynczego płaskiej listy, można określić zależności zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-287">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="f2a33-288">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów.</span><span class="sxs-lookup"><span data-stu-id="f2a33-288">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="f2a33-289">Te zależności są instalowane razem, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-289">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="f2a33-290">`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listę zależności.</span><span class="sxs-lookup"><span data-stu-id="f2a33-290">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="f2a33-291">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="f2a33-291">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="f2a33-292">Nie można się zmieszać format grupy z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="f2a33-292">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="f2a33-293">W poniższym przykładzie pokazano różnych odmian `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="f2a33-293">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="f2a33-294">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="f2a33-294">Explicit assembly references</span></span>

<span data-ttu-id="f2a33-295">`<references>` Element jawnie określa zestawy, które projekt docelowy powinny odwoływać się przy użyciu pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-295">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="f2a33-296">Gdy ten element jest obecny, NuGet dodać odwołania do tylko zestawy wymienionych; nie powoduje dodania odwołania do innych zestawów, w tym pakiecie `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-296">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="f2a33-297">Na przykład następująca `<references>` elementu powoduje, że rozszerzenie NuGet, aby dodać odwołania do tylko `xunit.dll` i `xunit.extensions.dll` nawet, jeśli istnieją dodatkowe zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="f2a33-297">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="f2a33-298">Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="f2a33-298">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="f2a33-299">Korzystając z [kontrakty kodu](/dotnet/framework/debug-trace-profile/code-contracts), na przykład zestawy umowy muszą być obok zestawów środowiska uruchomieniowego, które mogą rozszerzyć, aby je znaleźć programu Visual Studio, ale zestawy kontraktu nie musi być przywoływanego przez projekt lub skopiowany w projekcie `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-299">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="f2a33-300">Podobnie jawnych odwołań może służyć do struktur testów jednostek, takich jak XUnit, którą jej narzędzi, zestawy znajdujące się obok zestawów środowiska uruchomieniowego, ale nie wymaga dołączeni ich jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-300">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="f2a33-301">Grupy odwołań</span><span class="sxs-lookup"><span data-stu-id="f2a33-301">Reference groups</span></span>

<span data-ttu-id="f2a33-302">Alternatywą dla pojedynczego płaskiej listy odwołania można określić zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<references>`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-302">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="f2a33-303">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="f2a33-303">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="f2a33-304">Te odwołania są dodawane do projektu, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-304">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="f2a33-305">`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listy odwołań.</span><span class="sxs-lookup"><span data-stu-id="f2a33-305">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="f2a33-306">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="f2a33-306">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="f2a33-307">Nie można się zmieszać format grupy z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="f2a33-307">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="f2a33-308">W poniższym przykładzie pokazano różnych odmian `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="f2a33-308">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="f2a33-309">Odwołania zestawu</span><span class="sxs-lookup"><span data-stu-id="f2a33-309">Framework assembly references</span></span>

<span data-ttu-id="f2a33-310">Zestawy struktury są te, które są częścią programu .NET framework i powinien już znajdować się w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej podanej maszyny.</span><span class="sxs-lookup"><span data-stu-id="f2a33-310">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="f2a33-311">Identyfikując te zestawy w ramach `<frameworkAssemblies>` elementu pakietu można upewnij się, że wymagane odwołania są dodawane do projektu, w przypadku, gdy projekt nie ma już odwołania te.</span><span class="sxs-lookup"><span data-stu-id="f2a33-311">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="f2a33-312">Takie zestawy oczywiście nie są uwzględnione w pakiecie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="f2a33-312">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="f2a33-313">`<frameworkAssemblies>` Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="f2a33-313">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="f2a33-314">Atrybut</span><span class="sxs-lookup"><span data-stu-id="f2a33-314">Attribute</span></span> | <span data-ttu-id="f2a33-315">Opis</span><span class="sxs-lookup"><span data-stu-id="f2a33-315">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2a33-316">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="f2a33-316">**assemblyName**</span></span> | <span data-ttu-id="f2a33-317">(Wymagane) W pełni kwalifikowanej nazwy zestawu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-317">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="f2a33-318">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="f2a33-318">**targetFramework**</span></span> | <span data-ttu-id="f2a33-319">(Opcjonalnie) Określa platformę docelową, której dotyczy odwołanie.</span><span class="sxs-lookup"><span data-stu-id="f2a33-319">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="f2a33-320">Jeśli argument jest pominięty, wskazuje, że odwołanie ma zastosowanie do wszystkich środowisk.</span><span class="sxs-lookup"><span data-stu-id="f2a33-320">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="f2a33-321">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="f2a33-321">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="f2a33-322">W poniższym przykładzie pokazano odwołanie do `System.Net` dla wszystkich docelowych struktur i odwołania do `System.ServiceModel` dla programu .NET Framework 4.0 tylko:</span><span class="sxs-lookup"><span data-stu-id="f2a33-322">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="f2a33-323">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="f2a33-323">Including assembly files</span></span>

<span data-ttu-id="f2a33-324">Jeśli stosujesz konwencje opisanego w [Tworzenie pakietu](../create-packages/creating-a-package.md), nie trzeba jawnie określić listę plików w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="f2a33-324">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="f2a33-325">`nuget pack` Polecenia automatycznie przejmuje on niezbędne pliki.</span><span class="sxs-lookup"><span data-stu-id="f2a33-325">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="f2a33-326">Po zainstalowaniu do projektu pakiet NuGet automatycznie dodaje odwołania do zestawów do pakietu biblioteki dll, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie.</span><span class="sxs-lookup"><span data-stu-id="f2a33-326">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="f2a33-327">Z tego powodu należy unikać `.resources.dll` dla plików, w przeciwnym razie zawierające kod essential pakietu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-327">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="f2a33-328">Aby pominąć to zachowanie automatyczne i jawnie kontrolować pliki, które są umieszczone w pakiecie, umieść `<files>` element jako element podrzędny elementu `<package>` (i element równorzędny `<metadata>`), identyfikowanie poszczególnych plików za pomocą oddzielnego `<file>` elementu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-328">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="f2a33-329">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f2a33-329">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="f2a33-330">Nuget 2.x i starszych i projektów za pomocą `packages.config`, `<files>` element umożliwia również dołączać niezmienne pliki zawartości, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="f2a33-330">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="f2a33-331">Za pomocą narzędzi NuGet 3.3 + i projekty PackageReference `<contentFiles>` element jest używany zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f2a33-331">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="f2a33-332">Zobacz [pliki zawartości w tym](#including-content-files) poniżej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f2a33-332">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="f2a33-333">Atrybuty elementu pliku</span><span class="sxs-lookup"><span data-stu-id="f2a33-333">File element attributes</span></span>

<span data-ttu-id="f2a33-334">Każdy `<file>` element określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="f2a33-334">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="f2a33-335">Atrybut</span><span class="sxs-lookup"><span data-stu-id="f2a33-335">Attribute</span></span> | <span data-ttu-id="f2a33-336">Opis</span><span class="sxs-lookup"><span data-stu-id="f2a33-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2a33-337">**src**</span><span class="sxs-lookup"><span data-stu-id="f2a33-337">**src**</span></span> | <span data-ttu-id="f2a33-338">Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-338">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="f2a33-339">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="f2a33-339">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="f2a33-340">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="f2a33-340">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f2a33-341">**Docelowy**</span><span class="sxs-lookup"><span data-stu-id="f2a33-341">**target**</span></span> | <span data-ttu-id="f2a33-342">Względna ścieżka do folderu, w pakiecie, gdzie są umieszczone pliki źródłowe, musi zaczynać się od `lib`, `content`, `build`, lub `tools`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-342">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="f2a33-343">Zobacz [tworzenie .nuspec z katalogu roboczego oparty na Konwencji](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="f2a33-343">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="f2a33-344">**exclude**</span><span class="sxs-lookup"><span data-stu-id="f2a33-344">**exclude**</span></span> | <span data-ttu-id="f2a33-345">Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f2a33-345">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="f2a33-346">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="f2a33-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="f2a33-347">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f2a33-347">Examples</span></span>

<span data-ttu-id="f2a33-348">**Pojedynczy zestaw**</span><span class="sxs-lookup"><span data-stu-id="f2a33-348">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="f2a33-349">**Pojedynczy zestaw specyficzne dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="f2a33-349">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="f2a33-350">**Zbiór bibliotek DLL, przy użyciu symboli wieloznacznych**</span><span class="sxs-lookup"><span data-stu-id="f2a33-350">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="f2a33-351">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="f2a33-351">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="f2a33-352">**Wykluczenie plików**</span><span class="sxs-lookup"><span data-stu-id="f2a33-352">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="f2a33-353">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="f2a33-353">Including content files</span></span>

<span data-ttu-id="f2a33-354">Pliki zawartości są niezmienne pliki, które pakietu musi zawierać się w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f2a33-354">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="f2a33-355">Trwa niezmienne, nie mają one zostać zmodyfikowane przez konsumencki projektu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-355">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="f2a33-356">Pliki zawartości przykład obejmują:</span><span class="sxs-lookup"><span data-stu-id="f2a33-356">Example content files include:</span></span>

- <span data-ttu-id="f2a33-357">Obrazy, które są osadzane jako zasoby</span><span class="sxs-lookup"><span data-stu-id="f2a33-357">Images that are embedded as resources</span></span>
- <span data-ttu-id="f2a33-358">Pliki źródłowe, które już są kompilowane</span><span class="sxs-lookup"><span data-stu-id="f2a33-358">Source files that are already compiled</span></span>
- <span data-ttu-id="f2a33-359">Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="f2a33-359">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="f2a33-360">Pliki konfiguracji dla pakietów, które należy uwzględnić w projekcie, ale nie ma potrzeby zmiany specyficzne dla projektu</span><span class="sxs-lookup"><span data-stu-id="f2a33-360">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="f2a33-361">Zawartość, pliki są zawarte w pakiecie przy użyciu `<files>` elementu, określając `content` folderu w `target` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-361">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="f2a33-362">Jednak takie pliki są ignorowane, gdy pakiet jest zainstalowany w projekcie przy użyciu funkcji PackageReference, który zamiast tego używa `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-362">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="f2a33-363">Maksymalna zgodność z wykorzystywanie projektów pakietu najlepiej określa pliki zawartości w oba te elementy.</span><span class="sxs-lookup"><span data-stu-id="f2a33-363">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="f2a33-364">Za pomocą elementu plików dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="f2a33-364">Using the files element for content files</span></span>

<span data-ttu-id="f2a33-365">W przypadku plików zawartości, po prostu użyć tego samego formatu jak w przypadku plików zestawu jednak określić `content` jako podstawowy folder w `target` atrybutu, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="f2a33-365">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="f2a33-366">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="f2a33-366">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="f2a33-367">**Pliki zawartości przy użyciu struktury katalogów**</span><span class="sxs-lookup"><span data-stu-id="f2a33-367">**Content files with directory structure**</span></span>

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

<span data-ttu-id="f2a33-368">**Plik zawartości, które są specyficzne dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="f2a33-368">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="f2a33-369">**Skopiowany do folderu z dot w nazwie pliku zawartości**</span><span class="sxs-lookup"><span data-stu-id="f2a33-369">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="f2a33-370">W tym przypadku NuGet widzi, że rozszerzenie w `target` nie pasuje do rozszerzenia w `src` i w związku z tym traktuje tę część nazwy w `target` jako folder:</span><span class="sxs-lookup"><span data-stu-id="f2a33-370">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="f2a33-371">**Pliki zawartości, bez rozszerzenia**</span><span class="sxs-lookup"><span data-stu-id="f2a33-371">**Content files without extensions**</span></span>

<span data-ttu-id="f2a33-372">Aby dołączyć pliki bez rozszerzenia, należy użyć `*` lub `**` symboli wieloznacznych:</span><span class="sxs-lookup"><span data-stu-id="f2a33-372">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="f2a33-373">**Pliki zawartości głębokości ścieżki i głębokiego obiektem docelowym**</span><span class="sxs-lookup"><span data-stu-id="f2a33-373">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="f2a33-374">W tym przypadku ponieważ pasuje do rozszerzenia pliku źródłowego i docelowego, NuGet zakłada, że obiekt docelowy jest nazwa pliku, a nie folder:</span><span class="sxs-lookup"><span data-stu-id="f2a33-374">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="f2a33-375">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="f2a33-375">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="f2a33-376">**Wykluczenie plików**</span><span class="sxs-lookup"><span data-stu-id="f2a33-376">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="f2a33-377">Za pomocą elementu contentFiles dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="f2a33-377">Using the contentFiles element for content files</span></span>

<span data-ttu-id="f2a33-378">*NuGet 4.0 + przy użyciu funkcji PackageReference*</span><span class="sxs-lookup"><span data-stu-id="f2a33-378">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="f2a33-379">Domyślnie pakiet umieszcza zawartość `contentFiles` folder (patrz poniżej) i `nuget pack` uwzględnione wszystkie pliki w folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="f2a33-379">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="f2a33-380">W takim przypadku nie jest konieczne uwzględnienie `contentFiles` w węźle `.nuspec` wcale.</span><span class="sxs-lookup"><span data-stu-id="f2a33-380">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="f2a33-381">Do kontroli, które pliki są uwzględnione `<contentFiles>` element określa to zbiór `<files>` obejmują elementy, które identyfikują konkretne pliki.</span><span class="sxs-lookup"><span data-stu-id="f2a33-381">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="f2a33-382">Te pliki są określane za pomocą zestaw atrybutów, które opisują, jak powinna być używana w ramach systemu projektu:</span><span class="sxs-lookup"><span data-stu-id="f2a33-382">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="f2a33-383">Atrybut</span><span class="sxs-lookup"><span data-stu-id="f2a33-383">Attribute</span></span> | <span data-ttu-id="f2a33-384">Opis</span><span class="sxs-lookup"><span data-stu-id="f2a33-384">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2a33-385">**include**</span><span class="sxs-lookup"><span data-stu-id="f2a33-385">**include**</span></span> | <span data-ttu-id="f2a33-386">(Wymagane) Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-386">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="f2a33-387">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="f2a33-387">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="f2a33-388">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="f2a33-388">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f2a33-389">**exclude**</span><span class="sxs-lookup"><span data-stu-id="f2a33-389">**exclude**</span></span> | <span data-ttu-id="f2a33-390">Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f2a33-390">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="f2a33-391">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="f2a33-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="f2a33-392">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="f2a33-392">**buildAction**</span></span> | <span data-ttu-id="f2a33-393">Akcja kompilacji, aby przypisać do elementu zawartości dla platformy MSBuild, takich jak `Content`, `None`, `Embedded Resource`, `Compile`itp. Wartość domyślna to `Compile`.</span><span class="sxs-lookup"><span data-stu-id="f2a33-393">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="f2a33-394">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="f2a33-394">**copyToOutput**</span></span> | <span data-ttu-id="f2a33-395">Wartość Boolean wskazującą, czy chcesz skopiować elementy zawartości do kompilacji (lub opublikować) folder wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="f2a33-395">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="f2a33-396">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="f2a33-396">The default is false.</span></span> |
| <span data-ttu-id="f2a33-397">**spłaszczanie**</span><span class="sxs-lookup"><span data-stu-id="f2a33-397">**flatten**</span></span> | <span data-ttu-id="f2a33-398">Wartość logiczna wskazująca, czy skopiować elementy zawartości na pojedynczy folder w danych wyjściowych kompilacji (true) czy zachować strukturę folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="f2a33-398">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="f2a33-399">Ta flaga działa tylko, gdy copyToOutput flaga jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="f2a33-399">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="f2a33-400">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="f2a33-400">The default is false.</span></span> |

<span data-ttu-id="f2a33-401">Instalując pakiet NuGet dotyczy elementów podrzędnych `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-401">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="f2a33-402">Jeśli wiele wpisów pasuje do tego samego pliku wszystkie wpisy są stosowane.</span><span class="sxs-lookup"><span data-stu-id="f2a33-402">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="f2a33-403">Wpis umieszczony najwyżej zastępuje wpisy niżej, jeśli występuje konflikt z tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f2a33-403">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="f2a33-404">Struktura folderów pakietu</span><span class="sxs-lookup"><span data-stu-id="f2a33-404">Package folder structure</span></span>

<span data-ttu-id="f2a33-405">Projekt pakietu powinien struktury zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="f2a33-405">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="f2a33-406">`codeLanguages` może być `cs`, `vb`, `fs`, `any`, lub litery odpowiednikiem danego `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="f2a33-406">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="f2a33-407">`TxM` jest dowolnym prawne krótka nazwa docelowej platformy obsługującej NuGet (zobacz [ustalać platformy docelowe](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="f2a33-407">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="f2a33-408">Dowolnej struktury folderów może być dołączany na końcu tej składni.</span><span class="sxs-lookup"><span data-stu-id="f2a33-408">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="f2a33-409">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f2a33-409">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="f2a33-410">Puste foldery można użyć `.` zrezygnować z dostarczanie zawartości dla niektórych kombinacji języka i TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="f2a33-410">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="f2a33-411">Sekcji z przykładowym pliki</span><span class="sxs-lookup"><span data-stu-id="f2a33-411">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="f2a33-412">Przykład nuspec plików</span><span class="sxs-lookup"><span data-stu-id="f2a33-412">Example nuspec files</span></span>

<span data-ttu-id="f2a33-413">**Prosty `.nuspec` nie określające zależności lub plików**</span><span class="sxs-lookup"><span data-stu-id="f2a33-413">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="f2a33-414">**A `.nuspec` z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="f2a33-414">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="f2a33-415">**A `.nuspec` z plikami**</span><span class="sxs-lookup"><span data-stu-id="f2a33-415">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="f2a33-416">**A `.nuspec` za pomocą zestawów framework**</span><span class="sxs-lookup"><span data-stu-id="f2a33-416">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="f2a33-417">W tym przykładzie poniżej są zainstalowane dla określonego projektu celów:</span><span class="sxs-lookup"><span data-stu-id="f2a33-417">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="f2a33-418">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="f2a33-418">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="f2a33-419">. NET4 -> Profil klienta `System.Net`</span><span class="sxs-lookup"><span data-stu-id="f2a33-419">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="f2a33-420">Program Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="f2a33-420">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="f2a33-421">Program Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="f2a33-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="f2a33-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="f2a33-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
