---
title: Jak opublikować pakiety symboli NuGet przy użyciu nowego formatu pakietu symboli '.snupkg'| Dokumenty firmy Microsoft
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak utworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, debugowanie pakietu NuGet, obsługa debugowania NuGet, symbole pakietów, konwencje pakietów symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380421"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="25440-104">Tworzenie pakietów symboli (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="25440-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="25440-105">Dobre środowisko debugowania opiera się na obecności symboli debugowania, ponieważ zapewniają one krytyczne informacje, takie jak skojarzenie między skompilowanym i kodem źródłowym, nazwy zmiennych lokalnych, ślady stosu i więcej.</span><span class="sxs-lookup"><span data-stu-id="25440-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="25440-106">Można użyć pakietów symboli (.snupkg) do dystrybucji tych symboli i poprawić środowisko debugowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="25440-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25440-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="25440-107">Prerequisites</span></span>

<span data-ttu-id="25440-108">[nuget.exe v4.9.0 lub powyżej](https://www.nuget.org/downloads) lub [dotnet CLI v2.2.0 lub wyższy](https://www.microsoft.com/net/download/dotnet-core/2.2), które implementują wymagane [protokoły NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="25440-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="25440-109">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="25440-109">Creating a symbol package</span></span>

<span data-ttu-id="25440-110">Jeśli używasz dotnet CLI lub MSBuild, musisz `IncludeSymbols` `SymbolPackageFormat` ustawić właściwości i, aby utworzyć plik .snupkg oprócz pliku .nupkg.</span><span class="sxs-lookup"><span data-stu-id="25440-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="25440-111">Dodaj następujące właściwości do pliku csproj:</span><span class="sxs-lookup"><span data-stu-id="25440-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="25440-112">Możesz też określić te właściwości w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="25440-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="25440-113">lub</span><span class="sxs-lookup"><span data-stu-id="25440-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="25440-114">Jeśli używasz programu NuGet.exe, możesz użyć następujących poleceń, aby utworzyć plik .snupkg oprócz pliku nupkg:</span><span class="sxs-lookup"><span data-stu-id="25440-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="25440-115">Właściwość [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) może mieć jedną `symbols.nupkg` z dwóch wartości: (domyślnie) lub `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="25440-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="25440-116">Jeśli ta właściwość nie jest określona, zostanie utworzony starszy pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="25440-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="25440-117">Starszy format `.symbols.nupkg` jest nadal obsługiwany, ale tylko ze względu na zgodność (patrz [Starsze pakiety symboli).](Symbol-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="25440-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="25440-118">Serwer symboli NuGet.org akceptuje tylko nowy format `.snupkg`pakietu symboli - .</span><span class="sxs-lookup"><span data-stu-id="25440-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="25440-119">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="25440-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="25440-120">Dla wygody najpierw zapisz klucz interfejsu API za pomocą programu NuGet (zobacz [publikowanie pakietu).](../nuget-org/publish-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="25440-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="25440-121">Po opublikowaniu pakietu podstawowego do nuget.org wypchnij pakiet symboli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="25440-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="25440-122">Można również wypchnąć pakiety podstawowe i symbole w tym samym czasie za pomocą polecenia poniżej.</span><span class="sxs-lookup"><span data-stu-id="25440-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="25440-123">Zarówno pliki .nupkg, jak i .snupkg muszą znajdować się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="25440-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="25440-124">NuGet opublikuje oba pakiety do nuget.org. `MyPackage.nupkg` zostanie opublikowana jako pierwsza, a następnie `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="25440-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="25440-125">Jeśli pakiet symboli nie został opublikowany, sprawdź, czy źródło NuGet.org zostało `https://api.nuget.org/v3/index.json`skonfigurowane jako .</span><span class="sxs-lookup"><span data-stu-id="25440-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="25440-126">Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="25440-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="25440-127">Serwer NuGet.org symboli</span><span class="sxs-lookup"><span data-stu-id="25440-127">NuGet.org symbol server</span></span>

<span data-ttu-id="25440-128">NuGet.org obsługuje własne repozytorium serwerowe symboli i akceptuje tylko nowy `.snupkg`format pakietu symboli - .</span><span class="sxs-lookup"><span data-stu-id="25440-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="25440-129">Konsumenci pakietów mogą używać symboli opublikowanych do nuget.org `https://symbols.nuget.org/download/symbols` serwera symboli, dodając do swoich źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25440-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="25440-130">Zobacz [Określanie symbolu (pdb) i plików źródłowych w debugerze programu Visual Studio, aby](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) uzyskać szczegółowe informacje na temat tego procesu.</span><span class="sxs-lookup"><span data-stu-id="25440-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="25440-131">Ograniczenia pakietu NuGet.org symboli</span><span class="sxs-lookup"><span data-stu-id="25440-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="25440-132">NuGet.org ma następujące ograniczenia dla pakietów symboli:</span><span class="sxs-lookup"><span data-stu-id="25440-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="25440-133">W pakietach symboli dozwolone są tylko `.pdb` `.nuspec`następujące `.xml` `.psmdcp`rozszerzenia `.rels`plików: , , , ,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="25440-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="25440-134">Tylko zarządzane [przenośne kontrolery domeny](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obsługiwane na serwerze symboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="25440-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="25440-135">Biblioteki DLL i skojarzone z nimi biblioteki DLL .nupkg muszą być budowane za pomocą kompilatora w programie Visual Studio w wersji 15.9 lub nowszej (zobacz [skrót kryptograficzny PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="25440-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="25440-136">Pakiety symboli opublikowane w NuGet.org zakończy się niepowodzeniem sprawdzania poprawności, jeśli te ograniczenia nie są spełnione.</span><span class="sxs-lookup"><span data-stu-id="25440-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="25440-137">Sprawdzanie poprawności i indeksowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="25440-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="25440-138">Pakiety symboli opublikowane [w celu NuGet.org](https://www.nuget.org/) przechodzą kilka weryfikacji, w tym skanowanie złośliwego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="25440-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="25440-139">Jeśli pakiet nie powiedzie się sprawdzanie poprawności, jego szczegóły pakietu strona wyświetli komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="25440-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="25440-140">Ponadto właściciele pakietu otrzymają wiadomość e-mail z instrukcjami dotyczącymi rozwiązywania zidentyfikowanych problemów.</span><span class="sxs-lookup"><span data-stu-id="25440-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="25440-141">Gdy pakiet symboli przeszedł wszystkie weryfikacje, symbole zostaną zindeksowane przez serwery symboli NuGet.org i będą dostępne do użycia.</span><span class="sxs-lookup"><span data-stu-id="25440-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="25440-142">Sprawdzanie poprawności i indeksowanie pakietów zwykle trwa mniej niż 15 minut.</span><span class="sxs-lookup"><span data-stu-id="25440-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="25440-143">Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź [status.nuget.org,](https://status.nuget.org/) aby sprawdzić, czy NuGet.org występują przerwy.</span><span class="sxs-lookup"><span data-stu-id="25440-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="25440-144">Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie szczegółów pakietu.</span><span class="sxs-lookup"><span data-stu-id="25440-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="25440-145">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="25440-145">Symbol package structure</span></span>

<span data-ttu-id="25440-146">Pakiet symboli (.snupkg) ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="25440-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="25440-147">.snupkg ma ten sam identyfikator i wersję co odpowiadający mu pakiet NuGet (.nupkg).</span><span class="sxs-lookup"><span data-stu-id="25440-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="25440-148">.snupkg ma taką samą strukturę folderów jak odpowiadający jej .nupkg dla dowolnych plików DLL lub EXE z rozróżnieniem, że zamiast bibliotek DLL/EXE, ich odpowiednie pliki PDB zostaną uwzględnione w tej samej hierarchii folderów.</span><span class="sxs-lookup"><span data-stu-id="25440-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="25440-149">Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pominięte w snupkg.</span><span class="sxs-lookup"><span data-stu-id="25440-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="25440-150">Plik .nuspec pakietu symboli `SymbolsPackage` ma typ pakietu:</span><span class="sxs-lookup"><span data-stu-id="25440-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="25440-151">Jeśli autor zdecyduje się użyć niestandardowego nuspec do zbudowania nupkg i snupkg, snupkg powinien mieć tę samą hierarchię folderów i pliki wyszczególnione w 2).</span><span class="sxs-lookup"><span data-stu-id="25440-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="25440-152">Z nuspec snupkg wyłączone ```authors```będą następujące pola: ```owners``` ```requireLicenseAcceptance```, ```license type``` ```licenseUrl```, ```icon```, , i .</span><span class="sxs-lookup"><span data-stu-id="25440-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="25440-153">Nie należy ```<license>``` używać elementu.</span><span class="sxs-lookup"><span data-stu-id="25440-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="25440-154">A .snupkg jest objęty tą samą licencją co odpowiadający mu plik .nupkg.</span><span class="sxs-lookup"><span data-stu-id="25440-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="25440-155">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="25440-155">See also</span></span>

<span data-ttu-id="25440-156">Należy rozważyć użycie łącza źródłowego, aby włączyć debugowanie kodu źródłowego zestawów .NET.</span><span class="sxs-lookup"><span data-stu-id="25440-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="25440-157">Aby uzyskać więcej informacji, zapoznaj się ze [wskazówkami dotyczącymi łącza źródłowego](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="25440-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="25440-158">Aby uzyskać więcej informacji na temat pakietów symboli, zapoznaj się z [nuget pakiet debugowania & symbole ulepszenia specyfikacji](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) projektu.</span><span class="sxs-lookup"><span data-stu-id="25440-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
