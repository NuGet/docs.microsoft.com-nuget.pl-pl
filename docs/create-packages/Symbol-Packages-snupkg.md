---
title: Jak opublikować pakiety NuGet symboli, przy użyciu nowego formatu pakietu symbol ".snupkg" | Dokumentacja firmy Microsoft
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak utworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, pakietów NuGet, debugowanie, obsługa NuGet debugowania pakiet symboli, konwencje pakietu symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 43f346dc64ebbc59d02b9c7875b04205d8c5d83a
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852445"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="4f76a-104">Tworzenie pakietów symbol (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="4f76a-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="4f76a-105">Pakiety symboli umożliwiają lepsze środowisko debugowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="4f76a-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f76a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4f76a-106">Prerequisites</span></span>

<span data-ttu-id="4f76a-107">[nuget.exe v4.9.0 lub nowszej](https://www.nuget.org/downloads) lub [dotnet.exe v2.2.0 lub nowszej](https://www.microsoft.com/net/download/dotnet-core/2.2), który implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="4f76a-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="4f76a-108">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="4f76a-108">Creating a symbol package</span></span>

<span data-ttu-id="4f76a-109">Można utworzyć snupkg symbol pakietu dotnet.exe NuGet.exe oraz programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4f76a-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="4f76a-110">Jeśli używasz NuGet.exe służy następujących poleceń do utworzenia pliku .snupkg oprócz pliku .nupkg:</span><span class="sxs-lookup"><span data-stu-id="4f76a-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="4f76a-111">Jeśli używasz dotnet.exe lub MSBuild umożliwia utworzenie pliku .snupkg oprócz pliku .nupkg następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4f76a-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="4f76a-112">Dodaj następujące właściwości do pliku csproj:</span><span class="sxs-lookup"><span data-stu-id="4f76a-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="4f76a-113">Pakiet projektu za pomocą `dotnet pack MyPackage.csproj` lub `msbuild -t:pack MyPackage.csproj`.</span><span class="sxs-lookup"><span data-stu-id="4f76a-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="4f76a-114">`SymbolPackageFormat` Właściwość może mieć jedną z dwóch wartości: `symbols.nupkg` (ustawienie domyślne) lub `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4f76a-114">The `SymbolPackageFormat` property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="4f76a-115">Jeśli `SymbolPackageFormat` właściwość nie zostanie określony, jego wartość domyślna to `symbols.nupkg` i zostanie utworzony pakiet symboli starszej wersji.</span><span class="sxs-lookup"><span data-stu-id="4f76a-115">If the `SymbolPackageFormat` property is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="4f76a-116">Format starszych `.symbols.nupkg` jest nadal obsługiwane, ale tylko ze względu na zgodność (zobacz [pakiety ze starszych wersji Symbol](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="4f76a-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="4f76a-117">Serwer symboli NuGet.org akceptuje tylko na nowy format pakietu symboli — `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4f76a-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="4f76a-118">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="4f76a-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="4f76a-119">Dla wygody, najpierw zapisać swój klucz interfejsu API z NuGet (zobacz [publikowanie pakietu](../create-packages/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="4f76a-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="4f76a-120">Po opublikowaniu pakiet podstawowego na stronie nuget.org, Wypchnij następujący pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="4f76a-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="4f76a-121">Można również wypchnąć podstawowych i symboli pakietów w tej samej chwili poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f76a-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="4f76a-122">Pliki .nupkg i .snupkg muszą znajdować się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="4f76a-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="4f76a-123">NuGet opublikuje oba pakiety na stronie nuget.org. `MyPackage.nupkg` zostaną opublikowane w pierwszym, następuje `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4f76a-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="4f76a-124">Serwer symboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4f76a-124">NuGet.org symbol server</span></span>

<span data-ttu-id="4f76a-125">NuGet.org obsługuje własne repozytorium serwer symboli i akceptuje tylko na nowy format pakietu symboli — `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="4f76a-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="4f76a-126">Konsumentów pakietu można użyć symboli publikowane w witrynie nuget.org serwera symboli, dodając `https://symbols.nuget.org/download/symbols` źródła symbol w programie Visual Studio, umożliwia przechodzenie do pakietu kodu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f76a-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="4f76a-127">Zobacz [określanie plików symboli (.pdb) i plików źródłowych w debugerze programu Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) szczegółowe informacje na temat tego procesu.</span><span class="sxs-lookup"><span data-stu-id="4f76a-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="4f76a-128">Ograniczenia pakietu symboli Nuget.org</span><span class="sxs-lookup"><span data-stu-id="4f76a-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="4f76a-129">Pakiety symboli, obsługiwane w witrynie nuget.org mają następujące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="4f76a-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="4f76a-130">Tylko następujące rozszerzenia są dozwolone do dodania do pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="4f76a-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="4f76a-131">Tylko zarządzane [przenośnych plików PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obecnie obsługiwane na serwerze symboli nuget.</span><span class="sxs-lookup"><span data-stu-id="4f76a-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="4f76a-132">Plików PDB i bibliotek DLL skojarzonych nupkg muszą zostać skompilowane przez kompilator w Visual Studio w wersji 15.9 lub nowszej (zobacz [skrót kryptograficzny pliku pdb](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="4f76a-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="4f76a-133">Pakowanie symboli publikowanie w witrynie nuget.org zakończy się niepowodzeniem, jeśli inne typy plików są objęte .snupkg.</span><span class="sxs-lookup"><span data-stu-id="4f76a-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="4f76a-134">Sprawdzanie poprawności pakietu symboli i indeksowania</span><span class="sxs-lookup"><span data-stu-id="4f76a-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="4f76a-135">Symbol pakiety opublikowane do [NuGet.org](https://www.nuget.org/) uczestniczenia w kilku operacji sprawdzania poprawności, takich jak sprawdzanie przed wirusami.</span><span class="sxs-lookup"><span data-stu-id="4f76a-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="4f76a-136">Gdy pakiet został przekazany wszystkie testy sprawdzania poprawności, może to zająć trochę czasu symbole, aby zaindeksować i być dostępne do użytku z serwerów symboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4f76a-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="4f76a-137">W przypadku niepowodzenia sprawdzania poprawności pakietu stronie szczegółów pakietu .nupkg zostanie zaktualizowana, aby wyświetlić skojarzony błąd i zostanie wysłana wiadomość e-mail z powiadomieniem o nim.</span><span class="sxs-lookup"><span data-stu-id="4f76a-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="4f76a-138">Sprawdzanie poprawności pakietu i indeksowanie zwykle trwa mniej niż 15 minut.</span><span class="sxs-lookup"><span data-stu-id="4f76a-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="4f76a-139">Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, jeśli nuget.org występuje przerw.</span><span class="sxs-lookup"><span data-stu-id="4f76a-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="4f76a-140">Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się na stronie nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z działem pomocy technicznej na stronie szczegółów pakietu.</span><span class="sxs-lookup"><span data-stu-id="4f76a-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="4f76a-141">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="4f76a-141">Symbol package structure</span></span>

<span data-ttu-id="4f76a-142">Plik .nupkg będą dokładnie takie same jest już dziś, ale plik .snupkg będzie mieć następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="4f76a-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="4f76a-143">.snupkg mają ten sam identyfikator i wersja jako odpowiednie .nupkg.</span><span class="sxs-lookup"><span data-stu-id="4f76a-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="4f76a-144">.snupkg ma strukturę folderów dokładne jak nupkg do plików DLL lub EXE z różnica, zamiast pliku biblioteki DLL/exe ich odpowiednich plików PDB zostaną uwzględnione w tej samej hierarchii.</span><span class="sxs-lookup"><span data-stu-id="4f76a-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="4f76a-145">Poza snupkg pozostanie plików i folderów przy użyciu rozszerzeń innych niż plik PDB.</span><span class="sxs-lookup"><span data-stu-id="4f76a-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="4f76a-146">Pliku .nuspec w .snupkg będzie również określić nowy PackageType zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="4f76a-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="4f76a-147">Powinna to być tylko jeden PackageType, określony.</span><span class="sxs-lookup"><span data-stu-id="4f76a-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="4f76a-148">Jeśli autor zdecyduje się użyć niestandardowych nuspec do utworzenia ich nupkg i snupkg, snupkg powinny mieć tej samej hierarchii folderów i plików szczegółowe w wersji 2).</span><span class="sxs-lookup"><span data-stu-id="4f76a-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="4f76a-149">```authors``` i ```owners``` pola, które zostaną wykluczone z snupkg nuspec.</span><span class="sxs-lookup"><span data-stu-id="4f76a-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="4f76a-150">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4f76a-150">See Also</span></span>

[<span data-ttu-id="4f76a-151">NuGet — pakiet — debugowanie — & - symbole — ulepszenia</span><span class="sxs-lookup"><span data-stu-id="4f76a-151">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
