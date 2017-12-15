---
title: Polecenie restore interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Informacje dotyczące polecenia restore nuget.exe"
keywords: "nuget przywrócić odwołania, przywrócić pakiety, polecenie"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a>polecenie Restore (NuGet CLI)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 2.7 +

NuGet 2.7 +: Pobiera i instaluje wszystkie pakiety brakuje `packages` folderu.

NuGet 3.3 + z projektami za pomocą `project.json`: generuje `project.lock.json` pliku i `<project>.nuget.props` plików, jeśli to konieczne. (Oba pliki można pominąć z kontroli źródła).

NuGet 4.0 + z projektem, w którym pakiecie odwołania znajdują się w pliku projektu bezpośrednio: generuje `<project>.nuget.props` pliku, w razie potrzeby w `obj` folderu. (Plik można pominąć z kontroli źródła).

Mac OS x i Linux z poziomu interfejsu wiersza polecenia na Mono Przywracanie pakietów nie jest obsługiwane w formacie PackageReference.

## <a name="usage"></a>Użycie

```
nuget restore <projectPath> [options]
```

gdzie `<projectPath>` Określa lokalizację rozwiązania, `packages.config` pliku, lub `project.json` pliku. Zobacz [uwagi](#remarks) poniżej behawioralnej szczegółowe informacje.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany. |
| DirectDownload | *(4.0 +)*  Pobiera pakiety bezpośrednio, bez wypełnianie pamięci podręczne z plików binarnych lub metadanych. |
| DisableParallelProcessing | Wyłącza Przywracanie wielu pakietów równolegle. |
| FallbackSource | *(3.2 +)*  Lista źródła pakietów do użycia jako przejścia, w przypadku, gdy nie można znaleźć pakietu w podstawowej lub źródło domyślne. |
| ForceEnglishOutput | *(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| MSBuildPath | *(4.0 +)*  Określa ścieżkę MSBuild do użycia z poleceniem pierwszeństwo `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Określa wersję programu MSBuild ma być używany z tego polecenia. Obsługiwane wartości to 4, 12, 14, 15. Domyślnie jest wybierany MSBuild w ścieżce w przeciwnym razie domyślnie najwyższy zainstalowanej wersji programu MSBuild. |
| NoCache | Zapobiega z pamięci podręcznej komputera lokalnego za pomocą pakietów NuGet. |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie jest określony, używany jest bieżący folder. |
| PackageSaveMode | Określa typy plików, aby zapisać po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`. |
| PackagesDirectory | Taki sam jak `OutputDirectory`. |
| Project2ProjectTimeOut | Limit czasu w sekundach dla rozpoznawania odwołań projektu do projektu. |
| Cykliczne | *(4.0 +)*  Przywraca wszystkie projekty odwołań dla projektów uniwersalnych systemu Windows i .NET Core. Nie ma zastosowania do projektów przy użyciu `packages.config`. |
| RequireConsent | Sprawdza, czy Przywracanie pakietów jest włączona przed pobierania i instalowania pakietów. Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder rozwiązania. Nieprawidłowy gdy trwa przywracanie pakietów dla rozwiązania. |
| Źródło | Określa listę źródła pakietu (jako adresy URL) do użycia na potrzeby przywracania. W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Szczegółowość |> określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="remarks"></a>Uwagi

Polecenie restore wykonuje następujące czynności:

1. Określ tryb działania polecenia restore.
    Typ pliku projectPath | Zachowanie
    | --- | --- |
    Rozwiązania (folder) | Wyszukuje NuGet `.sln` pliku i korzysta z jeśli je znaleziono; w przeciwnym razie zwraca błąd. `(SolutionDir)\.nuget`jest używana jako folder początkowy.
    `.sln`plik | Przywracanie pakietów zidentyfikowane przez rozwiązanie; Zwraca błąd, jeśli `-SolutionDirectory` jest używany. `$(SolutionDir)\.nuget`jest używana jako folder początkowy.
    `packages.config`, `project.json`, lub plik projektu | Przywróć pakiety wymienione w pliku rozwiązania i instalowanie zależności.
    Innego typu pliku | Plik zakłada się, że `.sln` plik jako powyżej; Jeśli nie jest to rozwiązanie zapewnia NuGet błąd.
    (nie określono projectPath) | -NuGet wyszukuje pliki rozwiązania w bieżącym folderze. Jeśli zostanie znaleziony jeden plik, że jeden służy do przywracania pakietów; w przypadku znalezienia wielu rozwiązań NuGet zawiera błąd.
    |— Jeśli nie ma żadnych plików rozwiązania, NuGet szuka `packages.config` lub `project.json` i użyty pod kątem przywracania pakietów.
    |— Jeśli plik rozwiązania nie `packages.config`, lub `project.json` zostanie znaleziony, NuGet zawiera błąd.

1. Określ folder pakietów przy użyciu następującej kolejności priorytet (NuGet zwraca błąd, jeśli żadnego z tych folderów nie są znaleziono):

    - `%userprofile%\.nuget\packages` Wartość w `project.json`.
    - Folder określony za pomocą `-PackagesDirectory`.
    - `repositoryPath` Vale w`Nuget.Config`
    - Folder określony za pomocą`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. Trwa przywracanie pakietów dla rozwiązania, NuGet wykonuje następujące czynności:
    - Ładuje plik rozwiązania.
    - Przywraca poziomu pakietów rozwiązania na liście `$(SolutionDir)\.nuget\packages.config` do `packages` folderu.
    - Przywracanie pakietów na liście `$(ProjectDir)\packages.config` do `packages` folderu. Dla każdego pakietu określony Przywracanie pakietu równolegle, chyba że `-DisableParallelProcessing` jest określona.

## <a name="examples"></a>Przykłady

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
