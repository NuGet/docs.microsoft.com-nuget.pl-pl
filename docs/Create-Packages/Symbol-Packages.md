---
title: "Tworzenie pakietów NuGet symbol | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4667a70d-5a17-4f1e-b2f2-b8d0c6af3882
description: "Jak tworzyć pakiety NuGet, które zawierają tylko symbole, aby zapewnić obsługę debugowania innych pakietów NuGet w programie Visual Studio."
keywords: "Pakiety symboli NuGet, pakietu NuGet, debugowanie, obsługi debugowania pakietu symboli, symbol konwencje pakietów NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1a29fe6e9a3dec6847dbed07761e28fb8eb9b19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="c4663-104">Tworzenie pakietów — symbol</span><span class="sxs-lookup"><span data-stu-id="c4663-104">Creating symbol packages</span></span>

<span data-ttu-id="c4663-105">Oprócz tworzenia pakietów dla nuget.org lub innych źródeł, NuGet również obsługuje tworzenie pakietów skojarzone symboli i publikowania ich do [repozytorium SymbolSource](http://www.symbolsource.org/Public).</span><span class="sxs-lookup"><span data-stu-id="c4663-105">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the [SymbolSource repository](http://www.symbolsource.org/Public).</span></span>

<span data-ttu-id="c4663-106">Konsumenci pakiet można następnie dodać `http://srv.symbolsource.org/pdb/Public` źródła symbol w programie Visual Studio, umożliwia wykonywanie krok po kroku do pakietu kodu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4663-106">Package consumers can then add `http://srv.symbolsource.org/pdb/Public` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="c4663-107">Zobacz [Określ symboli (.pdb) i plików źródłowych w debugerze programu Visual Studio](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) szczegółowe informacje na temat tego procesu.</span><span class="sxs-lookup"><span data-stu-id="c4663-107">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>


## <a name="creating-a-symbol-package"></a><span data-ttu-id="c4663-108">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="c4663-108">Creating a symbol package</span></span>

<span data-ttu-id="c4663-109">Aby utworzyć pakiet symboli, zgodne z konwencjami te:</span><span class="sxs-lookup"><span data-stu-id="c4663-109">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="c4663-110">Nazwa podstawowego pakietu (swoim własnym kodem) `{identifier}.nupkg` i zawiera wszystkie pliki z wyjątkiem `.pdb` plików.</span><span class="sxs-lookup"><span data-stu-id="c4663-110">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="c4663-111">Nazwa pakietu symboli `{identifier}.symbols.nupkg` i obejmują używanemu zestawowi biblioteki DLL, `.pdb` plików, pliki XMLDOC, pliki źródłowe (zobacz w kolejnych sekcjach).</span><span class="sxs-lookup"><span data-stu-id="c4663-111">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="c4663-112">Możesz utworzyć oba pakiety z `-Symbols` opcji, albo z `.nuspec` pliku lub pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="c4663-112">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="c4663-113">Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="c4663-113">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="c4663-114">Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.</span><span class="sxs-lookup"><span data-stu-id="c4663-114">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="c4663-115">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="c4663-115">Symbol package structure</span></span>

<span data-ttu-id="c4663-116">Pakiet symboli można kierować wiele docelowych platform w taki sam sposób, który wykonuje pakiet biblioteki, dlatego struktury `lib` folder powinien być dokładnie taki sam jak podstawowy pakiet, tylko włączając `.pdb` pliki z biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="c4663-116">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="c4663-117">Na przykład pakiet symboli, przeznaczonego dla programu .NET 4.0 i Silverlight 4 byłyby ten układ:</span><span class="sxs-lookup"><span data-stu-id="c4663-117">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="c4663-118">Pliki źródłowe następnie są umieszczane w oddzielnym folderze specjalne o nazwie `src`, które należy wykonać względną struktury repozytorium źródła.</span><span class="sxs-lookup"><span data-stu-id="c4663-118">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="c4663-119">To dlatego PDB zawierają bezwzględnej ścieżki do plików źródłowych, używana do kompilowania zgodne biblioteki DLL i muszą można znaleźć w procesie publikowania.</span><span class="sxs-lookup"><span data-stu-id="c4663-119">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="c4663-120">Podstawowa ścieżka (wspólnej ścieżki prefiks) mogą być usunięte wychodzących. Rozważmy na przykład biblioteki zbudowane na podstawie tych plików:</span><span class="sxs-lookup"><span data-stu-id="c4663-120">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="c4663-121">Z wyjątkiem `lib` folderu, pakiet symboli musi zawierać ten układ:</span><span class="sxs-lookup"><span data-stu-id="c4663-121">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="c4663-122">Odwołujące się do plików w plik nuspec</span><span class="sxs-lookup"><span data-stu-id="c4663-122">Referring to files in the nuspec</span></span>

<span data-ttu-id="c4663-123">Pakiet symboli mogą być wbudowane w Konwencji z struktury folderów, zgodnie z opisem w poprzedniej sekcji, lub podając jego zawartość w `files` sekcji manifestu.</span><span class="sxs-lookup"><span data-stu-id="c4663-123">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="c4663-124">Na przykład, aby utworzyć pakiet wyświetlone w poprzedniej sekcji, należy użyć następującego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="c4663-124">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="c4663-125">Publikowania pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="c4663-125">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="c4663-126">Pakiety wypychania do nuget.org musi używać [nuget.exe v4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="c4663-126">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="c4663-127">Dla wygody, najpierw zapisać klucz interfejsu API z programem NuGet (zobacz [opublikowania pakietu](../create-packages/publish-a-package.md), która będzie stosowana do nuget.org i symbolsource.org, ponieważ symbolsource.org będzie sprawdzać z nuget.org do sprawdzenia, czy jesteś właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="c4663-127">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="c4663-128">Po opublikowaniu pakietu podstawowego do nuget.org, push pakietu symboli, które będą automatycznie używać symbolsource.org jako element docelowy z powodu `.symbols` w nazwie pliku:</span><span class="sxs-lookup"><span data-stu-id="c4663-128">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> <span data-ttu-id="c4663-129">Z nuget.exe 4.5.0 lub powyżej symbole pakiety nie są automatycznie przypisany do symbolsource.org. Będzie potrzebny do dystrybuowania pakietów symbole oddzielnie zgodnie z objaśnieniem w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="c4663-129">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

1. <span data-ttu-id="c4663-130">Publikowanie do repozytorium inny symbol lub push pakietu symboli, który nie będzie zgodna z konwencją nazewnictwa, należy użyć `-Source` opcji:</span><span class="sxs-lookup"><span data-stu-id="c4663-130">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. <span data-ttu-id="c4663-131">Możesz również push podstawowych i symboli w tym samym czasie, za pomocą następujących pakietów do obu repozytoria:</span><span class="sxs-lookup"><span data-stu-id="c4663-131">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="c4663-132">W takim przypadku opublikuje NuGet `MyPackage.symbols.nupkg`, jeśli jest obecny, aby https://nuget.smbsrc.net/ (wypychania adres URL symbolsource.org), po publikuje pakiet główny w usłudze nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c4663-132">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="c4663-133">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c4663-133">See Also</span></span>

 - <span data-ttu-id="c4663-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Za pomocą SymbolSource</a> (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="c4663-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Using SymbolSource</a> (symbolsource.org)</span></span>
