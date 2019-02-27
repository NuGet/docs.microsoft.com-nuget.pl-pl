---
title: Odwołanie do wersji pakietu NuGet
description: Szczegółowymi informacjami na temat na temat określania numerów wersji i zakresy dla innych pakietów, od którego zależy od pakietu NuGet i jak zależności są zainstalowane.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852471"
---
# <a name="package-versioning"></a><span data-ttu-id="c0518-103">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="c0518-103">Package versioning</span></span>

<span data-ttu-id="c0518-104">Określony pakiet zawsze jest określany za pomocą jego identyfikatora pakietu i liczbą dokładna wersja.</span><span class="sxs-lookup"><span data-stu-id="c0518-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="c0518-105">Na przykład [Entity Framework](https://www.nuget.org/packages/EntityFramework/) w witrynie nuget.org zawiera kilka tuzinów określone pakiety dostępne od wersji *4.1.10311* do wersji *6.1.3* (Najnowsza wersja stabilna wydania) i różne wersje wstępne, takie jak *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="c0518-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="c0518-106">Tworząc pakiet, możesz przypisać odpowiedniego numeru wersji sufiks opcjonalny tekst wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="c0518-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="c0518-107">Podczas korzystania z pakietów, z drugiej strony, można określić numeru wersji dokładne lub zakres dopuszczalnych wersji.</span><span class="sxs-lookup"><span data-stu-id="c0518-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="c0518-108">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="c0518-108">In this topic:</span></span>

