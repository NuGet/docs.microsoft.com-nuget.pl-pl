---
title: Odwołanie do pliku .nuspec programu NuGet
description: Plik .nuspec zawiera metadane pakietów używane podczas tworzenia pakietu i podaj informacje dla konsumentów pakietu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c11b50aa1637c00f0f0e71a6e20ce5d435db402b
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="nuspec-reference"></a><span data-ttu-id="07fbf-103">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="07fbf-103">.nuspec reference</span></span>

<span data-ttu-id="07fbf-104">A `.nuspec` plik jest manifestu XML zawierający metadane pakietów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="07fbf-105">Tego manifestu jest używany zarówno do tworzenia pakietu i źródło informacji dla konsumentów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="07fbf-106">Manifest zawsze znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="07fbf-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="07fbf-107">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="07fbf-107">In this topic:</span></span>

- [<span data-ttu-id="07fbf-108">Ogólny kształt i schematu</span><span class="sxs-lookup"><span data-stu-id="07fbf-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="07fbf-109">[Zastąpienie tokenów](#replacement-tokens) (w przypadku użycia z projektu programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="07fbf-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="07fbf-110">Zależności</span><span class="sxs-lookup"><span data-stu-id="07fbf-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="07fbf-111">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="07fbf-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="07fbf-112">Odwołania do zestawów struktury</span><span class="sxs-lookup"><span data-stu-id="07fbf-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="07fbf-113">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="07fbf-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="07fbf-114">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="07fbf-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="07fbf-115">Przykłady</span><span class="sxs-lookup"><span data-stu-id="07fbf-115">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="07fbf-116">Ogólny kształt i schematu</span><span class="sxs-lookup"><span data-stu-id="07fbf-116">General form and schema</span></span>

<span data-ttu-id="07fbf-117">Bieżący `nuspec.xsd` można znaleźć w pliku schematu [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="07fbf-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="07fbf-118">W tym schemacie `.nuspec` plik ma następujący format Ogólne:</span><span class="sxs-lookup"><span data-stu-id="07fbf-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="07fbf-119">Dla wyczyść wizualną reprezentację schematu, otwórz plik schematu w programie Visual Studio w trybie projektowania, a następnie wybierz polecenie **Eksploratora schematu XML** łącza.</span><span class="sxs-lookup"><span data-stu-id="07fbf-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="07fbf-120">Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz **Pokaż Eksploratora schematu XML**.</span><span class="sxs-lookup"><span data-stu-id="07fbf-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="07fbf-121">W obu przypadkach (jeśli jest to przede wszystkim rozwinięty) wyświetlony widok, tak jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="07fbf-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Explorer schematu z nuspec.xsd Otwórz](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="07fbf-123">Atrybuty metadanych</span><span class="sxs-lookup"><span data-stu-id="07fbf-123">Metadata attributes</span></span>

<span data-ttu-id="07fbf-124">`<metadata>` Elementu obsługuje atrybuty opisane w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="07fbf-124">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="07fbf-125">Atrybut</span><span class="sxs-lookup"><span data-stu-id="07fbf-125">Attribute</span></span> | <span data-ttu-id="07fbf-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="07fbf-126">Required</span></span> | <span data-ttu-id="07fbf-127">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-127">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="07fbf-128">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="07fbf-128">**minClientVersion**</span></span> | <span data-ttu-id="07fbf-129">Nie</span><span class="sxs-lookup"><span data-stu-id="07fbf-129">No</span></span> | <span data-ttu-id="07fbf-130">Określa minimalną wersję klienta NuGet, który można zainstalować ten pakiet, wymuszane przez nuget.exe i Menedżer pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07fbf-130">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="07fbf-131">To jest używana zawsze, gdy pakiet jest zależny od konkretnych cech `.nuspec` plików, które zostały dodane w przypadku konkretnej wersji klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="07fbf-131">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="07fbf-132">Na przykład pakietu za pomocą `developmentDependency` atrybut powinien określać "2.8" dla `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-132">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="07fbf-133">Podobnie, pakietu za pomocą `contentFiles` (zobacz następną sekcję) należy ustawić element `minClientVersion` do "3.3".</span><span class="sxs-lookup"><span data-stu-id="07fbf-133">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="07fbf-134">Należy zauważyć, że ponieważ klientów NuGet przed 2.5 nie rozpoznają tej flagi one *zawsze* odmówić można zainstalować pakietu, niezależnie od tego, co `minClientVersion` zawiera.</span><span class="sxs-lookup"><span data-stu-id="07fbf-134">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="07fbf-135">Elementy wymagane metadane</span><span class="sxs-lookup"><span data-stu-id="07fbf-135">Required metadata elements</span></span>

<span data-ttu-id="07fbf-136">Następujące elementy są minimalne wymagania dotyczące pakietu, należy rozważyć dodanie [elementy opcjonalne metadane](#optional-metadata-elements) celu usprawnienie obsługi ogólnej mogą korzystać z pakietem.</span><span class="sxs-lookup"><span data-stu-id="07fbf-136">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="07fbf-137">Te elementy muszą występować w `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-137">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="07fbf-138">Element</span><span class="sxs-lookup"><span data-stu-id="07fbf-138">Element</span></span> | <span data-ttu-id="07fbf-139">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07fbf-140">**id**</span><span class="sxs-lookup"><span data-stu-id="07fbf-140">**id**</span></span> | <span data-ttu-id="07fbf-141">Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowa w nuget.org lub niezależnie od pakietu, który znajduje się w galerii.</span><span class="sxs-lookup"><span data-stu-id="07fbf-141">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="07fbf-142">Identyfikatory nie może zawierać spacji ani znaków, które nie są prawidłowe dla danego adresu URL i ogólnie zgodne reguły obszaru nazw .NET.</span><span class="sxs-lookup"><span data-stu-id="07fbf-142">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="07fbf-143">Zobacz [Wybieranie identyfikator unikatowy pakiet](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) orientacji.</span><span class="sxs-lookup"><span data-stu-id="07fbf-143">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="07fbf-144">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="07fbf-144">**version**</span></span> | <span data-ttu-id="07fbf-145">Wersja pakietu, następujące *Wersja_główna.WERSJA_POMOCNICZA.poprawka* wzorca.</span><span class="sxs-lookup"><span data-stu-id="07fbf-145">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="07fbf-146">Numery wersji może zawierać sufiks wersji wstępnej, zgodnie z opisem w [wersji pakietu](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="07fbf-146">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="07fbf-147">**Opis elementu**</span><span class="sxs-lookup"><span data-stu-id="07fbf-147">**description**</span></span> | <span data-ttu-id="07fbf-148">Długi opis pakietu do wyświetlenia interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07fbf-148">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="07fbf-149">**Autorzy**</span><span class="sxs-lookup"><span data-stu-id="07fbf-149">**authors**</span></span> | <span data-ttu-id="07fbf-150">Rozdzielana przecinkami lista autorzy pakietów, zgodne z nazwami profilu na nuget.org. Te są wyświetlane w galerii NuGet w nuget.org i są odwoływania się do pakietów przez tego samego autorów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="07fbf-151">Elementy opcjonalne metadane</span><span class="sxs-lookup"><span data-stu-id="07fbf-151">Optional metadata elements</span></span>

<span data-ttu-id="07fbf-152">Te elementy mogą być widoczne w `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-152">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="07fbf-153">Pojedyncze elementy</span><span class="sxs-lookup"><span data-stu-id="07fbf-153">Single elements</span></span>

| <span data-ttu-id="07fbf-154">Element</span><span class="sxs-lookup"><span data-stu-id="07fbf-154">Element</span></span> | <span data-ttu-id="07fbf-155">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-155">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07fbf-156">**Tytuł**</span><span class="sxs-lookup"><span data-stu-id="07fbf-156">**title**</span></span> | <span data-ttu-id="07fbf-157">Tytuł przyjaznych dla człowieka pakietu, zwykle używanych w wyświetla interfejsu użytkownika na nuget.org i Menedżera pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07fbf-157">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="07fbf-158">Jeśli nie zostanie określony, identyfikator pakietu jest używany.</span><span class="sxs-lookup"><span data-stu-id="07fbf-158">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="07fbf-159">**Właściciele**</span><span class="sxs-lookup"><span data-stu-id="07fbf-159">**owners**</span></span> | <span data-ttu-id="07fbf-160">Rozdzielana przecinkami lista twórców pakietu przy użyciu nazwy profilu na nuget.org. Jest to często jak w tej samej listy `authors`i jest ignorowane w przypadku przekazywania pakietu do nuget.org. Zobacz [Zarządzanie właścicieli pakietu na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="07fbf-160">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="07fbf-161">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="07fbf-161">**projectUrl**</span></span> | <span data-ttu-id="07fbf-162">Wyświetla adres URL strony głównej pakietu, często są wyświetlane w interfejsie użytkownika oraz nuget.org.</span><span class="sxs-lookup"><span data-stu-id="07fbf-162">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="07fbf-163">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="07fbf-163">**licenseUrl**</span></span> | <span data-ttu-id="07fbf-164">Adres URL wyświetlany w wyświetla interfejsu użytkownika, a także nuget.org licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-164">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="07fbf-165">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="07fbf-165">**iconUrl**</span></span> | <span data-ttu-id="07fbf-166">Adres URL obrazu 64 x 64, przezroczystość tła ma być używana jako ikonę pakietu w wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07fbf-166">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="07fbf-167">Pamiętaj, że ten element zawiera *bezpośredni adres URL obrazu* , a nie adres URL strony sieci web zawierającej obraz.</span><span class="sxs-lookup"><span data-stu-id="07fbf-167">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="07fbf-168">Na przykład, aby użyć obrazu z witryny GitHub, użyj plik raw, takie jak adres URL  <em>https://github.com/ \<username\>/\<repozytorium\>/raw/\<gałęzi\> / \<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="07fbf-168">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> |
| <span data-ttu-id="07fbf-169">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="07fbf-169">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="07fbf-170">Wartość logiczna, określając, czy klient musi monitować o konsumenta, aby zaakceptować licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-170">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="07fbf-171">**DevelopmentDependency**</span><span class="sxs-lookup"><span data-stu-id="07fbf-171">**developmentDependency**</span></span> | <span data-ttu-id="07fbf-172">*(2.8 +)*  Wartość logiczna A, określając, czy pakiet jest oznaczone jako programowanie — tylko zależność, która zapobiega włączaniu jako zależności w innych pakietach pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-172">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="07fbf-173">**Podsumowanie**</span><span class="sxs-lookup"><span data-stu-id="07fbf-173">**summary**</span></span> | <span data-ttu-id="07fbf-174">Krótki opis pakietu do wyświetlenia interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07fbf-174">A short description of the package for UI display.</span></span> <span data-ttu-id="07fbf-175">Pominięcie skrócona wersja `description` jest używany.</span><span class="sxs-lookup"><span data-stu-id="07fbf-175">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="07fbf-176">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="07fbf-176">**releaseNotes**</span></span> | <span data-ttu-id="07fbf-177">*(w wersji 1.5 +)*  Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak **aktualizacje** kartę programu Visual Studio Menedżer pakietów zamiast Opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-177">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="07fbf-178">**copyright**</span><span class="sxs-lookup"><span data-stu-id="07fbf-178">**copyright**</span></span> | <span data-ttu-id="07fbf-179">*(w wersji 1.5 +)*  Copyright szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-179">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="07fbf-180">**Język**</span><span class="sxs-lookup"><span data-stu-id="07fbf-180">**language**</span></span> | <span data-ttu-id="07fbf-181">Identyfikator ustawień regionalnych dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-181">The locale ID for the package.</span></span> <span data-ttu-id="07fbf-182">Zobacz [tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="07fbf-182">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="07fbf-183">**Tagi**</span><span class="sxs-lookup"><span data-stu-id="07fbf-183">**tags**</span></span>  | <span data-ttu-id="07fbf-184">Rozdzieloną spacjami listę tagów i słów kluczowych, które opisują odnajdywania pakietu i pomocy pakietów za pomocą wyszukiwania i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="07fbf-184">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="07fbf-185">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="07fbf-185">**serviceable**</span></span> | <span data-ttu-id="07fbf-186">*(3.3 +)*  Programu NuGet wewnętrznego użytku.</span><span class="sxs-lookup"><span data-stu-id="07fbf-186">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="07fbf-187">Elementy kolekcji</span><span class="sxs-lookup"><span data-stu-id="07fbf-187">Collection elements</span></span>

| <span data-ttu-id="07fbf-188">Element</span><span class="sxs-lookup"><span data-stu-id="07fbf-188">Element</span></span> | <span data-ttu-id="07fbf-189">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-189">Description</span></span> |
| --- | --- |
<span data-ttu-id="07fbf-190">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="07fbf-190">**packageTypes**</span></span> | <span data-ttu-id="07fbf-191">*(3.5 +)*  Kolekcji zero lub więcej `<packageType>` elementy określenie typu pakietu, jeśli inne niż tradycyjne zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-191">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="07fbf-192">Każdy packageType ma atrybuty *nazwa* i *wersji*.</span><span class="sxs-lookup"><span data-stu-id="07fbf-192">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="07fbf-193">Zobacz [ustawienie typu pakietu](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="07fbf-193">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="07fbf-194">**Zależności**</span><span class="sxs-lookup"><span data-stu-id="07fbf-194">**dependencies**</span></span> | <span data-ttu-id="07fbf-195">Kolekcja zero lub więcej `<dependency>` elementy określania zależności dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-195">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="07fbf-196">Poszczególne zależności ma atrybuty *identyfikator*, *wersji*, *obejmują* (3.x+) i *wykluczyć* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="07fbf-196">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="07fbf-197">Zobacz [zależności](#dependencies) poniżej.</span><span class="sxs-lookup"><span data-stu-id="07fbf-197">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="07fbf-198">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="07fbf-198">**frameworkAssemblies**</span></span> | <span data-ttu-id="07fbf-199">*(1.2 +)*  Kolekcji zero lub więcej `<frameworkAssembly>` elementy identyfikowanie odwołań zestawu .NET Framework, które wymaga tego pakietu, który zapewnia dodania odwołań do projektów korzystających z pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-199">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="07fbf-200">Każdy frameworkAssembly ma *assemblyName* i *targetFramework* atrybutów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-200">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="07fbf-201">Zobacz [określenie zestawu struktury odwołuje się do pamięci podręcznej GAC](#specifying-framework-assembly-references-gac) poniżej.</span><span class="sxs-lookup"><span data-stu-id="07fbf-201">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="07fbf-202">**Odwołania**</span><span class="sxs-lookup"><span data-stu-id="07fbf-202">**references**</span></span> | <span data-ttu-id="07fbf-203">*(w wersji 1.5 +)*  Kolekcji zero lub więcej `<reference>` elementy nazw zestawów, w tym pakiecie `lib` folderów, które są dodawane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-203">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="07fbf-204">Odwołanie do każdego ma *pliku* atrybutu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-204">Each reference has a *file* attribute.</span></span> <span data-ttu-id="07fbf-205">`<references>` może również zawierać `<group>` element z *targetFramework* atrybut, który następnie zawiera `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-205">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="07fbf-206">Pominięcie wszystkie odwołania w `lib` są uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="07fbf-206">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="07fbf-207">Zobacz [odwołania do zestawów jawne określenie](#specifying-explicit-assembly-references) poniżej.</span><span class="sxs-lookup"><span data-stu-id="07fbf-207">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="07fbf-208">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="07fbf-208">**contentFiles**</span></span> | <span data-ttu-id="07fbf-209">*(3.3 +)*  Kolekcja `<files>` elementy identyfikujące pliki zawartości do uwzględnienia w projekcie odbierającą.</span><span class="sxs-lookup"><span data-stu-id="07fbf-209">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="07fbf-210">Te pliki są określane za pomocą zestawu atrybutów, które opisują jak powinny być używane w ramach systemu projektu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-210">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="07fbf-211">Zobacz [określenie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej.</span><span class="sxs-lookup"><span data-stu-id="07fbf-211">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="07fbf-212">Element Pliki</span><span class="sxs-lookup"><span data-stu-id="07fbf-212">Files element</span></span>

<span data-ttu-id="07fbf-213">`<package>` Węzeł może zawierać `<files>` węzeł jako element równorzędny do `<metadata>`, a lub `<contentFiles>` dziecka poniżej `<metadata>`, aby określić, które pliki zestawu i zawartości do uwzględnienia w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="07fbf-213">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="07fbf-214">Zobacz [w tym pliki zestawu](#including-assembly-files) i [plików zawartości w tym](#including-content-files) dalszej części tego tematu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="07fbf-214">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="07fbf-215">Zastąpienie tokenów</span><span class="sxs-lookup"><span data-stu-id="07fbf-215">Replacement tokens</span></span>

<span data-ttu-id="07fbf-216">Podczas tworzenia pakietu, [ `nuget pack` polecenia](../tools/cli-ref-pack.md) zastępuje rozdzielany $ tokenów w `.nuspec` pliku `<metadata>` węzeł z wartości pochodzących z jednego pliku projektu lub `pack` polecenia `-properties`przełącznika.</span><span class="sxs-lookup"><span data-stu-id="07fbf-216">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="07fbf-217">W wierszu polecenia, określić wartości tokenów z `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-217">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="07fbf-218">Na przykład, takich jak można użyć tokenu `$owners$` i `$desc$` w `.nuspec` i podaj wartości w pakowania czasu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="07fbf-218">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="07fbf-219">Aby użyć wartości z projektu, określ tokeny opisane w poniższej tabeli (AssemblyInfo odwołuje się do pliku w `Properties` takich jak `AssemblyInfo.cs` lub `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="07fbf-219">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="07fbf-220">Aby użyć tych tokenów, uruchom `nuget pack` z pliku projektu, a nie tylko `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-220">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="07fbf-221">Na przykład przy użyciu następującego polecenia `$id$` i `$version$` tokenów w `.nuspec` plików są zastępowane projektu `AssemblyName` i `AssemblyVersion` wartości:</span><span class="sxs-lookup"><span data-stu-id="07fbf-221">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="07fbf-222">Zwykle, gdy projekt, tworzenia `.nuspec` początkowo przy użyciu `nuget spec MyProject.csproj` automatycznie zawierające niektóre z tych standardowe tokenów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-222">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="07fbf-223">Jednak jeśli projekt nie ma wartości dla wymaganych `.nuspec` elementy, a następnie `nuget pack` zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="07fbf-223">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="07fbf-224">Ponadto w przypadku zmiany wartości projektu, upewnij się odbudować przed utworzeniem pakietu; Można to zrobić wygodnie przy użyciu polecenia pakiet `build` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="07fbf-224">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="07fbf-225">Z wyjątkiem produktów `$configuration$`, wartości w projekcie są używane zamiast wszelkie przypisane do tego samego tokenu w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="07fbf-225">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="07fbf-226">Token</span><span class="sxs-lookup"><span data-stu-id="07fbf-226">Token</span></span> | <span data-ttu-id="07fbf-227">Wartość źródła</span><span class="sxs-lookup"><span data-stu-id="07fbf-227">Value source</span></span> | <span data-ttu-id="07fbf-228">Wartość</span><span class="sxs-lookup"><span data-stu-id="07fbf-228">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="07fbf-229">**$id$**</span><span class="sxs-lookup"><span data-stu-id="07fbf-229">**$id$**</span></span> | <span data-ttu-id="07fbf-230">plik projektu</span><span class="sxs-lookup"><span data-stu-id="07fbf-230">Project file</span></span> | <span data-ttu-id="07fbf-231">AssemblyName (tytuł) z pliku projektu</span><span class="sxs-lookup"><span data-stu-id="07fbf-231">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="07fbf-232">**$version$**</span><span class="sxs-lookup"><span data-stu-id="07fbf-232">**$version$**</span></span> | <span data-ttu-id="07fbf-233">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="07fbf-233">AssemblyInfo</span></span> | <span data-ttu-id="07fbf-234">AssemblyInformationalVersion, jeśli jest obecna, w przeciwnym razie AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="07fbf-234">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="07fbf-235">**$author$**</span><span class="sxs-lookup"><span data-stu-id="07fbf-235">**$author$**</span></span> | <span data-ttu-id="07fbf-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="07fbf-236">AssemblyInfo</span></span> | <span data-ttu-id="07fbf-237">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="07fbf-237">AssemblyCompany</span></span> |
| <span data-ttu-id="07fbf-238">**$title$**</span><span class="sxs-lookup"><span data-stu-id="07fbf-238">**$title$**</span></span> | <span data-ttu-id="07fbf-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="07fbf-239">AssemblyInfo</span></span> | <span data-ttu-id="07fbf-240">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="07fbf-240">AssemblyTitle</span></span> |
| <span data-ttu-id="07fbf-241">**$description$**</span><span class="sxs-lookup"><span data-stu-id="07fbf-241">**$description$**</span></span> | <span data-ttu-id="07fbf-242">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="07fbf-242">AssemblyInfo</span></span> | <span data-ttu-id="07fbf-243">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="07fbf-243">AssemblyDescription</span></span> |
| <span data-ttu-id="07fbf-244">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="07fbf-244">**$copyright$**</span></span> | <span data-ttu-id="07fbf-245">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="07fbf-245">AssemblyInfo</span></span> | <span data-ttu-id="07fbf-246">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="07fbf-246">AssemblyCopyright</span></span> |
| <span data-ttu-id="07fbf-247">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="07fbf-247">**$configuration$**</span></span> | <span data-ttu-id="07fbf-248">Zestaw biblioteki DLL</span><span class="sxs-lookup"><span data-stu-id="07fbf-248">Assembly DLL</span></span> | <span data-ttu-id="07fbf-249">Konfiguracja używany do tworzenia zestawu, domyślnie używany do debugowania.</span><span class="sxs-lookup"><span data-stu-id="07fbf-249">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="07fbf-250">Pamiętaj, że do utworzenia pakietu przy użyciu konfiguracji wydanie, zawsze używać `-properties Configuration=Release` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="07fbf-250">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="07fbf-251">Tokeny mogą służyć do rozpoznawania ścieżek po dołączeniu [pliki zestawu](#including-assembly-files) i [zawartości plików](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="07fbf-251">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="07fbf-252">Tokeny mają takie same nazwy jako właściwości programu MSBuild, dzięki czemu można wybrać pliki, które zostaną uwzględnione w zależności od bieżącej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="07fbf-252">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="07fbf-253">Na przykład, jeśli można używać następujących tokenów w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="07fbf-253">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="07fbf-254">I kompilacji zestawu których `AssemblyName` jest `LoggingLibrary` z `Release` konfiguracji w programie MSBuild, wynikowy wiersze `.nuspec` pliku w pakiecie jest następujący:</span><span class="sxs-lookup"><span data-stu-id="07fbf-254">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="07fbf-255">Zależności</span><span class="sxs-lookup"><span data-stu-id="07fbf-255">Dependencies</span></span>

<span data-ttu-id="07fbf-256">`<dependencies>` w elemencie `<metadata>` zawiera dowolną liczbę `<dependency>` elementy, które identyfikują inne pakiety, od których zależy Pakiet najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-256">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="07fbf-257">Atrybuty dla każdego `<dependency>` są następujące:</span><span class="sxs-lookup"><span data-stu-id="07fbf-257">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="07fbf-258">Atrybut</span><span class="sxs-lookup"><span data-stu-id="07fbf-258">Attribute</span></span> | <span data-ttu-id="07fbf-259">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-259">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="07fbf-260">(Wymagane) Identyfikator pakietu zależności, takich jak "EntityFramework" i "NUnit", czyli nazwa nuget.org pakietu zawiera stronę pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-260">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="07fbf-261">(Wymagane) Zakres wersji akceptowane jako zależność.</span><span class="sxs-lookup"><span data-stu-id="07fbf-261">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="07fbf-262">Zobacz [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards) dla określonej składni.</span><span class="sxs-lookup"><span data-stu-id="07fbf-262">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="07fbf-263">include</span><span class="sxs-lookup"><span data-stu-id="07fbf-263">include</span></span> | <span data-ttu-id="07fbf-264">Rozdzielana przecinkami lista dołączania/wykluczania znaczniki (patrz poniżej) wskazujący zależności, aby uwzględnić w ostatnim pakiecie.</span><span class="sxs-lookup"><span data-stu-id="07fbf-264">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="07fbf-265">Wartość domyślna to `none`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-265">The default value is `none`.</span></span> |
| <span data-ttu-id="07fbf-266">wykluczanie</span><span class="sxs-lookup"><span data-stu-id="07fbf-266">exclude</span></span> | <span data-ttu-id="07fbf-267">Rozdzielana przecinkami lista dołączania/wykluczania znaczniki (patrz poniżej) wskazujący zależności do wykluczenia w ostatnim pakiecie.</span><span class="sxs-lookup"><span data-stu-id="07fbf-267">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="07fbf-268">Wartość domyślna to `all`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-268">The  default value is `all`.</span></span> <span data-ttu-id="07fbf-269">Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-269">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="07fbf-270">Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-270">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="07fbf-271">Dołączania/wykluczania tag</span><span class="sxs-lookup"><span data-stu-id="07fbf-271">Include/Exclude tag</span></span> | <span data-ttu-id="07fbf-272">Odpowiednie foldery elementu docelowego</span><span class="sxs-lookup"><span data-stu-id="07fbf-272">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="07fbf-273">Pliki</span><span class="sxs-lookup"><span data-stu-id="07fbf-273">contentFiles</span></span> | <span data-ttu-id="07fbf-274">Zawartość</span><span class="sxs-lookup"><span data-stu-id="07fbf-274">Content</span></span> |
| <span data-ttu-id="07fbf-275">środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="07fbf-275">runtime</span></span> | <span data-ttu-id="07fbf-276">Środowisko uruchomieniowe, zasobów i FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="07fbf-276">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="07fbf-277">Kompilacji</span><span class="sxs-lookup"><span data-stu-id="07fbf-277">compile</span></span> | <span data-ttu-id="07fbf-278">lib</span><span class="sxs-lookup"><span data-stu-id="07fbf-278">lib</span></span> |
| <span data-ttu-id="07fbf-279">kompilacja</span><span class="sxs-lookup"><span data-stu-id="07fbf-279">build</span></span> | <span data-ttu-id="07fbf-280">Kompilacja (właściwości programu MSBuild i elementy docelowe)</span><span class="sxs-lookup"><span data-stu-id="07fbf-280">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="07fbf-281">natywne</span><span class="sxs-lookup"><span data-stu-id="07fbf-281">native</span></span> | <span data-ttu-id="07fbf-282">natywne</span><span class="sxs-lookup"><span data-stu-id="07fbf-282">native</span></span> |
| <span data-ttu-id="07fbf-283">brak</span><span class="sxs-lookup"><span data-stu-id="07fbf-283">none</span></span> | <span data-ttu-id="07fbf-284">Brak folderów</span><span class="sxs-lookup"><span data-stu-id="07fbf-284">No folders</span></span> |
| <span data-ttu-id="07fbf-285">wszystkie</span><span class="sxs-lookup"><span data-stu-id="07fbf-285">all</span></span> | <span data-ttu-id="07fbf-286">Wszystkie foldery</span><span class="sxs-lookup"><span data-stu-id="07fbf-286">All folders</span></span> |

<span data-ttu-id="07fbf-287">Na przykład wskazać zależności następujące wiersze na `PackageA` wersji 1.1.0 lub nowszej, i `PackageB` wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="07fbf-287">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="07fbf-288">Następujące wiersze oznaczają zależności na te same pakiety, ale określa uwzględnienie `contentFiles` i `build` folderów do `PackageA` i wszystko, ale `native` i `compile` foldery `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="07fbf-288">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="07fbf-289">Uwaga: Podczas tworzenia `.nuspec` projektu używającego `nuget spec`, zależności, które istnieją w tym projekcie są automatycznie umieszczane w wynikowym `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="07fbf-289">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="07fbf-290">Grupy zależności</span><span class="sxs-lookup"><span data-stu-id="07fbf-290">Dependency groups</span></span>

<span data-ttu-id="07fbf-291">*W wersji 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="07fbf-291">*Version 2.0+*</span></span>

<span data-ttu-id="07fbf-292">Alternatywą dla pojedynczego płaską listę zależności można określić zgodnie z profil platformy docelowej projektu przy użyciu `<group>` elementów w obrębie `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-292">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="07fbf-293">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-293">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="07fbf-294">Te zależności są zainstalowane jednocześnie, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-294">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="07fbf-295">`<group>` Bez `targetFramework` atrybut jest używany jako domyślny lub powrotu listę zależności.</span><span class="sxs-lookup"><span data-stu-id="07fbf-295">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="07fbf-296">Zobacz [platform docelowych](../reference/target-frameworks.md) identyfikatorów dokładne framework.</span><span class="sxs-lookup"><span data-stu-id="07fbf-296">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="07fbf-297">Format grupy nie może się zmieszać z płaska lista.</span><span class="sxs-lookup"><span data-stu-id="07fbf-297">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="07fbf-298">W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="07fbf-298">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="07fbf-299">Odwołania do zestawów jawne</span><span class="sxs-lookup"><span data-stu-id="07fbf-299">Explicit assembly references</span></span>

<span data-ttu-id="07fbf-300">`<references>` Element jawnie określa zestawy, które docelowy projekt powinien odwoływać się przy użyciu pakietu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-300">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="07fbf-301">Gdy ten element jest obecny, NuGet Dodaj odwołania do tylko zestawy wymienionych; nie powoduje dodania odwołania do innych zestawów, w tym pakiecie `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-301">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="07fbf-302">Na przykład następująca `<references>` NuGet, aby dodać odwołania do tylko powoduje, że element `xunit.dll` i `xunit.extensions.dll` nawet jeśli istnieją dodatkowe zestawy w pakiecie:</span><span class="sxs-lookup"><span data-stu-id="07fbf-302">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="07fbf-303">Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="07fbf-303">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="07fbf-304">Korzystając z [kontraktów kodu](/dotnet/framework/debug-trace-profile/code-contracts), na przykład zestawów kontraktu musi być obok zestawy środowiska wykonawczego, do których one rozszerzyć, aby można je odnaleźć programu Visual Studio, ale zestawów kontraktu nie musi być odwołuje się projekt lub kopiowane w projekcie `bin` folderu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-304">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="07fbf-305">Podobnie jawne odwołania mogą być używane dla platform testów jednostkowych, takich jak XUnit, którą należy jej narzędzi zestawy znajdujące się obok zestawy środowiska wykonawczego, ale nie wymaga ich uwzględniane jako odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-305">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="07fbf-306">Grupy odwołania</span><span class="sxs-lookup"><span data-stu-id="07fbf-306">Reference groups</span></span>

<span data-ttu-id="07fbf-307">Alternatywą dla pojedynczego płaska lista odwołań można określić zgodnie z profil platformy docelowej projektu przy użyciu `<group>` elementów w obrębie `<references>`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-307">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="07fbf-308">Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-308">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="07fbf-309">Te odwołania są dodawane do projektu, gdy platforma docelowa jest zgodny z profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-309">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="07fbf-310">`<group>` Bez `targetFramework` atrybut jest używany jako domyślny lub powrotu lista odwołań.</span><span class="sxs-lookup"><span data-stu-id="07fbf-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="07fbf-311">Zobacz [platform docelowych](../reference/target-frameworks.md) identyfikatorów dokładne framework.</span><span class="sxs-lookup"><span data-stu-id="07fbf-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="07fbf-312">Format grupy nie może się zmieszać z płaska lista.</span><span class="sxs-lookup"><span data-stu-id="07fbf-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="07fbf-313">W poniższym przykładzie przedstawiono różne odmiany `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="07fbf-313">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="07fbf-314">Odwołania do zestawów struktury</span><span class="sxs-lookup"><span data-stu-id="07fbf-314">Framework assembly references</span></span>

<span data-ttu-id="07fbf-315">Zestawy struktury są tymi, które są częścią programu .NET framework i powinna już być w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej podanej maszyny.</span><span class="sxs-lookup"><span data-stu-id="07fbf-315">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="07fbf-316">Dzięki identyfikacji te zestawy w `<frameworkAssemblies>` elementu pakietu można upewnij się, że odwołania wymagane są dodawane do projektu, w przypadku gdy projekt nie ma takich odwołania już.</span><span class="sxs-lookup"><span data-stu-id="07fbf-316">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="07fbf-317">Takie zestawy oczywiście nie znajdują się w pakiecie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="07fbf-317">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="07fbf-318">`<frameworkAssemblies>` Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="07fbf-318">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="07fbf-319">Atrybut</span><span class="sxs-lookup"><span data-stu-id="07fbf-319">Attribute</span></span> | <span data-ttu-id="07fbf-320">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-320">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07fbf-321">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="07fbf-321">**assemblyName**</span></span> | <span data-ttu-id="07fbf-322">(Wymagane) Nazwa FQDN zestawu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-322">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="07fbf-323">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="07fbf-323">**targetFramework**</span></span> | <span data-ttu-id="07fbf-324">(Opcjonalnie) Określa platformę docelową, do którego odnosi się to odwołanie.</span><span class="sxs-lookup"><span data-stu-id="07fbf-324">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="07fbf-325">Pominięcie wskazuje, że odwołanie jest stosowana do wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="07fbf-325">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="07fbf-326">Zobacz [platform docelowych](../reference/target-frameworks.md) identyfikatorów dokładne framework.</span><span class="sxs-lookup"><span data-stu-id="07fbf-326">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="07fbf-327">W poniższym przykładzie przedstawiono odwołanie do `System.Net` dla wszystkich docelowych platform oraz odwołanie do `System.ServiceModel` dla programu .NET Framework 4.0 tylko:</span><span class="sxs-lookup"><span data-stu-id="07fbf-327">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="07fbf-328">W tym pliki zestawu</span><span class="sxs-lookup"><span data-stu-id="07fbf-328">Including assembly files</span></span>

<span data-ttu-id="07fbf-329">Jeśli wykonujesz konwencje opisanego w [utworzenie pakietu](../create-packages/creating-a-package.md), nie trzeba jawnie określić listę plików w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="07fbf-329">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="07fbf-330">`nuget pack` Polecenie automatycznie przejmuje wymaganych plików.</span><span class="sxs-lookup"><span data-stu-id="07fbf-330">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="07fbf-331">Po zainstalowaniu pakietu w projekcie NuGet automatycznie dodaje odwołania do zestawów do biblioteki dll pakietu, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie.</span><span class="sxs-lookup"><span data-stu-id="07fbf-331">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="07fbf-332">Z tego powodu należy unikać `.resources.dll` plików, które w przeciwnym razie zawiera istotne pakiet kodu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-332">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="07fbf-333">Aby pominąć to działanie automatyczne i jawnie kontrolować pliki, które są umieszczone w pakiecie, umieść `<files>` element jako element podrzędny `<package>` (i element równorzędny `<metadata>`), identyfikowanie poszczególnych plików za pomocą oddzielnego `<file>` elementu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-333">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="07fbf-334">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="07fbf-334">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="07fbf-335">Nuget 2.x i wcześniej i projektów przy użyciu `packages.config`, `<files>` elementu służy również do obejmuje niezmienne plików zawartości, gdy jest zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="07fbf-335">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="07fbf-336">Z projektów PackageReference i NuGet 3.3 + `<contentFiles>` zamiast tego użyć elementu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-336">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="07fbf-337">Zobacz [plików zawartości w tym](#including-content-files) poniżej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="07fbf-337">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="07fbf-338">Atrybuty elementu</span><span class="sxs-lookup"><span data-stu-id="07fbf-338">File element attributes</span></span>

<span data-ttu-id="07fbf-339">Każdy `<file>` element określa następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="07fbf-339">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="07fbf-340">Atrybut</span><span class="sxs-lookup"><span data-stu-id="07fbf-340">Attribute</span></span> | <span data-ttu-id="07fbf-341">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-341">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07fbf-342">**src**</span><span class="sxs-lookup"><span data-stu-id="07fbf-342">**src**</span></span> | <span data-ttu-id="07fbf-343">Lokalizacja pliku lub plików do uwzględnienia, mogą ulec wykluczenia określony przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-343">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="07fbf-344">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="07fbf-344">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="07fbf-345">Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="07fbf-345">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="07fbf-346">**docelowy**</span><span class="sxs-lookup"><span data-stu-id="07fbf-346">**target**</span></span> | <span data-ttu-id="07fbf-347">Względna ścieżka do folderu w pakiecie, gdzie znajdują się pliki źródłowe, musi rozpoczynać się od `lib`, `content`, `build`, lub `tools`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-347">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="07fbf-348">Zobacz [tworzenie .nuspec z katalogu roboczego opartych na konwencjach](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="07fbf-348">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="07fbf-349">**exclude**</span><span class="sxs-lookup"><span data-stu-id="07fbf-349">**exclude**</span></span> | <span data-ttu-id="07fbf-350">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="07fbf-350">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="07fbf-351">Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="07fbf-351">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="07fbf-352">Przykłady</span><span class="sxs-lookup"><span data-stu-id="07fbf-352">Examples</span></span>

<span data-ttu-id="07fbf-353">**Jednym zestawie**</span><span class="sxs-lookup"><span data-stu-id="07fbf-353">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="07fbf-354">**Specyficzne dla platformy docelowej jednym zestawie**</span><span class="sxs-lookup"><span data-stu-id="07fbf-354">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="07fbf-355">**Zestaw biblioteki DLL przy użyciu symboli wieloznacznych**</span><span class="sxs-lookup"><span data-stu-id="07fbf-355">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="07fbf-356">**Biblioteki DLL dla różnych platform**</span><span class="sxs-lookup"><span data-stu-id="07fbf-356">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="07fbf-357">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="07fbf-357">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="07fbf-358">W tym pliki zawartości</span><span class="sxs-lookup"><span data-stu-id="07fbf-358">Including content files</span></span>

<span data-ttu-id="07fbf-359">Pliki zawartości są niezmienne pliki pakietu musi zawierać się w projekcie.</span><span class="sxs-lookup"><span data-stu-id="07fbf-359">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="07fbf-360">Są niezmienne, nie mają zostać zmodyfikowane przez odbierającą projektu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-360">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="07fbf-361">Pliki zawartości przykład obejmują:</span><span class="sxs-lookup"><span data-stu-id="07fbf-361">Example content files include:</span></span>

- <span data-ttu-id="07fbf-362">Obrazy osadzone jako zasoby</span><span class="sxs-lookup"><span data-stu-id="07fbf-362">Images that are embedded as resources</span></span>
- <span data-ttu-id="07fbf-363">Pliki źródłowe, które już są kompilowane</span><span class="sxs-lookup"><span data-stu-id="07fbf-363">Source files that are already compiled</span></span>
- <span data-ttu-id="07fbf-364">Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu</span><span class="sxs-lookup"><span data-stu-id="07fbf-364">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="07fbf-365">Pliki konfiguracji pakietu, które należy uwzględnić w projekcie, ale nie ma potrzeby zmiany specyficznego dla projektu</span><span class="sxs-lookup"><span data-stu-id="07fbf-365">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="07fbf-366">Zawartości plików znajdują się w pakietu przy użyciu `<files>` elementu, określając `content` folderu w `target` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-366">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="07fbf-367">Jednak takie pliki są ignorowane, gdy pakiet jest zainstalowany w projekcie przy użyciu PackageReference, którego użyje `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-367">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="07fbf-368">Maksymalną zgodność z używania projektów pakietu w idealnym przypadku określa pliki zawartości w obu elementów.</span><span class="sxs-lookup"><span data-stu-id="07fbf-368">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="07fbf-369">Za pomocą elementu plików dla plików zawartości</span><span class="sxs-lookup"><span data-stu-id="07fbf-369">Using the files element for content files</span></span>

<span data-ttu-id="07fbf-370">Dla plików zawartości, po prostu używany ten sam format plików zestawu jednak określić `content` jako podstawowy folder w `target` atrybutu, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="07fbf-370">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="07fbf-371">**Podstawowe pliki zawartości**</span><span class="sxs-lookup"><span data-stu-id="07fbf-371">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="07fbf-372">**Pliki zawartości ze struktury katalogów**</span><span class="sxs-lookup"><span data-stu-id="07fbf-372">**Content files with directory structure**</span></span>

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

<span data-ttu-id="07fbf-373">**Plik zawartości, które są specyficzne dla platformy docelowej**</span><span class="sxs-lookup"><span data-stu-id="07fbf-373">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="07fbf-374">**Kopiowane do folderu z kropką w nazwie pliku zawartości**</span><span class="sxs-lookup"><span data-stu-id="07fbf-374">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="07fbf-375">W takim przypadku NuGet widzi, że rozszerzenie w `target` nie pasuje do rozszerzenia w `src` i w związku z tym traktuje część nazwy w `target` jako folder:</span><span class="sxs-lookup"><span data-stu-id="07fbf-375">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="07fbf-376">**Pliki zawartości bez rozszerzenia**</span><span class="sxs-lookup"><span data-stu-id="07fbf-376">**Content files without extensions**</span></span>

<span data-ttu-id="07fbf-377">Aby uwzględnić pliki bez rozszerzenia, należy użyć `*` lub `**` symboli wieloznacznych:</span><span class="sxs-lookup"><span data-stu-id="07fbf-377">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="07fbf-378">**Pliki zawartości ze ścieżki głębokie i celem bezpośrednich**</span><span class="sxs-lookup"><span data-stu-id="07fbf-378">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="07fbf-379">W takim przypadku ponieważ pasuje do rozszerzenia plików źródłowych i docelowych, NuGet zakłada, że element docelowy nazwę pliku, a nie folder:</span><span class="sxs-lookup"><span data-stu-id="07fbf-379">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="07fbf-380">**Zmiana nazwy pliku zawartości w pakiecie**</span><span class="sxs-lookup"><span data-stu-id="07fbf-380">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="07fbf-381">**Wykluczanie plików**</span><span class="sxs-lookup"><span data-stu-id="07fbf-381">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="07fbf-382">Za pomocą elementu pliki plików zawartości</span><span class="sxs-lookup"><span data-stu-id="07fbf-382">Using the contentFiles element for content files</span></span>

<span data-ttu-id="07fbf-383">*NuGet 4.0 + z PackageReference*</span><span class="sxs-lookup"><span data-stu-id="07fbf-383">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="07fbf-384">Domyślnie pakiet umieszcza zawartość `contentFiles` folder (patrz poniżej) i `nuget pack` uwzględnione wszystkie pliki w tym folderze przy użyciu atrybutów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="07fbf-384">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="07fbf-385">W takim przypadku nie jest konieczne jest stosowanie `contentFiles` w węźle `.nuspec` wcale.</span><span class="sxs-lookup"><span data-stu-id="07fbf-385">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="07fbf-386">Do kontroli, które pliki są uwzględnione `<contentFiles>` element określa jest kolekcją `<files>` obejmują elementy, które identyfikują konkretne pliki.</span><span class="sxs-lookup"><span data-stu-id="07fbf-386">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="07fbf-387">Te pliki są określane za pomocą zestawu atrybutów, które opisują jak powinny być używane w ramach systemu projektu:</span><span class="sxs-lookup"><span data-stu-id="07fbf-387">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="07fbf-388">Atrybut</span><span class="sxs-lookup"><span data-stu-id="07fbf-388">Attribute</span></span> | <span data-ttu-id="07fbf-389">Opis</span><span class="sxs-lookup"><span data-stu-id="07fbf-389">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07fbf-390">**include**</span><span class="sxs-lookup"><span data-stu-id="07fbf-390">**include**</span></span> | <span data-ttu-id="07fbf-391">(Wymagane) Lokalizacja pliku lub plików do uwzględnienia, mogą ulec wykluczenia określony przez `exclude` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-391">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="07fbf-392">Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="07fbf-392">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="07fbf-393">Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="07fbf-393">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="07fbf-394">**exclude**</span><span class="sxs-lookup"><span data-stu-id="07fbf-394">**exclude**</span></span> | <span data-ttu-id="07fbf-395">Rozdzielana średnikami lista plików lub wzorców plików do wykluczenia z `src` lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="07fbf-395">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="07fbf-396">Wieloznaczny `*` jest dozwolone i podwójne symbol wieloznaczny `**` oznacza cyklicznego folderu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="07fbf-396">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="07fbf-397">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="07fbf-397">**buildAction**</span></span> | <span data-ttu-id="07fbf-398">Akcja kompilacji można przypisać do elementu zawartości dla programu MSBuild, takich jak `Content`, `None`, `Embedded Resource`, `Compile`itp. Wartość domyślna to `Compile`.</span><span class="sxs-lookup"><span data-stu-id="07fbf-398">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="07fbf-399">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="07fbf-399">**copyToOutput**</span></span> | <span data-ttu-id="07fbf-400">Wartość logiczna wskazująca, czy skopiować elementy zawartości do kompilacji (lub opublikować) folder wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="07fbf-400">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="07fbf-401">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="07fbf-401">The default is false.</span></span> |
| <span data-ttu-id="07fbf-402">**spłaszczanie**</span><span class="sxs-lookup"><span data-stu-id="07fbf-402">**flatten**</span></span> | <span data-ttu-id="07fbf-403">Wartość logiczna wskazująca, czy można skopiować elementy zawartości do pojedynczego folderu w danych wyjściowych kompilacji (true) czy zachowanie struktury folderów w pakiecie (false).</span><span class="sxs-lookup"><span data-stu-id="07fbf-403">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="07fbf-404">Ta flaga działa tylko wtedy, gdy copyToOutput flaga jest ustawiona na true.</span><span class="sxs-lookup"><span data-stu-id="07fbf-404">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="07fbf-405">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="07fbf-405">The default is false.</span></span> |

<span data-ttu-id="07fbf-406">Podczas instalowania pakietu, NuGet stosuje elementy podrzędne `<contentFiles>` od góry do dołu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-406">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="07fbf-407">Jeśli wiele wpisów pasuje do tego samego pliku wszystkie wpisy są stosowane.</span><span class="sxs-lookup"><span data-stu-id="07fbf-407">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="07fbf-408">Wpis najwyższy przesłania wpisy niższe konflikt dla tego samego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="07fbf-408">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="07fbf-409">Struktura folderów pakietu</span><span class="sxs-lookup"><span data-stu-id="07fbf-409">Package folder structure</span></span>

<span data-ttu-id="07fbf-410">Projekt pakietu wymagana struktura zawartości przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="07fbf-410">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="07fbf-411">`codeLanguages` może być `cs`, `vb`, `fs`, `any`, lub małe odpowiednikiem danego `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="07fbf-411">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="07fbf-412">`TxM` jest żadnych moniker platformy docelowej prawnych, która obsługuje NuGet (zobacz [platform docelowych](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="07fbf-412">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="07fbf-413">Dowolnej struktury folderów może dołączany na końcu tej składni.</span><span class="sxs-lookup"><span data-stu-id="07fbf-413">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="07fbf-414">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="07fbf-414">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="07fbf-415">Można użyć puste foldery `.` rezygnacji z zawarto dla niektórych kombinacji języka i TxM, na przykład:</span><span class="sxs-lookup"><span data-stu-id="07fbf-415">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="07fbf-416">Przykładowe pliki sekcji</span><span class="sxs-lookup"><span data-stu-id="07fbf-416">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="07fbf-417">Przykład .nuspec plików</span><span class="sxs-lookup"><span data-stu-id="07fbf-417">Example .nuspec files</span></span>

<span data-ttu-id="07fbf-418">**Prosty `.nuspec` które nie określają zależności lub plików**</span><span class="sxs-lookup"><span data-stu-id="07fbf-418">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="07fbf-419">**A `.nuspec` z zależnościami**</span><span class="sxs-lookup"><span data-stu-id="07fbf-419">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="07fbf-420">**A `.nuspec` z plikami**</span><span class="sxs-lookup"><span data-stu-id="07fbf-420">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="07fbf-421">**A `.nuspec` z zestawów struktury**</span><span class="sxs-lookup"><span data-stu-id="07fbf-421">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="07fbf-422">W tym przykładzie poniżej są zainstalowane dla określonego projektu celów:</span><span class="sxs-lookup"><span data-stu-id="07fbf-422">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="07fbf-423">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="07fbf-423">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="07fbf-424">. NET4 -> Client Profile `System.Net`</span><span class="sxs-lookup"><span data-stu-id="07fbf-424">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="07fbf-425">-> Silverlight 3 `System.Json`</span><span class="sxs-lookup"><span data-stu-id="07fbf-425">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="07fbf-426">-> Programu Silverlight 4 `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="07fbf-426">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="07fbf-427">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="07fbf-427">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
