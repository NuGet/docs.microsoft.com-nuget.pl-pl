---
title: Dokumentacja wersji pakietu NuGet
description: Dokładne szczegóły dotyczące określania numerów wersji i zakresów dla innych pakietów, od których zależy pakiet NuGet, oraz sposobu instalowania zależności.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2020
ms.locfileid: "80147451"
---
# <a name="package-versioning"></a><span data-ttu-id="08c61-103">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="08c61-103">Package versioning</span></span>

<span data-ttu-id="08c61-104">Określony pakiet zawsze jest określany przy użyciu identyfikatora pakietu i dokładnego numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="08c61-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="08c61-105">Na przykład [Entity Framework](https://www.nuget.org/packages/EntityFramework/) w NuGet.org ma kilka dziesiątych dostępnych pakietów, od wersji *4.1.10311* do wersji *6.1.3* (najnowszej stabilnej wersji) i różne wersje wstępne, takie jak *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="08c61-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="08c61-106">Podczas tworzenia pakietu przypisujesz określony numer wersji z opcjonalnym sufiksem tekstu w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="08c61-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="08c61-107">W przypadku używania pakietów, z drugiej strony, można określić dokładny numer wersji lub zakres akceptowalnych wersji.</span><span class="sxs-lookup"><span data-stu-id="08c61-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="08c61-108">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="08c61-108">In this topic:</span></span>

