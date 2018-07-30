---
title: Jak utworzyć pakiety symboli NuGet
description: Jak utworzyć pakiety NuGet, które zawierają tylko symbole, aby zapewnić obsługę debugowania innych pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e917895d0fa6ed6dc4bc24b72afc7fa0770f2dd0
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843371"
---
# <a name="creating-symbol-packages"></a>Tworzenie pakietów symboli

Oprócz tworzenia pakietów nuget.org lub innych źródeł, NuGet również obsługuje tworzenie skojarzone pakiety symboli i publikowania ich w repozytorium SymbolSource.

Konsumenci pakiet można następnie dodać `https://nuget.smbsrc.net` źródła symbol w programie Visual Studio, umożliwia przechodzenie do pakietu kodu w debugerze programu Visual Studio. Zobacz [określanie plików symboli (.pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) szczegółowe informacje na temat tego procesu.

## <a name="creating-a-symbol-package"></a>Tworzenie pakietu symboli

Aby utworzyć pakiet symboli, postępuj zgodnie z tych konwencji:

- Nazwij pakiet główny (Twoim kodem) `{identifier}.nupkg` i Dołącz wszystkie pliki z wyjątkiem `.pdb` plików.
- Nazwij pakiet symboli `{identifier}.symbols.nupkg` i obejmuje zestaw bibliotek DLL, `.pdb` pliki, pliki XMLDOC, pliki źródłowe (zobacz w kolejnych sekcjach).

Możesz utworzyć oba pakiety za pomocą `-Symbols` opcji z `.nuspec` pliku lub pliku projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Należy pamiętać, że `pack` wymaga platformy Mono 4.4.2 w systemie Mac OS X, a nie działa w systemach Linux. Na komputerze Mac, należy także przekonwertować nazwy Windows ścieżek w `.nuspec` plik do ścieżki stylu systemu Unix.

## <a name="symbol-package-structure"></a>Struktura pakietu symboli

Pakiet symboli można wskazać wiele platform docelowych w taki sam sposób, który wykonuje pakietu biblioteki, więc struktury `lib` folder powinien być dokładnie takie same, jak pakiet podstawowego, tylko tym `.pdb` plików wraz z biblioteki DLL.

Na przykład pakiet symboli, który jest przeznaczony dla .NET 4.0 i Silverlight 4 będą mieć ten układ:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Pliki źródłowe następnie są umieszczane w oddzielnym folderze specjalnym, o nazwie `src`, które należy wykonać względne struktury repozytorium źródłowym. Jest to spowodowane plików PDB zawierać ścieżek bezwzględnych do plików źródłowych, używana do kompilowania zgodnych bibliotek DLL i muszą one można znaleźć w procesie publikowania. Ścieżki podstawowej (Wspólny prefiks ścieżki) może być wycięte. Rozważmy na przykład biblioteki, utworzony na podstawie tych plików:

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

Z wyjątkiem `lib` folderze pakiet symboli musi zawierać ten układ:

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

## <a name="referring-to-files-in-the-nuspec"></a>Odwołujące się do plików w nuspec

Mogą być wbudowane pakiet symboli, konwencje ze struktury folderów, zgodnie z opisem w poprzedniej sekcji, lub podając jego zawartość w `files` sekcji manifestu. Na przykład, aby utworzyć pakiet pokazano w poprzedniej sekcji, należy użyć następującego w `.nuspec` pliku:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Publikowanie pakietu symboli

> [!Important]
> Do wypychania pakietów nuget.org, należy użyć [nuget.exe verze 4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md).

1. Dla wygody, najpierw zapisać swój klucz interfejsu API z NuGet (zobacz [publikowanie pakietu](../create-packages/publish-a-package.md), która będzie stosowana do nuget.org i symbolsource.org, ponieważ symbolsource.org sprawdzi się z repozytorium nuget.org, aby sprawdzić, czy jesteś właścicielem pakietu.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Po opublikowaniu pakiet podstawowego na stronie nuget.org, Wypchnij pakiet symboli w następujący sposób, który będzie automatycznie używać symbolsource.org jako element docelowy z powodu `.symbols` w nazwie pliku:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Aby opublikować w repozytorium innego symbolu lub wypychania pakiet symboli, które nie są zgodne z konwencją nazewnictwa, użyj `-Source` opcji:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Można również wypchnąć podstawowych i symboli pakietów do obu repozytoriów, w tym samym czasie przy użyciu następujących:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Nuget.exe 4.5.0 lub powyżej symbole pakiety nie zostaną automatycznie wypchnięte do symbolsource.org. Będziesz potrzebować do wypychania pakietów symbole oddzielnie, zgodnie z opisem w następnym kroku.
   
W tym przypadku będzie publikować NuGet `MyPackage.symbols.nupkg`, jeśli jest obecna, aby https://nuget.smbsrc.net/ (URL wypychania dla symbolsource.org), po publikuje pakiet główny na stronie nuget.org.

## <a name="see-also"></a>Zobacz też

[Przejście do nowego aparatu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
