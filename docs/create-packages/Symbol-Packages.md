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
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Tworzenie starszych pakietów symboli (.symbols.nupkg)

> [!Important]
> Nowy zalecany format dla pakietów symboli to .snupkg. Zobacz [Tworzenie pakietów symboli (.snupkg)](Symbol-Packages-snupkg.md). </br>
> Plik .symbols.nupkg jest nadal obsługiwany, ale tylko ze względu na zgodność.

Oprócz tworzenia pakietów dla nuget.org lub innych źródeł, NuGet obsługuje również tworzenie skojarzonych pakietów symboli, które mogą być publikowane na serwerach symboli. Starszy format pakietu symboli symboli symboli .symbols.nupkg można wypchnąć do repozytorium SymbolSource.

Konsumenci pakietów można `https://nuget.smbsrc.net` następnie dodać do swoich źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio. Zobacz [Określanie symbolu (pdb) i plików źródłowych w debugerze programu Visual Studio, aby](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) uzyskać szczegółowe informacje na temat tego procesu.

## <a name="creating-a-legacy-symbol-package"></a>Tworzenie starszego pakietu symboli

Aby utworzyć starszy pakiet symboli, postępuj zgodnie z tymi konwencjami:

- Nazwij pakiet podstawowy (z kodem) `{identifier}.nupkg` `.pdb` i dołącz wszystkie pliki z wyjątkiem plików.
- Nazwij starszy `{identifier}.symbols.nupkg` pakiet symboli i `.pdb` dołącz bibliotekę DLL zespołu, pliki, pliki XMLDOC, pliki źródłowe (zobacz sekcje, które następują).

Oba pakiety można `-Symbols` utworzyć z opcją, `.nuspec` z pliku lub pliku projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Należy `pack` pamiętać, że wymaga Mono 4.4.2 na Mac OS X i nie działa na systemach Linux. Na komputerze Mac należy również przekonwertować `.nuspec` nazwy ścieżek systemu Windows w pliku na ścieżki w stylu Uniksa.

## <a name="legacy-symbol-package-structure"></a>Starsza struktura pakietu symboli

Starszy pakiet symboli może być przeznaczone dla wielu struktur docelowych w taki `lib` sam sposób, jak pakiet biblioteki, `.pdb` więc struktura folderu powinna być dokładnie taka sama jak pakiet podstawowy, tylko w tym pliki obok biblioteki DLL.

Na przykład starszy pakiet symboli przeznaczony dla platformy .NET 4.0 i Silverlight 4 miałby ten układ:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Pliki źródłowe są następnie umieszczane `src`w osobnym folderze specjalnym o nazwie , który musi być zgodny ze względną strukturą repozytorium źródłowego. Dzieje się tak, ponieważ kontrolery PDB zawierają ścieżki bezwzględne do plików źródłowych używanych do kompilowania pasującej biblioteki DLL i należy je znaleźć podczas procesu publikowania. Ścieżka podstawowa (wspólny prefiks ścieżki) może zostać usunięta. Rozważmy na przykład bibliotekę utwory utworzone z tych plików:

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

Oprócz folderu `lib` starszy pakiet symboli musiałby zawierać ten układ:

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

Starszy pakiet symboli może być zbudowany przez konwencje, ze struktury folderów, jak opisano `files` w poprzedniej sekcji lub określając jego zawartość w sekcji manifestu. Na przykład, aby utworzyć pakiet pokazany w poprzedniej sekcji, użyj w `.nuspec` pliku następujących elementów:

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
> Aby wypchnąć pakiety do nuget.org należy użyć [nuget.exe v4.9.1 lub wyższej](https://www.nuget.org/downloads), który implementuje wymagane [protokoły NuGet](../api/nuget-protocols.md).

1. Dla wygody najpierw zapisz klucz interfejsu API za pomocą nuget (zobacz [publikuj pakiet](../nuget-org/publish-a-package.md), który będzie stosowany zarówno do nuget.org, jak i symbolsource.org, ponieważ symbolsource.org skontaktuje się z nuget.org, aby sprawdzić, czy jesteś właścicielem pakietu.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Po opublikowaniu pakietu podstawowego do nuget.org wypchnij starszy pakiet symboli w następujący sposób, który `.symbols` automatycznie użyje symbolsource.org jako obiektu docelowego ze względu na nazwę pliku:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Aby opublikować w innym repozytorium symboli lub wypchnąć starszy pakiet symboli, `-Source` który nie jest zgodny z konwencją nazewnictwa, użyj tej opcji:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Można również wypchnąć zarówno pakiety podstawowe, jak i symbole do obu repozytoriów w tym samym czasie, korzystając z następujących elementów:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > W nuget.exe 4.5.0 lub wyższym pakiety symboli nie są automatycznie wypychane do symbolsource.org. Należy wypchnąć pakiety symboli oddzielnie, jak wyjaśniono we wcześniejszych krokach.
   
W takim przypadku NuGet `MyPackage.symbols.nupkg`opublikuje , https://nuget.smbsrc.net/ jeśli jest obecny, do (adres URL wypychania dla symbolsource.org), po opublikowaniu pakietu podstawowego do nuget.org.

## <a name="see-also"></a>Zobacz też

* [Tworzenie pakietów symboli (.snupkg)](Symbol-Packages-snupkg.md) - Nowy zalecany format dla pakietów symboli
* [Przejście do nowego aparatu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
