---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakietów w wersji wstępnej
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 5dda56ccd4c959bcbcbd12b7a4771ddff1fe7530
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623009"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="70270-103">Tworzenie pakietów w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="70270-103">Building pre-release packages</span></span>

<span data-ttu-id="70270-104">Za każdym razem, gdy zostanie wydane zaktualizowanego pakietu przy użyciu nowego numeru wersji, program NuGet uważa, że jest on wyświetlany jako "Najnowsza stabilna wersja", na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="70270-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interfejs użytkownika Menedżera pakietów przedstawiający najnowszą stabilną wersję](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="70270-106">Stabilna wersja jest uważana za wystarczającą do użycia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="70270-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="70270-107">Najnowsza stabilna wersja jest również taka, która zostanie zainstalowana jako aktualizacja pakietu lub podczas przywracania pakietu (z uwzględnieniem ograniczeń opisanych w temacie [ponowne instalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="70270-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="70270-108">Aby można było obsługiwać cykl wydawania oprogramowania, program NuGet 1,6 i nowsze umożliwiają dystrybucję pakietów w wersji wstępnej, gdzie numer wersji zawiera sufiks wersji semantycznej, taki jak `-alpha` , `-beta` lub `-rc` .</span><span class="sxs-lookup"><span data-stu-id="70270-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="70270-109">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji pakietu](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="70270-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="70270-110">Możesz określić takie wersje przy użyciu jednego z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="70270-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="70270-111">\*\*Jeśli używany [`PackageReference`](../consume-packages/package-references-in-project-files.md) jest projekt \*\*: Dołącz sufiks wersji semantycznej do `.csproj` elementu pliku [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) :</span><span class="sxs-lookup"><span data-stu-id="70270-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="70270-112">**Jeśli projekt zawiera [`packages.config`](../reference/packages-config.md) plik**: Dołącz sufiks wersji semantycznej do [`.nuspec`](../reference/nuspec.md) [`version`](../reference/nuspec.md#version) elementu pliku:</span><span class="sxs-lookup"><span data-stu-id="70270-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="70270-113">Gdy wszystko będzie gotowe do zwolnienia stabilnej wersji, wystarczy usunąć sufiks, a pakiet ma pierwszeństwo przed wszystkimi wersjami wstępnymi.</span><span class="sxs-lookup"><span data-stu-id="70270-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="70270-114">Ponownie zapoznaj się z artykułem [wersja pakietu](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="70270-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="70270-115">Instalowanie i aktualizowanie pakietów wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="70270-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="70270-116">Domyślnie NuGet nie uwzględnia wersji wstępnych podczas pracy z pakietami, ale można zmienić to zachowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="70270-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="70270-117">**Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: w interfejsie użytkownika **Zarządzanie pakietami NuGet** zaznacz pole **Uwzględnij wersję wstępną** :</span><span class="sxs-lookup"><span data-stu-id="70270-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Pole wyboru Uwzględnij wersję wstępną w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="70270-119">Ustawienie lub wyczyszczenie tego pola spowoduje odświeżenie interfejsu użytkownika Menedżera pakietów oraz listę dostępnych wersji, które można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="70270-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="70270-120">**Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznika z `Find-Package` poleceniami,,, `Get-Package` `Install-Package` `Sync-Package` i `Update-Package` .</span><span class="sxs-lookup"><span data-stu-id="70270-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="70270-121">Zapoznaj się z dokumentacją [programu PowerShell](../reference/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="70270-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="70270-122">**Interfejs wiersza polecenia NuGet**: Użyj `-prerelease` przełącznika z `install` `update` `delete` poleceniami,, i `mirror` .</span><span class="sxs-lookup"><span data-stu-id="70270-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="70270-123">Zapoznaj się z dokumentacją [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="70270-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="70270-124">Semantyczna obsługa wersji</span><span class="sxs-lookup"><span data-stu-id="70270-124">Semantic versioning</span></span>

<span data-ttu-id="70270-125">W przypadku [semantyki wersji lub Konwencji SemVer](https://semver.org/spec/v1.0.0.html) opisano, jak używać ciągów w numerach wersji do przekazywania znaczenia kodu bazowego.</span><span class="sxs-lookup"><span data-stu-id="70270-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="70270-126">W tej Konwencji każda wersja ma trzy części, `Major.Minor.Patch` i ma następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="70270-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="70270-127">`Major`: Istotne zmiany</span><span class="sxs-lookup"><span data-stu-id="70270-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="70270-128">`Minor`: Nowe funkcje, ale zgodność z poprzednimi wersjami</span><span class="sxs-lookup"><span data-stu-id="70270-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="70270-129">`Patch`: Tylko poprawki zgodne z poprzednimi usterkami</span><span class="sxs-lookup"><span data-stu-id="70270-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="70270-130">Wersje wstępne są następnie oznaczane przez dołączenie łącznika i ciągu po numerze poprawki.</span><span class="sxs-lookup"><span data-stu-id="70270-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="70270-131">Mówiąc technicznie, można użyć *dowolnego* ciągu po łączniku i NuGet będzie traktować pakiet jako wersję wstępną.</span><span class="sxs-lookup"><span data-stu-id="70270-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="70270-132">Następnie pakiet NuGet wyświetla pełny numer wersji w odpowiednim interfejsie użytkownika, pozostawiając konsumentom interpretację znaczenia dla siebie.</span><span class="sxs-lookup"><span data-stu-id="70270-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="70270-133">Z tego względu zazwyczaj warto przestrzegać rozpoznanych konwencji nazewnictwa, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="70270-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="70270-134">`-alpha`: Wydanie alfa, zwykle używane do pracy w toku i eksperymentowanie</span><span class="sxs-lookup"><span data-stu-id="70270-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="70270-135">`-beta`: Wydanie beta, zazwyczaj takie, które jest kompletne dla następnej planowanej wersji, ale może zawierać znane usterki.</span><span class="sxs-lookup"><span data-stu-id="70270-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="70270-136">`-rc`: Release Candidate, zwykle wydanie, które jest potencjalnie ostateczne (stabilne), chyba że nastąpiły znaczne błędy.</span><span class="sxs-lookup"><span data-stu-id="70270-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="70270-137">Pakiet NuGet 4.3.0 + obsługuje [semantykę wersji v 2.0.0](https://semver.org/spec/v2.0.0.html), która obsługuje numery wersji wstępnej z notacją kropkową, jak w `1.0.1-build.23` .</span><span class="sxs-lookup"><span data-stu-id="70270-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="70270-138">Notacja kropki nie jest obsługiwana w wersjach NuGet przed 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="70270-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="70270-139">We wcześniejszych wersjach programu NuGet możesz użyć takiego formularza, `1.0.1-build23` ale jest on zawsze traktowany jako wersja wstępna.</span><span class="sxs-lookup"><span data-stu-id="70270-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="70270-140">Jednak wszelkie używane sufiksy NuGet będą mieć pierwszeństwo w odwrotnej kolejności alfabetycznej:</span><span class="sxs-lookup"><span data-stu-id="70270-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="70270-141">Jak pokazano, wersja bez żadnego sufiksu zawsze będzie mieć pierwszeństwo przed wersjami wstępnymi.</span><span class="sxs-lookup"><span data-stu-id="70270-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="70270-142">Wiodące 0s nie są potrzebne w przypadku semver2, ale są z starym schematem wersji.</span><span class="sxs-lookup"><span data-stu-id="70270-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="70270-143">Jeśli używasz sufiksów liczbowych ze znacznikami wersji wstępnej, które mogą używać cyfr dwucyfrowych (lub więcej), użyj wiodących zer jako wersji beta. 01 i beta. 05, aby upewnić się, że są one sortowane prawidłowo, gdy liczby są większe.</span><span class="sxs-lookup"><span data-stu-id="70270-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="70270-144">To zalecenie dotyczy tylko starszego schematu wersji.</span><span class="sxs-lookup"><span data-stu-id="70270-144">This recommendation only applies to the old version schema.</span></span>
