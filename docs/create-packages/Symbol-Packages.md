---
title: Jak utworzyć pakiety symboli NuGet
description: Jak utworzyć pakiety NuGet, które zawierają tylko symbole obsługujące debugowanie innych pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f7503dd413a976997580aa03da26df0c462ff0e1
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564551"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="f8ed2-103">Tworzenie pakietów symboli (starsza wersja)</span><span class="sxs-lookup"><span data-stu-id="f8ed2-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="f8ed2-104">Nowy zalecany format pakietów symboli to. snupkg.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="f8ed2-105">Zobacz [Tworzenie pakietów symboli (. snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="f8ed2-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="f8ed2-106">. Symbols. NUPKG jest nadal obsługiwana, ale tylko ze względów zgodności.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="f8ed2-107">Oprócz kompilowania pakietów dla nuget.org lub innych źródeł, pakiet NuGet obsługuje również tworzenie skojarzonych pakietów symboli i publikowanie ich w repozytorium SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="f8ed2-108">Odbiorcy pakietów mogą następnie dodawać `https://nuget.smbsrc.net` do ich źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="f8ed2-109">Aby uzyskać szczegółowe informacje na temat tego procesu, zobacz [Określanie symboli (. pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="f8ed2-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="f8ed2-110">Tworzenie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="f8ed2-110">Creating a symbol package</span></span>

<span data-ttu-id="f8ed2-111">Aby utworzyć pakiet symboli, postępuj zgodnie z następującymi konwencjami:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="f8ed2-112">Nazwij pakiet podstawowy (z kodem) `{identifier}.nupkg` i Dołącz wszystkie pliki z wyjątkiem `.pdb` plików.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="f8ed2-113">Nadaj nazwę pakietowi `{identifier}.symbols.nupkg` symboli i Uwzględnij `.pdb` plik DLL zestawu, pliki, pliki XMLDOC, pliki źródłowe (Zobacz poniższe sekcje).</span><span class="sxs-lookup"><span data-stu-id="f8ed2-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="f8ed2-114">Oba pakiety można utworzyć przy użyciu `-Symbols` opcji, `.nuspec` z pliku lub pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="f8ed2-115">Należy pamiętać `pack` , że wymaga mono 4.4.2 w Mac OS X i nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="f8ed2-116">Na komputerze Mac należy również skonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku na ścieżki w stylu systemu UNIX.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="f8ed2-117">Struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="f8ed2-117">Symbol package structure</span></span>

<span data-ttu-id="f8ed2-118">Pakiet symboli może kierować wiele platform docelowych w taki sam sposób, w jaki działa pakiet biblioteki, dlatego struktura `lib` folderu powinna być dokładnie taka sama jak w przypadku pakietu podstawowego, w tym `.pdb` tylko plików obok biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="f8ed2-119">Na przykład pakiet symboli przeznaczony dla programów .NET 4,0 i Silverlight 4 ma następujący układ:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="f8ed2-120">Pliki źródłowe są następnie umieszczane w osobnym folderze specjalnym o nazwie `src`, który musi być zgodny ze strukturą względną repozytorium źródłowego.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="f8ed2-121">Wynika to z faktu, że plików PDB zawierają bezwzględne ścieżki do plików źródłowych użytych do skompilowania zgodnej biblioteki DLL i muszą znajdować się w trakcie procesu publikowania.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="f8ed2-122">Ścieżka bazowa (wspólny prefiks ścieżki) może zostać usunięta. Rozważmy na przykład bibliotekę utworzoną na podstawie tych plików:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="f8ed2-123">`lib` Poza folderem pakiet symboli musi zawierać następujący układ:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="f8ed2-124">Odwoływanie się do plików w nuspec</span><span class="sxs-lookup"><span data-stu-id="f8ed2-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="f8ed2-125">Pakiet symboli może być skompilowany przy użyciu konwencji, z struktury folderów, zgodnie z opisem w poprzedniej sekcji lub przez określenie jego zawartości w `files` sekcji manifestu.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="f8ed2-126">Na przykład, aby skompilować pakiet przedstawiony w poprzedniej sekcji, użyj następującego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="f8ed2-127">Publikowanie pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="f8ed2-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="f8ed2-128">Aby wypchnąć pakiety do nuget.org należy użyć pliku [NuGet. exe v 4.9.1 lub nowszego](https://www.nuget.org/downloads), który implementuje wymagane [Protokoły NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f8ed2-128">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="f8ed2-129">Dla wygody należy najpierw zapisać klucz interfejsu API za pomocą narzędzia NuGet (zobacz temat [Publikowanie pakietu](../nuget-org/publish-a-package.md), który będzie stosowany zarówno do NuGet.org, jak i symbolsource.org, ponieważ symbolsource.org sprawdzi się z NuGet.org, aby sprawdzić, czy jesteś właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-129">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="f8ed2-130">Po opublikowaniu pakietu podstawowego w `.symbols` programie NuGet.org wypchnij pakiet symboli w następujący sposób, który będzie automatycznie używać symbolsource.org jako elementu docelowego z powodu pliku w nazwie:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="f8ed2-131">Aby opublikować w innym repozytorium symboli lub wypchnąć pakiet symboli, który nie jest zgodny z konwencją nazewnictwa, użyj `-Source` opcji:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="f8ed2-132">Jednocześnie można wypchnąć zarówno podstawowe, jak i główne pakiety do obu repozytoriów, korzystając z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="f8ed2-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="f8ed2-133">W przypadku programu NuGet. exe 4.5.0 lub nowszego pakiety symboli nie są automatycznie wypychane do symbolsource.org. Należy wypchnąć pakiety symboli oddzielnie, jak wyjaśniono w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="f8ed2-134">W takim przypadku pakiet NuGet opublikuje `MyPackage.symbols.nupkg` https://nuget.smbsrc.net/ (jeśli istnieje) (adres URL wypychania dla symbolsource.org), po opublikowaniu pakietu podstawowego do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f8ed2-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="f8ed2-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f8ed2-135">See Also</span></span>

<span data-ttu-id="f8ed2-136">[Przechodzenie do nowego aparatu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="f8ed2-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
