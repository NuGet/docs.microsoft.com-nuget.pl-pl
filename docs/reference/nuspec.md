---
title: Odwołanie do pliku .nuspec dla NuGet
description: Plik .nuspec zawiera metadane pakietów używane podczas tworzenia pakietu i do dostarczania informacji klientów pakietu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 110d1aa29fc7238f1a82c1a81ec6431dfe437420
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020456"
---
# <a name="nuspec-reference"></a><span data-ttu-id="d3db5-103">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="d3db5-103">.nuspec reference</span></span>

<span data-ttu-id="d3db5-104">A `.nuspec` plik jest manifestu XML, który zawiera metadane pakietów.</span><span class="sxs-lookup"><span data-stu-id="d3db5-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="d3db5-105">Ten manifest służy do tworzenia pakietu i podaj informacje dla klientów.</span><span class="sxs-lookup"><span data-stu-id="d3db5-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="d3db5-106">Manifest zawsze znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="d3db5-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="d3db5-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="d3db5-107">In this topic:</span></span>

- [<span data-ttu-id="d3db5-108">Ogólna postać i schematu</span><span class="sxs-lookup"><span data-stu-id="d3db5-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="d3db5-109">[Zastąpienia tokenów](#replacement-tokens) (jeśli jest używana w projekcie programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d3db5-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="d3db5-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="d3db5-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="d3db5-111">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="d3db5-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="d3db5-112">Odwołania zestawu</span><span class="sxs-lookup"><span data-stu-id="d3db5-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="d3db5-113">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="d3db5-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="d3db5-114">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="d3db5-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="d3db5-115">Przykład nuspec plików</span><span class="sxs-lookup"><span data-stu-id="d3db5-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="d3db5-116">Ogólna postać i schematu</span><span class="sxs-lookup"><span data-stu-id="d3db5-116">General form and schema</span></span>

<span data-ttu-id="d3db5-117">Bieżący `nuspec.xsd` można znaleźć w pliku schematu [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="d3db5-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="d3db5-118">W tym schemacie `.nuspec` plik ma następującą postać ogólne:</span><span class="sxs-lookup"><span data-stu-id="d3db5-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="d3db5-119">Wizualnych reprezentacji schematu, otwórz plik schematu w programie Visual Studio w trybie projektowania, a następnie kliknij przycisk na **Eksploratora schematu XML** łącza.</span><span class="sxs-lookup"><span data-stu-id="d3db5-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="d3db5-120">Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz **Pokaż Eksploratora schematu XML**.</span><span class="sxs-lookup"><span data-stu-id="d3db5-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="d3db5-121">W obu przypadkach, uzyskasz widoku podobne do pokazanego poniżej (w przypadku większości rozwinięte):</span><span class="sxs-lookup"><span data-stu-id="d3db5-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Explorer schematu z nuspec.xsd Otwórz](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="d3db5-123">Elementy wymagane metadane</span><span class="sxs-lookup"><span data-stu-id="d3db5-123">Required metadata elements</span></span>

<span data-ttu-id="d3db5-124">Mimo że następujące elementy są minimalne wymagania dotyczące pakietu, należy rozważyć dodanie [elementy opcjonalne metadane](#optional-metadata-elements) usprawniających atrakcyjniejsze środowisko pracy deweloperzy muszą z pakietem.</span><span class="sxs-lookup"><span data-stu-id="d3db5-124">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="d3db5-125">Te elementy muszą znajdować się w `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-125">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="d3db5-126">identyfikator</span><span class="sxs-lookup"><span data-stu-id="d3db5-126">id</span></span> 
<span data-ttu-id="d3db5-127">Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowa w witrynie nuget.org lub cokolwiek innego pakietu, który znajduje się w galerii.</span><span class="sxs-lookup"><span data-stu-id="d3db5-127">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="d3db5-128">Identyfikatory nie mogą zawierać spacji ani znaków, które nie są prawidłowe dla danego adresu URL i zazwyczaj korzystają z reguły w przestrzeni nazw .NET.</span><span class="sxs-lookup"><span data-stu-id="d3db5-128">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="d3db5-129">Zobacz [wybierając identyfikator unikatowy pakiet](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) wskazówki.</span><span class="sxs-lookup"><span data-stu-id="d3db5-129">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> <span data-ttu-id="d3db5-130">### Wersja pakietu, następujące *Wersja_główna.WERSJA_POMOCNICZA.poprawka* wzorca.</span><span class="sxs-lookup"><span data-stu-id="d3db5-130">#### version The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="d3db5-131">Numery wersji mogą zawierać sufiks wersji wstępnej, zgodnie z opisem w [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="d3db5-131">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="d3db5-132">opis</span><span class="sxs-lookup"><span data-stu-id="d3db5-132">description</span></span>
<span data-ttu-id="d3db5-133">Długi opis pakietu do wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d3db5-133">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="d3db5-134">Autorzy</span><span class="sxs-lookup"><span data-stu-id="d3db5-134">authors</span></span>
<span data-ttu-id="d3db5-135">Rozdzielana przecinkami lista autorów pakietów, pasujące nazwy profilu w witrynie nuget.org. Te są wyświetlane w galerii pakietów NuGet w witrynie nuget.org i są odwoływania się do pakietów przez ten sam autorów.</span><span class="sxs-lookup"><span data-stu-id="d3db5-135">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="d3db5-136">Elementy opcjonalne metadane</span><span class="sxs-lookup"><span data-stu-id="d3db5-136">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="d3db5-137">Tytuł</span><span class="sxs-lookup"><span data-stu-id="d3db5-137">title</span></span>
<span data-ttu-id="d3db5-138">Tytuł przyjaznego dla człowieka pakietu, zwykle używanych w interfejsie użytkownika wyświetla w witrynach nuget.org i Menedżera pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3db5-138">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="d3db5-139">Jeśli nie zostanie określony, identyfikator pakietu jest używany.</span><span class="sxs-lookup"><span data-stu-id="d3db5-139">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="d3db5-140">Właściciele</span><span class="sxs-lookup"><span data-stu-id="d3db5-140">owners</span></span>
<span data-ttu-id="d3db5-141">Rozdzielana przecinkami lista twórców pakietów przy użyciu nazwy profilu w witrynie nuget.org. Jest to często tej samej listy podobnie jak w `authors`i jest ignorowana podczas przekazywania pakietu na stronie nuget.org. Zobacz [właścicieli pakietu zarządzania w witrynie nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="d3db5-141">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="d3db5-142">projectUrl</span><span class="sxs-lookup"><span data-stu-id="d3db5-142">projectUrl</span></span>
<span data-ttu-id="d3db5-143">Adres URL strony głównej pakietu, często wyświetlany w użytkownika, jak również adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d3db5-143">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="d3db5-144">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="d3db5-144">licenseUrl</span></span>
<span data-ttu-id="d3db5-145">Adres URL licencji pakietu, często wyświetlany w użytkownika, jak również adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d3db5-145">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="d3db5-146">IconUrl</span><span class="sxs-lookup"><span data-stu-id="d3db5-146">iconUrl</span></span>
<span data-ttu-id="d3db5-147">Adres URL obrazu 64 x 64 z przezroczystość tła do użycia jako ikona dla pakietu wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d3db5-147">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="d3db5-148">Pamiętaj, że ten element zawiera *bezpośredni adres URL obrazu* a nie jej adres URL strony sieci web zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="d3db5-148">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="d3db5-149">Na przykład, aby użyć obrazu z witryny GitHub, należy użyć plik raw, takie jak adres URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="d3db5-149">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="d3db5-150">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d3db5-150">requireLicenseAcceptance</span></span>
<span data-ttu-id="d3db5-151">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-151">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="d3db5-152">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="d3db5-152">developmentDependency</span></span>
<span data-ttu-id="d3db5-153">*(2.8 +) * Wartość logiczna określająca, czy pakiet jest oznaczone jako — tylko zależnością programistyczną, co zapobiega uwzględniane jako zależności w innych pakietach pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-153">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span>
#### <a name="summary"></a><span data-ttu-id="d3db5-154">podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d3db5-154">summary</span></span>
<span data-ttu-id="d3db5-155">Krótki opis pakietu do wyświetlania w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d3db5-155">A short description of the package for UI display.</span></span> <span data-ttu-id="d3db5-156">Jeśli argument jest pominięty, skróconą wersję `description` jest używany.</span><span class="sxs-lookup"><span data-stu-id="d3db5-156">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="d3db5-157">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d3db5-157">releaseNotes</span></span>
<span data-ttu-id="d3db5-158">*(w wersji 1.5 +) * Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak **aktualizacje** kartę z Menedżera pakietów Visual Studio zamiast opisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-158">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="d3db5-159">informacji o prawach autorskich,</span><span class="sxs-lookup"><span data-stu-id="d3db5-159">copyright</span></span>
<span data-ttu-id="d3db5-160">*(w wersji 1.5 +) * Copyright szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-160">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="d3db5-161">język</span><span class="sxs-lookup"><span data-stu-id="d3db5-161">language</span></span>
<span data-ttu-id="d3db5-162">Identyfikator ustawień regionalnych dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-162">The locale ID for the package.</span></span> <span data-ttu-id="d3db5-163">Zobacz [tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d3db5-163">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="d3db5-164">tagi</span><span class="sxs-lookup"><span data-stu-id="d3db5-164">tags</span></span>
<span data-ttu-id="d3db5-165">Rozdzielany spacjami lista tagów i słów kluczowych, które opisują możliwości pakietu i pomocy pakietów za pomocą wyszukiwania i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="d3db5-165">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="d3db5-166">zdatne do użytku</span><span class="sxs-lookup"><span data-stu-id="d3db5-166">serviceable</span></span> 
<span data-ttu-id="d3db5-167">*(3.3 +) * NuGet wewnętrznego użytku tylko.</span><span class="sxs-lookup"><span data-stu-id="d3db5-167">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="d3db5-168">repozytorium</span><span class="sxs-lookup"><span data-stu-id="d3db5-168">repository</span></span>
<span data-ttu-id="d3db5-169">Metadane repozytorium, składający się z czterech atrybuty opcjonalne: *typu* i *adresu url* *(4.0 i nowsze)*, i *gałęzi* i *zatwierdzenie* *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="d3db5-169">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="d3db5-170">Te atrybuty zezwalać na mapowanie .nupkg do repozytorium, którego kompilacja, z których można pobrać jak wyjaśniono, jak poszczególne gałęzi lub zatwierdzania, który skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="d3db5-170">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="d3db5-171">Powinna to być publicznie dostępnego adresu url, który może być wywoływany bezpośrednio przez oprogramowania do kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="d3db5-171">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="d3db5-172">Ponieważ jest on przeznaczony dla komputera nie powinna być strony html.</span><span class="sxs-lookup"><span data-stu-id="d3db5-172">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="d3db5-173">Łącze do strony projektu, użyj `projectUrl` pola zamiast. |</span><span class="sxs-lookup"><span data-stu-id="d3db5-173">For linking to project page, use the `projectUrl` field, instead.|</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="d3db5-174">Atrybut MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="d3db5-174">minClientVersion</span></span>
<span data-ttu-id="d3db5-175">Określa minimalną wersję klienta NuGet, który można zainstalować ten pakiet, wymuszane przez nuget.exe oraz Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3db5-175">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="d3db5-176">Jest on używany zawsze wtedy, gdy pakiet jest zależny od określonych funkcji `.nuspec` plików, które zostały dodane w konkretnej wersji klienta programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3db5-176">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="d3db5-177">Na przykład pakiet przy użyciu `developmentDependency` atrybut należy określić "2.8" dla `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-177">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="d3db5-178">Podobnie, pakiet przy użyciu `contentFiles` (zobacz następną sekcję) należy ustawić element `minClientVersion` do "3.3".</span><span class="sxs-lookup"><span data-stu-id="d3db5-178">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="d3db5-179">Należy zauważyć, że ponieważ klienci programu NuGet przed 2.5 nie rozpoznają tej flagi należy ich *zawsze* odmówić można zainstalować pakietu, niezależnie od tego, co `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="d3db5-179">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="d3db5-180">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="d3db5-180">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="d3db5-181">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="d3db5-181">packageTypes</span></span>
<span data-ttu-id="d3db5-182">*(3.5 +) * Zbiór zero lub więcej `<packageType>` elementów, określając typ pakietu, jeśli inne niż tradycyjne zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-182">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="d3db5-183">Każdy packageType ma atrybuty *nazwa* i *wersji*.</span><span class="sxs-lookup"><span data-stu-id="d3db5-183">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="d3db5-184">Zobacz [ustawienie typu pakietu](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="d3db5-184">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="d3db5-185">zależności</span><span class="sxs-lookup"><span data-stu-id="d3db5-185">dependencies</span></span>
<span data-ttu-id="d3db5-186">Kolekcja zero lub więcej `<dependency>` elementy określenie zależności dotyczących pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-186">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="d3db5-187">Poszczególne zależności ma atrybuty *identyfikator*, *wersji*, *obejmują* (3.x+) i *wykluczyć* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="d3db5-187">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="d3db5-188">Zobacz [zależności](#dependencies-element) poniżej.</span><span class="sxs-lookup"><span data-stu-id="d3db5-188">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="d3db5-189">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d3db5-189">frameworkAssemblies</span></span>
<span data-ttu-id="d3db5-190">*(1.2 +) * Zbiór zero lub więcej `<frameworkAssembly>` elementów identyfikowanie odwołania do zestawów .NET Framework, które wymaga tego pakietu, dzięki któremu czy odwołania są dodawane do projektów, korzystanie z pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-190">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="d3db5-191">Została każda frameworkAssembly *assemblyName* i *targetFramework* atrybutów.</span><span class="sxs-lookup"><span data-stu-id="d3db5-191">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="d3db5-192">Zobacz [określenie zestawu struktury odwołuje się do globalnej pamięci podręcznej zestawów](#specifying-framework-assembly-references-gac) poniżej.</span><span class="sxs-lookup"><span data-stu-id="d3db5-192">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="d3db5-193">odwołania</span><span class="sxs-lookup"><span data-stu-id="d3db5-193">references</span></span>
<span data-ttu-id="d3db5-194">*(w wersji 1.5 +) * Zbiór zero lub więcej `<reference>` elementy nazewnictwa zestawów, w tym pakiecie `lib` folderu, które są dodawane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-194">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="d3db5-195">Każde odwołanie zawiera *pliku* atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-195">Each reference has a *file* attribute.</span></span> <span data-ttu-id="d3db5-196">`<references>` może również zawierać `<group>` element z *targetFramework* atrybut, który następnie zawiera `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="d3db5-196">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="d3db5-197">Jeśli argument jest pominięty, wszystkie odwołania w `lib` są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="d3db5-197">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="d3db5-198">Zobacz [odwołania do zestawów jawne określenie](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="d3db5-198">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="d3db5-199">Pliki</span><span class="sxs-lookup"><span data-stu-id="d3db5-199">contentFiles</span></span>
<span data-ttu-id="d3db5-200">*(3.3 +) * Zbiór `<files>` elementy, które identyfikują plików zawartości do uwzględnienia w projekcie odbierająca komunikaty.</span><span class="sxs-lookup"><span data-stu-id="d3db5-200">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="d3db5-201">Te pliki są określane przy użyciu zestawu atrybutów, które opisują, jak powinna być używana w ramach systemu projektu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-201">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="d3db5-202">Zobacz [określenie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej.</span><span class="sxs-lookup"><span data-stu-id="d3db5-202">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="d3db5-203">— pliki</span><span class="sxs-lookup"><span data-stu-id="d3db5-203">files</span></span> 
<span data-ttu-id="d3db5-204">`<package>` Węzeł może zawierać `<files>` węzeł jako element równorzędny do `<metadata>`, a lub `<contentFiles>` podrzędne w ramach `<metadata>`, aby określić, które pliki zestawu i zawartości do uwzględnienia w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="d3db5-204">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="d3db5-205">Zobacz [w tym pliki zestawu](#including-assembly-files) i [pliki zawartości w tym](#including-content-files) później w tym temacie, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d3db5-205">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="d3db5-206">Zastąpienia tokenów</span><span class="sxs-lookup"><span data-stu-id="d3db5-206">Replacement tokens</span></span>

<span data-ttu-id="d3db5-207">Podczas tworzenia pakietu [ `nuget pack` polecenia](../tools/cli-ref-pack.md) zastępuje rozdzielonych $ tokenów w `.nuspec` pliku `<metadata>` węzła z wartości, które pochodzą z poziomu pliku projektu lub `pack` polecenia `-properties`przełącznika.</span><span class="sxs-lookup"><span data-stu-id="d3db5-207">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="d3db5-208">W wierszu polecenia określ wartości tokenu `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-208">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="d3db5-209">Na przykład takie jak możesz użyć tokenu `$owners$` i `$desc$` w `.nuspec` i podaj wartości w pakowania czasu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d3db5-209">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="d3db5-210">Aby użyć wartości z projektem, określ tokenów opisane w poniższej tabeli (AssemblyInfo odwołuje się do pliku w `Properties` takich jak `AssemblyInfo.cs` lub `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="d3db5-210">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="d3db5-211">Aby korzystać z tych tokenów, należy uruchomić `nuget pack` przy użyciu pliku projektu, a nie po prostu `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-211">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="d3db5-212">Na przykład przy użyciu następującego polecenia `$id$` i `$version$` tokenów w `.nuspec` pliku są zastępowane projektu `AssemblyName` i `AssemblyVersion` wartości:</span><span class="sxs-lookup"><span data-stu-id="d3db5-212">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="d3db5-213">Zazwyczaj w przypadku projektu tworzony `.nuspec` początkowo przy użyciu `nuget spec MyProject.csproj` automatycznie zawierający niektóre z tych tokenów standardowych.</span><span class="sxs-lookup"><span data-stu-id="d3db5-213">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="d3db5-214">Jednakże jeśli projekt nie ma wartości dla wymaganych `.nuspec` elementów, a następnie `nuget pack` zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d3db5-214">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="d3db5-215">Ponadto w przypadku zmiany wartości projektu, upewnij się odbudować przed utworzeniem pakietu; Można to zrobić wygodna przy użyciu polecenia pakietu `build` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="d3db5-215">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="d3db5-216">Z wyjątkiem produktów `$configuration$`, wartości w projekcie są używane zamiast dowolne przypisane do tego samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d3db5-216">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="d3db5-217">Token</span><span class="sxs-lookup"><span data-stu-id="d3db5-217">Token</span></span> | <span data-ttu-id="d3db5-218">Wartość źródła</span><span class="sxs-lookup"><span data-stu-id="d3db5-218">Value source</span></span> | <span data-ttu-id="d3db5-219">Wartość</span><span class="sxs-lookup"><span data-stu-id="d3db5-219">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="d3db5-220">**$id$**</span><span class="sxs-lookup"><span data-stu-id="d3db5-220">**$id$**</span></span> | <span data-ttu-id="d3db5-221">plik projektu</span><span class="sxs-lookup"><span data-stu-id="d3db5-221">Project file</span></span> | <span data-ttu-id="d3db5-222">AssemblyName (tytuł) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="d3db5-222">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="d3db5-223">**$version$**</span><span class="sxs-lookup"><span data-stu-id="d3db5-223">**$version$**</span></span> | <span data-ttu-id="d3db5-224">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d3db5-224">AssemblyInfo</span></span> | <span data-ttu-id="d3db5-225">AssemblyInformationalVersion, jeśli jest obecna, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="d3db5-225">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="d3db5-226">**$author$**</span><span class="sxs-lookup"><span data-stu-id="d3db5-226">**$author$**</span></span> | <span data-ttu-id="d3db5-227">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d3db5-227">AssemblyInfo</span></span> | <span data-ttu-id="d3db5-228">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="d3db5-228">AssemblyCompany</span></span> |
| <span data-ttu-id="d3db5-229">**$title$**</span><span class="sxs-lookup"><span data-stu-id="d3db5-229">**$title$**</span></span> | <span data-ttu-id="d3db5-230">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d3db5-230">AssemblyInfo</span></span> | <span data-ttu-id="d3db5-231">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="d3db5-231">AssemblyTitle</span></span> |
| <span data-ttu-id="d3db5-232">**$description$**</span><span class="sxs-lookup"><span data-stu-id="d3db5-232">**$description$**</span></span> | <span data-ttu-id="d3db5-233">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d3db5-233">AssemblyInfo</span></span> | <span data-ttu-id="d3db5-234">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="d3db5-234">AssemblyDescription</span></span> |
| <span data-ttu-id="d3db5-235">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="d3db5-235">**$copyright$**</span></span> | <span data-ttu-id="d3db5-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d3db5-236">AssemblyInfo</span></span> | <span data-ttu-id="d3db5-237">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="d3db5-237">AssemblyCopyright</span></span> |
| <span data-ttu-id="d3db5-238">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="d3db5-238">**$configuration$**</span></span> | <span data-ttu-id="d3db5-239">Zestaw bibliotek DLL</span><span class="sxs-lookup"><span data-stu-id="d3db5-239">Assembly DLL</span></span> | <span data-ttu-id="d3db5-240">Konfiguracja używana do tworzenia zestawu, domyślnie używany do debugowania.</span><span class="sxs-lookup"><span data-stu-id="d3db5-240">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="d3db5-241">Należy pamiętać, że aby utworzyć pakiet za pomocą konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d3db5-241">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="d3db5-242">Tokeny, również może służyć do rozpoznawania ścieżek, po włączeniu [plików zestawu](#including-assembly-files) i [zawartości plików](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="d3db5-242">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="d3db5-243">Tokeny mają takie same nazwy właściwości programu MSBuild, dzięki czemu można wybrać pliki do uwzględnienia w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d3db5-243">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="d3db5-244">Na przykład, jeśli używasz następujące generatory kodów w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="d3db5-244">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="d3db5-245">I kompilowania zestawu którego `AssemblyName` jest `LoggingLibrary` z `Release` konfiguracji w programie MSBuild, a wiersze wynikowe `.nuspec` plik w pakiecie znajduje się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d3db5-245">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="d3db5-246">Element zależności</span><span class="sxs-lookup"><span data-stu-id="d3db5-246">Dependencies element</span></span>

<span data-ttu-id="d3db5-247">`<dependencies>` Elemencie `<metadata>` zawiera dowolną liczbę `<dependency>` elementy, które identyfikują innych pakietów, od których zależy Pakiet najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-247">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="d3db5-248">Atrybuty dla każdego `<dependency>` są następujące:</span><span class="sxs-lookup"><span data-stu-id="d3db5-248">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="d3db5-249">Atrybut</span><span class="sxs-lookup"><span data-stu-id="d3db5-249">Attribute</span></span> | <span data-ttu-id="d3db5-250">Opis</span><span class="sxs-lookup"><span data-stu-id="d3db5-250">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="d3db5-251">(Wymagane) Identyfikator pakietu zależności, takie jak "EntityFramework" i "NUnit", czyli nazwy nuget.org pakietu zawiera strona pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-251">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="d3db5-252">(Wymagane) Zakres wersji dopuszczalne jako zależność.</span><span class="sxs-lookup"><span data-stu-id="d3db5-252">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="d3db5-253">Zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards) dla określonej składni.</span><span class="sxs-lookup"><span data-stu-id="d3db5-253">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="d3db5-254">include</span><span class="sxs-lookup"><span data-stu-id="d3db5-254">include</span></span> | <span data-ttu-id="d3db5-255">Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności do uwzględnienia w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="d3db5-255">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="d3db5-256">Wartość domyślna to `none`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-256">The default value is `none`.</span></span> |
| <span data-ttu-id="d3db5-257">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="d3db5-257">exclude</span></span> | <span data-ttu-id="d3db5-258">Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności, które mają zostać wykluczone w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="d3db5-258">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="d3db5-259">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-259">The  default value is `all`.</span></span> <span data-ttu-id="d3db5-260">Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-260">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="d3db5-261">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-261">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="d3db5-262">Uwzględnianie/wykluczanie znaczników</span><span class="sxs-lookup"><span data-stu-id="d3db5-262">Include/Exclude tag</span></span> | <span data-ttu-id="d3db5-263">Odpowiednie foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="d3db5-263">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="d3db5-264">Pliki</span><span class="sxs-lookup"><span data-stu-id="d3db5-264">contentFiles</span></span> | <span data-ttu-id="d3db5-265">Zawartość</span><span class="sxs-lookup"><span data-stu-id="d3db5-265">Content</span></span> |
| <span data-ttu-id="d3db5-266">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="d3db5-266">runtime</span></span> | <span data-ttu-id="d3db5-267">Środowisko uruchomieniowe, zasobów i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="d3db5-267">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="d3db5-268">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="d3db5-268">compile</span></span> | <span data-ttu-id="d3db5-269">lib</span><span class="sxs-lookup"><span data-stu-id="d3db5-269">lib</span></span> |
| <span data-ttu-id="d3db5-270">kompilacja</span><span class="sxs-lookup"><span data-stu-id="d3db5-270">build</span></span> | <span data-ttu-id="d3db5-271">Kompilacja (cele i właściwości programu MSBuild)</span><span class="sxs-lookup"><span data-stu-id="d3db5-271">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="d3db5-272">natywne</span><span class="sxs-lookup"><span data-stu-id="d3db5-272">native</span></span> | <span data-ttu-id="d3db5-273">natywne</span><span class="sxs-lookup"><span data-stu-id="d3db5-273">native</span></span> |
| <span data-ttu-id="d3db5-274">brak</span><span class="sxs-lookup"><span data-stu-id="d3db5-274">none</span></span> | <span data-ttu-id="d3db5-275">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="d3db5-275">No folders</span></span> |
| <span data-ttu-id="d3db5-276">wszystkie</span><span class="sxs-lookup"><span data-stu-id="d3db5-276">all</span></span> | <span data-ttu-id="d3db5-277">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="d3db5-277">All folders</span></span> |

<span data-ttu-id="d3db5-278">Na przykład następujące wiersze wskazywać zależności na `PackageA` wersji 1.1.0 lub nowszej, a `PackageB` wersji 1.x.</span><span class="sxs-lookup"><span data-stu-id="d3db5-278">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="d3db5-279">Następujące wiersze wskazują zależności na te same pakiety, ale określono jako uwzględniane `contentFiles` i `build` folderów `PackageA` i wszystko, ale `native` i `compile` folderów `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="d3db5-279">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="d3db5-280">Uwaga: Podczas tworzenia `.nuspec` projektu używającego `nuget spec`, zależności, które istnieją w tym projekcie są automatycznie uwzględniane w wynikowym `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="d3db5-280">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="d3db5-281">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="d3db5-281">Dependency groups</span></span>

<span data-ttu-id="d3db5-282">*W wersji 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="d3db5-282">*Version 2.0+*</span></span>

<span data-ttu-id="d3db5-283">Jako alternatywy dla pojedynczego płaskiej listy, można określić zależności zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-283">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="d3db5-284">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów.</span><span class="sxs-lookup"><span data-stu-id="d3db5-284">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="d3db5-285">Te zależności są instalowane razem, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-285">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d3db5-286">`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listę zależności.</span><span class="sxs-lookup"><span data-stu-id="d3db5-286">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="d3db5-287">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="d3db5-287">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d3db5-288">Nie można się zmieszać format grupy z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="d3db5-288">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d3db5-289">W poniższym przykładzie pokazano różnych odmian `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="d3db5-289">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="d3db5-290">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="d3db5-290">Explicit assembly references</span></span>

<span data-ttu-id="d3db5-291">`<references>` Element jawnie określa zestawy, które projekt docelowy powinny odwoływać się przy użyciu pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-291">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="d3db5-292">Gdy ten element jest obecny, NuGet dodać odwołania do tylko zestawy wymienionych; nie powoduje dodania odwołania do innych zestawów, w tym pakiecie `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-292">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="d3db5-293">Na przykład następująca `<references>` elementu powoduje, że rozszerzenie NuGet, aby dodać odwołania do tylko `xunit.dll` i `xunit.extensions.dll` nawet, jeśli istnieją dodatkowe zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="d3db5-293">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="d3db5-294">Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="d3db5-294">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="d3db5-295">Korzystając z [kontrakty kodu](/dotnet/framework/debug-trace-profile/code-contracts), na przykład zestawy umowy muszą być obok zestawów środowiska uruchomieniowego, które mogą rozszerzyć, aby je znaleźć programu Visual Studio, ale zestawy kontraktu nie musi być przywoływanego przez projekt lub skopiowany w projekcie `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-295">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="d3db5-296">Podobnie jawnych odwołań może służyć do struktur testów jednostek, takich jak XUnit, którą jej narzędzi, zestawy znajdujące się obok zestawów środowiska uruchomieniowego, ale nie wymaga dołączeni ich jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-296">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="d3db5-297">Grupy odwołań</span><span class="sxs-lookup"><span data-stu-id="d3db5-297">Reference groups</span></span>

<span data-ttu-id="d3db5-298">Alternatywą dla pojedynczego płaskiej listy odwołania można określić zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<references>`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-298">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="d3db5-299">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="d3db5-299">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="d3db5-300">Te odwołania są dodawane do projektu, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-300">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="d3db5-301">`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listy odwołań.</span><span class="sxs-lookup"><span data-stu-id="d3db5-301">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="d3db5-302">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="d3db5-302">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="d3db5-303">Nie można się zmieszać format grupy z płaską listą.</span><span class="sxs-lookup"><span data-stu-id="d3db5-303">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="d3db5-304">W poniższym przykładzie pokazano różnych odmian `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="d3db5-304">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="d3db5-305">Odwołania zestawu</span><span class="sxs-lookup"><span data-stu-id="d3db5-305">Framework assembly references</span></span>

<span data-ttu-id="d3db5-306">Zestawy struktury są te, które są częścią programu .NET framework i powinien już znajdować się w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej podanej maszyny.</span><span class="sxs-lookup"><span data-stu-id="d3db5-306">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="d3db5-307">Identyfikując te zestawy w ramach `<frameworkAssemblies>` elementu pakietu można upewnij się, że wymagane odwołania są dodawane do projektu, w przypadku, gdy projekt nie ma już odwołania te.</span><span class="sxs-lookup"><span data-stu-id="d3db5-307">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="d3db5-308">Takie zestawy oczywiście nie są uwzględnione w pakiecie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="d3db5-308">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="d3db5-309">`<frameworkAssemblies>` Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="d3db5-309">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="d3db5-310">Atrybut</span><span class="sxs-lookup"><span data-stu-id="d3db5-310">Attribute</span></span> | <span data-ttu-id="d3db5-311">Opis</span><span class="sxs-lookup"><span data-stu-id="d3db5-311">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3db5-312">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="d3db5-312">**assemblyName**</span></span> | <span data-ttu-id="d3db5-313">(Wymagane) W pełni kwalifikowanej nazwy zestawu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-313">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="d3db5-314">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="d3db5-314">**targetFramework**</span></span> | <span data-ttu-id="d3db5-315">(Opcjonalnie) Określa platformę docelową, której dotyczy odwołanie.</span><span class="sxs-lookup"><span data-stu-id="d3db5-315">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="d3db5-316">Jeśli argument jest pominięty, wskazuje, że odwołanie ma zastosowanie do wszystkich środowisk.</span><span class="sxs-lookup"><span data-stu-id="d3db5-316">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="d3db5-317">Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.</span><span class="sxs-lookup"><span data-stu-id="d3db5-317">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="d3db5-318">W poniższym przykładzie pokazano odwołanie do `System.Net` dla wszystkich docelowych struktur i odwołania do `System.ServiceModel` dla programu .NET Framework 4.0 tylko:</span><span class="sxs-lookup"><span data-stu-id="d3db5-318">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="d3db5-319">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="d3db5-319">Including assembly files</span></span>

<span data-ttu-id="d3db5-320">Jeśli stosujesz konwencje opisanego w [Tworzenie pakietu](../create-packages/creating-a-package.md), nie trzeba jawnie określić listę plików w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="d3db5-320">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="d3db5-321">`nuget pack` Polecenia automatycznie przejmuje on niezbędne pliki.</span><span class="sxs-lookup"><span data-stu-id="d3db5-321">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="d3db5-322">Po zainstalowaniu do projektu pakiet NuGet automatycznie dodaje odwołania do zestawów do pakietu biblioteki dll, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie.</span><span class="sxs-lookup"><span data-stu-id="d3db5-322">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="d3db5-323">Z tego powodu należy unikać `.resources.dll` dla plików, w przeciwnym razie zawierające kod essential pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-323">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="d3db5-324">Aby pominąć to zachowanie automatyczne i jawnie kontrolować pliki, które są umieszczone w pakiecie, umieść `<files>` element jako element podrzędny elementu `<package>` (i element równorzędny `<metadata>`), identyfikowanie poszczególnych plików za pomocą oddzielnego `<file>` elementu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-324">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="d3db5-325">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d3db5-325">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="d3db5-326">Nuget 2.x i starszych i projektów za pomocą `packages.config`, `<files>` element umożliwia również dołączać niezmienne pliki zawartości, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="d3db5-326">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="d3db5-327">Za pomocą narzędzi NuGet 3.3 + i projekty PackageReference `<contentFiles>` element jest używany zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="d3db5-327">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="d3db5-328">Zobacz [pliki zawartości w tym](#including-content-files) poniżej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d3db5-328">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="d3db5-329">Atrybuty elementu pliku</span><span class="sxs-lookup"><span data-stu-id="d3db5-329">File element attributes</span></span>

<span data-ttu-id="d3db5-330">Każdy `<file>` element określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="d3db5-330">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="d3db5-331">Atrybut</span><span class="sxs-lookup"><span data-stu-id="d3db5-331">Attribute</span></span> | <span data-ttu-id="d3db5-332">Opis</span><span class="sxs-lookup"><span data-stu-id="d3db5-332">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3db5-333">**src**</span><span class="sxs-lookup"><span data-stu-id="d3db5-333">**src**</span></span> | <span data-ttu-id="d3db5-334">Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-334">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d3db5-335">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="d3db5-335">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d3db5-336">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="d3db5-336">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d3db5-337">**Docelowy**</span><span class="sxs-lookup"><span data-stu-id="d3db5-337">**target**</span></span> | <span data-ttu-id="d3db5-338">Względna ścieżka do folderu, w pakiecie, gdzie są umieszczone pliki źródłowe, musi zaczynać się od `lib`, `content`, `build`, lub `tools`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-338">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="d3db5-339">Zobacz [tworzenie .nuspec z katalogu roboczego oparty na Konwencji](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="d3db5-339">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="d3db5-340">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d3db5-340">**exclude**</span></span> | <span data-ttu-id="d3db5-341">Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d3db5-341">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d3db5-342">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="d3db5-342">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="d3db5-343">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d3db5-343">Examples</span></span>

<span data-ttu-id="d3db5-344">**Pojedynczy zestaw**</span><span class="sxs-lookup"><span data-stu-id="d3db5-344">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="d3db5-345">**Pojedynczy zestaw specyficzne dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="d3db5-345">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="d3db5-346">**Zbiór bibliotek DLL, przy użyciu symboli wieloznacznych**</span><span class="sxs-lookup"><span data-stu-id="d3db5-346">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="d3db5-347">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="d3db5-347">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="d3db5-348">**Wykluczenie plików**</span><span class="sxs-lookup"><span data-stu-id="d3db5-348">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="d3db5-349">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="d3db5-349">Including content files</span></span>

<span data-ttu-id="d3db5-350">Pliki zawartości są niezmienne pliki, które pakietu musi zawierać się w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d3db5-350">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="d3db5-351">Trwa niezmienne, nie mają one zostać zmodyfikowane przez konsumencki projektu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-351">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="d3db5-352">Pliki zawartości przykład obejmują:</span><span class="sxs-lookup"><span data-stu-id="d3db5-352">Example content files include:</span></span>

- <span data-ttu-id="d3db5-353">Obrazy, które są osadzane jako zasoby</span><span class="sxs-lookup"><span data-stu-id="d3db5-353">Images that are embedded as resources</span></span>
- <span data-ttu-id="d3db5-354">Pliki źródłowe, które już są kompilowane</span><span class="sxs-lookup"><span data-stu-id="d3db5-354">Source files that are already compiled</span></span>
- <span data-ttu-id="d3db5-355">Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="d3db5-355">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="d3db5-356">Pliki konfiguracji dla pakietów, które należy uwzględnić w projekcie, ale nie ma potrzeby zmiany specyficzne dla projektu</span><span class="sxs-lookup"><span data-stu-id="d3db5-356">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="d3db5-357">Zawartość, pliki są zawarte w pakiecie przy użyciu `<files>` elementu, określając `content` folderu w `target` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-357">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="d3db5-358">Jednak takie pliki są ignorowane, gdy pakiet jest zainstalowany w projekcie przy użyciu funkcji PackageReference, który zamiast tego używa `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-358">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="d3db5-359">Maksymalna zgodność z wykorzystywanie projektów pakietu najlepiej określa pliki zawartości w oba te elementy.</span><span class="sxs-lookup"><span data-stu-id="d3db5-359">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="d3db5-360">Za pomocą elementu plików dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="d3db5-360">Using the files element for content files</span></span>

<span data-ttu-id="d3db5-361">W przypadku plików zawartości, po prostu użyć tego samego formatu jak w przypadku plików zestawu jednak określić `content` jako podstawowy folder w `target` atrybutu, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="d3db5-361">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="d3db5-362">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="d3db5-362">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="d3db5-363">**Pliki zawartości przy użyciu struktury katalogów**</span><span class="sxs-lookup"><span data-stu-id="d3db5-363">**Content files with directory structure**</span></span>

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

<span data-ttu-id="d3db5-364">**Plik zawartości, które są specyficzne dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="d3db5-364">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="d3db5-365">**Skopiowany do folderu z dot w nazwie pliku zawartości**</span><span class="sxs-lookup"><span data-stu-id="d3db5-365">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="d3db5-366">W tym przypadku NuGet widzi, że rozszerzenie w `target` nie pasuje do rozszerzenia w `src` i w związku z tym traktuje tę część nazwy w `target` jako folder:</span><span class="sxs-lookup"><span data-stu-id="d3db5-366">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="d3db5-367">**Pliki zawartości, bez rozszerzenia**</span><span class="sxs-lookup"><span data-stu-id="d3db5-367">**Content files without extensions**</span></span>

<span data-ttu-id="d3db5-368">Aby dołączyć pliki bez rozszerzenia, należy użyć `*` lub `**` symboli wieloznacznych:</span><span class="sxs-lookup"><span data-stu-id="d3db5-368">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="d3db5-369">**Pliki zawartości głębokości ścieżki i głębokiego obiektem docelowym**</span><span class="sxs-lookup"><span data-stu-id="d3db5-369">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="d3db5-370">W tym przypadku ponieważ pasuje do rozszerzenia pliku źródłowego i docelowego, NuGet zakłada, że obiekt docelowy jest nazwa pliku, a nie folder:</span><span class="sxs-lookup"><span data-stu-id="d3db5-370">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="d3db5-371">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="d3db5-371">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="d3db5-372">**Wykluczenie plików**</span><span class="sxs-lookup"><span data-stu-id="d3db5-372">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="d3db5-373">Za pomocą elementu contentFiles dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="d3db5-373">Using the contentFiles element for content files</span></span>

<span data-ttu-id="d3db5-374">*NuGet 4.0 + przy użyciu funkcji PackageReference*</span><span class="sxs-lookup"><span data-stu-id="d3db5-374">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="d3db5-375">Domyślnie pakiet umieszcza zawartość `contentFiles` folder (patrz poniżej) i `nuget pack` uwzględnione wszystkie pliki w folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="d3db5-375">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="d3db5-376">W takim przypadku nie jest konieczne uwzględnienie `contentFiles` w węźle `.nuspec` wcale.</span><span class="sxs-lookup"><span data-stu-id="d3db5-376">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="d3db5-377">Do kontroli, które pliki są uwzględnione `<contentFiles>` element określa to zbiór `<files>` obejmują elementy, które identyfikują konkretne pliki.</span><span class="sxs-lookup"><span data-stu-id="d3db5-377">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="d3db5-378">Te pliki są określane za pomocą zestaw atrybutów, które opisują, jak powinna być używana w ramach systemu projektu:</span><span class="sxs-lookup"><span data-stu-id="d3db5-378">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="d3db5-379">Atrybut</span><span class="sxs-lookup"><span data-stu-id="d3db5-379">Attribute</span></span> | <span data-ttu-id="d3db5-380">Opis</span><span class="sxs-lookup"><span data-stu-id="d3db5-380">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3db5-381">**include**</span><span class="sxs-lookup"><span data-stu-id="d3db5-381">**include**</span></span> | <span data-ttu-id="d3db5-382">(Wymagane) Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-382">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="d3db5-383">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="d3db5-383">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="d3db5-384">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="d3db5-384">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d3db5-385">**exclude**</span><span class="sxs-lookup"><span data-stu-id="d3db5-385">**exclude**</span></span> | <span data-ttu-id="d3db5-386">Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d3db5-386">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="d3db5-387">Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego.</span><span class="sxs-lookup"><span data-stu-id="d3db5-387">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="d3db5-388">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="d3db5-388">**buildAction**</span></span> | <span data-ttu-id="d3db5-389">Akcja kompilacji, aby przypisać do elementu zawartości dla platformy MSBuild, takich jak `Content`, `None`, `Embedded Resource`, `Compile`itp. Wartość domyślna to `Compile`.</span><span class="sxs-lookup"><span data-stu-id="d3db5-389">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="d3db5-390">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="d3db5-390">**copyToOutput**</span></span> | <span data-ttu-id="d3db5-391">Wartość Boolean wskazującą, czy chcesz skopiować elementy zawartości do kompilacji (lub opublikować) folder wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="d3db5-391">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="d3db5-392">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="d3db5-392">The default is false.</span></span> |
| <span data-ttu-id="d3db5-393">**spłaszczanie**</span><span class="sxs-lookup"><span data-stu-id="d3db5-393">**flatten**</span></span> | <span data-ttu-id="d3db5-394">Wartość logiczna wskazująca, czy skopiować elementy zawartości na pojedynczy folder w danych wyjściowych kompilacji (true) czy zachować strukturę folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="d3db5-394">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="d3db5-395">Ta flaga działa tylko, gdy copyToOutput flaga jest ustawiona na wartość true.</span><span class="sxs-lookup"><span data-stu-id="d3db5-395">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="d3db5-396">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="d3db5-396">The default is false.</span></span> |

<span data-ttu-id="d3db5-397">Instalując pakiet NuGet dotyczy elementów podrzędnych `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-397">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="d3db5-398">Jeśli wiele wpisów pasuje do tego samego pliku wszystkie wpisy są stosowane.</span><span class="sxs-lookup"><span data-stu-id="d3db5-398">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="d3db5-399">Wpis umieszczony najwyżej zastępuje wpisy niżej, jeśli występuje konflikt z tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d3db5-399">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="d3db5-400">Struktura folderów pakietu</span><span class="sxs-lookup"><span data-stu-id="d3db5-400">Package folder structure</span></span>

<span data-ttu-id="d3db5-401">Projekt pakietu powinien struktury zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="d3db5-401">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="d3db5-402">`codeLanguages` może być `cs`, `vb`, `fs`, `any`, lub litery odpowiednikiem danego `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="d3db5-402">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="d3db5-403">`TxM` jest dowolnym prawne krótka nazwa docelowej platformy obsługującej NuGet (zobacz [ustalać platformy docelowe](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="d3db5-403">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="d3db5-404">Dowolnej struktury folderów może być dołączany na końcu tej składni.</span><span class="sxs-lookup"><span data-stu-id="d3db5-404">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="d3db5-405">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d3db5-405">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="d3db5-406">Puste foldery można użyć `.` zrezygnować z dostarczanie zawartości dla niektórych kombinacji języka i TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="d3db5-406">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="d3db5-407">Sekcji z przykładowym pliki</span><span class="sxs-lookup"><span data-stu-id="d3db5-407">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="d3db5-408">Przykład nuspec plików</span><span class="sxs-lookup"><span data-stu-id="d3db5-408">Example nuspec files</span></span>

<span data-ttu-id="d3db5-409">**Prosty `.nuspec` nie określające zależności lub plików**</span><span class="sxs-lookup"><span data-stu-id="d3db5-409">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="d3db5-410">**A `.nuspec` z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="d3db5-410">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="d3db5-411">**A `.nuspec` z plikami**</span><span class="sxs-lookup"><span data-stu-id="d3db5-411">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="d3db5-412">**A `.nuspec` za pomocą zestawów framework**</span><span class="sxs-lookup"><span data-stu-id="d3db5-412">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="d3db5-413">W tym przykładzie poniżej są zainstalowane dla określonego projektu celów:</span><span class="sxs-lookup"><span data-stu-id="d3db5-413">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="d3db5-414">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d3db5-414">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="d3db5-415">. NET4 -> Profil klienta `System.Net`</span><span class="sxs-lookup"><span data-stu-id="d3db5-415">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="d3db5-416">Program Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="d3db5-416">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="d3db5-417">Program Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="d3db5-417">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="d3db5-418">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="d3db5-418">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
