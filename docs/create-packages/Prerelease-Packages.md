---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakiety w wersji wstępnej
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 845f0ea84bcb92fedf9e5f4fb2b1deee1462a004
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610500"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="5f958-103">Tworzenie pakietów w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="5f958-103">Building pre-release packages</span></span>

<span data-ttu-id="5f958-104">Zawsze, gdy zwolnieniu zaktualizowany pakiet za pomocą nowego numeru wersji NuGet uzna, że jeden jako "najnowsza stabilna wersja" jak pokazano na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5f958-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Najnowsza stabilna wersja przedstawiający interfejs użytkownika Menedżera pakietów](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="5f958-106">Stabilnej wersji jest taki, który jest uznawany za niezawodny, ma być używany w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="5f958-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="5f958-107">Najnowsza stabilna wersja jest również zainstalowanej aktualizacji pakietu lub podczas przywracania pakietów (podlegających ograniczeniom opisanym w [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="5f958-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="5f958-108">Do obsługi cyklu życia wersji oprogramowania, NuGet w wersji 1.6 i nowszych umożliwia dystrybucja pakiety w wersji wstępnej, numer wersji uwzględniającym sufiks wersji semantycznej takich jak `-alpha`, `-beta`, lub `-rc`.</span><span class="sxs-lookup"><span data-stu-id="5f958-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="5f958-109">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="5f958-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="5f958-110">Można określić takie wersji przy użyciu jednej z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="5f958-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="5f958-111">**Jeśli projekt używa [ `PackageReference` ](../consume-packages/package-references-in-project-files.md)** : zawierać sufiks wersji semantycznej `.csproj` pliku [ `PackageVersion` ](/dotnet/core/tools/csproj.md#packageversion) elementu:</span><span class="sxs-lookup"><span data-stu-id="5f958-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="5f958-112">**Jeżeli projekt zawiera [ `packages.config` ](../reference/packages-config.md) pliku**: zawierać sufiks wersji semantycznej [ `.nuspec` ](../reference/nuspec.md) pliku [ `version` ](../reference/nuspec.md#version) element:</span><span class="sxs-lookup"><span data-stu-id="5f958-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="5f958-113">Gdy wszystko będzie gotowe do wydania stabilną wersję, po prostu usuń sufiks, a pakiet mają pierwszeństwo przed wszystkie wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="5f958-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="5f958-114">Znajduje się w artykule [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="5f958-114">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="5f958-115">Instalowanie i aktualizowanie pakietów w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="5f958-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="5f958-116">Domyślnie podczas pracy z pakietami NuGet obejmuje wersje wstępne, ale można zmienić to zachowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5f958-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="5f958-117">**Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: W **Zarządzaj pakietami NuGet** interfejsu użytkownika, sprawdź **Uwzględnij wersję wstępną** pola:</span><span class="sxs-lookup"><span data-stu-id="5f958-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Wstępna pola wyboru Dołącz w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="5f958-119">Ustawienie lub usunięcie zaznaczenia tego pola spowoduje odświeżenie interfejs użytkownika Menedżera pakietów i listę dostępnych wersji, które można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="5f958-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="5f958-120">**Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznik z `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, i `Update-Package` poleceń.</span><span class="sxs-lookup"><span data-stu-id="5f958-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="5f958-121">Zapoznaj się [dokumentacja programu PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5f958-121">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="5f958-122">**Interfejs wiersza polecenia NuGet**: Użyj `-prerelease` przełącznik z `install`, `update`, `delete`, i `mirror` poleceń.</span><span class="sxs-lookup"><span data-stu-id="5f958-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="5f958-123">Zapoznaj się [dokumentacja interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="5f958-123">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="5f958-124">Przechowywanie wersji semantyczne</span><span class="sxs-lookup"><span data-stu-id="5f958-124">Semantic versioning</span></span>

<span data-ttu-id="5f958-125">[Konwencji Semantic Versioning lub SemVer](http://semver.org/spec/v1.0.0.html) w tym artykule opisano sposób wykorzystywania ciągi numerów wersji, aby przekazywać znaczenie odpowiedni kod.</span><span class="sxs-lookup"><span data-stu-id="5f958-125">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="5f958-126">W niniejszej Konwencji, każda wersja ma trzy części `Major.Minor.Patch`, mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="5f958-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="5f958-127">`Major`: Fundamentalne zmiany</span><span class="sxs-lookup"><span data-stu-id="5f958-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="5f958-128">`Minor`: Nowe funkcje, ale wstecznie zgodne</span><span class="sxs-lookup"><span data-stu-id="5f958-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="5f958-129">`Patch`: Wstecznie zgodny poprawek błędów oprogramowania tylko</span><span class="sxs-lookup"><span data-stu-id="5f958-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="5f958-130">Wersje wstępne następnie są wskazywane przez dołączenie łącznika i ciąg po numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="5f958-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="5f958-131">Technicznie rzecz biorąc, można użyć *wszelkie* ciągu po NuGet i łącznika, będą traktować pakietu jako wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="5f958-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="5f958-132">NuGet następnie wyświetla pełny numer wersji w interfejsie użytkownika dotyczy pozostawienie w konsumentach napisanych interpretacji znaczenie dla siebie.</span><span class="sxs-lookup"><span data-stu-id="5f958-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="5f958-133">Pamiętając o tym, zazwyczaj dobrze jest postępuj zgodnie z rozpoznanym konwencji nazewnictwa, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="5f958-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="5f958-134">`-alpha`: Wersja alfa, zwykle używane do pracy w toku i eksperymentowanie</span><span class="sxs-lookup"><span data-stu-id="5f958-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="5f958-135">`-beta`: Wydania beta, zazwyczaj taki, który jest funkcja ukończone przez następne zaplanowane wersji, ale może zawierać znanych błędów.</span><span class="sxs-lookup"><span data-stu-id="5f958-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="5f958-136">`-rc`: W wersji Release candidate, zwykle wydania jest potencjalnie ostateczne (stable), chyba że wyłaniać znaczące błędy.</span><span class="sxs-lookup"><span data-stu-id="5f958-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="5f958-137">Obsługuje NuGet 4.3.0+ [v2.0.0 Semantic Versioning](http://semver.org/spec/v2.0.0.html), który obsługuje numerów wersji wstępnej przy użyciu notacji z kropką, podobnie jak w `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="5f958-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="5f958-138">Kropkowego jest nieobsługiwane w przypadku wersje NuGet wcześniejsze niż 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="5f958-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="5f958-139">We wcześniejszych wersjach programu NuGet, można użyć formularza, takich jak `1.0.1-build23` , ale zawsze uznano wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="5f958-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="5f958-140">Niezależnie od sufiksów, jednak należy użyć, NuGet da im pierwszeństwo w odwrotnej kolejności alfabetycznej:</span><span class="sxs-lookup"><span data-stu-id="5f958-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="5f958-141">Jak widać, wersji bez dowolny sufiks ma zawsze pierwszeństwo wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="5f958-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="5f958-142">Należy zauważyć, jeśli używasz sufiksy wartości liczbowych przy użyciu tagów wersji wstępnej, które mogą używać jednocyfrowy liczb (lub więcej), użyj zer wiodących beta01 i beta05 aby upewnić się, że są poprawne sortowanie podczas uzyskać większej liczby.</span><span class="sxs-lookup"><span data-stu-id="5f958-142">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
