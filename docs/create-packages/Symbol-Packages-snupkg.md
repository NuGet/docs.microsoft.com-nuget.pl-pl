---
title: Jak publikować pakiety symboli NuGet przy użyciu nowego formatu pakietu symboli ". snupkg" | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak utworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, debugowanie pakietów NuGet, obsługa debugowania NuGet, symbole pakietów i konwencje pakietów symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: e62d1872497e0e5e703bf7c49a87249ce9a996c7
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959675"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="7dfd9-104">Tworzenie pakietów symboli (. snupkg)</span><span class="sxs-lookup"><span data-stu-id="7dfd9-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="7dfd9-105">Pakiety symboli umożliwiają zwiększenie możliwości debugowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dfd9-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7dfd9-106">Prerequisites</span></span>

<span data-ttu-id="7dfd9-107">[NuGet. exe v 4.9.0 lub nowszy](https://www.nuget.org/downloads) albo [dotnet. exe v 2.2.0 lub nowszy](https://www.microsoft.com/net/download/dotnet-core/2.2), które implementują wymagane [Protokoły NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7dfd9-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="7dfd9-108">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="7dfd9-108">Creating a symbol package</span></span>

<span data-ttu-id="7dfd9-109">Pakiet symboli snupkg można utworzyć przy użyciu programu dotnet. exe, NuGet. exe lub MSBuild.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="7dfd9-110">Jeśli używasz programu NuGet. exe, możesz użyć następujących poleceń, aby utworzyć plik. snupkg oprócz pliku. nupkg:</span><span class="sxs-lookup"><span data-stu-id="7dfd9-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="7dfd9-111">Jeśli używasz programu dotnet. exe lub MSBuild, wykonaj następujące kroki, aby utworzyć plik. snupkg oprócz pliku. nupkg:</span><span class="sxs-lookup"><span data-stu-id="7dfd9-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="7dfd9-112">Dodaj następujące właściwości do pliku. csproj:</span><span class="sxs-lookup"><span data-stu-id="7dfd9-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="7dfd9-113">Pakowanie projektu z `dotnet pack MyPackage.csproj` lub `msbuild -t:pack MyPackage.csproj`.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="7dfd9-114">Właściwość może mieć jedną z dwóch wartości: `symbols.nupkg` (wartość domyślna) lub `snupkg`. [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)</span><span class="sxs-lookup"><span data-stu-id="7dfd9-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="7dfd9-115">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) Jeśli właściwość nie jest określona, zostanie utworzony starszy pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-115">If the [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="7dfd9-116">Starszy format `.symbols.nupkg` jest nadal obsługiwany, ale tylko ze względu na zgodność (zobacz [starsze pakiety symboli](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="7dfd9-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="7dfd9-117">NuGet. serwer symboli organizacji akceptuje tylko nowy format pakietu symboli — `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="7dfd9-118">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="7dfd9-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="7dfd9-119">Dla wygody najpierw Zapisz klucz interfejsu API za pomocą narzędzia NuGet (zobacz [Publikowanie pakietu](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="7dfd9-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="7dfd9-120">Po opublikowaniu pakietu podstawowego w programie nuget.org wypchnij pakiet symboli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="7dfd9-121">Możesz również wypchnąć zarówno podstawowe, jak i w tym samym czasie pakiety symboli przy użyciu poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="7dfd9-122">Oba pliki. nupkg i. snupkg muszą znajdować się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="7dfd9-123">Program NuGet opublikuje Oba pakiety w nuget.org. zostanie opublikowany jako pierwszy, `MyPackage.snupkg`a następnie. `MyPackage.nupkg`</span><span class="sxs-lookup"><span data-stu-id="7dfd9-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="7dfd9-124">Jeśli pakiet symboli nie jest opublikowany, sprawdź, czy źródło NuGet.org zostało skonfigurowane jako `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="7dfd9-125">Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API programu NuGet v3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="7dfd9-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="7dfd9-126">Serwer symboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="7dfd9-126">NuGet.org symbol server</span></span>

