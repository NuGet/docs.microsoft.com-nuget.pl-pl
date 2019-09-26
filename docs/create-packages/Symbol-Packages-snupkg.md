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
ms.openlocfilehash: 0197902e4dbc18893d68833fbcfe4263f185a594
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307187"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="cdd6d-104">Tworzenie pakietów symboli (. snupkg)</span><span class="sxs-lookup"><span data-stu-id="cdd6d-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="cdd6d-105">Pakiety symboli umożliwiają zwiększenie możliwości debugowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdd6d-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cdd6d-106">Prerequisites</span></span>

<span data-ttu-id="cdd6d-107">[NuGet. exe v 4.9.0 lub nowszy](https://www.nuget.org/downloads) albo [dotnet. exe v 2.2.0 lub nowszy](https://www.microsoft.com/net/download/dotnet-core/2.2), które implementują wymagane [Protokoły NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="cdd6d-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="cdd6d-108">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="cdd6d-108">Creating a symbol package</span></span>

<span data-ttu-id="cdd6d-109">Jeśli używasz programu dotnet. exe lub MSBuild, musisz ustawić `IncludeSymbols` właściwości i `SymbolPackageFormat` , aby utworzyć plik. snupkg oprócz pliku. nupkg.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="cdd6d-110">Dodaj następujące właściwości do pliku. csproj:</span><span class="sxs-lookup"><span data-stu-id="cdd6d-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="cdd6d-111">Lub Określ te właściwości w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="cdd6d-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="cdd6d-112">lub</span><span class="sxs-lookup"><span data-stu-id="cdd6d-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="cdd6d-113">Jeśli używasz programu NuGet. exe, możesz użyć następujących poleceń, aby utworzyć plik. snupkg oprócz pliku. nupkg:</span><span class="sxs-lookup"><span data-stu-id="cdd6d-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="cdd6d-114">Właściwość może mieć jedną z dwóch wartości: `symbols.nupkg` (wartość domyślna) lub `snupkg`. [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)</span><span class="sxs-lookup"><span data-stu-id="cdd6d-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="cdd6d-115">Jeśli ta właściwość nie zostanie określona, zostanie utworzony starszy pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="cdd6d-116">Starszy format `.symbols.nupkg` jest nadal obsługiwany, ale tylko ze względu na zgodność (zobacz [starsze pakiety symboli](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="cdd6d-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="cdd6d-117">NuGet. serwer symboli organizacji akceptuje tylko nowy format pakietu symboli — `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="cdd6d-118">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="cdd6d-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="cdd6d-119">Dla wygody najpierw Zapisz klucz interfejsu API za pomocą narzędzia NuGet (zobacz [Publikowanie pakietu](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="cdd6d-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="cdd6d-120">Po opublikowaniu pakietu podstawowego w programie nuget.org wypchnij pakiet symboli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="cdd6d-121">Możesz również wypchnąć zarówno podstawowe, jak i w tym samym czasie pakiety symboli przy użyciu poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="cdd6d-122">Oba pliki. nupkg i. snupkg muszą znajdować się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="cdd6d-123">Program NuGet opublikuje Oba pakiety w nuget.org. zostanie opublikowany jako pierwszy, `MyPackage.snupkg`a następnie. `MyPackage.nupkg`</span><span class="sxs-lookup"><span data-stu-id="cdd6d-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="cdd6d-124">Jeśli pakiet symboli nie jest opublikowany, sprawdź, czy źródło NuGet.org zostało skonfigurowane jako `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="cdd6d-125">Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API programu NuGet v3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="cdd6d-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="cdd6d-126">Serwer symboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="cdd6d-126">NuGet.org symbol server</span></span>

<span data-ttu-id="cdd6d-127">NuGet.org obsługuje własne repozytorium serwera symboli i akceptuje tylko nowy format pakietu symboli — `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="cdd6d-128">Odbiorcy pakietu mogą korzystać z symboli opublikowanych na serwerze symboli NuGet.org przez dodanie `https://symbols.nuget.org/download/symbols` ich do źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="cdd6d-129">Aby uzyskać szczegółowe informacje na temat tego procesu, zobacz [Określanie symboli (. pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="cdd6d-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="cdd6d-130">Ograniczenia pakietu symboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="cdd6d-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="cdd6d-131">NuGet.org ma następujące ograniczenia dotyczące pakietów symboli:</span><span class="sxs-lookup"><span data-stu-id="cdd6d-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="cdd6d-132">W pakietach symboli są dozwolone tylko następujące rozszerzenia plików: `.pdb`, `.nuspec`, `.xml` `.psmdcp` `.rels`,,,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="cdd6d-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="cdd6d-133">Tylko zarządzane [plików PDB przenośne](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obsługiwane przez pakiet NuGet. serwer symboli w organizacji.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="cdd6d-134">Plików PDB i skojarzone z nimi biblioteki DLL NUPKG muszą być kompilowane przy użyciu kompilatora w programie Visual Studio w wersji 15,9 lub nowszej (zobacz [skrót kryptografii PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="cdd6d-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="cdd6d-135">W przypadku, gdy te ograniczenia nie są spełnione, pakiety symboli opublikowane w programie NuGet.org będą kończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="cdd6d-136">Walidacja i indeksowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="cdd6d-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="cdd6d-137">Pakiety symboli opublikowane w [NuGet.org](https://www.nuget.org/) przechodzą kilka walidacji, w tym skanowanie złośliwego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="cdd6d-138">Jeśli pakiet nie zostanie zweryfikowany, na stronie szczegółów pakietu zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="cdd6d-139">Ponadto właściciele pakietu otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu rozwiązywania zidentyfikowanych problemów.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="cdd6d-140">Gdy pakiet symboli przeszedł wszystkie walidacje, symbole będą indeksowane przez NuGet. serwery symboli w organizacji.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="cdd6d-141">Po indeksowaniu symbol będzie dostępny do użycia z serwerów symboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="cdd6d-142">Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa 15 minut.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="cdd6d-143">Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.NuGet.org](https://status.nuget.org/) , aby sprawdzić, czy w NuGet.org występują jakiekolwiek przerwy.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="cdd6d-144">Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z pomocą techniczną na stronie Szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="cdd6d-145">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="cdd6d-145">Symbol package structure</span></span>

<span data-ttu-id="cdd6d-146">Plik. nupkg będzie dokładnie taki sam, jak dzisiaj, ale plik. snupkg ma następującą charakterystykę:</span><span class="sxs-lookup"><span data-stu-id="cdd6d-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="cdd6d-147">Element. snupkg będzie miał ten sam identyfikator i wersję co odpowiadający element. nupkg.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="cdd6d-148">Plik. snupkg będzie miał dokładną strukturę folderów jako NUPKG dla każdej biblioteki DLL lub EXE z rozróżnieniem, które zamiast bibliotek DLL/exe, odpowiadające im plików PDB zostaną uwzględnione w tej samej hierarchii folderów.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="cdd6d-149">Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pozostawione z snupkg.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="cdd6d-150">Plik. nuspec w pliku. snupkg określi również nowy element PackageType w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="cdd6d-151">Powinien to być określony tylko jeden pakiet.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="cdd6d-152">Jeśli autor zdecyduje się użyć niestandardowych nuspec do kompilowania ich NUPKG i snupkg, snupkg powinien mieć tę samą hierarchię folderów i pliki szczegółowe w 2).</span><span class="sxs-lookup"><span data-stu-id="cdd6d-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="cdd6d-153">```authors```i ```owners``` pole zostanie wykluczone z nuspec snupkg.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="cdd6d-154">Nie należy używać ```<license>``` elementu.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="cdd6d-155">A. snupkg jest objęta tą samą licencją co odpowiadające mu. nupkg.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="cdd6d-156">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cdd6d-156">See Also</span></span>

<span data-ttu-id="cdd6d-157">Rozważ użycie linku źródłowego, aby włączyć debugowanie kodu źródłowego zestawów .NET.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="cdd6d-158">Aby uzyskać więcej informacji, zapoznaj się ze [wskazówkami dotyczącymi linku do źródła](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="cdd6d-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="cdd6d-159">Aby uzyskać więcej informacji na temat pakietów symboli, zapoznaj się z artykułem [debugowanie pakietu NuGet & symbole udoskonalenia](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) projektu Specyfikacja.</span><span class="sxs-lookup"><span data-stu-id="cdd6d-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
