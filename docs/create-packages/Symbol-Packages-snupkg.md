---
title: Jak opublikować pakiety NuGet symboli, przy użyciu nowego formatu pakietu symbol ".snupkg" | Dokumentacja firmy Microsoft
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak utworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, pakietów NuGet, debugowanie, obsługa NuGet debugowania pakiet symboli, konwencje pakietu symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453458"
---
# <a name="creating-symbol-packages-snupkg"></a>Tworzenie pakietów symbol (.snupkg)

## <a name="prerequisites"></a>Wymagania wstępne

[nuget.exe v4.9.0 lub nowszej](https://www.nuget.org/downloads) lub [dotnet.exe v2.2.0 lub nowszej](https://www.microsoft.com/net/download/dotnet-core/2.2), który implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Tworzenie pakietu symboli

Pakiet symboli snupkg mogą być tworzone z pliku .nuspec lub z pliku csproj. Obsługiwane są zarówno NuGet.exe i dotnet.exe. Po opcji ```-Symbols -SymbolPackageFormat snupkg``` używane są polecenia pakietu nuget.exe w specialfolder.ProgramFiles plikowi .nupkg zostanie utworzony plik .snupkg.

Przykładowe polecenia, aby utworzyć pliki .snupkg
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

`.snupkgs` nie są tworzone domyślnie. Należy przekazać `SymbolPackageFormat` właściwości wraz z `-Symbols` przypadku nuget.exe, `--include-symbols` przypadku dotnet.exe, lub `-p:IncludeSymbols` w przypadku programu msbuild.

Właściwość SymbolPackageFormat może mieć jedną z dwóch wartości: `symbols.nupkg` (ustawienie domyślne) lub `snupkg`. Jeśli nie określono SymbolPackageFormat, jego wartość domyślna to `symbols.nupkg` i zostanie utworzony pakiet symboli starszej wersji.

> [!Note]
> Format starszych `.symbols.nupkg` jest nadal obsługiwane, ale tylko ze względu na zgodność (zobacz [pakiety ze starszych wersji Symbol](Symbol-Packages.md)). Serwer symboli NuGet.org akceptuje tylko na nowy format pakietu symboli — `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publikowanie pakietu symboli

1. Dla wygody, najpierw zapisać swój klucz interfejsu API z NuGet (zobacz [publikowanie pakietu](../create-packages/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po opublikowaniu pakiet podstawowego na stronie nuget.org, Wypchnij następujący pakiet symboli.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Można również wypchnąć podstawowych i symboli pakietów w tej samej chwili poniższego polecenia. Pliki .nupkg i .snupkg muszą znajdować się w bieżącym folderze.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet opublikuje oba pakiety na stronie nuget.org. `MyPackage.nupkg` zostaną opublikowane w pierwszym, następuje `MyPackage.snupkg`.

## <a name="nugetorg-symbol-server"></a>Serwer symboli NuGet.org

NuGet.org obsługuje własne repozytorium serwer symboli i akceptuje tylko na nowy format pakietu symboli — `.snupkg`. Konsumentów pakietu można użyć symboli publikowane w witrynie nuget.org serwera symboli, dodając `https://symbols.nuget.org/download/symbols` źródła symbol w programie Visual Studio, umożliwia przechodzenie do pakietu kodu w debugerze programu Visual Studio. Zobacz [określanie plików symboli (.pdb) i plików źródłowych w debugerze programu Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) szczegółowe informacje na temat tego procesu.

### <a name="nugetorg-symbol-package-constraints"></a>Ograniczenia pakietu symboli Nuget.org

Pakiety symboli, obsługiwane w witrynie nuget.org mają następujące ograniczenia

- Tylko następujące rozszerzenia są dozwolone do dodania do pakietu symboli. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Tylko zarządzane [przenośnych plików PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obecnie obsługiwane na serwerze symboli nuget.
- Plików PDB i bibliotek DLL skojarzonych nupkg muszą zostać skompilowane przez kompilator w Visual Studio w wersji 15.9 lub nowszej (zobacz [skrót kryptograficzny pliku pdb](https://github.com/dotnet/roslyn/issues/24429))

Pakowanie symboli publikowanie w witrynie nuget.org zakończy się niepowodzeniem, jeśli inne typy plików są objęte .snupkg.

### <a name="symbol-package-validation-and-indexing"></a>Sprawdzanie poprawności pakietu symboli i indeksowania

Symbol pakiety opublikowane do [NuGet.org](https://www.nuget.org/) uczestniczenia w kilku operacji sprawdzania poprawności, takich jak sprawdzanie przed wirusami.

Gdy pakiet został przekazany wszystkie testy sprawdzania poprawności, może to zająć trochę czasu symbole, aby zaindeksować i być dostępne do użytku z serwerów symboli NuGet.org. W przypadku niepowodzenia sprawdzania poprawności pakietu stronie szczegółów pakietu .nupkg zostanie zaktualizowana, aby wyświetlić skojarzony błąd i zostanie wysłana wiadomość e-mail z powiadomieniem o nim.

Sprawdzanie poprawności pakietu i indeksowanie zwykle trwa mniej niż 15 minut. Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, jeśli nuget.org występuje przerw. Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się na stronie nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z działem pomocy technicznej na stronie szczegółów pakietu.

## <a name="symbol-package-structure"></a>Struktura pakietu symboli

Plik .nupkg będą dokładnie takie same jest już dziś, ale plik .snupkg będzie mieć następujące właściwości:

1) .snupkg mają ten sam identyfikator i wersja jako odpowiednie .nupkg.
2) .snupkg ma strukturę folderów dokładne jak nupkg do plików DLL lub EXE z różnica, zamiast pliku biblioteki DLL/exe ich odpowiednich plików PDB zostaną uwzględnione w tej samej hierarchii. Poza snupkg pozostanie plików i folderów przy użyciu rozszerzeń innych niż plik PDB.
3) Pliku .nuspec w .snupkg będzie również określić nowy PackageType zgodnie z poniższymi instrukcjami. Powinna to być tylko jeden PackageType, określony. 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) Jeśli autor zdecyduje się użyć niestandardowych nuspec do utworzenia ich nupkg i snupkg, snupkg powinny mieć tej samej hierarchii folderów i plików szczegółowe w wersji 2).
5) ```authors``` i ```owners``` pola, które zostaną wykluczone z snupkg nuspec.

## <a name="see-also"></a>Zobacz też

[NuGet — pakiet — debugowanie — & - symbole — ulepszenia](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
