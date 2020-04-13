---
title: Odwołanie do wersji pakietu NuGet
description: Dokładne szczegóły dotyczące określania numerów wersji i zakresów dla innych pakietów, od których zależy pakiet NuGet i jak są instalowane zależności.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147451"
---
# <a name="package-versioning"></a><span data-ttu-id="cc20a-103">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="cc20a-103">Package versioning</span></span>

<span data-ttu-id="cc20a-104">Określony pakiet jest zawsze odwoływany przy użyciu jego identyfikator pakietu i dokładny numer wersji.</span><span class="sxs-lookup"><span data-stu-id="cc20a-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="cc20a-105">Na przykład [entity framework](https://www.nuget.org/packages/EntityFramework/) na nuget.org ma kilkadziesiąt konkretnych pakietów dostępnych, od wersji *4.1.10311* do wersji *6.1.3* (najnowsza stabilna wersja) i różnych wersji przedpremierowych, takich jak *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="cc20a-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="cc20a-106">Podczas tworzenia pakietu należy przypisać określony numer wersji z opcjonalnym sufiksem tekstu w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="cc20a-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="cc20a-107">Podczas korzystania z pakietów, z drugiej strony, można określić dokładny numer wersji lub zakres dopuszczalnych wersji.</span><span class="sxs-lookup"><span data-stu-id="cc20a-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="cc20a-108">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="cc20a-108">In this topic:</span></span>

