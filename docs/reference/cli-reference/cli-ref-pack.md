---
title: Pakiet interfejsu wiersza polecenia NuGet
description: Informacje dotyczące polecenia nuget.exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622957"
---
# <a name="pack-command-nuget-cli"></a>Pack — polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** &bullet; **obsługiwane wersje** tworzenia pakietów: 2.7 +

Tworzy pakiet NuGet na podstawie określonego pliku [. nuspec](../nuspec.md) lub projektu. `dotnet pack`Polecenie (zobacz [polecenia dotnet](../dotnet-Commands.md)) i `msbuild -t:pack` (zobacz [elementy docelowe programu MSBuild](../msbuild-targets.md)) może być używane jako alternatywy.

> [!Important]
> Użyj [`dotnet pack`](../dotnet-Commands.md) lub [`msbuild -t:pack`](../msbuild-targets.md) dla projektów opartych na [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> W obszarze mono Tworzenie pakietu z pliku projektu nie jest obsługiwane. Należy również dostosować ścieżki nielokalne w `.nuspec` pliku do ścieżek w stylu systemu UNIX, ponieważ nuget.exe nie konwertują samych nazw ścieżek systemu Windows.

## <a name="usage"></a>Użycie

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

gdzie `<nuspecPath>` i `<projectPath>` Określ `.nuspec` odpowiednio plik projektu lub.

## <a name="options"></a>Opcje
- **`-BasePath`**

   Ustawia ścieżkę podstawową plików zdefiniowanych w pliku [. nuspec](../nuspec.md) .

- **`-Build`**

  Określa, że projekt powinien zostać skompilowany przed skompilowaniem pakietu.

- **`-ConfigFile`**

  Plik konfiguracji NuGet, który ma zostać zastosowany. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-Exclude`**

  Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu. Aby określić więcej niż jeden wzorzec, powtórz flagę-Exclude. Zobacz przykład poniżej.

- **`-ExcludeEmptyDirectories`**

  Uniemożliwia dołączenie pustych katalogów podczas kompilowania pakietu.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dla polecenia.

- **`-IncludeReferencedProjects`**

  Wskazuje, że skompilowany pakiet powinien zawierać przywoływane projekty jako zależności lub jako część pakietu. Jeśli projekt, do którego istnieje odwołanie `.nuspec` , ma odpowiedni plik, który ma taką samą nazwę jak projekt, ten, do którego odwołuje się projekt, jest dodawany jako zależność. W przeciwnym razie przywoływany projekt zostanie dodany jako część pakietu.

- **`-InstallPackageToOutputPath`**

  Określ, czy polecenie ma przygotować katalog wyjściowy pakietu, aby obsługiwał udział jako źródło danych.

- **`-MinClientVersion`**

  Ustaw atrybut *minClientVersion* dla utworzonego pakietu. Ta wartość spowoduje przesłonięcie wartości istniejącego atrybutu *minClientVersion* (jeśli istnieje) w `.nuspec` pliku.

- **`-MSBuildPath`**

  *(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, które ma pierwszeństwo przed `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild.

- **`-NoDefaultExcludes`**

  Zapobiega domyślnemu wykluczeniu plików pakietów NuGet oraz plików i folderów rozpoczynających się od kropki, takich jak `.svn` i `.gitignore` .

- **`-NonInteractive`**

  Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.

- **`-NoPackageAnalysis`**

  Określa, że pakiet nie powinien uruchamiać analizy pakietu po skompilowaniu pakietu.

- **`-OutputDirectory`**

  Określa folder, w którym jest przechowywany utworzony pakiet. Jeśli folder nie zostanie określony, używany jest bieżący folder.

- **`-OutputFileNamesWithoutVersion`**

  Określ, czy polecenie ma przygotować nazwę wyjściową pakietu bez wersji.

- **`-PackagesDirectory`**

  Określa folder Packages.

- **`-p|-Properties`**

  Powinna zostać wyświetlona jako Ostatnia w wierszu polecenia po innych opcjach. Określa listę właściwości, które zastępują wartości w pliku projektu; Zobacz [wspólne właściwości projektu MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) dla nazw właściwości. Argument właściwości znajduje się na liście par token = wartość, oddzielonych średnikami, gdzie każde wystąpienie `$token$` w `.nuspec` pliku zostanie zastąpione daną wartością. Wartości mogą być ciągami w cudzysłowie. Należy pamiętać, że w przypadku właściwości "Configuration" wartością domyślną jest "debug". Aby zmienić konfigurację wydania, użyj programu `-Properties Configuration=Release` . **Ogólnie rzecz**biorąc, właściwości powinny być takie same, które były używane podczas odpowiedniej kompilacji projektu, aby uniknąć potencjalnie nietypowego zachowania.

- **`-SolutionDirectory`**

  Określa katalog rozwiązania.

- **`-Suffix`**

  *(3.4.4 +)* Dołącza sufiks do wewnętrznie wygenerowanego numeru wersji, zazwyczaj używany do dołączania kompilacji lub innych identyfikatorów w wersji wstępnej. Na przykład za pomocą `-suffix nightly` program utworzy pakiet z numerem wersji podobnym do `1.2.3-nightly` . Sufiksy muszą zaczynać się literą, aby uniknąć ostrzeżeń, błędów i potencjalnych niezgodności z różnymi wersjami programu NuGet i Menedżera pakietów NuGet.

- **`-SymbolPackageFormat`**

  Podczas tworzenia pakietu symboli, umożliwia wybór między `snupkg` `symbols.nupkg` formatem a.

- **`-Symbols`**

  Określa, że pakiet zawiera źródła i symbole. W przypadku użycia z `.nuspec` plikiem tworzony jest zwykły plik pakietu NuGet i odpowiedni pakiet symboli. Domyślnie tworzy on [starszy pakiet symboli](../../create-packages/Symbol-Packages.md). Nowy zalecany format pakietów symboli to. snupkg. Zobacz [Tworzenie pakietów symboli (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).

- **`-Tool`**

   Określa, że pliki wyjściowe projektu powinny zostać umieszczone w `tool` folderze.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .

- **`-Version`**

  Zastępuje numer wersji z `.nuspec` pliku.

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Wykluczanie zależności programistycznych

Niektóre pakiety NuGet są przydatne jako zależności programistyczne, które ułatwiają tworzenie własnych bibliotek, ale nie muszą być potrzebne jako rzeczywiste zależności pakietów.

`pack`Polecenie zignoruje `package` wpisy w `packages.config` , które mają `developmentDependency` atrybut ustawiony na `true` . Te wpisy nie zostaną uwzględnione jako zależności w utworzonym pakiecie.

Rozważmy na przykład następujący `packages.config` plik w projekcie źródłowym:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Dla tego projektu pakiet utworzony przez ma `nuget pack` zależność od elementu `jQuery` , `microsoft-web-helpers` ale nie `netfx-Guard` .

## <a name="suppressing-pack-warnings"></a>Pomijanie ostrzeżeń pakietu

Mimo że zaleca się rozwiązanie wszystkich ostrzeżeń NuGet podczas operacji pakietu, w niektórych sytuacjach pomijanie ich jest uzasadnione.

Można to osiągnąć w następujący sposób: 

> Pakiet nuget.exe Pack nuspec-Properties nowarn = NU5104

## <a name="examples"></a>Przykłady

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
