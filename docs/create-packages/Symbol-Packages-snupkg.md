---
title: Jak publikować pakiety symboli NuGet przy użyciu nowego formatu pakietu symboli ".snupkg" | Microsoft Docs
author: JonDouglas
ms.author: jodou
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak tworzyć pakiety symboli NuGet (snupkg).
keywords: Pakiety symboli NuGet, debugowanie pakietów NuGet, obsługa debugowania NuGet, symbole pakietów, konwencje pakietów symboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: a62996a28348bf95e4581af180597d72cd5aa298
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387338"
---
# <a name="creating-symbol-packages-snupkg"></a>Tworzenie pakietów symboli (snupkg)

Dobre środowisko debugowania opiera się na obecności symboli debugowania, ponieważ zapewniają one krytyczne informacje, takie jak skojarzenie między skompilowanym i kodem źródłowym, nazwy zmiennych lokalnych, ślady stosu i inne. Za pomocą pakietów symboli (snupkg) można rozpowszechniać te symbole i ulepszać środowisko debugowania pakietów NuGet.

> Należy pamiętać, że pakiet symboli nie jest jedyną strategią, aby udostępnić symbole debugowania klientom biblioteki. Można je również [mieć w `embed` ](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) obiekcie lub z `dll` `exe` następującą właściwością projektu:`<DebugType>embedded</DebugType>`

## <a name="prerequisites"></a>Wymagania wstępne

