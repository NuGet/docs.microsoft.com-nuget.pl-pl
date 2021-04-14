---
title: Jak publikować pakiety symboli NuGet przy użyciu nowego formatu pakietu symboli ".snupkg" | Microsoft Docs
author: JonDouglas
ms.author: jodou
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak tworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, debugowanie pakietów NuGet, obsługa debugowania NuGet, symbole pakietów, konwencje pakietów symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: a62996a28348bf95e4581af180597d72cd5aa298
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387338"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="ac7ad-104">Tworzenie pakietów symboli (snupkg)</span><span class="sxs-lookup"><span data-stu-id="ac7ad-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="ac7ad-105">Dobre środowisko debugowania opiera się na obecności symboli debugowania, ponieważ zapewniają one krytyczne informacje, takie jak skojarzenie między skompilowanym i kodem źródłowym, nazwy zmiennych lokalnych, ślady stosu i inne.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="ac7ad-106">Za pomocą pakietów symboli (snupkg) można rozpowszechniać te symbole i ulepszać środowisko debugowania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

> <span data-ttu-id="ac7ad-107">Należy pamiętać, że pakiet symboli nie jest jedyną strategią, aby udostępnić symbole debugowania klientom biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-107">Note that symbol package isn't the only strategy to make the debug symbols available to the consumers of your library.</span></span> <span data-ttu-id="ac7ad-108">Można je również [mieć w `embed` ](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) obiekcie lub z `dll` `exe` następującą właściwością projektu:`<DebugType>embedded</DebugType>`</span><span class="sxs-lookup"><span data-stu-id="ac7ad-108">It's also [possible to `embed`](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) them in the `dll` or `exe` with the following project property: `<DebugType>embedded</DebugType>`</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac7ad-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ac7ad-109">Prerequisites</span></span>

