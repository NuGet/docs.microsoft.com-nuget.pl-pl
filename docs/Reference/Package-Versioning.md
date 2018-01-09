---
title: "Odwołanie do pakietu NuGet w wersji | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "Dokładne szczegóły dotyczące określania numery wersji i zakresy dla innych pakietów, od którego zależy od pakietu NuGet i jak zależności są zainstalowane."
keywords: "przechowywanie wersji, zależności pakietów NuGet, wersje zależności NuGet, numery wersji NuGet, wersja pakietu NuGet, zakresy wersji, specyfikacji wersji, numery wersji znormalizowane"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb5624a2fd99e8afd8a8226fd786343f485041c4
ms.sourcegitcommit: c27e565de485cbe836e6c2a66e44a50b35b487ff
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/09/2018
---
# <a name="package-versioning"></a><span data-ttu-id="eed25-104">Przechowywanie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="eed25-104">Package versioning</span></span>

<span data-ttu-id="eed25-105">Określony pakiet jest zawsze określone za pomocą jego identyfikatora pakietu i numer dokładnej wersji.</span><span class="sxs-lookup"><span data-stu-id="eed25-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="eed25-106">Na przykład [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org ma kilka dozen określonych pakietów dostępne począwszy od wersji *4.1.10311* do wersji *6.1.3* (najnowsze stały Zwolnij) i różne wersje wstępne, takich jak *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="eed25-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="eed25-107">Podczas tworzenia pakietu, należy przypisać numer określoną wersję z sufiksem opcjonalny tekst wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="eed25-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="eed25-108">Podczas używania pakietów, z drugiej strony, można określić liczby dokładnej wersji lub zakresu akceptowalnych wersji.</span><span class="sxs-lookup"><span data-stu-id="eed25-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="eed25-109">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="eed25-109">In this topic:</span></span>

