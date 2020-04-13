---
title: Tworzenie pakietu NuGet przy użyciu pliku wiersza polecenia nuget.exe
description: Szczegółowy przewodnik po procesie projektowania i tworzenia pakietu NuGet, w tym kluczowych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b3e6f0efc9e2e12de186ffd4ce29d496d07d5fc4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428948"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="e6b26-103">Tworzenie pakietu przy użyciu pliku wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e6b26-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="e6b26-104">Bez względu na to, co pakiet robi lub jaki kod zawiera, należy użyć jednego z narzędzi interfejsu wiersza polecenia, albo `nuget.exe` lub `dotnet.exe`, aby spakować tę funkcjonalność do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="e6b26-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="e6b26-105">Aby zainstalować narzędzia NuGet CLI, zobacz [Instalowanie narzędzi klienckich NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="e6b26-106">Należy zauważyć, że program Visual Studio nie zawiera automatycznie narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e6b26-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="e6b26-107">W przypadku projektów w stylu innych niż SDK, zazwyczaj .NET Framework projektów, wykonaj kroki opisane w tym artykule, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="e6b26-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="e6b26-108">Aby uzyskać instrukcje krok po kroku `nuget.exe` przy użyciu programu Visual Studio i interfejsu wiersza polecenia, zobacz [Tworzenie i publikowanie pakietu .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="e6b26-109">W przypadku projektów .NET Core i .NET Standard, które używają [formatu w stylu zestawu SDK,](../resources/check-project-format.md)oraz innych projektów w stylu zestawu SDK, zobacz [Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="e6b26-110">W przypadku projektów `packages.config` migrowanych z programu [PackageReference](../consume-packages/package-references-in-project-files.md)należy użyć [pliku msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="e6b26-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="e6b26-111">Technicznie rzecz biorąc pakiet NuGet to tylko plik ZIP, który `.nupkg` został przemianowany z rozszerzeniem i którego zawartość odpowiada niektórym konwencjom.</span><span class="sxs-lookup"><span data-stu-id="e6b26-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="e6b26-112">W tym temacie opisano szczegółowy proces tworzenia pakietu, który spełnia te konwencje.</span><span class="sxs-lookup"><span data-stu-id="e6b26-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="e6b26-113">Pakowanie rozpoczyna się od skompilowanego kodu (zestawów), symboli i/lub innych plików, które chcesz dostarczyć jako pakiet (zobacz [Omówienie i przepływ pracy](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="e6b26-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="e6b26-114">Ten proces jest niezależny od kompilowania lub w inny sposób generowania plików, które idą do pakietu, chociaż można rysować z informacji w pliku projektu, aby zachować skompilowane zestawy i pakiety w synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="e6b26-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="e6b26-115">W tym temacie stosuje się do projektów w stylu innych niż SDK, zazwyczaj projektów innych niż .NET Core i .NET Standard projektów przy użyciu programu Visual Studio 2017 i wyższych wersji i NuGet 4.0+.</span><span class="sxs-lookup"><span data-stu-id="e6b26-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="e6b26-116">Określanie, które zestawy mają być pakowane</span><span class="sxs-lookup"><span data-stu-id="e6b26-116">Decide which assemblies to package</span></span>

<span data-ttu-id="e6b26-117">Większość pakietów ogólnego przeznaczenia zawiera jeden lub więcej zestawów, które inni deweloperzy mogą używać w swoich własnych projektach.</span><span class="sxs-lookup"><span data-stu-id="e6b26-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="e6b26-118">Ogólnie rzecz biorąc najlepiej jest mieć jeden zestaw na pakiet NuGet, pod warunkiem, że każdy zestaw jest niezależnie przydatne.</span><span class="sxs-lookup"><span data-stu-id="e6b26-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="e6b26-119">Na przykład, jeśli `Utilities.dll` masz, `Parser.dll`który `Parser.dll` zależy od , i jest przydatny samodzielnie, a następnie utworzyć jeden pakiet dla każdego.</span><span class="sxs-lookup"><span data-stu-id="e6b26-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="e6b26-120">Pozwala to programistom `Parser.dll` na `Utilities.dll`korzystanie niezależnie od .</span><span class="sxs-lookup"><span data-stu-id="e6b26-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="e6b26-121">Jeśli biblioteka składa się z wielu zestawów, które nie są niezależnie przydatne, to dobrze jest połączyć je w jeden pakiet.</span><span class="sxs-lookup"><span data-stu-id="e6b26-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="e6b26-122">Przy użyciu poprzedniego `Parser.dll` przykładu, jeśli zawiera `Utilities.dll`kod, który jest używany `Parser.dll` tylko przez , to jest w porządku, aby zachować w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="e6b26-123">Podobnie, jeśli `Utilities.dll` zależy `Utilities.resources.dll`od , gdzie znowu ten ostatni nie jest przydatny sam, a następnie umieścić zarówno w tym samym opakowaniu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="e6b26-124">Zasoby są w istocie szczególnym przypadkiem.</span><span class="sxs-lookup"><span data-stu-id="e6b26-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="e6b26-125">Gdy pakiet jest zainstalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu dll pakietu, `.resources.dll` z *wyłączeniem* tych, które są nazwane, ponieważ są one uważane za zlokalizowane zestawy sateliczne (zobacz [Tworzenie zlokalizowanych pakietów](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="e6b26-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="e6b26-126">Z tego powodu `.resources.dll` należy unikać używania dla plików, które w przeciwnym razie zawierają kod pakietu istotne.</span><span class="sxs-lookup"><span data-stu-id="e6b26-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="e6b26-127">Jeśli biblioteka zawiera zestawy współdziałacze COM, postępuj zgodnie z dodatkowymi wskazówkami w [aplikacji Tworzenie pakietów z zestawami współdziałań COM.](author-packages-with-com-interop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="e6b26-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="e6b26-128">Rola i struktura pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="e6b26-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="e6b26-129">Gdy wiesz, jakie pliki chcesz spakować, następnym krokiem jest `.nuspec` utworzenie manifestu pakietu w pliku XML.</span><span class="sxs-lookup"><span data-stu-id="e6b26-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="e6b26-130">Manifest:</span><span class="sxs-lookup"><span data-stu-id="e6b26-130">The manifest:</span></span>

1. <span data-ttu-id="e6b26-131">Opisuje zawartość pakietu i sam znajduje się w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="e6b26-132">Dyski zarówno tworzenie pakietu i instruuje NuGet na jak zainstalować pakiet w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="e6b26-133">Na przykład manifest identyfikuje inne zależności pakietu, takie jak NuGet można również zainstalować te zależności, gdy pakiet główny jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="e6b26-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="e6b26-134">Zawiera właściwości wymagane i opcjonalne, jak opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e6b26-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="e6b26-135">Aby uzyskać dokładne informacje, w tym inne właściwości, o których nie wspomniano tutaj, zobacz [.nuspec reference](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="e6b26-136">Wymagane właściwości:</span><span class="sxs-lookup"><span data-stu-id="e6b26-136">Required properties:</span></span>

- <span data-ttu-id="e6b26-137">Identyfikator pakietu, który musi być unikatowy w galerii, która obsługuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="e6b26-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="e6b26-138">Określony numer wersji w postaci *Major.Minor.Patch[-Sufiks]* gdzie *-Suffix* identyfikuje [wersje przedpremierowe](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e6b26-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="e6b26-139">Tytuł pakietu, który powinien pojawić się na hoście (np. nuget.org)</span><span class="sxs-lookup"><span data-stu-id="e6b26-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="e6b26-140">Informacje o autorze i właścicielu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-140">Author and owner information.</span></span>
- <span data-ttu-id="e6b26-141">Długi opis paczki.</span><span class="sxs-lookup"><span data-stu-id="e6b26-141">A long description of the package.</span></span>

<span data-ttu-id="e6b26-142">Typowe właściwości opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="e6b26-142">Common optional properties:</span></span>

- <span data-ttu-id="e6b26-143">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="e6b26-143">Release notes</span></span>
- <span data-ttu-id="e6b26-144">Informacje o prawach autorskich</span><span class="sxs-lookup"><span data-stu-id="e6b26-144">Copyright information</span></span>
- <span data-ttu-id="e6b26-145">Krótki opis interfejsu [użytkownika Menedżera pakietów w programie Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="e6b26-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="e6b26-146">Identyfikator ustawień regionalnych</span><span class="sxs-lookup"><span data-stu-id="e6b26-146">A locale ID</span></span>
- <span data-ttu-id="e6b26-147">Adres URL projektu</span><span class="sxs-lookup"><span data-stu-id="e6b26-147">Project URL</span></span>
- <span data-ttu-id="e6b26-148">Licencja jako wyrażenie`licenseUrl` lub plik ( jest przestarzałe, użyj [ `license` elementu metadanych nuspec)](../reference/nuspec.md#license)</span><span class="sxs-lookup"><span data-stu-id="e6b26-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="e6b26-149">Ikona URL</span><span class="sxs-lookup"><span data-stu-id="e6b26-149">An icon URL</span></span>
- <span data-ttu-id="e6b26-150">Listy zależności i odwołań</span><span class="sxs-lookup"><span data-stu-id="e6b26-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="e6b26-151">Tagi ułatwiających wyszukiwanie w galerii</span><span class="sxs-lookup"><span data-stu-id="e6b26-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="e6b26-152">Poniżej znajduje się typowy (ale `.nuspec` fikcyjny) plik z komentarzami opisującymi właściwości:</span><span class="sxs-lookup"><span data-stu-id="e6b26-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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

<span data-ttu-id="e6b26-153">Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [packages.config](../reference/packages-config.md) i [Package versioning](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="e6b26-154">Jest również możliwe do powierzchni zasobów z zależności bezpośrednio w `include` `exclude` pakiecie przy `dependency` użyciu i atrybuty na element.</span><span class="sxs-lookup"><span data-stu-id="e6b26-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="e6b26-155">Zobacz [.nuspec Reference - Zależności](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="e6b26-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="e6b26-156">Ponieważ manifest znajduje się w pakiecie utworzonym z niego, można znaleźć dowolną liczbę dodatkowych przykładów, badając istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="e6b26-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="e6b26-157">Dobrym źródłem jest folder *pakietów globalnych* na komputerze, którego lokalizacja jest zwracana przez następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e6b26-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="e6b26-158">Przejdź do dowolnego *folderu package\version,* `.nupkg` skopiuj `.zip` plik do pliku, a następnie otwórz ten `.zip` plik i sprawdź w `.nuspec` nim.</span><span class="sxs-lookup"><span data-stu-id="e6b26-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="e6b26-159">Podczas tworzenia `.nuspec` z projektu Visual Studio manifest zawiera tokeny, które są zastępowane informacjami z projektu, gdy pakiet jest zbudowany.</span><span class="sxs-lookup"><span data-stu-id="e6b26-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="e6b26-160">Zobacz [Tworzenie nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="e6b26-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="e6b26-161">Tworzenie pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="e6b26-161">Create the .nuspec file</span></span>

<span data-ttu-id="e6b26-162">Tworzenie pełnego manifestu zazwyczaj rozpoczyna `.nuspec` się od pliku podstawowego wygenerowanego za pomocą jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="e6b26-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="e6b26-163">Katalog roboczy oparty na konwencji</span><span class="sxs-lookup"><span data-stu-id="e6b26-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="e6b26-164">Biblioteka DLL zespołu</span><span class="sxs-lookup"><span data-stu-id="e6b26-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="e6b26-165">Projekt programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e6b26-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="e6b26-166">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="e6b26-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="e6b26-167">Następnie edytuj plik ręcznie, tak aby opisywłaścił dokładną zawartość, którą chcesz w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="e6b26-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="e6b26-168">Wygenerowane `.nuspec` pliki zawierają symbole zastępcze, które muszą `nuget pack` zostać zmodyfikowane przed utworzeniem pakietu za pomocą polecenia.</span><span class="sxs-lookup"><span data-stu-id="e6b26-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="e6b26-169">To polecenie kończy `.nuspec` się niepowodzeniem, jeśli zawiera żadnych symboli zastępczych.</span><span class="sxs-lookup"><span data-stu-id="e6b26-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="e6b26-170">Z katalogu roboczego opartego na konwencji</span><span class="sxs-lookup"><span data-stu-id="e6b26-170">From a convention-based working directory</span></span>

<span data-ttu-id="e6b26-171">Ponieważ pakiet NuGet to tylko plik ZIP, który `.nupkg` został zmieniony z rozszerzeniem, często najłatwiej jest utworzyć odpowiednią strukturę folderów w lokalnym systemie plików, a następnie utworzyć `.nuspec` plik bezpośrednio z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="e6b26-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="e6b26-172">Następnie `nuget pack` polecenie automatycznie dodaje wszystkie pliki w tej strukturze folderów `.`(z wyłączeniem folderów, które zaczynają się od , co pozwala zachować prywatne pliki w tej samej strukturze).</span><span class="sxs-lookup"><span data-stu-id="e6b26-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="e6b26-173">Zaletą tego podejścia jest to, że nie trzeba określić w manifeście, które pliki mają zostać uwzględnione w pakiecie (jak wyjaśniono w dalszej części tego tematu).</span><span class="sxs-lookup"><span data-stu-id="e6b26-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="e6b26-174">Możesz po prostu mieć proces kompilacji produkcji dokładnej struktury folderu, który przechodzi do pakietu i można łatwo dołączyć inne pliki, które nie mogą być częścią projektu w przeciwnym razie:</span><span class="sxs-lookup"><span data-stu-id="e6b26-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="e6b26-175">Zawartość i kod źródłowy, które powinny być wstrzykiwane do projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="e6b26-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="e6b26-176">Skrypty środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6b26-176">PowerShell scripts</span></span>
- <span data-ttu-id="e6b26-177">Przekształcenia do istniejących plików konfiguracji i kodu źródłowego w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="e6b26-178">Konwencje folderów są następujące:</span><span class="sxs-lookup"><span data-stu-id="e6b26-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="e6b26-179">Folder</span><span class="sxs-lookup"><span data-stu-id="e6b26-179">Folder</span></span> | <span data-ttu-id="e6b26-180">Opis</span><span class="sxs-lookup"><span data-stu-id="e6b26-180">Description</span></span> | <span data-ttu-id="e6b26-181">Działanie po zainstalowaniu pakietu</span><span class="sxs-lookup"><span data-stu-id="e6b26-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e6b26-182">(korzeń)</span><span class="sxs-lookup"><span data-stu-id="e6b26-182">(root)</span></span> | <span data-ttu-id="e6b26-183">Lokalizacja dla readme.txt</span><span class="sxs-lookup"><span data-stu-id="e6b26-183">Location for readme.txt</span></span> | <span data-ttu-id="e6b26-184">Program Visual Studio wyświetla plik readme.txt w katalogu głównym pakietu po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="e6b26-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="e6b26-185">lib/{tfm}</span></span> | <span data-ttu-id="e6b26-186">Pliki`.dll`zestawu (`.xml`), dokumentacji`.pdb`( ) i symbolu ( ) dla danego monikera ram docelowych (TFM)</span><span class="sxs-lookup"><span data-stu-id="e6b26-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="e6b26-187">Zestawy są dodawane jako odwołania do kompilacji, a także środowiska wykonawczego; `.xml` i `.pdb` skopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="e6b26-188">Zobacz [Obsługa wielu struktur docelowych](supporting-multiple-target-frameworks.md) do tworzenia podfolderów specyficznych dla platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="e6b26-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="e6b26-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="e6b26-189">ref/{tfm}</span></span> | <span data-ttu-id="e6b26-190">Pliki`.dll`zestawu (`.pdb`) i symbol ( ) dla danego monikera ram docelowych (TFM)</span><span class="sxs-lookup"><span data-stu-id="e6b26-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="e6b26-191">Zestawy są dodawane jako odwołania tylko dla czasu kompilacji; Więc nic nie zostanie skopiowane do folderu bin projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="e6b26-192">środowiska wykonawcze</span><span class="sxs-lookup"><span data-stu-id="e6b26-192">runtimes</span></span> | <span data-ttu-id="e6b26-193">Pliki zestawu specyficznego dla architektury (`.dll`), symbolu (`.pdb`) i zasobów natywnych (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="e6b26-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="e6b26-194">Zestawy są dodawane jako odwołania tylko dla środowiska wykonawczego; inne pliki są kopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="e6b26-195">Zawsze powinien istnieć odpowiedni `AnyCPU` (TFM) `/ref/{tfm}` określonego zestawu w folderze, aby zapewnić odpowiedni zestaw czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="e6b26-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="e6b26-196">Zobacz [Obsługa wielu struktur docelowych](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="e6b26-197">content</span><span class="sxs-lookup"><span data-stu-id="e6b26-197">content</span></span> | <span data-ttu-id="e6b26-198">Dowolne pliki</span><span class="sxs-lookup"><span data-stu-id="e6b26-198">Arbitrary files</span></span> | <span data-ttu-id="e6b26-199">Zawartość jest kopiowana do katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-199">Contents are copied to the project root.</span></span> <span data-ttu-id="e6b26-200">Potraktowanie folderu **zawartości** jako katalogu głównego aplikacji docelowej, która ostatecznie zużywa pakiet.</span><span class="sxs-lookup"><span data-stu-id="e6b26-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="e6b26-201">Aby pakiet dodać obraz w folderze */images* aplikacji, umieść go w folderze *zawartości/obrazów* pakietu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="e6b26-202">kompilacja</span><span class="sxs-lookup"><span data-stu-id="e6b26-202">build</span></span> | <span data-ttu-id="e6b26-203">*(3,x+)* MSBuild `.targets` `.props` i pliki</span><span class="sxs-lookup"><span data-stu-id="e6b26-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="e6b26-204">Automatycznie wstawiany do projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="e6b26-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="e6b26-205">buildMultiTargeting</span></span> | <span data-ttu-id="e6b26-206">*(4,0+)* MSBuild `.targets` `.props` i pliki do kierowania krzyżowego</span><span class="sxs-lookup"><span data-stu-id="e6b26-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="e6b26-207">Automatycznie wstawiany do projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="e6b26-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="e6b26-208">buildTransitive</span></span> | <span data-ttu-id="e6b26-209">*(5,0+)* MSBuild `.targets` `.props` i pliki, które przepływają przechodnie do dowolnego projektu zużywającego.</span><span class="sxs-lookup"><span data-stu-id="e6b26-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="e6b26-210">Zobacz stronę [funkcji.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)</span><span class="sxs-lookup"><span data-stu-id="e6b26-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="e6b26-211">Automatycznie wstawiany do projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="e6b26-212">narzędzia</span><span class="sxs-lookup"><span data-stu-id="e6b26-212">tools</span></span> | <span data-ttu-id="e6b26-213">Skrypty i programy programu Powershell dostępne z konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="e6b26-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="e6b26-214">Folder `tools` jest dodawany `PATH` do zmiennej środowiskowej tylko dla konsoli `PATH` Menedżera pakietów (w szczególności *nie* do zestawu ustawionego dla MSBuild podczas tworzenia projektu).</span><span class="sxs-lookup"><span data-stu-id="e6b26-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="e6b26-215">Ponieważ struktura folderów może zawierać dowolną liczbę zestawów dla dowolnej liczby struktur docelowych, ta metoda jest konieczna podczas tworzenia pakietów, które obsługują wiele struktur.</span><span class="sxs-lookup"><span data-stu-id="e6b26-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="e6b26-216">W każdym razie po utworzeniu żądanej struktury folderów uruchom następujące polecenie `.nuspec` w tym folderze, aby utworzyć plik:</span><span class="sxs-lookup"><span data-stu-id="e6b26-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="e6b26-217">Ponownie wygenerowane `.nuspec` nie zawiera żadnych jawnych odwołań do plików w strukturze folderów.</span><span class="sxs-lookup"><span data-stu-id="e6b26-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="e6b26-218">NuGet automatycznie zawiera wszystkie pliki podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="e6b26-219">Nadal jednak trzeba edytować wartości zastępcze w innych częściach manifestu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="e6b26-220">Z biblioteki DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="e6b26-220">From an assembly DLL</span></span>

<span data-ttu-id="e6b26-221">W prostym przypadku tworzenia pakietu z zestawu, można `.nuspec` wygenerować plik z metadanych w zestawie za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e6b26-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="e6b26-222">Za pomocą tego formularza zastępuje kilka symboli zastępczych w manifeście z określonych wartości z zestawu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="e6b26-223">Na przykład `<id>` właściwość jest ustawiona na `<version>` nazwę zestawu i jest ustawiona na wersję zestawu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="e6b26-224">Inne właściwości w manifeście, jednak nie mają pasujące wartości w zestawie i w związku z tym nadal zawierają symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="e6b26-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="e6b26-225">Z projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e6b26-225">From a Visual Studio project</span></span>

<span data-ttu-id="e6b26-226">Tworzenie `.nuspec` z `.csproj` pliku `.vbproj` lub jest wygodne, ponieważ inne pakiety, które zostały zainstalowane w tym projekcie są automatycznie odwoływane jako zależności.</span><span class="sxs-lookup"><span data-stu-id="e6b26-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="e6b26-227">Wystarczy użyć następującego polecenia w tym samym folderze co plik projektu:</span><span class="sxs-lookup"><span data-stu-id="e6b26-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="e6b26-228">Wynikowy `<project-name>.nuspec` plik zawiera *tokeny,* które są zastępowane w czasie pakowania wartościami z projektu, w tym odwołaniami do innych pakietów, które zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="e6b26-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="e6b26-229">Jeśli masz zależności pakietu do uwzględnienia w *.nuspec*, zamiast użyć `nuget pack`, i uzyskać plik *nuspec* z poziomu wygenerowanego pliku *nupkg.*</span><span class="sxs-lookup"><span data-stu-id="e6b26-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="e6b26-230">Na przykład użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e6b26-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="e6b26-231">Token jest rozdzielany `$` symbolami po obu stronach właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="e6b26-232">Na przykład `<id>` wartość w manifeście wygenerowanym w ten sposób zazwyczaj pojawia się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e6b26-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="e6b26-233">Ten token jest `AssemblyName` zastępowany wartością z pliku projektu w czasie pakowania.</span><span class="sxs-lookup"><span data-stu-id="e6b26-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="e6b26-234">Aby uzyskać dokładne mapowanie `.nuspec` wartości projektu do tokenów, zobacz [odwołanie tokeny zastępcze](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="e6b26-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="e6b26-235">Tokeny zwalniają cię z konieczności aktualizacji kluczowych `.nuspec` wartości, takich jak numer wersji w podczas aktualizowania projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="e6b26-236">(Zawsze można zastąpić tokeny wartościami literału, w razie potrzeby).</span><span class="sxs-lookup"><span data-stu-id="e6b26-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="e6b26-237">Należy zauważyć, że istnieje kilka dodatkowych opcji pakowania dostępnych podczas pracy z projektu programu Visual Studio, zgodnie z opisem w [Running nuget pack do wygenerowania pliku nupkg](#run-nuget-pack-to-generate-the-nupkg-file) później.</span><span class="sxs-lookup"><span data-stu-id="e6b26-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="e6b26-238">Pakiety na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="e6b26-238">Solution-level packages</span></span>

<span data-ttu-id="e6b26-239">*Tylko nuGet 2.x. Niedostępne w nuget 3.0+.*</span><span class="sxs-lookup"><span data-stu-id="e6b26-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="e6b26-240">NuGet 2.x obsługiwane pojęcie pakietu na poziomie rozwiązania, który instaluje narzędzia lub dodatkowe polecenia `tools` dla Konsoli Menedżera pakietów (zawartość folderu), ale nie dodaje odwołania, zawartość lub budować dostosowania do żadnych projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="e6b26-241">Takie pakiety nie zawierają `lib` `content`żadnych `build` plików w jego bezpośrednim , lub foldery, `content`a `build` żadna z jego zależności nie ma plików w ich odpowiednich `lib`, lub folderów.</span><span class="sxs-lookup"><span data-stu-id="e6b26-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="e6b26-242">NuGet śledzi zainstalowane pakiety `packages.config` na poziomie `.nuget` rozwiązania w pliku w `packages.config` folderze, a nie w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="e6b26-243">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="e6b26-243">New file with default values</span></span>

<span data-ttu-id="e6b26-244">Następujące polecenie tworzy domyślny manifest z symbolami zastępczymi, który zapewnia rozpoczęcie od prawidłowej struktury pliku:</span><span class="sxs-lookup"><span data-stu-id="e6b26-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="e6b26-245">Jeśli pominiesz \<\>nazwę pakietu, wynikowy plik to `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e6b26-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="e6b26-246">Jeśli podasz nazwę, `Contoso.Utility.UsefulStuff`taką jak `Contoso.Utility.UsefulStuff.nuspec`, plik jest .</span><span class="sxs-lookup"><span data-stu-id="e6b26-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="e6b26-247">Wynikowy `.nuspec` zawiera symbole zastępcze `projectUrl`dla wartości, takich jak .</span><span class="sxs-lookup"><span data-stu-id="e6b26-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="e6b26-248">Przed użyciem go do utworzenia pliku `.nupkg` końcowego należy edytować plik.</span><span class="sxs-lookup"><span data-stu-id="e6b26-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="e6b26-249">Wybieranie unikatowego identyfikatora pakietu i ustawianie numeru wersji</span><span class="sxs-lookup"><span data-stu-id="e6b26-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="e6b26-250">Identyfikator pakietu (`<id>` element) i numer`<version>` wersji ( element) są dwie najważniejsze wartości w manifeście, ponieważ jednoznacznie identyfikują dokładny kod, który jest zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="e6b26-251">**Najważniejsze wskazówki dotyczące identyfikatora pakietu:**</span><span class="sxs-lookup"><span data-stu-id="e6b26-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="e6b26-252">**Unikatowość:** identyfikator musi być unikatowy w nuget.org lub dowolnej galerii hostuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="e6b26-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="e6b26-253">Przed podjęciem decyzji o identyfikatorze przeszukaj odpowiednią galerię, aby sprawdzić, czy nazwa jest już używana.</span><span class="sxs-lookup"><span data-stu-id="e6b26-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="e6b26-254">Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej `Contoso.`części identyfikatora, takiej jak .</span><span class="sxs-lookup"><span data-stu-id="e6b26-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="e6b26-255">Nazwy podobne do **przestrzeni nazw:** Postępuj zgodnie ze wzorcem podobnym do obszarów nazw w domenie .NET, używając notacji kropkowej zamiast łączników.</span><span class="sxs-lookup"><span data-stu-id="e6b26-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="e6b26-256">Na przykład `Contoso.Utility.UsefulStuff` użyj, `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`a nie lub .</span><span class="sxs-lookup"><span data-stu-id="e6b26-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="e6b26-257">Konsumenci również znaleźć przydatne, gdy identyfikator pakietu pasuje do obszarów nazw używanych w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="e6b26-258">**Przykładowe pakiety:** Jeśli tworzysz pakiet przykładowego kodu, który `.Sample` pokazuje, jak używać innego pakietu, `Contoso.Utility.UsefulStuff.Sample`dołącz jako sufiks do identyfikatora, jak w .</span><span class="sxs-lookup"><span data-stu-id="e6b26-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="e6b26-259">(Przykładowy pakiet będzie oczywiście zależny od innego pakietu.) Podczas tworzenia przykładowego pakietu należy użyć opisanej wcześniej metody katalogu roboczego opartego na konwencji.</span><span class="sxs-lookup"><span data-stu-id="e6b26-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="e6b26-260">W `content` folderze rozmieść przykładowy `\Samples\<identifier>` kod `\Samples\Contoso.Utility.UsefulStuff.Sample`w folderze o nazwie w pliku .</span><span class="sxs-lookup"><span data-stu-id="e6b26-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="e6b26-261">**Najważniejsze wskazówki dotyczące wersji pakietu:**</span><span class="sxs-lookup"><span data-stu-id="e6b26-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="e6b26-262">Ogólnie rzecz biorąc ustaw wersję pakietu, aby dopasować bibliotekę, chociaż nie jest to ściśle wymagane.</span><span class="sxs-lookup"><span data-stu-id="e6b26-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="e6b26-263">Jest to prosta sprawa, gdy ograniczysz pakiet do pojedynczego zestawu, jak opisano wcześniej w [podejmowaniu decyzji, które zestawy do spakowania](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="e6b26-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="e6b26-264">Ogólnie rzecz biorąc, należy pamiętać, że NuGet sam zajmuje się wersjami pakietów podczas rozpoznawania zależności, a nie wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="e6b26-265">Korzystając z niestandardowego schematu wersji, należy wziąć pod uwagę reguły wersji NuGet, jak wyjaśniono w [wersji pakietu.](../concepts/package-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="e6b26-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="e6b26-266">Poniższa seria krótkich wpisów na blogu są również pomocne w zrozumieniu przechowywania wersji:</span><span class="sxs-lookup"><span data-stu-id="e6b26-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="e6b26-267">Część 1: Biorąc na DLL Hell</span><span class="sxs-lookup"><span data-stu-id="e6b26-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="e6b26-268">Część 2: Podstawowy algorytm</span><span class="sxs-lookup"><span data-stu-id="e6b26-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="e6b26-269">Część 3: Ujednolicenie za pomocą przekierowań wiążących</span><span class="sxs-lookup"><span data-stu-id="e6b26-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="e6b26-270">Dodawanie pliku readme i innych plików</span><span class="sxs-lookup"><span data-stu-id="e6b26-270">Add a readme and other files</span></span>

<span data-ttu-id="e6b26-271">Aby bezpośrednio określić pliki do uwzględnienia `<files>` w pakiecie, `.nuspec` użyj węzła w pliku, który *następuje po* tagu: `<metadata>`</span><span class="sxs-lookup"><span data-stu-id="e6b26-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> <span data-ttu-id="e6b26-272">Korzystając z podejścia opartego na konwencji katalogu roboczego, można umieścić readme.txt `content` w katalogu głównym pakietu i innej zawartości w folderze.</span><span class="sxs-lookup"><span data-stu-id="e6b26-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="e6b26-273">W `<file>` manifeście nie są potrzebne żadne elementy.</span><span class="sxs-lookup"><span data-stu-id="e6b26-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="e6b26-274">Po dołączeniu pliku `readme.txt` o nazwie w katalogu głównym pakietu program Visual Studio wyświetla zawartość tego pliku jako zwykły tekst bezpośrednio po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e6b26-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="e6b26-275">(Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności).</span><span class="sxs-lookup"><span data-stu-id="e6b26-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="e6b26-276">Na przykład, oto jak readme dla pakietu HtmlAgilityPack pojawia się:</span><span class="sxs-lookup"><span data-stu-id="e6b26-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Wyświetlanie pliku readme dla pakietu NuGet po instalacji](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="e6b26-278">Jeśli dodasz `<files>` pusty węzeł `.nuspec` w pliku, NuGet nie zawiera żadnych innych treści w `lib` pakiecie innych niż to, co znajduje się w folderze.</span><span class="sxs-lookup"><span data-stu-id="e6b26-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="e6b26-279">Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie</span><span class="sxs-lookup"><span data-stu-id="e6b26-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="e6b26-280">W niektórych przypadkach można dodać niestandardowe obiekty docelowe kompilacji lub właściwości w projektach, które korzystają z pakietu, takich jak uruchamianie niestandardowego narzędzia lub procesu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="e6b26-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="e6b26-281">Można to zrobić, umieszczając `<package_id>.targets` pliki `<package_id>.props` w `Contoso.Utility.UsefulStuff.targets`formularzu `\build` lub (na przykład) w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="e6b26-282">Pliki w `\build` folderze głównym są uważane za odpowiednie dla wszystkich struktur docelowych.</span><span class="sxs-lookup"><span data-stu-id="e6b26-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="e6b26-283">Aby udostępnić pliki specyficzne dla struktury, należy je najpierw umieścić w odpowiednich podfolderach, takich jak:</span><span class="sxs-lookup"><span data-stu-id="e6b26-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="e6b26-284">Następnie w `.nuspec` pliku, należy odwołać się `<files>` do tych plików w węźle:</span><span class="sxs-lookup"><span data-stu-id="e6b26-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="e6b26-285">W tym MSBuild rekwizyty i obiekty docelowe w pakiecie został [wprowadzony z NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), dlatego zaleca się dodać `minClientVersion="2.5"` atrybut do `metadata` elementu, aby wskazać minimalną wersję klienta NuGet wymagane do korzystania z pakietu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="e6b26-286">Gdy NuGet instaluje `\build` pakiet z plikami, `<Import>` dodaje MSBuild elementów `.props` w pliku projektu wskazując i `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="e6b26-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="e6b26-287">(`.props` jest dodawany w górnej części pliku projektu; `.targets` dodaje się na dole).) Oddzielny warunkowy element MSBuild `<Import>` jest dodawany dla każdej struktury docelowej.</span><span class="sxs-lookup"><span data-stu-id="e6b26-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="e6b26-288">MSBuild `.props` `.targets` i pliki dla kierowania cross-framework `\buildMultiTargeting` mogą być umieszczane w folderze.</span><span class="sxs-lookup"><span data-stu-id="e6b26-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="e6b26-289">Podczas instalacji pakietu NuGet `<Import>` dodaje odpowiednie elementy do pliku projektu z warunkiem, że struktura docelowa nie jest ustawiona (właściwość `$(TargetFramework)` MSBuild musi być pusta).</span><span class="sxs-lookup"><span data-stu-id="e6b26-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="e6b26-290">W nuget 3.x cele nie są dodawane do projektu, ale zamiast tego są udostępniane za pośrednictwem `{projectName}.nuget.g.targets` i `{projectName}.nuget.g.props`.</span><span class="sxs-lookup"><span data-stu-id="e6b26-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="e6b26-291">Uruchom pakiet nuget, aby wygenerować plik nupkg</span><span class="sxs-lookup"><span data-stu-id="e6b26-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="e6b26-292">W przypadku używania zestawu lub katalogu roboczego opartego `nuget pack` na `.nuspec` konwencji `<project-name>` utwórz pakiet, uruchamiając plik, zastępując określoną nazwę pliku:</span><span class="sxs-lookup"><span data-stu-id="e6b26-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="e6b26-293">Podczas korzystania z projektu `nuget pack` programu Visual Studio, uruchom z pliku projektu, który automatycznie ładuje `.nuspec` plik projektu i zastępuje wszystkie tokeny w nim przy użyciu wartości w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="e6b26-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="e6b26-294">Korzystanie z pliku projektu bezpośrednio jest niezbędne do zastąpienia tokenu, ponieważ projekt jest źródłem wartości tokenu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="e6b26-295">Zastępowanie tokenu nie `nuget pack` ma `.nuspec` miejsca, jeśli używasz z plikiem.</span><span class="sxs-lookup"><span data-stu-id="e6b26-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="e6b26-296">We wszystkich `nuget pack` przypadkach nie obejmuje folderów rozpoczynających `.git` się `.hg`od kropki, takich jak lub .</span><span class="sxs-lookup"><span data-stu-id="e6b26-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="e6b26-297">NuGet wskazuje, jeśli istnieją błędy `.nuspec` w pliku, które wymagają poprawiania, takie jak zapominanie o zmianie wartości zastępczych w manifeście.</span><span class="sxs-lookup"><span data-stu-id="e6b26-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="e6b26-298">Po `nuget pack` pomyślnym, `.nupkg` masz plik, który można opublikować w odpowiedniej galerii, zgodnie z opisem w [Publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e6b26-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="e6b26-299">Pomocnym sposobem zbadania pakietu po jego utworzeniu jest otwarcie go w narzędziu [Eksplorator pakietów.](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)</span><span class="sxs-lookup"><span data-stu-id="e6b26-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="e6b26-300">Daje to graficzny widok zawartości pakietu i jego manifestu.</span><span class="sxs-lookup"><span data-stu-id="e6b26-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="e6b26-301">Można również zmienić nazwę `.nupkg` pliku `.zip` wynikowego na plik i eksplorować jego zawartość bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e6b26-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="e6b26-302">Opcje dodatkowe</span><span class="sxs-lookup"><span data-stu-id="e6b26-302">Additional options</span></span>

<span data-ttu-id="e6b26-303">Można użyć różnych przełączników wiersza polecenia, `nuget pack` aby wykluczyć pliki, zastąpić numer wersji w manifeście i zmienić folder wyjściowy, między innymi funkcje.</span><span class="sxs-lookup"><span data-stu-id="e6b26-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="e6b26-304">Pełna lista znajduje się w [1999 roku.](../reference/cli-reference/cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="e6b26-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="e6b26-305">Następujące opcje są kilka, które są wspólne z projektami programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e6b26-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="e6b26-306">**Projekty, do których istnieją odwołania:** Jeśli projekt odwołuje się do innych projektów, można dodać projekty, `-IncludeReferencedProjects` do których istnieje odwołanie, jako część pakietu lub jako zależności, za pomocą opcji:</span><span class="sxs-lookup"><span data-stu-id="e6b26-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="e6b26-307">Ten proces dołączania jest cykliczny, więc jeśli `MyProject.csproj` odwołania do projektów B i C, a te projekty odnoszą się do D, E i F, a następnie pliki z B, C, D, E i F są zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="e6b26-308">Jeśli projekt, do `.nuspec` którego istnieje odwołanie, zawiera własny plik, następnie NuGet dodaje, że odwołuje się do projektu jako zależność zamiast.</span><span class="sxs-lookup"><span data-stu-id="e6b26-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="e6b26-309">Należy spakować i opublikować ten projekt oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="e6b26-310">**Konfiguracja kompilacji:** Domyślnie NuGet używa domyślnej konfiguracji kompilacji ustawionej w pliku projektu, zazwyczaj *debugowania*.</span><span class="sxs-lookup"><span data-stu-id="e6b26-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="e6b26-311">Aby spakować pliki z innej konfiguracji kompilacji, takiej jak *Release*, użyj `-properties` opcji z konfiguracją:</span><span class="sxs-lookup"><span data-stu-id="e6b26-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="e6b26-312">**Symbole**: aby uwzględnić symbole, które umożliwiają konsumentom przechodzenie przez `-Symbols` kod pakietu w debugerze, użyj tej opcji:</span><span class="sxs-lookup"><span data-stu-id="e6b26-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="e6b26-313">Instalacja pakietu testowego</span><span class="sxs-lookup"><span data-stu-id="e6b26-313">Test package installation</span></span>

<span data-ttu-id="e6b26-314">Przed opublikowaniem pakietu zazwyczaj chcesz przetestować proces instalowania pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="e6b26-315">Testy upewnij się, że wszystkie pliki koniecznie kończy się w ich odpowiednich miejscach w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e6b26-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="e6b26-316">Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia, wykonując [normalne kroki instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="e6b26-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="e6b26-317">W przypadku automatycznych testów podstawowy proces jest następujący:</span><span class="sxs-lookup"><span data-stu-id="e6b26-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="e6b26-318">Skopiuj `.nupkg` plik do folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e6b26-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="e6b26-319">Dodaj folder do źródeł pakietu `nuget sources add -name <name> -source <path>` za pomocą polecenia (patrz [źródła nuget](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="e6b26-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="e6b26-320">Należy pamiętać, że to źródło lokalne należy ustawić tylko raz na danym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e6b26-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="e6b26-321">Zainstaluj pakiet z tego `nuget install <packageID> -source <name>` `<name>` źródła, używając miejsca, w `nuget sources`którym jest to zgodne z nazwą źródła, jak podano .</span><span class="sxs-lookup"><span data-stu-id="e6b26-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="e6b26-322">Określenie źródła zapewnia, że pakiet jest zainstalowany tylko z tego źródła.</span><span class="sxs-lookup"><span data-stu-id="e6b26-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="e6b26-323">Sprawdź system plików, aby sprawdzić, czy pliki są poprawnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="e6b26-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6b26-324">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6b26-324">Next Steps</span></span>

<span data-ttu-id="e6b26-325">Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w [polu Publikowanie pakietu.](../nuget-org/publish-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="e6b26-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="e6b26-326">Można również rozszerzyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze, jak opisano w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="e6b26-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="e6b26-327">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="e6b26-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="e6b26-328">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="e6b26-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e6b26-329">Przekształcenia plików źródłowych i konfiguracyjnych</span><span class="sxs-lookup"><span data-stu-id="e6b26-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="e6b26-330">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="e6b26-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="e6b26-331">Wersje w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="e6b26-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="e6b26-332">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="e6b26-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="e6b26-333">Tworzenie pakietów z zestawami współdziałań COM</span><span class="sxs-lookup"><span data-stu-id="e6b26-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="e6b26-334">Na koniec istnieją dodatkowe typy pakietów, o których należy pamiętać:</span><span class="sxs-lookup"><span data-stu-id="e6b26-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="e6b26-335">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="e6b26-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="e6b26-336">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="e6b26-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