- <span data-ttu-id="08c61-109">[Podstawy wersji](#version-basics) , w tym sufiksy wstępne.</span><span class="sxs-lookup"><span data-stu-id="08c61-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="08c61-110">Zakresy wersji</span><span class="sxs-lookup"><span data-stu-id="08c61-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="08c61-111">Znormalizowane numery wersji</span><span class="sxs-lookup"><span data-stu-id="08c61-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="08c61-112">Podstawy wersji</span><span class="sxs-lookup"><span data-stu-id="08c61-112">Version basics</span></span>

<span data-ttu-id="08c61-113">Określony numer wersji ma postać *główna. pomocnicza. poprawka [-sufiks]* , gdzie składniki mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="08c61-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="08c61-114">*Główna: istotne*zmiany</span><span class="sxs-lookup"><span data-stu-id="08c61-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="08c61-115">*Pomocniczy*: nowe funkcje, ale zgodność z poprzednimi wersjami</span><span class="sxs-lookup"><span data-stu-id="08c61-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="08c61-116">*Poprawka*: tylko poprawki zgodności z poprzednimi wersjami</span><span class="sxs-lookup"><span data-stu-id="08c61-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="08c61-117">*-Sufiks* (opcjonalnie): Łącznik, po którym następuje ciąg oznaczający wersję wstępną (zgodnie z [Konwencją o wersji semantyki lub SemVer 1,0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="08c61-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="08c61-118">**Pokazują**</span><span class="sxs-lookup"><span data-stu-id="08c61-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="08c61-119">nuget.org odrzuca przekazywanie pakietów, które nie mają dokładnego numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="08c61-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="08c61-120">Wersja musi być określona w `.nuspec` lub pliku projektu użytym do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="08c61-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="08c61-121">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="08c61-121">Pre-release versions</span></span>

<span data-ttu-id="08c61-122">Mówiąc technicznie, twórcy pakietów mogą używać dowolnego ciągu jako sufiksu do oznaczania wersji wstępnej, ponieważ NuGet traktuje wszystkie takie wersje jako wersji wstępnej i nie wykonuje żadnej innej interpretacji.</span><span class="sxs-lookup"><span data-stu-id="08c61-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="08c61-123">Oznacza to, że pakiet NuGet wyświetla pełny ciąg wersji w dowolnym interfejsie użytkownika, pozostawiając wszelką interpretację znaczenia sufiksu dla konsumenta.</span><span class="sxs-lookup"><span data-stu-id="08c61-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="08c61-124">Wspomniane w ten sposób deweloperzy pakietów zazwyczaj przestrzegają rozpoznawanych konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="08c61-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="08c61-125">`-alpha`: wydanie Alpha, zwykle używane do pracy w toku i eksperymentowania.</span><span class="sxs-lookup"><span data-stu-id="08c61-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="08c61-126">`-beta`: wydanie beta, zazwyczaj takie, które jest kompletne dla następnej planowanej wersji, ale mogą zawierać znane usterki.</span><span class="sxs-lookup"><span data-stu-id="08c61-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="08c61-127">`-rc`: Release Candidate, zazwyczaj wersja, która jest potencjalnie końcowa (stabilna), chyba że nastąpiły znaczne błędy.</span><span class="sxs-lookup"><span data-stu-id="08c61-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="08c61-128">Pakiet NuGet 4.3.0 + obsługuje [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), który obsługuje numery wersji wstępnej z notacją kropkową, tak jak w przypadku *1.0.1-Build. 23*.</span><span class="sxs-lookup"><span data-stu-id="08c61-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="08c61-129">Notacja kropki nie jest obsługiwana w wersjach NuGet przed 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="08c61-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="08c61-130">Możesz użyć formularza, takiego jak *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="08c61-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="08c61-131">Przy rozwiązywaniu odwołań do pakietów i wielu wersjach pakietów różni się tylko sufiksem, pakiet NuGet wybiera wersję bez sufiksu, a następnie stosuje pierwszeństwo w wersji wstępnej w odwrotnej kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="08c61-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="08c61-132">Na przykład następujące wersje zostałyby wybrane w dokładnie pokazanej kolejności:</span><span class="sxs-lookup"><span data-stu-id="08c61-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="08c61-133">2\.0.0 wersji semantycznej</span><span class="sxs-lookup"><span data-stu-id="08c61-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="08c61-134">Dzięki narzędziom NuGet 4.3.0 + i Visual Studio 2017 w wersji 15.3 + pakiet NuGet obsługuje [semantykę wersji 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="08c61-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="08c61-135">Niektóre semantyka SemVer v 2.0.0 nie są obsługiwane przez starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="08c61-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="08c61-136">Pakiet NuGet traktuje wersję pakietu jako SemVer v 2.0.0, jeśli jedno z następujących instrukcji jest prawdziwe:</span><span class="sxs-lookup"><span data-stu-id="08c61-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="08c61-137">Etykieta wersji wstępnej jest oddzielona kropką, na przykład *1.0.0-alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="08c61-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="08c61-138">Wersja zawiera metadane kompilacji, na przykład *1.0.0 + githash*</span><span class="sxs-lookup"><span data-stu-id="08c61-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="08c61-139">W przypadku nuget.org pakiet jest zdefiniowany jako pakiet SemVer v 2.0.0, jeśli jest spełniony jeden z następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="08c61-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="08c61-140">Własna wersja pakietu to SemVer v 2.0.0 zgodna, ale nie SemVer v 1.0.0 zgodna, zgodnie z definicją powyżej.</span><span class="sxs-lookup"><span data-stu-id="08c61-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="08c61-141">Dowolna z zakresów wersji zależności pakietu ma wersję minimalną lub maksymalną, która jest zgodna z SemVer v 2.0.0, ale nie SemVer v 1.0.0 zgodna z definicją powyżej; na przykład *[1.0.0-alpha. 1,)* .</span><span class="sxs-lookup"><span data-stu-id="08c61-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="08c61-142">W przypadku przekazania pakietu SemVer v 2.0.0 do nuget.org pakiet jest niewidoczny dla starszych klientów i dostępny tylko dla następujących klientów NuGet:</span><span class="sxs-lookup"><span data-stu-id="08c61-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="08c61-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="08c61-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="08c61-144">Visual Studio 2017 w wersji 15.3 +</span><span class="sxs-lookup"><span data-stu-id="08c61-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="08c61-145">Visual Studio 2015 z pakietem [NuGet VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="08c61-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="08c61-146">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="08c61-146">dotnet</span></span>
  - <span data-ttu-id="08c61-147">dotnetcore. exe (zestaw SDK 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="08c61-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="08c61-148">Klienci innych firm:</span><span class="sxs-lookup"><span data-stu-id="08c61-148">Third-party clients:</span></span>

- <span data-ttu-id="08c61-149">JetBrains</span><span class="sxs-lookup"><span data-stu-id="08c61-149">JetBrains Rider</span></span>
- <span data-ttu-id="08c61-150">Paket w wersji 5.0 +</span><span class="sxs-lookup"><span data-stu-id="08c61-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="08c61-151">Zakresy wersji</span><span class="sxs-lookup"><span data-stu-id="08c61-151">Version ranges</span></span>

<span data-ttu-id="08c61-152">W przypadku odwoływania się do zależności pakietów NuGet obsługuje używanie notacji interwału do określania zakresów wersji, podsumowywane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="08c61-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="08c61-153">Służąc</span><span class="sxs-lookup"><span data-stu-id="08c61-153">Notation</span></span> | <span data-ttu-id="08c61-154">Zastosowana reguła</span><span class="sxs-lookup"><span data-stu-id="08c61-154">Applied rule</span></span> | <span data-ttu-id="08c61-155">Opis</span><span class="sxs-lookup"><span data-stu-id="08c61-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="08c61-156">1.0</span><span class="sxs-lookup"><span data-stu-id="08c61-156">1.0</span></span> | <span data-ttu-id="08c61-157">x ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="08c61-157">x ≥ 1.0</span></span> | <span data-ttu-id="08c61-158">Minimalna wersja, włącznie</span><span class="sxs-lookup"><span data-stu-id="08c61-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="08c61-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="08c61-159">(1.0,)</span></span> | <span data-ttu-id="08c61-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="08c61-160">x > 1.0</span></span> | <span data-ttu-id="08c61-161">Wersja minimalna, wyłączna</span><span class="sxs-lookup"><span data-stu-id="08c61-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="08c61-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="08c61-162">[1.0]</span></span> | <span data-ttu-id="08c61-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="08c61-163">x == 1.0</span></span> | <span data-ttu-id="08c61-164">Dopasowanie dokładnej wersji</span><span class="sxs-lookup"><span data-stu-id="08c61-164">Exact version match</span></span> |
| <span data-ttu-id="08c61-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="08c61-165">(,1.0]</span></span> | <span data-ttu-id="08c61-166">x ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="08c61-166">x ≤ 1.0</span></span> | <span data-ttu-id="08c61-167">Maksymalna wersja, włącznie</span><span class="sxs-lookup"><span data-stu-id="08c61-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="08c61-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="08c61-168">(,1.0)</span></span> | <span data-ttu-id="08c61-169">x < 1,0</span><span class="sxs-lookup"><span data-stu-id="08c61-169">x < 1.0</span></span> | <span data-ttu-id="08c61-170">Maksymalna wersja, wyłączna</span><span class="sxs-lookup"><span data-stu-id="08c61-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="08c61-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="08c61-171">[1.0,2.0]</span></span> | <span data-ttu-id="08c61-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="08c61-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="08c61-173">Dokładny zakres, włącznie</span><span class="sxs-lookup"><span data-stu-id="08c61-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="08c61-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="08c61-174">(1.0,2.0)</span></span> | <span data-ttu-id="08c61-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="08c61-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="08c61-176">Dokładny zakres, wyłączny</span><span class="sxs-lookup"><span data-stu-id="08c61-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="08c61-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="08c61-177">[1.0,2.0)</span></span> | <span data-ttu-id="08c61-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="08c61-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="08c61-179">Mieszana wartość minimalna i wyłączna wersja Maksymalna</span><span class="sxs-lookup"><span data-stu-id="08c61-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="08c61-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="08c61-180">(1.0)</span></span>    | <span data-ttu-id="08c61-181">nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="08c61-181">invalid</span></span> | <span data-ttu-id="08c61-182">nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="08c61-182">invalid</span></span> |

<span data-ttu-id="08c61-183">W przypadku korzystania z formatu PackageReference, pakiet NuGet obsługuje także użycie notacji zmiennoprzecinkowej, \*, w przypadku elementów głównych, pomocniczych, poprawek i prefiksu w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="08c61-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="08c61-184">Wersje zmiennoprzecinkowe nie są obsługiwane w formacie `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="08c61-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="08c61-185">Zakresy wersji w programie PackageReference obejmują wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="08c61-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="08c61-186">Zgodnie z projektem wersje zmiennoprzecinkowe nie rozwiązują wersji wstępnych, chyba że zostały uwzględnione w.</span><span class="sxs-lookup"><span data-stu-id="08c61-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="08c61-187">Aby uzyskać stan żądania powiązanej funkcji, zobacz [problem 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="08c61-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="08c61-188">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08c61-188">Examples</span></span>

<span data-ttu-id="08c61-189">Należy zawsze określać wersję lub zakres wersji dla zależności pakietów w plikach projektu, `packages.config` plikach i plikach `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="08c61-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="08c61-190">Bez wersji lub zakresu wersji, program NuGet 2.8. x i wcześniejsza wersja wybiera najnowszą dostępną wersję pakietu podczas rozpoznawania zależności, natomiast w przypadku programu NuGet 3. x lub nowszego jest wybierana najniższa wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="08c61-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="08c61-191">Określenie wersji lub zakresu wersji pozwala uniknąć tej niepewności.</span><span class="sxs-lookup"><span data-stu-id="08c61-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="08c61-192">Odwołania w plikach projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="08c61-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="08c61-193">**Odwołania w `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="08c61-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="08c61-194">W `packages.config`każda zależność jest wyświetlana z dokładnym atrybutem `version` używanym podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="08c61-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="08c61-195">Atrybut `allowedVersions` jest używany tylko podczas operacji aktualizacji, aby ograniczyć wersje, do których pakiet może zostać zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="08c61-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="08c61-196">**Odwołania w plikach `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="08c61-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="08c61-197">Atrybut `version` w elemencie `<dependency>` opisuje wersje zakresu, które są akceptowalne dla zależności.</span><span class="sxs-lookup"><span data-stu-id="08c61-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="08c61-198">Znormalizowane numery wersji</span><span class="sxs-lookup"><span data-stu-id="08c61-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="08c61-199">Jest to istotna zmiana dotycząca programu NuGet 3,4 i nowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="08c61-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="08c61-200">Podczas uzyskiwania pakietów z repozytorium podczas operacji instalacji, ponownego instalowania lub przywracania program NuGet 3.4 + traktuje numery wersji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="08c61-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="08c61-201">Zera wiodące są usuwane z numerów wersji:</span><span class="sxs-lookup"><span data-stu-id="08c61-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="08c61-202">Zero w czwartej części numeru wersji zostanie pominięte</span><span class="sxs-lookup"><span data-stu-id="08c61-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- <span data-ttu-id="08c61-203">Metadane kompilacji SemVer 2.0.0 są usuwane</span><span class="sxs-lookup"><span data-stu-id="08c61-203">SemVer 2.0.0 build metadata is removed</span></span>

        1.0.7+r3456 is treated as 1.0.7

<span data-ttu-id="08c61-204">operacje `pack` i `restore` normalizuje wersje, jeśli jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="08c61-204">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="08c61-205">W przypadku pakietów, które zostały już skompilowane, normalizacja nie ma wpływu na numery wersji w samych pakietach; ma wpływ tylko na to, jak program NuGet dopasowuje wersje podczas rozpoznawania zależności.</span><span class="sxs-lookup"><span data-stu-id="08c61-205">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="08c61-206">Jednak repozytoria pakietów NuGet musi traktować te wartości w taki sam sposób jak NuGet, aby zapobiec duplikowaniu wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="08c61-206">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="08c61-207">W ten sposób repozytorium zawierające wersję *1,0* pakietu nie powinno również hostować wersji *1.0.0* jako oddzielnego i innego pakietu.</span><span class="sxs-lookup"><span data-stu-id="08c61-207">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
