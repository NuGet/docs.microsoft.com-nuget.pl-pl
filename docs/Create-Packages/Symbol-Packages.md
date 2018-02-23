---
title: "Tworzenie pakietów NuGet symbol | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Jak tworzyć pakiety NuGet, które zawierają tylko symbole, aby zapewnić obsługę debugowania innych pakietów NuGet w programie Visual Studio."
keywords: "Pakiety symboli NuGet, pakietu NuGet, debugowanie, obsługi debugowania pakietu symboli, symbol konwencje pakietów NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: e1d90009c739a7f358e9581c7032523b8b284936
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="creating-symbol-packages"></a>Tworzenie pakietów — symbol

Oprócz tworzenia pakietów dla nuget.org lub innych źródeł, NuGet również obsługuje tworzenie skojarzone pakiety symboli i opublikować go do repozytorium SymbolSource.

Konsumenci pakiet można następnie dodać `https://nuget.smbsrc.net` źródła symbol w programie Visual Studio, umożliwia wykonywanie krok po kroku do pakietu kodu w debugerze programu Visual Studio. Zobacz [Określ symboli (.pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) szczegółowe informacje na temat tego procesu.

## <a name="creating-a-symbol-package"></a>Tworzenie pakietu symboli

Aby utworzyć pakiet symboli, zgodne z konwencjami te:

- Nazwa podstawowego pakietu (swoim własnym kodem) `{identifier}.nupkg` i zawiera wszystkie pliki z wyjątkiem `.pdb` plików.
- Nazwa pakietu symboli `{identifier}.symbols.nupkg` i obejmują używanemu zestawowi biblioteki DLL, `.pdb` plików, pliki XMLDOC, pliki źródłowe (zobacz w kolejnych sekcjach).

Możesz utworzyć oba pakiety z `-Symbols` opcji, albo z `.nuspec` pliku lub pliku projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux. Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.

## <a name="symbol-package-structure"></a>Struktura pakietu symboli

Pakiet symboli można kierować wiele docelowych platform w taki sam sposób, który wykonuje pakiet biblioteki, dlatego struktury `lib` folder powinien być dokładnie taki sam jak podstawowy pakiet, tylko włączając `.pdb` pliki z biblioteki DLL.

Na przykład pakiet symboli, przeznaczonego dla programu .NET 4.0 i Silverlight 4 byłyby ten układ:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Pliki źródłowe następnie są umieszczane w oddzielnym folderze specjalne o nazwie `src`, które należy wykonać względną struktury repozytorium źródła. To dlatego PDB zawierają bezwzględnej ścieżki do plików źródłowych, używana do kompilowania zgodne biblioteki DLL i muszą można znaleźć w procesie publikowania. Podstawowa ścieżka (wspólnej ścieżki prefiks) mogą być usunięte wychodzących. Rozważmy na przykład biblioteki zbudowane na podstawie tych plików:

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

Z wyjątkiem `lib` folderu, pakiet symboli musi zawierać ten układ:

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

## <a name="referring-to-files-in-the-nuspec"></a>Odwołujące się do plików w plik nuspec

Pakiet symboli mogą być wbudowane w Konwencji z struktury folderów, zgodnie z opisem w poprzedniej sekcji, lub podając jego zawartość w `files` sekcji manifestu. Na przykład, aby utworzyć pakiet wyświetlone w poprzedniej sekcji, należy użyć następującego w `.nuspec` pliku:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Publikowania pakietu symboli

> [!Important]
> Pakiety wypychania do nuget.org musi używać [nuget.exe v4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).

1. Dla wygody, najpierw zapisać klucz interfejsu API z programem NuGet (zobacz [opublikowania pakietu](../create-packages/publish-a-package.md), która będzie stosowana do nuget.org i symbolsource.org, ponieważ symbolsource.org będzie sprawdzać z nuget.org do sprawdzenia, czy jesteś właścicielem pakietu.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po opublikowaniu pakietu podstawowego do nuget.org, push pakietu symboli, które będą automatycznie używać symbolsource.org jako element docelowy z powodu `.symbols` w nazwie pliku:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> Z nuget.exe 4.5.0 lub powyżej symbole pakiety nie są automatycznie przypisany do symbolsource.org. Będzie potrzebny do dystrybuowania pakietów symbole oddzielnie zgodnie z objaśnieniem w następnym kroku.

1. Publikowanie do repozytorium inny symbol lub push pakietu symboli, który nie będzie zgodna z konwencją nazewnictwa, należy użyć `-Source` opcji:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. Możesz również push podstawowych i symboli w tym samym czasie, za pomocą następujących pakietów do obu repozytoria:

    ```cli
    nuget push MyPackage.nupkg
    ```

W takim przypadku opublikuje NuGet `MyPackage.symbols.nupkg`, jeśli jest obecny, aby https://nuget.smbsrc.net/ (wypychania adres URL symbolsource.org), po publikuje pakiet główny w usłudze nuget.org.

## <a name="see-also"></a>Zobacz też

[Przeniesienie na nowy aparat SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
