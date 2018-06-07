---
title: Polecenie pakietu NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia pakiet nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3140d56ac827d932c2323182ad040b8a4d14da5c
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818042"
---
# <a name="pack-command-nuget-cli"></a>pack command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 2.7 +

Tworzy oparte na określony pakiet NuGet `.nuspec` lub pliku projektu. `dotnet pack` Polecenia (zobacz [polecenia dotnet](dotnet-Commands.md)) i `msbuild /t:pack` (zobacz [docelowych elementów MSBuild](../reference/msbuild-targets.md)) może być używany jako alternatyw.

> [!Important]
> W obszarze Mono Tworzenie pakietu z pliku projektu nie jest obsługiwane. Należy również dostosować innego niż lokalne ścieżki w `.nuspec` plików do ścieżek typu Unix, jak nuget.exe nie konwertuje nazwy ścieżek systemu Windows, sama.

## <a name="usage"></a>Użycie

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

gdzie `<nuspecPath>` i `<projectPath>` określ `.nuspec` lub odpowiednio projektu pliku.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| BasePath | Ustawia ścieżki podstawowej plików zdefiniowanych w `.nuspec` pliku. |
| Kompilacja | Określa, czy projekt powinien skompilowany przed zbudowaniem pakietu. |
| Wyklucz | Określa jeden lub więcej wzorców symboli wieloznacznych, które mają zostać wykluczone podczas tworzenia pakietu. Aby określić więcej niż jeden wzorzec, powtórz flagi - Exclude. Zobacz poniższy przykład. |
| ExcludeEmptyDirectories | Uniemożliwia włączenie puste katalogi, podczas tworzenia pakietu. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| IncludeReferencedProjects | Wskazuje, że wbudowanych pakiet powinien zawierać przywoływane projekty jako zależności lub jako część pakietu. Jeśli przywoływanego projektu ma odpowiadające mu `.nuspec` pliku, który ma taką samą nazwę jak projekt, do którego istnieje odwołanie projektu jest dodawana jako zależność. W przeciwnym razie przywoływanego projektu jest dodawana jako część pakietu. |
| Element MinClientVersion | Ustaw *minClientVersion* atrybutu utworzonego pakietu. Ta wartość zastępuje wartość istniejącej *minClientVersion* atrybutu (jeśli istnieją) w `.nuspec` pliku. |
| MSBuildPath | *(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia. Obsługiwane wartości to 4, 12, 14, 15. Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild. |
| NoDefaultExcludes | Zapobiega domyślne wykluczenie NuGet pakiet plików i pliki i foldery rozpoczynający się kropką, na przykład `.svn` i `.gitignore`. |
| NoPackageAnalysis | Określa, że pakiet nie należy uruchamiać analizy pakietu po utworzeniu pakietu. |
| OutputDirectory | Określa folder, w którym przechowywany jest utworzony pakiet. Jeśli folder nie jest określony, używany jest bieżący folder. |
| Właściwości | Powinna zostać wyświetlona ostatniego wiersza polecenia po innych opcji. Określa listę właściwości, które przesłaniają wartości w pliku projektu. zobacz [wspólne właściwości projektów MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) dla nazwy właściwości. Argument właściwości w tym miejscu znajduje się lista tokenu = pary wartości, oddziel je średnikami, gdzie każde wystąpienie `$token$` w `.nuspec` pliku zostaną zastąpione podanej wartości. Możliwe wartości ciągów w cudzysłowy. Należy pamiętać, że dla właściwości "Konfiguracja", wartość domyślna to "Debug". Aby zmienić konfigurację, wersji, należy użyć `-Properties Configuration=Release`. |
| Suffix | *(3.4.4+)*  Dołącza sufiks z numerem wersji wewnętrznie generowane zwykle używany w przypadku dołączania kompilacji lub innych identyfikatorów w wersji wstępnej. Na przykład za pomocą `-suffix nightly` utworzy pakiet z podobne do numeru wersji `1.2.3-nightly`. Sufiksy musi rozpoczynać się od litery, aby uniknąć potencjalnych niezgodności z różnymi wersjami programu NuGet i Menedżer pakietów NuGet, błędy i ostrzeżenia. |
| Symbole | Określa, że pakiet zawiera źródła i symbole. W przypadku użycia z `.nuspec` pliku, tworzy zwykły plik pakietu NuGet i odpowiedniego pakietu symboli. |
| Narzędzie | Określa, że pliki wyjściowe projektu powinna zostać umieszczona w `tool` folderu. |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |
| Wersja | Zastępuje numer wersji z `.nuspec` pliku. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Z wyjątkiem programowanie zależności

Niektóre pakiety NuGet są przydatne jako programowanie zależności, które ułatwiają tworzenie własnych biblioteki, ale niekoniecznie nie są wymagane jako zależności pakietów rzeczywiste.

`pack` Zignoruje polecenia `package` wpisów w `packages.config` zawierających `developmentDependency` ustawić atrybutu `true`. Te wpisy nie będzie zawierał jako zależności w pakiecie utworzony.

Na przykład, należy wziąć pod uwagę następujące `packages.config` plik w projekcie źródła:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Dla tego projektu, pakiet utworzony przez `nuget pack` będzie zależy od `jQuery` i `microsoft-web-helpers` , ale nie `netfx-Guard`.

## <a name="examples"></a>Przykłady

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