- <span data-ttu-id="eed25-110">[Podstawowe informacje o wersji](#version-basics) tym sufiksy wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="eed25-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="eed25-111">Zakresy wersji i symboli wieloznacznych</span><span class="sxs-lookup"><span data-stu-id="eed25-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="eed25-112">Numery wersji znormalizowane</span><span class="sxs-lookup"><span data-stu-id="eed25-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="eed25-113">Podstawowe informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="eed25-113">Version basics</span></span>

<span data-ttu-id="eed25-114">Numer wersji ma postać *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]*, których składniki mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="eed25-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="eed25-115">*Główne*: fundamentalne zmiany</span><span class="sxs-lookup"><span data-stu-id="eed25-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="eed25-116">*Drobne*: nowe funkcje, ale wstecznie zgodne</span><span class="sxs-lookup"><span data-stu-id="eed25-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="eed25-117">*Poprawka*: wstecznie zgodna tylko poprawki.</span><span class="sxs-lookup"><span data-stu-id="eed25-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="eed25-118">*-Sufiks* (opcjonalnie): łącznika następuje ciąg oznaczający wersji wstępnej (następujące [Wersjonowania semantycznego lub 1.0 programu SemVer Konwencji](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="eed25-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="eed25-119">**Przykłady:**</span><span class="sxs-lookup"><span data-stu-id="eed25-119">**Examples:**</span></span>
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="eed25-120">nuget.org odrzuca wszystkie przekazywanie pakietu, który nie ma numer wersji dokładne.</span><span class="sxs-lookup"><span data-stu-id="eed25-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="eed25-121">Wersja musi być określony w `.nuspec` lub plik projektu używany do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="eed25-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="eed25-122">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="eed25-122">Pre-release versions</span></span>

<span data-ttu-id="eed25-123">Jak to działa, twórców pakietu można użyć jako sufiks dowolnego ciągu określający wersję wstępną NuGet traktuje takie wersji jako wstępną i sprawia, że nie inne interpretacji.</span><span class="sxs-lookup"><span data-stu-id="eed25-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="eed25-124">Oznacza to pełną wersję ciąg w dowolnie wybrany interfejs użytkownika wyświetla NuGet uczestniczy, pozostawiając żadnej interpretacji znaczenie sufiks konsumenta.</span><span class="sxs-lookup"><span data-stu-id="eed25-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="eed25-125">Inaczej mówiąc, deweloperzy pakietu należy wykonać rozpoznanym konwencji nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="eed25-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="eed25-126">`-alpha`: Wersja alfa zwykle używany w przypadku pracy w toku i eksperymenty.</span><span class="sxs-lookup"><span data-stu-id="eed25-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="eed25-127">`-beta`: Wydania beta, zazwyczaj jest pełną Następna funkcja planowane wersji, ale może zawierać znanych błędów.</span><span class="sxs-lookup"><span data-stu-id="eed25-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="eed25-128">`-rc`: Wersji release candidate, zwykle potencjalnie ostateczną zlecenia (stable), chyba że wyłonić znaczących usterki.</span><span class="sxs-lookup"><span data-stu-id="eed25-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="eed25-129">Obsługuje NuGet 4.3.0+ [programu SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), który obsługuje numerów wersji wstępnej mają kropkowego, podobnie jak w *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="eed25-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="eed25-130">Kropkowego nie jest obsługiwany w wersjach NuGet przed 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="eed25-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="eed25-131">Można użyć formularza, takich jak *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="eed25-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="eed25-132">Podczas rozpoznawania odwołania do pakietu i wiele wersji pakietu różnią się jedynie sufiks, NuGet wybierze wersji bez sufiksu najpierw, a następnie stosuje pierwszeństwo wersji wstępnych w odwrotnej kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="eed25-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="eed25-133">Na przykład w pokazanej kolejności dokładne zostałaby wybrana następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="eed25-133">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="eed25-134">Wersjonowania semantycznego 2.0.0</span><span class="sxs-lookup"><span data-stu-id="eed25-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="eed25-135">NuGet 4.3.0+ i Visual Studio 2017 wersji 15 ustęp 3 + obsługuje NuGet [Wersjonowania semantycznego 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="eed25-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="eed25-136">Niektóre semantyki v2.0.0 programu SemVer nie są obsługiwane w starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="eed25-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="eed25-137">NuGet uwzględnia wersja pakietu za v2.0.0 programu SemVer określone, jeśli jest spełniony jeden z następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="eed25-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="eed25-138">Etykieta wersji wstępnej jest oddzielona kropkami, na przykład *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="eed25-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="eed25-139">Wersja ma metadane kompilacji, na przykład *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="eed25-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="eed25-140">Dla nuget.org pakiet jest zdefiniowany jako pakiet v2.0.0 programu SemVer, jeśli spełniony jest jeden z następujących instrukcji:</span><span class="sxs-lookup"><span data-stu-id="eed25-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="eed25-141">Wersja tego pakietu jest v2.0.0 programu SemVer zgodne, ale nie programu SemVer v1.0.0 zgodne, zgodnie z definicją powyżej.</span><span class="sxs-lookup"><span data-stu-id="eed25-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="eed25-142">Wszelkie zakresy wersji zależności pakietu ma minimalną lub maksymalną wersję, która jest v2.0.0 programu SemVer zgodne, ale nie programu SemVer v1.0.0 zgodne, zdefiniowanych powyżej; na przykład *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="eed25-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="eed25-143">Po wysłaniu pakietu v2.0.0 specyficzne dla programu SemVer do nuget.org pakiet jest niewidoczna dla starszych klientów i jest dostępny tylko dla następujących klientów NuGet:</span><span class="sxs-lookup"><span data-stu-id="eed25-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="eed25-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="eed25-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="eed25-145">Visual Studio 2017 wersji 15 ustęp 3 +</span><span class="sxs-lookup"><span data-stu-id="eed25-145">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="eed25-146">Visual Studio 2015 z [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="eed25-146">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="eed25-147">DotNet.exe (2.0.0+ zestawu .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="eed25-147">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="eed25-148">Klienci innych firm:</span><span class="sxs-lookup"><span data-stu-id="eed25-148">Third-party clients:</span></span>

- <span data-ttu-id="eed25-149">Kierowcy JetBrains</span><span class="sxs-lookup"><span data-stu-id="eed25-149">JetBrains Rider</span></span>
- <span data-ttu-id="eed25-150">Paket w wersji 5.0 +</span><span class="sxs-lookup"><span data-stu-id="eed25-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="eed25-151">Zakresy wersji i symboli wieloznacznych</span><span class="sxs-lookup"><span data-stu-id="eed25-151">Version ranges and wildcards</span></span>

<span data-ttu-id="eed25-152">W odniesieniu do zależności pakietów NuGet obsługuje przy użyciu notacji interwał służący do określania zakresu, podsumować w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eed25-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="eed25-153">Notacja</span><span class="sxs-lookup"><span data-stu-id="eed25-153">Notation</span></span> | <span data-ttu-id="eed25-154">Reguła zastosowana</span><span class="sxs-lookup"><span data-stu-id="eed25-154">Applied rule</span></span> | <span data-ttu-id="eed25-155">Opis</span><span class="sxs-lookup"><span data-stu-id="eed25-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="eed25-156">1.0</span><span class="sxs-lookup"><span data-stu-id="eed25-156">1.0</span></span> | <span data-ttu-id="eed25-157">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="eed25-157">1.0 ≤ x</span></span> | <span data-ttu-id="eed25-158">Minimalna wersja włącznie</span><span class="sxs-lookup"><span data-stu-id="eed25-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="eed25-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="eed25-159">(1.0,)</span></span> | <span data-ttu-id="eed25-160">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="eed25-160">1.0 < x</span></span> | <span data-ttu-id="eed25-161">Minimalna wersja wyłączności</span><span class="sxs-lookup"><span data-stu-id="eed25-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="eed25-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="eed25-162">[1.0]</span></span> | <span data-ttu-id="eed25-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="eed25-163">x == 1.0</span></span> | <span data-ttu-id="eed25-164">Wersja dokładnego dopasowania</span><span class="sxs-lookup"><span data-stu-id="eed25-164">Exact version match</span></span> |
| <span data-ttu-id="eed25-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="eed25-165">(,1.0]</span></span> | <span data-ttu-id="eed25-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="eed25-166">x ≤ 1.0</span></span> | <span data-ttu-id="eed25-167">Maksymalna wersja włącznie</span><span class="sxs-lookup"><span data-stu-id="eed25-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="eed25-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="eed25-168">(,1.0)</span></span> | <span data-ttu-id="eed25-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="eed25-169">x < 1.0</span></span> | <span data-ttu-id="eed25-170">Maksymalna wersja wyłączności</span><span class="sxs-lookup"><span data-stu-id="eed25-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="eed25-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="eed25-171">[1.0,2.0]</span></span> | <span data-ttu-id="eed25-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="eed25-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="eed25-173">Dokładny zakres włącznie</span><span class="sxs-lookup"><span data-stu-id="eed25-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="eed25-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="eed25-174">(1.0,2.0)</span></span> | <span data-ttu-id="eed25-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="eed25-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="eed25-176">Dokładny zakres wyłączności</span><span class="sxs-lookup"><span data-stu-id="eed25-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="eed25-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="eed25-177">[1.0,2.0)</span></span> | <span data-ttu-id="eed25-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="eed25-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="eed25-179">Mieszane z wartościami granicznymi minimalna i wyłącznego maksymalna wersja</span><span class="sxs-lookup"><span data-stu-id="eed25-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="eed25-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="eed25-180">(1.0)</span></span>    | <span data-ttu-id="eed25-181">nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="eed25-181">invalid</span></span> | <span data-ttu-id="eed25-182">nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="eed25-182">invalid</span></span> |

<span data-ttu-id="eed25-183">Korzystając z PackageReference lub `project.json` pakietu NuGet odwołanie formatów również obsługuje za pomocą notacji symboli wieloznacznych, \*, główna, pomocnicze, poprawki i sufiks wersji wstępnej części numeru.</span><span class="sxs-lookup"><span data-stu-id="eed25-183">When using the PackageReference or `project.json` package reference formats, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="eed25-184">Symbole wieloznaczne nie są obsługiwane przez `packages.config` format.</span><span class="sxs-lookup"><span data-stu-id="eed25-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="eed25-185">Wersje wstępne nie są uwzględniane podczas rozpoznawania zakresu.</span><span class="sxs-lookup"><span data-stu-id="eed25-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="eed25-186">Wersji wstępnych *są* uwzględnione przy użyciu symbolu wieloznacznego (\*).</span><span class="sxs-lookup"><span data-stu-id="eed25-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="eed25-187">Zakres wersji *[1.0,2.0]*, na przykład nie zawiera wersji 2.0 beta, ale notacji symbolu wieloznacznego _2.0-*_ jest.</span><span class="sxs-lookup"><span data-stu-id="eed25-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-*_ does.</span></span> <span data-ttu-id="eed25-188">Zobacz [wystawiać 912](https://github.com/NuGet/Home/issues/912) dla dalszego omówione symboli wieloznacznych wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="eed25-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="eed25-189">Przykłady</span><span class="sxs-lookup"><span data-stu-id="eed25-189">Examples</span></span>

<span data-ttu-id="eed25-190">Zawsze podać wersja lub zakres wersji dla zależności pakietów w plikach projektu `packages.config` pliki, i `.nuspec` plików.</span><span class="sxs-lookup"><span data-stu-id="eed25-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="eed25-191">Bez wersja lub zakres wersji, NuGet 2.8.x i wcześniej wybiera opcję najnowszą wersję pakietu dostępne podczas rozpoznawania zależności, podczas gdy NuGet 3.x, a później zdecyduje Najniższa wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="eed25-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="eed25-192">Określanie wersji lub wersji tego niedokładność pozwala uniknąć zakresu.</span><span class="sxs-lookup"><span data-stu-id="eed25-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="eed25-193">Odwołania w plikach projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="eed25-193">References in project files (PackageReference)</span></span>

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="eed25-194">**Odwołania w `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="eed25-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="eed25-195">W `packages.config`, co zależności znajduje się dokładnie `version` atrybut, który jest używany podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="eed25-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="eed25-196">`allowedVersions` Atrybut jest używany tylko podczas operacji update Aby ograniczyć wersje, które mogły zostać zaktualizowane pakietu.</span><span class="sxs-lookup"><span data-stu-id="eed25-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="eed25-197">**Odwołania w `.nuspec` plików**</span><span class="sxs-lookup"><span data-stu-id="eed25-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="eed25-198">`version` Atrybutu w `<dependency>` element zawiera opis wersji zakresu, które są dozwolone dla zależności.</span><span class="sxs-lookup"><span data-stu-id="eed25-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="eed25-199">Numery wersji znormalizowane</span><span class="sxs-lookup"><span data-stu-id="eed25-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="eed25-200">Jest to istotne zmiany dla NuGet 3.4 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="eed25-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="eed25-201">Uzyskiwanie pakietów z repozytorium podczas instalacji, ponowne zainstalowanie lub operacji, przywracania NuGet 3.4 + traktuje numery wersji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eed25-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="eed25-202">Zera wiodące są usuwane z numerów wersji:</span><span class="sxs-lookup"><span data-stu-id="eed25-202">Leading zeroes are removed from version numbers:</span></span>

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- <span data-ttu-id="eed25-203">Zero w czwartym część numeru wersji zostaną pominięte.</span><span class="sxs-lookup"><span data-stu-id="eed25-203">A zero in the fourth part of the version number will be omitted</span></span>

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

<span data-ttu-id="eed25-204">Ta wartość nie wpływa na numery wersji pakietów. ma wpływ na sposób NuGet jest zgodny tylko wersje podczas rozpoznawania zależności.</span><span class="sxs-lookup"><span data-stu-id="eed25-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="eed25-205">Jednak repozytoriów pakietu NuGet należy traktować te wartości w taki sam sposób jak NuGet, aby uniknąć duplikowania wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="eed25-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="eed25-206">W związku z tym repozytorium, która zawiera wersję *1.0* pakietu nie powinny również hostować wersji *1.0.0* jako osobne i inny pakiet.</span><span class="sxs-lookup"><span data-stu-id="eed25-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