- <span data-ttu-id="cc20a-109">[Podstawy wersji,](#version-basics) w tym sufiksy wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="cc20a-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="cc20a-110">Zakresy wersji</span><span class="sxs-lookup"><span data-stu-id="cc20a-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="cc20a-111">Znormalizowane numery wersji</span><span class="sxs-lookup"><span data-stu-id="cc20a-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="cc20a-112">Podstawy wersji</span><span class="sxs-lookup"><span data-stu-id="cc20a-112">Version basics</span></span>

<span data-ttu-id="cc20a-113">Określony numer wersji jest w postaci *Major.Minor.Patch[-Sufiks]*, gdzie składniki mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="cc20a-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="cc20a-114">*Główne*: Przełomowe zmiany</span><span class="sxs-lookup"><span data-stu-id="cc20a-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="cc20a-115">*Minor*: Nowe funkcje, ale wstecznie kompatybilne</span><span class="sxs-lookup"><span data-stu-id="cc20a-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="cc20a-116">*Poprawka:* Tylko poprawki błędów zgodne z powrotem</span><span class="sxs-lookup"><span data-stu-id="cc20a-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="cc20a-117">*-Sufiks* (opcjonalnie): myślnik, po którym następuje ciąg oznaczający wersję wstępną (po [konwencji Semantic Versioning lub SemVer 1.0).](https://semver.org/spec/v1.0.0.html)</span><span class="sxs-lookup"><span data-stu-id="cc20a-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="cc20a-118">**Przykłady:**</span><span class="sxs-lookup"><span data-stu-id="cc20a-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="cc20a-119">nuget.org odrzuca wszystkie przesłane pakiety, które nie mają dokładnego numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="cc20a-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="cc20a-120">Wersja musi być określona `.nuspec` w pliku lub projektu użytym do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="cc20a-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="cc20a-121">Wersje w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="cc20a-121">Pre-release versions</span></span>

<span data-ttu-id="cc20a-122">Technicznie rzecz biorąc twórcy pakietu mogą używać dowolnego ciągu jako sufiksu do oznaczania wersji wstępnej, ponieważ NuGet traktuje dowolną taką wersję jako wersję wstępną i nie wykonuje żadnej innej interpretacji.</span><span class="sxs-lookup"><span data-stu-id="cc20a-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="cc20a-123">Oznacza to, że NuGet wyświetla ciąg pełnej wersji w cokolwiek interfejsu użytkownika jest zaangażowany, pozostawiając wszelkie interpretacji znaczenia sufiksu do konsumenta.</span><span class="sxs-lookup"><span data-stu-id="cc20a-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="cc20a-124">Mimo to deweloperzy pakietów zazwyczaj przestrzegają uznanych konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="cc20a-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="cc20a-125">`-alpha`: Alpha release, zwykle używane do pracy w toku i eksperymentowania.</span><span class="sxs-lookup"><span data-stu-id="cc20a-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="cc20a-126">`-beta`: Wersja beta, zazwyczaj taka, która jest kompletna dla następnej planowanej wersji, ale może zawierać znane błędy.</span><span class="sxs-lookup"><span data-stu-id="cc20a-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="cc20a-127">`-rc`: Release candidate, zazwyczaj wydanie, które jest potencjalnie ostateczne (stabilne), chyba że pojawią się istotne błędy.</span><span class="sxs-lookup"><span data-stu-id="cc20a-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="cc20a-128">NuGet 4.3.0+ obsługuje [semver 2.0.0](https://semver.org/spec/v2.0.0.html), który obsługuje numery wersji wstępnej z notacją kropkową, jak w *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="cc20a-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="cc20a-129">Notacja kropki nie jest obsługiwana w wersjach NuGet przed wersją 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="cc20a-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="cc20a-130">Można użyć formularza takiego jak *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="cc20a-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="cc20a-131">Podczas rozwiązywania odwołań do pakietu i wielu wersji pakietu różnią się tylko przez sufiks, NuGet wybiera wersję bez sufiksu pierwszy, a następnie stosuje pierwszeństwo do wersji przed wydaniem w odwrotnej kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="cc20a-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="cc20a-132">Na przykład w podanej kolejności zostaną wybrane następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="cc20a-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="cc20a-133">Przechowywanie wersji semantycznych 2.0.0</span><span class="sxs-lookup"><span data-stu-id="cc20a-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="cc20a-134">Z NuGet 4.3.0+ i Visual Studio 2017 w wersji 15.3+, NuGet obsługuje [semantyczne przechowywanie wersji 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="cc20a-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="cc20a-135">Niektóre semantyki SemVer v2.0.0 nie są obsługiwane w starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="cc20a-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="cc20a-136">NuGet uważa, że wersja pakietu jest SemVer v2.0.0 specyficzne, jeśli którakolwiek z następujących instrukcji jest spełniony:</span><span class="sxs-lookup"><span data-stu-id="cc20a-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="cc20a-137">Etykieta wydania wstępnego jest oddzielona kropkami, na przykład *1.0.0-alfa.1*</span><span class="sxs-lookup"><span data-stu-id="cc20a-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="cc20a-138">Wersja ma build-metadane, na przykład *1.0.0+ githash*</span><span class="sxs-lookup"><span data-stu-id="cc20a-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="cc20a-139">Dla nuget.org pakiet jest zdefiniowany jako pakiet SemVer w wersji 2.0.0, jeśli spełniony jest jeden z następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="cc20a-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="cc20a-140">Wersja własna pakietu jest zgodna ze standardem SemVer v2.0.0, ale nie zgodna ze standardem SemVer v1.0.0, jak zdefiniowano powyżej.</span><span class="sxs-lookup"><span data-stu-id="cc20a-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="cc20a-141">Każdy z zakresów wersji zależności pakietu ma minimalną lub maksymalną wersję, która jest zgodna z SemVer v2.0.0, ale nie jest zgodna z SemVer v1.0.0, zdefiniowana powyżej; na przykład *[1.0.0-alfa.1, ).*</span><span class="sxs-lookup"><span data-stu-id="cc20a-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="cc20a-142">Jeśli przekażesz pakiet specyficzny dla SemVer w wersji 2.0.0 do nuget.org, pakiet jest niewidoczny dla starszych klientów i dostępny tylko dla następujących klientów NuGet:</span><span class="sxs-lookup"><span data-stu-id="cc20a-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="cc20a-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="cc20a-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="cc20a-144">Visual Studio 2017 w wersji 15.3+</span><span class="sxs-lookup"><span data-stu-id="cc20a-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="cc20a-145">Visual Studio 2015 z [NuGet VSIX w wersji 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="cc20a-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="cc20a-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="cc20a-146">dotnet</span></span>
  - <span data-ttu-id="cc20a-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="cc20a-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="cc20a-148">Klienci zewnętrzni:</span><span class="sxs-lookup"><span data-stu-id="cc20a-148">Third-party clients:</span></span>

- <span data-ttu-id="cc20a-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="cc20a-149">JetBrains Rider</span></span>
- <span data-ttu-id="cc20a-150">Paket wersja 5.0+</span><span class="sxs-lookup"><span data-stu-id="cc20a-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="cc20a-151">Zakresy wersji</span><span class="sxs-lookup"><span data-stu-id="cc20a-151">Version ranges</span></span>

<span data-ttu-id="cc20a-152">Odnosząc się do zależności pakietów, NuGet obsługuje przy użyciu notacji interwału do określania zakresów wersji, podsumowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cc20a-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="cc20a-153">Notacja</span><span class="sxs-lookup"><span data-stu-id="cc20a-153">Notation</span></span> | <span data-ttu-id="cc20a-154">Reguła stosowana</span><span class="sxs-lookup"><span data-stu-id="cc20a-154">Applied rule</span></span> | <span data-ttu-id="cc20a-155">Opis</span><span class="sxs-lookup"><span data-stu-id="cc20a-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="cc20a-156">1.0</span><span class="sxs-lookup"><span data-stu-id="cc20a-156">1.0</span></span> | <span data-ttu-id="cc20a-157">x ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="cc20a-157">x ≥ 1.0</span></span> | <span data-ttu-id="cc20a-158">Wersja minimalna włącznie</span><span class="sxs-lookup"><span data-stu-id="cc20a-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="cc20a-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="cc20a-159">(1.0,)</span></span> | <span data-ttu-id="cc20a-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="cc20a-160">x > 1.0</span></span> | <span data-ttu-id="cc20a-161">Wersja minimalna, ekskluzywna</span><span class="sxs-lookup"><span data-stu-id="cc20a-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="cc20a-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="cc20a-162">[1.0]</span></span> | <span data-ttu-id="cc20a-163">x == 1,0</span><span class="sxs-lookup"><span data-stu-id="cc20a-163">x == 1.0</span></span> | <span data-ttu-id="cc20a-164">Dokładne dopasowanie wersji</span><span class="sxs-lookup"><span data-stu-id="cc20a-164">Exact version match</span></span> |
| <span data-ttu-id="cc20a-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="cc20a-165">(,1.0]</span></span> | <span data-ttu-id="cc20a-166">x ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="cc20a-166">x ≤ 1.0</span></span> | <span data-ttu-id="cc20a-167">Maksymalna wersja włącznie</span><span class="sxs-lookup"><span data-stu-id="cc20a-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="cc20a-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="cc20a-168">(,1.0)</span></span> | <span data-ttu-id="cc20a-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="cc20a-169">x < 1.0</span></span> | <span data-ttu-id="cc20a-170">Maksymalna wersja, ekskluzywna</span><span class="sxs-lookup"><span data-stu-id="cc20a-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="cc20a-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="cc20a-171">[1.0,2.0]</span></span> | <span data-ttu-id="cc20a-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="cc20a-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="cc20a-173">Dokładny zakres, włącznie</span><span class="sxs-lookup"><span data-stu-id="cc20a-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="cc20a-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="cc20a-174">(1.0,2.0)</span></span> | <span data-ttu-id="cc20a-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="cc20a-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="cc20a-176">Dokładny zakres, ekskluzywny</span><span class="sxs-lookup"><span data-stu-id="cc20a-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="cc20a-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="cc20a-177">[1.0,2.0)</span></span> | <span data-ttu-id="cc20a-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="cc20a-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="cc20a-179">Mieszana minimalna i ekskluzywna wersja maksymalna włącznie</span><span class="sxs-lookup"><span data-stu-id="cc20a-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="cc20a-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="cc20a-180">(1.0)</span></span>    | <span data-ttu-id="cc20a-181">nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="cc20a-181">invalid</span></span> | <span data-ttu-id="cc20a-182">nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="cc20a-182">invalid</span></span> |

<span data-ttu-id="cc20a-183">Podczas korzystania z PackageReference format, NuGet obsługuje \*również przy użyciu zmiennoprzecinkowy notacji, dla głównych, minor, patch i pre-release sufiks części numeru.</span><span class="sxs-lookup"><span data-stu-id="cc20a-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="cc20a-184">Wersje przestawne nie `packages.config` są obsługiwane w formacie.</span><span class="sxs-lookup"><span data-stu-id="cc20a-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="cc20a-185">Zakresy wersji w PackageReference obejmują wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="cc20a-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="cc20a-186">Zgodnie z projektem wersje przestawne nie rozwiązują wersji wstępnej, chyba że zostanie to uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="cc20a-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="cc20a-187">Aby uzyskać stan powiązanego żądania funkcji, zobacz [problem 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="cc20a-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="cc20a-188">Przykłady</span><span class="sxs-lookup"><span data-stu-id="cc20a-188">Examples</span></span>

<span data-ttu-id="cc20a-189">Zawsze określ zakres wersji lub wersji dla `packages.config` zależności pakietów w plikach, plikach i `.nuspec` plikach projektu.</span><span class="sxs-lookup"><span data-stu-id="cc20a-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="cc20a-190">Bez zakresu wersji lub wersji NuGet 2.8.x i wcześniej wybiera najnowszą dostępną wersję pakietu podczas rozpoznawania zależności, podczas gdy NuGet 3.x i nowsze wybiera najniższą wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="cc20a-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="cc20a-191">Określenie zakresu wersji lub wersji pozwala uniknąć tej niepewności.</span><span class="sxs-lookup"><span data-stu-id="cc20a-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="cc20a-192">Odwołania w plikach projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="cc20a-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="cc20a-193">**Odniesienia w: `packages.config`**</span><span class="sxs-lookup"><span data-stu-id="cc20a-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="cc20a-194">W `packages.config`obszarze , każda zależność `version` jest wyświetlana z dokładnym atrybutem, który jest używany podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="cc20a-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="cc20a-195">Atrybut `allowedVersions` jest używany tylko podczas operacji aktualizacji, aby ograniczyć wersje, do których pakiet może być aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="cc20a-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="cc20a-196">**Odwołania w `.nuspec` plikach**</span><span class="sxs-lookup"><span data-stu-id="cc20a-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="cc20a-197">Atrybut `version` w elemencie `<dependency>` opisuje wersje zakresu, które są dopuszczalne dla zależności.</span><span class="sxs-lookup"><span data-stu-id="cc20a-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="cc20a-198">Znormalizowane numery wersji</span><span class="sxs-lookup"><span data-stu-id="cc20a-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="cc20a-199">Jest to przełomowa zmiana dla NuGet 3.4 i nowsze.</span><span class="sxs-lookup"><span data-stu-id="cc20a-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="cc20a-200">Podczas uzyskiwania pakietów z repozytorium podczas operacji instalacji, ponownej instalacji lub przywracania nuget 3.4+ traktuje numery wersji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cc20a-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="cc20a-201">Zera wiodące są usuwane z numerów wersji:</span><span class="sxs-lookup"><span data-stu-id="cc20a-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="cc20a-202">Zero w czwartej części numeru wersji zostanie pominięte</span><span class="sxs-lookup"><span data-stu-id="cc20a-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- <span data-ttu-id="cc20a-203">Metadane kompilacji SemVer 2.0.0 są usuwane</span><span class="sxs-lookup"><span data-stu-id="cc20a-203">SemVer 2.0.0 build metadata is removed</span></span>

        1.0.7+r3456 is treated as 1.0.7

<span data-ttu-id="cc20a-204">`pack`i `restore` operacje normalizują wersje, gdy tylko jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="cc20a-204">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="cc20a-205">W przypadku pakietów już utworzonych ta normalizacja nie wpływa na numery wersji w samych pakietach; wpływa tylko na to, jak NuGet dopasowuje wersje podczas rozpoznawania zależności.</span><span class="sxs-lookup"><span data-stu-id="cc20a-205">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="cc20a-206">Jednak repozytoria pakietów NuGet muszą traktować te wartości w taki sam sposób jak NuGet, aby zapobiec duplikowaniu wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="cc20a-206">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="cc20a-207">W związku z tym repozytorium, które zawiera wersję *1.0* pakietu nie należy również hostować wersji *1.0.0* jako oddzielny i inny pakiet.</span><span class="sxs-lookup"><span data-stu-id="cc20a-207">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
