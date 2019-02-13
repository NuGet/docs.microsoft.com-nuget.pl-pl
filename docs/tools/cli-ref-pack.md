---
title: Polecenie pakietu NuGet interfejsu wiersza polecenia
description: Dokumentacja dotycząca poleceń pakietu nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9db24b2dd6ced0869ac84b25f9796ded5df10f86
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145647"
---
# <a name="pack-command-nuget-cli"></a>pack command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** Tworzenie pakietu &bullet; **obsługiwane wersje:** 2.7+

Tworzy pakiet NuGet na podstawie `.nuspec` lub pliku projektu. `dotnet pack` Polecenia (zobacz [polecenia dotnet](dotnet-Commands.md)) i `msbuild -t:pack` (zobacz [elementów docelowych MSBuild](../reference/msbuild-targets.md)) może być używany jako wersje alternatywne.

> [!Important]
> W obszarze platformy Mono Tworzenie pakietu z pliku projektu nie jest obsługiwane. Trzeba będzie również dostosować ścieżek inną niż lokalna w `.nuspec` plików do ścieżek typu Unix nuget.exe nie konwertuje nazwy ścieżek Windows, sam.

## <a name="usage"></a>Użycie

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

gdzie `<nuspecPath>` i `<projectPath>` określ `.nuspec` lub projektu pliku, odpowiednio.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| BasePath | Ustawia ścieżki podstawowej plików zdefiniowanych w `.nuspec` pliku. |
| Kompilacja | Określa, czy projektu powinny zostać skompilowane przed kompilacją pakietu. |
| Wyklucz | Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu. Aby określić więcej niż jeden wzorzec, powtórz flagi - wykluczania. Zobacz przykład poniżej. |
| ExcludeEmptyDirectories | Uniemożliwia włączenie puste katalogi, podczas tworzenia pakietu. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| ConfigFile | Określ plik konfiguracji dla polecenia pakietu. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| IncludeReferencedProjects | Wskazuje, że utworzone pakiet powinien zawierać przywoływane projekty, jako zależności lub jako część pakietu. Jeśli przywoływany projekt ma odpowiadające mu `.nuspec` pliku, który ma taką samą nazwę jak projektu, a następnie przywoływanego projektu zostanie dodany jako zależność. W przeciwnym razie przywoływany projekt jest dodawany jako część pakietu. |
| MinClientVersion | Ustaw *atrybutu minClientVersion* atrybut utworzony pakiet. Ta wartość zastępuje wartość istniejącej *atrybutu minClientVersion* atrybutu (jeśli istnieją) w `.nuspec` pliku. |
| MSBuildPath | *(4.0 +)*  Określa ścieżkę program MSBuild będzie używać za pomocą polecenia pierwszeństwo `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Określa numer wersji MSBuild ma być używany za pomocą tego polecenia. Obsługiwane wartości to 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Domyślnie program MSBuild w ścieżce jest pobierana w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild. |
| NoDefaultExcludes | Zapobiega domyślne wykluczenia pakietu nuget pakowanie plików i plików i folderów, rozpoczynając od kropki, takich jak `.svn` i `.gitignore`. |
| NoPackageAnalysis | Określa, że pakiet nie należy uruchamiać analizy pakietu po utworzeniu pakietu. |
| OutputDirectory | Określa folder, w którym utworzono pakiet jest przechowywany. Jeśli żaden folder jest określony, używany jest bieżącego folderu. |
| Właściwości | Powinien zostać wyświetlony ostatni wiersz polecenia po innych opcji. Określa listę właściwości, które zastępują wartości w pliku projektu. zobacz [wspólne właściwości projektów MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) dla nazw właściwości. Argument właściwości w tym miejscu znajduje się lista token = pary wartości, oddziel je średnikami, gdzie każde wystąpienie `$token$` w `.nuspec` pliku zostaną zastąpione danej wartości. Możliwe wartości ciągów w znaki cudzysłowu. Należy pamiętać, że dla właściwości "Konfiguracja", wartość domyślna to "Debug". Aby zmienić konfigurację wydania, należy użyć `-Properties Configuration=Release`. |
| Suffix | *(3.4.4+)*  Dołącza sufiks numerowi wersji wewnętrznie generowane, zwykle używane do wykonania operacji dołączania kompilacji lub innych identyfikatorów w wersji wstępnej. Na przykład za pomocą `-suffix nightly` spowoduje utworzenie pakietu z podobny do numeru wersji `1.2.3-nightly`. Sufiksy musi zaczynać się literą, aby uniknąć ostrzeżenia, błędy i potencjalnych niezgodności z użyciem różnych wersji programu NuGet i Menedżer pakietów NuGet. |
| Symbole | Określa, że pakiet zawiera źródła i symboli. Gdy jest używane z `.nuspec` pliku, spowoduje to utworzenie pliku pakietu NuGet regularnych oraz odpowiednich symboli pakietu. Domyślnie tworzy [symbol starszej wersji pakietu](../create-packages/Symbol-Packages.md). Nowy format zalecane pakiety symboli jest .snupkg. Zobacz [tworzenia pakietów symbol (.snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| Narzędzie | Określa, że pliki wyjściowe projektu, należy umieścić w `tool` folderu. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*. |
| Wersja | Zastępuje numer wersji z `.nuspec` pliku. |

Zobacz też [zmiennych środowiskowych](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Z wyjątkiem tworzenia zależności

Niektóre pakiety NuGet są przydatne jako zależności programowania, które pomagają tworzyć własne biblioteki, ale niekoniecznie nie są wymagane jako zależności pakietów rzeczywistych.

`pack` Polecenie będzie ignorować `package` wpisów w `packages.config` , które mają `developmentDependency` ustawioną wartość atrybutu `true`. Te wpisy nie zostaną uwzględnione jako zależności w pakiecie utworzony.

Na przykład, należy wziąć pod uwagę następujące `packages.config` pliku w projekcie źródła:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Dla tego projektu, pakiet utworzony przez `nuget pack` będzie mieć zależność na `jQuery` i `microsoft-web-helpers` , ale nie `netfx-Guard`.

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