- <span data-ttu-id="c0518-109">[Podstawowe informacje o wersji](#version-basics) tym sufiksy wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="c0518-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="c0518-110">Zakresów wersji i symboli wieloznacznych</span><span class="sxs-lookup"><span data-stu-id="c0518-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="c0518-111">Numery wersji znormalizowana</span><span class="sxs-lookup"><span data-stu-id="c0518-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="c0518-112">Podstawowe informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="c0518-112">Version basics</span></span>

<span data-ttu-id="c0518-113">Numer wersji określonego ma postać *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]*, których składniki mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="c0518-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="c0518-114">*Główne*: Zmiany powodujące niezgodność</span><span class="sxs-lookup"><span data-stu-id="c0518-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="c0518-115">*Drobne*: Nowe funkcje, ale wstecznie zgodne</span><span class="sxs-lookup"><span data-stu-id="c0518-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="c0518-116">*Poprawka*: Wstecznie zgodny poprawek błędów oprogramowania tylko</span><span class="sxs-lookup"><span data-stu-id="c0518-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="c0518-117">*-Sufiks* (opcjonalnie): łącznik następuje ciąg oznaczający wersji wstępnej (następujących [Konwencji Semantic Versioning lub SemVer 1.0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="c0518-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="c0518-118">**Przykłady:**</span><span class="sxs-lookup"><span data-stu-id="c0518-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="c0518-119">nuget.org odrzuca wszelkie przekazywania pakietu, który nie ma numeru wersji dokładne.</span><span class="sxs-lookup"><span data-stu-id="c0518-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="c0518-120">Wersja musi być określona w `.nuspec` lub plik projektu do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="c0518-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="c0518-121">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="c0518-121">Pre-release versions</span></span>

<span data-ttu-id="c0518-122">Technicznie rzecz biorąc, twórców pakietów można użyć jako sufiks dowolnego ciągu do oznaczania wersji wstępnej, jak NuGet traktuje takie wersji jako wersji wstępnej i sprawia, że nie inne interpretacji.</span><span class="sxs-lookup"><span data-stu-id="c0518-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="c0518-123">Oznacza to wyświetla NuGet pełną wersję ciągu, niezależnie od interfejsu użytkownika uczestniczy, pozostawiając żadnej interpretacji znaczenie tego sufiksu konsumenta.</span><span class="sxs-lookup"><span data-stu-id="c0518-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="c0518-124">Inaczej mówiąc, deweloperów pakietu zazwyczaj korzystają z rozpoznanym konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="c0518-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="c0518-125">`-alpha`: Wersja alfa, zwykle używane do pracy w toku i eksperymentowanie.</span><span class="sxs-lookup"><span data-stu-id="c0518-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="c0518-126">`-beta`: Wydania beta, zazwyczaj taki, który jest funkcja ukończone przez następne zaplanowane wersji, ale może zawierać znanych błędów.</span><span class="sxs-lookup"><span data-stu-id="c0518-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="c0518-127">`-rc`: W wersji Release candidate, zwykle wydania jest potencjalnie ostateczne (stable), chyba że wyłaniać znaczące błędy.</span><span class="sxs-lookup"><span data-stu-id="c0518-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="c0518-128">Obsługuje NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), który obsługuje numerów wersji wstępnej przy użyciu notacji z kropką, podobnie jak w *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="c0518-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="c0518-129">Kropkowego jest nieobsługiwane w przypadku wersje NuGet wcześniejsze niż 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="c0518-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="c0518-130">Można użyć formy, takich jak *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="c0518-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="c0518-131">Podczas rozpoznawania odwołań do pakietów i wiele wersji pakietu różnią się jedynie sufiks, NuGet najpierw wybierze wersji bez sufiksu, a następnie stosuje pierwszeństwo wersji wstępnych w odwrotnej kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="c0518-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="c0518-132">Na przykład następujące wersje powinny być wybierane w takiej kolejności, które są wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="c0518-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="c0518-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c0518-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="c0518-134">Za pomocą NuGet 4.3.0+ i programu Visual Studio 2017 w wersji 15.3 + obsługuje NuGet [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="c0518-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="c0518-135">Niektóre semantyki SemVer v2.0.0 nie są obsługiwane w starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="c0518-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="c0518-136">NuGet uwzględnia wersję pakietu do określonego v2.0.0 SemVer, jeśli jest spełniony jeden z następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="c0518-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="c0518-137">Przed wydaniem etykieta jest oddzielona, na przykład *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="c0518-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="c0518-138">Wersja ma metadane kompilacji, na przykład *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="c0518-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="c0518-139">Dla nuget.org pakiet jest zdefiniowana jako pakiet v2.0.0 SemVer, jeśli spełniony jest dowolny z następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="c0518-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="c0518-140">Wersja tego pakietu jest v2.0.0 SemVer zgodne, ale nie SemVer 1.0.0 zgodne, jak określono powyżej.</span><span class="sxs-lookup"><span data-stu-id="c0518-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="c0518-141">Żadnego z zakresów wersji zależności pakietu ma minimalnych i maksymalnych wersji v2.0.0 SemVer zgodne, ale nie SemVer 1.0.0 zgodne, zdefiniowane powyżej. na przykład *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="c0518-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="c0518-142">Jeśli załadujesz pakietu specyficzne dla v2.0.0 SemVer na stronie nuget.org, pakiet jest niewidoczne dla starszych klientów i dostępne, aby tylko następujących klientów NuGet:</span><span class="sxs-lookup"><span data-stu-id="c0518-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="c0518-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="c0518-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="c0518-144">Visual Studio 2017 w wersji 15.3 +</span><span class="sxs-lookup"><span data-stu-id="c0518-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="c0518-145">Visual Studio 2015 z [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="c0518-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="c0518-146">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="c0518-146">dotnet</span></span>
  - <span data-ttu-id="c0518-147">dotnetcore.exe (2.0.0+ zestawu .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="c0518-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="c0518-148">Klienci firm:</span><span class="sxs-lookup"><span data-stu-id="c0518-148">Third-party clients:</span></span>

- <span data-ttu-id="c0518-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="c0518-149">JetBrains Rider</span></span>
- <span data-ttu-id="c0518-150">Paket w wersji 5.0 +</span><span class="sxs-lookup"><span data-stu-id="c0518-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="c0518-151">Zakresów wersji i symboli wieloznacznych</span><span class="sxs-lookup"><span data-stu-id="c0518-151">Version ranges and wildcards</span></span>

<span data-ttu-id="c0518-152">W odniesieniu do zależności pakietów NuGet obsługuje przy użyciu notacji interwału do określania zakresów wersji, podsumować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c0518-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="c0518-153">Notacja</span><span class="sxs-lookup"><span data-stu-id="c0518-153">Notation</span></span> | <span data-ttu-id="c0518-154">Zastosowana reguła</span><span class="sxs-lookup"><span data-stu-id="c0518-154">Applied rule</span></span> | <span data-ttu-id="c0518-155">Opis</span><span class="sxs-lookup"><span data-stu-id="c0518-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="c0518-156">1.0</span><span class="sxs-lookup"><span data-stu-id="c0518-156">1.0</span></span> | <span data-ttu-id="c0518-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="c0518-157">x ≥ 1.0</span></span> | <span data-ttu-id="c0518-158">Minimalna wersja (włącznie)</span><span class="sxs-lookup"><span data-stu-id="c0518-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="c0518-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="c0518-159">(1.0,)</span></span> | <span data-ttu-id="c0518-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="c0518-160">x > 1.0</span></span> | <span data-ttu-id="c0518-161">Minimalna wersja wyłączne</span><span class="sxs-lookup"><span data-stu-id="c0518-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="c0518-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="c0518-162">[1.0]</span></span> | <span data-ttu-id="c0518-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="c0518-163">x == 1.0</span></span> | <span data-ttu-id="c0518-164">Dokładna wersja dopasowania</span><span class="sxs-lookup"><span data-stu-id="c0518-164">Exact version match</span></span> |
| <span data-ttu-id="c0518-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="c0518-165">(,1.0]</span></span> | <span data-ttu-id="c0518-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="c0518-166">x ≤ 1.0</span></span> | <span data-ttu-id="c0518-167">Maksymalna wersja (włącznie)</span><span class="sxs-lookup"><span data-stu-id="c0518-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="c0518-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="c0518-168">(,1.0)</span></span> | <span data-ttu-id="c0518-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="c0518-169">x < 1.0</span></span> | <span data-ttu-id="c0518-170">Maksymalna wersja wyłączne</span><span class="sxs-lookup"><span data-stu-id="c0518-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="c0518-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="c0518-171">[1.0,2.0]</span></span> | <span data-ttu-id="c0518-172">X ≤ 1.0 ≤ w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="c0518-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="c0518-173">Dokładny zakres (włącznie)</span><span class="sxs-lookup"><span data-stu-id="c0518-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="c0518-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="c0518-174">(1.0,2.0)</span></span> | <span data-ttu-id="c0518-175">1.0 < x < w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="c0518-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="c0518-176">Dokładny zakres wyłączne</span><span class="sxs-lookup"><span data-stu-id="c0518-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="c0518-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="c0518-177">[1.0,2.0)</span></span> | <span data-ttu-id="c0518-178">1.0 ≤ x < w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="c0518-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="c0518-179">Mieszane włącznie minimalną i wyłączne maksymalna wersja</span><span class="sxs-lookup"><span data-stu-id="c0518-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="c0518-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="c0518-180">(1.0)</span></span>    | <span data-ttu-id="c0518-181">nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="c0518-181">invalid</span></span> | <span data-ttu-id="c0518-182">nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="c0518-182">invalid</span></span> |

<span data-ttu-id="c0518-183">Gdy w formacie PackageReference NuGet obsługuje również za pomocą notacji symbolu wieloznacznego, \*, główne, pomocnicze, poprawki i sufiks wersji wstępnej części numeru.</span><span class="sxs-lookup"><span data-stu-id="c0518-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="c0518-184">Symbole wieloznaczne nie są obsługiwane z `packages.config` formatu.</span><span class="sxs-lookup"><span data-stu-id="c0518-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="c0518-185">Wersje wstępne nie są uwzględniane podczas rozpoznawania zakresów wersji.</span><span class="sxs-lookup"><span data-stu-id="c0518-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="c0518-186">Wersji wstępnych *są* uwzględniana podczas użycie symbolu wieloznacznego (\*).</span><span class="sxs-lookup"><span data-stu-id="c0518-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="c0518-187">Zakres wersji *[1.0,2.0]*, na przykład, nie ma w wersji 2.0 w wersji beta, ale notacji symbolu wieloznacznego _w wersji 2.0 — \*_ jest.</span><span class="sxs-lookup"><span data-stu-id="c0518-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="c0518-188">Zobacz [wystawiać 912](https://github.com/NuGet/Home/issues/912) do dalszego dyskusji na temat symboli wieloznacznych w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="c0518-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="c0518-189">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c0518-189">Examples</span></span>

<span data-ttu-id="c0518-190">Zawsze określać wersja lub zakres wersji w przypadku zależności pakietów w plikach projektu `packages.config` plików, a `.nuspec` plików.</span><span class="sxs-lookup"><span data-stu-id="c0518-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="c0518-191">Bez wersji lub zakres wersji, NuGet 2.8.x, a wcześniej najnowszej wersji pakietu dostępne podczas rozpoznawania zależności natomiast NuGet 3.x, a później Najniższa wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="c0518-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="c0518-192">Określanie wersji lub czy zakres pozwala uniknąć niepewności.</span><span class="sxs-lookup"><span data-stu-id="c0518-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="c0518-193">Odwołania w plikach projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="c0518-193">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="c0518-194">**Przywoływane w `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="c0518-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="c0518-195">W `packages.config`, zależności, co jest wyświetlany na liście dokładnie `version` atrybut, który jest używany podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c0518-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="c0518-196">`allowedVersions` Atrybut jest używany tylko podczas operacji aktualizacji, ograniczenie wersji, do których pakiet mogły zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="c0518-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="c0518-197">**Przywoływane w `.nuspec` plików**</span><span class="sxs-lookup"><span data-stu-id="c0518-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="c0518-198">`version` Atrybutu w `<dependency>` element zawiera opis wersji zakresu, które mogą być stosowane dla zależności.</span><span class="sxs-lookup"><span data-stu-id="c0518-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="c0518-199">Numery wersji znormalizowana</span><span class="sxs-lookup"><span data-stu-id="c0518-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="c0518-200">Jest to istotną zmianę dla NuGet 3.4 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="c0518-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="c0518-201">Podczas uzyskiwania pakietów z repozytorium, podczas instalacji, ponownie zainstaluj lub operacji przywracania NuGet 3.4 + traktuje numery wersji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c0518-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="c0518-202">Zer wiodących są usuwane z numerami wersji:</span><span class="sxs-lookup"><span data-stu-id="c0518-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="c0518-203">W czwartej części numeru wersji wartość zero zostanie pominięta.</span><span class="sxs-lookup"><span data-stu-id="c0518-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="c0518-204">Ta normalizacji nie ma wpływu na numery wersji pakietów. ma to wpływ, jak NuGet jest zgodny tylko wersje podczas rozpoznawania zależności.</span><span class="sxs-lookup"><span data-stu-id="c0518-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="c0518-205">Jednak repozytoriów pakietów NuGet musi traktować te wartości w taki sam sposób jak NuGet, aby uniknąć duplikowania wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="c0518-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="c0518-206">Tym samym repozytorium, które zawiera wersję *1.0* pakietu nie powinien również hostować wersji *1.0.0* jako oddzielny i inny pakiet.</span><span class="sxs-lookup"><span data-stu-id="c0518-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
