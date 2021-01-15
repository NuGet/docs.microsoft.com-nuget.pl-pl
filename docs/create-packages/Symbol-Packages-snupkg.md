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
ms.openlocfilehash: fbcc035a6b800617f995d3bcebd7e1764aa467b0
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235727"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="b2e12-104">Tworzenie pakietów symboli (. snupkg)</span><span class="sxs-lookup"><span data-stu-id="b2e12-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="b2e12-105">Dobre środowisko debugowania opiera się na obecności symboli debugowania, ponieważ zawierają one krytyczne informacje, takie jak skojarzenie między skompilowanym i źródłowym kodem, nazwami zmiennych lokalnych, śladów stosu i innymi.</span><span class="sxs-lookup"><span data-stu-id="b2e12-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="b2e12-106">Za pomocą pakietów symboli (. snupkg) można dystrybuować te symbole i ulepszać środowisko debugowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="b2e12-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2e12-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2e12-107">Prerequisites</span></span>

<span data-ttu-id="b2e12-108">[nuget.exe v 4.9.0 lub nowszym](https://www.nuget.org/downloads) lub [interfejsu wiersza polecenia dotnet w wersji 2.2.0 lub nowszej](https://www.microsoft.com/net/download/dotnet-core/2.2), który implementuje wymagane [Protokoły NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="b2e12-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="b2e12-109">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="b2e12-109">Creating a symbol package</span></span>

<span data-ttu-id="b2e12-110">Jeśli używasz interfejsu wiersza polecenia dotnet lub MSBuild, musisz ustawić `IncludeSymbols` właściwości i, `SymbolPackageFormat` Aby utworzyć plik. snupkg oprócz pliku. nupkg.</span><span class="sxs-lookup"><span data-stu-id="b2e12-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="b2e12-111">Dodaj następujące właściwości do pliku. csproj:</span><span class="sxs-lookup"><span data-stu-id="b2e12-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="b2e12-112">Lub Określ te właściwości w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="b2e12-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="b2e12-113">lub</span><span class="sxs-lookup"><span data-stu-id="b2e12-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="b2e12-114">Jeśli używasz NuGet.exe, możesz użyć następujących poleceń, aby utworzyć plik. snupkg oprócz pliku. nupkg:</span><span class="sxs-lookup"><span data-stu-id="b2e12-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="b2e12-115">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)Właściwość może mieć jedną z dwóch wartości: `symbols.nupkg` (wartość domyślna) lub `snupkg` .</span><span class="sxs-lookup"><span data-stu-id="b2e12-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="b2e12-116">Jeśli ta właściwość nie zostanie określona, zostanie utworzony starszy pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="b2e12-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="b2e12-117">Starszy format `.symbols.nupkg` jest nadal obsługiwany, ale tylko ze względów zgodności, takich jak pakiety natywne (zobacz [starsze pakiety symboli](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="b2e12-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="b2e12-118">NuGet. serwer symboli organizacji akceptuje tylko nowy format pakietu symboli — `.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="b2e12-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="b2e12-119">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="b2e12-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="b2e12-120">Dla wygody najpierw Zapisz klucz interfejsu API za pomocą narzędzia NuGet (zobacz [Publikowanie pakietu](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="b2e12-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="b2e12-121">Po opublikowaniu pakietu podstawowego w programie nuget.org wypchnij pakiet symboli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="b2e12-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="b2e12-122">Możesz również wypchnąć zarówno podstawowe, jak i w tym samym czasie pakiety symboli przy użyciu poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b2e12-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="b2e12-123">Oba pliki. nupkg i. snupkg muszą znajdować się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="b2e12-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="b2e12-124">Program NuGet opublikuje Oba pakiety w nuget.org. `MyPackage.nupkg` zostanie opublikowany jako pierwszy, a następnie `MyPackage.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="b2e12-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="b2e12-125">Jeśli pakiet symboli nie jest opublikowany, sprawdź, czy źródło NuGet.org zostało skonfigurowane jako `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="b2e12-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="b2e12-126">Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API programu NuGet v3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="b2e12-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="b2e12-127">Serwer symboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="b2e12-127">NuGet.org symbol server</span></span>

<span data-ttu-id="b2e12-128">NuGet.org obsługuje własne repozytorium serwera symboli i akceptuje tylko nowy format pakietu symboli — `.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="b2e12-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="b2e12-129">Odbiorcy pakietu mogą korzystać z symboli opublikowanych na serwerze symboli nuget.org przez dodanie `https://symbols.nuget.org/download/symbols` ich do źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2e12-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="b2e12-130">Aby uzyskać szczegółowe informacje na temat tego procesu, zobacz [Określanie symboli (. pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="b2e12-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="b2e12-131">Ograniczenia pakietu symboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="b2e12-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="b2e12-132">NuGet.org ma następujące ograniczenia dotyczące pakietów symboli:</span><span class="sxs-lookup"><span data-stu-id="b2e12-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="b2e12-133">W pakietach symboli są dozwolone tylko następujące rozszerzenia plików: `.pdb` , `.nuspec` ,,, `.xml` `.psmdcp` `.rels` , `.p7s`</span><span class="sxs-lookup"><span data-stu-id="b2e12-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="b2e12-134">Tylko zarządzane [plików PDB przenośne](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obsługiwane przez pakiet NuGet. serwer symboli w organizacji.</span><span class="sxs-lookup"><span data-stu-id="b2e12-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="b2e12-135">Plików PDB i skojarzone z nimi biblioteki DLL NUPKG muszą być kompilowane przy użyciu kompilatora w programie Visual Studio w wersji 15,9 lub nowszej (zobacz [skrót kryptografii PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="b2e12-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="b2e12-136">W przypadku, gdy te ograniczenia nie są spełnione, pakiety symboli opublikowane w programie NuGet.org będą kończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="b2e12-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="b2e12-137">Natywne projekty, takie jak projekty C++, tworzą plików PDB systemu Windows zamiast przenośnych plików PDB.</span><span class="sxs-lookup"><span data-stu-id="b2e12-137">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="b2e12-138">Nie są one obsługiwane przez pakiet NuGet. serwer symboli w organizacji.</span><span class="sxs-lookup"><span data-stu-id="b2e12-138">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="b2e12-139">Zamiast tego użyj [starszych pakietów symboli](Symbol-Packages.md) .</span><span class="sxs-lookup"><span data-stu-id="b2e12-139">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="b2e12-140">Walidacja i indeksowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="b2e12-140">Symbol package validation and indexing</span></span>

<span data-ttu-id="b2e12-141">Pakiety symboli opublikowane w [NuGet.org](https://www.nuget.org/) przechodzą kilka walidacji, w tym skanowanie złośliwego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="b2e12-141">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="b2e12-142">Jeśli pakiet nie zostanie zweryfikowany, na stronie szczegółów pakietu zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="b2e12-142">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="b2e12-143">Ponadto właściciele pakietu otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu rozwiązywania zidentyfikowanych problemów.</span><span class="sxs-lookup"><span data-stu-id="b2e12-143">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="b2e12-144">Gdy pakiet symboli przeszedł wszystkie walidacje, symbole będą indeksowane przez NuGet. serwery symboli organizacji i będą dostępne do użycia.</span><span class="sxs-lookup"><span data-stu-id="b2e12-144">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="b2e12-145">Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa 15 minut.</span><span class="sxs-lookup"><span data-stu-id="b2e12-145">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="b2e12-146">Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.NuGet.org](https://status.nuget.org/) , aby sprawdzić, czy w NuGet.org występują jakiekolwiek przerwy.</span><span class="sxs-lookup"><span data-stu-id="b2e12-146">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="b2e12-147">Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z pomocą techniczną na stronie Szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="b2e12-147">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="b2e12-148">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="b2e12-148">Symbol package structure</span></span>

<span data-ttu-id="b2e12-149">Pakiet symboli (. snupkg) ma następującą charakterystykę:</span><span class="sxs-lookup"><span data-stu-id="b2e12-149">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="b2e12-150">Element. snupkg ma ten sam identyfikator i wersję, co odpowiadający mu pakiet NuGet (. nupkg).</span><span class="sxs-lookup"><span data-stu-id="b2e12-150">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="b2e12-151">Plik. snupkg ma taką samą strukturę folderu jak odpowiadająca jej. nupkg dla każdej biblioteki DLL lub EXE z rozróżnieniem, które zamiast bibliotek DLL/exe, odpowiadające im plików PDB zostaną uwzględnione w tej samej hierarchii folderów.</span><span class="sxs-lookup"><span data-stu-id="b2e12-151">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="b2e12-152">Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pozostawione z snupkg.</span><span class="sxs-lookup"><span data-stu-id="b2e12-152">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="b2e12-153">Plik NUSPEC pakietu symboli ma `SymbolsPackage` Typ pakietu:</span><span class="sxs-lookup"><span data-stu-id="b2e12-153">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="b2e12-154">Jeśli autor zdecyduje się użyć niestandardowych nuspec do kompilowania ich NUPKG i snupkg, snupkg powinien mieć tę samą hierarchię folderów i pliki szczegółowe w 2).</span><span class="sxs-lookup"><span data-stu-id="b2e12-154">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="b2e12-155">Następujące pola zostaną wykluczone z nuspec snupkg: ```authors``` ,,,, ```owners``` ```requireLicenseAcceptance``` ```license type``` ```licenseUrl``` i  ```icon``` .</span><span class="sxs-lookup"><span data-stu-id="b2e12-155">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="b2e12-156">Nie należy używać ```<license>``` elementu.</span><span class="sxs-lookup"><span data-stu-id="b2e12-156">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="b2e12-157">A. snupkg jest objęta tą samą licencją co odpowiadające mu. nupkg.</span><span class="sxs-lookup"><span data-stu-id="b2e12-157">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="b2e12-158">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b2e12-158">See also</span></span>

<span data-ttu-id="b2e12-159">Rozważ użycie linku źródłowego, aby włączyć debugowanie kodu źródłowego zestawów .NET.</span><span class="sxs-lookup"><span data-stu-id="b2e12-159">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="b2e12-160">Aby uzyskać więcej informacji, zapoznaj się ze [wskazówkami dotyczącymi linku do źródła](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="b2e12-160">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="b2e12-161">Aby uzyskać więcej informacji na temat pakietów symboli, zapoznaj się z artykułem [debugowanie pakietu NuGet & symbole udoskonalenia](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) projektu Specyfikacja.</span><span class="sxs-lookup"><span data-stu-id="b2e12-161">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
