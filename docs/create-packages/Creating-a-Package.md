---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia NuGet. exe
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym najważniejszych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: e4223c25daa1c14c30de1ef063cd0f48df70c8b5
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564571"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="31f7d-103">Tworzenie pakietu przy użyciu interfejsu wiersza polecenia NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="31f7d-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="31f7d-104">Niezależnie od tego, co Twój pakiet lub jaki kod zawiera, użyj jednego z narzędzi `nuget.exe` interfejsu wiersza polecenia lub `dotnet.exe`, aby spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="31f7d-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="31f7d-105">Aby zainstalować narzędzia interfejsu wiersza polecenia NuGet, zobacz [Instalowanie narzędzi klienckich programu NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="31f7d-106">Należy pamiętać, że program Visual Studio nie zawiera automatycznie narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="31f7d-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="31f7d-107">W przypadku projektów typu non-SDK, zwykle .NET Framework projektów, wykonaj kroki opisane w tym artykule, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="31f7d-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="31f7d-108">Aby uzyskać instrukcje krok po kroku dotyczące korzystania z programu Visual Studio `nuget.exe` i interfejsu wiersza polecenia, zobacz [Tworzenie i publikowanie pakietu .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="31f7d-109">W przypadku projektów .NET Core i .NET Standard, które używają [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, zobacz [Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="31f7d-110">W przypadku projektów migrowanych z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md)Użyj programu [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="31f7d-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="31f7d-111">Mówiąc technicznie, pakiet NuGet jest tylko plikiem ZIP, którego nazwa została zmieniona z rozszerzeniem `.nupkg` i którego zawartość pasuje do określonych konwencji.</span><span class="sxs-lookup"><span data-stu-id="31f7d-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="31f7d-112">W tym temacie opisano szczegółowy proces tworzenia pakietu, który spełnia te konwencje.</span><span class="sxs-lookup"><span data-stu-id="31f7d-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="31f7d-113">Pakowanie rozpoczyna się od skompilowanego kodu (zestawów), symboli i/lub innych plików, które mają być dostarczane jako pakiet (zobacz [Omówienie i przepływ pracy](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="31f7d-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="31f7d-114">Ten proces jest niezależny od kompilacji lub w inny sposób wygenerowania plików, które przechodzą do pakietu, mimo że można rysować z informacji w pliku projektu, aby zachować synchronizację skompilowanych zestawów i pakietów.</span><span class="sxs-lookup"><span data-stu-id="31f7d-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="31f7d-115">Ten temat dotyczy projektów nie należących do zestawu SDK, zwykle projektów innych niż .NET Core i .NET Standard projektów przy użyciu programu Visual Studio 2017 i nowszych wersji oraz NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="31f7d-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="31f7d-116">Wybór zestawów do spakowania</span><span class="sxs-lookup"><span data-stu-id="31f7d-116">Decide which assemblies to package</span></span>

<span data-ttu-id="31f7d-117">Większość pakietów ogólnego przeznaczenia zawiera jeden lub więcej zestawów, które mogą być używane przez innych deweloperów w swoich projektach.</span><span class="sxs-lookup"><span data-stu-id="31f7d-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="31f7d-118">Ogólnie rzecz biorąc, najlepszym rozwiązaniem jest posiadanie jednego zestawu na pakiet NuGet, pod warunkiem, że każdy zestaw jest niezależnie przydatny.</span><span class="sxs-lookup"><span data-stu-id="31f7d-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="31f7d-119">Na przykład jeśli masz `Utilities.dll` , który jest zależny od `Parser.dll`, i `Parser.dll` jest używany samodzielnie, Utwórz jeden pakiet dla każdej z nich.</span><span class="sxs-lookup"><span data-stu-id="31f7d-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="31f7d-120">Dzięki temu deweloperzy mogą używać `Parser.dll` niezależnie od programu. `Utilities.dll`</span><span class="sxs-lookup"><span data-stu-id="31f7d-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="31f7d-121">Jeśli biblioteka składa się z wielu zestawów, które nie są niezależnie przydatne, warto połączyć je w jeden pakiet.</span><span class="sxs-lookup"><span data-stu-id="31f7d-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="31f7d-122">Korzystając z poprzedniego przykładu, `Parser.dll` jeśli zawiera kod, który jest używany `Utilities.dll`tylko przez, wówczas warto zachować `Parser.dll` w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="31f7d-123">Podobnie, jeśli `Utilities.dll` jest to zależne od `Utilities.resources.dll`, gdzie ponownie nie jest on używany, należy umieścić oba te elementy w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="31f7d-124">Zasoby są w rzeczywistości szczególnym przypadkiem.</span><span class="sxs-lookup"><span data-stu-id="31f7d-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="31f7d-125">Gdy pakiet jest instalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu do bibliotek DLL pakietu, *z wyjątkiem* tych, które są nazwane `.resources.dll` , ponieważ zakłada się, że są to zlokalizowane zespoły satelickie (zobacz [Tworzenie zlokalizowanych pakiety](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="31f7d-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="31f7d-126">Z tego powodu należy unikać używania `.resources.dll` dla plików, które w przeciwnym razie zawierają istotny kod pakietu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="31f7d-127">Jeśli biblioteka zawiera zestawy międzyoperacyjności modelu COM, postępuj zgodnie z dodatkowymi wskazówkami w temacie [Tworzenie pakietów z zestawami międzyoperacyjnymi com](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="31f7d-128">Rola i struktura pliku. nuspec</span><span class="sxs-lookup"><span data-stu-id="31f7d-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="31f7d-129">Po poznaniu plików do spakowania następnym krokiem jest utworzenie manifestu pakietu w `.nuspec` pliku XML.</span><span class="sxs-lookup"><span data-stu-id="31f7d-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="31f7d-130">Manifest:</span><span class="sxs-lookup"><span data-stu-id="31f7d-130">The manifest:</span></span>

1. <span data-ttu-id="31f7d-131">Opisuje zawartość pakietu i jest zawarta w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="31f7d-132">Dyski umożliwiają utworzenie pakietu i instruuje pakiet NuGet o sposobie instalacji pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="31f7d-133">Na przykład manifest identyfikuje inne zależności pakietu, aby pakiet NuGet mógł także zainstalować te zależności po zainstalowaniu pakietu głównego.</span><span class="sxs-lookup"><span data-stu-id="31f7d-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="31f7d-134">Zawiera właściwości wymagane i opcjonalne, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="31f7d-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="31f7d-135">Aby uzyskać dokładne informacje, w tym inne właściwości, które nie zostały wymienione w tym miejscu, zobacz [nuspec.](../reference/nuspec.md)</span><span class="sxs-lookup"><span data-stu-id="31f7d-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="31f7d-136">Wymagane właściwości:</span><span class="sxs-lookup"><span data-stu-id="31f7d-136">Required properties:</span></span>

- <span data-ttu-id="31f7d-137">Identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="31f7d-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="31f7d-138">Określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersje wstępne](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="31f7d-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="31f7d-139">Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)</span><span class="sxs-lookup"><span data-stu-id="31f7d-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="31f7d-140">Informacje o autorze i właścicielu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-140">Author and owner information.</span></span>
- <span data-ttu-id="31f7d-141">Długi opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-141">A long description of the package.</span></span>

<span data-ttu-id="31f7d-142">Wspólne właściwości opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="31f7d-142">Common optional properties:</span></span>

- <span data-ttu-id="31f7d-143">Uwagi do wersji</span><span class="sxs-lookup"><span data-stu-id="31f7d-143">Release notes</span></span>
- <span data-ttu-id="31f7d-144">Informacje o prawach autorskich</span><span class="sxs-lookup"><span data-stu-id="31f7d-144">Copyright information</span></span>
- <span data-ttu-id="31f7d-145">Krótki opis [interfejsu użytkownika Menedżera pakietów w programie Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="31f7d-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="31f7d-146">Identyfikator ustawień regionalnych</span><span class="sxs-lookup"><span data-stu-id="31f7d-146">A locale ID</span></span>
- <span data-ttu-id="31f7d-147">Adres URL projektu</span><span class="sxs-lookup"><span data-stu-id="31f7d-147">Project URL</span></span>
- <span data-ttu-id="31f7d-148">Licencja jako wyrażenie lub plik (`licenseUrl` jest przestarzały, [ `license` Użyj elementu metadanych nuspec](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="31f7d-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="31f7d-149">Adres URL ikony</span><span class="sxs-lookup"><span data-stu-id="31f7d-149">An icon URL</span></span>
- <span data-ttu-id="31f7d-150">Listy zależności i odwołań</span><span class="sxs-lookup"><span data-stu-id="31f7d-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="31f7d-151">Tagi pomocne w przeszukiwaniu galerii</span><span class="sxs-lookup"><span data-stu-id="31f7d-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="31f7d-152">Poniżej znajduje się typowy (ale fikcyjny) `.nuspec` plik z komentarzami opisującymi właściwości:</span><span class="sxs-lookup"><span data-stu-id="31f7d-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

<span data-ttu-id="31f7d-153">Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [Packages. config](../reference/packages-config.md) i [Versioning Package](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="31f7d-154">Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu `include` atrybutów `exclude` i dla `dependency` elementu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="31f7d-155">Zobacz [. nuspec — zależności](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="31f7d-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="31f7d-156">Ponieważ manifest jest zawarty w utworzonym przez niego pakiecie, można znaleźć dowolną liczbę dodatkowych przykładów, sprawdzając istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="31f7d-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="31f7d-157">Dobrym źródłem jest folder *Global-Packages* na komputerze, który jest zwracany przez następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="31f7d-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="31f7d-158">Przejdź do dowolnego *folderu package\version* `.nupkg` , skopiuj plik do `.zip` pliku, a `.nuspec` następnie otwórz ten `.zip` plik i przejrzyj go.</span><span class="sxs-lookup"><span data-stu-id="31f7d-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="31f7d-159">Podczas tworzenia `.nuspec` z projektu programu Visual Studio manifest zawiera tokeny, które są zastępowane informacjami z projektu podczas kompilowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="31f7d-160">Zobacz [Tworzenie nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="31f7d-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="31f7d-161">Utwórz plik. nuspec</span><span class="sxs-lookup"><span data-stu-id="31f7d-161">Create the .nuspec file</span></span>

<span data-ttu-id="31f7d-162">Tworzenie kompletnego manifestu zwykle zaczyna się od pliku `.nuspec` podstawowego wygenerowanego za pomocą jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="31f7d-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="31f7d-163">Katalog roboczy oparty na Konwencji</span><span class="sxs-lookup"><span data-stu-id="31f7d-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="31f7d-164">Biblioteka DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="31f7d-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="31f7d-165">Projekt programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31f7d-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="31f7d-166">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="31f7d-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="31f7d-167">Następnie możesz edytować plik ręcznie, tak aby opisuje dokładną zawartość, którą chcesz w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="31f7d-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="31f7d-168">Wygenerowane `.nuspec` pliki zawierają symbole zastępcze, które należy zmodyfikować przed utworzeniem pakietu `nuget pack` przy użyciu polecenia.</span><span class="sxs-lookup"><span data-stu-id="31f7d-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="31f7d-169">To polecenie kończy się niepowodzeniem, jeśli `.nuspec` zawiera symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="31f7d-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="31f7d-170">Z katalogu roboczego opartego na Konwencji</span><span class="sxs-lookup"><span data-stu-id="31f7d-170">From a convention-based working directory</span></span>

<span data-ttu-id="31f7d-171">Ponieważ pakiet NuGet jest tylko plikiem ZIP, którego nazwa została zmieniona przy użyciu `.nupkg` rozszerzenia, często najłatwiej jest utworzyć strukturę folderu w lokalnym systemie plików, a następnie `.nuspec` utworzyć plik bezpośrednio z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="31f7d-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="31f7d-172">Polecenie automatycznie dodaje wszystkie pliki w tej strukturze folderów (z wyjątkiem folderów, które `.`zaczynają się od, co pozwala na przechowywanie prywatnych plików w tej samej strukturze). `nuget pack`</span><span class="sxs-lookup"><span data-stu-id="31f7d-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="31f7d-173">Zaletą tego podejścia jest to, że nie trzeba określać w manifeście plików, które mają zostać uwzględnione w pakiecie (jak wyjaśniono w dalszej części tego tematu).</span><span class="sxs-lookup"><span data-stu-id="31f7d-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="31f7d-174">Możesz po prostu utworzyć proces kompilacji o dokładnej strukturze folderów, która znajduje się w pakiecie, i można łatwo dołączać inne pliki, które mogą nie być częścią projektu:</span><span class="sxs-lookup"><span data-stu-id="31f7d-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="31f7d-175">Zawartość i kod źródłowy, które powinny zostać dodane do projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="31f7d-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="31f7d-176">Skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="31f7d-176">PowerShell scripts</span></span>
- <span data-ttu-id="31f7d-177">Przekształca do istniejącej konfiguracji i plików kodu źródłowego w projekcie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="31f7d-178">Konwencje folderów są następujące:</span><span class="sxs-lookup"><span data-stu-id="31f7d-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="31f7d-179">Folder</span><span class="sxs-lookup"><span data-stu-id="31f7d-179">Folder</span></span> | <span data-ttu-id="31f7d-180">Opis</span><span class="sxs-lookup"><span data-stu-id="31f7d-180">Description</span></span> | <span data-ttu-id="31f7d-181">Akcja po zainstalowaniu pakietu</span><span class="sxs-lookup"><span data-stu-id="31f7d-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31f7d-182">pierwiastek</span><span class="sxs-lookup"><span data-stu-id="31f7d-182">(root)</span></span> | <span data-ttu-id="31f7d-183">Lokalizacja pliku Readme. txt</span><span class="sxs-lookup"><span data-stu-id="31f7d-183">Location for readme.txt</span></span> | <span data-ttu-id="31f7d-184">Program Visual Studio wyświetla plik Readme. txt w katalogu głównym pakietu po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="31f7d-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="31f7d-185">lib/{tfm}</span></span> | <span data-ttu-id="31f7d-186">Zestaw (`.dll`), dokumentacja (`.xml`) i pliki symboli (`.pdb`) dla danej monikera platformy docelowej (TFM)</span><span class="sxs-lookup"><span data-stu-id="31f7d-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="31f7d-187">Zestawy są dodawane jako odwołania do kompilowania, a także środowiska uruchomieniowego. `.xml` i`.pdb` skopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="31f7d-188">Zobacz [Obsługa wielu struktur docelowych](supporting-multiple-target-frameworks.md) na potrzeby tworzenia podfolderów specyficznych dla platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="31f7d-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="31f7d-189">ref/{TFM}</span><span class="sxs-lookup"><span data-stu-id="31f7d-189">ref/{tfm}</span></span> | <span data-ttu-id="31f7d-190">Zestaw (`.dll`) i pliki symboli (`.pdb`) dla danej monikera platformy docelowej (TFM)</span><span class="sxs-lookup"><span data-stu-id="31f7d-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="31f7d-191">Zestawy są dodawane jako odwołania tylko dla czasu kompilacji; Nic nie zostanie skopiowane do folderu bin projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="31f7d-192">Runtime</span><span class="sxs-lookup"><span data-stu-id="31f7d-192">runtimes</span></span> | <span data-ttu-id="31f7d-193">Zestaw specyficzny dla architektury`.dll`(), symbol`.pdb`() i pliki zasobów natywnych (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="31f7d-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="31f7d-194">Zestawy są dodawane jako odwołania tylko dla środowiska uruchomieniowego; inne pliki są kopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="31f7d-195">Zawsze powinien istnieć odpowiedni zestaw (TFM) `AnyCPU` określony w obszarze `/ref/{tfm}` folder, aby zapewnić odpowiedni zestaw czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="31f7d-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="31f7d-196">Zobacz [Obsługa wielu platform docelowych](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="31f7d-197">zawartość</span><span class="sxs-lookup"><span data-stu-id="31f7d-197">content</span></span> | <span data-ttu-id="31f7d-198">Dowolne pliki</span><span class="sxs-lookup"><span data-stu-id="31f7d-198">Arbitrary files</span></span> | <span data-ttu-id="31f7d-199">Zawartość jest kopiowana do katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-199">Contents are copied to the project root.</span></span> <span data-ttu-id="31f7d-200">Folder **zawartości** należy traktować jako katalog główny aplikacji docelowej, która ostatecznie zużywa pakiet.</span><span class="sxs-lookup"><span data-stu-id="31f7d-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="31f7d-201">Aby pakiet mógł dodać obraz w folderze */images* aplikacji, umieść go w folderze *content/images* pakietu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="31f7d-202">kompilacja</span><span class="sxs-lookup"><span data-stu-id="31f7d-202">build</span></span> | <span data-ttu-id="31f7d-203">*(3. x +)* MSBuild `.targets` i `.props` pliki</span><span class="sxs-lookup"><span data-stu-id="31f7d-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="31f7d-204">Automatycznie wstawione do projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="31f7d-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="31f7d-205">buildMultiTargeting</span></span> | <span data-ttu-id="31f7d-206">*(4.0 +)* Program `.targets` MSBuild `.props` i pliki dla celów międzyplatformowych</span><span class="sxs-lookup"><span data-stu-id="31f7d-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="31f7d-207">Automatycznie wstawione do projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="31f7d-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="31f7d-208">buildTransitive</span></span> | <span data-ttu-id="31f7d-209">*(5.0 +)* Program `.targets` MSBuild `.props` i pliki, które są przesyłane przechodniie do dowolnego, zużywanego projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="31f7d-210">Zobacz stronę [funkcji](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="31f7d-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="31f7d-211">Automatycznie wstawione do projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="31f7d-212">narzędzia</span><span class="sxs-lookup"><span data-stu-id="31f7d-212">tools</span></span> | <span data-ttu-id="31f7d-213">Skrypty i programy PowerShell dostępne z konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="31f7d-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="31f7d-214">Folder jest dodawany `PATH` do zmiennej środowiskowej tylko dla konsoli Menedżera pakietów ( `PATH` w odróżnieniu od ustawienia ustawionego dla programu MSBuild podczas kompilowania projektu). `tools`</span><span class="sxs-lookup"><span data-stu-id="31f7d-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="31f7d-215">Ponieważ struktura folderów może zawierać dowolną liczbę zestawów dla dowolnej liczby platform docelowych, ta metoda jest konieczna podczas tworzenia pakietów, które obsługują wiele platform.</span><span class="sxs-lookup"><span data-stu-id="31f7d-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="31f7d-216">W każdym przypadku, gdy masz pożądaną strukturę folderów, uruchom następujące polecenie w tym folderze, aby utworzyć `.nuspec` plik:</span><span class="sxs-lookup"><span data-stu-id="31f7d-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="31f7d-217">Ponownie wygenerowany `.nuspec` nie zawiera żadnych jawnych odwołań do plików w strukturze folderów.</span><span class="sxs-lookup"><span data-stu-id="31f7d-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="31f7d-218">Pakiet NuGet automatycznie uwzględnia wszystkie pliki podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="31f7d-219">Mimo to należy edytować wartości zastępcze w innych częściach manifestu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="31f7d-220">Z biblioteki DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="31f7d-220">From an assembly DLL</span></span>

<span data-ttu-id="31f7d-221">W prostym przypadku tworzenia pakietu z zestawu można wygenerować `.nuspec` plik z metadanych w zestawie przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="31f7d-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="31f7d-222">Użycie tego formularza zastępuje kilka symboli zastępczych w manifeście przy użyciu określonych wartości z zestawu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="31f7d-223">Na przykład `<id>` właściwość jest ustawiana na nazwę zestawu i `<version>` jest ustawiona na wersję zestawu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="31f7d-224">Inne właściwości w manifeście nie mają jednak pasujących wartości w zestawie i w ten sposób nadal zawierają symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="31f7d-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="31f7d-225">Z projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31f7d-225">From a Visual Studio project</span></span>

<span data-ttu-id="31f7d-226">Tworzenie pliku `.nuspec` `.csproj` z lub`.vbproj` jest wygodne, ponieważ inne pakiety, które zostały zainstalowane w projekcie, są automatycznie przywoływane jako zależności.</span><span class="sxs-lookup"><span data-stu-id="31f7d-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="31f7d-227">Po prostu Użyj następującego polecenia w tym samym folderze, w którym znajduje się plik projektu:</span><span class="sxs-lookup"><span data-stu-id="31f7d-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="31f7d-228">Utworzony `<project-name>.nuspec` plik zawiera *tokeny* , które są zastępowane w czasie pakowania z wartościami z projektu, w tym odwołaniami do innych pakietów, które zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="31f7d-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="31f7d-229">Jeśli masz zależności pakietu do uwzględnienia w *nuspec*, zamiast tego użyj `nuget pack`i Pobierz plik *. nuspec* z wygenerowanego pliku *. nupkg* .</span><span class="sxs-lookup"><span data-stu-id="31f7d-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="31f7d-230">Na przykład użyj poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="31f7d-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="31f7d-231">Token jest rozdzielany `$` symbolami po obu stronach właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="31f7d-232">Na przykład `<id>` wartość w manifeście wygenerowaną w ten sposób zwykle pojawia się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="31f7d-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="31f7d-233">Ten token jest zastępowany `AssemblyName` wartością z pliku projektu w czasie pakowania.</span><span class="sxs-lookup"><span data-stu-id="31f7d-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="31f7d-234">Aby uzyskać dokładne mapowanie wartości projektu na `.nuspec` tokeny, zobacz odwołanie do tokenów [zastępczych](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="31f7d-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="31f7d-235">Tokeny zwalniają z konieczności aktualizowania najważniejszych wartości, takich jak numer wersji w `.nuspec` trakcie aktualizacji projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="31f7d-236">(Można zawsze zastąpić tokeny wartościami literału, jeśli jest to wymagane).</span><span class="sxs-lookup"><span data-stu-id="31f7d-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="31f7d-237">Należy pamiętać, że podczas pracy z projektem programu Visual Studio jest dostępnych kilka dodatkowych opcji pakowania, zgodnie z opisem w artykule [uruchamianie pakietu NuGet w celu wygenerowania pliku. nupkg](#run-nuget-pack-to-generate-the-nupkg-file) w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="31f7d-238">Pakiety na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="31f7d-238">Solution-level packages</span></span>

<span data-ttu-id="31f7d-239">*Tylko pakiet NuGet 2. x. Niedostępne w programie NuGet 3.0 lub nowszym.*</span><span class="sxs-lookup"><span data-stu-id="31f7d-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="31f7d-240">Pakiet NuGet 2. x obsługuje pojęcie pakietu na poziomie rozwiązania, który instaluje narzędzia lub dodatkowe polecenia dla konsoli Menedżera pakietów (zawartość `tools` folderu), ale nie dodaje odwołań, zawartości ani dostosowań kompilacji do dowolnych projektów w Narzędzie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="31f7d-241">Takie pakiety nie zawierają plików w `lib`jego bezpośredniej `content`,, `build` ani folderach i żadna z jej zależności nie ma plików w odpowiednich `lib`folderach `content`,, `build` ani.</span><span class="sxs-lookup"><span data-stu-id="31f7d-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="31f7d-242">Pakiet NuGet śledzi zainstalowane pakiety na poziomie rozwiązania w `packages.config` pliku `.nuget` w folderze, `packages.config` a nie w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="31f7d-243">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="31f7d-243">New file with default values</span></span>

<span data-ttu-id="31f7d-244">Następujące polecenie tworzy manifest domyślny z symbolami zastępczymi, co zapewnia rozpoczęcie od właściwej struktury plików:</span><span class="sxs-lookup"><span data-stu-id="31f7d-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="31f7d-245">Jeśli pominięto \<nazwę\>pakietu, plik będzie `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="31f7d-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="31f7d-246">Jeśli podano nazwę, taką jak `Contoso.Utility.UsefulStuff`, plik jest. `Contoso.Utility.UsefulStuff.nuspec`</span><span class="sxs-lookup"><span data-stu-id="31f7d-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="31f7d-247">Wyniki `.nuspec` zawierają symbole zastępcze dla wartości, `projectUrl`takich jak.</span><span class="sxs-lookup"><span data-stu-id="31f7d-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="31f7d-248">Pamiętaj, aby edytować plik przed jego użyciem, aby utworzyć końcowy `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="31f7d-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="31f7d-249">Wybierz unikatowy identyfikator pakietu i ustaw numer wersji</span><span class="sxs-lookup"><span data-stu-id="31f7d-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="31f7d-250">Identyfikator pakietu (`<id>` element) i numer wersji (`<version>` element) to dwie najważniejsze wartości w manifeście, ponieważ jednoznacznie identyfikują dokładny kod zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="31f7d-251">**Najlepsze rozwiązania dotyczące identyfikatora pakietu:**</span><span class="sxs-lookup"><span data-stu-id="31f7d-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="31f7d-252">**Unikatowość**: Identyfikator musi być unikatowy w obrębie nuget.org lub dowolnej galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="31f7d-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="31f7d-253">Przed podjęciem decyzji o identyfikatorze Przeszukaj stosowną galerię, aby sprawdzić, czy nazwa jest już używana.</span><span class="sxs-lookup"><span data-stu-id="31f7d-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="31f7d-254">Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej części identyfikatora, na przykład `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="31f7d-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="31f7d-255">**Nazwy podobne do nazw**: Postępuj zgodnie ze wzorcem podobnym do przestrzeni nazw w programie .NET przy użyciu notacji kropkowej zamiast łączników.</span><span class="sxs-lookup"><span data-stu-id="31f7d-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="31f7d-256">Na przykład użyj `Contoso.Utility.UsefulStuff` `Contoso-Utility-UsefulStuff` zamiast lub `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="31f7d-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="31f7d-257">Konsumenci są również pomocne, gdy identyfikator pakietu jest zgodny z przestrzeniami nazw używanymi w kodzie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="31f7d-258">**Przykładowe pakiety**: Jeśli utworzysz pakiet przykładowego kodu, który pokazuje, jak używać innego pakietu, Dołącz `.Sample` jako sufiks do identyfikatora, jak w. `Contoso.Utility.UsefulStuff.Sample`</span><span class="sxs-lookup"><span data-stu-id="31f7d-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="31f7d-259">(Przykładowy pakiet jest oczywiście zależny od innego pakietu). Podczas tworzenia przykładowego pakietu Użyj metody katalogu roboczego opartej na Konwencji opisanej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="31f7d-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="31f7d-260">W folderze Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` w `\Samples\Contoso.Utility.UsefulStuff.Sample`. `content`</span><span class="sxs-lookup"><span data-stu-id="31f7d-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="31f7d-261">**Najlepsze rozwiązania dotyczące wersji pakietu:**</span><span class="sxs-lookup"><span data-stu-id="31f7d-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="31f7d-262">Ogólnie rzecz biorąc Ustaw wersję pakietu na zgodną z biblioteką, chociaż nie jest to wymagane absolutnie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="31f7d-263">Jest to prosta kwestia w przypadku ograniczenia pakietu do jednego zestawu, zgodnie z wcześniejszym opisem w [wyborze zestawów do spakowania](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="31f7d-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="31f7d-264">Ogólnie, pamiętaj, że sam pakiet NuGet zajmuje się wersjami pakietu podczas rozpoznawania zależności, a nie wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="31f7d-265">W przypadku korzystania ze schematu wersji niestandardowej należy wziąć pod uwagę reguły obsługi wersji NuGet zgodnie z opisem w temacie [wersja pakietu](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="31f7d-266">Poniższa seria krótkich wpisów w blogu pomaga również zrozumieć przechowywanie wersji:</span><span class="sxs-lookup"><span data-stu-id="31f7d-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="31f7d-267">Część 1. Pobieranie na Hell DLL</span><span class="sxs-lookup"><span data-stu-id="31f7d-267">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="31f7d-268">Część 2. Podstawowy algorytm</span><span class="sxs-lookup"><span data-stu-id="31f7d-268">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="31f7d-269">Część 3: Ujednolicenie za pomocą przekierowań powiązań</span><span class="sxs-lookup"><span data-stu-id="31f7d-269">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="31f7d-270">Dodaj plik Readme i inne pliki</span><span class="sxs-lookup"><span data-stu-id="31f7d-270">Add a readme and other files</span></span>

<span data-ttu-id="31f7d-271">Aby bezpośrednio określić pliki do dołączenia do pakietu, użyj `<files>` węzła `.nuspec` w pliku, który *następuje* po `<metadata>` tagu:</span><span class="sxs-lookup"><span data-stu-id="31f7d-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="31f7d-272">W przypadku korzystania z podejścia do katalogu roboczego opartego na konwencji można umieścić plik Readme. txt w katalogu głównym pakietu i w innej zawartości w `content` folderze.</span><span class="sxs-lookup"><span data-stu-id="31f7d-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="31f7d-273">W `<file>` manifeście nie są wymagane żadne elementy.</span><span class="sxs-lookup"><span data-stu-id="31f7d-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="31f7d-274">Po dołączeniu pliku o `readme.txt` nazwie w katalogu głównym pakietu program Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst bezpośrednio po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="31f7d-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="31f7d-275">(Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności).</span><span class="sxs-lookup"><span data-stu-id="31f7d-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="31f7d-276">Na przykład poniżej przedstawiono sposób wyświetlania pliku Readme dla pakietu HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="31f7d-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Wyświetlanie pliku Readme dla pakietu NuGet podczas instalacji](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="31f7d-278">W przypadku dołączenia `<files>` pustego węzła do `lib` pliku,pakietNuGetniezawierażadnejinnejzawartościpakietu`.nuspec` niż zawartość folderu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="31f7d-279">Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="31f7d-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="31f7d-280">W niektórych przypadkach może zajść potrzeba dodania niestandardowych elementów docelowych kompilacji lub właściwości w projektach korzystających z pakietu, takich jak uruchamianie niestandardowego narzędzia lub procesu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="31f7d-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="31f7d-281">W tym celu należy umieścić pliki w `<package_id>.targets` postaci lub `<package_id>.props` ( `\build` takie jak `Contoso.Utility.UsefulStuff.targets`) w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="31f7d-282">Pliki w folderze głównym `\build` są uważane za odpowiednie dla wszystkich platform docelowych.</span><span class="sxs-lookup"><span data-stu-id="31f7d-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="31f7d-283">Aby zapewnić pliki specyficzne dla struktury, należy najpierw umieścić je w odpowiednich podfolderach, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="31f7d-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="31f7d-284">Następnie w `.nuspec` pliku Pamiętaj o odwoływaniu się do tych plików `<files>` w węźle:</span><span class="sxs-lookup"><span data-stu-id="31f7d-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="31f7d-285">W tym, że w pakiecie [NuGet 2,5 wprowadzono](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files) `minClientVersion="2.5"` atrybuty i elementy docelowe programu MSBuild, dlatego zaleca się dodanie atrybutu do `metadata` elementu w celu wskazania minimalnej wersji klienta NuGet wymaganej do korzystania z pakietu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="31f7d-286">Gdy `\build` NuGet instaluje pakiet z plikami, dodaje elementy programu MSBuild `<Import>` w pliku `.targets` projektu wskazujące pliki i `.props` .</span><span class="sxs-lookup"><span data-stu-id="31f7d-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="31f7d-287">(`.props` zostanie dodany u góry pliku projektu; `.targets` zostanie dodany u dołu). Dla każdej platformy docelowej `<Import>` dodawany jest oddzielny warunkowy element programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="31f7d-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="31f7d-288">Program `.props` MSBuild `.targets` i pliki dla celów docelowych dla wielu platform `\buildMultiTargeting` można umieścić w folderze.</span><span class="sxs-lookup"><span data-stu-id="31f7d-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="31f7d-289">Podczas instalacji pakietu NuGet dodaje odpowiednie `<Import>` elementy do pliku projektu z warunkiem, że platforma docelowa nie jest ustawiona (Właściwość `$(TargetFramework)` programu MSBuild musi być pusta).</span><span class="sxs-lookup"><span data-stu-id="31f7d-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="31f7d-290">W przypadku programu NuGet 3. x elementy docelowe nie są dodawane do projektu, ale zamiast tego są `{projectName}.nuget.g.targets` udostępniane `{projectName}.nuget.g.props`za pomocą i.</span><span class="sxs-lookup"><span data-stu-id="31f7d-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="31f7d-291">Uruchom pakiet NuGet, aby wygenerować plik. nupkg</span><span class="sxs-lookup"><span data-stu-id="31f7d-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="31f7d-292">W przypadku korzystania `.nuspec` z zestawu lub katalogu roboczego opartego na Konwencji Utwórz pakiet, uruchamiając `nuget pack` plik, zastępując `<project-name>` go określoną nazwą pliku:</span><span class="sxs-lookup"><span data-stu-id="31f7d-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="31f7d-293">W przypadku korzystania z projektu programu Visual Studio `nuget pack` Uruchom polecenie z plikiem projektu, który automatycznie ładuje `.nuspec` plik projektu i zastępuje wszystkie tokeny w nim przy użyciu wartości w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="31f7d-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="31f7d-294">Użycie pliku projektu bezpośrednio jest niezbędne do zastąpienia tokenu, ponieważ jest to źródło wartości tokenu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="31f7d-295">Zastępowanie tokenu nie odbywa `nuget pack` `.nuspec` się w przypadku użycia z plikiem.</span><span class="sxs-lookup"><span data-stu-id="31f7d-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="31f7d-296">We wszystkich przypadkach `nuget pack` wyklucza foldery, które zaczynają się od kropki, takie `.git` jak `.hg`lub.</span><span class="sxs-lookup"><span data-stu-id="31f7d-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="31f7d-297">Pakiet NuGet wskazuje, czy w `.nuspec` pliku występują błędy, które wymagają skorygowania, na przykład zapominanie o zmianie wartości symboli zastępczych w manifeście.</span><span class="sxs-lookup"><span data-stu-id="31f7d-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="31f7d-298">Po `nuget pack` pomyślnym `.nupkg` wykonaniu tej procedury istnieje plik, który można opublikować w odpowiedniej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="31f7d-299">Przydatnym sposobem na badanie pakietu po jego utworzeniu jest otwarcie go w narzędziu [Eksplorator pakietów](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) .</span><span class="sxs-lookup"><span data-stu-id="31f7d-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="31f7d-300">Dzięki temu można wyświetlić graficzny widok zawartości pakietu i jego manifestu.</span><span class="sxs-lookup"><span data-stu-id="31f7d-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="31f7d-301">Możesz również zmienić nazwę wyniku `.nupkg` pliku `.zip` w pliku i zbadać jego zawartość bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="31f7d-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="31f7d-302">Opcje dodatkowe</span><span class="sxs-lookup"><span data-stu-id="31f7d-302">Additional options</span></span>

<span data-ttu-id="31f7d-303">W `nuget pack` celu wykluczania plików można użyć różnych przełączników wiersza polecenia, zastąpić numer wersji w manifeście i zmienić folder wyjściowy między innymi.</span><span class="sxs-lookup"><span data-stu-id="31f7d-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="31f7d-304">Pełną listę można znaleźć w [dokumentacji polecenia pakietu](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="31f7d-305">Poniżej wymieniono kilka opcji, które są wspólne dla projektów programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="31f7d-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="31f7d-306">**Przywoływane projekty**: Jeśli projekt odwołuje się do innych projektów, można dodać przywoływane projekty jako część pakietu lub jako zależności, korzystając z `-IncludeReferencedProjects` opcji:</span><span class="sxs-lookup"><span data-stu-id="31f7d-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="31f7d-307">Ten proces dołączania jest cykliczny `MyProject.csproj` , więc jeśli odwołuje się do projektów b i c, a te projekty odwołują się do D, E i f, wówczas pliki z B, C, D, E i f są zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="31f7d-308">Jeśli przywoływany projekt zawiera `.nuspec` własny plik, wówczas pakiet NuGet dodaje do projektu przywoływanego jako zależność.</span><span class="sxs-lookup"><span data-stu-id="31f7d-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="31f7d-309">Należy osobno spakować i opublikować ten projekt.</span><span class="sxs-lookup"><span data-stu-id="31f7d-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="31f7d-310">**Konfiguracja kompilacji**: Domyślnie NuGet używa domyślnego zestawu konfiguracji kompilacji w pliku projektu, zazwyczaj *Debuguj*.</span><span class="sxs-lookup"><span data-stu-id="31f7d-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="31f7d-311">Aby spakować pliki z innej konfiguracji kompilacji, takiej jak *wersja*, użyj `-properties` opcji z konfiguracją:</span><span class="sxs-lookup"><span data-stu-id="31f7d-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="31f7d-312">**Symbole**: Aby dołączyć symbole umożliwiające użytkownikom przechodzenie przez kod pakietu w debugerze, użyj `-Symbols` opcji:</span><span class="sxs-lookup"><span data-stu-id="31f7d-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="31f7d-313">Instalacja pakietu testowego</span><span class="sxs-lookup"><span data-stu-id="31f7d-313">Test package installation</span></span>

<span data-ttu-id="31f7d-314">Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="31f7d-315">Testy upewniają się, że wszystkie pliki, które się na bieżąco, kończą się w ich prawidłowym miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="31f7d-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="31f7d-316">Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="31f7d-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="31f7d-317">W przypadku zautomatyzowanych testów proces podstawowy jest następujący:</span><span class="sxs-lookup"><span data-stu-id="31f7d-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="31f7d-318">`.nupkg` Skopiuj plik do folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="31f7d-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="31f7d-319">Dodaj folder do źródeł pakietów przy użyciu `nuget sources add -name <name> -source <path>` polecenia (zobacz [źródła NuGet](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="31f7d-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="31f7d-320">Należy pamiętać, że to źródło lokalne należy ustawić tylko raz na danym komputerze.</span><span class="sxs-lookup"><span data-stu-id="31f7d-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="31f7d-321">Zainstaluj pakiet z tego źródła, używając `nuget install <packageID> -source <name>` gdzie `<name>` jest zgodny z nazwą źródła określoną dla `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="31f7d-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="31f7d-322">Określenie źródła gwarantuje, że pakiet jest instalowany wyłącznie z tego źródła.</span><span class="sxs-lookup"><span data-stu-id="31f7d-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="31f7d-323">Sprawdź system plików, aby sprawdzić, czy pliki są poprawnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="31f7d-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31f7d-324">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31f7d-324">Next Steps</span></span>

<span data-ttu-id="31f7d-325">Po utworzeniu pakietu, który jest `.nupkg` plikiem, można go opublikować w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="31f7d-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="31f7d-326">Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="31f7d-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="31f7d-327">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="31f7d-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="31f7d-328">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="31f7d-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="31f7d-329">Przekształcenia plików źródłowych i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="31f7d-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="31f7d-330">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="31f7d-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="31f7d-331">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="31f7d-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="31f7d-332">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="31f7d-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="31f7d-333">Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM</span><span class="sxs-lookup"><span data-stu-id="31f7d-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="31f7d-334">Na koniec należy pamiętać o dodatkowych typach pakietów:</span><span class="sxs-lookup"><span data-stu-id="31f7d-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="31f7d-335">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="31f7d-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="31f7d-336">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="31f7d-336">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
