---
title: Tworzenie starszych pakietów symboli (. Symbols. nupkg)
description: Jak utworzyć pakiety NuGet, które zawierają tylko symbole obsługujące debugowanie innych pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476272"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Tworzenie starszych pakietów symboli (. Symbols. nupkg)

> [!Important]
> Nowy zalecany format pakietów symboli to. snupkg. Zobacz [Tworzenie pakietów symboli (. snupkg)](Symbol-Packages-snupkg.md). </br>
> . Symbols. NUPKG jest nadal obsługiwana, ale tylko ze względów zgodności.

Oprócz kompilowania pakietów dla nuget.org lub innych źródeł, pakiet NuGet obsługuje również tworzenie skojarzonych pakietów symboli, które mogą być publikowane na serwerach symboli. Starszy format pakietu symboli (. Symbols. nupkg) można wypchnąć do repozytorium SymbolSource.

Odbiorcy pakietów mogą następnie dodać `https://nuget.smbsrc.net` do ich źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio. Aby uzyskać szczegółowe informacje na temat tego procesu, zobacz [Określanie symboli (. pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

## <a name="creating-a-legacy-symbol-package"></a>Tworzenie starszego pakietu symboli

Aby utworzyć starszy pakiet symboli, postępuj zgodnie z następującymi konwencjami:

- Nazwij pakiet podstawowy (z kodem) `{identifier}.nupkg` i Uwzględnij wszystkie pliki z wyjątkiem plików `.pdb`.
- Nazwij pakiet starszego symbolu `{identifier}.symbols.nupkg` i Uwzględnij biblioteki DLL zestawu, pliki `.pdb`, pliki XMLDOC, pliki źródłowe (Zobacz poniższe sekcje).

Można utworzyć Oba pakiety z opcją `-Symbols`, z pliku `.nuspec` lub pliku projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Należy pamiętać, że `pack` wymaga zastosowania mono w Mac OS X i nie działa w systemach Linux. Na komputerze Mac należy również skonwertować nazwy ścieżek systemu Windows w pliku `.nuspec` na ścieżki w stylu systemu UNIX.

## <a name="legacy-symbol-package-structure"></a>Struktura pakietu starszego symbolu

Pakiet starszego symbolu może kierować wiele platform docelowych w taki sam sposób, w jaki działa pakiet biblioteki, dlatego Struktura folderu `lib` powinna być dokładnie taka sama jak w przypadku pakietu podstawowego, w tym tylko do `.pdb` plików obok biblioteki DLL.

Na przykład starszy pakiet symboli przeznaczony dla programu .NET 4,0 i Silverlight 4 ma następujący układ:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Pliki źródłowe są następnie umieszczane w osobnym folderze specjalnym o nazwie `src`, który musi być zgodny ze strukturą względną repozytorium źródłowego. Wynika to z faktu, że plików PDB zawierają bezwzględne ścieżki do plików źródłowych użytych do skompilowania zgodnej biblioteki DLL i muszą znajdować się w trakcie procesu publikowania. Ścieżka bazowa (wspólny prefiks ścieżki) może zostać usunięta. Rozważmy na przykład bibliotekę utworzoną na podstawie tych plików:

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

Oprócz folderu `lib` starszy pakiet symboli musi zawierać następujący układ:

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

## <a name="referring-to-files-in-the-nuspec"></a>Odwoływanie się do plików w nuspec

Starszy pakiet symboli może być skompilowany przy użyciu konwencji, z struktury folderów, zgodnie z opisem w poprzedniej sekcji lub przez określenie jego zawartości w sekcji `files` manifestu. Na przykład, aby skompilować pakiet przedstawiony w poprzedniej sekcji, użyj następującego w pliku `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Publikowanie starszego pakietu symboli

> [!Important]
> Aby wypchnąć pakiety do nuget.org należy użyć pliku [NuGet. exe v 4.9.1 lub nowszego](https://www.nuget.org/downloads), który implementuje wymagane [Protokoły NuGet](../api/nuget-protocols.md).

1. Dla wygody należy najpierw zapisać klucz interfejsu API za pomocą narzędzia NuGet (zobacz temat [Publikowanie pakietu](../nuget-org/publish-a-package.md), który będzie stosowany zarówno do NuGet.org, jak i symbolsource.org, ponieważ symbolsource.org sprawdzi się z NuGet.org, aby sprawdzić, czy jesteś właścicielem pakietu.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Po opublikowaniu pakietu podstawowego w programie nuget.org wypchnij starszy pakiet symboli w następujący sposób, który będzie automatycznie używać symbolsource.org jako obiektu docelowego z powodu `.symbols` w nazwie pliku:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Aby opublikować w innym repozytorium symboli lub wypchnąć starszy pakiet symboli, który nie jest zgodny z konwencją nazewnictwa, użyj opcji `-Source`:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Jednocześnie można wypchnąć zarówno podstawowe, jak i główne pakiety do obu repozytoriów, korzystając z następujących metod:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > W przypadku programu NuGet. exe 4.5.0 lub nowszego pakiety symboli nie są automatycznie wypychane do symbolsource.org. Należy wypchnąć pakiety symboli oddzielnie, jak wyjaśniono w poprzednich krokach.
   
W takim przypadku pakiet NuGet opublikuje `MyPackage.symbols.nupkg`, jeśli istnieje, aby https://nuget.smbsrc.net/ (adres URL wypychania dla symbolsource.org), po opublikowaniu pakietu podstawowego do nuget.org.

## <a name="see-also"></a>Zobacz też

* [Tworzenie pakietów symboli (. snupkg)](Symbol-Packages-snupkg.md) — nowy zalecany format dla pakietów symboli
* [Przejście do nowego aparatu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