<span data-ttu-id="7dfd9-127">NuGet.org obsługuje własne repozytorium serwera symboli i akceptuje tylko nowy format pakietu symboli — `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="7dfd9-128">Odbiorcy pakietu mogą korzystać z symboli opublikowanych na serwerze symboli NuGet.org przez dodanie `https://symbols.nuget.org/download/symbols` ich do źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="7dfd9-129">Aby uzyskać szczegółowe informacje na temat tego procesu, zobacz [Określanie symboli (. pdb) i plików źródłowych w debugerze programu Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) .</span><span class="sxs-lookup"><span data-stu-id="7dfd9-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="7dfd9-130">Ograniczenia pakietu symboli Nuget.org</span><span class="sxs-lookup"><span data-stu-id="7dfd9-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="7dfd9-131">Pakiety symboli obsługiwane na nuget.org mają następujące unikatowego</span><span class="sxs-lookup"><span data-stu-id="7dfd9-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="7dfd9-132">Tylko następujące rozszerzenia plików mogą być dodawane do pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="7dfd9-133">Tylko zarządzane [plików PDB przenośne](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obecnie obsługiwane na serwerze symboli NuGet.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="7dfd9-134">Plików PDB i skojarzone biblioteki DLL NUPKG muszą być kompilowane przy użyciu kompilatora w programie Visual Studio w wersji 15,9 lub nowszej (zobacz [skrót kryptografii PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="7dfd9-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="7dfd9-135">Publikowanie pakietu symboli w usłudze nuget.org zakończy się niepowodzeniem, jeśli jakiekolwiek inne typy plików znajdują się w pliku. snupkg.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="7dfd9-136">Walidacja i indeksowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="7dfd9-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="7dfd9-137">Pakiety symboli opublikowane w [NuGet.org](https://www.nuget.org/) poddają się kilku walidacji, takich jak sprawdzanie wirusów.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="7dfd9-138">Gdy pakiet przeszedł wszystkie sprawdzenia poprawności, może upłynąć trochę czasu, aby symbole były indeksowane i dostępne do użycia z serwerów symboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="7dfd9-139">Jeśli pakiet nie zostanie zweryfikowany, Strona szczegółów pakietu dla elementu. nupkg zostanie zaktualizowana w celu wyświetlenia powiązanego błędu i otrzymasz również wiadomość e-mail z powiadomieniem o tym fakcie.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="7dfd9-140">Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa 15 minut.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="7dfd9-141">Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.NuGet.org](https://status.nuget.org/) , aby sprawdzić, czy w NuGet.org występują jakiekolwiek przerwy.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="7dfd9-142">Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z pomocą techniczną na stronie Szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="7dfd9-143">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="7dfd9-143">Symbol package structure</span></span>

<span data-ttu-id="7dfd9-144">Plik. nupkg będzie dokładnie taki sam, jak dzisiaj, ale plik. snupkg ma następującą charakterystykę:</span><span class="sxs-lookup"><span data-stu-id="7dfd9-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="7dfd9-145">Element. snupkg będzie miał ten sam identyfikator i wersję co odpowiadający element. nupkg.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="7dfd9-146">Plik. snupkg będzie miał dokładną strukturę folderów jako NUPKG dla każdej biblioteki DLL lub EXE z rozróżnieniem, które zamiast bibliotek DLL/exe, odpowiadające im plików PDB zostaną uwzględnione w tej samej hierarchii folderów.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="7dfd9-147">Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pozostawione z snupkg.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="7dfd9-148">Plik. nuspec w pliku. snupkg określi również nowy element PackageType w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="7dfd9-149">Powinien to być określony tylko jeden pakiet.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-149">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="7dfd9-150">Jeśli autor zdecyduje się użyć niestandardowych nuspec do kompilowania ich NUPKG i snupkg, snupkg powinien mieć tę samą hierarchię folderów i pliki szczegółowe w 2).</span><span class="sxs-lookup"><span data-stu-id="7dfd9-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="7dfd9-151">```authors```i ```owners``` pole zostanie wykluczone z nuspec snupkg.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="7dfd9-152">Nie należy używać <license> elementu.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-152">Do not use the <license> element.</span></span> <span data-ttu-id="7dfd9-153">A. snupkg jest objęta tą samą licencją co odpowiadające mu. nupk.</span><span class="sxs-lookup"><span data-stu-id="7dfd9-153">A .snupkg is covered under the same license as the corresponding .nupk.</span></span>

## <a name="see-also"></a><span data-ttu-id="7dfd9-154">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7dfd9-154">See Also</span></span>

[<span data-ttu-id="7dfd9-155">NuGet-Package-Debug-&-Symbols — ulepszenia</span><span class="sxs-lookup"><span data-stu-id="7dfd9-155">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