<span data-ttu-id="ac7ad-110">[nuget.exe w wersji 4.9.0](https://www.nuget.org/downloads) lub powyższej albo interfejs wiersza polecenia dotnet w wersji [2.2.0](https://www.microsoft.com/net/download/dotnet-core/2.2)lub wersji powyżej , które implementują wymagane [protokoły NuGet.](../api/nuget-protocols.md)</span><span class="sxs-lookup"><span data-stu-id="ac7ad-110">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="ac7ad-111">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="ac7ad-111">Creating a symbol package</span></span>

<span data-ttu-id="ac7ad-112">Jeśli używasz interfejsu wiersza polecenia dotnet lub programu MSBuild, musisz ustawić właściwości i , aby oprócz pliku nupkg utworzyć plik `IncludeSymbols` `SymbolPackageFormat` zippkg.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-112">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="ac7ad-113">Dodaj następujące właściwości do pliku csproj:</span><span class="sxs-lookup"><span data-stu-id="ac7ad-113">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="ac7ad-114">Możesz też określić następujące właściwości w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="ac7ad-114">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="ac7ad-115">lub</span><span class="sxs-lookup"><span data-stu-id="ac7ad-115">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="ac7ad-116">Jeśli używasz narzędzia NuGet.exe, możesz użyć następujących poleceń, aby utworzyć plik zippkg oprócz pliku .nupkg:</span><span class="sxs-lookup"><span data-stu-id="ac7ad-116">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="ac7ad-117">Właściwość [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) może mieć jedną z dwóch wartości: `symbols.nupkg` (wartość domyślna) lub `snupkg` .</span><span class="sxs-lookup"><span data-stu-id="ac7ad-117">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="ac7ad-118">Jeśli ta właściwość nie zostanie określona, zostanie utworzony starszy pakiet symboli.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-118">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="ac7ad-119">Starszy format jest nadal obsługiwany, ale tylko ze względu na zgodność, na przykład pakiety `.symbols.nupkg` natywne (zobacz [Starsze pakiety symboli).](Symbol-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="ac7ad-119">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="ac7ad-120">Serwer symboli nuGet.org akceptuje tylko nowy format pakietu symboli — `.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="ac7ad-120">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="ac7ad-121">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="ac7ad-121">Publishing a symbol package</span></span>

1. <span data-ttu-id="ac7ad-122">Dla wygody najpierw zapisz klucz interfejsu API za pomocą pakietu NuGet (zobacz [publikowanie pakietu](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="ac7ad-122">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="ac7ad-123">Po opublikowaniu pakietu podstawowego w nuget.org wypchnąć pakiet symboli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-123">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="ac7ad-124">Możesz również wypchnąć jednocześnie pakiety podstawowe i symboli za pomocą poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-124">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="ac7ad-125">Zarówno pliki .nupkg, jak i .tabpkg muszą być obecne w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-125">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="ac7ad-126">NuGet opublikuje oba pakiety w nuget.org. `MyPackage.nupkg` Zostanie najpierw opublikowany, a następnie `MyPackage.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="ac7ad-126">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="ac7ad-127">Jeśli pakiet symboli nie został opublikowany, sprawdź, czy skonfigurowano źródło NuGet.org jako `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="ac7ad-127">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="ac7ad-128">Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API NuGet w wersji 3.](../api/overview.md#versioning)</span><span class="sxs-lookup"><span data-stu-id="ac7ad-128">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="ac7ad-129">NuGet.org serwera symboli</span><span class="sxs-lookup"><span data-stu-id="ac7ad-129">NuGet.org symbol server</span></span>

<span data-ttu-id="ac7ad-130">NuGet.org obsługuje własne repozytorium serwerów symboli i akceptuje tylko nowy format pakietu symboli — `.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="ac7ad-130">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="ac7ad-131">Odbiorcy pakietów mogą używać symboli opublikowanych na serwerze symboli nuget.org przez dodanie ich do źródeł symboli w u Visual Studio, co umożliwia przechodzenie do kodu pakietu w Visual Studio `https://symbols.nuget.org/download/symbols` debugerze.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-131">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="ac7ad-132">Szczegółowe informacje na temat tego procesu można znaleźć w temacie [Specify symbol (.pdb) and source files in the Visual Studio debugger (Określanie plików symboli (pdb)](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) i plików źródłowych w Visual Studio debugerze.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-132">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="ac7ad-133">NuGet.org ograniczeń pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="ac7ad-133">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="ac7ad-134">NuGet.org ma następujące ograniczenia dotyczące pakietów symboli:</span><span class="sxs-lookup"><span data-stu-id="ac7ad-134">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="ac7ad-135">W pakietach symboli dozwolone są tylko następujące rozszerzenia plików: `.pdb` , , , , , `.nuspec` `.xml` `.psmdcp` `.rels` , `.p7s`</span><span class="sxs-lookup"><span data-stu-id="ac7ad-135">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="ac7ad-136">Na serwerze [symboli](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) nuGet.org są obsługiwane tylko zarządzane przenośne pliki PDB.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-136">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="ac7ad-137">Pliki PDB i skojarzone z nimi biblioteki DLL nupkg muszą zostać skumulowane przy użyciu kompilatora w wersji Visual Studio 15.9 lub nowszej (zobacz skrót kryptograficzny pliku [PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="ac7ad-137">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="ac7ad-138">Pakiety symboli opublikowane w NuGet.org sprawdzanie poprawności nie powiedzie się, jeśli te ograniczenia nie zostaną spełnione.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-138">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="ac7ad-139">Projekty natywne, takie jak projekty języka C++, tworzyć pliki PDB systemu Windows zamiast przenośnych plików PDB.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-139">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="ac7ad-140">Nie są one obsługiwane przez serwer symboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-140">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="ac7ad-141">Zamiast tego użyj [starszych pakietów symboli.](Symbol-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="ac7ad-141">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="ac7ad-142">Walidacja i indeksowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="ac7ad-142">Symbol package validation and indexing</span></span>

<span data-ttu-id="ac7ad-143">Pakiety symboli opublikowane [w NuGet.org](https://www.nuget.org/) przechodzą kilka weryfikacji, w tym skanowanie w poszukiwaniu złośliwego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-143">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="ac7ad-144">Jeśli sprawdzenie poprawności pakietu zakończy się niepowodzeniem, na stronie szczegółów pakietu zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-144">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="ac7ad-145">Ponadto właściciele pakietu otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu rozwiązania zidentyfikowanych problemów.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-145">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="ac7ad-146">Po zatwierdzeniu wszystkich weryfikacji przez pakiet symboli symbole zostaną zindeksowane przez serwery symboli NuGet.org i będą dostępne do użycia.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-146">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="ac7ad-147">Walidacja i indeksowanie pakietów zwykle trwa poniżej 15 minut.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-147">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="ac7ad-148">Jeśli publikowanie pakietów trwa dłużej niż oczekiwano, odwiedź [status.nuget.org,](https://status.nuget.org/) aby sprawdzić, NuGet.org występują jakieś przerwy w działaniu.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-148">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="ac7ad-149">Jeśli wszystkie systemy są operacyjne i pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do witryny nuget.org i skontaktuj się z nami przy użyciu linku Skontaktuj się z pomocą techniczną na stronie szczegółów pakietu.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-149">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="ac7ad-150">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="ac7ad-150">Symbol package structure</span></span>

<span data-ttu-id="ac7ad-151">Pakiet symboli (snupkg) ma następujące cechy:</span><span class="sxs-lookup"><span data-stu-id="ac7ad-151">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="ac7ad-152">Pakiet .snupkg ma ten sam identyfikator i wersję co odpowiadający mu pakiet NuGet (nupkg).</span><span class="sxs-lookup"><span data-stu-id="ac7ad-152">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="ac7ad-153">Plik .snupkg ma taką samą strukturę folderów jak odpowiadający mu plik nupkg dla wszystkich plików DLL lub EXE z różnicą, że zamiast plików DLL/EXE odpowiednie pliki PDB zostaną uwzględnione w tej samej hierarchii folderów.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-153">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="ac7ad-154">Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pozostawione poza plikiem tabupkg.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-154">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="ac7ad-155">Plik nuspec pakietu symboli ma `SymbolsPackage` typ pakietu:</span><span class="sxs-lookup"><span data-stu-id="ac7ad-155">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="ac7ad-156">Jeśli autor zdecyduje się na użycie niestandardowego programu nuspec do skompilowania swoich plików nupkg i snupkg, pakiet snupkg powinien mieć tę samą hierarchię folderów i pliki szczegółowo opisane w 2).</span><span class="sxs-lookup"><span data-stu-id="ac7ad-156">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="ac7ad-157">Następujące pola zostaną wykluczone z nuspec tego nuspec: ```authors``` , , , , i ```owners``` ```requireLicenseAcceptance``` ```license type``` ```licenseUrl```  ```icon``` .</span><span class="sxs-lookup"><span data-stu-id="ac7ad-157">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="ac7ad-158">Nie używaj ```<license>``` elementu .</span><span class="sxs-lookup"><span data-stu-id="ac7ad-158">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="ac7ad-159">Pakiet .snupkg jest objęty taką samą licencją jak odpowiedni .nupkg.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-159">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="ac7ad-160">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ac7ad-160">See also</span></span>

<span data-ttu-id="ac7ad-161">Rozważ użycie linku źródłowego, aby włączyć debugowanie kodu źródłowego zestawów .NET.</span><span class="sxs-lookup"><span data-stu-id="ac7ad-161">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="ac7ad-162">Aby uzyskać więcej informacji, zapoznaj się ze [wskazówkami linku źródłowego](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="ac7ad-162">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="ac7ad-163">Aby uzyskać więcej informacji na temat pakietów symboli, zapoznaj się ze specyfikacją projektu Debugowanie pakietów [NuGet & symboli.](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)</span><span class="sxs-lookup"><span data-stu-id="ac7ad-163">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>