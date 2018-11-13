---
title: Jak utworzyć pakiety symboli NuGet
description: Jak utworzyć pakiety NuGet, które zawierają tylko symbole, aby zapewnić obsługę debugowania innych pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3321cba9082eb35b53ba693e246db18e5d8e187b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580262"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="59ff4-103">Tworzenie pakietów symbol (starsza wersja)</span><span class="sxs-lookup"><span data-stu-id="59ff4-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="59ff4-104">Nowy format zalecane pakiety symboli jest .snupkg.</span><span class="sxs-lookup"><span data-stu-id="59ff4-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="59ff4-105">Zobacz [tworzenia pakietów symbol (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="59ff4-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="59ff4-106">. symbols.nupkg nadal jest obsługiwany, ale tylko ze względu na zgodność.</span><span class="sxs-lookup"><span data-stu-id="59ff4-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="59ff4-107">Oprócz tworzenia pakietów nuget.org lub innych źródeł, NuGet również obsługuje tworzenie skojarzone pakiety symboli i publikowania ich w repozytorium SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="59ff4-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="59ff4-108">Konsumenci pakiet można następnie dodać `https://nuget.smbsrc.net` źródła symbol w programie Visual Studio, umożliwia przechodzenie do pakietu kodu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59ff4-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="59ff4-109">Zobacz [określanie plików symboli (.pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) szczegółowe informacje na temat tego procesu.</span><span class="sxs-lookup"><span data-stu-id="59ff4-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="59ff4-110">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="59ff4-110">Creating a symbol package</span></span>

<span data-ttu-id="59ff4-111">Aby utworzyć pakiet symboli, postępuj zgodnie z tych konwencji:</span><span class="sxs-lookup"><span data-stu-id="59ff4-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="59ff4-112">Nazwij pakiet główny (Twoim kodem) `{identifier}.nupkg` i Dołącz wszystkie pliki z wyjątkiem `.pdb` plików.</span><span class="sxs-lookup"><span data-stu-id="59ff4-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="59ff4-113">Nazwij pakiet symboli `{identifier}.symbols.nupkg` i obejmuje zestaw bibliotek DLL, `.pdb` pliki, pliki XMLDOC, pliki źródłowe (zobacz w kolejnych sekcjach).</span><span class="sxs-lookup"><span data-stu-id="59ff4-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="59ff4-114">Możesz utworzyć oba pakiety za pomocą `-Symbols` opcji z `.nuspec` pliku lub pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="59ff4-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="59ff4-115">Należy pamiętać, że `pack` wymaga platformy Mono 4.4.2 w systemie Mac OS X, a nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="59ff4-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="59ff4-116">Na komputerze Mac, należy także przekonwertować nazwy Windows ścieżek w `.nuspec` plik do ścieżki stylu systemu Unix.</span><span class="sxs-lookup"><span data-stu-id="59ff4-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="59ff4-117">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="59ff4-117">Symbol package structure</span></span>

<span data-ttu-id="59ff4-118">Pakiet symboli można wskazać wiele platform docelowych w taki sam sposób, który wykonuje pakietu biblioteki, więc struktury `lib` folder powinien być dokładnie takie same, jak pakiet podstawowego, tylko tym `.pdb` plików wraz z biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="59ff4-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="59ff4-119">Na przykład pakiet symboli, który jest przeznaczony dla .NET 4.0 i Silverlight 4 będą mieć ten układ:</span><span class="sxs-lookup"><span data-stu-id="59ff4-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="59ff4-120">Pliki źródłowe następnie są umieszczane w oddzielnym folderze specjalnym, o nazwie `src`, które należy wykonać względne struktury repozytorium źródłowym.</span><span class="sxs-lookup"><span data-stu-id="59ff4-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="59ff4-121">Jest to spowodowane plików PDB zawierać ścieżek bezwzględnych do plików źródłowych, używana do kompilowania zgodnych bibliotek DLL i muszą one można znaleźć w procesie publikowania.</span><span class="sxs-lookup"><span data-stu-id="59ff4-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="59ff4-122">Ścieżki podstawowej (Wspólny prefiks ścieżki) może być wycięte. Rozważmy na przykład biblioteki, utworzony na podstawie tych plików:</span><span class="sxs-lookup"><span data-stu-id="59ff4-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="59ff4-123">Z wyjątkiem `lib` folderze pakiet symboli musi zawierać ten układ:</span><span class="sxs-lookup"><span data-stu-id="59ff4-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="59ff4-124">Odwołujące się do plików w nuspec</span><span class="sxs-lookup"><span data-stu-id="59ff4-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="59ff4-125">Mogą być wbudowane pakiet symboli, konwencje ze struktury folderów, zgodnie z opisem w poprzedniej sekcji, lub podając jego zawartość w `files` sekcji manifestu.</span><span class="sxs-lookup"><span data-stu-id="59ff4-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="59ff4-126">Na przykład, aby utworzyć pakiet pokazano w poprzedniej sekcji, należy użyć następującego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="59ff4-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="59ff4-127">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="59ff4-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="59ff4-128">Do wypychania pakietów nuget.org, należy użyć [nuget.exe verze 4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="59ff4-128">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="59ff4-129">Dla wygody, najpierw zapisać swój klucz interfejsu API z NuGet (zobacz [publikowanie pakietu](../create-packages/publish-a-package.md), która będzie stosowana do nuget.org i symbolsource.org, ponieważ symbolsource.org sprawdzi się z repozytorium nuget.org, aby sprawdzić, czy jesteś właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="59ff4-129">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="59ff4-130">Po opublikowaniu pakiet podstawowego na stronie nuget.org, Wypchnij pakiet symboli w następujący sposób, który będzie automatycznie używać symbolsource.org jako element docelowy z powodu `.symbols` w nazwie pliku:</span><span class="sxs-lookup"><span data-stu-id="59ff4-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="59ff4-131">Aby opublikować w repozytorium innego symbolu lub wypychania pakiet symboli, które nie są zgodne z konwencją nazewnictwa, użyj `-Source` opcji:</span><span class="sxs-lookup"><span data-stu-id="59ff4-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="59ff4-132">Można również wypchnąć podstawowych i symboli pakietów do obu repozytoriów, w tym samym czasie przy użyciu następujących:</span><span class="sxs-lookup"><span data-stu-id="59ff4-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="59ff4-133">Nuget.exe 4.5.0 lub powyżej symbole pakiety nie zostaną automatycznie wypchnięte do symbolsource.org. Będziesz potrzebować do wypychania pakietów symbole oddzielnie, zgodnie z opisem w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="59ff4-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="59ff4-134">W tym przypadku będzie publikować NuGet `MyPackage.symbols.nupkg`, jeśli jest obecna, aby https://nuget.smbsrc.net/ (URL wypychania dla symbolsource.org), po publikuje pakiet główny na stronie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="59ff4-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="59ff4-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="59ff4-135">See Also</span></span>

<span data-ttu-id="59ff4-136">[Przejście do nowego aparatu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="59ff4-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
