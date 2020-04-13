---
title: Tworzenie starszych pakietów symboli (.symbols.nupkg)
description: Jak utworzyć pakiety NuGet, które zawierają tylko symbole do obsługi debugowania innych pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476272"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="9ab60-103">Tworzenie starszych pakietów symboli (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="9ab60-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="9ab60-104">Nowy zalecany format dla pakietów symboli to .snupkg.</span><span class="sxs-lookup"><span data-stu-id="9ab60-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="9ab60-105">Zobacz [Tworzenie pakietów symboli (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="9ab60-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="9ab60-106">Plik .symbols.nupkg jest nadal obsługiwany, ale tylko ze względu na zgodność.</span><span class="sxs-lookup"><span data-stu-id="9ab60-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="9ab60-107">Oprócz tworzenia pakietów dla nuget.org lub innych źródeł, NuGet obsługuje również tworzenie skojarzonych pakietów symboli, które mogą być publikowane na serwerach symboli.</span><span class="sxs-lookup"><span data-stu-id="9ab60-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="9ab60-108">Starszy format pakietu symboli symboli symboli .symbols.nupkg można wypchnąć do repozytorium SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="9ab60-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="9ab60-109">Konsumenci pakietów można `https://nuget.smbsrc.net` następnie dodać do swoich źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ab60-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="9ab60-110">Zobacz [Określanie symbolu (pdb) i plików źródłowych w debugerze programu Visual Studio, aby](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) uzyskać szczegółowe informacje na temat tego procesu.</span><span class="sxs-lookup"><span data-stu-id="9ab60-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="9ab60-111">Tworzenie starszego pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="9ab60-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="9ab60-112">Aby utworzyć starszy pakiet symboli, postępuj zgodnie z tymi konwencjami:</span><span class="sxs-lookup"><span data-stu-id="9ab60-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="9ab60-113">Nazwij pakiet podstawowy (z kodem) `{identifier}.nupkg` `.pdb` i dołącz wszystkie pliki z wyjątkiem plików.</span><span class="sxs-lookup"><span data-stu-id="9ab60-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="9ab60-114">Nazwij starszy `{identifier}.symbols.nupkg` pakiet symboli i `.pdb` dołącz bibliotekę DLL zespołu, pliki, pliki XMLDOC, pliki źródłowe (zobacz sekcje, które następują).</span><span class="sxs-lookup"><span data-stu-id="9ab60-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="9ab60-115">Oba pakiety można `-Symbols` utworzyć z opcją, `.nuspec` z pliku lub pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="9ab60-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="9ab60-116">Należy `pack` pamiętać, że wymaga Mono 4.4.2 na Mac OS X i nie działa na systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="9ab60-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="9ab60-117">Na komputerze Mac należy również przekonwertować `.nuspec` nazwy ścieżek systemu Windows w pliku na ścieżki w stylu Uniksa.</span><span class="sxs-lookup"><span data-stu-id="9ab60-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="9ab60-118">Starsza struktura pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="9ab60-118">Legacy symbol package structure</span></span>

<span data-ttu-id="9ab60-119">Starszy pakiet symboli może być przeznaczone dla wielu struktur docelowych w taki `lib` sam sposób, jak pakiet biblioteki, `.pdb` więc struktura folderu powinna być dokładnie taka sama jak pakiet podstawowy, tylko w tym pliki obok biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="9ab60-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="9ab60-120">Na przykład starszy pakiet symboli przeznaczony dla platformy .NET 4.0 i Silverlight 4 miałby ten układ:</span><span class="sxs-lookup"><span data-stu-id="9ab60-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="9ab60-121">Pliki źródłowe są następnie umieszczane `src`w osobnym folderze specjalnym o nazwie , który musi być zgodny ze względną strukturą repozytorium źródłowego.</span><span class="sxs-lookup"><span data-stu-id="9ab60-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="9ab60-122">Dzieje się tak, ponieważ kontrolery PDB zawierają ścieżki bezwzględne do plików źródłowych używanych do kompilowania pasującej biblioteki DLL i należy je znaleźć podczas procesu publikowania.</span><span class="sxs-lookup"><span data-stu-id="9ab60-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="9ab60-123">Ścieżka podstawowa (wspólny prefiks ścieżki) może zostać usunięta. Rozważmy na przykład bibliotekę utwory utworzone z tych plików:</span><span class="sxs-lookup"><span data-stu-id="9ab60-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="9ab60-124">Oprócz folderu `lib` starszy pakiet symboli musiałby zawierać ten układ:</span><span class="sxs-lookup"><span data-stu-id="9ab60-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="9ab60-125">Odwoływanie się do plików w nuspec</span><span class="sxs-lookup"><span data-stu-id="9ab60-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="9ab60-126">Starszy pakiet symboli może być zbudowany przez konwencje, ze struktury folderów, jak opisano `files` w poprzedniej sekcji lub określając jego zawartość w sekcji manifestu.</span><span class="sxs-lookup"><span data-stu-id="9ab60-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="9ab60-127">Na przykład, aby utworzyć pakiet pokazany w poprzedniej sekcji, użyj w `.nuspec` pliku następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="9ab60-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="9ab60-128">Publikowanie starszego pakietu symboli</span><span class="sxs-lookup"><span data-stu-id="9ab60-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="9ab60-129">Aby wypchnąć pakiety do nuget.org należy użyć [nuget.exe v4.9.1 lub wyższej](https://www.nuget.org/downloads), który implementuje wymagane [protokoły NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="9ab60-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="9ab60-130">Dla wygody najpierw zapisz klucz interfejsu API za pomocą nuget (zobacz [publikuj pakiet](../nuget-org/publish-a-package.md), który będzie stosowany zarówno do nuget.org, jak i symbolsource.org, ponieważ symbolsource.org skontaktuje się z nuget.org, aby sprawdzić, czy jesteś właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="9ab60-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="9ab60-131">Po opublikowaniu pakietu podstawowego do nuget.org wypchnij starszy pakiet symboli w następujący sposób, który `.symbols` automatycznie użyje symbolsource.org jako obiektu docelowego ze względu na nazwę pliku:</span><span class="sxs-lookup"><span data-stu-id="9ab60-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="9ab60-132">Aby opublikować w innym repozytorium symboli lub wypchnąć starszy pakiet symboli, `-Source` który nie jest zgodny z konwencją nazewnictwa, użyj tej opcji:</span><span class="sxs-lookup"><span data-stu-id="9ab60-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="9ab60-133">Można również wypchnąć zarówno pakiety podstawowe, jak i symbole do obu repozytoriów w tym samym czasie, korzystając z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="9ab60-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="9ab60-134">W nuget.exe 4.5.0 lub wyższym pakiety symboli nie są automatycznie wypychane do symbolsource.org. Należy wypchnąć pakiety symboli oddzielnie, jak wyjaśniono we wcześniejszych krokach.</span><span class="sxs-lookup"><span data-stu-id="9ab60-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="9ab60-135">W takim przypadku NuGet `MyPackage.symbols.nupkg`opublikuje , https://nuget.smbsrc.net/ jeśli jest obecny, do (adres URL wypychania dla symbolsource.org), po opublikowaniu pakietu podstawowego do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9ab60-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="9ab60-136">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9ab60-136">See also</span></span>

* <span data-ttu-id="9ab60-137">[Tworzenie pakietów symboli (.snupkg)](Symbol-Packages-snupkg.md) - Nowy zalecany format dla pakietów symboli</span><span class="sxs-lookup"><span data-stu-id="9ab60-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="9ab60-138">[Przejście do nowego aparatu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="9ab60-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
