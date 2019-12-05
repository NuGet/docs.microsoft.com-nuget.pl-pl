---
title: Jak publikować pakiety symboli NuGet przy użyciu nowego formatu pakietu symboli ". snupkg" | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak utworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, debugowanie pakietów NuGet, obsługa debugowania NuGet, symbole pakietów i konwencje pakietów symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 8528261f90e75e2dfac8cb746b396d227c3741f4
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825176"
---
# <a name="creating-symbol-packages-snupkg"></a>Tworzenie pakietów symboli (. snupkg)

Pakiety symboli umożliwiają zwiększenie możliwości debugowania pakietów NuGet.

## <a name="prerequisites"></a>Wymagania wstępne

[NuGet. exe v 4.9.0 lub nowszy](https://www.nuget.org/downloads) albo [dotnet. exe v 2.2.0 lub nowszy](https://www.microsoft.com/net/download/dotnet-core/2.2), które implementują wymagane [Protokoły NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Tworzenie pakietu symboli

Jeśli używasz programu dotnet. exe lub MSBuild, musisz ustawić `IncludeSymbols` i `SymbolPackageFormat` właściwości, aby utworzyć plik. snupkg oprócz pliku. nupkg.

* Dodaj następujące właściwości do pliku. csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* Lub Określ te właściwości w wierszu polecenia:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  lub

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Jeśli używasz programu NuGet. exe, możesz użyć następujących poleceń, aby utworzyć plik. snupkg oprócz pliku. nupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Właściwość [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) może mieć jedną z dwóch wartości: `symbols.nupkg` (wartość domyślna) lub `snupkg`. Jeśli ta właściwość nie zostanie określona, zostanie utworzony starszy pakiet symboli.

> [!Note]
> Starszy format `.symbols.nupkg` nadal jest obsługiwany, ale tylko ze względu na zgodność (zobacz [starsze pakiety symboli](Symbol-Packages.md)). NuGet. serwer symboli organizacji akceptuje tylko nowy format pakietu symboli — `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publikowanie pakietu symboli

1. Dla wygody najpierw Zapisz klucz interfejsu API za pomocą narzędzia NuGet (zobacz [Publikowanie pakietu](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po opublikowaniu pakietu podstawowego w programie nuget.org wypchnij pakiet symboli w następujący sposób.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Możesz również wypchnąć zarówno podstawowe, jak i w tym samym czasie pakiety symboli przy użyciu poniższego polecenia. Oba pliki. nupkg i. snupkg muszą znajdować się w bieżącym folderze.

    ```cli
    nuget push MyPackage.nupkg
    ```

Program NuGet opublikuje Oba pakiety w nuget.org. `MyPackage.nupkg` zostanie opublikowany jako pierwszy, a następnie `MyPackage.snupkg`.

> [!Note]
> Jeśli pakiet symboli nie jest opublikowany, sprawdź, czy źródło NuGet.org zostało skonfigurowane jako `https://api.nuget.org/v3/index.json`. Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API programu NuGet v3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>Serwer symboli NuGet.org

NuGet.org obsługuje własne repozytorium serwera symboli i akceptuje tylko nowy format pakietu symboli — `.snupkg`. Odbiorcy pakietu mogą korzystać z symboli opublikowanych na serwerze symboli nuget.org przez dodawanie `https://symbols.nuget.org/download/symbols` do ich źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio. Aby uzyskać szczegółowe informacje na temat tego procesu, zobacz [Określanie symboli (. pdb) i plików źródłowych w debugerze programu Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

### <a name="nugetorg-symbol-package-constraints"></a>Ograniczenia pakietu symboli NuGet.org

NuGet.org ma następujące ograniczenia dotyczące pakietów symboli:

- W pakietach symboli są dozwolone tylko następujące rozszerzenia plików: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- Tylko zarządzane [plików PDB przenośne](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obsługiwane przez pakiet NuGet. serwer symboli w organizacji.
- Plików PDB i skojarzone z nimi biblioteki DLL NUPKG muszą być kompilowane przy użyciu kompilatora w programie Visual Studio w wersji 15,9 lub nowszej (zobacz [skrót kryptografii PDB](https://github.com/dotnet/roslyn/issues/24429))

W przypadku, gdy te ograniczenia nie są spełnione, pakiety symboli opublikowane w programie NuGet.org będą kończyć się niepowodzeniem. 

### <a name="symbol-package-validation-and-indexing"></a>Walidacja i indeksowanie pakietu symboli

Pakiety symboli opublikowane w [NuGet.org](https://www.nuget.org/) przechodzą kilka walidacji, w tym skanowanie złośliwego oprogramowania. Jeśli pakiet nie zostanie zweryfikowany, na stronie szczegółów pakietu zostanie wyświetlony komunikat o błędzie. Ponadto właściciele pakietu otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu rozwiązywania zidentyfikowanych problemów.

Gdy pakiet symboli przeszedł wszystkie walidacje, symbole będą indeksowane przez NuGet. serwery symboli w organizacji. Po indeksowaniu symbol będzie dostępny do użycia z serwerów symboli NuGet.org.

Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa 15 minut. Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.NuGet.org](https://status.nuget.org/) , aby sprawdzić, czy w NuGet.org występują jakiekolwiek przerwy. Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z pomocą techniczną na stronie Szczegóły pakietu.

## <a name="symbol-package-structure"></a>Struktura pakietu symboli

Plik. nupkg będzie dokładnie taki sam, jak dzisiaj, ale plik. snupkg ma następującą charakterystykę:

1) Element. snupkg będzie miał ten sam identyfikator i wersję co odpowiadający element. nupkg.
2) Plik. snupkg będzie miał dokładną strukturę folderów jako NUPKG dla każdej biblioteki DLL lub EXE z rozróżnieniem, które zamiast bibliotek DLL/exe, odpowiadające im plików PDB zostaną uwzględnione w tej samej hierarchii folderów. Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pozostawione z snupkg.
3) Plik. nuspec w pliku. snupkg określi również nowy element PackageType w następujący sposób. Powinien to być określony tylko jeden pakiet.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Jeśli autor zdecyduje się użyć niestandardowych nuspec do kompilowania ich NUPKG i snupkg, snupkg powinien mieć tę samą hierarchię folderów i pliki szczegółowe w 2).
5) pola ```authors``` i ```owners``` zostaną wykluczone z nuspec snupkg.
6) Nie należy używać elementu ```<license>```. A. snupkg jest objęta tą samą licencją co odpowiadające mu. nupkg.

## <a name="see-also"></a>Zobacz także

Rozważ użycie linku źródłowego, aby włączyć debugowanie kodu źródłowego zestawów .NET. Aby uzyskać więcej informacji, zapoznaj się ze [wskazówkami dotyczącymi linku do źródła](/dotnet/standard/library-guidance/sourcelink).

Aby uzyskać więcej informacji na temat pakietów symboli, zapoznaj się z artykułem [debugowanie pakietu NuGet & symbole udoskonalenia](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) projektu Specyfikacja.
