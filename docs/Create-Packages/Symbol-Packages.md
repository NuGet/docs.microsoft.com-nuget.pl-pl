---
title: Tworzenie pakietów NuGet symbol
description: Jak tworzyć pakiety NuGet, które zawierają tylko symbole, aby zapewnić obsługę debugowania innych pakietów NuGet w programie Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cf8761ac4c994d864cd49a8fb31b3be626d4c0a6
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="88612-103">Tworzenie pakietów — symbol</span><span class="sxs-lookup"><span data-stu-id="88612-103">Creating symbol packages</span></span>

<span data-ttu-id="88612-104">Oprócz tworzenia pakietów dla nuget.org lub innych źródeł, NuGet również obsługuje tworzenie skojarzone pakiety symboli i opublikować go do repozytorium SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="88612-104">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="88612-105">Konsumenci pakiet można następnie dodać `https://nuget.smbsrc.net` źródła symbol w programie Visual Studio, umożliwia wykonywanie krok po kroku do pakietu kodu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88612-105">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="88612-106">Zobacz [Określ symboli (.pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) szczegółowe informacje na temat tego procesu.</span><span class="sxs-lookup"><span data-stu-id="88612-106">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="88612-107">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="88612-107">Creating a symbol package</span></span>

<span data-ttu-id="88612-108">Aby utworzyć pakiet symboli, zgodne z konwencjami te:</span><span class="sxs-lookup"><span data-stu-id="88612-108">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="88612-109">Nazwa podstawowego pakietu (swoim własnym kodem) `{identifier}.nupkg` i zawiera wszystkie pliki z wyjątkiem `.pdb` plików.</span><span class="sxs-lookup"><span data-stu-id="88612-109">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="88612-110">Nazwa pakietu symboli `{identifier}.symbols.nupkg` i obejmują używanemu zestawowi biblioteki DLL, `.pdb` plików, pliki XMLDOC, pliki źródłowe (zobacz w kolejnych sekcjach).</span><span class="sxs-lookup"><span data-stu-id="88612-110">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="88612-111">Możesz utworzyć oba pakiety z `-Symbols` opcji, albo z `.nuspec` pliku lub pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="88612-111">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="88612-112">Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="88612-112">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="88612-113">Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.</span><span class="sxs-lookup"><span data-stu-id="88612-113">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="88612-114">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="88612-114">Symbol package structure</span></span>

<span data-ttu-id="88612-115">Pakiet symboli można kierować wiele docelowych platform w taki sam sposób, który wykonuje pakiet biblioteki, dlatego struktury `lib` folder powinien być dokładnie taki sam jak podstawowy pakiet, tylko włączając `.pdb` pliki z biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="88612-115">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="88612-116">Na przykład pakiet symboli, przeznaczonego dla programu .NET 4.0 i Silverlight 4 byłyby ten układ:</span><span class="sxs-lookup"><span data-stu-id="88612-116">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="88612-117">Pliki źródłowe następnie są umieszczane w oddzielnym folderze specjalne o nazwie `src`, które należy wykonać względną struktury repozytorium źródła.</span><span class="sxs-lookup"><span data-stu-id="88612-117">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="88612-118">To dlatego PDB zawierają bezwzględnej ścieżki do plików źródłowych, używana do kompilowania zgodne biblioteki DLL i muszą można znaleźć w procesie publikowania.</span><span class="sxs-lookup"><span data-stu-id="88612-118">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="88612-119">Podstawowa ścieżka (wspólnej ścieżki prefiks) mogą być usunięte wychodzących. Rozważmy na przykład biblioteki zbudowane na podstawie tych plików:</span><span class="sxs-lookup"><span data-stu-id="88612-119">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="88612-120">Z wyjątkiem `lib` folderu, pakiet symboli musi zawierać ten układ:</span><span class="sxs-lookup"><span data-stu-id="88612-120">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="88612-121">Odwołujące się do plików w plik nuspec</span><span class="sxs-lookup"><span data-stu-id="88612-121">Referring to files in the nuspec</span></span>

<span data-ttu-id="88612-122">Pakiet symboli mogą być wbudowane w Konwencji z struktury folderów, zgodnie z opisem w poprzedniej sekcji, lub podając jego zawartość w `files` sekcji manifestu.</span><span class="sxs-lookup"><span data-stu-id="88612-122">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="88612-123">Na przykład, aby utworzyć pakiet wyświetlone w poprzedniej sekcji, należy użyć następującego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="88612-123">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="88612-124">Publikowania pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="88612-124">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="88612-125">Pakiety wypychania do nuget.org musi używać [nuget.exe v4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="88612-125">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="88612-126">Dla wygody, najpierw zapisać klucz interfejsu API z programem NuGet (zobacz [opublikowania pakietu](../create-packages/publish-a-package.md), która będzie stosowana do nuget.org i symbolsource.org, ponieważ symbolsource.org będzie sprawdzać z nuget.org do sprawdzenia, czy jesteś właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="88612-126">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="88612-127">Po opublikowaniu pakietu podstawowego do nuget.org, push pakietu symboli, które będą automatycznie używać symbolsource.org jako element docelowy z powodu `.symbols` w nazwie pliku:</span><span class="sxs-lookup"><span data-stu-id="88612-127">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="88612-128">Z nuget.exe 4.5.0 lub powyżej symbole pakiety nie są automatycznie przypisany do symbolsource.org. Będzie potrzebny do dystrybuowania pakietów symbole oddzielnie zgodnie z objaśnieniem w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="88612-128">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

3. <span data-ttu-id="88612-129">Publikowanie do repozytorium inny symbol lub push pakietu symboli, który nie będzie zgodna z konwencją nazewnictwa, należy użyć `-Source` opcji:</span><span class="sxs-lookup"><span data-stu-id="88612-129">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="88612-130">Możesz również push podstawowych i symboli w tym samym czasie, za pomocą następujących pakietów do obu repozytoria:</span><span class="sxs-lookup"><span data-stu-id="88612-130">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="88612-131">W takim przypadku opublikuje NuGet `MyPackage.symbols.nupkg`, jeśli jest obecny, aby https://nuget.smbsrc.net/ (wypychania adres URL symbolsource.org), po publikuje pakiet główny w usłudze nuget.org.</span><span class="sxs-lookup"><span data-stu-id="88612-131">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="88612-132">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="88612-132">See Also</span></span>

<span data-ttu-id="88612-133">[Przeniesienie na nowy aparat SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="88612-133">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
