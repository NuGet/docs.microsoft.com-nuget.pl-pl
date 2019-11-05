---
title: Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia NuGet. exe
description: Szczegółowy przewodnik dotyczący procesu projektowania i tworzenia pakietu NuGet, w tym najważniejszych punktów decyzyjnych, takich jak pliki i przechowywanie wersji.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 12ecfb8374c43a04d57d32575556adebc991d053
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610703"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="b9c2c-103">Tworzenie pakietu przy użyciu interfejsu wiersza polecenia NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="b9c2c-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="b9c2c-104">Niezależnie od tego, co Twój pakiet lub jaki kod zawiera, użyj jednego z narzędzi interfejsu wiersza polecenia, `nuget.exe` lub `dotnet.exe`, aby spakować tę funkcję do składnika, który może być współużytkowany i używany przez dowolną liczbę innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="b9c2c-105">Aby zainstalować narzędzia interfejsu wiersza polecenia NuGet, zobacz [Instalowanie narzędzi klienckich programu NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="b9c2c-106">Należy pamiętać, że program Visual Studio nie zawiera automatycznie narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="b9c2c-107">W przypadku projektów typu non-SDK, zwykle .NET Framework projektów, wykonaj kroki opisane w tym artykule, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="b9c2c-108">Instrukcje krok po kroku dotyczące korzystania z programu Visual Studio i interfejsu wiersza polecenia `nuget.exe` można znaleźć w temacie [Tworzenie i publikowanie pakietu .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="b9c2c-109">W przypadku projektów .NET Core i .NET Standard, które używają [formatu zestawu SDK](../resources/check-project-format.md)i innych projektów w stylu zestawu SDK, zobacz [Tworzenie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="b9c2c-110">W przypadku projektów migrowanych z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md)Użyj programu [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="b9c2c-111">Mówiąc technicznie, pakiet NuGet jest tylko plikiem ZIP, którego nazwa została zmieniona z rozszerzeniem `.nupkg` i którego zawartość pasuje do określonych konwencji.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="b9c2c-112">W tym temacie opisano szczegółowy proces tworzenia pakietu, który spełnia te konwencje.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="b9c2c-113">Pakowanie rozpoczyna się od skompilowanego kodu (zestawów), symboli i/lub innych plików, które mają być dostarczane jako pakiet (zobacz [Omówienie i przepływ pracy](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="b9c2c-114">Ten proces jest niezależny od kompilacji lub w inny sposób wygenerowania plików, które przechodzą do pakietu, mimo że można rysować z informacji w pliku projektu, aby zachować synchronizację skompilowanych zestawów i pakietów.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="b9c2c-115">Ten temat dotyczy projektów nie należących do zestawu SDK, zwykle projektów innych niż .NET Core i .NET Standard projektów przy użyciu programu Visual Studio 2017 i nowszych wersji oraz NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="b9c2c-116">Wybór zestawów do spakowania</span><span class="sxs-lookup"><span data-stu-id="b9c2c-116">Decide which assemblies to package</span></span>

<span data-ttu-id="b9c2c-117">Większość pakietów ogólnego przeznaczenia zawiera jeden lub więcej zestawów, które mogą być używane przez innych deweloperów w swoich projektach.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="b9c2c-118">Ogólnie rzecz biorąc, najlepszym rozwiązaniem jest posiadanie jednego zestawu na pakiet NuGet, pod warunkiem, że każdy zestaw jest niezależnie przydatny.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="b9c2c-119">Na przykład jeśli masz `Utilities.dll`, która zależy od `Parser.dll`, a `Parser.dll` jest przydatna, Utwórz jeden pakiet dla każdej z nich.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="b9c2c-120">Dzięki temu deweloperzy mogą używać `Parser.dll` niezależnie od `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="b9c2c-121">Jeśli biblioteka składa się z wielu zestawów, które nie są niezależnie przydatne, warto połączyć je w jeden pakiet.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="b9c2c-122">Korzystając z poprzedniego przykładu, jeśli `Parser.dll` zawiera kod, który jest używany tylko przez `Utilities.dll`, warto zachować `Parser.dll` w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="b9c2c-123">Podobnie, jeśli `Utilities.dll` zależy od `Utilities.resources.dll`, gdzie jeszcze nie jest on używany, należy umieścić oba te elementy w tym samym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="b9c2c-124">Zasoby są w rzeczywistości szczególnym przypadkiem.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="b9c2c-125">Gdy pakiet jest instalowany w projekcie, NuGet automatycznie dodaje odwołania do zestawu do bibliotek DLL pakietu, *z wyłączeniem* tych, które mają nazwę `.resources.dll`, ponieważ zakłada się, że są to zlokalizowane zestawy satelickie (zobacz [Tworzenie zlokalizowanych pakietów ](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="b9c2c-126">Z tego powodu należy unikać używania `.resources.dll` w przypadku plików, które w przeciwnym razie zawierają istotny kod pakietu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="b9c2c-127">Jeśli biblioteka zawiera zestawy międzyoperacyjności modelu COM, postępuj zgodnie z dodatkowymi wskazówkami w temacie [Tworzenie pakietów z zestawami międzyoperacyjnymi com](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="b9c2c-128">Rola i struktura pliku. nuspec</span><span class="sxs-lookup"><span data-stu-id="b9c2c-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="b9c2c-129">Po poznaniu plików, które chcesz spakować, następnym krokiem jest utworzenie manifestu pakietu w pliku XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="b9c2c-130">Manifest:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-130">The manifest:</span></span>

1. <span data-ttu-id="b9c2c-131">Opisuje zawartość pakietu i jest zawarta w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="b9c2c-132">Dyski umożliwiają utworzenie pakietu i instruuje pakiet NuGet o sposobie instalacji pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="b9c2c-133">Na przykład manifest identyfikuje inne zależności pakietu, aby pakiet NuGet mógł także zainstalować te zależności po zainstalowaniu pakietu głównego.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="b9c2c-134">Zawiera właściwości wymagane i opcjonalne, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="b9c2c-135">Aby uzyskać dokładne informacje, w tym inne właściwości, które nie zostały wymienione w tym miejscu, zobacz [nuspec.](../reference/nuspec.md)</span><span class="sxs-lookup"><span data-stu-id="b9c2c-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="b9c2c-136">Wymagane właściwości:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-136">Required properties:</span></span>

- <span data-ttu-id="b9c2c-137">Identyfikator pakietu, który musi być unikatowy w galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="b9c2c-138">Określony numer wersji w postaci *główna. pomocnicza. poprawka [-sufiks]* , gdzie *-sufiks* określa [wersje wstępne](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="b9c2c-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="b9c2c-139">Tytuł pakietu, który powinien pojawić się na hoście (na przykład nuget.org)</span><span class="sxs-lookup"><span data-stu-id="b9c2c-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="b9c2c-140">Informacje o autorze i właścicielu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-140">Author and owner information.</span></span>
- <span data-ttu-id="b9c2c-141">Długi opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-141">A long description of the package.</span></span>

<span data-ttu-id="b9c2c-142">Wspólne właściwości opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-142">Common optional properties:</span></span>

- <span data-ttu-id="b9c2c-143">Uwagi do wersji</span><span class="sxs-lookup"><span data-stu-id="b9c2c-143">Release notes</span></span>
- <span data-ttu-id="b9c2c-144">Informacje o prawach autorskich</span><span class="sxs-lookup"><span data-stu-id="b9c2c-144">Copyright information</span></span>
- <span data-ttu-id="b9c2c-145">Krótki opis [interfejsu użytkownika Menedżera pakietów w programie Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="b9c2c-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="b9c2c-146">Identyfikator ustawień regionalnych</span><span class="sxs-lookup"><span data-stu-id="b9c2c-146">A locale ID</span></span>
- <span data-ttu-id="b9c2c-147">Adres URL projektu</span><span class="sxs-lookup"><span data-stu-id="b9c2c-147">Project URL</span></span>
- <span data-ttu-id="b9c2c-148">Licencja jako wyrażenie lub plik (`licenseUrl` jest przestarzały, użyj [elementu metadanych nuspec `license`](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="b9c2c-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="b9c2c-149">Adres URL ikony</span><span class="sxs-lookup"><span data-stu-id="b9c2c-149">An icon URL</span></span>
- <span data-ttu-id="b9c2c-150">Listy zależności i odwołań</span><span class="sxs-lookup"><span data-stu-id="b9c2c-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="b9c2c-151">Tagi pomocne w przeszukiwaniu galerii</span><span class="sxs-lookup"><span data-stu-id="b9c2c-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="b9c2c-152">Poniżej znajduje się typowy (ale fikcyjny) plik `.nuspec` z komentarzami opisującymi właściwości:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

<span data-ttu-id="b9c2c-153">Aby uzyskać szczegółowe informacje na temat deklarowania zależności i określania numerów wersji, zobacz [Packages. config](../reference/packages-config.md) i [Versioning Package](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="b9c2c-154">Istnieje również możliwość, że zasoby są zależne od zależności bezpośrednio w pakiecie przy użyciu atrybutów `include` i `exclude` w elemencie `dependency`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="b9c2c-155">Zobacz [. nuspec — zależności](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="b9c2c-156">Ponieważ manifest jest zawarty w utworzonym przez niego pakiecie, można znaleźć dowolną liczbę dodatkowych przykładów, sprawdzając istniejące pakiety.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="b9c2c-157">Dobrym źródłem jest folder *Global-Packages* na komputerze, który jest zwracany przez następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="b9c2c-158">Przejdź do dowolnego folderu *package\version* , skopiuj plik `.nupkg` do pliku `.zip`, a następnie otwórz ten plik `.zip` i Przeanalizuj w nim `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="b9c2c-159">W przypadku tworzenia `.nuspec` z projektu programu Visual Studio manifest zawiera tokeny, które są zastępowane informacjami z projektu podczas kompilowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="b9c2c-160">Zobacz [Tworzenie nuspec z projektu programu Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="b9c2c-161">Utwórz plik. nuspec</span><span class="sxs-lookup"><span data-stu-id="b9c2c-161">Create the .nuspec file</span></span>

<span data-ttu-id="b9c2c-162">Tworzenie kompletnego manifestu zwykle zaczyna się od podstawowego pliku `.nuspec` wygenerowanego za pomocą jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="b9c2c-163">Katalog roboczy oparty na Konwencji</span><span class="sxs-lookup"><span data-stu-id="b9c2c-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="b9c2c-164">Biblioteka DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="b9c2c-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="b9c2c-165">Projekt programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9c2c-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="b9c2c-166">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="b9c2c-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="b9c2c-167">Następnie możesz edytować plik ręcznie, tak aby opisuje dokładną zawartość, którą chcesz w pakiecie końcowym.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="b9c2c-168">Wygenerowane pliki `.nuspec` zawierają symbole zastępcze, które należy zmodyfikować przed utworzeniem pakietu przy użyciu polecenia `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="b9c2c-169">To polecenie kończy się niepowodzeniem, jeśli `.nuspec` zawiera symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="b9c2c-170">Z katalogu roboczego opartego na Konwencji</span><span class="sxs-lookup"><span data-stu-id="b9c2c-170">From a convention-based working directory</span></span>

<span data-ttu-id="b9c2c-171">Ponieważ pakiet NuGet jest tylko plikiem ZIP, którego nazwa została zmieniona przy użyciu rozszerzenia `.nupkg`, często najłatwiej jest utworzyć strukturę folderu w lokalnym systemie plików, a następnie utworzyć plik `.nuspec` bezpośrednio z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="b9c2c-172">Polecenie `nuget pack` automatycznie dodaje wszystkie pliki w tej strukturze folderów (z wyjątkiem folderów, które zaczynają się od `.`, co pozwala na przechowywanie plików prywatnych w tej samej strukturze).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="b9c2c-173">Zaletą tego podejścia jest to, że nie trzeba określać w manifeście plików, które mają zostać uwzględnione w pakiecie (jak wyjaśniono w dalszej części tego tematu).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="b9c2c-174">Możesz po prostu utworzyć proces kompilacji o dokładnej strukturze folderów, która znajduje się w pakiecie, i można łatwo dołączać inne pliki, które mogą nie być częścią projektu:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="b9c2c-175">Zawartość i kod źródłowy, które powinny zostać dodane do projektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="b9c2c-176">Skrypty programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9c2c-176">PowerShell scripts</span></span>
- <span data-ttu-id="b9c2c-177">Przekształca do istniejącej konfiguracji i plików kodu źródłowego w projekcie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="b9c2c-178">Konwencje folderów są następujące:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="b9c2c-179">Folder</span><span class="sxs-lookup"><span data-stu-id="b9c2c-179">Folder</span></span> | <span data-ttu-id="b9c2c-180">Opis</span><span class="sxs-lookup"><span data-stu-id="b9c2c-180">Description</span></span> | <span data-ttu-id="b9c2c-181">Akcja po zainstalowaniu pakietu</span><span class="sxs-lookup"><span data-stu-id="b9c2c-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9c2c-182">pierwiastek</span><span class="sxs-lookup"><span data-stu-id="b9c2c-182">(root)</span></span> | <span data-ttu-id="b9c2c-183">Lokalizacja pliku Readme. txt</span><span class="sxs-lookup"><span data-stu-id="b9c2c-183">Location for readme.txt</span></span> | <span data-ttu-id="b9c2c-184">Program Visual Studio wyświetla plik Readme. txt w katalogu głównym pakietu po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="b9c2c-185">lib/{TFM}</span><span class="sxs-lookup"><span data-stu-id="b9c2c-185">lib/{tfm}</span></span> | <span data-ttu-id="b9c2c-186">Zestaw (`.dll`), dokumentacja (`.xml`) i pliki symboli (`.pdb`) dla danej monikera platformy docelowej (TFM)</span><span class="sxs-lookup"><span data-stu-id="b9c2c-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="b9c2c-187">Zestawy są dodawane jako odwołania do kompilowania, a także środowiska uruchomieniowego. `.xml` i `.pdb` skopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="b9c2c-188">Zobacz [Obsługa wielu struktur docelowych](supporting-multiple-target-frameworks.md) na potrzeby tworzenia podfolderów specyficznych dla platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="b9c2c-189">ref/{TFM}</span><span class="sxs-lookup"><span data-stu-id="b9c2c-189">ref/{tfm}</span></span> | <span data-ttu-id="b9c2c-190">Zestaw (`.dll`) i pliki symboli (`.pdb`) dla danej monikera platformy docelowej (TFM)</span><span class="sxs-lookup"><span data-stu-id="b9c2c-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="b9c2c-191">Zestawy są dodawane jako odwołania tylko dla czasu kompilacji; Nic nie zostanie skopiowane do folderu bin projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="b9c2c-192">Runtime</span><span class="sxs-lookup"><span data-stu-id="b9c2c-192">runtimes</span></span> | <span data-ttu-id="b9c2c-193">Zestaw specyficzny dla architektury (`.dll`), symbol (`.pdb`) i pliki zasobów natywnych (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="b9c2c-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="b9c2c-194">Zestawy są dodawane jako odwołania tylko dla środowiska uruchomieniowego; inne pliki są kopiowane do folderów projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="b9c2c-195">Zawsze powinien istnieć odpowiedni zestaw (TFM) `AnyCPU` specyficzny dla elementu w folderze `/ref/{tfm}`, aby zapewnić odpowiedni zestaw czasu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="b9c2c-196">Zobacz [Obsługa wielu platform docelowych](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="b9c2c-197">zawartość</span><span class="sxs-lookup"><span data-stu-id="b9c2c-197">content</span></span> | <span data-ttu-id="b9c2c-198">Dowolne pliki</span><span class="sxs-lookup"><span data-stu-id="b9c2c-198">Arbitrary files</span></span> | <span data-ttu-id="b9c2c-199">Zawartość jest kopiowana do katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-199">Contents are copied to the project root.</span></span> <span data-ttu-id="b9c2c-200">Folder **zawartości** należy traktować jako katalog główny aplikacji docelowej, która ostatecznie zużywa pakiet.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="b9c2c-201">Aby pakiet mógł dodać obraz w folderze */images* aplikacji, umieść go w folderze *content/images* pakietu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="b9c2c-202">kompilacja</span><span class="sxs-lookup"><span data-stu-id="b9c2c-202">build</span></span> | <span data-ttu-id="b9c2c-203">*(3. x +)* MSBuild `.targets` i `.props` plików</span><span class="sxs-lookup"><span data-stu-id="b9c2c-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="b9c2c-204">Automatycznie wstawione do projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="b9c2c-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="b9c2c-205">buildMultiTargeting</span></span> | <span data-ttu-id="b9c2c-206">*(4.0 +)* Pliki programu MSBuild `.targets` i `.props` dla elementów docelowych dla wielu platform</span><span class="sxs-lookup"><span data-stu-id="b9c2c-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="b9c2c-207">Automatycznie wstawione do projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="b9c2c-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="b9c2c-208">buildTransitive</span></span> | <span data-ttu-id="b9c2c-209">*(5.0 +)* Pliki programu MSBuild `.targets` i `.props`, które są przesyłane przechodniie do dowolnego, zużywanego projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="b9c2c-210">Zobacz stronę [funkcji](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="b9c2c-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="b9c2c-211">Automatycznie wstawione do projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="b9c2c-212">narzędzia</span><span class="sxs-lookup"><span data-stu-id="b9c2c-212">tools</span></span> | <span data-ttu-id="b9c2c-213">Skrypty i programy PowerShell dostępne z konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="b9c2c-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="b9c2c-214">Folder `tools` jest dodawany do zmiennej środowiskowej `PATH` tylko dla konsoli Menedżera pakietów (w *odróżnieniu* od `PATH` jako zestawu MSBuild podczas kompilowania projektu).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="b9c2c-215">Ponieważ struktura folderów może zawierać dowolną liczbę zestawów dla dowolnej liczby platform docelowych, ta metoda jest konieczna podczas tworzenia pakietów, które obsługują wiele platform.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="b9c2c-216">W każdym przypadku, gdy masz pożądaną strukturę folderów, uruchom następujące polecenie w tym folderze, aby utworzyć plik `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="b9c2c-217">Ponownie wygenerowany `.nuspec` nie zawiera żadnych jawnych odwołań do plików w strukturze folderów.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="b9c2c-218">Pakiet NuGet automatycznie uwzględnia wszystkie pliki podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="b9c2c-219">Mimo to należy edytować wartości zastępcze w innych częściach manifestu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="b9c2c-220">Z biblioteki DLL zestawu</span><span class="sxs-lookup"><span data-stu-id="b9c2c-220">From an assembly DLL</span></span>

<span data-ttu-id="b9c2c-221">W prostym przypadku tworzenia pakietu z zestawu można wygenerować plik `.nuspec` z metadanych w zestawie przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="b9c2c-222">Użycie tego formularza zastępuje kilka symboli zastępczych w manifeście przy użyciu określonych wartości z zestawu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="b9c2c-223">Na przykład właściwość `<id>` jest ustawiona na nazwę zestawu, a `<version>` jest ustawiona na wersję zestawu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="b9c2c-224">Inne właściwości w manifeście nie mają jednak pasujących wartości w zestawie i w ten sposób nadal zawierają symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="b9c2c-225">Z projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9c2c-225">From a Visual Studio project</span></span>

<span data-ttu-id="b9c2c-226">Tworzenie `.nuspec` z pliku `.csproj` lub `.vbproj` jest wygodne, ponieważ inne pakiety, które zostały zainstalowane w tym projekcie, są automatycznie przywoływane jako zależności.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="b9c2c-227">Po prostu Użyj następującego polecenia w tym samym folderze, w którym znajduje się plik projektu:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="b9c2c-228">Plik `<project-name>.nuspec` zawiera *tokeny* , które zostały zastąpione w czasie pakowania wartościami z projektu, włącznie z odwołaniami do innych pakietów, które zostały już zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="b9c2c-229">Jeśli masz zależności pakietu do uwzględnienia w pliku *. nuspec*, zamiast tego użyj `nuget pack` i Pobierz plik *. nuspec* z wygenerowanego *. nupkg* .</span><span class="sxs-lookup"><span data-stu-id="b9c2c-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="b9c2c-230">Na przykład użyj poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="b9c2c-231">Token jest rozdzielony przez symbole `$` po obu stronach właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="b9c2c-232">Na przykład wartość `<id>` w manifeście generowanym w ten sposób zwykle pojawia się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="b9c2c-233">Ten token jest zastępowany wartością `AssemblyName` z pliku projektu w czasie pakowania.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="b9c2c-234">Dokładne mapowanie wartości projektu do `.nuspec` tokenów zawiera [odwołanie do tokenów zastępczych](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="b9c2c-235">Tokeny zwalniają z konieczności aktualizowania najważniejszych wartości, takich jak numer wersji w `.nuspec` podczas aktualizowania projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="b9c2c-236">(Można zawsze zastąpić tokeny wartościami literału, jeśli jest to wymagane).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="b9c2c-237">Należy pamiętać, że podczas pracy z projektem programu Visual Studio jest dostępnych kilka dodatkowych opcji pakowania, zgodnie z opisem w artykule [uruchamianie pakietu NuGet w celu wygenerowania pliku. nupkg](#run-nuget-pack-to-generate-the-nupkg-file) w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="b9c2c-238">Pakiety na poziomie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="b9c2c-238">Solution-level packages</span></span>

<span data-ttu-id="b9c2c-239">*Tylko pakiet NuGet 2. x. Niedostępne w programie NuGet 3.0 lub nowszym.*</span><span class="sxs-lookup"><span data-stu-id="b9c2c-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="b9c2c-240">Pakiet NuGet 2. x obsługuje pojęcie pakietu na poziomie rozwiązania, który instaluje narzędzia lub dodatkowe polecenia dla konsoli Menedżera pakietów (zawartość folderu `tools`), ale nie dodaje odwołań, zawartości ani dostosowań kompilacji do żadnych projektów w Narzędzie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="b9c2c-241">Takie pakiety nie zawierają żadnych plików w folderach bezpośrednio `lib`, `content` lub `build`, a żadna z jej zależności nie ma plików w odpowiednich `lib`, `content` lub `build` folderów.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="b9c2c-242">Pakiet NuGet śledzi zainstalowane pakiety na poziomie rozwiązania w pliku `packages.config` w folderze `.nuget`, a nie w pliku `packages.config` projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="b9c2c-243">Nowy plik z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="b9c2c-243">New file with default values</span></span>

<span data-ttu-id="b9c2c-244">Następujące polecenie tworzy manifest domyślny z symbolami zastępczymi, co zapewnia rozpoczęcie od właściwej struktury plików:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="b9c2c-245">W przypadku pominięcia \<nazwy pakietu\>, otrzymany plik zostanie `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="b9c2c-246">Jeśli podano nazwę, taką jak `Contoso.Utility.UsefulStuff`, plik jest `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="b9c2c-247">Wyniki `.nuspec` zawierają symbole zastępcze dla wartości, takich jak `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="b9c2c-248">Pamiętaj, aby edytować plik przed jego użyciem, aby utworzyć końcowy plik `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="b9c2c-249">Wybierz unikatowy identyfikator pakietu i ustaw numer wersji</span><span class="sxs-lookup"><span data-stu-id="b9c2c-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="b9c2c-250">Identyfikator pakietu (element `<id>`) i numer wersji (element `<version>`) to dwie najważniejsze wartości w manifeście, ponieważ jednoznacznie identyfikują dokładny kod zawarty w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="b9c2c-251">**Najlepsze rozwiązania dotyczące identyfikatora pakietu:**</span><span class="sxs-lookup"><span data-stu-id="b9c2c-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="b9c2c-252">**Unikatowość**: Identyfikator musi być unikatowy w obrębie NuGet.org lub dowolnej galerii, w której znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="b9c2c-253">Przed podjęciem decyzji o identyfikatorze Przeszukaj stosowną galerię, aby sprawdzić, czy nazwa jest już używana.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="b9c2c-254">Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej części identyfikatora, takiej jak `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="b9c2c-255">**Nazwy podobne do nazw**: Postępuj zgodnie ze wzorcem podobnym do przestrzeni nazw w programie .NET przy użyciu notacji kropkowej zamiast łączników.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="b9c2c-256">Na przykład użyj `Contoso.Utility.UsefulStuff`, a nie `Contoso-Utility-UsefulStuff` lub `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="b9c2c-257">Konsumenci są również pomocne, gdy identyfikator pakietu jest zgodny z przestrzeniami nazw używanymi w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="b9c2c-258">**Przykładowe pakiety**: w przypadku tworzenia pakietu przykładowego kodu, który demonstruje sposób użycia innego pakietu, należy dołączyć `.Sample` jako sufiks do identyfikatora, jak w `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="b9c2c-259">(Przykładowy pakiet jest oczywiście zależny od innego pakietu). Podczas tworzenia przykładowego pakietu Użyj metody katalogu roboczego opartej na Konwencji opisanej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="b9c2c-260">W folderze `content` Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` jako `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="b9c2c-261">**Najlepsze rozwiązania dotyczące wersji pakietu:**</span><span class="sxs-lookup"><span data-stu-id="b9c2c-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="b9c2c-262">Ogólnie rzecz biorąc Ustaw wersję pakietu na zgodną z biblioteką, chociaż nie jest to wymagane absolutnie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="b9c2c-263">Jest to prosta kwestia w przypadku ograniczenia pakietu do jednego zestawu, zgodnie z wcześniejszym opisem w [wyborze zestawów do spakowania](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="b9c2c-264">Ogólnie, pamiętaj, że sam pakiet NuGet zajmuje się wersjami pakietu podczas rozpoznawania zależności, a nie wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="b9c2c-265">W przypadku korzystania ze schematu wersji niestandardowej należy wziąć pod uwagę reguły obsługi wersji NuGet zgodnie z opisem w temacie [wersja pakietu](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="b9c2c-266">Poniższa seria krótkich wpisów w blogu pomaga również zrozumieć przechowywanie wersji:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="b9c2c-267">Część 1: pobieranie biblioteki DLL Hell</span><span class="sxs-lookup"><span data-stu-id="b9c2c-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="b9c2c-268">Część 2: podstawowy algorytm</span><span class="sxs-lookup"><span data-stu-id="b9c2c-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="b9c2c-269">Część 3: ujednolicenie za pośrednictwem przekierowań powiązań</span><span class="sxs-lookup"><span data-stu-id="b9c2c-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="b9c2c-270">Dodaj plik Readme i inne pliki</span><span class="sxs-lookup"><span data-stu-id="b9c2c-270">Add a readme and other files</span></span>

<span data-ttu-id="b9c2c-271">Aby bezpośrednio określić pliki do dołączenia do pakietu, Użyj węzła `<files>` w pliku `.nuspec`, który *następuje* po tagu `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="b9c2c-272">W przypadku korzystania z podejścia do katalogu roboczego opartego na konwencji można umieścić plik Readme. txt w katalogu głównym pakietu i w innej zawartości w folderze `content`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="b9c2c-273">W manifeście nie są wymagane żadne elementy `<file>`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="b9c2c-274">Po dołączeniu pliku o nazwie `readme.txt` w katalogu głównym pakietu program Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst natychmiast po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="b9c2c-275">(Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="b9c2c-276">Na przykład poniżej przedstawiono sposób wyświetlania pliku Readme dla pakietu HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Wyświetlanie pliku Readme dla pakietu NuGet podczas instalacji](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="b9c2c-278">Jeśli dołączysz pusty węzeł `<files>` w pliku `.nuspec`, pakiet NuGet nie będzie zawierał żadnej innej zawartości w pakiecie innym niż zawartość folderu `lib`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="b9c2c-279">Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="b9c2c-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="b9c2c-280">W niektórych przypadkach może zajść potrzeba dodania niestandardowych elementów docelowych kompilacji lub właściwości w projektach korzystających z pakietu, takich jak uruchamianie niestandardowego narzędzia lub procesu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="b9c2c-281">W tym celu należy umieścić pliki w formularzu `<package_id>.targets` lub `<package_id>.props` (takie jak `Contoso.Utility.UsefulStuff.targets`) w folderze `\build` projektu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="b9c2c-282">Pliki w folderze głównym `\build` są uważane za odpowiednie dla wszystkich platform docelowych.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="b9c2c-283">Aby zapewnić pliki specyficzne dla struktury, należy najpierw umieścić je w odpowiednich podfolderach, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="b9c2c-284">Następnie w pliku `.nuspec` zapoznaj się z tymi plikami w węźle `<files>`:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="b9c2c-285">W tym, że w pakiecie [NuGet 2,5 wprowadzono](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)atrybuty i elementy docelowe programu MSBuild, dlatego zaleca się dodanie atrybutu `minClientVersion="2.5"` do elementu `metadata` w celu wskazania minimalnej wersji klienta NuGet wymaganej do korzystania z pakietu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="b9c2c-286">Gdy narzędzie NuGet zainstaluje pakiet z plikami `\build`, spowoduje to dodanie elementów programu MSBuild `<Import>` w pliku projektu wskazujących pliki `.targets` i `.props`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="b9c2c-287">(`.props` zostanie dodany u góry pliku projektu; w dolnej części zostanie dodany `.targets`). Dla każdej platformy docelowej dodawany jest oddzielny warunkowy element `<Import>` programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="b9c2c-288">Pliki programu MSBuild `.props` i `.targets` dla określania wartości docelowej między platformami można umieścić w folderze `\buildMultiTargeting`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="b9c2c-289">Podczas instalacji pakietu NuGet dodaje odpowiednie elementy `<Import>` do pliku projektu z warunkiem, że platforma docelowa nie jest ustawiona (Właściwość programu MSBuild `$(TargetFramework)` musi być pusta).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="b9c2c-290">W przypadku programu NuGet 3. x elementy docelowe nie są dodawane do projektu, ale zamiast tego są udostępniane za pomocą `{projectName}.nuget.g.targets` i `{projectName}.nuget.g.props`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="b9c2c-291">Uruchom pakiet NuGet, aby wygenerować plik. nupkg</span><span class="sxs-lookup"><span data-stu-id="b9c2c-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="b9c2c-292">W przypadku korzystania z zestawu lub katalogu roboczego opartego na Konwencji Utwórz pakiet, uruchamiając `nuget pack` z plikiem `.nuspec`, zastępując `<project-name>` z określoną nazwą pliku:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="b9c2c-293">W przypadku korzystania z projektu programu Visual Studio Uruchom `nuget pack` z plikiem projektu, który automatycznie ładuje plik `.nuspec` projektu i zastępuje wszystkie tokeny w nim przy użyciu wartości w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="b9c2c-294">Użycie pliku projektu bezpośrednio jest niezbędne do zastąpienia tokenu, ponieważ jest to źródło wartości tokenu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="b9c2c-295">Zastępowanie tokenu nie następuje, jeśli używasz `nuget pack` z plikiem `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="b9c2c-296">We wszystkich przypadkach `nuget pack` wyklucza foldery, które zaczynają się kropką, na przykład `.git` lub `.hg`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="b9c2c-297">Pakiet NuGet wskazuje, czy w pliku `.nuspec` występują błędy, które wymagają skorygowania, na przykład zapominanie o zmianie wartości symboli zastępczych w manifeście.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="b9c2c-298">Po pomyślnym wykonaniu `nuget pack` masz plik `.nupkg`, który można opublikować w odpowiedniej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="b9c2c-299">Przydatnym sposobem na badanie pakietu po jego utworzeniu jest otwarcie go w narzędziu [Eksplorator pakietów](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) .</span><span class="sxs-lookup"><span data-stu-id="b9c2c-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="b9c2c-300">Dzięki temu można wyświetlić graficzny widok zawartości pakietu i jego manifestu.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="b9c2c-301">Możesz również zmienić nazwę wyniku pliku `.nupkg` na plik `.zip` i eksplorować jego zawartość bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="b9c2c-302">Opcje dodatkowe</span><span class="sxs-lookup"><span data-stu-id="b9c2c-302">Additional options</span></span>

<span data-ttu-id="b9c2c-303">Można użyć różnych przełączników wiersza polecenia z `nuget pack`, aby wykluczyć pliki, zastąpić numer wersji w manifeście i zmienić folder wyjściowy, między innymi.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="b9c2c-304">Pełną listę można znaleźć w [dokumentacji polecenia pakietu](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="b9c2c-305">Poniżej wymieniono kilka opcji, które są wspólne dla projektów programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="b9c2c-306">**Przywoływane projekty**: Jeśli projekt odwołuje się do innych projektów, można dodać przywoływane projekty jako część pakietu lub jako zależności przy użyciu opcji `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="b9c2c-307">Ten proces dołączania jest cykliczny, więc jeśli `MyProject.csproj` odwołuje się do projektów B i C, a te projekty odwołują się do D, E i F, wówczas pliki z B, C, D, E i F są zawarte w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="b9c2c-308">Jeśli projekt, do którego istnieje odwołanie, zawiera plik `.nuspec`, wówczas pakiet NuGet dodaje do niego przywoływany projekt jako zależność.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="b9c2c-309">Należy osobno spakować i opublikować ten projekt.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="b9c2c-310">**Konfiguracja kompilacji**: domyślnie NuGet używa domyślnego zestawu konfiguracji kompilacji w pliku projektu, zazwyczaj *Debuguj*.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="b9c2c-311">Aby spakować pliki z innej konfiguracji kompilacji, takiej jak *wersja*, użyj opcji `-properties` z konfiguracją:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="b9c2c-312">**Symbole**: Aby dołączyć symbole umożliwiające użytkownikom przechodzenie przez kod pakietu w debugerze, użyj opcji `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="b9c2c-313">Instalacja pakietu testowego</span><span class="sxs-lookup"><span data-stu-id="b9c2c-313">Test package installation</span></span>

<span data-ttu-id="b9c2c-314">Przed opublikowaniem pakietu zazwyczaj należy przetestować proces instalacji pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="b9c2c-315">Testy upewniają się, że wszystkie pliki, które się na bieżąco, kończą się w ich prawidłowym miejscu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="b9c2c-316">Instalacje można testować ręcznie w programie Visual Studio lub w wierszu polecenia przy użyciu standardowych [kroków instalacji pakietu](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="b9c2c-317">W przypadku zautomatyzowanych testów proces podstawowy jest następujący:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="b9c2c-318">Skopiuj plik `.nupkg` do folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="b9c2c-319">Dodaj folder do źródeł pakietów przy użyciu polecenia `nuget sources add -name <name> -source <path>` (zobacz [źródła NuGet](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="b9c2c-320">Należy pamiętać, że to źródło lokalne należy ustawić tylko raz na danym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="b9c2c-321">Zainstaluj pakiet z tego źródła przy użyciu `nuget install <packageID> -source <name>`, gdzie `<name>` dopasowuje nazwę źródła zgodnie z `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="b9c2c-322">Określenie źródła gwarantuje, że pakiet jest instalowany wyłącznie z tego źródła.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="b9c2c-323">Sprawdź system plików, aby sprawdzić, czy pliki są poprawnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="b9c2c-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9c2c-324">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b9c2c-324">Next Steps</span></span>

<span data-ttu-id="b9c2c-325">Po utworzeniu pakietu, który jest plikiem `.nupkg`, można opublikować go w wybranej galerii, zgodnie z opisem w artykule [Publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b9c2c-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="b9c2c-326">Możesz również chcieć zwiększyć możliwości pakietu lub w inny sposób obsługiwać inne scenariusze zgodnie z opisem w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="b9c2c-327">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="b9c2c-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="b9c2c-328">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="b9c2c-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="b9c2c-329">Przekształcenia plików źródłowych i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="b9c2c-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="b9c2c-330">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="b9c2c-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b9c2c-331">Wersje wstępne</span><span class="sxs-lookup"><span data-stu-id="b9c2c-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="b9c2c-332">Ustawianie typu pakietu</span><span class="sxs-lookup"><span data-stu-id="b9c2c-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="b9c2c-333">Tworzenie pakietów z zestawami międzyoperacyjnymi modelu COM</span><span class="sxs-lookup"><span data-stu-id="b9c2c-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="b9c2c-334">Na koniec należy pamiętać o dodatkowych typach pakietów:</span><span class="sxs-lookup"><span data-stu-id="b9c2c-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="b9c2c-335">Pakiety natywne</span><span class="sxs-lookup"><span data-stu-id="b9c2c-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="b9c2c-336">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="b9c2c-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
