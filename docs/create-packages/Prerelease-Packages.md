---
title: Wersje wstępne w pakietach NuGet
description: Wskazówki dotyczące tworzenia pakiety w wersji wstępnej
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: d6925df63daf3096455a8205d6aeb07b4475f715
ms.sourcegitcommit: 5c5f0f0e1f79098e27d9566dd98371f6ee16f8b5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645636"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="f96e8-103">Tworzenie pakietów w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="f96e8-103">Building pre-release packages</span></span>

<span data-ttu-id="f96e8-104">Zawsze, gdy zwolnieniu zaktualizowany pakiet za pomocą nowego numeru wersji NuGet uzna, że jeden jako "najnowsza stabilna wersja" jak pokazano na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f96e8-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Najnowsza stabilna wersja przedstawiający interfejs użytkownika Menedżera pakietów](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="f96e8-106">Stabilnej wersji jest taki, który jest uznawany za niezawodny, ma być używany w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f96e8-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="f96e8-107">Najnowsza stabilna wersja jest również zainstalowanej aktualizacji pakietu lub podczas przywracania pakietów (podlegających ograniczeniom opisanym w [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="f96e8-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="f96e8-108">Do obsługi cyklu życia wersji oprogramowania, NuGet w wersji 1.6 i nowszych umożliwia dystrybucja pakiety w wersji wstępnej, numer wersji uwzględniającym sufiks wersji semantycznej takich jak `-alpha`, `-beta`, lub `-rc`.</span><span class="sxs-lookup"><span data-stu-id="f96e8-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="f96e8-109">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="f96e8-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="f96e8-110">Należy określić taki wersji na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="f96e8-110">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="f96e8-111">`.nuspec` Plik: zawierać sufiks wersji semantycznej `version` elementu:</span><span class="sxs-lookup"><span data-stu-id="f96e8-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="f96e8-112">Zestawu atrybutów: podczas tworzenia pakietu z projektu programu Visual Studio (`.csproj` lub `.vbproj`), użyj `AssemblyInformationalVersionAttribute` do określenia wersji:</span><span class="sxs-lookup"><span data-stu-id="f96e8-112">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="f96e8-113">NuGet przejmuje tę wartość, a nie określona w `AssemblyVersion` atrybut, który nie obsługuje wersji semantycznej.</span><span class="sxs-lookup"><span data-stu-id="f96e8-113">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="f96e8-114">Gdy wszystko będzie gotowe do wydania stabilną wersję, po prostu usuń sufiks, a pakiet mają pierwszeństwo przed wszystkie wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="f96e8-114">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="f96e8-115">Znajduje się w artykule [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="f96e8-115">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="f96e8-116">Instalowanie i aktualizowanie pakietów w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="f96e8-116">Installing and updating pre-release packages</span></span>

<span data-ttu-id="f96e8-117">Domyślnie podczas pracy z pakietami NuGet obejmuje wersje wstępne, ale można zmienić to zachowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f96e8-117">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="f96e8-118">**Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: W **Zarządzaj pakietami NuGet** interfejsu użytkownika, sprawdź **Uwzględnij wersję wstępną** pola:</span><span class="sxs-lookup"><span data-stu-id="f96e8-118">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Wstępna pola wyboru Dołącz w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="f96e8-120">Ustawienie lub usunięcie zaznaczenia tego pola spowoduje odświeżenie interfejs użytkownika Menedżera pakietów i listę dostępnych wersji, które można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="f96e8-120">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="f96e8-121">**Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznik z `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, i `Update-Package` poleceń.</span><span class="sxs-lookup"><span data-stu-id="f96e8-121">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="f96e8-122">Zapoznaj się [dokumentacja programu PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f96e8-122">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="f96e8-123">**Interfejs wiersza polecenia NuGet**: Użyj `-prerelease` przełącznik z `install`, `update`, `delete`, i `mirror` poleceń.</span><span class="sxs-lookup"><span data-stu-id="f96e8-123">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="f96e8-124">Zapoznaj się [dokumentacja interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="f96e8-124">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="f96e8-125">Przechowywanie wersji semantyczne</span><span class="sxs-lookup"><span data-stu-id="f96e8-125">Semantic versioning</span></span>

<span data-ttu-id="f96e8-126">[Konwencji Semantic Versioning lub SemVer](http://semver.org/spec/v1.0.0.html) w tym artykule opisano sposób wykorzystywania ciągi numerów wersji w celu przekazania ich znaczenie odpowiedni kod.</span><span class="sxs-lookup"><span data-stu-id="f96e8-126">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="f96e8-127">W niniejszej Konwencji, każda wersja ma trzy części `Major.Minor.Patch`, mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="f96e8-127">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="f96e8-128">`Major`: Zmiany powodujące niezgodność</span><span class="sxs-lookup"><span data-stu-id="f96e8-128">`Major`: Breaking changes</span></span>
- <span data-ttu-id="f96e8-129">`Minor`: Nowe funkcje, ale wstecznie zgodne</span><span class="sxs-lookup"><span data-stu-id="f96e8-129">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="f96e8-130">`Patch`: Wstecznie zgodny poprawek błędów oprogramowania tylko</span><span class="sxs-lookup"><span data-stu-id="f96e8-130">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="f96e8-131">Wersje wstępne następnie są wskazywane przez dołączenie łącznika i ciąg po numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="f96e8-131">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="f96e8-132">Technicznie rzecz biorąc, można użyć *wszelkie* ciągu po NuGet i łącznika, będą traktować pakietu jako wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="f96e8-132">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="f96e8-133">NuGet następnie wyświetla pełny numer wersji w interfejsie użytkownika dotyczy pozostawienie w konsumentach napisanych interpretacji znaczenie dla siebie.</span><span class="sxs-lookup"><span data-stu-id="f96e8-133">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="f96e8-134">Pamiętając o tym, zazwyczaj dobrze jest postępuj zgodnie z rozpoznanym konwencji nazewnictwa, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="f96e8-134">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="f96e8-135">`-alpha`: Wersja alfa, zwykle używane do pracy w toku i eksperymentowanie</span><span class="sxs-lookup"><span data-stu-id="f96e8-135">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="f96e8-136">`-beta`: Wydania beta, zazwyczaj taki, który jest funkcja ukończone przez następne zaplanowane wersji, ale może zawierać znanych błędów.</span><span class="sxs-lookup"><span data-stu-id="f96e8-136">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="f96e8-137">`-rc`: W wersji Release candidate, zwykle wydania jest potencjalnie ostateczne (stable), chyba że wyłaniać znaczące błędy.</span><span class="sxs-lookup"><span data-stu-id="f96e8-137">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="f96e8-138">Obsługuje NuGet 4.3.0+ [v2.0.0 Semantic Versioning](http://semver.org/spec/v2.0.0.html), który obsługuje numerów wersji wstępnej przy użyciu notacji z kropką, podobnie jak w `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="f96e8-138">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="f96e8-139">Kropkowego jest nieobsługiwane w przypadku wersje NuGet wcześniejsze niż 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="f96e8-139">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="f96e8-140">We wcześniejszych wersjach programu NuGet, można użyć formularza, takich jak `1.0.1-build23` , ale zawsze uznano wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="f96e8-140">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="f96e8-141">Niezależnie od sufiksów, jednak należy użyć, NuGet da im pierwszeństwo w odwrotnej kolejności alfabetycznej:</span><span class="sxs-lookup"><span data-stu-id="f96e8-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="f96e8-142">Jak widać, wersji bez dowolny sufiks ma zawsze pierwszeństwo wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="f96e8-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="f96e8-143">Należy zauważyć, jeśli używasz sufiksy wartości liczbowych przy użyciu tagów wersji wstępnej, które mogą używać jednocyfrowy liczb (lub więcej), użyj zer wiodących beta01 i beta05 aby upewnić się, że są poprawne sortowanie podczas uzyskać większej liczby.</span><span class="sxs-lookup"><span data-stu-id="f96e8-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
