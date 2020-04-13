---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakietów przedpremierowych
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610714"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="c7074-103">Tworzenie pakietów przedpremierowych</span><span class="sxs-lookup"><span data-stu-id="c7074-103">Building pre-release packages</span></span>

<span data-ttu-id="c7074-104">Za każdym razem, gdy zwalniasz zaktualizowany pakiet z nowym numerem wersji, NuGet uważa, że jeden jako "najnowsze stabilne wydanie", jak pokazano, na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c7074-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interfejs użytkownika Menedżera pakietów przedstawiający najnowszą stabilną wersję](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="c7074-106">Stabilne wydanie jest jednym, który jest uważany za wystarczająco wiarygodne, aby być używane w produkcji.</span><span class="sxs-lookup"><span data-stu-id="c7074-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="c7074-107">Najnowsza stabilna wersja jest również tą, która zostanie zainstalowana jako aktualizacja pakietu lub podczas przywracania pakietu (z zastrzeżeniem ograniczeń opisanych w [temacie Ponowna instalacja i aktualizacja pakietów).](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="c7074-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="c7074-108">Aby obsługiwać cykl życia wydania oprogramowania, NuGet 1.6 i nowsze umożliwia dystrybucję pakietów wersji wstępnej, gdzie `-alpha` `-beta`numer `-rc`wersji zawiera semantyczny sufiks przechowywania wersji, taki jak , lub .</span><span class="sxs-lookup"><span data-stu-id="c7074-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="c7074-109">Aby uzyskać więcej informacji, zobacz [Przechowywanie wersji pakietu](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="c7074-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="c7074-110">Takie wersje można określić za pomocą jednego z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="c7074-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="c7074-111">\*\*Jeśli projekt używa [`PackageReference`](../consume-packages/package-references-in-project-files.md) \*\*: dołącz sufiks wersji semantycznej [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) w elemencie `.csproj` pliku:</span><span class="sxs-lookup"><span data-stu-id="c7074-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="c7074-112">**Jeśli projekt ma [`packages.config`](../reference/packages-config.md) plik:** dołącz sufiks wersji semantycznej [`version`](../reference/nuspec.md#version) w elemencie [`.nuspec`](../reference/nuspec.md) pliku:</span><span class="sxs-lookup"><span data-stu-id="c7074-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="c7074-113">Gdy będziesz gotowy do wydania stabilnej wersji, po prostu usuń sufiks, a pakiet ma pierwszeństwo przed dowolnymi wersjami wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="c7074-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="c7074-114">Ponownie, zobacz [Przechowywanie wersji pakietu](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="c7074-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="c7074-115">Instalowanie i aktualizowanie pakietów wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="c7074-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="c7074-116">Domyślnie NuGet nie zawiera wersji wstępnych podczas pracy z pakietami, ale można zmienić to zachowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c7074-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="c7074-117">**Interfejs użytkownika Menedżera pakietów w programie Visual Studio:** W interfejsie użytkownika **zarządzania pakietami NuGet** zaznacz pole wyboru **Dołącz zawartość wstępną:**</span><span class="sxs-lookup"><span data-stu-id="c7074-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Pole wyboru Uwzględnij wydanie wstępne w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="c7074-119">Ustawienie lub wyczyszczenie tego pola spowoduje odświeżenie interfejsu użytkownika Menedżera pakietów i listy dostępnych wersji, które można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="c7074-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="c7074-120">**Konsola Menedżera pakietów:** Użyj przełącznika `-IncludePrerelease` z poleceniami `Find-Package`, `Get-Package` `Install-Package`, `Sync-Package`, i. `Update-Package`</span><span class="sxs-lookup"><span data-stu-id="c7074-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="c7074-121">Zapoznaj się z [odwołaniem programu PowerShell](../reference/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c7074-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="c7074-122">**NuGet CLI**: `-prerelease` Użyj `install`przełącznika `delete`z `mirror` , `update`, , i polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7074-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="c7074-123">Zapoznaj się z [odwołaniem nuget cli](../reference/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="c7074-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="c7074-124">Przechowywanie wersji semantycznych</span><span class="sxs-lookup"><span data-stu-id="c7074-124">Semantic versioning</span></span>

<span data-ttu-id="c7074-125">[Semantyczne przechowywanie wersji lub SemVer konwencji](https://semver.org/spec/v1.0.0.html) opisuje, jak korzystać z ciągów w numerach wersji do przekazywania znaczenia kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="c7074-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="c7074-126">W tej konwencji każda wersja `Major.Minor.Patch`ma trzy części, o następującym znaczeniu:</span><span class="sxs-lookup"><span data-stu-id="c7074-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="c7074-127">`Major`: Przełomowe zmiany</span><span class="sxs-lookup"><span data-stu-id="c7074-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="c7074-128">`Minor`: Nowe funkcje, ale wstecznie kompatybilne</span><span class="sxs-lookup"><span data-stu-id="c7074-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="c7074-129">`Patch`: Korekty błędów zgodne ze standardem wstecz</span><span class="sxs-lookup"><span data-stu-id="c7074-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="c7074-130">Wersje w wersji wstępnej są następnie oznaczane przez dołączenie łącznika i ciągu po numerze poprawki.</span><span class="sxs-lookup"><span data-stu-id="c7074-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="c7074-131">Technicznie rzecz biorąc, można użyć *dowolnego* ciągu po łącznika i NuGet będzie traktować pakiet jako wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="c7074-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="c7074-132">Następnie NuGet wyświetla pełny numer wersji w odpowiednim interfejsie użytkownika, pozostawiając konsumentów do interpretacji znaczenia dla siebie.</span><span class="sxs-lookup"><span data-stu-id="c7074-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="c7074-133">Mając to na uwadze, ogólnie dobrze jest przestrzegać uznanych konwencji nazewnictwa, takich jak:</span><span class="sxs-lookup"><span data-stu-id="c7074-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="c7074-134">`-alpha`: Alpha release, zwykle używany do pracy w toku i eksperymentowania</span><span class="sxs-lookup"><span data-stu-id="c7074-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="c7074-135">`-beta`: Wersja beta, zazwyczaj taka, która jest kompletna dla następnej planowanej wersji, ale może zawierać znane błędy.</span><span class="sxs-lookup"><span data-stu-id="c7074-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="c7074-136">`-rc`: Release candidate, zazwyczaj wydanie, które jest potencjalnie ostateczne (stabilne), chyba że pojawią się istotne błędy.</span><span class="sxs-lookup"><span data-stu-id="c7074-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="c7074-137">NuGet 4.3.0+ obsługuje [semantyczne przechowywanie wersji v2.0.0](https://semver.org/spec/v2.0.0.html), które obsługuje numery wersji `1.0.1-build.23`wstępnej z notacją kropkową, jak w .</span><span class="sxs-lookup"><span data-stu-id="c7074-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="c7074-138">Notacja kropki nie jest obsługiwana w wersjach NuGet przed wersją 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="c7074-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="c7074-139">We wcześniejszych wersjach NuGet można użyć `1.0.1-build23` formularza, jak ale to zawsze było uważane za wersję wstępną.</span><span class="sxs-lookup"><span data-stu-id="c7074-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="c7074-140">Niezależnie od używanych przyrostków, jednak NuGet da im pierwszeństwo w odwrotnej kolejności alfabetycznej:</span><span class="sxs-lookup"><span data-stu-id="c7074-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="c7074-141">Jak pokazano, wersja bez sufiksu zawsze będzie mieć pierwszeństwo przed wersjami wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="c7074-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="c7074-142">Wiodące 0s nie są potrzebne z semver2, ale są one ze starym schematem wersji.</span><span class="sxs-lookup"><span data-stu-id="c7074-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="c7074-143">Jeśli używasz sufiksów numerycznych z tagami wersji wstępnej, które mogą używać liczb dwucyfrowych (lub więcej), użyj zer wiodących, jak w wersjach beta.01 i beta.05, aby upewnić się, że są one sortowane poprawnie, gdy liczby stają się większe.</span><span class="sxs-lookup"><span data-stu-id="c7074-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="c7074-144">To zalecenie dotyczy tylko starego schematu wersji.</span><span class="sxs-lookup"><span data-stu-id="c7074-144">This recommendation only applies to the old version schema.</span></span>
