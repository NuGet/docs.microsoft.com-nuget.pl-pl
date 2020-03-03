---
title: Pakiet interfejsu wiersza polecenia NuGet
description: Dokumentacja polecenia NuGet. exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 2358cedc05520a3ec82a39aef34b6d467e44460b
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231165"
---
# <a name="pack-command-nuget-cli"></a>pack command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** tworzenie pakietu &bullet; **obsługiwane wersje:** 2.7 +

Tworzy pakiet NuGet na podstawie określonego pliku [. nuspec](../nuspec.md) lub projektu. Polecenie `dotnet pack` (zobacz [polecenia dotnet](../dotnet-Commands.md)) i `msbuild -t:pack` (zobacz [elementy docelowe programu MSBuild](../msbuild-targets.md)) mogą być używane jako alternatywy.

> [!Important]
> Użyj [`dotnet pack`](../dotnet-Commands.md) lub [`msbuild -t:pack`](../msbuild-targets.md) dla projektów opartych na [PackageReference](../../consume-packages/package-references-in-project-files.md) .
> W obszarze mono Tworzenie pakietu z pliku projektu nie jest obsługiwane. Należy również dostosować ścieżki nielokalne w pliku `.nuspec` do ścieżek w stylu systemu UNIX, ponieważ program NuGet. exe nie konwertuje samych nazw ścieżek systemu Windows.

## <a name="usage"></a>Sposób użycia

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

gdzie `<nuspecPath>` i `<projectPath>` określają odpowiednio `.nuspec` lub plik projektu.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| BasePath | Ustawia ścieżkę podstawową plików zdefiniowanych w pliku [. nuspec](../nuspec.md) . |
| Kompilacja | Określa, że projekt powinien zostać skompilowany przed skompilowaniem pakietu. |
| Exclude | Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu. Aby określić więcej niż jeden wzorzec, powtórz flagę-Exclude. Zobacz przykład poniżej. |
| ExcludeEmptyDirectories | Uniemożliwia dołączenie pustych katalogów podczas kompilowania pakietu. |
| ForceEnglishOutput | *(3.5 +)* Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury. |
| ConfigFile | Określ plik konfiguracji dla polecenia pakietu. |
| Pomoc | Wyświetla informacje pomocy dla polecenia. |
| IncludeReferencedProjects | Wskazuje, że skompilowany pakiet powinien zawierać przywoływane projekty jako zależności lub jako część pakietu. Jeśli projekt, do którego istnieje odwołanie, ma odpowiedni plik `.nuspec`, który ma taką samą nazwę jak projekt, przywoływany projekt jest dodawany jako zależność. W przeciwnym razie przywoływany projekt zostanie dodany jako część pakietu. |
| MinClientVersion | Ustaw atrybut *minClientVersion* dla utworzonego pakietu. Ta wartość spowoduje przesłonięcie wartości istniejącego atrybutu *minClientVersion* (jeśli istnieje) w pliku `.nuspec`. |
| MSBuildPath | *(4.0 +)* Określa ścieżkę programu MSBuild do użycia z poleceniem, która ma pierwszeństwo przed `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Określa wersję programu MSBuild, która ma być używana z tym poleceniem. Obsługiwane wartości to 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Domyślnie program MSBuild w ścieżce jest wybierany, w przeciwnym razie domyślnie jest to najwyższa zainstalowana wersja programu MSBuild. |
| NoDefaultExcludes | Zapobiega domyślnemu wykluczeniu plików pakietów NuGet oraz plików i folderów zaczynających się od kropki, takich jak `.svn` i `.gitignore`. |
| NoPackageAnalysis | Określa, że pakiet nie powinien uruchamiać analizy pakietu po skompilowaniu pakietu. |
| OutputDirectory | Określa folder, w którym jest przechowywany utworzony pakiet. Jeśli folder nie zostanie określony, używany jest bieżący folder. |
| Właściwości | Powinna zostać wyświetlona jako Ostatnia w wierszu polecenia po innych opcjach. Określa listę właściwości, które zastępują wartości w pliku projektu; Zobacz [wspólne właściwości projektu MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) dla nazw właściwości. Argument właściwości znajduje się na liście par token = wartość, oddzielonych średnikami, gdzie każde wystąpienie `$token$` w pliku `.nuspec` zostanie zastąpione daną wartością. Wartości mogą być ciągami w cudzysłowie. Należy pamiętać, że w przypadku właściwości "Configuration" wartością domyślną jest "debug". Aby zmienić konfigurację wydania, użyj `-Properties Configuration=Release`. **Ogólnie rzecz**biorąc, właściwości powinny być takie same, jak w odpowiednich `nuget build`, aby uniknąć potencjalnie nietypowego zachowania. |
| Suffix | *(3.4.4 +)* Dołącza sufiks do wewnętrznie wygenerowanego numeru wersji, zazwyczaj używany do dołączania kompilacji lub innych identyfikatorów w wersji wstępnej. Na przykład za pomocą `-suffix nightly` utworzy pakiet z numerem wersji, takim jak `1.2.3-nightly`. Sufiksy muszą zaczynać się literą, aby uniknąć ostrzeżeń, błędów i potencjalnych niezgodności z różnymi wersjami programu NuGet i Menedżera pakietów NuGet. |
| Symbole | Określa, że pakiet zawiera źródła i symbole. Gdy jest używany z plikiem `.nuspec`, tworzy on zwykły plik pakietu NuGet i odpowiedni pakiet symboli. Domyślnie tworzy on [starszy pakiet symboli](../../create-packages/Symbol-Packages.md). Nowy zalecany format pakietów symboli to. snupkg. Zobacz [Tworzenie pakietów symboli (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Narzędzie | Określa, że pliki wyjściowe projektu należy umieścić w folderze `tool`. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*. |
| Wersja | Zastępuje numer wersji z pliku `.nuspec`. |

Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Wykluczanie zależności programistycznych

Niektóre pakiety NuGet są przydatne jako zależności programistyczne, które ułatwiają tworzenie własnych bibliotek, ale nie muszą być potrzebne jako rzeczywiste zależności pakietów.

`pack` polecenie zignoruje `package` wpisów w `packages.config`, które mają atrybut `developmentDependency` ustawiony na `true`. Te wpisy nie zostaną uwzględnione jako zależności w utworzonym pakiecie.

Rozważmy na przykład następujący plik `packages.config` w projekcie źródłowym:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Dla tego projektu pakiet utworzony przez `nuget pack` będzie miał zależność od `jQuery` i `microsoft-web-helpers` ale nie `netfx-Guard`.

## <a name="suppressing-pack-warnings"></a>Pomijanie ostrzeżeń pakietu

Mimo że zaleca się rozwiązanie wszystkich ostrzeżeń NuGet podczas operacji pakietu, w niektórych sytuacjach pomijanie ich jest uzasadnione.

Można to osiągnąć w następujący sposób: 

> NuGet. exe Pack Package. nuspec-Properties nowarn = NU5104

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
