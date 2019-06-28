---
title: Jak utworzyć pakiet NuGet
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym punkty kluczowe decyzje, np. plików i przechowywania wersji.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: e3a40a521a3b16d9757ef1bbf2511a1537d8bddb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425818"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="40dc3-103">Tworzenie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="40dc3-103">Creating NuGet packages</span></span>

<span data-ttu-id="40dc3-104">Niezależnie od tego, co robi pakietu lub co do kodu zawiera, możesz użyć jednej z narzędzi interfejsu wiersza polecenia albo `nuget.exe` lub `dotnet.exe`, aby spakować tej funkcji do składnika udostępnione i używane przez innych programistów.</span><span class="sxs-lookup"><span data-stu-id="40dc3-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="40dc3-105">Aby zainstalować narzędzia interfejsu wiersza polecenia NuGet, zobacz [narzędzia klienta programu NuGet zainstalować](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="40dc3-106">Należy pamiętać, że program Visual Studio nie ma automatycznie narzędzie interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="40dc3-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="40dc3-107">Dla projektów .NET Core i .NET Standard, które używają formatu zestawu SDK stylu ([atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions)), oraz wszelkie inne projekty zestawu SDK stylu, NuGet używa informacji w pliku projektu bezpośrednio, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="40dc3-107">For .NET Core and .NET Standard projects that use the SDK-style format ([SDK attribute](/dotnet/core/tools/csproj#additions)), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="40dc3-108">Aby uzyskać więcej informacji, zobacz [Utwórz standardowy pakiety .NET za pomocą programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md) i [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-108">For details, see [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

- <span data-ttu-id="40dc3-109">Dla projektów w stylu bez zestawu SDK wykonaj czynności opisane w tym artykule, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="40dc3-109">For non-SDK-style projects, follow the steps described in this article to create a package.</span></span>

- <span data-ttu-id="40dc3-110">Dla projektów migracji z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md), użyj [msbuild - t: pakiet](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="40dc3-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="40dc3-111">Technicznie rzecz biorąc, pakiet NuGet jest po prostu plik ZIP, który jest zastępowana `.nupkg` rozszerzenie i których zawartość dopasowania do określonych konwencji.</span><span class="sxs-lookup"><span data-stu-id="40dc3-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="40dc3-112">W tym temacie opisano szczegółowe proces tworzenia pakietu, który spełnia te Konwencji.</span><span class="sxs-lookup"><span data-stu-id="40dc3-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="40dc3-113">Ukierunkowane instruktażu, można znaleźć [Szybki Start: tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-113">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="40dc3-114">Pakowanie zaczyna się od skompilowanego kodu (zestawów), symbole i/lub innych plików, które mają zostać dostarczone jako pakiet (zobacz [omówienie i przepływ pracy](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="40dc3-114">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="40dc3-115">Ten proces jest niezależna od kompilacji, albo w przeciwnym razie generowania plików, które są przekazywane do pakietu, mimo że można narysować z informacji w pliku projektu, aby zachować synchronizację skompilowanych zestawów i pakietów.</span><span class="sxs-lookup"><span data-stu-id="40dc3-115">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="40dc3-116">W tym temacie dotyczą projektów styl bez zestawu SDK, a zwykle projekty inne niż platformy .NET Core i .NET Standard projektów przy użyciu programu Visual Studio 2017 i wyższych wersji i NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="40dc3-116">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="40dc3-117">Przy wyborze rozwiązania, które zestawy do pakietu</span><span class="sxs-lookup"><span data-stu-id="40dc3-117">Deciding which assemblies to package</span></span>

<span data-ttu-id="40dc3-118">Najbardziej ogólnego przeznaczenia pakiety zawierają jeden lub więcej zestawów, umożliwiające innym deweloperom w ich własnych projektów.</span><span class="sxs-lookup"><span data-stu-id="40dc3-118">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="40dc3-119">Ogólnie rzecz biorąc najlepiej jest mieć jeden zestaw dla pakietu NuGet, pod warunkiem, że każdy zestaw przydaje się niezależnie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-119">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="40dc3-120">Na przykład, jeśli masz `Utilities.dll` zależy `Parser.dll`, i `Parser.dll` przydaje się samodzielnie, a następnie utworzyć jeden pakiet, dla każdego.</span><span class="sxs-lookup"><span data-stu-id="40dc3-120">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="40dc3-121">Dzięki temu deweloperzy mogą używać `Parser.dll` niezależnie od `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-121">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="40dc3-122">Jeśli Twoja biblioteka składa się z wielu zestawów, które nie są przydatne niezależnie, jest dobrym rozwiązaniem połączyć je w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-122">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="40dc3-123">W poprzednim przykładzie, jeśli `Parser.dll` zawiera kod, który jest używany wyłącznie przez `Utilities.dll`, a następnie jest dobrym rozwiązaniem zachować `Parser.dll` w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-123">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="40dc3-124">Podobnie jeśli `Utilities.dll` zależy od `Utilities.resources.dll`, w którym ponownie nie jest on przydatny samodzielnie, następnie składane w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-124">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="40dc3-125">Zasoby są w rzeczywistości szczególny przypadek.</span><span class="sxs-lookup"><span data-stu-id="40dc3-125">Resources are, in fact, a special case.</span></span> <span data-ttu-id="40dc3-126">Po zainstalowaniu do projektu pakiet NuGet automatycznie dodaje odwołania do zestawów do pakietu biblioteki dll, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie (patrz [ Tworzenie zlokalizowanych pakietów](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="40dc3-126">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="40dc3-127">Z tego powodu należy unikać `.resources.dll` dla plików, w przeciwnym razie zawierające kod essential pakietu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-127">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="40dc3-128">Jeśli Twoja biblioteka zawiera zestawy międzyoperacyjne COM, wykonaj dodatkowe wskazówki zawarte w [tworzenia pakietów z zestawy międzyoperacyjne COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="40dc3-128">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="40dc3-129">Rola i struktura pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="40dc3-129">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="40dc3-130">Gdy wiesz, jakie pliki, które chcesz pakietu, następnym krokiem jest utworzenie manifestu pakietu w `.nuspec` pliku XML.</span><span class="sxs-lookup"><span data-stu-id="40dc3-130">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="40dc3-131">Manifest:</span><span class="sxs-lookup"><span data-stu-id="40dc3-131">The manifest:</span></span>

1. <span data-ttu-id="40dc3-132">W tym artykule opisano zawartość pakietu i jest uwzględniony w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-132">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="40dc3-133">Tworzenia pakietu i powoduje, że NuGet na temat instalowania pakietu do projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-133">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="40dc3-134">Na przykład manifest identyfikuje inne zależności pakietu, taki sposób, że NuGet można także zainstalować te zależności, po zainstalowaniu pakietu głównego.</span><span class="sxs-lookup"><span data-stu-id="40dc3-134">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="40dc3-135">Zawiera właściwości wymagane i opcjonalne, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="40dc3-135">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="40dc3-136">Szczegółowymi informacjami na temat, w tym inne właściwości, które nie są wymienione w tym miejscu można znaleźć [odwołania .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-136">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="40dc3-137">Wymagane właściwości:</span><span class="sxs-lookup"><span data-stu-id="40dc3-137">Required properties:</span></span>

- <span data-ttu-id="40dc3-138">Identyfikator pakietu musi być unikatowa w galerii, który jest hostem pakietu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-138">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="40dc3-139">Numer wersji określonej w formie *Wersja_główna.WERSJA_POMOCNICZA.poprawka [-sufiks]* gdzie *-sufiks* identyfikuje [wersje wstępne](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="40dc3-139">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="40dc3-140">Tytuł pakietu, ponieważ powinien pojawić się na hoście (np. nuget.org)</span><span class="sxs-lookup"><span data-stu-id="40dc3-140">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="40dc3-141">Informacje dotyczące autora i właściciela.</span><span class="sxs-lookup"><span data-stu-id="40dc3-141">Author and owner information.</span></span>
- <span data-ttu-id="40dc3-142">Długi opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-142">A long description of the package.</span></span>

<span data-ttu-id="40dc3-143">Wspólne właściwości opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="40dc3-143">Common optional properties:</span></span>

- <span data-ttu-id="40dc3-144">Uwagi do wersji</span><span class="sxs-lookup"><span data-stu-id="40dc3-144">Release notes</span></span>
- <span data-ttu-id="40dc3-145">Informacje o prawach autorskich</span><span class="sxs-lookup"><span data-stu-id="40dc3-145">Copyright information</span></span>
- <span data-ttu-id="40dc3-146">Krótki opis [interfejs użytkownika Menedżera pakietów w programie Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="40dc3-146">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="40dc3-147">Identyfikator ustawień regionalnych</span><span class="sxs-lookup"><span data-stu-id="40dc3-147">A locale ID</span></span>
- <span data-ttu-id="40dc3-148">Adres URL projektu</span><span class="sxs-lookup"><span data-stu-id="40dc3-148">Project URL</span></span>
- <span data-ttu-id="40dc3-149">Licencja jako wyrażenie lub plik (`licenseUrl` jest wycofywany, użyj [ `license` elementu metadanych nuspec](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="40dc3-149">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="40dc3-150">Adres URL ikony</span><span class="sxs-lookup"><span data-stu-id="40dc3-150">An icon URL</span></span>
- <span data-ttu-id="40dc3-151">Listy zależności i odwołań</span><span class="sxs-lookup"><span data-stu-id="40dc3-151">Lists of dependencies and references</span></span>
- <span data-ttu-id="40dc3-152">Tagi, które pomagają w galerii wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="40dc3-152">Tags that assist in gallery searches</span></span>

<span data-ttu-id="40dc3-153">Poniżej przedstawiono typowe (ale fikcyjne) `.nuspec` pliku z komentarzami opisujący właściwości:</span><span class="sxs-lookup"><span data-stu-id="40dc3-153">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

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

<span data-ttu-id="40dc3-154">Aby uzyskać szczegółowe informacje dotyczące zadeklarowania zależnościami i określania numerów wersji, zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-154">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="40dc3-155">Możliwe jest również do powierzchni zasoby z zależnościami bezpośrednio w pakiecie przy użyciu `include` i `exclude` atrybuty na `dependency` elementu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-155">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="40dc3-156">Zobacz [odwołanie .nuspec — zależności](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="40dc3-156">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="40dc3-157">Ponieważ manifestu jest uwzględniony w pakiecie utworzonych na jej podstawie, dowolną liczbę dodatkowe przykłady można znaleźć, sprawdzając istniejących pakietów.</span><span class="sxs-lookup"><span data-stu-id="40dc3-157">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="40dc3-158">Jest dobrym źródłem *globalnymi pakietami* folderu na komputerze, lokalizacji, który jest zwracany przez polecenie:</span><span class="sxs-lookup"><span data-stu-id="40dc3-158">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="40dc3-159">Przejdź do dowolnego *package\version* folderu, kopiowanie `.nupkg` plik `.zip` pliku, a następnie otwórz to `.zip` plików i zbadaj `.nuspec` znajdujący się w nim.</span><span class="sxs-lookup"><span data-stu-id="40dc3-159">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="40dc3-160">Podczas tworzenia `.nuspec` z projektu programu Visual Studio manifest zawiera tokenów, które są zastępowane informacjami z projektu podczas kompilowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-160">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="40dc3-161">Zobacz [tworzenie .nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="40dc3-161">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="40dc3-162">Tworzenie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="40dc3-162">Creating the .nuspec file</span></span>

<span data-ttu-id="40dc3-163">Tworzenie pełny manifeście zwykle zaczyna się od podstawowego `.nuspec` plik wygenerowany za pomocą jednego z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="40dc3-163">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="40dc3-164">Przejdź do katalogu roboczego oparty na Konwencji</span><span class="sxs-lookup"><span data-stu-id="40dc3-164">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="40dc3-165">Zestaw bibliotek DLL</span><span class="sxs-lookup"><span data-stu-id="40dc3-165">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="40dc3-166">A Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="40dc3-166">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="40dc3-167">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="40dc3-167">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="40dc3-168">Możesz następnie przeprowadź edycję pliku ręcznie, aby go w tym artykule opisano dokładnie zawartość, którą chcesz w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="40dc3-168">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="40dc3-169">Wygenerowany `.nuspec` pliki zawierają symbole zastępcze, które muszą zostać zmodyfikowane, przed utworzeniem pakietu o `nuget pack` polecenia.</span><span class="sxs-lookup"><span data-stu-id="40dc3-169">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="40dc3-170">Czy polecenie zakończy się niepowodzeniem, jeśli `.nuspec` zawiera wszystkie symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="40dc3-170">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="40dc3-171">Z katalogu roboczego oparty na Konwencji</span><span class="sxs-lookup"><span data-stu-id="40dc3-171">From a convention-based working directory</span></span>

<span data-ttu-id="40dc3-172">Ponieważ pakiet NuGet jest po prostu plik ZIP, który jest zastępowana `.nupkg` rozszerzenia, często łatwiej jest utworzyć strukturę folderów w lokalnym systemie plików, a następnie utwórz `.nuspec` pliku bezpośrednio z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="40dc3-172">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="40dc3-173">`nuget pack` Polecenie następnie automatycznie dodaje wszystkie pliki w tej strukturze folderu (z wyłączeniem wszystkie foldery, które zaczynają się od `.`, dzięki czemu możesz przechowywać pliki prywatne w tej samej struktury).</span><span class="sxs-lookup"><span data-stu-id="40dc3-173">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="40dc3-174">Zaletą tego podejścia jest to, nie należy określić w manifeście pliki, które mają zostać uwzględnione w pakiecie (opisany w dalszej części tego tematu).</span><span class="sxs-lookup"><span data-stu-id="40dc3-174">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="40dc3-175">Po prostu może mieć proces kompilacji, tworzyć strukturę folderów dokładnie, która przechodzi do pakietu i innych plików, które mogą być częścią projektu w przeciwnym razie można łatwo dołączyć:</span><span class="sxs-lookup"><span data-stu-id="40dc3-175">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="40dc3-176">Zawartość i kod źródłowy, który powinien dodane do projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="40dc3-176">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="40dc3-177">Skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="40dc3-177">PowerShell scripts</span></span>
- <span data-ttu-id="40dc3-178">Przekształcenia do istniejącej konfiguracji i plikami źródła kodu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-178">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="40dc3-179">Konwencje folderze są następujące:</span><span class="sxs-lookup"><span data-stu-id="40dc3-179">The folder conventions are as follows:</span></span>

| <span data-ttu-id="40dc3-180">Folder</span><span class="sxs-lookup"><span data-stu-id="40dc3-180">Folder</span></span> | <span data-ttu-id="40dc3-181">Opis</span><span class="sxs-lookup"><span data-stu-id="40dc3-181">Description</span></span> | <span data-ttu-id="40dc3-182">Akcja po instalacji pakietu</span><span class="sxs-lookup"><span data-stu-id="40dc3-182">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40dc3-183">(root)</span><span class="sxs-lookup"><span data-stu-id="40dc3-183">(root)</span></span> | <span data-ttu-id="40dc3-184">Lokalizacja readme.txt</span><span class="sxs-lookup"><span data-stu-id="40dc3-184">Location for readme.txt</span></span> | <span data-ttu-id="40dc3-185">Visual Studio Wyświetla plik readme.txt w katalogu głównym pakietu, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="40dc3-185">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="40dc3-186">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="40dc3-186">lib/{tfm}</span></span> | <span data-ttu-id="40dc3-187">Zestaw (`.dll`), dokumentacji (`.xml`) i symbol (`.pdb`) plików dla danego Moniker Framework docelowych (TFM)</span><span class="sxs-lookup"><span data-stu-id="40dc3-187">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="40dc3-188">Zestawy są dodawane jako odwołania do kompilacji, jak również środowisko uruchomieniowe `.xml` i `.pdb` skopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-188">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="40dc3-189">Zobacz [Obsługa wielu platform docelowych](supporting-multiple-target-frameworks.md) tworzenia framework podfoldery specyficznych dla obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="40dc3-189">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="40dc3-190">REF / {tfm}</span><span class="sxs-lookup"><span data-stu-id="40dc3-190">ref/{tfm}</span></span> | <span data-ttu-id="40dc3-191">Zestaw (`.dll`) i symbol (`.pdb`) plików dla danego Moniker Framework docelowych (TFM)</span><span class="sxs-lookup"><span data-stu-id="40dc3-191">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="40dc3-192">Zestawy są dodawane jako odwołania tylko w przypadku kompilowania; Nic nie zostanie więc skopiowane do folderu bin projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-192">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="40dc3-193">środowiska uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="40dc3-193">runtimes</span></span> | <span data-ttu-id="40dc3-194">Architektury zestawu (`.dll`), symbol (`.pdb`), a zasób macierzysty (`.pri`) plików</span><span class="sxs-lookup"><span data-stu-id="40dc3-194">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="40dc3-195">Zestawy są dodawane jako odwołania tylko dla środowiska uruchomieniowego; inne pliki są kopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-195">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="40dc3-196">Zawsze powinien istnieć odpowiedni (TFM) `AnyCPU` określony zestaw, w obszarze `/ref/{tfm}` folder w celu zapewnienia odpowiedniego zestawu czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="40dc3-196">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="40dc3-197">Zobacz [Obsługa wielu platform docelowych](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-197">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="40dc3-198">zawartość</span><span class="sxs-lookup"><span data-stu-id="40dc3-198">content</span></span> | <span data-ttu-id="40dc3-199">Wybrane pliki</span><span class="sxs-lookup"><span data-stu-id="40dc3-199">Arbitrary files</span></span> | <span data-ttu-id="40dc3-200">Zawartość jest kopiowana do katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-200">Contents are copied to the project root.</span></span> <span data-ttu-id="40dc3-201">Traktować **zawartości** folder jako katalog główny aplikacji docelowej, który ostatecznie używa pakietu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-201">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="40dc3-202">Do pakietu, Dodaj obraz w aplikacji */obrazy* folder, umieść go w tym pakiecie *zawartości/obrazów* folderu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-202">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="40dc3-203">kompilacja</span><span class="sxs-lookup"><span data-stu-id="40dc3-203">build</span></span> | <span data-ttu-id="40dc3-204">Program MSBuild `.targets` i `.props` plików</span><span class="sxs-lookup"><span data-stu-id="40dc3-204">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="40dc3-205">Automatycznie wstawiany do pliku projektu lub `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="40dc3-205">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="40dc3-206">narzędzia</span><span class="sxs-lookup"><span data-stu-id="40dc3-206">tools</span></span> | <span data-ttu-id="40dc3-207">Skrypty programu PowerShell i programów dostępne z konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="40dc3-207">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="40dc3-208">`tools` Folder zostanie dodany do `PATH` zmiennej środowiskowej tylko za pomocą konsoli Menedżera pakietów (w szczególności *nie* do `PATH` według stawki ustalonej dla platformy MSBuild podczas kompilowania projektu).</span><span class="sxs-lookup"><span data-stu-id="40dc3-208">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="40dc3-209">Twoja struktura folderów może zawierać dowolną liczbę zestawów dla dowolnej liczby platform docelowych, ta metoda jest niezbędna, podczas tworzenia pakietów, które obsługują wiele platform.</span><span class="sxs-lookup"><span data-stu-id="40dc3-209">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="40dc3-210">W każdym przypadku, gdy struktura żądany folder w miejscu, uruchom następujące polecenie w tym folderze, aby utworzyć `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="40dc3-210">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="40dc3-211">Ponownie wygenerowany `.nuspec` nie zawiera żadnych jawnych odwołań do plików w strukturze folderu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-211">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="40dc3-212">Po utworzeniu pakietu NuGet automatycznie uwzględnia wszystkie pliki.</span><span class="sxs-lookup"><span data-stu-id="40dc3-212">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="40dc3-213">Nadal należy jednak edytować wartości symboli zastępczych w innych częściach manifestu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-213">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="40dc3-214">Z zestawu biblioteki DLL</span><span class="sxs-lookup"><span data-stu-id="40dc3-214">From an assembly DLL</span></span>

<span data-ttu-id="40dc3-215">W prostym przypadku tworzenie pakietu z zestawu, można wygenerować `.nuspec` pliku z metadanych w zestawie, używając następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="40dc3-215">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="40dc3-216">Za pomocą tego formularza zastępuje kilka symboli zastępczych w manifeście z określonymi wartościami z zestawu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-216">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="40dc3-217">Na przykład `<id>` właściwość jest ustawiona na nazwę zestawu i `<version>` ustawiono wersję zestawu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-217">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="40dc3-218">Inne właściwości w manifeście, jednak nie ma pasującej wartości w zestawie i związku z tym nadal zawierają symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="40dc3-218">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="40dc3-219">From a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="40dc3-219">From a Visual Studio project</span></span>

<span data-ttu-id="40dc3-220">Tworzenie `.nuspec` z `.csproj` lub `.vbproj` pliku jest wygodne, ponieważ inne pakiety, które zostały zainstalowane do tych projektu są automatycznie określane jako zależności.</span><span class="sxs-lookup"><span data-stu-id="40dc3-220">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="40dc3-221">W tym samym folderze co plik projektu, po prostu użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="40dc3-221">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="40dc3-222">Wartość wynikowa `<project-name>.nuspec` plik zawiera *tokenów* , zostaną zastąpione podczas pakowania wartości z projektu, w tym odwołania do innych pakietów, które zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="40dc3-222">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="40dc3-223">Token jest rozdzielone `$` symbole po obu stronach właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-223">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="40dc3-224">Na przykład `<id>` wartość manifestu wygenerowane w ten sposób zwykle pojawia się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="40dc3-224">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="40dc3-225">Token ten zostanie zastąpiony `AssemblyName` wartości z pliku projektu w czasie pakowania.</span><span class="sxs-lookup"><span data-stu-id="40dc3-225">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="40dc3-226">Dokładne mapowania projektu wartości `.nuspec` tokenów, zobacz [odwoływać się do zastąpienia tokenów](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="40dc3-226">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="40dc3-227">Tokeny zwalnia z konieczności aktualizowania niezwykle istotne wartości, takich jak numer wersji w `.nuspec` podczas aktualizowania projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-227">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="40dc3-228">(Możesz zawsze zastąpić tokeny przy użyciu wartości literału w razie potrzeby).</span><span class="sxs-lookup"><span data-stu-id="40dc3-228">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="40dc3-229">Należy pamiętać, że kilka opcji tworzenia dodatkowych pakietów dostępne podczas pracy z projektu programu Visual Studio, zgodnie z opisem w [uruchomiony pakiet nuget, aby wygenerować plik .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) później.</span><span class="sxs-lookup"><span data-stu-id="40dc3-229">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="40dc3-230">Pakiety na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="40dc3-230">Solution-level packages</span></span>

<span data-ttu-id="40dc3-231">*NuGet 2.x tylko. Nie jest dostępna w pakiecie NuGet 3.0 +.*</span><span class="sxs-lookup"><span data-stu-id="40dc3-231">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="40dc3-232">NuGet 2.x obsługuje pojęcie pakiet poziomie rozwiązania, który instaluje narzędzia lub dodatkowych poleceń konsoli Menedżera pakietów (zawartość `tools` folderu), ale dodaj odwołania do zawartości, ani nie lacji do żadnych projektów rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-232">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="40dc3-233">Takie pakiety zawierają żadnych plików w jego bezpośredniej `lib`, `content`, lub `build` foldery i żaden z jej zależnościami mieć plików w odpowiednich `lib`, `content`, lub `build` folderów.</span><span class="sxs-lookup"><span data-stu-id="40dc3-233">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="40dc3-234">Śledzi NuGet zainstalowanych pakietów poziomie rozwiązania w `packages.config` w pliku `.nuget` projektu, a nie folder `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="40dc3-234">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="40dc3-235">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="40dc3-235">New file with default values</span></span>

<span data-ttu-id="40dc3-236">Następujące polecenie tworzy domyślny manifest z symbolami zastępczymi, który gwarantuje, że rozpoczynać struktury odpowiednich plików:</span><span class="sxs-lookup"><span data-stu-id="40dc3-236">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="40dc3-237">Jeżeli pominięto \<nazwy pakietu\>, wynikowy plik jest `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-237">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="40dc3-238">Jeśli takie jak Podaj nazwę `Contoso.Utility.UsefulStuff`, plik jest `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-238">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="40dc3-239">Wartość wynikowa `.nuspec` zawiera symbole zastępcze dla wartości, takich jak `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-239">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="40dc3-240">Pamiętaj edytować plik przed użyciem jej do utworzenia końcowe `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="40dc3-240">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="40dc3-241">Wybieranie identyfikator unikatowy pakiet i ustawiania numeru wersji</span><span class="sxs-lookup"><span data-stu-id="40dc3-241">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="40dc3-242">Identyfikator pakietu (`<id>` elementu) i numeru wersji (`<version>` elementu) są dwoma najważniejszymi wartościami w manifeście, ponieważ jednoznacznie zidentyfikować dokładny kod, który jest zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-242">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="40dc3-243">**Najlepsze rozwiązania dotyczące identyfikator pakietu:**</span><span class="sxs-lookup"><span data-stu-id="40dc3-243">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="40dc3-244">**Unikatowość**: Identyfikator musi być unikatowa w witrynie nuget.org lub niezależnie od galerii obsługuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="40dc3-244">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="40dc3-245">Przed podjęciem decyzji o odpowiadającym, wyszukiwanie dotyczy galerii, sprawdź, czy nazwa jest już używana.</span><span class="sxs-lookup"><span data-stu-id="40dc3-245">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="40dc3-246">Aby uniknąć konfliktów, dobrym deseń ma używać nazwy firmy jako pierwsza część identyfikatora, takich jak `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-246">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="40dc3-247">**Jak Namespace nazw**: Wykonaj podobny do przestrzeni nazw na platformie .NET, używając zapisu kropkowego zamiast łączniki wzorca.</span><span class="sxs-lookup"><span data-stu-id="40dc3-247">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="40dc3-248">Na przykład użyć `Contoso.Utility.UsefulStuff` zamiast `Contoso-Utility-UsefulStuff` lub `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-248">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="40dc3-249">Odbiorcy również okazać się pomocne podczas identyfikator pakietu jest zgodny przestrzenie nazw używane w kodzie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-249">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="40dc3-250">**Przykładowe pakiety**: W przypadku utworzenia pakiet przykładowy kod, który pokazuje, jak korzystać z innym pakietem, dołącz `.Sample` jako sufiks do identyfikatora, jak `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-250">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="40dc3-251">(Przykładowego pakietu oczywiście musi zależność od innego pakietu.) Podczas tworzenia pakiet przykładowy, użyj opisanego wcześniej metody opartej na Konwencji katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="40dc3-251">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="40dc3-252">W `content` folderze Rozmieść przykładowego kodu w folderze o nazwie `\Samples\<identifier>` jak `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-252">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="40dc3-253">**Najlepsze rozwiązania dla używanej wersji pakietu:**</span><span class="sxs-lookup"><span data-stu-id="40dc3-253">**Best practices for the package version:**</span></span>

- <span data-ttu-id="40dc3-254">Ogólnie rzecz biorąc należy ustawić wersję pakietu pasuje do biblioteki, chociaż nie jest to bezwzględnie konieczne.</span><span class="sxs-lookup"><span data-stu-id="40dc3-254">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="40dc3-255">To będzie polegać na ograniczenie pakietu w jednym zestawie, jak opisano wcześniej w [podejmowania decyzji, które zestawy do pakietu](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="40dc3-255">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="40dc3-256">Ogólnie należy pamiętać, że NuGet, sama zajmuje się wersje pakietów, podczas rozpoznawania zależności, a nie wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-256">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="40dc3-257">Przy użyciu schematu niestandardowej wersji, należy wziąć pod uwagę reguły kontroli wersji NuGet, jak wyjaśniono w [przechowywanie wersji pakietów](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-257">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="40dc3-258">Następujące serię wpisów w blogu krótki są pomocne w zrozumieniu przechowywanie wersji:</span><span class="sxs-lookup"><span data-stu-id="40dc3-258">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="40dc3-259">Część 1. Biorąc na piekłem bibliotek DLL</span><span class="sxs-lookup"><span data-stu-id="40dc3-259">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="40dc3-260">Część 2. Algorytm core</span><span class="sxs-lookup"><span data-stu-id="40dc3-260">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="40dc3-261">Część 3: Ujednolicenie słów za pomocą przekierowania powiązań</span><span class="sxs-lookup"><span data-stu-id="40dc3-261">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="40dc3-262">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="40dc3-262">Setting a package type</span></span>

<span data-ttu-id="40dc3-263">Nuget 3.5 + pakiety mogą być oznaczone określonym *typ pakietu* do wskazania jego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="40dc3-263">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="40dc3-264">Domyślnie nie jest oznaczona za pomocą typu, w tym wszystkie pakiety utworzone w starszych wersjach programu NuGet, pakietów `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-264">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="40dc3-265">`Dependency` pakiety typu Dodaj zasoby kompilacji lub czasu wykonywania bibliotek i aplikacji, a można zainstalować w dowolnym typem projektu (przy założeniu, że są one zgodne).</span><span class="sxs-lookup"><span data-stu-id="40dc3-265">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="40dc3-266">`DotnetCliTool` rozszerzenia są pakiety typu [.NET CLI](/dotnet/articles/core/tools/index) i są wywoływane z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="40dc3-266">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="40dc3-267">Takie pakiety można zainstalować tylko w projektach .NET Core i nie mają wpływu na operacje przywracania.</span><span class="sxs-lookup"><span data-stu-id="40dc3-267">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="40dc3-268">Więcej informacji na temat tych rozszerzeń-projekt są dostępne w [rozszerzalność platformy .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="40dc3-268">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="40dc3-269">Pakiety typu niestandardowego Użyj identyfikatora dowolnego typu, który jest zgodny z tych samych zasad format jako pakiet identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="40dc3-269">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="40dc3-270">Dowolny typ inny niż `Dependency` i `DotnetCliTool`, jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40dc3-270">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="40dc3-271">Typy pakietów są ustawiane w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="40dc3-271">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="40dc3-272">Jest najlepszym rozwiązaniem dla zapewnienia zgodności, aby *nie* jawnie ustawionej `Dependency` wpisz i zamiast polegać na NuGet, zakładając, że tego typu, gdy typ nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="40dc3-272">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="40dc3-273">`.nuspec`: Wskazuje typ pakietu we `packageTypes\packageType` węźle `<metadata>` elementu:</span><span class="sxs-lookup"><span data-stu-id="40dc3-273">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="40dc3-274">Dodawanie pliku readme i inne pliki</span><span class="sxs-lookup"><span data-stu-id="40dc3-274">Adding a readme and other files</span></span>

<span data-ttu-id="40dc3-275">Aby bezpośrednio określić pliki do dołączenia do pakietu, należy użyć `<files>` w węźle `.nuspec` pliku, który *następuje* `<metadata>` tag:</span><span class="sxs-lookup"><span data-stu-id="40dc3-275">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="40dc3-276">Korzystając z podejścia opartego na Konwencji katalog roboczy, możesz umieścić readme.txt w głównym pakietu i innych zawartości `content` folderu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-276">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="40dc3-277">Nie `<file>` elementy są niezbędne w manifeście.</span><span class="sxs-lookup"><span data-stu-id="40dc3-277">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="40dc3-278">Gdy uwzględnisz plik o nazwie `readme.txt` w katalogu głównym pakietu Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst od razu po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="40dc3-278">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="40dc3-279">(Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności).</span><span class="sxs-lookup"><span data-stu-id="40dc3-279">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="40dc3-280">Na przykład poniżej przedstawiono sposób wyświetlania pliku readme pakietu HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="40dc3-280">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Wyświetlanie pliku readme podczas instalacji pakietu NuGet](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="40dc3-282">Jeśli dołączysz pustą `<files>` w węźle `.nuspec` pliku NuGet nie zawiera także do innej zawartości w pakiecie innych niż `lib` folderu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-282">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="40dc3-283">W tym cele i właściwości programu MSBuild w pakiecie</span><span class="sxs-lookup"><span data-stu-id="40dc3-283">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="40dc3-284">W niektórych przypadkach warto dodać obiekty docelowe kompilacji niestandardowej lub właściwości w projektach korzystających z pakietu, takie jak uruchomienie niestandardowego narzędzia lub procesu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="40dc3-284">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="40dc3-285">Można to zrobić, umieszczanie plików w postaci `<package_id>.targets` lub `<package_id>.props` (takie jak `Contoso.Utility.UsefulStuff.targets`) w ramach `\build` folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-285">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="40dc3-286">Pliki w folderze głównym `\build` folderu są traktowane jako odpowiednie dla wszystkich ustalać platformy docelowe.</span><span class="sxs-lookup"><span data-stu-id="40dc3-286">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="40dc3-287">Do udostępnienia plików określonej platformy, najpierw umieścić je w odpowiednich podfolderach, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="40dc3-287">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="40dc3-288">Następnie w `.nuspec` pliku, pamiętaj odwoływać się do tych plików w `<files>` węzła:</span><span class="sxs-lookup"><span data-stu-id="40dc3-288">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="40dc3-289">W tym cele i właściwości programu MSBuild w pakiecie został [wprowadzone w programie NuGet w wersji 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), dlatego zalecane jest dodawanie `minClientVersion="2.5"` atrybutu `metadata` element, aby wskazać, minimalna wersja klienta NuGet, wymagane do Używanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-289">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="40dc3-290">Gdy NuGet instaluje pakiet o `\build` pliki, dodaje MSBuild `<Import>` elementy w pliku projektu, wskazując `.targets` i `.props` plików.</span><span class="sxs-lookup"><span data-stu-id="40dc3-290">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="40dc3-291">(`.props` zostanie dodany w górnej części pliku projektu; `.targets` zostanie dodany w dolnej części.) Oddzielne MSBuild warunkowego `<Import>` element jest dodawany dla każdej platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="40dc3-291">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="40dc3-292">Program MSBuild `.props` i `.targets` pliki for cross-adresowanie można umieścić w `\buildMultiTargeting` folderu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-292">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="40dc3-293">Podczas instalacji pakietu NuGet dodaje odpowiednich `<Import>` elementy do pliku projektu z warunkiem, że platforma docelowa nie jest ustawiona (właściwości programu MSBuild `$(TargetFramework)` może być pusta).</span><span class="sxs-lookup"><span data-stu-id="40dc3-293">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="40dc3-294">Nuget 3.x, elementy docelowe nie są dodawane do projektu, ale zamiast tego udostępnionych za pośrednictwem `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-294">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="40dc3-295">Tworzenie pakietów przy użyciu zestawów międzyoperacyjnych COM</span><span class="sxs-lookup"><span data-stu-id="40dc3-295">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="40dc3-296">Pakiety, które zawierają zestawy międzyoperacyjne COM musi zawierać odpowiednią [plik docelowy](#including-msbuild-props-and-targets-in-a-package) tak, aby poprawny `EmbedInteropTypes` metadane dodawane do projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="40dc3-296">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="40dc3-297">Domyślnie `EmbedInteropTypes` metadanych ma zawsze wartość false dla wszystkich zestawów stosowania PackageReference więc plik elementów docelowych dodaje te metadane jawnie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-297">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="40dc3-298">Aby uniknąć konfliktów, nazwa docelowego powinna być unikatowa. w idealnym przypadku należy użyć zestawienia nazwę pakietu i zestaw jest osadzony, zastępując `{InteropAssemblyName}` w poniższym przykładzie przy użyciu tej wartości.</span><span class="sxs-lookup"><span data-stu-id="40dc3-298">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="40dc3-299">(Zobacz też [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) np.)</span><span class="sxs-lookup"><span data-stu-id="40dc3-299">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="40dc3-300">Należy pamiętać, że podczas korzystania `packages.config` zarządzania formatu, dodawanie odwołań do zestawów z pakietów powoduje, że NuGet i programu Visual Studio sprawdzić, czy są zestawy międzyoperacyjne COM i ustawić `EmbedInteropTypes` na wartość true w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-300">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="40dc3-301">W tym przypadku cele są zastąpione.</span><span class="sxs-lookup"><span data-stu-id="40dc3-301">In this case the targets are overriden.</span></span>

<span data-ttu-id="40dc3-302">Ponadto domyślnie [zasoby kompilacji nie została przechodnio przepływu](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="40dc3-302">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="40dc3-303">Pakiety utworzone zgodnie z opisem w tym miejscu pracy inaczej, gdy są one pobierane jako zależność przechodnich z odwołaniem projektu do projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-303">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="40dc3-304">Konsument pakietu można zezwolić na przepływ, modyfikując wartość domyślną PrivateAssets wykluczającą kompilacji.</span><span class="sxs-lookup"><span data-stu-id="40dc3-304">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="40dc3-305">Z dodatkiem Service pack nuget, aby wygenerować plik .nupkg</span><span class="sxs-lookup"><span data-stu-id="40dc3-305">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="40dc3-306">Korzystając z zestawu lub katalog roboczy oparty na Konwencji, Utwórz pakiet, uruchamiając `nuget pack` za pomocą usługi `.nuspec` pliku, zastępując `<project-name>` za pomocą usługi określonej nazwy pliku:</span><span class="sxs-lookup"><span data-stu-id="40dc3-306">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="40dc3-307">Korzystając z projektu programu Visual Studio, uruchom `nuget pack` przy użyciu pliku projektu, który automatycznie ładuje projektu `.nuspec` plików i zastępuje wszystkie tokeny znajdujący się w nim przy użyciu wartości w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="40dc3-307">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="40dc3-308">Bezpośrednio przy użyciu pliku projektu jest niezbędna do zastępowania tokenu, ponieważ projekt jest źródłem wartości tokenu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-308">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="40dc3-309">Zastępowania tokenu nie następuje, jeśli używasz `nuget pack` z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="40dc3-309">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="40dc3-310">We wszystkich przypadkach `nuget pack` wyklucza folderów rozpoczynających się od kropki, takich jak `.git` lub `.hg`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-310">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="40dc3-311">NuGet wskazuje, czy istnieją błędy w `.nuspec` plików, które wymagają korygowanie, takie jak Zapominanie o zmieniać wartości symboli zastępczych w manifeście.</span><span class="sxs-lookup"><span data-stu-id="40dc3-311">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="40dc3-312">Gdy `nuget pack` zakończy się powodzeniem, masz `.nupkg` pliku, który można opublikować odpowiedni galerii, zgodnie z opisem w [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-312">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="40dc3-313">Można zbadać pakietu po jej utworzeniu go otworzyć w [narzędziu Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="40dc3-313">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="40dc3-314">Umożliwia graficzne przedstawienie zawartości pakietu i jego manifestu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-314">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="40dc3-315">Można również zmienić nazwę wynikowy `.nupkg` plik `.zip` pliku i przejrzyj jego zawartość bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="40dc3-315">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="40dc3-316">Dodatkowe opcje</span><span class="sxs-lookup"><span data-stu-id="40dc3-316">Additional options</span></span>

<span data-ttu-id="40dc3-317">Można użyć różnych przełączników wiersza polecenia przy użyciu `nuget pack` Aby wykluczyć pliki, zastąpić numer wersji w manifeście i zmienić folderu wyjściowego, m.in.</span><span class="sxs-lookup"><span data-stu-id="40dc3-317">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="40dc3-318">Aby uzyskać pełną listę, zobacz [pakietu odniesienie do polecenia](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-318">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="40dc3-319">Dostępne są następujące opcje: kilka są powszechne projektów programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="40dc3-319">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="40dc3-320">**Odwołanie do projektów**: Jeśli projekt odwołuje się do innych projektów, możesz dodać projektów występujących w odwołaniu jako część pakietu, lub zależności, za pomocą `-IncludeReferencedProjects` opcji:</span><span class="sxs-lookup"><span data-stu-id="40dc3-320">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="40dc3-321">Ten proces dołączania plików jest cykliczna, więc jeśli `MyProject.csproj` odwołań projektów B i C i projekty, odwołania D i E, F, a następnie pliki z B, C, D, E i f. znajdują się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-321">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="40dc3-322">Jeśli przywoływany projekt zawiera `.nuspec` plik własną, następnie NuGet dodaje przywoływanego projektu jako zależność zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="40dc3-322">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="40dc3-323">Należy w pakietach i publikowanie projektu oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-323">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="40dc3-324">**Konfiguracja kompilacji**: Domyślnie program NuGet używa domyślnej konfiguracji kompilacji, zwykle ustawić w pliku projektu *debugowania*.</span><span class="sxs-lookup"><span data-stu-id="40dc3-324">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="40dc3-325">Umieszczenie plików z konfiguracji różnych kompilacji, takie jak *wersji*, użyj `-properties` opcji konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="40dc3-325">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="40dc3-326">**Symbole**: aby uwzględnić symboli, które pozwala użytkownikom przejść przez kod pakietu w debugerze, należy użyć `-Symbols` opcji:</span><span class="sxs-lookup"><span data-stu-id="40dc3-326">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="40dc3-327">Testowanie instalacji pakietu aktualizacji</span><span class="sxs-lookup"><span data-stu-id="40dc3-327">Testing package installation</span></span>

<span data-ttu-id="40dc3-328">Przed opublikowaniem pakietu, zazwyczaj chcesz przetestować proces instalowania pakietu do projektu.</span><span class="sxs-lookup"><span data-stu-id="40dc3-328">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="40dc3-329">Testy, upewnij się, że zawsze pliki wszystkie znajdą się w ich w odpowiednim miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="40dc3-329">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="40dc3-330">Testowanie instalacji ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu normalnych [kroki instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="40dc3-330">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="40dc3-331">Potrzeby zautomatyzowanego testowania podstawowy proces jest następująca:</span><span class="sxs-lookup"><span data-stu-id="40dc3-331">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="40dc3-332">Kopiuj `.nupkg` plik do folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="40dc3-332">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="40dc3-333">Dodaj folder ze źródłami pakietów przy użyciu `nuget sources add -name <name> -source <path>` polecenia (zobacz [źródła nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="40dc3-333">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="40dc3-334">Należy pamiętać, że będą potrzebne tylko ustawić to źródło lokalne raz na dowolnym danym komputerze.</span><span class="sxs-lookup"><span data-stu-id="40dc3-334">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="40dc3-335">Zainstaluj pakiet z tego źródła za pomocą `nuget install <packageID> -source <name>` gdzie `<name>` jest zgodna z nazwą swojego źródła jako przydzielony do `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="40dc3-335">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="40dc3-336">Określanie źródła gwarantuje, że pakiet jest zainstalowany z tego samego źródła.</span><span class="sxs-lookup"><span data-stu-id="40dc3-336">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="40dc3-337">Sprawdź system plików, aby sprawdzić, czy pliki są poprawnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="40dc3-337">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40dc3-338">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40dc3-338">Next Steps</span></span>

<span data-ttu-id="40dc3-339">Po utworzeniu pakietu, który jest `.nupkg` pliku, można opublikować ją w Galerii wybranym zgodnie z opisem na [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="40dc3-339">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="40dc3-340">Możesz również chcieć rozszerzają możliwości pakietu lub w przeciwnym razie obsługuje inne scenariusze, zgodnie z opisem w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="40dc3-340">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="40dc3-341">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="40dc3-341">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="40dc3-342">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="40dc3-342">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="40dc3-343">Przekształceń źródła i plików konfiguracji</span><span class="sxs-lookup"><span data-stu-id="40dc3-343">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="40dc3-344">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="40dc3-344">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="40dc3-345">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="40dc3-345">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="40dc3-346">Ponadto istnieją typów dodatkowych pakietów, których trzeba pamiętać:</span><span class="sxs-lookup"><span data-stu-id="40dc3-346">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="40dc3-347">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="40dc3-347">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="40dc3-348">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="40dc3-348">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