[nuget.exe w wersji 4.9.0](https://www.nuget.org/downloads) lub powyższej albo interfejs wiersza polecenia dotnet w wersji [2.2.0](https://www.microsoft.com/net/download/dotnet-core/2.2)lub wersji powyżej , które implementują wymagane [protokoły NuGet.](../api/nuget-protocols.md)

## <a name="creating-a-symbol-package"></a>Tworzenie pakietu symboli

Jeśli używasz interfejsu wiersza polecenia dotnet lub programu MSBuild, musisz ustawić właściwości i , aby oprócz pliku nupkg utworzyć plik `IncludeSymbols` `SymbolPackageFormat` zippkg.

* Dodaj następujące właściwości do pliku csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Możesz też określić następujące właściwości w wierszu polecenia:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  lub

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Jeśli używasz narzędzia NuGet.exe, możesz użyć następujących poleceń, aby utworzyć plik zippkg oprócz pliku .nupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Właściwość [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) może mieć jedną z dwóch wartości: `symbols.nupkg` (wartość domyślna) lub `snupkg` . Jeśli ta właściwość nie zostanie określona, zostanie utworzony starszy pakiet symboli.

> [!Note]
> Starszy format jest nadal obsługiwany, ale tylko ze względu na zgodność, na przykład pakiety `.symbols.nupkg` natywne (zobacz [Starsze pakiety symboli).](Symbol-Packages.md) Serwer symboli nuGet.org akceptuje tylko nowy format pakietu symboli — `.snupkg` .

## <a name="publishing-a-symbol-package"></a>Publikowanie pakietu symboli

1. Dla wygody najpierw zapisz klucz interfejsu API za pomocą pakietu NuGet (zobacz [publikowanie pakietu](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po opublikowaniu pakietu podstawowego w nuget.org wypchnąć pakiet symboli w następujący sposób.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Możesz również wypchnąć jednocześnie pakiety podstawowe i symboli za pomocą poniższego polecenia. Zarówno pliki .nupkg, jak i .tabpkg muszą być obecne w bieżącym folderze.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet opublikuje oba pakiety w nuget.org. `MyPackage.nupkg` Zostanie najpierw opublikowany, a następnie `MyPackage.snupkg` .

> [!Note]
> Jeśli pakiet symboli nie został opublikowany, sprawdź, czy skonfigurowano źródło NuGet.org jako `https://api.nuget.org/v3/index.json` . Publikowanie pakietów symboli jest obsługiwane tylko przez [interfejs API NuGet w wersji 3.](../api/overview.md#versioning)

## <a name="nugetorg-symbol-server"></a>NuGet.org serwera symboli

NuGet.org obsługuje własne repozytorium serwerów symboli i akceptuje tylko nowy format pakietu symboli — `.snupkg` . Odbiorcy pakietów mogą używać symboli opublikowanych na serwerze symboli nuget.org przez dodanie ich do źródeł symboli w u Visual Studio, co umożliwia przechodzenie do kodu pakietu w Visual Studio `https://symbols.nuget.org/download/symbols` debugerze. Szczegółowe informacje na temat tego procesu można znaleźć w temacie [Specify symbol (.pdb) and source files in the Visual Studio debugger (Określanie plików symboli (pdb)](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) i plików źródłowych w Visual Studio debugerze.

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org ograniczeń pakietu symboli

NuGet.org ma następujące ograniczenia dotyczące pakietów symboli:

- W pakietach symboli dozwolone są tylko następujące rozszerzenia plików: `.pdb` , , , , , `.nuspec` `.xml` `.psmdcp` `.rels` , `.p7s`
- Na serwerze [symboli](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) nuGet.org są obsługiwane tylko zarządzane przenośne pliki PDB.
- Pliki PDB i skojarzone z nimi biblioteki DLL nupkg muszą zostać skumulowane przy użyciu kompilatora w wersji Visual Studio 15.9 lub nowszej (zobacz skrót kryptograficzny pliku [PDB](https://github.com/dotnet/roslyn/issues/24429))

Pakiety symboli opublikowane w NuGet.org sprawdzanie poprawności nie powiedzie się, jeśli te ograniczenia nie zostaną spełnione. 

> [!NOTE]
> Projekty natywne, takie jak projekty języka C++, tworzyć pliki PDB systemu Windows zamiast przenośnych plików PDB. Nie są one obsługiwane przez serwer symboli NuGet.org. Zamiast tego użyj [starszych pakietów symboli.](Symbol-Packages.md)

### <a name="symbol-package-validation-and-indexing"></a>Walidacja i indeksowanie pakietu symboli

Pakiety symboli opublikowane [w NuGet.org](https://www.nuget.org/) przechodzą kilka weryfikacji, w tym skanowanie w poszukiwaniu złośliwego oprogramowania. Jeśli sprawdzenie poprawności pakietu zakończy się niepowodzeniem, na stronie szczegółów pakietu zostanie wyświetlony komunikat o błędzie. Ponadto właściciele pakietu otrzymają wiadomość e-mail z instrukcjami dotyczącymi sposobu rozwiązania zidentyfikowanych problemów.

Po zatwierdzeniu wszystkich weryfikacji przez pakiet symboli symbole zostaną zindeksowane przez serwery symboli NuGet.org i będą dostępne do użycia.

Walidacja i indeksowanie pakietów zwykle trwa poniżej 15 minut. Jeśli publikowanie pakietów trwa dłużej niż oczekiwano, odwiedź [status.nuget.org,](https://status.nuget.org/) aby sprawdzić, NuGet.org występują jakieś przerwy w działaniu. Jeśli wszystkie systemy są operacyjne i pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do witryny nuget.org i skontaktuj się z nami przy użyciu linku Skontaktuj się z pomocą techniczną na stronie szczegółów pakietu.

## <a name="symbol-package-structure"></a>Struktura pakietu symboli

Pakiet symboli (snupkg) ma następujące cechy:

1) Pakiet .snupkg ma ten sam identyfikator i wersję co odpowiadający mu pakiet NuGet (nupkg).
2) Plik .snupkg ma taką samą strukturę folderów jak odpowiadający mu plik nupkg dla wszystkich plików DLL lub EXE z różnicą, że zamiast plików DLL/EXE odpowiednie pliki PDB zostaną uwzględnione w tej samej hierarchii folderów. Pliki i foldery z rozszerzeniami innymi niż PDB zostaną pozostawione poza plikiem tabupkg.
3) Plik nuspec pakietu symboli ma `SymbolsPackage` typ pakietu:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Jeśli autor zdecyduje się na użycie niestandardowego programu nuspec do skompilowania swoich plików nupkg i snupkg, pakiet snupkg powinien mieć tę samą hierarchię folderów i pliki szczegółowo opisane w 2).
5) Następujące pola zostaną wykluczone z nuspec tego nuspec: ```authors``` , , , , i ```owners``` ```requireLicenseAcceptance``` ```license type``` ```licenseUrl```  ```icon``` .
6) Nie używaj ```<license>``` elementu . Pakiet .snupkg jest objęty taką samą licencją jak odpowiedni .nupkg.

## <a name="see-also"></a>Zobacz też

Rozważ użycie linku źródłowego, aby włączyć debugowanie kodu źródłowego zestawów .NET. Aby uzyskać więcej informacji, zapoznaj się ze [wskazówkami linku źródłowego](/dotnet/standard/library-guidance/sourcelink).

Aby uzyskać więcej informacji na temat pakietów symboli, zapoznaj się ze specyfikacją projektu Debugowanie pakietów [NuGet & symboli.](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)