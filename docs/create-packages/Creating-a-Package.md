---
title: Jak utworzyć pakiet NuGet
description: Szczegółowy przewodnik dotyczący proces projektowania i tworzenia pakietu NuGet, w tym punkty decyzyjne klucza, takich jak pliki i przechowywania wersji.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 435db2d0cddcfd6b9db530cb384cf7facb9170dd
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818467"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="1ea4f-103">Tworzenie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="1ea4f-103">Creating NuGet packages</span></span>

<span data-ttu-id="1ea4f-104">Niezależnie od tego, czego pakiet lub jego kodu zawiera, użyj `nuget.exe` do tej funkcji do składnika, który można udostępniać i używane przez dowolną liczbę inni deweloperzy pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="1ea4f-105">Aby zainstalować `nuget.exe`, zobacz [instalowania NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="1ea4f-106">Należy pamiętać, że program Visual Studio nie ma automatycznie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="1ea4f-107">Jak to działa, pakiet NuGet jest tylko plik ZIP, który jest zastępowana `.nupkg` rozszerzenia i których zawartość odpowiada niektórych Konwencji.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="1ea4f-108">W tym temacie opisano szczegółowe proces tworzenia pakietu, który spełnia te Konwencji.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="1ea4f-109">Wskazówki ukierunkowanych, można znaleźć w temacie [Szybki Start: tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="1ea4f-110">OPAKOWYWANIE rozpoczyna się od skompilowanego kodu (zestawy), symbole i/lub innych plików, które mają zostać dostarczone jako pakiet (zobacz [Przegląd i przepływ pracy](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="1ea4f-111">Ten proces jest niezależna od kompilowania lub w przeciwnym razie generowania plików, które są przekazywane do pakietu, mimo że można narysować z informacji w pliku projektu w celu synchronizowania skompilowane zestawy i pakietów.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="1ea4f-112">W tym temacie dotyczą projektów typu innego niż projektów .NET Core za pomocą programu Visual Studio 2017 i NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="1ea4f-113">W tych projektach platformy .NET Core NuGet używa informacji w pliku projektu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="1ea4f-114">Aby uzyskać więcej informacji, zobacz [utworzyć .NET Standard pakiety z programu Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) i [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="1ea4f-115">Przy wyborze zestawy, które do pakietu</span><span class="sxs-lookup"><span data-stu-id="1ea4f-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="1ea4f-116">Najbardziej ogólnego przeznaczenia pakietów zawiera jeden lub więcej zestawów, które innych deweloperzy mogą używać w ich własnych projektów.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="1ea4f-117">Ogólnie rzecz biorąc najlepiej jeden zestaw na pakietu NuGet, pod warunkiem, że każdy zestaw przydaje się niezależnie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="1ea4f-118">Na przykład, jeśli masz `Utilities.dll` to zależy od `Parser.dll`, i `Parser.dll` przydaje się samodzielnie, a następnie utworzyć jeden pakiet dla każdego.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="1ea4f-119">Dzięki temu deweloperom używanie `Parser.dll` niezależnie od `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="1ea4f-120">Jeśli biblioteki składa się z wielu zestawów, które nie są przydatne niezależnie, jest poprawnie połączyć je w jeden pakiet.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="1ea4f-121">W poprzednim przykładzie, jeśli `Parser.dll` zawiera kod, który jest używany tylko przez `Utilities.dll`, a następnie; można zachować `Parser.dll` w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="1ea4f-122">Podobnie jeśli `Utilities.dll` zależy od `Utilities.resources.dll`, gdzie ponownie nie jest on przydatny samodzielnie, następnie umieść zarówno w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="1ea4f-123">Zasoby są w rzeczywistości w szczególnych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="1ea4f-124">Po zainstalowaniu pakietu w projekcie NuGet automatycznie dodaje odwołania do zestawów do biblioteki dll pakietu, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie (zobacz [ Tworzenie zlokalizowanych pakietów](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="1ea4f-125">Z tego powodu należy unikać `.resources.dll` plików, które w przeciwnym razie zawiera istotne pakiet kodu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="1ea4f-126">Jeśli biblioteka zawiera zestawy międzyoperacyjne COM, wykonaj dodatkowe wskazówki zawarte w [tworzenia pakietów z zestawy międzyoperacyjne COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="1ea4f-127">Rola i struktura pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="1ea4f-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="1ea4f-128">Po sprawdzeniu, jakie pliki do pakietu, następnym krokiem jest utworzenie manifestu pakietu w `.nuspec` pliku XML.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="1ea4f-129">Plik manifestu:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-129">The manifest:</span></span>

1. <span data-ttu-id="1ea4f-130">Zawiera opis zawartości pakietu i jest uwzględniony w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="1ea4f-131">Dyski tworzenia pakietu i program NuGet w sposób instalowania pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="1ea4f-132">Na przykład manifest identyfikuje innych zależności pakietów tak, aby NuGet można także zainstalować te zależności, po zainstalowaniu pakietu głównego.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="1ea4f-133">Zawiera właściwości zarówno wymaganych i opcjonalnych, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="1ea4f-134">Dokładne szczegółów, w tym inne właściwości nie są wymienione w tym miejscu można znaleźć [odwołania .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="1ea4f-135">Wymagane właściwości:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-135">Required properties:</span></span>

- <span data-ttu-id="1ea4f-136">Identyfikator pakietu musi być unikatowa w galerii, który jest hostem pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="1ea4f-137">Numer wersji określonej w formie *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]* gdzie *-sufiks* identyfikuje [wersje wstępne](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="1ea4f-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="1ea4f-138">Tytuł pakietu jako powinien pojawia się na hoście (na przykład nuget.org)</span><span class="sxs-lookup"><span data-stu-id="1ea4f-138">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="1ea4f-139">Informacje o autora i właściciela.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-139">Author and owner information.</span></span>
- <span data-ttu-id="1ea4f-140">Długi opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-140">A long description of the package.</span></span>

<span data-ttu-id="1ea4f-141">Wspólne właściwości opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-141">Common optional properties:</span></span>

- <span data-ttu-id="1ea4f-142">Uwagi do wersji</span><span class="sxs-lookup"><span data-stu-id="1ea4f-142">Release notes</span></span>
- <span data-ttu-id="1ea4f-143">Informacje o prawach autorskich</span><span class="sxs-lookup"><span data-stu-id="1ea4f-143">Copyright information</span></span>
- <span data-ttu-id="1ea4f-144">Krótki opis [interfejsu użytkownika Menedżera pakietów w programie Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="1ea4f-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="1ea4f-145">Identyfikator ustawień regionalnych</span><span class="sxs-lookup"><span data-stu-id="1ea4f-145">A locale ID</span></span>
- <span data-ttu-id="1ea4f-146">Strona główna i adres URL licencji</span><span class="sxs-lookup"><span data-stu-id="1ea4f-146">Home page and license URLs</span></span>
- <span data-ttu-id="1ea4f-147">Adres URL ikony</span><span class="sxs-lookup"><span data-stu-id="1ea4f-147">An icon URL</span></span>
- <span data-ttu-id="1ea4f-148">Wyświetla zależności i odwołań</span><span class="sxs-lookup"><span data-stu-id="1ea4f-148">Lists of dependencies and references</span></span>
- <span data-ttu-id="1ea4f-149">Tagi, które pomagają w galerii wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="1ea4f-149">Tags that assist in gallery searches</span></span>

<span data-ttu-id="1ea4f-150">Poniżej przedstawiono typowe (ale fikcyjne) `.nuspec` pliku z komentarzami opisujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-150">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="1ea4f-151">Szczegółowe informacje o deklarowanie zależności i określanie numerów wersji, zobacz [wersji pakietu](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-151">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="1ea4f-152">Możliwe jest również do powierzchni zasoby z zależnościami bezpośrednio w pakiecie przy użyciu `include` i `exclude` atrybutów na `dependency` elementu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-152">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="1ea4f-153">Zobacz [.nuspec — odwołanie do zależności](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-153">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="1ea4f-154">Ponieważ manifestu jest uwzględniony w pakiecie z niej utworzyć, dowolną liczbę dodatkowe przykłady można znaleźć, sprawdzając istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-154">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="1ea4f-155">Jest dobrym źródłem *globalne pakiety* folderu na komputerze, lokalizację, jest zwracany za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-155">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="1ea4f-156">Przejdź do dowolnego *package\version* folder, kopia `.nupkg` pliku na `.zip` pliku, a następnie otwórz to `.zip` pliku i sprawdź, czy `.nuspec` znajdujące się w nim.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-156">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="1ea4f-157">Podczas tworzenia `.nuspec` z projektu programu Visual Studio manifestu zawiera tokenów, które są zastępowane informacji z projektu, podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-157">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="1ea4f-158">Zobacz [tworzenie .nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-158">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="1ea4f-159">Tworzenie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="1ea4f-159">Creating the .nuspec file</span></span>

<span data-ttu-id="1ea4f-160">Tworzenie manifestu pełną zwykle zaczyna się od podstawowego `.nuspec` plik wygenerowany za pomocą jednego z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-160">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="1ea4f-161">Katalog roboczy opartych na konwencjach</span><span class="sxs-lookup"><span data-stu-id="1ea4f-161">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="1ea4f-162">Zestaw biblioteki DLL</span><span class="sxs-lookup"><span data-stu-id="1ea4f-162">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="1ea4f-163">Projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ea4f-163">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="1ea4f-164">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="1ea4f-164">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="1ea4f-165">Możesz następnie przeprowadź edycję pliku ręcznie tak aby dokładnie zawartość, którą chcesz w ostatnim pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-165">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="1ea4f-166">Wygenerowany `.nuspec` pliki zawierają symbole zastępcze, które muszą zostać zmodyfikowane przed utworzeniem pakietu z `nuget pack` polecenia.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-166">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="1ea4f-167">Aby polecenie kończy się niepowodzeniem, jeśli `.nuspec` zawiera wszystkie elementy zastępcze.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-167">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="1ea4f-168">Z katalogu roboczego opartych na konwencjach</span><span class="sxs-lookup"><span data-stu-id="1ea4f-168">From a convention-based working directory</span></span>

<span data-ttu-id="1ea4f-169">Ponieważ pakiet NuGet jest tylko plik ZIP, który jest zastępowana `.nupkg` rozszerzenia jego często najłatwiej Utwórz strukturę folderów w lokalnym systemie plików, następnie utwórz `.nuspec` pliku bezpośrednio z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-169">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="1ea4f-170">`nuget pack` Polecenia następnie automatycznie dodaje wszystkie pliki w tej struktury folderów (z wyłączeniem wszelkich folderów zaczynające się `.`, co pozwala przechowywać pliki prywatne w tej samej struktury).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-170">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="1ea4f-171">Zaletą tej metody jest, że nie należy określić w manifeście pliki, które mają zostać uwzględnione w pakiecie (zgodnie z objaśnieniem w dalszej części tego tematu).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-171">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="1ea4f-172">Program może po prostu utworzyć strukturę folderów dokładne, który jest przesyłany w pakiecie procesu kompilacji i łatwo może zawierać inne pliki, które mogą być częścią projektu w przeciwnym razie:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-172">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="1ea4f-173">Zawartość i kod źródłowy, który powinien zostać dodane do projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-173">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="1ea4f-174">Skrypty programu PowerShell (pakietów używane w NuGet 2.x można uwzględnić również skrypty instalacji, który nie jest obsługiwany w NuGet 3.x lub nowszy).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-174">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="1ea4f-175">Przekształcenia do istniejących plików konfiguracji i źródła kodu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-175">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="1ea4f-176">Konwencje folderu są następujące:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-176">The folder conventions are as follows:</span></span>

| <span data-ttu-id="1ea4f-177">Folder</span><span class="sxs-lookup"><span data-stu-id="1ea4f-177">Folder</span></span> | <span data-ttu-id="1ea4f-178">Opis</span><span class="sxs-lookup"><span data-stu-id="1ea4f-178">Description</span></span> | <span data-ttu-id="1ea4f-179">Akcja po instalacji</span><span class="sxs-lookup"><span data-stu-id="1ea4f-179">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ea4f-180">(root)</span><span class="sxs-lookup"><span data-stu-id="1ea4f-180">(root)</span></span> | <span data-ttu-id="1ea4f-181">Lokalizacja readme.txt</span><span class="sxs-lookup"><span data-stu-id="1ea4f-181">Location for readme.txt</span></span> | <span data-ttu-id="1ea4f-182">Visual Studio Wyświetla plik readme.txt w folderze głównym pakietu, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-182">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="1ea4f-183">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="1ea4f-183">lib/{tfm}</span></span> | <span data-ttu-id="1ea4f-184">Zestaw (`.dll`), dokumentacji (`.xml`) oraz symbol (`.pdb`) plików dla danego docelowej Framework Moniker (TFM)</span><span class="sxs-lookup"><span data-stu-id="1ea4f-184">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="1ea4f-185">Zestawy są dodawane jako odwołania; `.xml` i `.pdb` kopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-185">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="1ea4f-186">Zobacz [obsługujący wiele platform docelowych](supporting-multiple-target-frameworks.md) tworzenia framework podfoldery specyficznych dla obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-186">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="1ea4f-187">środowisk uruchomieniowych</span><span class="sxs-lookup"><span data-stu-id="1ea4f-187">runtimes</span></span> | <span data-ttu-id="1ea4f-188">Zestaw architektury (`.dll`), symbol (`.pdb`), a zasób macierzysty (`.pri`) plików</span><span class="sxs-lookup"><span data-stu-id="1ea4f-188">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="1ea4f-189">Zestawy są dodawane jako odwołania; inne pliki są kopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-189">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="1ea4f-190">Zobacz [obsługujący wiele platform docelowych](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-190">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="1ea4f-191">zawartość</span><span class="sxs-lookup"><span data-stu-id="1ea4f-191">content</span></span> | <span data-ttu-id="1ea4f-192">Wybrane pliki</span><span class="sxs-lookup"><span data-stu-id="1ea4f-192">Arbitrary files</span></span> | <span data-ttu-id="1ea4f-193">Zawartość jest kopiowana do katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-193">Contents are copied to the project root.</span></span> <span data-ttu-id="1ea4f-194">Pomyśl o **zawartości** folder jako katalog główny aplikacji docelowej, który ostatecznie wykorzystuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-194">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="1ea4f-195">Aby dodać obraz w aplikacji pakietu */obrazy* folderu, umieść go w pakiecie *zawartości/obrazów* folderu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-195">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="1ea4f-196">kompilacja</span><span class="sxs-lookup"><span data-stu-id="1ea4f-196">build</span></span> | <span data-ttu-id="1ea4f-197">MSBuild `.targets` i `.props` plików</span><span class="sxs-lookup"><span data-stu-id="1ea4f-197">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="1ea4f-198">Automatycznie dodaje do pliku projektu lub `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-198">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="1ea4f-199">narzędzia</span><span class="sxs-lookup"><span data-stu-id="1ea4f-199">tools</span></span> | <span data-ttu-id="1ea4f-200">Skrypty programu PowerShell i programy dostępne w konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="1ea4f-200">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="1ea4f-201">`tools` Folderu zostanie dodany do `PATH` zmiennej środowiskowej tylko za pomocą konsoli Menedżera pakietów (w szczególności *nie* do `PATH` zgodnie z ustaleniami dla MSBuild podczas kompilowania projektu).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-201">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="1ea4f-202">Struktury folderu może zawierać dowolną liczbę zestawów dla dowolnej liczby docelowych platform, ta metoda jest niezbędne, podczas tworzenia pakietów, które obsługuje wiele platform</span><span class="sxs-lookup"><span data-stu-id="1ea4f-202">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="1ea4f-203">W każdym przypadku, gdy struktura odpowiedni folder w miejscu, uruchom następujące polecenie w tym folderze, aby utworzyć `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-203">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="1ea4f-204">Ponownie wygenerowanego `.nuspec` nie zawiera żadnych jawnych odwołań do plików w folderze struktury.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-204">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="1ea4f-205">Po utworzeniu pakietu NuGet automatycznie uwzględnia wszystkie pliki.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-205">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="1ea4f-206">Nadal trzeba jednak edytować symbole zastępcze w innych częściach manifestu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-206">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="1ea4f-207">Z zestawu biblioteki DLL</span><span class="sxs-lookup"><span data-stu-id="1ea4f-207">From an assembly DLL</span></span>

<span data-ttu-id="1ea4f-208">W przypadku prostego tworzenia pakietu z zestawu, można wygenerować `.nuspec` pliku z metadanych w zestawie przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-208">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="1ea4f-209">Za pomocą tego formularza zastępuje kilka symbole zastępcze w manifeście z określonymi wartościami z zestawu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-209">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="1ea4f-210">Na przykład `<id>` właściwość jest ustawiona na nazwę zestawu, a `<version>` ustawiono wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-210">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="1ea4f-211">Inne właściwości w manifeście, jednak nie pasują do wartości w zestawie i w związku z tym nadal zawierają symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-211">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="1ea4f-212">Z projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ea4f-212">From a Visual Studio project</span></span>

<span data-ttu-id="1ea4f-213">Tworzenie `.nuspec` z `.csproj` lub `.vbproj` plik jest wygodne, ponieważ inne pakiety, które zostały zainstalowane w projekcie tych odwołuje się automatycznie jako zależności.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-213">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="1ea4f-214">W tym samym folderze co plik projektu, po prostu użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-214">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="1ea4f-215">Powstałe w ten sposób `<project-name>.nuspec` plik zawiera *tokenów* który są zamieniane w czasie tworzenia pakietów z wartościami z projektu, w tym odwołania do innych pakietów, które zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-215">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="1ea4f-216">Token jest rozdzielone `$` symbole po obu stronach właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-216">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="1ea4f-217">Na przykład `<id>` wartości w manifeście, generowane w ten sposób zwykle wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-217">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="1ea4f-218">Token ten zostaje zastąpiony `AssemblyName` wartości z pliku projektu w czasie pakowania.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-218">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="1ea4f-219">Mapowanie dokładne wartości projektu do `.nuspec` tokenów, zobacz [odwołują się zastąpienia tokenów](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-219">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="1ea4f-220">Tokeny zwalnia z konieczności aktualizacji ważnych wartości, takich jak numer wersji w `.nuspec` jak aktualizacji projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-220">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="1ea4f-221">(Możesz zawsze zastąpić tokenów wartości literałów w razie potrzeby).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-221">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="1ea4f-222">Należy pamiętać, że dostępnych jest kilka dodatkowych pakietów opcji dostępne podczas pracy z projektu programu Visual Studio, zgodnie z opisem w [uruchomiony pakiet nuget do wygenerowania pliku .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) później.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-222">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="1ea4f-223">Rozwiązanie na poziomie pakietów</span><span class="sxs-lookup"><span data-stu-id="1ea4f-223">Solution-level packages</span></span>

<span data-ttu-id="1ea4f-224">*NuGet tylko 2.x. Nie jest dostępna w NuGet 3.0 +.*</span><span class="sxs-lookup"><span data-stu-id="1ea4f-224">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="1ea4f-225">NuGet 2.x obsługiwane podstawowe pojęcie w zakresie rozwiązania na poziomie pakietu, który instaluje narzędzia lub dodatkowych poleceń dla konsoli Menedżera pakietów (zawartość `tools` folderu), ale nie dodać odwołania do zawartości, lub utworzyć dostosowań do żadnych projektów rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-225">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="1ea4f-226">Takie pakiety zawierają żadne pliki w jego bezpośrednio `lib`, `content`, lub `build` folderów, a żaden z jego zależności są pliki w odpowiednich `lib`, `content`, lub `build` folderów.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-226">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="1ea4f-227">Śledzi NuGet zainstalowane pakiety poziomu rozwiązania w `packages.config` w pliku `.nuget` , zamiast folderu projektu `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-227">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="1ea4f-228">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="1ea4f-228">New file with default values</span></span>

<span data-ttu-id="1ea4f-229">Poniższe polecenie tworzy manifest domyślny z symbole zastępcze, co zapewnia spełnienie rozpoczynać struktura prawidłowego pliku:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-229">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="1ea4f-230">W przypadku pominięcia \<nazwy pakietu\>, wynikowy plik jest `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-230">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="1ea4f-231">Jeśli podasz nazwę taką jak `Contoso.Utility.UsefulStuff`, plik jest `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-231">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="1ea4f-232">Powstałe w ten sposób `.nuspec` zawiera symbole zastępcze dla wartości, takich jak `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-232">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="1ea4f-233">Pamiętaj edytować plik przed użyciem jej do utworzenia ostatecznego `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-233">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="1ea4f-234">Wybieranie identyfikator unikatowy pakiet i ustawianie numeru wersji</span><span class="sxs-lookup"><span data-stu-id="1ea4f-234">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="1ea4f-235">Identyfikator pakietu (`<id>` element) oraz numer wersji (`<version>` element) są dwie najważniejsze wartości w manifeście, ponieważ jednoznacznie zidentyfikować dokładną kod, który jest zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-235">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="1ea4f-236">**Najlepsze rozwiązania dotyczące identyfikator pakietu:**</span><span class="sxs-lookup"><span data-stu-id="1ea4f-236">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="1ea4f-237">**Unikatowość**: identyfikator musi być unikatowa w nuget.org lub niezależnie od galerii znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-237">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="1ea4f-238">Przed podjęciem decyzji na podstawie identyfikatora, wyszukiwanie odpowiednich galerii, aby sprawdzić, czy nazwa jest już używany.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-238">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="1ea4f-239">Aby uniknąć konfliktów, dobrym wzorzec jest używać nazwy firmy jako pierwsza część identyfikatora, takich jak `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-239">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="1ea4f-240">**Nazw Namespace przypominającej**: postępuj zgodnie z wzorcem podobne do przestrzeni nazw w programie .NET, używając zapisu kropkowego zamiast łączniki.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-240">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="1ea4f-241">Na przykład użyć `Contoso.Utility.UsefulStuff` zamiast `Contoso-Utility-UsefulStuff` lub `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-241">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="1ea4f-242">Konsumenci znajduje się także przydatne, gdy identyfikator pakietu jest zgodna z obszarów nazw używanych w kodzie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-242">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="1ea4f-243">**Przykładowe pakiety**: Jeśli utworzyć pakiet przykładowy kod, który demonstruje sposób używania inny pakiet, dołącz `.Sample` sufiks identyfikatora, jak w `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-243">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="1ea4f-244">(Przykładowy pakiet oczywiście mają zależności na inny pakiet.) Podczas tworzenia pakietu próbki, metoda opartych na konwencjach pracy katalogu opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-244">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="1ea4f-245">W `content` folderu, Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` jako w `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-245">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="1ea4f-246">**Najlepsze rozwiązania dla wersji pakietu:**</span><span class="sxs-lookup"><span data-stu-id="1ea4f-246">**Best practices for the package version:**</span></span>

- <span data-ttu-id="1ea4f-247">Ogólnie rzecz biorąc Ustaw wersję pakietu do dopasowania biblioteki, chociaż nie jest ścisłym wymogiem.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-247">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="1ea4f-248">Jest to proste sprawa ograniczenie długości pakietu w jednym zestawie zgodnie z wcześniejszym opisem w [podejmowania decyzji o którym zestawów do pakietu](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-248">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="1ea4f-249">Ogólnie należy pamiętać, że NuGet sam dotyczy wersji pakietu, podczas rozpoznawania zależności, a nie wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-249">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="1ea4f-250">Podczas korzystania z niestandardowej wersji schematu, należy wziąć pod uwagę NuGet reguły kontroli wersji, zgodnie z objaśnieniem w [wersji pakietu](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-250">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="1ea4f-251">Następujący szereg krótki blogach są także zrozumieć, przechowywanie wersji:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-251">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="1ea4f-252">Część 1: Przyjęcia piekłem bibliotek DLL</span><span class="sxs-lookup"><span data-stu-id="1ea4f-252">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="1ea4f-253">Część 2: Algorytm core</span><span class="sxs-lookup"><span data-stu-id="1ea4f-253">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="1ea4f-254">Część 3: Ujednolicenie za pomocą przekierowania powiązań</span><span class="sxs-lookup"><span data-stu-id="1ea4f-254">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="1ea4f-255">Ustawienie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="1ea4f-255">Setting a package type</span></span>

<span data-ttu-id="1ea4f-256">Nuget 3.5 +, można oznaczyć pakiety z określonym *typu* wskazująca jego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-256">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="1ea4f-257">Domyślnie pakiety nie oznaczona atrybutem typu, w tym wszystkich pakietów utworzonych w starszych wersjach programu NuGet, `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-257">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="1ea4f-258">`Dependency` pakiety typu Dodaj kompilacji lub wykonywania zasoby do biblioteki i aplikacji, a można zainstalować w dowolnym typie projektu (przy założeniu, że są one zgodne).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-258">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="1ea4f-259">`DotnetCliTool` rozszerzenia są pakiety typu [.NET CLI](/dotnet/articles/core/tools/index) i są wywoływane z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-259">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="1ea4f-260">Takie pakiety można zainstalować tylko w projektach platformy .NET Core i nie mają wpływu na operacje przywracania.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-260">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="1ea4f-261">Więcej informacji na temat tych rozszerzeń dla projektu są dostępne w [rozszerzenia architektury .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-261">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="1ea4f-262">Typ niestandardowy pakietów, użyj identyfikatora dowolnego typu, który odpowiada te same zasady stosowania formatu w pakiecie identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-262">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="1ea4f-263">Dowolny typ innych niż `Dependency` i `DotnetCliTool`, jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-263">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="1ea4f-264">Typy pakietów są ustawiane w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-264">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="1ea4f-265">Najlepiej dla zapewnienia zgodności do *nie* jawnie ustawione `Dependency` wpisz i zamiast tego polegać na NuGet zakładając, że ten typ, jeśli żaden typ nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-265">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="1ea4f-266">`.nuspec`: Określ typ pakietu w `packageTypes\packageType` węźle `<metadata>` elementu:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-266">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="1ea4f-267">Dodawanie pliku readme i innych plików</span><span class="sxs-lookup"><span data-stu-id="1ea4f-267">Adding a readme and other files</span></span>

<span data-ttu-id="1ea4f-268">Aby określić bezpośrednio plików do uwzględnienia w pakiecie, należy użyć `<files>` w węźle `.nuspec` pliku, który *następuje* `<metadata>` tagu:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-268">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="1ea4f-269">Korzystając z podejścia opartych na konwencjach katalog roboczy, możesz umieścić readme.txt w katalogu głównym pakietu i innych zawartości w `content` folderu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-269">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="1ea4f-270">Nie `<file>` elementy są niezbędne w manifeście.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-270">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="1ea4f-271">Jeśli dołączysz plik o nazwie `readme.txt` w katalogu głównym pakietu Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst od razu po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-271">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="1ea4f-272">(Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-272">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="1ea4f-273">Na przykład poniżej przedstawiono sposób wyświetlania plik readme dla pakietu HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-273">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Wyświetlanie plik readme dla pakietu NuGet podczas instalacji](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="1ea4f-275">Jeśli dołączysz pustą `<files>` w węźle `.nuspec` pliku NuGet nie zawiera innej zawartości w pakiecie inne niż w `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-275">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="1ea4f-276">W tym właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="1ea4f-276">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="1ea4f-277">W niektórych przypadkach można dodać elementów docelowych niestandardowej kompilacji lub właściwości w projektach używające pakietu, takie jak uruchomienie niestandardowego narzędzia lub procesu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-277">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="1ea4f-278">Możesz to zrobić przez umieszczenie plików w postaci `<package_id>.targets` lub `<package_id>.props` (takich jak `Contoso.Utility.UsefulStuff.targets`) w ramach `\build` folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-278">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="1ea4f-279">Pliki w folderze głównym `\build` folderu są traktowane jako odpowiednie dla wszystkich docelowych platform.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-279">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="1ea4f-280">Aby zapewnić pliki określonej struktury, najpierw umieścić te w odpowiednie podfoldery, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-280">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="1ea4f-281">Następnie w `.nuspec` pliku, pamiętaj odwołać się do tych plików w `<files>` węzła:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-281">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="1ea4f-282">W tym właściwości programu MSBuild i obiektów docelowych w pakiecie został [wprowadzone w systemie NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), dlatego zalecane jest dodawanie `minClientVersion="2.5"` atrybutu `metadata` element, aby wskazać minimalnej wersji klienta NuGet wymaganej do Korzystanie z pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-282">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="1ea4f-283">Gdy NuGet instaluje pakiet o `\build` pliki, dodaje MSBuild `<Import>` elementów w pliku projektu wskazujący `.targets` i `.props` plików.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-283">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="1ea4f-284">(`.props` dodaje się u góry pliku projektu; `.targets` zostanie dodany na dole.) Oddzielne MSBuild warunkowego `<Import>` element jest dodawany do każdej platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-284">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="1ea4f-285">MSBuild `.props` i `.targets` plików dla framework między celem można umieścić w `\buildCrossTargeting` folderu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-285">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="1ea4f-286">Podczas instalacji pakietu NuGet dodaje odpowiadającego `<Import>` elementy do pliku projektu z warunkiem, że platforma docelowa nie jest ustawiona (właściwość MSBuild `$(TargetFramework)` może być pusta).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-286">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="1ea4f-287">Nuget 3.x, elementy docelowe nie zostaną dodane do projektu, ale zamiast tego stają się dostępne za pośrednictwem `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-287">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="1ea4f-288">Tworzenie pakietów z zestawy międzyoperacyjne COM</span><span class="sxs-lookup"><span data-stu-id="1ea4f-288">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="1ea4f-289">Pakiety, które zawierają zestawy międzyoperacyjne COM musi zawierać odpowiednie [plik elementów docelowych](#including-msbuild-props-and-targets-in-a-package) , aby poprawny `EmbedInteropTypes` metadanych jest dodawana do projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-289">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="1ea4f-290">Domyślnie `EmbedInteropTypes` metadanych zawsze ma wartość false dla wszystkich zestawów stosowania PackageReference tak jawnie dodaje plik elementów docelowych tych metadanych.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-290">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="1ea4f-291">Aby uniknąć konfliktów, nazwa docelowego powinna być unikatowa; najlepiej, jeśli jest użycie kombinacji nazwę pakietu i zestaw są osadzone, zastępując `{InteropAssemblyName}` w przykładzie poniżej tej wartości.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-291">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="1ea4f-292">(Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) np.)</span><span class="sxs-lookup"><span data-stu-id="1ea4f-292">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="1ea4f-293">Należy pamiętać, że przy użyciu `packages.config` format zarządzania Dodawanie odwołania do zestawów z pakietów powoduje NuGet i Visual Studio sprawdzić zestawy międzyoperacyjne COM i ustaw `EmbedInteropTypes` na wartość true w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-293">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="1ea4f-294">W takim przypadku elementy docelowe są zastąpione.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-294">In this case the targets are overriden.</span></span>

<span data-ttu-id="1ea4f-295">Ponadto domyślnie [zasoby kompilacji nie przepływu przechodnie](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-295">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="1ea4f-296">Pakiety utworzone zgodnie z opisem w tym miejscu pracy inaczej, gdy są one pobierane jako zależność przechodnie z odwołaniem projektu do projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-296">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="1ea4f-297">Konsument pakietu zezwolić im na przepływ, zmieniając wartość domyślną PrivateAssets, aby nie był uwzględniany kompilacji.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-297">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="1ea4f-298">Z dodatkiem Service pack nuget, aby wygenerować plik .nupkg</span><span class="sxs-lookup"><span data-stu-id="1ea4f-298">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="1ea4f-299">Korzystając z zestawu lub katalog roboczy opartych na konwencjach, Utwórz pakiet, uruchamiając `nuget pack` z Twojej `.nuspec` pliku, zastępując `<project-name>` z Twojej określonej nazwy pliku:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-299">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="1ea4f-300">Korzystając z projektu programu Visual Studio, uruchom `nuget pack` z pliku projektu, który automatycznie ładuje projektu `.nuspec` pliku i zastępuje wszystkie tokeny w nim przy użyciu wartości w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-300">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="1ea4f-301">Bezpośrednio przy użyciu pliku projektu jest niezbędna dla zastępujący tokenu, ponieważ projekt jest źródłem wartości tokenów.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-301">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="1ea4f-302">Token zastępczy nie następuje, jeśli używasz `nuget pack` z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-302">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="1ea4f-303">We wszystkich przypadkach `nuget pack` wyklucza foldery, które zaczynać się kropką, takich jak `.git` lub `.hg`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-303">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="1ea4f-304">NuGet wskazuje, czy wystąpiły żadne błędy w `.nuspec` pliku, który należy korygowanie, takich jak włączaniu zmienić symbole zastępcze w manifeście.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-304">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="1ea4f-305">Raz `nuget pack` zakończy się powodzeniem, masz `.nupkg` pliku, który można opublikować odpowiedni galerii zgodnie z opisem w [publikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-305">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="1ea4f-306">Można zbadać pakietu po jego utworzeniu otworzyć go w [Explorer pakietu](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-306">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="1ea4f-307">Umożliwia widoku graficznego elementów zawartości pakietu i jego manifestu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-307">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="1ea4f-308">Można również zmienić powstałe w ten sposób `.nupkg` pliku `.zip` plików i przejrzyj jego zawartość bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-308">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="1ea4f-309">Dodatkowe opcje</span><span class="sxs-lookup"><span data-stu-id="1ea4f-309">Additional options</span></span>

<span data-ttu-id="1ea4f-310">Można użyć różnych przełączników wiersza polecenia z `nuget pack` Aby wykluczyć pliki, Zastąp numer wersji w manifeście i zmień folder wyjściowy, między innymi funkcjami.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-310">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="1ea4f-311">Pełną listę można znaleźć [pakietu poleceń](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-311">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="1ea4f-312">Czy masz kilka typowych z projektów Visual Studio są następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-312">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="1ea4f-313">**Odwołanie do projektów**: Jeśli projekt odwołuje się do innych projektów, możesz dodać przywoływane projekty jako część pakietu lub zależności, za pomocą `-IncludeReferencedProjects` opcji:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-313">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="1ea4f-314">Ten proces dołączania jest rekursywny, więc jeśli `MyProject.csproj` odwołań projektów B i C i tych projektów odwołania D i E, F, a następnie pliki z B, C, D, E i F znajdują się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-314">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="1ea4f-315">Jeśli przywoływanego projektu zawiera `.nuspec` pliku własną, następnie NuGet dodaje przywoływanego projektu jako zależności zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-315">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="1ea4f-316">Należy spakować i oddzielnie publikowanie tego projektu.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-316">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="1ea4f-317">**Konfiguracja kompilacji**: domyślnie NuGet używa domyślnej konfiguracji kompilacji ustawione w pliku projektu, zwykle *debugowania*.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-317">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="1ea4f-318">Można spakować pliki z różnych kompilacji konfiguracji, takich jak *wersji*, użyj `-properties` opcji konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-318">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="1ea4f-319">**Symbole**: Aby dołączać symbole, umożliwiających konsumentów do wykonania kroków opisanych w debugerze kodu pakietu, należy użyć `-Symbols` opcji:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-319">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="1ea4f-320">Testowanie instalacji pakietu aktualizacji</span><span class="sxs-lookup"><span data-stu-id="1ea4f-320">Testing package installation</span></span>

<span data-ttu-id="1ea4f-321">Przed opublikowaniem pakietu, zwykle można przetestować proces instalowania pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-321">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="1ea4f-322">Testy, upewnij się, że zawsze pliki wszystkie kończyć w ich w odpowiednim miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-322">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="1ea4f-323">Testowanie instalacji ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu normalnych [kroki instalacji pakietu](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-323">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="1ea4f-324">Do testów automatycznych podstawowy proces przebiega w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-324">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="1ea4f-325">Kopiuj `.nupkg` plik do folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-325">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="1ea4f-326">Dodaj folder do źródła pakietu przy użyciu `nuget sources add -name <name> -source <path>` polecenia (zobacz [źródeł nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-326">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="1ea4f-327">Należy pamiętać, że tylko należy ustawić tego lokalnego źródła raz na dowolnym komputerze z danym.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-327">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="1ea4f-328">Zainstaluj pakiet z tego źródła za pomocą `nuget install <packageID> -source <name>` gdzie `<name>` jest zgodna z nazwą źródła przydzieloną `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-328">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="1ea4f-329">Określanie źródła zapewnia zainstalowanie pakietu z tego samego źródła.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-329">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="1ea4f-330">Sprawdź, czy system plików, aby sprawdzić, czy pliki są zainstalowane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="1ea4f-330">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ea4f-331">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ea4f-331">Next Steps</span></span>

<span data-ttu-id="1ea4f-332">Po utworzeniu pakietu, który jest `.nupkg` plików, można opublikować w Galerii wybranym zgodnie z opisem na [publikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="1ea4f-332">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="1ea4f-333">Można również rozszerzyć możliwości pakietu lub w przeciwnym razie sprostania innym sytuacjom zgodnie z opisem w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-333">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="1ea4f-334">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="1ea4f-334">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="1ea4f-335">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="1ea4f-335">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="1ea4f-336">Przekształcenia źródła i plików konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1ea4f-336">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="1ea4f-337">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="1ea4f-337">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="1ea4f-338">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="1ea4f-338">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="1ea4f-339">Ponadto istnieją typy dodatkowego pakietu pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="1ea4f-339">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="1ea4f-340">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="1ea4f-340">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="1ea4f-341">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="1ea4f-341">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
