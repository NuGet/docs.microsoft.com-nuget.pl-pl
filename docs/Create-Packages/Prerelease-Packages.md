---
title: "Wersji wstępnej wersji w pakietach NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Wskazówki dotyczące tworzenia pakiety wersji wstępnej"
keywords: "przechowywanie wersji, przechowywanie wersji pakietu NuGet, wersje wstępne NuGet, wstępnej pakietów NuGet, wersje pakietu w wersji zapoznawczej, wersji RC pakietów, wersje pakietu w wersji Beta, wersjonowania semantycznego NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f07b4a0428685b036640a7153190fd8454885608
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="6ef5c-104">Tworzenie pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="6ef5c-104">Building pre-release packages</span></span>

<span data-ttu-id="6ef5c-105">Zawsze, gdy zwolnieniu zaktualizowany pakiet z nowym numerem wersji NuGet uzna, że jeden jako "najnowsza stabilna wersja" jak pokazano na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-105">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interfejs użytkownika Menedżera pakietów przedstawiający najnowsze stabilna wersja](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="6ef5c-107">Stabilna wersja to taki, który jest uznawany za niezawodny do użycia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-107">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="6ef5c-108">Najnowsze stabilna wersja jest również ten, który zostanie zainstalowany jako aktualizacja pakietu lub w czasie przywracania pakietu (pod warunkiem ograniczenia zgodnie z opisem w [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="6ef5c-108">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="6ef5c-109">Do obsługi cyklu życia wersji oprogramowania, NuGet w wersji 1.6 lub nowszym umożliwia dystrybucji pakiety wersji wstępnej, gdzie numer wersji obejmuje sufiks wersjonowania semantycznego takich jak `-alpha`, `-beta`, lub `-rc`.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-109">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="6ef5c-110">Aby uzyskać więcej informacji, zobacz [wersji pakietu](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="6ef5c-110">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="6ef5c-111">Można określić takie wersji na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-111">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="6ef5c-112">`.nuspec`Plik: zawiera sufiksu wersją semantyczną w `version` elementu:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-112">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="6ef5c-113">Zestawu atrybutów: podczas tworzenia pakietu z projektu programu Visual Studio (`.csproj` lub `.vbproj`), użyj `AssemblyInformationalVersionAttribute` do określania wersji:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-113">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="6ef5c-114">NuGet przejmuje zamiast określona w tym wartości `AssemblyVersion` atrybut, który nie obsługuje wersjonowania semantycznego.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="6ef5c-115">Gdy wszystko jest gotowe do wydania stabilną wersję, po prostu usuń sufiks i pakiet ma pierwszeństwo przed wszystkie wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="6ef5c-116">Ponownie, zobacz [wersji pakietu](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="6ef5c-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="6ef5c-117">Instalowanie i aktualizowanie pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="6ef5c-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="6ef5c-118">Domyślnie podczas pracy z pakietami NuGet nie zawiera wersji wstępnych, ale to zachowanie można zmienić w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="6ef5c-119">**Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: W **Zarządzaj pakietami NuGet** interfejsu użytkownika, sprawdź **Uwzględnij wersję wstępną** pola:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Dołącz wstępnej pole wyboru w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="6ef5c-121">Ustawienie lub usunięcie zaznaczenia tego pola, zostaną odświeżone interfejsu użytkownika Menedżera pakietów i listę dostępnych wersji, które można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="6ef5c-122">**Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznik z `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, i `Update-Package` poleceń.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="6ef5c-123">Zapoznaj się [w programie PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="6ef5c-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="6ef5c-124">**Interfejs wiersza polecenia NuGet**: Użyj `-prerelease` przełącznik z `install`, `update`, `delete`, i `mirror` poleceń.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="6ef5c-125">Zapoznaj się [odwołanie NuGet interfejsu wiersza polecenia](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="6ef5c-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="6ef5c-126">Wersjonowania semantycznego</span><span class="sxs-lookup"><span data-stu-id="6ef5c-126">Semantic versioning</span></span>

<span data-ttu-id="6ef5c-127">[Wersjonowania semantycznego lub programu SemVer Konwencji](http://semver.org/spec/v1.0.0.html) opisano, jak korzystać z ciągów numery wersji w celu przedstawienia ich znaczenie kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="6ef5c-128">W tym Konwencji każdej wersji ma trzy części `Major.Minor.Patch`, mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="6ef5c-129">`Major`: Zmiany krytyczne</span><span class="sxs-lookup"><span data-stu-id="6ef5c-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="6ef5c-130">`Minor`: Nowe funkcje, ale wstecznie zgodne</span><span class="sxs-lookup"><span data-stu-id="6ef5c-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="6ef5c-131">`Patch`: Wstecznie zgodne wprowadzono poprawki błędów tylko</span><span class="sxs-lookup"><span data-stu-id="6ef5c-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="6ef5c-132">Wersje wstępne następnie są wskazywane przez dodanie łącznika i ciąg po numer poprawki.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="6ef5c-133">Jak to działa, można użyć * żadnych * ciągu po łącznika i NuGet, będą traktować pakietu jako wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-133">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="6ef5c-134">Następnie NuGet Wyświetla numer wersji pełnej w odpowiednich interfejsu użytkownika, pozostawiając konsumentów interpretować znaczenie dla siebie.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="6ef5c-135">Pamiętając o tym warto zazwyczaj wykonaj rozpoznanym konwencji nazewnictwa, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="6ef5c-136">`-alpha`: Wersja alfa, zwykle używany w przypadku pracy w toku i eksperymenty</span><span class="sxs-lookup"><span data-stu-id="6ef5c-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="6ef5c-137">`-beta`: Wydania beta, zazwyczaj jest pełną Następna funkcja planowane wersji, ale może zawierać znanych błędów.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="6ef5c-138">`-rc`: Wersji release candidate, zwykle potencjalnie ostateczną zlecenia (stable), chyba że wyłonić znaczących usterki.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="6ef5c-139">NuGet nie obsługuje [zgodnego programu SemVer (v2.0.0)](http://semver.org/spec/v2.0.0.html) wersja wstępna liczby za pomocą kropkowego, podobnie jak w `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-139">NuGet does not support [SemVer-compatible (v2.0.0)](http://semver.org/spec/v2.0.0.html) prerelease numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="6ef5c-140">Można użyć formularza, takich jak `1.0.1-build23` , ale jest to zawsze uważane za wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-140">You can use a form like `1.0.1-build23` but this is always considered a pre-release version.</span></span>

<span data-ttu-id="6ef5c-141">Niezależnie od sufiksy, jednak należy użyć, NuGet zapewni ich pierwszeństwo w odwrotnej kolejności alfabetycznej:</span><span class="sxs-lookup"><span data-stu-id="6ef5c-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="6ef5c-142">Co zostało pokazane, wersji bez żadnego sufiksu będą zawsze miały pierwszeństwo przed wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="6ef5c-143">Należy pamiętać, że użycie numeryczny sufiksy z tagami wersji wstępnej, którzy mogą korzystać z dwucyfrowych numery (lub więcej), umożliwia zera wiodące beta01 i beta05 upewnij się, że ich sortowania prawidłowo po dłuższego liczby.</span><span class="sxs-lookup"><span data-stu-id="6ef5c-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
