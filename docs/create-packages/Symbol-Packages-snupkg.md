---
title: Jak opublikować pakiety symboli NuGet przy użyciu nowego formatu pakietu symboli '.snupkg'| Dokumenty firmy Microsoft
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak utworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, debugowanie pakietu NuGet, obsługa debugowania NuGet, symbole pakietów, konwencje pakietów symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380421"
---
# <a name="creating-symbol-packages-snupkg"></a>Tworzenie pakietów symboli (.snupkg)

Dobre środowisko debugowania opiera się na obecności symboli debugowania, ponieważ zapewniają one krytyczne informacje, takie jak skojarzenie między skompilowanym i kodem źródłowym, nazwy zmiennych lokalnych, ślady stosu i więcej. Można użyć pakietów symboli (.snupkg) do dystrybucji tych symboli i poprawić środowisko debugowania pakietów NuGet.

## <a name="prerequisites"></a>Wymagania wstępne

[nuget.exe v4.9.0 lub powyżej](https://www.nuget.org/downloads) lub [dotnet CLI v2.2.0 lub wyższy](https://www.microsoft.com/net/download/dotnet-core/2.2), które implementują wymagane [protokoły NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Tworzenie pakietu symboli

Jeśli używasz dotnet CLI lub MSBuild, musisz `IncludeSymbols` `SymbolPackageFormat` ustawić właściwości i, aby utworzyć plik .snupkg oprócz pliku .nupkg.

* Dodaj następujące właściwości do pliku csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Możesz też określić te właściwości w wierszu polecenia:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  lub

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Jeśli używasz programu NuGet.exe, możesz użyć następujących poleceń, aby utworzyć plik .snupkg oprócz pliku nupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Właściwość [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) może mieć jedną `symbols.nupkg` z dwóch wartości: (domyślnie) lub `snupkg`. Jeśli ta właściwość nie jest określona, zostanie utworzony starszy pakiet symboli.

> [!Note]
> Starszy format `.symbols.nupkg` jest nadal obsługiwany, ale tylko ze względu na zgodność (patrz [Starsze pakiety symboli).](Symbol-Packages.md) Serwer symboli NuGet.org akceptuje tylko nowy format `.snupkg`pakietu symboli - .

## <a name="publishing-a-symbol-package"></a>Publikowanie pakietu symboli

1. Dla wygody najpierw zapisz klucz interfejsu API za pomocą programu NuGet (zobacz [publikowanie pakietu).](../nuget-org/publish-a-package.md)

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po opublikowaniu pakietu podstawowego do nuget.org wypchnij pakiet symboli w następujący sposób.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Można również wypchnąć pakiety podstawowe i symbole w tym samym czasie za pomocą polecenia poniżej. Zarówno pliki .nupkg, jak i .snupkg muszą znajdować się w bieżącym folderze.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet opublikuje oba pakiety do nuget.org. `MyPackage.nupkg` zostanie opublikowana jako pierwsza, a następnie `MyPackage.snupkg`.

> [!Note]
> Jeśli pakiet symboli nie został opublikowany, sprawdź, czy źródło NuGet.org zostało `https://api.nuget.org/v3/index.json`skonfigurowane jako . Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>Serwer NuGet.org symboli

NuGet.org obsługuje własne repozytorium serwerowe symboli i akceptuje tylko nowy `.snupkg`format pakietu symboli - . Konsumenci pakietów mogą używać symboli opublikowanych do nuget.org `https://symbols.nuget.org/download/symbols` serwera symboli, dodając do swoich źródeł symboli w programie Visual Studio, co umożliwia przechodzenie do kodu pakietu w debugerze programu Visual Studio. Zobacz [Określanie symbolu (pdb) i plików źródłowych w debugerze programu Visual Studio, aby](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) uzyskać szczegółowe informacje na temat tego procesu.

### <a name="nugetorg-symbol-package-constraints"></a>Ograniczenia pakietu NuGet.org symboli

NuGet.org ma następujące ograniczenia dla pakietów symboli:

- W pakietach symboli dozwolone są tylko `.pdb` `.nuspec`następujące `.xml` `.psmdcp`rozszerzenia `.rels`plików: , , , ,`.p7s`
- Tylko zarządzane [przenośne kontrolery domeny](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) są obsługiwane na serwerze symboli NuGet.org.
- Biblioteki DLL i skojarzone z nimi biblioteki DLL .nupkg muszą być budowane za pomocą kompilatora w programie Visual Studio w wersji 15.9 lub nowszej (zobacz [skrót kryptograficzny PDB](https://github.com/dotnet/roslyn/issues/24429))

Pakiety symboli opublikowane w NuGet.org zakończy się niepowodzeniem sprawdzania poprawności, jeśli te ograniczenia nie są spełnione. 

### <a name="symbol-package-validation-and-indexing"></a>Sprawdzanie poprawności i indeksowanie pakietu symboli

Pakiety symboli opublikowane [w celu NuGet.org](https://www.nuget.org/) przechodzą kilka weryfikacji, w tym skanowanie złośliwego oprogramowania. Jeśli pakiet nie powiedzie się sprawdzanie poprawności, jego szczegóły pakietu strona wyświetli komunikat o błędzie. Ponadto właściciele pakietu otrzymają wiadomość e-mail z instrukcjami dotyczącymi rozwiązywania zidentyfikowanych problemów.

Gdy pakiet symboli przeszedł wszystkie weryfikacje, symbole zostaną zindeksowane przez serwery symboli NuGet.org i będą dostępne do użycia.

Sprawdzanie poprawności i indeksowanie pakietów zwykle trwa mniej niż 15 minut. Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź [status.nuget.org,](https://status.nuget.org/) aby sprawdzić, czy NuGet.org występują przerwy. Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie szczegółów pakietu.

## <a name="symbol-package-structure"></a>Struktura pakietu symboli

Pakiet symboli (.snupkg) ma następujące właściwości:

1) .snupkg ma ten sam identyfikator i wersję co odpowiadający mu pakiet NuGet (.nupkg).
2) .snupkg ma taką samą strukturę folderów jak odpowiadający jej .nupkg dla dowolnych plików DLL lub EXE z rozróżnieniem, że zamiast bibliotek DLL/EXE, ich odpowiednie pliki PDB zostaną uwzględnione w tej samej hierarchii folderów. Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pominięte w snupkg.
3) Plik .nuspec pakietu symboli `SymbolsPackage` ma typ pakietu:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Jeśli autor zdecyduje się użyć niestandardowego nuspec do zbudowania nupkg i snupkg, snupkg powinien mieć tę samą hierarchię folderów i pliki wyszczególnione w 2).
5) Z nuspec snupkg wyłączone ```authors```będą następujące pola: ```owners``` ```requireLicenseAcceptance```, ```license type``` ```licenseUrl```, ```icon```, , i .
6) Nie należy ```<license>``` używać elementu. A .snupkg jest objęty tą samą licencją co odpowiadający mu plik .nupkg.

## <a name="see-also"></a>Zobacz też

Należy rozważyć użycie łącza źródłowego, aby włączyć debugowanie kodu źródłowego zestawów .NET. Aby uzyskać więcej informacji, zapoznaj się ze [wskazówkami dotyczącymi łącza źródłowego](/dotnet/standard/library-guidance/sourcelink).

Aby uzyskać więcej informacji na temat pakietów symboli, zapoznaj się z [nuget pakiet debugowania & symbole ulepszenia specyfikacji](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) projektu.
